**Check CPU architecture**

`dpkg --print-architecture`{{execute}}

**Download the amd64 version**

`curl -O https://get.helm.sh/helm-v2.16.1-linux-amd64.tar.gz`{{execute}}

**Extract tar file**

`tar -zxvf helm-v2.16.1-linux-amd64.tar.gz`{{execute}}

**Move**

`mv linux-amd64/helm /usr/local/bin/helm`{{execute}}

**Verify**

`helm version --client`{{execute}}

### Initialize Helm and Tiller

**Check if two nodes are ready**

Check if controlplane(master) and node01 are in Ready; wait until two nodes are in Ready.

`kubectl get nodes`{{execute}}

**Helm init**

`helm init --wait`{{execute}}

**Wait and Watch**

It may take a while until Tiller is ready.

In Terminal 2, `watch 'kubectl get pods -A | grep tiller'`{{execute T2}}

**Tiller role binding**

```
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
```{{execute}}

**Verify**

`helm version`{{execute}}

Once Tiller is ready, please go to next step.
