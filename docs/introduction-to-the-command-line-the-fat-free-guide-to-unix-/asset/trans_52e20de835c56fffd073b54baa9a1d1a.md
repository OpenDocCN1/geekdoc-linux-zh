
## iostat

**用途：** 显示 I/O 使用率统计数据。

**用法语法：** `iostat [OPTIONS] [DELAY] [COUNT]`

```
# iostat -d 2 5
Linux 2.6,24-19-server (vmware-02)    05/03/2010

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda            56.65        3.44         756.95      9462264    2080033488

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             3.50        0.00          64.00            0           128

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             6.97        0.00          59.70            0           120

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda             0.00        0.00           0.00            0             0

Device:         tps  Blk_read/s  Blk_writn/s   Blk_read     Blk_writn
sda            61.50        0.00         524.00            0          1048

Displaying I/O utilization using the iostat command
```

**iostat** 命令用于显示磁盘驱动器以及网络文件系统的 I/O 使用率统计。它在监控磁盘驱动器方面非常有用，因为磁盘驱动器往往是系统性能中的一个主要瓶颈。在上述示例中，显示了五行 I/O 统计数据。第一行显示自上次系统启动以来的统计信息。后续的每一行则显示自前一行打印以来的累计数据。

### 常见用法示例：

- `iostat` - 显示一次 I/O 使用率后退出
- `iostat [DELAY]` - 在指定间隔更新 I/O 使用率
- `iostat [DELAY] [COUNT]` - 达到指定次数后结束
- `iostat -k` - 以每秒千字节显示统计信息
- `iostat -m` - 以每秒兆字节显示统计信息
- `iostat -d` - 仅显示 I/O 设备
- `iostat -P` - 单独显示每个分区
- `iostat -n` - 显示 NFS I/O 使用率

## dstat

**用途：** 监控 CPU、磁盘、网络和交换分区（swap）的使用情况。

**用法语法：** `dstat [OPTIONS] [DELAY] [COUNT]`

```
$ dstat 2 10
---total-cpu-usage----	-dsk/total-	-net/total-	---paging--	---system--
usr sys idle wai hiq siq read writr rcv send in out intr cs
0 2 97 0 0 0|1763B 379k| 0 0 0 131 2611
0 9 91 0 0 0| 0 0| 346K 99K| 0 0 0 482 4746
0 3 97 0 0 0| 0 410K| 141K 16K| 0 0 0 125 3189
0 3 97 0 0 0| 0 0| 55K 90908| 0 0 0 114 3054
0 3 96 0 0 0| 0 0| 55K 9.9K| 0 0 0 100 2723
0 4 96 0 0 0| 0 376K| 63K 11K| 0 0 0 115 2904
0 3 96 0 0 0| 0 0| 55K 9.8K| 0 0 0 127 3221
0 2 98 0 0 0| 0 182K| 64K 13K| 0 0 0 135 3067
0 2 97 0 0 0| 0 0| 55K 10K| 0 0 0 115 2925
0 4 96 0 0 0| 0 0| 54K 9832B| 0 0 0 118 3129
0 13 87 0 0 0| 0 94K| 37K 11K| 0 0 0 548 4950
Monitoring system performance using the dstat command
```

**dstat** 是一个适用于 Linux 系统的综合性能监控工具。上述示例展示了 **dstat** 的默认输出，它在一个易于阅读的单行显示中同时呈现 CPU、磁盘、网络和交换分区的使用情况。

> **提示** *dstat 的输出可以通过多个命令行选项自定义以满足您的需求。更多信息请参阅 man dstat。*

### 常见用法示例：

- `dstat` - 监控系统使用情况
- `dstat [DELAY]` - 在指定间隔更新结果
- `dstat [DELAY] [COUNT]` - 达到指定次数后结束监控

## nfsstat

**用途：** 显示 NFS 统计数据。

**用法语法：** `nfsstat [OPTIONS]`

```
# nfsstat
Server rpc stats:
calls    badcalls   badauth   badclnt   xdr_call
1        0          0         0         0

Server nfs v3:
null    getattr     setattr     lookup    access    readlink
1       100% 0     0% 0        0% 0      0% 0      0% 0
read    write       create      mkdir     symlink   mnod
0       0% 0        0% 0        0% 0      0% 0      0%
remove  rmdir       rename      link      readdir   readdirplus
0       0% 0        0% 0        0% 0      0% 0      0%
fstat   fsinfo      pathconf    commit
0       0% 0        0% 0        0% 0      0%

Client rpc stats:
calls    retrans   authrefresh
2924     0         0

Client nfs v3:
null    getattr     setattr     lookup    access    readlink
0       0% 2761     94% 0        0% 2      0% 87     2% 0
read    write       create      mkdir     symlink   mnod
1       0% 0        0% 0        0% 3      0% 0       0%
remove  rmdir       rename      link      readdir   readdirplus
0       0% 0        0% 0        0% 0      0% 0       0% 66
fstat   fsinfo      pathconf    commit
0       0% 2        0% 1        0% 0      0%

Displaying NFS statistics
```

