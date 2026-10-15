
实用的 `-m` 选项允许你在创建时设置模式，而不是单独使用 `chmod` 命令进行设置。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Partition.html—Linux 分区 HOWTO 包含了大量关于分区和你需求的详细信息。

http://batleth.sapienti-sat.org/projects/FAQs/ext3-faq.html—Linux ext3 FAQ 是一份非官方的常见问题，包含一些有用信息，特别是关于将 ext3 分区转换回 ext2 的。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Undeletion.html—你在 ext2/3 分区上删除了一个文件？Linux Ext2fs 撤销微型 HOWTO 可以为你提供帮助。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Ext2fs-Dir-Struct.html—你在 ext2/3 分区上删除了一个目录？请阅读《Ext2 目录结构撤销 HOWTO》来了解如何救回你的数据。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Loopback-Root-FS.html—这里有一个概念：我们不仅拥有传统的文件系统，还可以在一个位于其他文件系统的大文件内部创建一个系统。Loopback 根文件系统 HOWTO 解释了这一点。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/LVM-HOWTO—抛弃那些将物理磁盘与固定大小系统绑定的概念吧；逻辑卷管理器（LVM）HOWTO 解释了如何克服这种限制性的稀释。

http://linux.org/article/ivm—关于逻辑卷管理器的良好概述和讨论。

http://www.coda.cs.edu/—Coda 网络系统主页。

http://www.inter-mezzo.org/—Intermezzo 网络系统主页。

http://www.math.ualberta.ca/imaging/snfs—通过 SSH 隧道实现安全 NFS 是解决公网上 NFS 安全性短板的一个非常有趣的尝试。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/UMDSOS-HOWTO—如果你对使用 umdos 文件系统感兴趣，UMDSOS HOWTO 提供了丰富的信息。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/NFS-Root.html—NFS-Root 微型 HOWTO。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/NFS-Root-Client-mini-HOWTO.html—详细解释了如何设置和使用 NFS 导出文件系统。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Multi-Disk-HOWTO—多磁盘系统调优 HOWTO 包含了对驱动程序和控制器硬件的有用解释，以及文件系统的讨论。它提供了一个关于优化多磁盘集的有趣章节。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Software-RAID-HOWTO.html—软件-RAID HOWTO 是软件 RAID 的极佳工具。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Tips-HOWTO—Linux Tips HOWTO 提供了一些实用的技巧，值得阅读，因为它解决了一些文件系统问题，如“是否有足够的可用空间？”以及“我是否在文件系统之间移动目录？”

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Large-Disk-HOWTO.html—仍然对驱动几何结构、LILO 和 GRUB 的限制以及那些巨大的磁盘不确定吗？大磁盘 HOWTO 对此提供了实用的细节。它还告诉你如何处理使用 OnTrack 和 EZ_Drive 等磁盘管理器的磁盘。

http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/BootPrompt-HOWTO—BootPrompt HOWTO 通知你可以传递给内核的启动时参数，用于处理异常硬件、配置非即即插设备等。对于本章，第 7 节“硬盘”最有用。

http://www.namesys.com/—关于 reiserfs 改进以及 Reiser4 发布的详细信息（见 http://www.namesys.com/v4/v4.html）。

http://www.linux-usb.org/USB-guide/x498.html—大存储和其他 USB 设备的 USB指南。如果你有一个 USB 设备并需要知道它是否被支持以及如何访问，请查看此处。（提示：USB 存储设备被模拟为 SCSI 设备。）

# 第 40 章

# 内核与模块管理

## 本章内容

- Linux 内核
- 管理模块
- 何时需要重新编译
- 内核版本
- 获取内核源码
- 为内核打上补丁
- 编译内核
- 当出现问题时

Linux 内核
管理模块
何时需要重新编译
内核版本
获取内核源码
为内核打上补丁
编译内核
当出现问题时

Linux 内核是一个复杂的软件，许多人称其为 Linux。作为用户，你很少（甚至从不）与之交互。相反，它是许多人多年工作的成果。内核是操作系统中许多人称为 Linux 的部分。在本章中，我们将研究内核并学习它的作用。在本章中，我们还学习了如何获取内核源码以及如何为内核打补丁。本章将教你内核配置中的基本步骤、如何构建和安装模块，并教你关于 GRUB（默认引导程序）的重要方面。最后，本章的故障排除信息将帮助你在 Linux 安装出现问题时该做什么。尽管这些问题看起来令人不安，但本章向你展示了一些解决内核问题的简单方法。

# 内核模块管理

大多数用户发现预编译的内核符合他们的需求。在某些时刻，你可能需要重新编译内核以支持特定的硬件或添加新功能。如果你听过关于重新编译内核困难的恐怖故事，可以放松；本章为你提供了理解该过程所需的所有信息。

# Linux 内核

Linux 内核是操作系统中许多人称为“Linux”的部分。尽管许多人认为整个发行版都是 Linux，但唯一可以正确被称为 Linux 的部分是内核。Fedora 与许多 Linux 发行版一样，包含内核软件包，其中带有与内核交互的附加软件，使用户能够有意义的方式与系统交互。

