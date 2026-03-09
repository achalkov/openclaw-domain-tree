# software — Homelab application-layer services and Docker containers

## Purpose
Documents all Docker containers and application-layer services running on homelab that
do NOT operate at the network layer. This includes media servers, web UIs, databases,
monitoring stacks, and any other containerized workloads.

What belongs here:
- Docker Compose stacks and individual container definitions
- Application configuration and exposed ports (app-layer, not routing)
- Service health checks for app-layer services
- Container image sources and update procedures

What does NOT belong here:
- Network-layer containers (Lancache, Shadowsocks) → `./networking.md`
- Container image pull/prune as a scheduled maintenance task → `./maintenance.md`
- Disk/volume layout for container data → `./storage.md`

## Content

### Docker maintenance context (from 2026-03-08 maintenance log)
- Docker is running on homelab; maintenance includes `docker pull` for running container images.
- Registry-based images can be pulled by name; image-ID-only references are not pullable by name.
- Dangling image pruning reclaimed ~933.7 MB on 2026-03-08.

### Container management
- Running containers: check with `docker ps` on homelab.
- Compose stacks: typically in `/home/alpha/` or `/opt/` directories (verify on host).
- To update a container image: `docker pull <image>` then `docker compose up -d` for the stack.

### Procedures
- **Check running containers**: `ssh -p 22022 alpha@95.165.27.175 'docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Image}}"'`
- **Check container logs**: `docker logs <container_name> --tail 50`
- **Restart a container**: `docker compose -f <path>/docker-compose.yml restart <service>`

## Variables
- `agent.inventory.homelab.docker.compose_dir` — directory where Compose stacks live (verify on host)

## Accumulated rules
(empty)
