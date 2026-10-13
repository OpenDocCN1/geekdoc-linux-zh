
将整个硬盘用于 Linux 是直观且在概念上简单的。无论你覆盖了哪个（或哪些分区），都会破坏磁盘上的所有数据。对于此讨论，我假设你只有一个分区，这是 DOS 和 Windows 安装的典型情况。

# 制作启动软盘

通常需要创建一个启动软盘来启动红帽安装程序。软盘包含基础的 Linux 内核和文件系统。文件系统为内核运行提供了基础；它对 Linux 的运行至关重要。当你启动计算机时，启动软盘会加载基础 Linux 操作系统并启动安装。

Probing PCI hardware.

Calibrating delay.. ok - 35.94 BogoMIPSMemory:

63180k/6536k available(720k kernel code, 384k reserved,

125k data)Swansea University Computer Society NET3.035 for Linux 2.0

NET3: Unix domain sockets 0.13 for Linux NET3.035.Swansea University Computer Society TCP/IP for NET3.034

IP Protocols: ICMP, UDP, TCP

FS: Diskquotas version dquot_5.6.0 initialized

Checking 386/387 coupling.. Ok, fpu using exception 16 error Reporting.Checking 'hit' instruction... Ok.Linux version

```
2.0.30 (root@atlas.paunchy.net) (gcc version 2.7.2.1) #1 Thu Aug 21 16:27:26 MDT 1997
```

Serial driver version 4.13 with no serial options enabled

tty0 at 0x03fb (irq = 4) is a 16550

tty1 at 0x02fb (irq = 3) is a 16550

Ramdisk driver initialized : 16 ramdisks of 4096K sizehead: WDC AC2160H, 15498MB/128KB Cache, LBA.

CSH=787/64/63

Partition check: hda1

VFS: mounted (ext2 filesystem) readonly.

Swansea University Computer Society IPX for NET3.35

# 从 CD-ROM 启动

如果你有一台可以从 CD-ROM 启动的计算机，就不需要软盘驱动器。这种能力在 1998 年左右变得常见。你需要查看你的 BIOS 配置以确定你的 CD-ROM 是否可以启动。查看启动序列来做出判断。描述如何操作超出了本书的范围。如果你有主板，请咨询你的主板以获取有关该过程更多信息。如果你可以并想从 CD-ROM 启动，请配置你的 BIOS 以实现。在插入红帽发行版 CD-ROM 后重启计算机。你的计算机将识别 CD-ROM 并从其开始安装过程。

# 安装 Linux

## 第一章：安装红帽 Linux

红帽提供了图形界面 (GUI) 和基于文本的安装系统。如果你发现文本系统比 GUI 兼容更广泛的硬件，我在这里描述基于文本的系统。如果你愿意，请使用 GUI 系统——它非常好用。如果你这样做了，你可能希望将这些指令作为通用指南，因为 GUI 遵循与文本系统相同的序列。

对于安装过程中的每一步，你都会看到一个不同的窗口。大多数窗口提供了一个用于选择项的子菜单，例如 CD-ROM 驱动器的类型。在其他情况下，你通过选择屏幕上的按钮来选择一个选项。使用方向键选择子菜单。按空格键切换按钮的开启或关闭。你也可以按回车键选择高亮的按钮。`Tab` 键和 `Shift+Tab` 键组合可以切换。

红帽 CD-ROM 的 `D:\IMAGES` 目录包含许多文件，这些文件是 Linux 内核和文件系统的映像。一个名为 `RAWWRITE` 的程序（你可以在 `D:\DOSUTILS` 中找到）会将你的内核和基础文件系统映像（包含最核心的系统和应用程序）逐字节地传输到软盘上。当该磁盘插入你的软盘驱动器并重启计算机时，Linux 将接管控制并将文件系统复制到系统内存（ramdisk），然后红帽安装程序就会启动。这时你就可以安装一个完整的 Linux 系统了。

> 注意：红帽安装系统缺乏优雅的退出机制。一旦开始安装，你必须重启。

Linux 使用了一种名为虚拟终端的机制。虚拟终端允许你的单台计算机像多个独立终端一样工作。通过按下 `Alt+F1` 到 `Alt+F5`，你可以在不同的屏幕之间切换。红帽利用这一特性在每个终端提供有关安装过程的不同信息。下表描述了每个虚拟终端的功能：

