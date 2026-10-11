

## XFS 文件布局

`xfs_db` 允许检查 XFS 文件系统的结构。`xfs_db` 工具以设备作为参数。`xfs_db` 手册页包含有关如何显示 XFS 数据结构的信息。

本节展示了如何在 XFS 系统上显示一个 inode。

XFS 文件系统位于设备 /dev/hda5 上。

```bash
# mount -t xfs /dev/hda5 /xfs
# cd /xfs
```

将位于 /etc 目录中的 fstab 文件复制到 XFS 文件系统上。

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

要查看文件的 inode，需要其 inode 号。使用 `ls` 命令并加上 `-i` 选项来确定该号码。在以下示例中，fstab 文件的 inode 号是 131。

```bash
# ls -i
    128 .       128 ..        131 fstab
# cd ..
# umount /xfs
```

`xfs_db` 中查看 inode 的选项是 `inode` 命令。`inode` 命令使用 inode 号作为参数。要打印关于该 inode 的文件系统信息，请使用 `p` 命令。

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

## 文件系统调优

现在你已经熟悉了 Linux 中支持的各种类型文件系统的布局，让我们来看看如何调优 Ext3、ReiserFS、JFS 和 XFS 文件系统。我们将展示如何通过在每个文件系统上使用外部日志和使用可用的挂载选项来调优每个文件系统。

### Ext3 调优选项：使用单独的日志设备

外部日志可以提高文件系统性能，因为日志更新被保存在与对应文件系统不同的分区上，从而减少了硬盘寻道次数。

要为 Ext3 文件系统使用外部日志，首先需在日志设备上运行 `mkfs`。外部日志的块大小必须与 Ext3 文件系统的块大小相同。本节中的示例使用 /dev/hdb1 设备作为 Ext3 文件系统的外部日志。

创建外部日志有两个步骤。第一步是格式化日志；第二步是格式化分区并告诉 `mkfs` 日志将是外部的。在以下示例中，Ext3 分区将位于设备 /dev/hda1 上，而外部日志将位于设备 /dev/hdb1 上。`mkfs -b` 选项设置文件系统的块大小。

```bash
# mkfs.ext3 -b 4096 -O journal_dev /dev/hdb1
# mkfs.ext3 -b 4096 -J device=/dev/hdb1 /dev/hda1
```

接下来的几个示例使用 tiobench 程序来查看外部日志是否有助于提高 Ext3 文件系统上此基准测试的性能。tiobench 基准测试是一个多线程 I/O 基准测试。它用于测量文件系统在四种基本操作中的性能：顺序读取、随机读取、顺序写入和随机写入。

首先，将设备 /dev/hda1 格式化为 ext3。

```bash
# mkfs.ext3 /dev/hda1
# mount -t ext3 /dev/hda1 /ext3
# cd /ext3

# tar zxvf tiobench-0.3.3.tar.gz
# cd tiobench-0.3.3
# make
# date && ./tiobench.pl --size 500 --numruns 5 threads=32 && date
```

以下是日志在分区内部的 tiobench 输出样本。

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

接下来，为了确定外部日志是否能提高文件系统基准测试的性能，将配置更改为使用外部日志。在示例中，外部日志位于 /dev/hdb1 上。

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

日志位于外部的 tiobench 输出。

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

### 顺序读取

| 文件标识符 | CPU 效率 | 文件大小 | 块大小 | 线程数 | 平均速率 | 平均延迟 (CPU%) | 最大延迟 | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 187 | 500 | 4096 | 32 | 6.54 | 3.496 | 83.189 | 40436.07 | 2.41211 | 0.00000 |

### 随机读取

| 文件标识符 | CPU 效率 | 文件大小 | 块大小 | 线程数 | 平均速率 | 平均延迟 (CPU%) | 最大延迟 | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 100 | 500 | 4096 | 32 | 0.89 | 0.890 | 540.200 | 2620.12 | 0.00000 | 0.00000 |

### 顺序写入

| 文件标识符 | CPU 效率 | 文件大小 | 块大小 | 线程数 | 平均速率 | 平均延迟 (CPU%) | 最大延迟 | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 71 | 500 | 4096 | 32 | 4.71 | 6.682 | 53.069 | 23588.61 | 1.31673 | 0.00000 |

### 随机写入

| 文件标识符 | CPU 效率 | 文件大小 | 块大小 | 线程数 | 平均速率 | 平均延迟 (CPU%) | 最大延迟 | Lat% >2s | Lat% >10s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2.4.20-4GB | 122 | 500 | 4096 | 32 | 0.53 | 0.432 | 0.278 | 404.22 | 0.00000 | 0.00000 |

Fri Jun 27 11:30:35 PDT 2003

