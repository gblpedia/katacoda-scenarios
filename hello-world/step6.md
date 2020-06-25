## Steps

1. Add Helm repo `helm repo add codecentric https://codecentric.github.io/helm-charts`{{execute}}
2. Update repo `helm repo update`{{execute}}

### Prepare Domain and values file

1. Add Helm Repo

`helm repo add infuseai https://charts.infuseai.io`{{execute}}
`helm repo update`{{execute}} 


2. Generate values file.

  HOST2 Domain: `[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com`{{copy}}

  ```
  PRIMEHUB_DOMAIN=[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com
  PRIMEHUB_PASSWORD=password
  KEYCLOAK_DOMAIN=[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com
  KEYCLOAK_PASSWORD=password
  STORAGE_CLASS=local-path
  GRAPHQL_SECRET_KEY=$(openssl rand -hex 32)
  HUB_AUTH_STATE_CRYPTO_KEY=$(openssl rand -hex 32)
  HUB_PROXY_SECRET_TOKEN=$(openssl rand -hex 32)

  cat <<EOF > primehub-values.yaml
  primehub:
    scheme: http
    domain: ${PRIMEHUB_DOMAIN}
    keycloak:
      scheme: http
      domain: ${KEYCLOAK_DOMAIN}
      username: keycloak
      password: ${KEYCLOAK_PASSWORD}
  bootstrap:
    usernmae: phadmin  
    password: ${PRIMEHUB_PASSWORD}
  graphql:
    sharedGraphqlSecret: ${GRAPHQL_SECRET_KEY}
  groupvolume:
    storageClass: ${STORAGE_CLASS}
  ingress:
    annotations:
      # If `primehub.scheme` is `http`, the following annotations are required
      kubernetes.io/ingress.allow-http: "true"
      nginx.ingress.kubernetes.io/ssl-redirect: "false"
    hosts:
    -  ${PRIMEHUB_DOMAIN}
  jupyterhub:
    auth:
      state:
        cryptoKey: ${GRAPHQL_SECRET_KEY}
    hub:
      db:
        pvc:
          storageClassName: ${STORAGE_CLASS}
    proxy:
      secretToken: ${HUB_PROXY_SECRET_TOKEN}
    singleuser:
      storage:
        dynamic:
          storageClass: ${STORAGE_CLASS}
  EOF
  ```

3. Helm Install

  ```
  helm upgrade \
  --install \
  --reset-values \
  --namespace hub  \
  --values primehub-values.yaml \
  --timeout 3000\
  primehub infuseai/primehub
  ```