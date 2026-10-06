# 17.4 Multicast Data Path in the Linux Kernel 345

(igmp_timer_expire()) for this group (timer in the ip_mc_list structure). In addition, the variable reporter in the function igmp_timer_expire() remembers that this station replied to the query. This information may be required later to tell the router that the computer wants to leave that group.

However, igmp_send_report() serves not only to send query reports; it can also be used to send packets to announce that a computer wants to leave a group (leave messages). The actions are identical in both cases: the destination address and the IGMP message type are different. In case of a report, the packet is sent to the corresponding group; in case of a leave message, all multicast routers in the LAN (all-routers). Notice that the value of the TTL field has to be set to 1 to ensure that the response will spread only within the LAN. Next, the IP packet is built, and the IGMP fields are set accordingly. Finally, the packet is shipped out over

```
ip_check_mc()
```

```
net/ipv4/igmp.c
```

ip_check_mc(in_dev, mc_addr) is actually not part of the IGMP protocol; it is used for IP routing. More specifically, ip_check_mc() checks whether the local computer is currently a member of the multicast group mc_addr. For this purpose, the list of active groups of the network device's IP instance (mc_list in the in_device structure) is checked and compared against the group address passed. If a match is found, then one is returned; otherwise, null is returned

ip_check_mc() is also used in the ip_route_input() to learn whether the packet should be delivered locally. If this is the case (as is always true for multicast routers), then the packet is passed to ip_route_input_mc(). If the computer does not act as a multicast router, and if the packet does not belong to any group of the input network device, then it will be discarded. This actually means that rather few packets are discarded, because most undesired multicast packets are normally filtered out by the hardware filter in the network card.(See Section 17.4.1).

# 17.4 MULTICAST DATA PATH IN THE LINUX KERNEL

This section describes how multicast packets are processed in the Linux kernel. To get a good insight into matters, we will first explain how a multicast packet takes across the kernel, then discuss different aspects of the data path. We will begin on the MAC layer, to see how multicasting is supported in local area networks and to introduce the following IP multicast concepts:

+   - virtual network devices,
- multicast routing tables, and
- replicating of data packets.

As we introduce the implementation, we will emphasize differences between multicast-capable end systems and multicast routers.