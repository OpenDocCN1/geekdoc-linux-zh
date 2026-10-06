# 348 Linux Administration: A Beginner's Guide

![](bbox=[0.205, 0.135, 0.783, 0.386])

Figure 12-1 Our sample network

depending on course on the speed of the PC, the CPU cache, the type of NIC, Peripheral Component Interconnect (PCI) or other interfaces, and the system bus speeds. In fact, several commercial routers exist that are running a stripped and optimized Linux kernel under their hood with a nice GUI administration front-end.

# Routing with Static Routes

Let us assume that we want to configure a dual-homed Linux system as a router, as shown in Figure 12-1.

In this network, we want to route packets between the 192.168.1.0/24 network and the 192.168.2.0/24 network. The default route is through the 192.168.1.8 router, which is performing network address translation (NAT) to the Internet. (We discuss NAT in further detail in Chapter 13.) For all the machines on the 192.168.2.0/24 network, we want to set their default route to 192.168.2.1 and let the Linux router out how to forward on to the Internet and the 192.168.1.0/24 network. For the systems on the 192.168.1.0/24 network, we want to configure 192.168.1.15 as the default route so that all the machines can see the Internet and the 192.168.2.0/24 network.

This requires that our Linux system have two network interfaces: eth0 and eth1. We configure them as follows:

```
[root@server ~]# ip address 192.168.1.15/24 eth0
[root@server ~]# ip address 192.168.2.1/24 eth1
```