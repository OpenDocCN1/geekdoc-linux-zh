
# clubase subsystem attributes

| Attribute | Description |
|---|---|
| `cluster_expected_votes` | This attribute contains the maximum number of votes that the cluster expects to have if every voting member is up. Note that this value also includes the vote for the quorum disk if it is configured and is assigned a vote. The `cluster_expected_votes` attribute value should be the same on **all** cluster members. |
| `cluster_interconnect` | This attribute contains the cluster interconnect type. As of this writing, this can be: 
- `mct` — Memory Channel Transport
- `tcp` — LAN Interconnect |
| `cluster_name` | The `cluster_name` attribute contains the name of the cluster. All members must have the same cluster name. The attribute is used as the name of the Default Cluster Alias as well. For more information on cluster aliasing, see Chapter 16. |
| `cluster_node_inter_name` | This attribute contains the node name for the virtual cluster interconnect (`ics0`). |
| `cluster_node_name` | This attribute contains the node name of the cluster member. |
| `cluster_node_votes` | This attribute contains the number of votes this member will contribute toward quorum. As of this writing, this value can be 0 or 1. |
| `cluster_qdisk_major, cluster_qdisk_minor` | This is the major and minor number of the quorum disk’s “h” partition. This partition is the cnx partition and is discussed in section 17.4. |
| `cluster_qdisk_votes` | This attribute contains the number of votes that the quorum disk will contribute toward quorum. As of this writing, this value can be 0 or 1. |
| `cluster_seqdisk_major, cluster_seqdisk_minor` | This is the major and minor number of the member boot disk’s “h” partition. This partition is the cnx partition and is discussed in section 17.4. |

## Table 17-3: The Clubase subsystem attributes

- Quiesce the cluster.
- Drain any outstanding I/O in process.
- Continue to access the cnx partition on the cluster member and quorum disks.
- Attempt to reform the cluster from surviving members.

Note: The cluster may continue to function for a period of time after quorum is lost; however, all application I/O directed at cluster storage will be suspended to preserve data integrity.

The cluster will appear hung, but it’s not hung. If you check the console, you will see output similar to the following:

```
CNX MGR: quorum lost, suspending cluster operations.
```

The Connection Manager continues to function, attempting to accumulate enough votes to regain quorum so that the cluster can resume operation.

```
CNX MGR: quorum (re) gained, (re) starting cluster operations.
```

Every system that is added to the cluster can be a voting member or a non-voting member. Furthermore, a quorum disk can be added to the cluster to increase availability and act as a tiebreaker in the event of a cluster partition. Currently, a system can have one vote or zero votes (the same is true for the quorum disk).

Every member (or potential member) determines what quorum is based on the "Quorum Algorithm."

### 17.3.1 The Quorum Algorithm

The CNX calculates the number of votes needed for quorum based on the number of votes it expects to see in the cluster if all voting members (and the quorum disk if configured and assigned a vote) are up.

The first thing that the CNX needs to do is determine the maximum number of booting nodes that are fully connected (meaning that each node can communicate with every other node).

Secondly, the CNX will determine the Cluster's Expected Votes (CEV) from the set of "fully connected" nodes.

The CEV is defined as the maximum number of votes from the following:

- The previous CEV.
  The previous CEV only applies if the cluster is going through a membership transition and not when the cluster is first forming (as the CEV from a previous cluster incarnation is not stored).

> 4 For more information on the quorum disk, see section 17.8.3.

- The highest member-specific cluster_expected_votes attribute value.
  This is the clubase:cluster_expected_votes attributes from each member’s sysconfigtab file in the /.local../boot_partition/etc directory.
  Normally this value should be the same for all members.

- The sum of node votes (cluster_node_votes) and quorum disk votes (cluster_qdisk_votes).
  The cluster_node_votes and cluster_qdisk_votes are located in the clubase subsystem. The specific values are defined in each member’s sysconfigtab file in the /.local../boot_partition/etc directory.

Finally, the CNX will determine the number of votes required to reach quorum.

The quorum votes (QV) value is calculated as follows:

```
QV = round_down ((CEV + 2)/2)
```

Here’s another way of looking at this, especially if you’re a programmer:

```
QV = (CEV >> 1) + 1
```

For example, in a three-member cluster where each member has one vote, every member should have a cluster_expected_votes value of 3.

If the CEV is 3:

```
QV = (3 + 2) / 2
QV = 5 / 2
QV = 2.5
QV = 2
```

So in order to form a cluster, at least two systems must be booted.

Here’s a little one line Perl script to calculate quorum.

```
# perl -e 'printf("%d\n", (CEV >> 1) + 1);'
```

```
# perl -a 'printf("%d\n", (3 >> 1) + 1);'
2
```
