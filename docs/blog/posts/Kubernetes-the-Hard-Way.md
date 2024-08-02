---
draft: false
date: 2024-08-01
categories:
  - Kubernetes
  - Linux
authors:
  - junho
---


I read through [`kubernetes.io`](https://kubernetes.io/docs/home/) documentation to set-up local Kubernetes cluster with 1-master and 2-worker node in Raspberry pi 5 cluster.

<img src="https://imgur.com/YZT2OTv.png" alt="pi-cluster" width="500">

<!-- more -->

# Kubernetes the Hard way

- [Linux Primer](#linux-primer)
    - [File Permissions](#file-permissions)
    - [curl](#curl)
    - [terminology](#terminology)
    - [Subnetting](#subnetting)
- [Raspberry Pi](#raspberry-pi)
- [Ubuntu](ubuntu)
    - [Time sync](#time-sync)
    - [SSH access](#ssh-access)
    - [Initial Settings](#initial-settings)
    - [minikube](#minikube)
- [Ansible](#ansible)
- [Kubernetes](#kubernetes)
- [Reference](#reference)



# Linux Primer

## File Permissions

```sh
ls -l
    drwxr-xr-x. 4 root root    68 Jun 13 20:25 tuned
    -rw-r--r--. 1 root root  4017 Feb 24  2022 vimrc
```

- File type: - or d
- Permission settings: rw-r--r--
- Extended attributes: dot (.)
- User owner: root
- Group owner: root
- Others
    - First, it checks if you are the file's `owner`. If so, you get the owner's permissions.
    - If not, it checks if you belong to the file's `group`; if so, you get the group's permissions.
    - If neither, "others" permissions apply. These fields are mutually exclusive, so you can't be covered by more than one.

[↑ Back to top](#)
<br><br>

## curl

```sh
curl https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt

# output to a file
curl -O https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
ls verne_twenty-thousand-leagues.txt

# output to a specific filename
curl -o jules.txt https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
```

## terminology

- `Connection`: In networking, a connection refers to pieces of related information that are transferred through a network. Generally speaking, a connection is established before data transfer (by following the procedures laid out in a protocol) and may be deconstructed at the end of the data transfer.
- `Packet`: A packet is the smallest unit that is intentionally transferred over a network. When communicating over a network, packets are the envelopes that carry your data (in pieces) from one end point to the other. The main portion of a packet contains the actual data being transferred. It is sometimes called the body or the payload. Packets have a header portion that contains information about the packet including the source and destination, timestamps, network hops, etc. The main portion of a packet contains the actual data being transferred. It is sometimes called the body or the payload.
- `Network Interface`: A network interface can refer to any kind of software interface to networking hardware. For instance, if you have two network cards in your computer, you can control and configure each network interface associated with them individually. A network interface may be associated with a physical device, or it may be a representation of a virtual interface. The “loopback” device, which is a virtual interface available in most Linux environments to connect back to the same machine, is an example of this.
- `LAN`: LAN stands for “local area network”. It refers to a network or a portion of a network that is not publicly accessible to the greater internet. A home or office network is an example of a LAN.
- `WAN`: WAN stands for “wide area network”. It means a network that is much more extensive than a LAN. While WAN is the relevant term to use to describe large, dispersed networks in general, it is usually meant to mean the internet, as a whole. If an interface is said to be connected to the WAN, it is generally assumed that it is reachable through the internet.
- `Protocol`: A protocol is a set of rules and standards that define a language that devices can use to communicate. Some low level protocols are TCP, UDP, IP, and ICMP. Some familiar examples of application layer protocols, built on these lower protocols, are HTTP (for accessing web content), SSH, and TLS/SSL.
- Port: A port is an address on a single machine that can be tied to a specific piece of software. It is not a physical interface or location, but it allows your server to be able to communicate using more than one application.
- `Firewall`: A firewall is a program that decides whether traffic coming or going from a server should be allowed. A firewall usually works by creating rules for which type of traffic is acceptable on which ports. Generally, firewalls block ports that are not used by a specific application on a server.
- `NAT`: NAT stands for network address translation. It is a way to repackage and send incoming requests to a routing server to the relevant devices or servers on a LAN. This is usually implemented in physical LANs as a way to route requests through one IP address to the necessary backend servers.
- `VPN`: VPN stands for virtual private network. It is a means of connecting separate LANs through the internet, while maintaining privacy. This is used to connect remote systems as if they were on a local network, often for security reasons.


- `Hub`
    - problem of data collision
    - Frame stores mac address (6-byte; Hexadecimal `fe:1b:63:84:45:e6`) to specify sender, receiver
        - 3-byte(octet) Organisationally Unique, 3-octet(byte) Network Interface Controller specific
    - from mac-addr-1 to mac-addr-2

- `Ethernet Frame`
    - = PREAMBLE 7 + SFD 1 + DEST_MAC_ADDR 6 + SOURCE_MAC_ADDR 6 + LENGTH 2 + ETHERNET_TYPE + DATA 46-1500 + CRC 4
    - like an evelope in a Hub
    - SFD indicates the start of the data after 1-byte (10101011)
    - ETHERNET_TYPE: 0x 0806: ARP Packet, 0x0800: Ip Packet
    - DATA contains ARP Request packet / IP Request packet
    - CRC: Hash pattern

- `Switch`
    - advanced; solve a lot of problems of `Hub`
    - no data collision; in flow and out flow lanes do not intercept
    - remember mac adresses for each port
    - it forms LAN that contains many local PCs and devices
    - switch forms LAN -> LANs can be connected with Router : WAN
    - Routers can be also connected with each other: DO NOT USE Mac Address!
    - Mac Addresses can not be used in router-to-router connection
        - use Ip address instead.

- `WAN`
    - intranet or internet

- `Ip address`
    - can be allocated statically or dynamically.

- `Ethernet Frame` and `Packet`
    - `Packet` inside Frame's Data bytes
    - `Packet` contains
        - Protocol
        - Source IP Address
        - Dest IP Address
        - Data
    - only `Packet` travels through Routers and encapsulated in LAN again


- `Routing`
    - LAN do not know about Mac Addr of a Router. So how to travel through Router to another Router and into another LAN?
    - Address Resolution Protocol (ARP) allows ip address to resolve to Mac Addr
    - Send Frame to Router and Packet can travel afterward!
        - Mac Addr: Hardware info
        - Ip Addr: Hardware Location info

- `ARP` Request packet
    - Send ARP Packet to know the Mac Address of the Destination Device
    - `Request ARP packet`: SOURCE_IP + DEST_IP + request_mac_ip 00:00:00:00
    - DEST_IP: Router ip (DEFAULT GATEWAY in Windows) 192.168.0.1
    - `Reply ARP packet`: Router reply with Mac_addr
    - Frame (with Mac_addr) + `ip packet` => Send to Router => Send `ip packet` to other Router in `WAN`

- Router's Mac Addr is identified using communication of ARP packet
- Use this Router's Mac Addr to send IP Packet (contains Source IP Addr and Destination Ip Addr)



- IP class
    - A class:
        - 1-126. 0-255. 0-255. 0-255
        - Network.HOST.HOST.HOST
        - Subnet Mask 255.0.0.0; `CIDR` /8
    - 127.0.0.0 ~ 127.255.255.255: Host Addr (Loopback address)
        - for checking operating system and networks are connected
    - B class:
        - 128-191. 0-255. 0-255. 0-255
        - Network.Network.HOST.HOST
        - Subnet Mask 255.255.0.0; `CIDR` /16
    - C class:
        - 192-223. 0-255. 0-255. 0-255
        - Network.Network.Network.HOST
        - Subnet Mask 255.255.255.0; `CIDR` /24
        - Subnet Mask: (Network 1's, Host 0's)

Use Subnet Mask to determine which ip class is for a given IP.


[↑ Back to top](#)
<br><br>


## Subnetting

Internet Service Provider (ISP) provides a IPv4 range e.g. 200.100.100.0/24.
Suppose I have 4 teams to get assigned IP ranges.

- Class C: `Network, Network, Network, Host`; CIDR /24; total 254 ips
    - Network address 200.100.100.0
    - Broadcast address DHCP 200.100.100.255
    - 200.100.100.1 ~ 200.100.100.64
    - 200.100.100.65 ~ 200.100.100.128
    - 200.100.100.129 ~ 200.100.100.192
    - 200.100.100.193 ~ 200.100.100.254
    - Without Router, Switch connects all devices in LAN

- CIDR range for each team: 
    - 200.100.100.0/26  255.255.255.192
    - 200.100.100.64/26  255.255.255.192
    - 200.100.100.128/26  255.255.255.192
    - 200.100.100.192/26  255.255.255.192
    - Subnet Mask 11111111 1111111 11111111 11000000

- Class C CIDR /24: take 0 bit from Host; # of subnet = 1
    - Host 00000000
- Class C CIDR /25: take 1 bit from Host; # of subnet = 2
    - Host 00000000
    - Host 10000000
- Class C CIDR /26: take 2 bits from Host; # of subnet = 4
    - Host 00000000
    - Host 10000000
    - Host 01000000
    - Host 11000000
- Class C CIDR /27: take 3 bits from Host; # of subnet = 8
    - Host 00000000
    - Host 10000000
    - Host 01000000
    - Host 00100000
    - Host 01100000
    - Host 10100000
    - Host 11000000
    - Host 11100000


[↑ Back to top](#)
<br><br>

## Raspberry Pi

- NVMe SSD boot : https://www.jeffgeerling.com/blog/2023/nvme-ssd-boot-raspberry-pi-5

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


## Ubuntu

- install Ubuntu 24.04 LTS server on Raspberry Pi 5

### Time sync

- Use `timedatectl` and `timesyncd` instead of `ntp` for time synchronization
    - https://askubuntu.com/a/1418563
    - https://ubuntu.com/server/docs/use-timedatectl-and-timesyncd
    - https://www.server-world.info/en/note?os=Ubuntu_24.04&p=ntp&f=3
- (Optional) Use `chrnony` to server NTP server.
    - install and configure `chronyd`


```sh
# Deprecated : ntpd, ntpdate
sudo systemctl stop ntpd
sudo systemctl disable ntpd
sudo apt-get remove ntp ntpdate

sudo timedatectl set-timezone Asia/Seoul

sudo apt update
sudo apt install systemd-timesyncd -y

# The server from which to fetch time for timedatectl and timesyncd can be specified
sudo vim /etc/systemd/timesyncd.conf
[Time]
NTP=time.bora.net
PollIntervalMinSec=32
PollIntervalMaxSec=600

sudo systemctl enable systemd-timesyncd
sudo systemctl restart systemd-timesyncd

timedatectl timesync-status
date
```

[↑ Back to top](#)
<br><br>

### SSH access

- https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys

By default password ssh is disabled on Ubuntu 24.04.

1. ENABLE password ssh
2. Create Public key and copy the public key content into the target server
3. DISABLE password ssh

```sh
# 1. ENABLE password ssh via direct console access to Raspberry pi 5 hardware
sudo su -
vim /etc/ssh/sshd_config.d/50-cloud-init.conf
    PasswordAuthentication yes
systemctl restart ssh

# 2. Create Public key to enable ssh with public key and copy the public key content into the target server's ~/.ssh/authorized_keys manually!
ssh-keygen
ssh-copy-id ubuntu@192.168.0.23
    # /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/foo/.ssh/id_ed25519.pub"
    # /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    # /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    # ubuntu@192.168.0.23's password:

    # Number of key(s) added: 1

    # Now try logging into the machine, with:   "ssh 'ubuntu@192.168.0.23'"
    # and check to make sure that only the key(s) you wanted were added.

# ssh WITHOUT password; NOW ssh with public key intead!
ssh ubuntu@192.168.0.23

# 3. DISABLE password ssh AGAIN!
sudo su -
vim /etc/ssh/sshd_config.d/50-cloud-init.conf
    PasswordAuthentication no
systemctl restart ssh
```

[↑ Back to top](#)
<br><br>

### Initial Settings

- (01) Add User Accounts
- (02) Enable root User Account
- (03) Network Settings
- (04) Service Settings
- (05) Update System
- (06) Vim Settings
- (07) Sudo Settings
- (08) Hostname


```sh
#----------------------
# (01) Add User Accounts
sudo adduser mobb
sudo usermod -aG sudo mobb
su - mobb
cd /home/mobb
mkdir .ssh
chmod 700 ~/.ssh

sudo chmod 600 ~/.ssh/authorized_keys
sudo chown mobb:mobb ~/.ssh/authorized_keys

sudo ls -al /home/mobb/.ssh



#----------------------
# (02) Enable root User Account
# To use root priviledges, basically it's better to use the sudo command with administrative accounts.



#----------------------
# (03) Network Settings
# Change to static IP addres if you use Ubuntu as a server.

sudo su -
cd /etc/netplan
mv /etc/netplan/50-cloud-init.yaml /etc/netplan/50-cloud-init.yaml.orig
touch /etc/netplan/01-netcfg.yaml
chmod 600 /etc/netplan/01-netcfg.yaml

network:
  ethernets:
    # interface name
    eth0:
      dhcp4: false
      # IP address/subnet mask
      addresses: [192.168.0.11/24]
      # default gateway
      # [metric] : set priority (specify it if multiple NICs are set)
      # lower value is higher priority
      routes:
        - to: default
          via: 192.168.0.1
          metric: 100
      nameservers:
        # name server to bind
        addresses: [8.8.8.8, 8.8.4.4]
        # DNS search base
        #search: [srv.world,server.education]
      dhcp6: false
  version: 2

sudo netplan apply
sudo journalctl -u systemd-networkd

ip addr



#----------------------
# (04) Service Settings
# Display services.
systemctl -t service

# If there are some unnecessary services,
# it's possible to Stop and turn OFF auto-start setting like follows.
# (possible to omit [.service] words)
systemctl list-unit-files -t service



#----------------------
# (07) Sudo Settings

#----------------------
# (08) Hostname
sudo hostnamectl set-hostname master
sudo hostnamectl set-hostname worker1
sudo hostnamectl set-hostname worker2
```

[↑ Back to top](#)
<br><br>

### minikube

```sh
# install in ARM 64 system
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_arm64.deb
sudo dpkg -i minikube_latest_arm64.deb

minikube start --cpus 4 --memory 4g


# Minikube recommends building images inside the Minikube environment,
# and to do that, set your local docker CLI to use Minikube’s Docker daemon:
eval $(minikube docker-env)
docker build -t hello-go .

kubectl create deployment hello-go --image=hello-go
kubectl edit deployment hello-go
    containers:
    - image: hello-go
      imagePullPolicy: IfNotPresent
      name: hello-go

# Note that, when running Minikube, a LoadBalancer service won’t acquire an external IP address
# Locally, Minikube doesn’t integrate with another service to run external load balancers.
# in most other environments, when you use a Kubernetes LoadBalancer,
# it will provision a load balancer external to your cluster, for example
# an Elastic Load Balancer (ELB) in AWS, or a Cloud Load Balancer in GKE.

kubectl expose deployment hello-go --type=LoadBalancer --port=8180
kubectl get service hello-go
    NAME      TYPE          CLUSTER-IP    EXTERNAL-IP     PORT(S)
    hello-go  LoadBalancer  10.110.50.96  <pending>       8180:31565/TCP

minikube service hello-go
    http://192.168.64.31:31565

kubectl logs -l app=hello-go -f
kubectl scale deployments/hello-go --replicas=4
kubectl get deployment hello-go

# CLEAN UP
kubectl delete service hello-go
kubectl delete deployment hello-go
eval $(minikube docker-env)
docker rmi hello-go

# To conserve your workstation’s CPU and memory, it’s a good idea to at least stop
# Minikube (minikube stop) when you’re not using it.
minikube stop
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
  - 3. container runetime - containerd

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

# 3. container runetime - containerd
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

### CNI (Container Network Interface)


Without CNI, the coredns pods are `pending` and `podSubnet` is not specified in the cluster configuration..

Use `Calico` as a Container Network Interface implementation!


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

### Installing a Pod network add-on

You must deploy a Container Network Interface (CNI) based Pod network add-on so that your Pods can communicate with each other. Cluster DNS (CoreDNS) will not start up before a network is installed.

[↑ Back to top](#)
<br><br>

## Reference

- [kubernetes.io](https://kubernetes.io/docs/home/)
- [server world](https://www.server-world.info/en/note?os=Ubuntu_24.04&p=download)
- [networking-terminology](https://www.digitalocean.com/community/tutorials/an-introduction-to-networking-terminology-interfaces-and-protocols)
- [understanding-ip-subnets-and-cidr](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)
- [Calico](https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico)
- [Argo CD](https://argo-cd.readthedocs.io/en/stable/)

