# Storage Architecture

## TrueNAS SCALE

TrueNAS SCALE provides centralized storage for the homelab.

### Pool

- Pool: `AppleTree`
- Drives: 2 x 10 TB HDD
- Layout: ZFS mirror
- Usable capacity: approximately 9.1 TiB

The mirror provides disk redundancy but is not treated as an independent backup.

## Datasets

### `immich`

Stores photo and video data for Immich, which runs directly on TrueNAS SCALE.

### `ISO`

Stores Linux ISO images and is exported over NFS for Proxmox use.

Path:

```text
/mnt/AppleTree/ISO
```

### `nextcloud_data`

Legacy Nextcloud storage. It remains exported over NFS but is no longer the primary Nextcloud data location.

Path:

```text
/mnt/AppleTree/nextcloud_data
```

### `proxmox-nfs`

Shared Proxmox storage exported through NFS.

TrueNAS path:

```text
/mnt/AppleTree/proxmox-nfs
```

Proxmox mount:

```text
/mnt/pve/proxmox
```

Storage ID:

```text
proxmox
```

The storage is available to both Proxmox nodes and supports VM/LXC disks, root filesystems, ISOs, templates, snippets, imports, and backup content.

### `SMB`

General-purpose SMB dataset for local workstation file sharing.

## Media Storage Architecture

The media environment does not mount the TrueNAS export directly into the Servarr VM.

```text
TrueNAS AppleTree/proxmox-nfs
        │
        │ NFS
        ▼
Proxmox pve1
        │
        │ 7 TB RAW virtual disk
        ▼
Media LXC
/data - ext4
        │
        │ Samba / SMB
        ▼
Servarr VM
/data - CIFS
        │
        ▼
Media Docker applications
```

The Media LXC is container ID 105. Its `/data` filesystem is backed by a 7 TB RAW disk stored on the TrueNAS-backed Proxmox NFS storage.

The LXC exports:

- `/data` as Samba share `data`
- `/docker` as Samba share `docker`

Access is restricted to the `192.168.0.0/24` network. The Servarr VM mounts the `data` share over CIFS.

## Current Data Protection State

- ZFS mirror: configured
- ZFS snapshots: none configured
- TrueNAS replication: none configured
- External backup: none configured
- Scheduled Proxmox backups: none configured