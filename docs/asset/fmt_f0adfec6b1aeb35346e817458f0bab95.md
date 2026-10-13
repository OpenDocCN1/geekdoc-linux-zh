
版权。与所有的 HOWTO 文档一样，可以在任何媒介（物理或电子）上全部或部分复制和分发，只要在所有副本上都保留此版权声明。允许并鼓励商业分发；然而，作者希望收到此类分发的通知。你可以将此 HOWTO 翻译成任何语言，前提是你保持此版权声明和免责声明完整，并附上说明翻译文档是谁的通知。

免责声明。尽管我尝试包含我所能找到的最准确、最新的信息，但我无法保证使用本文中的信息不会导致数据或设备的丢失。我对本 HOWTO 中的信息不提供任何保证，对于使用本 HOWTO 信息所导致的任何后果，我不承担责任。

### E.1.2 本档的新版本

本文的最新版本可以在 `ftpp://gatekeeper.com/pub/Digital/Linux-Alpha/Miniloader/docs` 找到，David Mosberger-Tang 慷慨地将其一些有趣的 HTML 格式包含在他出色的 Linux FAQ 网站 `http://www.azstarnet.com/ axplinux` 中。

### E.2 什么是 MILO？

在基于 Intel 的系统上，BIOS 固件设置系统，然后加载镜像以从 DOS 文件系统的启动块运行。这在很大程度上是 MILO 在 Alpha 系统上做的事情，但 BIOS 固件与 MILO 之间存在一些有趣的区别，其中之一是 MILO 包含并使用了未修改的标准 Linux 设备驱动。MILO 是固件，不像 BIOS 依赖 BIOS 固件来加载自身。MILO 的主要功能部分包括：

- 1. PALCode，
- 2. 内存设置代码（构建页表并开启虚拟地址），
- 3. 视频代码（BIOS 仿真代码和 TGA (21030))，
- 4. Linux 内核代码。这包括真实的 Linux 内核代码（例如中断处理）以及替代或模拟的 Linux 内核，
- 5. Linux 块设备驱动（例如软盘驱动器），
- 6. 文件系统支持（ext2, MS-DOS 和 ISO9660），
- 7. 用户界面代码（MILO），
- 8. 内核接口代码（为 Linux 设置 HWRPB 和内存映射

（注：OCR 文本提供了 E.2 的重复和碎片列表。上述根据提供的文档逻辑进行了合并。）

## E.4 如何构建 MILO

你需从内核（Kernel）独立构建 MILO。由于 MILO 的运行需要内核的部分支持（例如中断处理），你必须首先配置并构建与你想构建的 MILO 相匹配的内核。通常这意味着构建版本号相同的内核。因此，`MILO-2.0.25.tar.gz` 将针对 `linux-2.0.25.tar.gz` 进行构建，但在没有匹配的情况下，MILO ELF 共享库尚未完全支持，有两个版本的 MILO 源码。要在 ELF 系统下构建，你必须先解压标准的 MILO 源码然后对这些源码进行补丁。在后续讨论中，我假设你的工作内核源码和对象文件存储在 `/usr/src/linux` 子树中，并且 Linux 内核已通过 `make` 命令完全构建。

要构建 MILO，请将工作目录更改到 MILO 源码目录并调用 `make`：

```
$ make KSRC=/usr/src/linux config
```

与内核一样，你会被问及一系列问题：

> 将输出回到串口 (`MILO_SERIAL_ECHO`) [y]

如果可能，将内核打印输出到 `/dev/tty0` 是个好主意。如果你可以（并且想），输入 "y"，否则输入 "n"。所有标准的预编译 MILO 镜像都包含了使用 COMI 的串口 I/O。

> 使用 Digital 的 BIOS 仿真代码（非免费） (`MINI_DIGITAL_BIOS_EMU`) [y]

此代码作为库包含在内，只要在基于 Alpha 的系统上使用即可免费分发。源码不可用。如果你回答 n，则将构建免费的 BIOS 仿真。注意，目前你无法在 ELF 系统中构建 Digital 的 BIOS 仿真代码（该库尚未就绪），因此你必须对此问题回答 no。

> 从源码构建 PALCODE（警告：此操作存在危险） (`MINI_BUILD_PALCODE_FROM_SOURCES`) [n]

