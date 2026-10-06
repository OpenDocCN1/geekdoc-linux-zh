
## 16.3 implementation 309

The result of a search in a routing table is essentially a network interface, which should be used to forward the current packet, and the next router, if the destination system is not in the network directly connected over this interface. The dev parameter can be used to specify a network interface. The next router is specified by the via parameter, if required.

A next router can be specified only provided that it is known how this router can be reached. This means that another router describing the subnetwork of the router has to exist; naturally, the next router always has to be in a directly connected subnetwork. The network interface used to reach this router can be determined from it. For this reason, when using via to specify a router when you create an entry, you don't have to use dev to specify a network interface.

There are a number of additional attributes you can assign to a routing entry (see Chapter 24), which will be used when the entry is assigned to a TCP connection.

The following example shows the commands used to build the main routing table for router B from Figure 16–4:

```
root@tux # ip route add 10.0.3/24 dev eth0
root@tux # ip route add 10.0.4/24 dev eth1
root@tux # ip route add 10.0.5/24 via 10.0.4.3
root@tux # ip route add 10.0.2.1 dev ppp0
root@tux # ip route add default 10.0.2.1
```

However, the last two entries would not be created manually, but automatically by the PPP daemon as soon as a PPP connection is established. ip route show can be used to obtain the table shown in Figure 16–5 (in a slightly different format):

```
root@tux # ip route show
10.0.2.1 dev ppp0 scope link
10.0.4/24 dev eth1 scope link
10.0.5/04 via 10.0.4.3 dev eth1
10.0.3/24 dev eth0 scope link
default via 10.0.2.1 dev ppp0
```

## 16.3 IMPLEMENTATION

The following discussion divides the routing implementation in Linux into three functional units:

As described in Section 14.2, ip_route_input() and ip_route_output() are the two functions invoked when IP packets are handled to run routing-specific

> For efficiency reasons, rather than doing a routing request for each single IP packet created by TCP, there is only one single routing request when a connection is established.

tasks; they will be described in Section 16.3.4. These functions are also called “forwarding functions” in the following discussion.

Rules and routing tables together form the so-called forwarding-information base (FIB). Whenever necessary, forwarding functions query the forwarding-information base; this action is also called a forwarding query or FIB request in the following discussion. An FIB request is initiated by the fib_lookup() function. The implementation of routing rules is strongly encapsulated within the FIB, so routing rules and routing tables will be discussed separately in Sections 16.3.1 and 16.3.2. Because using the FIB for each single IP packet received or sent would require too much time, an additional routing cache that stores the table entries the most recently and allows fast access to these entries. Section 16.3.3 describes how this routing cache is implemented.

### 16.3.1 Routing Rules

As described in Section 16.1.6, rule-based routing uses a set of rules to decide which routing tables should be searched in which sequence for a suitable entry to forward a packet and whether the packet may be forwarded at all. The rules are processed successively by ascending priority until a decision can be made.

The entire implementation of the rules-processing method, including the data types used, is included in the fib_rules.c file. The narrow interface is described by some function prototypes and inline functions in a common header file, ip.h, fib.h. If rule-based routing is enabled in the kernel configuration (CONFIG_IP_MULTIPLE_TABLES; see Section 16.2.1), then fib_rules.c is not compiled. In this case, the “replacement functionality” of the two routing tables local and main in this sequence is fully handled by the inline functions in ip_fib.h.

**Data Structures** The set of rules is represented in the kernel by a linear list of fib rule structures, sorted in ascending order by priority value and hooked into the stub fib_rules variable. Initially, this list contains three entries: the fib structures default_rule, main_rule, and local_rule, which are statically defined. Figure 16-6 shows this status of the rules list. A read-write spinlock fib_rules_lock is used to regulate access to the list.

```
struct fib_rule net/ipv4/fib_rule.c
```

The fib_rule structure, to begin contains two counters, a link pointer, struct fib_rule *next, and a reference counter, atomic_t r_clref. The latter specifies the number of references to a specific instance of the structure. The counter is incremented by atomic_inc() when new rules are added, and especially when a reference to a rule is returned in a result for a forwarding request. A call to atomic_dec_and_test() in the interface function fib_rule_put(), which frees fib_rules, decrements the reference counter. The memory is actually freed when this counter reaches a value of zero. In this situation, the function additionally checks for whether the entry was set to one by explicitly deleting the rule

