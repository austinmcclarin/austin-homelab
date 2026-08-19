# Networking

## Gateway and LAN

- Gateway: UniFi Cloud Gateway Ultra (UCG Ultra)
- Gateway IP: `192.168.0.1`
- WAN provider: Starlink
- Primary LAN: `192.168.0.0/24`
- DHCP server: UCG Ultra
- DHCP mode: DHCP Server
- DHCP range: `192.168.0.2` - `192.168.0.249`
- VLANs: none

## Switching

Core switch:

- UniFi Switch Lite 8 PoE
- 8 x 1 GbE
- PoE support

Connected infrastructure includes:

- UCG Ultra
- `pve`
- `pve1`
- TrueNAS
- AI server
- Main workstation
- U7 Lite access point

## Wireless

- Access point: UniFi U7 Lite
- Network: primary `192.168.0.0/24` LAN
- Wireless security: WPA2
- Dedicated wireless VLAN: none

## DNS

AdGuard Home runs in an LXC on `pve`.

- Address: `192.168.0.128`
- Address assignment: DHCP, currently without a reservation
- DHCP-provided DNS server: `192.168.0.128`
- Role: DNS filtering and ad/tracker blocking
- Upstream resolver: Quad9
- Upstream protocol: DNS-over-HTTPS
- DoH endpoint: `dns10.quad9.net`

Normal DNS path:

```text
LAN Client
    │
    ▼
AdGuard Home
192.168.0.128
    │ DNS-over-HTTPS
    ▼
Quad9
```

The main workstation may use VPN-provided DNS while its VPN is active, bypassing the normal LAN AdGuard path.

## Reverse Proxy

NGINX Proxy Manager runs in Docker on the Debian VM.

- Debian VM / NPM address: `192.168.0.16`
- Role: internal hostname routing and TLS termination
- Certificates: self-signed
- Public router port forwards: none

Example routing path:

```text
proxmox.example.com
      │ DNS
      ▼
192.168.0.16
NGINX Proxy Manager
      │
      ▼
Proxmox Web Interface
```

## Remote Access

Tailscale LXCs run on both Proxmox nodes.

- Purpose: remote access and management
- Advertised subnet: `192.168.0.0/24`
- Exit node usage: none
- Public administrative ports: none

Remote path:

```text
Remote Device
    │ Tailscale
    ▼
Tailscale Subnet Router
    │
    ▼
192.168.0.0/24 Homelab LAN
```

## Current Segmentation

- VLANs: none
- Dedicated management network: no
- Dedicated IoT network: no
- Current topology: single flat LAN
