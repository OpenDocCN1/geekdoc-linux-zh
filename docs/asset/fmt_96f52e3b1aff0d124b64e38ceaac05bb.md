
```
# parted /dev/sdc
GNU Parted 1.8.1
Using /dev/sdc
Welcome to GNU Parted! Type 'help' to view a list of commands.
```

## 使用 `mkpart` 创建分区

在本演示中，创建一个 500MB 的分区：

```
(parted) mkpart
分区类型？主/扩展？primary
文件系统类型？[ext2] linux-swap
开始位置？501m
结束位置？1000m
```

## 执行 `print` 以验证

```
(parted) print
```

Model: Vmware, VMware Virtual S (scsi)

Disk: `/dev/sdc`: 8590MB

Sector size (logical/physical): 512B/512B

Partition Table: mdsos

## 退出 `parted` 并执行 `partprobe`

退出 `parted` 并在命令提示符处执行 `partprobe` 命令，强制内核重新读取更新后的分区表信息：

```
# partprobe
```

## 确认分区信息

使用以下任意命令确认分区信息：

```
# parted /dev/sdc print
```

Model: Vmware, VMware Virtual S (scsi)

Disk:`/dev/sdc`: 8590GB

Sector size (logical/physical): 512B/512B

Partition Table: mdsos

| Number | Start | End | Size | Type | File system | Flags |
| 1 | 0.51kB | 500MB | 500MB | primary | ext2 | |
| 2 | 500MB | 1000MB | 500MB | primary | | |

> 信息：如有必要，忘记更新 `/etc/fstab`。

```
# grep sdc /proc/partitions
```

## 删除分区

删除分区将从分区表删除分区信息。让我们删除之前创建的分区。

### 在 `/dev/sdc` 磁盘上执行 `parted` 命令

```
# parted /dev/sdc
GNU Parted 1.8.1
Using /dev/sdc
Welcome to GNU Parted! Type 'help' to view a list of commands.
```

### 执行 `rm` 删除分区

```
(parted) rm 1
(parted) rm 2
```

### 执行 `print` 以验证

```
(parted) print

Model: Vmware, VMware Virtual S (scsi)
Disk /dev/sdc: 8590MB
Sector size (logical/physical): 512B/512B
Partition Table: mdsos

Number Start End Size Type File system Flags
```

### 退出 `parted` 并执行 `partprobe`

退出 `parted` 并在命令提示符处执行 `partprobe` 命令，强制内核重新读取更新后的分区表信息：

### 确认分区信息

```
# parted /dev/sdc print
Model: Vmware, VMware Virtual S (scsi)
Disk /dev/sdc: 8590MB
Sector size (logical/physical): 512B/512B
Partition Table: mdsos
```

软件 RAID 使用现有的标准分区，RAID 1 至少需要两个分区，RAID 5 至少需要三个。必须在系统上安装名为 `mdadm` 的软件包来配置软件 RAID：

```
# rpm -qa | grep mdadm
mdadm-2.6.4-1.el5
```

## 创建 RAID 1 阵

以下是创建 RAID 1 阵的步骤：

### 创建分区

使用本章之前介绍的方法，通过 `fdisk` 或 `parted` 创建两个分区。在本演示中，假设你已经有了大小为 1GB 的 `/dev/sdb1` 和 `/dev/sdc1` 分区，且每个分区的分区 ID 类型设置为 "fd"（Linux 自动检测）。你应该能够看到这两个分区：

```
# fdisk -l
...
Disk /dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = 13065 * 512 = 82252080 bytes

Device Start End Blocks Id System
/dev/sdb1 1 123 987966 fd Linux autodetect

Disk /dev/sdc: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = 13065 * 512 = 82252080 bytes

Device Start End Blocks Id System
/dev/sdc1 1 123 987966 fd Linux autodetect
....
```

### 执行 `mdadm` 创建 RAID 1

该命令将创建一个 `-C` 类型为 `-I` RAID 1、名为 `/dev/md0` 的 RAID 阵，并包含两个分区 `-n` `/dev/sdb1` 和 `/dev/sdc1`。`-v` 选项用于详细输出。

```
# mdadm -VC /dev/md0 -n=2 /dev/sdb1 /dev/sdc1 -l=1
mdadm: size set to 981248K
mdadm: array /md0 started.
```

### 验证阵列

通过列出 `/proc/mdstat` 文件的内容或运行带有 `-D` (detail) 选项的 `mdadm` 命令来验证该阵：

```
# cat /proc/mdstat
[raid1]
Personalities : active raid1 sdc1[0] sdb1[0]
md0 : active raid1 sdc1[0] sdb1[0]
981248 blocks [2/2] [UU]
unused devices: <none>
```

```
# mdadm -D /dev/md0
```

```
/dev/md0:
Version : 00.90.03
Creation Time : Wed Dec 10 19:54:36 2008
Raid Level : raid1
Array Size : 981248 (958.41 MiB 1004.80 MB)
Used Device Size : 981248 (958.41 MiB 1004.80 MB)
Raid Devices : 2
Total Devices : 2
Preferred Minor : 0
Persistence : Superblock is persistent

Update Time : Wed Dec 10 19:55:40 2008
State : clean
Active Devices : 2
Working Devices : 2
Failed Devices : 0
Spare Devices : 0
UUID : 2affd94a6:bc8c4b06:c2eaa3:ba36d256
Events : 2
```

| Number | Major | Minor | Raid | Device State |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 8 | 17 | active sync | /dev/sdb1 |
| 1 | | 33 | active sync | /dev/sdc1 |

## 创建 RAID 5 阵

以下是创建 RAID 5 阵的步骤：

使用本章之前介绍的方法，通过 `fdisk` 或 `parted` 创建四个分区。在本演示中，假设你已经有了四个大小为 1GB 的 `/dev/sdb1`、`/dev/sdc1`、`/dev/vdd1` 和 `/dev/sdl1` 分区，且每个分区的分区 ID 类型设置为 "fd"（Linux 自动检测）。你应该能够看到这四个分区：

```
# fdisk -l
................
Disk /dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280
```

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
