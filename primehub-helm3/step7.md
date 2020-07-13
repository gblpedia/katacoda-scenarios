
**Login**

Login PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com as `phadmin`{{copy}}/`password`{{copy}}.

You will see the User Portal.

**Create Instance Type**

Due to the shortage of the allocatable cpu resource in Katacoda environment, we are required to create a specific instance type for this scenario. In a real circumstance, *it is not required and not recommended*.

While creating an instance type, we will add a **toleration** which can tolerate the tainted controlplane(master) node so that JupyterHub pod is allowed to be scheduled on the controlplane/master node.

1. Click `Admin Dashboard` in Admin section, then click `Instance Types`.

2. Click `+ Add` for an instance type addition.

3. Fill **tiny** in `Name`, **0.5** in `CPU Limit` and **1.0** in `Memory Limit`.

4. Enable `Global`.

5. Click the tab `Tolerations` beside the tab `Basic Info`.

6. Click `+ Add` for a toleration addition.

7. Fill `node-role.kubernetes.io/master`{{copy}} in `Key`.

8. Select `Exists` from `Operator`.

9. Select `NoSchedule` from `Effect` and click `OK`.

10. Click `Confirm`.

**Launch JupyterHub**

Go back to **User Portal** by clicking **PrimeHub logo** at top-left corner.

1. Click `JupyterHub`.

2. Select the instance type, **tiny** and select the default image, **base-notebook (Universal)**.

3. Click `Start Notebook`

It will take a while for spawning. After it, you will see a JupyterHub.

That's all. Feel free to try PrimeHub CE. Please don't be too harsh on this Katacoda environment.

Hope you like it. Why not giving PrimeHub CE a try in your circumstance. Enjoy!
