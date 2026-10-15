
> [1] 我们稍后会谈论内核构建系统和宏。

```
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 14
EXTRAVERSION = =
Name=Affluent Albatross
```

在同一个 makefile 的后面，这些宏被用于组成一个版本级宏，如下所示：

```
KERNELRELEASE-$(PATCHLEVEL).$(SUBLEVEL)$(EXTRAVERSION)
```

该宏用于内核源码树中的多个地方，以指示内核版本。事实上，版本信息的使用频率非常高，内核开发者专门定义了一组从 makefile 中的版本宏派生的宏，位于 Linux 内核源码树的 `.../include/linux/version.h` [2]。这些宏在此处重现，如列表 4-1。

> [2] 在本书中，任何路径前的三个点用于表示在你的系统中到达顶层 Linux 源码树可能采取的路径。

# 列表 4-1. 内核包含文件：`.../include/linux/version.h`

```
#define UTS_RELEASE "2.6.14"
#define LINUX_VERSION_CODE 132622
#define KERNEL_VERSION(a,b,c) (((a) << 16) + ((b) << 8) + (c))
```

你可以通过在 Linux 系统上运行命令来检查内核版本：

```
$ cat /proc/version
Linux version 2.6.13 (chris@pluto) (gcc version 4.0.0) (DENX ELDK 4.0 0.0)) #2
Thu Feb 16 19:03:13 2006
```

关于内核版本的最后一个说明是：你可以通过自定义 `ExtraVersion` 字段，轻松地跟踪自己内核的内核版本。

例如，如果你正在为某些新内核功能开发增强，你可能会将 `EXTRAVERSION` 设置为如下：

```
EXTRAVERSION=foo
```

之后，当你使用 `/proc/version` 时，你会看到 `Linux version 2.6.13-foo`，这可以帮助你区分自己内核的开发版本。

## 4.1.2. 内核源码仓库

内核源码的官方地址是 `www.kernel.org`。在那里你可以找到 Linux 的当前版本和历史版本，以及许多补丁。位于 `ftp.kernel.org` 的主要 FTP 仓库包含了追溯到 Linux 版本 1.0 的子目录。该站点是 Linux 内核持续开发活动的主要焦点。

如果你从 kernel.org 下载了最近的内核，你会在源码树中找到针对 25 种架构和子架构的文件。其他几个开发树支持主要的架构。其中一个问题仅仅是内核开发和更改的数量极其巨大。如果每个架构上的每个开发者都向 kernel 提交补丁，维护者会被大量的更改和补丁管理淹没，将永远无法进行任何功能开发，作为任何参与内核开发的人，这本身已经非常忙了！

在主线 kernel.org 源码之外存在其他公共树，主要用于特定架构的开发。例如，MIPS 架构的开发者可能会在 `www-linux-mips.org` 找到合适的内核。通常情况下，架构树中的工作最终会同步到主线内核，以便尽可能跟上新进展。然而，将自己的补丁纳入主线内核并不总是易的，而且总是存在滞后。在任何时刻架构内核树之间都存在差异。

如果你想如何为你的特定应用程序找到内核，最好的方法是获取最新的稳定 Linux 源码树。检查是否存在对你特定处理器的支持，并在内核邮件列表中搜索与你的应用程序相关的任何问题。还要找到与你兴趣最匹配的邮件列表，并也搜索该存档。

附录 E，“开源资源”包含了几个与内核源码仓库、邮件列表等相关的良好参考文献和信息来源。

## 4.2. Linux 内核构建

在接下来的几节中，我们将探索 Linux 内核的布局、组织和构建。掌握了这些知识，你会发现导航复杂的内核将容易得多。随着时间的推移，架构取得了显著改进，我们将看到许多架构的顶层源码树。

### 4.2.1. 顶层源码目录

顶层目录包含以下目录：

```
arch      crypto    fs       include
init      ipc       lib      mm
net       security  usr
```

