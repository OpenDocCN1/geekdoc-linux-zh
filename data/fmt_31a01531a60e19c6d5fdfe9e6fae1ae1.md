
已经是最新（up to-date）。

你刚刚下载的文件应该是最新的，如示例所示。每当你想要将工作目录中的代码与 URL 上的最新源码同步时，随时执行此命令。

# 阅读文档

内核包包含了最新的文档，其中某些可能在其他文档中没有。你可能希望查看内核源码目录顶部的 `README` 文件以及 `Documentation` 子目录下的相关文件。此外，`/usr/share/doc/kernel-package` 目录下有大量信息。阅读《Linux Kernel-HOWTO》可以获得关于安装和配置 Linux 内核的详细但有些过时的通用指南。

# 配置并编译 Linux 内核

本节介绍了如何配置内核、如何编译内核以及如何下载和编译内核模块。

## .config：配置内核

在编译代码并创建 Linux 内核之前，你必须决定并指定你希望内核支持的功能。你可以通过两种方式配置内核支持大多数功能：将功能构建到内核中，或将功能指定为可加载内核模块（第 564 页），根据需要加载到内核中。在决定使用哪种方法时，你必须权衡内核的大小与加载模块的时间。让内核尽可能小，同时尽量减少加载模块的频率。除非必要，否则不要使用 SCSI 驱动模块化。

你下载源码目录中的 `.config` 文件控制了新内核将支持哪些功能以及如何支持它们。“自定义内核”（第 561 页）解释了如果该文件不存在如何创建一个默认版本的内核，以及如果它已存在如何编辑该文件。

## 替换自定义内核

如果你已经配置了一个自定义内核，你可能想将其替换为配置相似的更新内核。然而，每个内核都可能具有不同的配置选项，因此使用旧的 `.config` 文件编译新内核是一个糟糕的做法。本节介绍了如何升级现有的 `.config` 文件，它包含了新内核特有的选项，并保留了旧选项的现有配置。

在你下载或提取源码的目录中工作。系统在 `/boot/` 中保留了运行的本地系统的配置文件副本。以下命令将该文件复制到工作目录：

```
$ cp /boot/config-$(uname -r) .config
```

执行 `make oldconfig` 命令，它会显示新内核中新增的选项并保留旧选项的现有配置。如果你想对新内核的选项进行交互式确认，可以使用 `make menuoldconfig`，它会询问所有新内核中新增的选项。如果你想从头开始配置内核，可以使用 `makeconfig`。如果你想使用默认配置内核，可以使用 `make defconfig`，它会根据架构创建一个默认的 `.config` 文件。

完成后，使用 `make` 命令来编译内核：

```
$ make
```

编译完成后，内核镜像将位于 `arch/x86/boot/vmlinuz`，内核模块将位于 `/lib/modules/$(uname -r)/`。你可以使用以下命令安装编译好的模块：

```
$ make modules_install
```

最后，更新 GRUB 配置以加载新内核：

```
$ sudo update-grub
```

现在，你就可以重启系统并使用新编译的内核了。

# 第 15 章 构建 Linux 内核

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_613_0.png)

图 15-1 Linux 内核配置窗口，分屏视图

图 15-1 显示了分屏视图。在此中，左帧显示选项，右上视图列出每个选项的功能。右下视图描述选中的选项或功能。图 15-2 显示视图。

在任何视图中，你都可以点击选项和子选项旁边的框和圆。空框/空圆表示功能被禁用，打钩表示它被包含在内核中，点则表示它可以编译为模块。当选中某个选项或子选项时，你还可以按 `M` 表示模块，按 `N` 表示不包含，按 `Y` 表示编译进内核。选择菜单栏：`Options`（选项)->`Show All Options`（显示所有选项）以显示所有选项和功能。

遍历选项并按照你希望在内核中配置的方式标记功能。在配置过程中的任何时候，你都可以将当前定义的配置保存到文件中、从文件中加载配置，或退出时不保存更改。选择菜单栏：`File`（文件)->`Save and close`（保存并关闭）窗口。

## 清理源码树

在生成 `.config` 文件之后编译或重新编译内核之前，使用以下命令清除源码树中所有可能过时的 `*.o` 文件：

