# 15.3 Implementing the ARP Instance in the Linux Kernel 281

constructor. In the arp_tbl structure, this pointer references the function arp_constructor(), which will be described later.

gc_timer: A garbage collection (GC) timer is created for each neighbour_table. This timer checks the state of each entry and updates these states periodically. The handling routine used by this timer is neighbour_periodic_timer(). hash_buckets[NEIGH_HASHMASK+1]: This table includes the pointers to the hash rows that link the neighbour entries linearly. The arp_hash() function is used to compute hash values.

phash_buckets[PNEIGH_HASHMASK+1]: This second hash table manages neighbour structures when the computer is used as an ARP proxy.

```
 // include/net/neighbour.h
```

The ops field of each neighbour structure includes a pointer to a neigh_ops structure. The available options define different types of neighbors and include several functions belonging to a neighbour type (connected_output(), hh_output(),etc.). For example, the functions needed to send packets to a neighboring computer are defined in the options. The following four types are available for entries in the ARP cache: generic, direct, hh, and broken.

The respective functions of these types are shown in Figure 15-5. Depending on the type of network device used, the ops fields for new neighbour structures in the arp_constructor() function are set to one of the following:

+   - arp_direct_ops() is used when the existing network device does not include hardware headers (dev->hard_header == NULL). These are directly reachable, and no layer-2 packet header is required (e.g., for PPP).
- arp_broken_ops() is reserved for special network devices (ROSE. AX25, and NETROM).
- arp_hh_ops() is set when the network device has a cache for layer-2 packet headers (dev->hard_header_cache). In this case, the ops field is set to arp_hh_ops.
- arp_generic_ops() is used when the above cases exists.

The output() functions of the neigh_ops structure are particularly important. Each neighbour structure includes an output() pointer to a function used to send data packets to a neighboring station. For ARP cache entries in the NUD_REACHABLE, NUD_PERMANENT, or NUD_NOARP state, the output() pointer references the function connected_output() of the neigh_ops structure; it is the fastest of all. these three states mean that the reachability was confirmed recently or that no confirmation is required (permanent entry or point-to-point).

For neighbour stations in other states, the output() pointer references the output() function, which is slower and more careful. Direct reachability is doubted, so an initial attempt is made to obtain a confirmation of the neighboring computer's reachability (probe).

![](bbox=[0.109, 0.95, 0.941, 0.983])