
- 输入以下命令进入包含 MS-DOS 工具的目录：

```
C:\> F: (使用你的 CD-ROM 驱动器号。） F:\> CD DOSUTILS
```

- 使用以下命令启动 Linux：

```
F:\DOSUTILS> AUTOBOOT
```

## 安装 Linux

安装可能是一个复杂的过程，因此我们将其分解。每一系列安装步骤都包含在一个章节中。如果你按照顺序操作，你应该能够在你的电脑上安装 Linux。

### 第一阶段：开始安装

Linux 安装程序现在接管了工作。实际上，你启动了一个非常精简的 Linux 操作系统，它足够智能可以运行安装程序。安装程序会自动运行，如下：

- 安装程序首先询问你是否有彩色显示器。使用 Tab 键在“是”和“否”之间移动。当光标位于正确答案时，按回车。

- 随后会出现启动界面，给出软件描述，以及指向 Red Hat 网页的链接：

```
http://www.redhat.com
```

按回车继续。

> TIP 在安装过程中，你可以随时通过 Alt+F3 查看安装日志。通过 Alt+F4 查看内核消息。程序生成的任何消息都会将其输出到通过 Alt+F5 访问的屏幕。

- 你可以按 Alt+F1 返回主安装窗口。还有一个 Shell 窗口，你可以通过 Alt+F2 查看。可用的屏幕如下：

### 快捷键屏幕

| | |

|---|---|

| Alt+F1 | 主安装 |

| Alt+F2 | Shell |

| Alt+F3 | 安装日志 |

| Alt+F4 | 内核消息 |

| Alt+F5 | 程序输出 |

> 提示 所有的安装问题和解答都显示在主屏幕上。其他屏幕用于信息和特殊用途。在正常安装期间，你不需要查看它们。

- 4. 系统向你显示一个键盘列表。选择属于你系统的键盘，然后按回车。

- 5. 接下来，系统会询问你是否需要 PCMCIA 支持。如果你是从笔记本电脑进行安装，且要安装的设备是 PCMCIA 插槽，请回答 Yes。对于大多数系统，答案是 No。

- 6. 接下来的问题涉及安装介质。由于你购买这本书时附带了 CD-ROM，假设你的第一次安装是来自 CD-ROM。使用方向键选择介质。当正确的介质被高亮时，按回车。

- 7. 软件要求你将 CD-ROM 放入驱动器中。完成后按回车。

### 第二阶段：准备硬盘

Linux 安装过程现在已经知道从哪里获取软件，但它需要一个硬盘来存放它们。在这个阶段，你将对硬盘进行分区和格式化，并执行一些基本的磁盘配置。按照以下步骤继续安装：

- 1. 安装程序询问这是新安装还是升级。你正在进行安装，所以选择 Install。

- 2. 下一个屏幕询问你是否有任何 SCSI 设备。如果你回答 Yes，系统会向你询问 SCSI 控制器信息，然后将其配置到系统中。

- 3. 你现在到达了分区磁盘（Partition Disks）菜单，如图 2-1 所示。

除非你已经使用 Linux 对磁盘进行了分区（FIPS 不算），否则你现在需要对它们进行分区。如果你已经使用 Linux 划分了分区，可以选择 Done 并继续第 4 步。

![](img/d86aa78922e215fd387e0c1556445cac_63_0.png)

**图 2-1** 分区磁盘菜单

> ALL FIPS 会将你的 MS-DOS 分区分为两部分，一个用于 MS-DOS，一个用于 Linux。Linux 分区需要再次划分为 Linux 文件系统和交换分区（swap partition）。

某些应用程序你可能需要一个更大的 Linux 交换分区。

- 4. 使用 Tab 键进入滚动列表。使用方向键选择你想要分区的磁盘。按回车启动磁盘分区工具。

- 5. 你需要创建一个类型为 82 的分区（Linux swap），包含约 30 到 50MB，以及一个类型为 83 的分区（Linux native），并包含至少 100MB。以下列表显示了一个典型的分区过程：

此磁盘的磁道（cylinders）数设置为 4092。这比 1024 大，可能会导致以下问题：

- 1) 在启动时运行的软件（例如 LILO）

- 2) 从其他操作系统启动并分区软件（例如 DOS DISK，OS/2 DISK）

要做的第一件事是获取帮助。你可以通过 `m` 命令获取帮助。（为什么 `m` 被翻译为 help？某些错综复杂的脑回路将其与 menu 联系在一起。）

```
Command (m for help): m
Command action
  a toggle a bootable flag
  b edit bsd disklabel
  c toggle the dos compatibility flag
  d delete a partition
  l list known partition types
  m print this menu
  n add a new partition
  p print the partition table
  q without saving changes
  t change a partition's system id
  u change display/entry units
  v verify partition table
  w write table to disk and exit
  x extra functionality (experts only)
```

下面的示例显示了为 Linux 对整个磁盘进行分区。交换分区（编号 1）从磁道 1 开始，延伸 200 个磁道。根分区（编号 2）占据磁盘的剩余部分。

你需要为 Linux 交换分区创建一个新分区，因此使用新分区命令：`n`。当你在命令提示符处使用 `n` 时，结果如下：

```
Command (m for help): n
Command action
  e extended
  p primary partition (1-4)
```

程序正在询问你是想要主分区还是扩展分区。你通过输入来定义分区，Linux 需要知道分区号（在本例中，它是第一个分区，即 1）、第一个磁道（在本例中，它是磁盘的开头）以及分区的尺寸（在本例中为 200 个磁道），如下：

```
Partition number (1-4): 1
First cylinder (1-4092): 1
Last cylinder or +size +sizeM or +sizeK ([1-4092]): 200
```

现在在命令提示符处输入 `n`，为 Linux 根创建一个更大的分区（磁盘的剩余部分）。命令及其结果如下：

![](img/d86aa78922e215fd387e0c1556445cac_64_0.png)

```
Command (m for help): n

Command action
e extended
p primary partition (1-4)

pPartition number (1-4): 2
First cylinder (1-4092): 201
Last cylinder or +size +sizeM or +sizeK ([1-4092]): 4092
```

此时，你可能想通过输入 `p` 来确认布局。显示如下：

```
Command (m for help): p

Partition number (1-4): 2
First cylinder (1-4092): 201
Last cylinder or +size +sizeM or +sizeK ([1-4092]): 4092

Disk /hd1: 16 heads, 63 sectors, 4092 cylinders
Units = cylinders of 1008 * 512 bytes

| Device | Begin | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hd1 | | 1 | 200 | 10078 | 82 | |
| /dev/hd2 | | 201 | 4092 | 19552 | 83 |
```

分区看起来良好。目前它们都被标识为 Linux native，这意味着你可以在它们上放置 Linux 文件系统。第一个分区需要标记为可启动（bootable）。要进行标记，在命令提示符处输入 `t`。显示如下：

```
Command (m for help): t
Partition number (1-4): 1
```

第二个分区需要标记为可启动。要进行标记，在命令提示符处输入 `a`，如下所示：

```
Command (m for help): a
Partition number (1-4): 2
```

此时，你可能想再次检查分区表。当你输入 `p` 时，程序的响应如下：
