

不幸的是，LILO 不适用于 UEFI 系统，因此它在现代系统上的用途有限，并迅速淡出历史舞台。

第一个版本的 GRUB 引导加载程序（现在称为 *GRUB Legacy*）创建于 1999 年，旨在提供一个更健壮、更可配置的引导加载程序来替代 LILO。GRUB 很快成为所有 Linux 发行版的默认引导加载程序，无论它们运行在 BIOS 还是 UEFI 系统上。

*GRUB2* 于 2005 年创建，作为对 GRUB Legacy 系统的全面重写。它支持高级功能，例如加载硬件驱动模块，以及使用逻辑语句根据检测到的系统条件（例如是否连接了外部硬盘）动态更改启动菜单选项。

![](img/c0a399aca0d18f8822d714ad0a173123_204_0.png)

由于 UEFI 可以加载任意大小的引导加载程序，现在可以直接加载 Linux 操作系统内核，而无需特殊的引导加载程序。此功能从 3.3.0 版本开始集成到 Linux 内核中。然而，这种方法并不常见，因为引导加载程序在启动时可以提供更大的灵活性，特别是在处理多个操作系统时。

以下章节将介绍 GRUB Legacy 和 GRUB2 引导加载程序的基本知识，这应该涵盖如今你会遇到的几乎所有 Linux 发行版。

## GRUB Legacy

GRUB Legacy 引导加载程序旨在简化创建启动菜单和向内核传递选项的过程。GRUB Legacy 允许你使用菜单界面和交互式 shell 来选择多个内核和/或操作系统。你配置菜单界面以提供要启动的每个内核或操作系统的选项。交互式 shell 提供了一种在启动时即时定制启动命令的方式。

菜单和交互式 shell 都使用一组控制引导加载程序功能的命令。以下章节将介绍如何配置 GRUB Legacy 引导加载程序、如何安装它，以及如何在启动时与其交互。

## 配置 GRUB Legacy

当你使用 GRUB Legacy 交互式菜单时，需要使用特殊的 GRUB *菜单命令* 告诉它显示哪些选项。

GRUB Legacy 系统在一个名为 *menu.lst* 的标准文本配置文件中存储菜单命令。此文件存储在 `/boot/grub` 文件夹中（虽然这不是强制要求，但一些 Linux 发行版会在硬盘上创建一个单独的 `/boot` 分区）。基于 Red Hat 的 Linux 发行版（如 CentOS 和 Fedora）使用 *grub.conf* 而不是 *menu.lst* 作为配置文件。

GRUB Legacy 配置文件由两部分组成：

- 全局定义
- 操作系统启动定义

全局定义部分定义了控制 GRUB Legacy 启动菜单整体操作的命令。全局定义必须位于配置文件的最前面。你可以进行的全局设置只有少数几个；表 5.1 显示了这些设置。

### 表 5.1 GRUB Legacy 全局命令

| 设置 | 描述 |
| :--- | :--- |
| `color` | 指定在启动菜单中使用的前景和背景颜色 |
| `default` | 定义默认选择的菜单选项 |
| `fallback` | 如果默认菜单选项失败，则使用的次要菜单选择 |
| `hiddenmenu` | 不显示菜单选择选项 |
| `splashimage` | 指向用作启动菜单背景的图片文件 |
| `timeout` | 指定在使用默认选项之前等待菜单选择的时间量 |

对于 GRUB Legacy，要定义命令的值，请将值列为命令行参数：

```
default 0
timeout 10
color white/blue yellow/blue
```

`color` 命令定义菜单的颜色方案。第一对定义正常菜单项的前/后景颜色对，而第二对定义选中菜单项的前/后景颜色对。

在全局定义之后，你放置系统中已安装的各个操作系统的定义。每个操作系统应有其自己的定义部分。有许多启动定义设置可用于自定义引导加载程序如何找到操作系统内核文件。幸运的是，定义操作系统只需要少数几个命令。需要记住的命令如下：

- `title`—每个启动定义部分的第一行；这是显示在启动菜单中的内容。
- `root`—定义 GRUB `/boot` 文件夹所在系统上的磁盘和分区。
- `kernel`—定义要加载的存储在 `/boot` 文件夹中的内核映像文件。
- `initrd`—定义初始 RAM 磁盘文件，其中包含内核与系统硬件交互所需的驱动程序。
- `rootnoverify`—定义非 Linux 启动分区，例如 Windows。