构建系统输出多个常用文件，以及特定架构的二进制文件。理解大型镜像的有效方法之一是查看其组件。事实上，入口点（执行的第一行代码）可以在压缩内核中找到。

### 4.2.2. 编译内核

理解像内核这样庞大的软件是一项艰巨的任务。构建系统输出多个常用文件，以及特定架构的二进制文件。两个常用文件是 `system.map` 和 `vmlinux`。前者在内核调试期间非常有用且特别有趣。它包含了内核符号的可读列表及其相应的地址。后者是 ELF 格式的特定架构。

[2] 可执行与链接格式，二进制可执行文件的事实标准。

列表 4-2 是在最近的 ARM Xscale 架构内核执行 `make` 输出片段。基于 Intel IPX25 处理器为 ADI Coyote 参考板配置，使用了以下命令：

```
make ARCH=arm CROSS_COMPILE=xscale-be- ipxxx_defconfig
```

该命令并不构建内核，而是为该架构准备内核。它根据 `ipxxx_defconfig` 文件中的默认值，为该架构构建一个默认配置（`.config` 文件），该文件驱动内核。我们稍后将在第 4.3 节“内核构建系统”中对配置过程进行更多说明。

列表 4-2 显示了构建内核的命令。这里只显示构建输出的开头和最后几行。

# 列表 4-2. 内核构建输出

```
$ make ARCH=arm CROSS_COMPILE=xscale_be- zImage
include/linux/version.h
HOSTCC          scripts/basic/fixdep
<hundreds of lines of output omitted here>
  LD              vmlinux
SYSMAP         System.map
.tmp_System.map
OBJCOPY        arch/arm/boot/Image is ready
Kernel:         arch/arm/boot/compressed/head.o
AS              arch/arm/boot/compressed/piggy.gz
GZIP           arch/arm/boot/compressed/piggy.o
AS              arch/arm/boot/compressed/misc.o
CC              arch/arm/boot/compressed/head-xscale.o
AS              arch/arm/boot/compressed/big-endian.o
```

```
LD arch/arm/boot/compressed/vmlinux
OBJCOPY arch/arm/boot/zImage
Kernel arch/arm/boot/zImage is ready
Building modules, stage 2.
...
```

首先，注意构建的调用。在命令行中指定了目标架构（`ARCH=arm`）和工具链（`CROSS_COMPILE=xscale-be-`）。这强制使 `make` 使用 XScale 工具链来构建内核镜像，并使用内核源码中特定 arm 的分支来处理构建中依赖架构的部分。我们还指定了目标 `zImage`。该目标对于许多架构都是通用的，并在第 5 章“内核初始化”中进行了描述。

你可能注意到的下一点是，每个步骤的实际命令已被隐藏，并替换为简写符号。这样做的动机是清理构建输出，以让人们能够关注中间构建过程，特别是编译器警告。在早期的内核源码树中，每个编译或链接命令都会详尽地输出到控制台，这通常每个步骤都需要几行。新系统绝对是一个改进，因为构建过程中任何未被察觉的错误都能被发现。如果你需要查看特定的构建步骤，可以在命令行上使用 `V=1` 来强制输出。

为了清晰，我们在列表 4-2 中省略了大部分实际的编译和链接步骤。这个特定的构建在构建过程中包含 900 多个单独编译和链接命令。那确实会花费很长时间。毕竟在所有中间文件和库存档被构建和编译后，它们被组合在一个名为 `vmlinux` 的 ELF 构建目标中。尽管它是特定架构的，但这个 `vmlinux` 目标是为所有支持的 Linux 架构产生的通用目标。

## 4.2.3 内核本身：vmlinux

注意列表 4-2 中的这一行：

```
LD /arch/arm/boot/compressed/vmlinux
```

`vmlinux` 文件是真正的内核本身。它是一个完全独立的单体镜像。`vmlinux` 二进制文件中不存在未解析的外部引用。当被调用在正确的上下文中执行时（通过用于启动 Linux 内核的加载器），它会启动运行其上的板卡，并留下一个功能完备的内核。

