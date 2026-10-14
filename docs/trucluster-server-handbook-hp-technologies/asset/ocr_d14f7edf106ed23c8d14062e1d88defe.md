![](bbox=[0.22, 0.14, 0.88, 0.38])

# Figure 17-6: Describe Nodes

+   - Allocate a CSID for each node that has been selected as a potential member.
+   - Describe the nodes to each other (see Figure 17-6) and prepare a connectivity matrix (or topology).

Think of the matrix as a topology bitmap that shows node connectivity. The goal is to determine the best-connected (or fully connected) cluster. This is done to prevent a cluster partition.

If every member is communicating with every other member, then the matrix will be identical for all members. This is the normal operating environment.

When there is a communication problem, this matrix may not be the same. The CNX will determine the best-connected cluster from the topology bitmap. Systems not communicating will hang or panic. The systems in the matrix will continue as the cluster.

Figure 17-7 shows an example of a connectivity matrix with a communication problem. Every member can communicate with the quorum disk, but member3 and member5 cannot communicate with other members. Since the CNX will detect this problem, member3 and member5 will not be allowed to join the cluster.

+   - Determine the best-connected cluster from the connectivity matrix and clear nodes from the

![](bbox=[0.22, 0.78, 0.85, 0.97])

# Figure 17-7: Connectivity Matrix (aka Topology Bitmap)