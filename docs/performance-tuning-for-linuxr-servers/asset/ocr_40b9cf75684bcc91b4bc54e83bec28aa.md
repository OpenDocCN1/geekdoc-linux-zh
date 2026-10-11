from SGI. These file systems provide concurrent read/write access to files located on a shared disk file system.

Communication between HPC nodes often makes use of message-passing libraries such as MPI or PVM. These libraries are based on common standards and allow the easy porting of parallel applications to different cluster environments.

# High-Availability Clusters

Some workloads are more sensitive to failurethat is, a failure of the workload can have expensive repercussions for a business. Sample workloads include customer relationship management (CRM), inventory control, messaging servers, databases, and file and print servers. Availability is critical to these workloads; availability requirements are often described as the five-nines of availability (99.999%). Providing that level of availability allows about 5 minutes of outage per year.

One method of preventing downtime caused by failure of a system running these critical workloads is the use of high-availability (HA) clusters. An HA cluster consists minimally of two independent computers with a “heartbeat” monitoring program that monitors the health of the other node(s) in the cluster. If one node fails, another node detects the failure and automatically picks up the work of the failed node.

It is common for HA clusters to be built from larger computers (four or more processors). Typical HA clusters have only a handful of nodes. Ideally, there is enough excess capacity on the nodes in a cluster to absorb the workload from one failed node. Thus, in a two-node cluster, each node should normally run at 50% capacity so that there is headroom to absorb the load of the other node. In a four-node cluster, each node could run at 75% capacity and there would be sufficient excess capacity to absorb the workload of a failed node. Thus, it is more efficient to have larger node counts. However, the efficiency of large node centers comes at the cost of additional complexity and administrative overhead.

For HA clusters, all nodes need to have access to the data being used by the application, which is normally a database. Use of Fibre Channel adapters and switches is usually necessary to connect more than a few nodes to a common disk storage array. This can often be the limiting factor on the number of nodes in an HA cluster.

Within the Linux community is an active group focused on high-availability clusters (see [http://linux-ha.org](http://linux-ha.org)). This site provides details on the design and configuration of Linux high-availability clusters and provides links to papers that describe various implementations and deployments of Linux HA clusters.

Clusters are a way of consolidating resources. In the following section, see what consolidation means in terms of the mainframe.