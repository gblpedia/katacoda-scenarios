**Create namespace**

`kubectl create namespace metacontroller`{{execute}}

**Create service account and role-binding**

`kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller-rbac.yaml`{{execute}}

**Create CRDs and StatefulSet**

`kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller.yaml`{{execute}}

**Verify**

`kubectl get crd | grep metacontroller`{{execute}}

You should see something similar.

```
compositecontrollers.metacontroller.k8s.io     2020-01-06T01:24:57Z
controllerrevisions.metacontroller.k8s.io      2020-01-06T01:24:57Z
decoratorcontrollers.metacontroller.k8s.io     2020-01-06T01:24:57Z
```
