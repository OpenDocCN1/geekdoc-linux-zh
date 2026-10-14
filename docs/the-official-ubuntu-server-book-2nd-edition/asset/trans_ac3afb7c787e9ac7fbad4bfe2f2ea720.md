

为每个数组生成兼容的字符串，所以你所要做的就是将该输出重定向到 /etc/mdadm/mdadm.conf 文件：

```
$ sudo sh -c 'mdadm --detail --scan >> /etc/mdadm/mdadm.conf'
```

现在编辑你的 /etc/fstab 并添加一个 /dev/md0 的条目，就像对待其他任何挂载点一样。在我的例子中我会添加

```
/dev/md0  /mnt/storage  ext3  defaults  0 0
```

或者，我也可以在 fstab 中指定该设备的 UUID，就像其他分区一样。要查明这一点，我会输入

```
$ sudo blkid | grep /dev/md0
/dev/md0: UUID="99e190a7-dfe7-48ee-bf56-f426ef5343af" type="ext4"
```

一旦 /etc/mdadm/mdadm.conf 和 /etc/fstab 设置好，我就可以重启，然后检查 /proc/mdstat 以确保阵列启动，然后确认它已挂载。

## Software RAID Management

你对软件 RAID 阵列的大部分管理是在两个地方进行的：/proc/mdstat 和 mdadm。/proc/mdstat 文件提供了所有正在运行的 RAID 阵列的当前状态，包括如果其中任何一个重建磁盘时应有的进度条。单个 RAID 阵列的标准 /proc/mdstat 文件可能如下所示：

```
$ cat /proc/mdstat
Personalities : [raid6] [raid5] [raid4]
md0 : active raid5 sdd1[2] sdc1[1] sdb1[0]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]

unused devices: <none>
```

在输出中你可以看到哪个阵列处于活动状态（md0），它使用什么 RAID 级别（raid5），以及它使用哪些分区（sdd1、sdc1 和 sdb1）。在最后一行你可以看到 RAID 是健康的，因为它有三个磁盘全部处于活动状态（[3/3] [UUU]）。如果任何磁盘出现故障，该部分会发生变化，如下所示。

虽然你可以通过 /proc/mdstat 获取状态，但大部分实际的 RAID 管理是通过 mdadm 完成的。例如，此工具可以使用 --query 和 --detail 参数分别报告有关阵列的基本和更完整的信息：

```
$ sudo mdadm --query /dev/md0
/dev/md0: 15.99GiB raid5 3 devices, 0 spares. Use mdadm --detail for more detail.
$ sudo mdadm --detail /dev/md0
/dev/md0:
        Version : 00.90.03
        Creation Time : Wed Feb 11 21:31:16 2009
        Raid Level : raid5
        Array Size : 16771584 (15.99 GiB 17.17 GB)
        Used Dev Size : 8385792 (8.00 GiB 8.59 GB)
        Raid Devices : 3
        Total Devices : 3
        Preferred Minor : 0
        Persistence : Superblock is persistent
        Update Time : Wed Feb 11 22:11:49 2009
        State : clean
        Active Devices : 3
        Working Devices : 3
        Failed Devices : 0
        Spare Devices : 0
        Layout : left-symmetric
        Chunk Size : 64K
        UUID : 37090db5:5fafad78:e368bf24:bd0fce41 (local to host ubuntu)
        Events : 0.4
```

| Number | Major | Minor | RaidDevice | State |
| 0 | 8 | 17 | 0 | active sync | /dev/sdb1 |
| 1 | 8 | 33 | 1 | active sync | /dev/sdc1 |
| 2 | 8 | 49 | 2 | active sync | /dev/sdd1 |

## Replace a Failed Disk

虽然 mdadm 的所有信息都可能有用，但你会发现你主要在驱动器故障时使用 mdadm。当驱动器故障时，系统上运行的 mdadm 守护进程会自动向主机上的 root 用户发送电子邮件。要更改此设置，请编辑 /etc/mdadm/mdadm.conf 并在文件中找到 MAILADDR 选项。保存更改后，运行 sudo /etc/init.d/mdadm reload 以加载新选项。除了电子邮件之外，你也可以从 /proc/mdstat 看到驱动器已故障：

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md0 : active raid5 sdb1[0] sdd1[3](F) sdc1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]

unused devices: <none>
```

在这里你可以看到 sdd1 被标记为 (F) 表示它已故障，并且在输出的第三行阵列显示三个磁盘中有两个（[3/2] [UU_]）。下一步是从 /dev/md0 中移除该磁盘，以便我可以用新驱动器替换它。为此我运行带有 --remove 选项的 mdadm：

```
$ sudo mdadm /dev/md0 --remove /dev/sdd1
```

驱动器必须被设置为故障驱动器才能将其移除，因此如果由于某种原因 mdadm 没有检测到驱动器故障但你想将其替换，你可能需要在移除之前将其设置为故障：

```
$ sudo mdadm /dev/md0 --fail /dev/sdd1
```

mdadm 命令支持命令链，所以你可以在同一行中使驱动器故障并移除它：

```
$ sudo mdadm /dev/md0 --fail /dev/sdd1 --remove /dev/sdd1
```

一旦你从阵列中移除驱动器，它将从 /proc/mdstat 中消失：

```
$ cat /proc/mdstat
Personalities : [linear] [multipath] [raid0] [raid1] [raid6]
[raid5] [raid4] [raid10]
md0 : active raid5 sdb1[0] sdc1[1]
16771584 blocks level 5, 64k chunk, algorithm 2 [3/2] [UU_]

unused devices: <none>
```

