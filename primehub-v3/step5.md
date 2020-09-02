
**Login**

Login PrimeHub Console: https://[[HOST2_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com as `phadmin`{{copy}}/`<the_password>`.

The landing page is called **User Portal**.

**Create Instance Type**

Due to the shortage of the allocatable cpu resource in Katacoda environment, we are required to create a specific **instance type** for this scenario. In a real circumstance, *it is not required and not recommended*.

While creating an instance type, we will add a **toleration** which can *tolerate the tainted controlplane(master) node* so that JupyterHub pod is allowed to be scheduled on the controlplane/master node.

1. Hover the cursor over the icon at **top-right** corner, from a dropdown menu, click `Admin Portal`, then select `Instance Types` from the side menu.

2. Click `+ Add` for an instance type creation.

3. Fill **tiny** in `Name`, **0.5** in `CPU Limit` and **1.0** in `Memory Limit`.

4. Enable `Global`.

5. Click the tab `Tolerations` beside the tab `Basic Info`.

6. Click `+ Add` for a toleration creation.

7. Fill `**node-role.kubernetes.io/master**`{{copy}} in `Key`.

8. Select **Exists** from `Operator`.

9. Select **NoSchedule** from `Effect` and click `OK`.

10. Click `Confirm`.

**Launch JupyterHub**

Go back to **User Portal** by clicking **PrimeHub logo** at top-left corner.

1. Select `JupyterHub` from the side menu.

2. Select the instance type, **tiny** and select the default image, **base-notebook (Universal)**.

3. Click `Start Notebook` and wait until the spawning is finished and see two `Stop My Sever` and `My Server` buttons on the page.

4. The JupyterHub is popped up as a new tab, usually, *it is blocked initially by the browser*.

5. Click the **pop-up-blocked** icon at the rightmost side of url bar to allow the pop-ups.

6. Click `My Server`, the JupyterHub will be opened in a new tab successfully.

That's all. Feel free to try PrimeHub CE. 

Please be noticed that Katacoda environment could be time out soon anytime. Don't be too harsh on this Katacoda environment.

Hope you like it. Why not giving PrimeHub CE a try in your circumstance to start a real project. Enjoy!
