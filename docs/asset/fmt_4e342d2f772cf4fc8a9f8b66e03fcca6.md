
### 设置 RAID

到为止，我们已经了了分区、交换分区以及如何设置它们。现在让我们转向最后的分区类型：RAID 分区允许更高级的功能，如冗性和更好的性能。在描述如何实现 RAID 之前，让我们看看不同的类型： RAID 0 (条列)：磁盘组合形成一个大驱动器。以可用性为代价提供了更好的性能。如果任何一个磁盘故障，整个磁盘组将无法使用。RAID 1 (镜像)：磁盘从一个复制到另一个，允许冗余。如果一个磁盘故障，另一个磁盘将接管，拥有原始磁盘的精确副本。缺点是写入缓慢。 RAID 5 (带校验的条列)：与 RAID 0 类似组合形成一个大驱动器。区别是磁盘的 25% 用于校验位，允许在单个磁盘故障时恢复。

虽然 RAID 可以在硬件级别实现，但 Red Hat 考试不是基于硬件的，因此重点是通过 `MD` 驱动程序的软件实现。接下来，使用上一节中的三个空驱动器（`hdb`, `hdc` 和 `hdd`）设置 RAID 阵列。

步骤 1. 安装以下包：

```bash
# yum install -y mdadm
```

步骤 2. 验证安装：

```bash
# rpm -qa | grep mdadm
mdadm-3.1.3-1.el6.x86_64
```

该包应该已经随系统安装，你可以验证其存在。要开始，你需要在使用的磁盘上创建分区（是的，我知道你在上一节结束时有了它们……当作练习）。你从 RAID 5 设置开始，因此需要在三个磁盘上分区。

# 现实世界提示

如果你刚开始接触 RAID，注意到可以在单个磁盘上创建分区并使用它们创建 RAID 以观察如何实现。但在现实世界中，在单个磁盘上设置 RAID 完全违背了 RAID 的目的，因为 RAID 是为了性能和冗余，这可以通过将所有分区放在单独的磁盘来实现。

# 创建 RAID 阵列

你应该知道如何创建基本分区，因此创建一个 RAID 阵列对你来说应该是很好的练习。在每个磁盘（`hdb`, `hdc`, `hdd`）上创建一个分区，允许每个分区消耗整个磁盘。

完成后你看到的运行如下：

步骤 1.

```
# fdisk -l
Disk /dev/hda: 21.5 GB, 2147836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x0021654
```

| Device | Boot | Start | End | Blocks | Id | System |
| /dev/hda | * | 1 | | 512000 | 83 | Linux |
| Partition 1 does not exist on cylinder boundary. | | | | | | |
| /dev/hdb | | 64 | | 2045896 | | |

```
Disk /dev/hdb: 8589 MB, 8589934952 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xf3f3a90
```

| Device | Boot | Start | End | Blocks | Id | System |
| /dev/hdb1 | | 1 | | 1044 | 83 | Linux |

```
Disk /dev/hdd: 8589 MB, 8589934952 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

| Device | Boot | Start | End | Blocks | Id | System |
| /dev/hdd1 | | 1 | | 1044 | 83 | Linux |

## 第 3 章：磁盘与分区 103

I/O own（最小/最优）：512 字节 / 512 字节
磁盘标识符：0x000793351

| 设备 | 启动 | 起始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/hdd1 | 1 | 1044 | 8385898+ | 83 | Linux |

现在你可以可以开始使用这三个分区设置 RAID 5 阵列了。你可以使用 `mdadm` 命令创建任何 RAID 阵列。

语法：`mdadm [options]`

选项：

- `-a`, `xx` 向当前阵列添加磁盘
- `-C`, `--create` 创建新的 RAID 阵列
- `-D`, `--detail` 打印阵列详细信息
- `-G`, `--grow` 更改活动阵列的大小或形状
- `-l`, `--level` 指定要创建的 RAID 阵列的级别（类型）
- `-n`, `--raid-devices` 指定 RAID 阵列中的设备
- `-q`, `--quiet` 指定不显示输出
- `-S`, `--stop` 停止阵列
- `-v`, `--verbose` 提供详细输出

**步骤 2。** 你可以从以下命令判断你创建了一个新的 RAID 阵列 (`/dev/md0`)，它是 RAID 5，并且包含三块磁盘：

```
# mdadm -Cv /dev/md0 -level=5 -n3 /dev/hdd1 /dev/hdc1 /dev/hdd1
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```

```
# mdadm -D /dev/md0
/dev/md0:
  Version : 1.2
  Creation Time : Jan 27 14:09:23 2011
  Raid Level : raid5
  Array Size : 167690824 (15.99 GiB 17.17 GB)
  Used Size : 8384512 (8.00 GiB 8.59 GB)
  Raid Devices : 3
  Total Devices : 3
  Persistence : Superblock is persistent
```

Update Time : Thu Jan 27 14:15:27 2011
State : clean
Active Devices : 3
Working Devices : 3
Failed Devices : 0
Spare Devices : 0

Layout : left-symmetric
Chunk Size : 512K

Name : RHEL-01: (local to host RHEL-01)
UUID : a02fb98a:63a7cbbf:762c7a7f:e681a8eee

| 编号 | 主设备号 | 次设备号 | RaidDevice | 状态 | 位置 |
|---|---|---|---|---|---|
| 0 | 8 | 17 | 0 | active sync | /dev/hdb1 |
| 1 | 8 | 33 | 1 | active sync | /dev/hdc1 |
| 3 | 8 | 49 | 2 | active sync | /dev/hdd1 |

在第 10 章，你将学习如何查询内核信息（以及如何显示系统上当前的 RAID 阵列）。你也可以通过这种捷径查询内核信息。

**步骤 4。** 查看新创建的 RAID 阵列的状态：

```
# cat /proc/mdstat
Personalities : [raid0] [raid6] [raid5] [raid4]
md0 : active raid5 hdd1[3] hdc1[1] hdb1[0]
      16769024 blocks super 1.2 level 5, 512k chunk, algorithm 2 [3/2] [UU_]
============= recovery = 17.8% (6148864/8384512)
finish=2.9min speed=20872K/sec
```
