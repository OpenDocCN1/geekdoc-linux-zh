
```
Athena:~ # df -h
Filesystem             Size  Used Avail Use% Mounted on
/dev/sda1              9.4G  2.2G  6.8G  25% /
tmpfs                   93M  8.0K   93M   3% /dev/shm
Athena:~ #
```

Or

```
Athena:~# cat /etc/fstab
/dev/sda1       /                 ext3    acl,user_xattr          1 1
/dev/sda2       swap              swap    pri=42                  0 0
devpts          /dev/pts           devpts  mode=0620,gid=5         0 0
proc            /proc              proc    defaults                0 0
usbfs           /proc/bus/usb      usbfs   noauto                  0 0
sysfs           /sys               sysfs   noauto                  0 0
/dev/dvd        /media/dvd         subfs   noauto                  0 0
fs=cd|ss.ro,procuid,nodev,nosuid,noexec,iocharset=utf8 0 0
/dev/fd0        /media/floppy      subfs   noauto                  0 0
fs=floppyfs,procuid,nodev,nosuid,sync 0 0
Athena:~#
```

### Fstab 格式

`fstab` 文件关联物理分区以及有关它们将如何添加到系统中的信息。`fstab` 中的每条记录分为六个不同的部分：

- 1. 第一个字段标识要挂载的块设备。这通常是你想要挂载的分区的名称（例如，`/dev/sda1`）。

- 2. 第二个字段指示分区将关联到的挂载点的名称（例如，`/home`）。

- 3. 第三个字段标识分区的

文件系统格式。SUSE 可以识别大量文件系统类型，例如 MS-DOS、`ext2`、`ext3`、`reiserfs`、CD 格式 `iso9660` 等。

- 4. 第四列包含 `mount` 命令的选项。你可以指定分区以只读方式挂载（`ro`）、以读写方式挂载（`rw`）、接受访问控制列表（`acl`）以及支持基于用户的配额（`usrquota`）。还有许多其他选项可用——有些取决于文件系统。有关这些值的更多信息可在 `mount` 命令的手册页中找到。

- 5. 第五个字段代表传递给 `dump` 实用程序的数值。`dump` 命令用于备份分区上的数据。此处指定的值通常为 `1`，表示第 1 级增量备份。此值可使用实际的备份工具覆盖。

- 6. 第六个也是最后一个字段控制文件系统在启动时检查的方式。数字表示分区检查的顺序。`/` 分区应首先检查，其值为 `1`。后续分区应具有大于 `1` 的值。由于检查的并行性质，同一设备上的分区会并发验证。

从这些列表中可以看出，系统中似乎只有一个 SCSI 磁盘（`sda`），并且它被分为两个分区——即 `/` 和一个交换分区。当添加新磁盘时，它会获得唯一的 SCSI ID，在本例中为 `1`，并将作为系统中的第二个 SCSI 磁盘出现，即 `sdb`。如果我们使用基于 IDE 的系统，磁盘将分别显示为 `hda` 和 `hdb`。

第一个步骤是决定磁盘的低级配置。分区表包含有关磁盘如何细分的的信息。创建分区表的最简单方法是使用 `fdisk` 实用程序。你通过在命令行中使用 `fdisk` 动词，后跟目标设备名称，如列表 2.1 所示，来调用此工具。必须确保将此实用程序指向正确的设备。否则可能会导致现有设备的分区表损坏。有关此实用程序的详细信息可在手册页中找到。一旦调用此动词，就可以在 `fdisk` 中使用菜单 `m` 命令列出内部命令集。此时的可能值如表 2.1 所示。

**表 2.1**

**fdisk 内部命令集**

| 命令 | 用途 |
|---|---|
| a | 切换可引导标志 |
| b | 编辑 bsd 磁盘标签 |
| c | 切换 DOS 兼容性标志 |
| d | 删除一个分区 |
| l | 列出已知分区类型 |
| m | 打印此菜单 |
| n | 添加一个新分区 |
| o | 创建一个新的空 DOS 分区表 |
| p | 打印分区表 |
| q | 不保存更改而退出 |
| s | 创建一个新的空 Sun 磁盘标签 |
| t | 更改分区的系统 ID |
| u | 更改显示/输入单位 |
| v | 验证分区表 |
| w | 将表写入磁盘并退出 |
| x | 提供额外功能（仅限专家） |

#### 警告

正确配置且完整的分区表是系统运行的强制性条件。在此阶段最好过于谨慎并三重检查你的操作。这里的一个错误可能会使你的服务器成为船锚并让你花费大量时间。确保在继续之前拥有适当的灾难恢复计划并拥有有效的备份。

以下将为新添加的磁盘创建适当的分区表：

##### 第 1 步：查看现有的分区表。

不期望新磁盘包含有效的分区表。如果有，这可能表明你将实用程序指向了错误的卷，或者你正在使用可能被意外销毁数据的磁盘。在控制台提示符下，键入 `fdisk` 后跟新卷的名称（`sdb`）：

#### 列表 2.1

一个 `fdisk` 工具会话示例

```
Athena:~ # fdisk /dev/sdb
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

The number of cylinders for this disk is set to 5221.
There is nothing wrong with that, but this is larger than 1024, and could in certain cases cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
   (e.g., DOS FDISK, OS/2 FDISK)
Warning: invalid flag 0x0000 of partition table 4 will be
corrected by w(rite)
Command (m for help):
```

打印出此磁盘当前分区表的副本：

```
Command (m for help): p

Disk /dev/sdb: 42.9 GB, 42949672960 bytes
255 heads, 63 sectors/track, 5221 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
```

```
   Device Boot    Start       End    Blocks   Id  System

Command (m for help):
```

打印命令显示一个没有预先存在分区表的设备。你现在可以继续并对磁盘进行细分。在本例中，将创建一个分区来包含用户的 home 目录（`/home`），并创建另一个分区来保存 Web 内容文件夹的根目录（`/srv`）。为此目的，将磁盘大致均分为两半。

##### 第 2 步：创建 2 个分区
