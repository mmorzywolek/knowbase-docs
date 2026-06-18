---
description: Connect Knowbase to Perplexity as a custom remote connector
---

# Perplexity

Perplexity supports custom remote MCP connectors that pull live data into your conversations and Computer workflows.

{% hint style="info" %}
Custom connectors are available to Perplexity's **Pro**, **Max**, and **Enterprise** subscribers.
{% endhint %}

## Add Knowbase

1. Go to **Settings → Connectors**.
2. Click **Add custom MCP connector** (or **Add connector → Custom**).
3. Enter the Knowbase MCP server URL:

   ```
   https://mcp.knowbase.ai/mcp
   ```
4. Choose **OAuth** authentication, then sign in with your Knowbase account and approve access.

<!-- screenshot: perplexity-add-connector -->

Once connected, Knowbase is available in your conversations and Computer workflows — ask something like *"Search my Knowbase library for …"*.

{% hint style="info" %}
Enterprise administrators can share the connector across the whole organization and control whether members may add their own.
{% endhint %}