|_rules | fib_rule |
| :--- | :--- |
| r_next | r_next |
| r_clref: 2 | r_clref: 2 |
| r_preference: 0 | r_preference: 3276 |
| r_table: RT_TABLE_LOCAL | r_table: RT_TABLE_MAIN |
| r_action: RTN_UNICAST | r_action: RTN_UNICAST |
| r_dst_len: 0 | ... |
| r_src_len: 0 | |
| r_src: 0x0 | fib_rule |
| r_srcmask: 0x0 | r_next |
| r_dst: 0x0 | r_next: 0x0 |
|__mask: 0x0 | r_clref: 2 |
| r_srcmap: 0x0 | r_preference: 3276 |
| r_flags: 0 | r_table: RT_TABLE_DEFAULT |
| r_tos: 0 | r_action: RTN_UNICAST |
| r_ifindex: 0 | |
| r_ifname[]: | |
| r_dead: 0 | |

FIGURE 16-6 List routing rules (initial state). Optional structure entries are not shown (by inet_rtm_delrule(); see further below). If this is not the case, then there must be an implementation error which is written to the system log for the user's attention. Next within the structure follows some information about the rule: the priority value u32 r_preference, the unsigned char r_table for a routing table to be used, and the field unsigned char r_action, which specifies the action that should run if the rule's mask matches the packet processed. The rule types mentioned in Section 16.1 can be coded with the RTN_UNICAST, RTN_BLACKHOLE, RTN_UNREABLE, RTN_PROHIBIT, and RTN_NAT, which are declared in include/linux/netlink.h. Additional attributes for the action are the u32 r_srcmap and u32 classid. The first of these two entries is the source address for static translation. The second entry is present only if the kernel was configured with the CONFIG_NET_CLS_ROUTE option (See Section 16.2.1.). It contains a class identifier for the discipline that is assigned to packets, the following routing entry does not contain a class identifier. The rule's selector is represented by an address prefix and a corresponding network mask for the packet's source and destination (u32 r_src, r_src_mask, r_dst, r_dstmask), by the network interface (int r_ifindex), by the content in the TOS field (u8 r_tos), and additionally by the framework (u32 r_fwmark). Moreover, the structure includes the lengths of the address prefixes (unsigned char r_src_len, r_dst_len) and the network interface name (char r_ifname[IFSIZ]). These attributes are used when rules are deleted, and displayed at the RT netlink interface. In contrast, forwarding decisions uses only the address mask and the much faster integer index for the network Though the u8 r_flags entry is accepted from the RT netlink interface, it has no meaning in routing processing.

**Initialization and Internal Functions** The initialization function fib_rules_init(), which is invoked (from within ip_fib_init()), which, in turn, is invoked by ip_rt_init() when the routing is initialized during system start, does not have to initialize the rules list, because its initial entries are already statically linked and anchored. However, it registers the callback fib_rules_export() in the notification chain for state changes to network devices (See Section 5.2.4.). If changes occurs, fib_rules_event() is invoked, which branches to fib_rules_attach() when a new network device is registered, by fib_rules_detach() when a network device is unregistered. These two functions visit all existing rules and correct the ifindex entry, which is meaningful for registered devices only and should otherwise be set to -1. As mentioned in connection with the r_clref counter, the fib_rule_put() function is used to release references that point to fib structures. This function is also declared in ip_fib.h, because it is invoked not internally, but also when structures are released that were returned as replies to forwarding requests and a reference to the rule that led to the selection of a route from a routing table.

**RT Netlink Interface** The RT netlink interface represents the only way to manage routing rules. For this purpose, the table inet_rtnetlink_table[] (net/ipv4/devinet.c) has pointers for the message types RT_NEWRULE, RT_DEL_RULE, and RT_GETRULE that point to the functions inet_rtm_newrule(), inet_rtm_delrule(), and inet_dump_rules(). So that those functions are invoked to handle the corresponding RT netlink messages. A large part of the implementation of these functions consists of converting the data structures of RT netlink messages and the fib_rule structure. In addition, when new rules are added, the values are checked for whether or not they are valid and consistent. If a rule is added without stating a routing table, the function fib_empty_table() is invoked and searches for a table not used. If no priority is stated, then new rule is added to the rules list before all other rules with a nonzero priority.

**Interface to Forwarding Functions** The rules database represents the access point to the FIB virtually, because rules have to be used to identify a suitable routing table for each forwarding request. For this reason the "central" request function, fib_lookup(), is also implemented in fib_rules.c (or in ip_fib.h if route-based routing is used). However, it handles only a small part of the work involved; important parts are handled by invoking functions from other FIB parts, as we will see.

> If you invoke ip rule without stating a table, then it automatically uses the table main. To an RT netlink message with unspecified table, you have to use the table 0 option specifically with ip rule add.
