## Set up StorageClass

In this scenario, we use `local-path`; in a real circumstance, you may consider other [provisioners](https://kubernetes.io/docs/concepts/storage/storage-classes/).

### Steps

1. Apply `kubectl apply -f https://raw.githubusercontent.com/rancher/local-path-provisioner/master/deploy/local-path-storage.yaml`{{execute}}
2. Patch `kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`{{execute}}
3. Verify the storageclass `kubectl get sc`{{execute}}
