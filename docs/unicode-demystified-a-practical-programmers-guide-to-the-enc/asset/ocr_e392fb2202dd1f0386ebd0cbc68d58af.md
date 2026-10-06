# Types of Networks and How They Work 367

number of bits used for the subnet mask. If it were a class B network (of which 16 bits are already fixed), this yields 2^{28} (24 total bits - 16 fixed bits = 8 bits, 2^8 = 256) total networks with 2^8-2 (256-2=254) on each network. If you use a subnet mask, use netconfig to let the system know about it.

For example, when you divide the class 122.25.4.0 into eight subnets, you use a subnet mask of 255.255.255.224, FFFFFFE0, or /27 (27 Is). The eight result networks are 122.25.4.0, 122.25.4.32, 122.25.4.64, 122.25.4.96, 122.25.4.128, 122.25.4.160, 122.25.4.192, and 122.25.4.224. You can use a Web-based subnet mask calculator to calculate to determine the preceding subnet mask, use an IP address of 122.25.4.50, go to www.teleplanet.com/public/sparkman/netcalc.html for a nice subnet calculator.

# CIDR: Classless Inter-Domain Routing

CIDR (pronounced cipher) allows groups of addresses that are smaller than a class C block to be assigned to an organization or ISP or further subdivided and parce out. In addition, it helps to alleviate the potential problem of routing tables on major Internet backbone and peering devices too large to manage.

The pool of available IPv4 addresses has been depleted to the point that no one gets a class A address anymore. The trend is to reclaim these huge blocks, if possible, and recycle them into groups of smaller addresses. Also, as more class C addresses are assigned, routing tables on the Internet are filling up and causing memory overflows. The solution is to aggregate^{12} groups of addresses into blocks and allocate them to IPs in which turn subdivide these blocks and allocate them to customers. The address class designations (A, B, and C) described in the previous section are used less today, although still are used. When you request an address block, your ISP usually gives as many addresses as you need and more. The ISP aggregates several contiguous smaller blocks and routes them to your location. This aggregation is CIDR. Without CIDR, the Internet as we know it would not function.

For example, you might allocate the 192.168.5.0/22 IP address block, which could support 2^{10} hosts (32-22=10). Your ISP would set its routers so that any packets going to an address block would be sent to your network. Internally,

+   1. The first and last networks are reserved in a manner similar to the first and last host, although the standard is flexible. You can configure your router(s) to reclaim the first and last networks in a subnet. Different routers have different techniques for reclaiming these networks.
2. Subtract 2 because the first and last addresses on every network are reserved.
3. Aggregate means to join. In CIDR the aggregate of 208.178.99.124 and 208.178.99.124/23 (the aggregation of two class Cs).