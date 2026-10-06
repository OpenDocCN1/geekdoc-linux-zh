# Chapter 15 Address Resolution Protocol (ARP)

**Possible States for neighbour Entries** It is theoretically possible to leave the entries for all neighbouring states learned in the ARP cache. However, there are several reasons why these entries are valid for a limited period of time. First, it would mean memory wasted to maintain entries for all these computers, especially if there is little or no data exchange with them. Second, we have to keep these entries consistent. For example, there can be a situation when the network adapter in a computer is replaced and so this computer will have a different layer-2 address. This computer could no longer be reached with the old mapping. Therefore, it is assumed that the mapping stored for a computer is no valid if that computer has not sent anything for some time.

In practice, the size of the ARP cache is limited (normally to 512 entries), and of or rarely used entries are periodically removed by a kind of garbage collection. On the other hand, it could be that a computer does not communicate over a lengthy time, which means that its table is empty. In fact, this was not possible up to kernel Version 2.4, because the size of the table structure was also stored downwards: No garbage collection was done when the table included fewer than gc_thresh1 values, which normally mean 128 entries. This bottom limit no longer exists in kernel Version 2.4 and higher. You can use the arp command (see Section 15.2) to view the contents of the ARP cache.

Each neighbour entry in the ARP cache has a state, which is stored in the nud state structure. Figure 15-6 shows all possible states and the most important state transitions. There are other transitions, but

![](bbox=[0.158, 0.453, 0.952, 0.918])

FIGURE 15-6
State transition diagram for neighbour entries in neighbour caches.