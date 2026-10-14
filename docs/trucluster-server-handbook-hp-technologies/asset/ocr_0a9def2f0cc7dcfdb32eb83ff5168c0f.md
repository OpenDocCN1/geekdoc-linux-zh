Beyond these minimum configuration requirements, a cluster can have its cluster root (/), /usr, and /var over multiple disks and will certainly have additional disks for use in file systems for applications and users.

The availability features at your disposal to make these storage containers highly available in TruCluster Server are at different levels in the I/O hierarchy:

+   - Using LSM and/or Hardware RAID to create highly available volumes
+   - Using multiple paths from different members relying on the TruCluster Server software’s Device Request Dispatcher (DRD) to ensure that if all paths to storage from one member fail, another member can access the device on behalf of the member and transfer any required I/O across the cluster interconnect
+   - Using the Multi-Pathing between HBAs on the same host (intrinsic in Tru64 UNIX)
+   - Implementing redundant fabrics connecting HBAs to storage endpoints

As a general rule, try and make the storage architecture for the cluster as symmetrical as possible for ease of implementation, management, and troubleshooting.

General default rule of thumb:

+   - Have at least two HBAs in each host.
+   - Have at least two fabrics between the hosts and their storage.
+   - Assume the use of hardware RAID Arrays unless it is a small storage cluster and cost is an issue. Evaluate the use of LSM for ease of management or additional features on a case by case basis.

# 3.3.8 Use Hardware RAID and/or LSM?

In today’s computing environments for standalone systems as well as clusters, two methods are available to implement highly available RAID configurations for disk devices – software based RAID and hardware based RAID. In Tru64 UNIX and the TruCluster Server software, these are available as Logical Storage Manager (LSM) and the StorageWorks family of RAID Arrays respectively. The standard question is, “Which of the two solutions should be used?”

# 3.3.8.1    Enterprise Servers with 100GB+ of storage

The original question of software versus hardware RAID is lightly off target for almost all Enterprise solutions utilizing Tru64 UNIX. The reason is that in these cases, the site will already be investing in StorageWorks devices, which come with RAID capability to physically attach and reasonably manage the amount of total physical storage connecting to the cluster. In other words, hardware RAID is almost always a given as available to use, so the real question becomes: “I’ve already paid for hardware RAID capability in the storage hardware. Do I also utilize software RAID in LSM?”