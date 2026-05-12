# Changelog

All notable changes to weekly-outreach are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/). Versions match `plugin.json`.

## [0.2.4] — Person-page side effect (2026-05-12)

### Added
- **Person-page Recent-interactions append (Step 9).** After the queue is approved and CRM tasks / calendar placeholders are created, weekly-outreach appends a `<today> — queue-add — week of <week-start>: <channel>, <ask shape>` line to each queued contact's cortex person page if one exists at `<config-root>/memory/person/<slug>.md`. Updates Last meaningful contact in Relationship.
- **Graceful degradation.** No-op if cortex isn't installed or the contact has no graduated page. Doesn't graduate new pages — only updates existing.

### Why this matters
Phase 3 of SECOND-BRAIN-V2-SPEC. Weekly outreach was previously invisible at the person-page level; the queue gets re-built every week without leaving a trail on the people it touched. This side effect closes that loop additively.

## [0.2.3] — Platform-agnostic Step 0 (2026-05-12)

### Changed
- **Setup command Step 0 now platform-agnostic.** Every `request_cowork_directory(...)` call is conditional: "In Cowork, call `request_cowork_directory(...)`. In Claude Code (or any environment with direct filesystem access), no mount is needed." Same plugin source works in both runtimes.

### Why this matters
Phase 0 of SECOND-BRAIN-V2-SPEC. Removes the implicit Cowork-only assumption so Claude Code users do not hit unsupported tool calls during setup.

## [0.2.0] — Config-root refactor

### Changed
- **Plugin config moved to a user-chosen folder.** Reads and writes now go to `<config-root>/plugins/weekly-outreach.user-context.md`, where `<config-root>` is the folder the user chooses on first plugin setup (recorded at `~/Documents/.claude-plugin-config-root`).
- **`/setup-outreach` Step 0 bootstraps the config root.** Resolves the pointer; prompts for the root on first run; reads shared identity + voice; offers to migrate legacy config and pre-staged files.
- **All operating commands and skills** read from the new path.
- **User-facing prompts debranded** for fork-friendliness.

## [0.1.0] — Initial release

### Added
- Weekly relationship management and BD prep slash command (`/weekly-outreach`).
- Pulls upcoming external meetings and builds call prep for each.
- Builds prioritized outreach queue (default 10–12 contacts).
- Optionally fills queue with net-new prospects via Apollo (per setup configuration).
- Runs each contact through a "should we even send?" filter.
- Drafts a full message per contact following the user's voice rules.
- Creates CRM tasks and 15-min calendar placeholder events after explicit user approval (calendar events use `sendUpdates: "none"` so attendees aren't pinged).
- Delegates pipeline analysis to `pipeline-analyst` subagent (in `core-ops`) when installed; falls back to direct CRM queries otherwise.
- Optionally deepens top 3–5 contacts via `contact-researcher` subagent (in `lead-engine`) for sharper "why now" reasoning.
- Confidence-aware delegation — pauses on Low confidence from delegated agents.
- Setup reads `~/Documents/Claude/identity.md` and `~/Documents/Claude/voice.md` (shared config from cortex) when available.
- Setup interview captures ICP, CRM custom property names, owner ID, deal pipeline stages, cadence tiers, weekly target.
