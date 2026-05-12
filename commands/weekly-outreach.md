---
description: Weekly relationship management and BD prep. Pulls from CRM, email, and calendar; produces a prioritized outreach plan in chat (10–12 contacts by default), call prep for the week's external meetings, drafted messages, plus CRM tasks and calendar placeholders. Delegates pipeline analysis to pipeline-analyst and per-contact research to contact-researcher when installed.
---

# /weekly-outreach

End-to-end weekly outreach prep. The output stays in chat — review, iterate, then commit to CRM tasks and calendar placeholders only after you approve.

---

## Step 0 — Preflight

Read `<config-root>/plugins/weekly-outreach.user-context.md`. If missing, route to `/setup-outreach` and stop.

Extract:
- Identity (name, company, what you do)
- ICP (primary, secondary)
- CRM (tool, owner ID, custom property names, deal stages)
- Cadence tiers (weekly/monthly/quarterly/dormant definitions)
- Voice rules (banned phrases, tone)
- Weekly target (default 10–12)
- Apollo enabled? (yes/no)
- Companion plugins (core-ops for pipeline-analyst? lead-engine for contact-researcher? bizdev-outreach for shared voice rules?)

---

## Critical Rules

- **NEVER edit or update existing calendar events.** Existing events are strictly read-only.
- **Only CREATE new calendar events** — 15-minute placeholder blocks. Always `sendUpdates: "none"`.
- **Always present a confirmation table** before creating tasks or events. Wait for explicit approval.
- **Output stays in conversation** (no Slack canvas, no separate doc). The user reviews and iterates here.

---

## Step 1 — Gather this week's external calls

Query the calendar for Mon–Fri of the upcoming week. Identify external prospect/relationship calls:
- Attendees with domains other than your own
- Meeting titles suggesting prospect conversations (discovery, intro, catch-up, etc.)
- Exclude purely internal meetings

For each external call:
1. Look up the contact in the CRM (by email or name)
2. **If `contact-researcher` is available** (lead-engine installed): use the Task tool with `subagent_type="contact-researcher"`, purpose `"call-prep"`, time horizon 90d. Use the dossier for relationship summary and talking points.
3. **If not available:** search the CRM and Gmail directly for the 2–3 most recent threads with that person.
4. Prepare call prep: relationship summary (2–3 sentences), suggested focus, 3–4 discovery questions tailored to their org type and ICP segment.

---

## Step 2 — Build the outreach queue

**If `pipeline-analyst` is available** (core-ops installed): use the Task tool with `subagent_type="pipeline-analyst"` and pass:
- `user-context-path` — path to core-ops's user-context (or this plugin's, whichever is more current)
- `time-window` — 90 days
- `focus-filter` — "active deals + tier-A overdue + tier-B due + rewarm targets in 45–60d window"
- `top-n` — your weekly target (default 12)

The agent returns a ranked list with reasoning. Use that as your queue.

**Confidence check.** If `pipeline-analyst` returns `Confidence: Low` (e.g., "CRM connector returned partial data" or "user-context-path was missing scoring weights"), pause:

> "Pipeline analysis came back Low confidence: [specific gap]. The queue I build from this will be rougher. Want to fix the gap (e.g., re-run `/setup-core` or check CRM connection) and rerun, or proceed with what we have?"

If "proceed," continue but note the limitation in the final plan's PIPELINE SNAPSHOT section.

**If pipeline-analyst is not available:** query the CRM directly using the priority order from your user-context. Default order:

1. **Active deal contacts** — contacts associated with open deals.
2. **Tier-A contacts overdue** — engagement_cadence = weekly AND last_contacted ≥ 7d ago.
3. **Flagged for activity** — needs_activity_this_week = true AND weekly_activity_complete ≠ true.
4. **Rewarm targets** — last_contacted 45–60d ago, NOT in "do not engage" or "not a fit" status.
5. **Tier-B contacts due** — engagement_cadence = monthly AND last_contacted ≥ 55d ago.

For each contact, search Gmail for the last thread to capture conversation context.

---

## Step 3 — Fill the queue with net-new prospects (if needed)

If fewer than your weekly target after Step 2 *and* Apollo is enabled in user-context, fill the gap with net-new prospects.

Use Apollo (`apollo_mixed_people_api_search`, `apollo_mixed_companies_search`) with filters from your user-context's ICP definition: titles, org types, sizes, regions, industries.

**Mix it up:**
- Direct prospects (potential buyers)
- Connectors/referrers (consultants, foundation officers, vendors, board members)
- Recent industry events, conferences, or hooks (seasonal cycles, fiscal year, annual conferences)

Enrich each: email, title, company context, recent news or job changes that could serve as opening angle.

**Strategic recommendations** (always include if relevant):
- Contacts of contacts — warm intros worth requesting
- LinkedIn engagement targets — people posting in your space worth commenting on or DM-ing
- Seasonal hooks specific to your ICP

If Apollo isn't enabled or returns nothing, just deliver the shorter queue and surface the gap clearly.

---

## Step 3.5 — Apply the "should we even send?" filter

