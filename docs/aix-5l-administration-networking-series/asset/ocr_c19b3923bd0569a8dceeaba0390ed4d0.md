node you want to own a resource group, for example, if you want the cluster node with the highest processing capabilities to control a critical application.

In a cascading resource group, when a node fails, its resources are taken over by the available node with the next highest priority and then returned to the preferred node when it is available again, except for the cascading without fallback configuration, which allows you to schedule the primary node’s reintegration. However, there is always a temporary disruption in application availability when the failed node reintegrates into the cluster and takes back its "own" resources.

Cascading configurations do not require IP address takeover.

# Cascading Without Fallback Attribute

Cascading resource groups have an attribute cascading without fallback (CWOF) that allows you to alter the traditional cascading behavior. When CWOF is set to true, an owner node does not reacquire its resource groups when it is back in the cluster. It is thus similar to a rotating resource group, except that it does not require IP address takeover.

Using cascading resource groups with CWOF set to true avoids interruptions of service caused by failbacks. However, without IPAT, there are some conditions under which CWOF resource groups can "clump" on a single node (unlike rotating groups, which usually distribute themselves appropriately). If you use CWOF, you must be prepared to sometimes manually redistributed clumped resource groups. For more information on CWOF, see the HACMP manuals.

# Inactive Takeover Attribute

Inactive takeover is an attribute that allows you to fine-tune the initial acquisition of a cascading resource group by a node. If inactive takeover is set to true, then the first node in the resource group to join the cluster acquires the resource group, regardless of the node's designated priority. This brings the resource group up quickly but may cause a disruption when the highest priority node joins and acquires its resources. If inactive takeover is false (the default setting), each node joining the cluster acquires only those resource groups for which it has been designated the highest priority node.

# Why Use Concurrent Resource Groups?

If it is crucial to have constant shared access with no time lost to failovers or fallbacks, you may want to choose a concurrent configuration.

A concurrent access resource group is shared simultaneously by multiple nodes. All nodes concurrently accessing a resource group acquire that resource group when they join the cluster. There are no priorities among nodes, and no failover or fallback—and therefore no interruptions in service.

To define a concurrent configuration, you must have the Concurrent Resource Manager (CRM) software installed, and the application must support concurrent access.