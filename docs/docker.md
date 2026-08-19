# Docker Services

Docker workloads are split between two primary virtual machines.

## Debian Docker Host

General-purpose self-hosted services:

- Actual Budget
- Dockhand
- Homepage
- Nextcloud AIO
- NGINX Proxy Manager
- Paperless-ngx
- Uptime Kuma
- Vaultwarden

### Nextcloud AIO

Nextcloud AIO uses multiple supporting containers, including:

- Apache
- Collabora
- Database
- Imaginary
- Mastercontainer
- Nextcloud
- Notify Push
- Redis

### Paperless-ngx

Paperless application components run in Docker on the Debian VM while PostgreSQL runs separately in a dedicated LXC on `pve`.

Current Docker components include:

- `paperless_webserver`
- `paperless_broker`

## Servarr Docker Host

The Servarr VM on `pve1` hosts the media stack.

### Media Management

- Radarr
- Sonarr
- Lidarr
- Bazarr
- Prowlarr
- Seerr

### Media Server

- Jellyfin

### Download Clients

- qBittorrent
- NZBGet

### Networking / Support

- Gluetun
- FlareSolverr

### Maintenance

- Cleanuparr
- DeUnhealth

### Management

- Hawser

## Storage Relationship

The Servarr VM mounts the Media LXC's `/data` Samba share over CIFS. Media-related Docker applications consume that mounted path rather than directly mounting the TrueNAS NFS export.

## Secrets

Some Docker deployments use `.env` files. Passwords and API credentials are not intentionally stored directly in Compose files. Live `.env` files, API tokens, passwords, and private keys should not be committed to this repository.