系统实用程序和用户程序使计算机成为用户的工具。

第一个 Linux 内核
1991 年，Linus Torvalds 发布了 `.0` 版本的内核，这是他为自己的 Intel 80386 计算机想要一个强大的类 Unix 操作系统的结果。Linux 写了现在被称为 Linux 内核的初始代码，并将其与 Richard Stallman 的 GNU 工具结合。事实上，因为许多 Linux 系统工具都源自 GNU/Linux。自此以后，Linux 受益于数千名贡献者为 Linux 项目投入的天赋和时间。Linux 维护内核，决定哪些内容作为官方发布版（许多人称为原版或 Linux 内核）进入内核。

Linux 源码树

内核源码保存在称为内核源码树的目录中。内核源码树的结构很重要，因为编译（构建）内核的过程是自动化的；它由 `make` 程序解释的脚本控制。这些脚本被称为 `Makefile`，期望在特定位置找到内核代码，否则将无法工作。你将在本章稍后的部分学习如何使用 `make` 来编译内核。

`/usr/src/kernels/<yourkernel>` 目录包含了 `.config` 和 `Makefile` 等文件。`.config` 文件是你 Linux 内核编译时的配置。默认情况下没有 `.config` 文件；你必须从 `/configs` 子目录中选择一个。你会在那里找到 Fedora 发行版内核的配置文件，或者直接将适用于你系统的文件复制到默认目录并将其重命名为 `.config`。

我们已经讨论过 `/configs` 子目录的内容，现在让我们检查 `/usr/src/kernels/<yourkernel>` 下的其他目录。对我们来说最有用的是 `Documentation` 目录。在该目录及其子目录中，你将找到几乎关于内核每个部分的所有文档。每个 `Documentation` 子目录下的 `.00-INDEX` 文件还包含了主目录中的文件列表以及对它们内容的简要说明。许多文件仅为内核编程人员和应用程序编写人员编写，但对于在学习内核和设备驱动程序的中级或高级 Linux 用户来说，用处并不多。一些最有趣且实用的文档包括：

- `devices.txt`——位于 `/dev` 目录中表示的可能 Linux 设备列表，给出了主设备号、次设备号和简短描述。如果你曾经遇到提到 `char-major-xxx` 的错误信息，这就是该列表所在的地方。在第 38 章“管理文件系统”中提到了这些设备。

- `ide.txt`——如果你使用 IDE 硬盘，此文件讨论了内核如何与它们交互，并列出了可以用于解决 IDE 相关问题、手动设置数据结构以及其他管理你 IDE 硬盘的内核命令。大部分管理是自动的，但如果你想知道内核如何与 IDE 设备交互，这个文件对此了了解释。

- `initrd.txt`——第 38 章也讨论了初始 RAM 磁盘（initial RAM disk）。此文件提供了关于初始 RAM 磁盘的更深入知识，提供了用于创建磁盘的回环系统（loopback system）的细节，并解释了内核如何与其交互。

- `kernel-parameters.txt`——这是一个你可以在启动时传递的用于配置内核或硬件设置的参数列表，但乍看之下似乎没用，因为它只是一个列表。然而，知道某个参数的存在并可能与你正在寻找的内容有关，可以帮助你追踪更多信息，因为现在你有了可以输入到如 http://www.google.com/linux 等互联网搜索引擎中的术语。

- `sysrq.txt`——如果你曾经想过键盘上的 SysRq 键是做什么用的，这个文件就是答案。它是硬编码在内核中的组合键，可以帮助你从系统锁定恢复。Fedora 出于安全考虑禁用了它。你可以通过触发命令 `# echo '1' > /proc/sys/kernel/sysrq` 来启用它，通过回值 0 而不是 1 来禁用它。

在 `Documentation` 下的其他目录中，你将找到类似的文本文件，涉及用于 CD-ROM 驱动程序的内核模块、文件系统驱动程序、游戏手柄和摇杆驱动程序、视频驱动程序（不是显卡驱动程序——那些属于 X11R6 而不属于内核）、网络驱动程序，以及 Linux 操作系统中找到的所有其他驱动程序和系统。再次，这些文档通常是为程序员写的，但它们也可以为中级和高级 Linux 用户提供有用信息。

## 第 40 章 内核模块管理

名为 `scripts` 的目录包含许多有用的脚本。对于任何不是程序员或内核开发者（也称为内核黑客）的人来说，它确实不包含任何感兴趣的内容。

内核启动后，所有编译后的文件将填充 `arch` 目录及其子目录。虽然你可以手动将它们移动到最终位置，但我们将在图中展示 `make` 脚本将如何为你完成这一切。在 Linux 早期，这种编译后的文件重定位完全是手工完成的；你应该对此表示感谢。

> 注意
> `make` 工具是一个非常复杂的程序。关于 Makefile 结构的完整文档以及它可以接受的参数的完整文档，可以在 http://www.gnu.org/software/make/manual/make.html 找到。

