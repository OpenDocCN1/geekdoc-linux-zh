# 13.7.1 Concurrent Direct I/O (CDIO)

Concurrent Direct I/O was introduced in V5.1⁶ and enables members with direct access to the device where the file lives not only to bypass the UBC but also bypass the CFS server for I/O not related to log updates and metadata operations (file size changes, etc.). Those writes that allocate storage will continue to be sent to the CFS server.

It is also worth noting that CDIO is truly concurrent – all members with direct physical connectivity to the shared storage devices can read and write to the file systems simultaneously.

Figure 13-3 illustrates the I/O flow using CDIO.

The cluster keeps track of Concurrent Direct I/O operations performed on the cluster, and these statistics can be retrieved using the cfsstat command with the “direction” option.

For additional information on Direct I/O, see the TruCluster Server Cluster Administration Guide and the open(2) reference page.

# 13.8 Direct Access Cached Reads

In V5.1A, when a cluster member performs a read from a file greater than or equal to 64KB and that file is on an AdvFS file system on a device physically connected to that member, then the read will be performed directly. Metadata operations and log updates will continue to go through the CFS server; writes will also go through the CFS server unless the file is also opened O_DIRECTIO. Figure 13-4 illustrates the I/O flow within V5.1A. By performing reads directly, traffic across the cluster interconnect can be reduced.

![](bbox=[0.088, 0.57, 0.916, 0.789])

Figure 13-3: Concurrent Direct I/O

> ⁶ For the TruCluster Server product. Tru64 UNIX added support for CDIO in the base operating system in V5.0.