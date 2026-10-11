# Forest

A forest is one or more trees that do not share a contiguous namespace. The trees in the forest do share a common schema, configuration, and global catalog, but the trees do not share a contiguous name space. All trees in the forest trust each other through Kerberos transitive trusts. In actuality, the forest does not have a distinct name, but the trees are viewed as a hierarchy of trust relationships. The tree at the top of the hierarchy normally refers to the tree. For example, corp.com, production.corp.com, and mgmt.corp.com form a forest with corp.com serving as the forest root.

# Site

A site is not actually considered part of the Active Directory hierarchy, but it is configured in the Active Directory for replication purposes. A site is defined as a geographical location in a network containing Active Directory servers with a well-connected TCP/IP subnet. *Well-connected* means that the network connection is highly reliable and fast. Administrators use the Active Directory to configure replication between sites. Users do not have to be aware of site configuration. As far as the Active Directory is concerned, users only see domains.

# How the structure appears to administrators and users

As an administrator, you view the structure of the Active Directory through the administrative tools that you can explore in detail later in Chapters 14 through 21. From the tools, you can see the structure through the domains, OUs, and objects that are a part of the Active Directory.

![](bbox=[0.48, 0.32, 0.98, 0.57])

*Administrators can view the tree structure of the Active Directory.*

Users browse the Active Directory by accessing it in My Network Places. Users see a folder view for the domain and organizational units within the domain. The objects then reside in their respective OUs. Primarily, users find resources by performing LDAP searches instead of browsing (see Chapter 13).