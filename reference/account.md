---
description: Check your subscription tier, quotas, and current usage.
---

# Account

## `GET /api/v1/account`

Returns your subscription tier, quota limits, and current usage.

### Headers

| Name            | Type   | Description              |
| --------------- | ------ | ------------------------ |
| Authorization\* | string | `Bearer YOUR_API_TOKEN`  |

### Response (200: OK)

```json
{
  "email": "user@example.com",
  "tier": "Pro",
  "quotas": {
    "queries_limit": 2000,
    "queries_used": 342,
    "uploads_limit": 500,
    "uploads_used": 47,
    "storage_limit": "25.00 GB",
    "storage_used": "1.23 GB",
    "storage_remaining": "23.77 GB"
  }
}
```

### Example

```python
import requests

url = "https://api.knowbase.ai/api/v1/account"
headers = {"Authorization": "Bearer YOUR_API_TOKEN"}

account = requests.get(url, headers=headers).json()

print(f"Plan: {account['tier']}")
print(f"Queries: {account['quotas']['queries_used']}/{account['quotas']['queries_limit']}")
print(f"Storage: {account['quotas']['storage_used']} / {account['quotas']['storage_limit']}")
```
