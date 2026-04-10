---
description: Create and manage collections (groups of files) for organized querying.
---

# Collections

Collections let you group files together for targeted querying. When you chat with a collection, only the files in that collection are searched.

---

## Create a collection

`POST` `https://api.knowbase.ai/api/v1/collections`

#### Headers

| Name | Type | Description |
|------|------|-------------|
| Authorization* | string | `Bearer YOUR_API_TOKEN` |
| Content-Type* | string | `application/json` |

#### Request Body

| Name | Type | Description |
|------|------|-------------|
| name* | string | Name of the collection |
| file_ids* | array | List of file ID strings to include |

```json
{
  "name": "Q4 Reports",
  "file_ids": [
    "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "b2c3d4e5-f6a7-8901-bcde-f12345678901"
  ]
}
```

#### Response (201: Created)

```json
{
  "id": "c3d4e5f6-a7b8-9012-cdef-123456789012",
  "name": "Q4 Reports",
  "created_at": "2025-03-15",
  "files": [
    {"id": "a1b2c3d4-...", "filename": "report.pdf", "type": "pdf", "status": "success"},
    {"id": "b2c3d4e5-...", "filename": "analysis.docx", "type": "word", "status": "success"}
  ]
}
```

---

## List all collections

`GET` `https://api.knowbase.ai/api/v1/collections`

#### Response (200: OK)

```json
{
  "collections": [
    {
      "id": "c3d4e5f6-a7b8-9012-cdef-123456789012",
      "name": "Q4 Reports",
      "created_at": "2025-03-15",
      "files": [
        {"id": "a1b2c3d4-...", "filename": "report.pdf", "type": "pdf", "status": "success"}
      ]
    }
  ]
}
```

---

## Get collection details

`GET` `https://api.knowbase.ai/api/v1/collections/{collection_id}`

Returns the collection with its files.

---

## Delete a collection

`DELETE` `https://api.knowbase.ai/api/v1/collections/{collection_id}`

Deletes the collection. **The files inside are NOT deleted** -- they remain in your library.

#### Response (200: OK)

```json
{
  "message": "Collection deleted successfully"
}
```

---

### Example: Create and query a collection

```python
import requests

TOKEN = "YOUR_API_TOKEN"
BASE = "https://api.knowbase.ai/api/v1"
headers = {"Authorization": f"Bearer {TOKEN}", "Content-Type": "application/json"}

# Create a collection
collection = requests.post(f"{BASE}/collections", headers=headers, json={
    "name": "Research Papers",
    "file_ids": ["file-id-1", "file-id-2", "file-id-3"]
}).json()

# Chat with the collection
answer = requests.post(f"{BASE}/chat", headers=headers, json={
    "question": "What are the common themes across these papers?",
    "collection_id": collection["id"]
}).json()

print(answer["answer"])
```
