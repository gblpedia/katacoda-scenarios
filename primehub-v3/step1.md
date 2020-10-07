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
