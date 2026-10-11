
- 在 Microsoft Windows 中，在第二个硬盘上运行 `Scandisk` 工具。务必使用“彻底（Thorough）”选项来检测并锁定任何坏扇（包含缺陷的磁盘区域）。要运行 `Scandisk`，点击“开始”，指向“程序”，指向“辅助工具”，指向“系统工具”，然后选择 `Scandisk`。点击“彻底”，并勾选“自动修复错误”。

- 在 MS-DOS 中重启系统，并使用 `fdisk` 工具删除 D 分区。要启动 `fdisk`，输入 `c:\windows\command\disk` 并按回车。选择第二个。

## 设备配置

在本章中，你学习了如何安装红帽直接支持的一系列设备。

> **提示** 如果你是 Linux 新手，在学习所有基础知识之前，不要尝试这些设备。

表 4.5 获取设备信息的来源

| 设备 | 信息来源 |
|---|---|
| CD-R 驱动器 | CD-Writing HOWTO，作者 Winfried Trumper (http://metalab.unc.edu/LDP/CD-Writing-HOWTO.html)。刻录 CD 的友好软件包括 X-CD-Roast (http://www.fh-muenchen.de/ze/projects/scdroast/_overview.html)。对于许多 Linux 用户。通常情况下。 |
| 数字相机 | 由于数字相机制造商不愿发布有关产品如何传输的信息，支持并不完善。但有一个名为 `photopc` 的实验性程序适用于雅能、爱普、奥林巴斯、山丽和尼康相机，支持相机内 JPEG 压缩更多 http://www.average.org/digcam/）。`photopc` 的图形界面是 `photok` (http://www.mediacity.com/-pwhite/Photok/photok.html)。 |
| 红外 | Linux IR HOWTO，作者 Werner Heuser (http://metalab.unc.edu/LDP/IR-HOWTO.html)。对支持 IRDa 标准的所有红外设备都有实验性。 |
| 扫描仪 | `SANE`（Scanner Access Now Easy）是各种光栅图像设备的公共领域编程接口，包括扫描仪、相机和帧采集器 (http://www.mostang.com/sane/)。`XSane` 是用于扫描的图形界面 (http://www.wolfburg.de/-rauch/sane-sane-xsane.html)。不支持的扫描仪包括 Acer、许多手持式和 UMAX 并口扫描仪。HP Scanets 和 UMAX SCSI 扫描仪支持良好。 |
| 电视调调器 | 调调器/视频采集卡列表及安装/配置说明，请参见 Reijan 1999。你可以使用 `xawtw` 看电视 (http://www.in-berlin.de/User/xawtw.html)。 |
| UPS | 支持广泛的间断电源 (UPS)，请参见 UPS HOWTO，作者 Harvey J. Stein (http://metalab.unc.edu/HOWTO/UPS-HOWTO.html)。 |

## 第二部分 • 安装红帽 Linux

### 从这里开始

你准备好安装红帽 Linux 了。在下一章中，你将开始安装。在第 6 章中，你将完成安装软件的运行，第 7 章将展示如何在首次启动 Linux 后完成系统配置。

# 参考文献与延伸阅读

Koffler, Michael. 1997. Linux: Installation, Configuration, and Use. Reading, PA: Addison-Wesley.

Gonzato, Guido. 1998. “From DOS/Windows to Linux HOWTO.” Linux Documentation Project.在线获取：http://metalab.unc.edu/LDP.

Quinlan, Daniel. 1997. Filesystem Hierarchy—Version 2.0. 在线获取：http://www.pathname.com/fhs/2.0/fhs-toc.html.

Reijnen, Patrik. 1999. Linux Hardware Compatibility HOWTO. 在线获取：http://users.bart.nl/~patrick/hardware-howto/Hardware-HOWTO.html.

Welsh, Matt, et al. 1992-1998. Linux Installation and Getting Started. Linux Documentation Project. 在线获取：http://metalab.unc.edu/LDP/.

# 5

## 开始安装

如果你已经按照第 4 章的描述准备好安装 Linux，那么你就可以准备好在计算机上安装 Linux 操作系统了。本章将引导你完成在 PC 上安装 Red Hat Linux 6.0 的步骤。

### 为 Red Hat Linux 留空间

在运行安装软件之前，你需要确保已经为 Red Hat Linux 留出了空间。

你可以通过两种方式实现：

- 如果你想像上一章描述的那样创建一个双系统，你需要在硬盘上至少有 700MB 的空闲未分区空间，或者一个已经删除了所有分区的第二个硬盘。更多信息请参阅第 4 章中的“为双系统安装准备系统”。
- 如果你正在创建一个全 Linux 系统，可以使用 Red Hat 安装软件删除硬盘上现有的 DOS 分区。

### 决定如何启动系统

为了安装 Red Hat Linux，你必须使用随书附的 CD-ROM 或安装了精简版本 Linux 的软盘启动系统。

### 配置你的 PC 从 CD-ROM 启动

如果你的 PC 比较新（两年以内），你可能可以配置系统从 CD-ROM 启动。要确认这一点，请重启系统，并按下键（通常是 Delete）以更改计算机的 BIOS 设置。翻页设置选项，直到找到可以让你指定启动磁盘顺序的选项。（默认情况下，大多数系统被设置为从 A 盘和 C 盘启动。）如果你能更改此设置使第一个启动驱动器为 CD-ROM，你就可以直接从随书的 CDROM 安装 Linux。更改设置使你的计算机首先从 CD-ROM 启动。

如果你的计算机无法从 CD-ROM 启动，那么你需要制作一个启动盘。你将在下一节学习如何操作。

### 创建启动盘

本节适用于系统无法直接从 CD-ROM 启动的用户。你需要按照本节的说明创建一个启动盘。为此，你将使用 `rawwrite.exe` 程序，该程序位于 `\dosutils` 目录下。使用该程序将名为 `boot.img` 的文件（存储在 `\images` 目录）传输到软盘。该文件会将软盘转换为 Linux 启动盘。

创建 Linux 启动盘：

1. 格式化一张 3.5 英软磁盘。
2. 将软盘插入计算机的软盘驱动器（A 盘）。
3. 将本书的 CD-ROM 插入 CD-ROM 驱动器。
4. 使用 Windows 资源管理器查看 CD-ROM 磁盘的内容。
5. 显示 `\dosutils` 目录。
6. 定位并双击 `write.exe`。你会看到一个 MS-DOS 应用程序窗口。程序要求你指定要复制的镜像文件名称。
7. 输入 `..\images\boot.img` 并按回车。（不要忘记前面的两个点。）
8. 要识别文件的目标位置，输入 `a:` 并按回车。

`rewrite` 程序会将启动镜像文件传输到 A 盘的软盘中。

### 首次启动 Linux

> 提示：在计算机从 C 盘启动之前，确保其已设置为从 A 盘启动。这是大多数 PC 的默认设置，但你的系统可能被更改过。要检查默认启动序列，请重启系统，并按下键（通常是 Delete）以查看默认 BIOS 设置。找到可以指定默认启动序列的区域，并确保系统首先从 A 盘启动。

为了在 Linux 中启动计算机以便运行安装软件，请执行以下操作：

1. **重要：** 如果你的系统配备了可移动驱动器（如 Zip 驱动器），请向驱动器中插入磁盘。
2. 执行以下操作之一：

如果你的计算机可以从 CD-ROM 启动，将本书的 CD-ROM 插入 CD-ROM 驱动器，并重启计算机。

或

如果你制作了启动盘，将磁盘插入 A 盘，并重启计算机。

你将看到一个解释各种启动选项的屏幕。要继续，只需按回车。

> 提示：如果你看到指示安装失败的错误消息，意味着安装软件无法检测到你的硬件。你需要在专家模式下重新安装。更多信息请参阅本章稍后部分的“使用专家模式”。

### 开始安装

本节将引导你完成整个自定义（Custom）安装过程。如果你选择工作站（Workstation）或服务器（Server）级安装，你将看到本节讨论的一些对话框，但不是全部。我强烈建议选择自定义安装类；此选择将让你能够充分探索书中其余部分的程序和实用程序。

出现初始欢迎界面后，你将看到图 5.1 所示的窗口。在这里，你选择一种语言，但你应该花一点时间熟悉用于导航安装程序对话框的命令。
