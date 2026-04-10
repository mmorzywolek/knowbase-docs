---
description: Permanently delete a file, its embeddings, and chat history.
---

# Delete File

## Delete a file by ID

`DELETE` `https://api.knowbase.ai/api/v1/files/{file_id}`

Permanently deletes a file from your library, including its vector embeddings and associated chat history. This action cannot be undone.

#### Headers

| Name | Type | Description |
|------|------|-------------|
| Authorization* | string | `Bearer YOUR_API_TOKEN` |

#### Path Parameters

| Name | Type | Description |
|------|------|-------------|
| file_id* | string | The UUID of the file to delete |

#### Responses

**200: OK**

```json
{
  "message": "File deleted successfully"
}
```

**404: Not Found**

```json
{
  "error": {
    "code": "NOT_FOUND",
    "message": "File not found"
  }
}
```

### Example

```python
import requests

file_id = "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
url = f"https://api.knowbase.ai/api/v1/files/{file_id}"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}

response = requests.delete(url, headers=headers)
print(response.json())
```

```bash
curl -X DELETE https://api.knowbase.ai/api/v1/files/a1b2c3d4-e5f6-7890-abcd-ef1234567890 \
  -H "Authorization: Bearer YOUR_API_TOKEN"
```
