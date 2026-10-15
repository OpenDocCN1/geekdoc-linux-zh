
有用的选项 `-m` 允许你在创建文件时设置权限模式，而不是之后单独使用 `chmod` 命令。

你可以从 `devices.txt` 中获取 NAME、TYPE、MAJOR 和 MINOR 的值，该文件甚至包含一组实验性数字，如果你愿意尝试的话。

## 相关的 Fedora 和 Linux 命令

**管理 Linux 文件系统和分区**

你在 Fedora 中管理文件系统时使用这些命令：

- `df`—显示可用磁盘空间
- `du`—显示磁盘使用情况
- `dump`—ext2 文件系统备份实用程序
- `dumpe2fs`—显示关于 ext2 文件系统的信息
- `e2fsadm`—管理 LVM/ext2 文件系统
- `e2image`—创建 ext2 文件系统数据的映像文件
- `fdisk`—标准的 Linux 分区表编辑器
- `fsck`—检查或修复文件系统
- `lsraid`—显示关于 Linux RAID 设备的信息
- `mformat`—格式化 DOS 软盘；Mtools 工具套件的一部分
- `mkfs`—创建各种文件系统，并作为执行实际工作的程序封装器
- `mkisofs`—创建 iso9660 格式的 CD-ROM 文件系统
- `mkreiserfs`—创建 Linux reiserfs 文件系统
- `mkswap`—准备 Linux 交换设备
- `mount`—挂载支持的文件系统
- `parted`—GNU 分区编辑器和调整大小实用程序
- `reiserfsck`—检查 Linux reiserfs 文件系统
- `resize_reiserfs`—调整 Linux reiserfs 文件系统的大小
- `smbmount`—挂载 smbfs 文件系统
- `stat`—显示文件或文件系统状态
- `swapon`—显示交换使用量或开始使用系统交换设备
- `swapoff`—关闭交换使用
- `sync`—刷新文件系统缓冲区
- `tune2fs`—更改 ext2 文件系统的文件系统参数
- `umount`—卸载文件系统
- `usermount`—Fedora Core 图形化文件系统挂载和格式化工具

## 参考资料

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/FileSystems-HOWTO.html—在文件系统 HOWTO 中，你将找到有关原生 Linux 文件系统的广泛信息，以及更多奇异的文件系统。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Partition.html—Linux 分区 HOWTO 包含了关于分区及其要求的详细信息的很大篇幅。

http://battleh.sapienri-sat.org/projects/FAQs/ext3-faq.html—Linux ext3 FAQ 是一个非官方的常见问题解答，其中包含一些有用的信息，特别是关于将 ext3 分区转换回 ext2 的信息。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion.html—你在 ext2/3 分区上删除了一个文件？Linux Ext2fs 未删除（Undeletion）迷你 HOWTO 在那里帮助你。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion-Dir-Struct.html—你在 ext2/3 分区上删除了一个目录？阅读 Ext2fs 目录结构未删除（Undeletion）HOWTO，看看如何抢救你的数据。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Loopback-Root-FS.html—以下是其概念：我们不仅可以使用传统文件系统，还可以使用位于另一个文件系统中的一个大文件内的文件系统。回环根文件系统 HOWTO 检查了这是如何实现的。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Loopback-Encrypted-File-System-HOWTO.html—你可以使用回环设备来挂载加密文件系统，例如 /home，出于安全原因。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/LVM-HOWTO.html—抛弃那些将物理磁盘与有限大小文件系统结合的概念；逻辑卷管理器（LVM）HOWTO 解释了如何克服这种限制性思维。

http://linux.org/mt/article/lvm—关于逻辑卷管理器的良好概述和讨论。

http://www.coda.cs.cmu.edu/—Coda 网络文件系统的主页。

http://www.intermezzo.org/—InterMezzo 网络文件系统的网页。

http://www.math.ualberta.ca/imaging/sfs/—通过 SSH 隧道的安全 NFS（Secure NFS via an SSH Tunnel）是一个非常有创意的尝试，旨在解决 NFS 在公共网络上安全缺陷。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/UMSDOS-HOWTO.html—如果你对使用 umsdos 文件系统感兴趣，UMSDOS HOWTO 为你提供充足的信息。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/NFS-Root.html—NFS-Root 迷你 HOWTO。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/NFS-Root-Client-mini-HOWTO.html—详细解释如何设置和使用 NFS 来导出根文件系统。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Multi-Disk-HOWTO.html—多磁盘系统调整 HOWTO 包含有关驱动器和控制器硬件的解释，以及关于文件系统的讨论，这些都有用。它提供了一个关于优化多磁盘配置的有趣章节。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Software-RAID-HOWTO.html—软件 RAID HOWTO 是软件 RAID 的一次卓越的壮举。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Tips-HOWTO.html—Linux 技巧 HOWTO 提供了一些有用的技巧，使其值得花时间阅读，因为它处理了一些文件系统问题，例如“有足够多的空闲空间吗？”和“我如何在文件系统之间移动目录？”

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Large-Disk-HOWTO.html—仍然不确定驱动器几何形状、LILO 和 GRUB 的限制以及那些非常大的磁盘？大型磁盘 HOWTO 对此有有用的细节。它还告诉你如何处理使用 OnTrack 和 FZ_Drive 等磁盘管理器的磁盘。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/BootPrompt-HOWTO.html—BootPrompt HOWTO 告知你可以传递给内核以处理故障硬件、配置非 PNP 设备等启动参数。对于本章，第 7 节“硬盘”最有用的。

