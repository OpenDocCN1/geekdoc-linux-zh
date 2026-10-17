
在你最初安装 Linux 后，你可能希望创建一个新内核，该内核仅包含对你系统中已安装硬件的支持。特别是，如果你有一个 SCSI 适配器，你可能希望创建一个将 SCSI 驱动程序链接在内的内核。附赠 DVD-ROM 上的内核将 SCSI 驱动程序包含为外部模块，由内核在启动时加载。

如果你的系统拥有仅提供实验性支持的硬件，你必须重新构建内核以将该支持整合到操作系统中。

你可能希望重新编译内核并生成在你的特定 Pentium 处理器上运行良好的代码，而非大多数 Linux 发行版中通用的 386 处理器代码。

![](img/792720823146d68f19fd50c99ebfce4b_499_0.png)

要重新构建 Linux 内核，你需要内核源文件。内核源文件通常不会安装。请使用你的发行版的软件安装工具来安装内核源软件包。

![](img/792720823146d68f19fd50c99ebfce4b_499_1.png)

Fedora Core 不提供内核源软件包。相反，你必须安装源 RPM 文件 `kernel-version.src.rpm`，其中 `version` 是内核版本号。你可以在 Fedora Core 在线存储库的 SRPMS 目录中找到内核 SRPM。你必须使用命令 `rpm -Uvh kernel-version.src.rpm` 安装内核 SRPM。然后输入 `cd /usr/src/redhat/SPECS`，接着输入 `rpmbuild -bp --target $(arch) kernel.spec`。为了使内核源文件在 `/usr/src/linux` 目录中可用，请输入以下命令。将 `version` 替换为通过 `uname -r` 命令获取的内核版本号。

```
cd /usr/src/redhat/BUILD/kernel-VERSION/usr/src/
mv linux-VERSION /usr/src/
cd /usr/src/
ln -s ./linux-VERSION linux
```

![](img/792720823146d68f19fd50c99ebfce4b_499_2.png)

在 SUSE 中，使用 YaST 的软件管理工具来安装内核源——要找到它，请使用 YaST 软件安装窗口中的搜索功能，搜索 `kernel-source`。安装内核源软件包后，源文件将出现在 `/usr/src/linux-version` 目录中，其中 `version` 是内核的版本号。因此，对于内核版本 `2.6.13`，源文件位于 `/usr/src/linux-2.6.13` 目录中。一些发行版会自动将 `/usr/src/linux` 设置为指向包含 Linux 内核源文件的特定版本目录的符号链接。

## 重新构建内核

基于 Debian 的发行版中，内核源代码安装在 `/usr/src/kernel-source-version` 目录中，其中 `version` 表示内核版本。因此，对于内核版本 `2.6.11`，源代码位于 `/usr/src/kernel-source-2.6.11`。要在 Debian 中切换到内核源代码目录，请输入 `cd /usr/src/kernel-source*`。

构建内核包括以下几个阶段：

- 配置内核
- 构建内核
- 构建并安装模块
- 构建新的初始 RAM 磁盘 `initrd` 文件
- 安装内核并设置 GRUB

我将在接下来的几部分中解释这些阶段，但首先你需要了解将驱动链接进内核与将驱动构建为可加载模块之间的区别。

## 创建单体式内核与模块化内核

对于支持 Linux 中各种硬件设备所需的设备驱动程序，你有两种选择：

- **链接支持：** 你可以将系统上所有硬件的驱动链接到内核中。随着设备驱动程序代码被整合进内核，内核的大小会增加。将所有必要代码链接在一起的内核被称为*单体内核*，因为它是一个大的文件。
- **使用模块：** 你可以将设备驱动程序创建为可加载内核模块的形式。*模块*是一组代码，内核在开始运行后就可以加载它。使用模块的典型场景是在支持新设备时，无需为每个新设备重新构建内核。模块并不一定是设备驱动程序；它们也可以为内核添加新的功能。使用模块的内核被称为*模块化内核*。

