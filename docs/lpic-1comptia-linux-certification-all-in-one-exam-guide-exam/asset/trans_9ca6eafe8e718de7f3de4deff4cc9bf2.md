
## 配置 GRUB

GRUB。真是一个给引导加载器起的怪名字！GRUB 这个缩写听起来可不太吸引人，是吧？然而，作为引导加载器，GRUB 非常出色。GRUB 的全称是 Grand Unified Bootloader（通用大统一引导加载器）。与 LILO 类似，GRUB 是一种可用于启动系统硬盘上 Linux 内核（或者实际上任何其他操作系统内核）的引导加载器。

LILO 引导加载器曾非常流行，并被广泛使用了好几年。然而，在过去几年里，大多数发行版和许多 Linux 系统管理员一直在稳步地从 LILO 转向 GRUB。因此，你需要对 GRUB 的工作原理及其配置方法有扎实的理解。

在本章的这一部分中，我们将讨论以下 GRUB 主题：

- GRUB 的工作原理
- 安装 GRUB
- 配置 GRUB

让我们首先来讨论一下 GRUB 是如何工作的。

## GRUB 的工作原理

还记得我们之前说过 LILO 可以安装在启动硬盘的主引导记录（MBR）或引导分区中吗？GRUB 有点不同。GRUB 引导加载器被分为几个独立的块，称为阶段（stages）。包括以下几个部分：

- **阶段 1**：GRUB 的这个阶段通常存储在 MBR 中。它唯一真正的作用是指向阶段 1.5 或阶段 2 的位置。
- **阶段 1.5**：GRUB 的这个阶段位于硬盘的前 30KB 内，紧接在 MBR 之后，但在第一个分区之前。阶段 1.5 包含加载阶段 2 所需的任何驱动程序。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_235_0.png)

> **提示** 阶段 1 可以跳过阶段 1.5 并直接加载阶段 2，但通常配置为先加载阶段 1.5。

- **阶段 2**：GRUB 的这个阶段存储在一个磁盘分区中。当被阶段 1 或阶段 1.5 加载时，阶段 2 会在屏幕上显示一个图形菜单，允许用户选择应该加载的内核镜像。与 LILO 一样，你可以为 GRUB 配置默认镜像和超时值。如果用户未在超时期间内选择选项，系统将自动启动默认内核镜像。图 6-7 展示了一个典型的 GRUB 菜单。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_235_1.png)

> **注意** 与 LILO 类似，GRUB 也允许将阶段 1 安装在引导分区中。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_236_0.png)

图 6-7 GRUB 引导菜单

有了这个概述，让我们来谈谈如何安装 GRUB。

### 安装 GRUB

我对 GRUB 非常喜欢的一点是，当你进行小配置更改时，你不需要重新安装引导加载器。在安装之后，你可以修改你的配置文件，并且由于阶段 2 直接从磁盘上的配置文件读取，这些更改将在 GRUB 下次加载时生效。

为了初始安装 GRUB，你首先需要验证 grub 软件包是否已安装在系统上。在基于 rpm 的发行版上，可以在 shell 提示符下输入 `rpm -q grub` 来执行此操作，如下所示：

```bash
fs2:~ # rpm -q grub
grub-0.97-171.1.x86_64
fs2:~ #
```

此输出告诉我们 GRUB 软件包已安装。如果你没有看到该命令的任何输出，就知道 GRUB 尚未安装，必须在继续之前进行安装。

要安装 GRUB 引导加载器本身，请在 shell 提示符下输入 `grub-install _device_`。_device_ 选项是你要安装阶段 1 的 MBR 的设备名称。例如，如果你想将 GRUB 阶段 1 安装在系统第一个硬盘的 MBR 中，你会输入 `grub-install /dev/sda`，如下例所示：

```bash
fs2:~ # grub-install /dev/sda
Installation finished. No error reported.
This is the contents of the device map /boot/grub/device.map.
Check if this is correct or not. If any of the lines is incorrect, fix it and re-run the script 'grub-install'.

(fd0)    /dev/fd0
(hd0)    /dev/sda
fs2:~ #
```

安装好 GRUB 后，你准备好配置它了。让我们接下来讨论如何进行配置。

## 配置 GRUB

要配置 GRUB，你需要编辑一个基于文本的配置文件，其方式与我们之前讨论的 LILO 引导管理器非常相似。然而，对于 GRUB，你需要编辑的文件名称可能因发行版而异。表 6-2 列出了按发行版划分的常见实现方式。

一些发行版（如 Fedora）将 /boot/grub/menu.lst 符号链接到 /boot/grub/grub.conf 文件，因此无论编辑哪个文件，你都在正确的位置进行更改。Fedora 还将 /etc/grub.conf 文件符号链接到 /boot/grub/grub.conf，因此你也可以将文件加载到编辑器中以更改你的 GRUB 配置。找出应该使用哪个文件来配置 GRUB 的最简单方法只是切换到 /boot/grub 目录并寻找 grub.conf 或 menu.lst 文件，如下所示：

