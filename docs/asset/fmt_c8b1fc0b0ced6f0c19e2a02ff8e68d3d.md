
## 磁盘设备与分区管理

`/dev/sdc` — 第三个 SCSI 磁盘
`/dev/sdd` — 第四个 SCSI 磁盘

其他常见的磁盘分区：
`/dev/fd0` — 第一个软盘驱动器
`/dev/sda4` — 并口 IOMEGA Zip 驱动器

在我的计算机上，`/dev/hda` 是我的硬盘，`/dev/hdd` 是我的 CD-ROM 驱动器。`Partition Magic` 可以即时缩小、扩大、删除和创建分区。该产品与 Linux 配合工作良好，并且能识别 Linux 分区。如果你不想花钱购买商业产品，Slackware 附带了 `FIPS`。`FIPS` 是一种非破坏性的硬盘重新分区方式，就像 `Partition Magic` 一样。不过，为了以防万一，在更改分区之前请务必备份你的磁盘。

你也可以始终采用“寻杀”（Seek and Destroy）方法。这也行得通。以下是确保以稳妥方式分配磁盘空间的步骤：

1. 从你的 Windows 95、NT 或 OS/2 分区（你可能有其他兼容的操作系统）备份你的数据。如果你正在运行 Windows 95，在运行 `FIPS` 之前最好运行 Windows 碎片整理程序。
2. 删除所有分区。
3. 为其他操作系统分配至少最小空间。

> 确保为 Linux 留出至少 250 兆字节。这是实际操作系统和程序的最小需求。你还需要预留一些磁盘空间用于交换空间（在 50 到 100 兆字节之间）。

成功重新分区你的硬盘后，你就准备好继续安装 Linux 了。下一步是将 CD 插入 CD-ROM 驱动器，将启动盘插入软盘驱动器，然后重启。

> 尽管你的 Slackware CD-ROM 已经包含 `FIPS` 的副本，但由于修复了错误并增加了功能，你可能想要下载最新版本。最新的 `FIPS` 版本可在 [http://www.student.informatik.th-darmstadt.de/~schafer/figs.html](http://www.student.informatik.th-darmstadt.de/~schafer/figs.html) 获取。

## 检查安装过程

在重启过程中，你首先会看到类似 `Lilo` 或 `Loading . . .` 的内容。然后 Linux 加载驱动程序，你甚至可能会看到一些错误消息。如果这些消息是警告，请忽略它们；你稍后会对内核进行重新编译。你正在确保启动盘能识别你的 CD-ROM 并且 Linux 实际能够启动。

如果你只看到 `LI` 并且计算机在此之后死机，说明你使用了错误的启动盘（1.25 而不是 1.44）。请回到创建启动盘的步骤。

好吧，如果你能走到这一步，你应该会看到一条以以下内容开头的消息：

```text
Welcome to the Slackware Linux (v. 3.4.0) bootkernel disk!
```

以及一个提示，显示为

```text
boot:
```

除非你的计算机需要一些特殊的参数（如果你拥有特殊硬件），否则只需按下 Return 或 Enter。接下来你应该看到的行如下：

```text
Loading Ramdisk..........
```

随着驱动程序的加载，还会显示一些其他信息。下次文本停止时，你会看到以下内容：

```text
VFS: Insert root floppy disk to be loaded into ramdisk and press ENTER
```

移除启动盘，用 `color.gz`（或你选择的任意根分区包）替换为根分区盘，然后按下 Enter。你会看到另一个欢迎消息和一个提示符。在提示符处，输入 `root`（不带引号）。像这样：

```text
Slackware login: root
```

系统不会提示你输入密码。登录成功后，你会看到一个如下所示的提示符：

```text
#
```

这是 `root` 账户的提示符，意味着你对系统拥有完全控制权。一得到提示符，就为你的 Linux 分区进行格式化。

![](img/8ad518fddafc7f5e73715a2604b61d50_38_0.png)

请注意不要通过删除或格式化其他操作系统的分区来覆盖它们。

要格式化你的磁盘，请使用 Linux 命令 `fdisk`。

![](img/8ad518fddafc7f5e73715a2604b61d50_38_1.png)

请记住：从 Linux 侧发出 `fdisk` 命令，而不是从 DOS 或 Windows 分区发出。你可能之前遇到过 DOS 磁盘命令，但这并不是同一个程序！

要运行 `fdisk`，请在 `root` 提示符处输入 `fdisk`，使其看起来像这样：

```text
# fdisk
```

然后你将看到以下行：

```text
Using /dev/hda as default device!
Command (m for help):
```

这意味着它正在使用第一个 IDE 控制器上的主磁盘。如果你输入 `m`，你会得到选项列表，如下所示：

```text
Command action
a toggle a bootable flag
b edit bsd disklabel
c toggle the dos compatibility flag
d delete a partition
l list known partition types
m print this menu
n add a new partition
p print the partition table
q quit without saving changes
t change a partition's system id
u change display/entry units
v verify the partition table
w write table to disk and exit
x extra functionality (experts only)

Command (m for help):
```

我们要做的是添加一个新分区。要添加它，输入 `n`。

```text
Command (m for help): n
Command action
e extended
p primary partition (1-4)
```

按 `p`，然后选择分区号。如果你已经拥有 DOS、Windows 95 或其他操作系统，请确保指定至少 2 个分区。如果没有，你会收到一条消息，告诉你当前识别的唯一分区已被占用。接下来你会被提示指定用作新分区起始点的第一柱面。例如，它可能会说

```text
First cylinder (801-1023):
```

除非你喜欢玩弄磁盘空间的游戏，否则请告诉它 `801`。接下来你会被提示指定分区的最后柱面，这表明你想要多少空间。

```text
Last cylinder or +size or +sizeM or +sizeK (801-1023):
```

然而，告诉 `fdisk` 你想要多少空间会更快。假设你想让这个分区有 `250MB`。那么你应该输入 `+250M` 并按 Return 或 Enter。如果你的空间超过 `250MB`，请相应地输入该数值。

## 第 1 章：安装 Slackware Linux

![](img/8ad518fddafc7f5e73715a2604b61d50_40_0.png)

请确保你有足够的空间来包含一个交换分区（`swap` partition）；它的大小至少应该是你 `RAM` 的两倍。例如，对于 `32MB` 的 `RAM`，足够大的交换分区将是 `64MB`。

要创建交换空间，请遵循前面概述的创建磁盘空间的相同步骤。但是，需要额外的一步。你需要定义交换空间所属的文件系统类型；这被称为 *Linux* 交换分区。

```text
Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): l
0 Empty    9 AIX bootable   75 PC/IX    b7 BSDI fs
1 DOS 12-bit FAT a 0S/2 Boot Manag 80 01 MINIX  b8 BSDI swap
2 XENIX root   40 Venus 80286   81 Venus/MINIX c7 Syrix
3 XENIX usr   51 Novell?     82 Linux swap  db CP/M
4 DOS 16-bit <32M 52 Micropart   83 Linux native e1 DOS access
5 Extended    63 GNU HURD      93 Amoebe      e3 DOS R/O
6 DOS 16-bit >=32M 64 Novell Netware 94 Amoebe BBT   f2 DOS secondary
7 OS/2 HPFS   65 Novell Netware a5 BSD/386   ff BBT
8 AIX
Hex code (type L to list codes):
```

你可以看到 `82` 被指定为 *Linux* 交换分区。输入 `82` 并按下 Return 或 Enter 键。现在打印分区表以查看你得到的结果：
