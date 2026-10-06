
## 16.3 Implementation

slightly different and is characterized by the specific requirements of the functions that invoke inet_addr_type(): Formally invalid addresses are previously filtered and yield the RTN_MULTICAST result, and an address is treated as RTN_UNICAST, even if no entry is found in the local table.

### 16.3.3 The Routing Cache

Though the FIB data structures offer relatively fast queries, the cost to run such a query for each single IP packet would be altogether excessive. For reason the Linux kernel has a cache, in the FIB, that stores the results of the forwarding used most recently allowing them to be accessed quickly. Each forwarding operation first consults the routing cache, and the FIB is queried only if no matching entry exists in the cache. The result of the FIB query is used to create a new cache entry immediately.

The routing cache is based on a relatively simple data structure. One hash table includes the cache entries, which are linearly linked when the hash value is identical. The hash function processes the source and destination addresses for packets to be forwarded, plus their TOS values. Each cache entry contains all information required to forward a packet.

Figure 16-9 shows the hash table (left-hand side), organized as an array of rt_hash_bucket structures. The pointer struct rt_hash_bucket *rt_hash_table

| rtable | | |
|---|---|---|
| rt_hash_table[] | dst_entry | rtable |
| | next | |
| | ... | | |
| 0 | rt_hash_bucket | dev | net_dev |
| | | ... | | |
| | rt_hash_bucket | neighbour | neighbour |
| | chain | hh | hh_cache |
| | lock | input() | |
| | | output() | |
| 16 | rt_hash_bucket | ops | dst_ops |
| | | rt_flags | check() |
| | | rt_type | reroute() |
| | | rt_dst | destroy() |
| | | rt_src | negative_advice() |
| | | rt_iif | link_failure() |
| | | rt_gateway | negative_advice() |
| | rt_key | entries |
| | rt_spec_dst | ... | |
| | inet_peer | inet_peer | |

FIGURE 16-9
Data structures of the routing cache.

references this array. Within each rt_hash_bucket structure, the chain element forms the anchoring point for a list of rtable structures, representing the cache entries. Access to this list is is controlled by the read-write spinlock lock in the rt_hash_bucket structure. The size of the hash table is defined according to the main memory size when the routing code is initialized and remains unchanged afterwards.

```
struct rtable                                include/net/route.h
```

The rtable structure is rather extensive, and 16–9 show only an excerpt. In addition, we somewhat simplified the representation of its first element. Actually, the first element of the rtable structure is a union structure. u. which contains a dst_entry structure and an rtable pointer:

```
union {
    struct dst_entry dst;
    struct rtable *rt_next;
} u;
```

Both elements of u are used concurrently, without representing a problem, because the first element of the dst_entry structure is the dst_entry pointer next, and dst_entry structures occur only within rtable structures. This means that u.dst_next and u.rt_next are two different names for the same pointer; based on their types, the total object or only part of it are referenced.
The rt_src and rt_dst elements specify the source and destination addresses for IP packets handled by this entry. rt_gateway stores the address of the next router—or the destination address again, if no router is required. The interface identifier if can denote the output or input interface.
The rt_key structure integrated as element key is used as the key in searching the routing cache. The values stored do not necessarily have to match those outside. For example, in searching for an entry of a packet that was created locally and should be sent now, normally no source address is specified. which means that rt_key in the cache is null. However, the source address to be assigned to the new packet is stored in rt_src.

```
struct dst_entry
```

The dst_entry structure contains a large number of information elements. The most important elements are introduced below by origin and purpose:

Some pointers refer to other data structures required when forwarding IP packets and so they are available without additional effort—the net_device structure of the output interface, the neighbour structure to the next router or the destination system (corresponding to the rt_gateway element in the rtable structure), and hh_cache structure, which includes a packet header of the data-link layer that has just to be copied.

Function pointers to operations for further processing when receiving (input()) or transmitting (output()) an IP packet that matches the cache entry are

## 16.3 Implementation 323

invoked at the appropriate positions within the IP protocol procedure, the packet's being handled appropriately. The input() pointer refers to entries that can be used for incoming packets to ip_local_deliver() (unicast packets to be delivered locally), to ip_mr_input() (multicast packets), to ip_forward() (packets to be forwarded), or to ip_error() (forwarding impossible because destination is unreachable). The output() pointer refers to ip_output() (unicast packets) or ip_mc_output() (multicast packets).

