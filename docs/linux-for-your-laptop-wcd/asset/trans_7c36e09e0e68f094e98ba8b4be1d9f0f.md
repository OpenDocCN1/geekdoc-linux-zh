

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_115_0.png)

*图 3.1 ntvsys 命令可用于控制各种服务器软件的启动和使用。*

/etc/initab. 在 X11 终端窗口的命令行中输入 `cksysv` 并按下回车键。您将会看到图 3.2 中所示的对话框。

切勿随意使用此命令！在启动或关闭过程中，各种服务的顺序至关重要。例如，在关机进程卸载远程文件系统之前关闭 NFS 服务并不是一个好主意。另一方面，您可能希望在初始化以太网卡之前启用

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_115_1.png)

*图 3.2 tksysv 命令用于控制在系统不同运行级别期间可用的服务。它可以用来重新排序服务器守护进程的启动或停止时间。*

PCMCIA 支持。幸运的是，大多数 Linux 发行版的默认设置运行良好，因此您很少需要使用此程序（除非您安装了新的服务器软件）。

## 使用 Linuxconf

linuxconf 命令可以在有无 X11 的情况下使用，作为一种系统维护工具，当使用图形界面管理 Linux 时，它不断发展并越来越受欢迎。此客户端支持几乎所有 Linux 网络和服务器的配置和控制。如果您使用的是 Red Hat 或 Mandrake Linux，请在 /usr/lib/linuxconf/help.eng 目录下查找 HTML 帮助文件，或者使用 linuxconf 内置的帮助按钮。

## 工作站和服务器要求

根据 Red Hat, Inc. 的说法，典型的要求是：服务器操作需要 1.6GB，工作站使用需要 450MB，最小安装需要 120MB。根据 Mandrake Linux 团队的说法，完整的 Mandrake Linux 安装需要略多于 1GB。

在 Apple iBook 上安装 Yellow Dog Linux 中包含的所有内容至少需要 1.5GB。

您的安装所需磁盘空间还取决于您选择安装软件的数量。安装 Linux 时，系统会要求您选择安装类型。您还可以避免“默认”类型的安装，而是自行挑选软件包。这是避免安装冗余或不必要软件的好方法。例如，您的系统真的需要六种不同的文本编辑器吗？

如果您是新手且有足够的磁盘空间，请继续安装所有内容。您可以随时返回并删除软件以腾出更多空间。随着经验的积累，您将能够快速完成笔记本电脑上的新安装，并且您将知道哪些软件包是必需的，哪些可以省略。

## 最小化安装策略

如果硬盘空间不多，您的选择有限。好消息是，您可以执行最小化安装，其规模比表 3.1 中描述的默认 120MB 系统小得多。Linux 非常通用，系统可以从软盘（但在 iBook 上不行）、Iomega Zip 驱动器或单个可执行文件安装。

## WinLinux 2000

如果您希望避免对笔记本电脑硬盘进行分区和格式化的麻烦，您可以使用 WinLinux 2000 直接在 Windows 桌面上安装、配置和运行 Linux。您需要至少 500MB 的硬盘剩余空间来安装发行版；之后，您可以删除原始安装文件。

要安装此发行版，请运行 WL2000.EXE 安装程序并回答提示。不到一分钟，您将使用 KDE 作为桌面套件，通过 X11 启动到 Linux。该发行版包含 Netscape Communicator 和 Adobe 的免费 Acrobat 阅读器。此发行版通过在 Windows 卷上创建虚拟文件系统（例如一个 500MB 的单文件）来代表 Linux 文件系统来工作。

浏览至 http://www.winlinux2000.com/ 下载您的副本。

## Zipslack

要了解如何从 Iomega Zip 驱动器下载和安装 Slackware Linux，请浏览至 http://www.slackware.com/zipslack/

以下是基本步骤：

- 1. 下载 zipslack.zip、bootdisk.img 和 RAMRITE.EXE 文件。一个额外的文件 fourmeg.zip 支持在仅有 4MB RAM 的基于 386 的笔记本电脑上安装！
- 2. 将 zipslack 发行版解压到 Iomega 磁盘上。
- 3. （可选）使用 RAMRITE.EXE 创建块磁盘。
- 4. 运行 LOADLIN.EXE 命令以从 Iomega 磁盘启动 Linux。

