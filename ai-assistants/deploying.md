---
description: Get your assistant's embed code and deploy it
---

# Deploying

## Embed on your website

Copy the embed snippet and paste it into your website's HTML, just before the closing `</body>` tag:

```html
<script src="https://app.knowbase.ai/assets/widget.js"></script>
<script>
  KnowbaseChat.init({ token: 'YOUR_TOKEN' });
</script>
```

<!-- screenshot: deploy-embed-code -->

That's it — the widget will appear on your website.

## Preview

Click **Open demo page** to see your assistant in action before deploying. This opens a test page with the widget loaded.

<!-- screenshot: deploy-preview-button -->

{% hint style="warning" %}
If your assistant is **hidden** (toggled off on the Overview page), it won't appear in the preview or on your website. Make sure it's set to "Visible on website".
{% endhint %}

## Publishing

If you used the setup wizard, click **Publish** on the last step to set your assistant to "Live" status.

## Updating

All configuration changes (behavior, appearance, sources) **apply instantly** to deployed widgets. No need to update the embed code.