A reference to a dst_ops structure for IPv4 always points to the defined structure ipv4_dst_ops. It contains several function pointers, and users of routing-cache entries (e.g., TCP or ARP) can use them to supply feedback to the routing cache (e.g., about connection failures). In addition, the dst_ops structure holds a counter for occupied cache entries and stores a threshold value which, when exceeded, causes the garbage collection to start (as described later).

The usage counter__use is incremented when the cache entry is used. The time of the last is also stored in the lastuse element.

Various parameters for transport protocols are copied from the fib_infrastructure structure.

Some functions to manage dst_entry structures are defined in the files include/net/dst.h and net/core/dst.c.

Interface to Forwarding Functions The implementation of the routing cache is hardly encapsulated against the other program used for forwarding; you find both in the net/ipv4/route.c. For example, there is no separate function that searches for a cache entry. Each search operates directly on the cache data structure in main interface functions for IP packet processing (ip_route_input() and ip_route_output()—see Section 16.3.4). Part of the creation of new cache entries is done there as well.

Nevertheless, there are a few methods that are used by the forwarding functions, yet belong to the routing cache. The most important such methods are described below.

```
rt_hash_code()                                net/ipv4/route.c
```

rt_hash_code() is used to calculate the hash value from the source and destination addresses as parameters. This hash value serves as index in the hash table of the routing cache.

```
rt_intern_hash()                                net/ipv4/route.c
```

The forwarding functions use the rt_intern_hash() function to insert an almost complete rtable structure into the hash table of the routing cache. New entries are always inserted in the first position in a potential collision-resolution list. If an entry with identical key exists in the list, then this entry is moved to the front, and the new entry is discarded.

In addition to inserting entries, rt_intern_hash() procures the pointer to a neighbour structure matching the next router or destination system from the rtable

The initialization function ip_rt_init() allocates memory for the routing cache, once an appropriate size has been computed. Subsequently, each element of the array is initialized. In addition the slab cache "ip_dst" is initialized. The interface management and FIB are invoked, for the cache garbage collection is started, and finally, proc entries are created.

### Cache Garbage Collection

so we ensure that all entries that are no longer needed are deleted occasionally to limit the memory requirement and to keep caches fast.

First a periodic_timer, which is initially started by add_timer() (Section 2.7.1) in the initialization function ip_rt_init(), invokes the function rt_check_expire() at regular intervals. This timer is restarted in rt_check_expire(), where the interval (measured in 1/Hz seconds) is specified by the configuration variable ip_rt_gc.

Secondly, when the number of entries in the cache exceeds a threshold value, the function rt_garbage_collect() is invoked to delete old entries. A call to rt_garbage_collect() is also made when an attempt to allocate a neighbour structure has failed. This is done because it is then assumed that the corresponding tables are full, for some neighbour entries are referenced by routing cache entries and therefore they cannot be deleted. Old routing cache entries are deleted to remedy this.

```
rt_check_expire() net/ipv4/route.c
```

The function rt_check_expire() successively checks cache-entry lists anchored in the elements of the array rt_hash_table[]. If the element specifies an expiry time, this entry is deleted if it has been exceeded. If no expiry time is specified, then rt_may_expire() is invoked to check whether this entry should be deleted.

First of all, rt_may_expire() refuses to delete referenced entries (u_dst_refcnt != 0). Otherwise, it determines how an entry has been used and compares its "age" with two threshold values passed as arguments. Three types of entries are distinguished:

- Low-value entries: This includes broadcast and multicast entries, which are additionally not in the last position in a collision resolution list. Such entries are always deleted immediately.
- "Normal" entries: These entries are deleted if their age exceeds the first threshold.
- High-value entries: These entries are created by ICMP redirect messages. They are deleted only if their age exceeds the second threshold.

The first threshold passed by rt_check_expire() varies according to the entry's position in the collision-resolution list: Starting with a value identical to the second threshold, which comes from the configuration variable ip_rt_gc_timeout, it decreases by half in each step.
