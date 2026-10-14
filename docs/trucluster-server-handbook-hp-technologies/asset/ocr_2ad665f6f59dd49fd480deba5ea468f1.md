![](bbox=[0.22, 0.11, 0.82, 0.28])

# Figure 4-5: Redundant MC Virtual Hub Configuration

For more information on the other individual Memory Channel 2 jumper settings, please refer to Chapter 5 in the TruCluster Server Cluster Hardware Configuration Guide.

For the purposes of redundancy of the cluster interconnect, dual-rail MC is supported in a virtual hub mode. Dual-rail MC occurs when you have two Memory Channel adapter cards in one cluster node directly connected to another two Memory Channel adapter cards in another cluster node. How would this be configured from a Memory Channel adapter card perspective? You would identically jumper both Memory Channel adapters in cluster member1 as VH0. In the other cluster member, member2, both Memory Channel adapters cards would be jumpered as VH1. Each of the adapters cards with the VH0 setting in member1 would then be cabled to an adapter with the VH1 setting in member2. See Figure 4-5.

# 4.4.1.2 Standard Hub Mode

In standard hub mode, Memory Channel adapter cards are again in each cluster member, but instead of being directly connected to a Memory Channel adapter card in another cluster member, each is connected to a Memory Channel Line card in a central Memory Channel hub. All internode communications flows between the Memory Channel adapter cards through the Memory Channel Hub. Please see Figure 4-7 for an illustration.

Like the Memory Channel adapter cards in a virtual hub mode configuration, the Memory Channel adapter cards in standard hub mode configuration must be properly jumpered. For an MC1 adapter card jumper J4 is set accordingly for standard hub mode - see Table 4-6. For an MC2 adapter card jumper J1 is set for standard hub mode - see Table 4-7.

Dual-rail Memory Channel is also supported in a standard hub mode. How would this work? To implement a dual-rail Memory Channel configuration in a standard hub mode, it would require two Memory Channel adapter cards per cluster member and the use of two separate Memory Channel Hubs. As each primary Memory Channel adapter card is connected to a Memory Channel Line card in the primary Memory Channel Hub, take note of the physical slot of the Memory Channel Line card that is being used. When the secondary Memory Channel adapter card is connected to a Memory Channel Line card in the secondary Memory Channel Hub, it must use the same numbered slot in the secondary Memory Channel Hub as the primary Memory Channel Hub.

Let’s illustrate how to implement a dual-rail configuration on a three-node cluster as an example. In the primary Memory Channel Hub, the primary Memory Channel card in cluster member1 is physically connected to the Memory Channel Line card in slot 0. The primary Memory Channel card in cluster member2 is connected to the Memory Channel Line card in slot 1. The primary Memory Channel card in cluster member3 is connected to the Memory Channel Line card in slot 2. This same Memory Channel Hub configuration is replicated for the secondary Memory Channel Hub using the secondary Memory Channel adapter cards in each cluster node. See Figure 4-6.