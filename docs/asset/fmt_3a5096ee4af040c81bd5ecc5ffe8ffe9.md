
# 文件系统使用报告 `df`

| Filesystem | Kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/sda0` | 30191 | 10596 | 16576 | 39% | `/` |
| `/dev/sdg` | 220010 | 173838 | 26172 | 88% | `/usr` |
| `/dev/sdh` | 764758 | 243088 | 54195 | 35% | `/home` |
| `rs01-ch:/home/rsxx-ch` | 203166 | 185426 | 17348 | 91% | `/rsxx-ch` |
| `hcprophet:/hcprophet` | 18875 | 7449 | 9538 | 44% | `/hcprophet` |

此输出报告现有文件系统的状态，从根分区开始，每行显示：

- 文件系统名称
- 总 Kbytes 大小
- 已使用的 Kbytes
- 可用的 Kbytes (剩余)
- 文件系统当前使用的百分比

文件系统加载似乎是不可能的，但显示的百分比有时会超过 100%（最大值可以达到 111%）。这是如何做？为了传输，可用空间的 10% 被牺牲；然而，超级用户可以使用这些空间。完整的大小将返回“预留磁盘”。这个示例来自 BSD 4.1，它支持 BSD 格式的 `df` 命令。为了区分它们，BSD 类型命名为 `bdf`。这是来自 HP-UX 10.2 的示例：

```
$ df
```

| Filesystem | Kbytes | used | avail | %used | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/vg00/lv1` | 91669 | 58532 | 23970 | 71% | |
| `/dev/vg00/lv7` | 319125 | 252427 | 34785 | 88% | `/var` |
| `/dev/vg00/lv6` | 350997 | 294527 | 56470 | 93% | `/usr` |
| `/dev/vg00/lv5` | 99669 | 23060 | 66642 | 26% | `/tmp` |
| `/dev/vg00/lv4` | 252185 | 189044 | 37112 | 84% | `/opt` |

逻辑卷管理器 `LVM` 是 HP-UX 10.20 的标准部分，并为逻辑节点创建必要的设备。要报告 inode（实际上是关于文件的数值报告），请使用 `df -i`（`-i` 指向索引节点）：

```
$ df -i
```

| Filesystem | used | ifree | %used | Mounted on |
| :--- | :--- | :--- | :--- | :--- |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/sda0` | 1217 | 13887 | 8% | `/` |
| `/dev/sdg` | 13130 | 101150 | 12% | `/usr` |
| `/dev/sdh` | 10726 | 37426 | 3% | `/home` |
| `rs01-ch:/home/rsxx-ch` | * | * | * | `/rsxx-ch` |
| `vaxagr:$1DUB` | * | * | * | `/vaxagr/disk2` |
| `hcprophet:/hcprophet` | * | * | * | `/hcprophet` |

`df` 命令产生不同的报告。这是一个来自 Solaris 2.6 的示例：

```
$ df
/dev/dsk/cl00s0 1488210 blocks 290743
```

这是一个来自 HP-UX 10.20 的示例：

| Filesystem | blocks | i-nodes |
| :--- | :--- | :--- |
| `/opt (/dev/vg0/lvol4)` | 74224 | 36311 |
| `/tmp (/dev/vg0/lvol5)` | 133286 | 15592 |
| `/usr (/dev/vg0/lvol6)` | 42740 | 44762 |
| `/var (/dev/vg0/lvol7)` | 69570 | 35897 |
| | `(/dev/md0/lvol8)` | 47940 | 11893 |

报告包括：

- 文件系统挂载
- 特殊名称
- 块数（块=512 字节）
- inode 数量，即已使用数量

百分比字段（将已用空间表示为总空间的百分比）在通用 `df` 报告中缺失。然而，这是 BSD 类型命令所包含的最常用、可能也是最有价值的信息。因此，某些供应商为此提供了特殊选项：在 Solaris 2.x 中，`-k` 实际上将 `df` 命令转换回 Berkeley 样式。

| Filesystem | kbytes | used | avail | capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/disk/cl1t0s0` | 128076 | 536681 | 740904 | 42% | |
| `/proc` | 0 | 0 | 0 | 0% | `/proc` |
| `/dev` | 0 | 0 | 0 | 0% | `/dev` |
| `/dev/disk/cl1t0s3` | 192241 | 9 | 192040 | 1% | `/root` |
| `swap` | 456840 | 4416 | 501064 | 1% | `/tmp` |
| `/dev/md/d10` | 421182 | 354633 | 625133 | 86% | `/files` |

## 磁盘使用汇总 `du`

