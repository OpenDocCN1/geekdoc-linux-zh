# INTRODUCTION TO iptables 881

![](bbox=[0.2, 0.073, 0.952, 0.226])

Figure 25-15 Example of rules in a chain work

end of processing for that packet. If the answer is no, the kernel applies the second rule in the chain to see whether the packet came from the specified IP address. If the answer is yes, the destination in the packet's header is changed and the modified packet is sent on its way. If the answer is no, the packet is sent without being changed.

Chains are collected in three tables: Filter, NAT, and Mangle. Each of these has builtin chains (described next). You can create additional, user-defined chains in Filter, the default table.

Filter table The default table is mostly used to DROP or ACCEPT packets based on their content; it does not alter packets. Builtin chains are INPUT, FORWARD, and OUTPUT. All user-defined chains go into this table.

NAT table The Network Address Translation table. Packets that create new connections are routed through this table, which is used exclusively to translate the source or destination fields. Builtin chains are PREROUTING, OUTPUT, and POSTROUTING. Use this table with DNAT, SNAT, and MASQUERADE targets only.

+   * DNAT (destination NAT) alters the destination IP address of the first inbound packet in a connection so it is rerouted to another host. Subsequent packets in the connection are automatically DNed. DNAT is useful for redirecting packets from the Internet that are bound for a firewall or a NAT server (page 896).

+   * SNAT (source NAT) alters the source IP address of the first outbound packet in a connection so it appears to come from a fixed IP address—for example, a firewall or router. Subsequent packets in the connection are automatically de-SNATed. Replies are SNATed so they go back to the original sender. SNAT is useful for hiding LAN addresses from systems outside the LAN and using a single IP address to serve multiple local hosts.

+   * MASQUERADE differs from SNAT only in that it checks for an IP address to apply to each outbound packet, making suitable for use with dynamic IP addresses as those provided by DHCP (page 470). MASQUERADE is slightly slower than SNAT.

Mangle table Used exclusively to alter the TOS (type of service), TTL (time to live), and MARK fields in a packet. Builtin chains are PREROUTING and OUTPUT.