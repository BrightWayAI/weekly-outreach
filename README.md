# weekly-outreach

Weekly relationship management and business development prep, run as a Cowork slash command.

You walk away with: a prioritized outreach queue (10–12 contacts by default), call prep for the week's external meetings, drafted messages ready to copy/tweak, plus CRM tasks and calendar placeholders for accountability.

## What it does

- Pulls **upcoming external meetings** and builds call prep for each
- Builds a **prioritized outreach queue** from your CRM (delegates to `pipeline-analyst` if installed)
- Optionally fills the queue with **net-new prospects** via Apollo
- Runs each contact through a **"should we even send?" filter**
- Drafts a **full message per contact** following your voice rules
- Optionally **deepens the top contacts** with `contact-researcher` (if installed)
- Shows the whole plan in chat for review
- Creates **CRM tasks** and **calendar placeholder events** after you approve

## Install

Recommended: via the [BrightWayAI marketplace](https://github.com/BrightWayAI/claude-plugins).

```
/plugin marketplace add BrightWayAI/weekly-outreach
/plugin install weekly-outreach@weekly-outreach
```

## First-time setup

Run `/setup-outreach`. Captures:

- **Identity** — your name, company, what you do
- **ICP** — primary and secondary ICPs (titles, org types, sizes, regions)
- **CRM** — which CRM, your owner ID, deal pipeline stages, custom properties used for prioritization (e.g., `engagement_cadence`, `weekly_engagement_action`)
- **Cadence tiers** — how often each tier of contact should be touched (default: weekly / monthly / quarterly / dormant)
- **Voice and banned phrases** — feeds into drafting
- **Weekly target** — how many touches per week (default 10–12)
- **Apollo integration** — whether to use Apollo for net-new prospect fill-in

Saved to `references/user-context.md` (gitignored).

## Companion plugins

- **brightway-core** — provides the `pipeline-analyst` subagent for prioritization
- **lead-engine** — provides the `contact-researcher` subagent for top-contact deep-dives
- **bizdev-outreach** — shares voice rules; both can read each other's user-context for consistency
- **plan-tomorrow** — pulls outreach contacts from the weekly queue

Works without them, but the queue is rougher and drafts are less personalized.

## What's inside

```
.claude-plugin/plugin.json
commands/
  weekly-outreach.md         Slash command
  setup-outreach.md          Interview
skills/
  weekly-outreach/SKILL.md   Auto-fires on outreach phrases
  setup/SKILL.md             Auto-fires on setup phrases
references/
  user-context.template.md   Structure (committed)
  user-context.md            Your config (gitignored)
```

## License

MIT.
