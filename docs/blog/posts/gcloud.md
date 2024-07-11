---
draft: true
date: 2024-07-01
categories:
  - Project
  - GCP
authors:
  - junho
---

### GCP implementation

- Create google account to get free credit for gcloud

- create ubuntu vm
- ip restriction
- install google cloud sdk and init

<!-- more -->

```sh
gcloud compute security-policies create my-security-policy
gcloud compute security-policies rules create 1000 \
    --security-policy my-security-policy \
    --action allow \
    --src-ip-ranges <your-home-ip>
gcloud compute security-policies rules create 2000 
    --security-policy my-security-policy \
    --action deny \
    --src-ip-ranges 0.0.0.0/0
gcloud compute backend-services update <your-backend-service> \
    --security-policy my-security-policy
```

- GCP console setup
    - vm instacne : create with machine type(E2- memory 4GB)
    - VPC network : firewalls > add filewall rule (your ip)

- gcp ssh connect

```sh
gcloud compute ssh --zone "REGION" "INSTANCE_NAME" --project "PROJECT_NAME"
```



[↑ Back to top](#)
<br><br>


- Google Kubernetes Engine
    - <a href="https://www.youtube.com/watch?v=P1x1Rk_TzV4" target="_blank">Ingress in 5 Minutes</a>
    - <a href="https://youtu.be/8RQvtagsrg0?si=IwP0qNMz0kutUOVo" target="_blank">GKE Load Balancing</a>
    - <a href="https://youtu.be/jW_-KZCjsm0?si=u8-842mszl7O9Kr3" target="_blank">GKE tutorial</a>
    - https://www.youtube.com/watch?v=QvVmQtO-ftU&ab_channel=GoogleCloudTech

- GKE provides a variety of Kubernetes-native constructs to manage L4 and L7 load balancers on Google Cloud.
    - Service, Ingress, Gateway, Network endpoint groups
    - GKE load balancers work by routing traffic to pods based on a set of rules
    - Exposing services outside of the cluster
        - NodePort Service
            - uses GKE Node IP, exposes a service on the "same" port on every Node
        - Load Balancer Service
            - L4 routing (TCP/UDP), allocates a routable IP+port to a Cloud Load Balancer and uses a Node Port to forward traffic to backend pods
        - Ingress/Gateway
            - L7 routing (HTTP/S), allocates a routable IP + HTTP/S ports to a Cloud Load Balancer and uses Pods' IP address to forward traffic directly


0. Create new project and enable Google Kuberentes Engine api

1. Create Kubernetes cluster (console/cli)
    - in console create a cluster
    - 3 nodes, 6CPUs 12 GB

```sh
gcloud container clusters create my-cluster --zone=asia-northeast3-a --num-nodes=3 --machine-type=n1-standard-2

gcloud container clusters list
```

2. Download and install Google Cloud SDK (gcloud)

```sh
gcloud version
gcloud components install kubectl
```

3. Authenticate with gcloud
    - authenticate using your google cloud credentials

```sh
gcloud auth login
```

4. Configure kubectl to Use Your GKE Cluster

```sh
# set the default project for all gcloud commands
gcloud config set project poised-cortex-422112-g5

# Connect to cluster
# `in console 3 dots > Connect` gives a command:
gcloud container clusters get-credentials my-cluster --zone asia-northeast3-a --project poised-cortex-422112-g5
#     > kubeconfig entry generated for my-cluster

# Deploy microservices by creating deployment and service
kubectl create deployment hello-world-rest-api --image=jnuho/fe-nginx:latest

kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080

kubectl get service
    TYPE                 CLUSTER-IP         EXTERNAL-IP
    LoadBalancer 10.80.13.230     <pending>

k get svc --watch
    TYPE                 CLUSTER-IP         EXTERNAL-IP
    LoadBalancer 10.80.13.230     35.184.204.214

curl 35.184.204.214:8080/hello-world
```


[↑ Back to top](#)
<br><br>


- golang cloud library to create VM
    - Create Service account
        - IAM & Admin > Service accounts > Create Service account
            - Assign the `Compute Admin` role
            - click 3 dots for 'Key Management'
            - Create key (JSON) and download and rename `gcp-sa-key.json`
    - Write golang code to execute to create GCP VM.

```
gcp_credential="my-sa-key.json"
gcp_vm_region="asia-northeast3"
gcp_vm_zone="asia-northeast3-a"
gcp_vm_machine_type="e2-medium"
#ubuntu 24.04 50GB
#gcp_vm_boot_disk=50GB
#gcp_vm_identity_and_api_access="Allow full access to all Cloud APIs
#gcp_vm_firewall="http,https,loadbalancer_health_check"
```


- Download Google Cloud SDK and use gcloud to access vm

```sh
gcloud init
gcloud compute ssh instance-20240620-115251 --zone asia-northeast3-a
```

[↑ Back to top](#)
<br><br>