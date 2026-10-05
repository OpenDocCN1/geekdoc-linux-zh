# Routing 551

about 16 comparisons). Of course, the worst-case performance is the length of the address, or 32 comparisons for an IPv4 address.

### The next stage in the evolution of forwarding table lookup schemes was the idea of adding a cache of most-recently-used routes in front of the standard FIB. Before looking a destination in the standard FIB, the forwarding code will look up a destination in a route cache, which is hopefully a smaller table and can be searched more quickly. This idea sounds good until you realize that the performance advantage of caching depends on the pattern of access over time. Specifically, caching relies on temporal locality—this means that if a sequence of lookups resulting in fact tend to reference the same subset of destinations, and this subset only changes slower than the rate of actual packets arriving, then a cache can be a big win. In practice, it depends on whether you are in the Net this is true or not—certainly, according to measurements made by some experts for core routers, there doesn't appear to be a great deal of temporal locality. The Internet is “all over the place” [14]. On the other hand, a given router may see packets go by a very focused set of destinations.

### It was observed that one could have a hash table for each possible prefix length. A refinement of this is to see that, rather than searching all of these different tables linearly, one can do a binary search by prefix lengths, starting with the most common [12]. This is straightforward computing. Even with an IPv6 address of 128 bits, this will take eight hash lookups to find the longest matching entry.

A still more recent approach is to try to improve over the radix tree by compressing the tri in some way [13]. This scheme involves reducing the number of levels in the tri by increasing the degree of CAMs.

Content-addressable memory—CAMs. A CAM is a custom piece of hardware that is addressed by its content—a 32-bit-wide CAM would be a device that is accessed by presenting it with an input value (e.g., the IP destination), and returns another value (i.e., the next hop) if the input value is in its contents. Generally CAMs get expensive if the width is large, and require a number of refinements to these devices, as *ternary* CAMs. Ternary CAMs allow three values for each input bit, including a *don't* care. This allows multiple matches to be done in parallel—the order of the results typically implies preference.

# ### 8.3.2 FIB Purpose

Forwarding tables are consulted for every packet to be sent from a system.
An entry is indexed by IP destination address, and has to store this and the