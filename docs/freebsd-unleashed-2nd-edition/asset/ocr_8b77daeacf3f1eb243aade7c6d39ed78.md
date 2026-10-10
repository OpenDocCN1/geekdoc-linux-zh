# TABLE 8.2 Continued

| Filesystem | Name |
|---|---|
| CD9660 | ISO 9660 (CD-ROM) Filesystem |
| PROCS | Process Filesystem |

There is also support for the filesystems shown in Table 8.3, but they need to be compiled into a custom kernel in order to work (see “Compiling and Installing the Custom Kernel,” in Chapter 16).

# TABLE 8.3 Additional Available Filesystems

| Filesystem | Name |
|---|---|
| FDSC | File Descriptor Filesystem |
| KERNFS | Kernel Filesystem |
| NTFS | NT Filesystem |
| NULLFS | NULL Filesystem |
| NWFS | NetWare Filesystem |
| PORTAL | Portal Filesystem |
| SMBFS | SMB/CIFS Filesystem (Windows) |
| UMAPFS | UID Map Filesystem |
| UNION | Union Filesystem |
| CODA | CODA Filesystem |
| EXT2FS | Ext2 Filesystem (Linux) |

Some of these latter filesystems are more stable than others. As you saw earlier, union filesystems are available as an option, but they are only partially in a working state (and can damage your system). Therefore, it is not recommended that you use them unless absolutely necessary. EXT2FS and NTFS support is also given a caveat about completeness and stability. Filesystems that are not built in to the GENERIC kernel, in general, are not included for a reason.

The ideal circumstance for a filesystem type that isn’t part of the existing kernel is to be available as a kernel module in /modules, as many of the filesystems listed in the preceding tables are. If the filesystem is available as a kernel module, it will be automatically loaded when you try to mount the filesystem. At the time of this writing, these available modules include CODA, PORTAL, NWFS, NULL, NTFS, UNION, and some others that are already compiled into the GENERIC kernel and are provided in /modules for compatibility.

If you’re mounting a filesystem (MSDOSFS, for example) that is supported in the default kernel, or if you decide to accept the risks and plunge ahead with mounting a filesystem that isn’t initially built in, you’ll find that FreeBSD does provide some handy tools for doing the actual mounting. The following tools are available in /sbin (although their names may vary according to your version of FreeBSD):