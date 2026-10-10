To show the free space for all locally mounted drivers:

```
`[root@ford /root]# df -l`
```

To show the free space in a human-readable format, for the file system in which your current working directory is located:

```
`[root@ford /root]# df -h .`
```

To show the free space in a human-readable format, for the file system on which /tmp is located:

```
`[root@ford /root]# df -h /tmp`
```

# Synchronize Disks: sync

Like most other modern operating systems, Linux maintains a disk cache to improve efficiency. The drawback, of course, is that not everything you want written to disk will have been written to disk at any given moment.

To schedule the disk cache to be written out to disk, you use the `sync` command. If `sync` detects that writing the cache out to disk has already been scheduled, the kernel is instructed to immediately flush the cache. This command takes no command-line parameters.

To ensure the disk cache has been flushed:

```
`[root@ford /root]# sync ; sync`
```

# PROCESS MANIPULATION

Under Linux (and UNIX in general), each running program comprises at least one process. From the operating system’s standpoint, each process is independent of the others. Unless it specifically asks to share resources with other processes, a process is confined to the memory and CPU allocation assigned to it. Processes that overstep their memory allocation (which could potentially corrupt another running program and make the system unstable) are immediately killed. This method of handling processes has been a major contributor to the stability of UNIX systems: User applications cannot corrupt other user programs or the operating system.

This section describes the tools used to list and manipulate processes. They are very important elements of a system administrator’s daily work.

# List Processes: ps

The `ps` command lists all the processes in a system, their state, size, name, owner, CPU time, wall clock time, and much more. There are many command-line parameters available, and the ones most often used are described in Table 6-5.