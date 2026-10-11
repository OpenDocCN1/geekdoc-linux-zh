
如果你使用商业引导加载程序，例如 PowerQuest 的 BootMagic，请确保将 LILO 安装到根原生 Linux 分区！BootMagic 需要 MBR 来提供其图形操作系统选择对话框，并且安装时会覆盖 LILO。

如果你安装了 Linux，但发现 LILO 无法正常引导，你可以使用 LILO 启动消息进行诊断（如《LILO 用户指南》第 44 页所述）。表 3.4 列出了这些诊断信息。

表 3.4 LILO 诊断信息

| 诊断信息 | 描述 |
| :--- | :--- |
| *blank*（空白） | LILO 未加载或未安装 |
| L ## | LILO 的第一阶段已加载，但出现磁盘错误代码 (00, 01, 02, 03, 04 或 06)；参见《LILO 用户指南》第 5.2.2 节（指南第 44 页） |
| LI | LILO 的第一和第二阶段已加载，但磁盘几何问题或 LILO 映射安装程序问题阻止了执行（参见《用户指南》第 3.4 节） |
| LIL | LILO 的第二阶段已加载，但发生了几何或介质故障 |
| LIL? | LILO 的第二阶段已加载，但在错误的地址处（可能具有与 LI 相同的问题） |
| LIL- | 损坏的描述符表阻止了正常执行（参见《用户指南》） |

如果你遇到问题，请阅读位于 `/usr/doc/lilo*/doc` 目录下的《LILO 用户指南》。如果你正在运行 Linux，请使用 `gv` 命令像这样显示文件：

```
> gv /usr/doc/lilo*/doc/User*ps
```

你还应该创建一个安装了 LILO 的备份启动软盘。有关详情，请参阅《用户指南》第 4.1.6 节（第 37 页）。

#### 资源信息

- http://www.redhat.com/support

关于安装和配置 Red Hat Linux 的一般信息和常见问题解答。

- http://www.redhat.com/corp/support/manuals/

在线 Red Hat 安装手册。

- ftp://c3po.terraplex.com/pub/terrasoftsolutions/yellowdog/guide_to_install/

你可以获取 Yellow Dog Linux 用户指南（用于安装和配置）的 FTP 站点。

- http://www.mandrake.org/userguide/en/install/000.html#toc

在线 Mandrake Linux 用户指南。

- http://www.slackware.com/zipslack/

使用 Iomega Zip 磁盘下载、安装和配置 Slackware Linux 的链接。

- http://metlab.unc.edu/peanut/features.htm

Peanut Linux 发行版的功能。

- http://www.winlinux2000.com

WinLinux 2000 的下载和购买站点。

- http://elserv.ffm.fgan.de/~lermen/HOME.html

LOADLIN Linux 加载程序的所在地。

- BootPrompt-HOWTO

Paul Gortmaker 关于使用 LILO 启动提示符传递内核参数的指南。

- LILO mini-HOWTO

Cameron Spitzer 关于使用 LILO 的小型指南。

- Linux-DOS-Win95-OS2 mini-HOWTO

Mike Harlan 关于安装和引导四种不同操作系统的指南。

- Linux+FreeBSD mini-HOWTO

Niels Kristian Bech Jensen 关于使用 Linux 和 FreeBSD 的简明巨著，包括引导配置和安装。

- NT OS Loader + Linux mini-HOWTO

Bernd Reichert 关于使用 Windows NT 引导加载程序引导 Linux 的指南。

- Loadlin+Win95 mini-HOWTO

Chris Fischer 关于使用 LOADLIN 和 Windows 95 的长篇指南。

- `/usr/doc/lilo*/doc/User_Guide.ps`

LILO 用户指南（可以在 X11 下使用 `gv` 命令阅读）。一份关于在笔记本电脑或台式机上使用 LILO 的全面 50 页指南。

- `/usr/doc/lilo*/doc/Technical_Guide.ps`

