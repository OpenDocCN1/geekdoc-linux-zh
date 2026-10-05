# SAN networks

+   Utilization efficiency is increased because every client can have as much storage as it needs. Although space allocations for virtual disks are fixed, they are not limited to the standard sizes of physical hard disks. In addition, virtual disk blocks that the client never needs were actually stored on the server.

+   At the same time, a SAN makes storage infinitely more flexible and trivial to reconfigure. A "hard disk upgrade" can now be performed in a command or two from an administrator's terminal window.

+   Duplicate block detection techniques can reduce the cost of storing files that are the same on many machines.

+   Backup strategy for the enterprise can be unified through the use of shadow copies of stores on the SAN server. In some cases, every client gets access to advanced snapshot facilities as those found on logical volume managers, regardless of its operating system or the file's.

Performance is always of interest to system administrators, but it's hard to make general statements about the effect of a SAN on a server's I/O performance with knowing more about the specific implementation. Networks introduce latency costs and bandwidth retries that local disks do not. Even with advanced switching hardware, networks are semi-shared resources that can be subject to bandwidth contention among clients. On the positive side, large SAN servers came to the gills with memory and SSD caches. They use premium components and spread their physical I/O across many disks. In general, a properly implemented SAN is significantly faster than local storage.

That kind of setup isn't cheap, however. This is a domain of specialized, enterprise-class hardware, so to get that $80 hard disk from Fry's out of your mind from the start. Some major players in the SAN space are EMC, NetApp, HP, IBM, and perhaps surprisingly, Dell.

# SAN networks

Because network concerns are a major determinant of SAN performance, serious installations have traditionally relied on Fibre Channel networks for their infrastructure. Mainstream Fibre Channel speeds are typically 4 or 8 Gb/s, as opposed to 1 Gb/s speed of typical Ethernet.

Ethernet is rapidly gaining ground, however. There are several reasons for this, the two most important being the growing availability of inexpensive 10 Gb/s Ethnets and the increasing prevalence of virtualized servers; virtualization systems generally have better support for Ethernet than Fibre Channel. In course, it's also helpful that Ethernet-based systems don't require the installation of an expensive secondary physical network infrastructure.

![](bbox=[0.945, 0.436, 0.995, 0.545])