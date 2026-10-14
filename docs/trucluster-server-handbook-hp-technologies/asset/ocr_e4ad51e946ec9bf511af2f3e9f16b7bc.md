![](bbox=[0.18, 0.12, 0.88, 0.52])

Figure 14-6: CLSM Disk Group Connectivity

# 14.3.2 Cluster-common File Systems Rules and Restrictions

+   - The cluster_root domain cannot be an LSM volume or have an LSM volume as one of its AdvFS volumes prior to V5.1A. In order to bring the cluster_root domain under LSM control, you must use the volmigrate(8) command. See section 14.7.1 for more information.
+   - The cluster_usr and cluster_var domains can be encapsulated into LSM using the volencap(8) command. Alternatively, in V5.1A, you can migrate these domains to LSM volumes using the volmigrate command. See section 14.7 for a discussion on how to decide between migration and encapsulation.
+   - A cluster’s quorum disk cannot be an LSM volume.

# 14.3.3 Member Boot Disk Rules and Restrictions

+   - A member’s boot_partition cannot be an LSM volume.
+   - A member’s cnx partition cannot be an LSM volume.
+   - You cannot encapsulate a member’s swap partitions into LSM prior to V5.1A.
+   For an example on encapsulating a swap partition, see section 14.7.2.4.