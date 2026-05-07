---
title: Drafting feedback (living)
type: note
tags:
  - writing-system
created: {{DATE}}
updated: {{DATE}}
---

# Drafting feedback (living)

> **Status:** Living artifact. Append after each draft cycle. Drafting skills load this file alongside `kill-list.md` as the personal kill-list extension. The standing instructions section captures patterns extracted from real review feedback; the feedback log captures specific corrections per draft.

---

## How this file works

**At write time:** drafting skills load this file. Standing instructions override defaults when applicable. Skills enforce them in the same self-review pass that checks `kill-list.md`.

**After review:** when {{VAULT_OWNER_SHORT_NAME}} (or an editor) gives feedback on a draft, append it to the feedback log at the bottom. Format:

| Field | What goes there |
|---|---|
| **Date** | When the draft was reviewed |
| **Channel + topic** | e.g., *"Executive newsletter — issue title"* |
| **Feedback** | The correction, in actionable form (what to change, not just what was wrong) |
| **Applied to** | Which section / element of the draft |

**Periodic distillation:** every ~5 feedback entries, look for repeated patterns. When the same correction shows up 2+ times, promote it from the feedback log to a standing instruction in the relevant section above. Note the source(s) so we can trace how the rule emerged.

---

## Standing instructions

### Voice and language

- **Use {{VAULT_OWNER_SHORT_NAME}}'s actual phrasing** before defaulting to generic AI-newsletter language. When the exec has said something better in their own words (from interview transcripts, voice memos, or past writing), use their words.
- **Use real, current examples** over abstract framing. Specifics — named builds, specific tools, real timelines, dollar amounts — ground pieces and prevent genericness.
- **Plain language for technical concepts.** When introducing tools, automations, or technical systems — explain what each does for the reader in everyday terms. Don't assume familiarity.
- **Set realistic expectations.** Frame targets for the audience's actual situation. Relieve pressure where appropriate; don't add it.
- **Vary openers across pieces.** Don't default to the same opener phrase repeatedly. Rotate. Skim across recent pieces before settling on an opener.

### Identity and POV

- **{{VAULT_OWNER_SHORT_NAME}} is the author. First person, always.** *I, me, my.* Never refer to the exec in third person.
- **Don't open content with an EA-first or assistant-first framing** if {{VAULT_OWNER_SHORT_NAME}} is an executive. Open with a universal observation, a named conversation, or a specific moment they witnessed.

### Tone

- **Honest but not harsh.** Direct truth delivered with care. No punitive language. Brutally honest, not cruel.
- **Motivate through aspiration, not fear.** Lead with *"become the kind of person / team / operator who..."* rather than threat framing. Fear framing is saturated and exhausts readers.

### Format and structure

- **Steps and action items: bold label on its own line, content underneath.** Don't cram both into one dense paragraph. Easier on the eye. Skim-friendly.
- **Sections must chain.** Each section builds on the previous. Avoid scattering related ideas across non-adjacent sections.
- **Conciseness over word count.** Don't pad. If a point was made earlier, don't repeat it.
- **CTAs must match the body's framework.** Don't introduce concepts in the close (frameworks, offers, career paths) that the piece didn't build toward.

### Closing patterns

- **Keep concise labeled sections tight.** When using a named closing section, cap at two paragraphs maximum. Don't title every piece's close with the same heading; vary the framing.
- **Outcomes thesis, when relevant.** The goal is always outcomes — not tools for tools' sake. Whenever a piece teaches a tool or tactic, ground it in outcome language.

---

## Per-exec drafting feedback log

> **Status: blank.** Append entries as drafts get reviewed in this vault. Newest at top.

| Date | Channel + topic | Feedback | Applied to |
|---|---|---|---|

*(Empty — populated as drafts get reviewed.)*

---

## How drafting skills load this file

Each drafting skill (`email-writing`, `landing-page-writing`, `long-form-writing`, `repurposing`) reads this file alongside `kill-list.md` during the load-first phase. During self-review:

1. Run the draft against the **Top 5 highest-violation patterns** in `kill-list.md` (AI fingerprints, voice slop, etc.).
2. Run the draft against the **Standing instructions** in this file.
3. Both are non-negotiable. Either failing fails the self-review.

When in doubt: standing instructions in this file are more *exec-specific* (named entities, product specifics, voice nuances). The kill list is more *universal* (AI fingerprints, banned patterns). Both layers compound.

*(Drafting feedback compounds quality. Each review cycle's edits become new standing instructions or kill-list additions, distilled here.)*
