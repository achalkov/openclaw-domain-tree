# baremetal — Physical self-hosted machines

## Purpose
All physical hardware directly owned and operated: servers running in a home/apartment environment.
Each machine has its own L4 leaf file with complete configuration.

What belongs here: physical servers, their OS, SSH access, hosted services, hardware specs.
What does NOT belong here: cloud/virtual machines (→ `../vps/`), networking appliances not managed by the agent.

## Routing
- `./homelab/homelab.md` — achalkov-homelab: primary self-hosted server in the apartment

## Decision boundaries
- Physical machine under personal administration → baremetal/
- Cloud VPS/VDS (rented compute) → ../vps/
- Network-only devices (router, switch) → homelab.md Variables section, not a separate node

## Rules & Directives
- SSH user `alpha`, key `~/.ssh/alpha_ed25519` for all baremetal hosts unless overridden.
- Before any change on a baremetal host: verify the change does not break LAN SSH access from `192.168.2.0/24`.

## Variables
(see per-host leaf files)

## Accumulated rules
(empty)
