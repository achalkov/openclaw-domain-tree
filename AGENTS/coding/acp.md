# acp — ACP/Codex agent session management

## Purpose
Rules for spawning, managing, and integrating results from ACP (Agent Communication Protocol)
coding sessions via `sessions_spawn` with `runtime="acp"`.

Covers: session creation, Discord thread binding, agentId configuration, result integration.
Does NOT cover: inline coding tasks, shell/Python scripts (→ ./scripts.md).

## Rules & Directives

### Session creation
- ACP harness MUST use `sessions_spawn` with `runtime="acp"` — no other spawn mechanism
- Always set `agentId` explicitly unless `acp.defaultAgent` is already configured in the environment
- Do NOT route ACP through `subagents`/`agents_list` tool calls or local PTY exec flows
  — these are different runtimes and will not connect to the ACP backend

### Discord integration
- For Discord targets: use thread-bound persistent sessions by default
  — set `thread=true` and `mode="session"` in the spawn parameters
- Do NOT call `message(action=thread-create)` for ACP threads
  — ACP manages thread creation internally; calling it separately creates orphaned threads

### Session lifecycle
- Reuse existing sessions where possible instead of spawning fresh per-request
- Check for an active session in the relevant thread before spawning a new one
- After task completion, verify result quality before integrating into main context

### Cost awareness
- ACP/Codex sessions are the dominant cost driver (~97% of total spend)
- gpt-5.3-codex sessions: ~$99 over 14 days (1845 turns, 37M input tokens) as of 2026-03-09
- Scope ACP sessions tightly; avoid open-ended "keep going" prompts without exit conditions

## Variables
(none — agentId and model config live in ACP runtime environment)

## Accumulated rules
(empty)
