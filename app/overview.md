# System Overview

This document describes what this NLA does and how its pieces fit together. For what NLAs are and the principles behind them, see [nla-foundations.md](../nla-framework/core/nla-foundations.md).

---

## What This NLA Does

This system rewrites rough or poorly-toned emails into polished, sendable messages. It reads the original email, analyzes the context and recipient, suggests 3-4 appropriate tones, and rewrites the email in the user's chosen tone.

| Task | Purpose | Trigger |
|------|---------|---------|
| **Rewrite Email** | Analyze a rough email, suggest tones, rewrite in chosen tone | User provides an email to rewrite |

### Rewrite Email

The primary NLA task. Takes a raw email and:
- Reads the email to understand intent, recipient, and emotional register
- Suggests 3-4 context-appropriate tones via `AskUserQuestion`
- Rewrites the email in the user's selected tone
- Preserves all facts, dates, names, and action items
- Outputs plain text ready to paste into a mail client

**Source:** `rewrite-email.md`

### How It Connects

```
                    ┌─────────────────┐
                    │  Shared Context │
                    │  - Voice/Values │
                    │  - Patterns     │
                    │  - Output Spec  │
                    └────────┬────────┘
                             │
                    ┌────────┴────────┐
                    │  Rewrite Email  │
                    │                 │
                    │  1. Analyze     │
                    │  2. Suggest     │
                    │     tones       │
                    │  3. Rewrite     │
                    └────────┬────────┘
                             │
                    ┌────────┴────────┐
                    │   Sendable      │
                    │   Email         │
                    └─────────────────┘
```

The task reads shared context (voice, patterns, output spec) and applies it to rewrite emails. The voice file governs the system's own communication style; the output tone is selected dynamically by the user for each email.

### Invocation via Skills

Each task has an explicit entry point — a Claude Code skill:

| Skill | Purpose |
|-------|---------|
| `/startup` | Load foundational context at session start |
| `/rewrite-email` | Analyze a rough email, suggest tones, rewrite in chosen tone |
| `/friction-log` | Log observations to the friction log from any context |
| `/maintain` | Edit the NLA system itself |
| `/plan` | Planning mode for new tasks or major changes |

Skills live in `.claude/skills/` and load their context on demand — `CLAUDE.md` provides the runtime identity, and each skill pulls in the specific docs it needs. `/startup` can also be re-run mid-session to reload foundational context after a long conversation.

### The Improvement Pipeline

The system improves through the friction log:

```
Observation from any context → /friction-log captures it → Friction Log → /maintain implements
```

`/friction-log` captures observations from any context — during email rewriting, maintenance, or casual conversation. Entries accumulate in the friction log, where patterns emerge over time. `/maintain` processes them into doc changes. Resolved entries are archived to `friction-log-archive.md`.

This separation exists because capturing observations and editing system docs are different tasks with different guardrails. The friction log is the handoff contract between them.

---

## For Humans

**To change AI behavior:**
- Identify which document governs that behavior
- Edit the document
- The change takes effect immediately (next run)

**To debug unexpected output:**
- Check which documents the AI read
- Look for ambiguity or missing guidance
- Add clarification or examples

**To add a new task:**
1. Create a new file in `app/` (e.g., `app/my-new-task.md`)
2. Follow the structure of existing task docs
3. Create a skill in `.claude/skills/my-new-task/SKILL.md`
4. Add it to the skills table in this overview and in CLAUDE.md
5. The new task inherits all shared context

---

## Document Hierarchy

```
app/
├── overview.md                      ← This file
│
├── shared/
│   ├── voice-and-values.md          ← System tone and editorial identity
│   ├── common-patterns.md           ← Tone suggestion patterns, text cleanup
│   └── output-spec.md               ← Output format (plain text email)
│
└── rewrite-email.md                 ← Email rewriting task

../nla-framework/core/
├── nla-foundations.md               ← What NLAs are (framework)
└── skills/                          ← Skill logic (framework)

reference/
├── design-rationale.md              ← Why the system is built this way
├── friction-log.md                  ← Learning journal (active entries)
├── friction-log-archive.md          ← Resolved entries (searchable history)
├── system-status.md                 ← Current state snapshot
└── sessions/                        ← Maintenance session archives
```

---

## Document Index

### Shared Context
- [Voice and Values](shared/voice-and-values.md) — System tone, principles, editorial identity
- [Common Patterns](shared/common-patterns.md) — Tone suggestion patterns and text cleanup
- [Output Spec](shared/output-spec.md) — Output format details (plain text email)

### Tasks
- [Rewrite Email](rewrite-email.md) — Analyze, suggest tones, rewrite in chosen tone

### Reference
- [Design Rationale](../reference/design-rationale.md) — Why the system is built the way it is
- [Friction Log](../reference/friction-log.md) — Running log of issues and improvements
- [System Status](../reference/system-status.md) — Current state snapshot

---

## Getting Started

### First-Time Setup

1. Read [nla-foundations.md](../nla-framework/core/nla-foundations.md) — understand NLA concepts
2. Read this overview
3. Read shared context documents
4. Read the task document for your work

### Rewriting an Email

1. Start Claude Code and run `/startup`
2. Run `/rewrite-email`
3. Paste a rough email (and optionally mention the recipient)
4. Pick a tone from the suggestions (or describe your own)
5. Get the rewritten email, ready to send

---

*This is a living document. As the NLA system evolves, update this overview to reflect the current state.*
