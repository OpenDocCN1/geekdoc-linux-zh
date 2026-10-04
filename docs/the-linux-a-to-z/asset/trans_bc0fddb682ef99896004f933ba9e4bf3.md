
在本节的剩余部分，我假设你拥有一块 320 MB 的 IDE 硬盘，其分区方式如第 7.1 图示例所示，且 DOS 分区已创建并装入了你的 DOS 软件。我还假设你希望从 Slackware 发行版安装 A、AP、D、K、N、F、X、XAP 和 Y 软件集，并且你的安装介质为软盘（尽管安装过程本质上与任何其他安装介质相同：CD-ROM、硬盘或网络）。

准备好启动盘和根盘后，你应插入启动盘并重新启动机器。大多数发行版，包括 Slackware，都提供一个启动盘，可在提示后让你输入硬件配置详情。这只有在启动盘内核未能检测、正确识别或配置特定硬件设备这种不太可能的情况下才有必要。

我们的示例配置不应出现问题，因此你只需在提示时按 Enter 或 Return 键继续启动序列。过一会儿，你会被提示取出启动盘，换上根盘并按 Enter 或 Return 键完成初始启动序列。

此时，你将拥有一个最小的 Linux 系统，完全在内存中运行，使用 ramdisk 作为其根文件系统，如果一切顺利，你应该会看到 Login: 提示符。现在，以 root 身份登录。该账户未设置密码，因此你可以直接登录。

按惯例（本书示例中我将遵循此惯例），系统管理员或超级用户获得的提示符包含或至少以井号（#）符号结尾。在提示符中使用时，将井号符号专用于此目的是个好主意——这有助于避免混淆。

为了设置 Linux 分区，你需要在井号提示符下运行 fdisk，其输出如下：

```
# fdisk
Using /dev/hda as default device!

Command (m for help):
```

文件名 /dev/hda 是对应于第一块硬盘驱动器的整个设备的特殊文件名（SCSI 磁盘为 /dev/sda）。这是 fdisk 默认尝试操作的驱动器。如果你有第二块硬盘，可以通过将第二个驱动器的设备特殊文件的路径名（/dev/hdb 或 /dev/sdb）作为参数指定给命令，使 fdisk 改为操作它：

```
# fdisk /dev/hdb
```

在 Linux 下，每个磁盘驱动器和分区在 /dev 中都有一个名称。这些名称如下所示：

- hda 整个硬盘 1；
- sda 整个 SCSI 硬盘 1；
- hdb 整个硬盘 2；
- sdb 整个 SCSI 硬盘 2；
- fd0 整个软盘驱动器 0（DOS A：）；
- fd1 整个软盘驱动器 1（DOS B：）。

任何硬盘上的分区只需在整个驱动器的名称后加上适当的数字即可访问。下表显示了如何为驱动器 hda 命名分区：

- hda1 硬盘 1，主分区 1；
- hda2 硬盘 1，主分区 2；
- hda3 硬盘 1，主分区 3；
- hda4 硬盘 1，主分区 4；
- hda5 硬盘 1，逻辑分区 1；
- hda6 硬盘 1，逻辑分区 2；
- hda7 硬盘 1，逻辑分区 3，等等。

Linux 的 fdisk 命令与 DOS 的等价命令看起来不同，但它们执行的功能相似。你可以在 fdisk 运行后使用 ‘m’ 命令获取功能列表：

```
# fdisk
Using /dev/hda as default device!

Command (m for help): m
Command action
  a  toggle a bootable flag
  c  toggle the dos compatibility flag
  d  delete a partition
  l  list known partition types
  m  print this menu
  n  add a new partition
  p  print the partition table
  q  quit without saving changes
  t  change a partition's system id
  u  change display/entry units
  v  verify the partition table
  w  write table to disk and exit
  x  extra functionality (experts only)
```

