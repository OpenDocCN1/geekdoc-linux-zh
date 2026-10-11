
How Linux Works (Early Access) © 2021 by Brian Ward

这两种都是更好的，因为它们不依赖于特定的设备映射。
`ro` 参数指示内核在启动用户空间时以只读模式挂载根文件系统。这是正常的；只读模式确保 `fsck` 在尝试执行任何操作之前安全地检查根文件系统。检查之后，引导过程将以读写模式重新挂载文件系统。
当遇到它不理解的参数时，Linux 会保存该参数。内核稍后会在执行用户空间时将参数传递给 `init`。例如，如果你在参数中添加 `-s`，内核会将 `-s` 传递给 `init` 程序以指示以单用户模式启动。
如果你对启动参数感兴趣，`bootparam(7)` 手页提供了概述。如果你在寻找非常具体的参数，可以查看 Linux 内核带的参考文件 `kernel-params.txt`。
在涵盖这些基础知识后，你可以随心跳到第 6 章学习用户空间启动、初始内存磁盘以及内核作为第一个进程运行的 `init` 程序。本章剩余部分介绍了内核如何加载到内存并启动，包括它是如何获取参数的。

## 5.4 引导程序

在启动过程开始、内核和 `init` 启动之前，引导程序启动内核。引导程序的工作听起来很简单：它从磁盘的某处加载内核到内存并带参数启动内核。然而，这项工作比看起来要复杂。要理解为什么，请考虑引导程序必须回答的问题：

- 内核在哪里？
- 应该传递哪些内核参数？

通常，有一种模式是内核添加新功能（特别是存储技术方面），随后引导程序添加这些特征的版本以补偿。在 PC 上，引导程序使用传统的输入输出系统（BIOS）或较新的可扩展固件接口（UEFI）来访问磁盘。

How Linux Works (Early Access) © 2021 by Brian Ward

Linux 引导程序的核心功能包括执行以下操作：

- 选择多个内核。
- 在不同的内核参数集之间切换。
- 允许用户手动覆盖和编辑内核镜像名称和参数（例如进入单用户模式）。
- 提供引导其他操作系统的支持。

《Linux 工作原理》（早期访问版）© 2021 Brian Ward

## 5.4.2 启动加载程序概述

以下是你可能会遇到的主要启动加载程序：

- `GRUB`: Linux 系统上几乎通用的标准，分为 BIOS/MBR 和 UEFI 版本。
- `LILO`: 最早的 Linux 启动加载程序之一。`ELILO` 是其 UEFI 版本。
- `SYSLINUX`: 可以配置为从许多不同的文件系统运行。
- `LOADLIN`: 从 MS-DOS 启动内核。
- `systemd-boot`: 一个简单的 UEFI 启动管理器。
- `coreboot`（以前称为 LinuxBIOS）PC BIOS 的高性能替代品，可以包含内核。
- `Linux Kernel EFIUB`: 一种内核插件，用于直接从 EFI/UEFI 系统分区 (`ESP`) 加载内核。
- `efilinux`: 一个 UEFI 启动加载程序，旨在作为其他 UEFI 加载程序的模型和参考。

本书几乎完全涉及 `GRUB`。其他启动加载程序的原理是：它们比 `GRUB` 更简单、速度更快，或者提供了某些其他特殊功能。

通过进入可以输入内核名称和参数的启动提示符，你可以学习很多关于启动加载程序的知识。要做到这一点，你需要知道如何获取提示符或菜单。遗憾的是，这有时很难确定，因为 Linux 发行版高度自定义了启动加载程序的行为和外观。通常无法通过观察启动过程来判断该发行版使用的是哪种启动加载程序。

后续章节将告诉你如何进入启动提示符以输入内核名称和参数。一旦你熟悉了这些，你将看到如何配置和安装启动加载程序。

## 5.5 GRUB 介绍

`GRUB` 代表 Grand Boot Loader。我们将涵盖 `GRUB 2`，但还有一个名为 `GRUB Legacy` 的旧版本，已不再活跃使用。

