Instead, two implementations are commonly considered when it is determined that a firewall is needed. The first is a true firewall, called a filtering firewall or a packet-filtering firewall. The filtering firewall handles packets at the network level before they get to the application layer. The second method actually uses a proxy server but is often referred to as a firewall. A proxy is basically a machine that makes network connections for the user instead of the user having a direct connection. Quite often the two methods are used in tandem.

# The Packet–Filtering Firewall

A packet–filtering firewall is basically a router; its job is to examine data packets and forward them appropriately. Figure 15.2 shows one firewall configuration.

![](bbox=[0.12, 0.24, 0.77, 0.72])

As you can see, the firewall interfaces with both the Internet and the local area network and has two IP addresses as a result. Any of the machines on the LAN can send data packets to the firewall destined for some site outside. Conversely, data packets can come over the network to the firewall intended for a local user. Either way, the firewall determines whether the packet is to be permitted to proceed.

The firewall uses specific header information from the data packet to determine whether the packet should be allowed to pass through; this information includes the packet type, the source address and port number, the destination address and port number, the protocol, and any flags or options to TCP or IP. Data packets must follow certain “rules” to gain passage through the firewall. In Linux, you configure these rules using the IP Chains or IP Tables packages, which we’ll examine next.