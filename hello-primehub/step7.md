
**Login**

PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com

Login PrimeHub Console as `phadmin`{{copy}}/`password`{{copy}}.

**Create Instance Type**

While creating an instance type, we will add a toleration which can tolerate the tainted controlplane/master node so that JupyterHub pod is allowed to be scheduled on the controlplane/master node due to the shortage of the allocatable cpu resource in Katacoda environment. In a real circumstance, *it is not recommended*.

1. Click `Admin Dashboard`, then select `Instance Type`.

2. Click `+ Add` for an instance type creation.

3. Fill **tiny** in `Name`, **0.5** in `CPU Limit` and **1.0** in `Memory Limit`.

4. Enable `Global`.

5. Click `Tolerations` tab beside `Basic Info`.

6. Click `+ Add` for a toleration addition.

7. Fill `node-role.kubernetes.io/master`{{copy}} in `Key`.

8. Select `Exists` from `Operator`.

9. Select `NoSchedule` from `Effect` and click `OK`.

10. Click `Confirm`.

**Launch JupyterHub**

Go back to **User Portal by clicking **PrimeHub logo** at top-left corner.

1. Click `JupyterHub`.

2. Select the instance type, **tiny** and select the default image, **base-notebook**.

3. Click `Start Notebook`

After spawning, you should see a **JupyterHub**.
