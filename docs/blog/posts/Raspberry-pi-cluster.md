---
draft: false
date: 2024-08-01
categories:
  - Linux
authors:
  - junho
---

Raspberry-pi 5 cluster for a Kubernetes cluster

<img src="https://imgur.com/Av7PzuR.png" alt="pi-cluster" width="500">

<!-- more -->

# Raspberry pi 5 cluster

- [Raspberry Pi](#raspberry-pi)
    - [Enable the external PCI Express port](#enable-the-external-pci-express-port)
    - [Set NVMe early in the boot order](#set-nvme-early-in-the-boot-order)
- [Ansible](#ansible)
- [Kubernetes](#kubernetes)
- [containerd](#containerd)
- [Docker Registry](#docker-registry)
- [Reference](#reference)


## Raspberry Pi
- m.2 NVME SSD (2242) + m.2 Hat
- Cooling Fan
- Ethernet Cable (internet connection)
- Usb-C Power Cable (5A x 5V = 25W ideally)

In order to configure the pi to boot from NVME SSD, I referred to [LINK](https://www.jeffgeerling.com/blog/2023/nvme-ssd-boot-raspberry-pi-5).

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



[↑ Back to top](#)
<br><br>


## Ansible

We can automate some aspects of the Cloud Native application lifecycle using Ansible.

```sh
# install python
sudo apt install python3 python3-venv python3-pip -y
python3 -V

echo -e "import sys\nprint(sys.version)" > python3_test.py
python3 python3_test.py
  3.12.3 (main, Apr 10 2024, 05:33:47) [GCC 13.2.0]
rm python3_test.py


cd ~
python3 -m venv .venv
source .venv/bin/activate

pip install ansible
ansible --version
pip install --upgrade ansible
```

- inventory

```
# Before writing the playbook, create a file named inventory to tell Ansible how to connect to localhost:
[localhost]
127.0.0.1   ansible_connection=local
```

- playbook

```yml
# main.yml
---
- hosts: localhost
```

Now Run the ansible playbook!

```sh
ansible-playbook -i inventory main.yml
```

The best Ansible playbooks are idempotent, meaning you can run them more than one time,
and assuming the system hasn’t been changed outside of Ansible,
you’ll see no changes reported after the first time the playbook is run.
This is helpful for ensuring a consistent state across your application deployments,
and to verify there are no changes (intended or not) happening outside of your automation.


- install go

```
wget https://go.dev/dl/go1.22.5.linux-arm64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.22.5.linux-arm64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
source ~/.zshrc
```

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
vim /etc/fstab
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

cat <<EOF > kubeadm-config.yaml
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

Kubernetes 1.30 requires that you use a runtime that conforms with the Container Runtime Interface (CRI); containerd, CRI-O, Docker Engine.

I will be using [`containerd!`](https://github.com/containerd/containerd/blob/main/docs/getting-started.md)

- Install and configure prerequisites
  - 1. Enable IPv4 packet forwarding
  - 2. cgroup drivers: systemd
  - 3. container runtime - containerd

```sh
# 1. Enable IPv4 packet forwarding
#   By default, the Linux kernel does not allow IPv4 packets to be routed between interfaces.
#   sysctl params required by setup, params persist across reboots
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
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
sudo su -
containerd config default > /etc/containerd/config.toml
cat /etc/containerd/config.toml

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
sudo kubeadm init --pod-network-cidr=10.100.0.0/16 -v=5

# [init] Using Kubernetes version: v1.30.3
# [preflight] Running pre-flight checks
# [preflight] Pulling images required for setting up a Kubernetes cluster
# [preflight] This might take a minute or two, depending on the speed of your internet connection
# [preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
# W0802 17:25:33.748578    2514 checks.go:844] detected that the sandbox image "registry.k8s.io/pause:3.8" of the container runtime is inconsistent with that used by kubeadm.It is recommended to use "registry.k8s.io/pause:3.9" as the CRI sandbox image.

# [certs] Using certificateDir folder "/etc/kubernetes/pki"
# [certs] Generating "ca" certificate and key
# [certs] Generating "apiserver" certificate and key
# [certs] apiserver serving cert is signed for DNS names [kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local master] and IPs [10.96.0.1 192.168.0.10]
# [certs] Generating "apiserver-kubelet-client" certificate and key
# [certs] Generating "front-proxy-ca" certificate and key
# [certs] Generating "front-proxy-client" certificate and key
# [certs] Generating "etcd/ca" certificate and key
# [certs] Generating "etcd/server" certificate and key
# [certs] etcd/server serving cert is signed for DNS names [localhost master] and IPs [192.168.0.10 127.0.0.1 ::1]
# [certs] Generating "etcd/peer" certificate and key
# [certs] etcd/peer serving cert is signed for DNS names [localhost master] and IPs [192.168.0.10 127.0.0.1 ::1]
# [certs] Generating "etcd/healthcheck-client" certificate and key
# [certs] Generating "apiserver-etcd-client" certificate and key
# [certs] Generating "sa" key and public key
# [kubeconfig] Using kubeconfig folder "/etc/kubernetes"
# [kubeconfig] Writing "admin.conf" kubeconfig file
# [kubeconfig] Writing "super-admin.conf" kubeconfig file
# [kubeconfig] Writing "kubelet.conf" kubeconfig file
# [kubeconfig] Writing "controller-manager.conf" kubeconfig file
# [kubeconfig] Writing "scheduler.conf" kubeconfig file
# [etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
# [control-plane] Using manifest folder "/etc/kubernetes/manifests"
# [control-plane] Creating static Pod manifest for "kube-apiserver"
# [control-plane] Creating static Pod manifest for "kube-controller-manager"
# [control-plane] Creating static Pod manifest for "kube-scheduler"
# [kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
# [kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
# [kubelet-start] Starting the kubelet
# [wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests"
# [kubelet-check] Waiting for a healthy kubelet. This can take up to 4m0s
# [kubelet-check] The kubelet is healthy after 1.501769125s
# [api-check] Waiting for a healthy API server. This can take up to 4m0s
# [api-check] The API server is healthy after 7.002740784s
# [upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
# [kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
# [upload-certs] Skipping phase. Please see --upload-certs
# [mark-control-plane] Marking the node master as control-plane by adding the labels: [node-role.kubernetes.io/control-plane node.kubernetes.io/exclude-from-external-load-balancers]
# [mark-control-plane] Marking the node master as control-plane by adding the taints [node-role.kubernetes.io/control-plane:NoSchedule]
# [bootstrap-token] Using token: cc66r1.w7i0ydntja56y49x
# [bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
# [bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
# [bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
# [bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
# [bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
# [bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
# [kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
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
sudo kubeadm join 192.168.0.10:6443 --token dirh1v.jde74l3q3sy7xwhv \
        --discovery-token-ca-cert-hash sha256:718b98c04f0c5adff8b6af285bf11b6b5bc965141e54f383172d433f799edcd5
```

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
```


### Troubleshooting kubeadm

`coredns` is stuck in the Pending state. This is expected and part of the design. 

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/

```sh
k get pod -n kube-system
  NAME                             READY   STATUS    RESTARTS        AGE
  coredns-7db6d8ff4d-sv6bv         0/1     Pending   0               4h54m
  coredns-7db6d8ff4d-vtc4p         0/1     Pending   0               4h54m

k describe pod coredns-7db6d8ff4d-sv6bv -n kube-system
    # Warning  FailedScheduling  7m50s (x6 over 4h45m)  default-scheduler  0/3 nodes are available: 3 node(s) had untolerated taint {node.kubernetes.io/not-ready: }. preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.

```

### CNI

You must deploy a `Container Network Interface` (CNI) based Pod network add-on so that your Pods can communicate with each other. Cluster DNS (CoreDNS) will not start up before a network is installed. Without CNI, the coredns pods are `pending` and `podSubnet` is not specified in the cluster configuration.

: Use `Calico` as a Container Network Interface implementation!

#### Calico


```sh
# Check Pod Sunet is missing
kubectl get configmap -n kube-system kubeadm-config -o yaml
  networking:
        dnsDomain: cluster.local
        # ---> podSubnet is MISSING............
        serviceSubnet: 10.96.0.0/12
      scheduler: {}
```

1. Calico Operator - tigera-operator

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

2. Custom Resource

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
  metadata:
    annotations:
      projectcalico.org/metadata: '{"generation":1,"creationTimestamp":"2024-08-02T15:05:43Z","labels":{"app.kubernetes.io/managed-by":"tigera-operator"}}'
    creationTimestamp: "2024-08-02T15:05:43Z"
    generation: 1
    name: default-ipv4-ippool
    resourceVersion: "2656"
    uid: f26e7d00-fbac-414b-a275-9b82b8615d9c
  spec:
    allowedUses:
    - Workload
    - Tunnel
    blockSize: 26
    cidr: 10.100.0.0/16
    ipipMode: Never
    natOutgoing: true
    nodeSelector: all()
    vxlanMode: CrossSubnet
kind: List
metadata:
  resourceVersion: ""
```

[↑ Back to top](#)
<br><br>


## containerd


Why NERDCTL?

nerdctl is a Docker-compatible CLI for containerd

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
- https://www.docker.com/increase-rate-limits/


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

## Reference

- [kubernetes.io](https://kubernetes.io/docs/home/)
- [server world](https://www.server-world.info/en/note?os=Ubuntu_24.04&p=download)
- [networking-terminology](https://www.digitalocean.com/community/tutorials/an-introduction-to-networking-terminology-interfaces-and-protocols)
- [understanding-ip-subnets-and-cidr](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)
- [Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico)
- [Argo CD](https://argo-cd.readthedocs.io/en/stable/)