```bash
$ make-kpkg clean
exec make -f /usr/share/kernel-package/ruleset/minimal.mk clean
==== making target minimal_clean J====
Cleaning.
test ! -f .config | cp -pf .config.precise
test ! -e stamp-building | rm -f stamp-building
test ! -f Makefile || \
    make ARCH=i386 distclean
make[1]: Entering directory '/usr/src/linux-source-2.6.27'
CLEAN scripts/basic
CLEAN scripts/config
CLEAN /usr/src/linux-source-2.6.27/debian/
CLEAN include/config
CLEAN .config.old include/linux/autoconf.h
make[1]: Leaving directory '/usr/src/linux-source-2.6.27'
test ! -f config.precious || mv -f config.precious
rm -f modules/versions/kvsym.ver.conf scripts/cramfs/cramfsck
scripts/cramfs/mkramfs applied_patches stamp-build stamp-configure stamp-image stamp-headers-src stamp-diff stamp-doc manual-stamp-patch stamp-buildpackage stamp-debian
```

此命令确保在编译内核时能够正确应用任何编号方案。请以特权用户身份继续。

## 编译内核镜像和可加载模块

请参第 556 页的“前提”，获取编译源码必须安装的软件包列表。执行以下命令编译内核和模块。该命令会在工作目录的一部分生成一个 `.deb` 文件。

```bash
$ make-kpkg -intrd rootcmd fakeroot --append-to-version $(+s) kernel_image
exec make -f /usr/kernel-config/ruleset/minimal.mk deb
APPEND_TO_VERSION=1219799154 INTRO=ROOT_CMD=fakeroot
===== making target minimal_deb [new preqs]: =====
This is kernel package version.
test -d debian | mkdir deb
test ! -e stamp-building | rm -f stamp-building
Found kernel: /boot/vmlinuz-2.6.27-rc412199154
Found kernel: /boot/last-good-boot/vmlinuz
Found kernel: /boot/vmlinuz-2.6.5-generic
Found kernel: /boot/memtest86+.bin
Replacing config file /var/run/grub/menu.lst with new version
Updating /boot/grub/menu.lst
Examining /etc/kernel/postinst.deb
run-parts: executing /etc/kernel/postinst.d/nvidia-com
```

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_614_0.png)

图 15-2 Linux 内核配置窗口，全屏视图

`--append-to-version` 选项允许你指定一个字符串来唯一标识你正在构建的内核。该字符串有助于防止覆盖现有的内核。你可以像下面所示使用该选项指定任何字符串，使用小写字母、数字、`–`（减号）、`+`（加号）和 `.`（点）的字符。你指定的值将放置在内核名称末尾并在此字符串中，以帮助开发者跟踪错误。你可以在此字符串中记录应用于内核的补丁。先前的示例使用了命令替换（第 346 页），将自 UNIX 纪元以秒数放入内核名称中，从而轻松区分多个内核中哪一个是最新的。

## 使用可加载内核模块

可加载内核模块（第 1117 页）（有时也称为模块或可加载模块）是内核的一个对象文件，它在运行时链接到内核。模块可以随时插入内核或从内核中移除（除非模块正在被使用）。

# 加载模块

在用 `module-assistant` 安装模块后，你必须加载它才能让正在运行的内核可以使用。表 15-1 列出了一些可以帮助你处理模块的工具。请参考相应的帮助手册（`man pages`）以获取选项和更多信息。

| 工具/实用程序 | 功能 |
|---|---|
| `depmod` | 处理模块的依赖关系。 |
| `insmod` | 在运行的内核中加载模块。 |
| `lmod` | 列出已加载的模块。 |
| `modinfo` | 列出某个模块的信息。 |
| `modprobe` | 加载、卸载并报告模块。加载模块时，它还会加载依赖项。 |

# 安装内核、模块和关联文件

下一步是将编译好的内核、模块和关联文件拷贝到相应的目录（通常是 `/boot` 和 `/lib/modules` 的子目录）。当你挂载了 `/boot` 分区时，这些文件保留在该分区的根目录下。由于你创建了包，安装这些文件非常简单。以下命令安装新的内核文件：

