# Backup and Recovery

This document records the current backup, redundancy, and recovery state of the homelab.

## Storage Redundancy

### TrueNAS SCALE

- Pool: `AppleTree`
- Drives: 2 x 10 TB
- Layout: ZFS mirror
- Disk redundancy: yes
- Independent backup: no

The ZFS mirror protects against a single disk failure but is not considered a backup.

## TrueNAS Data Protection

Current state:

- ZFS snapshots: none configured
- Replication: none configured
- External backup: none configured
- TrueNAS configuration backup: not yet verified

## Proxmox Backups

Current state:

- Scheduled VM backups: none
- Scheduled LXC backups: none
- Existing manual/legacy Proxmox backup archives: none found

The shared TrueNAS-backed Proxmox NFS storage is configured to support backup content, but no backup jobs are currently configured.

Storage details:

- Storage ID: `proxmox`
- Mount point: `/mnt/pve/proxmox`
- TrueNAS export: `/mnt/AppleTree/proxmox-nfs`

## Docker and Application Backups

No centralized Docker/application backup process is currently documented.

Persistent data backup status for applications such as Nextcloud, Paperless-ngx, Vaultwarden, Immich, and Actual Budget has not been documented as independently backed up.

## Power Resilience

An Amazon Basics 600 VA UPS protects:

- `pve`
- `pve1`
- TrueNAS
- AI server
- Main workstation

Network UPS Tools (NUT) is used for power-state monitoring and graceful shutdown behavior during extended power loss.

## Recovery Procedures

Current state:

- Formal recovery documentation: none
- Tested VM/LXC restores: none documented
- Tested application restores: none documented
- Tested TrueNAS dataset recovery: none documented