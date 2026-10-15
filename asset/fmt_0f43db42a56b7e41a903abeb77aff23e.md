
6. A. 输入`useradd -c "Mike Huffman" -m -p "3X.N3pL9U8HNM" mhuffman`将创建`mhuffman`用户账户，将注释字段设置为`"Mike Huffman,"`，创建主目录(`-m`)，并将用户的加密密码设置为`3X.N3pL9U8HNM`。

7. B. 在shell提示符下输入`usermod -l "dnelson" -c "Diana Nelson" dgrow`将把`dgrow`用户账户重命名为`dnelson`。

8. C. 输入`userdel -r jcarr`将删除`jcarr`的账户并删除其主目录。

9. D. `/etc/group`文件存储组信息。

10. B. 在shell提示符下输入`groupmod -A "mhuffman,dnelson,jcarr" editors`将把`mhuffman`、`dnelson`和`jcarr`用户账户添加到`editors`组中。

11. D. 输入`groupmod -R "dnelson" editors`将把`dnelson`用户账户从`editors`组中移除。

## 管理 Linux 文件系统

在本章中，您将要学习：

- 管理磁盘分区
- 挂载可移动媒体
- 备份数据

是时候深入挖掘并真正开始操作 Linux 了！本章之前的所有章节都旨在构建您将在本书其余部分中使用的知识和技能基础。在本章中，我们将应用您迄今为止所学的知识，学习如何在 Linux 系统上管理分区和文件系统。

> **考试提示** 请做好充分准备，在 LPIC-1/CompTIA Linux+ 考试中，本章可能会受到非常严格的考察。根据您参加测试时获得的考试形式不同，您可能会发现仅本章就占考试题目的 15–20 百分比。

让我们从讨论如何管理 Linux 磁盘分区开始本章的内容。

## 管理磁盘分区

当您最初安装 Linux 系统时，您在硬盘上定义了一系列分区来托管您的文件系统。根据您安装的发行版不同，您很可能使用了某种图形界面或菜单驱动的分区实用程序来完成此任务。

系统使用一段时间后，您很可能在某个时间点需要增加更多的存储空间。如果您在系统中安装了新的硬盘，您将需要对其进行分区并在其上创建文件系统。为此，大多数发行版都为您提供某种图形分区实用程序。例如，在 OpenSUSE 系统上，您可以使用`YaST`分区模块来管理系统上的分区。该实用程序如图 10-1 所示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_401_0.png)

图 10-1 使用`YaST`管理磁盘分区

这些实用程序非常有效；但是，为了通过 LPIC-1/CompTIA Linux+ 认证考试，您必须知道如何从命令行管理分区。在本章的这一部分，您将学习以下内容：

- 使用`fdisk`管理磁盘分区
- 使用`mkfs`构建文件系统
- 理解 LVM
- 使用`mount`挂载分区
- 维护 Linux 文件系统

让我们开始学习如何使用`fdisk`。

### 使用 fdisk 管理磁盘分区

`fdisk`实用程序用于在 shell 提示符下通过命令行查看、创建或删除分区。若要使用`fdisk`创建新分区，首先打开一个终端会话。然后，在 shell 提示符下，通过输入`su -`并随后输入您的 root 用户密码来切换到 root 账户。

在 shell 提示符下，输入`fdisk 设备`。例如，如果您想管理系统中第一个硬盘上的分区，您将输入`fdisk /dev/sda`。此时，您需要输入一个命令来告诉`fdisk`您希望对硬盘做什么。

> **提示** 您可以在命令提示符下输入`m`来显示所有可用命令的列表。

例如，要查看硬盘上分区的列表，您可以输入`p`。如以下示例所示：

```
wsl: ~ # fdisk /dev/sda
WARNING: DOS-compatible mode is deprecated. It's strongly recommended to switch off the mode (command 'c') and change display units to sectors (command 'u').

Command (m for help): p

Disk /dev/sda: 42.9 GB, 42949672960 bytes
255 heads, 63 sectors/track, 5221 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00095821

Device Boot Start End Blocks Id System
/dev/sda1 * 14 103424 83 Linux
Partition 1 does not end on cylinder boundary.
/dev/sda2 14 274 2096128 82 Linux swap / Solaris
Partition 2 does not end on cylinder boundary.
/dev/sda3 274 1319 8386560 83 Linux
/dev/sda4 1319 1711 3148000 83 Linux

Command (m for help):
```

> **注意** 您也可以在 shell 提示符下输入`fdisk 设备 -l`来显示指定硬盘的分区表。输出类似于此处显示的内容。

在下一个示例中，系统中安装了新的硬盘（`/dev/sdb`），并且正在使用`fdisk`创建分区：

```
tur@wsl:~/Desktop> su -
Password:
wsl: ~ # fdisk /dev/sdb
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x165e0d41.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)
```

#### 使用 mkfs 构建文件系统

尽管我们已使用`fdisk`创建了分区，但目前还无法使用它。这是因为该分区尚未使用文件系统格式化。这需要借助若干命令之一来完成。在本章的这一部分中，我们将探讨以下主题：

- 使用`mkfs`
- 使用`mkreiserfs`
- 创建`xfs`和`vfat`文件系统
- 使用`mkswap`

##### 使用 mkfs

`mkfs`实用程序用于在分区上创建`ext2`、`ext3`或`ext4`文件系统。你甚至可以使用它在分区上创建`FAT`文件系统（Windows 和 DOS 使用的文件系统）。该实用程序实际上只是用于创建每种特定类型文件系统的真实命令的前端：

- `/sbin/mkfs.minix`
- `/sbin/mkfs.ntfs`
- `/sbin/mkfs.bfs`

警告：DOS 兼容模式已弃用。强烈建议关闭该模式（命令`c`）并将显示单位更改为扇区（命令`u`）。

命令 (`m` 表示帮助):

请注意，由于这是系统中的新磁盘，必须使用磁盘标签对其进行初始化。当你加载程序时，`fdisk`实用程序会帮你完成此操作。但是，除非你写入磁盘，否则这些更改不会生效。

在`fdisk`运行时，你会看到一个`Command:`提示符，可以使用它来输入`fdisk`命令。此时，最好做的事情之一就是输入`m`来查看`fdisk`帮助。这样做时，会显示一个命令列表，你可以使用这些命令通过`fdisk`执行操作。本示例中展示了这些命令：

```text
Command (m for help): m
Command action
a	切换可引导标志
b	编辑 bsd 磁盘标签
c	切换 dos 兼容性标志
d	删除一个分区
l	列出已知的分区类型
m	打印此菜单
n	添加一个新分区
o	创建一个新的空 DOS 分区表
p	打印分区表
q	退出不保存更改
s	创建一个新的空 Sun 磁盘标签
t	更改分区的系统 id
u	更改显示/输入单位
v	验证分区表
w	将表写入磁盘并退出
x	额外功能 (仅限专家)
```

命令 (`m` 表示帮助):
