**Helm Install**

`helm install stable/nginx-ingress --namespace ingress-nginx --name nginx-ingress --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

**Verify**

`kubectl get svc -n ingress-nginx`{{execute}}


Check https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

When Nginx-ingress is ready, the page should show `default backend - 404`. 

Keep refreshing the page several times until you see it, don't be scared by the error messages.
