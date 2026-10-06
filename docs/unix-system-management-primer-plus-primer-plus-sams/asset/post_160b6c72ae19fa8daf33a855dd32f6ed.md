
```
/usr/local/apache/libexec/mod_wl.so
/usr/local/apache/logs/access_log
/usr/local/sbin/sshd
```

The find command is very good at locating individual large files, but it does no good if a file system is full of thousands of small files. These files can consume storage just as easily as a few large files. The du command can help by printing the total usage of files under a directory; you can use du at the root of a file system to find where the excessive usage lies.

The -o option will ignore the contents of subdirectories when calculating sizes, and -k will print results in kilobytes. Pipeline the output into sort head, you can print the five directories with the highest usage in /usr/local on a Solaris server:

```bash
bash$ du -ok /usr/local | sort -nr | head -5
73809 /usr/local/apache/logs
52312 /usr/local/lib/gcc-lib/sparc-sun-solaris2.8/2.95.2
12212 /usr/local/bin
9231 /usr/local/lib
4985 /usr/local/BerkeleyDB.3.2/bin
```

# Measuring Disk Activity with iostat

iostat available on all Unix systems and can monitor disk, terminal, and tape performance. Its output can differ widely in different Unix distributions, but for the Solaris version of iostat, it provides some very useful statistics that do not. Some of the most interesting iostat reports are as follows:

| r/s | Read operations per second |
| w/s | Write operations per second |
| kr/s | Kilobytes read per second |
| kw/s | Kilobytes written per second |
| wait | Number of transactions waiting to be served |
| svc_t | Average service time |
| %w | Percent of time there are transactions waiting |
| %b | Percent of time the disk is busy |

Like vmstat, the first output from iostat is a summary of usage from boot time, but each subsequent report represents just the previous interval, which is much more useful. You can use the -x flag to diagnose a Solaris 8 server with poor performance for file systems on local disk, as follows:

# Chapter 11 - PERFORMANCE TUNING AND CAPACITY PLANNING

```bash
bash$ iostat -x extended device statistics
```

| device | r/s | w/s | kr/s | kw/s | wait act | svc_t | %w | %b |
|---|---|---|---|---|---|---|---|---|
| sd0 | 0.0 | 0.1 | 0.0 | 0.5 | 0.0 0.0 | 12.7 | 0 | 0 |
| sd1 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 0.0 | 0 | 0 |
| sd15 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 13.9 | 0 | 0 |

extended device statistics

| device | r/s | w/s | kr/s | kw/s | wait act | svc_t | %w | %b |
|---|---|---|---|---|---|---|---|---|
| sd0 | 73.6 | 124.4 | 1782.0 | 2209.0 | 0.0 1.8 | 8.9 | 0 | 93 |
| sd1 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 0.0 | 0 | 0 |
| sd15 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 0.0 | 0 | 0 |

extended device statistics

| device | r/s | w/s | kr/s | kw/s | wait act | svc_t | %w | %b |
|---|---|---|---|---|---|---|---|---|
| sd0 | 52.0 | 138.8 | 1604.8 | 2179.4 | 0.0 1.5 | 7.8 | 0 | 96 |
| sd1 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 0.0 | 0 | 0 |
| sd15 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 0.0 | 0.0 | 0 | 0 |

This output tells you that device sd0 (in this an internal 18GB SCSI drive) was reading 2MB and writing over 2MB of data per second in each interval, which is a lot of data, but well within the bandwidth limits of SCSI. There were almost 200 read and write operations per second, which is significant activity for a single SCSI drive. The last field, %b, indicates that the disk was busy for over 90% of the time.

All of these statistics demonstrate that the disk is indeed busy, and it should not be surprising that other operations on disk are performing poorly. After running top and ps to find out what was running at the time, this machine's administrator found a tar command that was archiving /var/sad, a large administrative repository on Solaris. The activity subsided after the command was completed.

# Analyzing Historical Disk Performance with sar

In addition to analyzing CPU utilization, you use sar to analyze historical disk performance; the sar -d option makes this possible. The -d option is available only on Solaris; Red Hat's version of sar unfortunately does not include detailed disk statistics. The statistics returned by sar -d are as follows:

| %busy | Percent of the time the device is busy |
|---|---|
| avque | Average transactions in the device's queue |
| r+w/s | Read and write operations per second |
| blks/s | 512-byte blocks transferred per second |
| avwait | Average wait time for the device (ms) |
| aserv | Average service time for requests |

# UNIX SYSTEM MANAGEMENT PRIMER PLUS

