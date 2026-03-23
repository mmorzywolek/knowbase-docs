---
description: List, view, and delete chat conversations.
---

# Conversations

Conversations are automatically created when you use the `/chat` endpoint. Each conversation maintains chat history for follow-up questions.

## List conversations

### `GET /api/v1/conversations`

Returns all conversations, ordered by most recent.

### Response (200: OK)

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

---

## Get conversation messages

### `GET /api/v1/conversations/{conversation_id}`

Returns all messages in chronological order.

### Response (200: OK)

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

### `DELETE /api/v1/conversations/{conversation_id}`

Permanently deletes a conversation and all its messages.

### Response (200: OK)

```json
{
  "deleted": 4
}
```

---

## Example

```python
import requests

TOKEN = "YOUR_API_TOKEN"
BASE = "https://api.knowbase.ai/api/v1"
headers = {"Authorization": f"Bearer {TOKEN}"}

# List conversations
convos = requests.get(f"{BASE}/conversations", headers=headers).json()
for c in convos["conversations"]:
    print(f"{c['title']} ({c['message_count']} messages)")

# Get messages
messages = requests.get(
    f"{BASE}/conversations/{convos['conversations'][0]['id']}",
    headers=headers
).json()

for msg in messages["messages"]:
    print(f"Q: {msg['question']}")
    print(f"A: {msg['answer'][:100]}...\n")
```
