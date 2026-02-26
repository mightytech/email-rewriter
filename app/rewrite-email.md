# Rewrite Email

Take a rough, blunt, or poorly-toned email and rewrite it in a tone the user selects — with you suggesting context-appropriate options.

---

## Purpose

People know what they want to say but not always how to say it. This task bridges the gap: the user provides the raw message and (optionally) context about the recipient, and you suggest tones that fit the situation. The user picks one, and you rewrite the email ready to send.

The key insight: **the right tone depends on the specific email.** A static menu of "professional / casual / formal" doesn't serve anyone well. You read the email, understand the relationship and stakes, and suggest tones that actually make sense for *this* message.

## Input

- **Raw email:** The rough draft, pasted by the user
- **Recipient context (optional):** Who it's going to — "my manager," "a client," "the vendor who messed up our order"
- **Additional instructions (optional):** "Keep it short," "I need to be firm but fair," etc.

## Output

- A rewritten email in the chosen tone, following the output spec
- Ready to paste into a mail client and send

---

## Prerequisites

**Before running this task, read:**

1. **[NLA Foundations](../nla-framework/core/nla-foundations.md)** — Understand what you're doing
2. **[Voice and Values](shared/voice-and-values.md)** — System voice and editorial standards
3. **[Common Patterns](shared/common-patterns.md)** — Tone suggestion patterns and text cleanup
4. **[Output Spec](shared/output-spec.md)** — Output format details

---

## Processing Steps

### Step 1: Read and Understand

Read the entire raw email before doing anything. Understand:

- **What is the sender trying to communicate?** (request, complaint, update, apology, etc.)
- **Who is the recipient?** Use explicit context if provided; otherwise infer from the email's content and language.
- **What's the emotional register?** Is the sender frustrated, apologetic, excited, neutral?
- **What's at stake?** Routine correspondence, or something career/relationship-affecting?
- **What are the concrete facts?** Names, dates, amounts, deadlines, action items — these survive every rewrite unchanged.

### Step 2: Suggest Tones

Use `AskUserQuestion` to present 3-4 tone options tailored to this specific email. Each option needs:

- **A short label** (2-3 words): "Warm and direct", "Diplomatically firm", "Casual and quick"
- **A description** (1 sentence): How this tone would change the email specifically. Not generic descriptions — show how each tone applies to *this* message.

**Guidelines for tone selection:**

- Make options genuinely distinct. If two options would produce similar rewrites, drop one.
- Always include at least one option close to the email's original register (in case the user just wants cleanup, not a tone shift).
- Consider the recipient. An email to a CEO and an email to a teammate warrant different option sets.
- The automatic "Other" option covers edge cases — the user can always describe exactly what they want.

**Example** (for a frustrated complaint to a vendor):

```
AskUserQuestion:
  question: "How should this email sound?"
  options:
    - label: "Firm but professional"
      description: "States the problem clearly and expects resolution, without anger"
    - label: "Diplomatically escalating"
      description: "Acknowledges the relationship while making clear this needs urgent attention"
    - label: "Direct and blunt"
      description: "Keeps your directness but cleans up the rough edges"
    - label: "Conciliatory"
      description: "Focuses on solving the problem together rather than assigning blame"
```

### Step 3: Rewrite

Once the user selects a tone (or describes their own via "Other"):

1. **Preserve all facts.** Names, dates, numbers, deadlines, action items, references to attachments or prior conversations — all carried over exactly.
2. **Transform the tone.** Rewrite sentences to match the selected tone. This may mean restructuring, softening, sharpening, shortening, or expanding — whatever the tone requires.
3. **Clean up.** Fix run-on sentences, reduce excessive punctuation, normalize capitalization. Apply cleanup patterns from common-patterns.md.
4. **Add appropriate framing.** Greeting and sign-off that match the tone and relationship. Don't add fluff — a "warm" tone doesn't require three sentences of pleasantries.
5. **Keep it concise.** Most emails are too long. Unless the selected tone specifically calls for elaboration, aim shorter than the original.

### Step 4: Deliver

Present the rewritten email following the output spec:

- Plain text, ready to paste
- No commentary wrapping the email (no "Here's your rewritten version:")
- Just the email itself

After the email, add a brief note (one sentence) about any judgment calls you made — things the user might want to adjust. If there are TK notes, explain them.

---

## Judgment Calls

### When the Original Is Already Fine

Sometimes the email just needs minor cleanup, not a full rewrite. If the user's tone is already appropriate for the context, say so — "Your email reads well as-is. I cleaned up [minor issues] but the tone fits the situation." Don't force a rewrite for the sake of having output.

### When Intent Is Ambiguous

If you can't tell whether the sender wants to be firm or conciliatory, apologetic or matter-of-fact — flag it. The tone suggestions should reflect the ambiguity: offer options on both sides.

### When the Email Has Problems Beyond Tone

If the email has structural issues (buries the ask, mixes three topics, rambles), fix them in the rewrite. Tone includes clarity. But note what you changed: "I moved your request to the top so it doesn't get lost."

### When Facts Seem Wrong

Don't correct facts. If a date seems wrong or a name seems misspelled, flag with `TK [VERIFY]` and keep the original. The user knows their context better than you do.

---

*The goal is an email the user can send immediately — or with one small tweak. Fast, accurate, and appropriately toned.*