http://www.namesys.com/—关于 reiserfs 改进和 Reiser4 发布的详细信息（参见 http://www.namesys.com/v4/v4.html）。

http://www.linux-usb.org/USB-guide/s48.html—面向大容量存储和其他 USB 设备的 USB 指南。如果你有一个 USB 设备，并需要知道是否支持以及如何访问它，请在此查看。（提示：USB 存储设备模拟为 SCSI 设备。）

## 第 39 章

# 内核与模块管理

## 本章内容

- Linux 内核
- 管理模块
- 何时重新编译
- 内核版本
- 获取内核源代码
- 修补内核
- 编译内核
- 出错时该怎么办
- 参考资料

内核是一种复杂的软件，负责管理操作系统中发生的过程及过程间的交互。作为用户，你很少（甚至从未）直接与其交互。相反，你操作的是内核所管理的应用程序。

Linux 内核就是 Linux。它是全球众多人员经过多年协作（有时甚至是争执不休）工作的成果。虽然只有一个通用的内核源代码树，但每个主要的 Linux 发行版都会对其版本进行微小的调整和修补，以添加功能、提升性能或提供选项。每个 Linux 发行版（包括 Fedora）都附带自己的预编译内核以及内核源代码，这赋予了对 Linux 操作系统的绝对控制权。在本章中，我们将考察内核，学习它为我们和操作系统做了什么。

在本章中，你还将学习如何获取内核源代码，以及何时以及如何修补内核。本章将引导你进行专家级的内核架构之旅，并教授内核配置的基本步骤、如何构建和安装模块，以及如何在 Fedora 中编译驱动程序。本章还教你与 GRUB（Fedora 的默认引导加载程序）协作的重要方面。最后，本章的故障排除信息将帮助你了解当 Linux 内核安装或编译过程出现问题时该怎么办。虽然这些问题可能看起来令人沮丧，但本章为你提供了许多内核问题的简单修复方法。

大多数用户会发现预编译的 Fedora 内核满足他们的需求。在某些时候，你可能需要重新编译内核以支持特定的硬件部件或为操作系统添加新功能。如果你听说过关于重新编译 Linux 内核困难重重的恐怖故事，你可以放心：本章提供了你需要的所有信息，帮助你理解何时需要重新编译以及如何无痛苦地完成这一过程。

### Linux 内核

Linux 内核是操作系统的管理部分，许多人称之为“Linux”。虽然许多人将整个发行版视为 Linux，但唯一可以正确被称为 Linux 的地方是内核。Fedora 与许多 Linux 发行版一样，包含一个内核，该内核打包了附加软件，这些软件与内核交互，使用户能够以有意义的方式与系统交互。

系统实用程序和用户程序使计算机成为对用户有价值的工具。

> **第一个 LINUX 内核**
>
> 1991 年，Linus Torvalds 发布了 Linux 内核的 .99 版本，这是他为了满足对一台用于 Intel 80386 个人计算机的强大、类 UNIX 操作系统的渴望而产生的结果。Linus 编写了创建如今所称的 Linux 内核所必需的初始代码，并将其与 Richard Stallman 的 GNU 工具结合。确实，由于许多 Linux 基础系统工具来自 GNU 项目，许多人将该操作系统称为 GNU/Linux。自那以来，Linux 受益于数千名贡献者为其项目付出才华和时间。Linus 仍然维护内核，决定哪些内容会作为官方版本进入内核，这些版本被许多人称为 vanilla 或 Linus Linux 内核。

### Linux 源代码树

Linux 内核的源代码存储在一组称为内核源代码树的目录中。内核源代码树的结构很重要，因为编译（构建）内核的过程是自动化的：它由 `make` 应用程序解释的脚本控制。这些被称为 `Makefiles` 的脚本，期望在特定位置找到内核代码的各个部分，否则它们将无法正常工作。稍后在本章中，你将学习如何使用 `make` 来编译内核。