只有在你更改了 PALcode 源码时才应此操作，否则请使用 MILO 自带的、预编译 PALcode。

你现在已准备好构建 MILO 镜像本身：

```
$ make KSRC=/usr/src/linux
```

当构建成功完成后，MILO 镜像将位于名为 `milo` 的文件中。有很多名为 `milo.*` 的镜像，这些应该被忽略。

## E.5 如何加载 MILO

最常用的 MILO 加载方法是从 Windows NT ARC 固件，因为大多数操作系统都支持此。然而，有多种加载 MILO 的方法。它可以从以下位置加载：

- 故障安全引导块软盘
- Windows NT ARC 固件
- Windows NT AlphaBIOS
- Digital 的 SRM 控制台
- Alpha 板调试监视器
- 闪存/ROM

### E.5.1 从 Windows ARC 固件加载 MILO

并非所有基于 AXP 的系统都包含 Windows NT ARC 固件，但这是启动 MILO 的优选方法。Windows NT ARC 固件是一个程序可以运行并调用固件执行操作的环境。Windows NT OSLoader 正是执行此点的程序。`Linload.exe` 是一个简单得程序，只需完成加载和执行 MILO 的工作。它将适当的镜像加载到内存的 `0x0000000` 处，然后进行切换。MILO 像 Linux 使用不同的 PALcode，这就是为什么必须进行切换。MILO 将自身重定位到 `0x2000`，并像以前一样通过 PALcode 重置点继续运行。

在添加启动选项之前，你需要将 `linload.exe` 和适当的 MILO 拷贝到 Windows NT ARC 固件可以读取的地方。在以下示例中，我假设你从 DOS 磁盘启动：

1. 在启动菜单中，选择 "Setup menu..."
2. 在 "Setup menu" 中，选择 "Set up the system..."
3. 在 "Setup menu" 中，选择 "Manage boot menu..."
4. 在 "Boot selections menu" 中，选择 "Add a selection"
5. 选择 "Floppy Disk"
6. 输入 "`linload.exe`" 作为 osloader 名称
7. 对于操作系统是否与 osloader 在同一分区上，回答 "yes"
8. 输入 "\" 作为系统根目录
9. 通常输入 "Linux" 作为此启动选项的名称
10. 对于不想在启动时初始化调试器，回答 "No"
11. 你现在应该回到了 "Boot selections menu"，选择 "Change a boot option" 并选取你刚刚创建的选项进行编辑
12. 使用下箭头移动到 "OSLOADFILENAME"，输入你想使用的 MILO 镜像名称，例如 "`noname.arc`" ，然后按回车
13. 按 ESC 返回 "Boot Selections menu"
14. 选择 "Setup Menu"（或再次按 ESC）并选择 "Menu, save changes" 选项
15. 按 ESC 将带你回到 "Boot menu"，你可以尝试启动 MILO。如果你不想让 Linux 作为第一个启动选项，可以在 "Boot selections menu" 中更改启动选项的顺序。

在完成所有操作后，你应该有一个类似所示的启动选项：

```
OSLOADIFIER=Linux
SYSTEMPARTITION=multi(0)disk(0)fdisk(0)
OSLOADER=multi(0)disk(0)fdisk(0)\linux.exe
OSLOADPARTITION=multi(0)disk(0)fdisk(0)
OSLOADFILENAME=\noname.arc
OSLOADOPTIONS=
```

（注：此处原文后续似乎存在格式混乱或内容重复，翻译已根据逻辑进行了整理）

在所有这些操作最后，你应该有一个这样的启动选项：

```
OSLOADIFIER=Linux
SYSTEMPARTITION=multi(0)disk(0)fdisk(0)
OSLOADER=multi(0)disk(0)fdisk(0)\linux.exe
OSLOADPARTITION=multi(0)disk(0)fdisk(0)
OSLOADFILENAME=\noname.arc
OSLOADOPTIONS=
```

（注：由于原文文本在 E.5.1 结尾处存在逻辑重复和格式混乱，此处尽可能按原意呈现）

### E.5.2 从 Windows NT AlphaBIOS 加载 MILO

随着 XLT 系列的引入，Digital 将其系统的控制台界面从 ARC 更改为 AlphaBIOS。AlphaBIOS 是一个面向的界面，对 PC 用户来说更加熟悉。对于想要运行 Linux 的用户，这种变化需要调整流程。
