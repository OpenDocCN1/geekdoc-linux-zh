Later that same year, Compaq quietly released TruCluster Server version 5.0 as a limited release to a select group of customers. TruCluster Server version 5.0 was the very first version of TruCluster Server to have SSI systems cluster features. From an UNIX perspective, this version of TruCluster Server was no longer evolutionary but revolutionary! It was revolutionary to be able to write a file from one server to a common cluster file system and then be able to read this same file almost instantaneously from another server.

2000 signaled the release of TruCluster Server version 5.0A and later TruCluster Server version 5.1 to customers. This was the first general release of TruCluster Server software that had SSI systems cluster features. As of the release of TruCluster Server version 5.0A, any new version of TruCluster Server software will release with any new version of Tru64 UNIX.

Tru64 UNIX version 5.1A and TruCluster Server version 5.1A was released in the fall of 2001.

That about brings us to the present (Summer, 2002). As of this writing, we expect the release of Tru64 UNIX version 5.1B and TruCluster Server version 5.1B in the fall of 2002.

# 1.4 What is TruCluster Server?

Now that we know what a cluster is, what is TruCluster Server? TruCluster Server is an amalgam of Tru64 UNIX software, storage devices, cluster interconnects, and two or more AlphaServer systems that operate together as a single virtual system. Each cluster member can share resources, storage, and cluster-wide file systems under a single systems management domain.

TruCluster Server versions 5.0A, 5.1, and 5.1A provide the following features:

+   - Cluster-wide namespace.
+   - Cluster-wide access to disk and tape storage.
+   - Cluster-wide Logical Storage Manager (LSM).
+   - Connection Manager⁶.
+   - Cluster application availability (CAA).
+   - Cluster alias.
+   - Highly available NFS server using cluster alias.

+   - Cluster Communications Interconnect.
+   - Distributed Lock Manager (DLM)⁵.
+   - Single-systems management.
+   - Single Security Domain.
+   - Rolling Upgrade/Patch.
+   - Expanded Process IDs (PIDs).

Again, with TruCluster Server, you are creating real single-systems image systems clusters from individual Tru64 UNIX servers. We will provide a more in-depth overview of Tru64 UNIX and TruCluster Server in Chapter 2.

> ⁵ Distributed Lock Manager is discussed in detail in Chapter 18.

> ⁶ Connection Manager is discussed in detail in Chapter 17.