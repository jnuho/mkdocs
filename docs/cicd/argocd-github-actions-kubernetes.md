---
draft: false
date: 2024-08-12
categories:
  - CICD
  - Kubernetes
authors:
  - junho
---

I will be creating a CI/CD pipeline -  Github actions as CI and Argo CD as CD. The target is a Kubernetes cluster I created in my home Raspberry pi cluster. And I'll be covering the CI/CD on AWS EKS as well. As a test bed, I will try to apply to the local Raspberry Pi cluster first.

<a href="https://imgur.com/SkvollY.gif" target="_blank"><img src="https://imgur.com/SkvollY.gif" alt="pi-cluster" width="800"></a>

<!-- more -->

# CI/CD pipeline for Kubernetes cluster

## Table of Contents

- [Github Actions](#github-actions)
- [Argo CD](#argo-cd)
    - [Install Argo CD](#install-argo-cd)
    - [Argo CD CLI](#argo-cd-cli)
    - [Configure TLS](#configure-tls)
    - [Create An Application From A Git Repository](#create-an-application-from-a-git-repository)
    - [Sync (Deploy) The Application](#sync-deploy-the-application)

## Github Actions


## Argo CD

"Argo CD is implemented as a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the Git repo)"



## Install Argo CD

<img src="https://imgur.com/ZFTjY2G.jpg" alt="pi-cluster" width="800">

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```


## Argo CD CLI

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


## Configure TLS

This default installation will have a self-signed certificate and cannot be accessed without a bit of extra work. Do one of:

```sh
# default self-signed certificate
kubectl get secret argocd-secret -nargocd -o yaml

    apiVersion: v1
    data:
      admin.password: PASSWORD_HERE
      admin.passwordMtime: PASSWORD_HERE
      server.secretkey: SECRETKEY_HERE
      tls.crt: CERT_HERE
      tls.key: KEY_HERE
    kind: Secret
    metadata:
      name: argocd-secret
      namespace: argocd
    type: Opaque
```

### Create self-signed TLS certificate

-  I referred to a book, [`Bulletproof SSL and TLS`](https://www.amazon.com/Bulletproof-SSL-TLS-Understanding-Applications/dp/1907117040).

```sh
# 1. Generate an RSA private key
openssl genrsa -out argocd.key 2048


# 2. Public key: have just the public part of a key separately
openssl rsa -in argocd.key -pubout -out argocd-public.key


# 3. Certificate Signing Request (CSR).
# This is a formal request asking a CA to sign a certificate, and it contains the public key of the
# entity requesting the certificate and some information about the entity.
# A CSR is always signed with the private key corresponding to the public key it carries.
# openssl req -new -key argocd.key -out argocd.csr
# Here, I did Unattended CSR Generation (non-interactive). it requires creating argocd.cnf beforehand.
cat << EOF > argocd.cnf
[req]
prompt = no
distinguished_name = dn
req_extensions = ext
[dn]
CN = www.catornot.com
emailAddress = cactoos555@gmail.com
O = CatOrNot Ltd
L = Seoul
C = KR

[ext]
subjectAltName = @alt_names

[alt_names]
DNS.1   = *.catornot.com
DNS.2   = catornot.com
DNS.3   = argocd-repo-server
DNS.4   = argocd-repo-server.argo-cd.svc
DNS.5   = argocd-dex-server
DNS.6   = argocd-dex-server.argo-cd.svc
IP.1    = 192.168.0.202
EOF

openssl req -new -config argocd.cnf -key argocd.key -out argocd.csr
# double-check that the CSR is correct
# openssl req -text -in argocd.csr -noout


# 4. Signing Your Own Certificates
# After a CSR is generated, use it to sign your own certificate and/or send it to a public CA
# and ask him or her to sign the certificate
# If you’re installing a TLS server for your own use, you probably don’t want to go to a CA to
# get a publicly trusted certificate. It’s much easier to sign your own. 

# (Required for) Creating Certificates Valid for Multiple Hostnames
cat << EOF > argocd.ext
subjectAltName = @alt_names
[alt_names]
DNS.1   = *.catornot.com
DNS.2   = catornot.com
DNS.3   = argocd-repo-server
DNS.4   = argocd-repo-server.argo-cd.svc
DNS.5   = argocd-dex-server
DNS.6   = argocd-dex-server.argo-cd.svc
IP.1    = 192.168.0.202
EOF

openssl x509 -req -days 3650 -in argocd.csr -signkey argocd.key -out argocd.crt -extfile argocd.ext

# examine the created certificate
openssl x509 -text -in argocd.crt -noout
```

### Create secrets using Self-signed certificate

- [TLS configuration](https://argo-cd.readthedocs.io/en/stable/operator-manual/tls/)

"Argo CD provides three inbound TLS endpoints that can be configured:"

- argocd-server
    - `argocd-server-tls` (higher priority) or `argocd-secret` (deprecated) secret that stores tls.crt and tls.key
    - if tls.crt and tls.key are found in neither of above secrets, a self-signed certificate is generated into `argocd-secret`

```sh
# To create this secret manually from an existing key pair, you can use kubectl:
# Argo CD will pick up changes to the argocd-server-tls secret automatically
# and will not require restart of the pods to use a renewed certificate.
cd argocd_certs
```

kubectl create secret tls catornot-tls \
  --cert=./argocd.crt \
  --key=./argocd.key

- argocd-repo-server

```sh
kubectl create -n argocd secret tls argocd-repo-server-tls \
  --cert=./argocd.crt \
  --key=./argocd.key

k get deploy/argocd-repo-server -nargocd
    NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
    argocd-repo-server                 1/1     1            1           16h

k rollout restart deploy/argocd-repo-server -nargocd
k get pod -nargocd
```

- argocd-dex-server
    - NOTE: as opposed to argocd-server, the argocd-repo-server is not able to pick up changes
    - to this secret automatically. If you create (or update) this secret,
    - the argocd-repo-server pods need to be `restarted`.

```sh
kubectl create -n argocd secret tls argocd-dex-server-tls \
  --cert=./argocd.crt \
  --key=./argocd.key

k get deploy/argocd-dex-server -nargocd
    NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
    argocd-dex-server                 1/1     1            1           16h

k rollout restart deploy/argocd-dex-server -nargocd
k get pod -nargocd
```

#### Configuring TLS between Argo CD components

- Configuring TLS to argocd-repo-server
    - Modify the pod startup parameters for argocd-server and argocd-application-controller
    - to include the `--repo-server-strict-tls` parameter.

```sh
kubectl get deploy/argocd-server -nargocd
    NAME            READY   UP-TO-DATE   AVAILABLE   AGE
    argocd-server   1/1     1            1           17h
kubectl edit deployment argocd-server -n argocd
    spec:
      containers:
      - args:
        - /usr/local/bin/argocd-server
        - --repo-server-strict-tls
        name: argocd-server


kubectl get statefulsets/argocd-application-controller -n argocd
    NAME                            READY   AGE
    argocd-application-controller   1/1     17h
kubectl edit statefulset argocd-application-controller -n argocd
    spec:
      containers:
      - args:
        - /usr/local/bin/argocd-application-controller
        - --repo-server-strict-tls
```

- Configuring TLS to argocd-dex-server
    - Modify the pod startup parameters for argocd-server to include the --dex-server-strict-tls parameter.

```sh
kubectl get deploy/argocd-server -nargocd
    NAME            READY   UP-TO-DATE   AVAILABLE   AGE
    argocd-server   1/1     1            1           17h
kubectl edit deployment argocd-server -n argocd
    spec:
      containers:
      - args:
        - /usr/local/bin/argocd-server
        - --repo-server-strict-tls
        - --dex-server-strict-tls
        name: argocd-server
```


### Check argocd-server pods if it correctly uses the created certificate!

```sh
kubectl exec -it argocd-server-66688f65d6-xdcl8 -nargocd /bin/bash
ls /app/config/server/tls

openssl x509 -text -in /app/config/server/tls/tls.crt -noout
```

### Register A Cluster To Deploy Apps To (Optional)

In case, argocd need to deploy application to a different Kubernetes cluster than the cluster that argocd is running in.
When deploying internally (to the same cluster that Argo CD is running in),
`https://kubernetes.default.svc` should be used as the application's K8s API server address.


```sh
argocd cluster list
    SERVER                          NAME        VERSION  STATUS   MESSAGE                                                  PROJECT
    https://kubernetes.default.svc  in-cluster           Unknown  Cluster has no applications and is not being monitored.


    arn:aws:eks:ap-northeast-2:094833749257:cluster/my-cluster
kubectl config get-contexts -o name
    minikube
    pi
argocd cluster add pi

argocd cluster list
    SERVER                          NAME        VERSION  STATUS      MESSAGE                                                  PROJECT
    https://192.168.0.10:6443       pi          1.30     Successful
    https://kubernetes.default.svc  in-cluster           Unknown     Cluster has no applications and is not being monitored.
```

.kube/config
    server: https://192.168.0.10:6443

## Ingress Configuration

- [Kubernetes/ingress-nginx](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#kubernetesingress-nginx)
    - [Option 1: SSL-Passthrough](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-1-ssl-passthrough)
    - [Option 2: SSL Termination at Ingress Controller](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-ssl-termination-at-ingress-controller)

### Option 1: SSL-Passthrough

- `--enable-ssl-passthrough` argument to `ingress-nginx-controller` container spec of deployment.

```sh
# curl -L https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.1/deploy/static/provider/cloud/deploy.yaml -o ingress-nginx.yaml
# vim ingress-nginx.yaml
# OR:
kubectl edit deploy ingress-nginx-controller -ningress-nginx
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ingress-nginx-controller
  namespace: ingress-nginx
spec:
  template:
    spec:
      containers:
      - args:
        - /nginx-ingress-controller
        - --enable-ssl-passthrough
```

- Helm `values.pi.yaml`

```yaml
# Helm values for argocd INGRESS
  - name: argocd-ingress
    namespace: argocd
    ingressClassName: nginx
    annotations:
      nginx.ingress.kubernetes.io/force-ssl-redirect: "true"
      nginx.ingress.kubernetes.io/ssl-passthrough: "true"
    tls:
    - hosts:
      - argocd.catornot.com
      secretName: argocd-server-tls
    hosts:
      - host: argocd.catornot.com
        http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: argocd-server
                port:
                  number: 443
```

- hosts file

```
192.168.0.201 catornot.com
192.168.0.201 argocd.catornot.com
```


- (Optional) Without using ingress configuration

```sh
# Method 1. port-forward just for testing
# kubectl port-forward svc/argocd-server -n argocd 8080:443

# Method 2. Service of LoadBalancer type and ROLLBACK to use ingress instead
kubectl get svc/argocd-server -n argocd
    NAME            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
    argocd-server   ClusterIP   10.98.233.38   <none>        80/TCP,443/TCP   15h

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
kubectl get svc/argocd-server -n argocd
    NAME            TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    argocd-server   LoadBalancer   10.98.233.38   192.168.0.202   80:32216/TCP,443:32427/TCP   15h

# Access available: http://192.168.0.202

# ROLLBACK
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "ClusterIP"}}'
```

### Create An Application From A Git Repository

- Create apps via CLI or UI

```sh
argocd login argocd.catornot.com
kubectl config get-contexts -o name
argocd cluster add pi

kubectl config set-context --current --namespace=argocd
argocd app create catornot --repo https://github.com/jnuho/infra.git --path helm-chart/cat-chart --dest-server https://kubernetes.default.svc --dest-namespace default

kubectl config set-context --current --namespace=default
kubectl config get-contexts
```

## Sync (Deploy) The Application

- Syncing via CLI or UI

```sh
argocd app get catornot

Name:               argocd/catornot
Project:            default
Server:             https://kubernetes.default.svc
Namespace:          default
URL:                https://argocd.catornot.com/applications/catornot
Source:
- Repo:             https://github.com/jnuho/infra.git
  Target:
  Path:             helm-chart/cat-chart
SyncWindow:         Sync Allowed
Sync Policy:        Manual
Sync Status:        Synced to  (1fc839b)
Health Status:      Healthy


argocd app sync catornot
```