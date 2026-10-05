

# 76 第二部分：安装 SuSE Linux

在 IDE 设备上，对于 SCSI 驱动器，磁道 1023 通常位于 512MB 标记以下，它通常低于 1GB 水平。如果你使用的是较小的磁盘，可能可能没问题。否则，在安装系统时，你可能需要考虑这个问题。确保内核位于磁道 0 到 1022 之间最简单的方法是让你的整个根分区位于第 1023 个磁道水平以下；你可以在进行磁盘分区时通过 `fdisk` 程序来指定此项。较新版本的 BIOS 支持逻辑块寻址 (LBA)，因此它们可能没有此局限性。通过使用 LBA，你可以欺骗 BIOS 认为磁盘拥有少于 1023 个磁道。

# 分区——对你的硬盘进行切分和处理

当 Linuxrc 加载 YaST 时，你会看到第一个标题为“安装类型”的对话框的提示，如前面的图 5-4 所示。由于这是你第一次安装，你应该选择“从头安装 Linux”（Installing Linux from Scratch）。接着出现的对话框将询问你是否想要分区，你应该选择“分区”（Partitioning）。YaST 会自动识别硬盘上的空闲空间，并询问你是否想将其用于安装 Linux。因为你想（或需要）自己创建分区，你应该选择“否”（如果你选择“是”，YaST 将为你你创建分区）。在“使用整个磁盘”（Use Entire Disk）的对话框中，你会被问是想进行分区还是使用整个磁盘。在这里你需要再次选择“分区”。现在你看到了一个标题为“编辑分区表”（Editing the Partition Table）的对话框，如图 5-8 所示。

![](img/96a9ce6a13d8d15ed05f867f41574278_103_0.png)

```
EDITING THE PARTITION TABLE
fdisk detected the following hard drive geometry:
/dev/hda 64 Heads 528 Sectors Cylinders.
One cylinder 206438 Bytes.

在此处，你可以看到 fdisk 程序的错误信息：

Current partition table of the selected hard disk:
Name From To Blocks Partition type
/dev/hda 1 51 102784 6 FAT16
F1=Help F3=Change type F4=Delete F5=Create
< Continue > < Abort >
```

# 第 5 章：安装：最后的冲刺

对话框会根据几点情况而略有不同。如果你的电脑中有两块硬盘，你必须首先选择要在哪块硬盘上安装 Linux。如果你要安装的硬盘上已经有一个跨越整个硬盘的分区，那么显而易见地，YaST 不会询问你是否想使用未分区的空间来安装 Linux。在这种情况下，你需要从“使用整个磁盘”中选择“分区”，然后会出现“编辑分区表”对话框，它用于编辑你的分区表（见图 5-8）。

# 编辑分区表

在“编辑分区表”对话框中，你可以查看现有分区、删除现有分区、创建新分区并更改分区类型。这些功能通过功能键（F3、F4、F5、F6）执行，如屏幕底部所示。例如，F5 键用于创建新分区。在图 5-8 中，你可以看到其中一个作者有一个 100MB 的 DOS 分区（记住，每 MB 有 1024 个块！）。

# 创建分区

在这个示例中，除了现有的 DOS 分区外，我们还创建了以下分区：

- 750MB 用于根分区
- 127MB 用于交换分区（swap partition）
- 100MB（所有剩余空间）用于主目录

要创建分区，按下 F5 功能键。下一个对话框“分区类型”（Partition Type）提示你选择分区类型，你应该选择“主分区”（Primary），如图 5-9 所示。

![](img/96a9ce6a13d8d15ed05f867f41574278_104_0.png)

# 78 第二部分：安装 SuSE Linux

如果你计划在硬盘上创建四个以上的分区，你需要创建一个创建一个扩展分区（extended partition）。在扩展分区内部，你可以创建多个逻辑分区。这种通过创建一个大型扩展分区并在其中创建多个逻辑分区的安排，并不是 Linux 的局限性，而是现代硬件的局限性。对于 Linux 而言，逻辑分区的功能与主分区没有区别。

接下来，你将看到一个可用分区的列表，你应该选择列表顶部的那个。这是一个示例，在图 5-10 中，第一个可用分区是 `/dev/hda2`。如果你正在创建一个逻辑分区，它将是 `/dev/hda6`。当你选择了想要创建的分区后，按下回车键。

在“分区位置”（Location of Partition）对话框中（见图 5-10），你需要输入你正在创建的分区的大小。自动出现的起始和结束值是你的硬盘未分区部分的第一个和最后一个磁道。

在图 5-11 中，你可以看到通过在结束磁道字段中指定该值（750 MB），我们创建了一个 750MB 的分区。指定完要创建的分区大小后，按下回车键并

```
EDITING THE PARTITION TABLE
fdisk detected the following hard drive geometry:
Disk /dev/hda 64 Heads
One cylinder 63 cylinders
/dev/hda2
/dev/h1
```

图 5-10：分区位置。大小。

# 106
第 5 章：安装：最后的冲刺

![](img/96a9ce6a13d8d15ed05f867f41574278_106_0.png)

# 修改类型

在“编辑分区表”对话框中，你可以查看现有分区、删除现有分区、创建新分区并更改分区类型。这些功能通过功能键（F3、F4、F5、F6）执行，如屏幕底部所示。例如，F5 键用于创建新分区。在图 5-8 中，你可以看到其中一个作者有一个 100MB 的 DOS 分区（记住，每 MB 有 1024 个块！）。

注意，除了选择挂载点和类型外，此对话框还有读取 fstab 和设置 Inode 密度。这些是高级选项，对于安装并不是必须的。

当你完成分区创建并将交换分区类型设置为 Linux Swap 后，你就准备好保存更改了。YaST 会确认它找到了交换分区（如果有的话），然后初始化交换分区。你会看到“创建文件系统”（Creating Filesystems）对话框，如图 5-14 所示。在对话框中，你为分区设置挂载点。

记住记录下哪些分区（如 `/dev/hda2` 或 `/dev/sdb3`）将用于文件系统，如 `/usr`、`/tmp` 或 `/`。

# 107
80 第二部分：安装 SuSE Linux

```
EDITING THE PARTITION TABLE
fdisk detected the following hard drive geometry:
Disk /dev/hda 64 Heads 528 Sectors Cylinders.
One cylinder 206438 Bytes.
```

在此处，你可以看到 fdisk 程序的错误信息：

| Name | From | To | Blocks | Partition type |
|---|---|---|---|---|
| /dev/hda | 1 | 51 | 102784 | 6 FAT16 |
| /dev/hda2 | 52 | 432 | 186096 | 83 Linux native |
| /dev/hda3 | 433 | 493 | 122976 | 83 Linux native |
| /dev/hda4 | 494 | 528 | 205630 | 83 Linux native |

# 删除分区

如果你发现需要删除某个分区，你可以使用 F4 键轻松实现。首先，你必须突出想要删除的分区；然后按下 F4。系统会询问你确认要删除该分区。如果你确定，按下回车键；如果，使用 Tab 键移动到“否”，然后按下回车键。

# 保存分区信息

当你完成分区创建并将交换分区类型设置为 Linux Swap 后，你就准备好保存更改了。按下回车键，系统将询问你是否确定将分区信息保存到磁盘上。

![](img/96a9ce6a13d8d15ed05f867f41574278_107_1.png)