```bash
fs2: # ls /boot/grub/ -l
total 216
-rw------- 1 root root   30 Jan 19 10:37 device.map
-rw-r--r-- 1 root root   29 Jan 19 10:24 device.map.old
-rw-r--r-- 1 root root  8608 Jul  5  2010 e2fs_stage1_5
-rwxr-xr-x 1 root root  7872 Jul  5  2010 fat_stage1_5
-rwxr-xr-x 1 root root  7136 Jul  5  2010 ffs_stage1_5
-rwxr-xr-x 1 root root  7136 Jul  5  2010 iso9660_stage1_5
-rwxr-xr-x 1 root root  8576 Jul  5  2010 jfs_stage1_5
-rw------- 1 root root  1088 Jan 19 10:37 menu.lst
-rw-r--r-- 1 root root   983 Jan 19 10:24 menu.lst.old
-rwxr-xr-x 1 root root  7236 Jul  5  2010 minix_stage1_5
-rwxr-xr-x 1 root root  9632 Jul  5  2010 reiserfs_stage1_5
-rwxr-xr-x 1 root root   512 Jul  5  2010 stage1
-rw-r--r-- 1 root root 10226 Feb 11 12:18 stage2
-rwxr-xr-x 1 root root  7456 Jul  5  2010 ufs2_stage1_5
-rwxr-xr-x 1 root root  6680 Jul  5  2010 vfatfs_stage1_5
-rwxr-xr-x 1 root root  9280 Jul  5  2010 xfs_stage1_5
fs2: #
```

无论你的 GRUB 配置文件使用哪个文件，它都会使用标准的结构。请记住，你的 LILO 配置文件使用了一个全局部分，然后是一个或多个特定镜像的部分。GRUB 配置文件以非常相似的方式工作。GRUB 配置文件的第一部分包含应用于所有菜单项的全局选项。然后它有一个或多个 title 部分，用于启动特定的操作系统。这里展示了一个典型的 GRUB 配置文件：

| 表 6-2：GRUB 配置文件 | |
| :-- | :-- |
| **GRUB 配置文件** | **发行版** |
| /boot/grub/grub.conf | Fedora |
| /boot/grub/menu.lst | SUSE Linux, Debian |

```bash
fs2:~ # cat /boot/grub/menu.lst
# Modified by YaST2. Last modification on Wed Jan 19 10:37:45 MST 2011
# THIS FILE WILL BE PARTIALLY OVERWRITTEN by perl-Bootloader
# Configure custom boot parameters for updated kernels in /etc/sysconfig/
bootloader

default 0
timeout 8
#YaST - generic_mbr
gfxmenu (hd0,1)/Boot/message
##YaST - activate

###Don't change this comment - YaST2 identifier: Original name: linux##
title Desktop -- openSUSE 11.3 - 2.6.34-12
root (hd0,1)
kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 resume=/dev/sda5
splash=silent quiet showspec vga=0x317
initrd /boot/initrd-2.6.34-12-desktop

###Don't change this comment - YaST2 identifier: Original name: failsafe##
title Failsafe -- openSUSE 11.3 - 2.6.34-12
root (hd0,1)
kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 showopts apm=off
nomodeset edd=off powersaved=off nohpet=off highres=off processor.max_cstate=1
initrd /boot/initrd-2.6.34-12-desktop

###Don't change this comment - YaST2 identifier: Original name: floppy##
title Floppy
rootnoverify (fd0)
chainloader +1
fs2:~ #
```

在我们探索这个示例 GRUB 配置文件中的条目之前，我们需要回顾一下 GRUB 的术语。首先，GRUB 引用系统中磁盘和分区的方式可能令人不熟悉。在处理 LILO 时，我们使用 /dev 中的设备文件来引用设备和分区，例如 /dev/sda1。GRUB 以不同的方式引用这些设备。GRUB 不使用 /dev 条目，而是使用以下语法：

```
(hd#ive_number,partition_number)
```

例如，第一个硬盘上的第一个分区（/dev/sda1）被 GRUB 称为 hd0,0。无论第一个磁盘是 IDE、SATA 还是 SCSI 驱动器——GRUB 都将其称为 hd0。

另一件可能会让你困惑的事情是，GRUB 创建了自己的“根”，称为 GRUB 根。这并不一定是挂载在 / 处的根文件系统。相反，它是 /boot 目录所在的分区（阶段 2 安装的位置）。这里令人困惑的部分是：如果你最初分区硬盘时没有为 /boot 创建独立的分区，那么 GRUB 将使用完整路径来引用 GRUB 根，通常是 /boot/grub。另一方面，如果你为 /boot 创建了独立的分区（这是一个很好的做法），那么这个分区就变成了 GRUB 根。GRUB 在引用 GRUB 根中的文件时不包含 /boot 路径。这会让你抓狂，直到你习惯它为止。在继续之前，你需要理解这两个事实；否则，GRUB 配置文件中的许多条目将毫无意义。
