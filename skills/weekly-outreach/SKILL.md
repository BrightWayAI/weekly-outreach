---
name: weekly-outreach
description: Run weekly relationship management and BD prep. Auto-fires on "/weekly-outreach", "run my weekly outreach", "do my outreach prep", "weekly prep", "outreach canvas", "prep my week", "who should I reach out to this week", "Monday outreach", "weekly relationship management", or any variation involving weekly business development planning. Pulls from CRM, email, and calendar; presents the plan in chat; commits to CRM tasks and calendar after your approval.
---

See `commands/weekly-outreach.md` for the full workflow.

## When this skill fires

- User runs `/weekly-outreach` directly
- User says: "run my weekly outreach", "do my outreach prep", "weekly prep", "prep my week", "who should I reach out to this week"
- User references their Monday outreach routine
- A scheduled task triggers this (when wired up in Cowork)

## Pre-flight check

Confirm `<config-root>/plugins/weekly-outreach.user-context.md` exists. If missing, route to `/setup-outreach` first — without ICP, CRM properties, and voice rules, the output is generic.

## What this skill is *not* for

- Drafting outreach for a single contact — that's `bizdev-outreach` (or `lead-engine`).
- Building a long list — the weekly target is a small, executable queue. If you need bulk, run Apollo searches separately.
- Modifying existing CRM data beyond creating new tasks. Read-only on existing records.
