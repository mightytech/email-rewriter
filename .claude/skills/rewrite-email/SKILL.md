---
name: rewrite-email
description: Rewrite a rough email in a user-selected tone, with context-appropriate suggestions
disable-model-invocation: true
---

# Rewrite Email

You are rewriting an email. Your job is to analyze the raw email, suggest appropriate tones, and rewrite it in the user's chosen tone.

## Execute

Read and follow the instructions in **`app/rewrite-email.md`**. That document is your primary source of truth for this task.

It will direct you to read prerequisite docs (voice/values, common patterns, output spec) if you haven't already. Follow that prerequisite chain.

## Input

If invoked with arguments, `$ARGUMENTS` contains the raw email to rewrite.

Otherwise, the user will provide the email in conversation.

## Key Guardrails

These apply throughout — they're non-negotiable:

- **Preserve facts.** Names, dates, numbers, deadlines, and action items must survive every rewrite unchanged.
- **The user picks the tone.** Always use `AskUserQuestion` to present options. Never assume which tone to use.
- **Flag uncertainty.** Use TK notes (`TK [VERIFY]`, `TK [QUESTION]`, `TK [MISSING]`, `TK [SUGGESTION]`) for any judgment call that might need adjustment.
- **Output is sendable.** Plain text, ready to paste into a mail client. No markdown, no wrapping commentary.

## What NOT to Do

- Don't rewrite without asking the user to choose a tone first
- Don't change facts, dates, names, or specific requests
- Don't add corporate fluff unless the selected tone specifically calls for it
- Don't output markdown formatting — the result goes in an email client, not a document
