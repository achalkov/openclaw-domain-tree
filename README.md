# openclaw-domain-tree

> Hierarchical domain-tree prompt architecture for OpenClaw agents.

## Goal

Replace the flat "load everything on every session" approach with a **lazy-loading domain tree**: the agent keeps a compact global core, and pulls only the relevant domain-specific rules when a task matches that domain.

## Key properties

- **Context efficiency** — baseline context stays small; domain rules load on demand.
- **Horizontal scalability** — new domains can be added without inflating core files.
- **Self-evolving** — the agent is instructed to create new domain files and extend existing ones as it learns from tasks (see `AGENTS.md` directive).
- **Depth limit: 4 levels** — prevents over-fragmentation while allowing enough specificity.

## Tree depth convention

| Level | What lives here | Example |
|-------|-----------------|---------|
| 1 | OpenClaw core files | `AGENTS.md`, `SOUL.md`, `USER.md` |
| 2 | Top-level domains | `domains/homelab/`, `domains/users/` |
| 3 | Sub-domains | `domains/homelab/networking/`, `domains/users/artem/` |
| 4 | Leaf rules (specific tools/workflows) | `domains/homelab/networking/vpn.md` |

Some domains naturally use fewer levels (e.g. `users/` has no sub-domains — only level-2 user files). Levels are always counted from the top (level 1 = root), consuming as many levels as needed starting from 1.

## Domain matching

The agent uses an explicit registry in `AGENTS.md` (similar to how OpenClaw skills work). On receiving a task, it reads the registry, identifies the matching domain(s), and loads only those rule files before proceeding.

## Self-evolution directive

The agent **must** extend this tree autonomously:
- If a task requires domain-specific rules not covered by any existing domain → create a new domain file.
- If a recurring pattern emerges in an existing domain → extend that domain's `.md` file.
- Creation threshold: topic appeared ≥2 times OR rules are non-trivial.
- After creating/extending: add/update the registry entry in `AGENTS.md`.

## Structure

```
AGENTS.md          ← core: global rules + domain registry
SOUL.md            ← identity & tone
USER.md            ← user profiles (level-1 → directly into domains/users/)
MEMORY.md          ← long-term memory policy
TOOLS.md           ← environment-specific notes
HEARTBEAT.md       ← proactive check policy
IDENTITY.md        ← agent persona
CODING_RULES.md    ← coding standards
PROACTIVITY_CONTRACT.md  ← proactivity rules

domains/
  users/
    artem.md       ← rules & context specific to Артём
    dasha.md       ← rules & context specific to Даша
  homelab/
    homelab.md     ← general homelab rules
    networking/
      networking.md
      vpn.md
    storage/
      storage.md
      raid.md
    docker/
      docker.md
  coding/
    coding.md
    acp/
      acp.md
    scripts/
      scripts.md
  content/
    content.md
    cloudtext/
      cloudtext.md
    telegram/
      telegram.md
  knowledge/
    knowledge.md
    history/
      history.md
    science/
      science.md
  finance/
    finance.md
  agent-ops/
    agent-ops.md
    memory/
      memory.md
    scheduling/
      scheduling.md
    skills/
      skills.md
```

## Contributing

This repo evolves autonomously. The agent commits changes directly. Human edits welcome — treat this as a living document.
