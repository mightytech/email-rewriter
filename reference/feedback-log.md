# Feedback Log

Accepted items from external feedback, waiting for implementation. Each entry captures
what was accepted, why, and where to find the full context.

The feedback log is the sibling of the friction log:
- **Friction log** — things *you* noticed while working
- **Feedback log** — things *others* noticed that you agreed with

Both feed into `/maintain`. Both are queues of actionable items.

---

## How to Use This Log

**When items are added:**
- After triaging feedback (via `/check-feedback` or any intake mechanism), accepted
  items are deposited here with their verdict rationale and a reference to the source.

**When items are resolved:**
- During `/maintain` sessions, the maintainer reviews pending items and implements them.
  Resolved entries are moved to `feedback-log-archive.md`.

**At session start:**
- `/maintain` checks this log alongside the friction log to surface what's waiting.

---

## Entry Format

```markdown
### [DATE] — [Brief description of the accepted item]

**Source:** [Link to GitHub Issue or intake item]
**Verdict:** [Accept / Adapt — and the reasoning]
**Status:** pending | in-progress | resolved

**What to do:**
[Concrete description of the change needed]

**Why it was accepted:**
[The rationale from triage — why this matters, what it improves]

**Resolved:** [DATE] — [brief description of what was changed and where]
```

Not every entry needs all fields. The essentials are: Source, What to do, Why it was
accepted, Status.

---

## Entries

*Entries are added chronologically, newest first.*

### 2026-02-18 — Framework convention update applied

**Source:** NLA Framework maintainer (direct deposit — no GitHub repo for this project)
**Verdict:** Informational — changes already applied, review recommended
**Status:** pending

**What happened:**

The framework removed its scaffold directory and established intent files as the single source of truth for project generation. As part of this transition, this project was manually updated from the framework side to align with current conventions. Changes were applied without the email rewriter's own AI context loaded.

**Changes made:**

- **Skill wrappers added:** `/validate`, `/preferences`, `/install`, `/update` (thin wrappers delegating to framework core)
- **Startup modified:** Added `disable-model-invocation: true` frontmatter (prevents spontaneous skill invocation; behavior unchanged)
- **Reference files created:** `feedback-log.md` (this file), `feedback-log-archive.md`, `installed-packages.md`
- **Config infrastructure created:** `app/config-spec.md` (configurable areas: tone suggestions, output style, TK notes, framework path, tracing), `config.md` (starter config), `config/.gitkeep`, `.gitignore`
- **CLAUDE.md updated:** Added Configuration section, expanded skills table, updated key files table

**What to review with project context:**

- **`app/config-spec.md` is the most important item to review.** It defines what users can configure — tone suggestion count, output style, TK note verbosity, tracing. This was written from the framework side without reading the full app docs. The email rewriter's own AI should read it against `app/overview.md`, `app/voice-and-values.md`, and the rewrite skill to confirm the configurable areas actually make sense for how this app works.
- **CLAUDE.md** — The Configuration section and expanded skills table should read naturally in context.
- **installed-packages.md** — Confirm the convention update entry is accurate.

**New capabilities:** `/install` and `/update` are now available. Future framework convention changes can be pulled via `/update` from within this project.

---

*This log is populated by `/check-feedback` (or any external feedback tool) and consumed
by `/maintain`. Resolved entries are moved to `feedback-log-archive.md`.*
