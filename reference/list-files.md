---
description: Retrieve all files in your library with their status and metadata.
---

# List Files

## `GET /api/v1/files`

Returns all files in your library with their processing status, size, type, and metadata.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |

### Response (200: OK)

```json
{
  "files": [
    {
      "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "filename": "report.pdf",
      "type": "pdf",
      "status": "success",
      "file_size": 1048576,
      "created_at": "2025-03-15",
      "summary": "This report covers Q4 financial results...",
      "errors": null
    },
    {
      "id": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
      "filename": "meeting.mp3",
      "type": "audio",
      "status": "success",
      "file_size": 5242880,
      "created_at": "2025-03-14",
      "summary": null,
      "errors": null
    }
  ]
}
```

### File status values

| Status                     | Meaning                                    |
| -------------------------- | ------------------------------------------ |
| `success`                  | Ready for querying                         |
| `embed_file_started`       | Currently being processed                  |
| `transcribe_file_started`  | Audio/video being transcribed              |
| `failure`                  | Processing failed (check `errors` field)   |

### Example

```python
import requests

url = "https://api.knowbase.ai/api/v1/files"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}

response = requests.get(url, headers=headers)
for file in response.json()["files"]:
    print(f"{file['filename']} - {file['status']}")
```
