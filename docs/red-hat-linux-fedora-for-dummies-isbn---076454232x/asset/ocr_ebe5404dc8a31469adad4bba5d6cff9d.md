Machine C is totally out of the loop. By making sure that C doesn't know what A and B are saying, the switch keeps network communication private. Hubs, on the other hand, broadcast the network traffic from one machine to all machines connected to the hub. When A sends information to B, the hub broadcasts that information to both B and C.

The following section describes how to build a wired network; the section after that shows a wireless one. You can mix wired and wireless networks, but, for simplicity, we describe how to build a pure wired or wireless network.

# ### *Wiring your network with, uh, wires*

Way back in prehistoric times (circa 1996), you had to be technically savvy to wire your own network. Wiring consisted of coaxial cables like those used for cable TV connections. Coaxial cables are bulky and require you to use special tools to attach the connectors to the cable ends.

Life is easy now. Wiring your network requires that you obtain *Cat 5* cables, similar in appearance to telephone cables. Cat 5 cables are manufactured with telephone-like connectors that are a snap (pardon the pun) to use. No muss, no fuss.

![](bbox=[0.13, 0.51, 0.2, 0.56])

**TIP**

You can buy Cat 5 cables at any electronics store. They come in many colors and sizes. Cat 5 cables aren't cheap, but they aren't terribly expensive, either. They're reliable and much easier to work with than coaxial cables.

You have to use a network switch or hub in conjunction with Cat 5 cables. Switches and hubs are the glue that holds your network together. Both switches and hubs connect individual computers so that they can communicate with each other.

Most — if not all —networking equipment is now based on the Ethernet protocol. Ethernet is inexpensive and readily available. You can purchase it from any consumer electronics store, mail-order catalog, or online computer seller. You don't need to know any of the technical aspects of Ethernet because it requires no configuration. You need to know only that an Ethernet connector looks similar to a telephone jack. However, Ethernet and telephone jacks aren't compatible.

![](bbox=[0.13, 0.8, 0.2, 0.87])

**TIP**

One byproduct of a switch's design is that it effectively makes your network faster. Network traffic flows only between the machines that are talking to each other. The computers that aren't talking to each other don't use the switch's bandwidth. For example, when machine A is sending information to B, machine C doesn't see any of the traffic.