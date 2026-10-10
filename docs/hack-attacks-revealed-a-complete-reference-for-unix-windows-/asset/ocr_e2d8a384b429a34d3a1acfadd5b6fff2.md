With Link State routing protocols, only partial routing table updates are transmitted, and only when necessary, for example, when a link goes down or comes up. The metric is based on a much more complex algorithm (Dijkstra), whereby the best or shortest path is determined and then selected. An example of this type of path determination is a scenario that features a low-bandwidth dial-up connection (only one hop away), as opposed to higher-bandwidth leased lines that, by design, are two or three hops away from the destination. With Distance Vector routing protocols, the dial-up connection may seem superior, as it is only one hop away; however, because the Link State routing protocol chooses the higher-bandwidth leased lines, it avoids potential congestion, and transmits data much faster.

Figure 6.20 lists the five most common routing protocols and their specifications.

# **Administrative Distance**

The Administrative Distance is basically a priority mechanism for choosing between different routes to a destination. The shortest administrative distance has priority:

| ROUTE | ADMINISTRATIVE DISTANCE |
| :--- | :--- |
| Attached | 0 |
| Interface | |
| Static Route | 1 |

| | **RIP** | **RIP v.2** | **IGRP** | **RTMP** | **OSPF** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Type** | Distance Vector | Distance Vector | Distance Vector | Distance Vector | Link State |
| **Updates** | Entire Table- 30 sec | Entire Table- 30 sec | 90 sec | Hello Packets- 10 sec | Hello Packets- 10 sec/ LSA- 30 min |
| **Class Support** | Classful | Classless | Classful | Classful | Classless |
| **Algorithm** | Bellman-Ford | Bellman- Ford | Bellman- Ford | Bellman- Ford | Dijkstra |

**Figure 6.20** The five most common routing protocols.

| | |
| :--- | :--- |
| EIGRP Summary | 5 |
| EBG P | 20 |
| EIGRP Internal | 90 |
| IGRP | 100 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| EGP | 140 |