在此阶段明智的做法是使用 ‘p’ 命令显示现有分区表，以检查 DOS 分区是否已正确设置：

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes

    Device Boot Begin Start  End Blocks Id System
    /dev/hda1   *       1     1   511 163812+  6  DOS 16-bit >=32M
```

已设置好，因此现在可以设置 Linux 分区，从 /dev/hda2 上的交换空间开始。你使用 ‘n’ 命令添加新分区，然后 fdisk 会询问你是否要创建主分区或扩展分区。在我们的示例中，我们需要主分区，因此你应在此提示下回答 ‘p’。然后会询问你要使用哪个分区号，你应回答 ‘2’。fdisk 的下一个问题要求你指定新分区应从哪个磁盘柱面开始。回答此问题时，你应给出 DOS 分区之后的下一个空闲柱面号。这里为 512。最后一个问题要求你指定新分区结束的位置。这可以给出柱面号，也可以直接指定分区的大小，单位为字节、千字节或兆字节。要指定一个 16 Mb 的交换分区，你应回答 ‘+16M’。整个序列如下所示：

```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)

p
Partition number (1-4): 2
First cylinder (512-1023): 512
Last cylinder or +size or +sizeM or +sizeK (512-1023): +16M
```

顺便说一下，没有什么可以阻止你拥有多个交换分区。例如，如果你有多于一块硬盘，那么这种安排可能最方便。

创建用于交换空间的分区后，可以对 /dev/hda3 上的 Linux 根分区执行类似的序列：

```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)

p
Partition number (1-4): 3
First cylinder (564-1023): 564
Last cylinder or +size or +sizeM or +sizeK (512-1023): 1023
```

在此序列结束时执行 ‘p’ 命令将确认一切按计划进行：

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes
```

| 设备 | 启动 | 起始 | 开始 | 结束 | 块数 | Id | 系统 |
|---|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 1 | 511 | 163812+ | 6 | DOS 16位 >=32M |
| /dev/hda2 |  | 512 | 512 | 563 | 16640 | 83 | Linux 原生 |
| /dev/hda3 |  | 564 | 564 | 1023 | 147200 | 83 | Linux 原生 |

看起来不错。然而，还有一件事情需要完成。分区 2 的系统类型仍标记为 Linux 原生，而应为 Linux 交换。这可以通过使用 ‘t’ 命令将 Id 从 83 切换到 82 来纠正。我怎么知道数字应该是多少？你可以在使用 ‘t’ 命令时让 fdisk 给出一个列表：

```
Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): L
```

|  |  |  |  |
|---|---|---|---|
| 0 空 | 8 AIX | 75 PC/IX | b7 BSDI fs |
| 1 DOS 12位 FAT | 9 AIX bootable | 80 Old MINIX | b8 BSDI swap |
| 2 XENIX root | a OS/2 Boot Man | 81 Linux/MINIX | c7 Syrinx |
| 3 XENIX usr | 40 Venix 80286 | 82 Linux swap | db CP/M |
| 4 DOS 16位 <32M | 51 Novell? | 83 Linux native | e1 DOS access |
| 5 Extended | 52 Microport | 93 Amoeba | e3 DOS R/O |
| 6 DOS 16位 >=32M | 63 GNU HURD | 94 Amoeba BBT | f2 DOS sec |
| 7 OS/2 HPFS | 64 Novell | a5 BSD/386 | ff BBT |
| Hex code (type L to list codes): 82 |  |  |  |

现在，终于，分区表应已按要求设置好。最后再看一眼以确保无误：

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes
```

| 设备 | 启动 | 起始 | 开始 | 结束 | 块数 | Id | 系统 |
|---|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 1 | 511 | 163812+ | 6 | DOS 16位 >=32M |
| /dev/hda2 |  | 512 | 512 | 563 | 16640 | 82 | Linux 交换 |
| /dev/hda3 |  | 564 | 564 | 1023 | 147200 | 83 | Linux 原生 |
