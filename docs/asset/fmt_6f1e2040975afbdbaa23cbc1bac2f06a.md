
`c7t2d0` DEGRADED 0 0 0 (resilvering)

4. 再次检查重银的状态。这次已完成，`rpool` 已恢复为双磁盘镜像在线状态。

```
root@solaris:~# zpool status

pool: rpool

state: ONLINE

scan: resilvered 32.4G in 0h9m with 0 errors on Mon Oct 27 06:40:15 2014

config:

NAME STATE READ WRITE CKSUM

rpool ONLINE 0 0 0

mirror-0 ONLINE 0 0 0

c7t1d0 ONLINE 0 0 0

c7t2d0 ONLINE 0 0 0

errors: No known data errors

root@solaris:~#
```

5. 使用 `format` 命令及其 `verify` 子命令检查新磁盘是否已格式化、切片，并且包含用于引导分区信息的 slice 0。在以下 `format` 显示中，原系统磁盘为磁盘 0，新添加的磁盘为磁盘 1。

```
root@solaris:~# format

Searching for disks...done

AVAILABLE DISK SELECTIONS:

0. c7t1d0 <ATA-ST1000DM003-1CH1-CC49-931.51GB>

/pci@0,0/pci103c,1609@11/disk@1,0

1. c7t2d0 <ATA-ST1000DM003-1CH1-CC49-931.51GB>

/pci@0,0/pci103c,1609@11/disk@2,0

Specify disk (enter its number): 1

selecting c7t2d0

[disk formatted]

/dev/dsk/c7t2d0s1 is part of active ZFS pool rpool. Please see zpool(1M).

FORMAT MENU:

disk - select a disk

type - select (define) a disk type

partition - select (define) a partition table

current - describe the current disk

format - format and analyze the disk

fdisk - run the fdisk program

repair - repair a defective sector

label - write label to the disk

analyze - surface analysis

defect - defect list management

backup      - search for backup labels

verify      - read and display labels

inquiry     - show disk ID

volname     - set 8-character volume name

!<cmd>      - execute <cmd>, then return

quit

format> verify
```

Volume name = <          >
ascii name = <ATA-ST1000DM003-1CH1-CC49-931.51GB>
bytes/sector = 512
sectors = 1953525167
accessible sectors = 1953525134

| Part | Tag | Flag | First Sector | Size | Last Sector |
| 0 | BIOS_boot | wm | 256 | 256.00MB | 524543 |
| 1 | usr | wm | 524544 | 931.26GB | 1953508750 |
| 2 | unassigned | wm | 0 | 0 | 0 |
| 3 | unassigned | wm | 0 | 0 | 0 |
| 4 | unassigned | wm | 0 | 0 | 0 |
| 5 | unassigned | wm | 0 | 0 | 0 |
| 6 | unassigned | wm | 0 | 0 | 0 |
| 8 | reserved | wm | 1953508751 | 8.00MB | 1953525134 |

```
format>quit

root@solaris:~#
```

6. 我们可以从前面的 `format verify` 看出，新磁盘已格式化、切片，并且包含用于引导分区信息的 slice 0。现在我们需要使新磁盘可引导。

```
root@solaris:~# /usr/sbin/bootadm install-bootloader

root@solaris:~#
```

## 练习 24.12

为测试镜像对中新硬盘的可用性，优雅地关闭机器。然后断开并移除机器上的第一块引导盘。最后，仅使用新硬盘重新启动机器。成功重启后，你附加第二块硬盘作为镜像的池的状态是什么？完成此练习后，你可以更换原始引导盘并正常引导。是否执行剩余步骤由你自行决定。

7. 如果你想保留此双磁盘镜像，则停止。如果想从池中分离第二块硬盘，从而销毁镜像，请执行以下操作：

```
root@solaris:~# zpool detach rpool /dev/dsk/c7t1d0

root@solaris:~#
```

结论：你已使用 `zpool attach` 用另一块等大小的硬盘创建了引导盘的双磁盘镜像。此外，你已使用

用于检查你添加的新磁盘完整性的 `format` 命令子命令。

## 示例 24.4：PC-BSD 上硬盘的镜像

### 目标：

将启动盘（有时称为系统盘）镜像到另一块硬盘上，该硬盘是在 PC-BSD 初始构建后的某个时间添加到系统中的。

### 简介：

以下示例演示了用户可以执行的最重要的磁盘维护过程之一：使用 `zpool attach` 镜像物理设备。在示例中，我们将 PC-BSD 启动盘镜像到另一块大小相同（或更大）的硬盘上。

这很重要，因为如果其中一块硬盘（可能是你的原始系统盘）发生故障，你的机器中会有一份精确的、可引导的副本，你可以用它重新启动系统。该系统盘上可能还包含你所有的用户数据集。然后，你可以更换故障磁盘，并通过几个简单的 ZFS 步骤恢复系统的完整性和冗余性，而无需将其离线！

此示例实现了与第 23 章中介绍的 Clonezilla Live 程序相同的功能，但有一个显著区别。Clonezilla Live 仅在某个离散时间点“克隆”整个磁盘（包括引导扇区），而将 ZFS `zpool attach` 应用于包含系统盘的镜像对，则会创建系统盘及其上任何其他数据集的持续镜像“克隆”。这一点至关重要，因为你永远不知道系统盘何时会发生故障。你可以像第 23 章和本章所示的那样，设置任意数量的备份方案，使用 `rsync` 或 `zfs snapshot` 通过滚动增量备份来保存用户数据集。但本示例的方法允许你在整个系统运行和活动期间，始终拥有一个精确的完整系统克隆。

当然，要实现此处所示的功能，更高级且必然更复杂的技术会涉及多块磁盘，包括单独的系统盘、更高级别的 RAIDZ 数据集磁盘，甚至保存 ZIL 的磁盘。

如果在过程中任何地方出错，你始终可以通过执行示例末尾显示的清理步骤重新开始。根据你在过程中进行的程度，你还可以使用 `gpart` 命令重新格式化新磁盘，然后从头开始。

### 先决条件：

1. 使用 PC-BSD。
2. 你之前已完成示例 24.3。
3. 你已正确连接并将第二块硬盘安装到系统中，该硬盘未分区，但可能带有 GPT 分区方案和分区表。它还应足够大，能够容纳我们将要使用的原始系统盘分区上的所有内容。
4. 你之前已使用第 24.2.1 节中的“一种快速简便的方法来找出系统上实际安装磁盘的逻辑设备名称”确定了逻辑设备名称及其完整路径。我们的原始硬盘（装有操作系统和所有文件的启动盘）以及我们要镜像到的第二块硬盘的完整逻辑设备名称（包括这些磁盘上的相应分区）分别是 `/dev/ada0s1` 和 `/dev/ada1p3`。在你的系统上，它们可能不完全相同，但会非常相似。
5. `tank`（我们 PC-BSD 默认系统池的名称）的字节大小小于或等于你将镜像 `tank` 到的第二块硬盘上分区的大小。

### 步骤：

按所示顺序执行以下步骤以达到目标。

1. 成为超级用户。

```
[bob@pcbsd-5867] ~# su

Password: xxx

[bob@pcbsd-5867] ~#
```

2. 在之前确定新硬盘的逻辑设备名为 `ada1` 后，你应删除与其上可能已存在的所有分区关联的 ZFS 元数据。这也会清除 `ada1` 上的分区。

```
