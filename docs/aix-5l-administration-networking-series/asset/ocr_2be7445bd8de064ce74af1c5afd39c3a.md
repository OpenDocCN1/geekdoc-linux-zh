manager can be starved for CPU time. Misbehaving applications running at a priority higher than the cluster manager can also cause this problem.

Setting tuning parameters correctly helps avoid such performance problems. It is recommended to adjust the AIX high and low watermarks for I/O pacing and the AIX *syncd* frequency rate first. Then, if further tuning proves necessary, you can adjust certain HACMP network tuning parameters such as failure detection rate and grace period for each type of network. See the HACMP manuals for complete information on these tasks.

# # CREATING A CLUSTER: DEFINING AND CONFIGURING RESOURCES

After configuring the cluster topology, you configure the highly available resources. Planning for and configuring resources takes careful thought and implementation.

The many resource types and their individual configuration instructions are discussed in detail in the HACMP manuals.

# ## SYNCHRONIZING THE CLUSTER

Synchronizing the cluster sends the entire cluster information contained on the local node to the remote nodes. You must synchronize cluster *topology* after defining or changing the cluster’s node, disk, network, or adapter configuration. You must synchronize cluster *resources* after defining or changing the cluster’s resource configuration.

During synchronization, a cluster verification utility runs; *clverify* checks that the configuration is valid and presents error or warning messages for any invalid or missing configuration information. This verification ensures that the AIX environment can support the cluster configuration, and that all nodes agree on the cluster topology, the network configuration, and the ownership and takeover of HACMP resources. You can add your own custom verification checks in addition to the ones HACMP automatically runs. When you make a change, or when you are first configuring HACMP, always work from the same node, and do the synchronization from the same node. If you make a change on one node and do the synchronization from a different node you overwrite the changes that you just made.

# ## TRADITIONAL IP ADDRESS TAKEOVER AND IPAT VIA IP ALIASING

Traditional IP address takeover (IPAT), in all HACMP Classic versions and in HACMP/ES prior to version 4.5, moves the IP address of an adapter on one node