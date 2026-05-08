# Changelog

All notable changes to weekly-outreach are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/). Versions match `plugin.json`.

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
