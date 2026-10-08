File System A disk partition or logical volume, or in the case of a workstation, this might be the entire disk.

Export To make a file system available for mounting on remote nodes using NFS.

Mount To access a remote file system using NFS.

Mount Point The name of a directory on which the NFS file system is mounted.

Import To mount a remote file system.

Before any data can be shared using NFS, the UNIX system must be set up with exported file systems. The /etc/exports file is often used on UNIX to define what file systems are exported.

This file has in it the directories exported and options such as "ro" for read only and "anon," which handles requests from anonymous users. If "anon" is equal to 65535, then anonymous users are denied access.

The following is an example /etc/exports file in which /opt/app1 is exported to everyone but anonymous users, and /opt/app1 is exported only to the system named system2:

```
/opt/app1 -anon=65534
/opt/app2 -access=system2
```

You may need to run a program such as exportfs -a on your UNIX system if you add a file system to export.