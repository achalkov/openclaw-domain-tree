# vps — Cloud virtual private servers

## Purpose
All rented cloud/virtual machines (VPS/VDS). Each VPS has its own L4 leaf file.

What belongs here: VPS nodes, their SSH access, hosted services, purpose.
What does NOT belong here: physical self-hosted machines (→ `../baremetal/`).

## Routing
- `./vps-nl.md` — Netherlands VPS, main personal VPN egress (achalkov)
- `./vps-lisa.md` — Netherlands VPS, relatives' Outline + OpenVPN egress (Лиза)

## Decision boundaries
- Rented cloud instance → vps/
- Physical machine at home → ../baremetal/

## Rules & Directives
- SSH user `alpha`, key `~/.ssh/alpha_ed25519` for all VPS unless overridden in leaf.

## Variables
(see per-host leaf files)

## Accumulated rules
(empty)
