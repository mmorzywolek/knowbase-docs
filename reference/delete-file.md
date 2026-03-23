---
description: Permanently delete a file, its embeddings, and chat history.
---

# Delete File

## `DELETE /api/v1/files/{file_id}`

Permanently deletes a file from your library, including its vector embeddings and associated chat history. This action cannot be undone.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |

### Path Parameters

| Name      | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| file\_id\* | string | The UUID of the file to delete |

### Responses

{% tabs %}
{% tab title="200: OK" %}
```json
{
  "message": "File deleted successfully"
}
```
{% endtab %}

{% tab title="404: Not Found" %}
```json
{
  "error": {
    "code": "NOT_FOUND",
    "message": "File not found"
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

file_id = "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
url = f"https://api.knowbase.ai/api/v1/files/{file_id}"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}

response = requests.delete(url, headers=headers)
print(response.json())
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X DELETE "https://api.knowbase.ai/api/v1/files/a1b2c3d4-e5f6-7890-abcd-ef1234567890" \
  -H "Authorization: Bearer YOUR_API_TOKEN"
```
{% endtab %}
{% endtabs %}
