**Check CPU architecture**

`dpkg --print-architecture`{{execute}}

**Download the amd64 version**

`curl -O https://get.helm.sh/helm-v3.3.4-linux-amd64.tar.gz`{{execute}}

**Extract and move tar file**

`tar -zxvf helm-v3.3.4-linux-amd64.tar.gz; mv linux-amd64/helm /usr/local/bin/helm`{{execute}}

**Verify**

`helm version`{{execute}}

**Check if two nodes are ready**

Check if **controlplane(master)** and **node01** are in Ready; wait until two nodes are in Ready.

`watch 'kubectl get nodes'`{{execute interrupt T2}}


`git clone https://github.com/InfuseAI/primehub`{{execute}}

`./primehub/install/primehub-install`{{execute}}

`./primehub/install/primehub-install required-bin`{{execute}}


`echo "export PATH=$HOME/bin:$PATH" >> ~/.bashrc`{{execute}}
`source ~/.bashrc`{{execute}}

`./primehub/install/primehub-install create primehub --primehub-ce --skip-domain-check --enable-https`{{execute}}

phadmin `password`{{execute}}
keycloak `password`{{execute}}o

`helm install nginx-ingress ingress-nginx/ingress-nginx --create-namespace --namespace ingress-nginx --set controller.hostNetwork=true --set rbac.create=true`{{execute}}

