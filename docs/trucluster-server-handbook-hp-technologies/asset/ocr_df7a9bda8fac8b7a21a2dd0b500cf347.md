communications among all cluster members. This cluster interconnect provides for Internode Communications (via the ICS<sup>12</sup>) between cluster nodes or members. The *TruCluster* Server software creates this virtual private network within the cluster, and this virtual private network exists side-by-side with the physical communications channel provided by the cluster interconnect.

How does this work? For each member, the cluster software creates a virtual network device for the cluster interconnect. In V5.1A, this device is named `ics0`. In V5.0A and V5.1, this device was named `mc0` as only Memory Channel adapter cards were supported as cluster interconnects. In any event, this device has its own IP name and IP address, which are used when establishing the system's membership in the cluster.

The hardware that may be used for the cluster interconnect can be either the Memory Channel (MC) adapter or an Ethernet local area network (LAN) card but not a mix of both.

The Cluster Interconnect is used to provide the following functions within a cluster:

+   - **Health and status messaging between cluster members.** The Connection Manager uses this information to monitor the cluster members and to coordinate membership. For more information on the Connection Manager subsystem, see Chapter 17.
+   - **Distributed lock manager (DLM) locking between cluster members.** This is used to coordinate access to shared resources. For more detailed information on the DLM, please see Chapter 18.
+   - **Accessing file systems between cluster members.** For storage located on a cluster member’s private bus but visible to all members of the cluster, all reads and writes from other cluster members are performed across the cluster interconnect. As Cluster File System uses a client-server model, this also is true for file systems on the shared bus.
+   - **The cluster interconnect, through the ICSnet, includes a full IP stack.** While this usage is not recommended for general-purpose network traffic, nothing can prevent an application from taking advantage of this with the exception of the bandwidth of the interconnect hardware. All non-cluster-related traffic should be kept off the cluster interconnect, and if a private network is needed, one should be added.
+   - **Cluster alias routing.** For more information, please see Chapter 16 on Cluster Alias.

To repeat, as of this writing, there are two approved types of Cluster Interconnect hardware for use with *TruCluster* Server – the Memory Channel (MC) adapter card and the Ethernet Local Area Network (LAN) card<sup>13</sup>. *TruCluster* Server supports up to eight members in a cluster regardless of which type of cluster interconnect is used.

In this section we will discuss how to configure and verify these different cluster interconnects, and why you may want to use one interconnect over another.

> 12  The Internode Communication Subsystem is covered in Chapter 18.
> 13  Ethernet Local Area Network card support as a cluster interconnect began in *TruCluster Server* version 5.1A.