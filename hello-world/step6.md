### Steps

#### Add Helm Repo

`helm repo add infuseai https://charts.infuseai.io`{{execute}}

`helm repo update`{{execute}}

#### Generate values file

Since Katacoda supports `https`, we use `primehub.scheme: https` & `primehub.keycloak.scheme: https` instead.

Run the command below

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
  scheme: https
  domain: ${PRIMEHUB_DOMAIN}
  keycloak:
    scheme: https
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
```{{execute}}

#### Verify

`cat primehub-values.yaml`{{execute}}

#### Helm Install

```
helm upgrade \
--install \
--reset-values \
--namespace hub  \
--values primehub-values.yaml \
--timeout 3000 \
primehub infuseai/primehub
```{{execute}}

**Watch the installation**

Open a new terminal, Terminal 2, and run the command to watch pods.
`watch 'kubectl -n hub get pods'`{{copy}}

Please ignores status, `CreateContainerConfigError` until you see `Completed` or `Running`.


#### Label Nodes

`kubectl label node component=singleuser-server --all`{{execute}}

###

#### Check PrimeHub Console

PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

Once you see the login dialogue of PrimeHub Console, please go to next step.
