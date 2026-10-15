# Route Summarization

Route summarization performs a similar function to that which static route supernetting provides—it combines multiple subnet routes into one entry. Route summarization is a step more versatile because the routing protocol is still aware of specific network outages through routing advertisements.

Figure 10.3 shows that router A has used route summarization for 10.0.0.0/8 through interface A1. (Assuming equal weights, the network can be summarized through A2 as well, but it would not be used until a failure occurs because it is an additional hop.) Router B can also summarize the route.

![](bbox=[0.22, 0.36, 0.82, 0.61])

Figure 10.3 Network management system.

# Avoiding Multiple Protocol Support

Supporting multiple dynamic routing protocols on the same network should be avoided. Multiple protocol support is usually the result of corporate acquisitions or failed upgrades from an older metric-based protocol to a link state protocol such as open shortest path first (OSPF).

Supporting multiple protocols requires not only an understanding of the protocols involved, but also how they interoperate on routers that support both protocols, which will typically be vendor specific. It must be understood which protocol takes priority on the routers that support both protocols, which entries are further propagated by the "other" protocol, and how to troubleshoot the interaction of the two protocols.

# Special Case Routing Functions

As covered in Chapter 7, "Kernel Support Tools", adding additional functions to Internet gateways can add additional value to a Linux router and, indeed, often gives Linux an edge over traditional routers as Internet access gateways.