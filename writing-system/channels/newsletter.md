---
title: "Channel: Newsletter"
type: note
tags:
  - writing-system
created: 2026-04-29
updated: 2026-04-30
---

# Channel: Newsletter

> **Status:** v1. Format rules for newsletters sent via the `<list-name>` list(s). Voice, audience, kill list are loaded separately.

---

## Newsletter skeleton (Garry-Tan-style as default)

Garry-Tan-style is the default for newsletters: confessional opening → tactical middle → philosophical close. See `engine/frameworks.md` for the full pattern.

1. **Subject line.** Treat as the hook. ≤ 50 chars. Specific over clever.
2. **Preview text.** 40–90 chars. Extends or contrasts the subject.
3. **Opening hook (confessional).** 1–3 paragraphs. Drop into a specific moment. Real, named subjects, real numbers.
4. **The pivot.** One paragraph naming what the moment revealed.
5. **Tactical middle.** What works, how, what to do. Receipts. Sub-headings okay.
6. **Section-break pullbacks** *(newsletter-specific feature)*. 2–4 sentence philosophical pullbacks at major section breaks. Vary the framing each time.
7. **Philosophical pullback (close).** 1–3 paragraphs that reframe what the tactic means for who the reader becomes.
8. **Sign-off.** `Your Pal,` newline `{{VAULT_OWNER_SHORT_NAME}}`
9. **P.S.** Direct reply ask, specific question.
10. **P.P.S.** *(optional)* Tactical add-on or pointer to related content.

---

## Length defaults

| Type | Word count |
|---|---|
| Standard newsletter | 800–1500 |
| Short take (mid-week) | 300–600 |
| Deep-dive / feature issue | 2000–3500 (use rarely; earn it with a story) |

---

## Section-break pullback pattern (newsletter-specific)

The newsletter format is the one place to do the philosophical pullback at *every* major section break, not just at the close. Keep them tight (2–4 sentences). Vary the angle each time. Don't repeat.

Example (after a tactical section on Maker Day):
> *"What you're really doing on Maker Day isn't shipping a new tool. You're proving, to yourself and to your team, that the bottleneck isn't the work. It's the permission you give yourself to stop being the executor."*

---

## Newsletter-specific format rules

### Skimmability and rhythm

- **Paragraph length: 1–2 sentences default. Maximum 3.** Only use 3 when a thought genuinely needs three beats. Single-sentence paragraphs encouraged for openers, transitions, punchlines, and emotional beats. The single most important formatting rule for this channel.
- **Bold section headers as the primary visual break.** Every major section gets a bold header. No section runs more than 3–5 short paragraphs before the next header. Horizontal rules used sparingly, only for major mode shifts.
- **Headers carry the story.** A reader skimming only the bold headers should get 80% of the message. If they can't, restructure with more headers and shorter paragraphs.
- **Pull quote.** One per newsletter, max. The single most important thesis statement, formatted as bold blockquote. Placed after the problem section or after the framework section, wherever the core insight lands hardest.
- **Italic emphasis.** Reserved for inner monologue, hypothetical quotes, or the hammer line. 1–2 per newsletter max. Sparingly.
- **Bold within paragraphs: rare.** Bold is for headers and labeled bullet items (e.g., *"Your 10%:"*). Avoid bold emphasis on random words inside body prose.
- **Closing format.** Short imperative sentences (2–3 punchy commands). Then a one-sentence forward look ("Next issue, I'll go deeper into…"). Then sign-off, then P.S. Don't pad the close with a section's worth of summary.

### Skimmability test (non-negotiable)

Before output, the draft must pass:

> **Can a reader skim ONLY the bold text (headers + bold labels) and get 80% of the message?**

If no — restructure. More headers, more bold-labeled bullet items, shorter paragraphs. Newsletters work for both readers and skimmers. If only readers can follow it, the rhythm has slipped.

### Other format rules

- Sign-off always *Your Pal, / {{VAULT_OWNER_SHORT_NAME}}*.
- P.S. always asks for direct reply with a specific question.
- Section names are NEVER literal repeats across consecutive issues. *"An Honest Note"* used in two consecutive newsletters reads as template (see `kill-list.md` and `engine/techniques.md` technique #11).
- Single core argument per issue. Don't try to cover three things.
- Long-form X article uses the same skeleton with platform-specific tweaks (see `channels/x-article.md`).

---

## When this skill fires vs. email

This channel is for **recurring content** — newsletters, essays, think-pieces, curated commentary. NOT for promotional emails, launches, or onboarding sequences.

If the task is *"send to the list"* and ambiguous, ask the user: is this content (newsletter) or pitch (email-copy)?

---

## Examples: in-voice vs. out-of-voice

### Subject line
- **OUT:** *"Newsletter — Week 17"*
- **IN:** *"my friend pre-sold a tech stack he hasn't built yet"*

### Opening hook (confessional)
- **OUT:** *"Welcome to this week's edition of the newsletter, where we explore the latest in operational excellence and AI-powered productivity for forward-thinking leaders…"*
- **IN:** *"A friend told me 'my life has changed' two weeks after I taught him to build with AI. That part you've heard. The part you haven't: he's now selling tools he hasn't built yet to his own competitors. They have no idea what's coming."*

### Section-break pullback
- **OUT:** *"In the next section, we'll explore additional benefits of this approach."*
- **IN:** *"What he actually proved isn't that AI is fast. It's that the people who already understand their industry now have a tool that lets them act on what they know without waiting on a stack they can't afford. That's a different kind of advantage than 'AI productivity.'"*

### Philosophical pullback (close)
- **OUT:** *"And it starts with one project. Build something this week!"*
- **IN:** *"What you're actually doing isn't building tools. You're moving the line of what you can decide alone. Every tool you ship is one less conversation you outsource to your dev team, your agency, or the consultant you've been emailing for two weeks. Call it productivity if you want. You and I both know it's a different relationship with what the business needs from you now."*