For each contact in the queue, check:
- Is the ball in their court? (they committed and haven't had time)
- Did your last message set a gracious tone that follow-up would undermine?
- Is there genuine new value to offer?
- Is it too soon based on their bandwidth signals?

Remove contacts where the answer is "don't send." Note them in **HOLDING PATTERN** with reason and revisit timeframe.

---

## Step 4 — (Optional) Deepen the top contacts via contact-researcher

For the top 3–5 highest-priority contacts (active deals + significantly overdue), if `contact-researcher` is available, delegate a deeper dossier.

For each, use the Task tool with `subagent_type="contact-researcher"`, purpose `"outreach"` (or `"re-engage"` for rewarms), 90d horizon. Use the dossier's:
- **Recent Public Signals** — sharpens "why now"
- **Three Talking Points** — seeds for the draft message
- **Suggested Next Step** — informs the message's CTA

**Confidence check per contact.** If a returned dossier is `Confidence: Low` AND key sections are empty, fall back to a thinner draft for that contact (use only what's in the CRM + last email thread). Note in HOLDING PATTERN that "research thin — verify context before sending." Don't pause and ask the user per contact — too disruptive at this scale.

Skip this step entirely on a quick refresh or for routine cadence touches.

---

## Step 5 — Draft messages

For each contact remaining in the queue, draft a full message ready to copy/tweak.

**Writing rules** (read voice section of user-context for additional rules and banned phrases):
- Lead with value, never with an ask
- Banned default phrases: "just checking in," "circling back," "touching base," "I hope this email finds you well," "per my last email," "at your earliest convenience," "synergy/leverage/align," "any luck with [X]?"
- Don't introduce new angles mid-thread — stick to existing context
- Mirror the contact's tone if prior correspondence exists; default to warm-but-professional if cold
- One clear, low-friction CTA per message
- Keep messages 3–5 sentences max
- Subject lines: specific to them, under 6 words, no clickbait

Match message type to context:
- **Deal follow-up** → advance the conversation, reference specific next step
- **Rewarm** → light touch, reference shared context or a relevant insight for their sector
- **Cold outreach** → lead with a specific observation about their org
- **Connector/referrer** → relationship nurture or genuine share, not an ask

---

## Step 6 — Present the outreach plan in conversation

Format for fast scanning. This is operational, not a report.

```
**CALL PREP** — [N] external calls this week
[per-meeting blocks: contact + deal stage + relationship summary + suggested focus + 3–4 discovery questions]

**PRIORITY OUTREACH** — [N] contacts
[per-contact blocks: name + title + org + why-now + last-contact + relationship type + cadence + suggested action + draft message]

**HOLDING PATTERN** — [N] contacts paused
[per-contact line: name + org + reason + revisit date]

**PIPELINE SNAPSHOT**
[quick table of active deals: name, stage, amount, last activity, next step]

**NET-NEW PROSPECTS** — [N] from Apollo (if used)
[per-prospect block: name + title + org + why-they-fit + opening angle + source]

**STRATEGIC RECOMMENDATIONS**
[broader outreach ideas: events, LinkedIn threads, intro requests, seasonal plays]
```

After presenting, ask if the user wants to adjust before committing. They can remove contacts, change priorities, tweak messages.

---

## Step 7 — Create CRM tasks (after approval)

For each contact in the priority queue, create an EMAIL task in the CRM:

- **Subject:** `Outreach: [Name] — [Org]`
- **Body:** full draft message + context (why now, last contact, relationship type, suggested action)
- **Due date:** Monday of the outreach week
- **Status:** NOT_STARTED
- **Type:** EMAIL
- **Priority:** HIGH for active deals + significantly overdue (30+d past cadence); MEDIUM otherwise
- **Owner:** your `crm-owner-id` from user-context
- **Association:** to the contact record

**Execution:**
1. Look up CRM IDs (parallel batch search by name/email)
2. Present a confirmation table — Contact, Org, Priority, Subject
3. Wait for explicit approval
4. Batch-create tasks (typical CRM API limit: 10 per request — split if needed)
5. Report successes and failures

---

## Step 8 — Create calendar placeholder events

For each priority contact, create a NEW calendar event as a send-email reminder.

- **Title:** `📧 Outreach: [Name] — [Org]`
- **Duration:** 15 minutes
- **Description:** priority + context (why now, last contact) + full draft message
- **Reminders:** 5-min popup for the first event of each day's batch; 0-min for subsequent events in the same block
- **sendUpdates:** always `"none"`

**Scheduling logic:**
1. Query the calendar for the outreach week to find existing events
2. Find open morning slots (9:00–11:00 AM ET preferred per user-context, or earlier if specified) that don't conflict
3. Stack outreach blocks in 15-min increments, starting at the earliest available slot each morning
4. Prioritize by urgency: P0 deal contacts on Monday morning first, then high-priority overdue, then medium/low later in the week
5. Avoid days with offsites or travel-day blocks

Present the proposed schedule. Wait for approval. Create.

---

## Reminder — Calendar rules

- NEVER edit or update existing events
- Only CREATE new events with `sendUpdates: "none"`
- Call prep for existing meetings stays in the outreach plan only — no calendar edits to existing meetings
