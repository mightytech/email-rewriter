# Configuration Spec

This document defines what users of this NLA can configure. The `/preferences` skill reads this to guide the configuration conversation and enforce constraints.

---

## What's Configurable

Users can adjust how the email rewriter behaves without changing the core application docs. The main areas:

### Tone Suggestions

- **Number of suggestions** — How many tone options to present. Default is 3-4 context-appropriate suggestions. Users who want more variety can increase; users who want faster flow can decrease.
- **Include "other" option** — Whether to always include an open-ended "describe your own tone" option alongside the suggestions.

**Defaults:** 3-4 suggestions. Include "other" option.

### Output Style

- **Greeting/closing style** — Whether to include standard greetings and sign-offs, or match whatever the original email had.
- **Length tendency** — Whether to tend toward concise rewrites or preserve the original length.

**Defaults:** Match original greeting/closing pattern. Preserve original length.

### TK Notes

- **Verbose** — Flag every judgment call, even minor ones
- **Standard** — Flag significant uncertainty and fact-preservation concerns
- **Minimal** — Only flag things that could change meaning or lose facts

**Default:** Standard.

### Framework Path

If the NLA Framework is not at the standard sibling location (`../nla-framework/`), users can specify the actual path.

**Default:** `../nla-framework/`

### Tracing

Runtime tracing logs the LLM's decisions during work sessions — which documents it read, what directives it found, what it decided and why. Useful for debugging unexpected behavior.

**Trace level:**

- **Off** — No tracing. Default.
- **Standard** — Log major decisions: tone analysis, rewrite choices, fact preservation checks.
- **Detailed** — Log everything including routine operations and alternatives considered.
- **Custom** — User writes natural language describing exactly what to trace.

**Defaults:** Tracing off.

---

## Constraints

- Fact preservation is not configurable. Names, dates, numbers, deadlines, and action items must always survive rewrites unchanged.
- Tone selection must always be user-driven. The system suggests; the user chooses.
- TK notes can be adjusted in verbosity but cannot be disabled entirely.

---

## Guidance for the Config Conversation

When users aren't sure what to configure, start with output style and tone suggestion count. These have the most visible effect on day-to-day use.

For first-time users, suggest trying the defaults first and coming back to `/preferences` after they've rewritten a few emails.

---

*This spec is maintained by the app developer via `/maintain`. Users interact with config through `/preferences`.*
