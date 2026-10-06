# 390 Chapter 19 Packet Filters and Firewalls

The criterion -i <interface> can be used to select only packets that arrive or come from a specific interface.

For the TCP protocol, we can use -y to specify that only packets with the SYN flag set and the ACK flag cleared should be considered. (See Section 19.1.2.)

We can use -f to specify that the rule should apply only to the second and all consecutive fragments of a fragmented IP packet. This criterion can be thought of as a predecessor of the netfilter introduced in Chapter 20, which implements stateful connection tracking. Only the first fragment includes the transport protocol header, so we cannot specify port numbers together with this criterion.

All criteria can be negated by a leading exception sign -s ! 127.0.0.1 would select all packets with a source address unequal 127.0.0.1.

Branch destination: This parameter specifies what should happen to packets subject to these rules. ACCEPT lets this packet pass; DENY discards packets silently; REJECT returns an ICMP error message of the type "Destination Unreachable" to the sender before it drops them. The branch destination RETURN is used for a conditioned return from a rules chain. This is particularly interesting during handling of user-defined rules lists, because it allows us to return to the calling rules lists.

Packets can be logged by the syslog mechanism by -log), in addition to one of the above branch destinations. This allows us, for example, to better detect and trace attempts of attacks (which means one of the criteria described in Section 19.1.3 is met) or to monitor the traffic volume at a specific network interface.

# 19.2.2 Drawbacks of the ipchains

Design flaws were observed soon after the introduction of ipchains in Linux 2.2. The most important problems are as follows:

+   - ipchains have no uniform programming interface that would have enabled us to embed new rules lists into the kernel without having to consider network implementation details. For this reason, adding rules lists was tiresome and error-prone.
- In contrast, the netfilter architecture supplies a framework that minimizes direct interventions in the network code and allows us to add additional code in the form of modules for packet mangling in the kernel by using the regular interface.
- The integration of code for transparent proxies was expensive in ipchains and was connected to many interventions in the Linux kernel.
- In ipchains, rules were necessarily necessary to bind a network address in general, which made the creation of rule sets too complicated because the address was the only way to distinguish packets generated locally from packets to be forwarded. ipchains implemented "masquerading" (a simple NAT variant) and the packet filter code in one piece, which made the code harder to read and unnecessarily complex.