| 键组合 | 显示 |
| :--- | :--- |
| `Alt+F5` | 程序输出 |

## 开始安装

以下是完成红帽 Linux 安装过程的步骤（每个数字对应一个安装步骤）：

Linux 是国际化的选择你想使用的语言并回车。

选择你的键盘类型。（以后可以使用 `kbdconfig` 命令修改你的选择。）

你被要求从 CD-ROM 还是硬盘安装。选择 CD-ROM 并点击 OK 按钮。

![](img/1fa05dc2b61f40be78509e4dbfc1fe6_45_0.png)

这是一个介绍性对话框。按任意键继续安装。

红帽提供了五种不同的安装类型供选择。本书将使用自定义系统，但会简要描述其他选项。它们是：

- 安装自定义系统
- 升级现有安装

前三种类型会在你的磁盘上写入预定义的分区，并选择要安装的软件。自定义系统要求你

## 第 1 章：安装 Red Hat Linux

选择要安装的分区和软件包包。“升级现有安装”（Upgrade Existing Installation）不会更改任何现有的分区，仅安装新软件。请参考侧边栏的“使用 Gnome/KDE 工作站和服务器类型安装”以获取有关这些系统的更多信息。本书描述的是“自定义系统”（Install Custom System）类型的安装。

选择自定义系统（Custom System）。

> 请记住，如果使用服务器或工作站选项，除非您选择手动选项，否则整个磁盘都将被擦除。

### 使用 Gnome/KDE 工作站和服务器类型安装

如果您选择 Gnome/KDE 工作站或服务器类型，系统将提示您允许 Red Hat 为您创建分区或手动进行。如果您选择手动分区方法，则将使用在“磁盘分区”节中描述的 Disk Druid 系统来创建分区。请参考该节的第 1 到 7 步以获取更多说明。

如果您选择让 Red Hat 自动分区，您的磁盘将获得一个 64MB 的交换分区（swap）、一个 16MB 的启动分区（boot）和一个大的根分区（/）。boot 分区包含 Linux 内核和支持程序。

如果您选择带有自动分区的服务器（Server），Red Hat 将尝试将下表所示的五个分区写入磁盘。

| 分区 | 描述 |
| :--- | :--- |
| `/` | 根分区。所有分区的挂载点 |
| `/boot` | 启动所需的 Linux 内核和额外 |
| `/usr` | 库和静态文件。以及额外的应用程序 |
| `/var` | 可变文件，如日志和临时文件 |
| `/home` | 用户家目录 |

根 (/) 和 var (/) 文件系统的大小相等，以便相互创建。usr (/usr) 和 home (/home) 分区也分配了相同的空间。boot (/boot) 分区的空间仅足够（约 16MB）存储 Linux 内核以及启动计算机所需的关联文件。根分区和 var 分区的空间分别约为 usr 和 home 分区的 10%。

### 分分区

您的第一个主要任务是对磁盘进行分区。以下指令说明了如何使用 Red Hat 的 Druid 系统完成此过程。

#### 1. 当前磁盘分区 (Disk Druid)

在 Linux 下，分区选择是一个比 Windows 重要得多的考虑因素。Windows 通常运行在一个或两个分区上。Linux 也可以运行在单个分区上，但这可能会在以后产生问题。

关于使用多少分区以及分区的大小有不同的哲学。书中的建议是基于作者的经验和最佳判断。

我建议的 1G 和 4G 磁盘的分区如表 1-2 和 1-3 所示。如果您使用更大的磁盘，会有更多的回旋地。使用 60MB 的根分区大小是为了防止您想安装 Red Hat 发布版（Publisher's Edition）光盘包含的所有软件；它还留出了一些额外的空间用于编译多个版本的内核（在第 4 章中描述）。对于较小或较大的磁盘，请根据您的最佳判断进行。

### 表 1-2 1-GB 磁盘的建议分区

| 分区 | 大小 | 功能 |
| :--- | :--- | :--- |
| `/` | 60 | 作为所有挂载文件系统的根 |
| `/var` | 100 | 主要用于临时文件和日志 |
| `/usr` | 400 | 用于静态或大部分静态的文件和库 |
