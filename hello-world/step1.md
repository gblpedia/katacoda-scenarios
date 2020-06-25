Install Helm v2.16.1

## Task

This is an _example_ of creating a scenario and running a **command**

1. Find CPU architecture `dpkg --print-architecture`{{execute}}
2. Download the adm64 version`curl -O https://get.helm.sh/helm-v2.16.1-linux-amd64.tar.gz`{{execute}}
3. `tar -zxvf helm-v2.16.1-linux-amd64.tar.gz`{{execute}}
4. `mv linux-amd64/helm /usr/local/bin/helm`{{execute}}
5. `helm init --service-account tiller --wait`{{execute}}
6. 
    ```bash
    kubectl apply -f - << EOF
    apiVersion: v1
    kind: ServiceAccount
    metadata:
    name: tiller
    namespace: kube-system
    ---
    apiVersion: rbac.authorization.k8s.io/v1
    kind: ClusterRoleBinding
    metadata:
    name: tiller
    roleRef:
    apiGroup: rbac.authorization.k8s.io
    kind: ClusterRole
    name: cluster-admin
    subjects:
    - kind: ServiceAccount
        name: tiller
        namespace: kube-system
    EOF
    ```
