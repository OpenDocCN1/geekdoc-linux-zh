

例如，如果你正在为某个新的内核功能开发增强功能，你可能会将 `EXTRAVERSION` 设置为类似以下内容：

```
EXTRAVERSION=-foo
```

稍后，当你使用 `cat /proc/version` 时，你会看到 Linux 版本 2.6.13-foo，这将有助于你区分自己内核的开发版本。

## 4.1.2 内核源代码库

内核源代码的官方主页是 [www.kernel.org](http://www.kernel.org)。在那里，你可以找到当前和历史版本的 Linux 内核，以及大量的补丁。位于 [ftp.kernel.org](http://ftp.kernel.org) 的主要 FTP 库包含一直回溯到 Linux 1.0 版本的子目录。该网站是 Linux 内核内持续开发活动的主要焦点。

如果你从 kernel.org 下载一个较新的 Linux 内核，你会发现在源代码树中有针对 25 种不同架构和子架构的文件。其他几个开发树支持主要架构。其中一个原因 simply 是内核开发人员和变更的数量之巨。如果每个架构上的每个开发人员都向 kernel.org 提交补丁，维护者将被变更和补丁管理淹没，从而无法进行任何功能开发。正如任何参与内核开发的人都会告诉你的那样，已经非常忙碌了！

在主线 kernel.org 源码之外，还有其他几个公共源码树存在，主要用于特定架构的开发。例如，正在处理 MIPS 架构的开发人员可能会在 [www.linux-mips.org](http://www.linux-mips.org) 找到一个合适的内核。通常，在架构树中完成的工作最终会提交到 kernel.org 的内核。大多数架构开发人员努力尽可能频繁地与主线内核同步，以跟上新的开发。然而，将个人的补丁包含进主线内核并不总是直接的，并且总会有滞后。事实上，在任何一个给定的时间点，架构内核树之间都存在差异。

如果你想知道如何为你的特定应用找到内核，最好的方法是获取最新的稳定 Linux 源码树。检查是否存在对你特定处理器的支持，然后搜索 Linux 内核邮件列表中任何与你应用程序相关的补丁或问题。此外，找到最符合你兴趣的邮件列表，并搜索该存档。

附录 E，“开源资源”，包含关于内核源代码库、邮件列表等的几个良好参考和信息来源。

## 4.2 Linux 内核构建

在接下来的几个章节中，我们将探讨 Linux 内核的布局、组织和构建。掌握这些知识，你会发现在这个庞大、复杂的代码库中导航变得容易得多。随着时间的推移，源码树的组织已经有了重大改进，特别是在架构分支中，该分支包含对众多架构和特定机器的支持。在本书撰写期间，正在进行一项努力，将 ppc 和 ppc64 架构分支合并为一个共同的 powerpc 分支。尘埃落定后，会有很多改进，包括消除重复代码、更好的文件组织以及功能分区。

### 4.2.1 顶级源代码目录

我们在书中频繁提到顶级源代码目录。在所有情况下，我们指的是内核源代码树中包含的最高级目录。在任何给定机器上，它可能位于任何地方，但在桌面 Linux 工作站上，它通常位于 /usr/src/linux-x.y.z，其中 x.y.z 表示内核版本。在整个书中，我们使用简写 .../ 来表示顶级内核源代码目录。

顶级内核源代码目录包含以下子目录。（为了清晰和简洁，我们省略了此列表中的非目录项，以及用于源代码控制的目录。）

arch crypto Documentation drivers fs include init ipc kernel lib mm net scripts security sound usr

这些子目录中的许多包含额外的几个层级的子目录，里面装有源代码、makefiles 和配置文件。Linux 内核源代码树中最大的分支无疑是在 .../drivers 下。在这里你可以找到以太网网卡、USB 控制器以及 Linux 内核支持的众多硬件设备的支持。正如你可以想象的那样，.../arch 子目录是第二大，包含对 20 多种独特处理器架构的支持。

在顶级 Linux 子目录中发现的其他文件包括顶级 makefile、一个隐藏配置文件（*dot-config*，在第 4.3.1 节“Dot-Config”中介绍）以及各种其他不参与构建本身的信息文件。最后，在成功构建后，在顶级内核源代码树中发现两个重要的构建目标：*System.map* 和内核本体，*vmlinux*。两者稍后都会描述。

### 4.2.2 编译内核

理解像 Linux 这样的大量软件可能是一项艰巨的任务。它太大，无法简单地“逐步执行”代码来跟踪正在发生的事情。多线程和抢占增加了分析的复杂性。事实上，即使定位入口点（进入内核时执行的第一行代码）也可能是具有挑战性的。理解大型二进制映像结构的一个更有用的方法是检查其构建组件。

内核构建系统的输出产生几个常见的文件，以及一个或多个特定架构的二进制模块。无论架构如何，常见文件始终都会构建。两个常见文件是 *System.map* 和 *vmlinux*，前面已介绍。前者在内核调试期间很有用，并且特别有趣。它包含内核符号及其各自地址的可读列表。后者是一个特定架构的 *ELF*³ 可执行格式文件。它由顶级内核 makefile 为每个架构生成。如果内核是用符号调试信息编译的，它将包含在 *vmlinux* 映像中。在实践中，虽然它是一个 ELF 可执行文件，但通常 *从不* 直接引导此文件，你很快就会看到。

Listing 4–2 是执行 make 命令后在配置为 ARM *XScale* 架构的最新内核树中产生的输出片段。内核源代码树配置为基于 Intel *IXP425* 网络处理器的 ADI Engineering Coyote 参考板，使用以下命令：

```
make ARCH=arm CROSS_COMPILE=xscale_be- ixp4xx_defconfig
```

此命令不构建内核；它为该架构准备内核源代码树，包括针对此架构和处理器初始默认配置。它构建一个默认配置（dot-config 文件），该配置基于 `ipx4xx_defconfig` 文件中的默认值来驱动内核构建。我们将在第 4.3 节“内核构建系统”中更多关于配置过程。

Listing 4-2 展示了构建内核的命令。此处仅显示构建输出的前几行和后几行以供讨论。

**Listing 4-2: 内核构建输出**

```
$ make ARCH=arm CROSS_COMPILE=xscale_be- zImage
CHK    include/linux/version.h
HOSTCC scripts/basic/fixdep
.
.  <此处省略了数百行输出>
.
LD     vmlinux
SYSLMAP System.map
SYSLMAP .tmp_System.map
OBJCOPY arch/arm/boot/Image
Kernel: arch/arm/boot/Image is ready
AS     arch/arm/boot/compressed/head.o
GZIP   arch/arm/boot/compressed/piggy.gz
AS     arch/arm/boot/compressed/piggy.o
CC     arch/arm/boot/compressed/misc.o
AS     arch/arm/boot/compressed/head-xscale.o
AS     arch/arm/boot/compressed/big-endian.o
LD     arch/arm/boot/compressed/vmlinux
OBJCOPY arch/arm/boot/zImage
Kernel: arch/arm/boot/zImage is ready
Building modules, stage 2.
```

首先，注意构建的调用。所需的架构（`ARCH=arm`）和工具链（`CROSS_COMPILE=xscale_be-`）都在命令行上指定。这强制 *make* 使用 XScale 工具链来构建内核映像，并使用内核源代码树中特定于 arm 的分支来构建依赖于架构的部分。我们还指定了一个称为 *zImage* 的目标。该目标在许多架构中很常见，并在第 5 章“内核初始化”中描述。

你可能注意到的下一件事是，用于每个步骤的实际命令已被隐藏，并用简写符号替换。这样做的动机是清理构建输出，以便更关注中间构建