你不必创建一个完全单体式或完全模块化的内核。实际上，将部分支持直接链接到内核中，而将不常用的设备驱动程序构建为模块的形式，这是一种常见的做法。对于 Linux 发行版来说，包含一个主要由模块组成的内核是有意义的，同时配备大量可以支持许多不同类型硬件的模块。然后，Linux 安装程序会配置系统，使其仅加载支持用户系统中已安装硬件所需的模块。

当你为你的硬件配置创建自定义内核时，你可能希望将所有必需的设备驱动程序链接到内核中。你仍然可以控制这种单体内核的大小，因为只链接你系统上安装的特定硬件组合的设备驱动程序。

## 配置内核

重新构建内核的第一步是配置它。要配置内核，请以 `root` 身份登录。然后使用 `cd` 命令更改内核源代码目录，如下所示：

```
cd /usr/src/linux*
```

要配置内核，你必须指明希望在你的 Linux 内核中包含哪些特性和设备驱动程序。本质上，你构建了一个仅包含你所需要特性的你自己的 Linux 内核版本。

Linux 提供了几种配置内核的方法：

- 输入 `make menuconfig` 通过类似文本模式 Linux 安装程序所使用的基于文本的界面输入内核配置参数。
- 输入 `make xconfig` 使用基于 X Window 系统的配置程序来配置内核。你需要运行 X 才能使用这个具有图形界面的配置程序。你还必须安装 Qt 开发 `qt-devel` 包，并将 `QTDIR` 环境变量设置为 Qt 安装的目录。如果你已安装 `qt-devel` 包，请输入 `export QTDIR=/usr/lib/qt-3.3` 以正确定义 `QTDIR`。
- 输入 `make config` 使用一个 shell 脚本，逐个询问每个配置选项。你可以从 Linux 命令提示符使用此配置程序。使用此选项时，你需要经历一个较长的问答过程来指定配置参数。对于每个问题，输入 `y` 将支持链接到内核，输入 `m` 构建模块，输入 `n` 跳过对该特定设备的支持。
- 输入 `make oldconfig` 使用 shell 脚本在升级源代码后重新配置内核。此配置脚本保留现有选项，并只提示你输入新增或更改的选项。

`make menuconfig`、`make xconfig`、`make config` 和 `make oldconfig` 命令达到相同的结果——每个命令都将你的选择存储在位于 `/usr/src/linux*` 目录中名为 `.config` 的文本文件中。由于文件名以句点开头，仅使用 `ls` 命令列出目录时你看不到它。相反，输入 `ls -a` 即可在目录列表中看到 `.config` 文件。

内核配置步骤仅仅是将你的选择捕获在 `.config` 文件中。事实上，直到你第一次配置内核之前，`.config` 文件并不存在。在使用 `make` 命令编译内核之前，内核文件不会改变。这意味着你可以任意多次执行内核配置选项。如果你希望从默认设置重新开始，请在开始配置内核之前输入以下命令：

```
make mrproper
```

若要查看你可以使用 `make` 命令执行的内核配置构建步骤概述，请在终端窗口中输入以下内容，在输入 `cd /usr/src/linux*` 将当前目录更改到正确位置之后：

```
make help | more
```

在开始重新配置内核之前，先看一下典型的 `.config` 文件。例如，以下是在我配置内核后在 Linux 系统上输入 `more .config` 时输出的一些行：

```
#
# Automatically generated make config: don't edit
CONFIG_X86=y
CONFIG_MMU=y
CONFIG_UID16=y
CONFIG_GENERIC_ISA_DMA=y
CONFIG_GENERIC_IOMAP=y
#
# Code maturity level options
#
CONFIG_EXPERIMENTAL=y
CONFIG_CLEAN_COMPILE=y
CONFIG_BROKEN_ON_SMP=y
CONFIG_INIT_ENV_ARG_LIMIT=32
#
# General setup

CONFIG_LOCALVERSION=""
CONFIG_SWAP=y
CONFIG_SYSVIPC=y
... lines deleted ...
```

基本上，每个配置选项都有一个名称，并且每个选项都被赋予一个值。名称以 `CONFIG_` 开头，后跟一个标识该选项的单词。每个被选中的选项的值为 `y` 将该特性的支持链接到内核或 `n` 为该特性使用模块。以 `#` 开头的行是注释。注释行列出了未选中的特性。
