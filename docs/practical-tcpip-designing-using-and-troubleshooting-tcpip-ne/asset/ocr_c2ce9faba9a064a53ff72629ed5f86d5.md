# **6.13 Complex sub-nets (4) – implementation**

Finally we come to implementing the sub-net scheme we have designed. Figure 6.22 shows the full network diagram. We’ve included part of the sub-net allocation diagram from Module 6.12 for reference. The only items missing from the figure are:

+   1. the default gateway for a router is the router above it, i.e.
+       - default gateway for Sales and Tech is Ops
+       - default gateway for Ops, HR, and Fin is HQ’s router
+       - (your ISP configures your HQ router or tells you what its default gateway is – the router upstream on your ISP connection)
+   2. the default gateway for a host on a sub-net is the router above it, i.e. the router connecting this sub-net to its parent
+   3. the IP address for a host in a sub-net must obviously be chosen from that sub-net’s range. The netmask for the host is the same as the netmask specifying the sub-net’s range. For example, a host on the HR sub-net might be:
+       IP number: 192.0.2.179
+       netmask: 255.255.255.240
+       and a host on the Tech sub-net might be
+       IP number: 192.0.2.85
+       netmask: 255.255.255.224
+   4. we have a couple of ranges left over as spares:
+       - on the Ops network, we have a range of 16 addresses that we can use for another small sub-net later on, or to expand the Ops-self network that occupies the numbers directly below it
+       - on the HQ network we have a 64-address range that we can use for extra sub-nets later on. In this instance we *couldn’t* combine it with the HR range (.176–.191) below because the maximum size of range that can start on .176 is 16, as shown in Figure 6.15.

We’ve used a few conventions in the diagram:

+   - we’ve numbered the routers with the highest IP numbers in their ranges. This is common practice on many sites.
+   
+   For example, the HQ network range is 192.0.2.160–192.0.2.175. The broadcast address is .175, so we’ve used .174, .173, .172, and .171 for the routers
+   - to reduce the clutter a little, we’ve shown the network ranges with a gray background. To familiarize you with the different range notations, we show each network range in three different but equivalent ways:
+       a. as IP number and netmask, e.g. 192.0.2.64, netmask 255.255.255.224
+       b. CIDR notation of IP number and number of bits in the netmask, e.g. 192.0.2.64/27
+       c. bottom and top IP numbers of the range, e.g. 192.0.2.64–192.0.2.95.

If you do implement a network like this, the first sanity check to carry out when you’ve designed it is that all interfaces on the same wire are in the same range and have the same netmask.