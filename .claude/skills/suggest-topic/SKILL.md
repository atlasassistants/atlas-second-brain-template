---
tags:
  - writing-system
  - planning
  - content-graph
created: '{{DATE}}'
updated: '{{DATE}}'
name: suggest-topic
description: Surface ranked topic recommendations from existing material. Cadence-aware in no-args mode — reads recent publish history and weights output toward the lagging domain. Activate on triggers like "what should I write about", "/suggest-topic", "/suggest-topic D1" (domain-driven), or "/suggest-topic --pillar <slug>" (pillar-narrowed). Returns 5 ranked topics in chat with material links, scoring rationale, and per-domain cadence reasoning.
tools: Read, Write, Edit, Glob, Grep, Bash
title: Suggest Topic Skill
type: note
---

# Suggest Topic Skill

## Load first — every time, before suggesting

Read these files in order:

1. `../../engine/editorial-filter.md` — two-filter scoring (Filter 1 domain fit + Filter 2 content quality)
2. `../../strategy/domains.md` — domain definitions
3. `../../strategy/pillars.md` — pillars + which domain each belongs to
4. `../../strategy/audience-mapping.md` — which domain serves which audience
5. `../../strategy/commercial-mapping.md` — commercial role per domain
6. `../../strategy/cadence.md` — per-domain target (see cadence.md for targets per domain)
7. `../../strategy/distribution.md` — distribution chain per domain
8. `../../content-graph/topics/_index.md` — existing curated topic pages
9. **Recent draft + published archives** for dedup (read both):
   - `../../../areas/content/newsletters/<list-name>/drafts/` and `../../../areas/content/newsletters/<list-name>/posts/`
   - `../../../areas/content/emails/drafts/`

<!-- per-vault: replace <list-name> with your actual newsletter folder names -->

---

## Triggers

- `/suggest-topic` (no args) — cadence-aware cross-domain mix. Reads recent publish history; weights output toward lagging domain.
- `/suggest-topic D1` (or other domain codes) — domain-driven, ignores cadence.
- `/suggest-topic --pillar <slug>` — pillar-narrowed within a domain.
- Optional flag on any mode: `--count N` (default 5).

---

## Workflow

1. **Read `used_material:` from recent drafts and published pieces** (last 90 days, across all listed archive paths — both `drafts/` and `posts/` directories for newsletters, `drafts/` for emails). Build a "material exhausted recently" set — wikilinks that have already been used. Topics whose anchor stories/receipts are in this set are demoted or suppressed. Reading both directories ensures dedup catches material the moment it's pulled into a draft, not just after publish.

2. **Cadence calculation (no-args mode only):**
   - Read recent publish history per domain by listing files in newsletter `posts/` directories and reading frontmatter `domain:` field on each. (Use `posts/` only for cadence counting — published pieces only.)
   - Compute per-domain backlog vs. quarterly cadence target per `../../strategy/cadence.md`.
   - Determine weighted output mix based on which domain is lagging behind its quarterly target.
   - **Cold-start fallback:** If recent posts have no `domain:` frontmatter (this happens for posts predating domain-tagging), report cadence as "indeterminate" in the output and skip domain weighting — surface candidates evenly across domains. Once enough new domain-tagged posts accumulate, cadence-aware weighting takes over automatically.

3. **Search `../../content-graph/`** for candidate topics. A candidate is a **clustering of available material**: multiple takes + at least one story or receipt + recent ideas that have clear domain fit and a relevant angle. Topic pages in `../../content-graph/topics/` are pre-clustered candidates — start there, then look for emergent clusters in `takes/` + `stories/` + `ideas/` that don't yet have topic pages.

4. **Score** each candidate against editorial-filter v2 six-criteria rubric.

5. **Suppress dedup'd candidates.** Drop or deprioritize any candidate whose primary anchor material is in the "exhausted recently" set from step 1.

6. **Return top N in chat** (default N=5).

---

## Output

In-chat only — no file written. {{VAULT_OWNER_SHORT_NAME}} picks one topic and passes it as input to a drafting skill.

### Output format

```markdown
# Topic Suggestions — {timestamp}

**Trigger:** /suggest-topic <args>
**Mode:** <cadence-aware no-args | domain-driven | pillar-narrowed>

{If no-args mode (cadence-aware), include cadence reasoning:}
**Cadence status (this quarter):**
- D1 (<domain name>): X/<target> published — {on track | lagging | ahead}
- D2 (<domain name>): X/<target> — ...
- D3 (<domain name>): X/<target> — ...
- D4 (<domain name>): X/<target> — ...
**Weighting:** Emphasizing D{lagging} in suggestions below.

{If domain-driven mode:}
**Filtered to:** D{N} — {domain name}
**Pillars considered:** {list of pillars in this domain}

{If pillar-narrowed mode:}
**Filtered to pillar:** {pillar slug} ({domain it belongs to})

---

## 1. <Proposed topic title>
- **Domain:** D2 — <domain name>
- **Pillar:** <pillar-slug>
- **Audience:** <audience per strategy/audience-mapping.md>
- **Commercial role:** <per strategy/commercial-mapping.md>
- **Available material:**
  - [[content-graph/takes/YYYY-MM-DD-{slug}]]
  - [[content-graph/stories/YYYY-MM-DD-{slug}]]
  - [[content-graph/receipts/{slug}]]
- **Score:** 5/6 (clears domain fit + 4 of 6 quality criteria; missing strong actionable angle — narrow framing in draft to address)
- **Why this now:** {one-line rationale}

(repeat for top N)
```

---

## Cross-skill relationships

- **Upstream:** `research-topics` writes ideas to `content-graph/ideas/`; this skill reads them as part of step 3.
- **Downstream:** {{VAULT_OWNER_SHORT_NAME}} picks one topic from this skill's output and invokes a drafting skill (`long-form-writing`, `email-writing`, `landing-page-writing`) with the picked topic. The drafting skill assembles material and writes the draft.
- **Dedup contract:** Reads `used_material:` from recent drafts (last 90 days) to suppress topics whose anchors are exhausted. This is the only dedup mechanism — no `used_in:` field on stories.
- **Lint:** `/lint` Phase 7 maintains the underlying content-graph health that this skill depends on.

---

## Out of scope (v1)

- Writing files. Output is in-chat only.
- Cross-piece reuse view ("this story has been used N times"). Beyond the 90-day dedup window, no global usage tracking. Add to `/lint` later if needed.
- Periodic / scheduled invocation.
