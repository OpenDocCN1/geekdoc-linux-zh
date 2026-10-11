
## XFS File Layout

The `xfs_db` enables the examination of XFS file system structures. The `xfs_db` utility takes the device as the parameter. The `xfs_db` man page contains information about how to display the data structures for XFS.

This section shows how to display an inode on an XFS system.

The XFS file system is on the device /dev/hda5.

```bash
# mount -t xfs /dev/hda5 /xfs
# cd /xfs
```

Copy the fstab file located in the /etc directory onto the XFS file system.

```bash
# cp /etc/fstab .
# ls -l
```

```text
total 12
drwxr-xr-x   2 root root     18 Dec  8 10:57 .
drwxr-xr-x   24 root root   4096 Dec  8 10:54 ..
-rw-r--r--   1 root root   948 Dec  8 10:57 fstab
```

To look at a file's inode, its inode number is required. Use the `ls` command with the `-i` option to determine this number. In the following example, the inode number for the fstab file is 131.

```bash
# ls -i
    128 .       128 ..        131 fstab
# cd ..
# umount /xfs
```

The `xfs_db` option to look at an inode is the `inode` command. The `inode` command uses the inode number as the parameter. To print the file system information about the inode, use the `p` command.

```bash
# xfs_db /dev/hda5
     xfs_db> inode 131
     xfs_db> p
core.magic = 0x494e
core.mode = 0100644
core.version = 1
core.format = 2 (extents)
core.nlinkvl = 1
core.uid = 0
core.gid = 0
core.flushiter = 2
core.atime.sec = Mon Dec  8 10:57:53 2003
core.atime.nsec = 123719000
core.mtime.sec = Mon Dec  8 10:57:53 2003
core.mtime.nsec = 1239430000
core.ctime.sec = Mon Dec  8 10:57:53 2003
core.ctime.nsec = 1239430000
core.size = 948
core.nblocks = 1
core.extsize = 0
core.nextents = 1
core.naextents = 0
core.forkoff = 0
core.aformat = 2 (extents)
core.dmevmask = 0
core.dmstate = 0
core.newrtbm = 0
core.prealloc = 0
core.realtime = 0
core.gen = 0
next_unlinked = null
u.bmx[0] = [startoff,startblock,blockcount,extentflag]
0: (0,12,1,0)
xfs_db> q
```

## Tuning File Systems

Now that you're familiar with the layout of the various types of file systems supported in Linux, let's examine how to tune the Ext3, ReiserFS, JFS, and XFS file systems. We'll show how to tune each of the file systems by using an external log and using some of the mount options that are available on each file system.

### Tuning Options for Ext3: Using a Separate Journal Device

External logs improve file system performance because the log updates are saved to a different partition than the corresponding file system, thereby reducing the number of hard disk seeks.

To use an external journal for the Ext3 file system, first run `mkfs` on the journal device. The block size of the external journal must be the same block size as the Ext3 file system. The example in this section uses the /dev/hdb1 device as the external log for the Ext3 file system.

There are two steps to creating an external log. The first is to format the journal; the second is to format the partition and tell `mkfs` that the log will be external. In the following example, the Ext3 partition will be on device /dev/hda1, and the external log will be on device /dev/hdb1. The `mkfs -b` option sets the block size for the file system.

```bash
# mkfs.ext3 -b 4096 -O journal_dev /dev/hdb1
# mkfs.ext3 -b 4096 -J device=/dev/hdb1 /dev/hda1
```

The next few examples use the tiobench program to see if an external log helps the performance of this benchmark on an Ext3 file system. The tiobench benchmark is a multithreaded I/O benchmark. It is used to measure file system performance in four basic operations: sequential read, random read, sequential write, and random write.

First, the device /dev/hda1 is formatted as ext3.

```bash
# mkfs.ext3 /dev/hda1
# mount -t ext3 /dev/hda1 /ext3
# cd /ext3

# tar zxvf tiobench-0.3.3.tar.gz
# cd tiobench-0.3.3
# make
# date && ./tiobench.pl --size 500 --numruns 5 threads=32 && date
```

The following is sample tiobench output with the log inside the partition.

