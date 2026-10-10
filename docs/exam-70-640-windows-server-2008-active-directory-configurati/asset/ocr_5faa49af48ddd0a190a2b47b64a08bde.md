One new feature of Group Policy management in Windows Server 2008 is the ability to search for a particular GPO setting under the Administrative Templates folder based on elements such as keywords or the minimum operating system level. This is a convenience to administrators, because literally hundreds of settings are available under any number of nodes and subnodes within the Administrative Templates folder. Figure 7-9 shows the Filter Options screen in the Group Policy Management Editor. In addition, each individual Administrative Templates setting now includes a Comment tab that allows you to enter free-form text to describe the entry. You can search against the text in these comments fields using the Filter Options window. Finally, you will also see the All Settings node below the Administrative Templates node for User Configuration and Computer Configuration, which allows you to browse and sort all available policies alphabetically or by state (i.e., Enabled, Disabled, or Not Configured).

![](bbox=[0.04, 0.25, 0.6, 0.6])

# Understanding Group Policy Processing

> As discussed earlier, you can have local policies, site policies, domain policies, and OU policies within your domain structure. To learn how to best implement Group Policies to serve the organization, you need to understand the order in which the policies are applied.

Nonlocal GPOs are created in Active Directory and linked to container objects. Nonlocal GPOs can be linked to Active Directory sites, domains, or OUs. They cannot be linked to built-in containers, such as the default Users, Builtin, or Computers containers. These containers can receive policies only through domain or site-linked policies that flow down to all objects within them. Policies affect the containers to which they are linked in the following ways:

+   * Site-linked policies affect all domains within a site.
+   * Domain-linked policies affect all users and computers within a domain and within any containers within a domain. This includes objects in built-in containers, as well as objects within OUs and sub-OUs within the domain structure.
+   * OU-linked policies affect all objects within the OU and any other OU structures nested within them.

To begin, policies are processed in the following order, typically referred to as LSDOU:

+   1. Local policies
+   2. Site policies