---
description: Ask questions against your documents with AI-powered answers and source citations.
---

# Chat

The chat endpoint is the core of the Knowbase API. Ask questions about your documents and get AI-powered answers with source citations.

---

## Send a query (non-streaming)

`POST` `https://api.knowbase.ai/api/v1/chat`

#### Headers

| Name | Type | Description |
|------|------|-------------|
| Authorization* | string | `Bearer YOUR_API_TOKEN` |
| Content-Type* | string | `application/json` |

#### Request Body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| question | string | Yes | Your question |
| file_ids | array | No | List of file IDs to query. Omit to search entire library |
| collection_id | string | No | Collection ID to query (alternative to file_ids) |
| conversation_id | string | No | Continue a previous conversation for follow-up questions |
| session_id | string | No | Stable identifier for one of your end users (see [Per-end-user sessions](#per-end-user-sessions)) |
| thinking_mode | boolean | No | Enable advanced multi-step reasoning (Pro/Team only) |

#### Example request

```json
{
  "question": "What were the key revenue drivers in Q4?",
  "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"],
  "conversation_id": null,
  "thinking_mode": false
}
```

#### Response (200: OK)

```json
{
  "answer": "Based on the Q4 report, the key revenue drivers were:\n\n1. **SaaS subscriptions** grew 23% YoY [1]\n2. **Enterprise deals** contributed $4.2M in new ARR [2]\n3. **International expansion** into APAC markets [1]\n\nThe report highlights that recurring revenue now represents 78% of total revenue [2].",
  "sources": [
    {
      "key": "1",
      "filename": "q4-report.pdf",
      "source": "12",
      "content": "SaaS subscription revenue grew 23% year-over-year...",
      "documentType": "pdf"
    },
    {
      "key": "2",
      "filename": "q4-report.pdf",
      "source": "15",
      "content": "Enterprise segment closed $4.2M in new ARR...",
      "documentType": "pdf"
    }
  ],
  "conversation_id": "d4e5f6a7-b8c9-0123-def0-1234567890ab",
  "session_id": null
}
```

The `sources` array contains numbered references matching the `[1]`, `[2]` citations in the answer. The `source` field indicates the page number (for documents) or timestamp (for audio/video).

---

## Send a query (streaming SSE)

`POST` `https://api.knowbase.ai/api/v1/chat/stream`

Same request body as `/chat`, but returns a **Server-Sent Events** stream for real-time token-by-token output.

#### SSE Events

| Event | Description | Data format |
|-------|-------------|-------------|
| `sources` | Source citations (sent first) | `{"sources": [...], "documentType": "pdf"}` |
| `token` | Incremental text token | `{"t": "word "}` |
| `thinking` | Thinking mode progress | `{"step": "searching", ...}` |
| `done` | Full response complete | `{"full_text": "...", "conversation_id": "..."}` |
| `error` | Error occurred | `{"error": {"code": "...", "message": "..."}}` |

#### Example: Streaming in Python

```python
import requests
import json

url = "https://api.knowbase.ai/api/v1/chat/stream"
headers = {
    "Authorization": "Bearer YOUR_API_TOKEN",
    "Content-Type": "application/json"
}
data = {
    "question": "Summarize the main findings",
    "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"]
}

response = requests.post(url, headers=headers, json=data, stream=True)

for line in response.iter_lines():
    line = line.decode("utf-8")
    if line.startswith("event: "):
        event_type = line[7:]
    elif line.startswith("data: "):
        payload = json.loads(line[6:])
        if event_type == "token":
            print(payload["t"], end="", flush=True)
        elif event_type == "sources":
            print(f"\nSources: {len(payload['sources'])} found")
        elif event_type == "done":
            print(f"\n\nDone. Conversation: {payload['conversation_id']}")
```

#### Example: Streaming in JavaScript

```javascript
const response = await fetch("https://api.knowbase.ai/api/v1/chat/stream", {
  method: "POST",
  headers: {
    "Authorization": "Bearer YOUR_API_TOKEN",
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    question: "What are the key takeaways?",
    file_ids: ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"]
  })
});

const reader = response.body.getReader();
const decoder = new TextDecoder();

while (true) {
  const { done, value } = await reader.read();
  if (done) break;

  const text = decoder.decode(value);
  for (const line of text.split("\n")) {
    if (line.startsWith("data: ")) {
      const data = JSON.parse(line.slice(6));
      if (data.t) process.stdout.write(data.t);
    }
  }
}
```

---

## Query scoping

You can control which documents are searched:

| Scope | How |
|-------|-----|
| **Entire library** | Omit both `file_ids` and `collection_id` |
| **Specific files** | Set `file_ids: ["id1", "id2"]` |
| **A collection** | Set `collection_id: "collection-uuid"` |

---

## Thinking mode

Set `thinking_mode: true` for complex questions that benefit from multi-step reasoning. The AI will iteratively search, assess confidence, and refine its answer. Available on Pro and Team plans.

```json
{
  "question": "Compare the financial performance across all quarterly reports",
  "thinking_mode": true
}
```

In streaming mode, you'll receive additional `thinking` events showing the AI's reasoning progress.

---

## Per-user sessions

If you're integrating Knowbase into a product that serves multiple end users, pass a stable `session_id` for each user. Same `session_id` continues the same conversation; different `session_id`s under the same API account are fully isolated — no cross-user history leakage.

You don't need to track Knowbase's `conversation_id` on your side; just send your own user identifier as `session_id` and we'll resolve it to the right thread.

#### Example: two users under one API account

```json
// First call for user "usr_42"
POST /api/v1/chat
{
  "question": "What were the key revenue drivers in Q4?",
  "session_id": "usr_42"
}
// → returns { "answer": "...", "conversation_id": "uuid-A", "session_id": "usr_42" }

// Follow-up for the same user — same conversation continues
POST /api/v1/chat
{
  "question": "Can you elaborate on the SaaS growth?",
  "session_id": "usr_42"
}
// → returns { "answer": "...", "conversation_id": "uuid-A", "session_id": "usr_42" }

// Different user — fresh, isolated history
POST /api/v1/chat
{
  "question": "Summarize the meeting notes",
  "session_id": "usr_99"
}
// → returns { "answer": "...", "conversation_id": "uuid-B", "session_id": "usr_99" }
```

#### Notes

- `session_id` is an opaque string of your choice (max 255 chars). We recommend using your product's stable user identifier.
- If you send both `conversation_id` and `session_id`, `conversation_id` wins (back-compat).
- To list a single user's conversations, see [Listing conversations by session](conversations.md#filter-by-session).
- Quotas and rate limits are enforced **per API account**, not per session. For high-volume integrations, contact us about an Enterprise plan.
