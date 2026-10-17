
unused devices: <none>

此输出显示你有一个包含三块磁盘的活动 RAID 5 阵列。最后几行显示 RAID 阵列中每个磁盘和分区的状态。你还可以看到 RAID 处于“恢复”模式，或者正在自我创建。

**步骤 5。** 如果你等待估计的 2.9 分钟然后再次查询，你将看到以下内容：

```
# cat /proc/mdstat

Personalities : [raid0] [raid6] [raid5] [raid4]

md0 : active raid5 hdd1[2] hdc1[1] hdb1[0]

      8001280 blocks level 5, 64k chunk, algorithm 2 [3/3] [UUU]
```

unused devices: <none>

现在你看到 RAID 已经完成构建，可以正常使用了。

## 当磁盘故障时怎么办

假设阵列中的某块磁盘故障了。在这种情况下，你需要将该磁盘从阵列中移除并替换为正常磁盘。你有额外的硬盘，对吧？你可以手动让磁盘故障，看看阵列中的磁盘故障时会是什么。

步骤 1。要使阵列中的磁盘故障，使用此命令：

```
# mdadm /dev/md0 -f /dev/hdd1

mdadm: set /dev/hdd1 faulty /dev/md0
```

步骤 2。通过查看 RAID 设备的详细信息验证阵列中的磁盘已故障：

```
# mdadm -D /dev/md0
/dev/md0:

  Version : 1.2

  Creation Time : Jan 27 14:09:23 2011

  Raid Level : raid5

  Array Size : 16769024 (15.99 GiB 17.17 GB)

  Used Size : 8384512 (8.00 GiB 8.59 GB)

  Raid Devices : 3

  Total Devices : 3

  Persistence : Superblock is persistent
```

Update Time : Thu Jan 27 14:28:55 2011
State : degraded
Active Devices : 2
Working Devices : 2
Failed Devices : 1
Spare Devices : 0

```
Layout : left-symmetric

Chunk Size : 512K
```

Name : RHEL-01: (local to host RHEL-01)
UUID : a02fb98a:63a7cbbf:762c7a7f:e681aeee
Events : 19

| 编号 | 主设备号 | 次设备号 | RaidDev | 状态 |
|---|---|---|---|---|
| 0 | 8 | 17 | active sync | /dev/hdd1 |
| 1 | 8 | 33 | active sync | /dev/hdc1 |
| 2 | 0 | 2 | removed | |
| 3 | 8 | 49 | faulty | /dev/hdd1 |

既然磁盘已故障，你需要将其从阵列中移除以便替换。

步骤 3。从阵列中移除磁盘，使用此命令：

```
# mdadm /dev/md0 -r /dev/hdd1

mdadm: removed /dev/hdd1
```

Red Hat 实操指南：RHCS 和 RHCE 认证

步骤 4。再次查看 RAID：

```
# mdadm -D /dev/md0
/dev/md0:

  Version : 1.2

  Creation Time : Jan 27 14:09:23 2011

  Raid Level : raid5

  Array Size : 16769024 (15.99 GiB 17.17 GB)

  Used Device : 8384512 (8.00 GiB 8.59 GB)

  Raid Devices : 3

  Total Devices : 2

  Persistence : Superblock
```

Update Time : Thu Jan 27 14:31:23 2011

State : clean, degraded

Active Devices : 2

Working Devices : 2

Failed Devices : 0

```
Layout : left-symmetric
Chunk Size : 512K
Name : RHEL-01: (local to host RHEL-01)
UUID : a02fb98a:63a7cbbf:702c7a7f:e61a8ee
Events : 22
```

| 编号 | 主设备号 | 次设备号 | RaidDevice | 状态 |
|---|---|---|---|---|
| 0 | 8 | 17 | active sync | /dev/hdb1 |
| 1 | 33 | 1 | active sync | /dev/hdc1 |
| 2 | 0 | 2 | removed |

你可以从输出的最后几行看到磁盘已被“移除”。如果是真实的故障，你可以取出磁盘并更换为正常磁盘。在这种情况下，使用“热插拔”硬盘很有用。

> 技巧
> 如果你想，可以将之前的两个命令合并为一个来故障并从阵列中移除，这样更容易理解。如果你想一起使用它们，可以使用：
> `# mdadm /dev/md0 -f /dev/hdd1 -r /dev/hdd1`

当你放了一个新磁盘时，需要让它在阵列中活动。首先，你需要像最初设置 RAID 阵列那样对磁盘进行分区。

步骤 5。磁盘分区后，按照如下方式将其添加回阵列：

```
# mdadm /dev/md0 -a /dev/hdd1

mdadm: re-added /dev/hdd1
```

**步骤 6。**验证它是否已正确添加：

```
# mdadm -D /dev/md0
/dev/md0:

  Version : 1.2

  Creation Time : Thu Jan 27 14:09:23 2011

  Raid Level : raid5

  Array Size : 16769924 (15.99 GiB 17.17 GB)

  Used Dev Device : 8384512 (8.00 GiB 8.59 GB)

  Raid Devices : 3

  Total Devices : 3

  Persistence : persistent
```

Update Time : Thu Jan 27 14:34:21 2011

State : clean, degraded, recovering

Active Devices : 2

Working Devices : 3

Failed Devices : 0

Layout : left-symmetric

Chunk Size : 512K

Name : RHEL-01: (local to host RHEL-01)

UUID : a02fb98a:63a7cbbf:762c7a7f:e61a8ee

Events : 26

| 编号 | 主设备号 | 次设备号 | RaidDevice | 状态 |

|---|---|---|---|---|

| 0 | 8 | 17 | active sync | /dev/hdb1 |

| 1 | 33 | 1 | active sync | /dev/hdc1 |

| 2 | 0 | 2 | removed |

注意磁盘的状态为“正在重建”。你可以查询内核以找出系统认为备盘重建之前还需要多长时间。

**步骤 7。**查询内核：

```
# cat /proc/mdstat
Personalities : [raid0] [raid6] [raid5] [raid4]
md0 : active raid5 hdb[2] hdc[1] hdb[0]
      16769024 blocks super 1.2 level 5, 512k chunk, algorithm 2 [3/2] [UU_]
============= recovery = 17.4% (69726/4000640)
finish=3.9min speed=13843K/sec
```

unused devices: <none>

**步骤 8。** 如果发生错误并你需要将 RAID 阵列离线，可以使用以下命令：

```
# mdadm -vS /dev/md0
mdadm: stopped /dev/md0
```

你可能还需要将阵列离线以对文件系统进行维护。完成所有更改后，你可以将阵列恢复在线。现在你的阵列可以像任何其他磁盘一样使用了。你可以对其进行格式化并像创建普通分区一样创建文件系统（指向 `/dev/md0` 而不是单个分区）。

### 删除 RAID 阵列

现在你已经成功实现了 RAID 阵列，可以通过删除阵列来将其拆解。

步骤 1。要删除阵列，首先停止它：
