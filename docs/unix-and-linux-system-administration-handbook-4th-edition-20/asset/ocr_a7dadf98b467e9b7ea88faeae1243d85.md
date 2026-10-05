# ICMP redirects

add the fourth and second routes displayed by netstat -rn above. (The first and third routes in that display were added by ifconfig when the eth0 and eth1 interfaces were configured.)

The final route is also added at boot time. It configures the loopback interface, which prevents packets sent from the host to itself going out on the network. Instead, they are transferred directly from the network output queue to the network queue inside the kernel.

In a stable local network, static routing is an efficient solution. It is easy to manage and reliable. However, it requires the system administrator to know the topology of the network accurately at boot time and that the topology not change often.

Most machines on a local area network have only one way to get out to the rest of the network, so the routing problem is easy. A default route added at boot time suffices to point the way out. Hosts that use DHCP (page 469) to get their IP addresses also obtain a default route with DHCP.

For more complicated networks, dynamic routing is required. Dynamic routing is implemented by a daemon process that maintains and modifies the routing table. Routing daemons on different hosts communicate to discover the topology of the network and to figure out how to reach distant destinations. Server routing daemons are available. See Chapter 15, Routing, for details.

# ICMP redirects

Although IP generally not concern itself with the management of routing information, it does define a name damage control called an ICMP redirect. When a router forwards a packet to a machine on the same network from which the packet was originally received, something is clearly wrong. The sender, the router, and the next-hop router are all on the same network, the packet could have been forwarded in one hop rather than two. The router can conclude that the sender's routing tables are inaccurate or incomplete.

In this situation, the router can notify the sender of its problem by sending an ICMP redirect packet. In effect, a redirect says, "You should not be sending packets for host xxx to me; you should send them to host yyy"

In theory, the recipient of a redirect can adjust its routing table to fix the problem. In practice, redirects usually ignores authentication information and are therefore untrustworthy. Dedicated routers ignore redirects, but most UNIX and Linux systems accept them and act on them by default. You'll need to consider the possible sources of redirects in your network and disable their acceptance if they could pose a problem.

Under Linux, the variable accept_redirects in the /proc hierarchy controls the acceptance of ICMP redirects. See page 504 for instructions on examining and resetting this variable.

![](bbox=[0.206, 0.863, 0.243, 0.903])