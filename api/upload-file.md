---
description: Upload a document to Knowbase for processing and AI-powered querying.
---

# Upload File

## Upload a document for processing

`POST` `https://api.knowbase.ai/api/v1/files`

Upload a file to your Knowbase library. The file will be automatically processed (embedded) for AI-powered search and chat. Supported types: PDF, DOCX, DOC, TXT, MD, PPTX, PPT, and audio/video files. Maximum size: 100 MB.

#### Headers

| Name | Type | Description |
|------|------|-------------|
| Authorization* | string | `Bearer YOUR_API_TOKEN` |

#### Request Body

| Name | Type | Description |
|------|------|-------------|
| file* | multipart/form-data | The file to upload |

#### Responses

**200: OK** File uploaded successfully

```json
{
  "message": "File uploaded successfully",
  "file_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "status": "processing"
}
```

**400: Bad Request** Quota exceeded or unsupported file

```json
{
  "error": {
    "code": "QUOTA_EXCEEDED",
    "message": "Upload limit reached (500). Upgrade your plan for more uploads."
  }
}
```

**401: Unauthorized** Invalid or missing token

```json
{
  "error": {
    "code": "INVALID_TOKEN",
    "message": "Invalid API token"
  }
}
```

**429: Too Many Requests** Rate limit exceeded

```json
{
  "error": {
    "code": "RATE_LIMIT",
    "message": "Rate limit exceeded (per minute)"
  }
}
```

### Example

```python
import requests

url = "https://api.knowbase.ai/api/v1/files"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}
files = {"file": ("document.pdf", open("document.pdf", "rb"), "application/pdf")}

response = requests.post(url, headers=headers, files=files)
print(response.json())
```

```javascript
const form = new FormData();
form.append("file", fs.createReadStream("document.pdf"));

const response = await fetch("https://api.knowbase.ai/api/v1/files", {
  method: "POST",
  headers: { "Authorization": "Bearer YOUR_API_TOKEN" },
  body: form
});
const data = await response.json();
console.log(data.file_id);
```

```bash
curl -X POST https://api.knowbase.ai/api/v1/files \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -F "file=@document.pdf"
```