根据理解系统必须首先理解其组成部分的哲学，让我们来看 `vmlinux` 内核对象的构建过程。列表 4-3 重现了生成 `vmlinux` ELF 的构建过程的实际链接阶段。我们使用换行符（由 UNIX 换行连接符 `\` 表示）对其进行了格式处理，使其更具可读性，但尽管它是列表 4-2 构建过程中 `vmlinux` 链接步骤产生的精确输出。如果你是手动构建内核，这就是你从命令行中发出的链接命令。

### 列表 4-3. 链接阶段：vmlinux

```
xscale-be-ld -p --no-undefined -X -o vmlinux \
-T arch/arm/kernel/vmlinux.lds \
arch/arm/kernel/head.o \
init/built-in.o \
--start-group \
usr/built-in.o \
arch/arm/kernel/built-in.o \
arch/arm/mm/built-in.o \
arch/arm/common/built-in.o \
arch/arm/mach-ixp4xx/built-in.o \
arch/arm/nwfpe/built-in.o \
kernel/built-in.o \
mm/built-in.o \
fs/built-in.o \
ipc/built-in.o \
security/built-in.o \
crypto/built-in.o \
lib/lib.a \
arch/arm/lib/lib.a \
lib/built-in.o \
arch/arm/lib/built-in.o \
drivers/built-in.o \
sound/built-in.o \
net/built-in.o \
--end-group \
tmp.kallsyms2.o
```

## 4.2.4 内核镜像组件

从列表 4-3 中，你可以看到 `vmlinux` 镜像由几个复合二进制镜像组成。现在，理解每个组件并不重要。重要的是理解组成内核的组件的高层视图。列表 4-3 中链接命令的第一行指定了输出文件（`-o vmlinux`）。第二行是链接脚本文件（`vmlinux.lds`），它是关于内核二进制镜像应如何链接的详细配方[4]。

> [4] 链接脚本文件具有特殊的语法。这可以在 GNU 链接器的文档中找到。

列表 4-3 中的第三行及后续行指定了形成结果二进制镜像的对象模块。第一个指定的对象是 `arch/arm/kernel/head.o`，这是一个特定架构的汇编源文件，用于执行非常底层的内核初始化。如果你正在寻找内核执行的第一行代码，那么从这里开始搜索是有意义的，因为它最终将是该链接阶段创建的二进制镜像中找到的第一代码。我们将在第 5 章中详细检查内核初始化。

下一个对象 `init_task.o` 设置了内核所需的初始线程和任务结构。紧随其后是一个巨大的对象模块集合，每个模块都有共同名称：`built-in.o`。然而，你会注意到每个 `built-in.o` 对象都来自内核源码树的特定部分，如 `built-in.o` 对象名称之前的路径组件所示。这些是包含在内核镜像中的二进制对象。一个插图可能会使更加清晰。图 4-1 展示了 `vmlinux` 镜像的二进制组成。它包含了链接阶段的每一行。由于空间考虑，你可以看到每个功能组件的相对大小（img/501695be171f3bb1c3274870cd783_84_0.png）。你可能会感到惊讶，最大的三个二进制组件是系统代码、网络代码和所有内置驱动程序。如果你将内核代码和架构代码放在一起，这就是下一个二进制组件。在这里你可以找到调度器、进程和线程管理、定时器管理和其他核心功能。内核包含架构特定的功能，例如上下文切换、硬件中断和异常处理，可以在 `arch/arm/kernel` 中找到。记住，在这里我们查看一个特定的示例。在这个特定的示例中，我们正在构建适用于 ARM 架构的内核。每个架构和机器在 `arch/arm/mach-ixp4xx` 板卡上有不同的架构特定二进制组件，因此 `vmlinux` 镜像的组成有所不同。为了帮助你理解，表 4-1 列出了组成 `vmlinux` 镜像的每个简短描述。

### 表 4-1. vmlinux 镜像组件

| 组件 | 描述 |
| :--- | :--- |
| `arch/arm/kernel/head.o` | 特定架构的启动代码。 |
| `init_task.o` | 内核所需的初始线程和任务结构。 |
| `init/built-in.o` | 主初始化。见第 5 章。 |
| `usr/built-in.o` | 内置 ramfs 镜像。见第 5 章。 |
| `arch/arm/kernel/built-in.o` | 特定架构的内核代码。 |
| `arch/arm/mm/built-in.o` | 特定架构的内存管理代码。 |
| `arch/arm/common/built-in.o` | 特定架构的通用代码。随架构变化 |
| `arch/arm/mach-ixp4xx/built-in.o` | 特定机器的代码，通常初始化。 |
| `arch/arm/nwfpe/built-in.o` | 特定架构的浮点模拟代码。 |
| `kernel/built-in.o` | 内核本身的通用组件。 |
| `mm/built-in.o` | 通用的内存管理组件。 |
| `ipc/built-in.o` | 进程间通信，如 SysV IPC。 |
| `security/built-in.o` | Linux 安全组件。 |
| `lib/lib.a` | 杂项函数。 |
| `arch/arm/lib/lib.a` | 特定架构的设施。随架构变化。 |
| `lib/built-in.o` | 通用辅助函数。 |
| `drivers/built-in.o` | 所有内置模块。 |
| `sound/built-in.o` | 音频驱动。 |
| `net/built-in.o` | Linux 网络。 |
| `tmp.kallsyms2.o` | 符号表。 |

当我们说内核本身时，引用了这个 `vmlinux` 镜像。如之前提到的很少平台启动此镜像。对于某些平台，它几乎是压缩的。至少，加载器必须解压镜像。许多平台需要在镜像上附加某种存根来执行解压。在第 5 章稍后学习如何为不同的架构、机器类型和加载器打包此镜像，以及启动的要求。

### 4.2.5. 子目录布局

现在你已经看到了构建系统如何控制内核镜像，让我们来看代表性的子目录。列表 4-4 详细介绍了 `mach-ixp425` 子目录的内容。该目录存在于源码树 `../arch/` 特定架构分支下。

### 列表 4-4. 子目录

```
$ ls -l linux-2.6/arch/mach-ixp425
total 92
-rw-r--r-- 1 chris chris 11892 Oct 10 14:53 built-in.o
-rw-r--r-- 1 chris chris 6924 Sep 29 15:39 common.c
-rw-r--r-- 1 chris chris 3525 Oct 10 14:53 common.o
-rw-r--r-- 1 chris chris 13002 Sep 29 15:39 common-pici.c
-rw-r--r-- 1 chris chris 7504 Oct 10 14:53 common-pici.o
-rw-r--r-- 1 chris chris 1728 Sep 29 15:39 coyote-pici.c
-rw-r--r-- 1 chris chris 1572 Oct 10 14:53 coyote-pici.o
-rw-r--r-- 1 chris chris 2118 Sep 29 15:39 coyote-setup.c
-rw-r--r-- 1 chris chris 2180 Oct 10 14:53 coyote-setup.o
-rw-r--r-- 1 chris chris 2042 Sep 29 15:39 ixdp425-pci.c
-rw-r--r-- 1 chris chris 3656 Sep 29 15:39 ixdp425-setup.c
-rw-r--r-- 1 chris chris 2761 Sep 29 15:39 Kconfig
-rw-r--r-- 1 chris chris 259 Sep 29 15:39 Makefile
-rw-r--r-- 1 chris chris 3102 Sep 29 15:39 prcmci100-pci.c
```

列表 4-4 中的目录内容在许多内核源码子目录具有共同组件：`Makefile` 和 `Kconfig`。这两个文件驱动了内核的配置和构建过程。让我们看看它是如何工作的。

## 4.3. 内核构建系统

Linux 内核的配置和构建系统相当复杂，正如人们对一个包含六十多万行代码的软件项目所预期的那样！在本节中，我们将为需要自定义环境的开发者介绍内核构建系统的基础知识。
