# Design Rationale

This document explains WHY this NLA system is built the way it is. It captures the reasoning, trade-offs, and principles that shaped the design.

**Audience:** Future maintainers (human or AI) who need to understand the decisions behind the system before modifying it.

**Purpose:** Prevent well-intentioned "improvements" that break things that work. Provide context that won't be obvious from the docs alone.

---

## Why an NLA?

Email tone is a judgment call. "Is this too blunt?" "Would this come across as passive-aggressive?" "Is this formal enough for a VP?" — these are questions that traditional code handles through rigid templates or keyword matching. An NLA handles them through understanding.

The email rewriter needs to:
- Read an email and grasp its intent, audience, and emotional register
- Suggest tones that fit *this specific email*, not a generic list
- Rewrite while preserving meaning and facts
- Apply judgment about what "professional" or "diplomatic" means in context

These are all "I know it when I see it" requirements — exactly where NLAs excel.

---

## Why This Structure

### The Two Channels

```
app/                    ← Operative channel (LLM reads and executes)
  overview.md
  shared/
  rewrite-email.md

../nla-framework/core/  ← Framework (shared NLA foundations and skills)
  nla-foundations.md
  skills/

reference/              ← Non-executing channel (maintainers read)
  design-rationale.md
  friction-log.md
  system-status.md
  sessions/
```

**Why separate:** The operative channel (`app/`) contains instructions the LLM follows. The reference channel (`reference/`) contains information about the system. Mixing them risks metadata influencing LLM behavior — for example, a friction log entry discussing a weakness could cause the LLM to second-guess correct behavior.

### Dynamic Tone Selection via AskUserQuestion

The system uses Claude Code's `AskUserQuestion` tool to present tone options interactively. This was chosen over simply listing options in text because:

- **It's interactive.** The user clicks an option rather than typing a response.
- **"Other" is built in.** The tool automatically provides an escape hatch for custom input.
- **It's structured.** Each option has a label and description, making the choice clear.
- **It constrains naturally.** 3-4 options is the right number — enough variety without decision paralysis.

The tone suggestions are generated fresh for each email based on context analysis, not pulled from a static menu. The common-patterns doc provides tone families as starting points, but the LLM adapts and invents based on the specific email.

### Plain Text Output

Emails are plain text. The output spec deliberately excludes markdown formatting because the rewritten email goes into a mail client, not a document. This is a conscious constraint — it keeps the output immediately usable.

---

## Key Design Decisions

### Friction Log Not Loaded at Startup

The friction log (`reference/friction-log.md`) is NOT loaded during email rewriting. It's reference material — loaded only by `/maintain` when that skill is invoked.

**Why:** Dual-channel separation. Maintenance data (known gaps, correction patterns) shouldn't influence runtime behavior. Also, allowing friction to accumulate before acting reveals patterns that single entries miss.

### The Improvement Pipeline

The improvement loop uses two skills:

- **`/friction-log`** — Captures observations from any context: during email rewriting, maintenance, or casual conversation. Produces entries in the friction log.
- **`/maintain`** — Processes friction log entries into documentation changes. Editorial, architectural.

**Why separate:** Capturing observations and editing system docs are different tasks with different guardrails. Separating them enables batching (accumulate learnings, then implement in one thoughtful pass) and lets `/maintain` see patterns across multiple observations.

### Judgment Over Rules

The docs explain *why*, not just *what*. "Suggest tones that fit the relationship between sender and recipient" is more useful than "always offer Professional, Casual, and Formal." Purpose enables the LLM to handle edge cases that rules would miss.

---

## Adding Decisions

When you make architectural changes (not just wording fixes), add an entry here documenting:
- What was decided
- Why (including what alternatives were considered)
- What it affects

This prevents future maintainers from re-introducing approaches that already failed or undoing decisions that had good reasons.

---

*This document is updated by the `/maintain` skill when architectural decisions are made.*
