---
description: >-
  Knowbase.ai API lets you upload documents, query them with AI, manage
  collections, and integrate document intelligence into your own applications.
---

# Welcome to Knowbase.ai API

Here you'll find all the documentation you need to get up and running with the Knowbase.ai API.

## Base URL

```
https://api.knowbase.ai/api/v1
```

## Authentication

All API requests require a Bearer token in the `Authorization` header:

```
Authorization: Bearer YOUR_API_TOKEN
```

Generate your API token from **Account Settings** in the [Knowbase.ai](https://app.knowbase.ai) web app, or via the `GET /api/v1/token` endpoint. API access requires a **Pro** or **Team** plan.

## Features

* **File Management** — Upload, list, get details, delete, and retrieve summaries
* **Collections** — Group files into named collections for organized querying
* **Chat (Q\&A)** — Ask questions against your documents with AI-powered answers and source citations
* **Streaming** — Real-time Server-Sent Events (SSE) for chat responses
* **Thinking Mode** — Advanced multi-step reasoning for complex questions (Pro and Team)
* **Conversations** — Persistent chat history with follow-up question support
* **Account Info** — Check your plan, quotas, and usage

## Supported File Types

**Documents:** PDF, DOCX, DOC, TXT, MD, PPTX, PPT

**Audio:** MP3, WAV, M4A, AAC, OGG, FLAC

**Video:** MP4, MOV, WEBM, AVI, MKV

## Plan Limits

|                    | Pro          | Team          |
| ------------------ | ------------ | ------------- |
| **Upload size**    | 100 MB       | 100 MB        |
| **Rate limit**     | 20/min       | 60/min        |
| **Queries/month**  | 2,000        | 5,000         |
| **Storage**        | 25 GB        | 100 GB        |
| **Uploads**        | 500          | Unlimited     |
| **Thinking Mode**  | Yes          | Yes           |

## Error Format

All errors return a consistent JSON structure:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable description"
  }
}
```

**Error codes:** `INVALID_TOKEN`, `EXPIRED_TOKEN`, `FORBIDDEN`, `NOT_FOUND`, `RATE_LIMIT`, `QUOTA_EXCEEDED`, `INVALID_REQUEST`, `FILE_TOO_LARGE`, `UNSUPPORTED_FILE_TYPE`, `FEATURE_GATED`, `INTERNAL_ERROR`

## Interactive Docs

Explore and test all endpoints at:

```
https://api.knowbase.ai/docs
```
