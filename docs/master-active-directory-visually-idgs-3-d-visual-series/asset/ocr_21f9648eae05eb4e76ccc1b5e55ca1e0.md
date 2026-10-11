# EXAMINING SITE PROPERTIES

You use the Active Directory Sites and Services snap-in to add new sites to the Active Directory. Remember that a site is a physical representation of a grouping of computers usually contained within a geographic area. A site can contain any number of domains.

After you create the site, you can configure the site, the server for the site, and inter-site transports for directory replication. To begin configuring a site, you should access the site's properties pages.

The most configurable aspects of the site's properties pages concern security for the site and group policy. Concerning security, the site

object in the Active Directory works like all other objects. You can set security so you can manage who can access the site object and what they can do with it. By default, only Enterprise Admins have full control over the site object. Additionally, you use the Group Policy tab to apply a desired group policy to the site. Group policies can be applied at the site, domain, or OU level.

![](bbox=[0.04, 0.5, 0.96, 0.82])

+   1. To access the Active Directory Sites and Services snap-in, choose Start->Programs->Administrative Tools->Active Directory Sites and Services.
+   2. Expand Sites, and then select the site you want to administer in the details pane.
+   3. Choose Action->Properties.