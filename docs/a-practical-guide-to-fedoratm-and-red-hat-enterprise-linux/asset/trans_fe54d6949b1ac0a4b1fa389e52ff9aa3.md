

- 将 ISO 映像文件写入 USB 闪存盘（Windows 和 Linux）：fedorahosted.org/liveusb-creator（liveusb-creator 软件包）和 unetbootin.sourceforge.net（unetbootin 软件包）
- 硬件兼容性：hardware.redhat.com
- RHEL 版本：www.redhat.com/products/enterprise-linux/server/compare.html
- 升级：fedoraproject.org/wiki/FedUp
- 验证下载的 ISO 映像文件（Linux 和 Windows）：fedoraproject.org/en/verify
- 发行说明：docs.fedoraproject.org/en-US/Fedora/19/html/Release_Notes
- 交换空间：docs.fedoraproject.org/en-US/Fedora/13/html/Installation_Guide/s2-diskpartitioning.html
- 刻录 DVD 或写入 USB 闪存盘：docs.fedoraproject.org/en-US/Fedora/19/html/Installation_Guide/sn-making-media.html
- 从 USB 闪存盘安装：docs.fedoraproject.org/en-US/Fedora/19/html/Installation_Guide/Making_USB_Media.html
- RAID：raid.wiki.kernel.org/index.php/Linux_Raid
- PXE：www.kegel.com/linux/pxe.html

### 下载
- Fedora/RHEL
- 最简单的下载方式：fedoraproject.org/get-fedora
- 下载资源：fedoraproject.org/get-fedora-all
- 比特流（Torrent）：torrent.fedoraproject.org
- Fedora 和 EPEL 镜像：mirrors.fedoraproject.org/publiclist
- 所有资源：dl.fedoraproject.org/pub
- RHEL 额外软件包：fedoraproject.org/wiki/EPEL
- 转发行版（Spins）：spins.fedoraproject.org

## 规划安装

在规划安装过程中的主要决策是如何将硬盘划分为分区，或者在双启动系统的情况下，确定将 Linux 分区放在哪里。安装完系统后，您可以决定想向基础系统添加哪些软件包（或者是否想要移除某些软件包）。除了这些主题之外，本节还讨论了硬件要求。

## 注意事项

### SELinux
SELinux（Security-Enhanced Linux，安全增强型 Linux）通过在内核中实施强制访问控制策略来增强系统安全性（第 473 页）。默认情况下，Fedora 以强制执行模式安装 SELinux，该模式实施了最佳实践安全策略。尽管您可以在安装系统之前或之后将 SELinux 设置为宽容模式或禁用模式，但这不是一个好主意，因为 SELinux 保护着系统。有关 SELinux 的更多信息，请参阅第 473 页。如果您希望在安装系统时关闭 SELinux，请参阅 selinux 引导参数（第 72 页）。

### 图形用户界面 (GUI)
服务器系统可以通过不包含图形用户界面（GUI）来节省资源。在其他系统中，GUI 提供了拥有多个工作区的桌面环境，可以包含许多窗口。Fedora/RHEL 默认安装 GNOME。

## 硬件要求

### 硬件
本章和第 3 章涵盖了在 64 位处理器架构上安装操作系统的过程，例如 AMD64 处理器和具备 Intel EM64T 技术的 Intel 处理器，以及较旧的 32 位 Intel 和兼容处理器架构（包括 AMD 处理器）。在这些处理器架构中，Fedora/RHEL 可以运行于许多可用的硬件上。您可以在 hardware.redhat.com 查看兼容和受支持硬件的列表。虽然这些列表针对的是 RHEL，但它们为 Fedora 可运行的硬件提供了良好的参考。Fedora 发行说明也提供硬件信息。许多互联网网站讨论了 Linux 硬件；使用 Google 搜索 **linux hardware**、**fedora hardware**，或者 **linux** 加上您想了解更多信息的具体硬件（例如，**linux sata** 或 **linux a8n**）。此外，许多 HOWTO 文档涵盖了特定硬件。*Linux 硬件兼容性 HOWTO* 也可供查阅，尽管在阅读时它可能不是最新的。除非系统包含非常新或特殊的组件，否则 Fedora/RHEL 通常可以在 Windows 运行的相同系统上运行。