对于系统运行或完成电子邮件、网页浏览或文字处理等典型任务来说，并没有必要在你的系统上安装 Linux 内核源代码。然而，如果你想要编译一个新的内核，那么必须安装内核源代码。在下一节中，我们将展示如何安装内核源文件以及如何设置所需的特殊符号链接。该链接是 `/usr/src/kernels-<你的内核版本>`，我们将使用它来指代内核源代码树的目录，以便我们检查内核源代码树的内容。

`/usr/src/kernels/<你的内核版本>` 目录中包含 `.config` 和 `Makefile` 文件等其他文件。`.config` 文件是你 Linux 内核的编译配置。默认情况下没有 `.config` 文件；你必须从 `/configs` 子目录中选择一个。在那里你会发现 Fedora 提供的每种内核口味的配置文件；只需将适合你系统的那份复制到默认目录并命名为 `.config` 即可。

我们已经讨论过 `/configs` 子目录的内容，所以让我们来看看 `/usr/src/kernels/<你的内核版本>` 下找到的其他目录。对我们最有用的是 `Documentation` 目录。在其中及其子目录中，你会发现几乎涵盖内核每个部分的几乎所有文档。`00_INDEX` 文件（每个 Documentation 子目录也包含一个 `00_INDEX` 文件）包含主目录中文件的列表以及关于它们的简要说明。许多文件仅面向内核程序员和应用程序编写者，但有些文件对于尝试了解内核和设备驱动问题的高级或中级 Linux 用户是有用的。

一些更有趣且有用的文档包括

- `devices.txt`——列出了所有在 `/dev` 目录中表示的可能的 Linux 设备，给出了主要和次要编号以及简短描述。如果你曾遇到过提到 char_major-xxx 的错误消息，这个文件就是保存该列表的地方。设备在第 38 章“文件系统管理”中提到。
- `ide.txt`——如果你的系统使用 IDE 硬盘，这个文件讨论了内核如何与之交互，并列出了可用于解决 IDE 相关硬件问题的各种内核命令，手动设置数据传输模式，以及手动管理你的 IDE 设备。大部分管理是自动的，但如果你想了解内核如何与 IDE 设备交互，这个文件会解释它。
- `instd.t`——第 38 章还讨论了初始 RAM 磁盘。这个文件提供了关于初始 RAM 磁盘的更深入知识，详细说明了用于创建和挂载它们的回环文件系统，并解释了内核如何与它们交互。
- `kernel_parameters.txt`——这个文件列出了大多数你可以在启动时传递以配置内核或硬件设置的参数。但乍一看它似乎不太有用，因为它只是一个列表。然而，知道存在某个参数并且可能与你要寻找的内容相关，可以帮助你追踪更多信息，因为你现在有了可以输入到如 http://www.google.com/linux 等互联网搜索引擎中的术语。
- `sysrq.txt`——如果你曾想知道键盘上的那个 SysRq 键是做什么用的，这个文件有答案。简而言之，它是硬编码在内核中的一个按键组合，可以帮助你从系统锁死中恢复。出于安全原因，Fedora 默认禁用此功能。你可以通过输入命令 `# echo '1' > /proc/sys/kernel/sysrq` 重新启用它，通过回显值 0 而不是 1 来禁用它。

在 `Documentation` 中的其他目录中，你会找到类似的文本文件，处理 CD-ROM 驱动程序的`内核模块`、文件系统驱动程序、游戏端子和摇杆驱动程序、视频驱动程序（不是显卡驱动程序——那些属于 X11R6，不属于`内核模块`）

内核、网络驱动程序以及 Linux 操作系统中发现的所有其他驱动和系统。同样，这些文档通常是写给程序员看的，但它们也能为中级和高级 Linux 用户提供的有用信息。

名为 `scripts` 的目录包含了许多 `make` 所使用的脚本。它确实不包含任何对非程序员或内核开发人员（也称为`内核黑客`）感兴趣的内容。

内核构建完成后，所有编译后的文件将位于 `arch` 目录及其子目录中。虽然你可以手动将它们移动到最终位置，但我们将在本章后面向你展示 `make` 脚本如何为你完成这项工作。在 Linux 的早期，这种编译后的文件重新定位都是手工完成的；你应该感谢 `make`。

> **注意**
>
> `make` 实用程序是一个非常复杂的程序。有关 `Makefile` 结构的完整文档，以及它可以接受的参数，可以在 http://www.gnu.org/software/make/manual/make.html 上找到。

其余目录包含内核和内核驱动的源代码。当你安装内核源代码时，这些文件会自动放在那里。当你打补丁（patch）内核源代码时，这些文件会自动被修改。当你编译内核时，这些文件会被自动访问。虽然你不需要接触源代码文件，但它们可能很有用。内核源文件只不过是具有特殊格式的文本文档，这意味着我们可以查看并阅读*程序员的*注释。有时，程序员会编写应用程序，但不能或通常不会编写文档。他放在源代码中的注释往往是该代码仅存的文档。

