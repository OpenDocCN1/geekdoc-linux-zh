# CONFIGURING SITE SETTINGS
CONTINUED

You can also use the Action menu to move a domain controller to a different site. This feature allows a domain controller to function within a particular site so that it can serve as the bridgehead server for that site. You do have to keep in mind, however, the physical design of your network and how the move will affect replication traffic.

You can designate the licensing computer for a site, which does not have to be a domain controller or the bridgehead server. For the best performance, the site’s licensing computer should be within the site. The Active Directory automatically designates a licensing computer for the site, but you can easily change this.

![](bbox=[0.03, 0.5, 0.48, 0.8])

# MOVING A DOMAIN
CONTROLLER TO A DIFFERENT SITE

+   1. To move a domain controller, select the domain controller and choose Action->Move.

![](bbox=[0.5, 0.5, 0.98, 0.8])

+   2. The Move Server window appears.
+      2. Select the site to which you want to move the domain controller.
+      3. Click OK.