```
$ cd ..
$ sudo dpkg -i linux-image-2.6.27-rc1_amd64.deb
选择之前未选择的 linux-image-2.6.27-rc1_amd64.deb
(正在读取数据库 ... 正在安装的文件和目录。)
解压 linux-image-2.6.27-rc1_amd64.deb ...
完成。
设置 linux-kernel-2.6.27-rc1_amd64.deb ...
运行 depmod
查找有效的 ramdisk 创建器。
使用 mkinitramfs 构建 ramdisk。
运行 postinst 脚本 update-grub。
```

# grub: Linux 引导程序

```
正在搜索 GRUB 安装目录 ... 找到 /boot/grub
正在搜索默认文件 ... 找到 /boot/grub/default
正在测试现有的 GRUB menu.lst 文件 ... 找到 /boot/grub/menu.lst
正在搜索启动图像 ... 无，跳过
找到内核: /boot/vmlinuz-2.6.27-rc1
找到内核: /boot/vmlinuz-generic
找到内核: /boot/vmlinuz-2.6.5-generic
找到内核: /boot/vmlinuz-memtest86.bin
用新版本替换文件 /boot/grub/menu.lst
更新 /boot/grub/menu.lst ... 完成
检查 /etc/kernel/postinst.d/
run-parts: 执行 /etc/kernel/postinst.d/nvidia-common
```

这种方式安装内核会更新 `menu.lst` 配置文件以包含新内核。`grub` 引导程序见下文。

# 重启

通过选择主菜单：`System-Quit` 然后点击 `Restart` 来重启系统。如果你在控制台操作，按下 `CTRL-ALT-DEL`。你也可以从控制台、字符终端或终端模拟器发出重启命令。

# grub: Linux 引导程序

引导程序是一个非常小的程序，引导过程（第 198 页）在计算机从关闭或重置变为完全功能状态时使用它。引导程序通常位于硬盘的起始扇，称为主引导记录（`MBR`）。

`BIOS`（第 197 页）存储在系统主板的 `EEPROM`（第 117 页）中，当你开启或重置计算机时，它获得了系统的控制权。在测试硬件后，`BIOS` 将控制权交给 `MBR`，然后通常将控制权交给分区引导记录。这种控制权的转移启动了引导程序，它负责找到操作系统内核（保留在 `/boot` 目录中）、将其加载到内存并启动它。`/boot` 目录（可能挂载在单独分区上）是系统启动 Linux 必须的。参考第 427 页的“启动系统”获取有关后续步骤更多信息。

`/boot` 你可以将 `/boot` 目录放置在硬盘开头的一个非常的文件系统上，BIOS 可以访问它。通过这种设置，根（文件系统）可以位于 Linux 可以访问但 BIOS 可能无法访问的任何硬盘上。如果你正在使用 `grub`（下文讨论），将存放 `/boot` 目录的文件系统设置为 `ext2` 文件系统。

`grub` 该名称代表 Grand 统一（统一引导程序）。它是 GNU 项目的产品，`grub` 引导程序符合多引导规范（第 1120 页），允许它直接加载许多自由操作系统，也可以链加载（第 1100 页）专有操作系统。`grub` 引导程序可以识别各种类型的文件系统和

# 第 15 章构建 Linux 内核

`grub` 名称代表 Grand Unified Loader（统一引导程序）。它是 GNU 项目的产品，`grub` 引导程序符合多引导规范（第 1120 页），允许它直接加载许多自由操作系统，也可以链加载（第 1100 页）专有操作系统。`grub` 引导程序可以识别各种类型的文件系统。

`/boot` 目录可以放置在硬盘开头的一个非常小的文件系统上，BIOS 可以访问它。通过这种设置，根文件系统可以位于 Linux 可以访问但 BIOS 可能无法访问的任何硬盘上。如果你正在使用 `grub`（下文讨论），将存放 `/boot` 目录的文件系统设置为 `ext2` 文件系统。

# 50 第 15 章 构建 LINUX 内核

```
$ cat /boot/grub/menu.lst

default 0

timeout 3

#hiddenmenu

color cyan/blue white/blue
```
