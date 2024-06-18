---
draft: false
date: 2022-03-01
categories:
  - project
authors:
  - junho
---

- What I learned about AWS (EC2, VPC, ElastiCache) while I worked at Rowem. Inc.

![diagram](https://d2cg24p20j4o18.cloudfront.net/playvote/000/20210819/82331f92-bc8c-403e-a1d1-5d51bc6fec79.jpg)

<!-- more -->

AWS Infra

- Public/private subnets in a VPC
- Security Group inbound port 6379 open
- ElastiCache Cluster : choose created VPC, Subnets
	- VPC: ElastiCache must be in a same VPC as EC2
	- Subnet Group: choose private Subnet

Create AWS Resources in the following order:

1. [VPC](#vpc)
2. [Internet Gateway](#internet-gateway)
3. [Subnet, Routing Table](#subnet-routing-table)
4. [Security Group](#security-group)
5. [EC2](#ec2)
5. [ElastiCache](#elasticache)

VPC

- CIDR 172.20.0.0/16

Internet Gateway

- attach to VPC

Subnet, Routing Table

- Public
  - Subnet : CIDR 172.20.0.0/24
  - Routing table - add internet gateway and link to subnet

- Private
  - Subnet : CIDR 172.20.10.0/23
  - Routing table - link to private subnet

- Security Group

Define security groups in a VPC

  - sg-bastion
    - inbound: SSH yourip:22

  - sg-starpass-was
    - inbound: sg-bastion:22

  - sg-starpass-redis
    - inbound: sg-was/web/bastion:6379

EC2

- install redis client in EC2 instance

```sh
# Install from source
# wget http://download.redis.io/redis-stable.tar.gz
# tar -xvzf redis-stable.tar.gz
# cd redis-stable
# make && make install

# Install using package manager (Ubuntu)
sudo apt update
sudo apt install redis

# Connect to Redis
redis-cli -h {ElastiCache endpoint} -p {port defined in a SG 6379}

> flushall
> keys *
```

ElastiCache

- Redis
- Node type: select memory type (r5, m5,r4,m4,r3,m3,t3,t2) and network type
- Create subnet group : same VPC as starpass-was-00, starpass-bastion > Select private subnet
- Select sg-starpass-redis for security group
- Uncheck auto-backup


Test

- ElastiCache is only accessible from ip defined in the Security Group inbound rules.
- EC2 redis-cli connection test to check jedis working from Spring environemnt.
- Test cache storing by using apache web server in EC2

