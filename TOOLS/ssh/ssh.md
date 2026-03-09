# ssh — SSH access configuration

## Purpose
SSH credentials and connection details for all agent-accessible machines.
Documents HOW to connect. For what runs on each host, see AGENTS/inventory/.

## Default credentials
- User: `${agent.tools.ssh.default_user}`
- Key: `${agent.tools.ssh.default_key}`

## Hosts

### homelab (achalkov-homelab)
- Primary: `${agent.inventory.homelab.ssh.primary_host}`
- Backup ISP: `${agent.inventory.homelab.ssh.backup_host}`
- User: alpha, Key: ~/.ssh/alpha_ed25519
- **CRITICAL:** Never make changes that could drop SSH access from LAN `192.168.2.0/24`.
- RU IP blocks: if a service is blocked, route via Shadowsocks — see AGENTS/inventory/baremetal/homelab/networking.md.

### vps-nl (Netherlands, main personal egress)
- Host: `${agent.inventory.vps_nl.ssh.host}`
- User: alpha

### vps-lisa (Netherlands, relatives' egress)
- Host: `${agent.inventory.vps_lisa.ssh.host}`
- User: alpha

## Variables
- `agent.tools.ssh.default_user` — `alpha`
- `agent.tools.ssh.default_key` — `~/.ssh/alpha_ed25519`
- `agent.inventory.homelab.ssh.primary_host` — `95.165.27.175:22022`
- `agent.inventory.homelab.ssh.backup_host` — `79.120.10.192:22022`
- `agent.inventory.vps_nl.ssh.host` — `194.87.62.225:22`
- `agent.inventory.vps_lisa.ssh.host` — `185.68.246.14:22`

## Accumulated rules
(empty)
