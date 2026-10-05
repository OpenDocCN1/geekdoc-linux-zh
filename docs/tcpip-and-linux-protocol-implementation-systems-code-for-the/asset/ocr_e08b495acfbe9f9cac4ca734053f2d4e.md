# 620 TCP/IP and Linux Protocol Implementation

messages up-stream towards the source to indicate that they have no need of traffic for this group. Of course, with dynamic membership, we might suddenly find someone at a site gains a member for a group where previously they had pruned themselves from the source tree. We must somehow allow the tree to regrow, and this is done by using a new message between dense routers called a prune message. In some senses, this just extends the idea of an IGMP join (as a graft message extends the idea of an IGMP leave) towards a source.

To keep life safe from lost messages, the prune state that suppresses data distribution is periodically subjected to timeout and removal, which leads to flooding of the data. Downstream nodes without prune again.

Of course, this scheme doesn't scale at all. However, it illustrates the basic idea of distribution trees and state management. It also resulted in a modest, but important change to routing, which is that the forwarding engine needs to update the routing information base as a result of routes being installed (at least for multicast) data driven, as well as because of router-router updates, or applications signing.

# 8.4.2 Sparse and Single-Source Multicast

The now widely used alternatives to dense-mode multicast are sparse mode and single source. These both leverage off the idea of an explicit graft message flowing from downstream nodes to join a tree towards a distribution point, known as the rendezvous point (RP). In the latter case, the rendezvous point is at the source (i.e., single-only) source itself. In both cases the data-driven nature of flooding and pruning is avoided entirely, but the distribution trees may be suboptimal—switching from an RP to a source-based tree is a configuration once the rendezvous with a receiver has been made.

# 8.5 QoS Routing

Traditional routing involves selection by destination address only. This means that it is hard to load balance or provide sensible choices of path or route to accord with non-default performance requirements. Traditional routers have one optimal path to destination, and the routing metrics are single values. For QoS routing, multiple paths would be possible, and alternative paths would have different QoS properties. Routing updates need to include QoS parameter information, and the route selection must use destination address, source address, ToS, and so on. The whole integrated services system, and to a lesser extent differentiated services, require some way to inform routers about these extra requirements.