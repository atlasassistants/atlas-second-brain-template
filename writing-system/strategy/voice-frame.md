---
title: Content Strategy — Voice Frame Per Domain
type: area
tags:
  - writing-system
  - strategy
  - voice
created: {{DATE}}
updated: {{DATE}}
status: blank
---

# {{VAULT_OWNER_SHORT_NAME}}'s Voice Frame Per Domain

> **Status: blank.** Populate via `/content-strategy-onboard` Phase 7.

This file does **not** override `writing-system/voice.md`. The voice itself is consistent across domains. What this file specifies is which moves get used most heavily in each domain, and which domain-specific kill-list additions apply.

The drafting skills (`long-form-writing`, `email-writing`, `landing-page-writing`, `repurposing`) load both `voice.md` and `kill-list.md` globally. When operating inside a specific domain, this file adds a per-domain layer on top.

---

## Voice frame summary table

| Domain | Voice flavor | Philosophical pullback weight |
|---|---|---|
| <!-- D1 --> | <!-- architectural, conversational, confessional, etc. --> | <!-- Heavy / Compressed / Light --> |
| <!-- D2 --> | <!-- ... --> | <!-- ... --> |

<!-- Add columns as needed: "Closest swipe-file neighbor", "Primary anchor moves", etc. -->

---

## D1 — <!-- domain name -->

**Voice flavor.** <!-- 1-2 sentences on the overall tone and density for this domain. -->

**Moves leaned on.**

<!-- 3-5 specific rhetorical moves that should appear most in this domain:
- Named concepts / vocabulary as proper nouns
- Receipts (specific numbers, named builds, timelines)
- Contrast-driven openings
- Second-person imperatives
- Story anchors
-->

**Moves leaned away from.**

<!-- What should NOT dominate this domain, even if it's in the global voice. -->

**Domain-specific kill-list additions.**

<!-- Specific patterns banned only in this domain. Examples:
- No tool-feature comparisons without the structural "why"
- No generic productivity framing
- No abstract motivation without concrete next moves
-->

---

## D2 — <!-- domain name -->

(Repeat structure per domain.)

---

## How the writing-system loads this

The drafting skills should load voice in this order:

1. **[[../voice.md]]** — global voice frame (always loaded).
2. **[[../kill-list.md]]** — global kill list (always loaded).
3. **`../audience/<audience>.md`** — audience layer (matched to the piece's domain).
4. **This file (`voice-frame.md`)** — domain-specific layer for the piece being drafted. Apply the section matching the piece's domain.

The drafter needs to know which domain a piece is being written into so the right per-domain layer applies.

---

## Cross-links

- [[domains.md]] — domain definitions
- [[pillars.md]] — pillars within each domain
- [[audience-mapping.md]] — single-audience-per-domain rule + pairing logic
- [[commercial-mapping.md]] — direct-CTA vs. warm-up per domain
- [[cadence.md]] — cadence per domain
- [[distribution.md]] — channel + repurposing chain per domain
- [[../voice.md]] — global voice signature (load first)
- [[../kill-list.md]] — global kill list (load second)
- [[../audience/]] — audience pages
- [[../engine/editorial-filter.md]] — topic gating
