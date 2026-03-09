# agent-ops/scheduling — Heartbeat, cron, and proactivity rules

## Purpose
Rules for all time-based agent activity: heartbeat checks, cron jobs, proactive messaging cadence, quiet hours, and autopilot loops.

---

## Heartbeat vs Cron — when to use each

| Use heartbeat when | Use cron when |
|---|---|
| Multiple checks can batch (inbox + calendar + notifications in one turn) | Exact timing matters ("9:00 AM Monday sharp") |
| Conversational context from recent messages is helpful | Task needs isolation from main session history |
| Timing can drift slightly (~30 min is fine) | Different model/thinking level desired for the task |
| Reducing API calls by combining periodic checks | One-shot reminders ("in 20 minutes") |
| | Output delivers directly to channel without main session |

## Heartbeat behavior

### Cadence
- Do NOT send non-urgent proactive messages during **23:00–08:00 user local time** (Europe/Moscow = UTC+3).
- Avoid more than one proactive ping within **~3 hours** of the last one, unless urgent.
- If nothing meaningful changed → respond `HEARTBEAT_OK` and stop.

### Default heartbeat prompt
> "Read HEARTBEAT.md if it exists (workspace context). Follow it strictly. Do not infer or repeat old tasks from prior chats. If nothing needs attention, reply HEARTBEAT_OK."

### Check rotation (2–4 times per day)
1. **Email** — any urgent unread messages?
2. **Calendar** — events in next 24–48 hours?
3. **Mentions** — social/channel notifications?
4. **Weather** — relevant if user might go outside?

Track last-check timestamps in `memory/heartbeat-state.json`:
```json
{
  "lastChecks": {
    "email": <unix_timestamp>,
    "calendar": <unix_timestamp>,
    "weather": null,
    "mentions": null
  }
}
```

### Homelab spot-checks
- Frequency: 2–4 times per week (adaptive based on risk signals).
- Check: containers up, RAID healthy, SMART clean, system logs quiet, no intrusion signals.
- If all green: log result + timestamp to memory and heartbeat-state; **do NOT message user**.
- If any issue: alert Артём with: problem + impact + proposed next step (1 step, concise).

### What to follow up on (contextual, HEARTBEAT.md)
Only if discussed recently and still relevant:
1. Planned actions with timing ("on weekend", "tonight", "tomorrow").
2. In-progress technical tasks where a short status check helps.
3. Risky/fragile setups deserving "how did it go?" check.
4. Promised returns ("we'll come back to this").
- Select only **1 high-value topic** per heartbeat window.
- Skip if user appears busy or recent conversation already covered it.

## Proactivity contract (from PROACTIVITY_CONTRACT.md)

### When to message first
Only when there is real value:
- Follow-up on an important recent topic (health, deadline, promised return).
- Risk/failure/anomaly requiring attention.
- Brief status on an autonomous task with substantial progress.

### When to stay silent
- All green / routine successful checks → log to memory only.
- Nothing new since last check.
- Checked < 30 minutes ago.
- Late night (23:00–08:00 local).

### Message format
- What was noticed.
- Why it matters.
- One proposed next step.
Keep it short, human, optional-invitation style. No guilt-tripping, no bureaucratic templates.

### Anti-regression
If user says "we already discussed this / you forgot again":
- Immediately record as regression in daily memory.
- Update HEARTBEAT.md and/or this file with the specific predicate.
- Explicitly state in reply what safeguard was added.

## Autopilot loops
When user requests "do X until done without my participation":
1. Spawn cron autopilot job.
2. Each cycle: sync state → check reviews/mergeability → make one safe incremental step → send concise status update.
3. Disable cron when task is complete.
4. Deliver only significant updates (not every micro-step).

## Variables
- `agent.agent-ops.heartbeat_state_path` — `memory/heartbeat-state.json`
- `agent.users.artem.quiet_hours` — 23:00–08:00 Europe/Moscow
- `agent.users.dasha.quiet_hours` — 23:00–08:00 Europe/Moscow

## Accumulated rules
- Batch related periodic checks into HEARTBEAT.md instead of separate cron jobs.
- Homelab green = silent; only alert on actual issues.
- One proactive topic per heartbeat window maximum.
