## Install Metacontroller

### Steps

1. Create namespace`kubectl create namespace metacontroller`{{execute}}
2. Apply `kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller-rbac.yaml`{{execute}}
3. Apply `kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller.yaml`{{execute}}
4. Verify `kubectl get crd | grep metacontroller`{{execute}}
