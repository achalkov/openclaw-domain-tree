# coding — Engineering and code-generation tasks

## Purpose
Covers all tasks where code is written, generated, modified, executed, or maintained.
Also covers agent session orchestration (ACP) and script automation.

Does NOT cover: content publishing (→ content/), research/lookup queries (→ knowledge/),
cost or budget analysis (→ finance/).

## Routing
- `./acp.md` — ACP/Codex agent session lifecycle (sessions_spawn with runtime="acp")
- `./scripts.md` — shell and Python utility scripts, one-off automation

## Decision boundaries
- Task involves spawning a `sessions_spawn` with runtime="acp" → acp.md
  because ACP has its own session model, thread binding, and identity rules separate from inline coding
- Task involves writing/running a shell or Python script (not ACP) → scripts.md
  because scripts are standalone executables with their own lifecycle (cron, CLI invocation)
- Task is inline code generation or debugging (no separate session/script file) → handled at this level

## Rules & Directives

### Core coding principles
- Optimize for LLM support: predictability, debuggability, regenerability > aesthetics
- Work in discrete steps; offload heavy or long-running work to sub-agents (sessions_spawn) instead of bloating main context
- Always pull fresh documentation via Context7 skill when touching any language, framework, library, or SDK — do NOT rely on training knowledge
- Before marking any task "done": verify tests pass, build succeeds, lint clean, minimal smoke-run executed (where applicable)
- Update project agent instructions files (e.g. `.github/copilot-instructions.md`, `agent.md`) when important details are learned or process changes
- Reuse and close terminal sessions; avoid terminal sprawl
- Act as a good employee: do exactly what was asked, no invented subtasks, deliver quality and predictable results

### Code style for LLM maintainability
- Linear control flow preferred over complex branching
- Small/medium functions with clear single responsibility
- Structural log statements at key boundaries (entry, exit, errors)
- Avoid clever abstractions that are hard to regenerate from scratch

## Variables
(none — no secrets stored at this level)

## Accumulated rules
(empty)