如果您正在旧式或极简硬件上安装 Fedora 并希望运行图形用户界面（GUI），请考虑安装 LXDE（第 118 页），因为它提供一个轻量级桌面，比 GNOME 更有效地利用系统资源。

### CPU（处理器）
至少，Fedora 需要 Intel Pentium Pro 处理器；它针对 i686 及更新的处理器进行了优化。文本系统的最低建议处理器速度为 500-700 兆赫兹，图形系统的最低建议为 1 吉赫兹。访问 www.redhat.com/products/enterprise-linux/server/compare.html 获取有关 RHEL 系统的信息。

### RAM（内存）
32 位和 64 位 Fedora 系统的内存要求相同。至少，文本（命令行）系统需要 32 兆字节 RAM，图形（桌面）系统需要 1 吉字节 RAM。在某些情况下，对于非常极简的文本安装，可以使用更少的 RAM。运行实时会话（来自 Live Image）至少需要 1 吉字节 RAM。访问 www.redhat.com/rhel/compare 获取有关 RHEL 系统的信息。

Linux 能很好地利用额外内存：系统的内存越多，运行速度越快。对于未受 CPU 限制的系统，增加内存是提升 Linux 系统速度最具成本效益的方法之一。

### 硬盘空间

系统所需的硬盘空间量取决于您安装的是 Fedora/RHEL 的哪个版本、安装了哪些软件包、安装了多少种语言以及用户数据（您的文件）需要多少空间。Fedora 操作系统通常需要 10 吉字节，尽管极简系统可以使用少得多的空间。用户数据需要额外的空间。为了确保文件系统正常操作，请保留至少 5% 的磁盘空间为空。访问 www.redhat.com/rhel/compare 获取有关 RHEL 系统的信息。

### BIOS 设置

现代计算机可以设置为从 DVD、硬盘或 USB 闪存盘启动。BIOS 决定系统尝试从每个设备启动的顺序。您可能需要更改此顺序：确保 BIOS 设置为在尝试从硬盘启动之前先尝试从 DVD 或 USB 驱动器启动。此外，如果您想在系统上运行虚拟机（第 17 章），可能需要在 BIOS 中启用虚拟化。有关 BIOS 的更多信息，请参阅第 590 页。

### CMOS

CMOS 是存储硬件配置信息的持久内存。要更改 BIOS 设置，您需要编辑存储在 CMOS 中的信息。当系统启动时，它会显示一条简短消息，说明如何进入系统设置或 CMOS 设置模式。按下指定的按键，然后将光标移动到处理系统启动的屏幕和行。通常有一个包含三个或四个设备的列表，系统会依次尝试从这些设备启动；如果第一次尝试失败，系统会尝试第二个设备，依此类推。调整该列表，使 DVD 或 USB 闪存盘成为第一选择，保存列表并重新启动。请参阅硬件/BIOS 手册以获取更多信息。

## 处理器架构

安装介质包含编译为在特定处理器架构（处理器或 CPU 类别）上运行的程序。以下列表描述了 Fedora/RHEL 所编译支持的每种架构。访问 docs.fedoraproject.org/en-US/Fedora/19/html/Installation_Guide/ch-new-users.html#hn5-which-arch 以查看每种架构中处理器的详细列表。由于 Linux 源代码对所有人开放，具备知识的用户可以编译 Fedora/RHEL 以在其他处理器架构上运行（第 14 章）。

### i386/i686 (Intel x86)

Fedora/RHEL 32 位 PC 安装介质上的软件编译为在 Intel x86 兼容处理器上运行，包括大多数配备 Intel 和 AMD 处理器的机器、几乎所有运行 Microsoft Windows 的机器，以及使用 Intel 处理器的较新的 Apple Macintosh 机器。N200 和 Z 系列 Atom 处理器也基于此架构。如果您不确定机器拥有哪种类型的处理器，请假设它具有此类型的处理器。

### x86_64 (AMD64 和 Intel EM64T)

Fedora/RHEL 64 位 PC 安装介质上的软件编译为在 AMD64 处理器上运行，包括 Athlon64、Opteron，以及集成 EM64T 技术的 Intel 64 位处理器，例如 EM6T2 Xeon。N 系列 Atom 处理器（除 N200 外）也基于此架构。

### Mac PowerPC (ppc)

Fedora/RHEL PPC 版本运行于 Apple Macintosh G3、G4、G5、PowerBook 和基于 PPC 的 Macintosh。

