# 262 Chapter 14 The Internet Protocol V4

cannot be transmitted. If the route can be determined without problem, the next step clears the remaining protocol header, as in the first way. The packet leaves the IP layer on the same path.

# 14.4 INTERNET CONTROL MESSAGE PROTOCOL (ICMP)

The Internet Control Message Protocol (ICMP) is the error-report mechanism for the IP layer, which also resides in the network layer. Though ICMP is based on IP, it doesn't make IP more reliable. Packets can be lost despite the use of ICMP and IP or won't notice that packets are lost. The only purposes of this error-report mechanism are to report errors to other computers and to respond to such reports. It is mandatory for each IP implementation to implement ICMP. The ICMP implementation is defined in the [Post81b] RFC documents:

+   RFC 792 [Post81b]: This is the basic definition, describing the packet types and uses.

+   RFC 1122 [Brad89]: Definition of the requirements on terminal equipment (hosts) connected to the Internet.

+   RFC 1812 [Bake95]: This document describes the requirements for switching computers (routers) in the Internet.

However, RFC specifications often leave much room for flexible implementation. For some functions, it is even optional whether you implement them. For this reason, ICMP implementations and even configurations of the same implementation can differ considerably.

The most popular application of ICMP is error detection or error diagnostics. In more than ninety percent of all cases, the first information transmitted by a newly installed network adapter over an IP network will probably be that of the ping command, which is fully based on ICMP. This allows you to check the reachability of other computers easily and without noticeable load on the network. This procedure is often done in automated form (e.g., to monitor servers). Beyond simply checking the reachability of computers, the set of error messages allow a network administrator for a network-analysis tool to obtain a detailed overview of the internal state of an IP network. For example, poorly selected local routing tables or wrongly set options in individual computers can be detected. And finally, it is possible to use ICMP to synchronize clocks within a network, in addition to other—partly outdated—functions, which will be briefly discussed in this section.

# 14.4.1 Functional Principle of ICMP

ICMP sends and receives special IP packets representing error or information messages. Error messages occur whenever IP packets have not reached their destinations. All cases create information messages, which can additionally include a request for reply. Notice that the ICMP functionality becomes active within the network implementation of the Linux kernel only provided that a problem situation occurs during another data traffic or when ICMP packets arrive from another computer. As mentioned earlier,