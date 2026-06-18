# Cluster Status - June 16, 2026

## Hardware
- 3x Dell VEP 1425 (8GB RAM each)
- Netgear GS108 Switch + TP-Link WiFi Extender (RE315)

## Installation Challenges & Solutions

### Ubuntu 22.04 Installation (Headless Servers)
- **Challenge**: Blank screen on HDMI, installer crashes (Subiquity issues), USB detection problems (`/dev/sdb` disappears).
- **Solution**:
  - Used **Serial Console** (micro-USB port + 115200 baud).
  - Kernel parameters: `nomodeset console=ttyS0,115200n8`
  - Switched to Ubuntu 22.04.5 LTS (more stable than 24.04 on VEP).

### k3s Installation
- **Challenge**: Low RAM (8GB) → k3s restarting due to bad eviction flags, permission issues.
- **Solution**:
  - Disabled heavy components: Traefik, ServiceLB, local-storage.
  - Used aggressive memory eviction settings.
  - Fixed kubeconfig permissions.

```bash
kubectl get nodes -o wide
```

# Cluster Status - June 17, 2026

## Deployed Applications

### Home Assistant
- Status: Running
- Namespace: `home-assistant`
- Persistent Storage: Yes (10Gi Local Path)
- Access: NodePort 30123 on any node IP

