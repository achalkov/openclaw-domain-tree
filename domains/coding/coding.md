# Coding Domain

> **Domain:** `coding`
> **Level:** 2
> **Path:** `domains/coding/coding.md`
> **Parent:** `AGENTS.md`

## Purpose
Rules for all coding and engineering tasks.

- LLM-first: predictability > aesthetics.
- Discrete steps; heavy work → sub-agents (sessions_spawn).
- Always pull fresh docs via Context7 skill.
- Verify: tests/lint/smoke before 'done'.
- Update project agent instructions when process changes.
- Linear control flow, small/medium functions, structural logs at boundaries.

## Rules & Directives

_(This section is intentionally minimal at creation time. The agent will extend it autonomously as tasks in this domain are encountered.)_

### How to extend this file
When working on a task in this domain:
1. Identify rules/patterns that were useful and non-obvious.
2. Add them below under a clear heading.
3. If a sub-domain is needed, create `domains/coding/<subdomain>/<subdomain>.md` and add it to the registry in `AGENTS.md`.

---

## Accumulated Rules

_(Agent: add rules here as they are discovered.)_
