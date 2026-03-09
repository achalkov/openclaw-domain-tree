# storage — Homelab disk, RAID, and backup configuration

## Purpose
All block-level and filesystem concerns for the homelab host: RAID array topology,
physical disk inventory, SMART monitoring, filesystem usage, and backup procedures.

What belongs here:
- RAID array status and configuration (mdadm)
- Physical disk list and SMART health state
- Filesystem mount points and usage
- Backup policies and destinations

What does NOT belong here:
- Application data layout inside containers (→ `./software.md`)
- Scheduled SMART checks as operational procedure (→ `./maintenance.md` for the procedure; storage.md holds the config/topology)
- Docker volume paths (→ `./software.md`)

## Decision boundaries
- **RAID vs Backup**: RAID = redundancy at the block device level (fault tolerance within the host). Backup = copies of data to separate destinations (protection against host-level failure or data corruption). They are complementary; RAID is not a backup.
- **storage.md vs maintenance.md**: storage.md holds the topology and config (what disks exist, how they are arranged). maintenance.md holds the operational checklist (how to run periodic checks). A SMART result finding → document in maintenance/ logs; the disk's existence → storage.md.

## Rules & Directives
- RAID array: `/dev/md0` (RAID5, verified clean `[UUUU]` as of 2026-03-08).
- Checked disks: `/dev/sd[a-e]`, `/dev/nvme[0-1]n1`.
- Root FS usage: ~38% (as of 2026-03-08).
- RAM: ~24 GiB available (as of 2026-03-08).

---

## RAID

### Purpose
Configuration, health status, and operational procedures for the RAID5 array on homelab.

### Array configuration
- **Device**: `/dev/md0`
- **Level**: RAID5
- **Member disks**: `/dev/sda`, `/dev/sdb`, `/dev/sdc`, `/dev/sdd`, `/dev/sde` (5 drives)
- **NVMe drives**: `/dev/nvme0n1`, `/dev/nvme1n1` (separate from RAID, used for OS/cache)
- **Last verified clean**: 2026-03-08, status `[UUUU]`, no failed devices

### Health check commands
```bash
# Quick status
cat /proc/mdstat

# Detailed array info
mdadm --detail /dev/md0

# SMART health for all disks
for d in /dev/sd{a..e} /dev/nvme{0,1}n1; do
  echo "=== $d ==="; smartctl -H $d
done
```

### Interpreting status
- `[UUUU]` = all drives Up → healthy
- `[UUU_]` = one drive failed → degraded, needs immediate attention
- Resync in progress → `[==>...]` shown in `/proc/mdstat` — do not reboot during resync

### Recovery procedures
1. Identify failed disk: `mdadm --detail /dev/md0` — look for `faulty` or `removed`.
2. Remove faulty disk from array: `mdadm /dev/md0 --remove /dev/sdX`
3. Physically replace disk.
4. Add new disk to array: `mdadm /dev/md0 --add /dev/sdX`
5. Monitor rebuild: `watch -n5 cat /proc/mdstat`

### When to escalate
- More than 1 drive failed simultaneously → do NOT attempt auto-recovery; snapshot data first.
- SMART `FAILED` result on a drive in the array → schedule replacement ASAP, treat as pre-failure.

---

## Backup

### Purpose
Documents backup strategy, destinations, and restore procedures for homelab data.

### Current backup posture (as of 2026-03-08)
- RAID5 provides local disk redundancy (not a backup — see note below).
- No explicit off-host backup destination was documented in source files.
- This file is a placeholder to be populated as backup infrastructure is established.

### RAID is not a backup
RAID5 protects against single-disk hardware failure but does NOT protect against:
- Accidental file deletion or corruption (changes replicate across all mirrors instantly)
- Host-level failures (fire, theft, power surge affecting all disks)
- Ransomware or software bugs that overwrite data

### Recommended backup targets (to define)
- Off-host: external VPS or cloud storage (e.g., Backblaze B2, rclone to S3-compatible)
- Frequency: daily incremental, weekly full snapshot for critical data
- Retention: at minimum 7 daily, 4 weekly

### Restore procedure (template)
1. Identify backup source (date, dataset).
2. Verify backup integrity before restore.
3. Restore to a test path first; verify data completeness.
4. Move to production path only after verification.

---

## Variables
- `agent.inventory.homelab.storage.raid_device` — `/dev/md0`
- `agent.inventory.homelab.storage.data_disks` — `/dev/sda,/dev/sdb,/dev/sdc,/dev/sdd,/dev/sde`
- `agent.inventory.homelab.storage.nvme_disks` — `/dev/nvme0n1,/dev/nvme1n1`
- `agent.inventory.homelab.backup.destination` — (not yet defined — populate when configured)
- `agent.inventory.homelab.backup.tool` — (not yet defined — rclone/restic/borgbackup TBD)

## Accumulated rules
(empty)
