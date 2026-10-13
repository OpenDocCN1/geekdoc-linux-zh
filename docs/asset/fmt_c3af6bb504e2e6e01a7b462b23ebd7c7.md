
该网站提供了如产品更新和错误列表、硬件兼容列表以及安装指南和手册等链接。特别是，你可以在 `http://www.redhat.com/apps/support/resources/` 找到手册和常见（常见问题）。

如果你对开源开发（包括 Linux）感兴趣，一个很好的资源是 `http://sourceforge.net` SourceForge.net 网站。

## 新闻组

为了跟上 Linux 的进展，你需要访问互联网，特别是新闻组。可以在表格 G-1 列出的新闻组找到有关特定 Linux 相关主题的讨论。

| 表格 G-1：互联网上的 Linux 新闻组 |
| 新闻组 | 提供以下内容 |
| comp.os.linux.admin | 关于 Linux 系统管理的信息 |
| comp.os.linux.advocacy | 关于推广 Linux 的讨论 |
| comp.os.linux.announce | 关于 Linux 的重要公告。（这是一个受审核的新闻组，这意味着你必须向管理员发送邮件，由他们将其发布到新闻组。） |
| comp.os.linux.answers | 关于 Linux 的问答。（所有的 Linux HOWTO 都发布在这个新闻组中。） |
| comp.os.linux.development | 当前 Linux 开发 |
| comp.os.linux.development.apps | Linux 应用开发 |
| comp.os.linux.development.system | Linux 操作系统开发 |
| comp.os.linux.hardware | 关于 Linux 及其各个方面的讨论 |
| comp.os.linux.help | 关于 Linux 各个方面的帮助 |
| comp.os.linux.misc | 关于 Linux 的杂题 |

## 附录 G：Linux 资源 993

| 新闻组 | 提供以下内容 |
| --- | --- |
| comp.os.linux.admin | 网络 |
| comp.os.linux.advocacy | Linux 安装 |
| comp.os.linux.announce | 设置 Linux |
| comp.os.linux.answers | Red Hat Linux |
| comp.os.linux.development | Red Hat Linux |
| comp.os.linux.development.apps | Linux 设置 |
| comp.os.linux.development.system | Red Hat Linux |
| comp.os.linux.hardware | Red Hat Linux |
| comp.os.linux.help | Red Hat Linux |
| comp.os.linux.misc | Red Hat Linux |

## 系统要求

请确保您的计算机符合本节列出的最低系统要求。如果您的计算机不符合这些大部分要求，您在使用 CD-ROM 时可能会遇到问题。

- 运行速度在 200MHz 或以上的奔腾处理器的 PC
- 计算机上至少安装了 64MB 总内存；为了获得最佳性能，我们建议至少 128MB
- 硬盘上至少有 4GB 空闲空间
- 以太网网卡 `NIC` 或速度至少为 56 Kbps 的调制调器
- 一个 CD-ROM 驱动器

## CD-ROM 安装说明

安装在 Linux 中可能是一个棘手的步骤。您需要特定的硬件信息，例如磁盘控制器、显卡和 CD-ROM 驱动器。Linux 通过驱动程序控制硬件，因此您需要确保当前的 Linux 版本包含适用于您硬件的驱动。由于 Linux 是免费的，您无法真正要求——或期待——对特定硬件的支持。然而，Linux 通过全球范围内程序员的合作正在不断改进。如果您的硬件足够流行，很有可能已经有人为其开发了驱动程序。无论如何，随附 CD-ROM 上的 Red Hat Linux 已经支持各种硬件，您 PC 的所有外设都能得到适当支持。

以下步骤说明了安装和配置 Linux 以及 X Windows系统的通用步骤。

1. 在安装 Linux 之前，收集有关您的 PC 硬件的信息，例如显卡、网络和 SCSI 卡。
2. 通过缩小现有 Windows 分区的大小为 Linux 留出空间。对于 Windows 95/98/Me，使用无破坏性重新分区程序 `FIPS` 对硬盘进行分区，而不会破坏现有内容。对于使用 NTFS 分区的 Windows NT/2000/XP 系统，使用商业磁盘分区程序（例如 PowerQuest 的 `PartitionMagic` (`http://www.powerquest.com/partitionmagic/`)）来缩小 NTFS 分区并为 Linux 留出空间。如果您计划将 Linux 作为唯一的操作系统，或者计划在 DOS/Windows 分区或空闲硬盘上安装 Red Hat Linux，请跳过此步骤。
3. 如果您的 PC 无法直接从 CD-ROM 启动，请将在 DOS 或 Windows 下创建 Linux 安装启动。
4. 从第一个 CD-ROM 启动您的 PC 或使用 Linux 安装启动盘启动（无论哪种情况，请确保第一个 CD-ROM 已在 CD-ROM 驱动器中）。此过程会自动运行 Red Hat 安装程序。从现在起，您必须响应多个对话框，因为 Red Hat 安装程序将引导您完成步骤。以下是一些关键安装步骤：

- 识别安装在 PC 上的任何 SCSI 适配器。
- 让安装程序使用您通过缩小现有 Windows 分区创建的空闲空间为 Red Hat Linux 创建分区。

## 附录 H：关于 CD-ROM 997

- 配置以太网（如果有）。您可能需要指定参数，例如 Red Hat Linux 系统的 IP 地址和主机名。
- 指定本地时区并设置根密码。
- 在硬盘的主引导记录 `MBR` 上安装 `GRUB` 引导加载程序，以便您在关闭 PC 后开机时启动 Linux。
- 选择您想要安装的特定软件包组，例如 X Window 系统和 Gnome 桌面环境。
- 配置 X Window 系统并启用图形登录界面，这样当您启动 Linux 系统时，它会显示登录对话框并在成功登录后直接进入 GNOME 或 KDE 图形桌面。

