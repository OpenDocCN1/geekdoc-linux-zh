# TABLE 4.1 Cable Lengths from Figure 4.4

| Inter-Computer Distance | Bus Topology Total Length | Star Topology Maximum Length | 10base-2 | 10base-5 | 10base-T and 100base-T |
|---|---|---|---|---|---|---|
| 10 ft. | 124 ft. | 22 ft. | ✓ | ✓ | ✓ |
| 50 ft. | 621 ft. | 112 ft. | X | ✓ | ✓ |
| 135 ft. | 1676 ft. | 302 ft. | X | X | ✓ |

Furthermore, with Ethernet it’s possible to link two hubs or switches, either using a crossover cable (p. 20) or uplink connectors (p. 24) on the hubs or switches. The result would be two networks like that in Figure 4.3, linked at their central points. If you look again at Figure 4.2, it’s not hard to see how the network would be wired initially. Chances are the hub would lie along the wall by the corridor, with cables run along the walls to each of the computers. The expansion into Room 2 could be accomplished either by running multiple lines from that hub into Room 2 or by running a single line and placing a second hub in Room 2 to service Room 2’s computers. Either solution could be accomplished without disrupting the existing network, assuming that the main hub or switch had enough room for expansion to begin with.

# The Ring Topology

A ring topology is logically similar to a bus topology, except that it’s a bus that’s linked to its own end, as shown in Figure 4.5. Ethernet doesn’t support a ring topology, so you won’t encounter one in most small networks. IBM’s Token Ring network technology is, as the name implies, based on a ring topology, so you’ll encounter the ring topology if you need to set up, maintain, or link to an existing Token Ring network.

Token Ring in particular, however, doesn’t look like a ring topology—not physically, at any rate. Like 10BaseT and 100BaseT Ethernet, Token Ring uses a hub with cables radiating out from it. This is because Token Ring implements the ring inside the hub, thus giving Token Ring many of a star topology’s characteristics. In practice, therefore, Token Ring closely resembles twisted-pair Ethernet in its physical cable layout requirements.

# Combining Topologies

Today, networks seldom operate in isolation. Networks—of the same or different topologies—can link to other networks in a variety of ways. A comprehensive list of such methods is beyond the scope of this book. I do discuss two important methods (bridges and routers) of