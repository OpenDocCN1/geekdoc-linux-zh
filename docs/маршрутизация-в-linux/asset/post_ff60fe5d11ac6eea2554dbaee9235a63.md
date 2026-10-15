
# Route Summarization

Route summarization performs a similar function to that which static route supernetting provides—it combines multiple subnet routes into one entry. Route summarization is a step more versatile because the routing protocol is still aware of specific network outages through routing advertisements.

Figure 10.3 shows that router A has used route summarization for 10.0.0.0/8 through interface A1. (Assuming equal weights, the network can be summarized through A2 as well, but it would not be used until a failure occurs because it is an additional hop.) Router B can also summarize the route.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_232_0.png)

Figure 10.3 Network management system.

## Avoiding Multiple Protocol Support

Supporting multiple dynamic routing protocols on the same network should be avoided. Multiple protocol support is usually the result of corporate acquisitions or failed upgrades from an older metric-based protocol to a link state protocol such as open shortest path first (OSPF).

Supporting multiple protocols requires not only an understanding of the protocols involved, but also how they interoperate on routers that support both protocols, which will typically be vendor specific. It must be understood which protocol takes priority on the routers that support both protocols, which entries are further propagated by the "other" protocol, and how to troubleshoot the interaction of the two protocols.

## Special Case Routing Functions

As covered in Chapter 7, "Kernel Support Tools", adding additional functions to Internet gateways can add additional value to a Linux router and, indeed, often gives Linux an edge over traditional routers as Internet access gateways.

## IP Version 6 Support

There are additional considerations, or special cases, that do arise when planning and deploying networks that you should be aware of:

Chapter 4, “IPv4 and IPv6 Addressing,” covers the innards of addressing networks. Organizations that choose to support IPv6 will need phase-in methodologies to support both versions of the Internet protocol.

RFC 1933, “Transition Mechanisms for IPv6 Hosts and Routers,” defines two methods for transitioning to IPv6: dual IP layer and IPv6 over IPv4 tunneling.

Dual IP layer is very similar to dual stacks to support multiple protocols. For example, many workstations and PCs supported both IP and Novell’s IPX during Novell’s popularity in the 1990s.

Dual stacks is a host-based solution, that is, the host can communicate with both IP version 6 and version 4 nodes, which provides a very broad base of interoperability capability.

Many organizations wish to deploy specific IPv6 networks as opposed to a dual stack approach. Therefore, RFC 1933 also defined tunneling of IPv6 over IPv4 networks. Tunneling of IP version 6 over version 4 is similar to other tunneling technology. An example of the tunneling is shown in Figure 10.4.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_233_0.png)

Figure 10.4 IP version 6 over IP version 4.

Node A and B both have IP version 6 and IP version 4 interfaces. For traffic flowing from A to B, A encapsulates the IPv6 packet received on interface A1 into a version 4 packet and routes it out interface A2. Router B then accepts the IPv4 packet on interface B1, strips the IPv4 header from the packet, and routes it out interface B2 as an IP version 6 packet.

## Multihoming

Multihoming, for most system administrators, describes connecting a host or network to multiple networks. A router, by definition, is multihomed. In this chapter, multihoming refers to actually connecting to the Internet via at least 2 upstream providers.

## Administrative Considerations

Internet service providers’ policies on multihoming vary greatly—from very little concern on how you implement multihoming (these ISPs will tend to use filtering very strongly on the edge of the network to ensure your network is not affecting the core network) to a very detailed list of dos and don’ts. This chapter covers the technical aspects of multihoming, but do consult with the ISPs of choice on their policies and recommendations.

## Simple Multihoming

The simplest form of multihoming is shown in Figure 10.5.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_234_0.png)

Figure 10.5 Simple multihoming.

In Figure 10.5, the enterprise is connected to ISP A and ISP B via T1 connections. On the router, penguin, two default routes with equal weights are pointed to each ISP A and B creating a load balance between the two ISPs. The major advantage to this solution is simplicity and a total bandwidth for Internet connectivity of 3Mbps. The major disadvantage of this solution is that 50% of traffic destined to ISP A for outsourced services such as W.W.W, DNS, or even email, will travel through ISP B. Static routes for the ISP’s networks can be entered to create a hybrid Simple Multihoming network; however, the ISPs also have many customers where traffic should go through a particular link (assuming the link is in service). Therefore, a more efficient method is often needed.

## BGP Multihoming

By using BGP with both providers, the edge router(s) can determine the best path to both ISP providers’ customers. This can be implemented in several ways. Should the provider only advertise customer networks with customers, then a direct BGP implementation is straightforward. Should the provider advertise all routes, a filtering mechanism is required at the edge of the provider’s network or on the customer premise.
