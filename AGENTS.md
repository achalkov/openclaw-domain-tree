# AGENTS.md — Core Rules & Domain Registry

> This is the top-level (Level 1) control file.
> It contains ONLY: global invariant rules + the domain registry.
> Domain-specific rules live in `domains/`. Load them on demand.

## Global Rules

### Session startup
1. Read `SOUL.md` — identity & tone.
2. Read `USER.md` — user profiles.
3. Read today's `memory/YYYY-MM-DD.md` and yesterday's for recent context.
4. In main session: also read `MEMORY.md`.
5. Do NOT pre-load domain files — load them when a task matches.

### Domain loading
- On receiving a task: scan the Domain Registry below.
- Match the task to the most specific applicable domain(s).
- Read the matched domain `.md` file(s) before proceeding.
- If multiple domains apply, read all matching files.
- If no domain matches: proceed with core rules only.

### Self-evolution directive (MANDATORY)
The agent MUST extend the domain tree autonomously:
- Task requires rules not covered by any existing domain → **create** a new domain file.
- A topic/pattern has appeared ≥2 times → **extend** the relevant domain file.
- Creation threshold: rules are non-trivial (not obvious from core).
- After create/extend: **update this registry**.
- Depth limit: max 4 levels total (level 1 = this file's directory).

### Safety
- Do not exfiltrate private data.
- `trash` > `rm`.
- External actions (email, posts, API writes) require confirmation unless task is clearly active and scoped.

### Coding
See `domains/coding/coding.md` for coding-specific rules.

### Proactivity
See `PROACTIVITY_CONTRACT.md` and `HEARTBEAT.md` for proactive messaging rules.

---

## Domain Registry

| Domain key | Path | Description | Match triggers |
|------------|------|-------------|----------------|
| `users.artem` | `domains/users/artem.md` | Rules & context for user Артём (id: 1285239) | Any interaction from Артём; personalization needs |
| `users.dasha` | `domains/users/dasha.md` | Rules & context for user Даша (id: 163037943) | Any interaction from Даша; non-tech communication |
| `homelab` | `domains/homelab/homelab.md` | General homelab operations | homelab, server, host, ssh, VPS |
| `homelab.networking` | `domains/homelab/networking/networking.md` | Networking, DNS, firewall | network, DNS, firewall, routing, proxy |
| `homelab.networking.vpn` | `domains/homelab/networking/vpn.md` | VPN, Shadowsocks, Outline | VPN, Shadowsocks, WireGuard, Outline, tunnel |
| `homelab.storage` | `domains/homelab/storage/storage.md` | Storage, disks, backups | storage, disk, backup, SMART, filesystem |
| `homelab.storage.raid` | `domains/homelab/storage/raid.md` | RAID management | RAID, mdadm, array, parity |
| `homelab.docker` | `domains/homelab/docker/docker.md` | Docker containers | docker, container, compose, image |
| `coding` | `domains/coding/coding.md` | General coding rules | code, script, programming, dev, bug fix |
| `coding.acp` | `domains/coding/acp/acp.md` | ACP/Codex agent sessions | codex, ACP, agent session, sessions_spawn |
| `coding.scripts` | `domains/coding/scripts/scripts.md` | Shell/Python scripts | bash, shell script, python script, automation |
| `content` | `domains/content/content.md` | Content creation general | write, draft, content, text, post |
| `content.cloudtext` | `domains/content/cloudtext/cloudtext.md` | CloudText platform workflows | CloudText, lk.cloudtext.ru, тест, задание |
| `content.telegram` | `domains/content/telegram/telegram.md` | Telegram publishing | Telegram group, channel publish, tg_group |
| `knowledge` | `domains/knowledge/knowledge.md` | Research & knowledge queries | explain, research, find info, what is |
| `knowledge.history` | `domains/knowledge/history/history.md` | History domain (incl. teaching) | история, history, ЕГЭ, ОГЭ |
| `knowledge.science` | `domains/knowledge/science/science.md` | Science & tech knowledge | science, physics, space, biology, tech |
| `finance` | `domains/finance/finance.md` | Finance & cost analysis | cost, price, budget, банк, расход, деньги |
| `agent-ops` | `domains/agent-ops/agent-ops.md` | Agent operations & meta | memory, heartbeat, cron, agent setup |
| `agent-ops.memory` | `domains/agent-ops/memory/memory.md` | Memory management rules | MEMORY.md, memory hygiene, forget, remember |
| `agent-ops.scheduling` | `domains/agent-ops/scheduling/scheduling.md` | Cron & scheduling | cron, schedule, reminder, recurring, heartbeat |
| `agent-ops.skills` | `domains/agent-ops/skills/skills.md` | Skill management | skill, install skill, find skill, SKILL.md |
