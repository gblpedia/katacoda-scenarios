

**Add InfuseAI Helm Repo**

`helm repo add infuseai https://charts.infuseai.io`{{execute T1}}

`helm repo update`{{execute}}

**Generate values file**

Since Katacoda supports **https** only, we add `primehub.scheme: https` & `primehub.keycloak.scheme: https` instead; In a real circumstance, http or https depends on your demand. 

*Notice* that this part of primehub-values.yaml is *slightly different* than the instructions on our [CE repo](https://github.com/InfuseAI/primehub).

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

Keep/memorize the password somewhere, we will need it at the final step.

**Label Nodes**

In the first Terminal.

`kubectl label node component=singleuser-server --all`{{execute}}


**Patch Instance Type**

Due to the shortage of the cpu/memory resources in Katacoda environment, we are required to patch one of default instance types in this scenario.  In a real circumstance, this step may not be required.

Run the patch

```
kubectl -n hub patch instancetype cpu-1 --type merge -p '{"spec":{"limits.cpu": 0.5, "requests.cpu": 0.5, "limits.memory": "1G", "requests.memory": "1G", "tolerations":[{"effect":"NoSchedule", "key": "node-role.kubernetes.io/master", "operator":"Exists"}]}}'
```{{execute}}


**Visit PrimeHub Console**

PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

You should see the login page of PrimeHub Console.

Hooray! PrimeHub CE has been installed and is running now. The final step, let's launch a Jupyter Notebook on PrimeHub.

Don't forget the password!
