

```
CONFIG_TMPFS=y
CONFIG_RAMFS=y
```

当然，还应该添加对内核核心子系统（例如 USB 和 PCI）以及驱动程序的支持。

## 轻量级 udev 实现：BusyBox mdev

嵌入式系统制造商发现，udev 并不总是适合非常小的系统。主要原因是，虽然 udev 的可执行文件是小型 C 程序，但 *udev* 守护进程可能会消耗超过 1 MB 的 RAM，这可能是因为它将规则保存在内存中。

下一章将介绍的工具集 BusyBox 提供了一种轻量级的 udev 实现，称为 *mdev*。如果节省 1 MB RAM 对你的系统很重要，你可能会对 *mdev* 感兴趣。

这是一个使用 *mdev* 的典型系统启动方案：

- 1. 挂载 */sys*：
  `mount -t sysfs none /sys`
- 2. 在 */dev* 上挂载 tmpfs 文件系统：
  `mount -t tmpfs mdev /dev`
- 3. 指示内核在每次热插拔事件发生时调用 */bin/mdev*：
  `echo /bin/mdev > /proc/sys/kernel/hotplug`
- 4. 将已在 */sys* 中找到的设备填充到 */dev*：
  `mdev -s`

请注意，*mdev* 依赖于原始的热插拔基础设施，就像以前的 udev 一样。因为它不使用 netlink 套接字，所以 *mdev* 不需要持续运行，因此不会永久占用 RAM。这对非常小的系统来说是另一个优势。

*mdev* 不具备 udev 那样复杂的命名能力；它只是使用在 */sys* 中找到的原始设备信息来命名设备文件。然而，*/etc/mdev.conf* 文件允许你控制设备文件的权限和所有权。对于此文件中的每个条目，也可以指定专门的脚本，例如，用于重命名设备文件或通知用户空间进程。

关于 BusyBox *mdev* 的更多细节可以在 BusyBox 源代码中的 *docs/mdev.txt* 文件中找到。

## 主要系统应用程序

除了内核的功能和根文件系统的结构外，Linux 继承了 Unix 非常丰富的命令集。问题在于，标准的工作站或服务器发行版配备了几千个命令二进制文件，每个都提供其自己的一组功能。显然，开发人员无法被期望逐一交叉编译如此大量的二进制文件，大多数嵌入式系统也不需要如此庞大的二进制文件库。

因此，有两种选择：选择少数几个标准命令，或者尝试将尽可能多的命令组合成极少数精简的应用程序，以实现基本的整体功能。我们将首先讨论第一种方法，但我们并不推荐它，因为它充其量是繁琐的。相反，我们将主要关注第二种方法以及实现它的各种项目。特别是，我们将讨论 BusyBox（包括 TinyLogin）和 embutils，它们是用于此目的的主要软件包。

### 完整的标准应用程序

如果你希望有选择地包含主流发行版中的一些标准应用程序，你最好的选择是从 Linux From Scratch 项目开始，该项目位于 *http://www.linuxfromscratch.org*。该项目的目标是提供解释和软件包链接，以帮助你构建自己的定制发行版。通过该项目网站可获得的 *Linux From Scratch* 是其主要文档。它包含逐一构建每个应用程序的说明和链接。对于每个软件包，说明提供了构建时间和磁盘空间估算。

或者，你可以从网络上逐一下载应用程序，并按照每个软件包的说明进行编译和交叉编译。由于很少有软件包包含完整的交叉编译说明，你可能需要查看软件包的 *Make files* 以确定适当的构建标志，或进行适当的修改，使软件包能够正确地进行交叉编译。

### BusyBox

BusyBox 项目由 Bruce Perens 于 1996 年发起，以帮助为 Debian 发行版构建安装磁盘。1999 年 12 月，uClibc 的维护者 Eric Andersen 复兴了该项目，最初作为 Linux 开源努力的一部分，后来作为独立于供应商的项目。自那以后，嵌入式 Linux 市场爆发式增长，BusyBox 项目在功能和用户群方面也大幅增长。现在，Busybox 可以在大多数嵌入式 Linux 系统和所有嵌入式 Linux 发行版中找到，并且拥有一个非常活跃的用户社区。项目的位置是 *http://www.busybox.net*。网站包含文档、下载、链接和邮件列表存档。BusyBox 遵循 GNU GPL 许可证。