`root` 命令定义包含 GRUB Legacy `/boot` 文件夹的硬盘和分区。不幸的是，GRUB Legacy 引用这些值的方式有些独特：

        `(hd`, `partition)`

同样不幸的是，GRUB Legacy 引用硬盘的方式与 Linux 不同；它使用编号系统来引用磁盘和分区，从 0 而不是 1 开始。例如，要引用系统上第一个硬盘的第一个分区，你应使用 `(hd0,0)`。要引用第一个硬盘的第二个分区，你应使用 `(hd0,1)`。`initrd` 命令是 GRUB Legacy 中的另一个重要功能。它有助于解决使用专用硬件或文件系统作为根驱动器时出现的问题。`initrd` 命令定义一个由内核在启动时挂载为 RAM 磁盘的文件，也称为 `initrd`。然后内核可以从 `initrd` RAM 磁盘加载模块，从而允许其访问未编译进内核本身的硬件或文件系统。位于 `/boot` 目录中的 `initrd` RAM 磁盘文件被称为 `initrd.img-kversion`，其中 `kversion` 是内核版本号。

![](img/c0a399aca0d18f8822d714ad0a173123_206_0.png)

如果你安装在系统上的新硬件需要在启动时可见，你需要修改 `initrd` 文件。你可以使用基于 Red Hat 的系统中的 `mkinitrd` 命令创建包含新硬件模块的新 `initrd` RAM 磁盘映像。对于基于 Debian 的系统，该文件被称为 `initramfs`，并使用 `mkinitramfs` 命令创建。或者，你可以使用 `dracut` 实用程序，它从框架创建 `initramfs` 映像并从已安装的模块复制文件。

清单 5.2 显示了一个示例 GRUB 配置文件，定义了用于启动的 Windows 和 Linux 分区。

### **清单 5.2**
GRUB Legacy 配置文件示例

```
default 0
timeout 10
color white/blue yellow/blue

title Ubuntu Linux
root (hd1,0)
kernel (hd1,0)/boot/vmlinuz
initrd /boot/initrd

title Windows
rootnoverify (hd0,0)
```

此示例显示了两个启动选项——一个用于 Ubuntu Linux 系统，一个用于 Windows 系统。Ubuntu 系统安装在第二个硬盘的第一个分区上，而 Windows 系统安装在第一个硬盘的第一个分区上。Linux 启动选择指定要加载的内核文件以及要加载到内存中的 initrd 映像文件。

![](img/c0a399aca0d18f8822d714ad0a173123_207_0.png)

你可能注意到，在清单 5.2 示例中内核文件名被称为 vmlinuz。不，那不是笔误——文件名末尾的 z 表示内核文件使用 bzimage 压缩方法进行压缩，这是大多数 Linux 发行版中非常常见的方法。对于未压缩的内核文件，内核映像文件通常被称为 vmlinux。

## 安装 GRUB Legacy

构建 GRUB Legacy 配置文件后，必须在 MBR 中安装 GRUB Legacy 程序。执行此操作的命令是 grub-install。

grub-install 命令使用单个参数——要安装 GRUB 的分区。你可以使用 Linux 或 GRUB Legacy 格式指定分区。例如，要使用 Linux 格式，你应使用

```
# grub-install /dev/sda
```

在第一个硬盘的 MBR 上安装 GRUB。要使用 GRUB Legacy 格式，你必须用引号括起硬盘格式：

```
# grub-install '(hd0)'
```

如果你使用链式加载方法，并希望将 GRUB Legacy 的副本安装到分区的引导扇区而不是硬盘的 MBR，你同样必须指定分区，再次使用 Linux 或 GRUB 格式：

```
# grub-install /dev/sda1
# grub-install 'hd(0,0)'
```

在对配置文件进行更改后，你不需要在 MBR 中重新安装 GRUB Legacy。GRUB Legacy 每次运行时都会读取配置文件。

## 与 GRUB Legacy 交互

当你启动使用 GRUB Legacy 引导加载程序的系统时，你将看到一个显示你在配置文件中定义的启动选项的菜单。如果等待超时过期，默认启动选项将被处理。或者，你可以使用箭头键选择其中一个启动选项，然后按 Enter 键进行选择。

