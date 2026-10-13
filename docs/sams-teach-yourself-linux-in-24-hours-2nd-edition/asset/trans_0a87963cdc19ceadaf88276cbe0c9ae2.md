
## 其他方式

多家硬件厂商也在新硬盘、笔记本电脑或计算机上预装 Linux。如果想要一台开箱即用的完全配置好的计算机，这就是方法。请浏览 http://metalab.unc.edu/LDP/HOWTO/VAR-HOWTO.html。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_38_0.png)

> 你可以随时请一位有 Linux 经验的朋友过来为你安装 OpenLinux！这是一个分享信息的好方法，有人在身边帮助可以让安装过程更轻松。或者，参加 Linux 用户组（LUG）的 InstallFest！请浏览 http://www.linux.org/users/index.html 找到你附近的 LUG。LUG 定期举行安装会议，你可以在很短时间内完成 OpenLinux 的安装和配置！

## 规划你的启动过程

启动 Linux 有多种不同方式。你需要决定是否要从启动提示符、DOS 中的命令行、软盘或商业软件程序启动 Linux。

- 1. LILO—Linux 加载器（LILO）是一个用于启动 Linux 或其他操作系统的微小程序。你可以在安装过程结束后将 LILO 安装在 DOS 分区的引导记录或硬盘上 Linux 分区的根分区中。
- 2. LOADLIN.EXE—使用 DOS 中的 LOADLIN 程序启动 Linux。如果你使用此程序，则无需安装 LILO。你需要将 Linux 内核复制到 DOS 分区或软盘上。从 DOS 启动的优点是可以使某些硬件（如 Mwave 适配器）与 OpenLinux 配合工作。
- 3. 启动软盘—启动软盘也可以用来启动 Linux。你可以将 LILO 保存到软盘上，然后启动 Linux、DOS 或其他操作系统。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_38_1.png)

> 在安装 Windows 之后再安装 OpenLinux 和 LILO。其他操作系统安装通常会无视这一点而覆盖 LILO（尽管可以通过使用 Linux 启动软盘启动并重新运行位于 /sbin 目录下的 lilo 命令来恢复。）

- 4. 软盘—想在安装 OpenLinux 之前先从软盘尝试 Linux 吗？请浏览 http://metalab.unc.edu/LDP/devel.html 并搜索适合软盘的 Linux 发行版。你可以用一张软盘启动 Linux（但你得不到 X Window 系统）。
- 5. System Commander—这是一个可用于启动多个操作系统的商业程序。详情请浏览 http://www.systemcommander.com。
- 6. BootMagic—随 PowerQuest Corp. 的 PartitionMagic 提供，BootMagic 可用于启动多个操作系统，如 Windows NT 和 IBM 的 OS/2。PartitionMagic 的商业版还包含一个名为 PQBoot 的 DOS 实用程序，它列出活动的可启动分区，并可用于启动其他操作系统，如 Linux。详情请浏览 http://www.powerquest.com。

## 准备你的硬盘

安装过程中的第一步（如果需要，先制作启动软盘）是分区，或在硬盘上腾出空间。如果你只想在计算机上使用 OpenLinux，请跳过本小时的其余部分，直接进入第 2 小时。但如果你想要双启动计算机，或启动至少两个不同的操作系统，你需要在硬盘上创建一个分区，为 OpenLinux 软件提供足够的空间。

分区不过是查看硬盘及其划分方式的一种特殊方法。分区有两种类型：主分区和扩展分区。你的硬盘可以包含四个主分区。如果你需要进一步划分或映射硬盘，可以将其中一个主分区指定为扩展分区（然后可以进一步细分）。

这些分区通常包含文件系统。文件系统是文件或目录写入硬盘的方式。DOS 和旧版 Windows 使用名为 FAT16 的文件系统。新版 Windows 使用 FAT32。Linux 使用两种文件系统：ext2（用于存储文件）和 swap（用于临时存储内存）。

