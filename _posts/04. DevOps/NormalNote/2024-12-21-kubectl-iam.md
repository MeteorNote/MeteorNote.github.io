---
title: Kubernetes IAM 인증 사용자 관리(ConfigMap)
layout: single
categories: DevOps
tags:
  - Kubernetes
  - AWS
  - NCP
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# IAM 인증 사용자 관리(ConfigMap)
## 1) 개요
Kubernetes는 클러스터 내 자원 접근을 제어하기 위해 다양한 인증 및 권한 부여 메커니즘을 제공합니다. 클라우드 상에서의 Kubernetes를 제어 및 관리하기 위해 IAM을 활용하여 리소스에 대한 액세스를 세분화하여 관리할 수 있습니다.
그 중 ConfigMap을 활용한 사용자 관리는 IAM 인증 사용자 정보를 Kubernetes 클러스터에 설정하고 관리하는 데 효과적인 방법입니다. ConfigMap은 Kubernetes의 기본 리소스로 비밀 정보가 아닌 데이터를 저장하고 환경 설정으로 활용할 수 있도록 지원합니다. 이를 통해 IAM 사용자 및 Role에 대한 매핑 정보를 클러스터 내에서 체계적으로 관리할 수 있습니다.
<br>

## 2) 설치 및 설정 - 예시 (NCP)
설치 내용은 아래 링크를 참고하였습니다.<br>
<a href="https://guide.ncloud-docs.com/docs/k8s-iam-auth-ncp-iam-authenticator" style="color: #0366d6; text-decoration: none; font-weight: bold;">
    NCP IAM Auth 설치 가이드
</a>

<h3> NCP IAM Authenticator 설치 </h3>

```shell
curl -o ncp-iam-authenticator -L https://github.com/NaverCloudPlatform/ncp-iam-authenticator/releases/latest/download/ncp-iam-authenticator_linux_amd64
chmod +x ./ncp-iam-authenticator
mkdir -p $HOME/bin && cp ./ncp-iam-authenticator $HOME/bin/ncp-iam-authenticator && export PATH=$PATH:$HOME/bin
echo 'export PATH=$PATH:$HOME/bin' >> ~/.bash_profile
```
<h3> NCP API 키 등록 </h3>

```shell
mkdir .ncloud
cat << EOF > .ncloud/configure
[DEFAULT]
ncloud_access_key_id = {Ncloud API AccessKey}
ncloud_secret_access_key = {Ncloud API SecretKey}
ncloud_api_url = https://ncloud.apigw.ntruss.com
EOF
```
<h3> kubeconfig 파일 생성 </h3>

```shell
ncp-iam-authenticator create-kubeconfig --region <region-code> --clusterUuid <cluster-uuid> --output kubeconfig.yaml

# 멀티 클러스터 (참고)
ncp-iam-authenticator update-kubeconfig --region KR --clusterUuid <cluster>
```

<h3> kubectl 설치 </h3>

```shell
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client --output=yaml
```

<h3> kubectl 실행 </h3>

```shell
kubectl get node --kubeconfig kubeconfig.yaml
cp kubeconfig.yaml .kube/config

vim ~/.bash_profile
alias kubectl='kubectl --kubeconfig="/root/kubeconfig.yaml"'
alias k=kubectl

source ~/.bash_profile
```
<br>
## 3) Kubernetes Configmap & Clusterrole 설정
<h3> Configmap </h3>

```shell
apiVersion: v1
kind: ConfigMap
metadata:
  name: ncp-auth
  namespace: kube-system
data:
  authenticateAll: "true"
```
<h3> Clusterrole </h3>

```shell
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: full-access-clusterrole
rules:
- apiGroups:
  - "*"
  resources:
  - "*"
  verbs:
  - "*"
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
 name: full-access-binding
subjects:
- kind: Group
  name: ncp-sub-account-group:그룹이름
  apiGroup: rbac.authorization.k8s.io
roleRef:
 kind: ClusterRole
 name: full-access-clusterrole
 apiGroup: rbac.authorization.k8s.io
```
위와 같이 설정하면 특정 그룹의 인원이 Kubernetes 내 모든 동작을 관리할 수 있게 됩니다.

## 4) Trouble Shooting
클라우드 상에서의 Kubernetes 운영은 Sub Account와 IAM 정책에 맞게 접근 관리가 필요하며 관리중 아래와 같은 에러를 처리할 수 있어야합니다.
<div class="notice--danger">
<h3> Error 1 </h3>
couldn't get current server API group list: the server has asked for the client to provide credentials
error: You must be logged in to the server (the server has asked for the client to provide credentials)
</div>
<div class="notice--success">
1) kubectl이 사용할 수 있는 인증 정보가 없는 경우 <br>
2) kubectl이 잘못된 컨텍스트를 사용하고 있는 경우 <br>
3) Kubernetes API 서버에 접근하려는 사용자가 올바른 권한을 가지고 있지 않은 경우
</div>
<br>
<div class="notice--danger">
<h3> Error 2 </h3>
"Unhandled Error" err="couldn't get current server API group list: Get \"http://localhost:8080/api?timeout=32s\": dial tcp 127.0.0.1:8080: connect: connection refused"
The connection to the server localhost:8080 was refused - did you specify the right host or port?
</div>
<div class="notice--success">

</div>
<br>
<div class="notice--danger">
<h3> Error 3 </h3>
error: You must be logged in to the server (Unauthorized)
</div>
<div class="notice--success">

</div>
<br>
<div class="notice--danger">
<h3> Error 4 </h3>
Error from server (Forbidden) : pods is forbidden: User "aaa" cannot list resource "pods" in API group "" in the namespace "defualt"
</div>
<div class="notice--success">

</div>
<br>
