# Output Specification

Defines the output format for rewritten emails.

---

## Format

Output as **plain text** — ready to paste directly into a mail client. No markdown, no HTML, no metadata.

### Structure

```
Subject: [subject line, if applicable]

[Greeting]

[Body paragraphs]

[Sign-off]
[Name placeholder or original name]
```

### What to Include

- **Subject line:** Only if the user provided one, or if the email clearly needs one. Don't invent subjects for reply/forward contexts.
- **Greeting:** Match the tone. "Hi Sarah" for casual, "Dear Ms. Chen" for formal, etc.
- **Body:** The rewritten content. Preserve all facts, requests, and deadlines from the original.
- **Sign-off:** Match the tone. "Best," "Thanks," "Regards," etc. Use the sender's name if provided, otherwise leave a placeholder like `[Your name]`.

### What to Omit

- Markdown formatting (no `**bold**`, no `- bullets`)
- Metadata or commentary (no "Here's your rewritten email:")
- The original email (don't include it for comparison — just deliver the rewrite)

## What Stays from the Original

- All factual content (names, dates, amounts, deadlines)
- Specific requests or action items
- References to attachments or prior conversations
- The sender's actual intent — tone changes, meaning doesn't

---

*The rewritten email should be immediately sendable. If the user needs to make edits, they should be minor tweaks, not structural changes.*