小型测试程序甚至隐藏在某些代码的注释中，以及一些指向其他信息的注释和引用。由于源代码是用一种几乎像英语一样容易阅读的语言编写的，非程序员可能会想了解应用程序或驱动实际在做什么（参见第 33 章，“Fedora 的 C/C++ 编程工具”）。这些信息对于中级到高级 Linux 用户遇到内核和驱动相关问题时可能有用。

> **注意**
>
> 硬件的交互和控制由内核中称为*设备驱动程序*的一小部分来处理。驱动程序告诉计算机如何响应用户提示来与调制解调器、SCSI 卡、键盘、鼠标等交互。如果没有设备驱动程序，内核不知道如何与相关设备交互。

## 内核类型

在 Linux 的早期，内核是包含针对处理器、主板和其他硬件的所有指令的单一代码块。如果你更改了硬件，你需要重新编译内核代码以包含你需要的部分并丢弃你不需要的部分。包含多余的、不需要的代码会带来代价，因为内核变得更大并占用更多内存。在只有 4MB–8MB 内存的旧系统上，浪费宝贵的内存用于不必要的代码是不可接受的。内核编译在早期 Linux 用户试图从其计算机中榨取最大性能时，有点像是玄学。这些作为单一代码块编译的内核被称为*单片式内核*。

随着内核代码变大以及可以添加到计算机中的设备数量增加，重新编译的要求变得繁重。开发了一种新的内核构建方法，以使编译任务更容易。内核源代码中组成设备驱动程序代码的部分可以选择性地编译为模块，这些模块可以根据需要加载和卸载到内核中。这被称为构建内核的*模块化*方法。现在，所有内核代码可以一次性编译——其中大部分代码被编译成这些模块。只有所需的模块会被加载；内核可以保持较小，添加硬件也变得更加简单。

典型的 Fedora 内核有一些驱动编译为内核本身的一部分（称为*内联*驱动），另一些编译为模块。在内核引导过程中，只有内联编译的设备驱动可供内核使用；模块化驱动只有在系统引导完成后才可用。

> **注意**
>
> 作为一个常见的例子，如果你打算从 SCSI 磁盘引导，SCSI 磁盘驱动器的驱动必须对内核可用。如果内核没有内联编译这些驱动，系统将无法引导，因为它将无法访问磁盘。
>
> 对于模块化内核，绕过此问题的一种方法是使用初始 RAM 磁盘（initrd），在“创建初始 RAM 磁盘映像”部分中稍后会进行讨论。initrd 加载一个小型内核和相应的设备驱动程序，然后驱动程序可以访问设备以加载你想要运行的实际内核。

某些代码只能是其一（对于普通用户来说技术上原因并不重要），但大多数代码可以编译为模块化或内联。根据应用情况，一些系统管理员可能偏好一种方式胜过另一种，但随着快速现代处理器和充足的系统内存，除了最狂热的 Linux 黑客外，性能差异几乎无关紧要。

在编译内核时，选择模块化或内联的步骤是 `make config` 步骤的一部分，我们将在本章后面详细说明。除非你有特定的理由不这样做，否则建议在选择时选择模块化选项。模块管理的过程在下一节中讨论，因为管理模块的频率将高于编译内核。

## 模块管理

在使用模块化内核时，需要特殊工具来管理模块。必须加载和卸载模块，最好能尽可能自动完成。我们还需要能够在加载模块时传递必要的参数——例如内存地址和中断。（这些信息因模块而异，因此你需要查看模块文档以确定需要传递什么信息，如果需要的话。）在本节中，我们将介绍用于管理模块的工具，然后查看一些使用它们的例子。

Linux 为我们提供了以下模块管理工具。所有这些命令（以及 `modprobe.conf`）都有 man 页面：

- `lsmod` — 列出已加载的模块。将此结果通过管道传递给 `less` 命令很有用，因为列表通常超过一页长。
- `insmod` — 此命令将指定模块加载到运行中的内核中。如果给出模块名称而没有完整路径，将搜索运行内核的默认位置 `/lib/modules/*/` 。此命令提供几个选项——最有用的是 `-f`，它强制加载模块。
- `rmmod` — 此命令从运行中的内核中卸载（移除）指定模块。一次可以指定多个模块。
- `modprobe` — `insmod` 和 `rmmod` 的更高级版本；它使用由 `depmod` 创建的依赖文件，并自动处理模块的加载，或者使用 `-r` 选项进行移除。没有强制选项。然而，`modprobe` 的一个有用选项是 `-t`，它使 `modprobe` 循环遍历一组驱动程序，直到找到一个匹配你系统的为止。如果你不确定哪个模块适用于你的网络卡，你可以使用此命令：

```
