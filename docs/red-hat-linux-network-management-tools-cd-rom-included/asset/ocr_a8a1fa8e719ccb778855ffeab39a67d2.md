![](bbox=[0.2, 0.08, 0.75, 0.5])

![](bbox=[0.2, 0.08, 0.75, 0.5])

# Figure 3.15 Subnet calculation window.

from the lower-level protocol details and makes few assumptions about the performance and reliability of the network. Data delivery is accomplished without any special coordination among other IP entities and, for the most part, operates quite well. However, conditions might exist beyond IP’s control that make delivery difficult or impossible. For example, a remote host could be temporarily removed from the network or a router could become overloaded when a network-intensive application is started. IP needs a way to detect these types of problems.

The Internet Control Message Protocol (ICMP) provides a general error message facility for the IP protocol and related services. ICMP provides a way for IP entities that encounter errors to report them to the source that caused the problem. It is the responsibility of the source entity to correct the error. This might include, for example, reporting the error to a higher-level application. Table 3.6 lists some of the ICMP message types.