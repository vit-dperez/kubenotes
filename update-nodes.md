### Upgrade kubernetes node

**Check cluster info**
```
kubectl get nodes
```

**Check if nodes can host workloads**
```
kubectl describe node | grep -i taints
```

**Get on which nodes are the pods deployed on**
```
kubectl get pods -o wide
```

**Upgrade one node at the time passing the workload to the other**

**Get the latest version available for upgrade**
```
kubeadm upgrade plan
```

**We will be upgrading the controlplane node first. Drain the controlplane node of workloads and mark it UnSchedulable**
```
kubectl drain --ignore-daemonsets <node-name>
```

**Changing the repo**
```
nano /etc/apt/sources.list.d/kubernetes.list
deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /
```

**Upgrade kubeadm** 

https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

```
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.30.0-*' && \
sudo apt-mark hold kubeadm
```

```
sudo kubeadm upgrade apply v1.30.0
```

```
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.30.0-*' kubectl='1.30.0-*' && \
sudo apt-mark hold kubelet kubectl
```

```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

```
kubectl uncordon controlplane
```


Worker nodes
```
sudo kubeadm upgrade node
```
