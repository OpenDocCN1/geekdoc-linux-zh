# Other Networking Commands and Setup

Setting up a network is an intensive planning exercise for both network and system administrators. No two networking environments are alike. There is typically a lot of networking electronics to which your system is connected. There are many useful commands related to testing connectivity to other systems and networking configuration. Should you encounter a problem, you want to have an understanding of some networking commands that can be lifesavers. In addition, you can encounter some tricky aspects to networking setup if you have some networking hardware that your UNIX systems must interface to, such as routers, gateways, bridges, etc. I give an example of one such case: connecting a UNIX system to a router. At the same time, I cover some of the most handy networking commands as part of this description.

Consider Figure 13-11, in which a UNIX system is connected directly to a router.

![](bbox=[0.15, 0.42, 0.92, 0.68])

Here we have a UNIX system connected to segment 128.185.61. This is a class "B" Internet address with subnetting enabled.

The /etc/hosts file needs to have in it the UNIX system with node ID 2, the router, and any other systems on this segment or segments on the other side of the router.

If the router is properly configured, we should be able to seamlessly connect from 61 to systems on segments 60, 62, and 63. The router should be configured to allow our system to connect to systems on other segments (60, 62, and 63) by going through the router. Some unforeseen configuration