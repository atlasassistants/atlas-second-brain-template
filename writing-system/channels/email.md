---
title: "Channel: Email"
type: note
tags:
  - writing-system
created: 2026-04-29
updated: 2026-04-29
---

# Channel: Email

> **Status:** v1. Format rules for emails sent via the list (Beehiiv or wherever the list lives). Voice, audience, kill list are loaded separately.

---

## Email skeleton

Compress for short emails, expand for long. Never invert the order.

1. **Subject line.** ≤ 50 characters ideal. Lowercase or sentence case. Never title case. Sounds like a private message between operators.
2. **Preview text.** 40–90 characters. Continues or contrasts the subject. Never wasted on *"View in browser."*
3. **Opening hook.** 1–3 sentences. Drops the reader in. See `engine/hooks.md`.
4. **Body.** One core argument. Build with receipts. Pick one framework from `engine/frameworks.md`.
5. **Pullback.** 1–2 lines at the close that reframe what the tactic means. Compressed version of the philosophical pullback in `voice.md`.
6. **Single CTA.** From `engine/cta-patterns.md`. Direct reply by default.
7. **Sign-off.** `Your Pal,` newline `{{VAULT_OWNER_SHORT_NAME}}`
8. **P.S.** Direct reply ask. Specific question.
9. **P.P.S.** *(optional)* Tactical add-on. Often: how to introduce this to a team, executive, or coach.

---

## Subject line patterns (for email specifically)

Hook formulas that work best in email subject lines (see `engine/hooks.md` for the full library):

- Authority-moment simulation
- Specific receipt
- Contrast
- Curiosity question

Patterns that work less well in email subjects: behind-the-scenes (better for LinkedIn / long-form), replacement (better for X short).

**Subject line rules:**
- Lowercase preferred unless capitalizing for a coined term (Maker Day, AI Operator, Bottleneck Builder).
- Never start with *"New:"* / *"Update:"* / *"This week:"* — feels like a generic newsletter blast.
- Never use *"Don't miss…"* / *"Last chance…"* / *"Limited time…"* — see `kill-list.md`.
- Specific over clever. Beats title-case marketing copy 9 times out of 10.

---

## Length defaults

| Type | Word count | Notes |
|---|---|---|
| Promotional broadcast | 200–450 | Single argument. One CTA. |
| Welcome sequence email | 150–300 | Tighter. Each email earns the next click. |
| Re-engagement | 100–250 | Shortest. Specific receipt + soft conditional CTA. |
| Long-form / story-led promo | 700–1200 | Use sparingly. Earn the length with a real story. |

When in doubt, shorter wins. The reader's inbox is the bottleneck, not their attention span.

---

## Email-specific format rules

- Plain text feel even when designed. No fancy templates that look like marketing spam.
- Minimal images. If used, screenshots of real things (a calendar, a dashboard, a Slack thread) beat stock graphics.
- No tracking pixels visible to the reader. No "you are receiving this because…" preamble at the top (move legal footer to bottom).
- One link, max two. More than two competes with the CTA.
- Sign-off and P.S. always rendered as separate paragraphs, not run-on.

---

## Examples: in-voice vs. out-of-voice

### Subject
- **OUT:** *"{{VAULT_OWNER_SHORT_NAME}}'s Business Helps Founders Reclaim Their Time"*
- **IN:** *"if your coach has been telling you to hire an EA"*

### Opening
- **OUT:** *"In today's fast-paced business world, founders are constantly battling for their time…"*
- **IN:** *"You've tried Notion. You've tried EOS. You've tried 'just one more push' on time-blocking. None of it stuck. There's a reason. It's not you."*

### Pullback close
- **OUT:** *"Take your business to the next level. Book a call today!"*
- **IN:** *"What you actually need isn't another system. It's permission to stop running the system yourself. The kind of leader you already are doesn't need to do this part anymore."*
