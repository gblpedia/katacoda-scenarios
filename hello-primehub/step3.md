**Helm Install**

`helm install stable/nginx-ingress --namespace ingress-nginx --name nginx-ingress --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

**Verify**

`kubectl get svc -n ingress-nginx`{{execute}}

When Ingress-Nginx is ready, it should show `default backend - 404`. Keep refreshing the page until you see it.

Check https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com.