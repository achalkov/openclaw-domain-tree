# AGENTS — Agent workspace rules and domain registry

## Purpose
Defines how the agent operates: behavioral rules, knowledge areas, operational standards.
This is L1. All operational knowledge lives in AGENTS/ sub-tree (L2–L4).

## Domain registry (AGENTS/ sub-tree)

| Domain | Path | Description | Max depth |
|--------|------|-------------|-----------|
| inventory | AGENTS/inventory/ | All infrastructure: hosts, networking, storage, services | L4 |
| coding | AGENTS/coding/ | Software development rules, ACP, scripts | L3 |
| content | AGENTS/content/ | Content creation and publishing | L3 |
| knowledge | AGENTS/knowledge/ | Reference knowledge: history, science | L3 |
| finance | AGENTS/finance.md | Cost tracking, model routing | L2 (leaf) |
| agent-ops | AGENTS/agent-ops/ | Agent self-management: memory, scheduling, skills | L3 |

## Navigation algorithm
1. Identify which domain the task belongs to from the registry above.
2. Navigate to L2 router → read → follow Routing section.
3. Repeat until reaching the appropriate leaf.
4. Load only files along that branch — do not load the entire tree.

## Global behavioral rules
- Confidence thresholds: 🔴 0.1 for user/finance questions, 🟡 0.25 for infra/coding, 🟢 0.4 for knowledge.
- Before risky/irreversible actions outside current task scope: show plan + confirm with user.
- Question ≠ command: if user asks → answer in words first; do not run tools unless explicitly asked.
- If task takes > 1 minute: send progress update; repeat every full minute until done.
- Never break LAN SSH access (192.168.2.0/24) on any infra change.

## Accumulated rules
(empty)
