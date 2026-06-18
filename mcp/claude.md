---
description: Connect Knowbase to Claude (Claude Desktop and claude.ai)
---

# Claude

Knowbase works as a custom remote connector in Claude — on **claude.ai** and **Claude Desktop**.

{% hint style="info" %}
Custom connectors are available on Claude's Free, Pro, Max, Team, and Enterprise plans (Free users can add one connector). The feature is currently in beta.
{% endhint %}

## Pro and Max plans

1. In Claude, go to **Customize > Connectors**.
2. Click **"+"**, then **Add custom connector**.
3. Enter the Knowbase MCP server URL:

   ```
   https://mcp.knowbase.ai/mcp
   ```
4. Click **Add**.
5. Click **Connect** on the Knowbase connector. A window opens — sign in with your Knowbase account and click **Allow** on the consent screen.

<!-- screenshot: claude-add-connector -->

## Team and Enterprise plans

An organization **Owner** adds the connector first:

1. Go to **Organization settings > Connectors**.
2. Click **Add**, hover over **Custom**, then select **Web**.
3. Enter the server URL `https://mcp.knowbase.ai/mcp` and click **Add**.

**Members** then connect:

1. Go to **Customize > Connectors**.
2. Find the **Knowbase** connector (marked "Custom") and click **Connect** to sign in.

## Using it in a chat

Enable the connector per conversation: click the **"+"** in the lower-left of the chat box, choose **Connectors**, and toggle **Knowbase** on. Then ask something like *"Search my Knowbase library for …"*.

<!-- screenshot: claude-enable-in-chat -->
