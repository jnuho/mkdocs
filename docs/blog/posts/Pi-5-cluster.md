---
draft: true
date: 1900-01-01
categories:
  - Linux
authors:
  - junho
---

Raspberry pi Kuberentes cluster

<!-- more -->


# Pi 5 Cluster

I use Raspberry pi to setup local Kubernetes cluster. I tried to implement [Kuberentes the Hard way](https://github.com/kelseyhightower/kubernetes-the-hard-way).
I will document the process of the setup.

## Motivation

I wanted to set up a local kuberentes cluster on my home lab. So I bought 3 raspberry pi (1 master node + 2 worker node).

## Prerequisite

- Hardware
    - 1 master node, 2 worker nodes
    - Each has a spec of 8GB Memory, 256 GB SSD.
    - I might add more Raspberry Pi for additional proxy server in the future.

- Ubuntu 24.04 installation on each pi server.

## Ubuntu setup

```sh
```