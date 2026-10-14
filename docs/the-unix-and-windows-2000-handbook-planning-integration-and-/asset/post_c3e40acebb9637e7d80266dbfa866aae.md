
ing systems and make it appear as though the files are on the local machine. NFS has become the de facto standard in UNIX operating systems, but it is also available on many other operating systems, including Windows 2000, which is discussed later in the chapter.

## PROCESSES

There are five main processes or daemons that NFS depends on for client and server functions.

- Biod asynchronous block I/O—Performs buffer cache read-ahead and write-behind.
- Lockd file locking.
- Statd status monitoring—Allows recovery of locks in the event of a crash.
- Mountd—Processes that mount requests.
- Nfsd—Services client requests.

Table 8.2 provides a mapping of daemons to client, server, and operating system.

The daemons are started during the boot process. Table 8.3 provides the location of the files for each operating system. All versions start the NFS client daemons. NFS server daemons are started if the /etc/exports file exists, or for Solaris, if the /etc/dfs/dfstab file exists. The exports and dfstab files contain the filesystems that are "exported" for remote access.

| Table 8.2 | Daemon Map | | | | | | | |
|---|---|---|---|---|---|---|---|---|
| Daemon | Client | Server | Solaris | Linux | HPUX | AIX | IRIX | |
| Biod | Yes | N/A | N/A | N/A | | | | |
| Rpciod | Yes | Yes | Yes | | | | | |
| Lockd | Yes | Yes | Yes | Yes | Yes | Yes | Yes | |
| Statd | Yes | Yes | Yes | Yes | Yes | Yes | Yes | |
| Mountd | N/A | Yes | Yes | Yes | Yes | Yes | Yes | |
| Nfsd | N/A | Yes | Yes | Yes | Yes | Yes | Yes | |

The first step in troubleshooting NFS problems is to make sure all the required processes are running. Use the ps command to make sure that the listed processes are running. If some are not starting, check the startup files in Table 8.3 for mistakes.

## NFS SERVER

While building your NFS server, think about whom you want to access your data, that is, what users on which machines will be authorized to read and/or write data onto your NFS shared partitions. Security should be a main concern when implementing NFS. Since UNIX shares files based on UIDs, it is very easy for an unauthorized user to masquerade as one of your users, especially if you do not restrict what systems can connect to your NFS server. This can also happen by accident if you allow remote systems to mount your partitions, or you mount remote partitions on your local systems.

## exportfs/share

To allow client systems to use NFS to connect to a server's partitions, you need a process for defining parameters to allow clients to connect to your NFS server. This process is called exporting. When you export a partition, you define the following:

| Table 8.3 Startup Files |
|---|---|
| Operating System | File Location |
| AIX | /etc/rc.nfs |
| HPUX | /sbin/init.d/nfs.client |
|  | /sbin/init.d/nfs.server |
|  | /etc/rc.config.d/nfsconf |
| IRIX | /etc/init.d/network |
|  | /etc/config/network |
| Linux | /etc/rc.d/init.d/nfs |
|  | /etc/sysconfig/network |
| Solaris | /etc/init.d/nfs.client |
|  | /etc/init.d/nfs.server |

- Which system or group of systems is allowed to access, or mount, the defined filesystem.
- Whether or not the filesystem should be accessed read/write or read-only. Read/write states that remote users can read and modify any files for which they have permission. Read-only prevents files on the partition from being written to when mounted remotely.
- What level of trust you give the root account on other systems.

The commands `exportfs` (BSD) and `share` (SysV) are used to export filesystems. A typical export command can look like:

```
mars# exportfs -o rw=earth:saturn,root=earth /users/data
```

For this example, the NFS server mars exports the filesystem `/users/data` read/write to the systems earth and saturn. The `-o` defines a list of options for that given filesystem. For multiple `-o` options, a comma (`,`) is used to separate distinct parameters, so we can see with the `rw` and `root` options. In this example, the `rw` option defines that saturn and earth are allowed to NFS mount `/users/data` read/write.

The `root` option in this example defines that the root user on the machine earth can perform root functions on the shared filesystem as if the root user on earth were the root user on mars.

```
mars# exportfs -u /users/data
```

> You should be very careful when allowing NFS client systems root access, and when the NFS client systems have root access on the client system full authority to add, remove, and change data on the filesystem. This can lead to security problems if you allow the creation of SUID (setuid) scripts.

The `exportfs` command can also be used to remove, or unexport, a filesystem by using the `-u` option. This will unexport the filesystem, removing all rights for remote systems to access the data store there. This command can be used while NFS operations are underway, so be careful if you use this option when the system is operational. The `-u` option should only be used on idle or test systems, or for debugging NFS problems. For SysV systems, the `share` command performs the function of exporting filesystems. An equivalent `share` command to our `exportfs` example would be:

```
mars# share -F NFS -o rw=earth:saturn,root=earth -d "User Data" /users/data
```

As you can see, the differences are small, except for the introduction of the `-F` and `-d` options.

The `-F` option defines the filesystem type being exported. The `-d` option allows you to add an identifier to the export. The `-d` is optional, and can be