```text
Fri Jun 27 10:17:14 PDT 2003
Run #1: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #2: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #3: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #4: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #5: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T

Unit information
================
File size = megabytes
Blk Size  = bytes
Rate      = megabytes per second
CPU%      = percentage of CPU used during the test
Latency   = milliseconds
Lat%      = percent of requests that took longer than
X seconds
CPU Eff   = Rate divided by CPU% - throughput per cpu load

Sequential Reads

     Lat%     CPU                 File Blk  Num                 Avg         Maximum      Lat%
Identifier      Eff Size  Size Thr Rate  (CPU%) Latency  Latency      >2s
    >10s       -
---  --
 --  -- -  -  --
2.4.20-4GB        500  4096   32  6.93  3.55%    72.342  39522.87    1.56413
 0.00000       195

Random Reads

     Lat%     CPU                 File Blk  Num                 Avg         Maximum      Lat%
Identifier      Eff Size  Size Thr Rate  (CPU%) Latency  Latency      >2s
    >10s     -
---  --
 --  -- -
2.4.20-4GB        500  4096   32  0.89  1.01%   514.676  2536.44     0.00000
 0.00000        88

Sequential Writes

     Lat%     CPU                 File Blk  Num                 Avg         Maximum      Lat%
Identifier      Eff Size  Size Thr Rate  (CPU%) Latency  Latency      >2s
    >10s     -
---  --
 --  -- -
2.4.20-4GB        500  4096   32  4.69  6.98%    49.635  23386.91    1.28907
 0.00000        67

Random Writes

     Lat%     CPU                 File Blk  Num                 Avg         Maximum      Lat%
Identifier      Eff Size  Size Thr Rate  (CPU%) Latency  Latency      >2s
    >10s     -
---  --
 --  -- -
2.4.20-4GB        500  4096   32  0.53  0.43%     0.302   573.19     0.00000
 0.00000       122
Fri Jun 27 10:37:14 PDT 2003

# umount /ext3
```

Next, to determine whether an external log increases the performance of the file system benchmark, change the configuration to have an external log. In the example, the external log is located on /dev/hdb1.

```bash
# mkfs.ext3 -b 4096 -O journal_dev /dev/hdb1
# mkfs.ext3 -b 4096 -J device=/dev/hdb1 /dev/hda1
# mount -t ext3 /dev/hda1 /ext3
# cd /ext3

# tar zxvf tiobench-0.3.3.tar.gz
# cd tiobench-0.3.3
# make
# date && ./tiobench.pl --size 500 --numruns 5 threads=32 && date
```

tiobench output with log external.

```text
Fri Jun 27 11:10:17 PDT 2003
Run #1: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #2: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #3: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #4: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T
Run #5: ./tiotest -t 32 -f 15 -r 125 -b 4096 -d . -T

Unit information
================
File size = megabytes
Blk Size  = bytes
Rate      = megabytes per second
CPU%      = percentage of CPU used during the test
Latency   = milliseconds
Lat%      = percent of requests that took longer than
X seconds
CPU Eff   = Rate divided by CPU% - throughput per cpu load
```

### Sequential Reads

| File Identifier | CPU Eff | File Size | Blk Size | Num Thr | Avg Rate | Avg Latency (CPU%) | Maximum Latency | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 187 | 500 | 4096 | 32 | 6.54 | 3.496 | 83.189 | 40436.07 | 2.41211 | 0.00000 |

### Random Reads

| File Identifier | CPU Eff | File Size | Blk Size | Num Thr | Avg Rate | Avg Latency (CPU%) | Maximum Latency | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 100 | 500 | 4096 | 32 | 0.89 | 0.890 | 540.200 | 2620.12 | 0.00000 | 0.00000 |

### Sequential Writes

| File Identifier | CPU Eff | File Size | Blk Size | Num Thr | Avg Rate | Avg Latency (CPU%) | Maximum Latency | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 71 | 500 | 4096 | 32 | 4.71 | 6.682 | 53.069 | 23588.61 | 1.31673 | 0.00000 |

### Random Writes

| File Identifier | CPU Eff | File Size | Blk Size | Num Thr | Avg Rate | Avg Latency (CPU%) | Maximum Latency | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 122 | 500 | 4096 | 32 | 0.53 | 0.432 | 0.278 | 404.22 | 0.00000 | 0.00000 |

Fri Jun 27 11:30:35 PDT 2003
