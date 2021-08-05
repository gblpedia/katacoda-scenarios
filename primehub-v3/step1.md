**Check status of two nodes**

Check if **controlplane(master)** and **node01** are in Ready; wait until two nodes are in Ready.

`watch 'kubectl get nodes'`{{execute interrupt T2}}

In this experimental scenario, we use storageclass, `local-path`; in a real circumstance, you may consider other [provisioners](https://kubernetes.io/docs/concepts/storage/storage-classes/).

**Apply**

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`{{execute T1}}

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/v0.0.17/deploy/local-path-storage.yaml`{{execute T1}}

**Patch**

`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`{{execute}}

**Verify**

`kubectl get sc`{{execute}}

