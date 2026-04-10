---
description: Get the AI-generated summary for a file.
---

# Get File Summary

## Get summary by file ID

`GET` `https://api.knowbase.ai/api/v1/files/{file_id}/summary`

Returns the AI-generated summary for a file. If the summary hasn't been generated yet, returns `status: "processing"`.

#### Headers

| Name | Type | Description |
|------|------|-------------|
| Authorization* | string | `Bearer YOUR_API_TOKEN` |

#### Path Parameters

| Name | Type | Description |
|------|------|-------------|
| file_id* | string | The UUID of the file |

#### Responses

**200: OK** Summary available

```json
{
  "file_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "summary": "This document presents the Q4 2024 financial results, highlighting a 15% revenue increase...",
  "status": "ready"
}
```

**200: OK** Summary still processing

```json
{
  "file_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "summary": null,
  "status": "processing"
}
```

### Example

```python
import requests

file_id = "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
url = f"https://api.knowbase.ai/api/v1/files/{file_id}/summary"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}

response = requests.get(url, headers=headers)
data = response.json()
if data["status"] == "ready":
    print(data["summary"])
else:
    print("Summary is still being generated...")
```
