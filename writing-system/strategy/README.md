---
title: Writing System — Strategy
type: area
tags:
  - writing-system
  - content-strategy
created: {{DATE}}
updated: {{DATE}}
---

# Strategy

> {{VAULT_OWNER_SHORT_NAME}}'s content strategy as it sits inside the writing-system. Every drafting skill and pipeline skill loads from here when a piece is being written. The strategy answers *what we write about, who reads it, when it ships, where it goes, and what voice it carries* — at a layer above voice/audience/kill-list (which answer *how to write*).

Populate this layer via `/content-strategy-onboard` (runs all 8 phases). Once complete, all drafting and pipeline skills load from here automatically.

---

## Files

| File | What it covers |
|---|---|
| [[domains.md]] | Content domains: the stable, recurring content streams. Identity, audience, editorial purpose, boundary notes per domain. |
| [[pillars.md]] | Pillars (sub-topics inside each domain). Canonical kebab-case slugs used in skill calls and draft frontmatter. |
| [[audience-mapping.md]] | Single-audience-per-domain matrix. Pairing rule for content streams. |
| [[commercial-mapping.md]] | Direct CTA target vs. indirect warm-up per domain. Which domain is designed to convert vs. warm up. |
| [[cadence.md]] | Per-domain publishing cadence and production load math. |
| [[distribution.md]] | Channel + repurposing chain per domain. Which channels each domain ships to; which formats apply. |
| [[voice-frame.md]] | Per-domain voice nuances + per-domain kill-list additions. Voice itself stays consistent; what changes is which moves get used most. |

---

## How skills load this

Drafting skills (`long-form-writing`, `email-writing`, `landing-page-writing`, `repurposing`) load this layer in addition to the global voice/kill-list/audience layer:

1. **[[../voice.md]]** — global voice signature
2. **[[../kill-list.md]]** — global kill list
3. **`../audience/<list>.md`** — audience layer (matched to the piece's domain)
4. **`../channels/<channel>.md`** — channel-specific drafting rules
5. **Strategy layer (this directory):** identify the domain → load the matching section of `voice-frame.md`. For repurposing, also consult `distribution.md` to know which formats apply per domain.

Pipeline skills (`suggest-topic`, `research-topics`) load the strategy more heavily:

- `domains.md` + `pillars.md` define the candidate space topic suggestion can pull from.
- [[../engine/editorial-filter.md]] uses the domain structure as Filter 1 (domain fit) before content-quality scoring.
- `cadence.md` informs how often each domain demands fresh ideas.
- `commercial-mapping.md` flags which domain a piece warms up for, informing CTA selection.

---

## When to update this

The strategy is locked but not frozen. Update when:

- **The exec's positioning shifts.** New domain emerges (rare). Existing domain retires (rarer).
- **Audience clarifies.** New sub-archetype validated, audience-domain mapping refines.
- **Offers change.** New commercial offer launches → update `commercial-mapping.md`. Offer retires → same.
- **Cadence proves unsustainable or under-utilized.** Bump or reduce per domain in `cadence.md`.
- **Channel performance shifts.** A channel turns out to drive disproportionate conversion for a domain → update `distribution.md`.
- **Voice frame learns something.** A specific kill-list addition keeps coming up in editor feedback for one domain → add to `voice-frame.md`.

Keep `[[../engine/editorial-filter.md]]` aligned with whatever changes here — it's the gatekeeper that loads this strategy.

---

## Cross-links

- [[../index.md]] — writing-system command center
- [[../engine/editorial-filter.md]] — topic gating, populated by /content-strategy-onboard Phase 8
- [[../voice.md]] — global voice signature
- [[../kill-list.md]] — global kill list
- [[../audience/]] — audience pages (populated by /voice-onboard)
