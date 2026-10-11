Disable subtree checking: **no_subtree_check** (page 740)

Sync write operations on request: **sync** (page 740)

Force sync of write operations immediately: **no_wdelay** (page 740)

Hide filesystems beneath: **nohide** (page 740)

Export only if mounted: **mountpoint** (page 740)

+   User Access tab Treat remote root user as local root: **no_root_squash** (page 741)
+   Treat all client users as anonymous users: **all_squash** (page 742)
+   Local user ID for anonymous users: **anounid** (page 742)
+   Local group ID for anonymous users: **anogid** (page 742)

After making the changes you want, click **OK** to close the Add/Edit NFS Share window and click **OK** again to close the NFS Server Configuration window. There is no need to restart any daemons.

# # EXPORTING A DIRECTORY HIERARCHY

Exporting a directory hierarchy makes the directory hierarchy *available for mounting* by a client on the network. “Exported” does not mean “mounted”: When a directory hierarchy is exported, it is placed in the list of directory hierarchies that can be mounted by other systems. An exported directory hierarchy may be mounted (or not) at any given time. A server holds three lists of exported directory hierarchies:

+   - /etc/exports—Access control list for exported directory hierarchies (discussed in the next section). The system administrator can modify this file by editing it or by running **system-config-nfs**.

+   - /var/lib/nfs/xtab—Access control list for exported directory hierarchies. Initialized from /etc/exports when the system is brought up. Read by **mountd** when a client asks to mount a directory hierarchy. Modified by **exportfs** (page 742) as directory hierarchies are mounted and unmounted by NFS.

+   - Kernel's export table—List of active exported directory hierarchies. The kernel obtains this information from /var/lib/nfs/xtab. You can display this table by giving the command **cat /proc/fs/nfs/exports**.

**Exporting symbolic links and device files**

> tip When you export a directory hierarchy that contains a symbolic link, make sure the file the link points to is available on the client (remote) system. If this file does not exist on a client system, you must export and mount it along with the exported link. Otherwise, the link will not point to the file it points to on the server.

A device file refers to a Linux kernel interface. When you export a device file, you export that interface. If the client system does not have the same type of device, the exported device will not work. From a client, you can use **mount**'s **no/dev** option (page 731) to prevent device files on mounted directory hierarchies from being used as devices.