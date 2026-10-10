
## fdisk 操作（基于流程隐含上下文）
p 命令显示磁盘当前的分区方案：

```
Command (m for help): p

Disk /dev/sda: 10.7 GB, 10737418240 bytes, 20971520 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000528e6

Device Boot    Start      End    Blocks  Id  System
/dev/sda1            2048  2099199  1048576 83 Linux
/dev/sda2         2099200  20971519  9436160 83 Linux
```

```
Command (m for help):
```

在此示例中，/dev/sda 磁盘被划分为两个分区：sda1 和 sda2。Id 和 System 列指的是该分区格式化以处理的文件系统类型。我们将在本章稍后的“理解文件系统”部分对此进行详细介绍。这两个分区都格式化为支持 Linux 文件系统。第一个分区分配了约 1 GB 的空间，而第二个分区分配了略多于 9 GB 的空间。

fdisk 命令功能较为原始，因为它不允许修改现有分区的大小；你所能做的只有删除现有分区并从头重建它。

若要从某个分区启动系统，你必须为该分区设置启动标志。你使用 a 命令来执行此操作。在输出列表中，可启动的分区会用星号（*）表示。

如果你对磁盘分区进行了任何更改，必须使用 w 命令退出，以便将更改写入磁盘。

## gdisk 操作

如果你在使用采用 GPT 索引方法的磁盘，你需要使用 gdisk 程序：

```
$ sudo gdisk /dev/sda
[sudo] password for rich:
GPT fdisk (gdisk) version 1.0.3

Partition table scan:
    MBR: protective
    BSD: not present
    APM: not present
    GPT: present
```

找到带有保护性 MBR 的有效 GPT；使用 GPT。

Command (? for help):

`gdisk` 程序会识别磁盘上使用的格式化类型。如果磁盘当前未使用 GPT 方法，`gdisk` 会提供选项将其转换为 GPT 磁盘。

转换磁盘指定方法时要小心。你选择的方法必须与系统固件（BIOS 或 UEFI）兼容。否则，你的磁盘将无法启动。

![](img/c0a399aca0d18f8822d714ad0a173123_400_0.png)

`gdisk` 程序还使用自己的命令提示符，允许你输入命令来操作磁盘布局，如表 11.2 所示。

### 常用 `gdisk` 命令

| 命令 | 描述 |
| :------ | :---------- |
| b | 将 GPT 数据备份到文件。 |
| c | 更改分区名称。 |
| d | 删除分区。 |
| i | 显示分区的详细信息。 |
| l | 列出已知的分区类型。 |
| n | 添加新分区。 |
| o | 创建一个新的空 GUID 分区表 (GPT)。 |
| p | 打印分区表。 |
| q | 退出不保存更改。 |
| r | 恢复和转换选项（仅限专家）。 |
| s | 排序分区。 |
| t | 更改分区类型代码。 |
| v | 验证磁盘。 |
| w | 将表写入磁盘并退出。 |
| x | 扩展功能（仅限专家）。 |
| ? | 打印此菜单。 |

你会发现，许多 gdisk 命令与 fdisk 程序中的命令相似，这使得在两个程序之间切换变得更加容易。其中一个可能很有用的新增选项是 i 选项，它可以显示关于分区的更详细信息：

```
Command (? for help): i
Partition number (1-3): 2
Partition GUID code: 0FC63DAF-8483-4772-8E79-3D69D8477DE4 (Linux filesystem)
Partition unique GUID: 5E4213F9-9566-4898-8B4E-FB8888A8DDE78
First sector: 1953792 (at 954.0 MiB)
Last sector: 26623999 (at 12.7 GiB)
Partition size: 24670208 sectors (11.8 GiB)
Attribute flags: 0000000000000000
Partition name: ''

Command (? for help):
```

## GNU parted 命令

GNU parted 程序提供了另一种命令行界面来处理磁盘分区：

```
$ sudo parted
GNU Parted 3.2
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sda: 15.6GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
```

