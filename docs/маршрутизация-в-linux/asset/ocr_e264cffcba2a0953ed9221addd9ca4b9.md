The beginning of this scenario works exactly as it did in Scenario 1. However, when router Arts returns to life, its neighbors will suddenly notice Hello messages that it always sends out of its interfaces—even though Arts would have noticed its neighbors were gone as well.

After the neighboring routers add Arts back to the possible paths for source/group traffic, a series of DR elections might occur if Arts suddenly duplicates traffic that's being sent by another router to a certain collection of networks. It's not long before everything's back in order.

The program used to implement PIM-DM in Linux is gated. Once again, remember that you also have to have a unicast protocol installed, such as OSPF or RIP-2, for any of the PIM protocols to function properly.

# Summary

The multicast routing protocols you're most likely to use in Linux are MOSPF, DVMRP, and either PIM-SM or PIM-DM. MOSPF is most useful in smaller multicast setups where you need a single protocol to handle both unicast and multicast, and RIP-2 doesn't really handle multicast data as much as it does unicast updates. DVMRP, PIM-SM, and PIM-DM all require an additional unicast protocol to work with. You would use PIM-SM if your multicast group members tend to be very spread out, and you'd use PIM-DM or DVMRP if they are more densely packed. Table 2.1 outlines the multicast protocols available to you and the data you'll need to get started.

Table 2.1 The Programs Used to Implement Multicast Routing Protocols in Linux, and the RFC Documents That Contain Vital Background Information

| Protocol | Program | RFC or Draft |
|---|---|---|
| MOSPF | mrouted | 1585 |
| DVMRP | mrouted | draft-ietf-idmr-dvmrp-v3-10.txt |
| PIM-SM | gated | 2362 |
| PIM-DM | gated | draft-ietf-pim-v2-dm-03.txt |

See http://www.multicasttech.com/multicast_faq.html if you have questions about multicast in general.