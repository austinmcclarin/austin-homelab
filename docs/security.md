# Security

This document records the current security controls in the homelab. It is a current-state inventory, not a claim that every component is fully hardened.

## Remote Access

Tailscale is used for remote homelab access and management.

- Subnet route: `192.168.0.0/24`
- Public administrative ports: none
- Exit nodes: none

## Firewalls

### Network Firewall

- Device: UniFi UCG Ultra
- Port forwards: none
- Publicly exposed services: none

### Proxmox Firewall

- Enabled: yes

### Host Firewalls

- Debian VM: UFW
- Servarr VM: UFW
- AI server: UFW
- Media LXC: not yet verified
- Other Linux systems: not yet individually verified

## SSH

### Key-Only Systems

SSH key authentication is used for:

- Both Proxmox nodes
- Debian VM
- Servarr VM
- AI server
- TrueNAS SCALE

Direct root SSH login is used only on the Proxmox nodes.

### Raspberry Pi Systems

The Raspberry Pi systems currently allow password-based SSH authentication.

## Web Administration

Administrative interfaces are intended for internal access through the LAN and, where permitted by local firewall/ACL rules, through Tailscale subnet routing.

This includes:

- Proxmox
- TrueNAS
- Docker management
- UniFi

No administrative interfaces are intentionally exposed through public router port forwarding.

## TLS / HTTPS

- Reverse proxy: NGINX Proxy Manager
- Deployment: Docker on Debian VM
- Current certificate type: self-signed

Internal HTTPS is used for services including:

- Actual Budget
- AdGuard Home
- Bazarr
- Cleanuparr
- Dockhand
- Immich
- Jellyfin
- Lidarr
- Nextcloud
- NZBGet
- Paperless-ngx
- Prowlarr
- Proxmox
- Radarr
- Seerr
- TrueNAS
- Uptime Kuma
- Vaultwarden

## DNS Security

AdGuard Home provides LAN DNS filtering.

- DNS filtering: enabled
- Upstream provider: Quad9
- Upstream protocol: DNS-over-HTTPS

## Credentials and Secrets

Password management currently includes Bitwarden cloud and a self-hosted Vaultwarden instance.

Some Docker deployments use `.env` files. Passwords and API credentials are not intentionally stored directly in Compose files.

API tokens are used for supported systems and services, including examples such as:

- TrueNAS
- Proxmox
- Media-related services
- Ollama

Live secrets, private keys, tokens, and credential files are intentionally excluded from this repository.

## Account Security

Current documented state:

- Proxmox MFA: not enabled
- TrueNAS MFA: not enabled
- Tailscale MFA: not independently configured in this inventory
- UniFi authentication: additional account verification is in use, exact method to be verified
- GitHub account protection: enabled, exact method to be verified

## Updates and Patching

Current patching is primarily manual.

- Proxmox: manual; automated update status needs verification
- Docker: manual; automated update status needs verification
- Linux servers: manual; automated update status needs verification
- TrueNAS SCALE: manual

## Network Segmentation

- VLANs: none
- Separate management network: no
- Separate IoT network: no