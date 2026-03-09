# networking — Homelab network-layer services

## Purpose
All services and configuration that operate at the network layer on the homelab host:
VPN tunnels, traffic proxying, DNS, LAN routing, IP-block bypass, and traffic interception/caching.

What belongs here:
- VPN endpoints and tunnel configuration (WireGuard, OpenVPN, Outline)
- Shadowsocks proxy (RU IP-block bypass)
- Lancache (traffic intercept/cache for LAN)
- DNS rules (`dnsmasq` config)
- Firewall rules that govern reachability

What does NOT belong here:
- Application containers that happen to expose a network port but don't route/intercept traffic (→ `./software.md`)
- Printer (→ it's a LAN device, documented in homelab.md variables; no networking sub-domain needed)
- SSH configuration (→ homelab.md, the host router)

## Decision boundaries
- **VPN vs Shadowsocks**: VPN = encrypted tunnel encapsulating all traffic or providing remote access. Shadowsocks = SOCKS5 proxy specifically for bypassing RU IP blocks via ipset routing; it doesn't encapsulate all traffic.
- **Shadowsocks vs VPN for Outline**: Outline Server (on vps-lisa) provides the egress; Shadowsocks on homelab provides the local routing rule engine via ipset. They cooperate but are documented separately within this file.
- **Lancache vs software/**: Lancache intercepts and redirects DNS + HTTP traffic at the network layer for the LAN → this file. A media streaming server that clients connect to voluntarily → software.md.

## Rules & Directives
- `dnsmasq` must remain active at all times; verify after any networking change.
- Never modify iptables/nftables rules in ways that block `192.168.2.0/24` → SSH.
- DNS upstream default: `9.9.9.9` (Quad9).

---

## VPN

### Purpose
Documents VPN tunnel endpoints, configurations, and procedures related to the homelab host.
Covers both tunnels terminating on homelab and tunnels routed through VPS nodes.

### Topology overview
- **homelab** acts as a LAN gateway; VPN/Outline clients on the LAN use vps-lisa as egress.
- **vps-lisa** (`185.68.246.14`) runs Outline Server + OpenVPN for relatives' remote access.
- **vps-nl** (`194.87.62.225`) is the primary personal VPN egress for homelab-connected devices.

### Outline (vps-lisa)
- Purpose: provides relatives with a censorship-resistant egress from Netherlands.
- Hosted on: `vps-nl-lizina` (`185.68.246.14:22`).
- Management: SSH to vps-lisa as `alpha` to manage Outline Manager keys.

### OpenVPN (vps-lisa)
- Purpose: OpenVPN server for relatives' remote access.
- Hosted on: `vps-nl-lizina` (`185.68.246.14:22`).

### WireGuard / personal VPN (vps-nl)
- Egress node: `vps-nl-main` (`194.87.62.225`), Netherlands.
- Purpose: main personal VPN egress for homelab + personal devices.

### Procedures
- To add a VPN user or rotate keys: SSH to respective VPS host, manage via service CLI.
- For RU IP-blocked services that need a proxy rather than full VPN → use Shadowsocks (see below).

---

## Shadowsocks

### Purpose
Documents the Shadowsocks-libev installation on homelab used to route traffic for
RU IP-blocked services through an overseas proxy. Uses `ipset` to route only specific
domains through the tunnel rather than all traffic.

### What it does
Shadowsocks-libev runs as a transparent proxy on homelab. When a domain is added to the
ipset, traffic to that domain is routed through the Shadowsocks tunnel instead of the
default gateway — bypassing Russian ISP IP blocks without affecting other traffic.

### How to add a blocked domain
```bash
sudo /etc/shadowsocks-libev/add-domain-to-ipset.sh <domain>
```

**Rules for adding domains:**
- Prefer the **highest necessary level** (usually 2nd-level domain, e.g. `example.com` not `sub.example.com`) to minimize the number of ipset entries.
- DNS upstream for added domains: default OK (`9.9.9.9`).
- Only add domains that are actually IP-blocked in RU; don't blanket-add domains.

### Config location
- Script: `/etc/shadowsocks-libev/add-domain-to-ipset.sh`
- Config: `/etc/shadowsocks-libev/` (config.json and related files)

### When to use Shadowsocks vs VPN
- **Shadowsocks**: specific service is RU-blocked; you want only that service to exit via proxy; all other traffic stays on the default path. Low overhead, surgical.
- **VPN**: you want all traffic (or a device's full traffic) to exit via a foreign IP. Use vps-nl for this.

---

## Lancache

### Purpose
Documents the Lancache deployment on homelab. Lancache operates at the network layer:
it intercepts DNS queries from LAN clients and redirects download traffic through a
local caching proxy, dramatically reducing WAN bandwidth for repeated game/software downloads.

### What it does
- Intercepts DNS for major CDN domains (Steam, Epic, Blizzard, etc.) via `dnsmasq` overrides.
- Redirects HTTP download requests to a local nginx-based cache running in Docker.
- Serves cached content to LAN clients on subsequent requests without hitting the WAN.

### Why it's in networking not software
Lancache changes LAN DNS resolution and intercepts traffic flows before they reach their
intended remote destination. This is a network-layer concern (routing + traffic interception),
not merely an application serving requests to voluntary clients. Even though it runs as a
Docker container, its primary function is network traffic manipulation.

### Integration with dnsmasq
- `dnsmasq` on homelab is the LAN DNS server.
- Lancache DNS entries override CDN domain resolutions to point to homelab's LAN IP.
- If `dnsmasq` is restarted or config is regenerated, verify Lancache DNS overrides remain intact.

### Maintenance note
- Lancache cache storage lives on homelab's data disks (see `./storage.md`).
- Docker container management (pull/prune) is handled in `./maintenance.md`.

---

## Variables
- `agent.inventory.homelab.shadowsocks.script` — `/etc/shadowsocks-libev/add-domain-to-ipset.sh`
- `agent.inventory.homelab.shadowsocks.config_dir` — `/etc/shadowsocks-libev/`
- `agent.inventory.homelab.dns.upstream` — `9.9.9.9`
- `agent.inventory.homelab.lan.dns_server` — homelab LAN IP (primary DNS for LAN clients; `192.168.2.x`)
- `agent.inventory.homelab.lancache.container` — lancache Docker container name (verify on host)
- `agent.inventory.vps_lisa.vpn.host` — `185.68.246.14`
- `agent.inventory.vps_nl.vpn.host` — `194.87.62.225`

## Accumulated rules
(empty)
