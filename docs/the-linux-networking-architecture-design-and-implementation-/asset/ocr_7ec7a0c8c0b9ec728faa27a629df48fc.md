# 20.2 Implementation 405

init(), fini(), init_or_cleanup() net/ipv4/netfilter/ip_conntrack_standalone.c

The init() and fini() functions are invoked to initialize or remove the connection-tracking module, and, in turn, invoke the function init_or_cleanup() with the parameter 1 (initialize) or 0 (remove).

During the initialization, the actual connection-tracking functionality is initialized by the first calling of ip_conntrack_init(). Subsequently, the entry in the proc file system is generated, and the functions ip_conntrack_in() and ip_conntrack_local() are hooked into the appropriate netfilter hooks. Inversely, these functions are unhooked when the module is removed, the entry is deleted from the proc file system, and finally, the function ip_conntrack_cleanup() is invoked.

# ip_conntrack_init() net/ipv4/netfilter/ip_conntrack_core.c

This is the initialization routine for the actual connection-tracking functionality. It adds the three standard protocols—TCP, UDP, and ICMP—to the protocol list and initializes the ip_conntrack_hash hash table.

# ip_conntrack_cleanup() net/ipv4/netfilter/ip_conntrack_core.c

This function prepares for a removal of the connection-tracking module. More specifically, a locking mechanism is used to ensure that all IP packets currently handled are properly completed. Subsequently, a few reserved memory locations are released.

# hash_conntrack() net/ipv4/netfilter/ip_conntrack_core.c

This helper function computes the hash value for a data structure of the type ip_conntrack_tuple.

# get_tuple() net/ipv4/netfilter/ip_conntrack_core.c

This function uses the protocol data passed from an IP packet to create a matching data structure of the type ip_conntrack_tuple. First, the IP source and destination addresses and the transport protocol are taken, and then the pkt_to_tuple of the matching transport protocol module is invoked.

# invert_tuple(), invert_tuplepr() net/ipv4/netfilter/ip_conntrack_core.c

These functions invert an ip_conntrack tuple structure by swapping the IP source and destination addresses. In addition, the function invert_tuple() of the matching transport protocol module is invoked—for example, to swap the source and destination ports for TCP or UDP.