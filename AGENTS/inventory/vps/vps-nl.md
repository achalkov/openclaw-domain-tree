# vps-nl — Netherlands VPS (main VPN egress)

## Purpose
Documents the Netherlands VPS used as the primary personal VPN egress node.
This is a lightweight cloud instance; no sub-domains are needed unless complexity grows.

## Content

### Host details
- **Name**: vps-nl-main
- **Location**: Netherlands
- **Purpose**: Primary VPN egress for homelab-connected devices and personal traffic
- **IP**: `194.87.62.225`
- **SSH port**: `22`
- **SSH user**: `alpha`
- **SSH key**: `~/.ssh/alpha_ed25519`

### Connectivity
```bash
ssh -p 22 -i ~/.ssh/alpha_ed25519 alpha@194.87.62.225
```

### Services running
- VPN server (WireGuard or similar) — provides Netherlands egress IP for personal use
- Acts as the "clean" exit node when Russian ISP routing is problematic

### Relationship to other hosts
- homelab uses vps-nl as its primary VPN egress for personal devices
- vps-lisa (`185.68.246.14`) is a separate VPS for relatives' Outline/OpenVPN access; do not confuse them
- Shadowsocks on homelab routes specific RU-blocked domains through a proxy — this is separate from the VPN tunnel to vps-nl

### Access rules
- Only `alpha` user with key auth; no password auth.
- Standard port 22 (unlike homelab which uses 22022).

## Variables
- `agent.inventory.vps_nl.ssh.host` — `194.87.62.225`
- `agent.inventory.vps_nl.ssh.port` — `22`
- `agent.inventory.vps_nl.ssh.user` — `alpha`
- `agent.inventory.vps_nl.ssh.key` — `~/.ssh/alpha_ed25519`

## Accumulated rules
(empty)
