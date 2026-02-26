# Email Rewriter

A Natural Language Application that rewrites rough emails in a user-selected tone, built on the [NLA Framework](../nla-framework/).

Paste a rough email, get 3-4 context-appropriate tone suggestions, pick one (or describe your own), and get a polished email ready to send.

---

## Prerequisites

**NLA Framework** must be available at `../nla-framework/` (sibling directory to this project).

```bash
# If you haven't cloned it yet:
git clone <framework-repo-url> ../nla-framework
```

**Claude Code** must be installed. This project runs inside Claude Code sessions.

---

## Quick Start

1. Start Claude Code in this directory
2. Run `/startup` to load foundational context
3. Run `/rewrite-email` and paste a rough email
4. Pick a tone from the suggestions (or choose "Other" to describe your own)
5. Get the rewritten email, ready to paste into your mail client
6. Notice something that could be better? Run `/friction-log` to capture it

---

## What's Inside

```
├── CLAUDE.md                        # Runtime identity and configuration
├── app/                             # The application (LLM reads and executes)
│   ├── overview.md                  # What this NLA does, how pieces connect
│   ├── shared/
│   │   ├── voice-and-values.md      # System tone and editorial identity
│   │   ├── common-patterns.md       # Tone suggestion patterns, text cleanup
│   │   └── output-spec.md           # Output format (plain text email)
│   └── rewrite-email.md             # Email rewriting task
├── reference/                       # Maintenance records (not loaded at runtime)
│   ├── design-rationale.md          # Why the system is built this way
│   ├── friction-log.md              # Learning journal (active entries)
│   ├── friction-log-archive.md      # Resolved entries
│   ├── system-status.md             # Current state snapshot
│   └── sessions/                    # Maintenance session archives
├── .claude/skills/                  # Skill entry points
│   ├── startup/                     # Framework wrapper
│   ├── maintain/                    # Framework wrapper
│   ├── friction-log/                # Framework wrapper
│   ├── plan/                        # Framework wrapper
│   └── rewrite-email/               # Domain skill
└── lib/                             # Traditional code helpers
```

---

## How It Works

1. You paste a rough email (and optionally mention who it's going to)
2. The LLM reads the email and analyzes the context — recipient, purpose, emotional register, stakes
3. It suggests 3-4 tones tailored to *this specific email* (not a generic menu)
4. You pick one, or describe exactly what you want
5. The LLM rewrites the email, preserving all facts and action items, and outputs plain text ready to send

---

## The Improvement Loop

```
Observe something → /friction-log captures it → Friction log stores it → /maintain implements changes
```

1. Use the rewriter normally
2. Notice something that could be better (tone suggestions, output quality, missed pattern)
3. Run `/friction-log` to record the observation
4. When ready, run `/maintain` to process accumulated observations into doc changes
5. The docs improve, and the rewriter improves with them

---

## Adding Tasks

To add a new task beyond email rewriting:

1. Create `app/my-task.md` following the structure of `rewrite-email.md`
2. Create `.claude/skills/my-task/SKILL.md` as a skill entry point
3. Add the skill to the tables in `CLAUDE.md` and `app/overview.md`
4. Update `reference/system-status.md`

The new task automatically inherits shared context (voice, patterns, output spec).

---

## Framework Updates

```bash
cd ../nla-framework
git pull
```

Framework updates (skill logic, NLA foundations) take effect immediately through the thin wrapper pattern. Your domain content is never touched.

---

*For more about the NLA Framework, see the [framework README](../nla-framework/README.md).*
