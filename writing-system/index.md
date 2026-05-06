---
title: Writing System Index
type: knowledge
tags:
  - writing-system
  - copywriting
  - voice
created: {{DATE}}
updated: {{DATE}}
subtype: ""
sources: []
related: []
---


# Writing System — Command Center

> The knowledge graph for {{VAULT_OWNER_SHORT_NAME}}'s writing. Activates whenever copy is written — emails, landing pages, newsletters, X long-form articles, X threads, X shorts, LinkedIn posts.

---

## 1. Identity

This is **{{VAULT_OWNER_SHORT_NAME}}'s personal writing system.** Built to enforce their voice across every surface where they communicate. Voice, audience, kill list, frameworks, hooks, and CTA patterns live here as a graph that any writing skill (or human) loads before producing copy.

**Voice owner:** {{VAULT_OWNER_SHORT_NAME}}
**Mission:** Every piece of copy that ships under {{VAULT_OWNER_SHORT_NAME}}'s name reads as {{VAULT_OWNER_SHORT_NAME}}, regardless of who or what drafted it.

---

## 2. Node map

Every node below is a knowledge file. Read the relevant ones before executing any writing task. Wikilinks are clickable; follow them.

### Voice (the core)

- [[voice]] — voice signature: rhythm, structural moves, philosophical-pullback pattern, formatting rules
- [[kill-list]] — banned words, phrases, structures, formatting tics; the AI-fingerprint detector

### Audience

- [[audience/<primary>]] — primary ICP; populate with your primary audience profile
- [[audience/<secondary>]] — secondary audience; populate with your secondary audience profile

<!-- per-vault: rename <primary> and <secondary> to match your actual audience file names -->

### Strategy (what we write about)

- [[strategy/README]] — entry point + how skills load this layer
- [[strategy/domains]] — content domains (define your D1–D4 or equivalent)
- [[strategy/pillars]] — pillars (4 per domain) with anchor content
- [[strategy/audience-mapping]] — single-audience-per-domain + pairing rules
- [[strategy/commercial-mapping]] — direct CTA vs. warm-up per domain
- [[strategy/cadence]] — cadence per domain
- [[strategy/distribution]] — channel + repurposing chain per domain
- [[strategy/voice-frame]] — per-domain voice nuances + kill-list additions

### Engine (cross-channel logic)

- [[engine/hooks]] — hook formula library, per-channel fit
- [[engine/frameworks]] — copywriting frameworks (Contrast-driven, PAS, BAB, Garry-Tan-style, Authority-moment)
- [[engine/techniques]] — signature rhetorical moves (cross-referenced to frameworks)
- [[engine/editorial-filter]] — topic gating (4 questions, 5 categories, scoring rubric)
- [[engine/cta-patterns]] — CTA library (direct reply, soft conditional, book a call, curious open-loop, authority-mirroring)
- [[engine/repurpose]] — chain logic for transforming long-form → short-mid form
- [[engine/scheduling]] — placeholder for cadence and timing

### Content graph (material the writing pulls from)

- [[content-graph/README]] — structure, contracts, taxonomy, cross-reference protocol with `knowledge/` and `context/`
- [[content-graph/takes]] — {{VAULT_OWNER_SHORT_NAME}}'s perspectives (1–3 sentences each)
- [[content-graph/stories]] — narrative-ready experiences (Setup → Turning Point → Resolution → Lesson)
- [[content-graph/ideas]] — market trends and external signals
- [[content-graph/topics]] — connective tissue: drafting-optimized topic pages
- [[content-graph/receipts]] — atomic citable proof points (specific numbers, named outcomes)
- [[content-graph/quotes]] — borrowed wisdom cited with attribution

**Three-layer model:** Context (`{{VAULT_NAME}}/context/`) holds *identity*. Knowledge (`{{VAULT_NAME}}/knowledge/`) holds *world facts*. Content graph (this) holds *{{VAULT_OWNER_SHORT_NAME}}'s voice material*. The test: knowledge answers what something IS; content answers what {{VAULT_OWNER_SHORT_NAME}} SAYS about it.

### Channels (per-format playbooks)

- [[channels/email]] — promotional / sequence / broadcast emails
- [[channels/landing-page]] — service / sales / offer pages
- [[channels/newsletter]] — newsletters (primary and secondary lists)
- [[channels/x-article]] — X long-form articles (newsletter sibling, X-native)
- [[channels/x-thread]] — serial X threads (5–10 tweets)
- [[channels/x-short]] — single-tweet posts (1–3 tweets)
- [[channels/linkedin-post]] — LinkedIn personal-narrative posts

### Skills (the activation surface)

**Drafting skills** (output to `{{VAULT_NAME}}/areas/content/`):

- [[../.claude/skills/email-writing/SKILL]] — promotional, broadcast, sequence emails
- [[../.claude/skills/landing-page-writing/SKILL]] — service / sales / offer pages
- [[../.claude/skills/long-form-writing/SKILL]] — newsletters and X long-form articles
- [[../.claude/skills/repurposing/SKILL]] — transforms a long-form piece into X thread + X short + LinkedIn post

