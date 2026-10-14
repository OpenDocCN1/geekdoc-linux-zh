several interconnected computers. Each interconnected computer has one or more processors, I/O capabilities, an operating-system kernel, and memory."1

What differentiates clustering from distributed computing is that with a cluster, a number of similar computers work together and form a cadre. This unifying relationship becomes the basis for providing the primary themes in clustering: increased application availability (or high availability), load balancing for scalability and performance, and ease of manageability.

This book provides a detailed description of how to create real, single-system image clusters from individual UNIX servers using Compaq’s Tru64 UNIX operating system and TruCluster Server software.

# 1.2 Overview of UNIX Cluster Types

There are three basic types of UNIX clusters: the Failover Cluster, the Single System Image (SSI) Application Cluster, and the Single Systems Image (SSI) Systems Cluster. There would be four different types of UNIX clusters if you count Linux or Beowulf Clustering, but the discussion in this book is limited to the first three types listed above.

# 1.2.1 Failover Cluster

The Failover Cluster is currently the most common form of UNIX clustering. In its many incarnations and flavors, it is available from most major computer hardware and system software vendors. While the main purpose of the failover cluster is high availability of applications, it is generally considered the most difficult to configure and manage due to the customizations required of application failover scripts.

In looking at a failover cluster from a hardware perspective, it usually has some kind of interconnect between cluster nodes, access to a common disk or storage subsystem from each node, and a network failover capability. Failover of applications is accomplished through scripts that start and stop the applications during cluster node failure and recovery.

Even though each node of a failover cluster is closely coupled through hardware, for the most part it is considered "shared-nothing" from a systems standpoint. Each cluster node must have its own copy of the operating system, and there can be no simultaneous access of disks or of memory between cluster nodes.

The difficulty in developing good, robust application failover scripts usually has to do with the timing and the synchronization for startup or failover of applications versus the common disk subsystem accessibility.