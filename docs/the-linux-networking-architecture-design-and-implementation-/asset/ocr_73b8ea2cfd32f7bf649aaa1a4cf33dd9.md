# 21.3.4 Initializing an Address-Binding Process

```
ipt_snat_target(), ip_dnat_target()          net/ipv4/netfilter/ip_nat_rule.c
```

ipt_snat_target() and ipt_dnat_target() functions are registered branch destinations for the nft table, nat. This process is processed only if the first packet of a new session flow was registered in ip_nat_fn(). The table uses lists to identify session flows subject to source NAT or destination NAT.

Initially, either of the two functions use ip_conntrack_get() to find the corresponding connection entry of the connection-tracking module and invokes the ip_nat_setup_info() function to do a new address binding. The result of this invocation, the address information of the newly assigned binding, is passed to the calling function.

```
ip_nat_setup_info()                               net/ipv4/netfilter/ip_nat_core.c
```

This function is invoked by the handling functions for the SNAT and DNAT branch destinations and essentially does three things:

+   - When the get_unique_tuple() (see below) is invoked, it searches for a free address available to do the translation. If no free address is available, then the value NF_DROP is returned and the packet is dropped.

+   - To other address translations into account, the entry for the reverse direction inverted by invert_tuplepr() is used as the basis rather than the connection-tracking address for the forward direction of the session flow, because the reverse direction entry already includes the translated addresses, in contrast to the forward direction.

+   - Invoking the ip_conntrack_alter_reply() function causes the reverse direction of a connection entry to be altered so that reply packets are allocated properly to the correct connection, despite its translated address.

+   - Finally, the new address binding is added to the substructure of the ip_nat_info connection entry. The mapping rules (e.g., transformation of source address and source port) are generated from comparing the original ip_conntrack_tuple structure with the new structure, supplied by get_unique_tuple().

```
get_unique_tuple()                               net/ipv4/netfilter/ip_nat_core.c
```

This function is invoked by ip_nat_setup_info() to search for a free address within a specified address range (represented by a structure of the ip_nat_multi_range).

If the function is invoked at the NF_IP_POST_ROUTING hook (i.e., to map the source address), then invoking the function find_appropriate_src() checks whether an address binding exists for the source address (IP address, protocol number, and protocol-specific part) in the bysource hash table for that packet. If this binding is within the specified address range, it is returned as a new address.