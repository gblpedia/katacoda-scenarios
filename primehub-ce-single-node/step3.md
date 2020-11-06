**Helm Install**

`helm repo add stable https://kubernetes-charts.storage.googleapis.com`{{execute T1}}

`helm repo update`{{execute}}

`helm install nginx-ingress stable/nginx-ingress --create-namespace --namespace ingress-nginx --version=1.31.0 --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

**Wait and Watch**

In Terminal 2, `watch 'kubectl -n ingress-nginx get pods'`{{execute interrupt T2}}

**Verify**

`kubectl get svc -n ingress-nginx`{{execute T1}}

When ingress-nginx pods are running, check https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com, the page should show `default backend - 404`. Keep refreshing the page several times until you see it, don't be scared by the messages.