移除几个大文件是一个更明智的主意。`du` 命令可以帮助完成这项重要任务。

`du` 命令汇总磁盘使用情况；它会递归地报告指定目录下所有文件和子目录占用的磁盘空间，并按子目录列出。磁盘使用情况以块 `block` 为单位报告（块在不同系统中有所不同）；BSD 使用 1KB 块，而 System V 使用 512 字节块。除此之外，这些版本之间没有区别。典型的 `du` 报告如下：

### Berkeley — SunOS

```
$ du /home/bjl
3753 /home/bjl/ncsa
376 /home/bjl/email
47 /home/bjl/pubdoc
266 /home/bjl/ftp/drivers
....
...
11476 /home/bjl
```

### System V 风格 — HP-UX 10.x 或 Solaris 2.x

```
$ du /users/bjl
8 /users/bjl/current
18 /users/bjl//sessions
42 /users/bjl/.elm
2 /users/bjl/Mail
....
342 /users/bjl
```

显然，这两个 UNIX 平台之间没有区别。对于每个子目录，报告中都会列出其所属的所有文件和子目录，以及单独的一行指示该子目录占用的磁盘空间总量。最后一行显示指定目录的总使用量。通常，这种报告可能非常长且冗长；一个包含几百行的报告显然很难阅读。通过指定 `-s` 选项，仅显示目录及其内容的磁盘空间总量，而会跳过子目录和文件：

```
$ du -s /home/bjl
11476 /home/bjl

$ du -s /users/bjl
342 /users/bjl
```

该命令可以通过管道传递给其他命令，以获取不同的报告，并根据不同的标准（大小、反向大小大小等）对子目录进行排序。

使用该命令的一种非常方便的方法是 `du -s *`，报告将包含当前目录下每个文件的大小以及每个子目录的总大小。这在跟踪文件系统大小的变化以及确定大小突然增加的原因时非常有用。从超大文件系统的挂载点目录开始，我们可以浏览相关的大型子目录，直到找到文件系统大小突然变化的文件或多个文件。为了更好地理解，可以按照此示例实施纠正措施：

```
$ df /var
Filesystem kbytes used avail Mounted on
```

`/var` 文件系统已达到临界大小（假设 90% 为临界值），应该进行检查和清理。为了高效发现潜在的违规者，我们必须找到大型子目录和文件，并检查是否可以删除或调整它们的大小。我们将从文件系统的挂载点开始浏览，在本例中为 `/var`。

```
# $ cd /var
```

```
$ du -s *
0 X11
585526 adm
2 dt
0 lost+found
36 mail
1292 opt
186746 patches
914 preserve
1886 sam
122656 spool
10 statmon
392 tmp
10900 yp
78 ...
...
...
```

`adm` 目录似乎过大了。因此，下一步是：

```
# $ cd adm
```

```
$ du -s *
3038 btmp
18 cron
32254 debug
7264 diag
40 ftmp.cron.log
4 inetd.sec
1914 lp
4598 mailog
2 netstat_data
1642 nettl.LOG00
50 sulog
300892 sw
221550 syslog
52 syslog
980 wtmp
...
```

## 重新挂载文件系统

当启动过程、重启或重新挂载期间发生修改时，会自动启动重启。当在根文件系统上执行了 `fsck` 命令后，也必须手动启动重启命令：

```
# reboot -n
```

`-n` 选项非常重要，它可以防止之前执行 `sync` 命令，该命令会刷新输出缓冲区，而在这种情况下，会导致文件系统再次损坏（这是系统在同步磁盘的情况下重启的唯一情况）。

一个示例（来自 Apollo 工作站和 HP-UX）：

```
$ fsck -y
fsck: /dev/disk01d6s0: root file system
continue (y/n)? y
** /dev/dc01d6s0
** Mounted on/
** Root file system
** Phase 1 - Check Blocks and Sizes
** Phase 2 - Check Pathnames
** Phase 3 - Check Connectivity
** Phase 4 - Check Reference Counts
FREE INDEX COUNT WRONG IN SUPERBLK
FIX?
** Phase 5 - Check Cyl groups
SUMMARY INFORMATION (SUPER BLOCK SUMMARIES) BAD
CYLINDER GROUPS
FIX?
** Phase 6 - Salvage Cylinder Groups
21806 files, 0 icount, 298674 used, 12832 free (1472 frags, 15855 blocks)
***** MAKING FILE SYSTEM CLEAN *****
***** FILE SYSTEM WAS MODIFIED *****
***** REBOOT HP-UX; DO NOT SYNC (USE reboot -n) *****
```
