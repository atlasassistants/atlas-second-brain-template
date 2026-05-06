---
title: Content Strategy — Voice Frame Per Domain (Sarah Chen)
type: area
tags:
  - writing-system
  - content-strategy
  - sample-exec
  - voice
  - kill-list
created: 2026-05-06
updated: 2026-05-06
status: populated
---

# Content Strategy — Voice Frame Per Domain

> **Status:** Populated for Sarah Chen / Gridline. Names which voice signature moves apply most heavily per domain and which domain-specific kill-list additions apply on top of the global kill list.

This file does **not** override [[../voice]]. Sarah's voice is consistent across domains. What this file specifies is which moves from the voice signature get used most heavily in each domain, and which domain-specific patterns are banned.

Load order for drafting skills:
1. [[../voice]] — global voice signature (always first)
2. [[../kill-list]] — global kill list (always second)
3. [[../audience/saas-founders]] or [[../audience/ic-to-leadership]] — audience layer
4. **This file** — domain-specific voice layer (apply the section matching the piece's domain)

---

## Voice frame summary table

| Domain | Voice flavor | Anchor moves leaned on | Philosophical pullback weight |
|---|---|---|---|
| **D1 — Engineering Velocity at Scale** | Structural, receipt-heavy, diagnostic | Receipt-first, builder-as-witness, concrete over abstract | Light (1 closing paragraph — the diagnosis suggests the stakes) |
| **D2 — AI-Native Infrastructure** | Category-creating, architecturally precise | Receipt-first, skeptic counter, leave-the-frame-open | Moderate (the architectural argument earns a "what this means for the craft" close) |
| **D3 — Founder-as-Builder** | Confessional, honest, earned | Builder-as-witness, leave-the-frame-open, skeptic counter | Heavy (the frame IS the piece — D3 is the philosophical domain) |

---

## D1 — Engineering Velocity at Scale

**Voice flavor.** Structural, receipt-heavy, diagnostic. Highest technical specificity of the three domains. Sarah is writing as an engineer who has seen these systems fail and knows exactly where the leak is. Opinions are structural, not motivational.

**Moves leaned on.**

- **Receipt-first.** D1 pieces should open with a specific artifact: a cycle time number, a team size, a specific failure. *"We shipped 14 features in Q1. Then we hired 6 engineers and shipped 9 in Q2."* That's the opening — not a thesis statement.
- **Builder-as-witness.** Frame D1 advice as *"here's what happened when we did this,"* not *"you should do this."* The authority is diagnostic, not prescriptive.
- **Concrete over abstract.** Every structural claim earns a specific instance. *"Handoff design breaks at 20 engineers"* — okay. *"Handoff design breaks at 20 engineers because you no longer have ambient context about every open PR"* — better. *"The receipt: we added a PR review template and cycle time dropped 40%"* — right.

**Moves leaned away from.**

- Abstract argument without the receipt. If a D1 piece has no specific shipped example or specific Gridline/engineering decision as anchor, it's not ready.
- Identity/philosophy as primary structure. D1 closes with stakes, not with reframes. *"This is what engineering at scale can look like"* is fine at close — not as the body.
- Permission-giving or motivational tone. D1 assumes the reader already knows they have a velocity problem; it doesn't need to convince them to care.

**Domain-specific kill-list additions (D1 only).**

- **No generic engineering-productivity framing.** *"Ship faster"* / *"move faster"* without a structural cause identified is empty.
- **No tool comparisons without the structural argument.** Recommending a tool without the architectural reason it fits the velocity problem is a buyer's guide, not D1 content.
- **No process-church content.** Advocating for a process framework (agile, scrum, shape up) without a specific receipt of what it actually changed at Gridline reads as religion, not engineering.
- **No hero-engineer framing.** Velocity is a property of the system, not of individual heroics. Don't write D1 in a way that suggests the answer is hiring smarter people.

---

## D2 — AI-Native Infrastructure

**Voice flavor.** Category-creating, architecturally precise. Sarah is writing as the person who is building Gridline inside the category she's also defining. These pieces should feel like the thesis behind the product made public — not a product page, but the engineering argument that justifies the product.

**Moves leaned on.**

- **Receipt-first.** D2 pieces open with a specific infrastructure decision Sarah has made — what Gridline built, what broke before it, what the constraint was. *"We evaluated 6 AI tooling options before building the harness layer ourselves. Here's what the evaluation actually revealed."*
- **Skeptic counter.** D2 is a domain with strong opposing intuitions (*"just use the latest model"*, *"bolt it on and iterate"*). Name the obvious objection early: *"I know this sounds like premature optimization…"* and address it directly.
- **Leave-the-frame-open.** D2 is a fast-moving domain. Not every piece should resolve cleanly — *"we don't have this fully figured out"* is a more honest close than a tidy 3-step framework.

**Moves leaned away from.**

- AI hype or futurism. D2 is about what Sarah has built and decided, not about what AI will make possible in 5 years. Every claim earns a specific receipt.
- Tutorial-without-judgment. Technical tutorials are fine if they serve the architectural argument — they're not a substitute for it. D2 is not a documentation domain.
- Bolted-on Gridline pitch. The product should emerge from the argument naturally, not as a tacked-on CTA that feels separate from the piece.

**Domain-specific kill-list additions (D2 only).**

- **No AI tool reviews.** *"Here are the best LLM tools for engineering teams"* is a listicle, not D2. D2 is about system design, not tool selection divorced from architectural context.
- **No *"just use AI"* framing.** D2 earns the right to be specific; generic AI enthusiasm belongs nowhere in Sarah's voice and least of all in D2.
- **No vendor-positioning language.** *"Cutting-edge," "state-of-the-art," "enterprise-grade"* — banned globally, doubly banned in D2 where credibility is the whole point.
- **No piece that would have the same argument without the Gridline receipt.** If the architectural claim doesn't come from something Sarah has actually built or decided, the piece isn't ready.

---

## D3 — Founder-as-Builder

**Voice flavor.** Confessional, honest, earned. This is the domain where Sarah's voice gets the most personal — not in a personal-life sense, but in the sense that she's writing about her own judgment, her own mistakes, her own ongoing negotiation with what it means to stay technical while running a company. The philosophical pullback is heaviest here because the philosophical question IS the subject.

**Moves leaned on.**

- **Builder-as-witness.** D3 pieces recount what actually happened — a specific hire, a specific code decision, a specific moment where Sarah's engineering instinct was right or wrong. The advice emerges from the receipt, not the other way around.
- **Leave-the-frame-open.** D3 pieces often end without resolution — *"I don't have a clean answer to this one"* is an honest close and matches Sarah's voice. D3 is not a domain for tidy frameworks.
- **Skeptic counter.** Sarah is aware her D3 audience has heard every founder-stays-technical take. Name that: *"I know every founder says they stay close to the code. Here's what that actually looked like for me last month."*

**Moves leaned away from.**

- Motivational framing. D3 does not encourage or permission-give — it witnesses. *"You can do this"* framing is wrong. *"Here's what happened when I tried"* is right.
- Generic founder advice. If the D3 piece could have been written by any founder, it's not ready. The receipts need to be specifically Sarah's, specifically technical, specifically Gridline.
- Personal-life as anchor. Family moments, personal struggles (unless directly tied to a technical identity question) — D3 is about craft identity, not personal narrative.

**Domain-specific kill-list additions (D3 only).**

- **No romanticizing the founder-engineer myth.** *"Real founders still write code"* as a tribal statement is off. Sarah's actual view is more nuanced: sometimes staying technical compounds, sometimes it's a delegation failure. D3 earns its authority by holding that complexity.
- **No burnout-glorification.** Framing overwork or sacrifice as proof of founder commitment is banned globally but doubly applicable in D3 where the personal stakes are highest.
- **No *"here's what separates great founders from average ones"* framing.** This is gatekeeping masquerading as insight. Sarah's D3 voice is *"here's what I'm still figuring out"* — not taxonomy of founder quality.
- **No productivity-system advice.** D3 is about technical identity and judgment — not about how Sarah manages her calendar or runs her week. Those belong elsewhere or nowhere.

---

## How the writing-system loads this

1. Identify which domain the piece belongs to (D1, D2, or D3) before drafting.
2. Load [[../voice]] + [[../kill-list]] globally.
3. Load the audience file ([[../audience/saas-founders]] for D1/D2; both audience files for D3).
4. Apply the domain-specific section of this file on top: voice flavor, moves leaned on, moves leaned away from, domain-specific kill-list additions.

If domain is ambiguous, surface it before drafting — the voice-frame choice affects the entire piece.

---

## Cross-links

- [[domains]] — domain definitions
- [[pillars]] — pillars within each domain
- [[audience-mapping]] — audience-domain matrix + pairing logic
- [[commercial-mapping]] — direct-CTA vs. warm-up per domain
- [[cadence]] — cadence per domain
- [[distribution]] — channel + repurposing chain per domain
- [[../voice]] — global voice signature (load first)
- [[../kill-list]] — global kill list (load second)
- [[../audience/saas-founders]] — primary audience
- [[../audience/ic-to-leadership]] — secondary audience (co-primary for D3)
