---
draft: true
date: 2024-04-05
categories:
  - Linux
authors:
  - junho
---

A Linux Primer. I try to learn Linux commands.


<!-- more -->


# Linux Commands


## Table of Contents

- [File Permissions](#file-permissions)
- [Commands](#commands)
- [Terminology](#terminology)
- [Reference](#referecne)


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


## Commands

- [curl](#curl)

### curl

```sh
curl https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt

# output to a file
curl -O https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
ls verne_twenty-thousand-leagues.txt

# output to a specific filename
curl -o jules.txt https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
```

## Terminology

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

## Referecne

- [networking-terminology](https://www.digitalocean.com/community/tutorials/an-introduction-to-networking-terminology-interfaces-and-protocols)
- [understanding-ip-subnets-and-cidr](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking)
