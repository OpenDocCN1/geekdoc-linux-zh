**MASQUERADE** Similar to SNAT with ---to-source, except that the IP information is grabbed from the interface on the specified port. For use on systems with dynamically assigned IP addresses, such as those that use DHCP, including most dial-up lines. Valid only in rules in the POSTROUTING chain of the NAT table.

**-to-ports port[-port]** Specifies the port for the interface you want to masquerade. Forgets connections when the interface goes down, as is appropriate for dial-up lines. You must specify the TCP or UDP protocol (--protocol tcp or udp) with this target.

**REJECT** Similar to DROP, except that it notifies the sending system that the packet was blocked.

**-reject-with type** Returns the error type to the originating system. The type can be any of the following, all of which return the appropriate ICMP (page 1087) error: icmp-net-unreachable, icmp-host-unreachable, icmp-port-unreachable, icmp-proto-unreachable, icmp-net-prohibited, or icmp-host-prohibited. You can specify type as echo-reply from rules that require an ICMP ping (page 379) packet to return a ping reply. You can specify tcp-reset from rules in or called from the INPUT chain to return a TCP RST packet. This parameter is valid in the INPUT, FORWARD, and OUTPUT chains and user-defined chains called from these chains.

**RETURN** Stops traversing this chain and returns the packet to the calling chain.

**SNAT** Source Network Address Translation—Rewrites the source address of the packet. Appropriate for hosts on a LAN that share an Internet connection.

**-to-source ip[-ip][:port[-port]]** Alters the source IP address of an outbound packet, and the source IP addresses of all future packets in this connection, to ip. Skips additional rules, if any. Returning packets are automatically de-SNATed to the originating host. Valid only in the POSTROUTING chain of the NAT table.

When you specify a range of IP addresses (-ip) or use multiple -to-source targets, iptables assigns the addresses in a round-robin fashion, cycling through the addresses, one for each new connection.

When the rule specifies the TCP or UDP protocol (-p tcp or -p udp), you can specify a range of ports. When you do not specify a range of ports, the rule matches all ports. Every connection on a NATed subnet must have a unique IP address and port combination. If two computers on a NATed subnet try to use the same port, the kernel maps one of the ports to another (unused) one. Ports less than 512 are mapped to other ports less than 512, ports from 512 to 1024 are mapped to other ports from 512 to 1024, and ports above 1024 are mapped to other ports above 1024.

# ## Copying Rules to and from the Kernel

The iptables-save utility copies packet filtering rules from the kernel to standard output so you can save them in a file. The iptables-restore utility copies rules from standard input, as written by iptables-save, to the kernel. Sample output from iptables-save follows: