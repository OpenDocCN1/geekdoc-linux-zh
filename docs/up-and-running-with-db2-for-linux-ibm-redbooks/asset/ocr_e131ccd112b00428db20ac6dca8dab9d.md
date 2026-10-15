# Database clustering architectures

There are two primary database clustering architectures: shared-disk and shared-nothing. Shared-disk is used by Oracle RAC. DB2 for Linux employs shared-nothing.

![](bbox=[0.27, 0.22, 0.88, 0.65])

Figure 1-4 Shared disk architecture

# Shared-disk

In a shared-disk environment, each database node has its own processors but shares the disks with other nodes. Therefore all the processors can access all the disks in the cluster. This introduces additional overhead for coordinating resources and locks between nodes. For example, if Node 1 wants to access data on a certain disk that has been locked for update by another node in the cluster, Node 1 must wait for other nodes to complete their operations. While this works well when there are few nodes in the cluster (for example, mainframe environments), the overhead for distributed lock management and cache coherency issues can severely limit scalability and introduce performance degradation for four or more nodes, making it impractical to exploit economies of large clusters on Linux. Furthermore, this approach involves specialized hardware and software for shared disk and cache management, making it much more expensive than shared-nothing.

# Shared-nothing

As the name implies, partitions (nodes) in a shared-nothing environment do not share processors, memory, or disks with partitions on other machines. Each