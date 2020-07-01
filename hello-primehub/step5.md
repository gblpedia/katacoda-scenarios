**Add Helm repo**

`helm repo add codecentric https://codecentric.github.io/helm-charts`{{execute}}

**Update repo**

`helm repo update`{{execute}}

**Prepare Domain and values file**

Current HOST2 Domain: `[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com`

**Generate values file**

```
KEYCLOAK_DOMAIN=[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com
KEYCLOAK_PASSWORD=password
KEYCLOAK_DB_PASSWORD=password
STORAGE_CLASS=local-path

cat <<EOF > keycloak-values.yaml
keycloak:
  ingress:
    enabled: true
    annotations:      
      kubernetes.io/ingress.class: nginx
      kubernetes.io/tls-acme: "true"    
      ingress.kubernetes.io/affinity: cookie
    hosts:
    - ${KEYCLOAK_DOMAIN}
    path: /auth
  username: keycloak
  password: ${KEYCLOAK_PASSWORD}
  persistence:    
    deployPostgres: true
    dbVendor: postgres
    dbPassword: ${KEYCLOAK_DB_PASSWORD}
postgresql:
  persistence:
    enabled: true
    storageClass: ${STORAGE_CLASS}
  postgresPassword: ${KEYCLOAK_DB_PASSWORD}
EOF
```{{execute}}


**Verify**

`cat keycloak-values.yaml`{{execute}}

**Helm install**

```
helm upgrade \
  --install \
  --reset-values \
  --namespace default  \
  --values keycloak-values.yaml \
  --version 7.2.1 \
  keycloak codecentric/keycloak
```{{execute}}

**Rollout Keycloak**

`kubectl -n default rollout status sts/keycloak`{{execute}}

**Wait and Watch**

In Terminal 2, `watch 'kubectl get pods'`{{execute interrupt T2}}


It will take a while until Keycloak pods are running and in Ready. When Keycloak is running, check Keycloak console https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/auth

You will see the web console. It's not necessary in the scenario, however, you are able to login **Administration Console** with `keycloak`{{copy}}/`password`{{copy}}.

So far, we have set up the prerequisites for PrimeHub CE. Next step, PrimeHub CE installation.
