# TABLE 19-2
iptables Targets

| Target | Function |
| --- | --- |
| ACCEPT | Allow packet to pass through the firewall. |
| DROP | Deny access by the packet. |
| REJECT | Deny access and notify the sender. |
| QUEUE | Send packets to user space. |
| RETURN | Jump to the end of the chain and let the default target process it. |

# Targets

A target could, in turn, be another chain of rules, even a chain of user-defined rules. A packet could be passed through several chains before finally reaching a target. In the case of user-defined chains, the default target is always the next rule in the chains from which it was called. This sets up a procedure or function call-like flow of control found in programming languages. When a rule has a user-defined chain as its target, when activated, that user-defined chain is executed. If no rules are matched, execution returns to the next rule in the originating chain.

> Tip Specialized targets and options can be added by means of kernel patches provided by the Netfilter site. For example, the SAME patch returns the same address for all connections. A patch-o-matic option for the Netfilter make file will patch your kernel source code, adding support for the new target and options. You can then rebuild and install your kernel as described in Chapter 33.

# Firewall Chains

The kernel uses three firewall chains: INPUT, OUTPUT, and FORWARD. When a packet is received through an interface, the INPUT chain is used to determine what to do with it. The kernel then uses its routing information to decide where to send it. If the kernel sends the packet to another host, the FORWARD chain is checked. Before the packet is actually sent, the OUTPUT chain is also checked. In addition, two NAT table chains, POSTROUTING and PREROUTING, are implemented to handle masquerading and packet address modifications. The built-in Netfilter chains are listed in Table 19-3.

# TABLE 19-3
Netfilter Built-in Chains

| Chain | Descriptions |
| --- | --- |
| INPUT | Rules for incoming packets |
| OUTPUT | Rules for outgoing packets |
| FORWARD | Rules for forwarded packets |
| PREROUTING | Rules for redirecting or modifying incoming packets, NAT table only |
| POSTROUTING | Rules for redirecting or modifying outgoing packets, NAT table only |