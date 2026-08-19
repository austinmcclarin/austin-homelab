# Monitoring and Observability

## Metrics Platform

### Prometheus

Prometheus runs in the Monitoring LXC on `pve`.

- Scrape interval: 15 seconds
- Evaluation interval: 15 seconds
- Role: metrics collection and time-series storage

Configured targets:

| Job | Target | Purpose |
|---|---|---|
| `pve-host1` | `192.168.0.10:9221` | Proxmox metrics for `pve` |
| `pve-host2` | `192.168.0.11:9221` | Proxmox metrics for `pve1` |
| `prometheus` | `localhost:9090` | Prometheus self-monitoring |

The Proxmox jobs use the `/pve` metrics path with the `default` module.

### Grafana

Grafana also runs in the Monitoring LXC on `pve`.

Current dashboards visualize Proxmox infrastructure metrics such as:

- Host CPU utilization
- Host memory utilization
- VM and LXC resource utilization
- Storage capacity and allocation
- VM/LXC disk usage
- Network I/O
- Disk I/O

## Monitoring Scope

### Proxmox

Monitored through Proxmox exporter/API-based metrics.

This provides visibility into:

- Physical Proxmox nodes
- Virtual machines
- LXC containers
- Storage
- CPU and memory utilization
- Network utilization
- Disk utilization

### Debian VM

- Proxmox VM-level metrics: yes
- Dedicated operating-system metrics: no

### Servarr VM

- Proxmox VM-level metrics: yes
- Dedicated operating-system metrics: no

### TrueNAS

- Prometheus monitoring: no

### AI Server

- Prometheus monitoring: no

### Docker

- Container-level Prometheus monitoring: no

### Network Equipment

UniFi Network provides native monitoring for the network infrastructure. UniFi metrics are not currently integrated into Prometheus.

## Node Exporter

A Prometheus Node Exporter process is running in the Monitoring LXC on port `9100`, but the current `prometheus.yml` does not configure `localhost:9100` as a scrape target.

Therefore, Node Exporter is running but is not currently part of the active Prometheus data collection path.

## Availability Monitoring

Uptime Kuma is installed in Docker on the Debian VM.

Current state:

- Active monitors: none
- Notifications: none

## Logging

- Centralized logging: no
- Log aggregation platform: none
- Current logging: individual host, application, Docker, Proxmox, and TrueNAS logs only

## Alerts and Notifications

- Prometheus alerting: not configured
- Grafana alerting: not configured
- Uptime Kuma notifications: not configured
- UPS notifications: none documented
- TrueNAS notifications: none documented
- UniFi monitoring alerts: none documented