**Ingestion skill** (input to `content-graph/`):

- [[../.claude/skills/content-ingest/SKILL]] — processes transcripts, voice memos, pasted text into takes and stories

**Research skill** (external signal → `content-graph/ideas/`):

- [[../.claude/skills/research-topics/SKILL]] — pulls external trending content via `last30days`, scores against editorial-filter v2, writes candidate ideas. Multi-mode: domain, pillar (`--pillar <slug>`), free-text seed.

**Planning skill** (what to write next):

- [[../.claude/skills/suggest-topic/SKILL]] — surfaces ranked topic recommendations from existing content-graph material. Cadence-aware in no-args mode (weights toward lagging domain); supports domain-driven and pillar-narrowed modes. Output is in-chat only; reads `used_material:` from recent drafts to suppress exhausted topics.

### Examples

- [[examples/in-voice]] — real drafts that pass review (filled over time)
- [[examples/out-of-voice]] — anti-examples / generic AI drafts to contrast against

### Reference

- [[_reference/sources]] — pointers to source material (swipe file, ICP doc, voice memos)
- [[_reference/drafting-feedback]] — living: standing instructions distilled from real review cycles + ongoing feedback log per draft

---

## 3. Execution instructions

When given a writing task, the activated skill will:

1. **Identify the channel.** Email? Landing page? Newsletter? X format? LinkedIn?
2. **Identify the audience.** Primary or secondary?
3. **Identify the domain.** Which content domain? See [[strategy/domains]] for definitions; ask if not specified by the request.
4. **Read the shared layer** in this order: voice → audience → kill-list → strategy/voice-frame (apply the section matching the domain) → engine/hooks → engine/frameworks → engine/cta-patterns.
5. **Read the channel file** for the target format.
6. **Pick one framework** (don't combine).
7. **Pick one hook formula** suited to the channel.
8. **Pick one CTA** suited to the channel, domain, and funnel stage.
9. **Draft.**
10. **Self-review** against the channel-specific checklist, the **Top 5** in `kill-list.md`, and the per-domain kill-list additions in [[strategy/voice-frame]].
11. **Output.**

**Critical rule:** the output is not 1 idea reformatted across N channels. It's N pieces that each *think about the topic differently*. Same idea, different angle, hook, voice, structure, and format per channel. (See `engine/repurpose.md` for the litmus test.)

---

## 4. Open layers (status)

Tracking what's filled and what's a placeholder.

| Node | Status | Next step |
|---|---|---|
| voice.md | ⚠️ Needs population | Run `/content-strategy-onboard` or populate manually |
| audience/<primary>.md | ⚠️ Needs population | Run `/content-strategy-onboard` or populate manually |
| audience/<secondary>.md | ⚠️ Needs population | Run `/content-strategy-onboard` or populate manually |
| kill-list.md | ⚠️ Needs population | Run `/content-strategy-onboard` or populate manually |
| engine/hooks.md | ✅ Template v1 | Track performance data |
| engine/frameworks.md | ✅ Template v1 | Refine if any framework consistently underperforms |
| engine/techniques.md | ✅ Template v1 | Add new techniques as patterns emerge from drafts |
| engine/editorial-filter.md | ⚠️ Needs population | Populate categories as positioning clarifies |
| engine/cta-patterns.md | ✅ Template v1 | Track reply rates per CTA |
| engine/repurpose.md | ✅ Template v1 | Refine litmus test based on real outputs |
| engine/scheduling.md | ⚠️ Placeholder | Defined as part of broader content cadence work |
| _reference/drafting-feedback.md | ⚠️ Empty | Append after every draft review cycle |
| content-graph/README.md | ✅ Template v1 | — |
| content-graph/{takes,stories,ideas,topics,receipts,quotes}/ | ⚠️ Empty | <!-- per-vault content-graph state --> |
| content-graph/_run-log.md | ✅ initialized | Updated by ingestion skills |
| All channel files | ✅ Template v1 | Refine with real performance feedback |
| skills/research-topics/ | ✅ Template v1 | Populates `content-graph/ideas/` |
| skills/suggest-topic/ | ✅ Template v1 | Cadence-aware; dedupes against `drafts/` + `posts/` |
| All other skill files | ✅ Template v1 | Live testing |
| examples/in-voice | ⚠️ Empty | Fill with real drafts that pass review |
| examples/out-of-voice | ⚠️ Empty | Fill with anti-examples for contrast |

---

## 5. How to update this system

This is a living graph. When something changes:

- **Voice evolves** → edit `voice.md` directly. Skills pick up the change on next invocation.
- **New audience captured** → fill or add `audience/<name>.md`.
- **New cringe pattern** spotted → add to `kill-list.md`.
- **New hook formula** that performs → add to `engine/hooks.md` and update the per-channel fit table.
- **New channel** added (TikTok, podcast, video, etc.) → create a new `channels/<name>.md` file. Update the index.
- **New skill** needed → create `.claude/skills/<name>/SKILL.md`.

Keep changes in this directory. The skill layer (`.claude/skills/`) automatically picks up changes here.