The output from sar can be intimidating on servers with a large disk of devices, especially in RAID configurations. The sar -d output contains statistics for each individual physical and logical device, even NFS mounts. Here is some sample output from a quiescent server:

| | device | %busy | avque | rw/s | blks/s | avwait | aserv |
|---|---|---|---|---|---|---|---|
| 00:00:00 | | 0 | 0.0 | 1 | 11 | 0.0 | 2.7 |
| 00:10:00 | sd1 | 0 | 0.0 | 0 | 3 | 0.0 | 2.9 |
| | sd1,a | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd1,b | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd1,c | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd1,d | 0 | 0.0 | 0 | 8 | 0.0 | 2.6 |
| | sd1,e | 0 | 0.0 | 1 | 11 | 0.0 | 0.9 |
| | sd15 | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,a | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,b | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,c | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,d | 0 | 0.0 | 1 | 18 | 0.0 | 2.6 |
| | sd15,e | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| 00:20:00 | sd1 | 0 | 0.0 | 0 | 5 | 0.0 | 2.2 |
| | sd1,a | 0 | 0.0 | 0 | 3 | 0.0 | 2.8 |
| | sd1,b | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd1,c | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd1,d | 0 | 0.0 | 0 | 2 | 0.0 | 1.5 |
| | sd1,e | 0 | 0.0 | 2 | 22 | 0.0 | 16.4 |
| | sd15 | 0 | 0.0 | 0 | 4 | 0.0 | 93.7 |
| | sd15,a | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,b | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,c | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |
| | sd15,d | 0 | 0.0 | 1 | 18 | 0.0 | 2.6 |
| | sd15,e | 0 | 0.0 | 0 | 0 | 0.0 | 0.0 |

The statistic most directly related to disk performance is aserv: The average service time is the time it takes to fulfill a request for disk/O from the operating system. This transaction involves many individual processes, for seeking the physical position of the data on the disk plat to the actual transfer of data. Service times in the hundreds of milliseconds should be considered excessive for modern disks, but disk activity can skew this. A disk with files that are not actively used may have cached data flushed periodically by the kernel. This activity can interfere with user disk/O, causing high service times. You can use vmstat to check file system activity, fpi, fpo, and fpf report system page-ins, page-outs, and page-frees respectively. If file system activity is low (zero or intermittent single-digit values), you can safely ignore the high service times on them. If the file system activity is high, however, you may want to examine the usage of the file systems (and potentially swap space) on the disk and spread the more active files across multiple disks.

# Chapter 11 • PERFORMANCE TUNING AND CAPACITY PLANNING

# Tuning Disk and File System Performance

Almost every task performed by Unix relies on the file system in some way, whether it is executing a program or querying a database. Due to its heavy use of file system data, properly tuned file systems and disks can offer a far greater impact on overall system performance than any amount of CPU tuning. This section discusses some of the most effective methods for tuning disks and file systems, including:

- Using disks with high rotational speeds
- Proper placement of file systems on disk
- Using RAID-0 (striping)
- Optimizing the number of inodes in a file system

# Using Disks with High Rotational Speed

The simplest way to get top disk performance is to use disks with high rotational speed. The rate at which a disk's platter spins is one factor that determines how quickly the heads can read or write data from the platters. Fast disk I/O operations result in higher bandwidth and better performance from your applications.

Using disks with high rotational speeds typically means using disks rated at 10,000 revolutions per second (rps), although this speed does come at a price. 5,400 rps and 7,200 rps may be cheaper (between 20% and 50%), but they may not be suitable for the high disk bandwidth of something like a large database.

# Placing File Systems in Optimal Cylinder

The physical location of a file system on a busy disk has a huge impact on its performance. The discussion of disk architecture earlier in the chapter, you learned that the outer tracks of a disk contain more sectors, and therefore more data, than the inner tracks. Because the rotational speed of a disk remains constant over the entire radius of the disk, more data can be read in the same amount of time from the outer tracks than can from the inner tracks.

![](img/894492738e879267320b8d6f9a044180_326_0.png)

# Position File Systems During Installation

Most Unix programs include an option to position file systems at particular cylinders (sequential sectors) on disk. Think about your file system layout before beginning the installation, as it is very difficult to change after the operating system is installed.

File systems located on these outer cylinders have the highest data transfer rates of all the file systems on the disk. These file systems, therefore, are suitable for data with sequential access patterns, such as database files. File systems on the outer cylinders are also suitable for nonfiction system data such as swap space, where data is accessed in hundreds or thousands of blocks in size.
