## Install Ingress-Nginx

### Steps

1. Install `helm install stable/nginx-ingress --namespace ingress-nginx --name nginx-ingress --set controller.hostNetwork=true --set rbac.create=true`{{execute}}
2. Verify `kubectl get svc -n ingress-nginx`{{execute}}
