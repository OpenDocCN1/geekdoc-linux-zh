# 21.1 Introduction 411

destination port] tuple. Similarly, an ICMP session flow can be identified by an [IP source address, IP destination address, ICMP type, ICMP ID] tuple.

[SrHo99] describes three characteristic requirements that should be met by all NAT variants:

+   - transparent allocation;
- transparent routing;
- correct handling of ICMP packets.

The following sections explain each of these requirements and what they mean.

# 21.1.2 Transparent Address Allocation

Because we can use NAT to connect networks with different address spaces, these addresses from the respective address spaces have to allocated among them. This allocation can be static or dynamic. If we use static allocation, the allocations are maintained during the entire operation of a NAT router. Static allocations simplify the address translation, because no state information about specific session flows has to be maintained. In dynamic allocation, the allocation is specified at the time that a session flow is opened. This allocation rule can be extended beyond the IP addresses to include the transport protocol ports. (See Section 21.1.6.) In any event, address allocation should be transparent. The mechanisms should be hidden from the applications in end systems.

# 21.1.3 Transparent Routing

We use the term “transparent routing” in the following discussion to distinguish the routing functionality of a NAT router from the functionality of a normal router. Transparent routing differs from normal routing in packets that are forwarded between two different address spaces by changing the address information in IP packets and routing to match these modified addresses.

Address binding: This phase permanently binds two addresses from the two address spaces to be bound. This should not be confused with the address allocation mentioned above—the address allocation determines value bindings. These bindings will then exist only after the address binding. In connections with static address allocation, address binding is also static, but dynamic binding occurs at the beginning of a session flow and is released as soon as this session ends. If we want to map internal network addresses to global, external addresses, then we should bind each additional session flow originating from the same end to the system address.

Address translation: Once an address has been bound, each IP packet of that session flow has to be manipulated. This manipulation can be limited to the IP addresses, but it could also extend to TCP/UDP ports. (See Section 21.1.6.) Notice that the checksum in the IP header, or in the UDP/TCP header, has to be recomputed.