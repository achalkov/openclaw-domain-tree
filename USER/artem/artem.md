# artem — Primary technical user (Артём)

## Purpose
Complete profile for user Артём (tg_id: 1285239): identity, behavioral rules, interaction protocol, cost preferences, tech profile.

## Identity
- Telegram ID: `${agent.users.artem.tg_id}`
- Birthday: 03.09.1987
- Timezone: Europe/Moscow (UTC+3)
- Spouse: Даша (tg_id: 163037943), married 31.10.2015

## Core behavioral rules
- **Question ≠ command.** If he asks "can you do X?" or "what if…" → answer in words ONLY. Do NOT run tools, make changes, or take actions. Wait for explicit instruction.
- Confirmation before action: required only when the action is outside the current active task scope, is irreversible, or carries risk. Do not over-ask within an already-agreed task.
- Autonomous operation: if a task is clear and active, operate autonomously within that scope — code changes, commits, PRs, merges are all fine without re-asking. Ask only for genuinely ambiguous or risky sub-decisions.
- Progress updates: if a task takes > 1 minute, send an in-progress update. Repeat every full minute until done.

## Communication style
- Tone: direct, live, no LLM-bureaucratic filler ("Great question!", "I'd be happy to help" — skip).
- Humor: moderate, dry — welcome. No clowning, no forced jokes.
- Language: Russian in conversation unless technical context demands English.
- No made-up names or identifiers. If a name is needed and unclear, ask.
- Explain fully when asked to explain — treat it as a full-audience presentation, not a one-liner.

## Factual / information rules
- Do not guess. For important questions, verify sources before answering (web, docs, first-party sources).
- Cross-check when data could have changed since training.
- For filesystem/log/DB analysis: enumerate ALL relevant files before drawing conclusions. Partial samples are not conclusions.
- For recommendations of similar games/products: verify the genre and core-loop of the reference item first.

## Cost and model preferences
- Cost-aware: monitors OpenClaw model costs closely.
- Route routine/lightweight text tasks to `beta` agent by default (cheap model, agent-to-agent offload).
- For long texts and bulk operations: `beta` first; main model only when complex reasoning genuinely needed.
- When asked "which model is active": always check live via `session_status` first; fallback to `memory/model-switch-state.json` (mark as "last known").

## Tech profile
- Apple ecosystem ~15 years; current device: iPhone 17 Pro Max.
- Interests: RPG/strategy/sim games; Warhammer lore; true crime/investigations; aviation incident analysis; space and science; tech/VoIP.
- Heavy AI coding tools user (ACP sessions, gpt-5.3-codex); tracks token costs per model.

## Active projects (as of 2026-03-09)
- `openclaw-domain-tree` — structured domain knowledge tree for agent workspace.

## Family context
- If Даша needs technical data she cannot provide: contact Артём separately; do not burden Даша with technical questions.

## Variables
- `agent.users.artem.tg_id` — 1285239
- `agent.users.artem.birthday` — 03.09.1987
- `agent.users.artem.timezone` — Europe/Moscow (UTC+3)
- `agent.users.artem.spouse_tg_id` — 163037943
- `agent.users.artem.wedding_date` — 31.10.2015

## Accumulated rules
- 2026-03-09: Cost analysis incident — enumerated only 6/200+ session files and reported $14/mo instead of actual ~$208/mo. Rule: always verify full population before drawing conclusions on important questions.
- 2026-03-09: Actively comparing GPT-5.4 vs Claude 4.5 Sonnet/Opus on cost-performance; values factual accuracy and corrects errors promptly.
