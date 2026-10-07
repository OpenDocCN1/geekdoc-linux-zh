memory, and as we will see, file caking shares the same paging dynamics as the rest of the memory system.

# 15.1.2 Block Buffer Cache

The old buffer cache is used in Solaris for caching of inodes and file metadata and is now also dynamically sized. In old versions of Unix, the buffer cache was fixed in size by the nbuf kernel parameter, which specified the number of 512-byte buffers. We allow the buffer cache to grow by nbuf, as needed, until it reaches a ceiling specified by the bufwm kernel parameter. By default, the buffer cache is allowed to grow until it uses 2 percent of physical memory. We can look at the upper limit for the buffer cache by using the sysdef command.

```
# sysdef
* Tunable Parameters
7758024  maximum memory allowed in buffer cache (bufwm)
5930    maximum number of processes (v_v proc)
99      maximum global priority in sys class (MAXCLSYSPRPRI)
5925    maximum processes per user id (v_v_maxup)
30      auto update in seconds (HAUTOUP)
25      page stealing low water mark (GPSLO)
25      fsflush run rate (FSFLUSH)
25      minimum resident memory for avoiding deadlock (MINARMMEM)
25      minimum swappable memory for avoiding deadlock (MINASMEM)
```

Now that we only keep inode and metadata in the buffer cache, we don't need a large buffer. In fact, we only need 300 bytes per inode and about 2 gigabytes of files that we expect to be accessed concurrently (note that this rule of thumb is for UFS file systems).

For example, if we have a database system with 100 files totaling 100 gigabytes of storage space and we estimate that we will access only 50 gigabytes of those at the same time, then at most we would need 100 × 300 bytes = 30 kilobytes for the inodes, and about 50 / 2 * 1 megabyte = 25 megabytes for the metadata (direct and indirect blocks). On a system with 5 gigabytes of physical memory, the defaults for bufwm would provide us with a bufwm of 102 megabytes, which is more than sufficient for the buffer cache. If we are really memory misers, we could limit bufwm to 30 megabytes (specified in kilobytes) by setting the bufwm parameter in the /etc/system file. To set bufwm smaller for this example, we would put the following line into the /etc/system file.

+   * Limit size of bufwm

```
set bufwm=30000
```

You can monitor the buffer cache hit statistics using sar -b. The statistics for the buffer cache show the number of logical reads and writes into the buffer cache,