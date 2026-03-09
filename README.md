# openclaw-domain-tree

> Hierarchical domain-tree prompt architecture for OpenClaw agents.

## Goal

Replace the flat "load everything on every session" approach with a **lazy-loading domain tree**: the agent keeps a compact global core, and pulls only the relevant domain-specific rules when a task matches that domain.

## Key properties

- **Context efficiency** — baseline context stays small; domain rules load on demand.
- **Horizontal scalability** — new domains can be added without inflating core files.
- **Self-evolving** — the tree grows dynamically through the process of learning (see "Dynamic growth" below).
- **Depth limit: 4 levels** — prevents over-fragmentation while allowing enough specificity.

---

## Tree structure model

### Levels

| Level | Role | Example path | Example file |
|-------|------|-------------|--------------|
| L1 | Core files | `/` | `AGENTS.md`, `SOUL.md` |
| L2 | Top-level domain | `domains/inventory/` | `inventory.md` |
| L3 | Sub-domain or entity | `domains/inventory/homelab/` | `homelab.md` |
| L4 | Leaf topic | `domains/inventory/homelab/networking/` | `vpn.md`, `networking.md` |

### Router vs Leaf

Every level (L2–L4) consists of exactly one **router** and zero or more **leaves**:

- **Router** (`<name>.md`) — describes the abstraction at this level and explicitly routes to children:
  - Each child directory → "for X, go to `./x/` and read `x.md`"
  - Each leaf file → "for Y, read `./y.md`"
- **Leaf file** (`<topic>.md`) — terminal content; no sub-directory, no further routing.
- **Leaf directory** (`<topic>/`) — contains the next level's router + its own leaves.

**Rule:** a router at L2–L3 must be an abstraction, never a concrete entity. Concrete entities (a specific machine, a specific user, a specific tool) live at L3 or deeper.

### Example: reaching VPN config for homelab

```
AGENTS.md                              ← L1: global rules + domain registry
  → domains/inventory/inventory.md     ← L2: all hosts, common practices, routes to each host
    → homelab/homelab.md               ← L3: homelab facts, IPs, access, routes to categories
      → networking/networking.md       ← L4 router: network topology, routes to topics
        networking/vpn.md              ← L4 leaf: VPN-specific config & procedures
        networking/lancache.md         ← L4 leaf: Lancache config & procedures
      → software/software.md           ← L4 router
        software/docker.md             ← L4 leaf
      → maintenance/maintenance.md     ← L4 router
```

### Example: reaching Artem's preferences

```
AGENTS.md
  → domains/users/users.md             ← L2: user list, common rules across all users
    → artem/artem.md                   ← L3 router: Artem's facts & context
      artem/preferences.md             ← L3 leaf: Artem's preferences (terminal)
    → dasha/dasha.md                   ← L3 router
      dasha/preferences.md             ← L3 leaf
```

---

## Dynamic growth

The tree is not a fixed schema — it grows through the agent's **process of learning**:

1. **On receiving new information:** the agent checks whether it belongs to an existing domain.
2. **If the domain exists:** find the right level (router or leaf) and update or extend it.
3. **If the domain does not exist:** create it — including any intermediate levels needed — at the most appropriate location in the tree.
4. **After any structural change:** update the parent router to reference the new child, and update the domain registry in `AGENTS.md`.

**Creation threshold:** a topic warrants its own node if it appeared ≥2 times OR if its rules are non-trivial (not a one-liner).

This means the tree at any given time reflects the agent's accumulated knowledge. Missing domains are not gaps — they are areas not yet encountered. They will appear when needed.

---

## Current tree

```
AGENTS.md                     ← L1 core: global rules + domain registry
SOUL.md                       ← identity & tone
USER.md                       ← user profiles pointer (→ domains/users/)
MEMORY.md                     ← long-term memory policy
TOOLS.md                      ← environment-specific notes (SSH, printers, etc.)
HEARTBEAT.md                  ← proactive check policy
IDENTITY.md                   ← agent persona
CODING_RULES.md               ← coding standards
PROACTIVITY_CONTRACT.md       ← proactivity rules

domains/
  inventory/                  ← all machines & infrastructure
    inventory.md              ← L2 router
    homelab/
      homelab.md              ← L3 router (achalkov-homelab, 95.165.27.175)
      networking/
        networking.md         ← L4 router
        vpn.md                ← L4 leaf
        lancache.md           ← L4 leaf (to be created)
      software/
        software.md           ← L4 router
        docker.md             ← L4 leaf
      maintenance/
        maintenance.md        ← L4 router
      storage/
        storage.md            ← L4 router
        raid.md               ← L4 leaf
    vps-nl/
      vps-nl.md               ← L3 router (vps-nl-main, 194.87.62.225)
    vps-de/
      vps-de.md               ← L3 router (local machine / vps-de)
    vps-lisa/
      vps-lisa.md             ← L3 router (vps-nl-lizina, 185.68.246.14)

  users/                      ← all users interacting with the agent
    users.md                  ← L2 router
    artem/
      artem.md                ← L3 router
      preferences.md          ← L3 leaf
    dasha/
      dasha.md                ← L3 router
      preferences.md          ← L3 leaf

  agent-ops/                  ← agent self-management
    agent-ops.md              ← L2 router
    memory/
      memory.md               ← L3 leaf
    scheduling/
      scheduling.md           ← L3 leaf
    skills/
      skills.md               ← L3 leaf

  coding/                     ← software development
    coding.md                 ← L2 router
    acp/
      acp.md                  ← L3 leaf
    scripts/
      scripts.md              ← L3 leaf

  content/                    ← content creation & publishing
    content.md                ← L2 router
    cloudtext/
      cloudtext.md            ← L3 leaf
    telegram/
      telegram.md             ← L3 leaf

  knowledge/                  ← reference knowledge bases
    knowledge.md              ← L2 router
    history/
      history.md              ← L3 leaf
    science/
      science.md              ← L3 leaf

  finance/
    finance.md                ← L2 leaf (no sub-domains yet)
```

---

## Contributing

This repo evolves autonomously. The agent commits changes directly as it learns.
Human edits welcome — treat this as a living document.
