The times specified in this table are approximate and depend on the speed of the system, the speed of the storage, and whether or not the command is being executed on the CFS server (for the cluster_root (or /), cluster_usr (or /usr), and cluster_var (or /var) file systems). Please also note that the time required for the Setup Stage can be quite lengthy (beyond 120 minutes) – depending on the number of nodes in your cluster. The reason for this is that copies of all system level files are made on disk.

# 25.4 What to Consider Before Starting a Rolling Upgrade

Disk space requirements are an important issue during any rolling upgrade of a cluster. As a general rule, there should be at least 50 percent free space in the root file system (cluster_root#root); 50 percent free space in the /usr file system (cluster_usr#usr); and 50 percent free space in the /var file system (cluster_var#var). If this is not the case, then either remove unwanted files from these file systems or use the addvol(8) command to temporarily add unused volumes to these file systems.

# WARNING:

When adding additional unused volumes to these system-level file systems, please do not attempt to use unused disk partitions from the quorum disk(s). To do so will cause you a great deal of grief and possible downtime for the entire cluster.

A final word on disk space requirements: it is recommended that there be at least 50 MB free space on each cluster member's boot_partition. If this is not the case, then remove unwanted files from the member's root domain. If you are unable to free up any space in the member's root domain, please do not use the addvol command to add additional space. Instead, see the section in Chapter 22 on how to restore a cluster member's boot disk.

# 25.5 The Rolling Upgrade

Without further ado, let's show you how to perform a rolling upgrade, the stages of which are described in the following flow diagram (see Figure 25-1).

# 25.5.1 Preparation Stage

Preparing the cluster for the rolling upgrade includes several parts. Each of these parts must be completed before you can continue to the next stage of the rolling upgrade.