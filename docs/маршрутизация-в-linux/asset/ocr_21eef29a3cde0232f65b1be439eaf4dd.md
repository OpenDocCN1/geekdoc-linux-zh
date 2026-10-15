The Destination column when combined with the Genmask, which is the netmask of the destination network, identifies the network entry to be routed. The Gateway column identifies the gateway to be used for the particular network, should the G (gateway) flag be set in the Flags column. The Flags column tells the administrator how the kernel is going to interpret the routing entry. The various flags and their meanings are summarized in Table 9.5.

# Table 9.5 route Flags

| Flag | Description |
|------|-------------|
| I | Learned routes for this network are rejected. |
| A | Route added by addrconf, an IPv6 address configuration protocol. (http://www.ietf.cnri.reston.va.us/proceedings/95apr/charters/addrconf-charter.html) |
| C | Cache entry. |
| D | Route created by routing daemon (D) or ICMP redirect. |
| G | Use the gateway (G) identified in the Gateway column for traffic bound to the network identified in the routing entry. |
| M | route has been modified (M) by a routing daemon or ICMP redirect. |
| R | Reinstate routing to allow routing updates for this particular routing entry. |
| U | The network route is created (up) and will be used by the kernel to make routing decisions. |

The route command without any parameters is equivalent to the netstat -r command covered later in this chapter.

# -C

The -C option displays the cache statistics for routing entries as well as directly connected hosts. The output of the route command with -C also shows the source and destination addresses that triggered the route lookup. The -C parameter is used to see that routing entries are active and being used. Here is an example of route -C in action:

```
[root@lefty /root]# route -C
Kernel IP routing cache
Source      Destination     Gateway         Flags Metric Ref    Use Iface
lefty       host4.some.com  192.168.1.1     0     0      10    eth0
lefty       192.168.1.102   192.168.1.102   0     2      4     eth0
lefty       host4.some.com  192.168.1.1     0     0      10    eth0
```