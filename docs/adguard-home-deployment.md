# AdGuard Home Deployment

## Overview
- Deployed: June 19, 2026
- Namespace: `adguard`
- Persistent Storage: Yes (5Gi Local Path)
- DNS: Port 53 (UDP/TCP)
- Web UI: NodePort 30080

## Access
- Web UI: `http://<node-ip>:30080`
- DNS Server: 192.168.4.20 (set on router for network-wide ad blocking)

## Key Features Configured
- Ad blocking and tracking protection
- Custom upstream DNS
- Persistent storage for filters and logs

## Lessons Learned
- Port mapping after initial setup (web port changes)
- DNS port 53 firewall and reachability troubleshooting
- NodePort for easy access in homelab
