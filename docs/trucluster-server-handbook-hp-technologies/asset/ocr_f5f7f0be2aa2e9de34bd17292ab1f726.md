![](bbox=[0.07, 0.12, 0.93, 0.38])

# Figure 16-5: Common Subnet: Physical vs. Logical View

will be transparent to the clients. Routing beyond the local network will involve host routes only (no network routes).

Suppose you have no spare IP addresses at your site. Does this mean that you cannot use cluster aliases? That sad situation would eliminate one of the more important capabilities within the cluster.

The solution is to use an IP address from within a "virtual subnet." A "virtual subnet" is made up of IP addresses that are not associated with any real interfaces. Clients will access the IP addresses in the virtual subnet (used by the cluster aliases, naturally) through the cluster member serving as the router for that alias. When dealing with high traffic, a common subnet is likely to provide better performance than a virtual subnet, although a virtual subnet provides much more flexibility.

One notable difference when dealing with virtual subnets is that the route advertised by gated will be both a network route and a host route (a common subnet would advertise the host route only).

![](bbox=[0.07, 0.8, 0.93, 0.95])

# Figure 16-6: Virtual Subnet: Physical vs. Logical View