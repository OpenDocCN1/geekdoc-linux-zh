A variant on this design is to put only the processors and memory on the main node, and then have the I/O buses be separate. Another design option is to have separate nodes for processors, memory, and I/O buses, which are all interconnected.

It is also possible to have nodes that contain nodes, resulting in a hierarchical NUMA design. This is depicted in [Figure 3-3](#).

# ### Types of Interconnects

There is no standardization of interconnect technology. More relevant to Linux, however, is the topology of the interconnect. NUMA machines can use the following interconnect topologies:

+   *   *Ring topology*, in which each node is connected to the node on either side of it. Memory access latencies can be nonsymmetricthat is, accesses from node A to node B might take longer than accesses from node B to node A.

+   *   *Crossbar interconnect*, where all nodes connect to a common crossbar.

+   *   *Point-to-point*, where each node has a number of ports to connect to other nodes. The number of nodes in the system is limited to the number of connection ports plus one, and each node is directly connected to each other node. This type of configuration is depicted in [Figure 3-3](#).

+   *   *Mesh topologies*, which are more complex topologies that, like point-to-point topologies, are built on each node having a number of connection ports. Unlike point-to-point topologies, however, there is no direct connection between each node. [Figure 3-4](#) depicts a mesh topology for an 8-node NUMA system with each node having three interconnects. This allows direct connections to three "close" nodes. Access to other nodes requires an additional "hop," passing through a close node.

![](bbox=[0.2, 0.7, 0.73, 0.76])