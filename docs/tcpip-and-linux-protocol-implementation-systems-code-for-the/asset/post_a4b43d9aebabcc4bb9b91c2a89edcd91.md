
Routing calculation location. Having accumulated information about the state of the network, we need to compute the best routes. This might be done at a central node that would distribute actual path information to a central and every router, or, more realistically, can be autonomously at each router. CPU power is cheap. Memory is reasonably cheap. Thus it makes sense to take the advantage of timeliness and independence from failure of other nodes, by distributing (and to some extent, effectively replicating) the computation of the routes at every router.

Routing update data semantics. Route updates carry link status information. At its simplest, this is a binary/down indication. However, increasingly network operators wish to select routes based on more complex metrics. These measurements can include propagation delay, current mean queuing delay, link capacity, monetary cost, loss statistics, and many other possibilities.

In special circumstances, other counterintuitive approaches have been taken in the design of routing systems. For example, in ad hoc radio networks, random routing is sometimes used. In systems with very limited computational resources (e.g., CPU, memory), hot potato routing is used, when packets are forwarded based on current local information, such as choosing the output link with the shortest current queue.

In practice, at the moment, Internet routing is largely distributed and adaptive. Forwarding decisions (frequent) are largely decoupled from routing calculations (occasional). These design choices make the forwarding task relatively simple, but the routing protocol and map computation task Routing Information Base (RIB) and Forwarding Information Base (FIB) relatively complex. A few other tasks need to be accomplished:

Neighbor discovery. A router starts either configured with information about who is down the end of them links or has to find it out by probing or listening.

Status. A router maintains some idea of the state of its neighbors, typically by periodically saying hello—this will sometimes be authenticated. The exact details for this operation are part of a specific routing protocol.

Distribution. Routers collaborate. They exchange views with each other about the state of the network as well as each other. There are actually two different approaches to the actual details of this. The common, cheap and cheerful way is called distance-vector. Each router tells its neighbors everything it knows and has learned so far. This is discussed later in this chapter. The more respectable method is called link-state. Here, each router floods reports about the state of links that it looks after to all the other routers in a domain or area.

## Routing 545

Scaling. As the Internet grows, the potential load on the links, router CPU, and memory systems also grows. Since network growth in the last two decades has been exponential, this would not bode well for network service providers or operators. Luckily, several techniques exist to reduce the load on the network routing and forwarding system.

- Hierarchical addressing. Most networks employ some kind of hierarchical addressing. In many networks, such as the postal system and the telephone network, addresses in use are variable in length. Only much of an address as necessary need be quoted to make it unique for the area within which it is being used. When constructing routes for the whole world, however, the full address must be used. When sending a letter to someone else in the same city, when the author does not have to quote the city name or country name; when the post offices of the world construct their routing tables to be able to deliver letters to anywhere in the world, they need to be able to distinguish 10 Downing St., London, from 10 Downing St., Cambridge, and both of these 10 Downing St., New York, NY, USA.

In the Internet, addresses are fixed in length, but a technique classless interdomain routing is used to provide the hierarchical addresses within a fixed-length field. This relies on associating a variable length mask with an address in use in a routing area, and exchanging the mask as the address when building up maps of the world. We look at this more below.

- Hierarchical routing. In large networks, it is generally the case that different regions in the network have more or less connectivity. If a region is connected to the rest of the world only via a single link (single homed), then it seems unnecessary to bother the rest of the world with the details of the internal topology of the region.

It is also the case that we deploy new routing protocols in part of the network at a time rather than having a flag day when we upgrade (downgrade) the entire network.

Thus it is important to separate routing into regions. This is done in two different ways in Internet routing. Firstly, routing protocols are divided into intradomain and interdomain. Here, the term domain refers to the autonomous management of routing, and not any other aspect of networking. Intradomain routing domains are separated from each other by interdomain routing protocols. In IP networks, these are known as Interior Gateway Protocol (IGP) and Exterior Gateway Protocol (EGP). Secondly, within a domain, a routing protocol may have explicit configuration management mechanisms for dividing routers and links into subdomains.

## 546 TCP/IP and Linux Protocol Implementation

there are several examples of this, ranging from subnet routing, up to area routing (in Open Shortest Path First (OSPF) and Intermediate System-Intermedia System (IS-IS)). We will revisit this briefly at the end of this chapter.

Routing table construction. It is an internal matter for a routing daemon how it constructs its routing information base. The entries will essentially list all the peer routers, and typically all possible destination prefixes, as well as some destinations known about but currently unreachable. The most general data structure for this would be a graph of nodes (routers) and edges (links), with the edges labeled with the various metrics for making route (or forwarding) decisions. Associated with any node and edge would be the source of the information about it, and the time that the last information was received. Of course, in practice, given all information arrives either from or via neighbors, this data could be built around a smaller data structure, such as a list of neighbors and the list of updates, with a single entry for the update time—it really depends on the granularity of information in the routing protocol.

Forwarding table computation. At the end of each update epoch, a computation is carried out by the routing daemon to derive the new forwarding information base (FIB). This is then downloaded into the forwarding engine—in Linux terms, the kernel FIB is updated by the routing process. This can and often is manual, of course.

In distance-vector algorithms, the data distribution is the computation. A router receives a vector of destinations and metrics from a neighbor, and simply replaces the forwarding entry for the next hop with the new value, if the value is better.

In state protocols, a more complex procedure is needed to derive the forwarding table from the set of route updates. At the end of the route flooding epoch, the network graph is built, by adding all the updates in a jigsaw puzzle. Subsequently, Dijkstra's well-known graph-walking algorithm can be used to carry out a search from the current router to all others (and the networks attached to those routers). This finds the path from here to there with the lowest metric. If paths with different metrics need to be considered (or multiple alternate paths for load balancing or instant failover), then the algorithm can be called multiple times.

Typically, we can imagine that this only occurs for the entire routing system very occasionally. Most updates may result in local parts of the graph being changed, and there are several techniques for incrementally computing a Dijkstra, and keeping the CPU to a minimum.

Forwarding is simple. However, the lookup of an entry is complicated by the fact that the procedure typically involves an algorithm called longest match
