---
name: tokslayer
version: 1.0.0
description: Slays tokens in pasted content before Claude processes them. Targets docs, READMEs, papers, tickets, emails — where clipboard bloat lives.
always: true
---

# Tokslayer

Slay tokens before they reach Claude.

Before responding to ANY message, detect what's in the prompt:

## Pattern 1 — Pasted content + command

When the prompt contains a large block of pasted English text (doc, paper, README, email, Jira ticket, Confluence page, Stack Overflow answer, Slack message) followed by a short command (summarize, explain, fix, analyze, review, what does this mean):

1. **Slay the bloat** in the pasted content:
   - Strip UI chrome — navigation, footers, breadcrumbs, share buttons, metadata that came along for the ride
   - Replace verbose phrases with their shortest equivalent that preserves meaning exactly
   - Use the most common English word that means the same thing — common words = single tokens in cl100k_base
   - Remove filler — words that carry zero information ("aforementioned", "in order to", "is responsible for", "it should be noted that", "at your earliest convenience")
   - Collapse redundant sentences — if two sentences say the same thing, keep one

2. **Leave untouched**: code blocks, stack traces, URLs, file paths, error messages, numbers, proper nouns, technical terms, variable names

3. **Show your work**:
```
ORIGINAL: "<first 60 chars>..." (~N tokens)
OPTIMIZED: "<first 60 chars>..." (~N tokens)
SAVED: ~N tokens (X%)
```

4. Respond to the command using the optimized content only.

## Pattern 2 — Pure typed prompt

When the prompt is something the user typed themselves:

1. Rewrite using the most common English word that means the same thing
2. Remove filler words that carry no meaning
3. Prefer short, high-frequency, whole words — these align with cl100k_base single-token merges
4. Show ORIGINAL / OPTIMIZED / SAVED
5. If already optimal — show SAVED: 0 and respond normally. Never invent savings.

## Hard rules

- Preserve intent exactly — meaning must never change
- Never touch code, stack traces, URLs, file paths, numbers, proper nouns, technical terms
- Never invent savings — if nothing improves, say so
- Same language as the original always
- One short typed prompt that's already direct — leave it alone
