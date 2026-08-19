# Physical Hardware

## Management Workstation

- AMD Ryzen 9 5900X
- 32 GB DDR4
- 2 TB M.2 storage
- 1 TB M.2 Windows drive
- AMD Radeon RX 9070 XT
- 2.5 GbE
- CachyOS
- Role: personal workstation, homelab administration, and local compute

## Networking

### UniFi Cloud Gateway Ultra

- Model: UCG Ultra
- Role: router, firewall, DHCP server, Internet gateway
- WAN provider: Starlink
- Gateway address: `192.168.0.1`

### UniFi Switch Lite 8 PoE

- Model: USW Lite 8 PoE
- 8 x 1 GbE
- PoE support
- Role: core LAN switch

### UniFi U7 Lite

- Role: primary wireless access point
- Wireless security: WPA2
- Network: primary `192.168.0.0/24` LAN

## Proxmox Nodes

### `pve`

- Lenovo ThinkCentre M910q
- Intel Core i5-7500T
- 16 GB DDR4
- 50 GB M.2
- 250 GB SSD
- 1 GbE
- Operating system: Proxmox VE

### `pve1`

- Lenovo ThinkCentre M910q
- Intel Core i5-7500T
- 24 GB DDR4
- 50 GB M.2
- 250 GB SSD
- 1 GbE
- Operating system: Proxmox VE
- Primary role: media-focused virtualization node

## AI Server

- AMD Ryzen 5 3600X
- 16 GB DDR4
- NVIDIA RTX 5060 Ti 16 GB
- 500 GB M.2 boot drive
- 250 GB SSD
- 4 TB HDD
- 1 GbE
- Ubuntu Server
- Role: local AI/LLM compute

## TrueNAS Server

- Intel Xeon E3-1230 v3
- 32 GB DDR3 ECC
- 120 GB SSD boot drive
- 2 x 10 TB HDD
- 1 GbE
- TrueNAS SCALE
- Role: centralized network storage

## Raspberry Pi Systems

- 4 x Raspberry Pi 3B+
- 32 GB SD card per system
- Ubuntu for Raspberry Pi
- Current workload roles are not yet documented

## Power

### UPS

- Amazon Basics 600 VA UPS
- Protects:
  - `pve`
  - `pve1`
  - TrueNAS
  - AI server
  - Main workstation
- NUT is used for monitoring and graceful shutdown behavior