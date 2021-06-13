# Kubernetes cheatsheet by Ehsan Shirzadi

First install docker:
```
apt install docker.io
```

### How to install master:
Run this for all nodes
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Change native cgroup to systemd
Run this for all nodes
```
cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

```
systemctl restart docker
```

### For debian:
```
sysctl -p
```
### To start master:
```
kubeadm init
```

Join a node with this command :
```
kubeadm join xxx.xxx.xxx.xxx:6443 --token wqjxpm.vqupwqtp5xyvf1cg \
        --discovery-token-ca-cert-hash sha256:637711c34b8e97dcd7531c8a1eda15725657d84dd39dfcbc8702050927ffe075
```

```
apt-get install bash-completion
```

Add these to .bashrc for master
```
complete -F __start_kubectl k
source <(kubectl completion bash)
export KUBECONFIG=/etc/kubernetes/admin.conf        
```
```
export kubever=$(kubectl version | base64 | tr -d '\n')
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"
```


Email: Ehsan.Shirzadi@Gmail.com
Web: www.ehsanshirzadi.com