**nfsstat** 显示 NFS 使用率统计。这对于监控 NFS 服务的性能很有帮助。上述示例展示了在本地系统上运行的 NFS 客户端和服务器的各项使用指标。

### 常见用法示例：

- `nfsstat` - 显示所有 NFS 统计数据
- `nfsstat -s` - 仅显示服务器统计数据
- `nfsstat -c` - 仅显示客户端统计数据

## free

**用途：** 显示系统内存和交换空间使用情况信息。

**用法语法：** `free [OPTIONS]`

```
$ free
               total        used        free       shared      buffers       cached
Mem:       8186412    8136752       49660            0       181960      7352700
-/+ buffers/cache:   602092     7584320
Swap:      23695832           88     23695744

Displaying memory and swap space utilization using the free command
```

**free** 显示 Linux 系统的内存和交换空间使用情况。**free** 命令的默认输出以千字节为单位显示总量，如上述示例所示。下一个示例展示了使用 **-m** 选项，该选项产生以兆字节为单位的更“人类友好”的输出。

```
$ free -m
               total        used        free       shared      buffers        cached
Mem:              7994        7946          48            0          177           7180
-/+ buffers/cache:        588        7406
Swap:             23140           0       23140

Displaying memory and swap space utilization in "human friendly" format
```

### 常见用法示例：

- `free` - 以千字节显示内存使用情况
- `free -m` - 以兆字节显示内存使用情况
- `free -g` - 以吉字节显示内存使用情况

## df

**用途：** 显示文件系统使用情况信息。

**用法语法：** `df [OPTIONS]`

```
$ df -h

Filesystem          Size  Used Avail Use% Mounted on
/dev/sda6           143G  9.1G 127G  7% /
/dev/sdb1           466G  426G 41G  92% /media/Seagate
tmpfs               2.0G     0  2.0G  0% /lib/init/rw
varrun              2.0K  104K  2.0G  1% /var/run
varlock             2.0G     0  2.0G  0% /var/lock
udev                2.0G  172K  2.0G  1% /dev
tmpfs               2.0G  508K  2.0G  1% /dev/shm
lrm                 2.0G  2.7M  1.9G  1% /lib/modules/2.6.28-11

Typical output of the df command
```

**df** 命令用于显示 Unix、Linux 和 BSD 系统上的文件系统使用情况。输出结果会显示每个文件系统的大小、已用空间和可用空间。

在某些系统上，**df** 还会显示关于伪文件系统的信息。这些文件系统通常不包含实际文件，仅存在于内存中，以提供对内核设施的访问。在上述示例中，前两行是实际文件系统，其余条目是伪文件系统。

> **提示**
> 某些系统可能支持如上述示例中所示的 `-h` 参数。此选项以千字节、兆字节和吉字节显示“人类可读”的输出，而不是默认的度量单位（通常为 1k 或 512k 块）。请查阅 `man df` 以验证本地系统默认使用的度量单位。

### 常见用法示例：

- `df` - 显示文件系统使用情况信息
- `df -h` - 以人类可读格式显示大小（即兆字节和吉字节）

## du

**用途：** 显示磁盘使用情况。

**用法语法：** `du [OPTIONS] [DIRECTORY/FILE]`

```
$ du -hs /usr
523M /usr
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_212_0.png)

du 命令用于显示磁盘使用情况信息。它可以显示特定目录或一组文件的大小。上述示例演示了如何使用 du 命令显示 /usr 目录的大小。-hs 选项指示 du 以“人类可读”的形式显示汇总结果。如果省略 -s 选项，则如下例所示，将递归显示 /usr 下每个文件的大小。

```
$ du -h /usr/
4.0K /usr/local/etc
1.4M /usr/local/bin
4.0K /usr/local/games
4.0K /usr/local/src
4.0K /usr/local/sbin
224K /usr/local/share/man/man1
228K /usr/local/share/man
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_212_1.png)

某些系统可能不支持 -h 参数。在这种情况下，du 命令将以块而非“人类可读”的度量单位显示文件大小，如下例所示。

```
$ du -s /usr
534884 /usr
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_212_2.png)

### 常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `du -hs` | 显示当前目录的大小 |
| `du -hs [DIRECTORY]` | 显示指定目录的大小 |
| `du -h [DIRECTORY]` | 显示指定目录中每个文件的大小 |

