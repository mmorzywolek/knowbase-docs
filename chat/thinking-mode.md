---
description: An AI research agent that works through your library step by step
---

# Thinking Mode

## What is Thinking Mode?

Thinking Mode turns chat into a **research agent**. Instead of answering from a single search, it works through your library the way a careful researcher would — and you watch it happen live:

1. It analyzes your question and plans an approach
2. It searches your documents — and refines its queries based on what comes back
3. When semantic search isn't enough, it looks for **exact matches** (names, numbers, quotes) or **reads entire documents**
4. It can browse your library by filename to locate a document you described
5. When it has solid evidence, it writes the answer with precise citations

The number of steps adapts to the question: a simple lookup finishes in seconds, while a hard cross-document question gets several rounds of research.

## Watch it think

While it works, a live panel shows every step — its reasoning, the exact searches it runs, and what it found:

- *Analyzing your question…*
- *Searching: "brand growth penetration"*
- *Exact match: "09.09.2025"*
- *Reading a full document…*
- *Reviewing 31 passages…*
- *Writing your answer…*

When the answer starts, the panel collapses to a single line — **"Thought for 45s"** — and you can click it anytime to review the full reasoning trail.

<!-- screenshot: thinking-mode-panel -->

## Works across languages

Thinking Mode searches in the language of your **documents**, not just the language of your question. Ask in German about a Ukrainian document (or in English about a Polish one) and it will reformulate its searches in the right language to find the answer.

## Precise citations

Answers cite sources inline with `[N]` markers. Clicking a citation navigates to the exact place the evidence came from — the PDF page, or the exact timestamp in an audio/video recording, which starts playing from that moment.

## Reply to a fragment

Select any part of an answer and click **Reply** — the fragment attaches to your next message as a quote, so the assistant knows exactly which part you're asking about.

<!-- screenshot: select-to-reply -->

## When to use it

- Questions spanning multiple documents or languages
- "Summarize document X" — it reads the whole document, not just fragments
- Finding exact facts: dates, names, figures, specific quotes
- Analysis and comparison tasks where a quick search would miss context

## How to enable it

Click the **mode selector** in the chat input and choose **Thinking Mode**.

<!-- screenshot: thinking-mode-toggle -->

## Fast Mode vs Thinking Mode

| Feature         | Fast Mode              | Thinking Mode                    |
| --------------- | ---------------------- | -------------------------------- |
| Speed           | Instant                | Seconds to a few minutes — adapts to the question |
| Search depth    | Single pass            | Iterative: search, refine, exact-match, read full documents |
| Languages       | Question language      | Searches in your documents' languages |
| Reasoning       | Hidden                 | Live step-by-step panel, reviewable afterwards |
| Best for        | Quick lookups          | Deep research, summaries, hard questions |

{% hint style="info" %}
**Plan requirement:** Thinking Mode is available on Pro and Team plans.
{% endhint %}

{% hint style="info" %}
Thinking Mode answers only from your library. If your documents don't cover a topic, it says so and points to the closest related material — it won't improvise an answer from general knowledge.
{% endhint %}
