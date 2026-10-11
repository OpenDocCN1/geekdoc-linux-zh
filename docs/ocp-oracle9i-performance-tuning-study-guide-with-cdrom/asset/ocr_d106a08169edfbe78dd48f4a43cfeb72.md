multi-CPU servers, consideration should be given to the impact that changing memory or device configurations will have on CPU utilization. Oracle is also a very “CPU-aware” product. This means that several Oracle Server configuration parameters change dynamically when CPUs are added or removed from the server.

# Disk (I/O)

The more Oracle Server activity that occurs in memory, the lower the physical I/O will be. However, placing too many demands on the available memory by oversizing Oracle’s memory structures can cause undesirable additional I/O in the form of operating system paging and swapping. Modern disk-caching hardware and software also complicate database I/O tuning, since I/O activity on these systems may result in reads from the disk controller’s cache and not directly from disk.

# Memory

The availability of memory for Oracle’s memory structures is key to good performance. Managing that memory is important so that it is used to maximum benefit without wasting any that could be better used by other server processes. Oracle offers several memory tuning options that help you make the most efficient use of the available memory.

> Optional Oracle9i features designed to improve the database’s functionality in one area, may at the same time hinder its performance in others if those features are not configured properly. For example, Oracle9i offers several new high availability features that can maximize the database’s uptime and recoverability, but may also occasionally introduce additional performance tuning considerations in the areas of resource contention and server resource tuning.

# Common Tuning Problem Areas

While examining your system for possible performance improvement, it is important to first examine those areas that are the most likely causes of poor