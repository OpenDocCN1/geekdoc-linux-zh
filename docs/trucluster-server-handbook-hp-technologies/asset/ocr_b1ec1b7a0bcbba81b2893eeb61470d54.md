cluster instead of trying to form a cluster.

The boot process for a system joining a cluster is pretty much the same as it is for systems forming a cluster except that once the system becomes aware that there is a cluster, it sends a join request to the existing cluster members as was shown in Figure 17-9.

Once the join request is sent, one of the cluster members will temporarily take charge of responding to this request by becoming the "Cluster Coordinator" for the cluster. The job of the coordinator is as follows:

+   - Determine whether or not the node requesting to join would cause the cluster to lose quorum. If this is true, then the node cannot be allowed to join the cluster.

```
CNX MGR: join request rejected: adding node would cause cluster to lose quorum
..
CNX MGR: halting join rejected 20 times
```

Allocate a CSID for the node and proceed to describe the requestor to each cluster member and describe each cluster member to the requestor (see Figure 17-10). Since each member should already have a CSB allocated for the requestor and the requestor should already have a CSB for each cluster member, this step really involves verification of the CSB and passing along the CSID.

Describe the cluster to the new node (see Figure 17-10). This involves passing the requestor the current cluster's information including the incarnation number, the founder, CSIDs of every member, etc.

Calculate Quorum based on the requestor's addition to the cluster.

Prepare a connectivity matrix (or topology).

![](bbox=[0.18, 0.78, 0.85, 0.94])

# Figure 17-9: Send a Join Request