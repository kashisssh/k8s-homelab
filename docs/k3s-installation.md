## Step 1: Prepare All Nodes

```bash
sudo apt update && sudo apt upgrade -y
sudo swapoff -a
sudo sed -i '/ swap / s/^$$ .* \$\$\$/#\1/g' /etc/fstab

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF

sudo sysctl --system

## Step 2: Install k3s on Master

```bash
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="server \
  --disable traefik \
  --disable servicelb \
  --disable local-storage \
  --kubelet-arg=eviction-hard=memory.available<400Mi" sh -

## Step 3: Join Worker Nodes

Get token from master:

```bash
sudo cat /var/lib/rancher/k3s/server/node-token

On each worker:
```bash
curl -sfL https://get.k3s.io | K3S_URL=https://192.168.4.43:6443 \
K3S_TOKEN=PASTE_TOKEN_HERE sh -

Step 4: Verify

```bash
kubectl get nodes -o wide
