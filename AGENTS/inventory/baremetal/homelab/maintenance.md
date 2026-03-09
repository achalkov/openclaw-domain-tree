# maintenance — Scheduled maintenance procedures for homelab

## Purpose
Operational checklists and results for time-based maintenance tasks on homelab:
system updates, SMART checks, Docker pruning, log review, and health verification.

## Content

### Maintenance schedule
- **Daily**: container health spot-check (`docker ps`, dnsmasq/ssh status)
- **Weekly**: SMART health for all disks, RAID array status check
- **On apt-upgrade run**: verify no reboot required; apply non-interactive updates; check for failed systemd units

### Standard maintenance checklist (run on homelab)

#### 1. Pre-checks
```bash
uptime                          # uptime + load average
df -h /                         # root FS usage (warn if >80%)
free -h                         # available RAM
systemctl --failed              # any unexpected failed units
```

#### 2. RAID health
```bash
cat /proc/mdstat
mdadm --detail /dev/md0
```
Expected: clean `[UUUU]`, no failed devices.

#### 3. SMART health
```bash
for d in /dev/sd{a..e} /dev/nvme{0,1}n1; do
  echo "=== $d ==="; smartctl -H $d; done
```
Expected: all `PASSED`.

#### 4. System updates
```bash
apt-get update -qq
apt-get upgrade --dry-run        # review before applying
apt-get upgrade -y               # apply non-interactively
```
Check `/var/run/reboot-required` after — reboot only if flag is present AND system is idle.

#### 5. Docker maintenance
```bash
# Pull updated images for running containers
docker ps --format '{{.Image}}' | sort -u | \
  grep '/' | xargs -I{} docker pull {}

# Prune dangling images
docker image prune -f
```
Note: image-ID-only references (no registry tag) cannot be pulled by name — skip those.

#### 6. Post-checks
```bash
systemctl is-active dnsmasq      # must be active
systemctl is-active ssh          # must be active
systemctl is-active systemd-networkd  # must be active
```

### Recent maintenance log (summary)
| Date | Outcome | Notes |
|------|---------|-------|
| 2026-03-08 | Clean | RAID `[UUUU]`, all SMART PASSED, 2 pkgs updated (sosreport 4.10.2, wpasupplicant 2.10-6ubuntu2.4), ~933.7 MB Docker pruned, no reboot required |

### Skip / abort conditions
- If `/etc/openclaw/maintenance-skip*` exists for the current MSK date → skip run.
- If in-use network traffic > 1 MB/s → defer disruptive steps (package upgrade, Docker pull).
- Never reboot during a RAID resync.

### Log file
Remote log is appended to `/var/log/openclaw-homelab-maintenance.log` on homelab after each run.

## Variables
- `agent.inventory.homelab.maintenance.log` — `/var/log/openclaw-homelab-maintenance.log`
- `agent.inventory.homelab.maintenance.skip_flag_dir` — `/etc/openclaw/`
- `agent.inventory.homelab.maintenance.traffic_threshold` — `1 MB/s`

## Accumulated rules
(empty)
