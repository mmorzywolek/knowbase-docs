---
description: List, view, and delete chat conversations.
---

# Conversations

Conversations are automatically created when you use the `/chat` endpoint. Each conversation has a unique ID and maintains chat history for follow-up questions.

---

## List conversations

`GET` `https://api.knowbase.ai/api/v1/conversations`

Returns all conversations with titles and message counts, ordered by most recent.

#### Query parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| session_id | string | No | Filter to one user's conversations only. See [Filter by session](#filter-by-session). |

#### Response (200: OK)

```json
{
  "conversations": [
    {
      "id": "d4e5f6a7-b8c9-0123-def0-1234567890ab",
      "title": "What were the key revenue drivers...",
      "timestamp": "2025-03-15T14:30:00",
      "message_count": 4
    },
    {
      "id": "e5f6a7b8-c9d0-1234-ef01-234567890abc",
      "title": "Summarize the meeting notes",
      "timestamp": "2025-03-14T10:15:00",
      "message_count": 2
    }
  ]
}
```

### Filter by session

If you serve multiple end users under one API account (see [Per-user sessions](chat.md#per-user-sessions)), pass `?session_id=...` to fetch a single user's conversations only:

```
GET /api/v1/conversations?session_id=usr_42
```

The response only includes conversations whose messages were sent with that `session_id`. Use this to render a single user's chat history in your UI.

---

## Get conversation messages

`GET` `https://api.knowbase.ai/api/v1/conversations/{conversation_id}`

Returns all messages in a conversation in chronological order.

#### Response (200: OK)

```json
{
  "messages": [
    {
      "id": "msg-uuid-1",
      "question": "What were the key revenue drivers in Q4?",
      "answer": "Based on the Q4 report, the key revenue drivers were...",
      "sources": [...],
      "timestamp": "2025-03-15T14:30:00"
    },
    {
      "id": "msg-uuid-2",
      "question": "Can you elaborate on the SaaS growth?",
      "answer": "The SaaS subscription revenue grew 23% YoY...",
      "sources": [...],
      "timestamp": "2025-03-15T14:31:00"
    }
  ]
}
```

---

## Delete a conversation

`DELETE` `https://api.knowbase.ai/api/v1/conversations/{conversation_id}`

Permanently deletes a conversation and all its messages.

#### Response (200: OK)

```json
{
  "deleted": 4
}
```

### Example

```python
import requests

TOKEN = "YOUR_API_TOKEN"
BASE = "https://api.knowbase.ai/api/v1"
headers = {"Authorization": f"Bearer {TOKEN}"}

# List conversations
convos = requests.get(f"{BASE}/conversations", headers=headers).json()
for c in convos["conversations"]:
    print(f"{c['title']} ({c['message_count']} messages)")

# Get messages for a conversation
messages = requests.get(
    f"{BASE}/conversations/{convos['conversations'][0]['id']}", headers=headers
).json()
for msg in messages["messages"]:
    print(f"Q: {msg['question']}")
    print(f"A: {msg['answer'][:100]}...\n")
```
