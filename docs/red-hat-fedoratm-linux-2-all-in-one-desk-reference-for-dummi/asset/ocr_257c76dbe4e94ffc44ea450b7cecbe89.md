+ **Perimeter network with bastion host:** This firewall configuration includes a perimeter network between the Internet and the protected internal network. A secure bastion host resides on the perimeter network and provides various services.

In a large organization, you may also have to isolate smaller internal networks from the corporate network. You can set up such internal firewalls the same way you set up Internet firewalls.

In the next few sections, I describe the common forms of a firewall: screening router with packet filtering, dual-homed host, perimeter network with bastion host, and application gateway.

# Screening the router with packet filtering

If you directly connect your organization's internal network to the Internet, you have to use a router to ensure proper exchange of packets between the internal network and the Internet. Most routers can block a packet according to its source or its destination IP address (as well as the port number it seeks to use). The router's packet-filtering capability can serve as a simple firewall. Figure 3-1 illustrates the basic concept of packet filtering.

![](bbox=[0.13, 0.54, 0.86, 0.82])

Many router vendors, such as Cisco and 3Com, offer routers that can be programmed to perform packet filtering. The exact details of filtering depend on