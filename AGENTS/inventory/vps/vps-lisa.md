# vps-lisa — Netherlands VPS (relatives' Outline + OpenVPN egress)

## Purpose
Documents the Netherlands VPS dedicated to providing relatives with a censorship-resistant
internet egress via Outline (Shadowsocks-based) and OpenVPN.
This is a separate host from vps-nl; it serves a different audience and must not be confused
with the primary personal egress VPS.

## Content

### Host details
- **Name**: vps-nl-lizina (internal alias: vps-lisa)
- **Location**: Netherlands
- **Purpose**: Relatives' Outline egress + OpenVPN server
- **IP**: `185.68.246.14`
- **SSH port**: `22`
- **SSH user**: `alpha`
- **SSH key**: `~/.ssh/alpha_ed25519`

### Connectivity
```bash
ssh -p 22 -i ~/.ssh/alpha_ed25519 alpha@185.68.246.14
```

### Services running
- **Outline Server**: provides Shadowsocks-based access keys for relatives. Client keys managed via Outline Manager CLI or API.
- **OpenVPN**: additional VPN option for relatives requiring full-tunnel access.

### Key operational notes
- This VPS is specifically for relatives — do NOT route personal/homelab traffic through it.
- Outline key rotation and new-user provisioning: SSH to this host, use Outline Manager API or shadowbox CLI.
- If OpenVPN config changes are needed: SSH to this host, modify `/etc/openvpn/` configs, restart service.

### Relationship to other hosts
- vps-nl (`194.87.62.225`) is the personal VPN egress — different host, different purpose.
- homelab's Shadowsocks ipset routes through a different proxy (not this VPS).

### Access rules
- Only `alpha` user with key auth; no password auth.
- Standard port 22.

## Variables
- `agent.inventory.vps_lisa.ssh.host` — `185.68.246.14`
- `agent.inventory.vps_lisa.ssh.port` — `22`
- `agent.inventory.vps_lisa.ssh.user` — `alpha`
- `agent.inventory.vps_lisa.ssh.key` — `~/.ssh/alpha_ed25519`

## Accumulated rules
(empty)