幸运的是，Caldera 的 OpenLinux CD-ROM 包含了为 OpenLinux 分区所需的一切！该 CD-ROM 包含 PowerQuest 的 PartitionMagic 和 Boot Magic 的有限版。安装这些实用程序后，你可以直接从 Windows 设置 Linux 分区（继续阅读以了解如何操作）。

在安装过程中，一些笔记本电脑和台式机用户可能会发现一个由计算机 BIOS 用于“Save to Disk”操作（如使计算机休眠）的小分区。该分区的大小通常与安装在计算机上的系统内存或 RAM 的大小相同。一般来说，请不要动这个分区。另请注意，如果你增加计算机的 RAM，分区可能需要调整大小以匹配新的内部内存大小（这可能会导致其他分区出现有趣的调整或重新调整大小）。

## 从 Windows 准备你的硬盘

为硬盘做好支持 Windows 和 OpenLinux 启动的准备的第一步是安装 Caldera 和 Power Quest 的实用程序。启动计算机。当 Windows 桌面出现时，插入你的 OpenLinux CD-ROM。OpenLinux 欢迎屏幕应出现，如图 1.1 所示。

### 图 1.1
OpenLinux 欢迎对话框是你 OpenLinux 之旅的起点！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_40_0.png)

如果安装过程未自动开始，请在“我的电脑”文件夹下双击计算机的 CD-ROM 图标。

按照提示操作，此设置程序将在“开始”菜单中创建 OpenLinux 程序文件夹。该文件夹将包含创建安装（启动）软盘、安装 Boot Magic（以支持 Windows 和 Linux 启动）以及分区硬盘和安装 Linux 的快捷方式。设置完成后，双击“分区并安装 Linux”图标（如图 1.2 所示）。

### 图 1.2
双击“分区并安装 Linux”程序开始安装。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_41_0.png)

这将启动如图 1.3 所示的 PartitionMagic Caldera Edition 设置程序。按照提示操作，设置将在你的硬盘上创建 PowerQuest 程序文件夹。还将为“开始”菜单创建 PartitionMagic 程序文件夹。

### 图 1.3
要开始安装，你必须先安装 PartitionMagic Caldera Edition 程序。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_41_1.png)

安装完成后，设置程序将要求你点击“完成”按钮。这将关闭 Windows 并运行 PartitionMagic。如图 1.4 所示，你将被要求在继续之前取出 OpenLinux CD-ROM。这是因为你必须先创建 Linux 分区，然后再安装 Linux。（如果 CD-ROM 仍插入，计算机可能会直接重新启动到安装 OpenLinux。）

### 图 1.4
不要忘记在继续安装之前取出你的 CD-ROM！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_42_0.png)

如果你已经安装了 Linux 并使用 LILO，你的计算机此时将重新启动到 LILO。要继续安装，请从 LILO 启动到 Windows。但是，安装程序将无法识别你现有的 Linux 分区。安装 OpenLinux 后，你会在 PartitionMagic 程序文件夹中找到一个“删除 Linux”图标，可用于删除 Linux 分区。在现有 Linux 系统上安装 OpenLinux 的最佳方法是重新启动并使用安装软盘或直接从 CD-ROM 安装 OpenLinux。详情请参阅第 2 小时“安装 Linux”。

PartitionMagic Caldera Edition 仅识别你的第一块硬盘，并且只能创建三种不同大小的分区：300 兆字节、500 兆字节和一千兆字节。当其对话框出现时，点击所需的 Linux 分区大小，然后点击“确定”按钮。然后你会看到 PartitionMagic 的对话框，显示分区进度。分区完成后，插入你的 OpenLinux 启动软盘和/或 OpenLinux CD-ROM，然后重新启动计算机开始安装。

如果你想要使用超过 PartitionMagic 有限版提供的一千兆字节最大值的更多硬盘空间，请使用启动软盘和/或 OpenLinux CD-ROM 直接启动到 OpenLinux 安装。在初始安装期间，选择“自定义”分区方案。但是请注意，你必须有一个可用的现有或空分区；该分区将被格式化为 Linux。

## 总结

本小时向你介绍了有关 Linux、OpenLinux 以及如何为 Linux 安装做准备的一些基本概念。
