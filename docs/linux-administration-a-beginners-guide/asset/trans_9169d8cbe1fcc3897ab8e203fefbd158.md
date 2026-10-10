
# Linux 管理：入门指南

> **注意：** `e2fsck` 并不是 ext2 修复工具的正确名称；它实际上只是一个封装器。`e2fsck` 封装器会尝试确定需要修复的文件系统类型，然后运行相应的修复工具，并传递所有传给 `e2fsck` 的参数。在 ext2 中，真正的工具被称为 `e2fsck`（注：原文此处似乎存在笔误，很可能意指真正的工具是 `fsck.ext2` 或类似名称，但严格遵循“保留信息”原则，仅纠正语境清晰的*明显*OCR错误。然而，原文表述“In ext2, the real tool is called e2fsck”与前一句存在事实矛盾。我将按原样保留，除非这是明显的OCR字符错误。实际上，查阅常见书籍，这可能是源书本身的笔误。如果我是在进行解释，我会将笔误“e2fsck”更正为“fsck.ext2”，但提示要求的是OCR错误纠正。“e2fsck”并不是“fsck.ext2”的OCR错误。我将假设文本是扫描原文正确的，或者是源文件的错误。等等，仔细看标准文本，`e2fsck` 是命令。底层工具通常是 `fsck.ext2` 或 `fsck.ext3`。句子“The `e2fsck` wrapper tries to determine... and runs the appropriate repair tool... In ext2, the real tool is called `e2fsck`”在逻辑上令人困惑。让我们看下一句：“When a system crash occurs, you may need to call `e2fsck` directly”。好的，我将按原样保留文本，假设源书有此措辞。）

### e2fsck 可用参数

表 8-4 中显示的参数可用于 `e2fsck`。

例如，要在 `/dev/hda3` 文件系统上运行 `e2fsck`，你需要执行：

```bash
[root@ford ~root]# e2fsck /dev/hda3
```

若要强制检查并自动回答出现的所有提示为“是”：

```bash
[root@ford]# e2fsck -f -y /dev/hda3
```

### 如果收到错误怎么办？

首先，放松。`fsck` 检查很少会发现它无法自行纠正的问题。当它确实需要人工干预时，告知其执行默认建议通常就足够了。极少有单次 `e2fsck` 运行无法清除所有问题的情况。

| e2fsck 参数 | 描述 |
|---|---|
| -b superblock | e2fsck 应从中读取分区信息的超级块编号。在大多数情况下，e2fsck 能够在块 1 处找到它，但如果该块损坏，你需要指定一个替代编号。超级块每隔 8192 个块出现一次，因此下一个超级块位于 8193，然后是 16385，以此类推。 |
| -c | 在运行 e2fsck 之前在磁盘上运行 badblocks 程序。这会逐个块搜索整个磁盘并验证块的完整性。这是检查磁盘的一种非常彻底的方法，但它*极其*耗时。 |
| -f | 强制运行检查，即使它认为文件系统已经是干净的。 |
| -y | 告诉 e2fsck 自动假设 e2fsck 发出的所有提示都回答“是”。 |

在极少数需要第二次运行的情况下，不应再出现新的错误。如果出现了，你很可能面临的是硬件故障。记得从明显的问题开始检查：检查电源是否可靠以及电缆连接是否牢固。任何使用 SCSI 系统的人都应验证其是否使用了正确类型的终结器，电缆是否过长，SCSI ID 是否冲突，以及电缆质量是否足够。（SCSI 对电缆质量尤其挑剔。）

### /lost+found 目录

另一种罕见情况是，当 e2fsck 找到无法与原始文件重新连接的文件片段时。在这些情况下，它会将片段放入分区的 lost+found 目录中。该目录位于分区的挂载点，因此，如果 /dev/hda3 挂载在 /usr 上，则 usr/lost+found 对应于 /dev/hda3。

任何东西都可以进入 lost+found 目录——文件片段、目录，甚至特殊文件。当普通文件出现在那里时，应该会附带文件所有者，你可以联系所有者并查看他们是否需要这些数据（通常他们不需要）。如果你在 lost+found 中遇到目录，你很可能更希望尝试从最近的备份中恢复它，而不是尝试从 lost+found 中重建它。

至少，lost+found 可以告诉你是否有内容错位。再次强调，这类错误极其罕见。

## 磁盘分区

