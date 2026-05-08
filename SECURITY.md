# Security Policy

## What this plugin does with your data

Weekly Outreach builds a prioritized BD plan from your CRM and calendar, drafts messages, and creates CRM tasks + calendar placeholders only after you approve. Read-most-things; write-with-confirmation.

**Reads:**
- **CRM** — contacts, deals, custom properties (e.g., `engagement_cadence`, `weekly_engagement_action`), recent activity.
- **Email** (Gmail) — last threads per contact for context.
- **Calendar** — upcoming external meetings for call prep.
- **Apollo** (if connected and enabled) — net-new prospect candidates matching your ICP.
- **Plugin references** — `references/user-context.md`.
- **Shared user-level config** — `~/Documents/Claude/identity.md`, `~/Documents/Claude/voice.md` (read-only).

**Writes (all behind explicit user approval):**
- **CRM tasks** — `EMAIL` task per priority outreach contact, due Monday of the outreach week. Created via the CRM connector after you confirm a presented table.
- **Calendar events** — 15-min placeholder reminders at your preferred outreach window. **Always created with `sendUpdates: "none"`** so attendees aren't pinged.
- **Plugin user-context** — `references/user-context.md` (after `/setup-outreach`).

**Does not:**
- **Edit existing calendar events.** Strictly read-only on existing events. Only creates new placeholder blocks.
- **Send any messages on your behalf.** Drafts go in CRM tasks for you to send manually (or via your email client).
- **Bypass the "should we even send?" filter.** Contacts in HOLDING PATTERN are surfaced with reasons; the user can override per contact.
- **Auto-write to CRM without confirmation.** A confirmation table is presented before any task creation.

## Where data lives

- Plugin reference files inside the installed plugin directory.
- Optional weekly archive at `runs/[date].md` (gitignored — local only).
- Shared identity/voice (read-only) at `~/Documents/Claude/`.

## What gets sent off your machine

- Whatever your authorized CRM, Gmail, calendar, and Apollo connectors send when invoked.

## Supported versions

| Version | Supported |
|---------|-----------|
| 0.1.x   | Yes       |

## Reporting a vulnerability

Report privately via GitHub Security Advisories:

https://github.com/BrightWayAI/weekly-outreach/security/advisories/new

Do not open a public issue for security concerns. We aim to respond within 5 business days.
