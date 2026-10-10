+   * The System V Release 4 file system layout described through-
+   out this book is implemented. This file system layout is condu-
+   cive to extensive file sharing, which is used in NFS Diskless.

+   * Read-only NFS mounts, such as **/usr** and **/opt/**<i>application</i>**, are supported.

+   * Distributed HP-UX functionality, such as context-dependent files, has been removed.

+   * Servers can be both Series 700 and Series 800 units.

+   * The physical link doesn't matter, so servers can use many interfaces such as IEEE 802.3 and FDDI. A server can also assign some diskless systems to one network card, and other systems to other network cards.

+   * Diskless systems can boot across a gateway, thereby allowing subnets to be used.

+   * Booting is implemented with standard Boot Protocol (BOOTP) and Trivial File Transfer Protocol (TFTP) proto- cols.

+   * Clients can swap to a local disk or swap using NFS to a remote disk.

Many additional features of NFS Diskless exist; however, since our focus is on management, let's take a closer look at this. Using SAM, all tasks related to NFS Diskless administration can be performed. This means that you have a single point of administration for the cluster. You can manage cluster-wide resources, such as printers and file systems, that can be managed from any node in the cluster. You can defer some operations until a later point in time if a node is unreachable. And, of course, you can add and delete clients in SAM.

Using SAM, you get a single point of administration for several NFS Diskless systems. This means that performing an operation in SAM affects all systems in the cluster. The single point of administration areas in SAM include: