---
draft: false
date: 2024-08-01
categories:
  - Linux
authors:
  - junho
---

Kubernetes the Hard way: Raspberry-pi 5 cluster.

I try to configure the Control plane myself. Kubernetes is a complex distributed system. By setting it up by hand, I hope to learn more about Kubernetes components.

<img src="https://imagej.net/media/icons/pi.svg" alt="pi" width="40">
<img src="https://kubernetes.io/images/kubeadm-stacked-color.png" alt="kubeadm" width="50">
<img src="https://raw.githubusercontent.com/cncf/artwork/master/projects/containerd/horizontal/color/containerd-horizontal-color.png" alt="containerd" width="70">
<img src="https://imgur.com/Av7PzuR.png" alt="pi-cluster" width="180">

<!-- more -->

# Table of Contents

- [Raspberry Pi Setup](#raspberry-pi-setup)
    - [Enable the external PCI Express port](#enable-the-external-pci-express-port)
    - [Set NVMe early in the boot order](#set-nvme-early-in-the-boot-order)
    - [Network settings](#network-settings)
- [Kubernetes](#kubernetes)
    - [Prerequisite](#prerequisite)
    - [Container runtime](#container-runtime)
        - [CRI-O](#cri-o)
        - [containerd](#containerd)
    - [Installing kubeadm, kubelet and kubectl](#installing-kubeadm-kubelet-and-kubectl)
    - [Creating a cluster with kubeadm](#creating-a-cluster-with-kubeadm)
    - [Troubleshooting kubeadm](#troubleshooting-kubeadm)
    - [CNI: Calico](#cni-calico)
    - [Controlling your cluster from machines other than the control-plane node](#controlling-your-cluster-from-machines-other-than-the-control-plane-node)
    - [Metrics server](#metrics-server)
    - [Nginx Ingress Controller](#nginx-ingress-controller)
    - [Metallb](#metallb)
- [Docker Registry](#docker-registry)
- [Argo CD](#argo-cd)
- [Reference](#reference)


## Raspberry Pi Setup

- Hardware
    - 3 x Raspberry pi 5 (1 Master node, 2 Worker nodes;)
        - 8GB Memory, 4-core CPU
    - 3 x Raspberry Pi M.2 HAT+  (1 master, 2 workers)
    - 3 x Raspberry Pi Active Cooler
    - 3 x SSD: SK Hynix BC901 256GB
    - 3 x Ethernet cable
    - 3 x Usb-C cable (power adapter ideally >= 25W = 5A x 5V)
    - 1 x TP LINK Switch Hub TL-SG105

Now, configure NVMD SSD Boot! [LINK](https://www.jeffgeerling.com/blog/2023/nvme-ssd-boot-raspberry-pi-5).

### Enable the external PCI Express port


```sh
sudo vim /boot/firmware/config.txt

# Add to bottom of /boot/firmware/config.txt
dtparam=pciex1

# Note: You could also just add the following (it is an alias to the above line)
# dtparam=nvme

# Optionally, you can control the PCIe lane speed using this parameter
# dtparam=pciex1_gen=3
```

### Set NVMe early in the boot order

```sh
# Edit the EEPROM on the Raspberry Pi 5.
sudo EDITOR=vim rpi-eeprom-config --edit

# Change the BOOT_ORDER line to the following:
BOOT_ORDER=0xf416

# Add the following line if using a non-HAT+ adapter:
PCIE_PROBE=1

# Press Ctrl-O, then enter, to write the change to the file.
# Press Ctrl-X to exit nano (the editor).
```

### Network settings

Check [linux set-up](https://blogd.org/blog/2024/07/01/linux/)


[↑ Back to top](#)
<br><br>


## Kubernetes

We will configure Kubernetes v1.30.

- [Prerequisite](#prerequisite)
- [Container runtime](#container-runtime)
- [Installing kubeadm, kubelet and kubectl](#installing-kubeadm-kubelet-and-kubectl)
- [Creating a cluster with kubeadm](#creating-a-cluster-with-kubeadm)

### Prerequisite

- Swap memory off
  - The default behavior of a kubelet was to fail to start if swap memory was detected on a node. 
  - You MUST disable swap if the kubelet is not properly configured to use swap.

```sh
# disable swapping temporarily.
sudo swapoff -a
# To make this change persistent across reboots, make sure swap is disabled in config files. Comment out swap
# vim /etc/fstab
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

- Required ports
  - Check required ports for both control plane and worker nodes
  - https://kubernetes.io/docs/reference/networking/ports-and-protocols/

```sh
nc 127.0.0.1 6443 -v
```

- Configuring a cgroup driver
  - https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/configure-cgroup-driver/

```sh
#   On Linux, control groups are used to constrain resources that are allocated to processes.
#   Both the `KUBELET` and the underlying `CONTAINER RUNTIME` need to interface with control groups
#   to enforce resource management for pods and containers and set resources such as cpu/memory requests and limits.
#   There are two cgroup drivers available: cgroupfs-default cgroup driver in the kubelet, systemd.
#   The Container runtimes page explains that the systemd driver is recommended for kubeadm based setups
#   instead of the kubelet's default cgroupfs driver, because kubeadm manages the kubelet as a systemd service.

cat << EOF > kubeadm-config.yaml
kind: ClusterConfiguration
apiVersion: kubeadm.k8s.io/v1beta3
kubernetesVersion: v1.30.3
---
kind: KubeletConfiguration
apiVersion: kubelet.config.k8s.io/v1beta1
cgroupDriver: systemd
EOF
```

[↑ Back to top](#)
<br><br>


### Container runtime

Kubernetes 1.30 requires that you use a runtime that conforms with the Container Runtime Interface (CRI); containerd, CRI-O, Docker Engine. You need to install a container runtime into each node in the cluster so that Pods can run there. (kubelet deprecated Docker support since Kubernetes>=1.24)

#### CRI-O

- [instruction](https://github.com/cri-o/packaging/blob/main/README.md#usage)

```sh
```


[↑ Back to top](#)
<br><br>


#### containerd

- Getting started with [containerd](https://github.com/containerd/containerd/blob/main/docs/getting-started.md)

- Install and configure prerequisites
  - 1. Enable IPv4 packet forwarding
  - 2. cgroup drivers: systemd
  - 3. container runtime - containerd


```sh
# 1. Enable IPv4 packet forwarding
#   By default, the Linux kernel does not allow IPv4 packets to be routed between interfaces.
#   sysctl params required by setup, params persist across reboots
cat << EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system

# Verify that net.ipv4.ip_forward is set to 1 with:
sysctl net.ipv4.ip_forward

# 2. cgroup drivers
#   On Linux, control groups are used to constrain resources that are allocated to processes.
#   LATER DO:
# kubeadm init --config kubeadm-config.yaml

# 3. container runtime - containerd
# https://github.com/containerd/containerd/blob/main/docs/getting-started.md
# Step 3-1: Installing containerd
wget https://github.com/containerd/containerd/releases/download/v1.7.20/containerd-1.7.20-linux-arm64.tar.gz
sudo tar Cxzvf /usr/local containerd-1.7.20-linux-arm64.tar.gz

# If you intend to start containerd via systemd, you should also download
#   the containerd.service unit file into /usr/local/lib/systemd/system/containerd.service
sudo mkdir -p /usr/local/lib/systemd/system/
sudo wget -O /usr/local/lib/systemd/system/containerd.service https://raw.githubusercontent.com/containerd/containerd/main/containerd.service

sudo systemctl daemon-reload
sudo systemctl enable --now containerd
sudo systemctl status containerd

# Step 3-2: Installing runc
wget https://github.com/opencontainers/runc/releases/download/v1.1.13/runc.arm64
sudo install -m 755 runc.arm64 /usr/local/sbin/runc

# Step 3-3: Installing CNI plugins
wget https://github.com/containernetworking/plugins/releases/download/v1.5.1/cni-plugins-linux-arm64-v1.5.1.tgz
sudo mkdir -p /opt/cni/bin
sudo tar Cxzvf /opt/cni/bin cni-plugins-linux-arm64-v1.5.1.tgz

# 4. You can find this file under the path /etc/containerd/config.toml.
# generate default config
sudo mkdir -p /etc/containerd
sudo containerd config default > /etc/containerd/config.toml
sudo cat /etc/containerd/config.toml

# 5. Configuring the systemd cgroup driver
#   To use the systemd cgroup driver in /etc/containerd/config.toml with runc, set
sudo vim /etc/containerd/config.toml

[plugins]
  # ...
  [plugins."io.containerd.grpc.v1.cri"]
    sandbox_image = "registry.k8s.io/pause:3.8"

        [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
          # ...
          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
            SystemdCgroup = true


sudo systemctl restart containerd
sudo systemctl status containerd
```

### nerdctl

"`nerdctl` is a Docker-compatible CLI for `containerd`"

[Why nerdctl?](https://blog.devgenius.io/k8s-why-use-nerdctl-for-containerd-f4ea49bcf900)

- Pre-requisite
  - containerd is installed, enabled, and running
  - cni plugins is installed (previously `cni-plugins-linux-arm64-v1.5.1.tgz`)
  - Configure [rootlesskit](https://rootlesscontaine.rs/getting-started/containerd/)
  - [Install Guide](https://www.techrepublic.com/article/deploy-container-nerdctl/)

```sh
# uidmap
sudo apt-get install uidmap -y

# RootlessKit
sudo apt-get install rootlesskit -y

wget https://github.com/containerd/nerdctl/releases/download/v2.0.0-rc.0/nerdctl-2.0.0-rc.0-linux-arm64.tar.gz
sudo tar Cxzvvf /usr/local/bin nerdctl-2.0.0-rc.0-linux-arm64.tar.gz

which nerdctl
  /usr/local/bin/nerdctl

#sudo sh -c "echo 1 > /proc/sys/kernel/unprivileged_userns_clone"
sudo vim /etc/sysctl.d/99-rootless.conf
kernel.unprivileged_userns_clone=1

# apply in 99-rootless.conf to system
sudo sysctl --system
# check if it is applied to system
sudo sysctl kernel.unprivileged_userns_clone

# DO NOT RUN AS `root` !!!
containerd-rootless-setuptool.sh install

# Now, you can run without root privilege!
nerdctl version
nerdctl
```


[↑ Back to top](#)
<br><br>


### Installing kubeadm, kubelet and kubectl

- For Kubernetes v1.30, you will install these packages on <b>ALL OF YOUR MACHINES</b>:
  - `kubeadm`: the command to bootstrap the cluster.
  - `kubelet`: the component that runs on all of the machines in your cluster and does things like starting pods and containers.
  - [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
  <!-- - [`helm`](https://helm.sh/docs/intro/install/) -->

```sh
# 1. Update the apt package index and install packages needed to use the Kubernetes apt repository:
sudo apt-get update
# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

# 2. Download the public signing key for the Kubernetes package repositories. The same signing key is used for all repositories so you can disregard the version in the URL:
# If the directory `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.
# sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# 3. Add the appropriate Kubernetes apt repository. 
# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# 4. Update the apt package index, install kubelet, kubeadm and kubectl, and pin their version:
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

# kublet : set node ip
sudo su -
local_ip="$(ip --json addr show eth0 | jq -r '.[0].addr_info[] | select(.family == "inet") | .local')"
echo $local_ip
cat > /etc/default/kubelet << EOF
KUBELET_EXTRA_ARGS=--node-ip=$local_ip
EOF
cat /etc/default/kubelet
exit

# 5. (Optional) Enable the kubelet service before running kubeadm:
sudo systemctl enable --now kubelet
```

[↑ Back to top](#)
<br><br>


### Creating a cluster with kubeadm

- Initializing your `control-plane node` (master node)

```sh
# --pod-network-cidr
# your Pod network must not overlap with any of the host networks

# on master node
# sudo kubeadm init --config kubeadm-config.yaml

POD_CIDR="10.100.0.0/16"
NODENAME=$(hostname -s)
MASTER_PRIVATE_IP=$(ip addr show eth0 | awk '/inet / {print $2}' | cut -d/ -f1)

echo ""
echo "POD_CIDR = $POD_CIDR"
echo "NODENAME = $NODENAME"
echo "MASTER_PRIVATE_IP = $MASTER_PRIVATE_IP"

sudo kubeadm init \
    --apiserver-advertise-address="$MASTER_PRIVATE_IP" \
    --apiserver-cert-extra-sans="$MASTER_PRIVATE_IP" \
    --pod-network-cidr="$POD_CIDR" \
    --node-name "$NODENAME" \
    --ignore-preflight-errors Swap \
    -v=5

# [addons] Applied essential addon: CoreDNS
# [addons] Applied essential addon: kube-proxy
# Your Kubernetes control-plane has initialized successfully!
# To start using your cluster, you need to run the following as a regular user:

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Alternatively, if you are the root user, you can run:
#   export KUBECONFIG=/etc/kubernetes/admin.conf
# You should now deploy a pod network to the cluster.
# Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
#   https://kubernetes.io/docs/concepts/cluster-administration/addons/
# Then you can join any number of worker nodes by running the following on each as root:

sudo kubeadm join 192.168.0.10:6443 --token thlb00.g7ge841m77zgkux3 \
        --discovery-token-ca-cert-hash sha256:7f789053ab02c6f81be6a7fcdc2ba94a307f1e168a08561b5ae6c7ad60a91772
```

- Worker nodes

```sh
kubectl get no
    NAME      STATUS   ROLES           AGE     VERSION
    master    Ready    control-plane   2d17h   v1.30.3
    worker1   Ready    <none>          2d17h   v1.30.3
    worker2   Ready    <none>          2d17h   v1.30.3

kubectl label node worker1 node-role.kubernetes.io/worker=worker
kubectl label node worker2 node-role.kubernetes.io/worker=worker

kubectl get no
    NAME      STATUS   ROLES           AGE     VERSION
    master    Ready    control-plane   2d17h   v1.30.3
    worker1   Ready    worker          2d17h   v1.30.3
    worker2   Ready    worker          2d17h   v1.30.3
```


### Troubleshooting kubeadm

- `coredns` is stuck in the Pending state. This is expected and part of the design. 
    - [troubleshooting-kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/)

```sh
k get pod -n kube-system
  NAME                             READY   STATUS    RESTARTS        AGE
  coredns-7db6d8ff4d-sv6bv         0/1     Pending   0               4h54m
  coredns-7db6d8ff4d-vtc4p         0/1     Pending   0               4h54m

k describe pod coredns-7db6d8ff4d-sv6bv -n kube-system
    # Warning  FailedScheduling  7m50s (x6 over 4h45m)  default-scheduler  0/3 nodes are available: 3 node(s) had untolerated taint {node.kubernetes.io/not-ready: }. preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.

```

- CIDR allocation failed

```sh
k logs kube-controller-manager-master -nkube-system
    E0805 23:30:48.648521       1 controller_utils.go:250] Error while processing Node Add
    : failed to allocate cidr from cluster cidr at idx:0: CIDR allocation failed;
    there are no remaining CIDRs left to allocate in the accepted range

ps aux | grep cluster-cidr
    --cluster-cidr=10.100.0.0/16

helm install --dry-run cat-release ./cat-chart -f ./cat-chart/values.pi.yaml
# change CIDR blocks 
```


- [Force delete](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

```sh
k delete --grace-period=0 --force -nkube-system pod/coredns-7db6d8ff4d-5dv6d
```


### CNI: Calico

Install Calico CNI (Container Network Interface) plugin to enable Pod networking!

You must deploy a `Container Network Interface` (CNI) based Pod network add-on so that your Pods can communicate with each other. Cluster DNS (CoreDNS) will not start up before a network is installed. Without CNI, the coredns pods are `pending` and `podSubnet` is not specified in the cluster configuration.


- 1-1. Install with manifest

```sh
# Check Pod Subnet is missing
kubectl get configmap -n kube-system kubeadm-config -o yaml
    ...
    networking:
      dnsDomain: cluster.local
      podSubnet: 10.100.0.0/16
      serviceSubnet: 10.96.0.0/12
    scheduler: {}
    ...
```

```sh
curl -O https://raw.githubusercontent.com/projectcalico/calico/v3.28.1/manifests/calico.yaml
kubectl apply -f calico.yaml

# Verify Calico installation in your cluster.
kubectl get pods -nkube-system

    NAME                                       READY   STATUS     RESTARTS   AGE
    calico-kube-controllers-77d59654f4-59qlx   0/1     Pending    0          21s
    calico-node-mn2kl                          0/1     Init:0/3   0          21s
    calico-node-sndg4                          0/1     Init:0/3   0          21s
    calico-node-wmwpm                          0/1     Init:0/3   0          21s
```


- 1-2. Install with Calico Operator - tigera-operator

```sh
# Install the operator on your cluster.
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.28.1/manifests/tigera-operator.yaml

```

- `custom-resources.yaml`

```yaml
# This section includes base Calico installation configuration.
# For more information, see: https://docs.tigera.io/calico/latest/reference/installation/api#operator.tigera.io/v1.Installation
apiVersion: operator.tigera.io/v1
kind: Installation
metadata:
  name: default
spec:
  # Configures Calico networking.
  calicoNetwork:
    ipPools:
    - name: default-ipv4-ippool
      blockSize: 26
      cidr: 10.100.0.0/16
      encapsulation: VXLANCrossSubnet
      natOutgoing: Enabled
      nodeSelector: all()

---

# This section configures the Calico API server.
# For more information, see: https://docs.tigera.io/calico/latest/reference/installation/api#operator.tigera.io/v1.APIServer
apiVersion: operator.tigera.io/v1
kind: APIServer
metadata:
  name: default
spec: {}
```

- Custom Resource

```sh
curl https://raw.githubusercontent.com/projectcalico/calico/v3.28.1/manifests/custom-resources.yaml -O
kubectl create -f custom-resources.yaml

# Verify Calico installation in your cluster.
watch kubectl get pods -n calico-system

NAME                                       READY   STATUS    RESTARTS   AGE
calico-kube-controllers-5857c9dccf-f6bh2   1/1     Running   0          6m43s
calico-node-l65nq                          1/1     Running   0          6m43s
calico-node-wtftp                          1/1     Running   0          6m43s
calico-node-xj2kn                          1/1     Running   0          6m43s
calico-typha-68cbb57dc7-752ch              1/1     Running   0          6m43s
calico-typha-68cbb57dc7-b49rn              1/1     Running   0          6m40s
csi-node-driver-5pt8r                      2/2     Running   0          6m43s
csi-node-driver-gqps8                      2/2     Running   0          6m43s
csi-node-driver-lkthq                      2/2     Running   0          6m43s
```

- To determine the pod network CIDR, you can inspect the configuration of the CNI plugin installed in your cluster.
- Here’s how you can check for some common CNI plugins:

```sh
# 1. `calico` CNI plugin
kubectl get ippools.crd.projectcalico.org -o yaml

    apiVersion: v1
    items:
    - apiVersion: crd.projectcalico.org/v1
      kind: IPPool
      spec:
        blockSize: 26
        cidr: 10.100.0.0/16
```

[↑ Back to top](#)
<br><br>


### Controlling your cluster from machines other than the control-plane node

```sh
scp root@<control-plane-host>:/etc/kubernetes/admin.conf .
scp mobb@192.168.0.10:/home/mobb/.kube/config .

# `cluster` `context` `user` -> add this to existing `~/.kube/config`
# change names to 'pi' which can be identified by you...
kubectl --kubeconfig ./config get nodes
  clusters:
  - cluster: ...
  contexts:
  - context: ...
  users:
  - name: ...

kubectl config get-contexts
kubectl config use-context pi


kubectl get no
  NAME      STATUS     ROLES           AGE     VERSION
  master    NotReady   control-plane   5h17m   v1.30.3
  worker1   NotReady   <none>          5h12m   v1.30.3
  worker2   NotReady   <none>          5h12m   v1.30.3

kubectl top no
    NAME      CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
    master    137m         3%     846Mi           10%
    worker1   56m          1%     528Mi           6%
    worker2   68m          1%     501Mi           6%

kubectl top pod -nkube-system
    NAME                                       CPU(cores)   MEMORY(bytes)
    calico-kube-controllers-77d59654f4-59qlx   2m           12Mi
    calico-node-mn2kl                          25m          117Mi
    calico-node-sndg4                          27m          117Mi
    calico-node-wmwpm                          24m          117Mi
    coredns-7db6d8ff4d-kvzq2                   2m           13Mi
    coredns-7db6d8ff4d-mqmj9                   2m           13Mi
    etcd-master                                20m          44Mi
    kube-apiserver-master                      48m          261Mi
    kube-controller-manager-master             12m          56Mi
    kube-proxy-7st54                           1m           13Mi
    kube-proxy-gcb6c                           1m           12Mi
    kube-proxy-wt555                           1m           13Mi
    kube-scheduler-master                      3m           18Mi
    metrics-server-5df54c66b8-zhr7h            4m           18Mi
```


[↑ Back to top](#)
<br><br>


### Metrics server

```sh
curl -L https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml -o metrics-server.yaml

vim metrics-server.yaml
      - args:
        - --kubelet-insecure-tls=true

kubectl apply -f metrics-server.yaml 

k get pod -nkube-system

    NAME                                       READY   STATUS    RESTARTS   AGE
    ...
    metrics-server-5df54c66b8-zhr7h            1/1     Running   0          35s
```


[↑ Back to top](#)
<br><br>

### Nginx Ingress Controller

- Install `helm`

```sh
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

- Install `Nginx Ingress Controller`
    - [quick start](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start)
    - [Guide](#https://medium.com/@tonylixu/devops-in-k8s-nginx-ingress-controller-0a09f48458e2)


```sh
helm upgrade --install ingress-nginx ingress-nginx \
    --repo https://kubernetes.github.io/ingress-nginx \
    --namespace ingress-nginx --create-namespace

kubectl get pods -ningress-nginx

kubectl get svc -ningress-nginx
    NAME                                 TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
    ingress-nginx-controller             LoadBalancer   10.102.120.211   <pending>     80:31362/TCP,443:32684/TCP   52s
    ingress-nginx-controller-admission   ClusterIP      10.99.130.218    <none>        443/TCP                      52s
```


### Metallb

<img src="https://kubernetes.github.io/ingress-nginx/images/baremetal/baremetal_overview.jpg" alt="A pure software solution: MetalLB" width="400">

- [A pure software solution for Nginx ingress controller: MetalLB](https://kubernetes.github.io/ingress-nginx/deploy/baremetal/)
- [installation](https://metallb.universe.tf/installation/)

- Preparation
    - If you’re using kube-proxy in IPVS mode, since Kubernetes v1.14.2 you have to enable strict ARP mode.

```sh
# kubectl edit configmap -n kube-system kube-proxy
# OR
# see what changes would be made, returns nonzero returncode if different
kubectl get configmap kube-proxy -n kube-system -o yaml | \
    sed -e "s/strictARP: false/strictARP: true/" | \
    kubectl diff -f - -n kube-system

# actually apply the changes, returns nonzero returncode on errors only
kubectl get configmap kube-proxy -n kube-system -o yaml | \
    sed -e "s/strictARP: false/strictARP: true/" | \
    kubectl apply -f - -n kube-system
```

- Installation with Helm

```sh
helm repo add metallb https://metallb.github.io/metallb
helm install metallb metallb/metallb -n metallb-system
```

- Configuration
    - https://metallb.universe.tf/configuration/

```sh
k get no
    NAME      STATUS   ROLES           AGE     VERSION
    master    Ready    control-plane   2d17h   v1.30.3
    worker1   Ready    <none>          2d17h   v1.30.3
    worker2   Ready    <none>          2d17h   v1.30.3

k get svc -ningress-nginx
    NAME                                 TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
    ingress-nginx-controller             LoadBalancer   10.106.139.9    <pending>     80:30777/TCP,443:30936/TCP   4h23m
    ingress-nginx-controller-admission   ClusterIP      10.110.127.70   <none>        443/TCP                      4h23m

k get ingress
    NAME               CLASS   HOSTS       ADDRESS   PORTS   AGE
    fe-nginx-ingress   nginx   localhost             80      81m



# apply metallb.yaml
cat << EOF > metallb.yaml
---
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: default
  namespace: metallb-system
spec:
  addresses:
  - 192.168.0.10-192.168.0.20
  autoAssign: true
---
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: default
  namespace: metallb-system
spec:
  ipAddressPools:
  - default
EOF


k apply -f metallb.yaml
```



## Docker Registry

### Local Registry

Set up local docker registry that Kubernetes Pods will pull images from. I used `worker1` node to set up a temporary docker registry. I will set-up another raspberry-pi machine in the future.

- Self-signed Certificate

```sh
mkdir -p certs
# Generate SSL Certificates:
openssl req -newkey rsa:4096 -nodes -sha256 -x509 \
  -keyout certs/domain.key \
  -days 365 \
  -out certs/domain.crt \
  -subj "/CN=192.168.0.11"


# Run the Registry Container with HTTPS:
docker run -d -p 5000:5000 \
  --restart=always \
  --name registry \
  -v $(pwd)/certs:/certs \
  -e REGISTRY_HTTP_ADDR=0.0.0.0:5000 \
  -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \
  -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key \
  registry:2

# Distribute the CA Certificate:
sudo mkdir -p /etc/docker/certs.d/192.168.0.11:5000
sudo cp certs/domain.crt /etc/docker/certs.d/192.168.0.11:5000/ca.crt

docker tag your-image 192.168.0.11:5000/your-image
docker push 192.168.0.11:5000/your-image
```

- Configure Containerd to Use the Secure Registry

```
# Edit the containerd Configuration:
sudo vim /etc/containerd/config.toml

[plugins."io.containerd.grpc.v1.cri".registry]
  [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
    [plugins."io.containerd.grpc.v1.cri".registry.mirrors."192.168.0.10:5000"]
      endpoint = ["https://192.168.0.10:5000"]
  [plugins."io.containerd.grpc.v1.cri".registry.configs]
    [plugins."io.containerd.grpc.v1.cri".registry.configs."192.168.0.10:5000".tls]
      ca_file = "/etc/docker/certs.d/192.168.0.10:5000/ca.crt"

sudo systemctl restart containerd
```

[↑ Back to top](#)
<br><br>

### Dockerhub

- Authenticate to dockerhub to increase image pull rate limit.
- [increase-rate-limits](https://www.docker.com/increase-rate-limits/)

```sh
sudo vim /etc/containerd/config.toml
      [plugins."io.containerd.grpc.v1.cri".registry.configs]
        [plugins."io.containerd.grpc.v1.cri".registry.configs."registry-1.docker.io".auth]
          username = "jnuho"
          password = "******"

      [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."registry-1.docker.io"]
          endpoint = ["https://registry-1.docker.io"]

sudo systemctl restart containerd
```

[↑ Back to top](#)
<br><br>

## Argo CD

- install argocd

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

- argocd CLI

```sh
cat << EOF > install-argocd-cli.sh
VERSION=$(curl -L -s https://raw.githubusercontent.com/argoproj/argo-cd/stable/VERSION)
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/download/v$VERSION/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
EOF

chmod +x install-argocd-cli.sh
./install-argocd-cli.sh

# NOTE: INITIAL PASSWORD!
argocd admin initial-password -n argocd

argocd account update-password --server "https://localhost:8080"
```

- ingress to EXPOSE argocd 

https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/

```sh
# test with port-forward just for testing..
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

[↑ Back to top](#)
<br><br>

## Reference

- [kubernetes.io](https://kubernetes.io/docs/home/)
- [server world](https://www.server-world.info/en/note?os=Ubuntu_24.04&p=download)
- [networking-terminology](https://www.digitalocean.com/community/tutorials/an-introduction-to-networking-terminology-interfaces-and-protocols)
- [understanding-ip-subnets-and-cidr](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)
- [Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico)
- [Argo CD](https://argo-cd.readthedocs.io/en/stable/)

