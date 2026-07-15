# Cluster Status - June 16, 2026

## Hardware
- 3x Dell Edge (8GB RAM each)
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

# Cluster Status - June 22, 2026

### AdGuard Home
- Status: Running
- Namespace: `adguard`
- Persistent Storage: Yes (5Gi Local Path)
- DNS: Port 53 (UDP/TCP)
- Web UI: NodePort 30080
- Purpose: Network-wide ad blocking

# Cluster Status - July 2026

## Hardware Move (June 28, 2026)
- Full power off and physical relocation of all hardware
- Cluster recovered successfully after move
- Required `kubectl uncordon` on workers + rollout restarts for some deployments
- AdGuard Home needed re-configuration (config file was lost during power cycle, but query data was preserved)

## Monitoring Stack Deployed
- **Namespace**: `monitoring`
- **Components**:
  - Prometheus (metrics collection)
  - Grafana (visualization)
  - Node Exporter (DaemonSet on all nodes)
- **Access**:
  - Prometheus: NodePort `30990`
  - Grafana: NodePort `31000`
- All components using Local Path Provisioner for persistence
- Node Exporter running with `hostNetwork: true` + `hostPort: 9100`

## GitOps (ArgoCD)
- Status: Managing AdGuard Home, Monitoring and Home Assistant
