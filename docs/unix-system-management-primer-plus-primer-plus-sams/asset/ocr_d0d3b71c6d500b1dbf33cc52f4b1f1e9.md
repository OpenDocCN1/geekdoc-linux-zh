# Real-World Example: Errors on Ethernet

A company had recently been getting complaints from customers regarding the company's Web site. The customer's browsers were hanging sporadically when connecting to the site, at random times and for random URLs. The server logs showed no record of a connection from clients during the times reported, the system administrator suspected a network problem. Using SNMP to query the network interface statistics on the firewall in front of the servers revealed an error rate of 0.1%, or an error in 1 of every 1000 packets, on the company's 100Mbps Ethernet link to the Internet. This high error rate was alarming. After the ISP confirmed that there were no network problems on its side, the company's system administrator tried to reboot the firewall. Amazingly, in this case, a moderate error rate didn't cause a major outage, but it was enough to cause stopped. Some customer hassles with dropped packets. If the administrator had set up a monitor to proactively watch error rates over time (see the next section for this type of monitor), he could have caught this before the majority of users had a chance to complain.

# Measuring Collisions

A collision occurs when two machines on a shared network medium attempt to transmit data at the same time. Each machine detects the collision and retransmits the packet after waiting for a random interval to reduce the chance that the collision will recur. Collisions rarely occur on switched Ethernet networks because each port sees only traffic destined for the machine on that port. Collisions, however, happen periodically on hubs, where traffic is broadcast to all ports.

On an switched network like that of an Ethernet hub, you should consider a collision rate of over 15% severe enough to warrant further investigation. The common solution is to move to a switched network or to reduce the number of nodes on the switched network.

A collision rate of over 5% on a switched network is cause for worry. Fortunately, the usual cause of collisions on a switched network is a duplex mismatch, which you learn about in the following section.

# Duplex Considerations

A connection is full-duplex if both sides can transmit data at the same time, and half-duplex if only one side can transmit at once. Full-duplex networks provide the lowest latency, because they enable concurrent transmissions. If both sides of a half-duplex connection transmit at once, a collision occurs; this is the only reason you should see collisions on a switched network. Most Ethernet hardware supports full-duplex mode, so you should take advantage of it whenever.

Most Ethernet hardware supports autonegotiation, which automatically determines the speed and duplex of a connection between two network interfaces. Unfortunately, autonegotiation was one of the last specifications put into the Ethernet standard, so many devices do not support it correctly. Incorrect autonegotiation support can result in one side thinking the connection is full-duplex while the other side thinks it is half-duplex, causing errors and collisions on each interface.

![](bbox=[0.085, 0.955, 0.315, 0.975])