---
name: voice-onboard
description: Walk EA + exec through voice intake to populate the writing-system layer. Populates voice.md, kill-list.md (personal-specific section), and audience/<primary>.md. Verifies output by drafting a sample email. Use when an exec is being onboarded to the writing-system addon and needs voice extraction. Trigger phrases: "/voice-onboard", "voice intake", "voice onboarding", "extract voice for {exec}", "populate voice signature".
tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

# Voice Onboard

## Overview + when to use

`/voice-onboard` is the second of three onboarding skills for the Atlas second-brain writing-system addon:

1. `/onboard` — cold-start: sets up the knowledge layer (context/, knowledge/, meetings/).
2. **`/voice-onboard`** — you are here: extracts the exec's voice signature, defines the primary audience (ICP), and extracts personal kill-list items.
3. `/content-strategy-onboard` — adds the strategy layer: domains, content pillars, cadence, distribution channels.

Voice intake is **decoupled from publishing intent**. Even if the exec never plans to post publicly, every exec benefits from a populated voice layer — it improves email drafts, Slack messages, internal memos, and any other writing the EA produces on their behalf. Run this skill before any drafting skill is used in anger.

Re-runs are **safe and additive** — re-running with additional source material merges new evidence into existing voice.md, kill-list.md, and audience pages rather than overwriting them.

---

## Required inputs

Have the following ready before invoking:

1. **Source material** — one of:
   - File path or vault wikilink to a transcript, voice memo transcription, or sample writing (e.g., `/voice-onboard [[meetings/2026-05-01-voice-intake]]`)
   - Pasted text in the invocation prompt with a source descriptor (*"from my voice memo on 2026-05-01"*)
   - No source at all → skill enters **live interview mode** and walks the EA through ~7 questions interactively

2. **Exec's name** — used in the voice.md H1 (e.g., "Marcus Reyes") and in sign-off fields

3. **Audience slug** — kebab-case, becomes the filename `audience/<slug>.md` (e.g., `ops-directors`, `agency-owners`, `bootstrapped-founders`)

If any required input is missing, the skill prompts for it before proceeding.

---

## Output paths

| File | Action |
|---|---|
| `{{VAULT_NAME}}/writing-system/voice.md` | Overwrite blank scaffolding with populated voice signature |
| `{{VAULT_NAME}}/writing-system/kill-list.md` | Update `{{VAULT_OWNER_SHORT_NAME}}-specific kill items` section only — universal section untouched |
| `{{VAULT_NAME}}/writing-system/audience/<primary-slug>.md` | Create new file from `audience/_template.md` |
| `{{VAULT_NAME}}/writing-system/audience/_index.md` | Append new audience entry to the index table |

---

## Workflow

### Phase 1: Intake source

Determine how the voice material is arriving. Four input modes:

**Mode A — file path or wikilink given.**
- Resolve path. Read the full file.
- `source` = file's `title` from frontmatter (or filename if no frontmatter).
- `source_link` = wikilink to the file.
- Pull literal phrases the exec used — these become voice signature evidence in Phase 2.

**Mode B — pasted text with source descriptor.**
- Parse source descriptor from prompt (*"from voice memo on 2026-05-01"*).
- `source` = parsed descriptor.
- `source_link` = empty (or create an inbox stub if user wants the text filed).
- Pull literal phrases from pasted text.

**Mode C — pasted text without source descriptor.**
- Create a stub at `{{VAULT_NAME}}/inbox/transcripts/YYYY-MM-DD-voice-intake-untitled.md` with minimal frontmatter (type: inbox, ingested: false).
- `source` = "Voice intake YYYY-MM-DD"
- Proceed with the stub as source.

**Mode D — live interview mode (no source material provided).**

Walk the EA through the following questions. Capture answers verbatim — these are the raw voice evidence. EA reads questions aloud to the exec, or types in the exec's answers.

1. *"Describe how you communicate at work — not how you want to sound, but how your team says you actually sound."*
2. *"Read me a message you sent recently that felt like you. Slack message, email, doesn't matter. What made it feel right?"*
3. *"What's a phrase or expression you use all the time — something your team probably associates with you?"*
4. *"Who is the single person you're most trying to reach with your writing? Describe them in 2-3 sentences — their role, their frustration, what they're trying to get done."*
5. *"What does that person currently do about their problem? What have they already tried?"*
6. *"What would make them roll their eyes at something you wrote? What would make them forward it to a colleague?"*
7. *"Is there anything you refuse to write about, or a way of writing you find embarrassing or cringe-worthy? Give me an example."*

