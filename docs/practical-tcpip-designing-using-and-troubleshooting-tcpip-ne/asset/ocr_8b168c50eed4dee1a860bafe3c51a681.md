# ## Summary

+   - when TCP/IP has to send a packet to another machine, it decides using its netmask whether it can send the packet directly to its destination on the local wire:
+   	- if it can, it sends the packet directly, using ARP if necessary
+   	- otherwise it sends the packet to a "router" that is also connected locally, to be forwarded on towards its final destination

+   - to have a router forward a packet onwards towards its destination, the sender sets the destination Ethernet address to the Ethernet address of the router, but sets the destination IP address to the IP address of the final destination. As long as the router is configured correctly to act as a router, it will forward the packet onwards towards its final destination

+   - to simplify the configuration of machines on the LAN, TCP/IP supports a default gateway router. If the destination IP address isn't on the directly connected LAN, this machine will send the packet to the default router to be forwarded. (This assumes that no other, more specific route to the destination has been configured explicitly on this machine. We cover such specific routes in Chapter 5)

+   - we have now introduced the three fundamental parameters of networking: (1) IP address, (2) netmask, (3) default gateway. Almost every networking problem you encounter will be due to an error in configuring these

+   - the **tracroute** program is a useful diagnostic tool, and lets you trace the route from your machine to any destination IP address.

# ## What’s next?

We’ve covered what routing is, in concept. Before we go on to more advanced routing – configuring multiple interfaces, and specifying routes in addition to or instead of your default gateway – we have to cover netmasks in much more detail, because they are so closely intertwined with routing and router configuration. The next chapter deals with netmasks and IP addresses in depth, and Chapter 5 then covers advanced routing.

# ## Notes and further reading

We have covered only basic troubleshooting here. We’ll go into it in much more detail in Chapter 5, when we have the necessary tools to explore routing in depth. For now, here are a couple of useful articles on routing problems with NT:

+   - [ ] MS-KB-Q151795 *Err Msg: The Route Addition Failed: 87*

As the article says helpfully, "this message alerts you that you have an addressing problem" (as if you didn't know already). Another more general article is:

+   - [ ] MS-KB-Q102908 *How to Troubleshoot TCP/IP Connectivity with Windows NT*