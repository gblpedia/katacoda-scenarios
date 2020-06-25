## Steps

1. Add Helm repo `helm repo add codecentric https://codecentric.github.io/helm-charts`{{execute}}
2. Update repo `helm repo update`{{execute}}

### Prepare Domain and values file

Render HOST2 Domain: [[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

port 8500: https://[[HOST_SUBDOMAIN]]-8500-[[KATACODA_HOST]].environments.katacoda.com/

1. Generate values file.

  ```
  KEYCLOAK_DOMAIN=[[HOST_SUBDOMAIN]]-[[KATACODA_HOST2]].environments.katacoda.com
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

2. Helm install

  ```
  helm upgrade \
    --install \
    --reset-values \
    --namespace default  \
    --values keycloak-values.yaml \
    --version 7.2.1 \
    keycloak codecentric/keycloak

  kubectl -n default rollout status sts/keycloak
  ```

3. Rollout Keycloak 
`kubectl -n default rollout status sts/keycloak`{{execute}}