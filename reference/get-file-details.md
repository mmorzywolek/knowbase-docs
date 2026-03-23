---
description: Get details and processing status for a specific file.
---

# Get File Details

## `GET /api/v1/files/{file_id}`

Returns details and processing status for a specific file.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |

### Path Parameters

| Name      | Type   | Description           |
| --------- | ------ | --------------------- |
| file\_id\* | string | The UUID of the file  |

### Response (200: OK)

```json
{
  "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "filename": "report.pdf",
  "type": "pdf",
  "status": "success",
  "file_size": 1048576,
  "created_at": "2025-03-15",
  "summary": "This report covers Q4 financial results...",
  "errors": null
}
```

### Error (404: Not Found)

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

response = requests.get(url, headers=headers)
print(response.json())
```
