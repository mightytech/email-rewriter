# Installed Packages

Packages installed in this NLA, maintained by `/install` and `/update`.

Each entry records what package was installed, when, what state the package was in, and what changes were made. This log is how `/update` knows what's current and what needs changing.

---

## NLA Framework

**Installed:** Pre-convention tracking (original `/create-app` generation)
**Source:** `../nla-framework/`

Original project generated via `/create-app` before the framework had formal package tracking.

### Convention Update — 2026-02-18

**Applied by:** Framework maintainer (manual, from framework side)
**Reason:** Framework removed scaffold directory and established intent files as single source of truth. Existing projects needed alignment with current conventions.

**Skill wrappers added:**
- `.claude/skills/validate/SKILL.md` — thin wrapper delegating to `core/skills/validate.md`
- `.claude/skills/preferences/SKILL.md` — thin wrapper delegating to `core/skills/preferences.md`
- `.claude/skills/install/SKILL.md` — thin wrapper delegating to `core/skills/install.md`
- `.claude/skills/update/SKILL.md` — thin wrapper delegating to `core/skills/update.md`

**Skill wrappers modified:**
- `.claude/skills/startup/SKILL.md` — added `disable-model-invocation: true` frontmatter

**Reference files created:**
- `reference/feedback-log.md` — standard feedback log structure
- `reference/feedback-log-archive.md` — empty archive
- `reference/installed-packages.md` — this file

**Configuration infrastructure created:**
- `app/config-spec.md` — configurable areas: tone suggestions, output style, TK notes, framework path, tracing
- `config.md` — starter config with framework path and TK note verbosity
- `config/.gitkeep` — directory placeholder for contextual config
- `.gitignore` — excludes config.md and config/

**CLAUDE.md updated:**
- Added Configuration section (read config.md at startup, governed by config-spec.md)
- Added `/validate`, `/preferences`, `/install`, `/update` to skills table
- Added `app/config-spec.md` and `config.md` to key files table

**Note:** Config-spec.md was written from the framework side without full app context. The project's own AI should review it against the actual app docs to confirm the configurable areas make sense.

---

<!-- /install and /update maintain this file. Each package gets a section with install
     history and update records. Don't remove old entries — they tell the full story. -->
