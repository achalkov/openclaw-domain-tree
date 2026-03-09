# homelab — Primary self-hosted server (achalkov-homelab)

## Purpose
Everything specific to the physical homelab server: SSH access, LAN topology, network
services, storage arrays, Docker containers, and maintenance schedules.

What belongs here:
- All sub-domains for this specific host (networking, storage, software, maintenance)
- Host-level SSH, LAN, and safety directives
- Hardware-bound concerns (RAID, printer, physical NICs)

What does NOT belong here:
- VPS hosts (→ sibling leaves `../vps-nl.md`, `../vps-lisa.md`)
- Generic agent procedures not tied to this host

## Routing
- `./networking.md` — network-layer services: VPN, Shadowsocks, lancache, LAN rules
- `./software.md` — Docker containers and application-layer services
- `./storage.md` — RAID array, disks, SMART, backups
- `./maintenance.md` — scheduled maintenance procedures (updates, pruning, checks)

## Decision boundaries
- **networking.md vs software.md**: A service routes or intercepts traffic at the network layer → networking.md. A service runs as a container serving app-layer requests → software.md. Example: Shadowsocks and lancache both intercept/modify traffic flows → networking.md. A media server or web app → software.md.
- **storage.md vs maintenance.md**: RAID configuration and disk layout → storage.md. The procedure for running SMART checks or pruning Docker images → maintenance.md (time-based operational work, even if it touches storage).
- **maintenance.md vs software.md**: Docker image pulls and prunes as part of a scheduled job → maintenance.md. The actual container definitions and running state → software.md.

## Rules & Directives
- **CRITICAL — SSH safety**: NEVER make changes that could drop SSH access from LAN `192.168.2.0/24`. This is an irreversible lockout risk.
- Primary SSH: `${agent.inventory.homelab.ssh.primary_host}` (port `${agent.inventory.homelab.ssh.primary_port}`)
- Backup SSH: `${agent.inventory.homelab.ssh.backup_host}` (same port); use if primary is unreachable
- SSH user: `alpha`, key: `~/.ssh/alpha_ed25519`
- Always verify SSH/networking stack is reachable after networking changes (`systemd-networkd`, `ssh` service active)

## Variables
- `agent.inventory.homelab.ssh.primary_host` — `95.165.27.175`
- `agent.inventory.homelab.ssh.primary_port` — `22022`
- `agent.inventory.homelab.ssh.backup_host` — `79.120.10.192`
- `agent.inventory.homelab.ssh.backup_port` — `22022`
- `agent.inventory.homelab.ssh.user` — `alpha`
- `agent.inventory.homelab.ssh.key` — `~/.ssh/alpha_ed25519`
- `agent.inventory.homelab.lan.subnet` — `192.168.2.0/24`

## Accumulated rules
(empty — agent adds here over time)
