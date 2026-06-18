---
description: Use Knowbase from Claude, ChatGPT, Perplexity and other AI assistants via MCP
---

# Use Knowbase in AI Assistants (MCP)

Knowbase exposes your document library to external AI assistants through the **Model Context Protocol (MCP)** — an open standard for connecting AI tools to data sources. Once connected, assistants like Claude, ChatGPT, and Perplexity can search and read your library to answer questions, with citations back to your source documents, without you leaving that assistant.

{% hint style="info" %}
**Plan requirement:** MCP access is included with the **Pro** and **Team** plans.
{% endhint %}

## The server URL

Add this remote MCP server URL in your assistant's connector settings:

```
https://mcp.knowbase.ai/mcp
```

You can copy it any time from **Account > MCP** in Knowbase.

<!-- screenshot: account-mcp-page -->

The first time you connect, a window opens where you sign in with your Knowbase account and approve access on a consent screen. Your assistant only ever sees the documents in your own library — never your password.

## What the assistant can do

Connecting adds these tools to your assistant:

| Tool | What it does |
| --- | --- |
| `search_library` | Searches your library and returns the most relevant passages with citations |
| `ask_knowbase` | Asks a question and returns a Knowbase-generated answer with sources |
| `list_documents` | Lists the documents in your library |
| `list_collections` | Lists your collections and their files |

The assistant decides when to call these based on your questions. Try prompts like *"Search my Knowbase library for our refund policy"*.

## Setup guides

- [Claude](claude.md)
- [ChatGPT](chatgpt.md)
- [Perplexity](perplexity.md)

Any assistant that supports remote MCP connectors can use Knowbase — these guides cover the most common ones.
