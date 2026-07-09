# k8s-homelab

3-node bare-metal **k3s** cluster on Dell for Smart Home + Media services + Network Services.

## Current Status
- 3 nodes running (k3s v1.35)
- Local Path Provisioner installed
- Home Assistant deployed with persistent storage
- AdGuard Home (network-wide ad blocker)
- Monitoring Stack — Prometheus + Grafana + Node Exporter (full node metrics)

## Documentation
- [Cluster Status & Challenges](docs/cluster-status.md)
- [k3s Installation](docs/k3s-installation.md)
- [Home Assistant Deployment](docs/home-assistant-deployment.md)
- [AdGuard Home](docs/adguard-home-deployment.md)
- [Storage Setup](docs/storage-setup.md)
- [Monitoring Stack](docs/monitoring-deployment.md)

## Hardware
- 3x Dell Edge Platform
- Netgear GS108 + TP-Link WiFi Extender

## Next Goals
- GitOps with ArgoCD