After all 7 answers are captured, treat the collected answers as the voice material and proceed to Phase 2.

**Quote extraction (all modes):** As you read the source, flag every phrase the exec actually used — pull these verbatim for `voice.md`'s Vocabulary signatures and Anchor moves sections. These are the evidence base. Do not paraphrase the voice in; capture what was said.

---

### Phase 2: Voice signature extraction

Read the full source (transcript, pasted text, or live-interview answers). Extract:

- **Tone** — overall register: direct, sardonic, warm, technical, conversational, etc. 2-4 sentences.
- **Sentence rhythm** — specific observable patterns: fragment usage, opening sentence length, punctuation moves (em-dash, colon), use of questions, list vs. prose preference. 3-5 bullets.
- **Vocabulary signatures** — 5-10 words/phrases the exec uses distinctively. Pull verbatim from source where possible.
- **Anti-patterns** — what does this exec NOT sound like? What moves do they avoid or reject (named explicitly or observable from tone)?
- **Anchor moves** — recurring rhetorical moves: do they open with a receipt (specific number, date, outcome)? Do they name the skeptic counter? Do they frame with "here's what nobody tells you"? 3-5 named moves with brief description.
- **Sources** — wikilink(s) to the source file(s) used.

**Write to `{{VAULT_NAME}}/writing-system/voice.md`:**
- Overwrite the blank scaffolding with the extracted content.
- Substitute `{{VAULT_OWNER_SHORT_NAME}}` in the H1 with the exec's actual short name (e.g., "Marcus Reyes's Voice Signature").
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

Reference [[writing-system/_examples/sample-exec/voice]] as a quality target for section depth and specificity.

---

### Phase 3: ICP definition

Ask 5-7 ICP questions to define the primary audience. If source material is a structured intake transcript, extract answers from it directly before asking — only ask what's not already answered in the source.

ICP questions:
1. *"Who is the person you're most trying to reach? Their job title, company stage, and one-sentence description."*
2. *"What is that person's biggest frustration right now — the thing keeping them stuck?"*
3. *"What have they already tried to fix that problem? What tools, frameworks, consultants?"*
4. *"Why did those solutions fail them?"*
5. *"What would make them immediately skeptical of something you wrote? What's their default cynical reaction?"*
6. *"What outcome would make them say 'this was worth reading'? Frame it concretely — ideally with a number or timeline."*
7. *"What do they fear most — professionally, organizationally, personally?"*

**Write to `{{VAULT_NAME}}/writing-system/audience/<primary-slug>.md`:**
- Copy `audience/_template.md` to `audience/<primary-slug>.md`.
- Populate all 7 sections with ICP answers.
- Set `audience_role: primary` in frontmatter.
- Set `audience_name: <primary-slug>` in frontmatter.
- Update `status: blank` → `status: populated`.

**Update `{{VAULT_NAME}}/writing-system/audience/_index.md`:**
- Append a row to the index table: `| [[<slug>]] | primary | <one-line description> | YYYY-MM-DD |`

---

### Phase 4: Kill-list extraction

