# **IP Sub-netting**

Routed IP environments require that your pool of IP addresses be sub-netted. This allows each sub-net to see itself as a separate segment of the larger internetwork. The router then ties together the various sub-nets into one network. The router knows how to route traffic to the correct segment because it builds a routing table. The routing table is basically the networks roadmap.

IP sub-netting is fairly complex, and so to make this discussion informative but still digestible at an introductory level, we will limit our exploration of sub-netting to one class of IP addresses; we will look at an example of sub-netting a Class B range of IP addresses. The mathematical tricks that we use to sub-net the Class B network can also be used to sub-net a Class A or Class C network (although sub-netting Class C networks greatly limits the number of usable IP addressed that you end up with).

Sub-netting is a two-part process.

First you must determine the sub-net mask for the network (it will be different than the default sub-net masks; for example, the default for Class B is 255.255.0.0). After figuring out the new sub-net mask for the network, you must then compute the range of IP addresses that will be in each sub-net.