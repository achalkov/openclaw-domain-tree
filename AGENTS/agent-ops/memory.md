# agent-ops/memory — Memory architecture and hygiene rules

## Purpose
Defines how agent memory is structured, where facts are stored, and how memory is maintained over time.

---

## Memory architecture

| Layer | File/Location | Contents | When to read | When to write |
|---|---|---|---|---|
| Long-term curated | `MEMORY.md` | Behavioral constants, rules, non-changing user preferences | Main session startup only | Heartbeat distillation; when rules change |
| Daily raw log | `memory/YYYY-MM-DD.md` | Session events, decisions, lessons, task outcomes | Read today + yesterday at session start | During session as events occur |
| SQLite index | `memory/memory.sqlite3` | Structured facts: preferences, decisions, todos, prior work | Query before answering about prior work/dates/prefs | After extracting durable facts from sessions |
| Heartbeat state | `memory/heartbeat-state.json` | Last check timestamps per channel (email, calendar, weather) | Every heartbeat run | After each heartbeat check |

## Load policy
- `MEMORY.md`: load **only in main session** (direct 1:1 chat with Артём or Даша). Do NOT load in group chats or shared contexts — privacy protection.
- Daily files: always read today's and yesterday's at session start.
- SQLite: query for relevant records before answering questions about past work, preferences, or todos. Do not skip this step.

## Write policy
- Session events, decisions, lessons → daily file during session.
- Durable facts (preferences, corrections, confirmed patterns) → SQLite index.
- Rule changes, behavioral constants → MEMORY.md (only during heartbeat distillation or explicit request).
- Do not store secrets or sensitive personal data outside MEMORY.md.

## MEMORY.md constraints
- Hard character limit: **5000 characters**. Never exceed.
- Content: rules and behavioral constants ONLY. No raw event logs, no one-off session details.
- Format: compact, operational. Remove outdated rules proactively.

## Memory hygiene (heartbeat task)
Every few days during a heartbeat:
1. Read recent `memory/YYYY-MM-DD.md` files.
2. Identify significant events, lessons, or insights worth keeping long-term.
3. Distill to `MEMORY.md` — curate, do not just append.
4. Remove stale or superseded entries from MEMORY.md.
5. Index durable facts in SQLite.

## Lessons learned (from operation)
- 2026-03-09: Partial file enumeration caused a 15× cost estimate error ($14 reported vs $208 actual). Never draw conclusions from partial data — always verify full population of relevant files/records before analysis.
- 2026-03-09: Session API in cron runtime only enumerates the cron session itself. Use transcript-path fallback when direct session recall fails.

## Variables
- `agent.agent-ops.memory_path` — `memory/` (workspace-relative)
- `agent.agent-ops.sqlite_path` — `memory/memory.sqlite3`
- `agent.agent-ops.memory_md_max_chars` — 5000
- `agent.agent-ops.heartbeat_state_path` — `memory/heartbeat-state.json`

## Accumulated rules
- Always query SQLite before answering questions about prior sessions, decisions, or preferences.
- MEMORY.md is for rules only; event details belong in daily files.
- Group chat sessions must NOT load MEMORY.md (privacy).
