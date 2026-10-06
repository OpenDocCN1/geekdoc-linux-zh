# 16.3 Implementation

slightly different and is characterized by the specific requirements of the functions that invoke inet_addr_type(): Formally invalid addresses are previously filtered and yield the RTN_MULTICAST result, and an address is treated as RTN_UNICAST, even if no entry is found in the local table.

# 16.3.3 The Routing Cache

Though the FIB data structures offer relatively fast queries, the cost to run such a query for each single IP packet would be altogether excessive. For reason reason the Linux kernel has a cache, in the FIB, that stores the results of the forwarding used most recently allowing them to be accessed quickly. Each forwarding operation first consults the routing cache, and the FIB is queried only if no matching entry exists in the cache. The result of the FIB query is used to create a new cache entry immediately.

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