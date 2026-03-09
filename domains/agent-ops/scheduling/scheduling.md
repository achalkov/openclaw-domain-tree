# Agent Ops: Scheduling

> **Domain:** `agent-ops.scheduling`
> **Level:** 3
> **Path:** `domains/agent-ops/scheduling/scheduling.md`
> **Parent:** `domains/agent-ops/agent-ops.md`

## Purpose
Rules for cron jobs, reminders, heartbeat scheduling, autopilot loops.

Key rules:
- Heartbeat: use for batched periodic checks.
- Cron: use for precise timing or isolated tasks.
- One-shot reminders → cron with kind=at.

## Rules & Directives

_(This section is intentionally minimal at creation time. The agent will extend it autonomously as tasks in this domain are encountered.)_

### How to extend this file
When working on a task in this domain:
1. Identify rules/patterns that were useful and non-obvious.
2. Add them below under a clear heading.
3. If a sub-domain is needed, create `domains/agent-ops/scheduling/<subdomain>/<subdomain>.md` and add it to the registry in `AGENTS.md`.

---

## Accumulated Rules

_(Agent: add rules here as they are discovered.)_
