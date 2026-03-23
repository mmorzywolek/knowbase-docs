---
description: Real-time streaming chat responses via Server-Sent Events (SSE).
---

# Chat Streaming (SSE)

## `POST /api/v1/chat/stream`

Same as `/chat` but returns a **Server-Sent Events** stream for real-time token-by-token output. The request body is identical to the [Chat](chat.md) endpoint.

### SSE Events

| Event      | Description                     | Data format                                          |
| ---------- | ------------------------------- | ---------------------------------------------------- |
| `sources`  | Source citations (sent first)   | `{"sources": [...], "documentType": "pdf"}`          |
| `token`    | Incremental text token          | `{"t": "word "}`                                     |
| `thinking` | Thinking mode progress          | `{"step": "searching", ...}`                         |
| `done`     | Full response complete          | `{"full_text": "...", "conversation_id": "..."}`     |
| `error`    | Error occurred                  | `{"error": {"code": "...", "message": "..."}}`       |

### Example: Python

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

event_type = None
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

### Example: JavaScript

```javascript
const response = await fetch("https://api.knowbase.ai/api/v1/chat/stream", {
  method: "POST",
  headers: {
    Authorization: "Bearer YOUR_API_TOKEN",
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    question: "What are the key takeaways?",
    file_ids: ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"],
  }),
});

const reader = response.body.getReader();
const decoder = new TextDecoder();
let eventType = null;

while (true) {
  const { done, value } = await reader.read();
  if (done) break;

  const text = decoder.decode(value);
  for (const line of text.split("\n")) {
    if (line.startsWith("event: ")) {
      eventType = line.slice(7);
    } else if (line.startsWith("data: ")) {
      const data = JSON.parse(line.slice(6));
      if (eventType === "token") {
        process.stdout.write(data.t);
      } else if (eventType === "done") {
        console.log("\nConversation:", data.conversation_id);
      }
    }
  }
}
```