为了清晰起见，并且以防你需要知道什么是分区以及它是如何工作的，让我们简要回顾一下这个主题。每个磁盘都必须进行分区。分区将磁盘划分开，每个段本身都作为一个完整的磁盘运行。一旦分区被填满，它就不能（在没有特殊软件的情况下）自动溢出到另一个分区。

通常，对磁盘进行分区的过程实现两个目标之一。要么用户需要安装两个不同的操作系统，每个操作系统都需要自己的分区；或者，确保一个分区上的空间使用不会干扰其他分区上专门用于其他任务的空间可能是明智的。

后者的一个例子发生在用户主目录中。当系统用户不是系统管理员时，管理员必须确保用户不会将其个人文件消耗整个磁盘。这会占用日志记录和临时文件所需的存储空间，导致系统行为异常。为了防止这种情况，会为创建了一个特殊的分区用于用户文件，以便它们不会溢出到受保护的系统空间。

> **注意：** 将磁盘分区设置为只有一个大分区占据整个磁盘是可以接受的。

### 磁盘的存在位置

在 Linux 下，每个磁盘都有其自己的设备名称。IDE 磁盘以名称 /dev/hdX 开头，其中 X 可以是 a 到 z，每个字母代表一个物理设备。例如，在一个仅包含 IDE 的系统，其中有一个硬盘和一个 CD-ROM，且两者位于同一条 IDE 链路上时，硬盘将是 /dev/hda，CD-ROM 将是 /dev/hdb。磁盘设备在系统安装期间自动创建。

当创建分区时，会使用新的设备。它们的格式为 /dev/hdXY，其中 X 是设备字母（如上所述），Y 是分区号。因此，/dev/hda 磁盘上的第一个分区是 /dev/hda1，第二个分区是 /dev/hda2，依此类推。

SCSI 磁盘遵循与 IDE 相同的基本方案，除了它们以 /dev/sd 开头而不是 /dev/hd。因此，第一个 SCSI 磁盘上的第一个分区将是 /dev/sda1，第三个 SCSI 磁盘上的第二个分区将是 /dev/sdc2，依此类推。

### 创建分区

> **警告**：创建分区的过程对磁盘上已有的数据具有不可逆的破坏性。在创建、更改或删除任何磁盘上的分区之前，你必须清楚被修改磁盘上有什么，并且如果该数据仍然需要，你需要拥有备份。

在安装过程中，你很可能使用了某种“美观”的工具来创建分区。不幸的是，Linux 平台不附带用于创建和管理分区的标准实用程序。所有 Linux 发行版都存在的一种基本机制是 fdisk。尽管它很小且略显笨拙，但它是一个可靠的分区工具。此外，如果你需要排查完全出错的系统，你应该熟悉 fdisk 等基础知识。fdisk 唯一的真正缺点是缺乏用户界面。

> **注意：** 还有一个称为 gfdisk 的更易用的封装器。然而，在紧急情况下可能无法获得此工具，因此，尽管 fdisk 略显笨拙，最好还是学习如何使用它。

在本次运行中，让我们假设我们要对 /dev/hdb 设备进行分区，这是一块 340MB 的 IDE 硬盘。（是的，你没看错。）我们通过带 /dev/hdb 参数运行 fdisk 开始。

```bash
[root@ford /root]# fdisk /dev/hdb
```

这会输出一个简单的提示：

```text
Command (m for help):
```

让我们使用 m 来查看我们的选项。此菜单大致自我解释。

```text
Command (m for help): m
Command action
a toggle a bootable flag
b edit bs'd disklabel
c toggle the dos compatibility flag
d delete a partition
l list known partition types
m print this menu
n add a new partition
o create a new empty DOS partition table
p print the partition table
q quit without saving changes
s create a new empty Sun disklabel
t change a partition's system id
u change display/entry units
v verify the partition table
w write table to disk and exit
x extra functionality (experts only)
Command (m for help):
```

我们首先使用 p 命令（打印分区表）查看现有分区：

```text
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hdb1 * 1 664 334624+ 6 FAT16
Command (m for help):
```

我们这里有一个小的遗留系统，你觉得呢？是时候升级这个磁盘了——我们首先使用 d 命令（删除分区）移除现有分区：

```text
Command (m for help): d
Partition number (1-4): 1
Command (m for help):
```

然后我们使用 p（打印分区表）命令来验证结果：

```text
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
Command (m for help):
```

那里没有分区了。是时候开始创建分区了。为了讨论方便，我们将假装这块磁盘足够大，可以容纳完整的工站配置。为此，我们需要创建表 9-5 中所示的分区。

