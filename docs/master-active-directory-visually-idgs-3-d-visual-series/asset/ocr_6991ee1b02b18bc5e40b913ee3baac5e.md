# **Why use sites?**

Because sites are typically used to segment physical locations of the WAN, sites help control how users access services and how bandwidth is conserved. A site can keep user access within its own subnet, unless a particular service becomes unavailable.

First, a subnet helps user authentication. Because the Active Directory uses multimaster replication, any Windows 2000 domain controller on the network can authenticate any user. This can present a problem with WAN bandwidth. The site keeps user authentication within the subnet so that the domain controllers in that subnet can first authenticate the user before the request is sent to other sites. This keeps the traffic localized on the subnet.

Next, you can use site links to control how the Active Directory replicates information among domain controllers at different sites. This feature helps you control bandwidth usage and fault tolerance among the sites. Along with the site links, you can also specify a bridgehead server. A bridgehead server is a server that is specified to send and receive intersite replication data. By default, all domain controllers replicate information to each other. The bridgehead server takes care of this process because it is dedicated to intersite replication.

Aside from authentication and replication, the sites also control user service requests to domain controllers. As with authentication, the service requests are directed to the domain controllers within the site instead of domain controllers in other sites.

![](bbox=[0.02, 0.16, 0.44, 0.48])

![](bbox=[0.02, 0.58, 0.44, 0.95])