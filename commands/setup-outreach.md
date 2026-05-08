---
description: Configure weekly-outreach for your ICP, CRM properties, voice rules, and companion-plugin integrations. Writes results to references/user-context.md so the weekly prep adapts to your firm. Re-run anytime to update.
---

# /setup-outreach

Short interview that captures what weekly-outreach needs to actually be useful for you.

---

## Pre-step — Read shared identity (if available)

Before asking identity-style questions (name, company, role, primary tools), check whether `~/Documents/Claude/identity.md` exists. This is a shared identity file populated by cortex's `/setup-identity` command — every BrightWayAI marketplace plugin reads it.

- **If it exists and is populated:** read it. Use the values to pre-fill Section 1 (Identity) of this interview. Skip those questions; just confirm what you read.
- **If it doesn't exist:** offer the user:
  > "There's a shared identity file (`/setup-identity` in cortex) that other plugins read too — capture name/company/role/tools once and every plugin uses it. Want to run `/setup-identity` first (recommended, ~2 min), or capture identity inline here only?"
  - "Run /setup-identity first" → route there, then resume.
  - "Inline" → proceed normally.

## Pre-step 2 — Read shared voice (if available)

After identity, check whether `~/Documents/Claude/voice.md` exists. This is a shared writing-voice file populated by cortex's `/setup-voice` command — used by every drafting plugin (bizdev-outreach, weekly-outreach, lead-engine, news-curator) so voice stays consistent.

- **If it exists and is populated:** read it. Use those values to pre-fill Section 5 (Voice and banned phrases) of this interview. Skip those questions; just confirm.
- **If it doesn't exist:** offer:
  > "Want to capture your writing voice once via `/setup-voice` (in cortex)? It saves to a shared file every drafting plugin reads — voice stays consistent across channels and you only update in one place. Or proceed inline here?"
  - "Run /setup-voice first" → route there, then resume.
  - "Inline" → proceed normally.

---

## Step 1 — Check for existing config

Read `references/user-context.md`. If populated → ask whether to update or restart. If missing → start fresh.

---

## Step 2 — The interview

One section at a time. Confirm before moving on.

### Section 1 — Identity
- Your name
- Your company
- One-sentence description of what your company does
- Your weekly outreach target (default 10–12 touches)

### Section 2 — ICP
- **Primary ICP** — titles + org types + size range + region (e.g., "Director/VP/C-suite at nonprofits and ed-orgs, 20–200 staff, US")
- **Secondary ICP** — same shape, less hot
- Anything explicitly out-of-ICP you want to never surface

### Section 3 — CRM
- Which CRM? (HubSpot / Salesforce / Pipedrive / Attio / other / "none")
- Your CRM owner ID
- **Deal pipeline stages, in order from earliest to latest** (e.g., "Initial Contact → Discovery → Proposal Sent → Negotiation → Verbal Yes → Closed")
- **Custom contact properties used for prioritization:**
  - Cadence/tier property (e.g., `engagement_cadence`)
  - Cadence values (e.g., "Tier A weekly / Tier B monthly / Tier C quarterly / Dormant / Do Not Engage")
  - Relationship type property (e.g., `relationship_type`)
  - Suggested action property (e.g., `weekly_engagement_action`)
  - Activity-flag properties (e.g., `needs_activity_this_week`, `weekly_activity_complete`)

### Section 4 — Cadence definitions
For each tier, capture:
- **Weekly tier:** name, how-often (e.g., "every 7 days"), what triggers a touch
- **Monthly/strategic tier:** name, how-often (e.g., "every 60 days")
- **Quarterly/passive tier:** name, how-often (default 90 days)
- **Dormant:** revisit-after (default 90 days)
- **Do not engage:** any explicit conditions

### Section 5 — Voice and banned phrases
- Three words describing your voice
- Banned phrases beyond the defaults (the command's defaults already include "just checking in," "circling back," etc.)
- Sentence length preference — short and punchy / mixed / longer
- Sign-off / CTA style

### Section 6 — Apollo and net-new prospecting
- Is Apollo connected? (Y/N)
- If yes: cap on net-new prospects per week (default 5)
- Sources you want surfaced beyond raw prospects (events, LinkedIn engagements, intro requests, seasonal hooks)

### Section 7 — Companion plugins
- Is `core-ops` installed? (Y/N — drives pipeline-analyst delegation)
- Is `lead-engine` installed? (Y/N — drives contact-researcher delegation)
- Is `bizdev-outreach` installed? (Y/N — share voice rules with that plugin's user-context if so)
- Is `plan-tomorrow` installed? (Y/N — surface that the weekly queue feeds the daily plan)

---

## Step 3 — Write the config

Populate `references/user-context.md`:

```markdown
# weekly-outreach user context

_Last updated: [date]_

## Identity
- **Name:** ...
- **Company:** ...
- **What we do:** ...
- **Weekly target:** ...

## ICP
- **Primary:** ...
- **Secondary:** ...
- **Out-of-ICP:** ...

## CRM
- **Tool:** ...
- **Owner ID:** ...
- **Deal pipeline stages:** ...
- **Cadence property:** ...
- **Cadence values:** ...
- **Relationship type property:** ...
- **Suggested action property:** ...
- **Activity-flag properties:** ...

## Cadence
- **Weekly tier:** ...
- **Monthly tier:** ...
- **Quarterly tier:** ...
- **Dormant revisit:** ...
- **Do not engage rules:** ...

## Voice
- **Three words:** ...
- **Additional banned phrases:** ...
- **Sentence length:** ...
- **Sign-off / CTA:** ...

## Apollo
- **Enabled:** ...
- **Weekly net-new cap:** ...
- **Strategic-recommendation sources:** ...

## Companion plugins
- **core-ops (pipeline-analyst):** ...
- **lead-engine (contact-researcher):** ...
- **bizdev-outreach:** ...
- **plan-tomorrow:** ...
```

---

## Step 4 — Confirm and offer next step

Summarize. Offer:
> "Run `/weekly-outreach` Monday morning to see your plan."

---

## Behavior rules

- One section at a time.
- Skip sections that don't apply.
- Idempotent — re-running updates rather than restarts.
