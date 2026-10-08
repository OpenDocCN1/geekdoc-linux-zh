# TROUBLESHOOTING IN THE NETWORK 523

+   - Does the port at the repeater or hub show 'red'? Maybe the cable is damaged.

+   - If present, can the name server be addressed? Does a ping work? Can you issue requests by means of nslookup and do you receive answers?

+   - Does the inetd run, and have the correct daemons entered in the file /etc/etc/inetd.conf? Can you see any peculiar entries in the log file of the inetd?

+   - Have the necessary RPC daemons started? You can check this by means of rpcinfo -p.

+   - The kernel display strange messages? You can view past messages by means of dmesg, but without time stamps. In this case, you should look into the corresponding system log (facility kern).

Depending on installation and use of the computer, further easily verifiable functions can be added or individual functions can be dropped. Especially with cabling problems, software alone does not get you far enough in your search for sources of trouble. For larger networks, the acquisition of a network analyser is highly recommended. With such an instrument, you can detect collisions, broken cables or missing terminations.

# 24.1.2 Bottlenecks in the Internet

Often, individual computers in the Internet cannot be reached at all or can only be reached with difficulty. By means of the traceroute command, you can gather an overview of all routers or gateways where the data transfer is likely to be carried out. The result is not 100 per cent accurate because a different route may be dynamically chosen for each individual packet. traceroute makes use of functions of the IP and ICMP to obtain this information. The program also exists for NT, where it is called tracer.

The program sends an IP packet which has only limited life cycle. This life cycle is stored in the file ttl (Time To Live, Max Hops in IPv6) in the IP header. The first packet is sent with a ttl of 1, the destination is a port number which is probably not used. The gateway that removes the packet from the network because it has exceeded its time to live, sends an ICMP message of the type 'time exceed.' On the basis of this message, this gateway be identified. Subsequently, the ttl is increased by one, and the packet is sent again. If