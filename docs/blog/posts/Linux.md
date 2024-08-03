---
draft: false
date: 2024-07-01
categories:
  - Kubernetes
  - Linux
authors:
  - junho
---

Over the course of the Raspberry-pi cluster setup, I tried to record Linux knowledge I learned.

<!-- more -->

# Table of contents

- [Linux Primer](#linux-primer)
    - [File Permissions](#file-permissions)
    - [curl](#curl)
    - [terminology](#terminology)
    - [Subnetting](#subnetting)
- [Ubuntu](ubuntu)
    - [Time sync](#time-sync)
    - [SSH access](#ssh-access)
    - [Initial Settings](#initial-settings)
    - [minikube](#minikube)
- [Reference](#reference)



# Linux Primer

Linux basics.

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

## Reference

- [server world](https://www.server-world.info/en/note?os=Ubuntu_24.04&p=download)
- [networking-terminology](https://www.digitalocean.com/community/tutorials/an-introduction-to-networking-terminology-interfaces-and-protocols)
- [understanding-ip-subnets-and-cidr](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)

