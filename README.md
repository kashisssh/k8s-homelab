# k8s-homelab

3-node bare-metal **k3s** cluster on Dell VEP 1425 for Smart Home + Media services.

## Current Status
- 3 nodes running (k3s v1.35)
- Local Path Provisioner installed
- Home Assistant deployed with persistent storage

## Documentation
- [Cluster Status & Challenges](docs/cluster-status.md)
- [k3s Installation](docs/k3s-installation.md)
- [Home Assistant Deployment](docs/home-assistant-deployment.md)
- [Storage Setup](docs/storage-setup.md)

## Hardware
- 3x Dell VEP 1425 (8GB RAM each)
- Netgear GS108 + TP-Link WiFi Extender

## Next Goals
- AdGuard Home
- Monitoring (Prometheus + Grafana)
- GitOps with ArgoCD
