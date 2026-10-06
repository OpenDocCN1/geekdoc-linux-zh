# 20.2 Implementation 407

```
init_conntrack()
net/ipv4/netfilter/ip_conntrack_core.c
```

This function creates a new connection entry. First, it creates a structure of the type ip_conntrack. This structure consists of the passed tuple for the forward direction and its inversion (created by invert_tuple) for the reverse direction. Next, atomic_set() sets the reference counter ct_general.use to value 1. The only reference that exists is initially owned by the timeout timer, which is also initialized, and its timeout function pointer is set to the function death_by_timeout(). Previously, the reference protocol module was initialized by calling its new(). The function pointer ct_general.destroy(), which is invoked to delete a connection entry, is set to the function destroy_conntrack(). In addition, a helper is entered, if one registered for the protocol used.

As soon as all data structures have been initialized, the next step depends on whether the connection to be entered was expected (i.e., whether it exists in the expected_list). If so, it is deleted from this list and set to the IPS_EXPECTED status.

```
ip_conntrack_in()
net/ipv4/netfilter/ip_conntrack_core.c
```

This function is hooked into the netfilter hook NF_IP_PRE_ROUTING; it is invoked for each packet arriving from the outside. It is also used by ip_conntrack_local(), because the only difference is in how fragmented packets are handled.

IP packets have been defragmented before they can be assigned to a connection: fragments that have already arrived are collected by the function ip_ct_gather_frags(), which, in turn, uses the ip_defrag() function. When the last fragment of a packet is received or if the packet was not fragmented, then an attempt is made to assign the packet to a connection.

First, find_proto() is used to determine the connection-tracking module for the transport protocol used. Next, the packet is checked to see whether it is an ICMP packet. If so, it is first passed to the function ip_error_track(). If successful, this function returns one, and the packet is accepted by returning NF_ACCEPT.

In contrast, ip_error_conntrack() returns null, like any other packet. resolve_normal_ct() chooses the correct connection entry (or creates one, if none exists). Subsequently, the packet() function of the associated transport protocol module is invoked and the help() functions of all registered helper modules are invoked. If one of these functions fails, then nf_conntrack_put() releases this connection entry.

```
ip_conntrack_local()
net/ipv4/netfilter/ip_conntrack_standalone.c
```

This function is hooked into the netfilter hook NF_IP_LOCAL_OUT; accordingly, it is invoked for each IP packet originating from a local process. The only difference from how incoming packets are handled in ip_conntrack_in() is that fragmented packets are not handled by the connection-tracking module. All other packets are simply passed to ip_conntrack_in().