要将特定项目从 CD-ROM 安装到您的硬盘上，请按照以下步骤操作：

1. 以 root 身份登录。
2. 将 CD-ROM 插入计算机的 CD-ROM 驱动器。
3. 如果您使用 GNOME 或 KDE GUI，请等待光盘挂载。否则，打开终端窗口并在命令提示符输入：
```
mount /dev/cdrom /mnt/cdrom
```
4. 浏览 CD-ROM 并按照第 21 章中的指令安装单个软件包。
5. 要从 CD-ROM 驱动器中移除 CD-ROM，请在命令提示符输入：
```
umount /mnt/cdrom
```
您也可以在桌面上右键点击 CD-ROM 图标并从选项中选择“弹出”。这将卸载您的 CD-ROM 并将其弹出。

## CD-ROM 中的内容

您可以在 Red Hat Linux 9 CD-ROM 上找到以下软件：

- Linux 内核 `2.4.20`，带有适用于所有主要 PC 硬件配置的驱动模块，包括 IDE/ATA 和 SCSI 驱动器、PCMCIA 设备和 CD-ROM
- 一套完整的设备（如键盘和鼠标）等设备的安装和配置工具
- 基于 XFreeBee 4.3.0 软件包的图形用户界面，带有 GNOME 和 KDE 桌面
- 用于 Internet、局域网和内网的完整 TCP/IP 网络功能
- 使用 PPP、SLIP 或拨号串口通信程序将 PC 连接到互联网服务提供商 `ISP` 的工具
- 一套完整的 Internet 应用程序，包括电子邮件 `sendmail` 和 `mail`、新闻 `inet`、Telnet、FTP、DNS 和 NSF
- Apache httpd `web` 服务器 `2.0.40`，将您的 PC 变为 Web 服务器；以及 Mozilla `1.2.1`，用于上网。
- Xianian Evolution `1.2.2` 免费电子邮件和日历应用程序
- OpenOffice.org `1.0.2` 办公套件，带有文字处理器、电子表格、软件等功能
- Samba `2.2.7a` LAN 管理器，用于 Microsoft Windows 连接并将 Linux 系统集成到 Windows 网络
- 若干文本编辑器（例如 GNU Emacs `21.2`；vim）
- 图形和图像处理软件，例如 GIMP、XPaint、Xfig、Gnuplot、Ghostscript、Ghostview 和 ImageMagick
- 编程语言（GNU C 和 C++ `3.2.2`、Perl `5.8.0`、Te/Tk `8.3.5`、Python `2.2.2`、GNU AWK `3.1.1`）和软件开发工具（GNU Debugger `5.3`、CVS `1.11.2`、RCS `5.7`、GNU Bison `1.35`、flex `2.5.4a`、TIFF 和 JPEG 库）
- 支持行业标准执行链接格式 `ELF` 和 Intel 二进制兼容规范 `iBCS`
- 来自 GNU 项目的标准 Unix 工具套
- 访问和使用 DOS 文件和程序的工具 `mtools 3`
- 文本格式化和排版 `DocBook`、`groff`、`TeX`、`LaTeX`

## 源码券

随-ROM 的源码自购买之日起有效期一年。此优惠在美国内为 9.95 美元，境外订单为 13.95 美元。

## 故障排除

在使用任何 CD-ROM 时遇到困难，请拨打客户服务热线 `800` `572-2974` 或发送电子邮件至 `techup@wiley.com`。有关详细说明，请参阅第 2 章。

# 1000 索引

以下为索引内容节选，保留核心条目格式。完整索引包含大量条目，为保持可读性已按原章节保留标题层级。

## Apache Web

- HTTP 服务器，虚拟主机和, 431–434
- httpd 服务器，与 Tomcat 的测试, 442–443
- httpd 源码 RPM 安装, 439–440
- 安装, 421–422
- Java servlets 和, 436–437
- Java 2 SDK 安装, 438
- mod_jk 模块, 440–441
- 进一步阅读资源, 421
- SSIs 和, 434–435
- Tomcat, 437

## CD-ROM 安装指南

将 CD-ROM 插入您的 CD-ROM 驱动器。CD-ROM 上的安装程序会自动启动，并显示可安装选项的对话框。选择您想要安装的选项，以及您想要安装软件的驱动器和子目录。

有关安装 CD-ROM 的更多信息，请参阅附录 H。

## RED HAT LINUX 9 内部秘籍

只有专家才能解锁 Red Hat Linux 9 最深层的秘密——揭示其内部真实的运作机制以及如何释放其全部潜力。从无忧安装到 shell、Perl 和 Tcl/Tk 编程，从配置带有 SSL 的 Apache 服务器，这是关于您想了解的 Red Hat Linux 9 的一切问题的内部指南。

## 发挥 Red Hat Linux 9 的力量

- 在笔记本电脑上安装 Red Hat Linux（参见第 2 章）
- 为 PC 显卡配置 XFree86™（参见第 3 章）
- 建立 CUPS 打印队列（参见第 4 章）
- 为未识别的声卡手动加载驱动程序（参见第 5 章）
- 找回忘记的密码（参见第 12 章）
- 挂载 NTFS 分区（参见第 12 章）
- 设置 Wi-Fi 无线局域网（参见第 13 章）
- 升级并自定义内核（参见第 21 章）

## GNU 通用公共许可证

第2版，1991年6月
版权所有 © 1989, 1991 Free Software Foundation, Inc.

## 无保证

11. 由于程序是免费许可的，在适用法律范围内，程序不提供任何保证。

```
