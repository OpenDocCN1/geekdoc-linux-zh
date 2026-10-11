# How should sites be linked together?

Remember that the purpose of site links is to connect Active Directory sites so that directory replication can occur. This process ensures that all directory information for the network is current, regardless of the physical location. Sites should be linked so that replication can occur between all sites. If you have multiple sites, you can also use site link bridges, which are discussed in the next section.

# What transports are available?

A transport is the protocol used to transport replication data between sites. The Active Directory supports both Internet Protocol (IP) and Simple Mail Transport Protocol (SMTP) for inter-site replication. Under most circumstances, you will use IP because the Active Directory is built on your TCP/IP network.

![](bbox=[0.02, 0.46, 0.95, 0.82])

+   3.  Type a name for the new site link.

+   4.  Click the sites you want to include in the link.

+   5.  Click Add.
+   *   You must specify at least two sites to create the site link.
+   6.  Click OK when you are done.

The new site link now appears in the list.