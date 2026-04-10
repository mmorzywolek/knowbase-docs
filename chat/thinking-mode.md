---
description: Deep multi-step analysis for complex questions
---

# Thinking Mode

## What is Thinking Mode?

Thinking Mode is an advanced chat mode that uses multi-step reasoning to answer complex questions. Instead of a single search, it:

1. Analyzes your question and breaks it into sub-queries
2. Searches your documents multiple times from different angles
3. Assesses confidence and searches again if needed
4. Synthesizes a comprehensive answer

## When to use it

- Questions that span multiple documents or sections
- Analysis and comparison tasks
- Questions where a quick search might miss important context

<!-- screenshot: thinking-mode-toggle -->

## How to enable it

Click the **mode selector** in the chat input and choose **Thinking Mode**. You'll see the reasoning steps as it works:

- Analyzing your question...
- Searching for relevant information...
- Found X relevant passages...
- Assessing confidence...
- Synthesizing answer...

<!-- screenshot: thinking-mode-steps-visible -->

## Fast Mode vs Thinking Mode

| Feature         | Fast Mode              | Thinking Mode          |
| --------------- | ---------------------- | ---------------------- |
| Speed           | Instant                | 5-15 seconds           |
| Search depth    | Single pass            | Multi-iteration        |
| Best for        | Quick lookups          | Complex analysis       |
| Reasoning       | Hidden                 | Visible steps          |

{% hint style="info" %}
**Plan requirement:** Thinking Mode is available on Pro and Team plans.
{% endhint %}