LILO 技术指南（可以在 X11 下使用 `gv` 命令阅读）。一份关于使用 LILO 引导所需了解的一切的八页指南。

- http://www.powerquest.com/usindex.html

PartitionMagic 和 BootMagic 产品的主页。

# 第 4 章：通用安装程序

- 从 CD-ROM 启动
- 创建启动软盘
- 从硬盘分区安装
- 网络安装
- 一些替代方案
- 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_126_0.png)

## 从 CD-ROM 启动

本章向您介绍在笔记本电脑上安装 Linux 的多种方法。当面临在笔记本电脑上安装 Linux 的任务时，了解您的选择至关重要，而实践不同的安装方式有助于您积累经验并建立信心。移动 Linux 用户专注、富有创造力，并且能够适应多种安装技术，这通常是硬件限制（例如缺少内置 CD-ROM 或无法直接引导至安装界面）的结果。

您将了解可以采取的各种技术，以便在您的笔记本电脑上安装 Linux。学习并练习这些技术将使您更深入地了解笔记本的硬件，并作为一名经验丰富的 Linux 安装人员获得经验。

幸运的是，大多数现代笔记本电脑（超轻量级机型除外）都配备了可启动的 CD-ROM。安装 Linux 就像插入 CD-ROM、重启笔记本并清空内置硬盘以安装 Linux 一样简单。如果您使用其他操作系统，例如 OpenBSD 或 FreeBSD，您可以选择拥有两个常驻操作系统，从而创建双启动系统。

从 CD-ROM 启动安装无疑是最简单的 Linux 安装方式。几乎所有的 Linux 发行版（某些小型集合除外）都提供了一个可启动的主 CD-ROM。如果您尝试直接引导到 Linux 安装程序，但发现您的笔记本坚持使用软驱或内部硬盘，请检查您的笔记本 BIOS 设置。您需要重启笔记本，然后按住适当的键以访问 BIOS（请查看制造商提供的手册）。

许多笔记本使用 Phoenix Technologies 的 BIOS。根据 BIOS 版本的不同，第一个屏幕可能如图 4.1 所示。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_128_0.png)

**图 4.1** BIOS 设置对于成功从 CD-ROM 安装 Linux 至关重要。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_128_1.png)

**图 4.2** 使用加号 (+) 键确保笔记本的内置 CD-ROM 位于启动顺序的首位（列表顶部）。

首先，确保您的 CD-ROM 驱动器已被识别。如果您的 CD-ROM 能在笔记本的当前操作系统下正常工作，那么您在启动 Linux 时遇到问题可能性很小。接下来，使用右光标键导航到启动菜单。您的 BIOS 屏幕应如图 4.2 所示。

使用上或下光标键高亮显示您笔记本电脑的 CD-ROM 驱动器。高亮显示后，按加号键 (+) 将 CD-ROM 设备移至列表顶部。此菜单代表您的笔记本搜索可启动设备的顺序。

完成后，按照您的 BIOS 屏幕说明保存并退出 BIOS 设置（Phoenix 用户将按 F10 然后按 Enter）。插入您的可启动 Linux CD-ROM，然后重启笔记本以启动安装程序（假设您对分区策略感到满意）。

## 启动 Yellow Dog Linux iBook 安装

Yellow Dog Linux Champion Server 1.2 直接从 CD-ROM 安装到 Apple iBook 上。使用磁盘设置（Drive Setup）为 Linux 准备一个未分配的分区并重启 iBook 后，安装 BootX 控制面板设备。接下来，将文件 `ramdisk.image.gz` 和 `vmlinux` 复制到您的 Mac 的系统文件夹中。运行 BootX 选择 `vmlinux` 内核，然后点击 BootX 选项按钮以选择使用 RAM 磁盘（Use RAM Disk）选项。请确保也选择无视频驱动程序（No Video Driver）选项。完成后，点击 BootX 对话框中的 Linux 按钮。您将直接引导至 Yellow Dog Linux 安装程序！

## 从 DOS 启动
