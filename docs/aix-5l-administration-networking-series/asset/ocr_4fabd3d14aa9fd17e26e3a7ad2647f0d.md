When the failed node has been repaired and rejoins the cluster, the resource group remains on its takeover node; the failed node joins as a standby node ready to take over the resource group if the node currently holding the resource group fails. Figure 28-3 displays this.

# Concurrent

A concurrent access resource group is shared simultaneously by multiple nodes. All nodes concurrently accessing a resource group acquire that resource group when they join the cluster. There are no priorities among nodes, and no failover or fallback—and therefore no interruptions in service.

The only resources included in a concurrent resource group are volume groups with raw logical volumes, raw disks, and application servers that use the disks. The device on which these logical storage entities are defined must support concurrent access. For more information, see the manuals for the devices and for HACMP.

# Basic Cluster Configuration Options

Another consideration for high availability is your basic configuration choice. The two basic types of cluster configurations are standby and takeover.

Standby configurations are the traditional redundant hardware configurations where one or more standby nodes stand idle, waiting for a server node to leave the cluster.

In takeover configurations, all cluster nodes do useful work, each processing part of the cluster's workload. There are no standby nodes. Takeover configurations use hardware resources more efficiently than standby configurations because there is no idle processing. Performance can degrade after node detachments, however, since the load on remaining nodes increases. A failover with two cascading resource groups that can both be run on the takeover node is referred to as mutual takeover.

Takeover configurations that use concurrent access use hardware efficiently and also minimize service interruption during failover because there is no need for the takeover node to acquire the resources released by the failed node—the takeover node already shares ownership of the resources.

These configurations can have many variations, depending on your hardware and what resource group types you select. The configuration options are described in detail in the HACMP manuals.

# The Cluster Manager

Each active node in an HACMP cluster has a cluster manager running that communicates with the cluster managers running on other cluster nodes. Using UDP packets called keepalives, or heartbeats, HACMP monitors the status of all configured network adapters, networks, and nodes. Missing keepalives cause the cluster manager to initiate problem determination to investigate what type of failure has occurred. The results of the problem determination trigger a series of primary and secondary events. Primary events are called by the cluster manager; secondary events are called by the primary events.