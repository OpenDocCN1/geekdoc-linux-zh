# 294 Chapter 16 IP Routing

Connection to the other networks of the Internet

![](bbox=[0.245, 0.098, 0.935, 0.305])

FIGURE 16-2 Routers interconnect networks.

lower layers, so it is irrelevant for the communication implemented over IP that the systems are connected to different LAN types.

Routers are used both to link local area networks and to connect local area networks to the Internet. In addition, networks in the “core” of the Internet which normally have a much larger geographic reach, are interconnected and linked to access networks through routers, or even built of direct links between routers (“two-node networks”).

Routers are often especially designed for this purpose—so-called “dedicated routing devices.” However, the Linux kernel also offers the required functionality to let you use a Linux system as a router.

# 16.1.2 Forwarding and Routing

Routers forward IP packets from one physical network to another, where the second network is normally “closer” to the destination network (not necessarily in the sense of geographic distance, but rather from a network-topology view) than the first network. To decide in which direction each packet has to be forwarded, the router requires a certain amount of information about the Internet topology, which it stores locally.

This topological knowledge—also called forwarding information in the rest of this course—can be managed manually for small networks like the example in Figure 16–2, because there is little of it and it changes only if the LAN topology changes. For example, all router B actually needs to know the end systems in networks 3, 4, and 5. It can send all packets not addressed to systems in these networks globally towards routers A, because the “rest of the Internet” is behind router A.

In the core area of the Internet, the situation is not as simple. Rather than a small LAN, there is a large area of the entire Internet that needs a network interface of a router. The knowledge required to be able to forward IP packets with arbitrary addresses in the correct direction is much more extensive. In addition, it has to be adapted continuously: when new paths are added, when old ones fail or are overloaded, and for these reasons, a network the size of the global Internet requires automatic methods to continually update the topology information and determine suitable routes.