其余目录包含了内核和内核驱动程序的源码。当你安装内核源码时，这些文件会自动放置在那里。当你修补内核源码时，这些文件会被自动修改。当你编译内核时，这些文件会被访问。尽管你永远不需要触碰源码文件，但有用的内核源码文件无非是带有特殊格式的文本文件，这意味着我们可以查看它们并阅读程序员的注释。有时，程序员会写一个应用程序，但无法（通常也不愿）编写文档。他在源代码中放置的注释通常是该代码存在的唯一文档。

某些代码的注释中甚至隐藏了小型测试程序，并附带了注释以及与其他信息的引用。由于源代码是用一种几乎可以像英语一样易读的语言编写的，非程序员可能能够了解应用程序或驱动程序实际上在做什么（参见第 33 章“Fedora 的 C/C++ 编程工具”）。这些信息对于面临内核和驱动程序相关问题的中高级 Linux 用户来说可能有用。

> 注意
> 硬件的交互和控制由内核中一个称为设备驱动程序的小部分处理。驱动程序告诉计算机如何响应用户提示，与调制调器、SCSI 卡、键盘、鼠标等进行交互。没有驱动程序，内核不知道如何与关联设备交互。

## 内核类型

在 Linux 早期，内核是单块代码，包含了针对处理器、主板和其他硬件的所有指令。如果你更改了硬件，你就必须重新编译内核代码以包含你需要的和不需要的内容。包含额外的、不需要的代码会带来代价，因为内核会变得更大并占用更多内存。在只有 4MB-8MB 内存的旧系统上，浪费宝贵的内存来运行必要的代码被认为是不可接受的。当 Linux 用户试图从他们的计算机中榨出最高性能时，内核编译在当时是一门黑术。这些作为单块代码编译的内核被称为单体内核（monolithic kernels）。

随着内核变得越来越大，可以向计算机添加的设备数量变得繁重。开发出了一种构建内核的新方法使编译任务变得更容易。内核源码中由设备驱动程序代码组成部分可以选择被编译为模块，根据需要加载和卸载到内核中。这被称为构建内核的模块化方法（modular approach）。现在，整个内核可以一次编译——大部分代码被编译成模块。只加载需要的模块；内核可以保持较小，添加硬件也变得简单得多。

典型的内核将驱动程序作为内核的一部分（称为内联驱动程序 inline drivers），其他驱动则编译为模块。在启动过程中，只有内联编译的设备对内核可用；模块化驱动程序仅在系统启动后可用。

注意
> 作为一个常见的例子，如果你打算从 SCSI 磁盘启动，则 SCSI 硬盘驱动程序必须对内核可用。如果内核没有编译这些驱动程序，系统将由于无法访问磁盘而无法启动。

模块化内核解决此问题的方法是使用初始 RAM 磁盘（Initrd），稍后在“创建初始 RAM 磁盘镜像”中讨论。`initrd` 加载一个小型内核和相应的设备驱动程序，然后它可以访问设备以加载你所需的实际内核。

某些代码可以是一种形式也可以是另一种形式（出于对普通用户无关的技术原因），但大多数代码都可以编译为模块或内联。取决于应用程序，某些系统管理员倾向于一种方法而非另一种，但在现代处理器和充足的系统内存的情况下，对于除最热诚的 Linux 黑客之外，性能差异并不重要。

在编译内核时，选择模块化或内联的步骤是 `make config` 步骤的一部分，我们将在本章中详细介绍。除非你有特定的理由，否则我们建议在提供选择时选择模块化选项。管理模块的过程将在下一节中介绍，因为你管理它们的频率比编译内核要高。

# 管理模块

当使用模块化内核时，需要特殊的工具来管理这些模块。必须加载和卸载模块，如果能尽可能自动地完成这些操作就太好了。我们在加载模块时，还需要向它们传递必要的参数——例如内存地址和中断。（这些信息因模块而异，因此你可能需要查看模块的文档来确定需要向其传递哪些信息如果有的话）。在本节中，我们将介绍用于管理模块的工具，然后查看使用这些工具的示例。

Linux 为我们提供了以下模块管理工具。所有命令（以及 `modprobe.conf`）都有很多页面介绍：

- `lsmod`—此命令列出模块。由于列表通常超过一页，因此通过管道传给 `less` 命令处理是很有用的。

- `insmod`—此命令将指定的模块加载到运行的内核中。如果给出的模块名没有带完整路径，它将搜索运行内核的默认位置 `/lib/modules/*`。该命令提供了几个选项——最用的是 `-f`，它可以强制加载模块。

- `rmod`—此命令从运行的内核中卸载（移除）指定的模块。一次可以指定一个模块。

- `modprobe`—这是 `insmod` 和 `rmod` 的高级版本，它使用默认创建的依赖文件并自动处理加载，或通过 `-r` 选项移除模块。有一个非常有用的选项 `modprobe -t`，它会让 modprobe 循环遍历驱动程序集，直到找到与你的系统匹配的一个。如果你不确定哪个模块适用于你的网卡，可以使用此命令：

```