Extract personal kill items by asking (or pulling from source material if it's an intake transcript):

1. *"What tone moves make you cringe when you read your own writing — or when you see a ghostwriter miss the mark?"*
2. *"Are there topics you won't write about publicly? Or topics that are on-brand for others but off-brand for you?"*
3. *"Are there structural patterns you refuse — numbered lists, bullet-everything, bold-everything, a specific opener formula?"*

**Write to `{{VAULT_NAME}}/writing-system/kill-list.md` — personal-specific section ONLY:**

Do not touch the `## Universal banned (ship-with-template)` section. Locate the `## {{VAULT_OWNER_SHORT_NAME}}-specific kill items` section and replace the blank placeholder content with populated kill items. Sub-organize as:

```markdown
## {{VAULT_OWNER_SHORT_NAME}}-specific kill items

### Tone moves
- [Item extracted]
- [Item extracted]

### Topics
- [Item extracted]
- [Item extracted]

### Structural
- [Item extracted]
- [Item extracted]
```

Update `updated:` in frontmatter. If the exec has no strong opinions in a subcategory, write `(none identified — update as voice develops)` as the only item.

---

### Phase 5: Verification draft

Load the following files before drafting:

1. `{{VAULT_NAME}}/writing-system/voice.md` — just populated
2. `{{VAULT_NAME}}/writing-system/audience/<primary-slug>.md` — just populated
3. `{{VAULT_NAME}}/writing-system/kill-list.md` — just updated
4. `{{VAULT_NAME}}/writing-system/engine/hooks.md`
5. `{{VAULT_NAME}}/writing-system/engine/frameworks.md`
6. `{{VAULT_NAME}}/writing-system/engine/techniques.md`
7. `{{VAULT_NAME}}/writing-system/engine/cta-patterns.md`

**Draft a 200-word sample email** using this scenario as the test bed:

- Subject: "Quick check-in on Q3 priorities"
- Sender: the exec (writing to their primary audience — someone on their team or a key stakeholder)
- Tone and structure must apply the populated voice signature

Write the draft to:
`{{VAULT_NAME}}/areas/content/emails/drafts/voice-verification-YYYY-MM-DD.md`

Frontmatter for the verification draft:
```yaml
---
title: Voice Verification Draft — YYYY-MM-DD
type: area
tags:
  - writing-system
  - voice-verification
  - draft
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Surface to exec (or EA relaying to exec):**

> "Here's a 200-word sample email written in the extracted voice. Does this sound like you?
>
> [draft content]
>
> If yes — we're done. The voice layer is live.
> If no — tell me what's off (too formal? wrong vocabulary? wrong rhythm?) and we return to Phase 2 with that feedback + a request for more source material."

**Hard gate:** If the exec disowns the draft, do NOT mark the skill complete. Return to Phase 2 with:
- The exec's specific objections
- A prompt: *"To improve the extraction, we need more source material. Can you share: (1) a recent email you wrote that felt right, (2) a Slack message that sounds like you, or (3) 5 minutes to answer more questions?"*

Re-run Phases 2-5 with the new material. Surface a revised verification draft. Repeat until exec approves or explicitly defers.

---

## Cross-skill relationships

| Skill | Relationship |
|---|---|
| `/onboard` | Runs before this skill. Sets up context/, knowledge/, meetings/. Run it first on a fresh vault. |
| `/content-strategy-onboard` | Runs after this skill. Adds the strategy layer: domains, content pillars, cadence, distribution channels. Voice must be populated before strategy makes sense. |
| `/content-ingest` | Ongoing transcript-to-content-graph pipeline. `/voice-onboard` is a one-shot intake; `/content-ingest` is the recurring ingestion skill for session-by-session voice material. They share transcript-handling logic — if the intake source is a structured transcript, `/voice-onboard` can call `/content-ingest` internally to extract any takes/stories it finds, writing them to `content-graph/` alongside the voice layer. |
| `/email-writing` and other drafting skills | Phase 5's verification draft uses email-writing's pattern as the test bed. Once voice-onboard is complete, drafting skills are fully enabled — they load voice.md + kill-list.md + audience pages automatically. |
| `/lint` | After running `/voice-onboard`, `/lint` can verify that all required writing-system files are populated (status: populated, no unfilled `{{...}}` placeholders in voice.md, kill-list.md, or audience pages). |

---

## Output summary format

At the end of a successful skill run, report back:

```
Voice onboard complete.

Files created / updated:
- writing-system/voice.md — populated (was: blank)
- writing-system/kill-list.md — personal section updated
- writing-system/audience/<primary-slug>.md — created
- writing-system/audience/_index.md — index updated
- areas/content/emails/drafts/voice-verification-YYYY-MM-DD.md — verification draft

Voice signature summary:
- [One-line pulled from tone section of voice.md]

Audience:
- <primary-slug> (primary) — [one-line role description]

Kill-list additions: [N] items
- Tone moves: [X]
- Topics: [Y]
- Structural: [Z]

Verification draft: areas/content/emails/drafts/voice-verification-YYYY-MM-DD.md
Voice-fit assessment: [APPROVED — exec confirmed fit | PENDING — returned to Phase 2 with exec feedback]

Next step:
- [If approved]: Run /content-strategy-onboard to add domains, pillars, cadence, and distribution.
- [If pending]: Collect more source material and re-run Phase 2.
```