| 编号 | 起始 | 结束 | 大小 | 文件系统 | 名称 | 标志 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1049kB | 1000MB | 999MB | fat32 | | boot, esp |
| 2 | 1000MB | 13.6GB | 12.6GB | ext4 | | |
| 3 | 13.6GB | 15.6GB | 2000MB | linux-swap(v1) | | |

```
(parted)
```

parted 程序的一个卖点功能是它允许你修改现有分区的大小，因此你可以轻松地缩小或扩展磁盘上的分区。

GNU parted 软件包还包含 partprobe 实用工具。partprobe 命令触发 Linux 系统重新读取特定磁盘的分区表。虽然在具有本地硬盘的系统上这不是必需的，但共享磁盘的系统可能需要使用此工具，如果一个系统更新了硬盘的分区表而另一个系统尚未知晓此更新的情况。

## 图形化工具

如果你正在图形桌面环境中工作，也可以使用一些图形化工具。其中最常见的是 GNOME 分区编辑器，称为 GParted。图 11.1 展示了在 Ubuntu 桌面环境中运行 gparted 命令的示例。

![](img/c0a399aca0d18f8822d714ad0a173123_402_0.png)

gparted 窗口每次显示系统中一个磁盘，并以图形布局展示该磁盘包含的所有分区。你右键单击分区以选择挂载或卸载、格式化、删除或调整分区大小的选项。

虽然完全可以以原始设备的方式与磁盘交互，但这通常不是 Linux 应用程序的工作方式。尝试读取和写入原始设备的数据需要大量的工作。相反，Linux 提供了一种方法来为我们处理所有繁琐的工作，我们将在下一节中介绍它。

## 理解文件系统

就像在壁橱里存放物品一样，在 Linux 系统中存储数据也需要某种组织方法才能高效。Linux 利用文件系统来管理存储在存储设备上的数据。文件系统利用一种方法来维护地图，以定位放置在存储设备中的每个文件。本节及后续章节描述了 Linux 文件系统，并展示了如何定位其中包含的文件和文件夹。

Linux 文件系统可能是操作 Linux 时最令人困惑的方面之一。在磁盘、CD 和 USB 存储棒上定位文件起初可能是一个挑战。

如果你熟悉 Windows 如何管理文件和文件夹，你就知道 Windows 为连接系统的每个存储设备分配驱动器号。例如，Windows 使用 C: 作为系统主驱动器，或使用 E: 作为插入系统的 USB 存储棒。

在 Windows 中，你习惯看到如下的文件路径：

```
C:\Users\rich\Documents\test.doc
```

此路径指示该文件位于用户 rich 的 Documents 文件夹中，该文件夹存储在分配了字母 C（通常是系统第一个驱动器）的磁盘分区上。

Windows 路径确切地告诉你文件存储在哪个物理设备上。然而，Linux 不使用此方法来引用文件。它使用虚拟目录结构。虚拟目录将安装在系统上的所有存储设备的文件路径合并到单一的目录结构中。

### 虚拟目录

Linux 虚拟目录结构包含一个根目录，称为根目录（root directory）。根目录根据其到达的文件夹路径列出其下方的文件和文件夹，类似于 Windows 的做法。

![](img/c0a399aca0d18f8822d714ad0a173123_403_0.png)

> **请注意这里的术语。** 尽管 Linux 中的主要管理员用户账户称为 *root*，但这与虚拟 *目录* 的 *root* 无关。它通常被称为 *root*，但表示为 *单个前向斜杠 (/)*。实际上，root 用户账户使用特殊的 Home 目录 /root，这使得事情变得更加混乱！

例如，一个 Linux 文件路径可能如下所示：

```
/home/rich/Documents/test.doc
```

首先，请注意 Linux 路径使用前向斜杠，而不是 Windows 使用的后向斜杠。这是一个让许多 Linux 新手管理员感到困惑的重要差异。就路径本身而言，还请注意没有驱动器号。路径仅指示文件 test.doc 存储在用户 rich 的 Documents 文件夹中；它没有提供任何关于哪个物理设备包含该文件的线索。

Linux 使用 *挂载点* 将物理设备放入虚拟目录中。挂载点是虚拟目录中的一个文件夹占位符，指向特定的物理设备。图 11.2 演示了此机制的工作原理。

