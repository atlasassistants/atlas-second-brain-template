---
name: content-strategy-onboard
description: Walk EA + exec through content strategy design. Populates strategy/*.md (domains, pillars, audience-mapping, commercial-mapping, cadence, distribution, voice-frame) and refreshes engine/editorial-filter.md against the populated domains. Use when an exec is being onboarded to the writing-system addon and needs to define their content strategy. Trigger phrases: "/content-strategy-onboard", "content strategy intake", "define content domains", "set up content strategy", "content cadence planning".
tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
---

# Content Strategy Onboard

## Overview + when to use

`/content-strategy-onboard` is the third of three onboarding skills for the Atlas second-brain writing-system addon:

1. `/onboard` — cold-start: sets up the knowledge layer (context/, knowledge/, meetings/).
2. `/voice-onboard` — extracts the exec's voice signature, defines the primary audience (ICP), and extracts personal kill-list items.
3. **`/content-strategy-onboard`** — you are here: adds the strategy layer. Defines content domains, pillars, audience-to-domain mapping, commercial mapping, cadence, distribution channels, and per-domain voice framing.

**Hard dependency:** This skill assumes `writing-system/voice.md` is populated (status: populated) and at least one `writing-system/audience/<slug>.md` exists. If either condition is not met, surface a clear prompt to the user:

> "Content strategy design assumes a populated voice signature and at least one audience page. Run `/voice-onboard` first, then return to this skill."

Do not proceed past this check if the dependency is missing.

Strategy design is genuinely strategic — it's not a form-filling exercise. Allocate real time with the exec (~30-60 minutes). The quality of the strategy files downstream (research-topics, suggest-topic, drafting skills) depends entirely on the specificity of the decisions made here.

---

## Required inputs

Have the following ready before invoking:

1. **Already-populated voice layer** — `writing-system/voice.md` (status: populated) and at least one `writing-system/audience/<slug>.md`. These are produced by `/voice-onboard`.

2. **Time with the exec** — approximately 30-60 minutes. Strategy intake is genuinely strategic, not mechanical. Rushing produces generic domain names that defeat the skill's purpose downstream.

3. **Optional: existing publishing history** — any prior posts, newsletter issues, or content archives. Helpful for Phase 4 (commercial mapping) and Phase 5 (cadence calibration). If the exec has been publishing, past patterns are better than guessing.

4. **Optional: commercial offers list** — what the exec sells (or plans to sell): services, products, courses, advisories. Populates Phase 4's offer table. Can be extracted interactively if not prepared in advance.

If any required input is missing, prompt for it before proceeding.

---

## Output paths

| Phase | File | Action |
|---|---|---|
| Phase 1 | `{{VAULT_NAME}}/writing-system/strategy/domains.md` | Replace blank scaffolding with populated domain definitions |
| Phase 2 | `{{VAULT_NAME}}/writing-system/strategy/pillars.md` | Replace blank scaffolding with populated pillar table per domain |
| Phase 3 | `{{VAULT_NAME}}/writing-system/strategy/audience-mapping.md` | Replace blank scaffolding with populated audience-domain matrix + pairing rules |
| Phase 4 | `{{VAULT_NAME}}/writing-system/strategy/commercial-mapping.md` | Replace blank scaffolding with populated offer table + domain CTA posture |
| Phase 5 | `{{VAULT_NAME}}/writing-system/strategy/cadence.md` | Replace blank scaffolding with populated cadence table + production-load math |
| Phase 6 | `{{VAULT_NAME}}/writing-system/strategy/distribution.md` | Replace blank scaffolding with populated distribution matrix + per-domain repurposing notes |
| Phase 7 | `{{VAULT_NAME}}/writing-system/strategy/voice-frame.md` | Replace blank scaffolding with per-domain voice flavor, anchor moves, and domain-specific kill-list additions |
| Phase 8 | `{{VAULT_NAME}}/writing-system/engine/editorial-filter.md` | Refresh Filter 1 domain table only — preserve Filter 2 quality criteria exactly as written |
| Phase 9 | (verification — no file written) | Test run of `/suggest-topic`; surface 1-paragraph strategy summary to exec |

---

## Resumability

This skill is **checkpointed per phase.** Phases 1-7 write incrementally as data arrives — the EA does not need to complete the entire intake in one sitting.

If the exec is pulled away mid-flow:
- All phases completed so far have been written to disk.
- Re-invoking the skill resumes from the next un-populated phase.
- The skill detects which files have `status: populated` in frontmatter and skips them.
- Do NOT hold strategy data in memory across interruptions — write each phase to disk before moving to the next.

The dependency check (voice + audience populated) still runs on re-invocation but will pass if voice-onboard has already run.

---

## Workflow

### Phase 1: Domain definition

**Purpose.** Identify the 2-4 content areas the exec wants to own. Domains are stable, recurring content streams with a clear identity, audience, and editorial purpose. They sit above pillars (sub-topics) and anchor everything downstream.

**Questions to ask the exec:**

1. *"What 2-4 areas do you want to be known for — where do you have the most lived experience, the strongest opinions, and the highest concentration of receipts?"*
2. *"For each area: what is the commercial or authority rationale? Why does running this content stream serve the business?"*
3. *"Which of your existing audiences primarily consumes this domain? (Cross-reference the audience pages already populated by `/voice-onboard`.)"*

**For each domain, capture:**
- Name (descriptive, 3-5 words)
- Slug (kebab-case, canonical — used in draft frontmatter and skill calls)
- One-line definition (what the domain covers; not a mission statement — a clear editorial scope)
- Why this domain (commercial + authority rationale in 2-4 sentences)
- Audience served (which audience page(s) this domain serves primarily)
- Filter check (brief: is material available? Is the audience specific? Is there a commercial connection?)

**Surface a pillar tension check before writing:** A domain is correctly scoped if a piece can clearly be tagged to it, but there are at least 3-4 distinct sub-topics (pillars) the exec can write about. If a domain is too narrow to generate sub-topics, expand it. If it's so broad it contains everything, split it.

**Write to `{{VAULT_NAME}}/writing-system/strategy/domains.md`:**
- Replace the blank scaffolding entirely.
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.
- Include a domain map summary table at the end (domain | slug | primary audience | commercial driver).

Reference [[writing-system/_examples/sample-exec/strategy/domains]] as the quality target for section depth and boundary notes.

---

### Phase 2: Pillar definition

**Purpose.** For each domain, define 3-4 pillars (recurring sub-topics). Pillars are granular enough that a piece can clearly tag one, but broad enough that the exec can write 5+ pieces about each over time. A pillar with only 2 possible pieces is too narrow; a pillar that contains half the domain is too broad.

**Questions to ask:**

1. *"Within [Domain Name], what are the 3-4 distinct angles you return to most? What sub-problems does this domain contain?"*
2. *"What would a piece that's clearly in Pillar A but not Pillar B look like? Can you tell them apart?"* (Pillar tension test — surfaced interactively if the distinctions feel fuzzy.)

**For each pillar, capture:**
- Name (descriptive)
- Slug (kebab-case, canonical — used verbatim in skill calls and draft frontmatter `pillar:` field)
- One-line definition (what pieces in this pillar are about; what they are NOT about to distinguish from neighboring pillars)

**Surface pillar design notes** (one paragraph per domain after the table): why the three pillars cover the domain's territory without overlapping. Mirrors the quality of the sample-exec example.

**Write to `{{VAULT_NAME}}/writing-system/strategy/pillars.md`:**
- Replace blank scaffolding entirely.
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.
- Include a canonical slug reference table at the top (domain | pillar | slug).

---

### Phase 3: Audience-domain mapping

**Purpose.** Assign each domain to a primary audience. Resolve production rules when multiple content streams coexist. Clarify when domains pair (companion pieces for multiple audiences) and when they stay single-stream.

**Questions to ask:**

1. *"For each domain — which of your audiences is the primary reader? Who is this content stream designed to serve first?"*
2. *"Are any domains genuinely dual-audience — where two different audiences are each a primary reader, not just an incidental reader?"* (Note: dual-primary-audience domains are valid but should be identified explicitly rather than left ambiguous.)
3. *"When would you deliberately write two companion pieces on the same topic — one for each audience? What conditions trigger that?"*
4. *"When would you never pair? What stays single-stream?"*

**Note on dual-audience domains:** Some domains serve two audiences as co-primary (e.g., Sarah Chen's D3 `founder-as-builder` serves both SaaS founders and IC-to-leadership transitioners as equal primary readers). If the exec has one of these, document it explicitly rather than forcing a single-primary assignment that misrepresents the content.

**Write to `{{VAULT_NAME}}/writing-system/strategy/audience-mapping.md`:**
- Replace blank scaffolding entirely.
- Populate the domain → audience matrix table.
- Document the pairing rule, with "when to pair deliberately" and "when NOT to pair" subsections.
- Note implications for production load (does a dual-stream mean double the pieces, or is one stream primary and one incidental?).
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

---

### Phase 4: Commercial mapping

**Purpose.** Map each domain to its commercial role. Drafting skills use this to select the right CTA posture per piece. Some domains convert directly; some warm up readers for later conversion; some are pure brand/authority plays.

**Questions to ask:**

1. *"What are your commercial offers — everything you sell or plan to sell? Include pre-launch or in-development offers."*
2. *"For each domain: when a reader finishes this piece, what's the right next step? Direct CTA (book a call, buy, demo)? Soft pointer (here's where to learn more)? No commercial mention at all?"*
3. *"Are any domains pure thought leadership — no commercial pull, brand-only? That's a valid choice; flag it explicitly."*

**For each domain, document:**
- Direct CTA target (which offer, if any, this domain converts toward directly)
- Indirect warm-up (which offers this domain seeds without a direct ask)
- CTA posture per domain: direct CTA native / soft pointer / indirect commercial / no commercial mention
- Whether the domain is pure thought leadership (brand-only)

**Write to `{{VAULT_NAME}}/writing-system/strategy/commercial-mapping.md`:**
- Replace blank scaffolding entirely.
- Populate the offers table and the domain → commercial mapping table.
- Add per-domain CTA posture description.
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

---

### Phase 5: Cadence

**Purpose.** Set yearly long-form targets per domain and validate the total production load is sustainable. Cadence decisions map to business goals (high cadence = top-of-funnel awareness; low cadence = evergreen or opportunistic).

**Questions to ask:**

1. *"How many long-form pieces per year feels sustainable for each domain? Be honest about bandwidth, not aspirational."*
2. *"Which domains are on a scheduled rhythm (consistent publish cadence) vs. opportunistic (only when material exists)?"* (Opportunistic cadence is valid for domains where receipts are scarce or where forcing output would thin quality.)
3. *"What's the primary publishing vehicle — newsletter, LinkedIn, X? What's the expected cadence of that vehicle?"*

**Production-load math — validate after collecting targets:**
- Sum total pieces/year across all domains.
- Divide by 52 to get pieces/week average.
- Confirm: is this load sustainable given current writing-system capacity? If a founder claims 40 long-form pieces/year without an EA or ghostwriter, flag it.
- If total load is too high, ask the exec to reduce targets before writing the file.

**Cadence modes:**
- **Scheduled** — consistent rhythm, predictable publish frequency within the domain.
- **Opportunistic** — published when strong material exists; no fixed cadence commitment. Use for domains where the receipts must come first and can't be manufactured.

**Write to `{{VAULT_NAME}}/writing-system/strategy/cadence.md`:**
- Replace blank scaffolding entirely.
- Include cadence table, production-load math, funnel logic, and per-pillar volume targets (indicative).
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

---

### Phase 6: Distribution

**Purpose.** Map which channels carry each domain and define the repurposing chain (how a long-form source piece compresses into shorter formats per channel). Drives the `repurposing` skill and informs production scheduling.

**Questions to ask:**

1. *"Which channels do you run? List everything: newsletter, LinkedIn, X (threads, long-form, shorts), email broadcasts, landing pages."*
2. *"For each domain — which channels does it always go to? Which channels are selective (some pieces, intentionally chosen)? Which channels never carry this domain?"*
3. *"Any per-domain distribution restrictions?* For example: 'D3 stays out of X — it's founder-personal content and I don't want it to go viral' is a valid restriction to document."*
4. *"For each domain: what does the repurposing chain look like? Does every long-form piece spawn a LinkedIn post? An X thread?"*

**Write to `{{VAULT_NAME}}/writing-system/strategy/distribution.md`:**
- Replace blank scaffolding entirely.
- List channels the exec runs.
- Populate the distribution matrix table (domain × channel; use ✅ always / ⚠️ selective / ❌ rarely-never).
- Add per-domain repurposing notes.
- Add production-load implications table (outputs per piece × annual domain volume).
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

---

### Phase 7: Voice frame

**Purpose.** Specify, per domain, which of the exec's voice signature moves lean heaviest and which pull back. Add any domain-specific kill-list items (patterns banned only in this domain even if acceptable globally). This file does NOT override `writing-system/voice.md` — the global voice is consistent. This is a per-domain layer applied on top.

**Questions to ask:**

1. *"In [Domain Name] — how would you describe the tone relative to your other domains? More technical? More confessional? More prescriptive?"*
2. *"Which of your rhetorical moves do you lean on most in [Domain Name]? (Reference voice.md anchor moves section.)"*
3. *"Are there moves you usually use that don't fit well in [Domain Name]?"*
4. *"Is there anything you'd never write in [Domain Name] that you might write elsewhere — patterns that feel wrong specifically for this domain?"*

**For each domain, capture:**
- Voice flavor (1-2 sentences — the overall tone and density of the domain)
- Moves leaned on (3-5 bullet points — specific rhetorical moves from voice.md that appear most often in this domain)
- Moves leaned away from (what does NOT dominate this domain even if it's in the global voice)
- Domain-specific kill-list additions (patterns banned ONLY in this domain — label as domain-specific, not global)

**Load order note to include in the file:** Drafting skills should load voice in this order: (1) voice.md global frame → (2) kill-list.md global kill list → (3) audience/<slug>.md → (4) this file, domain-specific section.

**Write to `{{VAULT_NAME}}/writing-system/strategy/voice-frame.md`:**
- Replace blank scaffolding entirely.
- Include voice frame summary table and per-domain sections.
- Update `status: blank` → `status: populated` in frontmatter.
- Update `updated:` to today's date.

---

### Phase 8: Editorial filter refresh

**Purpose.** Activate the editorial filter for this exec by replacing the placeholder domain table in `engine/editorial-filter.md` with the actual domains and slugs defined in Phase 1. This makes `/research-topics` and `/suggest-topic` use real domain gating.

**Steps:**

1. Read `{{VAULT_NAME}}/writing-system/strategy/domains.md` (just populated in Phase 1).
2. Read `{{VAULT_NAME}}/writing-system/engine/editorial-filter.md`.
3. Locate the **Filter 1: Domain fit** table — the one containing the placeholder comment `<!-- populated by /content-strategy-onboard from strategy/domains.md -->`.
4. Replace ONLY the Filter 1 table rows with the actual domains and slugs. Format:

```markdown
| Domain | Slug | Test |
|---|---|---|
| [D1 name] | `[d1-slug]` | Does the candidate idea sit within [brief one-line scope of D1]? |
| [D2 name] | `[d2-slug]` | Does the candidate idea sit within [brief one-line scope of D2]? |
| [D3 name] | `[d3-slug]` | Does the candidate idea sit within [brief one-line scope of D3]? |
```

5. **PRESERVE Filter 2: Quality criteria exactly as written.** Do not modify the 6 scoring criteria, the threshold (≥24/30), or the "Where this is loaded" and "Tie-in" sections. These are universal and belong to no specific exec.
6. Update `updated:` in frontmatter to today's date.

**Surface to user after writing:** "Editorial filter is now active. `/research-topics` and `/suggest-topic` will use these domain definitions to gate candidate ideas."

---

### Phase 9: Verification

**Purpose.** Confirm the strategy layer populated correctly and is readable by downstream skills.

**Test run:**

Invoke `/suggest-topic` (or simulate the invocation if live call is not available) against the populated strategy + an empty content-graph (no takes, stories, or ideas yet populated).

**Expected result:** A response indicating no content-graph material exists — something like:

> "No recent takes or stories in content-graph to suggest from. Populate via `/content-ingest` first."

This is a **SUCCESS signal.** It confirms that `/suggest-topic` loaded the strategy correctly, found real domain definitions, and correctly reported that the content-graph is empty. A success here means the strategy files have valid frontmatter, populated domains, and correct file paths.

**Failure signals** (surface these to the user if seen):
- `/suggest-topic` returns garbage suggestions or domain names that don't match what was just defined → strategy files may have invalid frontmatter or the wrong status field. Check `status: populated` in each file.
- `/suggest-topic` fails to load the strategy at all → check file paths and vault name substitution.

**Final surface to exec (or EA relaying):**

Produce a 1-paragraph strategy summary:

> "[Exec name]'s content strategy is live. [N] domains defined: [D1 name], [D2 name], [D3 name]. [Total pillar count] pillars across all domains. Target cadence: [total pieces/year] long-form pieces/year ([D1 N]/[D2 N]/[D3 N] per domain). Primary channels: [list]. Editorial filter is active. Confirm this is right or identify what needs adjustment before running `/research-topics`."

If the exec asks for changes at this stage, return to the relevant phase, update the file, and re-run Phase 8 (filter refresh) before closing.

---

## Cross-skill relationships

| Skill | Relationship |
|---|---|
| `/onboard` | Runs BEFORE this skill. Sets up the vault's knowledge layer. The exec's context must be populated before strategy intake makes sense. |
| `/voice-onboard` | Runs BEFORE this skill. Hard dependency — voice.md and at least one audience page must be populated before strategy design can proceed. Voice defines who the exec is; strategy defines what they'll write about. |
| `/research-topics` | Runs AFTER this skill. Consumes `strategy/domains.md` and `strategy/pillars.md` when filtering external trending content for fit. Without populated strategy files, research-topics has no domain gating — every topic passes. |
| `/suggest-topic` | Runs AFTER this skill. Consumes domains, pillars, cadence, and audience-mapping for cadence-aware topic ranking. Phase 9 of this skill tests suggest-topic as the verification step. |
| `/content-ingest` | Runs AFTER this skill (ongoing). Takes transcripts and voice memos and extracts takes/stories into `content-graph/`. The content-graph is what suggest-topic and research-topics draw from; content-strategy-onboard defines the filters those skills apply. |
| `/long-form-writing`, `/email-writing`, `/landing-page-writing`, `/repurposing` | All drafting skills load `strategy/voice-frame.md` per-domain on top of the global voice + kill list. Without a populated voice-frame.md, drafting skills default to global voice with no per-domain layer. |
| `/lint` | After running `/content-strategy-onboard`, `/lint` Phase 5 (Index Health) checks for un-populated strategy files. `status: blank` in any strategy file after this skill has run is flagged as a lint error. |

---

## Output summary format

At the end of a successful skill run, report back:

```
Content strategy onboard complete.

Strategy files populated:
- writing-system/strategy/domains.md — N domains (was: blank)
- writing-system/strategy/pillars.md — N pillars across N domains (was: blank)
- writing-system/strategy/audience-mapping.md — populated (was: blank)
- writing-system/strategy/commercial-mapping.md — N offers, N domains mapped (was: blank)
- writing-system/strategy/cadence.md — N long-form pieces/year total (was: blank)
- writing-system/strategy/distribution.md — N channels (was: blank)
- writing-system/strategy/voice-frame.md — N domain voice frames (was: blank)
- writing-system/engine/editorial-filter.md — Filter 1 refreshed with N domains (Filter 2 preserved)

Verification:
- /suggest-topic test: [SUCCESS — returned empty content-graph signal | FAILURE — see details]

Strategy summary:
[1-paragraph summary produced in Phase 9]

Next step:
- Run /research-topics [slug] to start populating ideas for a specific domain.
- Run /content-ingest <transcript> to start populating takes and stories into the content-graph.
- Run /suggest-topic once content-graph has material to get cadence-aware topic recommendations.
```
