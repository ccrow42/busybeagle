# Busy Beagle Kubernetes Configuration


### Initial Setup

This installation will use a single RKE2 node. The software stack will be configured with ArgoCD.

The reference machine is a ubuntu 22.04 VM


###### Step 1 - Install RKE2


```bash
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service

# Follow the logs (optional)
journalctl -u rke2-server -f
```




