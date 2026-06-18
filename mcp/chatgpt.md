---
description: Connect Knowbase to ChatGPT using Developer Mode
---

# ChatGPT

ChatGPT supports custom remote MCP connectors through **Developer Mode**.

{% hint style="info" %}
Developer Mode is available on ChatGPT's Pro, Plus, Business, Enterprise, and Education plans (web only).
{% endhint %}

## Enable Developer Mode

1. Go to **Settings → Apps** (Connectors).
2. Open **Advanced settings → Developer mode** and toggle it on.

<!-- screenshot: chatgpt-developer-mode -->

## Add Knowbase

1. In **Apps** settings, click **Create app** (next to Advanced settings — only visible once Developer Mode is on).
2. Enter the Knowbase MCP server URL:

   ```
   https://mcp.knowbase.ai/mcp
   ```
3. Choose **OAuth** authentication, then sign in with your Knowbase account and approve access.
4. Knowbase now appears as a Developer Mode tool in conversations.

## Using it in a chat

Open the **"+" menu → Developer Mode**, select **Knowbase**, then prompt explicitly, for example: *"Use the Knowbase app's search_library to find …"*.

{% hint style="warning" %}
Developer Mode is powerful — ChatGPT asks you to confirm before any write action. Knowbase's tools are read-only (search and list), so they only ever read from your library.
{% endhint %}
