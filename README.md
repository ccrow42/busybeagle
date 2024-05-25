# Busy Beagle Kubernetes Configuration


### Initial Setup

This installation will use a single RKE2 node. The software stack will be configured with ArgoCD.

The reference machine is a ubuntu 22.04 VM


#### Step 1 - Install RKE2

```bash
# Become root
sudo -i
```


```bash
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service
# Follow the logs (optional)
journalctl -u rke2-server -f
```


#### Step 2 - Configure kubectl access

```bash
# still as root
cp /etc/rancher/rke2/rke2.yaml /home/ccrow/.kube/config -rfv
# Replace ccrow with your username
chown ccrow:ccrow /home/ccrow/.kube/ -R
chmod 700 /home/ccrow/.kube/config
exit
```

We can install kubectl from the rancher installer
```bash
sudo cp /var/lib/rancher/rke2/bin/kubectl /usr/local/bin
```

We can (optionally) configure command autocompletion
```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
echo "alias k=kubectl" >> ~/.bashrc
echo "complete -o default -F __start_kubectl k" >> ~/.bashrc
source ~/.bashrc
```

#### Step 3 - Bootstrap argocd

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

#### Step 4 - Install ArgoCD Applications


