# **Why would I want to move a domain controller?**

You can use the Active Directory Sites and Services tool to move domain controllers between sites. Keep in mind that the configuration changes you make within this tool should accurately reflect the physical layout of your network. When you move a domain controller to a site, the domain controller then functions within that site for replication purposes.

# **What is a licensing computer?**

Each Active Directory site must have a licensing computer, which does not have to be a domain controller. When a site is configured, a licensing computer is selected by default, but you can change this. The role of the licensing computer is to track licenses for that particular site.

![](bbox=[0.02, 0.48, 0.48, 0.85])

+   1. Select the site name in the console.

+   2. Double-click the Licensing Site Settings.

![](bbox=[0.5, 0.48, 0.98, 0.82])

+   3. Type a description if desired.

+   4. If you want a different computer to serve as the licensing computer, click Change and select the new computer from the list that appears.