```
curl -O https://storage.googleapis.com/primehub-release/bin/primehub-install
```{{execute}}

```
chmod +x primehub-install
```{{execute}}

```
mkdir -p /root/.helm/plugins
```{{execute}}

```
./primehub-install create singlenode --k8s-version 1.17
```{{execute}}

>[Require Action] Please relogin this session and run create singlenode again

```
./primehub-install create singlenode --k8s-version 1.17
```{{execute}}

```
curl http://1.2.3.4.nip.io
```{{execute}}

>default backend - 404

```
./primehub-install create primehub --primehub-version v3.1.0 --primehub-ce --helm-timeout 6000 --skip-domain-check
```{{execute}}

```
watch kubectl get pod -n hub
```{{execute T2}}
