# k8s-homelab-staging
## Proxmox
- Make sure to have a DHCP service running in the server network.
- Download talos iso with qemu support.
- Create control-plane VM with iso.
- Start VM.
## Talos setup
Generte configs:
```bash
talosctl gen config talos-proxmox-cluster https://$CONTROL_PLANE_IP_STATIC:6443 --output-dir _out
```

Adjust configs to correct IP etc.:
```bash
talosctl apply-config --insecure --nodes $CONTROL_PLANE_IP_DHCP --file _out/controlplane.yaml
talosctl apply-config --insecure --nodes $WORKER_IP_DHCP --file _out/worker.yaml
```

Setup talosctl :
```bash
export TALOSCONFIG="_out/talosconfig"
talosctl config endpoint $CONTROL_PLANE_IP
talosctl config node $CONTROL_PLANE_IP
```

Bootstrap
```bash
talosctl bootstrap
```

Get Kubeconfig
```bash
talosctl kubeconfig .
```

## Install core components
- Install cilium via helm
- Install flux via helm

##
