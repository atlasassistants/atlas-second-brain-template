---
title: Editorial Filter
type: area
tags:
  - writing-system
  - editorial-filter
  - engine
created: {{DATE}}
updated: {{DATE}}
status: framework
---

# Editorial Filter

Two-filter design used by `/research-topics` and `/suggest-topic` to score candidate ideas:

## Filter 1: Domain fit

Does the candidate idea sit within one of {{VAULT_OWNER_SHORT_NAME}}'s defined domains?

| Domain | Slug | Test |
|---|---|---|
| <!-- populated by /content-strategy-onboard from strategy/domains.md --> | | |

A candidate that doesn't sit clearly in one domain gets dropped from the ranking.

## Filter 2: Quality criteria

Score each candidate that passes Filter 1 against these 6 criteria (1-5 scale):

1. **Specificity.** Does it reference a concrete situation, named tool, named person, dollar amount, or timeline?
2. **Skin-in-the-game.** Does {{VAULT_OWNER_SHORT_NAME}} have direct experience with the claim?
3. **Proof.** Is there a receipt — a story, dataset, or named outcome — that backs it up?
4. **Stakes.** Does ignoring the claim cost the audience something concrete?
5. **Audience match.** Does it land for the audience the domain serves?
6. **Voice fit.** Does the framing align with {{VAULT_OWNER_SHORT_NAME}}'s anchor moves and avoid kill-list patterns?

Total: ≥24/30 → priority candidate. 18-23/30 → bench. <18 → drop.

## Where this is loaded

- `/research-topics` — scores candidate ideas before writing to `content-graph/ideas/`
- `/suggest-topic` — scores material when ranking topic suggestions
- `/long-form-writing` Phase 1 — sanity-checks the chosen topic against this filter

## Tie-in

This filter is populated by `/content-strategy-onboard` Phase 8 (editorial filter refresh) using outputs from the strategy layer.
