**Helm Install**

`helm install stable/nginx-ingress --namespace ingress-nginx --name nginx-ingress --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

**Verify**

`kubectl get svc -n ingress-nginx`{{execute}}



**Wait and Watch**

In Terminal 2, `watch 'kubectl -n ingress-nginx get pods'`{{execute T2}}

When ingress-nginx are running, check https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com and the page should show `default backend - 404`. Keep refreshing the page several times until you see it, don't be scared by the error messages.
