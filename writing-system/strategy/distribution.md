---
title: Content Strategy — Distribution
type: area
tags:
  - writing-system
  - strategy
  - distribution
created: {{DATE}}
updated: {{DATE}}
status: blank
---

# {{VAULT_OWNER_SHORT_NAME}}'s Distribution Strategy

> **Status: blank.** Populate via `/content-strategy-onboard` Phase 6.

This file specifies which channels each domain reaches and how the long-form source piece repurposes (or doesn't) into shorter formats. Drives the `repurposing` skill and informs production scheduling.

---

## Channels {{VAULT_OWNER_SHORT_NAME}} runs

<!-- List every channel actively used. Examples:
- Newsletter (primary list name)
- Newsletter (secondary list name, if applicable)
- X long-form articles
- X threads
- X shorts
- LinkedIn posts
- Email broadcasts (campaign-level)
- Landing pages (per-campaign)
-->

---

## Distribution matrix

| Domain | Newsletter | X long-form | X thread | X short | LinkedIn | Email broadcast | Landing page |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| <!-- D1 --> | <!-- ✅ / ⚠️ selective / ❌ --> | | | | | | |
| <!-- D2 --> | | | | | | | |

**Legend:** ✅ always = every piece in this domain ships to this channel. ⚠️ selective = some pieces, intentionally chosen. ❌ rarely / never = default off; only with strong justification.

---

## Per-domain notes

### D1 — <!-- domain name -->

<!-- Describe the repurposing chain for this domain. Which formats does this domain compress into well? Which channels are primary vs. secondary? Any selective-only channels and the condition that triggers them? -->

### D2 — <!-- domain name -->

<!-- Repeat per domain. -->

---

## Repurposing pattern observations

<!-- Cross-domain notes:
- Do any domains share identical distribution patterns? (Note this — it simplifies repurposing skill logic.)
- Which domain has the narrowest chain? Why?
- Which domain uses email broadcasts as default-on (campaign) vs. selective?
-->

---

## Production-load implications

Per long-form source piece, repurposing chain output:

| Domain | Outputs per piece | Annual repurposed output |
|---|---|---|
| <!-- D1 --> | <!-- list formats --> | <!-- pieces/year × outputs --> |
| <!-- D2 --> | | |

<!-- Total annual content output = sum across all formats. This load is what the `repurposing` skill needs to support. -->

---

## Cross-links

- [[domains.md]] — domain definitions
- [[pillars.md]] — pillars within each domain
- [[audience-mapping.md]] — single-audience-per-domain rule
- [[commercial-mapping.md]] — direct-CTA vs. warm-up per domain
- [[cadence.md]] — cadence per domain
- [[voice-frame.md]] — voice nuances + per-domain kill-list additions
- [[../channels/]] — channel-specific drafting rules

## How this is used

- `repurposing` skill loads `distribution.md` to determine which formats to produce per domain
- `/content-strategy-onboard` Phase 6 produces this file
