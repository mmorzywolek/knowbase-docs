---
description: Upload a document to Knowbase for processing and AI-powered querying.
---

# Upload File

## `POST /api/v1/files`

Upload a file to your library. The file will be automatically processed for AI-powered search and chat.

**Supported types:** PDF, DOCX, DOC, TXT, MD, PPTX, PPT, and audio/video files. **Max size:** 100 MB.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |

### Request Body (multipart/form-data)

| Name   | Type | Description         |
| ------ | ---- | ------------------- |
| file\* | file | The file to upload  |

### Responses

{% tabs %}
{% tab title="200: OK" %}
```json
{
  "message": "File uploaded successfully",
  "file_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "status": "processing"
}
```
{% endtab %}

{% tab title="400: Bad Request" %}
```json
{
  "error": {
    "code": "QUOTA_EXCEEDED",
    "message": "Upload limit reached (500). Upgrade your plan for more uploads."
  }
}
```
{% endtab %}

{% tab title="401: Unauthorized" %}
```json
{
  "error": {
    "code": "INVALID_TOKEN",
    "message": "Invalid API token"
  }
}
```
{% endtab %}

{% tab title="429: Too Many Requests" %}
```json
{
  "error": {
    "code": "RATE_LIMIT",
    "message": "Rate limit exceeded (per minute)"
  }
}
```
{% endtab %}
{% endtabs %}

### Examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "https://api.knowbase.ai/api/v1/files"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}
files = {"file": ("document.pdf", open("document.pdf", "rb"), "application/pdf")}

response = requests.post(url, headers=headers, files=files)
print(response.json())
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const form = new FormData();
form.append("file", fs.createReadStream("document.pdf"));

const response = await fetch("https://api.knowbase.ai/api/v1/files", {
  method: "POST",
  headers: { Authorization: "Bearer YOUR_API_TOKEN" },
  body: form,
});
const data = await response.json();
console.log(data.file_id);
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X POST https://api.knowbase.ai/api/v1/files \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -F "file=@document.pdf"
```
{% endtab %}
{% endtabs %}