对 BusyBox 的热情源于它在保持非常小体积的同时提供的功能。BusyBox 通过单个可执行文件实现大多数 Unix 命令，该文件小于 1 MB（与 glibc 静态链接）或小于 500 KB（与 uClibc 静态链接）。BusyBox 甚至包括 DHCP 客户端和服务器（*udhcpc* 和 *udhcpd*）、包管理器（*dpkg* 和 *rpm*）、具有大部分功能的 *vi* 实现，最后但同样重要的是，还有一个 Web 服务器。该服务器应能满足许多嵌入式系统的典型需求，因为它支持 HTTP 身份验证、CGI 脚本和外部脚本（例如 PHP）。为具有所有功能的该服务器配置支持，仅为 BusyBox 1.5.0 增加了 9 KB（在 i386 上与 glibc 动态链接）。

使用 BusyBox 代替其包含的标准版本实用工具，可以节省大量存储空间——可能是数十兆字节。你还将节省大量时间，并发现更容易实现一个简单的系统，因为你不需要配置和构建每个工具的源代码。†

尽管 BusyBox 不支持其替代命令提供的所有选项，但它提供的子集对于大多数典型用途来说已经足够。BusyBox 发行版的 docs 目录包含其多种不同格式的文档。BusyBox 支持第 3 章中涵盖的所有架构。它可以静态或动态链接到 glibc 或 uClibc。

#### 设置

首先，你需要从项目网站下载一份 BusyBox 软件包副本，并放入你的 ${PRJROOT}/sysapps 目录中。本节示例将使用 BusyBox 1.4.2。

软件包解压后，在剩下的设置过程中进入其目录：

```
$ cd ${PRJROOT}/sysapps/busybox-1.4.2
```

从 1.3 版本开始，BusyBox 使用与 Linux 2.6 内核完全相同的配置工具。因此，描述配置参数的 Config 文件与内核 Kconfig 文件具有相同的语法。同样，所有配置设置都存储在根源代码目录中的 .config 文件中，可以使用相同的配置命令创建：

```
make xconfig
```

此命令启动基于 Qt 的图形界面 qconf，用于配置 Linux 内核。但是，BusyBox 发行版并不包含来自最新内核发行版的 qconf 版本。例如，BusyBox 1.4.2 的 qconf 在当时 Linux 版本中出现的搜索功能并未包含。

```
make gconfig
```

此命令启动 qconf 的 GTK 等价物。

> † 有些人坚持使用术语 GNU/Linux 而不仅仅是 Linux，以强调 GNU 项目的巨大贡献及其核心价值。虽然 GNU 开发工具链仍然是必不可少的，但许多使用 BusyBox 和 uClibc 库的嵌入式 Linux 系统不再包含任何 GNU 组件。因此，这样的系统可以被称为 BusyBox/Linux。

#### make menuconfig

这个基于 *ncurses* 库的基于文本的界面，是大多数 BusyBox 用户所熟悉的。在内核配置界面引入之前的几年里，它是友好的配置工具。

#### make defconfig

此命令为 BusyBox 提供通用配置。它启用大多数常用选项，可用于首次尝试 BusyBox 的人的初始配置。

#### make allnoconfig

此命令配置 BusyBox 仅启用最少的选项。通常在运行其中一个配置界面之前运行，因为它有助于构建仅包含系统所需功能的嵌入式系统。

#### make oldconfig

不要被此命令的名称混淆。它不是配置 BusyBox 的旧方法。相反，它旨在处理现有的 .config 文件，通常来自旧版本。每当引入新参数时，此命令行界面会要求用户选择一个值，而不是像 make xconfig、make gconfig 或 make menuconfig 那样静默选择一个默认值。

当在 .config 文件中进行手动更改时，使用此命令也是必不可少的。许多配置选项依赖于其他选项，因此当你启用某个选项时，可能需要新的选项。例如，一旦你启用了 *ls* 命令的支持，你需要将此命令的每个可选功能设置为 *y* 或 *n*。make oldconfig 会提示你为未定义的选项输入值，从而避免编译失败。

#### make help

这不是配置命令，但它解释所有可用的 Makefile 目标，例如 make clean、make mrproper 和 make install。你可以在较新版本的 BusyBox 上使用此命令来了解新的 Makefile 功能。由于 .config 文件包含主 Makefile 引用的 Makefile 变量定义，因此也可以在 make 命令行上定义配置设置。

### 编译

BusyBox 有几个配置选项来控制其构建方式。主要的是 CONFIG_STATIC。默认情况下，BusyBox 与 C 库动态链接。然而，在仅使用 BusyBox 和少数少量额外二进制文件的小系统中，将所有内容静态编译（为 BusyBox 设置 CONFIG_STATIC=y）可能是有意义的。这样，文件系统中不再需要整个 C 库，使系统更简单，而且通常更小，因为不包含 C 库符号的未使用部分。

