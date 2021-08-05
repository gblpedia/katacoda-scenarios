**Install PrimeHub CE**

Check the stable versions

`./primehub/install/primehub-install version`{{execute}}

Run the installation of latest stable version

`./primehub/install/primehub-install create primehub --primehub-ce --skip-domain-check --enable-https`{{execute}}

> Due to Katacoda supports HTTPS only, we add `--enable-https`, in real World, HTTP or HTTPS depends on the circumstance.

During the installation, it will prompt 3 questions for the user input.

+ Domain `[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com`{{execute}}
+ keycloak `password`{{execute}}
+ phadmin `password`{{execute}}


**Wait and Watch Progress of Installation**

In Terminal 2, `watch 'kubectl -n hub get pods'`{{execute interrupt T2}}

Please wait and ignore the interim status, `CreateContainerConfigError` until you see **primehub-bootstrap-xxx** pod and **admission-post-install-job-xxx** pod are **Completed** and other pods are **Running** in Ready(1/1).

Then go back to first Terminal and wait until you see messages:

```
[Completed] Install PrimeHub

  PrimeHub:   https://XXXXXXXX.environments.katacoda.com  ( phadmin / password )
  Id Server:  https://XXXXXXXX.environments.katacoda.com/auth/admin/ ( keycloak / password )

[Completed]"
```


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
