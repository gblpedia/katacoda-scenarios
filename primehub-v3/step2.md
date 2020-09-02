
In this experimental scenario, we use storageclass, `local-path`; in a real circumstance, you may consider other [provisioners](https://kubernetes.io/docs/concepts/storage/storage-classes/).

**Apply**

`kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`{{execute T1}}

**Patch**

`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`{{execute}}

**Verify**

`kubectl get sc`{{execute}}
