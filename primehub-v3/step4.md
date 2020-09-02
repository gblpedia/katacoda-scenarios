

**Add Helm Repo**

`helm repo add infuseai https://charts.infuseai.io`{{execute T1}}

`helm repo update`{{execute}}

**Generate values file**

Since Katacoda supports **https** only, we add `primehub.scheme: https` & `primehub.keycloak.scheme: https` instead; In a real circumstance, http or https depends on your demand. 

*Be noticed* that this part of primehub-values.yaml is *slightly different* with the instruction on our [CE repo](https://github.com/InfuseAI/primehub).

Generate `primehub-values.yaml`.

```
PRIMEHUB_DOMAIN=[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

cat <<EOF > primehub-values.yaml
primehub:
  scheme: https
  domain: ${PRIMEHUB_DOMAIN}
  keycloak:
    scheme: https
ingress:
  hosts:
  -  ${PRIMEHUB_DOMAIN}
EOF
```{{execute}}

**Verify**

`cat primehub-values.yaml`{{execute}}

**Helm Install**

It will install the latest PrimeHub CE.

```
helm upgrade \
primehub infuseai/primehub \
--install \
--create-namespace \
--namespace hub  \
--values primehub-values.yaml \
--timeout 10m \
--devel
```{{execute}}

**Wait and Watch**

In Terminal 2, `watch 'kubectl -n hub get pods'`{{execute interrupt T2}}

Please wait and ignore the interim status, `CreateContainerConfigError` until you see **primehub-bootstrap-xxx** pod and **admission-post-install-job-xxx** pod are **Completed** and other pods are **Running** in Ready(1/1).

Then go back to first Terminal and wait until you see messages:

```
NOTES:
PrimeHub is installed at:

To get the login account, please enter the following commands:
  echo "username: phadmin"
  echo "password: $(kubectl -n hub get secret primehub-bootstrap -o jsonpath='{.data.password}' | base64 --decode)"
```

According the instruction, let's find out the password of account, `phadmin`.
```
echo "username: phadmin"
echo "password: $(kubectl -n hub get secret primehub-bootstrap -o jsonpath='{.data.password}' | base64 --decode)"
```{{execute}}

Keep/copy the password somewhere, we will need it at the final step.

**Label Nodes**

In the first Terminal.

`kubectl label node component=singleuser-server --all`{{execute}}


**Check PrimeHub Console**

PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

You will see the login dialogue of PrimeHub Console.

Hooray! PrimeHub CE has been installed and is running now. The final step, let's launch a JupyterHub on PrimeHub.

Don't forget the password!
