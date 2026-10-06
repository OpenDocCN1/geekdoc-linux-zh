# NFS: Network Filesystem

The NFS (Network Filesystem, see page 391) protocol, developed by Sun Microsystems, allows you to share local files with remote machines and to access files from the local machine. Under NFS it is difficult to distinguish a remote file from a local one. NFS is a facto standard and supports heterogeneous environments.³32

The physical location of a file is irrelevant to a user under NFS. Traditionally one copy of an application program is stored on each machine. In order to upgrade the program, you need to upgrade it on each of the machines. With NFS you can store one copy of a program on one machine and give other users access to it over the network. This scenario uses storage more efficiently by reducing the number of locations that same data needs to be stored. In addition to efficiency, NFS gives users on the network access to the same data (not just application programs), improving data consistency and reliability. By consolidating data, NFS reduces system administration and overhead and improves security.

Before you use NFS, make sure that the necessary daemons are running:

```
# service nfs status
```

```
...
```

```
# /etc/rc.d/init.d/nfs statuspc.mount(pid 15795) is running...
nfsid (pid 15813 15812 15811 15810 15808 15807 15806) is running...
rpc.quotad (pid 15784) is running...
```

When NFS is not running, you will see messages telling you that the daemons are stopped. To start the daemons give the command service nfs start. If you have no output, perhaps no entries are in /etc/exports.

# exports: Stores Permissions to Mount Local Filesystems

The /etc/exports file controls which remote systems can access directories. You can edit this file directly. The following simple exports file gives bravo read and write access to all the files in /home and gives kudos access to /home/alex. In each case, access is implicitly granted for all subdirectories. Recent versions of exports (following) have changed the default commit process to conform to the NFS protocol³³³ and to complain when you do not sync or async.

+   32. NFS runs on UNIX

+   33. In versions higher than 1.0.0, sync is the default.