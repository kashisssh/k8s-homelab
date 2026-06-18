# Storage Setup (Local Path Provisioner)

## Why We Use It
- Provides persistent storage for apps (Home Assistant, etc.)
- Simple and lightweight for 3-node cluster
- Data survives pod restarts

## Installation Command

```bash
kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml
```

## Verify
```bash
kubectl get pods -n local-path-storage
kubectl get storageclass
```

## Usage Example (PVC)
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-app-data
  namespace: my-namespace
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: local-path
  resources:
    requests:
      storage: 10Gi
---

## Current Status
StorageClass local-path is default
Used by Home Assistant
