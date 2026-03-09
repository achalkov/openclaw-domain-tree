# agent-ops — Agent meta-operations and self-management

## Purpose
Rules for how the agent manages its own operations: memory storage, scheduling, skill use, and self-evolution.

What belongs here: memory architecture rules, heartbeat/cron scheduling logic, skill catalog and discovery, proactivity contracts.
What does NOT belong here: user identity (→ USER/), project code (→ coding/), domain-specific knowledge (→ knowledge/, homelab/, finance/).

## Routing
- `./memory.md` — memory architecture, storage policy, SQLite index, hygiene rules
- `./scheduling.md` — heartbeat cadence, cron usage, quiet hours, proactivity contract
- `./skills.md` — installed skills catalog, discovery, usage protocol

## Decision boundaries
- Where/how to store remembered facts → memory.md (architecture and policy lives there)
- When and how to proactively contact users → scheduling.md (heartbeat rules, quiet hours, proactivity contract)
- What tools/skills are available and how to select one → skills.md (catalog and selection logic)
- MEMORY.md contents (behavioral constants, user rules) → these are inputs/outputs of memory.md, not stored here
- Cron job implementation specifics → scheduling.md; actual cron entries live in system, not in this domain tree

## Rules & Directives
- Agent self-operations must not interrupt user sessions without justification (proactivity contract applies).
- Self-modifications to workspace files (MEMORY.md, AGENTS.md, skill files) require a brief preflight check: context, risks, dependencies.
- Before recommending or installing a skill: read its SKILL.md first.
- Failures in agent-ops (memory write error, cron misfire, skill crash) → log to daily memory file; escalate to Артём only if impact is user-visible or unrecoverable.

## Variables
- `agent.agent-ops.memory_path` — workspace-relative path to memory dir: `memory/`
- `agent.agent-ops.sqlite_path` — `memory/memory.sqlite3`
- `agent.agent-ops.heartbeat_state_path` — `memory/heartbeat-state.json`
- `agent.agent-ops.memory_md_max_chars` — 5000

## Accumulated rules
(empty)
