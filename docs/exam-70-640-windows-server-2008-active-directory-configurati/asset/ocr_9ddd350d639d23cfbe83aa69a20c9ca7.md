**4.** Select the Enable Universal Group Membership Caching checkbox, as shown in Figure 4-1.

![](bbox=[0.31, 0.12, 0.6, 0.38])

+   **Figure 4-1**
+   
+   Enabling universal group membership caching

**5.** In the Refresh Cache From field, select a site that you wish this site to receive updates from or leave it at <Default> to refresh from the nearest site that contains a global catalog server. Click **OK**.

**PAUSE.** CLOSE the Active Directory Sites and Services MMC snap-in.

You have just enabled universal group membership caching for a single site within Active Directory. This setting must be enabled for each site that you wish to configure for universal group membership caching.

# Configuring Additional Global Catalog Servers

> By default, the first domain controller in a forest is a global catalog server. Therefore, your initial site will already contain a global catalog server.

The following guidelines will help you decide when you should add a global catalog server.

- Each site should contain a global catalog server to facilitate user logons. If a remote site is located across an unreliable or slow WAN link, a locally deployed global catalog server will allow logons and Active Directory searches to take place regardless of the state of the WAN link. If this is not possible, consider enabling universal group membership caching.

- When placing a global catalog at a remote site, consider the amount of bandwidth necessary to replicate global catalog information. Responding to logon requests from other sites increases the demands on bandwidth for the remote site.

- The domain controller that hosts the global catalog must have enough space on the hard drive to house the global catalog. As a rule of thumb, you should estimate 50 percent of the size of the ntds.dit file of every other domain in the forest when sizing hardware for a global catalog server.

- A site that contains an application using port 3268 for global catalog queries should contain a global catalog server. Port 3268 is used for Active Directory object searches.

# CONFIGURE AN ADDITIONAL GLOBAL CATALOG SERVER

**GET READY.** Before you begin these steps, you must be logged on as a member of the Domain Admins group.

+   **1.** On the domain controller where you want the new global catalog, open **Active Directory Sites and Services** from the Administrative Tools folder.

+   **CERTIFICATION READY?**
+   
+   Configure the global catalog
+   
+   2, 5