# Quick Start

## 1. Get your API token

Your API requests are authenticated using a Bearer token. To obtain your token:

1. Log into [app.knowbase.ai](https://app.knowbase.ai)
2. Go to **Account** > **Manage Account** > **Generate API Key**
3. Copy your API token

You need a **Pro** or **Team** plan to access the API.

### Rate Limits

| Plan | Per Minute | Per Hour | Per Day |
|------|-----------|----------|---------|
| Pro  | 20        | 200      | 2,000   |
| Team | 60        | 600      | 5,000   |

## 2. Upload a file

```python
import requests

url = "https://api.knowbase.ai/api/v1/files"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}
files = {"file": ("report.pdf", open("report.pdf", "rb"), "application/pdf")}

response = requests.post(url, headers=headers, files=files)
data = response.json()
print(data)
# {"message": "File uploaded successfully", "file_id": "abc-123-...", "status": "processing"}
```

## 3. Check file status

Files need processing time (embedding). Poll until status is `success`:

```python
file_id = data["file_id"]
response = requests.get(f"https://api.knowbase.ai/api/v1/files/{file_id}", headers=headers)
print(response.json()["status"])  # "success" when ready
```

## 4. Chat with your documents

```python
import json

response = requests.post(
    "https://api.knowbase.ai/api/v1/chat",
    headers={**headers, "Content-Type": "application/json"},
    json={
        "question": "What are the key findings in this report?",
        "file_ids": [file_id]
    }
)
result = response.json()
print(result["answer"])
print(result["sources"])       # Source citations
print(result["conversation_id"])  # Use for follow-up questions
```

## 5. Follow-up questions

Use the `conversation_id` to ask follow-up questions with context:

```python
response = requests.post(
    "https://api.knowbase.ai/api/v1/chat",
    headers={**headers, "Content-Type": "application/json"},
    json={
        "question": "Can you elaborate on the second point?",
        "file_ids": [file_id],
        "conversation_id": result["conversation_id"]
    }
)
```

## 6. Query your entire library

Omit `file_ids` to search across all your uploaded documents:

```python
response = requests.post(
    "https://api.knowbase.ai/api/v1/chat",
    headers={**headers, "Content-Type": "application/json"},
    json={"question": "What do my documents say about revenue growth?"}
)
```

## 7. Serving multiple users under one account

If you're integrating Knowbase into a product where each of your users has their own chat history, pass a stable `session_id` per user. Same `session_id` continues the same thread; different `session_id`s are fully isolated.

```python
# User A's question
requests.post(f"{BASE}/chat", headers=headers, json={
    "question": "What were the key findings in Q4?",
    "session_id": "usr_42",
})

# User A's follow-up — same session, same thread
requests.post(f"{BASE}/chat", headers=headers, json={
    "question": "Can you elaborate on the second point?",
    "session_id": "usr_42",
})

# User B — fresh, isolated history
requests.post(f"{BASE}/chat", headers=headers, json={
    "question": "Summarize the meeting notes",
    "session_id": "usr_99",
})
```

See [Per-user sessions](chat.md#per-user-sessions) for the full reference.

## Full workflow example

```python
import requests
import time

TOKEN = "YOUR_API_TOKEN"
BASE = "https://api.knowbase.ai/api/v1"
headers = {"Authorization": f"Bearer {TOKEN}"}

# 1. Upload
files = {"file": ("report.pdf", open("report.pdf", "rb"), "application/pdf")}
upload = requests.post(f"{BASE}/files", headers=headers, files=files).json()
file_id = upload["file_id"]
print(f"Uploaded: {file_id}")

# 2. Wait for processing
while True:
    status = requests.get(f"{BASE}/files/{file_id}", headers=headers).json()["status"]
    if status == "success":
        break
    print(f"Processing... ({status})")
    time.sleep(5)

# 3. Chat
answer = requests.post(f"{BASE}/chat", headers=headers,
    json={"question": "Summarize this document", "file_ids": [file_id]}).json()
print(answer["answer"])

# 4. Clean up
requests.delete(f"{BASE}/files/{file_id}", headers=headers)
print("File deleted")
```
