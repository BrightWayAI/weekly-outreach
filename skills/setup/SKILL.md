---
name: setup
description: Configure weekly-outreach for your ICP, CRM, voice, and companion-plugin integrations. Auto-fires on "/setup-outreach", "set up weekly-outreach", "configure outreach prep", or when /weekly-outreach reports user-context.md is missing.
---

See `commands/setup-outreach.md` for the full interview.

## When this skill fires

- User runs `/setup-outreach` directly
- User says: "set up weekly-outreach", "configure my weekly outreach", "configure outreach prep"
- The `/weekly-outreach` command reports user-context.md is missing → auto-route here

## Quick path

If the user wants minimum-viable defaults to start: write a placeholder `<config-root>/plugins/weekly-outreach.user-context.md` with weekly target 10–12, CRM "none," generic ICP, default banned phrases. The command will work but output will be generic. Recommend running the full interview before relying on it for real outreach.
