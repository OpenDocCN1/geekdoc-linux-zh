As illustrated in Figure B-14, a special MAC address (all bits to 1: ff:ff:ff:ff:ff:ff) is used for the ARP broadcast:

![](bbox=[0.08, 0.15, 0.92, 0.48])

Figure B-14

The process is described below:

+   1. Host A issues a query to all computers through an ARP broadcast request via `ping C`: "Who is host C?"
+   2. Host C replies (ARP reply): "My hardware address is 00:50:34:B0:CF:07."
+   3. The communication is established.

Host A memorizes the reply to its query in a cache. You can view this cache with the `arp` (`/sbin/arp`) command. The command also provides options for editing the cache, such as deleting an invalid assignment of a MAC address to an IP address (`arp -d hostname`).

![](bbox=[0.12, 0.83, 0.27, 0.9])

For details on the `arp` command, enter `man arp`.

You can use the `arpwatch` program (`/usr/sbin/arpwatch`) to monitor ARP requests and replies. By doing this, you can locate errors in the ARP traffic.

# Internet Protocol (IP)

IP provides the underlying services for transferring data between end systems in TCP/IP networks and is specified in RFC 791.

Data is transported through the network in packet form (also called *datagrams*). The main characteristics of this protocol are that it is connectionless and unreliable.

The fact that IP is a connectionless protocol means that no end-to-end connection of communication partners is set up for data transfer.