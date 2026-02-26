# Common Patterns

Transformations and patterns shared across all tasks. Starting minimal — as you use the system and run `/friction-log`, patterns will emerge and you'll add them here.

---

## Tone Suggestion Patterns

### Reading the Email

Before suggesting tones, understand the email's context:

- **Who is the recipient?** (boss, client, teammate, vendor, stranger)
- **What is the purpose?** (request, complaint, follow-up, introduction, apology)
- **What is the emotional register?** (frustrated, neutral, enthusiastic, delicate)
- **What's at stake?** (routine, career-affecting, relationship-sensitive)

### Suggesting Tones

Offer 3-4 tones via `AskUserQuestion`. Each should be:

- **Distinct** — Don't offer "professional" and "business-like" as separate options
- **Contextually appropriate** — A complaint to a vendor doesn't need a "casual and fun" option
- **Labeled clearly** — Short label (2-3 words), description that shows how this tone would change the email

### Common Tone Families

These are starting points, not a fixed menu. Mix, adapt, and invent based on context.

| Family | When it fits | Characteristics |
|--------|-------------|-----------------|
| Professional and warm | Most workplace emails | Polished but human, clear and direct |
| Formal and diplomatic | Sensitive situations, senior audiences | Careful phrasing, measured, respectful |
| Casual and friendly | Teammates, informal contexts | Conversational, relaxed, approachable |
| Direct and assertive | Follow-ups, escalations, clear asks | No hedging, action-oriented, firm but fair |
| Empathetic and supportive | Apologies, bad news, sensitive topics | Acknowledges feelings, warm, careful |

---

## Text Cleanup

### Common Issues in Raw Emails

- Excessive exclamation marks (reduce to one where appropriate)
- ALL CAPS sections (rewrite in normal case with appropriate emphasis)
- Run-on sentences (break into clear, shorter sentences)
- Missing greetings or sign-offs (add if the tone calls for it)
- Passive-aggressive phrasing (rewrite to express the actual concern directly)

---

## TK Notes

When uncertain about a decision, flag it rather than guessing.

| Note | When to use |
|------|-------------|
| `TK [VERIFY]` | Judgment call that needs human review |
| `TK [QUESTION]` | Couldn't determine the right approach |
| `TK [MISSING]` | Content is needed (recipient name, context) |
| `TK [SUGGESTION]` | Alternative to consider |

TK notes are temporary — resolve during review, don't leave in sent emails.

---

*These patterns apply across all tasks. As you use the system, add patterns you discover through `/friction-log` and `/maintain`.*
