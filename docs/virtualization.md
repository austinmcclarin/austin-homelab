# Proxmox and Virtualization

## Cluster Nodes

### `pve`

Lenovo ThinkCentre M910q with 16 GB RAM.

#### Virtual Machines

| VM | Role | CPU | Memory | Storage |
|---|---|---:|---:|---:|
| Debian | General-purpose Docker host | 2 cores | 8 GiB | 60 GiB |
| HAOS | Home Assistant | 2 cores | 4 GiB | 32 GiB |

#### LXC Containers

| LXC | Role | CPU | Memory | Root Storage |
|---|---|---:|---:|---:|
| Tailscale | Remote access / subnet router | 1 core | 512 MiB | 8 GiB |
| AdGuard Home | DNS filtering | 1 core | 512 MiB | 10 GiB |
| Monitoring | Prometheus / Grafana | 2 cores | 512 MiB | 16 GiB |
| PostgreSQL | Paperless-ngx database | 1 core | 1 GiB | 30 GiB |

### `pve1`

Lenovo ThinkCentre M910q with 24 GB RAM. This node primarily supports media workloads.

#### Virtual Machines

| VM | Role | CPU | Memory | Storage |
|---|---|---:|---:|---:|
| Servarr | Media Docker host | 4 cores | 16 GiB | 100 GiB |

#### LXC Containers

| LXC | Role | CPU | Memory | Root Storage |
|---|---|---:|---:|---:|
| Tailscale | Remote access / subnet router | 1 core | 512 MiB | 8 GiB |
| Media | Samba storage gateway | 4 cores | 4 GiB | 64 GiB |

## Media LXC Storage

The Media LXC is container ID 105 and uses additional mount points beyond its root filesystem.

- `/data`: 7 TB RAW virtual disk stored on the TrueNAS-backed Proxmox NFS storage and formatted ext4 inside the LXC.
- `/docker`: 32 GB ZFS-backed mount on local `flash` storage.
- Root filesystem: 64 GB ZFS-backed subvolume.

The LXC exports `/data` and `/docker` through Samba. The Servarr VM mounts the `/data` share over CIFS.

## Shared Proxmox Storage

TrueNAS exports `/mnt/AppleTree/proxmox-nfs` over NFS. Proxmox mounts it as:

- Storage ID: `proxmox`
- Mount point: `/mnt/pve/proxmox`
- Server: `192.168.0.79`

The storage is configured to support VM/LXC images, root directories, ISO images, templates, snippets, imports, and backup content.