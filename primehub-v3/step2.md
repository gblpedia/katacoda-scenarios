**Download PrimeHub repository**

`git clone https://github.com/InfuseAI/primehub`{{execute T1}}

**Verify primehub-install tool**

`./primehub/install/primehub-install`{{execute}}

**Install tools of dependency**

`./primehub/install/primehub-install required-bin`{{execute}}

Add tools in $PATH 

`echo "export PATH=$HOME/bin:$PATH" >> ~/.bashrc`{{execute}}

`source ~/.bashrc`{{execute}}

**Helm Install**

`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`{{execute T1}}

`helm repo update`{{execute}}

**Install ingress-nginx**

`helm install nginx-ingress ingress-nginx/ingress-nginx --create-namespace --namespace ingress-nginx --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

**Wait and Watch**

In Terminal 2, `watch 'kubectl -n ingress-nginx get pods'`{{execute interrupt T2}}

**Verify**

`kubectl get svc -n ingress-nginx`{{execute T1}}

When ingress-nginx pods are running, check https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com, the page should show `404 Not Found`. Keep refreshing the page several times until you see it, don't be scared by the messages.
