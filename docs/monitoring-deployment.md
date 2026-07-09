# Monitoring Stack Deployment (Prometheus + Grafana + Node Exporter)

## Overview
- Deployed: June 28, 2026 (before hardware move)
- Namespace: `monitoring`
- Components:
  - Prometheus (metrics collection)
  - Grafana (dashboards & visualization)
  - Node Exporter (node-level metrics via DaemonSet)

## Architecture
- Prometheus scrapes:
  - Itself
  - Node Exporter on all 3 nodes (via hostNetwork + hostPort 9100)
- Grafana connects to Prometheus as data source
- All components use **Local Path Provisioner** for persistent storage

## Access URLs
| Component     | URL                              | Port   | Type     |
|---------------|----------------------------------|--------|----------|
| Prometheus    | `http://<MASTER_IP>:30990`      | 30990  | NodePort |
| Grafana       | `http://<MASTER_IP>:31000`      | 31000  | NodePort |
| Node Exporter | `http://<node-ip>:9100/metrics`  | 9100   | hostPort |

**Grafana Default Login:** `admin / admin` (change on first login)

## Important Notes / Lessons Learned

- **Node Exporter** must use `hostNetwork + hostPort` because Prometheus scrapes from the **node IP**, not pod IP.
- Initial Prometheus scrape config used `localhost:10250` (failed). Switched to Node Exporter on port 9100.
- RBAC was required for Prometheus to discover nodes via Kubernetes API.
- After full power cycle/move, some pods went into Pending → fixed by `kubectl uncordon` + rollout restart.
- Always export Grafana dashboards and Prometheus config after changes.

## Future Improvements
- Add **Loki** for log aggregation
- Add **Alertmanager** + alerting rules
- Use **Ingress** instead of NodePort
- GitOps deployment using ArgoCD

## Status (as of July 2026)
All components stable and collecting metrics from all 3 nodes.
