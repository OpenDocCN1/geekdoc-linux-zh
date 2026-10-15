
NTFS 在系统启动后首次访问卷时自动执行磁盘恢复。正如你可能想到的，这意味着每次启动 Windows NT 或 Windows 2000 时都会执行恢复。然而，如果不需要恢复，该过程将退出而不执行任何操作。NTFS 恢复依赖于内存中维护的以下两个表：
- `事务表`：跟踪尚未提交的活动事务。在恢复期间，这些事务的子操作必须从磁盘中删除。
- `脏页表`：记录哪些缓存页已被修改但尚未写入磁盘。在恢复期间，这些数据必须刷新到磁盘以保持卷的一致性。

NTFS 每五秒创建一个检查点记录并存储事务表和脏页表的副本。当在故障后启动恢复时，NTFS 打开日志文件并定位最新的检查点记录以及事务表和脏页表的副本。在大多数情况下，在最新的检查点记录之后存在更新记录。此时，日志文件被加载到内存中，恢复操作在三次传递中完成：

### 分析传递
在分析传递期间，NTFS 从上次检查点操作的开始扫描日志文件到文件末尾。在此传递期间，额外更新记录中的信息用于更新事务表和脏页表的副本。在分析传递结束时，事务表和脏页表应准确反映故障发生时的状态。

### 重做传递
在重做传递期间，NTFS 从分析传递中找到的最旧记录开始向前扫描日志文件。重做传递用于定位在故障前已完成但可能未及时从缓存刷新的页更新记录。找到的每个操作都会重新提交到缓存以完成。

### 撤销传递
撤销传递用于回滚系统故障时未提交的任何操作。撤销传递完成后，卷应稳定且连贯，直到故障发生时为止。

## chkdsk

尽管 NTFS 包含内置的恢复功能，有时手动检查卷是否存在错误仍然很有用。`chkdsk` 是 NTFS 的等价于 UNIX `fsck` 实用程序。`chkdsk` 具有扫描卷以检查文件系统的能力
errors, and for physical disk errors as well. You should not have to run `chkdsk` unless you are experiencing unusual file system problems. There are two common ways to run `chkdsk`:
- To have `chkdsk` scan and repair drive C: for filesystem errors, use the following syntax:
```
chkdsk C: /f
```
- To have `chkdsk` scan and repair drive C: for filesystem and physical media errors, use the following syntax:
```
chkdsk C: /f /r
```
Keep in mind that `chkdsk` cannot operate on volumes that are currently in use. If you need to run `chkdsk` on a volume currently in use (i.e. the System partition), you should execute one of the above commands, answer yes when prompted to run `chkdsk` during the next reboot, and then reboot the system. `chkdsk` will run at the time of the next reboot.

`chkdsk` scans a volume for filesystem errors and for physical errors.

## NTFS 容错性

NTFS 是少数支持高级卷配置和容错性的文件系统之一。NTFS 符合廉价磁盘冗余阵列（`RAID`）标准。所有高级卷，除了卷集之外，都符合 `RAID` 标准。有两种非容错配置：卷集和条带集。NTFS 还提供两种容错配置：镜像集和带奇偶校验的条带集。本节将讨论所有四种配置的属性。在每种情况下，磁盘管理员用于管理各种磁盘配置。不同的 `RAID` 级别在表 4.5 中描述。

### 卷集

卷集由位于一个或多个物理卷上的最多 32 个大小不一的空闲空间区域创建。数据按顺序写入卷集，卷集的性能几乎与单个磁盘上的单个分区相同。卷集的有用之处在于它们可以在不丢失其包含的数据的情况下进行扩展。但是，卷集不提供任何容错性，如果卷集中包含的磁盘之一损坏，整个卷集将被损坏。

### 条带集

条带集由一个或多个物理卷上两个或多个大小相同的空闲空间区域创建。条带集通常由两个或多个大小相同的磁盘创建。当数据写入条带集时，它被分解为大小相等的块，并将一个块写入条带集中的每个磁盘。对条带集的读写访问非常快，因为数据是从多个磁盘（以及可能多个磁盘控制器）流式传输的。条带集不能在不丢失其中包含的数据的情况下进行扩展。条带集不提供任何容错性，因此单个磁盘故障将导致所有数据丢失。条带集对应于 `RAID` 级别 0。

| Table 4.5 RAID Levels Supported on Windows 2000 |
|---|---|
| RAID Level | Description |
| 0: (Striping) | RAID Level 0 allows you to combine two or more disks of equal size into a larger logical volume. Data is written in equal-sized chunks to each disk in the volume. There is no redundancy in this configuration, but disk reads and writes are faster because multiple disks are being accessed concurrently. |
| 1: (Mirroring) | RAID Level 1 allows data from one physical disk to be duplicated to a second physical disk. In the event that the primary disk fails, the secondary disk can take the place of the primary disk with no data loss. |
| 5: (Striping with Parity) | RAID Level 5 provides similar functionality to RAID Level 0. However, this level provides redundancy when a single disk fails. A RAID 5 volume can be established using three or more disks of equal size. The actual size of the volume will be the number of disks minus one multiplied by the size of the disk. The reason for the "loss" of one disk is to store parity information so data can be regenerated if a disk fails. While read performance is better with RAID 5, write performance is slower that RAID 0 because parity information is generated and stored with each write. |

### 镜像集

镜像集由两个大小相同的磁盘创建。在镜像集中，两个磁盘包含完全相同的数据。如果磁盘发生故障，镜像集可以被中断，好的磁盘可以上线，就像什么也没发生过一样。一旦损坏的磁盘被更换，镜像

![](img/415c89a1ede71e11e5040a0038b6916c_161_0.png)

### Figure 4.18

Computer Management MMC snap-in.
- 1. 从控制面板和/或开始菜单中的管理工具文件夹打开计算机管理 MMC 管理单元。你应该会看到图 4.18 中的窗口。
- 2. 在存储菜单下选择磁盘管理条目。如果安装了全新的磁盘（没有预定义分区），你会看到写入签名和升级磁盘向导。按照向导操作以开始安装新磁盘。完成向导后，你将看到类似图 4.19 的屏幕。
- 3. 右键单击未分配的磁盘并选择创建卷选项以启动创建卷向导。回答问题以完成创建分区、分配驱动器号然后格式化新卷所需的步骤。默认选项应足够。
- 4. 向导完成后且格式化操作结束时，你的新磁盘即可使用。

![](img/415c89a1ede71e11e5040a0038b6916c_162_0.png)

**Figure 4.19**

磁盘管理实用程序。

## Summary

## UNIX FILESYSTEMS