`GRUB` 最重要的功能之一是文件系统导航，它允许轻松选择内核镜像和配置。观察其运行并泛学习 `GRUB` 的最佳方法之一是查看它的菜单。该界面易于导航，但你可能从未见过它。

要访问 `GRUB` 菜单，在 BIOS 启动界面首次出现时按住 `SHIFT`，如果你的系统是 UEFI，则按 `ESC`。否则，启动加载程序可能在加载内核之前不会暂停。

图 5-1 显示了 `GRUB` 菜单。

GNU GRUB version 2.02

![](img/048936caacb6c295aeb3ea5e3cfa45b9_148_0.png)

使用 `I` 和 `l` 键选择高亮的项目。
按回车启动选定的操作系统，按 `'e'` 在启动前编辑命令，或按 `'c'` 进入命令行。

图 5-1：`GRUB` 菜单

尝试以下操作来探索启动加载程序：

1. 重启或开启你的 Linux 系统。
2. 在 BIOS 自检期间按住 `SHIFT` 键或在固件启动屏处按 `ESC` 获取 `GRUB` 菜单。（这些屏幕有时是可见的，所以你必须猜测何时按键。）
3. 按 `e` 查看默认启动选项的启动加载程序配置命令。你应该能看到类似图 5-2 的内容（你可能需要向下滚动查看所有细节）

GNU GRUB version 2.02

```
setparams ubuntu

recordfail

load_video

gfxmode linux_gfx_mode

insmod gzio

if [ grub_platform = "xen" ]; then insmod zoiio; insmod is: \
insmod part_msdos

insmod ext2

search --no-floppy --fs-uuid --set-root 8b92610e-1db7-4b43-ac2f-3ee24b39de0

linux
/boot/vmlinuz-4.15.0-45-generic UUID=8b92610e-1db7-4b43-ac2f quiet splash vt_handoff

initrd /boot/initrd.img-4.15.0-45-generic
```

支持类似 Emacs 的最小编辑。`Tab` 允许补全。按 `Ctrl-x` 或 `F10` 启动，按 `Ctrl-c` 或 `F2` 进入命令行，或按 `ESC` 弃编辑并返回 `GRUB` 菜单。

图 5-2：`GRUB` 配置编辑器

此屏幕告诉我们，对于此配置，根目录通过 `UUID` 设置，内核镜像为 `/boot/vmlinux-4.15.0-45-generic`，内核参数包括 `ro`、`quiet` 和 `splash`。内存文件系统为 `/boot/initrd.img-4.15.0-45-generic`。但如果你以前见过这种配置，可能会觉得很困惑。为什么对根目录有多次引用，而且它们还不同？为什么这里有 `insmod`？如果你以前见过这个，可能会记得它是一个通常由 `udev` 运行的内核功能。

这种惊讶是有理由的，因为 `GRUB` 并不使用 Linux 内核（注：此处原文应为 *in memory*，它的任务是启动内核）。

[注：OCR 源文件中的剩余文本包含大量的重复痕迹和 OCR 错误，已根据上述提供的上下文进行了清理以保持可读性。]

# Linux 工作原理（早期访问版） © 2021 Brian Ward

由于输入实际的根分区极不方便，你可以替换 `$root` 变量来节省自己的时间：

```
grub$ ls ($root)/
```

输出是该分区文件系统中文件和目录名的简短列表，例如 `/etc/`、`bin/` 和 `dev/`。这是 `GRUB` 命令的一个完全不同的功能。之前，你列出的是设备、分区表，可能还有一些文件系统头信息。现在，你实际上是在查看文件系统的内容。

你可以以类似的方式深入查看分区上的文件和目录。例如，要检查 `/boot` 目录，可以从以下命令开始：

```
grub$ ls ($root)/
```

> 使用向上和向下方向键翻阅 `GRUB` 命令历史，使用左和右箭头编辑当前命令行。标准的 `readline` 快捷键（`CTRL-N`、`CTRL-P` 等）同样有效。

你还可以使用 `set` 命令查看所有当前的 `GRUB` 变量：

```
grub> set
=?ncolor_highlight=black/white

color_normal=white/black

--snip-

prefix=(hd0,msdos1)/boot/grub

root=hd0,msdos1
```
