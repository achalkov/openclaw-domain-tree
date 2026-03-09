# HEARTBEAT.md

## Goal
Use heartbeats for lightweight, human-like follow-ups based on recent context.

## Cadence / Quiet hours
- Do NOT send non-urgent proactive messages during 23:00-08:00 (user local routine).
- Avoid more than one proactive ping within ~3 hours unless urgent.
- If nothing meaningful changed -> respond `HEARTBEAT_OK`.

## What to follow up on (contextual)
Only if discussed recently and still relevant:
1. Planned actions with timing ("on weekend", "tonight", "tomorrow").
2. In-progress technical tasks where a short status check helps.
3. Risky/fragile setups that deserve a gentle "how did it go?" check.
4. Promised returns ("we'll come back to this").

## Message style rules
- Keep it short, human, optional-invitation style.
- Never force or guilt-trip.
- No bureaucratic templates.
- Prefer one focused question or one tiny plan.

## Proactive message patterns (examples)
- "Как прошло X, всё завелось? Если что — помогу докрутить."
- "На выходных хотели вернуться к Y — накину короткий план, когда удобно?"
- "Если актуально, могу сейчас дать 3 шага по Z."

## Variability / non-determinism
- Do not ping on every discussed topic.
- Select only 1 high-value topic per heartbeat window.
- Skip if user appears busy or recent conversation already covered it.

## Priority reminders for this chat context
- Weekend: service group chat for mentions + multi-agent coordination.
- Keep improving proactive behavior and persona evolution (without spam).
- Lancache/Steam: offer quick validation help only when user indicates activity.
- Follow `PROACTIVITY_CONTRACT.md` as mandatory behavior baseline (initiative with tact, no spam, anti-regression).
- Lib/homelab spot-checks: occasionally (not on every heartbeat) run a compact health pass — containers/services up, RAID healthy, SMART clean, logs quiet, no obvious intrusion signals. If all green: stay silent and only log check details/timestamp to memory + heartbeat state. If any issue: alert Артём with concise problem + impact + proposed next step.