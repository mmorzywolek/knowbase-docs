---
description: Ask questions against your documents with AI-powered answers and source citations.
---

# Chat

## `POST /api/v1/chat`

Ask a question and get an AI-powered answer with source citations. You can query specific files, a collection, or your entire library.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |
| Content-Type\*  | string | `application/json`       |

### Request Body

| Name             | Type    | Required | Description                                                    |
| ---------------- | ------- | -------- | -------------------------------------------------------------- |
| question         | string  | Yes      | Your question                                                  |
| file\_ids        | array   | No       | List of file IDs to query. Omit to search entire library       |
| collection\_id   | string  | No       | Collection ID to query (alternative to file\_ids)              |
| conversation\_id | string  | No       | Continue a previous conversation for follow-up questions       |
| thinking\_mode   | boolean | No       | Enable advanced multi-step reasoning (Pro/Team only)           |

### Query scoping

| Scope              | How                                        |
| ------------------ | ------------------------------------------ |
| **Entire library** | Omit both `file_ids` and `collection_id`   |
| **Specific files**  | Set `file_ids: ["id1", "id2"]`            |
| **A collection**    | Set `collection_id: "collection-uuid"`    |

### Example Request

```json
{
  "question": "What were the key revenue drivers in Q4?",
  "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"],
  "conversation_id": null,
  "thinking_mode": false
}
```

### Response (200: OK)

```json
{
  "answer": "Based on the Q4 report, the key revenue drivers were:\n\n1. **SaaS subscriptions** grew 23% YoY [1]\n2. **Enterprise deals** contributed $4.2M in new ARR [2]\n3. **International expansion** into APAC markets [1]\n\nRecurring revenue now represents 78% of total revenue [2].",
  "sources": [
    {
      "key": "1",
      "filename": "q4-report.pdf",
      "source": "12",
      "content": "SaaS subscription revenue grew 23% year-over-year...",
      "documentType": "pdf"
    },
    {
      "key": "2",
      "filename": "q4-report.pdf",
      "source": "15",
      "content": "Enterprise segment closed $4.2M in new ARR...",
      "documentType": "pdf"
    }
  ],
  "conversation_id": "d4e5f6a7-b8c9-0123-def0-1234567890ab"
}
```

The `sources` array contains numbered references matching the `[1]`, `[2]` citations in the answer. The `source` field indicates the page number (for documents) or timestamp (for audio/video).

### Thinking mode

Set `thinking_mode: true` for complex questions that benefit from multi-step reasoning. The AI will iteratively search, assess confidence, and refine its answer. Available on **Pro** and **Team** plans.

```json
{
  "question": "Compare the financial performance across all quarterly reports",
  "thinking_mode": true
}
```

### Examples

{% tabs %}
{% tab title="Python" %}
```python
import requests

url = "https://api.knowbase.ai/api/v1/chat"
headers = {
    "Authorization": "Bearer YOUR_API_TOKEN",
    "Content-Type": "application/json"
}

response = requests.post(url, headers=headers, json={
    "question": "What are the key findings?",
    "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"]
})

result = response.json()
print(result["answer"])

# Follow-up question
response = requests.post(url, headers=headers, json={
    "question": "Can you go into more detail on point 2?",
    "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"],
    "conversation_id": result["conversation_id"]
})
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X POST https://api.knowbase.ai/api/v1/chat \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "question": "Summarize the main findings",
    "file_ids": ["a1b2c3d4-e5f6-7890-abcd-ef1234567890"]
  }'
```
{% endtab %}
{% endtabs %}