这将允许您从 Zip 驱动器运行 Linux，而无需对笔记本电脑硬盘进行分区。阅读刚才提到的 Slackware 网站上的常见问题解答（FAQ），以了解如何在笔记本电脑上安装 zipslack Linux 发行版。

如果您硬盘存储空间较少，Slackware Linux 是一个很好的替代方案；最小化的 Slackware Linux 安装仅需 50MB 硬盘空间。您也可以使用软盘安装 Slackware，但您需要下载许多磁盘映像，创建磁盘，并按顺序安装每个磁盘。

## Peanut Linux

另一个具有相同 50MB 占用空间的小型发行版是 Peanut Linux。然而，这个发行版包括 X11、Netscape Communicator 以及 X11 客户端的特殊最小化选择，包括 K 桌面环境。对于笔记本电脑上紧凑但最新且功能强大的 Linux 安装来说，这个发行版可能是最佳选择。尽管 Peanut Linux 面向工作站，但包括 FTP 和 Web 服务器。浏览至 http://metalab.unc.edu/peanut

Peanut Linux 发行版可以从 CD-ROM 安装，或使用 Linux 安装（见刚才链接中提到的 INSTALL.TXT 文件）。

## 活动文件系统

一些 Linux 发行版，例如 SuSE 的最新版本，具有直接从 CD-ROM 运行或使用*活动*文件系统的功能。这是一种方便的方式，无需安装即可启动和运行 Linux，它允许您在不进行分区和格式化的情况下探索发行版的功能。

## 软盘 Linux

您还可以从软盘启动和运行 Linux。许多基于软盘的发行版提供一个使用一张或多张软盘的 Linux 环境。有关更多信息，请参见附录 A 表 A.4，“Linux 笔记本资源”。

## 选择启动方法

Linux 可以通过多种方式启动。在安装 Red Hat、Mandrake 和大多数其他发行版时，您有机会创建一个启动软盘。然后，您可以使用此启动盘在重启或打开笔记本电脑时使用。如果您在安装期间未创建软盘，请在启动 Linux 后使用 Red Hat 的 `mkbootdisk` 命令创建一个。您需要知道您正在使用的 Linux 版本，并且需要指定软盘设备。

首先，使用 `uname` 命令及其 `-r`（修订版）选项：

```bash
# uname -r
2.2.14-15mdk
```

接下来，在控制台或 X11 终端窗口的命令行中输入 `mkbootdisk`，指定软盘设备和 Linux 内核修订版，并按下回车：

```bash
# mkbootdisk -device /dev/fd0 2.2.14-15mdk
```

在 `/dev/fd0` 中插入一张磁盘。磁盘上的任何信息都将丢失。
按 `<Enter>` 继续或 `^C` 中止。

在提示处，插入一张空白软盘并按下回车。然后 `mkbootdisk` 命令将创建一个启动磁盘。如果您的启动加载程序（如稍后将讨论的 LILO）损坏，您可以使用此磁盘。

## LOADLIN

您还可以使用名为 LOADLIN 的程序直接从 DOS 会话启动 Linux。这个程序非常灵活。它可以用于使用 DOS C:\ 驱动器上的 Linux 内核启动 Linux。如果 Linux 安装在另一个分区（如 /dev/hda3）上，可以这样使用：

```bash
loadlin c:\vmlinuz root=/dev/hda3 ro
```

此命令行将使用 vmlinuz 内核启动 Linux，然后使用 /dev/hda3 上的 Linux 分区。您应该能在您的 Linux 发行版 CD-ROM 上找到关于 LOADLIN 的文档。LOADLIN 也在安装到您系统 /usr/doc/HOWTO 目录下的若干 HOWTO 和 mini-HOWTO 文档中提及。您还可以通过浏览作者的个人页 http://elserv.fim.fgan.de/~lrxmen/ 来阅读关于此程序的内容。

## LILO

启动 Linux 最流行的方法之一是使用 Linux Loader (LILO) 程序。LILO 通常在安装 Linux 时配置和安装，但也可以在从软盘启动 Linux 后安装和配置。此程序是一个小型启动加载程序，可以安装在软盘上，或安装在笔记本电脑硬盘的各个位置。

当您使用 LILO 安装和启动时，您应该会看到类似以下内容（但您的 LILO 启动提示可能不同）：

```bash
LILO
boot:
```

