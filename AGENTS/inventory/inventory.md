# inventory — Infrastructure inventory (hosts, networking, storage, services)

## Purpose
This domain is the single source of truth for all physical and virtual infrastructure:
SSH hosts, network topology, VPN/proxy configuration, storage arrays, Docker containers,
and maintenance procedures.

What belongs here:
- All SSH-reachable hosts (homelab, VPS nodes)
- Per-host networking, storage, software, and maintenance sub-trees
- Credentials, IPs, ports (as variables)
- Operational rules tied to specific infrastructure components

What does NOT belong here:
- Agent operational logic (→ `agent-ops/`)
- User profiles and preferences (→ `USER/`)
- Code repositories and coding workflows (→ `coding/`)
- Knowledge/research content (→ `knowledge/`)

## Routing
- `./baremetal/` → baremetal.md — physical self-hosted machines (homelab)
- `./vps/` → vps.md — rented cloud VPS nodes (vps-nl, vps-lisa)

## Decision boundaries
- **baremetal/ vs vps/**: physical machine under personal administration at home → baremetal/. Rented cloud instance → vps/.
- **networking vs software (within a host leaf)**: networking = concerns that affect routing, traffic interception, or connectivity at the network layer (VPN, Shadowsocks, DNS, Lancache). software = installed applications and Docker containers that don't route traffic.
- **storage vs software (within a host leaf)**: storage = block-level, filesystem, RAID, backups. software = application-layer services running on top of storage.
- **maintenance vs other topics (within a host leaf)**: maintenance = time-based operational procedures (updates, SMART checks, pruning) — even if the task touches storage or networking.

## Rules & Directives
- SSH user `alpha`, key `~/.ssh/alpha_ed25519` for ALL hosts unless overridden in a leaf.
- When an IP or port is referenced in a procedure, use the `agent.inventory.*` variable name, not a hardcoded value.
- Before any change on any host, verify it does not violate that host's critical safety rules (see per-host router files).

## Variables
- `agent.inventory.ssh.default_user` — `alpha`
- `agent.inventory.ssh.default_key` — `~/.ssh/alpha_ed25519`

## Accumulated rules
(empty — agent adds here over time)
