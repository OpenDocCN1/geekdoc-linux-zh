# Traceroute

Traceroute provides a peek into the path your network packets take to get to a remote host. It does this by sending a series of ping packets to the destination, but it uses a trick within the packets. The ICMP packet used for the ping includes a time-to-live value. The time-to-live value is decreased by every router that handles the packet along the path. When the time-to-live value reaches zero, the packet is discarded by the network, and the router returns an error packet to the source.

Traceroute uses this process to slowly increase the time-to-live value in the ICMP ping packet. As each router along the path returns the error packet, Traceroute documents the router, then sends another ICMP ping packet with the time-to-live value increased by one.

This process provides a trail of each router the packet traverses to get to the final destination, as shown in Figure 14-11.

![](bbox=[0.22, 0.52, 0.68, 0.73])

Figure 14-11: The Traceroute window with an active trace.

The first five entries in the list are for my internal home network. Once the packet leaves my DSL modem, it starts to traverse routers inside my ISP, then goes out to the Internet world until it reaches the final destination. Traceroute times each trip and displays the total amount of time each packet takes. This is great for determining whether you have a slow router in your network path.

> Because the Traceroute program uses ping packets, it's also susceptible to hosts and routers that ignore ping packets due to security concerns. Don't be surprised if your traceroute dies before getting to its final destination.