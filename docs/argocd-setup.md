# ArgoCD Setup

## Overview
- Deployed: 14th July 2026
- Purpose: GitOps for homelab applications
- Version: Latest

## Installation (Manual)
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

##Applications Managed
- AdGuard Home
- Home Assistant
- Prometheus + Grafana 
