# Atlas Second Brain Template

A starter template for an executive's AI-powered second brain — an Obsidian vault wired into Claude Code. Delivered as part of the Atlas AI Workspace Setup.

Learn more about Atlas: https://atlasassistants.com

## What's Inside

- `CLAUDE.md` — operating manual Claude Code reads on every session. Fill in the executive's details (search for `{{` placeholders).
- `RESOLVER.md` — deterministic routing table the ingest skills consult before creating any new page.
- `SETUP.md` — EA-facing setup runbook (intake → clone → fill placeholders → `/second-brain-onboard` → `/voice-onboard` → `/content-strategy-onboard` → schedule dream-cycle).
- `context/` — placeholder pages: `user.md`, `company.md`, `icp.md`, `brand.md`, `team.md`. Fill these in during intake.
- `knowledge/` — synthesized knowledge graph, split by entity type:
  - `people/`, `companies/`, `tools/`, `concepts/`, `comparisons/`
  - `_index.md` — catalog populated by ingest skills
- `projects/` — active and archived projects. `project-index.md` is the catalog.
- `areas/` — example areas of responsibility:
  - `content/`, `finances/`, `operations/`, `product/`, `strategic-planning/`
  - `operations/automations.md` — registry of every scheduled / event-triggered automation
- `meetings/`, `inbox/`, `sessions/` — load-bearing capture directories.
- `reports/` — `daily/`, `weekly/`, `monthly/`, `dream-cycle/`, `onboard/`.
- `writing-system/` — voice + audience + kill-list + frameworks + channels + content graph + drafting skills. Per-exec scaffolding populated by `/voice-onboard` and `/content-strategy-onboard`. Includes a worked sample-exec example (Sarah Chen / Gridline) at `writing-system/_examples/sample-exec/`.
- `.claude/skills/` — 16 skills shipped in this template (see below).
- `scripts/` — maintenance scripts (Atlas-internal: `port-skills-from-colin-brain.sh`; reference: `migrate-meeting-frontmatter.py`).

## Getting Started

1. **Clone** into your preferred location (default: `~/brain/`):

   ```bash
   git clone https://github.com/atlasassistants/atlas-second-brain-template.git ~/brain
   cd ~/brain
   ```

2. **Open** the folder as a vault in [Obsidian](https://obsidian.md).

3. **Fill placeholders** — search for `{{` to find them across:
   - `CLAUDE.md`
   - `context/user.md`, `context/company.md`, `context/team.md`
   - Skill Configuration blocks (`grep -lR '{{VAULT_OWNER' .claude/skills/`)

   See `SETUP.md` for the full placeholder list.

4. **Install** [Claude Code](https://docs.anthropic.com/claude/claude-code) and launch from the vault root:

   ```bash
   cd ~/brain
   claude
   ```

5. **Run the onboarding family in order:**
   - **`/second-brain-onboard`** — imports your meeting history, pre-populates your people graph, and bulk-ingests historical meetings.
   - **`/voice-onboard`** — extracts the exec's voice signature, ICP, and kill-list from intake material. Verifies with a sample email draft.
   - **`/content-strategy-onboard`** — defines content domains, pillars, audience-domain mapping, cadence, distribution, and voice frame. Refreshes the editorial filter against your domains.

6. **Schedule the dream-cycle** — see `SETUP.md` for launchd (macOS) / cron (Linux) / Task Scheduler (Windows) instructions.

7. (Optional) Enable [Obsidian Sync](https://obsidian.md/sync) for real-time multi-device access.

8. (Recommended) Install the [Obsidian Git](https://github.com/Vinzent03/obsidian-git) plugin and configure auto-commit + push every 5 minutes to a private Git repo you own. This enables Claude Code scheduled / cloud automations and acts as version history.

## Full Workspace Setup

This template is one piece of the Atlas AI Workspace Setup, which also covers IDE setup, Claude Code plugins, and Composio integrations. Atlas clients get the full setup delivered by their matched EA or the Atlas core team.

## Skills Included

**Onboarding family (run once after clone, in order):**
- **`/second-brain-onboard`** — One-time cold-start: validates context, imports historical meetings, pre-creates people pages, runs bulk ingest.
- **`/voice-onboard`** — Voice intake. Populates voice + audience + kill-list. Verifies with sample email draft.
- **`/content-strategy-onboard`** — Strategy intake. Populates 8 strategy files + refreshes editorial filter.

**Knowledge layer (ongoing):**
- **`/meeting-ingest <path>`** — Process a meeting note into people timelines, entity timelines, and project action candidates.
- **`/report-ingest <path>`** — Process a daily/weekly/monthly report into project + area updates.
- **`/knowledge-ingest <path>`** — Process raw captures (inbox items, articles) into synthesized knowledge pages.

**Writing system (drafting + content graph):**
- **`/long-form-writing`** — Newsletter / X long-form / LinkedIn long-form drafting in the exec's voice.
- **`/email-writing`** — Promotional, broadcast, and sequence email drafting.
- **`/landing-page-writing`** — Landing / sales / offer page copy.
- **`/repurposing`** — Transform a long-form piece into platform-native short-mid form.
- **`/content-ingest <path>`** — Process transcripts / voice memos / pasted text into structured takes and stories.
- **`/research-topics`** — Pull external trending content aligned with strategy, score against editorial filter, write candidate ideas.
- **`/suggest-topic`** — Surface ranked topic recommendations from existing material. Cadence-aware in no-args mode.

**Maintenance:**
- **`/dream-cycle`** — Nightly maintenance pass (auto-ingest, lint --fix, freshness audit, session synthesis).
- **`/triage`** — Periodic cleanup of auto-flagged action candidates (7-class / 3-lane workflow).
- **`/lint`** — Audit and auto-fix vault health (frontmatter, wikilinks, indexes, typed-link reciprocity, freshness, content-graph health).

## Architecture References

This template implements the second-brain reference architecture: see [`docs/architecture.md`](docs/architecture.md).

Eight portable patterns: three-layer brain (captures + synthesized + health signals), RESOLVER routing, typed wikilinks + reciprocity, ingest-skill contracts (4 guarantees), dream cycle (nightly maintenance), triage cycle (7-class / 3-lane action-candidate cleanup), pre-creation strategy (cold start), migration pattern (legacy data adoption).
