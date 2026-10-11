![](bbox=[0.08, 0.08, 0.55, 0.22])

Figure 1. Upon startup, the Red Hat Network Alert Notification Tool displays a blue check mark that indicates it is not aware of any new updates.

![](bbox=[0.08, 0.29, 0.55, 0.44])

Figure 2. The Red Hat Network Alert Notification Tool icon's green color means updates are currently being queried.

![](bbox=[0.08, 0.51, 0.55, 0.64])

Figure 3. The round red icon in the lower right corner of the panel indicates that updates are available.

![](bbox=[0.08, 0.71, 0.55, 0.8])

Figure 4. The blue check mark indicates that no updates are available.

If you move your mouse over the icon, a tooltip will display how many updates are available and how many have been ignored during the last update session. If the tooltip in Figure 3 alarms you (nearly 100 updates available), remember that there could be thousands of packages installed on an FC system. Furthermore, the more time that has passed since the time when the ISOs you used to install were made available and the last update session, the more updates will be available. If you install FC (or any distro, for that matter) with old files, there will likely be a lot of updates to install the first time you do an update, but significantly fewer each successive update.