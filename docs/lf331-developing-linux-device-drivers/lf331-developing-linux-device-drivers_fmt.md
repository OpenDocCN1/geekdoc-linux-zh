
# LF331 Linux 设备驱动开发

![](img/134c18b05ee9bbbe93ba3f4335720ac1_0_0.png)

![](img/134c18b05ee9bbbe93ba3f4335720ac1_2_0.png)

- 32.1 什么是块设备驱动程序? ..................................................................................................................................... 289
- 32.2 缓冲 ....................................................................................................................................................................... 290
- 32.3 注册块设备驱动程序 ................................................................................................................................................ 290
- 32.4 磁盘结构 (gendisk) ................................................................................................................................................ 292
- 32.5 请求处理 .................................................................................................................................................................... 293
- 32.6 实验 ..................................................................................................................................................................... 296

某些章节可能是可选的。它们包含了背景知识、特殊主题或高级课题。讲师可以根据课堂经验和时间限制决定是否涵盖。

# 图列表

- 3.1 从应用程序到设备 ................................................................. . . . . . . . . . . . . . . . . 19
- 3.2 USB: 控制器、核心与设备 ................................................................. . . . . . . . . . . . . . . . . 19
- 3.3 驱动程序中的二进制大对象 (Blobs) ................................................................. . . . . . . . . . . . . . . . 20
- 5.1 访问设备节点 ................................................................................................................................................................................. . . . . . . . 46
- 6.1 内核主任务 .................................................................................................................................................................................................... . . . . . . 60
- 6.2 用户空间与内核空间 .................................................................................................................................................................................................... . . . . . . . . 61
- 15.1 用户与内核地址区域 ................................................................................................................................................................................. . . . . . . 136
- 15.2 DMA、普通内存与高内存 .................................................................................................................................................................................................... . . . . . . 137
- 20.1 PCI 配置空间 .................................................................................................................................................................................................... . . . . . . . . 201
- 23.1 网络层 .................................................................................................................................................................................................................................................... . . . . . . . . 228
- 23.2 数据包封装 .................................................................................................................................................................................................................... . . . . . . 229
- 24.1 套接字缓冲区布局 ........................................................................................................................................................................................................................ . . . . . . . . 241



## 27.1 USB 拓扑 258

## 27.2 USB 描述符 259

## 表格列表

| 编号 | 名称 | 页码 |
|------|------|------|
| 3.3 | `printk()` 日志级别 | 25 |
| 5.1 | 设备节点宏 | 42 |
| 5.5 | `file` 结构元素 | 54 |
| 5.6 | `inode` 结构元素 | 55 |
| 7.1 | 32位 x86 异常 | 67 |
| 7.2 | IRQ 状态值 | 72 |
| 7.3 | IRQ 处理程序标志位 | 73 |
| 7.6 | IRQ 处理程序返回值 | 75 |
| 8.1 | 许可证 | 78 |
| 10.2 | 定时器组 | 100 |
| 12.1 | `ioctl()` 返回值 | 120 |
| 12.3 | `ioctl()` 命令位域 | 122 |
| 15.1 | `GFP` 内存分配标志 | 138 |
| 15.3 | 内存缓存标志 | 142 |
| 16.2 | `mmap()` 内存保护位 | 152 |
| 16.3 | `mmap()` 标志 | 152 |
| 17.1 | `poll()` 标志 | 170 |
| 18.1 | 软中断 (`Softirq`) 类型 | 175 |
| 18.2 | 延迟函数类型 | 175 |
| 19.2 | 串口鼠标节点和寄存器 | 197 |
| 20.1 | PCI 特性 | 200 |
| 20.2 | `pci.driver` 结构元素 | 203 |
| 22.1 | DMA 传输方向值 | 222 |
| 24.1 | 某些重要的 `netdevice` 结构元素 | 235 |
| 24.2 | `netdevice` 接口信息 | 236 |
| 24.3 | `netdevice` 直接设置字段 | 237 |
| 24.4 | `netdevice` 标志 | 237 |
| 24.5 | `netdevice` 特性 | 238 |
| 24.6 | `netdevice` 工具字段 | 238 |
| 24.7 | `net.device_ops` 功能方法 | 240 |
| 24.8 | Socket 缓冲区字段 | 242 |



| 24.9 | Socket 缓冲区函数 | ................................................................................................................................................ 243 |

| 26.1 | 多播标志 | ................................................................................................................................................... 252 |

| 27.2 | USB 设备类 | ............................................................................................................................................... 260 |

| 28.1 | MTD 链接 | ................................................................................................................................................................................ 268 |

| 28.2 | NOR 和 NAND 设备特性 | ................................................................................................ 269 |

| 29.1 | ACPI 电源状态 | ....................................................................................................................................... 274 |

| 29.2 | ACPI 设备电源状态 | ...................................................................................................... 275 |

# 第 1 章

## 引言

![](img/134c18b05ee9bbbe93ba3f4335720ac1_16_0.png)

我们概述了目标并描述了目标读者。

- 1.1 目标 1
- 1.2 谁是谁 2

### 1.1 目标

- 编写`Linux 设备驱动程序`旨在向经验丰富的程序员展示如何为 Linux 系统开发设备驱动，并让他们对 Linux 内核有基本的理解和熟悉。
- 掌握这些内容后，你将熟悉 Linux 下使用的不同类型的设备驱动，并知道设备（包括硬件和软件）与内核交互的适当 API。
- 我们将主要关注设备驱动程序，次要关注 Linux 内核。由于设备驱动是内核不可或缺的一部分，这两者是无法分离的。然而，设备驱动不需要学习内核的所有内容；你对内核如何处理事务了解得越多，编写的设备驱动就越好。
- 在许多闭源操作系统中，设备驱动和内核之间有清晰的隔离。因为 Linux 是开源的，设备驱动可以访问内核的所有内容。

### 引言

开发设备驱动在深度和广度上都是一个巨大的课题。为了保持内容的可管理性，我们将限制范围。这意味着我们不会深入研究内核内部细节。

我们的演示顺序不是公理性的；也就是说，会有一些前后引用和离题。目的是让你尽可能地开始编码。我们会尽早教你如何用简单的方法动态分配内存，稍后会更地涵盖该主题。此外，主题的顺序具有灵活性。

### 1.2 谁是谁

- 你对为 Linux 系统编写设备驱动程序感兴趣。也许你只是出于兴趣，但更有可能这是你工作的一部分。这里的目的是为你铺路，并可能缩短达到该领域基础水平所需的时间。
- 你能收获多少以及你编写的驱动效率和优化程度，取决于你在学习这些材料之前是一个多么优秀的程序员。这里没有打算或时间教你良好的编程元素或 Linux 操作系统设计。
- 你应该：
  - 精通 C 语言。
  - 熟悉基础的 Linux `Unix` 工具，如 `ls`、`rm`、`grep`、`tar`，并熟悉 shell 和脚本。
  - 熟练使用任何可用的文本编辑器（例如 `vi`、`emacs`）。
  - 了解编译和链接程序、构建 `Makefile` 的基础知识；也就是说，习惯在 Linux 或 Unix 环境下进行应用程序开发。
  - 对 Unix 或 Linux 环境下的系统编程有良好的理解，至少从编写应用程序的角度来看。
- 任何主流 Linux 发行版的经验都有帮助，但不是严格要求。
- 如果你有配置和编译内核以及编写内核模块和设备驱动的经验，你将从这些材料中获得更多。
- 如果你良好掌握操作系统原理并熟悉任何其他操作系统的内部，你将从这些材料中获更多。

# 第 2 章

# 准备知识

![](img/134c18b05ee9bbbe93ba3f4335720ac1_18_0.png)

我们将讨论我们的流程。我们还将对 Linux 发行版、内核版本和硬件平台进行一些说明，并向你展示如何为不同的内核版本快速重新编译。我们将介绍 Linux 驱动程序项目并描述阶段驱动程序（staging drivers）的使用。最后，我们将指出一些文档来源。

| 2.1 | 流程 | 3 |
| 2.2 | Linux 发行版 | 5 |
| 2.3 | 内核版本 | 6 |
| 2.4 | 自行编译内核 | 8 |
| 2.5 | 平台 | 12 |
| 2.6 | 硬件 | 12 |
| 2.7 | Linux 驱动程序项目 ** | 12 |
| 2.8 | 阶段驱动程序 | 13 |
| 2.9 | 文档与链接 | 13 |

> ** 这些章节可以被部分或全部视为可选内容。它们包含了背景材料、专门主题或高级课题。教师可能会根据课堂经验和时间限制，选择涵盖或不涵盖它们。

## 2.1 流程

- 你需要一台安装了当前最新 Linux 发行版的计算机，并妥善部署了重要的开发工具（用于编译等）。
- 重点将放在实操编程上，大多数章节都有实验室练习。在可行的情况下，实验室将建立在之前的实验作业的基础上。解决方案在可用后，可以从 `http://training.linuxfoundation.org/course_materials/LF331` 获取，错误列表和更新后的解决方案也将发布在该网站上。
- 我们将提供实验室解决方案，以便你至少看到一个成功的实现，并并在如果下一个实验练习是后续工作时，提供一个可以开始的模板。此外，在讲解过程中展示的示例也将作为 `SOLUTIONS` 软件包的一部分提供，位于 `EXAMPLES` 子目录中。一旦你获得了解决方案，可以使用以下命令进行解压：

```
$ tar zxvf LF331_SOLUTIONS*.tar.gz
```

或者

```
$ tar jxvf LF331_SOLUTIONS*.tar.bz2
```

替换为实际文件名。

- 在主解决方案目录下，有一个 `Makefile`，它可以递归编译所有子目录。它足够智能，区分内核代码、用户应用程序以及是否使用了多线程。
- 有一些可调的特征；默认情况下，所有子目录都会针对当前运行内核的源码进行递归编译。你可以在以下示例中缩小目录范围、选择不同的内核源码，或选择不同的架构：

```
$ MKDIRS=$22
$ KOTDIR=/lib/modules/3.1.0/build
$ MKDIRS=$0.0*23
$ KOTDIR=/lib/modules/linux-3.1.0/build
$ ARCH=i386
$ ARCH=arm CROSS_COMPILE=arm-toolchain-linux-gnueabi-
```

其中 `KOTDIR` 指向内核源文件。在 x86_64 平台上，指定 `i386` 将构建 32 位模块。若要在 x86 主机上为 ARM 编译内核，我们需要安装交叉编译器并设置 `CROSS_COMPILE` 标志。`CROSS_COMPILE` 标志用于指定编译器前缀。你的工具链的实际前缀可能不同，例如 `arm-linux-eabi-gcc` 二进制文件将具有 `arm-linux-eabi-` 作为编译器前缀。主目录下的 `genmake` 脚本对于自动生成 `Makefile` 非常有用，值得仔细读读。

- 为了使此工作，必须准备内核源码；特别是它必须有一个配置文件（内核源码目录下的 `.config`）并设置好正确的依赖关系。
- 注意，我们在解决方案中强调了清晰、简洁和严谨性；例如，我们没有尝试捕捉每一个可能的错误，也没有考虑到每一个可能的内核配置选项。代码并非无懈可击；它的目的是教学。



- 如果你对这些材料有任何问题或反馈，请通过以下邮箱与我们联系：trainingquestions@linuxfoundation.org。
- 提供的解决方案可能包含正未讨论的功能和特性。
- 这样做是为了说明完成解决问题最小工作之外的方法，并教授额外的材料。
- 如果有必须使用但材料中未涵盖的内容，那就是 bug 而不是特性，应该引起我们的注意。

## 2.2 Linux 发行版

有很多 Linux 发行版，从非常为人熟悉到冷门的皆有。它们根据预期用途、硬件和受众以及支持级别而异。你可以在 http://lwn.net/distributions/ 找到非常全面的列表。

我们努力让这些材料尽可能与发行版无关，因此我们将关注从 http://www.kernel.org 获取的原生内核（vanilla kernels）。对于除最专门的发行版外，这不会带来任何不便。

你应该能够在任何主流发行版上，使用供应商提供的内核完成此处提供的任何实验室练习，只要你安装了内核源码或开发包。此外，提供的解决方案应该编译，只要内核不是太旧；对于早于 2.6.26 的内核，可能需要进行细微调整。

偶尔你正在使用的发行版会产生重要性，但这只会在我们（不情愿地）深入系统管理时发生，例如当我们必须描述特定文件和目录的位置，或如何安装某些所需的软件包时。幸运的是，现代发行版在这些方面与 Linux 早期差异小得多，我们很少需要处理此类入侵。

材料主要在基于 Red Hat 的系统上开发，大部分是 64 位变体，并进行了测试。它在许多其他发行版上进行过测试。明确来说我们使用了：

- Red Hat Enterprise Linux 5, 6
- Fedora 15
- CentOS 5, 6
- Scientific Linux 5, 6
- Open Suse 11.3
- Debian Lenny and Squeeze
- Ubuntu 10.10, 11.04
- Gentoo

关于软件安装和控制，发行版倾向于使用基于 RPM 或基于 deb 的包管理。在上述列表中，Red Hat、Fedora、CentOS、Scientific 和 OpenSUSE 是基于 RPM 的，Debian 和 Ubuntu 是基于 deb 的。如有，我们将为这两个家族之一提供所需的说明。

`GENTOO` 既不基于上述任何一个，而是使用 `portage/emerge`。

## 2.3 内核版本

- 对于本课程，我们有多个内核源码选择可用。我们将使用最新的稳定 Linux 系列，版本为 2.6。实验室解决方案设计用于最新的内核（截至本文时为 3.1），并追溯到 2.6.26。由于 2.4 内核系列偶尔在使用，我们将指出重要的变化。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_21.png)

- 在材料的某处你会发现像这样的框，指示内核版本依赖。
- 它们可能会突出新的、最近修改、开发中或标记为过时的内核特性。

外部模块编译所需的内核源码部分（`kernel-dev` 包）应该已经安装在你的系统中。

各种版本的最新稳定发布可以从 http://www.kernel.org 获取，由 Linus Torvalds 发布的最新开发内核。存在许多仓库，但来源与主内核网站不同。例如，有针对网络问题、USB 等阶段树（staging trees）。

另一个值得特别提到的是 linux-next 项目，其信息见 http://linux-fseidel.de/linux-next/pmwiki/ 该内核积累了下一个内核版本的补丁集，即在 3.2 正在开发时，linux-next 收集并调试适用于 3.3 的材料并解决冲突。

使用网站的 服务器，你可以确定最新的内核版本：

$ @kernel.org

```
最新的内核版本是:      next-201101729
最新的快照 3 版本是:      3.0-git11
最新的主线 3 版本是:               3.0
最新的稳定 3 版本是:               3.0
最新的稳定 2.6.39 版本是:      2.6.39.3
最新的稳定 2.6.38 版本是:      2.6.38.8
最新的稳定 2.6.37 版本是:      2.6.37.6
```

## 2.3. 内核版本

最新的 2.6.36 版本 Linux 内核：2.6.36.4

最新的长支持版本 2.6.35 版本 Linux 内核：2.6.35.13

最新的长支持版本 2.6.34 版本 Linux 内核：2.6.34.10

最新的长支持版本 2.6.33 版本 Linux 内核：2.6.33.16

最新的长支持版本 2.6.32 版本 Linux 内核：2.6.32.43

最新的长支持版本 2.6.27 版本 Linux 内核：2.6.27.59

- 内核版本编号由三个整数组成，前两个表示主发行版本（major），第三个表示次要版本号（minor）；例如 2.6.39 或 2.4.33。此外，还可能附加一个额外的字符串如 2.6.33.1-rt11，这并不是真正的内核版本号的一部分。例如，如果内核在内核源码的主 Makefile 中是

```
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 33
EXTRAVERSION = .1-rt11
```

- 文件 `/usr/src/linux/include/version.h` 提供了了一些宏来方便操作：

```
#define LINUX_VERSION_CODE 132639
#define KERNEL_VERSION(a,b,c) (((a) << 16) + ((b) << 8) + (c))
```

其中 `LINUX_VERSION_CODE` 是通过 `KERNEL_VERSION()` 宏得到的。不等效的语句是：

```
#define KERNEL_VERSION(a,b,c) ( a ) * 65536 + ( b ) * 256 + ( c )
```

该头文件是在编译期间构建的，在原始源码中是不存在的。

- 在本示例中可以处理依赖于版本的代码：

```c
#include <version.h>

if LINUX_VERSION_CODE < KERNEL_VERSION(2,6,0)
    call_usermodehelper(cmd, argv,envp);
else
    call_usermodehelper(cmd, argv,envp);
```

> 这种显式的版本依赖在官方内核树中是不受鼓励的。人们应该放弃对早期内核版本的向后兼容，以保持代码的整洁和最高效率。

- 这种态度被外部设备驱动维护者认为是不方便的，因为当修补漏洞或安全问题时，会导致必须为旧内核维护不同的驱动程序源码。

- 从 2.6.11 开始，采用了一种新方案，第四位数字用于涉及严重漏洞和安全问题的小补丁。内核只接受非争议性的补丁，并按照 2.6.11.1、2.6.11.2、2.6.11.3 等方式进行编号。

## 第 2 节 预备知识

- 这种思想为开发过程带来了很大程度的稳定性，并平息了一些关于没有足够稳定的内核用于生产环境的抱怨。关于该稳定内核树接受哪些类型的补丁的规则可以在 `/usr/src/linux/Documentation/stable.kernel.rules.txt` 查看。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_23_0.png)

- 3.0 Linux 内核版本于 2011 年 7 月 22 日发布。主版本号的提升并不是为了反映重大变化或新功能。
- 内核编号现在将回到三个主数字；主发行版本将增加第二个数字，而稳定更新将反映在第三个数字中，例如 3.0.1、3.0.2 等。
- 某些用于构建内核的工具已经过修改以适应新方案，其他工具最终也会跟进。

## 2.4 编译你自己的自己的内核

- 出于实验目的，你可能想尝试使用另一个内核，特别是你可能想从 http://www.kernel.org 编译并安装一个原生内核（vanilla kernel）。为了做到，你需要两个文件：
- 压缩的内核源码（例如 `linux-3.1.tar.bz2`）
- 一个配置文件（例如 `config-3.1_x86_64`）
- 第一个文件可以从 http://www.kernel.org 获取，第二个文件可以从 http://training.linuxfoundation.org/course_materials/LF331 获取。（这些示例配置文件在所有情况下都能正常工作，但经过测试发现它们在大多数情况下是足够的。）
- 以下脚本（`DO_KERNEL.sh`）包含在你的解决方案中，它可以处理所有必要的解压、配置和安装步骤。你可能想将其放入路径中，例如通过复制到 `/usr/local/bin`。为了对 `linux-3.1.tar.bz2` 执行完成所有操作，只需输入：

```bash
$ /DO_KERNEL.sh linux-3.1.tar.bz2 config-3.1_x86_64
```



- 如果内核源码已经解压并配置过，只需进入内核源码目录并不带参数运行脚本即可完成编译和安装。

```bash
#!/bin/bash
## 用于编译和安装 Linux 的脚本
```

12

# 第 2 章 基础知识

## 2.5 平台

- 我们将尽可能保持平台无关性。然而，我们会显式地考虑 `x86` 架构，而不会过度关注 `IA64`、`Alpha`、`SPARC`、`PPC`、`ARM` 等平台上的 Linux。

- 显式考虑 `x86` 架构至少有三个理由：

  - Linux 内核的某些部分必须依赖于平台，要理解其具体运行机制需要某些特殊知识。

  - 你现在可能正在 `x86` 机器上工作。

  - 大多数开发 Linux 的人员都在关注这个平台。

- 我们将尝试将任何平台依赖显式化。所有解决方案都已经在 32 位和 64 位架构上通过了测试。

## 2.6 硬件

- 有时人们在教授设备驱动时，会使用挂在外部端口的简单设备。与其这样做，我们将使用机器上的硬件作为网卡和输入设备，并利用内核共享中断的能力，在已安装的驱动之上构建设备驱动程序。

- 问题通常属于以下几类：

  - 我的设备使用了多少个 I/O 端口？使用了哪些地址？

  - 是什么 `IRQ`？

  - 我读取的是字节（`bytes`）还是字（`words`）？每次中断读取多少个？

  - 设备遵循什么标准？

> 这些问题只能通过硬件规格书来回答，有时还需要通过检查硬件本身来回答。当你编写设备驱动程序时，必须具备此类知识，如果你无法编写驱动程序，就无法完成工作。（当然，通过探测一个保密规格的设备可以推导出很多信息，许多驱动程序都是这样工程化的。但随着 Linux 的成熟，这种情况已越来越少见，与其在这类工作上花费时间和精力和，不如鼓励制造商合作（如果他们希望自己的设备获得支持），这样更有价值。）

- 从硬件人员那里尽可能获取更多信息，但要准备好面对新设备时，其中某些信息可能是错误的或过时的。硬件与规格书不同步，或者设备未能完全遵循规格的情况并不罕见。有时这是因为设备制造商满足于设备在市场主导操作系统上运行良好，然后就停止了提问。

- Linux 驱动项目（Linux Driver Project）由一组内核开发人员和一些管理员组成，负责免费提供开源驱动程序。该项目将与制造商紧密合作，并在必要时只要最终工作符合适当的 GPL 协议，就会签署 `NDA`（保密协议）。

## 2.8 暂阶段驱动 (STAGING DRIVERS)

- 该项目由 Greg Kroah-Hartman 领导，他的博客地址为 `http://www.kroah.com/`。欢迎新志愿者加入。我们的主页位于 `http://linuxdriverproject.org/twiki/bin/view/`。潜在候选列表维护在 `http://linuxdriverproject.org/twiki/bin/view/`。此外，还维护了存在 Linux 驱动的设备列表，可以在 `http://www.kernel.org/devices/` 找到。

- 从 2.6 内核开始，内核源码中增加了一个用于暂阶段驱动（staging drivers）的新区域。大家都，以这种方式包含的驱动程序预计不会达到已包含在主内核树中的驱动程序的水平。

- 这些驱动可能无法工作，或者使用的用户空间接口比这些驱动程序中的任何一个都更可能发生变化。

- 此外，使用这些驱动会污染（taint）内核。

- 暂阶段驱动的目的是为内核源码树提供一个屏障，并接触更广泛的开发者。这部分是为了让那些抱怨让内核被内核有多困难的批评者闭嘴。

- 任何在暂阶段树中停留未改进或未获得关注的驱动，将在一段时间后被移除。暂阶段树的原始概念也已扩展，包含了那些由于不再维护或被新驱动取代而即将退出的驱动。

## 2.9 文档与链接

- 关于 Linux 内核的最佳文档来源是源码本身。在很多情况下，它是唯一的文档。在不查看源码的情况下，永远不要相信书籍（包括本书）或文章中看到的内容。

- `/src/linux/Documentation` 目录包含许多有用条目。部分文档是使用 DocBook 系统生成的（参见 `http://www.docbook.org/`）。要生成这些文档，进入 `/src/linux` 并输入：

```
$ make htmldocs | psdocs | pdfdocs
```

- 不同格式的文档可以通过网页、postscript、便携文档格式（PDF）或富文本格式提供，将出现在 `/src/linux/Documentation` 目录中。警告：生成这些文档可能比编译内核本身还要长时间！为了让其正常工作，你可能需要在系统上安装额外的软件，如 `jade` 或 `latex`。

### 书籍

- 《Linux Device Drivers, Third Edition》，由 Jonathan Corbet, Alessandro Rubini 和 Greg Kroah-Hartman 编写，O'Reilly 出，2005 年。

- 完整的未删减在线版本可以在 `http://lwn.net/Kernel/LDD3/` 查看并从 `http://lwn.net/Kernel/LDD3.pdf` 下载。

- 《Understanding the Linux Kernel, Third Edition》，由 Daniel P. Bovet 和 Marco Cesati 编写，O'Reilly 出，2005 年。

- 《Understanding Linux Network Internals》，由 Christian Benvenuti 编写，O'Reilly 出，2006 年。

- 《Linux Kernel in a Nutshell》，由 Christian Kroah-Hartman 编写，O'Reilly 出，2006 年。

- 该书的全文可以在 `http://www.kroah.com/lkn/` 查看或下载。

- 《Linux Kernel Development, Third Edition》，由 Robert Love 编写，Addison-Wesley 出，2010 年。

- 《Linux Debugging and Performance Tuning: Tips and Techniques》，由 Steve Best 编写，Prentice Hall 出，2005 年。

- 《Writing Linux Device Drivers: a guide with exercises》，由 Jerry Cooperstein 编写，CreateSpace 出，2009 年。

- 《Linux Program Development: a guide with exercises》，由 Jerry Cooperstein 编写，CreateSpace 出，2009 年。

### 内核开发与邮件列表网站

- `http://lwn.net` Linux Weekly News：最新的 Linux 新闻，包括内核板块。这个非常重要的网站由用户订阅支持，请考虑进行个人或企业捐赠！

- `http://ldn.linuxfoundation.org/book/how-participate-linux-community`：内核开发过程的完整视图以及如何加入。

- `http://lwn.net/Articles/driver-posting`：Jonathan Corbet 关于向 2.6 版本发布设备驱动的文章合集。

- `http://www.linuxfoundation.org/collaborate/lwf`：Linux 天气预报（Linux Weather Forecast）跟踪未来可能合并的内核开发进展。

- `http://lkml.org/`：内核邮件列表的实时存档。

- `http://www.tux.org/lkml`：内核邮件列表常见问题解答（FAQ）：如何订阅、发布到内核邮件列表，以及如如何提交和使用补丁的相关事项。

- `http://linux.yyz.yz/patch-format.html`：向官方树提交补丁的详细指南。

- `http://linux.yyz.yz/git-howto.html`：内核黑客 Git 指南，这是许多高级内核开发人员使用的源码管理系统。

# 第 3 章：设备驱动程序

我们将讨论如何使用设备驱动程序并考虑不同类型的设备；即字符设备、块设备和网络设备。我们将讨论机制（mechanism）与策略（policy）之间的区别。我们将考虑二进制大包（binary blobs）的缺点。然后，我们将快速介绍应用程序如何与设备驱动程序接口并进行系统调用。我们将看到错误是如何定义的，以及如何使用 `ioctl()` 获取输出。我们将详细考虑这些内容。

- 3.1 设备类型 ............................................ 17

- 3.2 机制 vs 策略 ................................ 20

- 3.3 避免大包 ........................................ 20

- 3.4 应用程序如何使用设备驱动程序 ............... 21



### 3.5 走通系统调用

### 3.6 数字

### 3.7 `ioctl()`

### 3.8

### 3.1 设备类型

设备驱动程序是软件的最低级，因为它直接绑定到设备的特性上。内核可以被视为设备驱动程序之上的应用程序；每个驱动程序管理一个或多个硬件部分，而内核处理进程调度、文件系统访问等。

驱动程序可以集成到内核中，也可以设计为可加载模块。并不是所有模块都是设备驱动程序。驱动程序可以被设计为模块化或内核的内置部分，且源代码很少或没有变化。在通常的分类中，有三种主要类型：

#### 字符设备

- 可以一次一个字节地进行读写。很好地表示为流。
- 通常允许顺序访问。
- 可以视为文件。
- 实现 `open`、`close`、`read` 和 `write` 函数。
- 串口/并行端口、控制台（显示器和键盘）等。
- 示例：`/dev/tty`、`/dev/ttyS0`、`/dev/tty0`、`/dev/lp`

#### 块设备

- 只能按块大小倍数进行读写；访问通常会被缓存。
- 允许随机访问。
- 文件系统可以挂载在这些设备上。
- 在 Linux 中，设备可以像字符设备一样一次传输任意数量的字节。
- 硬盘、CD 驱等。
- 示例：`/dev/sda`、`/dev/fd`

#### 网络设备

- 传输数据包。设备感知的是数据包，而不是流。
- 最多通过 socket 接口访问。
- 内核不是调用 `read` 和 `write`，而是调用接收和传输函数。
- 网络接口不映射到文件系统；它们通过名称识别。
- 示例：`eth0`、`ppp`

### 设备类型与用户-硬件连接

区分驱动程序类型的是它们用于连接内核与用户空间的方法。大多数情况下，连接通过 VFS（虚拟文件系统）传递，调用哪些方法取决于访问的是字符设备节点、块设备节点还是 socket。

- 字符驱动程序可能工作在字符流上，也可能不工作；关键是它们最直接地连接到用户和硬件。
- 块驱动程序通过文件系统、缓存和虚拟文件系统（VFS）连接到硬件和用户。
- 网络驱动程序通过各种协议栈连接到硬件和用户。

### 3.1. 设备类型

![](img/134c18b05ee9bbbe93ba3f433570ac1_34_0.png)

### 带有和控制器 API 的设备

- 有些设备在字符/块/网络划分之外还有另一个自由度（尽管在功能上它们可以用于这三种通用外设的任何一种）。
- SCSI（小型计算机系统互连）设备无论功能如何都共享一种底层协议。硬盘进入控制器硬件的驱动程序，该硬件可能运行许多设备。
- USB（通用串行总线）设备也共享一种底层协议。再次，各种外设的驱动程序绑定到控制器硬件。

![](img/134c18b05ee9bbbe93ba3f433570ac1_34_1.png)

### 用户空间设备

用户空间驱动程序（如集成到 [X.Org](http://www.x.org) 的视频驱动）位于用户空间但被赋予直接访问硬件。它们使用 `ierm()` 和 `iopl()` 函数来实现，我们将讨论读写端口。

## 3.2 机制 vs 策略

- 设备驱动程序应该在机制和策略之间保持清晰的区别。
- 通过机制，我们提供设备本身可以执行的能力。通过策略，我们控制这些能力的使用方式。
- 换句话说，某些决策取决于驱动程序（除非有硬件限制），例如：
    - 有多少进程同时使用设备。
    - I/O 是阻塞还是非阻塞，同步还是异步等。
    - 某些参数组合即使是不明智的也不会发生。

通常驱动程序可能会带有一个用户空间控制程序或守护进程，它具有控制设备的能力。

## 3.3 避免大包

- 有一种方法将驱动程序分为两个部分：
    - 二进制大包（binary blob），不提供源码。
    - 开源胶层，它调用二进制大包。

胶层为内核提供接口，而大包包含特定的硬件逻辑。

![](img/134c18b05ee9bbbe93ba3f433570ac1_35_0.png)

## 3.4 应用程序如何使用驱动程序

- 这种方法的著名例子是 Nvidia 显卡和网卡驱动。
- 使用这种方法内核会变得被污染，因为没有可用源码。
- 我们出于许多原因强烈反对这种方法，但两个原因就足够了：
    - 在内核中加载任意二进制代码是灾难的根源。
    - 制造商推广这种方法且不支持开源驱动程序的开发。

因此，我们不会教授这种方法，并且不鼓励使用此类驱动程序。

使用固件并不等于二进制大包。这些固件是本可以放在内存中的数据，但供应商发现让操作系统加载它更便宜。使用固件不会导致污染。

固件和二进制大包之间的界限很模糊，某些 Linux 发行版在发行需要固件的驱动程序时存在问题，或者不发行二进制固件本身。

## 第 3 章. 设备驱动程序

- 加载和卸载驱动程序会触发初始化和关闭回调函数。
- 内核的高层可能会调用用于电源管理等目的函数。
- 驱动程序可能会执行延迟任务，例如在经过特定时间后或某个条件变为真时。
- 如果驱动程序注册了处理特定的中断，则中断可能会驱动程序代码的异步执行。
- 因此，一旦设备驱动程序被加载，它的所有方法都会在内核中注册，并且它是事件驱动的；它响应用户应用程序的直接进入（这些可以是多个且同时发生的），并根据其他内核层的请求以及硬件触发的响应来执行代码。

## 3.5 追踪系统调用

- 让我们看看当应用程序尝试从一个已经打开的设备读取数据时，到底发生了什么。应用程序将通过以下方式打开并读取：

```
char *buf = malloc(nbytes);
fd = open("/dev/mydriver", O_RDWR);
read = read(fd, buf, nbytes);
```

（当然，我们只给出了代码片段，对错误检查等内容处理得很草率！）

- 我们重点关注 `read()` 调用，它比 `open()` 更容易追踪。`read()` 被 `bpf_libc` 拦截，它知道如何制作系统调用，内核通过位于 `/usr/src/linux/fs/read.c` 中的 `sys_read()` 函数进入。

```
3.1: 444 SYSCALLDEFINE(read, unsigned int, fd, char __user *, buf, size_t, count)
3.1: 445 {
3.1: 446 struct file *file;
3.1: 447 ssize_t ret = -ERADFS;
3.1: 448 int fput_needed;
3.1: 449

3.1: 450 file = fget_light(file, &fput_needed);
3.1: 451 if (file) {
3.1: 452 loff_t pos = file_pos_read(file);
3.1: 453 ret = vfs_read(file, buf, count, &pos);
3.1: 454 file_pos_write(file, pos);
3.1: 455 fput_light(file, fput_needed);
3.1: 456 }
3.1: 457

3.1: 458 return ret;
3.1: 459 }
```

`SYSCALL_DEFINE` 宏非常复杂，但它的作用是将函数名称更改为 `sys_read()`。

- 该函数将文件内核数据结构与 fd（用户应用程序的文件描述符）关联；内核在这些结构体内部工作，而不是文件描述符。然后它将工作传递给 `vfs_read()`：

```
3.1: 348 ssize_t vfs_read(struct file *file, char __user *buf, size_t count, loff_t *pos)
3.1: 349 {
3.1: 350 ssize_t ret;
```

## 3.6. 错误代码



```
3.1: 351    if (!(file->f_mode & FMODE_READ))
3.1: 352        return -EBADF;
3.1: 353

3.1: 354    if (!file->f_op && !(file->f_op->read && !file->f_op->aio_read)))
3.1: 355        return -EINVAL;
3.1: 356    if (unlikely(!access_ok(VERIFY_BUF, buf, count)))
3.1: 357        return -EFAULT;
3.1: 358

3.1: 359    ret = rv_verify_area(file, pos, count);
3.1: 360    if (ret > 0)
3.1: 361        count = ret;
3.1: 362            if (file->f_op->read)
3.1: 363            ret = file->f_op->read(file, buf, count, pos);
3.1: 364    else
3.1: 365        ret = do_sync_read(file, buf, count, pos);
3.1: 366    if (ret > 0) {
3.1: 367        fsnotify_access(file);
3.1: 368        add_rchar(current, ret);
3.1: 369    }
3.1: 370    }
3.1: 371    inc_sync(current);
3.1: 372

3.1: 373    return ret;
3.1: 374 }
3.1: 376 EXPORT_SYMBOL(vfs_read);
```

- 在检查文件是否已读取权限打开并进行其他安全检查后，它会查看嵌入在该结构中的 `file_operations` 结构体 (`file->f_op`)，如果它定义了读取方法 (`file->f_op->read`)，则直接将请求通过它传递。并将 `read` 的值返回回用户空间。

- 注意，该函数会增加或减少文件的引用计数；对于已进程使用的文件，这些函数的“轻量级”版本更快。

- 以上内容并非特定于设备驱动程序；如果打开的是普通文件，返回的将是相应的代码。

- 标准错误代码定义在 `linux/errno.h` 头文件中。第一组来自 `/usr/src/linux/include/asm-generic/errno-base.h`：

```
3.1: 4 #define EPERM /* 不允许操作 */
5 #define ENENT /* 无此类文件或目录 */
3.1: 6 #define ESRCH /* 无此类进程 */
7 #define EINTR /* 系统调用被中断 */
3.1: 8 #define EIO /* I/O 错误 */
3.1: 9 #define ENIOX /* 无此类设备或地址 */
3.1: 10 #define EBIG /* 参数过长 */
3.1: 11 #define ENOEM /* 格式错误 */
3.1: 12 #define EBADF /* 错误的文件 */
3.1: 13 #define ECHIL /* 无子进程 */
3.1: 14 #define EAGAIN /* 重试 */
3.1: 15 #define ENOMEM /* 内存不足 */
3.1: 16 #define EACCES /* 拒绝访问 */
3.1: 17 #define EFAULT /* 错误的地址 */
```

- 通常返回 `-ERROR`，而系统调用错误总是 `-1`，实际代码存储在用户空间的线程变量 `errno` 中。因此，在用户空间中典型的代码如下：

```
#include <errno.h>

if (ioctl(fd, arg) < 0){
    perror("MY_DRIVER_IO");
    return (errno);
}
```

- 通常可以通过检查 `NULL` 来检查具有指针返回值的函数状态。然而，内核允许返回值包含错误代码。处理这种情况的简单函数有：

```
void ERR_PTR(long error);
long IS_ERR(const void *ptr);
long PTR_ERR(const void *ptr);
```

- `PTR()` 编码错误，`IS_ERR()` 检查错误是否存在，`PTR_ERR()` 提取实际代码。

## 3.7 printk()

- `printk()` 与 `printf()` 相似，但有一些重要的区别。典型的调用可能是：

```
printk(KERN_INFO "Your device driver was opened with Major Number = %d\n", major_number);
```

- `printk()` 不支持浮点数。

- `printk()` 中的每条消息都有“日志级别”（如果没有明确给出，则应用默认级别）。这些级别定义在 `/usr/src/linux/include/printk.h` 中，如下：

```
3.1: 9 #define KERN_EMERG "<0>" /* 系统崩溃 */
3.1: 10 #define KERN_ALERT "<1>" /* 必须采取行动 */
3.1: 11 #define KERN_CRIT "<2>" /* 关键状况 */
3.1: 12 #define KERN_ERR "<3>" /* 错误状况 */
3.1: 13 #define KERN_WARNING "<4>" /* 警告状况 */
3.1: 14 #define KERN_NOTICE "<5>" /* 正常但重要的状况 */
3.1: 15 #define KERN_INFO "<6>" /* 信息 */
3.1: 16 #define KERN_DEBUG "<7>" /* 调试信息 */
```

- 日志级别（或优先级）会强制将一个非正式字符串添加到你的打印语句前面。

- 伪文件 `/proc/sys/kernel/printk` 列出了系统上设置的日志级别：在大多数系统中，你会得到数字 `6 4 1 7`，它们分别含义如下：

表 3.3 printk 日志级别

| 数值 | 含义 |
| :--- | :--- |
| console_loglevel | 优先级高于此的消息将打印到控制台。 |
| default_message_loglevel | 没有明确优先级的消息将按此优先级打印。 |
| minimum_console_level | console_loglevel 可以设置的最小（最高）值。 |
| default_console_loglevel | console_loglevel 的默认值。 |

- 注意，优先级越高意味着级别越低，进程可以动态更改 `console_loglevel`；在内核故障中，它会升到 15。

- 消息进入环形缓冲区，默认长度为 128 KB，可以在内核编译期间调整。可以使用 `dmesg` 工具查看消息；文件 `/var/log/dmesg` 包含了系统启动时的缓冲区内容。

- 在系统初始化期间，可以通过设置内核命令行参数 `log_len=n` 来覆盖缓冲区的默认大小，其中 `n` 必须是 2 的幂。

- 消息的位置取决于是否运行 `syslog` 或 `klogd` 以及它们如何配置。如果你无法简单地 `cat /proc/kmesg`，它们通常会进入 `/var/log/messages`（在某些最近的 Ubuntu 系统上进入 `/var/log/syslog`），但如果你正在运行 X，就无法看到它们。查看它们的好方法是打开终端并在并在输入 `tail /var/log/messages`。在 Gnome 桌面上，可以通过点击菜单中的系统->管理->系统日志或应用程序->系统工具->日志文件查看器访问消息。

- 内核日志的最终控制权在 `syslog` 和 `klogd` 守护进程手中。这可以控制行为的所有方面，包括默认级别和消息目的地，并根据源和严重程度引导。`syslog` 有手册页，也提供了内核内的 C 语言接口。

- 此功能可以通过设置参数 `printk.time=[1/Y/y] [0/N/n]` 在系统初始化时开启或关闭。

## 3.8 实验

### 实验 1：安装基础字符驱动

- 在本次练习中我们将编译、加载（并卸载）以及测试一个示例驱动（提供）。在随后的章节中，我们将详细讨论每一个步骤。

- 编译：首先，你必须确保已经安装了与正在运行的内核相同的源码。你可以通过以下操作验证这一点：

```bash
$ ls -l /lib/modules/$(uname -r)/build
```

确保它指向一个非空目录。如果不是，你的导师将帮助你修复，或者要求你重启到一个已安装相应文件的不同内核。



我们稍将深入讨论如何编写编译内核模块的 `Makefile`，但现在请使用 `genmake` 脚本；只需执行：

```bash
$ ../genmake
```

并使用以下命令编译内核：

```bash
$ make
```

使用与该位置内核模块相同的选项和标志来编译你的模块。

输出监控：如果你在终端或非图形模式下工作，你将在屏幕上看到模块的输出。否则，你必须关注 `/var/log/messages` 文件，系统日志引导内核打印消息。最佳方法是打开一个终端并输入：

```bash
$ tail /var/log/messages
```

加载与卸载：加载和卸载模块最简单的方法是：

```bash
$ /sbin/insmod lab_1_chrdrv.ko
$ /sbin/rmmod lab_1_chrdrv
```

尝试模块。如果你查看 `/proc/devices`，你应该看到驱动已注册；如果你查看 `/proc/modules`（或输入 `lsmod`），你应该看到你的模块已加载。

创建设备节点：在实际使用模块之前，你必须创建一个设备节点。使用 `mknod` 命令执行此操作：

```bash
$ mknod /dev/mydevice 700 0
```

注意设备节点的名称（`/dev/mydevice`）并不重要，内核通过主设备号（`700`）处理系统调用。从设备号（`0`）仅在驱动程序内部使用。

使用模块：你应该能够使用简单命令测试模块：

```bash
$ echo Some > /dev/mydevice
$ cat /dev/mydevice
$ dd if=/zero of=/dev/mydevice count=1
```

我们只粗略看了表面；稍后我们将考虑每个的细节。

# 第 4 章：模块：基础

我们将开始讨论 Linux 下的模块化技术。我们将定义什么是模块，并描述操作它们的工具。我们将讨论如何编译、加载和卸载模块，如何向它们传递参数，以及它们如何与热插交互。

| 节标题 | 页码 |
| :--- | :--- |
| 4.1 什么是模块？ | 29 |
| 4.2 简单示例 Hello World | 30 |
| 4.3 模块工具 | 31 |
| 4.4 传递参数 | 33 |
| 4.5 编译模块 | 34 |
| 4.6 模块与热插 | 38 |
| 4.7 实验 | 39 |

## 4.1 什么是模块？

内核模块是一个可以加载到（并卸载自）运行中内核的组件。它是一个可重定位的对象文件；即具有 `.ko` 扩展名。一旦加载，模块就拥有内核其他部分的能力。粗略来说，它将 Linux 内核作为一个共享库，通过符号和函数列表进行链接。模块依赖其他模块，因此加载和卸载的顺序可能需要小心进行。虽然许多模块是设备驱动程序，但许多与硬件无关。许多内核组件的设计使得将它们内置或链接为模块成为配置选项。大多数情况下，不需要修改源代码来包含此功能，它将始终被内置。这允许通过加载和卸载模块来测试新功能和增强，无需重新编译内核并重启，从而节省了大量时间。即使模块大量部署，Linux 内核在技术上仍然是一个单内核。这个术语与架构以及是否存在微内核有关。当模块加载时，它就变成了单内核的一部分。

### 简单示例 Hello World

这是一个简单模块的示例。它在加载和卸载时仅打印一条语句。

```c
#include <linux/module.h>
#include <linux/init.h>

static int __init my_init(void)
{
    printk(KERN_INFO "Hello: module loaded at 0x%p\n", my_init);
    return 0;
}

static void __exit my_exit(void)
{
    printk(KERN_INFO "Bye: module unloaded from 0x%p\n", my_exit);
}

module_init(my_init);
module_exit(my_exit);
```

所有模块都包含初始化和清理回调函数，通过 `module_init()` 和 `module_exit()` 宏指定。这些回调在模块加载和卸载时自动调用。没有清理函数的模块将无法卸载。此外，这些宏的使用简化了驱动程序（或其他代码）的编写，这些代码既可以作为模块使用，也可以直接进入内核。使用 `__init` 或 `__exit` 属性标记函数是稍后讨论的改进。

任何不开源许可证（通过 `MODULE_LICENSE()` 宏指定）的模块都将被标记为污染（tainted）：它将正常运行，但内核开发者对帮助任何调试将持敌态度。

```c
MODULE_AUTHOR("A GENIUS");
MODULE_LICENSE("GPL v2");
```

## 4.3 模块工具

你仍然会看到旧形式的模块：

```c
#include <linux/module.h>

int __init init_module(void)
{
    printk(KERN_INFO "Hello: init_module loaded at 0x%p\n", init_module);
    return 0;
}

void __exit cleanup_module(void)
{
    printk(KERN_INFO "Bye: cleanup_module loaded at 0x%p\n",
    cleanup_module);
}
```

虽然直接使用回调函数（`init_module()` 和 `cleanup_module()`）仍然有效，但在不采用 `module_init()` 和 `module_exit()` 宏的情况下使用它们已被废弃。

内核中的许多驱动程序将仅直接使用 `init_module()`、`cleanup_module()` 函数；这节省了几行代码，特别是对于始终作为模块加载的驱动程序。虽然这基本上是无害的，但这种形式最终将消失。

以下工具在用户空间运行，并是 `module-init-tools` 软件包的一部分。它们不直接属于内核源码。每个工具都有相当完整的手手册。

配置文件 `/etc/modprobe.conf`（以及 `/etc/modprobe.d` 中的任何文件）经常被模块工具查询。别名、传递给模块的选项、每当加载模块时处理的命令等都在其中指定。可能的命令有：

```
alias wildcard modulename
options modulename ...
install modulename ...
remove modulename ...
include filename
```

`install` 和 `remove` 命令可以替代默认的 `insmod` 和 `rmmod` 命令。

所有 Linux 发行版都规定了系统启动时加载特定模块的方法。然而，现代 Linux 发行版中的 `udev` 消除了这种需求。

在 Red Hat 上，`/etc/modules` 文件将从 `/etc/rc.d/sysinit` 执行。在任何文件中，都可以完全通过模块命令执行显式模块加载。

在 Debian 上，`/etc/modules` 中列出的任何模块都将被加载（该文件中只有模块名称，没有加载命令）；在 Gentoo 系统中，相同的角色由 `/etc/modules.autoload.d` 中的文件承担。

在 SUSE 上，需要修改的文件是 `/etc/sysconfig/kernel`。

## 4.4 传递参数

为了让 `depmod` 和 `modprobe` 找到模块，它们必须被指定在 `/lib/modules` 下的路径。

每当加载模块或运行 `depmod` 时，都会查询 `/etc/modprobe.conf` 文件。

当模块在外部目录构建并使用 `modules_install` 目标安装时，它们会被放置在 `extra` 子目录下。

### modprobe

`modprobe` 可以加载（或使用 `-r` 选项卸载）一组相互依赖的模块，并可以代替 `insmod`。

它也可以用于尝试一个模块列表，并在发现并成功加载第一个模块时立即退出。它也高度依赖于 `/etc/modprobe.conf`。

每当添加新模块或位置发生变化时，都应该运行 `depmod`。

`modutils` 软件包要求在使用 `insmod` 时使用 `.ko` 扩展，但 `modprobe` 和 `rmmod` 则不需要扩展名。

参数传递给 `modprobe` 的方式与传递给 `insmod` 的相同；例如，你可以执行：

```
/sbin/modprobe my_net_driver irq=10
```

## 4.4 传递参数

传递给模块的参数必须明确标记为此类，并进行类型检查。例如：

```
int irq = 12;
module_param(irq, int, 0);
```

有许多宏可以使用：



```c
#include <linux/moduleparam.h>
```

```c
module_param(name, type, perm);
module_param_named(name, value, type, perm);
module_param_array(name, value, type, num, perm);
module_param_string(name, string, len, perm);
```

- 在基础的 `module_param()` 中，`name` 是变量名，`type` 类型可以是 `byte`、`short`、`ushort`、`int`、`uint`、`long`、`char`、`pool`、`invol`。
- `perm` 参数是一个权限掩码，用于 `sysfs` 文件中对应的条目。如果你对 `sysfs` 不感兴趣，使用值 `0` 即可。通常可以使用值 `S_IRGO` (`0444`) 作为所有用户的读取权限。（请参见 `/usr/src/linux/include/linux/stat.h` 获取所有可能的值）。
在赋予权限后，通过写入与模块相关的 `sysfs` 文件系统条目，可以更改该参数，但请注意，只要 `sysfs` 值发生变化，模块就会收到通知！在这种情况下，权限可能是 `S_IRGO | S_IWUSR` (`0644`)。
- `module_param_named()` 变体使用的 `name` 是加载时用于描述变量的字符串，它不需要与 `value` 相同（`value` 是参数的实际值，而是模块中使用的参数名称）。注意，这些宏是内联的，因此参数必须出现在代码中。

# 第 4 章 模块 I：基础知识

- 在 `module_param_array()` 宏中，整数变量 `num` 给数组中的元素个数，可以像以下示例所示：
```
$ /bin/insmod my_project.ko irq=3,4,5
```
- `module_param_string()` 宏用于直接将字符串传递给 `char` 数组。
- 通过这种方法，可以构建自定义数据类型；它是可扩展的。更多细节请参阅 http://lwn.net/Articles/22197/
- 这种方法的特点是，它仍然可以使用驱动程序或其他内核功能工作，并且可以作为内置代码而非模块。2.6 之前的内核需要一套单独的函数（使用 `__setup()` 宏）来说在启动命令中向内核传递参数。这使得编写既可以作为模块也可以作为内置代码变得更加容易，且无需更改源代码。
- 将此类参数作为启动参数传递给内核的方法是在其名称前加上模块名和 `a_` 前缀；因此，内核启动命令行可能如下所示：
```
linux root=LABEL=/ ... my_project.irq=3,4,5 ...
```
所有已知参数的列表可以在 `/usr/src/linux/Documentation/kernelparameters.txt` 找到。
- 在 `/usr/src/linux/include/linux/module.h` 中定义了一些相关的宏，可以在模块中使用：
```
MODULE_AUTHOR(name);
MODULE_DESCRIPTION(desc);
MODULE_SUPPORTED_DEVICE(name);
MODULE_PARM_DESC(var,desc);
MODULE_FIRMWARE(filename);
MODULE_LICENSE(license);
MODULE_VERSION(version);
```
- 存储在那的信息通过运行 `modinfo` 命令生成。

## 4.5 编译模块

- 为了编译模块，你必须安装内核源码，或者至少安装所需的这些部分。这些部分始终可以在 `/lib/modules/$(uname -r)/build` 下找到。
- 编译模块的简单方法需要指定标志和选项，并指向正确的内核头文件。然而，这种方法早已被废弃，现在没有内核源码树已无法完全编译了。
- 现代模块的编译需要内核源码通过编译阶段，或者至少通过了 `make_prepare`，因为这是生成必要的配置和依赖信息所需的。此外，还需要包含内核配置的 `.config` 文件。
- 认可的方法仍然是在内核源码树之外工作，但进入其中进行编译。你至少需要一个包含以下内容的最小 `Makefile`：
```
obj
```
（注：后续文本由于重复且逻辑混乱，此处未予翻译）

## 4.5. 编译模块

`CLEANSTUFF="$U_X $T_X"`

```bash
# 也许可能没有内核模块

if [ "$GOJS" = "" ]; then
CLEANSTUFF="$CLEANSTUFF" Module.symvers modules.order
fi
```

```bash
# 获取所有目标 (ALL targets)

if [ "$U_X" = "" ]; then ALL=$ALL userprogs; fi
if [ "$T_X" = "" ]; then ALL=$ALL threadprogs; fi
if [ "$GOJS" = "" ]; then ALL=$ALL modules; fi
```

```bash
# 如果你好奇，可以输出一下 :>

echo K=$S_K OBJS=$GOJS $U_S=$U_X U_T=$T_S S_T=$T_X
```

```bash
################################################################################
# 准备工作完成，让我们最后构建 Makefilefile！

# 删除旧的 Makefile，构建一个新的

rm -f Makefile
```

```bash
echo #### 由 'genmake' 脚本自动生成的 Makefile #### >>Makefile
echo "### 版权所有 Jerry Coopersmith, coop@linuxfoundation.org 2/2003 - 1/2011" >> Makefile
echo "### 许可证: GPLv2 ####" >>Makefile
```

```bash
if [ "$K_S" = "" ]; then
echo -e "nobj-m +=$GOJS" >> Makefile
echo -e "export KROOT=$KROOT" >> Makefile
if [ "$ARCH" = "" ]; then
echo -e "export ARCH=$ARCH" >> Makefile
```

```bash
fi
echo -e "\nall:$ALL" >> Makefile
```

```bash
if [ "$K_S" = "" ]; then
echo "modules:" >> Makefile
echo -e "$(MAKE) -C$(KROOT) M=\$(PWD) modules" >> Makefile
echo "modules_install:" >> Makefile
echo -e "$(MAKE) -C$(KROOT) M=\$(PWD) modules_install" >> Makefile
echo "kernel_clean:" >> Makefile
echo -e "$(MAKE) -C$(KROOT) M=\$(PWD) clean" >> Makefile
```

```bash
fi
```

```bash
if [ "$U_X" = "" ]; then
echo -e "\nuserprogs:" >> Makefile
echo -e "\t$(MAKE) \\$CFLAGS_U_X\"" >> Makefile
if [ "$LDLIBS" = "" ]; then
echo -e "\tLDLIBS=\t$LDLIBS\" >> Makefile
```

```bash
if [ "$CPPFLAGS" = "" ]; then
echo -e "\tCPPFLAGS=\t$CPPFLAGS\"" >> Makefile
fi
```



```bash
echo - "$U_X" >> Makefile

fi

if [ "$T_X" != "" ]; then
    echo - "\nthreadprogs" >> Makefile
    echo - "\t\$(MAKE) \\" >> Makefile
    echo - "\ttCFLAGS\\$CFLAGS_T_X\\\" >> Makefile
    if [ "$LDLIBS" != "" ]; then
        echo - "\tLDLIBS\\$LDLIBS\\\" >> Makefile
    fi
    if [ "$CPPFLAGS" != "" ]; then
    echo - "\ttCPP\\$CPPFLAGS\\\" >> Makefile
    fi
    echo - "$T_X" >> Makefile

fi

if [ "$K_S" != "" ]; then
    echo - "inclean: kernel_clean" >> Makefile
else
    echo - "inclean:" >> Makefile
fi
echo - "\trm -rf $CLEANSTUFF" >> Makefile
```

## 4.6 模块与热插拔

- 当系统添加新设备或设备在启动时已存在时，系统会获得描述该设备的信息。这通常包括（但不限于）唯一的厂商 ID（vendor id）和产品 ID（product id）。
- 驱动程序可以指定它们能够处理哪些设备，当模块安装到系统上时，目录会被更新。然后，热插拔设施（用户空间）能够查询这些表，并在设备驱动程序不存在的情况下自动加载所需的设备驱动程序。
- 为了使此功能工作，驱动程序必须使用宏：

```c
MODULE_DEVICE_TABLE(type, name)
```

其中 `type` 指明驱动类型，`name` 指向一个结构体数组，其中的每个条目都指定一个设备。具体的结构取决于设备的类型。例如：

```c
static const struct pci_device_id sk_id_table[] = {
    { PCI_DEVICE(PCI_VENDOR_ID_3COM, PCI_DEVICE_ID_3C940) },
    { PCI_DEVICE(PCI_VENDOR_ID_3COM, PCI_DEVICE_ID_3C940B) },
    {
        PCI_VENDOR_ID_LINKSYS, 0x1032, PCI_ANY_ID, 0x0015 },
    { 0 }
};
MODULE_DEVICE_TABLE(pci, sk_id_table);
```

- 注意 `PCI_DEVICE()` 宏的使用；每个类型的子系统都有此类宏来辅助填充结构体表。

## 4. 实验

- 允许的类型及其对应的结构在 `/usr/src/linux/include/linux/mod_devicetable.h` 中划定，包括：`pci`, `ieee1394`, `usb`, `id`, `ccw`, `ap`, `css`, `acpi`, `pnp`, `pnp_card`, `servo`, `of_device_id`, `vio`, `input`, `eisa`, `parisc`, `sdb`, `virtio`, `i2c`, `spi`, `dmi`，以及 `platform`。这些每一个项都有与其关联的结构，例如 `usb_device_id`, `ieee1394_device_id` 等。
- 此外，当运行 `modules_install` 时，它会更新 `/lib/modules/$(uname -r)` 中的相应文件。
- 当新设备添加到系统时，会查询这些文件以查看它是否为已知设备，如果是且所需的驱动程序尚未加载，则会在相应的设备上运行 `modprobe`。

## 4.7 实验

### 实验 1：模块参数

- 编写一个在 `insmod` 加载时可以接收整数参数的模块。在未指定时，它应该有一个默认值。
- 加载并卸载它。在模块加载期间，查看其在 `/sys/module` 中的目录，并看看是否可以更改参数的值。

### 实验 2：初始化与清理

- 选取任何简单的模块，观察在没有同时具有初始化和清理函数的情况下会发生什么情况：
  - 只有初始化函数。
  - 只有清理函数。
  - 既没有初始化函数也没有清理函数。
  - 在这些情况下，尝试加载模块看会发生什么，如果成功，再尝试卸载它。

## 第 5 章：字符设备

我们将开始详细讨论构建设备驱动程序。我们将讨论设备节点、如何创建它们、访问它们以及将它们注册到内核。我们将详细描述重要的 `file_operations` 数据结构，并详细列出它指向的驱动程序入口项。我们还会考虑两个重要的数据结构：`file` 和 `inode` 结构。最后，我们将展示模块如何跟踪它们的使用情况，并讨论杂项驱动。

## 5.1 设备节点

- 字符设备和块设备有关联的文件系统项。这些节点可以被用户级程序用于与设备通信，其驱动程序可以管理多个设备节点。设备节点示例：

```
lrwx-xr-x 1 root root    3 Dec 28 06:30 cdrom -> sr0
lrwx-xr-x 1 root root    3 Dec 28 06:30 dvdr -> sr0
crw-rw---- 1 root root    3 Dec 28 06:30 dv
crw-rw---- 1 root root    10 Dec 28 06:30 bmem
crw-rw---- 1 root root      1 Dec 28 00:30 kmem
brw-rw---- 1 root disk      7 Dec 28 10:58 loop0
brw-rw---- 1 root disk      7 Dec 28 06:30 loop1
crw-rw---- 1 root root      6 Dec 28 00:30 pl0
brw-rw---- 1 root disk      8, 0 Dec 28 06:30 sda0
brw-rw---- 1 root disk      8, 1 Dec 28 06:30 sda1
brw-rw---- 1 root disk     18, 0 Dec 28 06:30 sdb2
brw-rw----+ 1 root cdrom     11, 0 Dec 28 06:30 sr0
```

## 5.2 主设备/次设备号

- 也可以使用内联便利函数：

```
unsigned iminor(struct inode inode); /* = MINOR(inode->i_rdev) */
unsigned imajor(struct inode inode); /* = MAJOR(inode->i_rdev) */
```

当需要处理 `inode` 结构体时可以使用。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_58_0.png)

- 在 2.4 内核中，设备号被封装在 `kdev_t` 类型中，该类型仅限于 16 个有效位，即使分为主号和次号，每个号的范围也被限制在 0 - 255 之间。
- 在 2.4 内核中，一旦驱动程序注册了主号，其他驱动程序就无法注册相同的主号，且所有的次号都属于该驱动程序。
- 在 2.6 内核中，驱动程序注册的是一个次号范围，该范围可以小于所有可用次号。事实上，两个同时加载的驱动程序只要次号范围不同，就可以拥有相同的主号。
- 与设备预先关联的主/次设备号列表可以在 `/usr/src/linux/Documentation/devices.txt` 中找到。（注意：主号 42、120-127 和 240-254 预留供本地和实验使用。）分配的主号的符号名称可以在 `/usr/src/linux/include/linux/major.h` 中找到。现在禁止进一步请求设备号预留，因为更现代的方法使用了动态分配。
- 请注意，设备号在用户空间中同样存在。事实上，如 `mknod()` 和 `stat()` 等 Posix 系统调用带有 `dev_t` 类型的参数，它们也使用了该类型的结构体。例如：

```
$ /boot/64/vmlinuz-2.6.35-rc3
```

```
File: /boot/64/vmlinuz-2.6.35-rc3
Size: 370593 Blocks: 7272 IO Block: 1024 regular file
Device: 802h/2050d Inode: 1856 Links: 1
Access: (0664/-rw-r--)Uid: (0/root) Gid: (0/root)
Access: 2010-06-13 08:21:00.000000000 -0500
Modify: 2010-06-13 08:21:00.000000000 -0500
Change: 2010-06-13 08:21:00.000000000 -0500
```

显示该文件位于主号为 8、次号为 2 的磁盘分区（`/dev/sda2`）上，其列出的值为 802h（十六进制）和 2050d（十进制）。



## 5.3 预留主/次设备号

- 向系统添加新驱动程序（即注册它）并为其分配主号，通常在设备的初始化例程期间进行。对于字符驱动程序，调用：

```c
#include <linux/fs.h>

int register_chdev_region(dev_t first, unsigned int count, char *name);
```

其中 `first` 是请求范围内的第一个设备，范围由 `count` 个连续的数字组成；通常 `first` 的次号部分为 0，但并非强制要求。

- `name` 是设备名称，它将在查看 `/proc/devices` 时显示。注意，这与你的驱动程序将使用的 `/dev` 节点名称不是同一个。（内核根据主/次号的组合决定调用哪个驱动程序，而不是根据名称。）

- 返回值为 0 表示成功；负值表示失败，且请求的设备号范围将不可用。注意，仍需运行 `mknod` 来创建相应的设备节点。

- 当不再需要设备号时，撤销注册时与设备号的关联是非常重要的。这通常在设备清理函数中通过以下操作完成：

注意这不会移除节点本身。

- 如果你未能成功注销设备，下次执行 `/proc/devices` 时将获得段错误（`segmentation fault`）。在不重启系统的情况下，要从此类错误中恢复是非常困难的（尽管并非不可能）。

### 2.4 内核的注册方式

![](img/134c18b05ee9bbbe93ba3f4335720ac1_60_0.png)

- 在 2.4 内核中，只有 8 位的主/次号可用，注册和注销的函数为：

```c
#include <linux/fs.h>

int register_chrdev(unsigned major, const char *name,
                     const struct file_operations *fops);
int unregister_chrdev(unsigned major, const char *name);
```

- 动态分配是通过指定主号为 0 实现的，返回值从 254 开始递减，直到找到一个未使用的号。（当请求动态分配时，成功返回 0。）

- 我们稍后将讨论 `file_operations` 结构体指针。

- 只有一个驱动程序可以使用给定的主号；在 2.6 内核中，要求主/次号是唯一的。

- 该接口比新的接口有限，用于某些旧驱动程序。然而，任何新驱动程序都应该使用更现代的方法。

### 主号的动态分配

- 选择唯一的主号可能是困难的：通过以下函数实现设备号的动态分配：

```c
#include <linux/fs.h>

int alloc_chrdev_region(dev_t *first, unsigned int count,
                     char *name);
```

其中 `first` 地址将由函数填充。参数 `first` 显然是请求的起始次号（通常为 0）。设备号的注销与此相同。

（注：原文后续存在大量重复内容，此处已根据文档工程师规范进行去重处理。）

# 第 5 章 字符设备

- 驱动程序在调用以下函数时将生效：

```c
cdev_add(mycdev, first, count);
```

在驱动程序准备好处理任何出现的情况之前，不应调用此函数。其相反函数是：

```c
cdev_del(mycdev)
```

在调用此函数后，设备将从系统中移除，且之后绝不应再次访问 `cdev` 结构。

## 5.6 udev 和 HAL

- 随着 Linux 的演进，管理设备节点的方法变得笨拙且困难。在大多数使用 2.4 内核系列的安装中，`/dev` 及其子目录下的设备节点数量达到了 15,000 到 20,000 个。对于在大多数安装中永远不会用到的各种设备，其节点仍会默认被创建，因为发行版无法无法确定切切需要哪种管理。

- 许多开发者和系统管理员将列表精简到实际需要的程度，特别是在嵌入式配置中，但这本质上是一项手动工作且可能出错的任务。

- 注意，设备节点不是普通文件，不会占用文件系统的大量空间；巨大的目录会减慢对设备节点的访问，尤其是在第一次使用时。此外，可用主号和次号的耗尽需要一种更现代、动态的方法来创建和管理设备节点。

- 理想情况下，人们希望通过名称注册设备。然而，主号和次号无法完全消除，因为 Posix 要求它们存在。

- `udev` 方法根据需要动态创建设备节点。不需要维护将要使用的设备节点计数：`udev` 代表 user（用户），创建、删除和修改节点的大部分工作是在用户态完成的。

- `udev` 处理设备节点的动态生成，但它不处理设备的发现或管理。硬件抽象层（简称 HAL）是 freedescript 的项目（http://www.freedesktop.org/hal）。

- HAL 使用 HAL 进程提供的 D-Bus 基础设施。它维护一个所有连接硬件的数据库，并与热插设施紧密耦合。该命令将导出 HAL 当前数据库中拥有的所有信息。系统上有多个配置文件（位于 `/usr/share/hal` 和 `/etc/hal`），用于控制行为和设置异常。

- 当设备通过热插子系统从系统中添加或删除时，`udev` 根据事件通知操作创建和移除具有正确名称、主号和次号等的设备节点；这些信息通过检查已注册在 sysfs 伪文件系统（挂载于 `/sys`）中的信息以及一组配置文件来收集。

## 5.7 FILE_OPERATIONS 结构

- 主配置文件是 `/etc/udev.conf`。它包含了如设备节点放置位置、默认权限和所有权等信息。默认的设备命名规则位于 `/etc/udev/rules.d`。通过阅读 `udev` 的手册页（`man` page），可以获得许多关于如何设置各种情况的具体信息。

- 在驱动程序内部动态创建和删除设备节点，是通过使用 `/src/linux/include/device.h` 中定义的函数实现的：

```c
#include <linux/device.h>

struct class *class_create(struct module *owner, const char *name);
struct device *device_create(struct class *cls, struct device *parent, dev_t dev,
    void *data, const char *fmt, ...);
void device_destroy(struct class *cls, dev_t dev);
void class_destroy(struct class *cls);
```

通常，父节点为 NULL 意味着类是在层次结构的顶层创建的。以下代码片段用于展示这些函数用法：

```c
static class *foo_class;

// 在 init 函数中创建节点
foo_class = class_create(THIS_MODULE, "my_class");
device_create(foo_class, NULL, "%s", "mycdrv", 1);

// 在 exit 函数中移除节点
device_destroy(foo_class);
class_destroy(foo_class);
```

- 必须小心在设备进入之前完成所有必要的操作以使设备可用，避免竞态条件。

- `file_operations` 结构定义在 `/src/linux/include/fs.h` 中，如下：



```c
struct file_operations {
    struct module *owner;
    loff_t (*seek) (struct file *f, loff_t int);
    size_t (*read) (struct file *f, const char *user, size_t, loff_t *);
    size_t (*write) (struct file *f, const char *user, size_t, loff_t *);
    size_t (*aio_read) (struct inode *kiocb, struct iovec *, unsigned long, loff_t *);
    size_t (*aio_write) (struct inode *kiocb, struct iovec *, unsigned long, loff_t *);
    int (*pread) (struct file *f, void *filp, struct_dir_t *);
    unsigned int (*poll) (struct file *f, struct poll_table *, unsigned long);
    int (*locked_ioctl) (struct file *f, unsigned int, unsigned long);
    int (*copyst_ioctl) (struct file *f, unsigned int, unsigned long);
    int (*mmap) (struct file *f, struct vm_area_struct *);
    int (*open) (struct inode *inode, struct file *f);
    int (*flush) (struct inode *inode, struct int *f_owner_id);
    int (*release) (struct inode *inode, struct file *f);
    int (*fsync) (struct file *f, loff_t, loff_t, int datascync);
    int (*aio_fsync) (struct kiocb *, int datasync);
    int (*fasync) (int, struct file *, int);
    int (*lock) (struct file *, struct file_lock *);
    size_t (*sendpage) (struct file *, struct page *, int, size_t, loff_t *, int);
    unsigned long (*get_unsapped_area) (struct file *, unsigned long, unsigned long, unsigned long);
    int (*check_flags)(int);
    int (*flock) (struct file *, int);
    size_t (*splice_write) (struct pipe_inode_info *, struct file *, size_t *);
    int (*fallocate) (struct file *, int mode, loff_t offset, loff_t len);
};
```

该结构用于字符驱动以外的其他用途（例如文件系统），因此某些条目将在此处不使用。这对于稍后讨论的 `file` 和 `inode` 结构也是如此。

- `file_operations fops` 使用如下代码初始化：

```c
struct file_operations fops = {
    count = THIS_MODULE,
    open = my_open,
    lease = my_close,
    read = my_read,
    write = my_write,
    unlocked_ioctl = my_unlocked_ioctl,
};
```

- 根据 `C99` 标准，字段的初始化顺序是无关的，任何未指定的元素均为 `NULL`。

- 这些操作通过 `cdev_init()` 函数与设备关联，该函数将 `file_operations` 结构的指针放置在父 `cdev` 结构中。每当对驱动程序拥有的设备节点执行相应的系统调用时，工作将传递给驱动程序；例如，对设备节点调用 `open` 会调用示例中的 `my_open()` 方法。

- 如果 `file_operations` 结构中未提供方法，当通过系统调用该方法时可能会出现两种情况：

- 方法将失败：例如 `lseek()`。

- 将调用通用默认方法：例如 `llseek()`。有时这意味着该方法总是成功：例如 `open()` 和 `release()`。

### 5.8 驱动程序入口点

- `struct *owner`;

该结构体中唯一不是方法的字段。指向拥有该结构体的模块，用于引用计数和避免竞态条件（例如在驱动程序正在使用时移除模块）。通常设置为 `THIS_MODULE`。

- `loff_t (*llseek)(struct file *file, char __loff_t offset, int whence);`

更改文件中的读写写位置，并返回新位置。注意在 32 位架构上，`loff_t` 是 64 位的。

如果有人想在设备上禁止寻址（例如在某些设备上），可以如下所示在文件结构体中 much `FMODE_LSEEK` 位（可能在 `open()` 方法期间进行）：

```c
file->f_mode = file->f_mode & ~FMODE_LSEEK;
```

- `ssize_t (*read)(struct file *file, char __user *buffer, size_t size, loff_t *offset);`

从设备读取数据，返回读取的字节数。错误返回值为负值；零表示设备末尾并非错误。如果数据尚未就绪且进程设置了非阻塞标志，你也可以选择阻塞。

- 一个简单的 `read()` 入口点 (`struct file *file, char __user *buf, size_t lbuf, loff_t *ppos`)

```c
int bytes = lbuf - copy_to_user(buf, kbuf + *ppos, lbuf);
*ppos += bytes;
printk(KERN_INFO "An reading function, bytes=%zd, pos=%ld\n", bytes, (long)*ppos);
return bytes;
```

在这种情况下，`read` 仅仅是将数据从内核空间（`kbuf`）拷贝到用户空间（`buf`）。但你不能使用 `memcpy()` 来执行此操作，因为在内核空间中解引用指针是不恰当的；所引用的地址可能并未指向当前的页内存，可能是因为尚未分配，或者它已经被交换出内存。

- 必须使用 `copy_to_user()` 和 `copy_from_user()` 函数（取决于方向），这些函数将处理这些问题。（我们稍后会看到更高级的技术来避免额外的拷贝，包括内存映射、原始 I/O 等。）

- 内核缓冲区将动态分配，内核每个任务的栈空间非常有限。这可以通过以下实现：

```c
#include <linux/slab.h>
char *kbuf = kmalloc(kbuf_size, GFP_KERNEL);

free(kbuf);
```

其中限制为 1024 页（在 x86 上为 4 MB）。

- 如果使用 `GFP_KERNEL` 标志，内存分配将阻塞直到资源可用；如果使用 `GFP_ATOMIC`，则请求是非阻塞的。我们将在稍后详细讨论内存分配。

- 设备中的位置通过通过修改指向当前值的 `*ppos` 值来更新。返回值是成功读取的字节数；在一种情况下，返回值为正值仍表示成功。

- `ssize_t (*write) (struct file *filp, char __user *buff, size_t size, off_t *offset);`

将数据写入设备，返回写入的字节数。错误返回负值；零可能表示设备末尾且不是错误。如果设备尚未就绪且进程未设置非阻塞标志，你也可以选择阻塞。

对于不直接使用用户空间指针的考虑也同样适用。在这里应该使用

```c
int nbytes = copy_from_user(kbuf + *ppos, buf, lbuf); // 修正后的逻辑
```

出于相同的原因。

- `int (*readdir) (struct file *filp, void *, filldir_t filldir)`

对于设备节点应为 `NULL`；仅用于目录，并由文件系统驱动程序使用，这些程序使用相同的 `file_operations` 结构。



- `unsigned int (*poll) (struct file *filp, struct poll_table_struct *ptab)`

检查设备是否可读、可写或处于某种特殊状态。用户空间通过 `poll()` 和 `select()` 调用访问。返回描述设备状态的位掩码。
- `int (*ioctl) (struct inode *inode, struct file *filp, unsigned int, unsigned long)`

使用设备特定命令的接口。注意，某些 `ioctl` 命令并不是设备特定的，它们会被内核拦截，而不会引用你的入口点。
- `long (*locked_ioctl) (struct file *filp, unsigned int, unsigned long)`

与普通的 `ioctl(1)` 入口不同，内核会在调用前获取锁，并在调用后释放。新代码应该使用此入口点；旧的入口将被忽略。
- `int (*mmap) (struct file *filp, struct vm_area_struct *vm)`

请求将设备内存映射到进程内存。如果你不实现此项，内核将返回 `-ODEV`。
- `int (*open) (struct inode *inode, struct file *filp)`

打开设备。如果你不实现此项，内核将返回 `-ODEV`。
- 一个简单的 `read()` 入口点 (`struct file *file`, `char __user *buf`, `size_t lbuf`, `loff_t *ppos`)

（注：原文此处存在逻辑重复描述，此处已根据逻辑结构对齐翻译）
*注：由于原文中存在大量重复片段，以下为对应的翻译内容：*
- 内核缓冲区将动态分配，内核每个任务的栈空间非常有限。这可以通过以下实现：

```c
#include <linux/slab.h>
char *kbuf = kmalloc(kbuf_size, GFP_KERNEL);

free(kbuf);
```

其中限制为 1024 页（在 x86 上为 4 MB）。
- 如果使用 `GFP_KERNEL` 标志，内存分配将阻塞直到资源可用；如果使用 `GFP_ATOMIC`，则请求是非阻塞的。我们将在稍后详细讨论内存分配。
- 设备中的位置通过修改指向当前值的 `*ppos` 值来更新。返回值是成功读取的字节数；在一种情况下，返回值为正值仍表示成功。
- `ssize_t (*write) (struct file *filp, char __user *buff, size_t size, off_t *offset);`

将数据写入设备，返回写入的字节数。错误返回负值；零可能表示设备末尾且不是错误。如果设备尚未就绪且进程未设置非阻塞标志，你也可以选择阻塞。
对于不直接使用用户空间指针的考虑也同样适用。在这里应该使用

```c
int nbytes = copy_from_user(kbuf + *ppos, buf, lbuf); // 修正后的逻辑
```

出于相同的原因。
- 对于设备节点应为 `NULL`；仅用于目录，并由文件系统驱动程序使用，这些程序使用相同的 `file_operations` 结构。
- 检查设备是否可读、可写或处于某种特殊状态。用户空间通过 `poll()` 和 `select()` 调用访问。返回描述设备状态的位掩码。
- 使用设备特定命令的接口。注意，某些 `ioctl` 命令并不是设备特定的，它们会被内核拦截，而不会引用你的入口点。
- 与普通的 `ioctl(1)` 入口不同，内核会在调用前获取锁，并在调用后释放。新代码应该使用此入口点；旧的入口将被忽略。
- 请求将设备内存映射到进程内存。如果你不实现此项，内核将返回 `-ODEV`。
- `int (*open) (struct inode *inode, struct file *filp)`

打开设备。如果你不实现此项，内核将返回 `-ODEV`。
（注：由于提供的原文后半部分存在大量重复的句子片段，翻译时已遵循“不要重复输出原文”的原则，对核心功能点进行了整合翻译。）

## 5.10. 杂项字符驱动

表 5.6: inode 结构元素

| 字段 | 含义 |
|---|--|
| `dev_t i_rdev` | 包含实际设备号，可以从中提取主设备号和从设备号。 |
| `dev_t i_cdev` | 指向基础字符驱动结构。 |

## 5.10 杂项字符驱动
- 对于大多数简单的字符驱动程序，利用 misc（杂项）字符驱动 API 更有意义，该 API 使用的代码行更少，并且会自动与 udev 系统接口，从而动态创建设备节点。这使得不再需要自己发明新的类（class）。
- 所有 misc 驱动程序共享相同的主设备号 (`10`)，可以请求特定的从设备号，也可以动态生成一个设备号。注册和注销函数以及相关数据结构定义在 `/usr/src/include/linux/linux/miscdevice.h` 中。

```c
#include <linux/miscdevice.h>

int misc_register(struct miscdevice *misc);
int misc_deregister(struct miscdevice *misc);

struct miscdevice {
	int minor;
	const char *name;
	const struct file_operations *fops;
	struct list_head list;
	 device *parent;
	 device *this_device;
	const char *modename;
	mode_t mode;
};
```

- 在设备加载时填充 `miscdevice` 结构并调用注册函数，在设备卸载时调用注销函数。这两个函数在成功时返回 0，失败时返回错误码。
- 通常只有 `miscdevice` 结构中的三个字段会被填充：

```c
static struct miscdevice my_misc_device = {
	.minor = MISC_DYNAMIC_MINOR,
	.name = MYDEV_NAME,
	.fops = kmycydrv_fops,
};
```

其中通过使用 `MISC_DYNAMIC_MINOR`，请求内核为我们分配一个从设备号，`name` 字段提供设备节点名称（将出现在 `/dev` 目录下），而 `fops` 是我们常用的函数表。
- 这比编写一个完整的字符驱动要容易得多。

## 模块使用计数

5.11 内核需要跟踪用户空间进程引用模块的次数（这与其他模块使用该模块的次数无关）。引用计数不为零的模块是无法移除的。
- 曾经，模块被要求自己完成大部分的记账工作：每当进程使用模块时增加使用计数，在完成后减少该计数。在不产生错误和竞态条件的情况下，实现这一过程是非常困难的。
- 作为一种改进，模块的使用情况现在由内核的高层进行跟踪，而不是手动维护。为了使这项工作生效，我们需要在所考虑模块类型的相应数据结构中设置 `owner` 字段。例如，对于字符设备驱动程序或文件系统驱动程序，这就是 `file_operations` 结构。可以通过以下设置：

```c
static struct file_operations fops = {
    owner = THIS_MODULE,
    my_open,
}
```

现在，内核将自动处理记账工作。（注意：对于内置内核代码，`THIS_MODULE` 被设置为 `NULL`）
- 其他包含回调函数表或入口结构的示例包括 `block_device_operations` 和 `fs_ops`。
- 如果需要手动修改模块的使用计数（以防止在模块在使用时被卸载），可以使用以下函数：

```c
int try_module_get(struct module *module);
void module_put(struct module *module);
```

- 像 `try_module_get(THIS_MODULE)` 这样的调用如果模块正在卸载过程中，可能会失败，此时返回 0；否则返回 1。如果在配置期间未开启允许卸载模块的内核选项，这些函数将不起作用。
- 引用计数嵌入在模块数据结构中，可以通过函数获取：

```c
unsigned int module_refcount (struct module *mod);
```

并在类似下面的地方调用：

```c
printk(KERN_INFO "Reference count = %d\n", module_refcount(THIS_MODULE));
```

## 5.12 实验

### 实验 1：改进基础字符设备
- 从 `sample driver.c` 开始，扩展它以：
- 跟踪自加载以来被打开的次数，并在每次打开设备时打印计数器。
- 在打开设备时打印主设备号和从设备号。

## 5.12. 实验



- 为了练习你的驱动程序，编写一个程序，使用标准的 Unix I/O 函数（`open()`, `write()`, `close()`）从节点进行读取（和/或写入）。

使用 `insmod` 加载模块后，使用此程序访问节点。

- 使用 `lsmod`（等于输入 `cat /proc/modules`）跟踪模块的使用情况。

### 实验 2：每个设备的私有数据

- 修改之前的驱动，使打开设备时分配自己的数据区域，并在释放时释放。数据在多次打开之间不会持久。

### 实验 3：寻求与设备末尾

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

- 实现 `seek()` 入口点。

### 实验 4：动态节点创建 (I)

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

### 实验 5：动态节点创建 (II)

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

### 实验 6：使用 misc API

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

- 适配之前的驱动程序，使 `read` 和 `write` 入目能够识别末尾。

## 6.2 用户态 vs 内 内态

执行模式

- 用户模式 (`user mode`)

  应用程序和守护进程以有限权限执行。（x86上的 Ring 3）。即使应用程序具有 root 权限，也是如此。

- 内核模式 (`kernel mode`)

  内核对硬件和内存具有直接的特权访问权限。（x86上的 Ring 0）。驱动程序（和模块）具有内核权限。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_76_0.png)

- 执行通过系统调用（使用同步中断或异常实现）和硬件中断（或异步中断）从用户态（空间）转移到内核态（空间）。

- 模式是多处理器系统中每个 CPU 的状态，而不是内核本身的状态，因为每个处理器可能处于不同的执行模式。

> 在运行虚拟化内核时，虚拟层监控程序（hypervisor）运行在 Ring 0，而客机（客户端）内核根据虚拟化类型运行在 Ring 0 或 Ring 1。如果是 Ring 1，则需要一定的技巧和/或模拟来完成这一操作。

## 6.3 调度算法与任务结构

- 调度无疑内核执行的最重要工作。

- 任务在内核态和用户态（在用户态下权限较低）之间不断切换。调度并不直接控制这些模式切换，但它必须处理不同任务之间的上下文切换。

- 在 Linux 下，任务本身不能抢占当前正在运行的任务并接管；它必须等待自己的时间片轮。然而，调度器可以抢占一个任务以允许另一个任务运行。

- 任务会一直运行，直到发生以下情况之一：

  - 它们需要等待某些系统事件完成（例如读取文件）。

  - 它们的时间片时长已耗尽。

  - 调度器被调用并发现了一个更值得运行的任务。

此外，2.6 内核具有抢占式内核的编译选项；配置后，每个单处理器系统都可以表现得像多处理器系统一样，或者在内核执行时降低延迟并抢占代码。因此，所有可以通过这种方式被抢占的代码必须是完全重入的（fully-entrant）。

任务的 `task_struct` 是 Linux 下的关键数据结构，包含了关于任务的所有内核信息以及所有用于进出切换的内容。它有时被称为进程描述符（process descriptor）。它定义在 `/usr/src/linux/include/sched.h` 中。

当前任务（在当前 CPU 上）的结构可以通过 `current` 宏引用，例如 `current->tg` 是进程 ID，`current->pid` 是当前任务 ID。（这些可能不同；对于多线程任务，每个线程共享相同的进程 ID，但具有唯一的任务（线程） ID。）该数据结构包含有关信号处理、进程使用的内存区域、父任务和子任务等信息。

在内核调度器中，运行在用户态或内核态的进程（更准确说是任务或线程）是通过指向 `task_struct` 的指针标识的，而不是通过 pid。人们始终可以通过 pid 获取指针：

```
struct task_struct *task = pid_find(vpid(pid), PIDTYPE_PID);
```

（注意，在多线程进程中，此宏将定位主线程，其进程标识符和线程标识符相匹配。）

通常不需要从模块获取此类信息，而且竞态条件可能会成为问题，因为 pid 在进程生命周期内可能会发生变化。

虽然 `schedule()` 函数可能会被直接调用（从内核代码而非用户代码调用），但它更有可能通过中断到达，例如：当当前任务进入睡眠并被放入等待队列时；当发生上下文切换时；当任务从内核返回用户态时；或者在处理中断后。

当调度器运行哪个任务应该占用 CPU 时，如果它与当前任务不同，就会发生上下文切换。它尝试将任务保持在同一个 CPU 上（以减少抖动）。当选择一个新任务运行时，当前任务的状态会被保存在它的 `task_struct` 中，切换入新任务使其成为当前任务。

在 2.6.23 内核之前，调度器被称为 O(1) 调度器；做出调度决策的时间与运行任务的数量无关。它的设计特别有利于 SMP 系统和具有大量任务的系统进行扩展。每个 CPU 维护有独立的队列；这些队列按优先级排序，而不需要触碰搜索任务来找到合适的运行任务，决策可以通过快速的位图查询来完成。

2.6.23 内核将 O(1) 调度器替换为一种全新的算法，该算法驱动了 CFS（完全公平调度器）调度。

完全公平的时间是任务等待运行的时间除以运行任务的数量（带有某些不同的优先级）。此时间会与下一个接收到的实际任务进行比较。

CFS 还包含分级调度器模块，每个模块都可以被依次调用。

## 6.4 进程上下文

- 当内核执行代码时，它拥有完全的内核权限，并且显然处于内核态。然而，它可以处于不同的上下文中。

- 在进程文中，内核代表某个进程执行代码。最可能是由于系统调用导致了进入内核。示例包括：

  - 系统调用导致了进入内核。

  - 应用程序（或守护进程）发出了 `read()` 或 `write()` 请求。

  - 用户进程通过系统调用来检查或设置其优先级，或通过 `getpid()` 获取其 ID。

- 在中断文中，内核不代表任何用户进程工作。示例包括：

  - 内核正在处理中断。

  - 内核正在执行在特定时间或为了方便而调度的任务。

  - 内核正在初始化、关闭或运行调度器。

- 内核上下文比用户进程上下文轻量；内核线程之间的切换比进程上下文要容易且快速得多。

- Linux 还部署了所谓的内核进程，它们与用户进程非常相似，但由内核直接运行。

- 这种伪进程用于管理线程，例如维护缓冲区和页缓存的线程，它们必须同步磁盘文件内容与内存。其他示例是 `ksoftirqd` 和 `kjournald`；执行 `ps aux` 并查看名称带有方括号的进程。

- 这些进程像普通进程一样执行，并允许睡眠。然而，它们没有真正的进程上下文，因此无法与用户态进行数据传输。

## 6.5 实验

实验 1：使用 `strace`。

`strace` 用于跟踪系统调用和信号。在最简单的情况下，你可以执行：

- `$ strace [options] command [arguments]`

- 每个系统调用、其参数和返回值都会被打印出来。根据帮助页（man page）所述：

- “参数以符号形式带有热情地打印。”

事实确实如此。有很多可用选项；请阅读 man 页！

- 例如，尝试运行

```bash
$ strace -lRF / 2>&1 | less
```

你需要复杂的重定向，因为 `strace` 会将其输出到标准错误（stderr），除非你使用 `-o` 选项将其重定向到文件。

- 在此程序运行时（在 `less` 下暂停状态），你可以通过检查 `/proc` 文件系统来查看有关 `ls` 进程的更多细节。执行：

```bash
$ ps aux | grep ls
```

以找到与进程相关的进程 ID（PID）。然后你可以查看伪文件：

`/proc/<pid>/fd/*` 映射到底层文件（或管道）等，

以查看文件描述符是如何使用的。

## 第7章

## 中断与异常

我们将详细查看 Linux 内核如何处理同步中断（异常）和异步中断。我们将考虑消息信号中断（MSI）。我们将展示如何启用/禁用中断。我们将讨论在中断上下文中可以做和不能做什么。我们将考虑与中断相关的主要数据结构，并展示如何安装中断处理程序或服务例程。最后，我们将详细讨论在这些函数的上半部分和下半部分中必须执行哪些操作。

7 7.1 什么是中断和异常？ .......................................................................... 65



# 7.2 异常

## 什么是中断和异常？

- 中断会改变（中断）处理器所遵循的指令序列。它总是由来自处理器内部或外部的电信号引起的。
- 当中断到达时，内核必须挂起当前执行的线程，通过调用分配给特定中断的一个或多个服务例程（ISR）或处理程序来处理它，然后返回到被挂起的线程，或处理另一个中断。
- 在 Linux 下，中断永远不应该丢失；服务例程可能会根据各种锁定机制和优先级被延迟，但最终会被调用的。然而，中断是不排队的；给定类型的类型只会被处理一次，尽管在处理期间如果到达了另一个相同类型的中断，它也将按顺序被处理。
- 中断有两种截然不同的类型：
  - 同步中断（通常称为异常）由 CPU 生成。
  - 异步中断（通常直接称为中断）由其他硬件设备产生，并通常通过 `APIC`（高级可编程中断控制器）馈送。
- 异常可能由运行时错误（如除以零）或特殊条件（如页错误）引起。它们也由某些指令引起，例如系统调用请求 CPU 进入内核模式以服务设备驱动程序的指令。它们可能发生在进程上下文内部或外部。它们通常会向一个或多个进程发送信号。
- 中断通常源于相对随机事件，如鼠标点击、键盘按键、网卡到达的数据包等，或更规则的事件，如定时器中断。

### 7.2 异常

- 异常分为两类：
  - 处理器检测的异常（Faults）在执行期间产生。
  - 陷阱（Traps）：寄存器包含故障指令的地址。
  - 终止异常（Aborts）：寄存器可能包含异常的值。
  - 程序化异常（Programmed exceptions）：由内核触发的。

#### 表 7.1：32位 x86 异常

| # | 异常/ 服务例程 | 类型 | 信号 | 含义 |
|---|---|---|---|---|
| 0 | 除法错误 `divide_error()` | fault | SIGFPE | 除零。 |
| 1 | 调试 `debug()` | trap | SIGTRAP | 用于调试。 |
| 2 | NMI `nmi()` | None | 非屏蔽中断。 |
| 3 | 断点 `int3()` | trap | SIGTRAP | 调试器插入的断点。 |
| 4 | 溢出 `overflow()` | trap | SIGSEV | 指令执行并溢出。 |
| 5 | 边界检查 `bounds()` | fault | SIGSEV | 执行超出有效边界。 |
| 6 | 无效操作码 `invalid_op()` | fault | SIGILL | 坏的操作码（CPU 指令）。 |
| 7 | 设备不可用 `device_not_available()` | fault | SIGSEV | 浮点或 MMX 指令。 |
| 8 | 双重故障 `double_fault()` | abort | | 在尝试处理之前的异常时检测到异常。 |
| 9 | 协处理器段溢出 `coprocessor_segment_overrun()` | abort | SIGFPE | 数学协处理器的问题，如 x87 。 |
| 10 | 无效 TSS `invalid_tss()` | fault | SIGSEV | 切换到具有无效 TSS 的进程。 |
| 11 | 段不存在 `segment_not_present()` | fault | SIGBUS | 引用内存中不存在的段。 |
| 12 | 栈异常 `stack_segment()` | fault | SIGBUS | 尝试超过栈段长度，或段不在内存中。 |
| 13 | 通用保护 `general_protection()` | fault | SIGSEV | 违反了保护模式。 |
| 14 | 页错误 `page_fault()` | fault | SIGSEV | 页不在内存、页表条目或其他分页问题。 |
| 15 | 预留 | None | None | |
| 16 | 浮点错误 `co_processor_error()` | fault | SIGFPE | 集成 FPU 错误状态，如溢出或除零。 |
| 17 | 对齐检查 `alignment_check()` | fault | SIGSEV | 操作数未对齐，例如位于 4 倍倍地址上的长整数。 |
| 18 | 机器检查 `machine_check()` | abort | None | 严重的硬件问题，通常在 CPU 或内存中。 |
| 19 | SIMD 错误 `simd_coprocessor_error()` | fault | SIGSEV | 执行 SIMD（单指令多数据）数学指令的问题。 |

# 7.3 异步中断

有两种类型的异步中断：

- 可屏蔽中断（Maskable interrupts）发送到微处理器的 `INTR` 引脚。它们可以通过在 `eflags` 寄存器中设置的适当标志位来禁用。
- 不可屏蔽中断（Nonmaskable interrupts）发送到微处理器的 `NMI` 引脚。它们无法被禁用，且当它们发生时，通常意味着严重的硬件故障。
- 任何发出中断的设备都有一条 `IRQ`（中断与请求）线，该线连接到 `APIC`（高级可编程中断控制器）。
- 在 x86 架构上，每个 CPU 内部集成了一个本地 `APIC`（Local APIC）。此外，通过了一个通过系统外设总线使用的 `I/O APIC`。
- 在 ARM 上，有 `IRQ` 和 `FIQ`（快速 IRQ 线）。`IRQ` 通常由中断控制器进行扩展，例如：`GIC`（通用中断控制器）`http://intercenter.arm.com/infocenter.com/index.jsp?topic=com.arm.doc.ii0048b/index.html`。
- 在 ARM 处理器（例如 `Cortex-A8`）上，异常存在一套固定的优先级系统（参见 `http://infocenter.arm.com/help/topic/com.arm.doc.dd0344k/Beigeaj.html`）。
- `I/O APIC` 根据其维护的重定向表将中断路由到各个 `APIC`。
- 本地 `APIC` 持续监控它负责的 `IRQ` 线，当它发现信号被拉高时：
  - 涉及哪个 `IRQ`？
  - 将其存储在它拥有的 `I/O` 端口中，可以通过数据总线进行读取。
  - 通过向其 `INTR` 引脚发送信号来发出中断。
- 当 CPU 通过回写控制器 `I/O` 端口确认 `IRQ` 时，它会清除 `INTR` 引脚。
- 返回等待新中断的到达。

# 7.4 MSI

# 7.5 启用/禁用中断

# 7.6 中断期间不能做的事

# 7.7 IRQ 数据结构

# 7.8 安装中断处理程序

# 7.9 实验



可以通过命令 `/proc/interrupts` 获取当前安装的中断处理程序列表，其输出类似于：

| CPU0 | CPU1 | CPU2 | CPU3 | IO-APIC-edge | timer |
|---|---|---|---|---|---|
| 0 | 129 | 2 | 1 | IO-APIC-edge | 8042 |
| 1 | 722 | 12 | 40 | IO-APIC-edge | rtc0 |
| 8 | 0 | 0 | 0 | IO-APIC-edge | | | |
| 9 | 0 | 0 | 0 | IO-APIC-fastie | acpi |
| 16 | 1546 | 948 | 90 | IO-APIC-fastie | uhci_cdub:usb3, patra_marnell, nvidia eth0, uhci_cdub:usb1, uhci_cdub:usb5, uhci_cdub:usb8 |
| 18 | 1628 | 10 | 14 | 1814 | IO-APIC-fastie | | |
| 19 | 2 | 1 | 0 | IO-APIC-fastie | uhci_cdub:7, uhci1394 |
| 21 | 0 | 0 | 0 | IO-APIC-fastie | uhci_cdub:4 |
| 22 | 534 | 151 | 4510 | IO-APIC-fastie | HBA_Int |
| 23 | 44436 | 37879 | 4654 | 4122 | IO-APIC-fastie | ehci_cdub:usb2, uhci_cdub:6 |
| 28 | 0 | 0 | 1 | PCI-MSI-edge | eth1 | | |

## MSI

| 29: | 17358 2567 18150 17191 | MSI-edge ahci |
| NMI: | 0 0 0 0 | 不可屏蔽中断 |
| LOC: | 255559 16184 147985 131046 | 本地定时器中断 |
| SPU: | 0 0 0 0 | 伪假中断 |
| RES: | 1849 1183 1520 1158 | 重新调度中断 |
| CAL: | 340 475 475 450 | 函数调用中断 |
| TLB: | 1777 2734 1720 2689 | TLB 关闭 |
| TRM: | 0 0 0 0 | 温度事件中断 |
| THR: | 0 0 0 0 | 阈值 APIC 中断 |
| ERR: | 0 | |
| MIS: | 0 | |

- 注意，这里的数字是中断线触发的次数。列表中仅列出当前安装的处理程序。如果某个处理程序被注销（例如卸载模块），并且另一个处理程序被重新注册，该数字将在过程中被清零。
- 你还会注意到两种类型的中断：
  - 电平触发中断（Level-triggered interrupts）响应具有特定值（通常是电压）的电信号。
  - 边触发中断（Edge-triggered interrupts）响应变化（可以是上升或下降）。原则上讲，如果只注意到了变化，可能会错过电平触发中断。
- 在 SMP 系统上，中断可以在任何 CPU 上服务。此外，在 ARM 上有 IRQ 和 FIQ（快速 IRQ 线）。IRQ 通常由中断控制器扩展：例如 GIC（通用中断控制器）http://intercenter.arm.com/infocenter.com/index.jsp?topic=com.arm.doc.ii0048b/index.html。
- 在 ARM 处理器（例如 Cortex-A8）上，异常有一套固定的优先级系统（参见 http://infocenter.arm.com/help/topic/com.arm.doc.dd0344k/Beigeaj.html）。
- I/O APIC 根据其维护的重定向表将中断路由到各个 APIC。
- 本地 APIC 持续监控它负责的 IRQ 线，当它发现信号被拉高时：
- 涉及哪个 IRQ？
- 将其存储在它拥有的 I/O 端口中，可以通过数据总线进行读取。
- 通过向其 INTR 引脚发送信号来发出中断。
- 当 CPU 通过回写控制器 I/O端口确认 IRQ 时，它会清除 INTR 引脚。
- 返回等待新中断的到达。

## 7.6 在中断期间你不能做的事

```c
unsigned long flags;
spinlock_t my_lock;
spinlock_init(&my_lock);

spin_lock_irqsave(&my_lock,flags);
.... 关键代码
spin_unlock_irqrestore(&my_lock,flags);
```

- 你在使用这些函数时必须非常小心，因为可能会导致系统瘫痪。

### 在中断期间不能做的事

- 中断不是运行在进程上下文中。因此，你不能引用 `current` 来访问 `task_struct` 的字段，因为这些字段在最坏的情况下也是未定义的。通常，`current` 指向进入中断服务程序时正在运行的任意进程，而该进程与 IRQ 没有任何先验联系。
- 任何会导致阻塞的操作都会导致内核冻结，至少被阻塞的处理器是这样。特别是，你不能直接或间接地调用 `schedule()` 或使用任何睡眠函数。间接使用的例子是，如果你尝试使用带有 `GFP_KERNEL` 标志分配内存，如果内存当前不可用，该操作会阻塞，因此你必须使用 `GFP_ATOMIC`。
- 你不能获取互斥锁（mutex）。
- 你不能对信号量（semaphore）执行 `down()`，因为它在等待资源时可能会阻塞。但是，你可以执行 `up()` 或任何类型的 `wake_up()`。
- 你不能使用 `request_module()` 请求加载模块。
- 你不能从进程地址空间向或从其传输任何数据；即不能使用 `get_user()`、`put_user()`、`copy_to_user()`、`copy_from_user()`。只有这些函数有睡眠的可能性，因为没有真实的用户上下文，你无法通过这些函数从用户空间传输数据。

## 7.7 IRQ 数据结构

- 涉及 IRQ 的基本数据结构定义 `/usr/src/linux/include/linux/irqdesc.h` 和 `/usr/src/linux/include/linux/interrupt.h` 中。
- 对于每个 IRQ，都有一个定义如下的描述符：

| 行 | 行 | 定义 |
| :--- | :--- | :--- |
| 3.1 | 39 struct irq_desc | |
| 3.1 | 40 struct irq_data | irq_data; |
| 3.1 | 41 struct timer_rand_state | timer_rand_state; |
| 3.1 | 42 unsigned int *kstat_irqs; |



| 3.1 | 43 `irq_handler_t` `handle_irq`; |

| 3.1 | 44 `#if defined(CONFIG_IRQ_PREFLOW_FAST)` | |

| 3.1 | 45 `irq_preflow_handler_t` | `preflow_handler`; |

| 3.1 | 47 `struct irqaction` | /* IRQ 列表 */ |

| 3.1 | 48 `unsigned int` | `status_use_accessors`; |

| 3.1 | 49 `unsigned int` | `core_internal_state__do_not_mess_with_it`; /* 嵌套中断禁用 */ |

| 3.1 | 50 `unsigned int` | `depth`; |

| 3.1 | 51 `unsigned int` | `wake_depth`; /* 嵌套唤醒开启 * | |

| 3.1 | 52 `unsigned int` | `irq_count`; /* 检测损坏的 IRQ * | |

| 31.1: 53 `unsigned long` `last_unhandled`; |

| 31.1: 54 `unsigned int` `irqs_unhandled`; |

| 31.1: 55 `raw_spinlock_t` `lock`; |

| 31.1: 56 `#ifdef CONFIG_SMP` | |

| 31.1: 57 `const struct cpumask *affinity_hint`; |

| 31.1: 58 `struct_irq_affinity_notify *affinity_notify`; |

| 31.1: 59 `#ifdef CONFIG_GENERIC_PENDING_IRQ` | |

| 31.1: 60 `cpumask_var_t` `pending_mask`; |

| 31.1: 61 `#endif` |

| 31.1: 62 `#endif` |

| 31.1: 63 `unsigned long` `threads_oneshot`; |

| 31.1: 64 `atomic_t` `threads_active`; |

| 31.1: 65 `wait_queue_head_t` `wait_for_threads`; |

| 31.1: 66 `#ifdef CONFIG_PROFS` | |

| `struct proc_dir_entry *dir`; |

| 31.1: 68 `#endif` | |

| 31.1: 69 `struct module *owner`; |

| 31.1: 70 `const char *name`; |

| 31.1: 71 `} ______cacheline_internode_aligned_in_smp;` |

- `status` 可以取以下值之一：

| 值 | 含义 |
| :--- | :--- |
| `IRQ_PROGRESS` | 此 IRQ 句处理程序当前正在执行中。 |
| `IRQ_DISABLED` | IRQ 线已禁用。 |
| `IRQ_PENDING` | 已发生一个 IRQ 并已确认，但尚未被处理。 |
| `IRQ_REPLAY` | IRQ 线已禁用，但该线上之前发生过的情况尚未在该 IRQ 线上被确认。 |
| `IRQ_AUTODETECT` / `IRQ_WAITING` | 内核正对此 IRQ 线进行自动检测，且未检测到中断。 |
| `IRQ_LEVEL` | IRQ 线被触发。 |
| `IRQ_MASKED` | IRQ 线被屏蔽，不应再次被看到。 |
| `IRQ_PER_CPU` | IRQ 是每个 CPU 私有的。 |

- `action` 列出了与 IRQ 关联的程序；元素指向列表中的第一个 `irqaction` 结构。我们将详细描述该结构。

- 如果 IRQ 线是启用的，则 `depth` 为 0。正值表示它被禁用的次数。每次 `disable_irq()` 都会增加计数器，每次 `each_irq()` 都会递减它，直到达到 0，此时会启用它。因此，此计数器被用作信号量。

- `lock` 用于防止竞态条件。

- `irqaction` 结构如下：

```c
struct irqaction {
    irq_handler_t handler;
    unsigned long flags;
```
```c
struct irqaction {
    // ...
109 void *dev_id;
110 struct irqaction *next;
111 int irq;
112 irq_handler_t fn;
113 task_struct *thread;
114 unsigned long flags;
115 unsigned long mask;
116 const char *name;
117 struct proc_dir_entry *dir;
118 ____cacheline_internode_aligned_in_smp;
};
```

- `status` 可以取以下值之一：

- `action` 列出了与 IRQ 关联的程序；元素指向列表中的第一个 `irqaction` 结构。我们将详细描述该结构。

- 如果 IRQ 线是启用的，则 `depth` 为 0。正值表示它被禁用的次数。每次 `disable_irq()` 都会增加计数器，每次 `each_irq()` 都会递减它，直到达到 0，此时会启用它。因此，此计数器被用作信号量。

- `lock` 用于防止竞态条件。

- `irqaction` 结构如下：

- 指向向相同 IRQ 的下一个 `irqaction` 结构。

- `dev_id` 是 `irqaction`结构中用于共享 IRQ 线的唯一标识符。它通常被用作传递给句处理程序的私有数据区域。如果 IRQ 不共享，可以使用 `NULL`。

# 第 7 章 中断与异常

![](img/134c18b05ee9bb93ba4335720ac1_89.png)

- `IR_DISABLED` 标志已弃很久，从内核 2.6.35 开始它不再有任何影响。

## 7.8 安装中断处理程序

- 通常设备驱动程序不会直接访问我们描述的数据结构。相反，它们使用以下函数来安装和卸载中断处理程序：

```c
#include <linux/interrupt.h>

request_irq(unsigned int irq,
irqreturn_t (*handler)(unsigned int irq, void *dev_id),
unsigned long flags,
const char *device,
void *dev_id);
synchronize_irq(unsigned int irq);
free_irq(unsigned int irq, void *dev_id);
```

- `irq` 是中断号。

- `handler()` 是要安装的处理程序。

- `flags` 是之前描述的相同位掩码；例如 `IRQF_DISABLED` 等。请求已注册为非共享的 IRQ 会产生冗长但无害的调试信息。

- `device` 与 `irqaction` 结构中的 `name` 字段相同；它设置了出现在 `/proc/interrupts` 中的标识符：

- `dev_id` 是 `irqaction`结构中用于共享 IRQ 线的唯一标识符。它通常被用作传递给句处理程序的私有数据区域。

## 7.8. 安装中断处理程序

![](img/134c18b05ee9bbbe93ba3f4335720ac1_90_0.png)

- 2.6.19 之前的内核包含第三个参数，该是一个类型为 `pt_regs` 的数据结构，它保存了中断发生前处理器上下文快照。它主要用于调试，以及在处理中断后恢复寄存器状态。该结构的精确定义依赖于 CPU；`/usr/src/linux/x86/include/asm/ptrace.h`

- `pt_regs` 参数在 2.6.19 内核中被移除，因为它在驱动程序中很少使用，移除它可以节省栈空间，并在一定程度上提升了性能。

- 如果需要访问此结构，可以使用内联函数 `struct pt_regs *regs = get_irq_regs();`。

`request_irq()` 可以在设备初始化时或第一次使用设备时（`open()`）进行调用。在引入 `udev` 之前，最好在第一次使用设备时在 `open()` 中进行。然而，有了 `udev` 后设备往往不会预加载。此函数应该在向设备发送指令之前调用，以确保中断的产生。

`free_irq()` 可以在清理或 `release()`（关闭）期间调用。此函数应该只在设备被指示不再中断 CPU 之后调用。

在调用 `free_irq()` 之前，应该调用 `synchronize_irq()`，它确保在发出请求之前，该特定 IRQ 的所有处理程序都已完成。应该注意此函数不会阻塞。

中断处理程序返回一个类型为 `irqreturn_t` 的值。三个可能的返回值和一个方便宏如下：

表 7.6: IRQ 处理程序返回值

| 返回值 | 含义 |
|---|---|



| `n IRQ_NONE` | 处理程序未识别出该事件；即，它是由于其他共享该的设备引起的，或者是一个伪中断。 |

| `IRQ_HANDLED` | 处理程序识别了该事件并执行了所有需要的操作。 |

| `IRQ_WAKE_THREAD` | 用于线程中断处理程序，稍后将讨论。 |

| `IRQ_RETVAL(x)` | 如果参数非零，则求值为 `IRQ_HANDLED`；否则为 `IRQ_NONE`。 |

- 如果没有注册的处理程序为给定的 IRQ 返回 `IRQ_HANDLED`，则假设它是伪中断并打印警告信息。注意，中断并没有被消耗；对于给定的 IRQ 线，所有注册的处理程序仍然会被调用，其中一个或多个处理程序声称已处理该事件。

## 7.9 实验

### 实验 1：共享中断

- 编写一个与你的网卡共享 IRQ 的模块。你可以通过浏览或 ping 来产生一些网络中断。（如果你在网络驱动程序上遇到问题，尝试使用鼠标中断。）
- 在模块加载时检查 `/proc/interrupts`。
- 让模块跟踪中断处理程序被调用的次数。

### 实验 2：共享所有中断

- 扩展之前的解决方案，构建一个字符驱动程序，该驱动程序与已安装的处理程序共享所有可能的中断。
- 你需要考虑的最高中断号取决于你的内核和平台；查看 `/proc/interrupts` 以确定必要的内容。
- 在调用 `free_irq()` 时要格外小心，如果你不小心，很容易冻结你的系统。
- 字符驱动程序可以非常简单；例如，如果没有指定 `open()` 和 `release()` 方法，则默认成功。
- 对设备进行 `read()` 操作应该返回一个关于每个 IRQ 处理的中断总数的简要报告。
- 为了实现这一点，你还需要编写一个简短的应用程序来检索并打印数据。（不要忘记在运行应用程序之前创建设备节点。）

## 第 8 章

## 模块 II：导出、许可与动态加载

![](img/134c18b05ee9bbbe93ba3f4335720ac1_92_0.png)

我们将看到符号是如何从内核导出到模块，以及从一个模块到另一个模块的。我们将讨论模块许可的某些方面。我们将考虑模块的按需加载以及动态加载和卸载。我们将看到为了让驱动程序成为内核的一部分而不是模块，需要哪些更改。

| 8.1 | 导出符号 | . . . . . . . . . . . . | 77 |
| 8.2 | 模块许可 | . . . . . . . . . . . . . . . | 78 |
| 8.3 | 模块的自动加载/卸载 | . . . | 80 |
| 8.4 | 内置驱动程序 | . . . . . . . . . . . . . . . | 81 |
| 8.5 | 实验 | . . . . . . . . . . . . . . . . . . . . | 83 |

## 8.1 导出符号

- 为了让内置内核代码提供的符号（即变量或函数）可供模块使用，它必须正确地导出它。如果一个模块拥有某些将被加载在其之后的的模块所使用的符号，

# 第 8 章 模块 II：导出、许可与动态加载

- 为了让内置内核代码提供的符号（即变量或函数）可供模块使用，它必须正确地导出它。如果一个模块拥有某些将被加载在其之后的的模块所使用的符号，

```c
struct pt_regs *regs = get_irq_regs();
```

## 8.2 许可

- 内核理解以下许可：

| 许可 | 含义 | 是否污染 (Tainted)? |
|---|---|---|
| GPL | 否 |
| GPL v2 | 否 |
| GPL and additional | 否 |
| Dual/GPL | 否 |
| Dual/GPL | 否 |
| Dual MIT/GPL | 否 |
| Proprietary (专有) | 是 |

# 第8章 模块II：导出、许可与动态加载

## 8.3 模块的自动加载/卸载

`request_module()`:

- 模块可以通过以下方式显式地请求加载一个或多个其他模块：

```c
#include <linux/kmod.h>

int request_module (const char *name, ...)
```

该模块名称将与任何其他所需的模块一起（使用 `modprobe`）动态加载。该名称可以是模块的实际名称，也可以 `/etc/modprobe.conf` 中指定的别名。当前进程将休眠直到模块加载完成。

- `request_module()` 额外的可变参数表示一个类似于 `printf()` 方式的格式化列表。例如，你可以这样做：

`request_module("my-device-xd", device_number);` 动态加载只能在进程上下发生；即，如果你在中断处理程序中调用 `request_module()`，将得到错误。它必须从驱动程序的入口函数中调用。

- `request_module()` 的返回值并不好用；成功仅意味着请求已妥善执行，并不意味着加载成功了。如果你翻阅源码，你会看到它请求执行 `modprobe()` 并对其报告错误状态。在这里，内核实际上进行了一次到用户空间的跳转。

- 注意，请求模块不能调用目标模块中的函数；如果是这样，它根本无法加载（由于存在未解析的引用）。因此，在某种意义上，此函数是一种预取。

### 需需加载（Demand Loading）：

- 模块可能需要按栈加载其他模块。这可以通过以下方式实现：
- 使用 `insmod` 按正确的顺序加载它们。
- 使用 `modprobe` 按栈加载它们。（注意，必须先运行 `depmod`，且按需加载的模块必须位于 `depmod` 已知的位置）。

### 动态加载（Dynamic Loading）：

- 通常人们希望当应用程序访问相应的设备节点时，自动加载模块。例如，每当应用程序对 `/dev/dsp` 进行读写时，都加载音频驱动。
- 这可以通过在 `/etc/modprobe.conf` 中插入如下形式的行来实现：

```
alias block-major-254-* mybdrd
alias block-major-254-* mybdrd
```

这里我们对从设备号使用了通配符。（注意，2.4 内核只接受主设备号，该格式仍然有效。）

## 8.4 内置驱动程序（BUILT-IN DRIVERS）

- 这假设 `mydrv.co` 可以在 `depmod` 搜索的路径中找到，并且你已经使用主设备号访问了设备节点。注意，设备节点的名称是由应用程序调用的，不需要与模块名称匹配。你也可以将此类名称作为 `request_module()` 的参数。
- 注意，`udev` 的使用减少对这种技术的需求。然而，底层方法非常不同。`udev` 在发现设备时加载驱动模块；而使用这些别名允许在第一次使用设备时加载它们，这应该发生得较晚，至少对于硬件驱动来说如此。
- 设备驱动和其他设施可以作为内核的整体加载，也可以作为模块加载，许多内核组件都具备以这两种方式使用的能力。包含在内核需要重新编译整个内核；而模块化则不需要。
- 代码只需要最少的更改；大多数情况下不需要更改。然而，内核配置文件必须处理所有三种可能性：内置的、模块的或两者都不是。
- 可以将数据和函数标记为在内核初始化后移除。这是通过关键字 `__init` 和 `__initdata` 实现的。例如，如果你有：

```c
static some_data __initdata = 1;
void __initsomefunc(void) { ... }
```

数据和代码将进入内核的一个特殊初始化区域并在执行后被丢弃。必须小心代码或数据在初始化后不再被引用。你可能在系统启动期间看到此类消息：

> [0.841689] Freeing unused memory: 424k

- `__exit` 宏在可执行文件中期望所有此类标记的内容。
- 如果你使用 `module_init()` 宏，你应该能够避免在代码中使用任何 `#ifdef` 语句，因为内置驱动程序永远不会加载。
- 此外，内核按照以下配方安排 `module__init()` 函数的加载，使得默认优先级为 6。这使得在 `.o` 文件中创建一个名为 `.initcall` 的段。这将包含一个指向所有函数的指针数组。因此，所有的 `.o` 文件链接在一起；可以为初始化调用分配优先级，这在 `/usr/src/linux/include/init.h` 中设置：

| 行 | 代码 |
| :--- | :--- |
| 3.1: 194 | `__pure_initcall(fn)` `define_initcall("0",0)` |
| 3.1: 195 |  |
| 3.1: 196 | `__core_initcall(fn)` `define_initcall("1",1)` |
| 3.1: 197 | `__core_initcall_sync(fn)` `define_initcall("is",is)` |



| 3.1: 198 | `__post_core_initcall(fn)` `define_initcall("2",2)` |
| 3.1: 199 | `__core_initcall_sync(fn)` `define_initcall("2s",2s)` |
| 3.1: 200 | `__arch_initcall(fn)` `define_initcall("3",3)` |
| 3.1: 201 | `__arch_initcall_sync(fn)` `define_initcall("3s",3s)` |
| 3.1: 202 | `__subsys_initcall(fn)` `define_initcall("4",4)` |
| 3.1: 203 | `__subsys_initcall_sync(fn)` `define_initcall("4s",4s)` |
| 3.1: 204 | `__fs_initcall(fn)` `define_initcall("5",5)` |
| 3.1: 205 | `__fs_initcall_sync(fn)` `define_initcall("5s",5s)` |
| 3.1: 206 | `__roots_initcall(fn)` `define_initcall("roots",roots)` |
| 3.1: 207 | `__device_initcall(fn)` `define_initcall("6",6)` |
| 3.1: 208 | `__device_initcall_sync(fn)` `define_initcall("6s",6s)` |
| 3.1: 209 | `__late_initcall(fn)` `define_initcall("7",7)` |
| 3.1: 210 | `__late_initcall_sync(fn)` `define_initcall("7s",7s)` |
| 3.1: 211 | `__initcall(fn)` `device_initcall(fn)` |
| 3.1: 212 | `__exitcall(fn)` `static __exitcall##fn __exit_call = fn` |
| 3.1: 213 | `__console_initcall(fn)` `static __initcall##fn used __section(.console_initcall.init) = fn` |
| 3.1: 214 | `__security_initcall(fn)` `static __initcall##fn used __section(.security_initcall.init) = fn` |

注意在 2.6.19 内核中引入了诸如 6 等额外的子级别。

- `/linux/init/main.c` 中调用所有函数的例程是：

```c
static void __init initcalls(void) {
  initcall_t *fn;
  for (fn = __early_initcall_end; fn < __initcall_end; fn++)
    do_one_initcall(*fn);
}
```

- 注意，除了使用 `module_init()` 宏外，每个驱动程序在定义初始化函数体时仍然应该使用 `__init` 属性。这会将代码放在 `.text` 段，该段是会被回收的段。

## 8.5 实验

### 实验 1：栈式模块

- 编写一对模块，其中一个使用另一个模块中定义的函数。
- 尝试使用 `insmod` 和 `modprobe` 加载和卸载它们。

### 实验 2：重复符号

- 将你的第一个模块复制为另一个，编译并尝试同时加载它们：

```bash
$ cp lab_module1.c lab_module1A.c
... 修改 Makefile 并编译
$ /sbin/insmod lab_module1.ko
$ /sbin/insmod lab_module1A.ko
```

- 这成功了吗？
- 使用 `make modules_install` 安装模块。
- 通过分析生成的 `modules.dep` 文件查看 `depmod` 是如何处理它的。

### 实验 3：动态模块加载

- 取上一个实验中的基础字符驱动程序并进行修改以使用动态加载：
- 构建一个简单的第二个模块并在字符驱动程序的 `open()` 入口点动态加载它。（确保请求的文件名与你的文件名相同）。
- 在你的字符驱动程序中添加一个小函数并让第二个模块引用它。
- 确保将你的模块放在 `modprobe` 可以找到的地方（使用目标 `modules_install` 安装将处理这一点）。
- 你可以使用 `cat` 或字符驱动实验中的主程序来测试你的模块。
- 如果尝试多次加载会发生什么？

### 实验 4：驱动程序的按需加载

- 使你的字符驱动程序在设备设备时加载，即当你执行如下操作时：

```bash
$ cat file > /dev/mycdrv
```

让驱动加载。
- 根据需要调整 `/etc/modprobe.conf` 并使用 `make modules_install` 将模块放在正确的位置。

# 第 9 章

# 调试技术

![](img/134c18b05ee9bbbe93ba3f4335720ac1_100_0.png)

我们将考虑用于调试设备驱动程序和内核的各种技术。我们将讨论 oops 消息，以及包括 kprobes 在内的调试器的直接使用。我们还会考虑 debugfs 的使用。

| 9.1 oops 消息 | 85 |
| 9.2 内核调试器 | 88 |
| 9.3 debugfs | 89 |
| 9.4 kprobes 和 jprobes | 91 |
| 9.5 实验 | 94 |

## 9.1 oops 消息

- `oops` 消息表示在内核模式下发生了故障。根据产生 `oops` 的故障性质，该故障可能是致命的、严重的、或无关紧要的。
- 如果 `oops` 发生在进程上下文中（`process context`），内核将尝试撤回当前任务，并可能会杀死它。如果它发生在中断上下文中（`interrupt context`），内核无法这样做并将导致崩溃，这发生在空闲任务（`pid=0`）或 `init`（`pid=1`）时也是如此。
- 提供的信息包含了崩溃时处理器寄存器的转储（`dump`）以及指示失败位置的调用栈跟踪（`call trace`）。有时，这就是人们所需要的全部内容。
- 要充分利用 `oops` 消息，以及几乎所有的内核调试技术，要求人们至少对汇编语言有一定的熟悉程度。关于如何处理 `oops` 的示例，请参阅 http://lkml.org/lkml/2008/1/7/406。
- 为了故意触发 `oops`，可以执行：

```c
if (disgusting_condition)
    BUG();
```

或者

```c
BUG_ON(disgusting_condition);
```

- 还可以通过打印此类消息来诱发系统崩溃，例如：

```c
if (fatal_condition)
    panic ("I'm giving up because of task %d\n", current->pid);
```

- 网站 http://www.kernelops.org 维护了一个当前 `oops` 的数据库，并帮助开发者成功成功了调试。遗憾的是，这种数据收集似乎在 2.6.34 内核之后停止了。
- 这是一个简单的微模块（`oops.c`），它包含一个可以触发 `oops` 消息的空指针解引用错误：

```c
#include <linux/module.h>
#include <linux/init.h>

static int __init_my_init(void)
{
    int *i;
    i = 0;
    printk(KERN_INFO "Hello: init_module loaded at address 0x%p\n",
    init_module);
    printk(KERN_INFO "i=%d\n", i);
    return 0;
}

static void __exit_my_exit(void)
{
    printk(KERN_INFO "Hello: cleanup_module loaded at address 0x%p\n",
    cleanup_module);
}

module_init(my_init);
module_exit(my_exit);

MODULE_LICENSE("GPL v2");
```

- 我们可以用 `objdump` 对代码进行反汇编。执行

```bash
$ objdump -d oopsit.ko
```

得到：



`oopsit.ko: file format elf64-x86-64`

Disassembly of section `.exit.text`:

```
| 0000000000000000 <cleanup_module>: |
| 0: | 55 push %rbp |
| 1: | 48 c7 06 00 00 00 00 mov $0,%rsi |
```

```
8:      48 89 e5      mov %rsp,%rbp
b:     48 c7 c7 00 00 00 00  mov $0x0,%di
12:     31 c0               xor %eax,%eax
14:     e8 00 00 00      call <cleanup_module+0x19>
19:     c9               leaq
1a:     c3               ret
```

### `.init.text` 的反汇编：

```
0000000000000000 <init_module>:
0:55                 push %rbp
1:     48 c7 c6 00 00 00 00  mov $0x0,%rsi
8:      48 89 e5           mov %rsp,%rbp
b:     48 c7 c7 00 00 00 00  mov $0x0,%di
12:     31 c0               xor %eax,%eax
14:     e8 00 00 00      call <init_module+0x19>
19:     8b 34 25 00 00      mov (%rsp),%edx
20:     48 c7 c7 00 00 00 00  mov $0x0,%rdx
27:     31 c0               xor %eax,%eax
29:     e8 00 00 00      call <init_module+0x1e>
2e:     31 c0               xor %eax,%eax
30:     c9               leaq
31:     c3               ret
```

- 尝试加载 `oopsit.ko` 会产生 `oops`，在初始化期间挂起并产生以下 `oops`（附加到 `/var/log/messages`）：

```
[... 1.467422] Hello:init_module loaded at address 0xffffffff002600
[... 1.467390] BUG: unable to handle NULL dereference (null)
[... 1.467355] IP: [0fffffa0026019]-my_init+0x19/0x32 [oops]
[... 1.467361] PGD 7a9b067 PUD 1b4067
[... 1.467367] Oops: 00000001 PREEMPT
[... 1.467373] CPU 0
[... 1.467375] Modules: (oopsit) offset 0x0
[... 1.467400] loaded: oops_exports,oops_audit,oops_dev,oops_timer
[... 1.467400] page_alloc 0x2b5250
[... 1.467400] serial_core+0cb8091
[... 1.467400] code_alloc_int_snd_da_codec_snd_device
[... 1.467400] crc16ahci libhciciahci_uhci_intel_agibt
[... 1.467400] last loaded: gptpt_wait_scsi
[... 1.467422] Pid: 6343, comm: T
[... 1.467425] Tainted 3.0 #2 manufacturer
[... 1.467432] RIP: 0fffffa0026019 [0fffffa0026019]-my_init+0x19/0x32 [oops]
[... 1.467438] RSP: 0ffff88037b2f88 EFLAGS: 00010029
[... 1.467441] RAX: 0x0000000000000b4 RBX: 0fffffa0026a40 RCX: 0x00000000000000
[... 1.467444] RDX: 0ffff88037b2fd8 RSI: 0ffff88037b2fd8 RDI: 0ffff8801f40f0
[... 1.467447] RBP: 0ffff88037b2f88 R8: 0x0000ffffffb6 R9: 0ffff88037b2fd0
[... 1.467450] R10: 0x0000000000000000 R11: 0x0000000000000000 R12: 0fffffe06
[... 1.467453] R13: 0x0000000000000000 R14: 0x0000000000000000 R15: 0x00000030 FS: 0007faa3c207f00 GS: 0ffff8cf0000(0000) CS:010
--- 跟踪栈结束 ---
```

## 9.2 内核调试器

- 理解在 Linux 上使用调试器的要点是，Torvalds 讨厌它们。对于他这种态度的解释，请见链接。简短的解释是，内核宽容（甚至鼓励）那些检查已知错误（例如，当我持有自旋锁时？）或只需要内核入口点的调试器，并允许通过模块完成工作。

### gdb

- 可以使用 `gdb` 调试器调试运行中的内核。一条执行命令为：

```bash
$ gdb /boot/vmlinux /proc/kcore
```

其中第一个参数是当前未压缩的内核。你可以使用 `ddd` 或 `gdb` 的图形界面。

### kgdb 和 kdb

- `kgdb` 是一个交互式内核调试器。在全功能模式下，它需要通过空调制串口连接两个计算机。在远程主机上运行 `gdb`（或其图形界面封装如 `ddd`），然后在目标系统中进入内核，设置断点、数据等。你可以在内核启动过程中停止目标机器内核。

- `kgdb` 在内核版本 `2.6.26` 中并入主内核。

- 另一个交互式内核调试器 `kdb` 长期作为树外内核补丁存在。它具有以下能力：

## 9.3 调试内核内存和数据结构

- 检查操作，例如单步执行、设置断点。

- 控制操作，例如单步执行、设置断点。

- 切换堆栈回溯、在内核汇编中执行指令等。

- 在 SMP 系统中切换 CPU。

- 等等。

- 当遇到 `oops`（内核模式下的数据访问错误）、在命令行上使用 `kdb` 标志或使用暂停键时，系统会自动进入 `kdb` 环境。

- `kdb` 和 `kgdb` 项目最终合并并包含在 `2.6.35` 内核中，目前有大量的活动和优化。可以通过 `ALT-Sysrq-g` 组合键或通过向 `/proc/sysrq-trigger` 写入（`echoing`）来进入调试器。

- 欲包括分步说明在内的完整文档，请参阅 James Wessel 写的文章（他是近期这两个项目整合的首席开发者），路径位于 `/usr/src/linux/Documentation/DocBook/kgdb.tmpl`；或者查看由内核源码生成的 pdf 格式，请访问：http://training.linuxfoundation.org/course_materials/LF331/kgdb.pdf。

## crash

- `crash` 工具可能由你的 Linux 发行版提供，完整文档可以在 http://people.redhat.com/android/ 找到。

- 使用 `crash` 可以检查内核中的所有数据结构、进行源代码反汇编、通过链表检查并设置内存等。`crash` 还可以检查由 `kdumppackage` 创建的内核转储文件（core dump files）。

## 9.3 debugfs

- `debugfs` 文件系统首次出现在 `2.6.11` 内核中。它可以作为 `/proc` 文件系统的更简单、更现代的替代方案，因为后者的接口不便，且内核开发者已对其失去了兴趣。

- `debugfs` 的主要目的是方便访问调试信息，可能用于设置调试行为。它的设计像任何其他文件系统一样被访问，这意味着可以使用标准的读写工具。

- 也可以使用 `sysfs` 实现相同的目的。然而，`sysfs` 用于系统管理中的信息，并且旨在按照系统总线映射的系统设备树以一致的方式使用。

- `debugfs` 的代码主要由 Greg Kroah-Hartman 开发。使用的函数有：



```c
#include <linux/fs.h>
#include <linux/debugfs.h>

struct *debugfs_create_dir(const char *name, struct directory *parent)
struct *debugfs_create_file(const char *name, mode_t mode, struct directory *parent,
    void *data, const struct file_operations *fops);
void debugfs_remove(struct entry *entry);
```

与 `/proc` 一样，你可以通过使用 `debugfs_create_dir()` 创建目录，在 debugfs 根目录下创建自己的条目；在上述函数中为 `parent` 提供 `NULL` 会将条目放在根目录下。`mode` 参数是无用的权限掩码，`data` 是一个可选参数，可以指向一个私有数据结构。

`fops` 指向一个 `file_operations` 结构，该结构包含一个针对该条目操作的跳转表，就像它在字符驱动程序中使用那样。你可能只需要提供所有者字段，以及读取和写入条目的入口函数。

对于读取函数，你可能想要利用以下函数：

```c
ssize_t simple_read_from_buffer(void __user *to, size_t count, loff_t *ppos,
                const void *from, size_t available);
```

该函数用于从 `from` 指向的内核缓冲区获取信息到用户缓冲区（正确地使用 `copy_to_read()`），其中位置 `ppos` 的进值不会超过 `available` 字节。一个使用此函数的读取函数示例如下：

```c
ssize_t size_t
my_read(struct file *file, char *buf, size_t count, loff_t *ppos)
{
    int nbytes;
    nbytes=sprintf(kstring, "%d\n", val);
    return simple_read_from_buffer(buf, count, ppos, kstring, nbytes);
}
```

更简单的方法是使用创建函数：

```c
struct dentry debugfs_create_u8 (const char *name, mode_t mode,
                struct dentry *parent, us *val);
struct dentry debugfs_create_u16 (const char *name, mode_t mode,
                struct dentry *parent, u16 *val);
struct dentry debugfs_create_u32 (const char *name, mode_t mode,
                struct dentry *parent, u32 *val);
struct dentry debugfs_create_bool (const char *name, mode_t mode,
                struct dentry *parent, u32 *val);
```

这种创建的条目通过 `name` 在父目录下进行标明，它用于简单地读写适当类型的变量。该变量以字符串的形式来回传输。因此，你只需要一行代码（包括头文件！）即可创建一个条目！

为了使用 debugfsset，你可能需要挂载 debugfs 伪文件系统：

```bash
$ mount -t debugfs /sys/kernel/debug
```

但所有最近的发行版都会自动执行此操作，你应该可以跳过这一步。

无论你如何创建条目，在退出时必须使用 `debugfs_remove()` 将其移除，因为像通常一样，内核不会进行垃圾回收。

关于 debugfs 的评审以及如何使用它，请访问 `http://lwn.org/Articles/334546`。

## 9.4 kprobes 和 jprobes

- `kprobes` 调试设施（最初由 IBM 开发者贡献）允许你在运行中内核的任何已知地址插入断点。你可以检查并修改处理器寄存器、数据结构等。

- 最多可以安装四个处理器：

- `pre-handler`（预处理函数）在被探测指令执行之前立即调用。

- `post-handler`（后处理函数）在被探测指令执行后立即调用（如果没有产生异常）。

- `fault-handler`（异常处理函数）在被探测指令产生异常时被调用。

- `break-handler`（断点处理函数）在被探测指令被单步执行或设置断点时被调用。

- 基本函数和数据结构定义在 `/usr/src/linux/include/linux/kprobes.h` 和 `/usr/src/linux/kernel/kprobes.c` 中：

```c
#include <linux/kprobes.h>

int register_kprobe(struct kprobe *p);
void unregister_kprobe(struct kprobe *p);

struct kprobe {
    structlist_node hlist;

    /* 探测位置 */
    kprobe_opcode_t *addr;

    /* 符号名称 */
    char *symbol_name;

    /* 符号偏移量 */
    unsigned int offset;

    /* 在执行 addr 之前调用 */
    kprobe_pre_handler pre_handler;

    /* 在执行 addr 后调用，除非... */
    kprobe_post_handler post_handler;

    /* addr 产生异常（例如页错误）时调用 */
    kprobe_fault_handler fault_handler;

    /* 探测点触发断点时调用 */
    kprobe_break_handler break_handler;

    /* 保存的操作码 */
    kprobe_opcode_t opcode;

    /* 原始指令 */
    struct arch_specific_insn a;
};

typedef int (*kprobe_break_handler)(struct kprobe *, struct pt_regs *);
typedef void (*kprobe_post_handler)(struct kprobe *, struct pt_regs *, unsigned long flags);
typedef int (*kprobe_fault_handler)(struct kprobe *, struct pt_regs *, int trapn);
```

- 注意，处理器接收 `pt_regs` 数据结构的指针，它包含了寄存器的内容。这显然取决于架构，详见 `/linux/arch/x86/asm/ptrace.h`。

- `post handler` 的 `flag` 参数可以取以下值：

```
KPROBE_FLAG_GONE        /* 断点已移除 */
KPROBE_FLAG_DISABLED   /* 探测临时禁用 */
KPROBE_FLAG_OPTIMIZED      /* 探测已过优化 */
```

且不是供 kprobe 用户直接设置。这里的优化意味着在某些架构上，用于中断执行流的断点指令可以替换为跳转指令，从而提升性能。`fault handler` 的 `trapn` 参数给出哪个异常导致故障。

- 为了使用探测，你必须：

- 使用提供的处理函数指针填充 `kprobe` 数据结构。

- 调用 `register_kprobe()`，返回 `0` 表示探测插入成功。

完成后，使用 `unregister_kprobe()`，如果忘记这样做，结果将是灾难性的。

- 剩下的唯一成分是获取被探测指令的地址。如果符号是导出的，那么你可以直接指向它，例如：

```c
addr = (kprobe_opcode_t *) mod_timer;
```

即使符号没有导出，你仍然可以直接指定名称，例如：

```c
kp.symbol_name = "do_fork";
```

你不应该同时设置地址和符号，因为会导致错误。

### 9.4. KPROBES 和 JPROBES

- 可以动态地开启或关闭 kprobes，即使它当前正在使用：

```
$ ls -l /sys/kernel/debug/kprobes
total 0
--rw---- 1 root root 0 Jun 11 08:28 enabled
-r--r--r-- 1 root root 0 Jun 11 01:44 list
```



- 通过向 `enabled` 写入 `1` 或 `0` 可以开启或关闭 `kprobes`。通过查看 `list`，可以检查所有当前加载的探针。

- 额外的 `jprobe` 功能允许你轻松地对内核中的任何函数进行插桩。相关的注册和注销函数以及新的相关数据结构如下：

```c
int register_jprobe(struct jprobe *jp);
void unregister_jprobe(struct jprobe *jp);
void jprobe_return(void);
struct jprobe {
    struct kprobe kp;
    kprobe_opcode_t *entry;
};
```

- 为了使用此功能，你必须设置一个类型为 `jprobe` 的结构体，其中 `entry` 字段指向一个与被探针函数原型和参数完全相同的函数，该函数应该像 `kprobes` 一样指向 `kp.addr` 字段。

- 每当被探针函数被调用时，插桩函数就会被调用，并且必须通过函数 `jprobe_return()` 退出。它在被探针函数之前调用。

- 在函数退出之前，寄存器和栈的内容会被恢复。然而，更改参数的值可能会导致（可能是破坏性的）差异。

## SystemTap

- 虽然 `kprobes` 非常强大，但它的使用需要较低的内核开销。`SystemTap` 提供了一个构建在 `kprobes` 之上的基础设施，简化了内核模块的编写、编译、安装以及有用输出的收集。`SystemTap` 项目可以在 `http://sourceware.org/systemtap/` 找到。

## 9.5 实验

### 实验 1：使用 kprobes

- 在内核中经常执行的地方放置一个 `kprobe`。一个很好的选择是 `do_fork()` 函数，每当有子进程诞生时它就会执行。

- 编写简单的处理函数。

- 通过加载模块并运行导致被探针指令执行的简单命令来测试模块，例如使用 `bash` 启动一个新的 `shell`。

### 实验 2：使用 jprobes

- 通过对常用的内核函数进行插桩来测试 `jprobes` 功能。

- 统计函数被调用的次数。如果你每次都打印它，请注意不要被输出淹没。

### 实验 3：探测模块

- 取一个早期的字符驱动模块，并编写一个新模块，使用 `kprobes` 和 `jprobes` 对字符驱动进行插桩。

- 你正在探测的函数是否需要导出以便供探针工具访问？

### 实验 4：使用 debugfs。

- 编写一个在 `debugfs` 中创建条目的模块。

- 首先是编写一个方便函数，用于在 `debugfs` 文件系统根目录下创建一个简单的变量条目，长度随你自定义。

- 接下来创建自己的目录并在其中放入一个或多个条目。

# 第 10 章

## 定时与定时器

我们将考虑 Linux 管理时间的各种方法。我们将看到 `jiffies` 是如何定义和使用的，以及延迟和计时是如何实现的。我们将讨论内核定时器，展示它们如何被使用以及在 Linux 内核中是如何实现的。我们还将讨论 `hrtimers` 特性及其高精度实现。

| 章节 | 页码 |
| :--- | :--- |
| 10.1 Jiffies | 95 |
| 10.2 插入延迟 | 97 |
| 10.3 什么是动态定时器？ | 98 |
| 10.4 定时器函数 | 98 |
| 10.5 定时器实现 | 99 |
| 10.6 高精度定时器 | 100 |
| 10.7 使用高精度定时器 | 101 |
| 10.8 实验 | 103 |

### 10.1 Jiffies

- 粗略的时间测量由在 `/usr/src/linux/include/jiffies.h` 中定义的变量 `unsigned long volatile jiffies` 提供。

- 在内核 `2.6.21` 之前，`jiffies` 只是一个随着每次定时中断而递增的计数器。然而，随着无滴答内核（tickless kernels）的引入，系统在空闲时不再继续处理中断。（详细信息请见 `http://www.kernel.org/projects/tickless.`）

- `x86` 上的默认频率为 `HZ=1000`，但在编译时可以配置，因此我们获得的 `jiffies` 分率在 `1` 到几毫秒之间。

- 在 `ARM` 上，默认定时器频率随 `SoC` 而异：`OMAP` 设置为 `128`，`Exynos` 设置为 `200`。

- 在 `HZ=1000` 的情况下，`jiffies` 将运行约 `50` 天后溢出（回绕）；如果有人一直在睡觉，可能无法达到那个运行时间。

- 为了避免任何潜在问题，`jiffies` 的值在启动期间设置为 `INITIAL_JIFFIES=0`，这会导致该值在五分钟后回绕。作为副作用，你可能会发现 `jiffies` 的值与 `/proc/interrupts` 中的中断次数不同（无滴答内核也打破了这一点）。

- 用于比较 `jiffies` 值的有用宏：

```c
time_after(a,b)
time_before(a,b)
time_after_eq(a,b)
time_before_eq(a,b)
```

其中第一个在 `a` 在 `b` 之后时为真，第二个则反之。另外两个检查相等性。

- 注意存在 `jiffies_64` 变量。在 `64` 位平台上，它与 `jiffies` 相同；在 `32` 位平台上，`jiffies` 指向它的低 `32` 位。由于 `jiffies_64` 在 `6` 亿年内都不会回绕，因此不需要担心它。

- 使用 `32` 位位计数器时必须小心，因为对值的访问不是原子的，所以需要使用

```c
u64 get_jiffies_64(void);
```

来读取该值。（注意永远不需要。）

- 提供了一些宏将 `jiffies` 相互转换为其他时间表示：

```c
#include <linux/jiffies.h>

unsigned long timespec_to_jiffies(struct timespec *val);
void jiffies_to_timespec(unsigned long jiffies, struct timespec *val);

unsigned long timeval_to_jiffies(struct timeval *val);
void jiffies_to_timeval(unsigned long jiffies, struct timeval *val);

unsigned int jiffies_to_msecs(unsigned long j);
unsigned int msecs_to_usec(unsigned long j);
unsigned long msecs_to_jiffies(unsigned int m);
unsigned long usecs_to_jiffies(unsigned int u);
```

其中 `timeval` 和 `timespec` 结构在用户态中应该是大家所熟悉的：

```c
struct timeval {
    long tv_sec;      /* 秒 */
    long tv_usec;    /* 微秒 */
};

struct timespec {
    long tv_sec;      /* 秒 */
    long tv_nsec;    /* 纳秒 */
};
```

### 10.2 插入延迟

- `jiffies` 的使用变得越来越少，人们认为时间最好用秒、毫秒、纳秒等实际时间单位来表示。

- 虽然可以使用 `jiffies` 来引入忙等待，例如：

```c
#include <linux/sched.h>

jiffone = jiffies + delay * HZ;
while ( time_before(jiffies, jiffone) )
{
    /* 什么都不做 */
}
```

这是惯用的做法；因为 `jiffies` 是 `volatile` 的，每次访问时都会重新读取。因此此循环在延迟期间会锁定 `CPU`（中断可能会被处理）。

- 对于短延迟，可以使用以下函数：

```c
#include <linux/delay.h>
```

```c
void nday(unsigned long nanoseconds);
void udelay(unsigned long microseconds);
void mdelay(unsigned long milliseconds);
```

不应期望 `nday` 真正的纳秒级；取决于硬件，它可能接近微秒。

- 另一种不涉及忙等待的延迟方法是使用函数：

```c
void msleep(unsigned int milliseconds);
unsigned long msleep_interruptible(unsigned int milliseconds);
```

如果 `msleep_interruptible()` 在睡眠结束前返回（因为信号），它将返回请求睡眠期剩余的毫秒数。

## 10.3 什么是动态定时器？



动态定时器（也称为内核定时器）用于延迟函数的执行，直到指定的时间间隔过去。该函数将在提交它的 CPU 上运行。

因为在执行时间点 CPU 可能立即不可用，所以你只能保证函数不会在定时器过期之前运行。虽然不存在显式的周期性调度函数，但让定时器函数自己插入是非常简单的。

函数不会在进程上下文中运行；它将作为软中断（`softir`）在原子上下文中运行。因此，你不能执行任何在中断期间无法执行的操作；例如，不使用 `GFP_KERNEL` 分配内存，不使用信号量等，因为这些方法会睡眠。

## 10.4 定时器函数

内核定时器使用的重要数据结构和函数是：

```c
#include <linux/timer.h>

struct timer_list {
    struct list_head entry;
    unsigned long expires;
    void (*function)(unsigned long);
    unsigned long data;
    struct timer_t_base_s *base;
};

void init_timer(struct timer_list *timer);
void add_timer(struct timer_list *timer);
void mod_timer(struct timer_list *timer, unsigned long expires);
int del_timer(struct timer_list *timer);
int del_timer_sync(struct timer_list *timer);
```

在此 `entry` 指向内核定时器的双向链循环列表；不应直接触摸它。用 `jiffies` 量的 `expires` 字段是一个绝对值，而不是相对值。要运行的函数通过 `function()` 传递，数据可以通过指针参数 `data` 传递给它。

`init_timer()` 在定时器入队之前将列表中的前后续指针置零。

`add_timer()` 将定时器插入全局定时器列表；`mod_timer()` 函数可以用于重置定时器过期的时间。

`del_timer()` 可以在定时器过期前删除它。如果删除了它，则返回 1；如果太晚了定时器函数已经开始执行，则返回 0。如果定时器自行过期，不需要调用 `del_timer()`。

`del_timer_sync()` 确保在返回时定时器函数没有另一个 CPU 上运行，并避免了竞态条件，通常是更好的选择。

## 10.5 定时器实现

定时器可以重新安装自己来设置周期性定时器。可以通过两种方式实现：

```c
init_timer(&t);
t.expires= jiffies + delay;
add_timer(&t);
```

或者

```c
mod_timer(&t, jiffies+delay);
```

通常使用这种更紧凑的形式。注意，在重新安装定时器时重新初始化定时器是非常重要的，`mod_timer()` 在底层已经完成了这一操作。

### 示例

```c
static struct timer_list my_timer;

init_timer(&my_timer);
my_timer.function = my_function;
my_timer.expires = jiffies+ticks;
my_timer.data = &my_data;

add_timer(&my_timer);
...
del_timer(&my_timer);

void my_function(unsigned long var){ };
```

动态定时器的实现必须处理两个不同的任务：

必须从定时器列表中插入和移除函数，或者修改它们的过期时间。

必须在适当的时间执行函数。

最简单的实现是维护一个内核定时器单链表，将新请求的定时器函数添加到列表尾部或以某种排序方式添加，然后当内核决定运行任何已计划的定时器函数时，扫描列表并运行那些时间值已到期的函数。

然而，这将是非常低效的。可能有许多甚至数千个定时器的过期时间需要扫描，内核会被这项任务所累。排序可能有助于扫描过程，但代价是昂贵的插入和删除操作。

Linux 实现了一种非常巧妙的方法，该方法实际上维护了 512 个双向循环链表，使得 `timer_list` 结构体中的 `next` 和 `prev` 字段在任何给定时刻只指向其中一个列表。哪一个列表取决于 `expires` 字段的值。

这些列表被进一步划分为 5 组：

| 组 | 节 (Ticks) | 时间 (HZ=1000) |
|---|---|---|
| tv1 | < 256 | < .256 秒 |
| tv2 | < 2^14 | < 16.4 秒 |
| tv3 | < 2^20 | < 17.5 分钟 |
| tv4 | < 2^26 | 18.6 小时 |
| tv5 | < ∞ | < ∞ |

### 表 10.2: 定时器组

`tv1` 组有一个包含 256 个双向链表的向量，其设置使得第一个列表中的项将在下一个定时器节拍中过期，第二个组的项将在之后的节拍过期，依此类推。同样，`tv2-5` 组各拥有一个包含 64 个双向链表的向量，并按时间组排序。

每当发生一次节拍（`tick`）时，`tv1` 向量列表的索引就会加 1，而需要启动的定时器函数都在同一个双向链表中。当此索引达到 256 时，触发第一次 `cascade_timers()`，它会将第一组 `tv2` 补到 `tv1`，将第一组 `tv3` 补到 `tv2`，依此类推。

## 10.6 高精度定时器

Linux 内核动态定时器的实现方法非常清晰且高效，随着自2.6.16 内核以来逐渐引入的新方法，它得到了极大的增强。

我们首先观察到，实际上存在两种动态定时器：

超时函数（Timeout functions）：主要用于网络代码和设备驱动程序中，用于信号某个事件在指定的时间窗口内未发生，此时应该丢弃任务或启动恢复操作。

定时器函数（Timer functions）：预期在指定的延迟和顺序内准确运行。

超时函数通常比定时器函数多得多，因此在目前的动态定时器实现中，在定时器运行前将其移除的频率远高于实际运行函数的频率。

超时函数对精度的要求较低，而（至少在原则上）定时器函数可能有更严格的需求。

原始实现对于定时器函数运行良好，特别是因为其移除定时器的速度非常快，因为只需要索引查找，且 `jiffies` 级的精度通常足够了。

`hrtimers`（高精度定时器）API 是为实际上预期会执行的动态定时器设计的。

它没有使用复杂的列表集，而是（每个 CPU）仅按过期时间排序的列表，使用红黑树算法。虽然插入和删除可能比原始方法慢，但不需要级联操作，且列表中的元素更少。

`hrtimers` 的过期周期以纳秒而非 `jiffies` 表示。

## 10.7 使用高精度定时器

`hrtimers` 特需要引入一种新的（且不透明的）`ktime_t`，如果特定架构支持，它可以以纳秒级分辨率测量时间。`ktime_t` 的内部表示在 64 位和 32 位平台上非常不同，不应对其进行修改。

处理此时间变量的函数包含在 `/usr/src/linux/include/linux/ktime.h` 中，不需要过多解释：

```c
#include <linux/ktime.h>
```

Linux 内核动态定时器的实现方法非常清晰且高效，随着自2.6.16 内核以来逐渐引入的新方法，它得到了极大的增强。

我们首先观察到，实际上存在两种动态定时器：

超时函数（Timeout functions）：主要用于网络代码和设备驱动程序中，用于信号某个事件在指定的时间窗口内未发生，此时应该丢弃任务或启动恢复操作。

定时器函数（Timer functions）：预期在指定的延迟和顺序内准确运行。

超时函数通常比定时器函数多得多，因此在目前的动态定时器实现中，在定时器运行前将其移除的频率远高于实际运行函数的频率。

超时函数对精度的要求较低，而（至少在原则上）定时器函数可能有更严格的需求。

原始实现对于定时器函数运行良好，特别是因为其移除定时器的速度非常快，因为只需要索引查找，且 `jiffies` 级的精度通常足够了。

`hrtimers`（高精度定时器）API 是为实际上预期会执行的动态定时器设计的。

它没有使用复杂的列表集，而是（每个 CPU）仅按过期时间排序的列表，使用红黑树算法。虽然插入和删除可能比原始方法慢，但不需要级联操作，且列表中的元素更少。

`hrtimers` 的过期周期以纳秒而非 `jiffies` 表示。

`hrtimers` 特需要引入一种新的（且不透明的）`ktime_t`，如果特定架构支持，它可以以纳秒级分辨率测量时间。`ktime_t` 的内部表示在 64 位和 32 位平台上非常不同，不应对其进行修改。



- 处理此时间变量的函数包含在`/usr/src/linux/include/linux/ktime.h`中，不需要过多解释：

# 10.8 实验

```c
static int __init_my_init(void) {
    data = kmalloc(sizeof(*data), GFP_KERNEL);
    data->period = ktime_set(1, 0);    /* short period, 1 second */
    hrtimer_init(&data->timer, CLOCK_REALTIME, HRTIMER_MODE_REL);
    data->timer.function = ktfunun;
    hrtimer_start(&data->timer, data->period, HRTIMER_MODE_REL);

    return 0;
}
```

```c
static void __exit_my_exit(void) {
    hrtimer_cancel(&data->timer);
    kfree(data);
}
```

```c
module_init(my_init);
module_exit(my_exit);
MODULE_LICENSE("GPL v2");
```

## 10.8 实验

### 实验 1：字符驱动中的内核定时器

- 编写驱动程序，每当对设备进行`write()`操作时，启动一个内核定时器。
- 向驱动程序传递一些数据并将其打印出来。
- 在定时器函数被调度时打印`current->pid`字段，然后在函数执行时再次打印。

### 实验 2：多个内核定时器

- 将第一个实验中的周期设置得足够长，以便在定时器函数运行之前可以执行多次写操作。提示：你可能想在运行此实验之前保存好你的数据。
- 该函数运行了多少次？
- 修复解决方案使多个定时器能够正常工作。

### 实验 3：周期性内核定时器

- 编写一个模块，启动一个周期性的内核定时器函数；即它应该重新安装自己。

### 实验 4：多个周期性内核定时器

- 编写一个模块，启动两个周期性的内核定时器函数；即它们应该重新安装自己。
- 一个周期序列应该小于 256 个 ticks，因此落在`tv1`向量中，另一个应该小于 16 K ticks，因此落在`tv2`向量中。
- 每当定时器函数执行时，打印自模块加载以来的总经过时间，以 jiffies 为单位。

### 实验 5：高分辨率定时器

- 执行与上一个练习相同的任务，设置两个周期性定时器，但这次使用`hrtimer`接口。

### 实验 6：使用 kprobes 获取统计数据

- 使用 kprobes 找出内核定时器在运行之前被删除的频率。
- 检查内核源码发现，定时器是通过`add_timer()`或`mod_timer()`的。
- 你可以通过监控`del_timer()`和`del_timer_sync()`来查看定时器删除的频率；然而在单处理器系统上，`del_timer_sync()`未定义。
- 定时器非常频繁，你可能不想在每次调度或删除时都打印，例如每 100 次打印一次加上最后的统计。
- 定时器的删除可能比调度更频繁吗？

# 第 11 章 竞态条件与同步方法

![](img/134c18b05ee9bbbe93ba3f4335720ac1_120_0.png)

我们将考虑内核用于同步和避免竞态条件的一些方法。我们将讨论原子函数和位操作、自旋锁、互斥锁、信号量以及完成函数的使用。最后我们将查看内核如何维护引用计数。

- 11.1 并发与同步方法 105
- 11.2 原子操作 107
- 11.3 位操作 108
- 11.4 自旋锁 109
- 11.5 大内核锁 110
- 11.6 互斥锁 111
- 11.17 信号量 113
- 11.8 完成函数 116
- 11.9 引用计数 116
- 11.10 实验 117

## 11.1 并发与同步方法

内核执行是异步且不可预测的；中断会随时发生，系统调用可能会被抢占。这可能导致竞态条件，即多个执行线程同时访问相同数据，从而产生不可预测的结果。

竞态条件发生在两个或多个执行线程并发访问共享数据时，且最终结果取决于访问的顺序。

为了避免竞态条件，内核使用了多种同步方法：

- 原子操作：这些操作保证在单个不可分割的步骤中完成。
- 自旋锁：一种锁，线程会在循环中“自旋”直到锁可用。
- 互斥锁：类似于自旋锁，但如果锁被占用，线程将进入睡眠。
- 信号量：用于控制多个线程或进程对资源的访问的同步机制。
- 完成函数：用于向线程通知事件已发生。

## 11.2 原子操作

```
int atomic_inc_return(int i, atomic_t *);
int atomic_dec_return(int i, atomic_t *);
```

- 注意`ATOMIC_INIT()`、`atomic_read()`和`atomic_set()`宏是自动原子的，因为它们只是读取和写入一个值。
- 在 64 位平台上，还有一种 64 位的原子类型和相关函数，例如`void atomic64_inc(atomic64_t *v)`。详情请参阅相应的头文件。

### 11.3 位操作

- 为了检查和修改各种标志位和锁变量中的单个位，内核提供了许多原子操作函数。
- 这些操作通过单条机器指令完成，因此非常快；在大多数平台上，这可以在不中断的情况下完成。
- 理出所料，这些函数根据架构而有所不同。它们定义在`/usr/src/linux/x86/include/asm/bitops.h`中。

```c
#include <asm/bitops.h>
```

```c
void set_bit(int nr, volatile unsigned long *addr);
void clear_bit(int nr, volatile unsigned long *addr);
void change_bit(int nr, volatile unsigned long *addr);
```

```c
int test_bit(int nr, volatile unsigned long *addr);
int test_and_set_bit(int nr, volatile unsigned long *addr);
int test_and_clear_bit(int nr, volatile unsigned long *addr);
int test_and_change_bit(int nr, volatile unsigned long *addr);
```

```c
long find_first_zero_bit(const unsigned long *addr, unsigned long size);
long find_next_zero_bit(const unsigned long *addr, unsigned long size, unsigned long offset);
long find_first_bit(const unsigned long *addr, unsigned long size);
```

```c
unsigned long fff(unsigned long word);
unsigned long ffs(int x);
unsigned long fls(int x);
```

- 在这些函数中，`nr`的类型取决于架构；对于 32 位 x86 和 ARM，它只是一个整数，而`alpha`是`unsigned long`。第二个参数是指要检查或修改的位的变量。其类型随架构而异，通常为`volatile long`。
- 这些函数返回之前的位值作为返回值。
- 注意，`ff()`、`ffs()`和`fls()`分别查找字字整数中的第一个 0 位、第一个置位和最后一个置位，而`find_first_zero_bit()`、`find_next_zero_bit()`和`find_first_bit()`函数在变变长度的掩码上工作。
- 还存在一组非原子位，它们与上述位不同之处在于带有`__set_bit()`前缀。它们可以在锁已获取并确保完整性时使用，且速度比原子版本快得多。

### 11.4 自旋锁

- 自旋锁是一种保护代码临界区的机制。在等待资源可用时它会自旋等待，而不是进入睡眠状态。
- 人可以防止同一代码段在多个 CPU 上执行，但更广泛地说，它还保护了对同一资源的并发访问，这些资源可能被不同的代码路径访问，并且可能在进程上下文中内部或之外。
- 在引入内核抢占之前，自旋锁仅在多处理器系统中是重要的。这是因为 SMP CPU 可以同时访问代码的临界区。因此，在内核抢占被纳入 2.6 内核之前，在单处理器系统上，自旋锁被定义为空操作 no-ops。然而，在可抢占、超线程或多核系统中，自旋锁始终会工作。



`/usr/src/linux/arch/x86/include/asm/spinlock.h` 中的宏（在 SMP 系统上从 `/usr/src/linux/include/linux/spinlock.h` 包含）包含了自旋锁的基础代码。

在最简单的情况下，你可能编写类似下面的代码：

```c
spin_t my_lock;
spin_lock_init(&my_lock);

spin_lock(&my_lock);
    critical code ............. 
spin_unlock(&my_lock);
```

这保证了触碰临界资源的代码不会在多个处理器上同时运行，而在非抢占内核的单处理器系统上则没有任何作用。然而，上述函数不应在进程上下文之外使用（即在中断处理程序中），因为在那种情况下可能会导致死锁。（进一步解释请参见 `/usr/src/linux/Documentation/spinlocks.txt`。）

人希望同时挂起或禁用中断处理。在这种情况下，这样做：

```c
unsigned long flags;
spin_t my_lock;

spin_lock_init(&my_lock);

spin_lock_irqsave(&my_lock,flags);
    critical code ............. 
spin_unlock_irqsave(&my_lock,flags);
```

这保证了触碰临界资源的代码不会在多个处理器上同时运行，而在非抢占内核的单处理器系统上则没有任何作用。然而，上述函数不应在进程上下文之外使用（即在中断处理程序中），因为在那种情况下可能会导致死锁。

# 第 11 章 竞态条件与同步方法

并且旨在被透明地使用。如果 `count` 为 1，则互斥锁是空闲；如果为 0，则已锁定；如果是负数，则表示已锁定且进程正在等待。

互斥锁在未锁定状态下初始化，可以使用：

`DEFINE_MUTEX(name);`

在编译时完成，或者使用

`void mutex_init(struct mutex *lock);`

在运行时完成。

锁原语有不可中断和可中断两种形式，但只有一个解锁函数：

```c
void mutex_lock(struct mutex *lock);
int mutex_lock_interruptible(struct mutex *lock);
int mutex_lock_killable(struct mutex *lock);
void mutex_unlock(struct mutex *lock);
```

任何信号都会中断通过 `mutex_lock_interruptible()` 获取的锁，而只有致命信号会中断通过 `mutex_lock_killable()` 获取的锁。通过 `mutex_lock()` 获取的锁不受信号影响。

使用互斥锁时有一些重要的限制：

- 互斥锁必须由原始所有者释放。
- 互斥锁不能递归应用。
- 不能在中断上下文中锁定或解锁互斥锁。
- 请注意，如果没有在内核中配置互斥锁调试，违反这些限制的行为将不会被检测。
- 互斥锁的所有者是在获取锁的上下文中执行的任务。如果该任务不再活跃，其他任务可以释放互斥锁而不会触发调试警告。

可以使用以下非阻塞尝试获取锁：

`mutex_trylock(struct mutex *lock);`

以及

`int mutex_is_locked(struct mutex *lock);`

检查锁的状态。

注意，`mutex_trylock()` 在获取锁成功时返回 1，这类似于 `spin_trylock()`，但与 `down_trylock()` 不同。

并没有像信号量、自旋锁等其他互斥设备那样的特殊读/写互斥锁。

## 信号量

也可以使用计数信号量来保护代码的临界区。它们作用于类型为 `semaphore` 和 `rw_semaphore` 的数据结构。

基本函数（定义为宏）可以在 `/usr/src/linux/include/linux/semaphore.h` 和 `/usr/src/linux/include/linux/rwsemaphore.h` 中找到。

```c
#include <linux/semaphore.h>

void down(struct semaphore *sem);
int down_interruptible(struct semaphore *sem);
int down_trylock(struct semaphore *sem);
void up(struct semaphore *sem);

void down_read(struct rw_semaphore *sem);
void down_write(struct rw_semaphore *sem);
void up_read(struct rw_semaphore *sem);
void up_write(struct rw_semaphore *sem);

struct semaphore {
    unsigned int count;
    int sleepers;
    wait_queue_head_t wait;
};

struct rw_semaphore {
    rw_count_t count;
    spinlock_t lock;
    struct list_head list_head;
};
```

`down()` 函数检查是否有人已经进入了临界区；如果信号量的值大于 0，则将其减1并返回。如果已经是 0，它将睡眠并在稍后重试。

`down_trylock()` 函数不同之处在于它可以被信号中断；另一种形式会阻塞进程的任何信号，应该只非常谨慎地使用。然而，如果你使用此函数，你必须检查信号是否到达，因此你的代码可能如下：

```c
if (down_interruptible(&sem)) return -ERARTSYS
```

这告诉系统重试系统调用或向应用程序返回 `-EINTR`；这取决于系统的设置。

`down_trylock()` 检查信号量是否可用，如果不可用则返回，因此它是一个非阻塞函数（这就是为什么不需要可中断的形式）。如果获取了锁，则返回 0。例如，驱动程序的典型读取入口可能包含：

```c
if (file->flags & O_NONBLOCK) {
    if (down_trylock(&sem))
        return -ERAGAIN;
}
else {
    if (down_interruptible(&sem))
        return -ERARTSYS;
}
```

`up()` 函数增加信号量的值，唤醒所有等待该信号量的进程。它不需要任何*可中断的形式*。

`_read`、`write` 形式提供了更细粒度的控制，允许多个读者访问受保护的资源，但只有一个写入者。

你必须小心处理信号量；你不能在睡眠非常糟糕的地方（例如在中断例程中）降低它们，并且你必须仔细思考以避免竞态条件。

信号量可以使用以下宏声明和初始化：

```c
DECLARE_MUTEX(name);
DECLARE_RWSEM(name);
```

其中 `name` 是 `struct semaphore` 类型的对象。

信号量的值可以通过内联函数直接操作：

```c
void sema_init(struct semaphore *sem, int val);
```

并且通常用以下内联便利函数初始化：

```c
static inline void init_MUTEX(struct semaphore *sem){
  sema_init(sem, 1);
}
static inline void init_MUTEX_LOCKED(struct semaphore *sem){
  sema_init(sem, 0);
}
```

摘自 `/src/linux/kernel/sys.c` 的示例：



```c
DECLARE_RWSEM(uts_sem);

SYSCALL_DEFINE2(gethostname, char __user *, name, int len) {
    int i, errno;
    struct new_utsname *u;
    if (len < 0)
        return -EINVAL;
    down_read(&uts_sem);
    u = unamename();
    i = 1 + strlen(u->nodename);
    if (i > 0)
        i = len;
    errno = 0;
    if (!copy_to_user(name, u->nodename, i)) {
        errno = -EFAULT;
        return errno;
    }
    up_read(&uts_sem);
    return errno;
}
```

![](img/134c1b05ee9bbbe93ba3f4335720ac1_130_0.png)

- 从历史上看，信号量更多地被用二进制互斥锁而不是计数器。
- 信号量比互斥锁更难调试，因为它可以有多个所有者。
- 除非真的需要信号量的计数功能，否则新代码应使用互斥锁，尽可能将信号量转换为互斥锁。
- 在内核版本 2.37 中使用 `DEFINE_SEMAPHORE(name);` 来代替 `DECLARE_MUTEX()`，这要清晰得多。
- 从内核 2.26 开始，尽可能移除信号量的努力正在逐步进行。
- 作为这项工作的一部分，与架构相关的代码被通用代码所取代。
- 与此同时，信号量结构中的 `count` 字段类型更改为 `unsigned int`。

# 第11 章 竞态条件与同步方法

## 11.8 完成函数

- 完成函数提供了一种等待事件发生的替代方法，并针对预期竞争的情况进行了优化，不像针对低竞争情况优化的信号量。

```c
#include <linux/completion.h>

struct completion {
    unsigned int done;
    wait_queue_head_t wait;
};

void init_completion(struct completion *c);
void wait_for_completion(struct completion *c);
int wait_for_completion_interruptible(struct completion *c);
void complete(struct completion *c);
void complete_and_exit(struct completion *c, long code);
```

```c
unsigned long wait_for_completion_timeout(struct completion *c, unsigned long timeout);
unsigned long wait_for_completion_interruptible(struct completion *c, unsigned long timeout);
```

- 带有 `timeout` 名称的功能变体会在到期时返回而不唤醒。这些和不可中断的形式都有非空返回值且需要检查。
- 完成结构可以通过两种方式之一声明并初始化：

```c
DECLARE_COMPLETION(x);

struct completion x;
init_completion(&x);
```

- `complete_and_exit()` 函数成功时不返回，接受一个额外参数 `code`，作为内核线程终止时的退出代码。显然，此函数只应用于终止后台线程，因为它会杀死正在执行。
- 与信号量的对应非常简单；方法之间是一一对应的：

```
struct semaphore <---> struct completion
sema_init()         ---> init_completion()
down()              <---> wait_for_completion()
up()               ---> complete()
```

- 通常需要为对象维护一个引用计数。如果资源在多个地方使用并传递给各种子系统，可能需要这样的引用计数。
应该使用 `kref` API 来维护引用计数，而不是手动构建。相关函数定义在 `/usr/src/linux/include/linux/kref.h` 中。

## 11.9 引用计数

## 11.10. 实验

```c
struct kref {
    atomic_t refcount;
};

void kref_init(struct kref *kref);
void kref_set(struct kref *kref, int num);
void kref_get(struct kref *kref);
int kref_put(struct kref *kref, void (*release) (struct kref *kref));
```

- 假设 `kref` 结构被嵌入在你正在使用的某个数据结构中，该结构可以是你用于引用计数的对象，如下所示：

```c
struct my_dev_data {
    ...
    struct kref my_refcount;
};
```

- 必须使用 `kref_init()` 进行初始化，并使用 `kref_get()` 增加引用计数。
- 减少引用计数通过 `kref_put()` 完成，如果引用计数变为零，则会调用 `kref_put` 第二个参数所指定的函数。该函数可能不为 `NULL`，也不仅仅是 `kfree()`（后者会被显式检查）。这可能像这样：

```c
struct my_dev_data *md;

kref_put(md->my_refcount, my_release);

static void my_release(struct kref *kref) {
    struct my_dev_data *md = container_of(kref, struct my_dev_data, my_refcount);
    my_dev_free(md);
}
```

其中在 `my_dev_free()` 中执行必要的操作以释放任何内存和其他资源。
- 注意 `container_of()` 宏的使用，它执行指针运算；其第一个参数是给定的指针，第二个参数是嵌入它的结构类型，第三个参数是它在该结构中的名称。返回的结果是该结构的指针。
- 关于使用内核引用计数的良好指南可以在 `/usr/src/linux/Documentation/kref.txt` 中找到。

## 11.10 实验

### 实验 1：互斥竞争

- 编写三个简单的模块，其中第二个和第三个模块使用从第一个模块导出的变量。第二个和第三个可以相同，只需只需它们不同的名称。
- 提示：你可以使用宏 `__stringify(KBUILD_MODNAME)` 来打印模块名称。
- 你可以通过对模块练习的结果进行细微修改来实现来实现这一点。
- 导出的变量应该是一个互斥锁（`mutex`）。第一个模块应该在未锁定状态下初始化它。
- 第二个（第三个）模块应该尝试锁定互斥锁，如果它已被锁定，则加载失败；确保从你的初始化函数返回适当的值。
- 确保在清理函数中释放互斥锁。
- 通过尝试同时加载两个模块来完成测试，看看是否可行。确保在一个模块被卸载后可以加载另一个模块，以确保你正确释放了互斥锁。

### 实验 2：信号量竞争

- 现在使用信号量（`semaphore`）代替互斥锁来执行相同的操作。

### 实验 3：在中断中解锁互斥锁。

- 修改简单的中断共享实验，使得在中断处理程序中获取互斥锁，然后释放它。
- 这被认为是非法的。它是被忽略了、强制执行还是被警告了？为什么？

# 第 12 章

## ioctls

![](img/134c18b05ee9bbbe93ba3f4335720ac1_134_0.png)

我们将考虑 `ioctl` 方法（I/O 控制），这是一个大锦囊，可以通过许多不同的方式供应用程序与设备驱动程序通信。我们将讨论 `ioctl` 是什么的、如何调用它们，以及如何为它们编写驱动程序入口点。

- 12.1 什么是 ioctls？........................................................................... 119
- 12.2 ioctls 的入口点...................................................................................... 120



## 12.1 什么是 ioctls?

`ioctl`（输入输出控制）是特殊的函数，用于与设备通信。`ioctl(1)` 是可以从用户态发送或接收的命令。

`ioctl` 几乎可以执行任何操作，类似于 `read()`、`read()` 等。

为了使用 `ioctl`，必须首先使用 `open()` 系统调用打开设备，然后发送相应的 `ioctl(1)` 命令。

```c
#include <sys/ioctl.h>

int ioctl(int fd, ...);
```

参数通常是 `char *arg`。成功时返回 0，错误时返回 `errno`。

表 12.1：`ioctl()` 返回值

| 值 | 含义 |
| :--- | :--- |
| EBADF | 错误的文件符 |
| ENOTTY | 未与设备关联 |
| EINVAL | 无效命令 |

示例：

```c
int fd = open("/dev/mydrvr", O_RDWR);
if (ioctl(fd, MYDRVR_SET, buf) < 0)
    perror("MYDRVR_SET failed");
```

## 12.2 ioctls 的入口点

`ioctl()` 的入口点如下：

```c
#include <linux/ioctl.h>
static int mydrvr_unlocked_ioctl(struct file *file, unsigned int cmd, unsigned long arg)
{
    if (_IOC_TYPE(cmd) != MYDRBASE)
        return -EINVAL;

    switch (cmd) {
        case MYDRVR_RESET:
            /* 执行某些操作 */
            return 0;

        case MYDRVR_OFFLINE:
            /* 执行某些操作 */
            return 0;
    }
}
```

## 12.3 加锁与无锁的 ioctls

从 Linux 早期开始，`ioctl()` 入口点实际上具有原型：

`int ioctl(struct inode *inode, struct file *filp, unsigned int cmd, unsigned long arg);`

不幸的是这些加锁调用会导致 BKL（大锁）；如果它们运行时间长，可能会导致无关区域出现巨大的延迟。

注意，BKL 允许睡眠，与其他锁不同，加入队列不足以阻塞系统；你实际上执行了一些占用 CPU 时间的工作。引入引入无锁入口点是为了避免 BKL，如果它存在 `file_operations` 结构中，它将取代加锁版本。

在 2.6.36 内内核中，加锁版本的 `ioctl()` 入口点最终被移除。驱动程序无法再次使用它。

移除加锁的 `ioctl()` 系统调用是移除系统调用和驱动程序中 BKL 项目的一部分，目标是逐个消除。

## 12.4 定义 ioctls

在使用 `ioctl()` 之前，必须为整数命令参数选择数字。仅仅随机选择数字是一个坏主意；它们在整个系统中应该是唯一的。

至少可能出现以下两种错误：

两个设备节点可能具有相同的主设备号。

应用程序可能会犯错，打开了多个设备并混淆了文件描述符，向错误的设备发送了正确的命令。

结果可能是灾难性的，甚至损坏硬件。

```c
case MYDRVR_GET_STATE:
    if (copy_to_user((void *)arg, &mydrvr_state_struct, sizeof(mydrvr_state_struct)))
        return -EFAULT;
    return 0;

default:
    return -EINVAL;
```

两个文件是 `/usr/src/linux/include/asm-generic/ioctl.h` 和 `/src/linux/Documentation/ioctl/ioctl-number.txt`。

在当前的实现中，命令长度为 32 位；命令位于低 16 位中（这是旧的大小）。它包含四个位域：

表 12.3: `ioctl()` 命令位域

| 位数 | 名称 | 含义 | 描述 |
|---|---|---|---|
| 8 | IOC_TYPEBEITS | type | 整个驱动程序中使用的魔数 |
| 8 | IOC_NRBITS | number | 序列号 |
| 14 | IOC_SIZEBITS | size | 数据传输的大小 |
| 2 | IOC_DIRBITS | direction | 数据传输的方向 |

方向可以是以下之一：

`IOC_NONE`

`IOC_READ`

`IOC_WRITE`

`IOC_READ | IOC_WRITE`

并且从应用程序的角度来看是这样定义的。

大小和方向信息可以使用 `arg` 作为指针来简化用户空间和内核空间之间的数据传传。请注意，这里没有强制规定；你可以向任何方向发送信息，而不取决于定义命令时使用的方向。通过这种方式设置的最大传输量是 16 KB，因为你只有 14 位用于编码大小。

你不需要关注命令中位拆分的情况，但这样做是一个好主意。

### 有用的宏：

编码 `ioctl` 数字：

```
IO(type, number)
IOR(type, number, size)
IOW(type, number, size)
IOWR(type, number, size)
```

人们必须小心参数大小的使用方式。与其传递一个整数，不如传递实际的数据结构，然后对该结构应用 `sizeof()` 原语；例如：

```
MY_IOCTL = IOWR('k', 1, struct my_data_structure);
```

如果 `my_data_structure` 是动态分配的，这将行不通，因为在这种情况下 `sizeof()` 将返回指针的大小。

解码 `ioctl` 数字：

`IOC_DIR(cmd)`

`IOC_TYPE(cmd)`

`IOC_NR(cmd)`

`IOC_SIZE(cmd)`

## 12.5 实验

示例：

```
#define MYDRBASE 'k'
#define MYDR_RESET IO(MYDRBASE, 1)
#define MYDR_STOP IO(MYDRBASE, 2)
#define MYDR_READ IOR(MYDRBASE, 2, my_data_buffer)
```

### 实验 1：使用 ioctl() 传递数据

编写一个简单的模块，使用 `ioctl` 方向信息在驱动程序和用户空间程序之间传回固定大小的数据缓冲区。

数据传输的大小和方向（们）应该编码在命令数字中。

你需要编写一个用户空间应用程序来测试此。

### 实验 2：使用 ioctl() 传递变长数据

扩展上一个练习，发送一个长度在运行时确缓冲区。你可能需要在用户空间程序中直接使用 `_IOC` 宏（参见 `linux/ioctl.h`）。

### 实验 3：使用 ioctl() 发送信号

有时需要从内核向应用程序发送信号。执行此操作的函数是：

`int send_sig(int signal, struct task_struct *tsk, int priv);`

其中 `signal` 是要发送的信号，`task` 指向要发送信号的进程对应的 `task` 结构，`priv` 表示权限级别（用户应用程序为 0，内核为 1）。

编写一个具有三个 `ioctl` 命令的字符驱动程序：

设置要发送信号的进程 ID。

设置要发送的信号。

发送信号。

记住你必须使用 `pid_task(find_vpid(pid), PIDTYPE_PID)` 将 `pid` 连接到它对应的 `task` 结构。

你还需要开发发送端程序。

如果没有给出任何参数，它应该向当前进程发送 `SIGKILL`。

如果给出了一个参数，它应该设置要发送信号的进程 ID。

如果给出了两个参数，它还应该设置信号。

# 第 13 章



# 统一设备模型和 sysfs

![](img/134c18b05ee9bbbe93ba3f4335720ac1_140_0.png)

我们将考虑**统一设备模型**、它的主要数据结构以及它们如何应用于真实设备，并检查 **sysfs** 伪文件系统。

13.1 统一设备模型 ................................................................ 125

13.2 基础结构 ....................................................................................... 126

13.3 真实设备 ................................................................................................ 127

13.4 sysfs ........................................................................................ 129

13.5 实验 ............................................................................................ 131

## 13.1 统一设备模型

- **统一设备模型（或集成设备模型）**引入 2.6 内核系列。在该方案下，所有设备都在一个框架中处理，具有相似的数据结构和功能方法。此外，该框架被表示为以系统总线为根的设备树。

- 在多数情况下，设备驱动程序不需要与底层模型直接交互，而是作为与其连接的总线类型（如 `pci`）下的设备注册。设备信息暴露在 `sysfs` 文件系统中，驱动程序可以选择性导出数据进行查看，作为使用 `/proc` 文件系统和 `ioctl()` 命令 更现代的替代方案。

- 驱动模型的根是**对象（objects）**，它们包含了与系统中任何对象相关的数据的简单表示，例如名称、类型、父节点、引用计数、锁等。一组类型相同的对象被包含在 `kset` 中。

- 包含在驱动模型中的结构包含每个设备的信息，例如该驱动用于什么、它们位于什么总线、、处于什么电源状态以及如何挂起和恢复。它们还描绘了系统总线的结构、它们如何相互连接以及可以附加和卸载哪些设备。

## 13.2 基础结构

```c
// 每个设备都是在 /usr/src/linux/include/device.h 中定义的通用结构
struct device {
    struct device *parent;
    void *private;
    struct kobj;
    const char *init_name; /* 设备的初始名称 */
    struct device_type *type;
    struct mutex mutex; /* 用于同步对其驱动调用的锁 */
    struct bus_type *bus; /* 设备所在的总线类型 */
    struct device_driver *driver; /* 驱动程序分配了这个设备 */
    void *platform_data; /* 平台特定数据，设备核心不碰它 */
    struct dev_pm_info power;
    struct dev_pm_domain *pm_domain;
#ifdef CONFIG_NUMA
    int numa_node; /* 靠近的 NUMA 节点 */
#endif
    u64 dma_mask; /* DMA掩码（如果是设备）类似于 dma_mask，但用于 alloc_coherent 映射，并非所有硬件都支持分配描述符64位地址 */
    struct device_dma_parameters *dma_parms;
    struct list_head dma_pools; /* DMA池（如果是DMA的） */
    struct dma_coherent_mem *dma_mem; /* 用于一致内存覆盖 */
    /* 体系特定的添加 */
    struct dev_archdata archdata;
    struct device_node *of_node; /* 关联的设备树节点 */
    dev_t dev_t; /* dev_t，创建 sysfs "dev" */
    spinlock_t devres_lock;
    struct list_head devres_head;
    struct list_node knode_class;
    struct class *class;
    const struct attribute_group *groups; /* 可选组 */
    void (*release)(struct device *dev);
};
```

## 13.3 实际设备

- 在重要字段初始化后，通过以下函数向系统内核注册和注销设备：

```c
int device_register (struct device *dev);
void device_unregister (struct device *dev);
```

- 设备的引用计数通过以下函数进行原子级增加和减少：

```c
struct device *get_device (struct device *dev);
void put_device (struct device *dev);
```

- 指向 `device_driver` 类型结构体的指针描述了设备的驱动程序：

```c
struct device_driver {
    const char *name;
    struct bus *bus;

    struct module *owner;
    const char *mod_name; /* 用于内置模块 */

    bool_suppress_bind_attr; /* 禁止通过 sysfs 绑定/解载 */

    const struct of_device_id *of_match_table;

    int (*probe)(struct device *dev);
    int (*remove)(struct device *dev);
    void (*shutdown)(struct device *dev);
    int (*suspend)(struct device *dev, pm_message_t state);
    int (*resume)(struct device *dev);
    const struct attribute_group *groups;

    const struct dev_pm_ops *pm;

    struct driver_private *p;
};
```

- 驱动程序通过相应的总线进行注册/注销：

```c
int driver_register (struct device_driver *drv);
void driver_unregister (struct device_driver *drv);
```

并且引用计数通过以下函数增加/减少：

```c
struct device_driver *get_driver (struct device_driver *drv);
put_driver (struct device_driver *drv);
```

- 接下来我们考虑这种通用基础设施如何连接到实际设备。

## 13.3 实际设备

- 实际设备驱动程序直接与我们目前描述的结构体工作；相反，它们被用于特定类型总线和/或设备的内部代码调用。

- 例如，PCI 设备有两个重要的结构体：

```c
struct pci_dev {
    ....
    struct pci_driver *driver;
    ....
    struct device *dev;
}

struct pci_driver {
    ....
    struct device_driver driver;
}
```

并且驱动程序通过以下方式向系统注册：

```c
#include <linux/pci.h>

int pci_register_driver (struct pci_dev *);
void pci_unregister_driver (struct pci_dev *);
```

而设备直接通过 `probe` 回调函数或 `pci_find_device()` 进行注册或发现。

- 这与通用基础设施是如何连接的？由于通用设备结构嵌入在 `pci_dev` 结构中，而通用 `device_driver` 结构又嵌入在 `pci_driver` 结构中，因此必须进行指针运算。

- 这是通过使用宏 `to_pci_dev()` 实现的，例如：



```c
struct device *dev;
    ....
struct pci_dev *pdev = to_pci_dev(dev);
```

该宏基于 `container_of(n)` 宏实现：

```c
#define to_pci_dev(n) container_of(n, struct pci_dev, dev)
```

- 同样，我们可以通过其嵌入的 `device_driver` 结构访问 `pci_driver` 结构：

```c
struct device_driver *drv;
    ....
struct pci_driver *pdrv = to_pci_driver(drv);
```

- 少数例外外（例如进行 DMA 传输），驱动程序并不涉及通用结构体和注册。例如，PCI 设备填充 `pci_driver` 结构，并调用 `pci_register_driver()`（以及其他某些函数）进入系统。然而，这些函数是基于底层设备模型编写的。

- 我们查看 PCI 设备是如何挂钩到统一设备模型中的；对于 USB 和网络等其他设备，关系可能是相同的。添加新设备只需遵循相同的路径。

## 13.4 sysfs

- `sysfs` 文件系统的支持构建在所有现代内核中，并应该被挂载到 `/sys`。然而，统一设备模型不需要挂载。

- 让我们看看在 2.6 内核中可以发现什么；该文件系统的布局通过命令：

```bash
ls -F /sys
block/class/devices/firmware/kernel/module/
```

这显示了基本的设备层次结构。设备可以通过以下方式进行检查：

```bash
ls -l /sys/class/
drwxr-xr-x 5 root 0 13:04 eth0/
drwxr-xr-x 5 root 0 13:04 eth1/
drwxr-xr-x 5 root 0 13:04 lo/
```

查看以太网卡：

```bash
ls -l /sys/class/net/eth0/
total 0
-r----r-- 1 root 4096 Oct 13:16 addr_assign_type
-r----r-- 1 root 4096 Oct 13:16 address
-r----r-- 1 root 4096 Oct 13:16 addr_len
-r----r-- 1 root 4096 Oct 13:16 broadcast
-r----r-- 1 root 4096 Oct 13:16 carrier
device -> lrwxrwxrwx 1 root 0 ../../../devices/pci000:00:00.0/004:02.0
-r----r-- 1 root 4096 Oct 13:16 dev_id
-r----r-- 1 root 4096 Oct 13:16 dormant
-r----r-- 1 root 4096 Oct 13:16 duplex
-r----r-- 1 root 4096 Oct 13:16 features
rw-s--r--x 1 root 4096 Oct 13:16 flags
rw-s--r--x 1 root 4096 Oct 13:16 ifalias
-r----r-- 1 root 4096 Oct 13:16 ifindex
-r----r-- 1 root 4096 Oct 13:16 iflink
-r----r-- 1 root 4096 Oct 13:16 link_mode
rw-s--r--x 1 root 4096 Oct 13:16 mtu
-r----r-- 1 root 4096 Oct 13:16 operstate
drwxr-xr-x 2 root 0 13:16 prefix
drwxr-xr-x 2 root 0 13:04 queues
drwxr-xr-x 2 root 0 13:09 statistics
lrwxrwxrwx 1 root 0 13:09 subsystem -> ../
rw-s--r--x 1 root 4096 Oct 13:16 tx_queue_len
-r----r-- 1 root 4096 Oct 13:04 type
rw-s--r--x 1 root 4096 Oct 13:16 uevent
```

注意到类型条目的值：

```bash
$ cat /sys/class/net/eth0/mtu
1500
```

## 第 13 章 统一设备模型与 SYSFS

我们意识到从 `/proc` 文件系统获取信息。其意图是每行一个文本值，尽管这并不被强制执行。

## 13.5 实验

实验 1：使用 libsysfs 和 sysfsutils。

- `systool` 多功能工具为检查 `/sys` 设备树提供了一个方便的接口，它是 `sysstools` 或 `sysfsutils` 软件包的一部分。目前它使用 `libsysfs`，该库正在被弃用并改为 `libhal`。

- 执行 `man systool` 并不带参数运行 `systool` 命令。它应该显示所有的总线类型、设备类和根设备。执行 `systool -h` 查看如何使用一些额外的参数和选项。

- 探索吧！

# 第 14 章

# 固件

![](img/134c18b05ee9bbbe93ba3f4335720ac1_148_0.png)

我们将讨论二进制固件以及如何使用它。

14.1 什么是固件？ . . . . . . . . . 133

14.2 加载固件 . . . . . . . . . 134

14.3 实验 . . . . . . . . . . . . . 134

## 14.1 什么是固件？

- 固件由嵌入在硬件设备中的指令和数据组成，这些对于设备的正常运行是必要的。这些二进制信息可以存储在 ROM、可重写的 EEPROM 或闪存媒体上。然而，供应商通常发现，由操作系统加载固件更廉廉且更灵活。

- 部署操作系统加载的固件与使用二进制大对象（binary blobs）之间存在一条灰色地带，对于给定的设备，哪种描述更合适通常很明确。使用固件不会导致 Linux 内核被“污染”（taint）。某些 Linux 发行版在分发需要二进制固件的驱动程序时存在问题，或者它们不发行固件本身。

- 我们将搁置从哪里获取特定设备固件的问题，因为这因设备而异。有时，你甚至必须从另一个操作系统的设备驱动程序中截取它，因为没有其他方法。

- 此外，关于固件是否应该随内核一起发布，如果不是，那么它是否应该存放在文件系统中，这个问题相当有争议，尚未完全定论。在某些情况下，它确实随内核发布；如果不是，则精确位置取决于二进制实现。对于大多数 Linux 系统，人们通常可以在 `/lib/firmware` 下找到非内核发布的固件。

## 14.2 加载固件

向驱动程序中加载固件可以通过以下方式完成：

```c
#include <linux/firmware.h>

struct firmware {
    size_t size;
    const u8 *data;
};
MODULE_FIRMWARE(filename);

int request_firmware(const struct firmware **fw, const char *filename, struct device *device);
void release_firmware(const struct firmware *fw);
```

其中 `filename` 是要加载的固件文件的名称；在任何现代 Linux 系统上，它都应该放置在 `/lib/firmware` 下。成功返回后，`request_firmware()` 将 `size` 字节放在固件结构体的 `data` 字段中。

对于连接到 PCI 等物理总线的设备，可以从相关的总线关联结构（如 `pci_dev`）轻松地获取设备结构的钩子。对于伪设备（这可能根本没有意义），在尝试加载固件之前，至少必须注册设备并填充设备结构的一些部分。固件的加载具有很强的用户态组件影响，并且在不同发行版之间有所不同。详见 `/usr/src/linux/Documentation/firmware`。

## 14.3 实验

### 实验 1：加载固件

- 编写一个从文件系统加载某些固件的模块。它应该打印出内容。为了实现这一点，你需要将固件文件放置在 `/lib/firmware` 下。你可以仅使用文本文件进行演示。

由于这是一个伪设备，你必须声明并初始化设备结构。至少你必须设置该结构中的 `dev_name` 字段，并调用 `int dev_set_name(struct device *dev, const char *fmt, ...);` 来设置设备名称，该名称可以通过方式读取：

```c
const char *dev_name(const struct device *dev);
```

（你可能想看看如果忽略其中一个操作会发生什么。）



在请求和释放固件之前，执行 `device_register(struct device *dev); device_unregister(struct device *dev);`。

# 第 15 章 内存管理与分配

我们将看到 Linux 如何区分虚拟内存和物理内存以及它们如何协同工作。我们将讨论内存区域（zone）方案。我们将考虑内存如何组织成页以及用于控制和访问页的各种算法。我们将考虑 Linux 在内核和设备驱动程序中分配内存的各种方法，区分 `kmalloc()` 和 `valloc()`，以及如何一次分配整个页或页范围。我们还考虑如何在启动时获取较大部分的内存。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_150.png)

- 15.1 虚拟内存与物理内存 135
- 15.2 内存区域 136
- 15.3 页表 137
- 15.4 kmalloc() 138
- 15.5 get_freepages() 139
- 15.6 valloc() 140
- 15.7 早期分配与启动 141
- 15.8 Slabs 和缓存分配 141
- 15.9 实验 144

## 15.1 虚拟内存与物理内存

- Linux 像所有现代操作系统一样，使用虚拟内存系统（VM）：虚拟内存比物理内存大。每个进程都有自己受保护的地址空间。当进程需要访问内存时，地址必须由内核翻译为物理地址反之亦然。
- 内核本身使用虚拟地址；然而，取决于架构和所使用的内存类型，翻译可能仅仅是偏移量。

### 内存管理与分配

在下面的图（针对 32 位平台）中，前 3 GB 虚拟地址用于用户空间内存，高 1 GB 用于内核空间内存（其他架构具有相同的设置，但 `PAGE_OFFSET` 值不同；对于 64 位平台，该值大得多）。

| | |
| :--- | :--- |
| 4 GB | 内核地址 |
| 3 GB | `PAGE_OFFSET` (C0000000) |
| 0 GB | 用户地址 |

图 15.1：用户和内核地址区域

内核允许为每个运行的进程分配公平的内存，并协调进程之间的内存共享。此外，可以使用映射将文件直接链接到进程的地址空间。此外，某些内存区域可以被保护以免写入和/或执行。

若要全面回顾《每个程序员都应该了解的内存知识》，Ulrich Drepper 在 http://people.redhat.com/drepper/cpumem.pdf 上的那篇长文深入讨论了许多问题，例如缓存的正确使用、对齐、NUMA 等。

## 15.2 内存区域

Linux 使用区域分配器算法，该算法实现在 `/usr/src/linux/mm/page_alloc.c` 中。在这种具有面向对象风格的方案中，每个区域都有自己的方法进行基本内存操作，如分配和释放内存页。共有三种内存区域：

- DMA 能力内存必须用于 DMA 数据传输。具体取决于平台；例如，在 x86 ISA 设备上，这意味着 16 MB 以下的内存。
- 高位内存（High memory）需要特殊处理，仅存在于某些平台上。它允许访问高达 64 GB 的物理内存。在 32 位 x86 上，这意味着 896 MB 及以上的内存。
- 普通内存（Normal memory）是其他所有内存。

通过查看 `/proc/zoneinfo` 可以确定每个操作区域的用法统计数据。

- 当分配内存时，内核会检查与请求相关的标志，并在此基础上构建一个可以使用的内存区域列表。当请求 `GFP_DMA` 标志时，只考虑 DMA 区域中的页。如果指定了 `GFP_HIGHMEM`，可以使用三个区域来获取空页。如果这两个标志都没有给出，则同时考虑普通区域和 DMA 区域。在没有高位内存概念的平台上，`GFP_HIGHMEM` 无影响；即所有内存都是低位内存，内存是平面的。
- Linux 允许在 32 位系统上使用高达 64 GB 的内存，每个进程的限制小于 3 GB。这是因为只有 4 GB 的地址空间（即受 32 位限制），且最高 GB 留给了内核地址。由于部分地址空间留给了内存映射设备，限制略小于 3 GB。

## 15.3 页表

- 内存被分成固定大小的页（x86 上为 4 KB）。移植代码不应依赖于特定的页大小。为了获取实际值，内核代码可以使用 `PAGE_SIZE` 宏，用户态程序可以调用 `getpagesize()` 函数。
- 对于 4K 页，虚拟地址的低 12 位包含偏移量；剩余位包含虚拟页帧号（PFN）。
- 虚拟内存的页在物理内存中可以是任意顺序的。处理器使用页表将虚拟 PFN 转换为物理 PFN。页表中的每个项都包含一个有效位、PFN 和访问控制信息。

## 15.4 kmalloc

- 如果请求的虚拟页无效，内核将产生缺页异常，然后尝试将页面调入物理内存。请求分页（Demand Paging）会不断尝试获取该页面。该页面可能已被交换到磁盘。
- 如果某个页面已被修改且空闲页不足，则该页面被标记为脏（dirty）。如果该页面对应于基于文件的数据，则会被丢弃；否则会被写入交换文件。被丢弃的页面是通过 LRU（最近最少使用）算法选择的。
- Linux 使用四级页表，尽管 32 位处理器只有两级页表。（在 2.6.10 版本之前，Linux 使用三级方案）。这允许对所有架构使用相同的函数方法；遍历多余的层级涉及穿透函数（fall-through functions）。
- 如果你在 x86 上使用 64 GB 选项，Linux 使用 PAE（物理地址扩展）机制，它提供了额外的 4 位地址空间。在这种情况下，它使用的是真正的三级方案，而不是四级。
- Linux 内核中用于分配和释放内存常用的函数是：

```c
#include <linux/slab.h>

void *kmalloc(unsigned int len, gfp_t gfp_mask);
void kfree(void *ptr);
```

- `gfp_mask` 参数的可能值详见 `/usr/src/kernel/include/linux/gfp.h`，它们可以是：

| Value | 含义 |
|---|---|
| `GFP_KERNEL` | 如果内存不可立即可用，则阻塞并进入睡眠，允许抢占发生。这是调用 `kmalloc()` 的正常方式。 |
| `GFP_ATOMIC` | 如果没有可用页面则立即返回。例如，这可能发生在从中断调用 `kmalloc()` 时，此时睡眠会阻止接收其他中断。 |
| `GFP_DMA` | 用于与 ISA DMA 设备配合缓冲区；与 `GFP_KERNEL` 或 `GFP_ATOMIC` 进行或。确保内存是连续的，并且在 x86 ISA 设备上符合 `MAX_DMA_ADDRESS=16 MB` 的限制；对于 PCI 则这是不需要的。此标志的确切含义取决于实现。 |
| `GFP_USER` | 为用户分配内存。可能会睡眠，是一个低优先级请求。 |
| `GFP_HIGUSER` | 类似于 `GFP_USER`，但从高内存分配。 |
| `GFP_NOIO` | 不用于文件系统调用，禁用 I/O 操作。 |
| `GFP_NFS` | 内部使用。 |

表 15.1：GFP 内存分配标志

- 驱动程序很少使用 `GFP_KERNEL`、`GFP_ATOMIC` 和 `GFP_DMA` 值。
- 可以使用 `in_interrupt()` 宏来检查你是否处于中断上下文或进程上下文。例如：

```c
char *buffer = kmalloc(nbytes, in_interrupt() ? GFP_ATOMIC : GFP_KERNEL);
```

## 15.5. _GET_FREE_PAGES()

另一个类似的宏 `in_atomic()` 也会检查你是否处于可抢占上下文。

> `GFP_ATOMIC` 分配允许消耗比 `GFP_KERNEL` 更多的内存资源，以减少失败几率；因此，在必要时才应使用它们。

- 要分配清零的内存，请使用 `void *kzalloc(size_t size, gfp_t flags);`，它调用 `kmalloc(size, flags)` 然后清空分配的内存区域。
- 还可以可以使用以下函数调整动态分配区域的大小：`void *krealloc(const void *p, size_t new_size, gfp_t flags);`
- `kmalloc()` 将返回匹配或超过 `len` 的 2 的幂幂的内存块。它不会清空内存，失败时返回 NULL，成功时返回内存指针。可以获得的最大分配是 1024 个页（x86 上为 4 MB）。对于稍大的请求（大于几 KB），使用 `__get_free_page()` 函数更好。
- `kmalloc()` 总是返回物理连续内存，例如 DMA 传输所需的内存。

## 15.5 - get_free_pages()

- 要一次性分配（并释放）整个内存页（或多个页），可以使用：



```c
#include <linux/mm.h>
unsigned long get_zeroed_page (gfp_t gfp_mask);
unsigned long _get_free_page (gfp_t gfp_mask);
unsigned long get_free_pages (gfp_t gfp_mask, unsigned long order);
void free_page (unsigned long addr);
void free_pages (unsigned long addr, unsigned long order);
```

- `GFP_mask` 参数的使用方式与 `kmalloc()` 相同。

- `order` 给出了页数（作为2 的幂）。限制是 1024 个页（x86 上为 4 MB）。在 `/usr/src/include/asm-generic/page.h` 中定义的函数 `get_order()` 可以根据字节数确定 `order`。

- `_get_free_pages()` 函数返回多个页长内存区域的首字节指针，且不清零该区域。注意这些页面是物理连续的。

- `_get_free_page()` 函数不清空页面；相对于 `get_zeroed_page()` 它更优，因为清空页面可能比单纯获取它要长时间。

## 15.5 - 内存管理与分配

假设你需要为一个小于一页或不是页大小倍数的对象分配内存，并且你不想通过请求页来浪费空间。假设你需要创建和销毁相同的对象，可能是数据结构或数据缓冲区。这些可能是页大小的倍数，也可能不是。无论何种情况，内核不断创建和销毁对象都是浪费的，而且不断回收部分页面导致碎片化也是浪费的。

你可以分配自己的内存池并建立自己的缓存系统，但 Linux 已经为此提供了定义的接口，并且应该这样做。Linux 使用基于已知 slab 分配器的算法。作为该方案的一部分，你可以创建一个特殊的内存池或缓存并根据需要从中添加和移除对象（所有大小相同）。如果内核在其他地方有内存，它可以动态收缩缓存，但如果缓存中仍有未使用的 slab，每当你需要时，它就不需要重新分配新对象。注意一个 slab 中可以包含多个对象，其大小是页的整数倍数。

## 15.6 vmalloc()

Linux 内核中用于分配和释放内存常用的函数是：

```c
#include <linux/slab.h>

void *kmalloc(unsigned int len, gfp_t gfp_mask);
void kfree(void *ptr);
```

## 15.7. 早期分配与 EARLY ALLOCATIONS AND BOOTMEM()

- 名称中包含 "`pages`" 的函数分配整个页；其他的不是页对齐。

- 可以释放使用这些函数分配的任何内存。然而，你已经获取了这块内存并可以运行。

- 这些函数主要用于在启动早期分配并在整个系统生命周期内都是的关键数据结构。然而，它们也可以用于其他目的。

- 以下函数创建、设置并销毁你自己的内存缓存：

```c
#include <linux/slab.h>

struct kmem_cache *kmem_cache_create (
const char *name, size_t size,
size_t offset, unsigned long flags,
void (*ctor)(void *, struct kmem_cache *, unsigned long flags),
)
int kmem_cache_shrink (struct kmem_cache *cache);
void kmem_cache_destroy (struct kmem_cache *cache);
```

# 第15章 内存管理与分配

- 这些函数创建一个类型为 `struct kmem_cache` 的新内存缓存，其中 `name` 参数用于标识它。缓存中的所有对象（可以是任何类型）长度均为 `size` 字节，且不能超过 1024 页（在 x86 架构上为 4 MB）。

- `offset` 参数表示你所分配的对象的对齐方式或在页中的偏移量；通常你会传入 0。

- `kmem_cache_create()` 的最后一个参数指向一个可选的构造函数，该函数在对象使用之前对其进行初始化；头文件中包含了关于参数的更详细信息，并且可以将标志位传递给这个极少使用的函数。

- `flags` 参数是 `/usr/src/linux/include/slab.h` 中提供的选项位掩码；主要的有：

表 15.3：内存缓存标志位

| 标志 (Flag) | 含义 |

|------|---|

| SLAB_HWCACHE_ALIGN | 强制数据对象在缓存行上对齐。这可以提高性能，但可能会浪费内存。对于关键性能代码应该设置此标志。 |

| SLAB_POISON | 将 slab 层填充为已知值 `a5a5a5a5`。这有助于检测对未初始化内存的访问。 |

| SLAB_RED_ZONE | 在分配的内存周围设置红区，当被触碰时会报警，用于检测缓冲区溢出。 |

| SLAB_PANIC | 在分配失败时导致系统崩溃（panic）。 |

| SLAB_DEBUG_FREE | 在释放对象时执行昂贵的检查 |

| SLAB_CACHE_DMA | 确保分配位于 DMA 区域。 |

- 当你的缓存部署后，`name` 将显示在 `/proc/slabinfo` 下，显示内容类似于：

```
slabinfo - version: 1.1
kmem_cache             59 78 100 2 2 1
mycache                0 1 4096 0 1 1
ip_count              0 11 352 0 1 1
tcp_tw_bucket           0 0 96 0 0 1
tcp_bind_bucket         12 113 32 1 1 1

size-8192(DMA)          0 0 8192 0 0 2
size-8192               0 1 8192 0 1 2
...
size-32(DMA)            0 0 32 0 0 1
size-32                 888 8814 32 69 78 1
```

其中标志的含义为：

- 缓存名称

- 活跃对象数量

- 总对象数量

- 对象大小

- 活跃 slab 数量

- 总 slab 数量

- 每个 slab 的页数

## 15.8. SLABS 与缓存分配

可以使用 `slabtop` 工具获取系统上各种缓存的动态交互式视图，其中元素可以以多种方式进行排序。使用 `vmstat -m` 命令也可以获得相同的信息。

现在你已经创建了内存缓存，可以使用以下函数创建与之关联的任意数量的对象，并释放它们：

```
void kmem_cache_alloc( struct kmem_cache *cache, gfp_t gfp_mask);
void kmem_cache_free( struct kmem_cache *cache, void * );
```

将你创建的缓存作为第一个参数。`gfp_mask` 参数与 `--get_free_pages()` 中的相同。（如果内存尚未存在于缓存中，它将使用这些标志位创建它）。`kmem_cache_free()` 的第二个参数直接指向你从 `kmem_cache_alloc()` 获取的内存地址。

你可以使用 `kmem_cache_shrink()` 函数来释放未使用的对象。当你不再需要内存缓存时，必须使用 `kmem_cache_destroy()` 释放它（它会先收缩缓存）；否则资源将不会被释放。如果分配到缓存的任何对象尚未释放，该函数将执行失败。

注意，还可能使用内存池（memory pool）设置一个永远不会低于特定大小的内存缓存，其 API 可以在 `/usr/src/linux/include/mempool.h` 中找到。这种内存是从正常的内存管理系统之外取的，应仅用于关键用途。

![](img/134c18b05ee9bbbe9ba3f435720ac1_158_png)

- 2.6.22 内核引入了 SLAB 分配器作为旧 SLAB 实现的替换。使用哪一个取决于编译选项；在 2.6.23 内核中，SLUB 被设为默认项。

- 新分配器减少了旧版本中的复杂性，内存占用更小，具有某些性能增强，能更好地适应 NUMA 系统，并具有更易于调试的能力。

- 最终 SLAB 可能会消失，但由于稳定缓存的重要性，这只会在 SLUB 经受住大规模测试后才会发生。事实上，还开发了 SLOB 分配器等替代方案。

## 15.9 实验

### 实验 1：内存缓存

- 扩展你的字符驱动程序，使用你自己的内存缓存来分配驱动内部缓冲区。确保释放你创建的任何 slab。

- 为了获得额外积分，请创建多个对象（可能是每次执行读或写时），并确保在销毁缓存之前释放它们。

### 实验 2：内存分配测试



- 查看使用 `kmalloc()` 和 `__get_free_pages()` 能够动态获取多少内存。

- 从请求 1 页内存开始，然后不断翻倍，直到请求失败为止。

- 确保释放你收到的任何内存。

- 你可能希望使用 `GFP_ATOMIC` 而不是 `GFP_KERNEL`。

- 如果由于碎片问题难以获取足够的内存，尝试编写一个简易的碎片器，然后重新运行。碎片器可以是一个获取所有可用内存、使用它并在完成后释放它的应用程序，从而清理缓存。你也可以尝试命令：`echo 3 > /proc/sys/vm/drop_caches`

Linux 处理用户空间和内核之间的数据传输。我们将讨论用于实现此点的各种函数，如 `put_user()`、`get_user()` 和 `copy_to_user()`。我们将考虑直接内核 I/O 以及 `get_user_pages()` 函数组，这些函数可以固定内存并提高 I/O 吞吐量。我们将讨论内存映射，并解释应用程序可以利用其优势的用户空间系统调用。我们还将检查进入字符驱动的映射入口。我们还会考虑 Relay 通道的使用。

![](img/134c18b05ee9bbbe9ba3f435720ac1_160_png)

| 章节 | 标题 | 页码 |
|---|---|---|
| 16.1 | 空间传输 | 146 |
| 16.2 | put_user/getuser() 与 copy_to_user() | 146 |
| 16.3 | 直接传输 - 内核 I/O 与内存映射 | 148 |
| 16.4 | 内核 I/O | 149 |
| 16.5 | 映射页 | 150 |
| 16.6 | 内存映射 | 151 |
| 16.7 | mmap 的用户空间函数 | 152 |
| 16.8 | mmap 的驱动入口 | 153 |
| 16.9 | Relay 通道 ** | 156 |
| 16.0 | Relay API ** | 157 |
| 16.11 | 从内核访问文件 | 159 |
| 16.12 | 实验 | 161 |

> ** 这些章节可以部分或全部作为可选内容考虑。它们包含了背景材料、特殊主题或高级课题。教师可以根据课堂经验和时间限制决定是否涵盖它们。

# 第16章 用户空间与内核空间之间的数据传输

## 16.1 空间传输

- 用户空间应用程序位于内核不同的（虚拟）内存空间。

- 当一个地址被传递给内核时，它是用户空间的虚拟地址。一个例子是 `read()` 和 `write()` 驱动入口点中的 `buf` 指针。

- 从内核内部直接访问这些指针的任何尝试都是极危险的。从原则上讲，这些地址在内核空间中可能没有意义。

- 你可能可以引用从用户空间传递的指针——如果页面被交换，灾难就会发生。这个故事的教训是，永远不要在内核空间中直接引用用户空间指针。

- 用于传输的函数执行两个不同的任务：

- 验证用户空间地址，并在页当前不在内存时处理可能发生的任何页错误。

- 在用户和内核地址之间执行拷贝。

## 16.2 PUT(GET)_USER() AND COPY_TO(FROM) USER()

- 这些函数是内核中唯一像在用户空间一样处理页错误的地方，根据访问是否合法，通过按需分页或段错误（segmentation faults）来解决。

- 这种情况仅发生在针对用户空间指针的页面上；内核永远不会交换自身使用的页面，并且始终以紧急方式分配这些页面，因此内核内存永远不会发生按需分页错误。

### access_ok()

- `type` 取决于你想在用户空间执行的操作，类型为 `VERIFY_READ` 或 `VERIFY_WRITE`。两种情况下均可使用 `VERIFY_WRITE`。

- `addr` 是要检查的地址。

- `size` 是字节计数。

- 大多数后续函数都会调用它；因此很少需要直接调用。

- 如果当前进程允许访问，返回 1 (true);失败则返回 0。

### get_user()

- 将数据从用户空间传输到内核空间。

- 将从指针 `ptr` 获取的数据赋值给 `1value`。

- 以宏的形式实现，取决于 `ptr` 的类型。

- 内部调用 `access_ok()`。

- 获取单个值。

- 成功返回 0，否则返回 `-EFAULT`。

### _get_user()

- 与 `get_user()` 相同，但不调用 `access_ok()`。在已确保安全时使用。

### put_user(), _put_user()

- 将数据从内核空间传输到用户空间。

- 与 `get_user()` 函数相同，但方向相反；将 `expr` 数据写入 `ptr` 处的用户空间。

### copy_from_user()

- 将 `len` 字节从用户空间传输到内核空间。

- 内部调用 `access_ok(ok)`。

- 还有 `__copy_from_user(to, from, len)`。

- 返回未传输的字节数。出错时，驱动程序应返回 `-EFAULT`。

### copy_to_user()

- 将 `len` 字节从内核空间传输到用户空间。

- 内部调用 `access_ok(ok)`。

- 还有 `__copy_to_user(to, from, len)`。

- 返回未传输的字节数。出错时，驱动程序应返回 `-EFAULT`。

```
strncpy(from_user(), strlen(user()), clear_user())
```

- 字符串函数的工作正如其名称所示，不同之处字符串指针位于用户空间。

- `clear_user()` 函数清除指针所指向内存位置的内容。

## 16.3 直接传输 - 内核 I/O 和内存映射

- Linux 可以使用两种互补的方法来避免使用上述的传输函数。

- 在 `kio` 方法中，内核被赋予直接访问用户空间指针的权限。在传输过程中，内存会被锁定，确保页面不会被换出且指针保持有效。传输完成后，解锁基于原始 I/O 实现。请注意，如果使用非标准的 `O_DIRECT` 标志打开文件，则对该文件将使用 `kio`。

- 在内存映射方法中，用户空间被赋予直接访问内核缓冲区权限，这些可能是直接位于设备上的内存区域。`mmap()` 调用是一个标准的 POSIX 系统调用。

- 这两种方法都避免了对传输数据的任何缓冲或缓存。它们设置和关闭之前讨论的拷贝方法需要更长时间。哪种方法最好取决于多个因素，例如传输的大小、频率、数据被重用的概率等。

## 16.4 内核 I/O

理想情况下完全跳过缓冲区和页缓存，让 I/O 操作以原始形式直接传递给设备。这消除了至少一次拷贝操作。大型数据库应用程序通常是所谓原始 I/O 操作的用户。

这可以用于锁定用户空间缓冲区并在内核中直接使用它们，而无需使用 `copy_to_user()` 和 `copy_from_user()`。

从用户空间，可以通过带有 `O_DIRECT` 标志打开文件来强制内核使用这种直接 I/O。这是一个 GNU 扩展，因此你可能需要定义：

```c
#define _GNU_SOURCE

fd = open(filename, O_DIRECT ...
```

只要使用此文件描述符，就会使用内核 I/O。下面是一个使用直接 I/O 拷贝文件的文件的短程序示例：



```c
/*
args: 1 = 输出文件, [3 = 块大小]

usage: %s outfile
*/

#define _GNU_SOURCE
#define SECTOR_SIZE 512

#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>
#include <stdio.h>
#include <malloc.h>
#include <string.h>

int main(int argc, char *argv[])
{
    char *buf;
    int fdin, fdout, rcr, rcw;
    /* 默认块 = 1 页 */
    int size = getpagesize();
    if (argc > 3)
        size = atoi(argv[3]);

    /* 打开输入文件，必须存在 */
    fdin = open(argv[1], O_RDONLY);

    /* 打开输出文件，创建或截断 */
    fdout = open(argv[2], O_DIRECT | O_RDWR | O_CREATE | O_TRUNC, 0666);

/* 使用扇区区内存 */
    buf = (char*)posix_memalign(SECTOR_SIZE, size);

    while ((rcr = read(fdin, buf, size)) > 0) {
      rcw = write(fdout, buf, size);
      printf("in = %d, out = %d\n", rcr, rcw);
      if (rcr != rcw) {
        printf("BAD values -- not sector aligned\n");
      }
    }
    close(fdin);
    close(fdout);
    exit(0);
}
```

## 16.5 映射用户页

- `get_user_pages()` 函数提供将用户空间内存暴露给内核的方法，这有助于避免额外的拷贝；在某种意义上它是内存映射的反操作（后者是将内核内存直接映射用户侧）。

- 核心函数是：

```c
#include <linux/mm.h>

int get_user_pages(struct task_struct *tsk,
                   struct mm_struct *mm,
                   unsigned long start,
                   int len,
                   int write,
                   int force,
                   struct page **pages,
                   struct vm_area_struct **vmas);
```

- 前两个参数是进程和用户空间；通常是 `current` 和 `current->mm`。

- `start` 参数给出长度为 `len`（不是字节）的用户缓冲区起始地址。如果要修改缓冲区，应设置 `write` 标志，无论权限如何，都可以设置 `force` 标志。

- 该函数的返回值是映射的页数，`pages` 参数接收指向页结构的数组。最后一个参数将填充为包含每个页的 `vm_area` 指针数组，除非它是 `NULL`。

- 该函数的典型用法可能是：

```c
down_read(&current->mm->mmap_sem);
rc = get_user_pages(current, current->mm, (unsigned long) start, npages, 0, pages, NULL);
up_read(&current->mm->mmap_sem);
```

在获取访问时对用户空间内存区域锁定。

- 需要记住，获取的是包含用户地址的 `struct page` 指针。要获取该页有用的内核地址，必须使用宏和函数：

```c
#include <linux/pagemap.h>

char *kbuf = page_address(pages[i]);

...
```

第二种形式也处理高内存情况，但必须确保完成解映射（在中断处理程序中，需要使用函数 `kmap_atomic()`、`kunmap_atomic()`，但在使用 `get_user_pages()` 时不会发生这种情况，因为你必须处于进程上下文中）。

- 注意，除非缓冲区恰好页对齐，否则只知道用户地址位于页的某个处；未提供偏移。可以使用 `posix_memalign()` 等函数产生页对齐内存，或使用感知对齐的工具（如 `dd`）。

- 还有必要清理对用户页的任何修改；否则由于跳过了虚拟内存系统可能会导致损坏。这是将修改后的页标记为脏并从页缓存中释放它们：

```c
set_page_dirty_lock(pages[i]);
page_cache_release(pages[i]);
```

## 16.6 内存映射

- 当映射文件时，文件（或其部分）可以与线性地址范围关联。对文件的输入输出操作可以通过简单的内存引用完成，而不是显式的 I/O 操作。

- 也可以在设备节点上执行，以直接访问硬件设备；在这种情况下，驱动程序必须注册并实现正确的 `mmap()` 入口。

- 该方法对于流式设备没有用。映射区域的大小必须是 `PAGE_SIZE` 的倍数，并且从页边界开始。

- 存在两种基本的内存映射：

    - 在共享内存映射中，对内存区域的任何操作完全等同于更改其代表的文件。更改会提交到磁盘（带有通常延迟），任何访问文件或映射它的进程都会看到更改。

    - 在私有内存映射中，任何更改都不会提交到磁盘，也不会被其他进程看到。这种方法效率更高，但设计上用于只读场景，或者当最终数据保存通过写入另一个文件完成时。

内存映射可能比普通的磁盘访问更有效，特别是当文件被多个进程共享时，每个进程共享访问某些页，从而最小化内存占用并加快访问速度。

## 16.7 mmap() 的用户态函数

* * 从用户侧，内存映射通过以下函数完成：

```c
#include <unistd.h>
#include <sys/mman.h>

void *mmap(void *start, size_t length, int prot, int flags, int fd, off_t offset);
int munmap(void *start, size_t length);
```

* * 这请求从 `fd` 指定的文件映射长度为 `length` 字节、从 `offset` 偏移开始的内存。偏移量必须是页的整数倍。

* * `start` 地址是映射的首选地址；如果给出 0（通常情况），`mmap()` 将选择地址并将其放入返回值。

* * `prot` 是期望的内存保护。它包含以下位：

# 表 16.2: mmap() 内存保护位

| 值 | 含义 |

| --- | --- |

| PROT_EXEC | 页面可以执行。 |

| PROT_READ | 页面可以读取。 |

| PROT_WRITE | 页面可以写入。 |

| PROT_NONE | 页面不能被访问。 |

* * `flags` 指定了映射对象的类型。它包含以下位：

# 表 16.3: mmap flags

| 值 | 含义 |

| --- | --- |

| MAP_FIXED | 如果无法使用 `start`，则失败。 |

| MAP_SHARED | 与所有其他进程共享映射。 |

| MAP_PRIVATE | 创建私有的写时拷贝映射。 |

必须指定 `MAP_SHARED` 或 `MAP_PRIVATE` 之一。记住，私有映射不会更改磁盘上的文件。任何更改在进程终止时都会丢失。

* * 可以指定其他非 POSIX 标志（参见 `man mmap.`）。特别是，`MAP_ANONYMOUS` 标志允许仅在内存中映射，而不与文件关联。

* * 这是一个使用匿名内存映射在父子进程间共享内存的简单示例：

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/mman.h>
```

## 16.8 MMAP() 的驱动入口点



```c
#include <sys/types.h>
#include <sys/wait.h>

int main(int argc, char **argv)
{
    int fd = -1, size = 4096, status;
    char *area;
    pid_t pid;

    area = mmap(NULL, size, PROT_READ | PROT_WRITE,
                MAP_SHARED | MAP_ANONYMOUS, fd, 0);

    pid = fork();
    if (pid == 0) {
        strcpy(area, "This is a message from the child");
        printf("Child has written: %s\n", area);
        exit(EXIT_SUCCESS);
    }
    if (pid > 0) {
        wait(&status);
        printf("Parent has read: %s\n", area);
        exit(EXIT_FAILURE);
    }
}

munmap(area);
```

- `munmap()` 删除映射并导致对该范围内地址的进一步引用变为无效内存引用。

- 参见 `man mmap` 获取有关错误代码的更多信息。

## 16.8 mmap 的驱动入口点

* * 从内核侧，驱动入口点如下：

```c
#include <linux/mm.h>

int (*mmap) (struct file *filp, struct vm_area_struct *vma);
```

* * `vm_area_struct` 数据结构定义在 `/usr/src/linux/include/linux/mm.h` 中，包含了重要信息。基本元素是：

```c
struct vm_area_struct {
    unsigned long vm_start;      /* vm_mm 中的起始地址 */
    unsigned long vm_end;        /* vm_mm 中的结束地址 */

    pgprot_t vm_page_prot;         /* VMA 的访问权限 */
    unsigned long vm_flags;      /* 标志，见 mm.h */

    /* 处理此结构体的函数指针 */
    const struct vm_operations *vm_ops;

    /* 关于我们的备份存储的信息 */
    unsigned long vm_pgo;      /* 文件内的偏移量（页） */
    unsigned long vm_size;       /* 映射区域的大小 */
    pgprot_t prot;               /* 此映射的保护标志 */
};
```

* * `vm_ops` 结构可以覆盖默认操作。可以为 `open()`、`close()`、`protect()`、`swapin()` 提供指针。

* * 一个示例展示了如何使用这些字段：

```c
#include <linux/mm.h>

int my_mmap(struct file *file, struct vm_area_struct *vma)
{
    if (!remap_pfn_range(vma, vma->vm_start, vma->vm_pgo, vma->vm_size, prot)) return -EAGAIN;
    return 0;
}
```

* * 大工作由 `remap_pfn()` 函数完成。注意 `pfn` 是页帧，从特定的虚拟地址获取它需要一些操作：

```c
pfn = __pa(vaddr) >> PAGE_SHIFT;
```

注意该函数允许在 32 位系统中映射超过 4 GB 的内存。

* * 如果映射的是 I/O 内存，你应该这样做：

```c
vma->vm_page_prot = pgprot_noncached(vma->vm_page_prot);
```

以防止缓存降低速度。

* * 这是一个测试 `mmap()` 入口的简单程序示例：

```c
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <fcntl.h>
#include <errno.h>
#include <sys/mman.h>

#define DEATH(msg) { perror(msg); exit(errno); }

int main(int argc, char **argv)
{
    int fd, size, rc;
    char *area, *tmp, *nodename = "/dev/mycdrv";
    char c[2] = "";

    if (argc > 1) {
        nodename = argv[1];
    }

    size = getpagesize(); /* 默认一页 */
    if (argc > 2) {
        size = atoi(argv[2]);
    }

    printf("Memory Mapping Node: %s, size of %d bytes\n", nodename, size);

    if ((fd = open(nodename, O_RDWR)) < 0) {
        DEATH("opening the node");
    }

    area = mmap(NULL, size, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);

    if (area == MAP_FAILED) {
        DEATH("error mapping");
    }

    /* 现在关闭文件 */
    close(fd);

    /* 在文件中反复放入字符串 */
    tmp = area;
    for (int j = 0; j < size - 1; j += 2, tmp += 2)
        memcpy(tmp, &c, 2);

    /* 输出文件查看是否生效 */
    rc = write(STDOUT_FILENO, area, size);

    if (rc != size) {
        DEATH("problems writing");
    }

    exit(EXIT_SUCCESS);
}
```

这是一个带有 `mmap()` 入口的简单驱动：

```c
/* 带有 mmap() 的示例字符驱动 */

#include <linux/module.h>
#include <linux/mm.h>

/* 这两个中的任一一个即可工作 * */
//#include "lab_char.h"
#include "lab_misdev.h"

static int mycdrv_mmap(struct file *file, struct vm_area_struct *vma)
{
    /* 不用管 open, release, read and write */
}static const struct file_operations mycdrv_fops = {
    .owner = THIS_MODULE,
    .mmap = mycdrv_mmap,
};

module_init(my_generic_init);
module_exit(my_generic_exit);

MODULE_AUTHOR("Jerry Cooperstein");
MODULE_DESCRIPTION("Sample Memory Map Driver Entry");
MODULE_LICENSE("GPL v2");
```

## 16.9 Relay Channels（中继通道）

* - 人需要在内核态和用户态之间传输信息，但并非所有需求都是相同的。人们可能需要或不需要双向性、效率或即时性。人们可能在有无设备驱动的情况下工作，数据量大或小。

- Relay通道接口（以前称为 relayfs）提供了一个使用某种机制的场所，该机制在方向是单向的（内核到用户）时运行非常完美。

- 对于每个通道，每个 CPU 有一个缓冲区。反之，每个缓冲区有一个或多个子缓冲区。

- 当子缓冲区填满以容纳新的数据块或消息时，将使用下一个缓冲区（如果可用）；消息永远不会拆分在子缓冲区之间（因此消息不应大于子缓冲区）。用户态可以收到子缓冲区已满通知。

- 缓冲区可以设置为覆盖模式或非覆盖模式（默认）；在后种模式下，内核客户端将阻塞，直到读者清空缓冲区。



进入`/path/to/xxx`目录，找到`xxx.json`。

当用户态应用程序通过`read()`调用访问数据时，缓冲区末尾的填充会被移除且缓冲区会被刷新。

当用户态应用程序通过`mmap()`访问数据时，整个缓冲区（包括所有子缓冲区）必须被映射，且不会刷新。这比仅使用`read`更高效，但也更复杂。

以下是可以在relay通道上使用的系统调用完整列表：

- `open()`, `close()`: 打开和关闭现有的通道缓冲区。如果没有其他进程或内核客户端仍在使用缓冲区，则通道在关闭时释放。
- `read()`: 从通道中读取字节。在非覆盖模式下，内核客户端同时写入是没问题的，但在覆盖模式下可能会发生不可预测的结果。子缓冲区的填充读者不可见。
- `mmap()`: 必须映射整个缓冲区，且没有刷新。
- `sendfile()`: 刷新一次读取。

## 16.10 Relay API

- `poll()`: 当到达子缓冲区（sub-buffer）边界时，会通知用户应用程序。支持标志位`POLLIN`、`POLLRDNORM`、`POLLERR`。

该机制的工作可以通过其他方法实现，例如`/proc`文件系统、在真实设备或伪设备上使用`ioctl()`命令、不当地使用`printk()`语句，或者最糟糕直接从内核访问日志文件；使用relay通道（relay channels）提供了一种简洁的方法。

> Relay通道在Linux内核中从未被广泛采用，它们能实现的所有功能可以通过较新的ftrace设施来实现，而该设施正有强大的持续开发支持。
>
> 因此，我们介绍这些材料是为了其教学价值，而不是作为其使用的建议。

## 16.10 Relay API

打开和关闭relay通道通过以下方式完成：

```c
#include <linux/relay.h>

struct rchan *relay_open(const char *base_filename,
	dentry *parent,
	size_t subbuf_size,
	size_t n_subbuffs,
	struct rchan_callbacks *cb,
	void *private_data);
void relay_close(struct rchan *chan);
```

这为每个CPU关联一个文件；例如，如果`base_filename = "my-chan"`，文件将被命名为`mychan0`、`my_chan1`、`my_chan2`。关联的文件将出现在`parent`指向的目录；如果为`NULL`，它们将位于文件系统的根目录。

`n_subbuffs`中的每一个缓冲区的大小为`subbuf_size`，因此缓冲区的总大小为`subbuf_size * n_subbuffs`。内核客户端发送的写入不应大于`subbuf_size`，因为它们无法分割子缓冲区。

当需要向relay通道写入时，通过以下方式完成：

```c
void relay_write(struct rchan *chan, const size_t data, size_t length);
```

信息将出现在关联的伪文件中。`relay_open()`的最后一个参数是一个回调函数表：

```c
struct rchan_callbacks {
	int (*subbuf_start, void)(struct rchan_buf *buf,
		void *subbuf,
		void *prev_subbuf,
		size_t prev_padding);
	void (*buf_mapped)(struct rchan_buf *buf,
		struct file *filp);
};
```

## 第16章 在用户空间和内核空间之间传输

```c
void (*buf_unmapped)(struct rchan_buf *buf,
      struct file *filp);
struct destroy *(*create_buf_file)(const char *filename,
      struct destroy *parent,
      int mode,
      struct rchan_buf *buf,
      int *is_global);
int (*remove_buf_file)(struct dentry *dentry);
}
```

当内存切换到新的子缓冲区时，调用`subbuf_start()`。当内存映射或取消映射时，调用`buf_mapped()`和`buf_unmapped()`。

`create_buf_file()`和`remove_buf_file()`（创建和删除）与relay通道关联的文件。注意，如果参数`is_global`不为零，则在多个CPU上只有一个文件；在这种情况下，你必须显式处理任何竞态条件。`mode`参数给出通常的权限，显然是父目录。`filename`必须由此方法创建/删除。

对于这些文件放在哪里没有先决要求。一个方便的地方是`debugfs`文件系统。

```c
static struct dentry
*create_buf_file_handler(const char *filename,
      struct dentry *parent,
      int mode,
      struct rchan_buf *buf,
      int *is_global)
{
  return debugfs_create_file(filename, parent, mode, buf,
      &relay_file_operations);
}
static int remove_buf_file_handler(struct dentry *dentry)
{
  debugfs_remove_file(dentry);
  return 0;
}
static struct rchan_callbacks relay_callbacks = {
  .create_buf_file = create_buf_file_handler,
  .remove_buf_file = remove_buf_file_handler,
};
```

其中`relay_file_operations`是在`os/kernel/relay.c`中定义的`file_operations`结构。

有额外的回调和工具函数可用于relay通道，并且可以在底层进行控制。

处理relay通道的内存操作比读取更复杂。

## 从内核访问文件

“我如何在内核中执行I/O？”是危险的，因为你不能在原子上下睡眠。

你不能使用标准的用户空间I/O函数，因为它们可能会睡眠。

你必须使用内核特定的函数，如`copy_from_user()`和`copy_to_user()`。

如果你需要访问内核文件，使用`kernel_file_read()`和`kernel_file_write()`。

映射内存空间是：



```c
#include <linux/module.h>
#include <linux/slab.h>
#include <linux/uaccess.h>

#include <linux/file>
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/relay.h>
#include <linux/delay.h>
#include <linux/atomic.h>

#define NBYTES_TO_READ 20

char *filename = "/tmp/relay_test";

static int __init_my_init(void)
{
    struct file *f;
    int nbytes, j;
    char *buffer;
    char newstring[] = "HELLO";
    buffer = kmalloc(PAGE_SIZE, GFP_KERNEL);
    printk(KERN_INFO "Trying to open file = %s\n", filename);
    f = filp_open(filename, O_RDWR, 0);

    if (IS_ERR(f)) {
        printk(KERN_INFO "error opening %s\n", filename);
        free(buffer);
        return PTR_ERR(f);
    }

    nbytes = kernel_read(f, buffer, NBYTES_TO_READ);
    printk(KERN_INFO "I read nbytes = %d, which were: %s\n", nbytes, buffer);
    for (j = 0; j < nbytes; j++) {
        printk(KERN_INFO "%c", buffer[j]);
    }

    strcpy(buffer, newstring);
    nbytes = kernel_write(f, buffer, strlen(newstring) + 1);
    printk(KERN_INFO "\n\nI write nbytes = %d, which were %s\n", nbytes, newstring);

    filp_close(f, NULL);
    free(buffer);

    return 0;
}

static void __exit_my_exit(void)
{
    printk(KERN_INFO "\nclosing up\n");
}

module_init(my_init);
module_exit(my_exit);

MODULE_LICENSE("GPL");
```

## 16.12 实验

- 实验 1：使用 `get_user()` 和 `put_user()`。

  适配你的字符驱动程序以使用 `get_user()` 和 `put_user()`。

- 实验 2：映射用户页。

  适配字符设备驱动程序，使用 `get_user_pages()` 实现 `read()` 和 `write()` 入点。

- 实验 3：映射分配的区域。

  编写一个实现 `mmap()` 入点的字符驱动程序，映射一个内核缓冲区（通常在初始化期间动态分配）。

- 实验 4：使用 relay 通道。

  编写一个内核模块，打开 relay 通道并使关联文件在 `debugfs` 中可见。当内核模块加载时，尝试使用 `mmap()` 进行读取。

# 第 17 章

# 睡眠与等待队列

我们将讨论等待队列。我们将考虑任务如何进入睡眠，以及它们如何被唤醒。我们还会考虑 `poll()` 入口点。

- 17.1 什么是等待队列？ ............................................................ 163

- 17.2 进入睡眠与唤醒 ................................................................ 164

- 17.3 进入睡眠细节 ........................................................ 166

- 17.4 排他性睡眠 ................................................................... 167

- 17.5 唤醒细节 ................................................................... 168

- 17.6 轮询 ....................................................................................... 169

- 17.7 实验 ............................................................................................. 171

![](img/134c18b05ee9bbbe93ba3f4335720ac1_178_0.png)

## 17.1 什么是等待队列？

- 当运行在内核模式下的任务达到了需要等待某些条件满足的程度时，就会使用等待队列。例如，它可能需要等待外围设备的数据到达。

- 在某些时刻，任务必须睡眠，直到它所等待的任何条件或资源可用。当资源可用或条件变为真时（可能通过中断的到达来信号），就有必要唤醒处于睡眠状态的任务。

- 系统中可以有很多个等待队列，它们以链表的形式连接。此外，一个给定的等待队列上可以放置多个一个任务。

- 理解等待队列的另一种方法是考虑任务组织和队列。所有在 `task_struct` 的 `state` 字段中状态为 `TASK_RUNNING` 的任务都有一个链表，称为 `runnable`（可运行队列）。一个被调度出去但希望在时间片可用时就立即运行的任务并没有在睡眠；它的状态仍然是 `TASK_RUNNING`。

## 第 17 章：睡眠与等待队列

睡眠任务（状态为 `TASK_INTERRUPTIBLE`、`TASK_UNINTERRUPTIBLE` 或 `TASK_KILLABLE` 的任务）会进入许多可能的等待队列之一，每个队列对应于由特定事件或一类事件的唤醒，此时睡眠任务可以回到运行队列。

睡眠和唤醒函数有两种形式：可中断的（interruptible）和不可中断的（uninterruptible）。不可中断的驱动程序不会被信号唤醒，因此应该极少使用，尤其是在设备驱动程序中。很难从这种状态挂起的任务中恢复出来；除了重启之外，可能是导致唤醒被祖先进程终止的唯一方法。

`TASK_KILLABLE` 状态只会被致命信号唤醒（而 `TASK_INTERRUPTIBLE` 会被任何信号唤醒）。它是在 2.6.25 内核中引入的。

当队列被唤醒时，等待队列上的所有任务都会被唤醒（除非使用了排他性睡眠，我们将所示）。

很容易创建一个不当使用等待队列的系统。特别是作为中断服务程序的内核执行线程永远不要进入睡眠。

等待队列使用的数据结构类型为 `wait_queue_head_t`，通常就是一个等待队列。它通过以下语句明确声明并初始化：

```c
#include <linux/sched.h>

wait_queue_head_t wq;
init_wait_queue(&wq);
```

如果等待队列不在运行时分配，则可以使用宏进行声明和初始化：

```c
DECLARE_WAIT_QUEUE_HEAD(wq);
```

不要忘记初始化等待队列。

## 17.2 进入睡眠与唤醒

现在我们已经好了等待队列，我们需要函数来让任务进入睡眠并唤醒它。这些函数是：

```c
#include <linux/wait.h>

wait_event               (wait_queue_head_t wq, int condition)
wait_event_interruptible  (wait_queue_head_t wq, int condition)
wait_event_killable      (wait_queue_head_t wq, int condition);
```

```c
void wake_up               (wait_queue_head_t *wq);
void wake_up_interruptible  (wait_queue_head_t *wq);
```

`wait_event()` 调用实际上是宏，而不是函数。它们接受 `wq` 而不是 `*wq` 作为参数。

正确的唤醒调用应该与原始信号调用配对。（然而，`wait_event_killable()` 应该与 `wake_up()` 配对，这并不显而易见。）



通常情况下你会使用可中断的等待函数，如果它们是因为唤醒调用而返回，则返回 `0`；如果它们是因为信号到达而返回，则返回 `-ERESTARTSYS`。其他形式不会被信号中止，仅供内核的关键区域使用，例如在等待从磁盘读取交换页时。

- 当你向可中断的形式发送信号时，你总是必须在唤醒后检查唤醒是因为信号到达了，还是因为有一个显式的唤醒调用。`signal_pending(current)` 宏可用于此目的。

- 条件测试有两个重要的目的：

- 它避免了竞态条件，即任务被指定进入睡眠，但在在此之前信号到达了，或者有一个显式的唤醒调用。`signal_pending(current)` 宏可用于此目的。

- 当你向可中断的形式发送信号时，你总是必须在唤醒后检查唤醒是因为信号到达了，还是因为有一个显式的唤醒调用。`signal_pending(current)` 宏可用于此目的。

（注：原文此处存在大量重复的翻译段落，根据指令“不要重复输出原文”及翻译逻辑，此处已提取核心含义翻译并精简，保持逻辑连贯。）

## 17.3 进入睡眠细节

## 17.4 独占睡眠

```c
for (;;) {
    prepare_to_wait(&wq, &_wait, TASK_INTERRUPTIBLE);
    if (condition) {
        break;
    }
    if (!signal_pending(current)) {
        schedule();
        continue;
    }
    ret = -ERESTARTSYS;
    break;
}
```

检查睡眠是否是因为传入的信号而结束，如果是，则返回值 `-ERESTARTSYS`。

- `for ()` 循环的超时变体：其中当超时期过后时，`schedule_timeout()` 会导致调度器被调用。

## 17.4 独占睡眠 (Exclusive Sleeping)

- 我们之前只处理了所谓的非独占睡眠任务。例如，可能有许多任务在等待磁盘操作完成，一旦操作完成，它们都将需要唤醒并返回。

- 如果有多个任务等待对资源的独占访问（一次时间只能由一个使用），那么这种唤醒方式是无效的，并且会导致“惊群效应”问题（`thundering herd problem`），即所有睡眠者都被唤醒，但同一时间只有一个可以使用该资源。

- 在这种情况下，需要相应的函数。设置等待会调用内联宏函数：

```c
wait_event_interruptible_exclusive (wait_queue_head_t wq, int condition);
```

（没有非中断的独占睡眠宏。）在这种情况下，将有一个睡眠者会被唤醒。如果需要控制新的唤醒函数，可以使用：

```c
void wake_up_all               ( wait_queue_head_t *wq);
void wake_up_interruptible_all ( wait_queue_head_t *wq);
void wake_up_nr               ( wait_queue_head_t *wq, int nr);
void wake_up_sync_nr          ( wait_queue_head_t *wq, int nr);
void wake_up_interruptible_nr  ( wait_queue_head_t *wq, int nr);
void wake_up_interruptible_sync_nr ( wait_queue_head_t *wq, int nr);
```

- 名字中带有 `all` 的的函数会唤醒队列中的所有任务，与非独占情况相同，但带有 `_nr` 的函数只会唤醒 `nr` 个任务（通常 `nr=1`）。

## 唤醒细节 (Waking Up Details)

所有的唤醒调用都是调用基础 `__wake_up()` 函数的宏，定义在 `/usr/src/linux/include/linux/wait.h`：

```c
#define wake_up(x)               __wake_up(x, TASK_NORMAL, 1, NULL)
#define wake_up_nr(x, nr)      __wake_up(x, TASK_NORMAL, nr, NULL)
#define wake_up_all(x)         __wake_up(x, TASK_NORMAL, 0, NULL)
#define wake_up_locked(x)      __wake_up_locked(x, TASK_NORMAL)

#define wake_up_interruptible(x) __wake_up(x, TASK_INTERRUPTIBLE, 1, NULL)
#define wake_up_interruptible_nr(x, nr) __wake_up(x, TASK_INTERRUPTIBLE, NULL)
#define wake_up_interruptible_all(x)   __wake_up(x, TASK_INTERRUPTIBLE, 0, NULL)
#define wake_up_interruptible_sync(x)   __wake_up_sync((x), TASK_INTERRUPTIBLE, 1)
```

其中

`TASK_NORMAL = TASK_INTERRUPTIBLE | TASK_UNINTERRUPTIBLE`

- 核心函数 `__wake_up()` 代码位于 `/usr/src/linux/kernel/sched.c`：

```c
void __wake_up(queue_head_t *q, unsigned int mode,
               int _exclusive, void *key)
{
    unsigned long flags;
    spin_lock_irqsave(&q->lock, flags);
    __wake_common(q, mode, int _exclusive, 0, key);
    spin_unlock_irqrestore(&q->lock, flags);
}
EXPORT_SYMBOL(wake_up);
```

它获取一个中断阻塞锁，并将工作传递给 `__wake_common()`：

```c
static void __wake_common(queue_head_t *q, unsigned int mode,
                           int _exclusive, int wake_flags, void *key)
{
    wait_queue_t *curr, next;
    list_for_each_entry(curr, next, &q->task_list, task_list) {
        unsigned flags = curr->flags;
        if (func(curr, mode, wake_flags, key) &&
            (flags & WQ_FLAG_EXCLUSIVE) && !_exclusive) {
            break;
        }
    }
}
```

- 函数遍历等待队列的链表，对于等待队列上的每个任务，它会调用唤醒函数（`curr->func()`），该函数默认设置为 `default_wake_function()`。（使用备唤醒函数的功能出现在 2.6 版本中）。之后，它会检查是否为独占，如果是，则正确地减少剩余任务的数量。默认唤醒函数反而调用 `try_to_up()`：

## 17.6 轮询 (POLLING)

```c
int default_wake_function(wait_queue_t *curr, unsigned int mode,
                           int wake_flags, void *key)
{
    return try_to_up(curr, mode, wake_flags);
}
EXPORT_SYMBOL(default_wake_function);
```

现在我们实际上执行 `try_to_up(task_t *p, unsigned int state, int sync)`，这是一个很长且复杂的函数，主要是因为需要确保任务没有在 CPU 上运行。如果它没有运行，它将状态设置为 `TASK_RUNNING`，并允许任务被重新调度。

## 17.6 轮询 (Polling)

- 应用程序监控多个描述符，以查看在任何给定时间是否可以对其中一个或多个描述符进行 I/O。

- 这种多路复用和异步 I/O 是传统的 Posix 系统调用 `select()` 和 `poll()` 的基础，Linux-epoll 系统调用在大数量描述符下的扩展性最好。它们要么坐着等待某个描述符变为活动状态，或者在其他任务工作时专门处理一个。



- 为了让 `poll()` 作用于对应于字符设备的描述符，需要在 `file_operations` 表中添加：

```c
static struct file_operations mycdrv_fops = {
    owner = THIS_MODULE,
    ...
    .poll = mycdrv_poll,
};
```

当 `mycdrv_poll(struct file *file, poll_table *wait)` 被调用时，它会检查哪些描述符就绪。它要么坐着等待某个描述符变为活动，或者在其他任务工作时专门处理一个。

为了让 `poll()` 作用于对应于字符设备的描述符，需要：

```c
static unsigned int mycdrv_poll(struct file *file, poll_table *wait)
{
    unsigned int revents = 0;
    poll_wait(file, &wq_read, wait);
    poll_wait(file, &wq_write, wait);

    if (atomic_read(&data_ready_to_read))
        revents |= POLLIN | POLLRDNORM;
    if (atomic_read(&data_ready_to_write))
        revents |= POLLOUT | POLLWRNORM;

    return revents;
}
```

当应用程序调用 `poll()` 时，会检查哪些描述符就绪。这些标志位可以组合：

### 表 17.1: poll() Flags

| 值 | 含义 |

|---|---|

| POLLIN | 设备可读，无需阻塞。 |

| POLLRDNORM | 普通数据可读。通常可读设备返回此标志位。 |

| POLLBAND | 优先级数据可读。 |

| POLLPRI | 高优先级数据可读，导致 select() 报告异常。 |

| POLLUP | 到达文件结束。 |

| POLLERR | 发生了错误。 |

| POLLOUT | 设备可写，无需阻塞。 |

| POLLWRNORM | 普通数据可写。通常可写设备返回此标志位。 |

| POLLWRBAND | 优先级数据可写。 |

## 17.7 实验 (Labs)

### 实验 1: 使用等待队列

- 将之前的字符驱动程序改进为使用等待队列，
- 让 `read()` 函数进入睡眠，直到被 `write()` 函数唤醒。（你也可以尝试反转读和写。）
- 你可能想打开两个窗口，在一个窗口读，另一个窗口写。
- 尝试让多个进程进入睡眠，即在运行写程序之前多次运行读程序。如果你记录了 PID，你应该能够检测出进程被唤醒的顺序。
- 给出了几种解决方案：
- 使用 `wait_event_interruptible()`。你可能需要对逻辑条件中使用的全局变量使用原子函数。
- 使用 `wait_for_completion()`。
- 使用信号量。
- 使用读写信号量。
- 在多读者解决方案中使用独占等待……有多少个进程被唤醒了？
- 如果你使用 `cat`、`echo` 或 `dd` 进行测试，结果可能与使用提供的简单读/写程序不同。为什么？

### 实验 2: 可杀死睡眠

- 修改 `wait_event()` 实验以使用 `wait_event_killable()`。在读取进程进入睡眠后，向它发送一个非致命信号，例如

```bash
$ kill -SIGCONT <pid>
```

随后发送一个杀杀死信号，例如 SIGKILL。

### 实验 3: 使用 poll()

- 扩展 `wait_event()` 解决方案以拥有一个 `poll()` 入口。
- 你需要一个打开设备节点并调用 `poll()` 等待数据可用的应用程序。

# 第 18 章

中断处理：延迟函数与用户驱动程序

![](img/134c18b05ee9bbbe93ba3f4335720ac1_188_0.png)

我们将继续研究 Linux 内核如何处理中断，重点关注工作如何在上半部（top halves）和下半部（bottom halves）之间分配，以及某些实现方法。我们将调查延迟函数的使用，包括 tasklets、工作队列（work queues）和内核线程旋转。我们将考虑使用的中断处理程序。最后，我们将介绍从用户空间处理中断的方法。

- 18.1 上半部与下半部 ................................ 173
- 18.2 延迟函数与 softirqs ....................... 174
- 18.3 Tasklets ............................................................... 176
- 18.4 工作队列 .......................................................... 178
- 18.5 创建内核线程 ................................... 180
- 18.6 线程中断处理程序 ................................ 181
- 18.7 用户空间中的中断处理 ....................... 182
- 18.8 实验 ................................................................. 183

## 18.1 上半部与下半部

- 高效的中断处理程序通常有上半部和下半部。
- 在上半部中，驱动程序尽可能快速完成必须完成的工作。这可能意味着确认中断并将数据从设备获取到缓冲区中。
- 从技术上说，上半部就是中断处理程序。一个典型的半部包括：
    - 检查并确保中断是由正确的硬件生成的；这对于中断共享是必要的。
    - 清除接口卡上的中断挂起位。
    - 需要立即执行的操作（通常是向设备读写某些内容）。数据通常写入或从之前分配的设备特定缓冲区中读取。
    - 设置中断下半部，驱动程序执行所有被延迟的任务。虽然在下半部运行时中断是开启的，但必要时可以禁用它们。然而，应该避免这样做，因为这违背了设置下半部的基本意图。
- 不同类型的下半部行为不同：
    - Tasklets 可以在不同的 CPU 上运行，但同一个 tasklet 一次只能运行一个。它们永远不会在进程环境中运行。Tasklets 只会在调度它们的 CPU 上运行。这导致了更好的缓存一致性和串行化，因为 tasklet 永远不会在处理程序完成之前执行，从而能更好地避免竞态条件。
    - 工作队列（Work queues）在进程环境中运行，因此允许睡眠（sleeping）。由于每个工作队列在每个 CPU 上都有自己的线程，因此睡眠不会阻塞其他任务。以这种方式实现的下半部可以在调度它的不同 CPU 上运行。
    - 取决于下半部的类型，它们以不同的方式启动：工作队列在其他任务中，而 tasklets 则在系统每处理完任何类型的异常（包括中断和系统调用）后检查是否有任何挂起的任务时就会被调用。
    - 实现下半部的另一种方法是通过维护一个内核线程。在设备初始化或打开时启动内核线程，然后它会一直睡眠，直到有工作需要处理。在唤醒线程处理工作时调度下半部，处理完后它会回到睡眠。在驱动程序卸载时使用此类线程必须非常小心。
- 不一定需要有下半部；如果需要的处理很少，直接在上半部执行可能更高效，而不是产生调度和启动下半部的开销，并且要小心处理同步问题。

示例（使用 tasklets）：

```c
static struct my_data { .... } my_fun_data;
```

```c
static void t_fun(unsigned long t_arg){ { ... }
```

```c
DECLARE_TASKLET(t_name, (unsigned long) &my_data);
```

```c
static void my_interrupt(int irq, void *dev_id)
{
    /* 执行一些操作 */
    tasklet_schedule(&t_name);
    return IRQ_HANDLED;
}
```

## 18.2 延迟函数与 softirqs

- 延迟函数在稍后（延迟的）时间尽快执行非关键任务。当函数运行时，它们可能会被中断。
- 主要有两种类型：softirqs（其中 tasklets 是其中一种类型），它们在中断上下文中运行且不允许睡眠；以及工作队列（workqueues），它们在进程环境中运行并允许睡眠。
- 有多种类型的 softirqs。按优先级从高到低排序为：

| 表 18.1: Softirq 类型 | 优先级 | 目的 |

| :--- | :--- | :--- |

| HI_SOFTIRQ | 0 | 高优先级 tasklets。 |



| `TIMER_SOFTIRQ` | 1 | 调度的定时器。 |

| `NET_TX_SOFTIRQ` | 2 | 网络包传输。 |

| `NET_RX_SOFTIRQ` | 3 | 网络包接收。 |

| `BLOCK_SOFTIRQ` | 4 | 设备工作。 |

| `TASKLET_SOFTIRQ` | 5 | 普通优先级 `tasklets`。 |

| `SCHED_SOFTIRQ` | 6 | 用于调度器。 |

| `HRTIMER_SOFTIRQ` | 7 | 使用高精度定时器时使用。 |

- 各种延迟函数的主要区别在于它们是否在进程环境中运行以及它们在多处理器系统上的行为。

| 表 18.2: 延迟函数类型 | SMP 行为 | 串行化 |
| :--- | :--- | :--- |
| `softirq` | 可以在不同的 CPU 上运行。 | 在调度它们的 CPU 上运行。 |
| `tasklet` | 可以在不同的 CPU 上运行，但不能同时运行。 | 在调度它们的 CPU 上运行。 |
| `workqueue` | 可以在任何 CPU 上运行。 | 允许延迟。 |

`Softirqs` 通过以下两种方式之一调用：

- 在处理完任何异常后，内核检查是否有任何挂起的 `softirqs`；按顺序执行它们。
- 在其他任务中调度。
- 为了防止 `softirq` 风暴，当 `softirq` 重新提交自身时需要这种机制。
- `MAX_SOFTIRQ_RESTART=1` 允许任务重启；它们被延迟。
- `__do_softirq()` 被调用以调度任务。

### 18.3 Tasklets

- `Tasklets` 用于排队稍后完成的工作。它们经常用于中断服务例程；典型的上半部完成从设备获取或写入数据并重新启用中断。
- `Tasklets` 可以在多 CPU 系统上运行。然而同一个 `tasklet` 不能在多个 CPU 上同时运行。
- `Tasklet` 总是运行在调度它的 CPU 上；除了其他，这优化了缓存使用。（但这可能会导致延迟，抵消缓存节省；可以使用工作队列代替。）结果是，许多竞态条件被自然地避免了；队列 `tasklet` 的线程必须在 `tasklet` 执行之前完成。
- `Tasklet` 的代码位于 `/usr/src/kernel/include/linux/interrupt.h`。重要的数据结构为：

```c
struct tasklet_struct {
    struct tasklet_struct *next;
    unsigned long state;
    atomic_t count;
    void (*func)(unsigned long);
    unsigned long data;
};
```

- `func` 指向要执行的函数，可以通过 `data` 传递数据。`state` 用于判断 `tasklet` 是否已经被调度；不能再次这样做。
- 主要涉及 `tasklet` 的宏和函数有：

```c
DECLARE_TASKLET(name, function, data);
DECLARE_TASKLET_DISABLED(name, function, data);

void tasklet_init(struct tasklet_struct *t, void (*func)(unsigned long), unsigned long data);

void tasklet_schedule(struct tasklet_struct *t);
void tasklet_enable(struct tasklet_struct *t);
void tasklet_disable(struct tasklet_struct *t);
void tasklet_kill(struct tasklet_struct *t);
```

- `tasklet` 在使用前必须初始化，可以通过为结构分配空间并调用 `tasklet_init()`，或者使用 `DECLARE_...` 宏，后者可以处理这两者，但它们必须在全局作用域使用。
- `tasklet_kill()` 用于杀死会重新调度自身的 `tasklets`。
- 当 `tasklet` 被调度时，会调用内联函数 `tasklet_schedule()`，其定义在 `/usr/src/linux/include/linux/interrupt.h:`：

### 15.3. TASKLETS

```
3.1: 542 static inline void tasklet_schedule(struct tasklet_struct *t)
3.1: 543
3.1: 544
    if (__test_and_set_bit(TASKLET_STATE_SCHED, &t->state))
3.1: 545
        __tasklet_schedule(t);
3.1: 546 }
```

这通过检查 `tasklet` 的状态字段来确保该 `tasklet` 已经被调度。注意，失败会导致 `tasklet` 被静默地丢弃，因为该函数没有返回值。

- *一个简单的示例：*

```c
#include <linux/module.h>
#include <linux/sched.h>
#include <linux/interrupt.h>
#include <linux/slab.h>
#include <linux/init.h>
```

```c
static void t_fun(unsigned long t_arg);

static struct simp {
    int i;
    int j;
} t_data;

static DECLARE_TASKLET(t_name, t_fun, (unsigned long)&t_data);

static int __init_my_init(void)
{
    t_data.i = 100;
    t_data.j = 200;
    printk(KERN_INFO "scheduling my tasklet, jiffies = %ld\n", jiffies);
    tasklet_schedule(&t_name);
    return 0;
}
```

```c
static void __exit_my_exit(void)
{
    printk(KERN_INFO "\nHello: unloading module\n",
           cleanup_module);
}
```

```c
static void t_fun(unsigned long t_arg)
{
    struct simp *datum;
    datum = (struct simp *)t_arg;
    printk(KERN_INFO "Entering t_fun, datum->i = %d, jiffies = %ld\n",
           datum->i, jiffies);
    printk(KERN_INFO "Entering t_fun, datum->j = %d, jiffies = %ld\n",
           datum->j, jiffies);
}
```

```c
module_init(my_init);
module_exit(my_exit);
```

## 第 18 章：中断处理：延迟函数与用户驱动程序

![](img/134c18b05ee9bbbe93ba3f4335720ac1_193_0.png)

- 之所以，是因为目前正在进行关于从 `Linux` 内核中消除 `tasklets` 的讨论。
- 首先，由于 `tasklets` 运行在软件中断模式下，你不能休眠、引用用户空间内存等，因此必须非常小心。
- 其次，由于 `tasklets` 作为软件中断运行，它们的优先级高于系统中的任何其他任务，因此如果代码编写不当，可能会导致其他任务产生不可控的延迟。
- 其主意是将几乎所有的 `tasklet` 替换为工作队列（`workqueues`），工作队列运行在可以睡眠的伪用户上下文中，并像其他任务一样被调度。一个概念性实现——使用包装器将所有 `tasklet` 转换为工作队列——并没有引起严重的问题。
- 然而，有些开发者对拟议的更改非常不满，特别是那些从事网络设备驱动程序的开发者。在这种情况下，测试会变得非常艰巨。
- 如果以历史为鉴，最可能的结果是 `tasklet` 的使用将逐渐减少，它们将在新代码中被废弃，而一些或许多旧代码将逐一转换，而不是全局转换。如果 `tasklet` 变得稀少，它们可能会在某时刻被一并消除，而无需为了它的发生而担心。

### 18.4 工作队列 (Work Queues)

- 一个**工作队列**包含一个 `tasklet` 链表，这些 `tasklet` 需要在延迟运行时（通常是越快越好）。



任务在进程上下文中运行；每个 CPU 上都会运行一个内核线程来启动它们。因此，这不仅是合法的，而且不会与在任何其他队列中运行的任务干扰。注意，你仍然无法与用户空间之间传输数据，因为没有真实的用户上下文可供访问。

与 `tasklet` 不同，工作队列上的任务可能在与调度它的进程不同的不同的处理器上运行。当不需要某些序列化（并希望最小化缓存抖动）时，它们是一个很好的选择，并且可以更快地完成延迟任务。

工作队列的代码可以在 `/usr/src/linux/include/linux/workqueue.h` 和 `/usr/src/linux/workqueue.c` 中找到。描述放入队列的任务的重要数据结构是：

```c
typedef void (*work_func_t)(struct work_struct *work);

struct work_struct {
    atomic_long_t data;
    struct list_head entry;
```

## 18.4 工作队列

```c
work_func_t func;
```

这里 `func()` 指向在工作完成后将运行的函数。其他参数供内部使用，通常不直接设置。

注意，数据条目的用法类似于 `tasklet` 的状态条目；如果请求了多个相同的工作队列，所有的第一个都将以相同的方式静默地丢弃。

## 18.6 线程化中断处理程序

创建的线程将运行 `threadfn(data)`，它将使用 `namefmt` 和任何后续参数来创建其名称，并在 `ps` 命令中显示该名称。

函数 `kthread_create()` 将进程初始化为睡眠状态；通常人们倾向于使用 `kthread_run()` 宏，它会在其之后调用：

```c
int wake_up_process(struct task_struct *task);
```

然而，人们可能想先调用 `kthread_bind()`，这会将线程绑定到特定的 CPU。

使用 `kthread_stop()` 终止线程。这会设置 `kthread_should_stop()`，唤醒线程并等待其退出。

例如，人们可能会执行如下的循环：

```c
do { ... } while (!kthread_should_stop());
```

其中循环可能会包含睡眠操作，并在该处调用 `kthread_stop()`。

内核线程只能从进程上下文中创建，因为它们的实现在现在等待资源时可能会阻塞。在原子上下文中调用将导致内核崩溃。一个旧的函数：

```c
int kernel_thread(int (*fn)(void), void *arg, unsigned long flags);
```

仍在内核的许多地方使用。它的用法更复杂，并且需要更多工作来完成终止。不应在新代码中使用它。

### 线程化中断处理程序 API

2.6.30 内核引入了编写中断处理程序的方法，其中下半部由一个调度的线程承担。此功能的出现目的是减少延迟和禁用中断的时间。

该 API 与普通中断处理程序中使用的略有不同；通过函数请求 IRQ：

```c
request_threaded_irq(unsigned int irq, irq_handler_t handler, irq_handler_t thread_fn, unsigned long flags, const char *name, void *dev);
```

新的方面是第三个参数 `thread_fn`，它本质上是一个下半部。上半部还有一个新的返回值 `IRQ_WAKE_THREAD`，在使用线程化下半部时应该使用。

因此，上半部在硬中断上下文中调用，并且必须首先检查中断是否源自其设备。如果不是，它返回 `IRQ_NONE`；否则，如果不需要进一步处理，则返回 `IRQ_HANDLED`；如果需要调用线程函数，则返回 `IRQ_WAKE_THREAD`。

## 第 18 章 中断处理：延迟函数和用户驱动程序

这种方法已用于许多设备驱动程序取代任务队列（`tasklets`）和工作队列（`work queues`），并且采用率可能会增加。如果内核使用命令行 `threadirqs` 启动，所有中断处理程序将被强制线程化，被显式标记为 `IRQF_NO_THREAD` 的那些除外。

### 18.7 用户空间中的中断处理

在用户空间编写的设备驱动程序可能具有某些优势，但显然并不是所有人都会认为这些属性的每一个都是优势。用户空间驱动使用 `ioperm()` 或 `ioper()` 函数访问 I/O 端口，或者层位于内核级驱动程序之上（例如并行、串口或 USB 端口）。例如，打印机和扫描仪驱动程序就是这种情况。

基础设施缺乏一种让用户驱动处理中断的通用方法。上述提到的驱动程序在轮询模式下工作；例如，驱动通过读取 I/O 端口每秒检查一次活动，而不是直接响应中断。

UIO 项目（用户空间 I/O）已完全集成到 2.6.23 内核中，作为处理来自用户空间中断的方法。

完整文档请参见 `/usr/src/linux/Documentation/DocBook/uio-howto.html`，或者查看从内核源码生成的 pdf：http://training.linuxfoundation.org/materials/LF331/uio-howto.pdf

创建的第一个设备将导致设备节点 `/dev/uio0` 的出现，第二个是 `/dev/uio1`……从这些设备节点进行注册将阻塞直到发生中断，并可以读取一个包含中断次数的无符号整数。对于阻塞型设备，你还可以使用 `select()`、`poll()` 并守在文件符上等待活动。

如果你只需要知道中断何时出现，仅一个用户驱动程序可能足够了。它可以使用所有可用的用户空间库和工具编写，并且不需要内核许可。

然而，很多时候你还需要编写一个短小的内核驱动程序，它可能需要执行诸如设备上的映射区域（你可以从用户空间访问）、清除设备寄存器上的中断等操作。还有一个通用的 API 用于编写 PCI 用户空间驱动程序，所有这些在之前提到的文档中都有描述。

我们应该注意，存在潜在的困难，例如在中断到达时可能丢失中断、共享中断的特殊问题，以及尝试避免大量的轮询（因为轮询会干扰中断系统中的真实同步性并可能导致不可接受的延迟）。

我们将进行练习，一方面使用 UIO 基础设施，另一方面使用特殊设备节点实现我们自己的一个。

## 18.8 实验

### 18.8 延迟函数

#### 实验 1：延迟函数

编写一个驱动程序，每当对设备进行 `write()` 操作时，就调度一个延迟函数。

将一些数据传递给驱动程序并让其打印出来。

在调度 `tasklet` 时打印 `current->pid` 字段，然后在执行队列中的函数时再次打印。

使用以下方式实现此：

- `tasklets`
- `work queues`

你可以使用在睡眠练习中使用的相同测试程序。

尝试调度多个延迟函数，看看它们是按 LIFO（后进先出）还是 FIFO（先进先出）顺序输出。如果尝试多次调度延迟函数会发生什么？

#### 实验 2：共享中断

编写一个与另一个设备共享 IRQ 的驱动程序。

使用下半部处理逻辑。

使用上半部确认中断。

使用以下方式实现此：

- `tasklets`
- `work queues`

确保你的驱动程序能够处理中断并非来自你设备的情况。



```c
/*
 * @Irqcontrol: 向 /dev/uioX 写入 0/1 时，禁用/启用中断请求（disable/enable irqs）
 */
struct uio_info {
    struct uio_device *uio_dev;
    const char         *name;
    const char         *version;
    struct uio_mem     mem[MAX_UIO_MAPS];
    struct uio_port    port[MAX_UIO_REGIONS];
    long               irq;
    unsigned long      irq_flags;
    void               *priv;
    irqreturn_t (*handler)(int irq, struct uio_info *dev_info);
    int (*mmap)(struct uio_info *info, struct vm_area_struct *vma);
    int (*open)(struct uio_info *info, struct inode *inode);
    int (*release)(struct uio_info *info, struct inode *inode);
    int (*irqcontrol)(struct uio_info *info, s32 irq_on);
};
```

你需要至少为 `name`、`irq`、`irq_flags` 和 `handler` 填充项，后者应返回 `IRQ_HANDLED`。

- 该结构体应该通过以下函数进行注册和注销：

```c
int uio_register_device(struct device *parent, struct uio_info *info);
void uio_unregister_device(struct uio_info *info);
```

- `parent` 字段应该是一个设备结构体，你需要在其中至少填充 `name` 字段并提供一个 `release()` 方法（参考你之前的固件练习），并且你应该先对该结构体调用 `device_register()`。

- 为了练习这一点，你需要编写一个简短的测试程序，该程序作用于 `/dev/uio0` 并等待中断到达，同时以 `unsigned long` 类型读取值。

# 第 19 章

# 硬件 I/O

![](img/134c18b05ee9bbbe93ba3f4335720ac1_202_0.png)

我们将看到 Linux 如何与数据总线和 I/O 端口通信、使用内存屏（memory barriers）、设备驱动如何注册和注销它们、如何进行读写操作以及如何减慢它们的速度。我们将看到如何读写内存映射设备。我们还将简要考虑如何从用户空间访问 I/O 端口。

| | | |
|---|---|---|
| 19.1 | 总线与端口 | 187 |
| 19.2 | 内存屏 | 188 |
| 19.3 | 注册 I/O 端口 | 189 |
| 19.4 | 资源管理 | 190 |
| 19.5 | 从 I/O 寄存器读写数据 | 191 |
| 19.6 | 减慢硬件 I/O 调用 ** ** | 192 |
| 19.7 | 分配和映射 I/O 内存 | 194 |
| 19.8 | 访问 I/O 内存 | 195 |
| 19.9 | 用户访问 - ioperm(), iopctl(), /dev/port | 196 |
| 19.10 | 实验 | 196 |

> ** 这些章节可以部分或全部被视为可选内容。它们包含了背景参考资料、特殊主题或高级课题。讲师可能会根据课堂经验和时间限制选择涵盖或不涵盖它们。

## 19.1 总线与端口

- 计算机需要数据路径来实现信息在处理器、内存以及各种 I/O 设备和其他外设之间的流传输。这些数据路径被称为总线（bus），有以下几种类型：
- 数据总线是一组并行传输传输的线路；在奔腾型处理器上，数据总线宽度为 64 位。
- 地址总线传输地址；在奔腾处理器上，地址总线宽度为 32 位。
- 控制总线传输控制信息，例如总线是否允许数据在 CPU 和 RAM 之间、或在 CPU 和 I/O 设备之间传输，或者是否要执行读或写操作。
- 连接 CPU 和 I/O 设备的总线称为 I/O 总线；x86 CPU 使用 32 条线来寻址 I/O 设备，并使用 8、16 或 32 条线传输数据。I/O 总线通过 I/O 接口和控制器的组合连接每个 I/O 设备。
- 总线可以是各种类型，如 ISA、EISA、PCI 和 MCA。我们将关注限制在 ISA 和 PCI。
- 控制外设设备通常涉及对寄存器进行读写。当我们谈论 I/O 端口时，指的是连续的地址和寄存器。
- 具体如何访问这些端口取决于 CPU。所有设备都连接到某种外设总线，但某些 CPU（如 x86）实际上具有不同的读写端口。I/O 总线通过 I/O 接口和控制器的组合连接每个 I/O 设备。- 控制外设设备通常涉及对寄存器进行读写。当我们谈论 I/O 端口时，指的是连续的地址和寄存器。
- 访问这些端口的具体方式取决于 CPU。所有设备都连接到某种外设总线，但某些 CPU（如 x86）实际上具有不同的读写端口。I/O 总线通过 I/O 接口和控制器的组合连接每个 I/O 设备。（*注：此处原文存在部分逻辑重复，翻译已遵循原文结构*）
- 总线可以是各种类型，如 ISA、EISA、PCI 和 MCA。我们将关注限制在 ISA 和 PCI。
- 控制外设设备通常涉及对寄存器进行读写。当我们谈论 I/O 端口时，指的是连续的地址和寄存器。
- 访问这些端口的具体方式取决于 CPU。所有设备都连接到某种外设总线，但某些 CPU（如 x86）实际上具有不同的读写端口。I/O 总线通过 I/O 接口和控制器的组合连接每个 I/O 设备。
- 总线可以是各种类型，如 ISA、EISA、PCI 和 MCA。我们将关注限制在 ISA 和 PCI。
- 控制外设设备通常涉及对寄存器进行读写。当我们谈论 I/O 端口时，指的是连续的地址和寄存器。
- 访问这些端口的具体方式取决于 CPU。所有设备都连接到某种外设总线，但某些 CPU（如 x86）实际上具有不同的读写端口。I/O 总线通过 I/O 接口和控制器的组合连接每个 I/O 设备。

（*注：原文中段落存在大量文本重复，翻译时已忠实保留了这些重复行，以确保不漏译*）

# 19.2 内存屏

- 内存屏（Memory Barriers）是确保指令执行顺序的机制。在多核或涉及硬件的编程中，CPU 或编译器可能会为了优化而重排指令，这可能导致逻辑错误。
- 内存屏主要分为：
    - `rmb`（读屏）：确保之前的读操作在之后的读写操作之前完成。
    - `wmb`（写屏）：确保之前的写操作在之后的读写操作之前完成。
    - `mb`（全屏）：同时确保读写操作顺序。
- 内存屏在驱动程序中至关重要，特别是在与硬件寄存器交互时。

## 19.3 注册 I/O 端口

- 在访问 I/O 端口之前，内核必须对它们进行注册，尽管硬件层面并没有强制执行这一机制，但这可能导致许多错误和系统崩溃。
- Linux 内核使用定义在 `/usr/src/linux/kernel/resource.c` 中的函数来请求和释放 I/O 端口：

```c
#include <linux/ioport.h>
```

```c
struct resource *request_region(unsigned long start, unsigned long len, const char *name);
void release_region(unsigned long start, unsigned long len);
```

- 在这些函数中，`start` 是 I/O 区域的起始地址，`len` 是端口或地址的数量，`name` 是出现在 `/proc/ioports` 中并声称了该区域的名称。
- 这些函数通常在初始化或卸载设备时调用。

## 第19章 硬件I/O

# 示例：

```c
#include <ioport.h>
static int my_dev_detect( unsigned long port_addr,
    unsigned long extent)
{
    if(request_region(port_addr, extent, "my_dev")
        return -EBUSY; /* 端口忙忙 */
    if(mydry_probe(port_addr,extent) != 0) {
        release_region(port_addr, extent);
        return -ENODEV /* 找不到设备 */
    }
    return 0;
}
```

## 19.4 资源管理



你可能已经注意到 `request_region()` 函数返回一个指向类型为结构的指针：

```c
struct resource {
    const char *name;
    unsigned long start, end;
    unsigned long flags;
    struct resource *parent, *sibling, *child;
};
```

它代表了一层抽象：资源是某个实体的一部分，可以独占地分配给某个设备驱动程序。在这种情况下，它是 I/O 端口的范围。

在此结构中，`name` 元素描述资源的所有者，`start` 和 `end` 元素给出资源的范围（它们的精确含义取决于资源的具体类型），`flags` 元素可以用于描述各种属性，而 `sibling` 和 `child` 字段将该结构置于资源树中，该树包含了所有相同类型的资源。

因此，所有引用 I/O 端口的项都在从 `ioport_resource` 根节点派生的树中。I/O 端口的管理可以通过以下函数完成：

```c
#include <ioport.h>
int request_resource(struct resource *root, struct resource *new);
int release_resource(struct resource *new);
```

而不是通过之前描述的 `*_region()` 函数，这些函数仅仅是 `*_region()` 函数的封装。

# 示例：

```c
#include <ioport.h>
static struct resource my_dev_resource = { "my_dev", };
static int my_dev_detect( unsigned long port_addr,
```

## 19.5 从 I/O 寄存器读写数据

```c
unsigned long end = port_addr + extent;
my_resource.start = port_addr;
my_resource.end = end;
```

```c
if (!request_resource(&ioport_resource, &my_resource)) {
    return -EBUSY;
}/* 端口忙 */
```

```c
if (mydrv_probe(port_addr, extent) != 0) {
    release_resource(&my_resource);
    return -ENODEV; /* 找不到设备 */
}
return 0;
```

对于特定的总线，有一些可选的便利函数，用于请求 I/O 资源并对其进行重映射。对于 PCI，可以使用在 `/usr/src/linux/drivers/pci/pci.c` 中定义的函数（以及函数）：

```c
int pci_request_region(struct pci_dev *pdev, int bar, const char *res_name);
int pci_request_regions(struct pci_dev *pdev, const char *res_name);
int pci_release_regions(struct pci_dev *pdev);
void pci_release_region(struct pci_dev *pdev, int bar);
```

你可以请求与设备相关的特定 `bar`（基地址寄存器），`bar` 的范围从 0 到 5，也可以请求与设备相关的所有区域。

`res_name` 参数是显示在 `/proc/iomem` 下的内容。

## 19.5 从 I/O 寄存器读写数据

下列宏定义在 `asm/io.h` 中，它们提供了单次或多次读写 8 位、16 位和 32 位端口的能力：

读取：

```c
unsigned char inb (unsigned long port_address);
unsigned short inw (unsigned long port_address);
unsigned long inl (unsigned long port_address);
void             insb (unsigned long port_address, void *addr, unsigned long count);
void             insw (unsigned long port_address, void *addr, unsigned long count);
void             insl (unsigned long port_address, void *addr, unsigned long count);
```

写入：

```c
void outb (unsigned char b, unsigned long port_address);
void outw (unsigned short w, unsigned long port_address);
```

```c
void outl (unsigned long 1, unsigned long port_address);
void outsb (unsigned port_address, void *addr, unsigned long count);
void outsw (unsigned port_address, void *addr, unsigned long count);
void outsl (unsigned port_address, void *addr, unsigned long count);
```

长长度函数仅提供 32 位操作，即使在 64 位平台上也没有 64 位的数据路径。

上述函数带有 `count` 参数，但并不是写入一个地址范围；它们只写入单个端口地址，但它们会高效地循环执行该操作。

这些函数都以小端序（little-endian）进行 I/O 操作，并进行任何必要的字节交换。

读写 I/O 端口可能需要使用内存屏（memory barriers），我们之前讨论过这些。

示例：

```c
outb(MSE_CONTROL, MSE_PORT);
dx = (inb)(MSE_PORT);
```

## 19.6 硬件 I/O

下列宏定义在 `asm/io.h` 中，提供了单次或多次读写 8 位、16 位和 32 位端口的能力：

（此处文本似乎存在重复或碎片化，保持结构）

有时，你可能会发现使用以下函数将 I/O 寄存器或端口与 I/O 内存关联起来：

```c
#include <asm-generic/iopmap.h>
void iomap(unsigned long io_port, unsigned int count);
void ounmap(void *addr);
```

通过使用这些函数，I/O 端口显示为内存。在此之前通常会请求这些端口。完成后，可以使用后续讨论的读写函数进行访问。

## 19.7 分配与映射 I/O

非平凡设备几乎总是通过内存访问。具体的访问方式取决于架构。然而，Linux 通过通用接口处理了这种依赖。

使用这些区域有三个基本步骤：请求、重映射以及使用相应的读写函数。

在使用此类内存区域之前，必须请求（并最终释放）：

```c
struct resource *request_mem_region(unsigned long start, unsigned long len, char *name);
void release_mem_region(unsigned long start, unsigned long len);
```

这些函数作用于设备，从地址延伸，并使用名称描述在 `/proc/mem` 中创建的条目。起始地址是设备的特性；例如，PCI 设备可以从配置寄存器读取，或从函数 `pci_resource_start()` 获取。

你不能直接使用起始地址的指针；相反必须对其进行重映射并最终取消：

```c
#include <linux/iopmap.h>
void iomap(unsigned long phys_addr, unsigned long size);
void ounmap(void *addr);
```

一旦有了特定总线的可选便利函数，例如：

```c
void pci_iomap(struct pci_dev *dev, int bar, unsigned long maxlen);
void pci_iounmap(struct pci_dev *dev, void *iomem *addr);
```

定义在 `/usr/src/linux/lib/iopmap.c` 中。

注意这些函数并不请求内存区域，那必须单独完成。

## 19.8 访问 I/O 内存

对重映射的 I/O 内存进行读写可以通过以下函数实现：



```c
#include <linux/io.h>

unsigned int iread8 (void *addr);
unsigned int iread16 (void *addr);
unsigned int iread32 (void *addr);

void iowrite8 (u8 val, void *addr);
void iowrite16 (u16 val, void *addr);
void iowrite32 (u32 val, void *addr);
```

`addr` 参数应该指向通过 `ioremap()` 获取的地址（带有物理地址偏移量），读取函数返回读取到的值。

多次读写可以使用以下函数完成：

```c
void iread8_rep (void *addr, void *buf, unsigned long count);
void iread16_rep (void *addr, void *buf, unsigned long count);
void iread32_rep (void *addr, void *buf, unsigned long count);

void iowrite8_rep (void *addr, void *buf, unsigned long count);
void iowrite16_rep (void *addr, void *buf, unsigned long count);
void iowrite32_rep (void *addr, void *buf, unsigned long count);
```

这些函数是对特定地址进行 I/O 操作，而不是针对地址范围，即从指向的内核地址读取或向其写入。

64 位架构也有 64 位的读写操作，函数如下：

```c
u64 readq (unsigned long address);
void writeq (unsigned long val, unsigned long address);
```

其用法非常显而易见，其中 `q` 代表 quad（四字节）。目前还没有 `iread64()` 和 `iowrite64()` 函数。

直接操作内存块可以使用以下函数：

```c
void memset_io (void *addr, u8 val, unsigned int count);
void memcpy_io (void *dest, void *source, unsigned int count);
void memcpy_to_io (void *dest, void *source, unsigned int count);
```

上述函数以小端序进行 I/O 操作，并进行任何必要的字节交换，`memmove` 除外，它仅处理字节流且不进行任何交换。

旧的 I/O 函数：

```c
unsigned char readb (unsigned long address);
unsigned short readw (unsigned long address);
unsigned long readl (unsigned long address);
```

```c
void writeb (unsigned char val, unsigned long address);
void writew (unsigned short val, unsigned long address);
void writel (unsigned long val, unsigned long address);
```

这些函数已经过弃，尽管它们仍然可以使用。它们不如新函数那样安全，因为它们没有进行足够彻底的类型检查。

## 19.9 用户态访问 - `ioperm()`, `iopl()`, `/dev/port`

- I/O 端口也可以从用户空间访问。这是一种常用于用户态驱动程序（如 X Server）的技术。执行此类操作的应用必须以 root 权限运行。因此，从稳定性和安全角度来看是危险的。

- 一方法是使用函数：

```c
#include <sys/io.h>

int ioperm(unsigned long from, unsigned long num, int turn_on);
int iopl(int level);
```

- `ioperm()` 获取单个端口的权限，范围从端口地址 `from` 开始的 `num` 个字节，如果 `turn_on = 1` 则启用。

- 前 `0x3ff` 个端口可以通过这种方式访问；对于较大的值，你必须使用 `iopl()`，它赋予对整个 I/O 空间的权限。

参数范围从 0 到 3。小于或等于该值的 Ring 级别将获得 I/O 端口的访问权限；因此，`level=3` 的值允许普通用户应用（在 Ring 3 中）访问 I/O 端口。

- 使用这些设施时，可以在用户空间使用 `inb()`、`outb()` 函数。这需要在开启优化的情况下进行编译，以确保内联函数的展开。

- 另一种方法是使用 `/dev/port` 设备节点。只需跳转到正确的偏移量并使用普通的读写函数即可。这个后门被认为相当危险，但经常在遗留应用程序中使用。

## 19.10 实验

### 实验 1：从用户空间访问 I/O 端口

- 查看 `/proc/ioports` 以找到一个空闲的 I/O 端口区域。一种可能性是使用第一个并行端口（通常在 `0x378`），你应该能够向基地址处的寄存器写入 0，并读取寄存器获取状态信息。

- 使用两种方法尝试对这些端口进行读写：

  - `ioperm()`

  - `/dev/port`

### 实验 2：访问 I/O 端口

- 查看 `/proc/ioports` 以找到一个空闲的 I/O 端口区域。

- 编写一个简单的模块来检查该区域是否可用并请求它。

- 检查并确认该区域已在 `/proc/ioports` 中正确注册。

- 完成后确保释放该区域。

- 模块应该向该区域发送一些数据，并从中读取一些数据。值是否一致？如果不一致，原因是什么？

- 注意：给出了两种解决方案，一种针对旧的区域 API，另一种针对较新的资源 API。

### 实验 3：重映射 I/O 端口

- 修改你的解决方案，使用 `ioremap()` 和正确的读写函数。

### 实验 4：串口鼠标驱动程序

- 将使用 Microsoft 协议的通用串口鼠标连接到空闲的串口。

- 根据你选择的串口，你需要知道相关的 IRQ 和基寄存器地址；即：

表 19.2：串口鼠标节点和寄存器

| 端口 | 节点 | IRQ | IOPORT |
|---|---|---|---|
| com1 | `/dev/ttyS0` | 4 | `0x03f8-0x03ff` |
| com2 | `/dev/ttyS1` | 3 | `0x02f8-0x02ff` |
| com3 | `/dev/ttyS2` | 4 | `0x03e8-0x03ef` |
| com4 | `/dev/ttyS3` | 3 | `0x02e8-0x02ef` |

- 你需要查看鼠标的手页，其中部分提到：

  Microsoft protocol

Microsoft 协议使用 1 位起始位和 7 位数据位。

# 第 20 章. PCI

子系统：ASUSTEK Computer Inc. 未知设备 `82d3`

标志：总线主，快速 devsel，延迟 0

能力：`[e0]` 厂商特定信息

`00ia:1.7` USB 控制器：Intel Corporation 82801JI (ICH10) 家族 Usb22 EHCI 控制器 #2 (prog-if 20 [EHCI])

子系统：ASUSTEK Computer Inc. 未知设备 `82d4`

标志：总线主，中等 devsel，延迟 0，IRQ 18

内存位于 `9ffffc00` (32位，非预取) [size=1K]

能力：`[50]` 电源管理版本 2

能力：`[58]` 调试端口

能力：`[98]` 厂商特定信息

`02:00.0` 以太网控制器：Marvell Technology Group Ltd. 82E8056 PCI-E 千兆网网控制器 (rev 12)

子系统：ASUSTEK Computer Inc. 未知设备 `81f8`

标志：总线主，快速 devsel，延迟 0，IRQ 29

内存位于 `fe9f6c00` (64位，非预取) [size=16K]

I/O 端口位于 `c800` [size=256]

扩展 RUM位于 `fe9c0000` [已禁用] [size=128K]

能力：`[48]` 电源管理版本 3

能力：`[50]` 关键产品数据

能力：`[55]` 消息信号中断：64bit+ Queue=0/0 已启用

能力：`[e0]` Express  legacy端点 IRQ 0

能力：`[100]` 高级错误报告

`01:00.0` VGA 兼容控制器：nvidia Corporation GeForce 8400 GS (rev a) (prog-if 00 [VGA 控制器])

子系统：ASUSTEK Computer Inc. 未知设备 `8278`



标志：总线主，快速 devsel，延迟 0，IRQ 16

内存位于 `fd0000000` (32位，非预取) [size=16M]

内存位于 `d00000000` (64位，非预取) [size=256M]

内存位于 `fa0000000` (64位，非预取) [size=32M]

I/O 端口位于 `c800` [size=128]

[虚拟] 扩展 RUM位于 `fe6c0000` [已禁用] [size=128K]

能力：[60] 电源管理版本 3

能力：[68] 消息信号中断：64bit+ Queue=0/已启用

能力：[78] Express Endpoint IRQ 0

能力：[100] 虚拟通道

能力：[128] 电源预算

能力：[600] 未知 (11)

# 表 20.1：PCI 特性

| 总线号： | 允许 256 个，但大多数 PC 只有几个。 |

| 设备号： | 每个总线最多可以有 32 个设备。 |

| 功能号： | 每个设备最多可以有 8 个功能。 |

- 注意用于标识 PCI 设备的前三个字段：
- 每个设备的信息都源于其配置寄存器，这是板 上的一个 256 字节的空间，在启动和 PCI 总线初始化期间进行读取。（PCI Express 将配置寄存器增加到 4096 字节。）

## 20.1. 什么是 PCI？

| 31 | 16 15 | 0 |
|---|---|---|
| 设备 ID | 厂商 ID | 00h |
| 状态 | 命令 | 04h |
| 类代码 | 版本 ID | 08h |
| BIST | 头部类型 | 延迟计时器 | 缓存行 5. | 0Ch |
| | | | | 10h |
| | | | | 14h |
| | | | | 18h |
| 基地址寄存器 | | | | 1Ch |
| | | | | 20h |
| | | | | | 24h |
| 子系统 ID | 子系统厂商 ID | 2Ch |
| 扩展 ROM 基地址 | | 30h |
| 预留 | 能力指针 | 34h |
| 预留 | | 38h |
| 最大延迟 | 最小授权 | 中断引脚 | 中断线路 | 3Ch |

图 20.1：PCI 配置空间

- 在 Linux 下，PCI 设备的检测是在启动时完成的；配置寄存器被定位，其内容以数据结构链表的形式的形式放置在内存中。（我们在本次讨论中排除了热插拔设备）
- 当 PCI 系统启动时，设备最初没有内存、I/O 端口、IRQ 或分配。系统 BIOS 在驱动程序访问这些资源之前，会为这些资源寻找安全的分配；然后就可以从配置寄存器中获取它们。设备上的任何固件都会在 BIOS 扫描后被读取。
- 通过查看 sysfs 可以轻松获取总线上的设备视图。例如，选择第六个总线、第三个设备槽、第一个功能：

```
$ ls -lF /sys/bus/pci/devices/0000:05:02.0
total 0
--r-xr--r-- 1 root root 4096 May 27 07:15 broken_parity_status
-rwxr-xr-x 1 root root 0022 May 27 02:14 bus -> ../../..//bus/pci/
--r-xr--r-- 1 root root 4096 May 27 07:15 class
```

```
-rw-r--r-- 1 root root      256 May 27 07:15 config
-rw-r--r-- 1 root root      4096 May 27 07:15 device
lrwxr-xr-x 1 root root           0 May 27 07:14 driver -> \
                                     ../../../../bus/pci/drivers/skge/
-rw-r--r-- 1 root root      4096 May 27 07:15 enable
-rw-r--r-- 1 root root      4096 May 27 07:15 irq
-rw-r--r-- 1 root root      4096 May 27 07:15 local_cpist
-rw-r--r-- 1 root root      4096 May 27 07:15 local_cpus
-rw-r--r-- 1 root root      4096 May 27 07:15 mediaslist
-rw-r--r-- 1 root root      4096 May 27 07:15 msi_bus
lrwxr-xr-x 1 root root           0 May 27 07:15 net_eth0 ->
                                     ../../../../class/net/eth0/
drw-xr-x 2 root root           0 May 27 07:15 power/
-rw-r--r-- 1 root root           0 May 27 07:15 resource
-rw-r--r-- 1 root root     16384 May 27 07:15 resource
-rw-r--r-- 1 root root       256 May 27 07:15 resource
```

- PCI 设备可能有许多不同类型，例如网络设备、字符设备或块设备。除了注册为 PCI 设备外，它还必须作为其特定类型的设备进行注册。
- 这通常在 `probe()` 回调函数中完成，在该函数中调用如 `register_netdev()` 等函数。
- 同样，`shutdown()` 回调函数会使用 `unregister_netdev()` 等函数取消设备的注销。

## 20.3 定位 PCI 设备

头文件 `/usr/src/linux/include/pci.h` 为 PCI 函数使用的数值、区域位置和值定义了符号化名称。头文件 `/usr/src/linux/include/linux/pci_ids` 包含了特定于设备和厂商的定义，并被包含在 `pci.h` 中。

描述 PCI 设备的基础结构体类型定义在 `/usr/src/linux/include/linux/pci.h` 中的 `pci_dev`。这是一个很长的结构体，我们在这里不需要深入其细节。

可以通过以下方式定位设备：

```c
#include <linux/pci.h>

struct pci_dev *pci_get_device(unsigned int vendor, unsigned int device,
struct pci_dev *from);
struct pci_dev *pci_get_dev_reverse(unsigned int vendor, unsigned int device,
struct pci_dev *from);
struct pci_dev *pci_get_dev_class(unsigned int class, struct pci_dev *from);
```

以及其他一些函数

`pci_get_device()` 函数请求有关设备的信息。如果 `vendor`/或 `device` 被指定为 `PCI_ANY_ID`，则匹配所有设备。在初始化设备链之前，应该将 `from` 的值设置为 `NULL`。这些函数通常在循环中调用。如果 `from` 在开始时被设置为 `NULL`，则它将在结束时返回 `NULL`。

如果这些函数的返回值不是 `NULL`，则返回描述设备的结构体，并增加设备的引用计数。当设备释放时（例如在卸载模块时），必须调用函数：

```c
void pci_dev_put(struct pci_dev *dev);
```

用以减少引用计数；否则，如果该设备支持热插拔，则无法从系统中移除。

记住，在找到设备后，在对其进行任何操作之前，您需要调用函数 `pci_enable_device(struct pci_dev *dev)` 来启用它。

## 20.4 访问配置空间

### 示例：

- 定位并启用一个特定的设备：

```c
#include <linux/pci.h>

struct pci_dev *pdev = NULL;

if (!pci_get_device(PCI_VENDOR_ID_INTEL, PCI_DEVICE_ID_INT_1682, &pdev))
    return -ENODEV;
pci_enable_device(pdev);
```

- 如果需要，可以调用函数

```c
char *pci_name(struct pci_dev *pdev)
```

来获取总线、设备号和函数号。它不是通过探测硬件来实现，而是通过遍历已存在的设备列表来实现。

- 还可以使用宏：

```c
struct pci_dev *pdev;
for_each_pci_dev(pdev) { ... }
```



来遍历所有 PCI 设备。

## 20.4 访问配置空间

- 可以通过 8 位、16 位或 32 位数据传输访问配置空间。

```c
int pci_read_config_byte(struct pci_dev *dev, u8 where, u8 *val);
int pci_read_config_word(struct pci_dev *dev, u8 where, u16 *val);
int pci_read_config_dword(struct pci_dev *dev, u8 where, u32 *val);
int pci_write_config_byte(struct pci_dev *dev, u8 where, u8 *val);
int pci_write_config_word(struct pci_dev *dev, u8 where, u16 *val);
int pci_write_config_dword(struct pci_dev *dev, u8 where, u32 *val);
```

- 这些函数从由 `dev` 标识的设备配置空间读取或写入。从配置空间起始位置的偏移量由 `where`。
- 注意类型 `u8`、`u16`、`u32`、`u64` 的使用。这些是在必须精确匹配位数时使用的内核无符号类型（有符号类型 `s8`、`s16`、`s32`、`s64` 很少使用）。你也可以在用户空间使用这些类型，只要在前面加上双下划线（例如 `_u32`）并包含 `linux/types.h`。
- 根据 PCI 标准，配置寄存器中的多字节项采用小端（little-endian），这是 x86 平台的约定。上述数据类型和函数会透明地处理任何字节序，当在像 SPARC 这样的大端（big-endian）系统上时，因此无需担心位顺序。但你应该意识到这一点。`word` 和 `dword` 函数会处理字节序问题（注意某些架构，如 alpha 和 IA64 实际上是双端的，可以配置为任意一种模式）。
- 配置变量使用在 `/usr/src/linux/include/linux/pci.h` 中定义的符号名称访问，或者使用：
`pci_read_config_byte(dev, PCI_REVISION_ID, &revision);`
- 也可以使用实用程序获取配置寄存器中的值。

## 20.5 访问 I/O 和内存空间

- 如所述，你不仅可以访问配置寄存器，还可以访问与 PCI 设备相关的 I/O 端口和内存区域。虽然可以在配置寄存器中寻找这些资源，但使用内核提供的通用资源管理函数更为简单。
- 相关函数有：

```c
unsigned long pci_resource_start(struct pci_dev *, int bar);
unsigned long pci_resource_end(struct pci_dev *, int bar);
unsigned long pci_resource_len(struct pci_dev *, int bar);
unsigned long pci_resource_flags(struct pci_dev *, int bar);
```

`bar` 代表基地址寄存器（Base Address Register）。
- 前两个函数返回 PCI 资源的起始地址和结束地址，第三个函数返回长度。`bar` 参数代表基地址寄存器。
- 最后一个函数返回 PCI 标志，定义在 `/usr/src/linux/include/ioport.h` 中。
- 这是一个使用 `ioport.h` 的示例：

```c
static int 139_init(struct pci_dev *pdev) {
    rc = pci_enable_device(pdev);
    if (rc)
        goto out;
    mmio_start = pci_resource_start(dev, 0);
    mmio_end = pci_resource_end(dev, 0);
    mmio_flags = pci_resource_flags(dev, 0);
    mmio_len = pci_resource_len(dev, 0);
```

## 20.6 PCI Express

- PCI 于 1991 年引入，尽管有了如 PCI-X 等增强，但已显出老态。特别是其总带宽被限制在 133 MB/s。
- PCI Express（通常称为 PCIe）于 2004 年引入，并正在逐渐取代 PCI。AGP（加速图形接口）已从主板上消失。
- PCIe 的主要优势是点对连接，带宽不再是共享的。

## 20.7 实验

- 根据 PCI 标准，配置寄存器中的多字节项采用小端序，这是 x86 平台的约定。
- PCI 卡将取决于插槽的大小；例如，x4 和 x8 插槽也符合标准。
- 为 PCI 编写的设备驱动在 PCIe 上也能正常工作，其设计尽可能减少了干扰。

### 实验 1：PCI 工具

`pciutils` 软件包 (`http://www.ucw.cz/pciutils.html`) 包含以下工具：
- `lspci` 显示 PCI 总线及连接设备的信息。
- `setpci` 评估和配置 PCI 设备属性。
- `update-pciids` 获取最新的 PCI ID 数据库并安装到系统中。
- 运行 `update-pciids` 更新你的数据库。如果失败，可以从 `http://pci-ids.ucw.cz/` 获取。下载的文件（`pci.ids`）的位置取决于你的发行版，但通常位于 `/usr/share` 下（输入 `pci.ids` 可以得知）。
- 通过 `lspci` 获取更多基础信息。你可以通过 `man lspci` 或 `lspci-help` 获取详情。例如，要使用系统中所有 Intel 设备的冗余信息，你可以输入 `lspci -vv -d 8086::*`；对于 AMD 设备使用 `lspci -vd -d 1022*:`。尝试 `-x(xx)` 选项获取配置寄存器的详细转储。
- 使用 `setpci` 评估或更改配置寄存器的特定值。如果你可以通过 `setpci -vd -d 1022*: DEVICE_ID` 找到系统中所有 Intel 设备的标识符，`-d` 选项可以防止实际更改。查看帮助页获取更改配置寄存器条目的示例。

### 实验 2：PCI 设备

- 编写一个模块扫描你的 PCI 设备并收集相关信息。
- 对于每个设备，从其配置寄存器读取某些信息。（请确保你读取了 `/usr/src/include/linux/pci.regs.h` 和 `/usr/src/include/linux/pci.ids.h` 以获取符号名称。）你可能想要的字段包括：`PCI_VENDOR_ID`、`PCI_DEVICE_ID`、`PCI_REVISION_ID`、`PCI_INTERRUPT_LINE`、`PCI_LATENCY_TIMER`、`PCI_COMMAND`。
- 你获得的信息应该与从 `lspci` 获取的一致。

# 第21 章

## 平台驱动

![](img/134c18b05ee9bbbe93ba3f4335720ac1_224_0.png)

我们将讨论平台驱动。

| | | |
| :--- | :--- | :---: |
| 21.1 | 什么是平台驱动？ | 209 |
| 21.2 | 主要数据结构 | 210 |
| 21.3 | 注册平台设备 | 211 |
| 21.4 | 示例 | 211 |
| 21.5 | 硬编码平台数据 | 215 |
| 21.6 | 新方法：设备树 | 216 |

** 这些章节可以部分或全部被视为可选内容。它们包含了背景参考材料、专门主题或高级课题。讲师可能会根据课堂课堂经验和时间限制，选择涵盖或不涵盖这些内容。

## 什么是平台驱动？

- 位于已知总线（如 PCI 和 USB）上的设备在统一设备模型（Unified Device Model）中有定义定义的方法，用于在它们通过热插拔机制连接或断开，或者在系统启动期间被发现时声明自己。
- 然而，许多现代 SoC（系统级芯片）可能已经内置了主机控制器等设备，并且不会以相同的方式向内核告知它们的存在。通常，此类设备可以通过 CPU 总线进行直接寻址，虽然它们很少通过其他类型的总线段连接，但它们的寄存器仍然是可以直接寻址的。
- 为了处理这些设备，Linux 使用了平台驱动接口（platform driver interface），该接口连接并类似于统一设备模型，并允许设备的虚拟添加和删除。每个设备都有一个唯一的名称并且是可以配置的。
因此，平台总线（platform bus）可以被理解为伪总线，既适用于 SoC 上的集成外设，也适用于没有像 PCI 或 USB 等主要维护规范的遗留互连。

## 21.2 主要数据结构



主要的数据结构和方法在 `/usr/src/linux/include/linux/platform_device.h` 中，其中 `platform_device` 结构描述了设备：

```c
struct platform_device {
    const char *name;
    int id;
    struct device dev;
    u32 num_resources;
    struct resource *resource;

    const struct platform_device_id *id_entry;
    /* MFD cell 指针 */
    struct mfd_cell *mfd_cell;

    /* 体系特定添加 */
    struct pdev_archdata archarchdata;
};
```

并且包含指向适当设备结构的指针。

`platform_driver` 结构描述了驱动：

```c
struct platform_driver {
    int (*probe)(struct platform_device *);
    int (*remove)(struct platform_device *);
    void (*shutdown)(struct platform_device *);
    int (*suspend)(struct platform_device *, pm_message_t state);
    int (*resume)(struct platform_device *);
    struct device_driver driver;
    const struct platform_device_id *id_table;
};
```

并且包含指向适当设备结构的指针。

注意，对于 PCI 设备，有宏定义可以在连接的设备和 `platform_device` 结构之间切换：

```c
#define platform_device_get_id(pdev) (pdev)->id_entry

#define to_platform_device(dev) container_of((dev), struct platform_device, dev)
```

与统一驱动模型框架中的其他设备一样，虽然设备的发现和枚举是在实际驱动之外完成的，但必须提供 `probe()` 和 `remove()` 方法以及通常的电源管理函数。特别重要的是，`probe()` 方法必须验证硬件确实存在，因为平台代码始终可以确定这一点。

## 21.3 注册平台设备

- 在填充 `platform_driver` 结构后，通过以下方式自注册/注销：

```c
int platform_driver_register(struct platform_driver *);
void platform_driver_unregister(struct platform_driver *);
```

在设备不可热插拔的情况下，可以使用：

```c
int platform_driver_register(struct platform_driver *driver, int (*probe)(struct platform_device *));
```

- 使用以下方式枚举设备：

```c
int platform_device_register(struct platform_device *);
void platform_device_unregister(struct platform_device *);
platform_device_add(struct platform_device **);
```

注意 `module_init` 的使用，因为此驱动必须被加载。

- `platform_driver` 结构通过以下内容填充：

- 指向底层 `device_driver` 结构的指针，包含一个唯一名称 `"pwm"`。

- 一个探测函数 `pwm_probe()`，我们将查看它。

- 一个移除函数 `pwm_remove()`，它被标记为 `__exit`，其作用仅仅是当驱动被编译掉时丢弃该代码。

- 一个 `platform_device_id_table`，`pwm_id_table`：

```c
static const struct platform_device_id pwm_id_table[] = {
    /* has_secondary_pwm */
    { "pwm2x", 0},
    { "pwm27", 0, HAS_SECONDARY_PWM },
    { "pwm68", 1},
    { "pwm90", 1},
};
MODULE_DEVICE_TABLE(platform, pwm_id_table);
```

它指定了驱动程序可以处理的设备，与 `pci_id_table` 具有相同的作用等。让我们来看看 `probe` 函数，它显然非常重要。首先是一个指向 `device_id` 表的指针：

```c
static int __init_pwm_probe(struct platform_device *pdev) {
    const struct platform_device_id *id = platform_get_device_id(pdev);
    struct platform_device *pwm, *secondary = NULL;
    struct resource *res;
    int ret = 0;
}
```

然后分配一个 `pwm_device` 结构（局部于驱动）：

```c
struct pwm_device {
    struct list_head node;
    struct platform_device *secondary;
    struct platform_device *pdev;

    const char *label;
    struct clk *clk;
    int clk_enabled;
    void __iomem *mmio_base;

    unsigned int use_count;
    unsigned int pwm_id;
};
```

然后使用 `clk_get()` 获取时钟引用，然后它必须被启用：

```c
pwm = kzalloc(sizeof(struct pwm_device), GFP_KERNEL);
if (pwm == NULL) {
    dev_err(&pdev->dev, "failed to allocate memory\n");
    return -ENOMEM;
}

pwm->clk = clk_get(&pdev->dev, NULL);
if (IS_ERR(pwm->clk)) {
    ret = PTR_ERR(pwm->clk);
    goto err_free;
}
```

## 21.4 示例

```c
pwm->clk_enabled = 0;
```

接下来初始化使用计数，填充一些结构，并调用 `platform_get_resource()` 和 `mem_region()` 来访问 I/O 内存：

```c
pwm->use_count = 0;
pwm->pwm_id = id->driver_data;
pwm->pdev = pdev;
r = platform_get_resource(pdev, IORESOURCE_MEM, 0);
if (r == NULL) {
    dev_err(&pdev->dev, "no resource defined\n");
    ret = -ENODEV;
    goto err_free_clk();
}
```

I/O 内存随后映射到一个可以使用的地址：

```c
pwm->mmio_base = ioremap(r->start, resource_size(r));
if (pwm->mmio_base == NULL) {
    dev_err(&pdev->dev, "failed to imap\n");
    ret = -ENODEV;
    goto err_free_mem;
}
```

此特定设备可能有一个次级：



```c
if (id->driver_data & HAS_SECONDARY_PWM) {
    secondary = kzalloc(sizeof(struct pwm_device), GFP_KERNEL);
    if (secondary == NULL) {
        ret = -ENOMEM;
        goto err_free_mem;
    }
    *secondary = *pwm;
    pwm->secondary = pdev;

    /* 第二个 PWM 偏移 0x10 的寄存器 */
    secondary->mmio_base = pwm->mmio_base + 0x10;
    secondary->pwm_id = pdev->id + 2;
}
```

现在我们准备好添加设备了：

```c
_add_pwm(pwm);
if (secondary)
    _add_pwm(secondary);
```

## 第21章 平台驱动

```c
3.1: 240    platform_set_drvdata(pdev, pwm);
3.1: 241      return 0;
3.1: 242
3.1: 243
3.1: 244  err_free_mem:
3.1: 245      release_mem_region(r->start, resource_size(r));
3.1: 246  err_free_clk:
3.1: 247      clk_put(pwm->clk);
3.1: 248  err_free:
3.1: 249      kfree(pwm);
3.1: 250      return ret;
3.1: 251 }
```

注意通过 `platform_set_drvdata()` 对嵌入在底层设备结构中的私有数据 `data_driver` 字段进行设置。`_add_pwm()` 函数将设备添加到设备设备链表中：

```c
3.1: 170 static inline _add_pwm(struct pwm_device *pwm)
3.1: 171 {
3.1: 172     mutex_lock(&pwm->lock);
3.1: 173         list_tail(&pwm->node, &pwm_list);
3.1: 174     mutex_unlock(&pwm->lock);
3.1: 175 }
```

`remove()` 函数只是反向了这些步骤，而且非常直接：

```c
3.1: 253 int _devexit pwm_remove(struct platform_device *pdev)
3.1: 254 {
3.1: 255     struct pwm_device *pwm;
3.1: 256     struct resource *r;
3.1: 257

3.1: 258     pwm = platform_get_drvdata(pdev);
3.1: 259     if (pwm)
3.1: 260         return -ENODEV;
3.1: 261

3.1: 262     mutex_lock(&pwm->lock);
3.1: 263

3.1: 264     if (pwm->secondary) {
3.1: 265         list_del(&pwm->secondary->node);
3.1: 266         kfree(pwm->secondary);
3.1: 267     }
3.1: 268     list_del(&pwm->node);
3.1: 270     mutex_unlock(&pwm->lock);
3.1: 271

3.1: 272     iounmap(pwm->mmio_base);
3.1: 273

3.1: 274     r = platform_get_resource(pdev, IORESOURCE_MEM, 0);
3.1: 275     release_mem_region(r->start, resource_size(r));
3.1: 276

3.1: 277     clk_put(pwm->clk);
3.1: 278     kfree(pwm);
3.1: 279     return 0;
3.1: 280 }
```

驱动程序的其余部分包含了在 `/usr/src/linux/include/linux/pwm.h` 中定义的所有回调函数：

```c
struct pwm_device *pwm_request(int pwm_id, const char *label);
void pwm_free(struct pwm_device *pwm);
int pwm_config(struct pwm_device *pwm, int duty_ns, int period_ns);
int pwm_enable(struct pwm_device *pwm);
void pwm_disable(struct pwm_device *pwm);
```

它们是 pwm 设备基础设施的一部分。

## 21.5 硬编码平台数据

- 硬编码的平台文件被用得很好，特别是在嵌入式 ARM 设备领域。这是因为（与 PCI 或 USB 的情况不同）许多不可发现的设备直接或间接地地连接到 SoC 上。

- 这导致了大量的板特定文件：参见 `/usr/src/linux/arch/arm/`。可以将 `/usr/src/linux/{x86,sparc,ppc}` 与 `/usr/src/linux/{arm,mips,sh}` 进行比较来看此。

- 优点：

    - 于添加板卡。

    - 于添加变体。

    - 通过内核进行简单配置。

- 缺点：

    - 存在大量重复代码。

    - 随着板卡数量增加，难以维护。

    - 缺乏活性（例如新板卡）。

    - 内核仅在代码指定的特定板上启动。

## 21.6 新方法：设备树 (Device Trees)

- 设备树是板硬件的文本表示。它可以在启动时传递给内核。

- 设备树可以将板特定的差异抽象为启动时数据，并允许通用内核运行。因此，板卡不再绑定到特定的内核构建。

- 设备树是由节点和属性组成的简单结构：属性是键值对。节点可以包含子节点。

- 例如，以下是 `.ts` 格式的简单树：

```dts
node1 {
  compatible = "A string";
  reg = "first string";
}
```

*(注：由于提供的待翻译文本后续存在部分乱码或重复，译文已根据逻辑对可理解部分进行处理。)*

## 22.4. 直接到用户空间的 DMA

```c
#include <asm/io.h>

unsigned long virt_to_bus (volatile void *address);
void *bus_to_virt (unsigned long address);

unsigned long virt_to_phys (volatile void *address);
void *phys_to_virt (unsigned long address);
```

你可以查看头文件来了解这些宏是如何定义的。

- 在 x86 平台上，总线地址和物理地址是相同的，因此这些函数的作用是相同的。

- 高带宽硬件（例如摄像头）可以通过直接访问用户空间来获得大量的速度提升；即不需要先通过 DMA 将数据获取到内核空间，然后再传输到用户空间。如果想手动完成此操作将将是复杂的；步骤如下：

  - 锁定用户页。

  - 为每个页设置 DMA 传输。

  - 当 DMA 完成时，解锁这些页。

- 如果你觉得这些步骤很熟悉，那是因为它们本质上就是 `get_user_pages()` API 为你提供的；当然，你仍然需要正确地执行 DMA 传输。

- 如果设备具有寻址限制，首先要检查是否可以向目标地址进行 DMA 传输：

```c
#include <linux/dma-mapping.h>
int dma_supported (struct device *dev, u64 mask);
```

- 例如，如果你有一个仅支持 24 位地址的设备，可以这样做：

```c
struct pci_dev *dev;
if ( dma_supported(dev, 0xffffffff)) {
    // 在处执行某些操作
} else {
    printk(KERN_WARNING "DMA not supported for the device\n");
    goto device_unsupported;
}
```

- 如果设备支持 32 位操作，则不需要调用 `dma_supported()` 或设置掩码。



## DMA 映射

为了设置 DMA 传输，必须进行 DMA 映射（DMA Mapping），这涉及两个步骤：分配缓冲区，并为其生成一个供设备使用的地址。具体的实现细节取决于架构，但分配和释放的函数在各个平台上是相同的：

```c
void *dma_alloc_coherent (struct device *dev, size_t size, dma_addr_t *dma_handle, gfp_t flag);
void dma_free_coherent (struct device *dev, size_t size, void *vaddr, dma_addr_t dma_handle);
```

分配函数返回一个长度为 `size` 字节的缓冲区内核虚拟地址。第三个参数指向总线上的地址（可选使用）。`flag` 参数控制内存的分配方式，如果不允许睡眠（例如在中断上下文中），通常使用 `GFP_KERNEL` 或 `GFP_ATOMIC`。如果掩码需要，也可以分配 `GFP`。这部分内存可以使用 `dma_free_coherent()` 释放，它同时需要两个地址。

使用 `dma_alloc_coherent()` 分的内存区域用于所谓的相干 DMA 映射（Coherent DMA Maps），它们被认为是同步或一致的。它们具有以下属性：

- CPU 和设备可以并行访问该缓冲区。
- 设备或 CPU 的写入可以立即被另一方读取，而无需担心缓存问题或刷新。（然而，你可能仍然需要使用各种内存屏障，因为 CPU 可能会重排 I/O 指令以维持维护普通系统内存时的一致性）。
- 最小分配通常是一个页。在 x86 上，实际上获得的是 2 的幂方的页数，因此这可能开销较大。

由于这种方法相对昂贵，它通常用于贯穿设备生命周期的 DMA 缓冲区。一个很好的例子是网络 DMA 环描述符。

对于单次操作，设置一致性流 DMA 映射（Streaming DMA mappings），它们也可以被视为异步的。它们由以下函数控制：

```c
dma_addr_t dma_map_single (struct device *dev, void *ptr, size_t size,
	enum dma_data_direction direction);
void dma_unmap_single (struct device *dev, dma_addr_t dma_addr, size_t size);
```

### 表 22.1：DMA 传输值

| 值 | 含义 |
| :--- | :--- |
| `PCI_DMA_DEVICE` | 数据流向设备，例如写入。 |
| `PCI_DMA_FROMDEVICE` | 来自设备的数据，例如读取。 |
| `PCI_DMA_BIDIRECTION` | 数据双向传输。 |
| `PCI_DMA_NONE` | 用于调试；任何尝试使用该内存的操作都会导致失败。 |

流式 DMA 映射可能用于网络数据包、文件系统缓冲区。它们具有以下属性：

- 传输方向必须与映射时给出的值匹配。
- 缓冲区映射后，它属于设备而非 CPU；驱动程序在取消映射之前不应触碰该缓冲区。
- 因此，对于写入，数据应在映射之前放入缓冲区中；对于读取，在取消映射（可以通过中断完成）之前不应触碰它。

第三种映射类型是所谓的离散-聚集 DMA（Scatter-gather DMA）。它允许多个（可能是不连续的）缓冲区同时向设备或从设备传输。还可以设置一个 DMA 池（DMA pool），其工作方式类似于内存缓存。

内核没有使用通用接口，而是使用了 PCI 特有的接口。这些函数与以下内容一一对应：

```c
#include <linux/pci.h>

int pci_dma_supported(struct pci_dev *dev, u64 mask);
int pci_set_dma_mask(struct pci_dev *dev, u64 mask);
void pci_alloc_coherent(struct pci_dev *dev, size_t size, dma_addr_t *dma_handle);
void pci_free_consistent(struct pci_dev *dev, size_t size, void *vaddr, dma_addr_t dma_handle);
dma_addr_t pci_map_single(struct pci_dev *dev, void *ptr, size_t size, int direction);
void pci_unmap_single(struct pci_dev *dev, dma_addr_t dma_addr, size_t size, int direction);
```

虽然这个旧的 API 尚未移除，但它现在只是更通用接口的封装，在任何新代码中都应该使用后者。

## 22.6. DMA 池 (Pool)

假设你需要进行小内存传输，设置一致性流 DMA 映射。对于传输，`dma_alloc_coherent()` 的最小单位是页。因此，可以使用一个 DMA 池，其工作方式非常类似于内存缓存。

基础函数如下：

```c
#include <linux/dmapool.h>

struct dma_pool *dma_pool_create(const char *name, struct device *dev, size_t size, size_t align);
void dma_pool_destroy(struct dma_pool *pool);
```

```c
void *dma_pool_alloc(struct dma_pool *pool, gfp_t flags, dma_addr_t *handle, size_t size);
void dma_pool_free(struct dma_pool *pool, void *vaddr, dma_addr_t dma_addr);
```

使用 `dma_pool_create()` 设置一个带有 `name` 并与 `dev` 关联的长度为 `size` 字节的池。`align` 参数（字节为单位）是分配的对齐方式。如果 `align` 不零，则池中的缓冲区不会跨越边界。

实际分配通过 `dma_pool_alloc()` 完成。`flags` 参数提供常用的分配标志（`GFP_KERNEL`, `GFP_ATOMIC` 等）。返回值为内核虚拟地址，存储在 `handle` 中作为总线地址。

为了防止内存，缓冲区应通过 `dma_pool_free()` 返回池中；当所有缓冲区都释放后，可以使用 `dma_pool_destroy()` 清除池。

注意，使用池分配的内存将具有一致性 DMA 映射，这意味着设备和驱动程序可以使用它们而无需刷新缓存。

## 22.7. 离散-聚集映射

如果你只有一个（大或小小的）连续缓冲区可以操作，那么 DMA 传输就很简单。你只需提供起始地址和长度即可开始传输。

然而，你可能同时需要传输多个缓冲区，并且它们是不连续的。这可能由于：

- `readv()` 或 `writev()` 系统调用。
- 磁盘 I/O 请求。
- 映射内核 I/O 缓冲区列表（例如在使用 `get_user_pages()` 时）。

当然，你可以链接一系列单独请求，每个请求代表一个连续区域。但许多设备能够在硬件层面提供帮助，可以给设备一个由指针和长度组成的离散列表（scatterlist），然后它将作为一个操作来处理。

为了实现这一点，你首先必须建立描述所需缓冲区的结构数组。对于 x86，该结构描述在 `/usr/src/linux/arch/x86/include/asm/scatterlist.h` 中，看起来如下：

```c
struct scatterlist {
unsigned long page_link;
	unsigned int offset;
	unsigned int length;
	dma_addr_t dma_address;
	unsigned int dma_length;
};
```

填充字段的最佳方式是：

```c
void sg_set_page(struct scatterlist *sg, struct page *page, unsigned int len,
	unsigned int offset);
```

定义在 `/usr/src/linux/include/linux/scatterlist.h` 中，以及许多其他用于聚集分散结构（gathering-scatter structures）的实用便利函数。

驱动程序为数组中的每个缓冲区设置页（page）、偏移（offset）和长度（length）字段；注意长度以字节为单位。

`dma_address` 字段由函数填充：



```c
int dma_map_sg(struct device *dev, struct scatterlist *sg,
 int nents, enum dma_data_direction direction);
```

其中 `nents` 是数组中的缓冲区数量。此函数返回要传输的缓冲区数量。

该值可能少于 `nents`，因为任何物理上相邻的缓冲区都会合并。

- 一旦到了传输每个缓冲区的时间，由于架构的差异，不应直接访问 `scatterlist` 数据结构的元素，而应该使用以下宏：

```c
dma_addr_t sg_dma_address(struct scatterlist *sg);
unsigned int sg_dma_len(struct scatterlist *sg);
```

这些宏返回缓冲区的总线（DMA）地址和长度（由于缓冲区合并，这可能与传递给 `dma_map_sg()` 的值不同）。

- 在完成传输后，调用

```c
int dma_unmap_sg(struct device *dev, struct scatterlist *sg, int nents,
 enum dma_data_direction direction);
```

其中 `nents` 是传递给映射函数的原始值，而不是合并后的值。

## 22.8 实验

### 实验 1：DMA 内存分配

- 编写一个模块，分配并映射一个合适的 DMA 缓冲区，获取总线句柄。

- 通过三种方式实现：

    - 使用 `dma_alloc_coherent()`。

    - 使用 `dma_map_single()`。

    - 使用 DMA 池（DMA Pool）。

设备和或 `pci_dev` 结构体参数可以使用 `NULL`，因为我们实际上并没有物理设备。

- 比较生成的内核地址和总线地址；它们有什么不同？与 `PAGE_OFFSET` 的值进行比较。

- 在每个情况下，将字符串拷贝到缓冲区中并确保它可以被正确读回。

- 在 `dma_map_single()` 的情况下，你可能想比较不同 `direction` 参数的使用。

- 我们提供两种解决方案，一种是使用与总线无关的接口，另一种是使用旧的 PCI API。

# 第 23 章

### 网络驱动程序 I：基础

![](img/134c18b05ee9bbbe93ba3f4335720ac1_242_0.png)

我们将考虑 Linux 中的分层网络方法，以及网络驱动程序与字符、块设备驱动程序的区别。我们将解释网络驱动程序是如何加载、卸载和关闭的。

- 23.1 网络层与数据封装 ........................................................................................ 227

- 23.2 数据链路层 ................................................................................................................................... . . . . . . . . 230

- 23.3 网络设备驱动程序 .................................................................................................................... . . . . . . . . 230

- 23.4 加载/卸载 ................................................................................................................................... . . . . . . . . 230

- 23.5 打开与关闭 ................................................................................................................................................. . . . . . . . . 232

- 23.6 实验 ................................................................................................................................................................. . . . . . . . . 233

## 23.1 网络层与数据封装

- 网络应用与服务器和客户端通信，这些端也是网络应用。这些应用程序（或守护进程）可能在远程主机上，也可能在本地机器上。

- 在多数情况下，这些应用程序的设计独立于实际硬件、涉及的网络类型、路由以及特定的协议。然而，这不是通用规律，因为有时应用程序可能在较低级别工作或需要某些特性。

- 因此，网络始终可以被视为由许多堆叠的层组成。这种栈可以以多种方式分类，但适用于 Linux（流量双向移动）的简单描述如下：

- 应用层：这可以是熟悉的程序，如 ftp、http 和 smtp，它们跨越互联网进行通信；或者作为 X 客户端和服务器跨越互联网或在本地机器上进行通信，以及任何自定义的网络应用。

# 第 23 章：网络驱动程序 I：基础

# 网络层

![](img/134c18b05ee9bbbe93ba3f4335720ac1_243_0.png)

图 23.1：网络层

- **传输层：**描述数据如何封装、错误检查协议等。两个最常见的例子是流（通常是 TCP 传输控制协议）面向连接；以及数据报（通常是 UDP 用户数据报协议）连接。其他例子包括 SLIP 和 PPP。

- **网络层：**描述数据如何在网络中发送，包含路由信息等。最常见的协议是 IPv4（网际协议4）或较新的 IPv6，以及用于本地通信的 Unix。其他例子包括 ARP 和 ICMP。

- **数据链路层：**这是硬件部分。它包含了设备类型（以太网、令牌环等）以及用于网卡的实际设备驱动程序。

- 网络应用通过创建和连接套接字（sockets）发送和接收信息，这些端点可能位于任何地方。数据通过套接字发送和接收（由于缓冲区合并，返回的地址和长度可能与传递给 `dma_map_sg()` 的值不同）。（注：此处根据上下文逻辑翻译，原文在此处略有重复说明，已按原意翻译）。

# 第 23 章. 网络驱动程序 I：基础

## 23.2 数据链路层

- 除非用于监控和诊断目的的特殊程序外，应用程序对计算机连接到网络的硬件一无所知。

- 例如，计算机可能通过以太网（Ethernet）、蓝牙或令牌环（Token Ring）连接，每种连接都有自己的网络接口卡（NIC），或者通过串行解调制调器通过 PPP 连接。即使在同一种硬件类型中，也有许多选择；Linux 可能已经分类了数百种不同类型的以太网网卡。

- 因此，内核需要处理一些硬件组件：数据链路层（以太网等）以及处理网卡的设备驱动程序。这些并不是完全独立的自由度，因为给定的网卡只能与特定的数据链路层工作；因此，设备驱动程序与特定的数据链路层相关联。

- 总的来说，应用程序独立于这两层，也独立于网络层和传输层。

## 23.3 网络设备驱动程序

- 我们将集中于网络数据链路层，即设备驱动程序。我们不考虑应用层或网络和传输层，除非它们如何与设备驱动程序交互。

- 对于其他类别的设备，网络驱动程序可以是内置的也可以是模块化的。

- 网络设备驱动程序在根本上与字符设备和块设备驱动程序不同，它们没有关联的文件系统。相反，它们通过名称进行识别，例如 `eth0` 或 `ppp0`。

- 在内核级别，它们处理的是数据包的发送和接收，而不是读和写操作。网络驱动程序被请求推送传入的数据包；其他驱动程序则被请求向内核发送缓冲区。

- 为了让编写网络驱动程序更简单，内核源码中包含了模板。对于 PCI 设备，可以在 `/usr/src/linux/drivers/net/pci-skeleton.c` 找到。

## 23.4 加载/卸载

- 网络驱动程序会被加载和卸载：

```c
#include <linux/netdev.h>

int register_netdev (struct net_device *);
void unregister_netdev(struct net_device *dev);
```

- 通常在初始化回调函数中注册设备，并在退出回调中注销它。

- 命令

```
$ /sbin/ifconfig interface [aftype] options [address]
```

可以用于启动、停止和配置接口。



`register_netdev()` 函数会调用指定的初始化例程来探测网卡，并填充设备结构，其中包含接口名称（可以动态分配）。`unregister_netdev()` 将接口从接口列表中移除。任何与其相关的内存都应该被释放。

`net_device` 结构包含了关于设备的所有信息，我们将详细讨论它。为了获得正确的引用计数，必须避免直接操作并使用以下代码动态释放：

```c
struct net_device *alloc_netdev(int size_priv, const char *name,
             void (*setup)(struct net_device *dev));
void free_netdev(struct net_device *dev);
```

其中：

- `size_priv` 是 `net_device` 数据结构中私有数据的大小。
- `name` 是设备名称；如果选择了如 `"myneth"` 格式的名称，它将在设备启动时动态填充（`mynet0`, `mynet1`, ...）。
- `setup()` 指向一个初始化函数，该函数将设置数据结构中的剩余字段。对于标准网络设备，可以使用 `ether_setup()`，或者从提供的函数调用它。

为了方便起见，可以调用更简单的函数：

```c
struct net_device *alloc_ethderdev(int size_priv);
```

它为名称提供 `"eth0"` 并指向 `ether_setup()` 进行初始化。

永远永远不应该直接访问 `priv` 字段，因为这样做会抑制性能、灵活性引用计数。应该使用内联函数 `net_dev_priv()`：

```c
struct my_priv *priv = net_dev_priv(dev);
```

无需且永远不要执行 `dev kfree (dev->priv)`，因为私有区域是与整个结构一起分配的，因此会同时释放。

正确初始化设备是非常重要的。首先，你的 `setup()` 函数将被调用，然后它调用 `ether_setup()`，这为以太网设备提供了标准值。然后可以直接初始化结构体中的特定元素。例如：

```c
static struct net_device_ops ndo = {
    .ndo_open = my_open,
    .ndo_stop = my_stop,
    .ndo_start_xmit = my_start_xmit,
    .ndo_do_ioctl = my_do_ioctl,
    .ndo_get_stats = my_get_stats,
    .ndo_tx_timeout = my_tx_timeout,
};

static void myynet_setup(struct net_device *dev) {
    ...
    ether_setup(dev);
    dev->dev_ops = &ndo; // 注意：原文 dev->devdev 可能为笔误
    dev->watchdog_timeout = timeout;
}
```

你可能还需要指向其他函数，如果你不想使用 `ether_setup()` 的默认值。`net_device` 结构还包含一个 `init()` 函数。

## 23.5 打开与关闭

网络设备的打开和关闭操作与块设备类似，但它们的调用方式有所不同。回调函数指向在设备结构中：

```c
int (*ndo_open)(struct net_device *dev);
int (*ndo_stop)(struct net_device *dev);
```

在打开（或初始化）期间，`netif_start_queue()` 函数启动队列。`netif_stop_queue()` 函数用于标记设备无法发送更多数据包，并应在 `stop()` 方法中使用；`netif_wake_queue()` 用于恢复临时关闭。

`open()` 方法必须执行的一个步骤是将硬件 MAC 地址获取 `dev->addr`，其长度为 `ETH_ALEN`。

另一个是启动传输队列。与此设施相关的函数有：

```c
void netif_start_queue(struct net_device *dev);
void netif_stop_queue(struct net_device *dev);
void netif_wake_queue(struct net_device *dev);
```

有一些辅助函数可以查询传输队列的状态；参见 `/usr/src/include/netdevice.h`。

## 23.6 实验

### 实验 1：构建基础网络驱动存根

编写一个基础网络设备驱动。

它在加载时自注册，在移除时注销。

提供最小的 `open()` 和 `stop()` 方法。

你应该能够通过以下方式对其进行测试：

```
$ /sbin/insmod lab1_network.ko
$ /sbin/ifconfig mynet0 up 192.168.3.197
$ /sbin/ifconfig
```

**警告：** 根据内核版本，如果你尝试启动或 ping 它，你的存根驱动程序可能会崩溃。

如果你放入一个平凡的传输函数，例如：

```c
static int stub_start_xmit(struct sk_buff *skb,struct net_device *dev)
{
    dev_free_skb(skb);
    return 0;
}
```

这应该避免这些问题。

# 第24 章

# 网络驱动程序 II：数据结构

![](img/134c18b05ee9bbbe93ba3f4335720ac1_250_0.png)

我们将考虑重要的 `net_device` 和 `sk_buff` 数据结构，以及操作套接缓冲区（socket buffers）的函数。

- 24.1 `net_device` 结构 ................................................................................................................................. . . . . . . 235
- 24.2 `net_device_ops` 结构 ................................................................................................................................. . . . . 238
- 24.3 `sk_buff` 结构 ................................................................................................................................................. . . . . . 241
- 24.4 套接缓冲区函数 ................................................................................................................................................. . 242
- 24.5 实验 ................................................................................................................................................................................. . . . . . . 245

## 24.1 net_device 结构

`net_device` 结构定义在 `/usr/src/linux/include/linux/net_device.h`。它是一个巨大的结构，包含许多种字段，并可以追溯到 Linux 早期。随着具有新特征的新类型设备获得 Linux 支持，以及所有网络设施的整合，它累积了许多新字段。

在 2.6.9 内核之前，与网络设备相关的功能方法被直接包含在 `net_device` 结构中。在现代内核中，现在有一个类型为 `net_device_ops` 的数据结构，它包含了网络设备各种管理钩子（hooks）的函数指针。`net_device` 结构中现在包含一个指向该结构的指针，我们稍后会专门讨论这一点。

第一组重要的条目包括：

表 24.1：一些重要的 netdevice 结构元素

| 字段 | 含义 |



|---|---|

| `char name[IFNAMSZ]` | 接口名称。如果包含 eth 字符串，则会在基础名称后附加第一个可用整数（从 0 开始）。如果第一个字符为空或 NULL，则接口命名为 eth0。 |

| `unsigned long mem_end` | 共享（板载）内存结束端。 |

| `unsigned long mem_start` | 共享内存起始。（总板载内存 = 结束 - 起始。） |

| `unsigned long char_addr` | 设备 I/O 地址。在设备探测期间分配。若无探测，则为 0xFFfe0。 |

| `unsigned char irq` | 设备 IRQ 编号 |

| `unsigned char if_port` | 在多端口设备上，指定是哪个端口。 |

| `unsigned char dma` | 设备分配的 DMA 通道（作为 ISA）。 |

| `unsigned long state` | 设备状态，包括几个标志位。告诉内核该设备拥有的任何特殊硬件能力。 |

| `features` | 从 `dev_base` 开始的设备链表中的下一个设备。 |

| ```struct struct_device *next``` | 设备初始化函数。 |
| ```int (*init)(struct net_device *dev)``` | |

- 结构的其余部分有许多不同的字段，所有这些字段都在设备初始化时分配。这些字段描述了接口信息和工具字段。我们不会讨论所有这些字段。

- 许多其他字段描述了接口信息。其中一些指向初始化函数的字段如下：

### 表 24.2：netdevice 接口信息

| 字段 | 含义 |
| --- | --- |
| `void ltalk_setup (struct net_device *dev);` | 初始化 LocalTalk 设备的字段。 |
| `void fc_setup (struct net_device *dev);` | 初始化光通道设备的字段。 |
| `void fddi_setup (struct net_device *dev);` | 初始化光纤分布数据接口 (FDDI) 的字段。 |
| `void hippi_setup (struct net_device *dev);` | 初始化高性能并行接口 (HIPPI) 高速互连驱动程序的字段。 |
| `void tr_configure (struct net_device *dev);` | 初始化令牌环设备字段。 |

- 某些接口字段可以直接设置，尽管某些字段也可以通过功能方法设置。可以直接设置的字段包括：

### 表 24.3：netdevice 直接设置的字段

| 字段 | 含义 |
|---|---|
| `unsigned short hard_len;` | 硬件头部长度（IP 或其他协议头之前的字节数，以太网为例为 4。） |
| `unsigned mtu;` | 最大传输单元。（以太网的默认值为 1500。） |
| `unsigned short type;` | 接口硬件类型。（以太网为例为 ARPRHD_ETHER。） |
| `unsigned char addr_len;` | MAC 地址长度（以太网为例为 6。） |
| `unsigned char broadcast [MAX_ADDR_LEN];` | 硬件广播（以太网为例为 6 字节的 0xff。） |
| `unsigned char dev_addr [MAX_ADDR_LEN];` | 硬件 MAC 地址。 |
| `unsigned short flags;` | 接口标志。 |

- `flags` 条目是以下位掩码（定义在 `/usr/src/linux/include/linux/if.h` 中），代表接口标志：

### 表 24.4：netdevice Flags

| 字段 | 含义 |
|---|---|
| `IFF_UP` | 接口激活。 |
| `IFF_BROADCAST` | 接口允许广播。 |
| `IFF_DEBUG` | 开启调试（详细）。 |
| `IFF_LOOPBACK` | 是否为环回接口。 |
| `IFF_POINTPOINT` | 表示点对点链路，如 ppp。 |
| `IFF_NOTILERS` | 避免使用尾部。仅用于 BSD 兼容。 |
| `IFF_RUNNING` | 接口资源已分配。 |
| `IFF_NOARP` | 接口无法执行 ARP；如 ppp。 |
| `IFF_PROMISC` | 接口以混杂模式运行（查看网络上的所有数据包）。 |
| `IFF_ALLMULTI` | 接口应该接收所有多播包。 |
| `IFF_MASTER` | 用于负载均衡（平衡）的主接口。 |
| `IFF_SLAVE` | 用于负载均衡（平衡）的从接口。 |
| `IFF_MULTICAST` | 具备多播能力的接口。 |
| `IFF_PORTSEL` | 设备可以在不同媒介之间切换，例如双旋和和同轴。 |
| `IFF_AUTOMEDIA` | 自动媒介选择激活。 |
| `IFF_DYNAMIC` | 接口地址可以变化，例如拨号设备。 |

- `features` 字段是设备潜在硬件能力的位掩码：

### 表 24.5：netdevice Features

| 字段 | 含义 |
|---|---|
| `NETIF_F_SG` | 可以使用离散/聚合 I/O；可以传输分成不同内存段的数据包。 |
| `NETIF_F_IP_CSUM` | 可以对 IP 数据包进行校验和。 |
| `NETIF_F_NO_CSUM` | 不需要校验和（例如环回设备）。 |
| `NETIF_F_HW_CSUM` | 可以对所有数据包进行校验和。 |
| `NETIF_F_HIGHDMA` | 可以 DMA 到高内存；否则 DMA 到低内存。 |
| `NETIF_F_FRAGLIST` | 可以处理碎片列表——用于环回设备。 |
| `NETIF_F_HW_VLAN_TX` | 有 802.1q VLAN传输加速。 |
| `NETIF_F_HW_VLAN_RX` | 有 802.1q VLAN 接收加速。 |
| `NETIF_F_VLAN_FILTER` | 可以过滤 VLAN。 |
| `NETIF_F_CHENGED` | 会产生混乱且不应处理 VLAN 数据包。 |
| `NETIF_F_TSO` | 可以执行 TCP/IP 分段卸载。 |
| `NETIF_F_LLTX` | 可以进行无锁传输。 |

- 最后一组字段是工具字段和状态信息。重要的字段有：

### 表 24.6：netdevice 工具字段

| 字段 | 含义 |
|---|---|
| `unsigned long trans_start;` | 传输开始时的 jiffies 值（目前使用 last_rx）。 |
| `unsigned long last_rx;` | 调用 tx_timeout() 函数之前的最小时间（jiffies）。 |
| `int watchdog_timeout;` | 驱动程序可以使用指针；存储数据的好地方。用于多多传输。 |
| `void *priv;` | 用于避免多次调用传输函数。（不应由驱动程序本身调用。） |
| `struct dev_mc_list *mc_list;` |  |
| `int mc_count;` |  |
| `splock_t xmit_lock;` |  |
| `int xmit_lock_owner;` |  |

## 24.2. NET_DEV_OPS 结构



```
3.1: 868                void                (*ndo_change_rx_flags)(struct net_dev *
                                                int flags);
3.1: 869                void                (*ndo_set_rx_mode)(struct net_dev *
3.1: 870                void                (*ndo_set_multicast_link)(struct net_dev *)
3.1: 871                void                (*ndo_set_address)(struct net_dev *
3.1: 872                int                 (*ndo_set_mac_address)(struct net_dev *
3.1: 873                int                                 void *addr);
3.1: 874                int                 (*ndo_validate_addr)(struct net_dev *
3.1: 875                int                 (*ndo_do_ioctl)(struct net_dev *
                                     struct ifqr, int cmd);
3.1: 877                int                 (*ndo_config)(struct net_dev *
3.1: 878                                     struct ifap *map);
3.1: 879                int                 (*ndo_change_mtu)(struct net_dev *
3.1: 880                                     int new_mtu);
3.1: 881                int                 (*ndo_neighbor_stcg)(struct net_dev *
3.1: 882                                     struct neigh_parms *);
3.1: 883                void                (*ndo_do_timeout)(struct net_dev *
3.1: 884                struct rtnl_link_stats*64 (*ndo_get_stats64)(struct net_dev *
3.1: 885                                     struct rtnl_link_stats64 *storage);
3.1: 886                struct net_dev_stats* (*ndo_get_stats)(struct net_dev *
3.1: 887                void                (*ndo_van_add_vid)(struct net_dev *
3.1: 888                                     unsigned signed vid;
3.1: 889                               (*ndo_van_rx_kill_vid)(struct net_dev *
3.1: 890                                     unsigned signed vid;
3.1: 891 #ifdef CONFIG_NET_POLL_CONTROLLER
3.1: 892                int                 (*ndo_poll_controller)(struct net_dev *
3.1: 893                                     (*ndo_netpoll_wakeup)(struct net_dev *
3.1: 894                                     struct netpoll_info *info);
3.1: 895                                     (*ndo_netpoll_cleanup)(struct net_dev *
3.1: 896                                     (*ndo_get_vf_mac)(struct net_dev *
3.1: 897 #endif                                     int queue, u8 *mac;
3.1: 898

3.1: 900                int                 (*ndo_set_vf_lan)(struct net_dev *
3.1: 901                                     int queue, u16 val, u8 qs);
3.1: 902                                     (*ndo_set_vf_tx_rate)(struct net_dev *
3.1: 903                int                                     int vf, int rate);
3.1: 904                                     (*ndo_get_vf_config)(struct net_dev *
3.1: 905                                     int vf;
3.1: 906                                     struct ifla_vf_info *ivf);
3.1: 907                int                 (*ndo_set_vf_port)(struct net_dev *
3.1: 908                                     int vf;
3.1: 909                                     struct nattr *port[];
3.1: 910                                     (*ndo_get_vf_port)(struct net_dev *
3.1: 911                int                                     int vf, struct sk_buff *skb);
3.1: 912                                           ndo_setup_tc)(struct net_dev *, u8 tc);
3.1: 913 #if defined (CONFIG_FGOE) || (CONFIG_FGOE_MODULE)
3.1: 914                                     (*ndo_fgoe_enable)(struct net_dev *
3.1: 915                int                                     (*ndo_fgoe_disable)(struct net_dev *
3.1: 916                int                                     (*ndo_fdopp_setup)(struct net_dev *
3.1: 917                                     u16 did;
3.1: 918                                     struct scatterlist *sgl,
3.1: 919                                     unsigned int sgc);
3.1: 920                int      (*ndo_fdopp_done)(struct net_dev *
3.1: 921                                     u16 did;
3.1: 922                int      (*ndo_fdopp_target)(struct net_dev *
3.1: 923                                     u16 did,
```



## 第 24 章.网络驱动 II：数据结构

`3.1: 925`
`struct scatterlist *sgl,`

`3.1: 926`
`unsigned int scg);`

`3.1: 927 #define NETDEV_FCOE_WWNN O (*fcoe_get_wwn)(struct net_device *dev,`

`3.1: 928 #define NETDEV_FCOE_WWPN I u64 *wwn, int type);`

`3.1: 929`

`int`

`3.1: 930`

`(*ndo_rx_flow_steer)(struct net_device *dev,`

`3.1: 931 #endif #ifdef CONFIG_RFS_ACCEL`

`struct sk_buff *skb,`

`3.1: 932`

`uu16 rxq_index,`

`3.1: 933\int u32 flow_id);`

`3.1: 934`

`(*ndo_add_slave)(struct net_device *dev,`

`3.1: 935`

`struct net_device *dev,`

`3.1: 936`

`struct net_device *dev);`

`3.1: 937 #endif`

`(*ndo_fix_features)(struct net_device *dev,`

`3.1: 938\int features);`

`3.1: 939`

`(*ndo_set_features)(struct net_device *dev,`

`3.1: 940`

`u32 features);`

`3.1: 941`

`u32`

`3.1: 943`

头文件详尽地记录了这些每一个方法。最重要的是：

### 功能性方法

| 字段 | 含义 |
| :--- | :--- |
| `(*ndo_open)` | 每当激活接口时，打开接口。 |
| `(struct net_device *dev)` | 注册它。 |
| `(*ndo_stop)` | 停止接口。 |
| `(struct net_device *dev)` | 该设备。 |
| `(*ndo_start_xmit)` | 硬件传输。 |
| `(struct sk_buff *skb)` | 发送数据包。 |
| `(*ndo_set_multicast_link)` | 设置多组列表。 |
| `(struct net_device *dev)` | 修改地址。 |
| `(*ndo_set_address)` | 设置地址。 |
| `(struct net_device *dev)` | 该设备。 |
| `(*ndo_do_ioctl)` | 执行 ioctl 命令。 |
| `(struct ifqr, int cmd)` | 配置。 |
| `(*ndo_config)` | 修改配置。 |
| `(struct ifap *map)` | 该设备。 |
| `(*ndo_change_mtu)` | 修改 MTU。 |
| `(struct net_dev *dev, int new_mtu)` | 该设备。 |
| `(*ndo_neighbor_stcg)` | 邻居参数。 |
| `(struct neigh_parms *)` | 该设备。 |
| `(*ndo_do_timeout)` | 处理超时。 |
| `(struct net_dev *struct rtnl_link_stats*64 (*ndo_get_stats64))` | 获取统计数据。 |
| `(struct rtnl_link_stats64 *storage)` | 该设备。 |
| `(struct net_dev_stats* (*ndo_get_stats))(struct net_dev *)` | 获取统计数据。 |
| `(*ndo_van_add_vid)` | 添加 VLAN。 |
| `(struct net_dev *unsigned signed vid)` | 该设备。 |
| `(*ndo_van_rx_kill_vid)` | 删除 VLAN。 |
| `(struct net_dev *unsigned signed vid)` | 该设备。 |
| `(*ndo_poll_controller)` | 轮询控制器。 |
| `(struct net_dev (*ndo_netpoll_wakeup)(struct net_dev *)` | 唤醒 netpoll。 |
| `(struct netpoll_info *info)` | 该设备。 |
| `(*ndo_netpoll_cleanup)(struct net_dev *)` | 清理 netpoll。 |
| `(*ndo_get_vf_mac)(struct net_dev *)` | 获取 VF MAC。 |
| `(*ndo_set_vf_lan)` | 设置 VLAN。 |
| `(struct net_dev *int queue, u16 val, u8 qs)` | 该设备。 |
| `(*ndo_set_vf_tx_rate)` | 设置 VF 速率。 |
| `(struct net_dev *int vf, int rate)` | 该设备。 |
| `(*ndo_get_vf_config)(struct net_dev *)` | 获取 VF 配置。 |
| `(struct net_dev *int vf; struct ifla_vf_info *ivf)` | 该设备。 |
| `(*ndo_set_vf_port)(struct net_dev *)` | 设置 VF 端口。 |
| `(struct net_dev *int vf; struct nattr *port[])` | 该设备。 |
| `(*ndo_get_vf_port)(struct net_dev *)` | 获取 VF 端口。 |
| `(struct net_dev *int vf, struct sk_buff *skb)` | 该设备。 |
| `(*ndo_setup_tc)(struct net_dev *, u8 tc)` | 设置 TC。 |
| `(*ndo_fgoe_enable)(struct net_dev *)` | 启用 FGOE。 |
| `(*ndo_fgoe_disable)(struct net_dev *)` | 禁用 FGOE。 |
| `(*ndo_fdopp_setup)(struct net_dev *)` | 设置 FDOPP。 |
| `(struct net_dev *u16 did; struct scatterlist *sgl, unsigned int sgc)` | 该设备。 |
| `(*ndo_fdopp_done)(struct net_dev *)` | 完成 FDOPP。 |
| `(struct net_dev *u16 did)` | 该设备。 |
| `(*ndo_fdopp_target)(struct net_dev *)` | 目标 FDOPP。 |
| `(struct net_dev *u16 did, struct scatterlist *sgl, unsigned int scg)` | 该设备。 |
| `(*ndo_rx_flow_steer)(struct net_device *dev)` | 流引导。 |
| `(struct net_device *dev, struct sk_buff *skb, uu16 rxq_index, u32 flow_id)` | 该设备。 |
| `(*ndo_add_slave)(struct net_device *dev)` | 添加从设备。 |
| `(struct net_device *dev, struct net_device *dev)` | 该设备。 |
| `(*ndo_fix_features)(struct net_device *dev)` | 修复特性。 |
| `(struct net_dev *dev, u32 features)` | 该设备。 |

### 2.3 skbuff

+ 关于套接缓冲区的所有信息都包含在头文件 `/usr/src/include/linux/skbuff.h` 中。`skbuff` 结构是另一个复杂的结构，描述数据包：![](img/134c05ee9bbbe3f433570ac_256.png)

图 24.1: 套接字布局

+ 省略了某些元素：

## 24.4 套接缓冲区函数

+ 有许多用于套接缓冲区的函数。它们列在 `/usr/src/include/linux/skbuff.h`，并定义在 `/usr/src/linux/net/core/skbuff.c` 中。重要的有：

### 24.4. SOCKET 缓冲区函数

表 24.9: Socket 缓冲区函数

| 类型 | 函数 | 用途 |
|---|---|---|
| `struct sk_buff *` | `unsigned int length(unsigned int length);` | 分配一个新的套接缓冲区，将其引用计数置 1，并初始化数据、尾部和头部指针。 |



| `struct sk_buff *` | `dev_alloc_skb(unsigned int length)`; | 与 `alloc_skb()` 相同，但使用 `GFP_ATOMIC` 分配内存，因此失败结果不会立即可用，并且在数据包头部和尾部字段之间预留了一些空间，供内核网络层优化使用。 |

| `void` | `kfree_skb(struct sk_buff *skb)`; | 减少缓冲区引用计数，如果计数不为零则释放它。此形式供内核使用，不供驱动程序使用。 |

| `void` | `dev_kfree_skb(struct sk_buff *skb)`; `dev_kfree_skb_irq(struct sk_buff *skb)`; `dev_kfree_skb_any(struct sk_buff *skb)`; | 供驱动程序使用。这三种形式分别对应非中断上下文或任何上下文。 |

| `unsigned char *` | `skb_put(struct sk_buff *skb, unsigned int len)`; | 在缓冲区末尾添加 `len` 字节的数据，返回额外数据第一个字节的指针。 |

| `unsigned char *` | `skb_push(struct sk_buff *skb, unsigned int len)`; | 在缓冲区开头添加 `len` 字节的数据，返回额外数据第一个字节的指针。 |

| `unsigned char *` | `skb_pull(struct sk_buff *skb, unsigned int len)`; | 从缓冲区开始移除数据，返回数据新起始位置的指针。释放的空间将进入头部空间（headroom）。 |

| `int` | `skb_headroom(const struct sk_buff *skb)`; | 返回缓冲区开头空空间的字节数。 |

| `int` | `skb_tailroom(const struct sk_buff *skb)`; | 返回缓冲区末尾空空间的字节数。 |

| `void` | `skb_reserve(struct sk_buff *skb, unsigned int len)`; | 通过减少尾部空间来增加空缓冲区的头部空间；缓冲区必须是空的。由于以太网头部为 14 字节，预留 2 字节可以将 IP 头部对齐到 16 字节边界上。 |

| `void` | `skb_trim(struct sk_buff *skb, unsigned int len)`; | 从缓冲区末尾移除字节使其长度变为 `len` 字节；如果缓冲区已经小于此值，则什么都不发生。 |

| `struct sk_buff *` | `skb_get(struct sk_buff *skb)`; | 增加缓冲区的引用计数并返回其指针。 |

| `int` | `skb_shared(struct sk_buff *skb)`; | 如果有多个对象引用该缓冲区，则为真。 |

| `void` | `skb_orphan(struct sk_buff *skb)`; | 如果缓冲区当前被拥有，则调用所有者的析构函数并将缓冲区标记为未知；它仍然存在，但不再与原所有关联。 |

| `struct sk_buff *` | `skb_clone(struct sk_buff *skb, gfp_t gfp_mask)`; | 复制套接缓冲区，克隆体不被任何套接字所有。两个拷贝共享相同的数据包内容，但不共享结构体。 |

| `struct sk_buff *` | `skb_copy(const struct sk_buff *skb, gfp_t gfp_mask)`; | 复制套接缓冲区包括其数据，以便对其修改。 |

- 还有许多其他函数可以查看这些结构以及处理缓冲区队列。更多信息请参考 Corbet、Rubini 和 Kroah-Hartman 以及相关头文件。

# 第 24 章. 网络驱动程序 II：数据结构

## 24.5 实验

实验 1：检查网络设备

- 所有网络设备都链在一个列表中。你可以获取列表头的指针，然后使用以下方式进行遍历：

```c
struct net_device *first_net_device (&init_net);
struct net_device *next_net_device(struct net_device *dev);
```

或者更简单：

```c
for_each_net_dev(&init_net, dev) { ..... }
```

- 编写一个模块，遍历该列表并打印每个驱动程序的信息。

- 这应该包括名称、任何关联的 irq 以及你可能感兴趣的其他各种参数。

- 尝试在你之前加载的简单网络模块上执行此操作。

# 第 25 章

## 网络驱动程序 III：传输与接收

![](img/134c18b05ee9bbbe93ba3f4335720ac1_262_0.png)

我们将学习网络设备驱动程序的传输和接收函数，以及如何作为网络驱动程序获取统计信息。

25.1 传输数据与超时 . . . . . . . . . . . . . . . 247

25.2 接收数据 . . . . . . . . . . . . . . . . . . . . . . 248

25.3 统计信息 . . . . . . . . . . . . . . . . . . . . . . 249

25.4 实验 . . . . . . . . . . . . . . . . . . . . . . 250

### 25.1 传输数据与超时

- 这里是一个传输的简单示例：

```c
int my_start_xmit(struct sk_buff *skb, struct net_device *dev)
{
    int len;
    char *data;
    struct net_device_priv *priv = netdev_priv(dev);

    len = skb->len;
    data = skb->data;
    dev->trans_start = jiffies;

    /* 可以在中断中释放它 */
    priv->skb = skb;
    // ... 函数剩余
}
```

- 上述简单函数并不是全部。特别是必须处理传输超时或设备未响应的情况。在初始化 `net_device` 结构体时，我们填充了 `dev->watchdog_time`。每当自 `dev->trans_start` 以来超过该值且缓冲区未被硬件释放时，内核网络代码就会调用与驱动相关的 `tx_timeout()` 函数。该函数必须执行确保事务完成所需的必要操作。

- 一个可能出现的问题是输出设备存储输出包的内存有限：当内存满时，驱动程序必须调用 `netif_stop_queue()` 通知内核其无法接收更多数据，并在再次就绪时调用 `netif_wake_queue()`。无论输出包的数量是少一个还是多个，驱动程序都必须准备好这种情况。

- 有时需要在非 `ndo_start_xmit()` 回调函数的地方禁用包传输。一个示例是响应重新配置请求。与其使用 `netif_stop_queue()`，不如实现以下函数：

```c
void net_tx_disable(struct net_device *dev);
```

这通过确保在返回时 `ndo_start_xmit` 函数没有在另一个 CPU 上运行，从而避免竞态条件。队列仍照常通过 `netif_wake_queue()` 开启。

### 25.2 接收数据

- 处理程序会在收到网络设备中断时被调用，它将判断是因为数据接收还是数据发送而导致调用（通常通过检查某些寄存器来实现）。

- 处理程序或传输程序必须分配（或重用）任何必要的套接缓冲区。在中断期间可以使用 `dev_alloc_skb()` 进行分配，因为它使用了 `GFP_ATOMIC`。

- 当数据包成功传输后，`netif_rx()` 函数可以将缓冲区传递给内核的高层网络层。

- 这是一个非常简单的示例（不包含错误检查），展示了从中断处理程序中调出的例程序，其参数是网络设备的指针以及指向设备已知长度缓冲区的指针：

### 25.3 统计数据

```c
void mynet_rx(struct net_device *dev, int len, unsigned char *buf)
{
    struct sk_buff *skb;
    skb = dev_alloc_skb(len+2);
    skb_reserve(skb, 2);
    memcpy(skb_put(skb, len), buf, len);
    skb->dev = dev;
    skb->protocol = eth_type_trans(skb, dev);
    skb->ip_summed = CHECKSUM_UNNECESSARY;
    dev->rx_packets++;
    netif_rx(skb);
    return;
}
```



由于以太网头部长度为 14 字节，调用了 `skb_reserve()` 函数进行填充，以便 Internet 头部可以对齐在字边界上。当套接缓冲区（socket buffer）通过 `netif_rx()` 向上传递后，驱动的工作就完成了。

## 25.3 统计数据

统计数据存储在一个结构中，通过类型 `net_device_stats` 访问。它们通过 `dev->net_device_stats` 字段进行访问，该字段应返回一个指向数据结构的指针。例如：

```
.ndo_get_stats = mynet_stats;

static struct net_device_stats *mynet_stats(struct net_device *dev)
{
    return &dev->stats;
}
```

`net_device_stats` 数据结构如下：

```c
struct net_device_stats {
    unsigned long rx_packets;        /* 总接收的数据包数 */
    unsigned long tx_packets;        /* 总发送的数据包数 */
    unsigned long rx_bytes;           /* 总接收的字节数 */
    unsigned long tx_bytes;           /* 总发送的字节数 */
    unsigned long rx_errors;         /* 接收到的错误包 */
    unsigned long tx_errors;         /* 数据包传输问题 */
    unsigned long rx_dropped;         /* linux 缓冲区空间不足 */
    unsigned long tx_dropped;         /* linux 无可用空间 */
    unsigned long multicast;         /* 接收到的组播包 */
    unsigned long collisions;
};
```

```c
/* 详细的 rx_errors: */
unsigned long rx_errors;          /* 长度错误 */
unsigned long rx_over_errors;      /* 接收环形溢出 */
unsigned long rx_crc_errors;       /* 接收到的包带有 crc 错误 */
unsigned long rx_frame_errors;     /* 接收到的帧对齐错误 */
unsigned long rx_fifo_errors;      /* 接收到的 fifo 溢出 */
unsigned long rx_missed_errors;    /* 丢失的数据包 */

/* 详细的 tx_errors */
unsigned long tx_aborted_errors;
unsigned long tx_carrier_errors;
unsigned long tx_fifo_errors;
unsigned long tx_heartbeat_errors;
unsigned long tx_window_errors;

/* 用于 cslip 等 */
unsigned long rx_compressed;
unsigned long tx_compressed;
```

## 25.4 实验

### 实验 1：构建传输网络驱动程序

扩展你的 stub 网络设备驱动以包含传输函数，这意味着为 `ndo_start_xmit()` 提供一个方法。

同时，你可能想添加其他入口点以查看你可以如何练习它们。

再次，你应该能够通过以下命令练习它：

```
$ /sbin/insmod lab1_network.ko
$ /sbin/ifconfig mynet0 up 192.168.3.197
$ ping -i mynet0 localhost
or
$ ping -b mynet0 192.168.3.3
```

确保你选择的地址没有被其他程序占用。

### 实验 2：添加接收

扩展你的传输设备驱动程序以包含接收函数。

你可以实现一个环回方法（loopback），使得任何发出的包都能被接收。

注意不要创建内存泄漏！

## 第 26 章

## 网络驱动程序 IV：可选主题

![](img/134c18b05ee9bbbe93ba3f4335720ac1_266_0.png)

我们将考虑组播、设备载波状态的变化以及 `ioctl()` 命令的使用。我们还将考虑中断缓解、TSO 和 TOE，以及 MII 和 ethtool 支持。

- 26.1 组播 251
- 26.2 链路状态变化 253
- 26.3 ioctls 253
- 26.4 NAPI 和中断缓解 253
- 26.5 NAPI 细节 254
- 26.6 TSO 和 TOE 254
- 26.7 MII 和 ethtool 255

> **这些章节可以部分或全部被视为可选的。它们包含了背景参考资料、专门主题或高级课题。教师可以根据课堂经验和时间限制选择涵盖或不涵盖它们。**

## 26.1 组播

组播网络包被发送到多个（但不是所有）网络目标。为了这一目的，给一组主机分配了一个唯一的硬件地址；任何发送到该地址的包都将由该组的所有成员接收。

以太网要求目标地址第一个字节的最低位被设置为 1；同时，设备地址第一个字节的第一位被清零。

组播包看起来与其他任何数据包没有区别，因此设备不需要特殊的处理来传输。这取决于内核将它们路由到正确的硬件。

然而，组播包的接收更为复杂，取决于网络设备的复杂程度，可能需要更多或更少的工作。某些设备具有特殊的组播能力。它们接收直接发送到其硬件或广播到所有地址的包。它们仅通过接收包来接收组播流量；这可能会导致系统崩溃。此类设备在其 `net_device` 结构体中没有 `IFF_MULTAST` 标志。

第二类设备可以区分组播包和普通包；它们接收每个包，并让软件决定是否是为它们准备的以及应该采取。这一类的开销比第一类低。

第三类设备在硬件中执行组播检测。这种类型的设备接受一个组播地址列表并忽略所有其他地址。这是最高效的设备，因为它们不需要在接收后再丢弃它们。每当有效组播地址列表被修改时，内核就会更新与设备关联的列表：

```
void (*set_multicast_list)(struct net_device *dev); (其中 dev 是设备的 net_device)。
```

设备关联的 `net_device` 结构体如下：

```
struct net_device_list {
    struct net_device_list *next;   /* 列表中的下一个 */
    u8 dmi_addr[ADDR_LEN];           /* 硬件地址 */
    unsigned char dmi_len;          /* 地址长度 */
    int dmi_users;                   /* 用户数 */
    int dmi_groups;                  /* 组数 */
};
```

`struct net_device_list *mc_list;` 每当有效组播地址列表被修改时，内核会调用：

`void (*set_multicast_list)(struct net_device *dev);`（其中 dev 是设备的 net_device）。如果驱动程序实现此函数，应返回 NULL。

`flags` 中的一些标志影响行为：

表 26.1：组播标志

| 标志 | 含义 |
|---|---|
| `IFF_MULTAST` | 如果未设置，设备将不处理组播包。 |
| `IFF_ALLMULTI` | 告知接收所有包。 |
| `IFF_PROMISC` | 将接口设置为混杂模式。 |

Corbet、Rubini 和 Kroah-Hartman 给出了 `set_multicast_list()` 方法的示例。

## 26.2 链路状态变化

### 26.2 链路状态变化

网络连接可能由于外部事件（如插拔电缆）而发生变化。几乎所有网络设备都有感知载波的能力；存在时意味着硬件可用。Linux 提供了以下函数在状态发生变化时通知其他网络层：

```
void netif_carrier_on(struct net_device);
void netif_carrier_off(struct net_device);
int netif_carrier_ok(struct net_device);
```

当驱动检测到状态变化时，调用 on 和 off 函数。它们也可以用于封装主要的配置更改或重置。

最后一个函数通过检查 `net_device` 结构体来感知。

## 26.3 ioctl



当 `ioctl()` 命令传递给套接字描述符时，首先与 `/usr/src/linux/include/sockios.h` 中定义的命令比较。

如果命令是套接字配置命令，如 `SIOCSIFADDR`，则由网络高层直接处理。

命令可能是头文件中定义的协议特定函数。在任何情况下，`ioctl()` 的第三个参数都被强制转换为 `ifreq` 结构指针，定义在 `/usr/src/linux/include/if.h` 中。

如果内核不识别该命令，则将其传递给驱动程序定义的 `do_ioctl()` 方法。

```
int (*do_ioctl)(struct net_device *dev, struct ifreq *ifr, int cmd);
```

注意 `ifr` 字段实际上指向用户传递的数据结构的内核空间副本。因此，驱动程序可以自由使用此结构，而无需调用 `copy_to_user()` 函数。

## 26.4 NAPI 和中断缓解

## 第 26 章. 网络驱动程序 IV：可选主题

能够使用 NAPI 的设备必须能够存储一定数量的数据包（在板载或内存 DMA 缓冲区中）。它还必须能够在禁用数据包接收中断的同时，继续为成功的传输（以及可能的其他事件）发送中断。

具备这些能力后，基于 NAPI 的驱动程序会关闭接收中断，并定期轮询累积的中断。当流量变慢时，重新开启正常中断，驱动程序将按旧方式运行。

应当重复的是，虽然许多设备都有基于 NAPI 的驱动程序，但它们可能无法直接提高吞吐量。然而，它们可以显著降低 CPU 负载。

## 26.5 NAPI 细节

假设设备具备了所需的硬件能力（关闭入站数据包中断以及关闭足够数量数据包的能力）。

必须编写一个函数来处理在入站数据中断关闭期间积累的数据。权重（weight）参数表示通过接口应接受多大的流量，对于 10 MB 的接口，应将其设置为 16；更快的接口应使用 64。权重参数不应大于接口能够存储的数据包数量。

还必须重写中断处理程序，以便当接收到入站数据包时（显然带有入站中断），它应该关闭后续的接收中断，并将数据包交给 `netif_rx_schedule(struct net_device *)` 函数，该函数将最终触发 `poll()` 方法的调用。

当所有可用数据包都已处理后，重新开启接收中断并调用 `netif_rx_complete()`，如果返回值为 0，则关闭轮询。返回 1 表示还需要处理更多数据包。

## 26.6 TSO 和 TOE

TSO（TCP 分段卸载）的目的是允许大于通常 MTU（最大传输单元，仅为 1500 字节）的缓冲区传递给网络设备。

将大缓冲区分解（分段）为较小的 mtu 大小的分段可以通过路由器、交换机等，这通常是由 CPU 在将数据传递给设备之前完成的。

通过 TOE，64 KB 的缓冲区在设备本身上拆分为 44 个 mtu 大的分段。每个片段（或数据包）都使用模板附加了 TCP 和 IP 协议头。

结果是 CPU 负载可能大幅减少，而不是像许多高级技术那样增加带宽。通常，TSO 仅对于高带宽（如 1 GB 或更高）的网络设备重要。

TOE（TCP/IP 卸载引擎）技术的目的是将 TCP/IP 处理移动到网卡上的集成电路上。与 TSO 类似，其想法是释放 CPU 执行其他工作。

与 TSO 不同，TOE 机制同时处理入站和出站流量。由于它是面向连接的协议，TOE 涉及大量的复杂性。

在 Linux 中，内核开发者拒绝包含 TOE，尽管他们非常欢迎它。原因之一是性能水平不足以证明其复杂性。

## 26.7 MII 和 ETHTOOL

此外，TCP/IP 栈在网卡上实现，通常位于闭源的黑盒中，很难保持安全性更新并使行为符合预期。

资源限制（如可以处理的并发连接数）比通用的 Linux 更有限；这可以被用于辅助拒绝服务攻击。

关于 TOE 为何永远不会被主 Linux 内核接受的详细解释，请参考 `http://www.linuxfoundation.org/collaborate/workgroups/networking/toe`。

## 26.7 MII 和 ethtool

许多网络设备符合 MII（介质独立接口）标准，该标准描述了网络控制器与以太网收发器之间的接口。

内核支持通用的 MII 接口，带有：

```c
#include <linux/mii.h>

struct mii_if_info {
 int phy_id;
 int advertising;
 int phy_id_mask;
 int reg_num_mask;

 unsigned int full_duplex : 1; /* is duplex */
 unsigned int force_media : 1; /* is autoneg. disabled? */

struct net_device *dev;
 int (*mdio_read)(struct net_device *dev, int, int, int);
 void (*mdio_write)(struct net_device *dev, int, int, int val);
};
```

嵌入结构中的关键方法是 `mdio_read()` 和 `mdio_write()`，它们负责与接口的通信。还有其他函数用于获取设备信息和更改设备状态，它们也设计为与 ethtool 实用协作。

ethtool 为管理员提供了一系列实用程序用于控制接口属性，如速度、介质类型、双工操作、校验和。驱动程序可能直接支持 ethtool 以充分利用其功能。

相关代码位于 `/usr/src/include/linux/ethtool.h`，并包含了 `ethtool_ops` 结构，其中包含一个可以实现的方法列表：

```c
struct ethtool_ops {
 int (*get_settings)(struct net_device *dev, struct ethtool_cmd *);
 int (*set_settings)(struct net_device *dev, struct ethtool_cmd *);
 void (*get_drvinfo)(struct net_device *dev, struct ethtool_drvinfo *);
 int (*get_regs)(struct net_device *dev);
 void (*get_regs)(struct net_device *dev, struct ethtool_regs *, void *regs);
 void (*get_wol)(struct net_device *dev, struct ethtool_wolinfo *);
 int (*set_wol)(struct net_device *dev, struct ethtool_wolinfo *);
 u32 (*get_msglev)(struct net_device *dev);
 u32 (*get_msglev)(struct net_device *, u32);
 int (*get_eeprom)(struct net_device *dev);
 u32 (*get_link)(struct net_device *);
 int (*get_eeprom_len)(struct net_device *);
 int (*get_eeprom)(struct net_device *, struct ethtool_eeprom *, u8);
 int (*get_eeprom)(struct net_device *, struct ethtool_coalesce *, u8 *);
 int (*get_coalesce)(struct net_device *dev, struct ethtool_coalesce *);
 int (*set_coalesce)(struct net_device *dev, struct ethtool_coalesce *);
```

要为你的设备启用 ethtool，你必须使用 `SET_ETHTOOL_OPS` 在 `netdevice` 中设置指向此结构的指针。如果也启用了 MII 支持，可以使用 `mii_ethtool_gset()` 和 `mii_ethtool_sset()` 函数来实现 `get_settings()` 和 `set_settings()` 方法。

它们是，描述它们的标准，集线器、外设和主机控制器的连接拓扑，以及涉及的各种描述符。我们将考虑可能的各种类别和数据传输。然后我们将看到 USB 在 Linux 下是如何实现的。回顾 USB 设备的注册/注销。我们将描述驱动程序的入口点以及一些主要函数和数据结构。最后，我们将对一个简单的 USB 驱动程序进行代码分析。



![](img/134c1b05ee9bbbe93ba3f435720ac1_272.png)

| | |

|---|--|

| 27.1 | 什么是 USB? | 257 |

| 27.2 | USB 拓扑 | 258 |

| 27.3 | 描述符 | 259 |

| 27.4 | USB 类 | 260 |

| 27.5 | 数据传输 | 260 |

| 27.6 | Linux 下的 USB | 261 |

| 27.7 | 注册 USB 设备 | 262 |

| 27.8 | USB 驱动示例 | 264 |

| 27.9 | 实验 | 266 |

# 27 USB 驱动程序

我们将讨论 USB 设备、它们是什么、描述它们的标准、集线器、外设和主机控制器的连接拓扑以及涉及的各种描述符。我们将考虑可能的各种类别和数据传输。然后我们将看到 USB 在 Linux 下是如何实现的。回顾 USB 设备的注册/注销。我们将描述驱动程序的入口点以及一些主要函数和数据结构。最后，我们将对一个简单的 USB 驱动程序进行代码分析。

## 27.1 什么是 USB?

- USB 代表通用串行总线。它允许将多个外设设备连接到一个端口，并在计算机运行时对连接（和拔除）的设备进行自动热插配置。几乎任何类型的外设（具有 USB 能力）都可以连接到 USB 端口；例如扫描仪、调制解调器、网卡、鼠标、打印机、存储设备等。
- 规范的 1.0 版本于 1996 年 1 月由康、英特尔、微软和 NEC 组成的联盟发布。1.1 版本于 1998 年 9 月发布，2.0 版本于 1999 年发布。
- 在考虑 USB 2.0 标准时，需要注意的是，当使用全速（full speed）或低速（low speed）短语时，指的是 USB 1.1。较新的标准被描述为高速（high speed）。
- 最多可以同时连接 127 个设备。USB 线包含四根线：电源、地线和两根信号线。在原始标准中，理想的总带宽被限制为 12 Mbit/s，但由于开销将其限制在 8.5 Mbit/s 左右，实际性能可能低至 2 Mbit/s。USB 2.0 引入了 480 Mbit/s 的理论速度限制。
- 设备可以是低速或高速，也可以根据功能运行在任种模式。连接到 USB 1:1 控制器或集线器的高速设备将受到较低能力限制的限制。
- 电源可以通过 USB 电缆传输，也可以通过外设自身的电源传输。每个控制器最多可提供 500 mA 电电。当设备插入时，它最初可以获取多达 100 mA，如果没有超过限制，则可以请求更多。
- 内核在 `/usr/src/linux/Documentation/usb` 目录下包含大量与 USB 相关的文档。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_273_0.png)

- 内核版本 2.6.31 包含了对新的 USB 3.0 标准（也称为 XHCI）的支持，使 Linux 成为第一个整合该标准的操作系统。
- USB 3.0 设计传输速率高达 5 GBit/s，降低了功耗，并向下兼容 USB 2.0。

## 27.2 USB 拓扑

![](img/134c18b05ee9bbbe93ba3f4335720ac1_273_1.png)

图 27.1：USB 拓扑

- 所有现代主板都集成了 USB 端口。在大多数情况下至少有 2 个端口。端口可以直接连接到设备，也可以连接到集线器，而集线器本身可以连接到更多的集线器或设备。主机控制器模拟了一个虚拟根集线器。端口加集线器的总数为 127。

## 27.3 描述符

- 从技术上说，USB 的物理结构并不是总线；它是一个具有上行节点和下行节点的树形结构。每个设备只能有一个上行连接（使用 A 类型连接器），但集线器节点可以有多个下行连接（使用 B 类型连接器）。
- 对于 USB 1.x，有两种类型的主机控制器：
  - 来自 Compaq 的 `OHCI`（开放主机控制器接口）。
  - 来自 Intel 的 `UHCI`（通用主机控制器接口）。
  `UHCI` 更加简单，因此需要一个相当复杂的设备驱动程序。外设在任何一种控制器上工作效果都同样良好。
- 对于 USB 2.0，标准是 `EHCI`（增强型主机控制器接口）。
- 连接到总线后，外设会识别自己属于若干类别中的某一个。当加载特定的驱动程序时，它将接管该设备并处理与其所有的通信。

### 27.3 描述符 (Descriptors)

![](img/134c18b05ee9bbbe93ba3f4335720ac1_274_0.png)

图 27.2：USB 描述符

- 每个 USB 设备都有一个唯一的设备描述符，在对外设连接到总线时分配给它。此外，它还会获得一个分配的设备号（从 1 到 127 的整数）。描述符包含了适用于该设备及其所有可能配置的所有相关信息。
- 设备具有一个或多个配置描述符。这包含了关于设备如何被使用的具体信息。
- 每个配置都指向一个或多个接口描述符。每个接口都可能指向关于设备如何使用的各种备用设置。例如，视频摄像头可能有三种备用设置，它们需要不同的带宽：摄像头激活、麦克风激活以及摄像头和麦克风激活。
- 每个接口指向一个或多个端点描述符，这些描述符提供了设备的数据源或汇点。（所有控制传输都使用零端点。）

## 27.4 USB 设备类

如果插入 USB 的设备属于某个已知的设备类，则预计它在设备和接口描述符方面符合某些标准。因此，同一个设备驱动程序可以用于任何声称是该类成员的设备。标准中定义了以下类别：

表 27.2：USB 设备类

| 基础类 | 描述符用途 | 描述 | 示例 |
|---|---|---|---|
| 00h | 设备 | 未指定 | 在接口描述符中使用类信息 |
| 01h | 接口 | 音频 | 扬声器、麦克风、声卡 |
| 02h | 两者 | 通信和 CDC 控制 | 网络适配器、调制解调器、串口适配器 |
| 03h | 接口 | HID（人机接口设备） | 鼠标、摇杆、键盘 |
| 05h | 接口 | 物理 | 力反馈摇杆 |
| 06h | 接口 | 图像 | 数字相机 |
| 07h | 接口 | 打印机 | 打印机 |
| 08h | 接口 | 质存储 | 优盘、MP3 播放器、内存卡阅读器 |
| 09h | 设备 | 集线器 | 全速和高速集线器 |
| 0Ah | 接口 | CDC-数据 | 与 CDC 控制配合 |
| 0Bh | 接口 | 智能卡 | 智能卡读卡器 |
| 0Dh | 接口 | 内容安全 | 安全 |
| 0Eh | 接口 | 视频 | 摄像头 |
| 0Fh | 接口 | 个人健康 | 医疗设备 |
| DCh | 两者 | 诊断设备 | USB 合规性测试设备 |
| E0h | 接口 | 无线控制器 | 蓝牙和 Wi-Fi 适配器 |
| EFh | 两者 | 杂项 | ActiveSync 设备 |
| FEh | 接口 | 特定应用 | 红外桥 |
| FFh | 两者 | 厂商特定 | 需要厂商特定设备的设备 |

其他设备需要编写完全自定义的设备驱动程序。

## 27.5 数据传输

与 USB 设备之间存在以下类型的数据传输：

控制传输是用于配置和获取设备状态的短命令。虽然可能还有特定的命令，但大多数或所有设备将支持 `/usr/linux/include/usb/ch9.h` 中定义的以下标准集：

| | | |
|---|---|---|
| 3.1: | 79 #define `USB_REQ_GET_STATUS` | 0x00 |
| 3.1: | 80 #define `USB_REQ_CLEAR_FEATURE` | 0x00 |
| 3.1: | 81 #define `USB_REQ_SET_FEATURE` | 0x01 |
| | | |
|---|---|---|
| 3.1: | 82 #define `USB_REQ_ADDRESS` | 0x03 |
| 3.1: | 83 #define `USB_REQ_GET_DESCRIPTOR` | 0x05 |
| 3.1: | 84 #define `USB_REQ_SET_FEATURE` | 0x06 |
| 3.1: | 85 #define `USB_REQ_SET_DESCRIPTOR` | 0x07 |
| 3.1: | 86 #define `USB_REQ_GET_INTERFACE` | 0x08 |
| 3.1: | 87 #define `USB_REQ_SET_INTERFACE` | 0x09 |
| 3.1: | 88 #define `USB_REQ_SYNCH_FRAME` | 0x0A |
| 3.1: | 89 #define `USB_REQ_GET_CONFIGURATION` | 0x0B |
| 3.1: | 90 #define (missing text) | 0x0C |
| 3.1: | 91 #define `USB_REQ_ENPTION` | 0x0D |



| 3.1: | 92 `#define USB_REQ_ENPTION` | 0x0E |
| 3.1: | 93 `#define USB_REQ_ABORT` | 0x0F |
| 3.1: | 94 `#define USB_REQ_SIZE` | 0x10 |
| 3.1: | 95 `#define USB_REQ_HANDAKE` | 0x11 |
| 3.1: | 96 `#define USB_REQ_PIPE` | 0x12 |
| 3.1: | 97 `#define USB_REQ_CONNECTION` | 0x13 |
| 3.1: | 98 `#define USB_REQ_SECURITY` | 0x14 |
| 3.1: | 99 `#define USB_REQ_WRITE` | 0x15 |
| 3.1: | 100 `#define USB_REQ_LOOPBACK` | 0x16 |
| 3.1: | 101 `#define USB_REQ_READ` | 0x17 |
| 3.1: | 102 `#define USB_REQ_LOOPBACK` | 0x18 |
| 3.1: | 103 `#define USB_REQ_SET` | 0x19 |
| 3.1: | 104 `#define (missing text)` | 0x1A |
| 3.1: | 105 `#define USB_REQ_DATA` | 0x1B |
| 3.1: | 106 `#define (missing text)` | 0x1C |
| 3.1: | 107 `#define (missing text)` | 0x1D |
| 3.1: | 108 `#define (missing text)` | 0x1E |
| 3.1: | 109 `#define (missing text)` | 0x1F |

## 27.6 Linux 下的 USB

USB 有三层层：
- 主机控制器驱动 (`OHCI`, `UHCI`, `EHCI`)
- USB 核心
- 设备驱动![](img/134c18b05ee9bbbe93ba3f4335720ac1_276_0.png)

## 27.7 注册设备

USB 设备通过以下函数进行注册和注销：

```c
#include <linux/usb.h>

int usb_register(struct usb_driver *drv);
void usb_deregister(struct usb_driver *drv);
```

- `usb_register()` 成功返回 0，失败返回负数。
- 在注册之前，所有重要的 `usb_driver` 结构体必须完全初始化。

```c
struct usb_driver {
    const char *name;
    int (*probe)(struct usb_interface *int, const struct usb_device_id *id);
    void (*disconnect)(struct usb_interface *int);
    int (*ioctl)(struct usb_interface *int, unsigned code, void *buf);
    int (*suspend)(struct usb_interface *int, pm_message_t *message);
    int (*resume)(struct usb_interface *int);
    int (*reset_resume)(struct usb_device_id *id);
    const struct usb_device_id *ids_table;
    struct usb_dynids *dynids;
    struct usb_bdrv_wrap drvwrap;
    unsigned int no_dynamic_autosuspend;
    unsigned int supports_autosuspend;
    unsigned int soft_unbind;
};
```

- `name`：驱动模块。它在所有 USB 驱动中是唯一的，并在加载时显示在 `/sys/bus/usb/drivers`。
- `probe` 指向检查设备的函数，在新设备添加到 USB 总线时调用。如果驱动可以根据传递它的 `usb_device_id` 结构体接管设备，则例程序应初始化设备并返回零。如果驱动不接管，应返回负值。
- `disconnect` 指向设备从 USB 总线移除时调用的函数，而 `suspend` 和 `resume` 指向用于电源管理的函数。
- 仅使用了主要字段；还有其他选项。我们可以有一个：

```c
static struct usb_driver my_usb_my_usb = {
    .name = "my_usb_device",
    .id_table = my_usb_id_table,
    .probe = my_usb_probe,
    .disconnect = my_usb_disconnect,
};
```

## 27.7. 注册 USB 设备

- `id_table` 指向一个类型为 `usb_device_id` 的标识结构，定义在 `/usr/src/linux/include/linux/devicetree.h`：

```c
struct usb_device_id {
    /* which fields to match against? */
    __u16 match_flags;

    /* Used for product specific matches; range is inclusive */
    __u16 idVendor;
    __u16 idProduct;
    __u16 bcdDevice_lo;
    __u16 bcdDevice_hi;

    /* Used for device class matches */
    __u8 bDeviceClass;
    __u8 bDeviceSubClass;
    __u8 bDeviceProtocol;

    /* Used for interface class matches */
    __u8 bInterfaceClass;
    __u8 bInterfaceSubClass;
    __u8 bInterfaceProtocol;

    /* not matched against */
    kernel_ulong_t driver_info;
};
```

- `match_flags` 设置了结构体中其他字段应该与设备进行匹配的内容。通常这不会直接设置；它由我们讨论的 `USB_DEVICE` 宏初始化。
- `idVendor` 是设备唯一的 USB 厂商 ID，由 USB 控制机构分配。`idProduct` 是产品 ID，由厂商设置。
- `bcdDevice_lo`, `bcdDevice_hi` 是厂商确定的产品数的低位和高位。
- `bDeviceClass`, `bDeviceSubClass`, `bDeviceProtocol` 由 USB 控制机构分配，描述整个设备，包括所有接口。
- `bInterfaceClass`, `bInterfaceSubClass`, `bInterfaceProtocol` 描述单个接口。
- `driver_info` 可供驱动程序在调用 `probe()` 时用于区分不同的设备。
- `usb_device_id` 表通常使用以下宏初始化：

```c
USB_DEVICE(vendor, product)
USB_DEVICE_VER(vendor, product, hi)
USB_DEVICE_INFO(class, subclass, protocol)
USB_INTERFACE_INFO(class, subclass, protocol)
```

以直观的方式进行。因此，对于只控制某个厂商中一个设备的简单驱动程序，你可能会有：

```c
static struct usb_device_id my_usb_id_table = {
    { USB_DEVICE(MY_VENDOR_ID, MY_VENDOR_PRODUCT_ID) },
    { /* Null terminator (required) */ }
};
MODULE_DEVICE_TABLE(usb, my_usb_id_table);
```

`MODULE_DEVICE_TABLE` 宏对于用户空间热插拔工具执行其工作是必要的。

你可能已经回调函数没有直接引用 `usb_driver` 结构，而是指向一个类型为 `usb_interface` 的结构。可以通过以下函数在两个结构之间切换：



```c
struct usb_device *interface_to_usbdev(struct usb_interface *intf);
void *usb_get_intfata(struct usb_interface *intf);
void *usb_set_intfata(struct usb_interface *intf);
```

第一个函数获取底层 `usb_device` 的指针。

另外两个函数获取 `struct device_driver` 结构中设置的数据元素的指针，该元素由 `struct usb_interface` 指向的 `struct usb_driver` 结构指向。由于这个私有数据指针嵌套在结构深处，这些函数非常有用。

`no_dynamic_id` 字段允许驱动程序禁用动态设备 ID 的分配。

## 27.8 USB 驱动程序示例

为了看到所有内容是如何结合在一起的，让我们来看看 `/usr/src/linux/drivers/usb/misc/rio500.c`，这是一个用于连接到 USB 端口的 MP3 设备的简单驱动程序。

我们将查看驱动中处理初始化、注册和探测连接的部分。实际的数据传输代码无疑非常依赖于硬件。它主要由 `file_operations` 映射表中指向的入口组成。

注意，这里作为字符设备引用了 `file_operations` 结构：

```c
static const struct file_operations usb_rio_fops = {
      .owner = THIS_MODULE,
      .read = read_io,
      .write = write_rio,
      .locked_ioctl = ioctl_rio,
      .open = open_rio,
      .release = close_rio,
      .llseek = noop_llseek,
};

static struct usb_class_driver usb_rio_class = {
      .name = "rio500d",
      .fops = &usb_rio_fops,
      .min_base = RIO_MINOR,
};
```

`file_operations` 结构由 `struct usb_class_driver` 中的一个项指向，该项将在 `usb_register_dev()` 函数调用中与设备关联，该调用是从 `probe()` 回调发出的。

还有一个类型为 `usb_device_id` 的结构指向回调函数：

```c
static const struct usb_device_id rio_table[] = {
    { USB_DEVICE(0x0841, 1) },
    /* Rio 500 * */
};  /* Terminating entity */
```

```c
MODULE_DEVICE_TABLE(usb, rio_table);

static struct usb_driver rio_driver = {
      .name = "rio500",
      .probe = probe_rio,
      .disconnect = disconnect_rio,
      .id_table = rio_table,
};
```

注意 `init` 函数只是简单地注册了 `usb_driver` 结构：

```c
static int __init_usb_rio(void) {
      int retval;
      retval = usb_register(&rio_driver);
      if (retval)
          goto out;
      printk(KERN_INFO "%s: %d\n", DRIVER_NAME, retval);
out:
      return retval;
}
```

同样，清理（或退出）函数简单地注销：

```c
static void __exit_usb_rio(void) {
      struct rio_usb_data *rio = &rio_instance;
      rio->present = 0;
      usb_deregister(&rio_driver);
}
```

实际工作由 `probe()` 和 `disconnect()` 函数完成，在资源设置和释放方面。这些入口点是由 USB 核调用的，而不是用户空间。

`probe()` 和 `disconnect()` 函数如下：

```c
static int probe_rio(struct usb_interface *intf) {
      const struct usb_device_id *id;
      usb_device *dev = interface_to_usbdev(intf);
      struct rio_usb_data *rio = &rio_instance;
      int retval;

      dev_info(&intf->dev, "USB found at %d\n", dev->devnum);
      retval = usb_register_dev(intf, &rio_class);
      if (retval)
             err("Not able to get a minor for this device.");
          return -ENOMEM;
      return retval;

      rio->rio_dev = dev;
      if (!(rio->obuf = kmalloc(GBUF_SIZE, GFP_KERNEL))) {
          err("probe_rio: Not enough memory for the output buffer\n");
          usb_unregister_dev(intf, &rio_class);
          return -ENOMEM;
      }
      dbg("probe_rio: obuf address:%p\n", rio->obuf);

      if (!(rio->oibuf = kmalloc(GBUF_SIZE, GFP_KERNEL))) {
          err("probe_rio: Not enough memory for the input buffer\n");
          usb_unregister_dev(intf, &rio_class);
          kfree(rio->obuf);
          return -ENOMEM;
      }
      dbg("probe_rio: ibuf address:%p\n", rio->oibuf);

      mutex_init(&(rio->lock));
      usb_set_intfdata(intf, rio);
      rio->present = 1;
      return 0;
}

static void disconnect_rio(struct usb_interface *intf) {
      struct rio_usb_data *rio = usb_get_intfdata(intf);

      rio->present = 0;
      usb_unregister_dev(intf, &rio_class);
      kfree(rio->obuf);
      kfree(rio->oibuf);
}
```

## 27.9 实验

### 实验 1：安装 USB obuf

- 我们将编写一个简单的 USB 设备驱动程序。
- 驱动程序应该在加载时向 USB 子系统注册，并在卸载时注销。
- 当设备从系统中添加或移除时，`probe()` 和 `disconnect()` 函数应该发出输出。
- 通过正确使用 `usb_device_id` 表，你可以配置驱动程序，使其检测任何插入的设备，或仅检测特定设备。你可以通过记录 USB 子系统感知连接时的输出获取厂商和设备 ID。
- 你必须确保你的内核已经编译了正确的 USB 支持，并且没有已经加载该设备的驱动程序，因为这可能会干扰你的驱动程序接管设备。
- 提示：你可能需要执行 `make modules_install` 以让自动加载正常工作。

# 第 28 章

## 存储技术设备 (MTD)

![](img/134c18b05ee9bbbe93ba3f4335720ac1_282_0.png)

我们将考虑不同类型的 MTD 设备、它们的实现方式以及与它们配合各种文件系统。



| 28.1 什么是 MTD 设备？ .................................................................................................................삭 | 267 |
| 28.2 NAND 与 NOR ................................................................................................................................. . . . . . . | 268 |
| 28.3 驱动程序与用户模块 ................................................................................................................................. . . . | 269 |
| 28.4 闪存文件系统 ................................................................................................................................................. . | 269 |
| 28.5 实验 ................................................................................................................................................................................. . . . . . . | 270 |

> **这些章节可以部分考虑或作为可选内容。它们包含了背景参考资料、专门主题或高级课题。教师可能会根据课堂经验和时间限制选择涵盖或不涵盖它们。

## 28.1 什么是 MTD 设备？

- 存储技术设备（MTD）是闪存存储设备。它们通常用于各种嵌入式设备。
- 此类设备可能其所有内存都在闪存中（其功能类似于硬盘，在掉电后仍保留值），但它通常会带有某种类型的普通 RAM。
- 闪存是一种高速 EEPROM，其数据以块为单位进行编程（和擦除），而不是像普通 EEPROM 那样按字节逐字节。
- MTD 设备既不是字符设备也不是块设备；特别是，它们区分了写操作和擦除操作，而块设备则不区分。
- 由于许多原因，普通文件系统通常不适用于闪存设备（我们将在稍后详细说明），因此设计了专门的文件系统。
- 现地执行（Execute in Place，简称 XIP）方法是指 CPU 将位于闪存的应用程序内存页直接映射到其虚拟地址空间，并先将页面复制到 RAM，这在嵌入式设备中非常有用。
- 一些有用的参考：

### 表 28.1：MTD 链接

| http://www.linux-mtd.infrade.org | Linux MTD 开发的主站。 |
| http://www.linuxforddevices.com/articles/A1T7478621147.html | Cliff Brake 和 Jeff Sutherland 关于在嵌入式 Linux 系统中使用闪存的论文。 |

## 28.2 NAND 与 NOR

- 有两种基本的闪存：NOR 和 NAND。
- NOR 闪存设备是较旧的，具有以下特征：
  - 线性寻址设备，具有独立的数据线和地址线；就像 DRAM 一样。
  - 地址可以直接映射到 CPU 的地址空间并像 ROM 一样访问。
  - 编程和擦除速度尚可；擦除比编程慢。
  - 功能像 RAM 一样，支持随机访问。
  - 擦除周期次数有限，大约 100,000 次左右。
  - 近期 MLC（多层单元）技术的发展，每个存储单元可以存储两个比特内存，提高了密度并降低了每个单位内存的制造成本，尽管可能以性能下降为代价。
  - 传统上这些设备与数据存储相关。
- NAND 闪存设备是较新的，具有以下特征：
  - 寻址是非线性的；数据和命令在 8 条 I/O 线上复用。因此，设备驱动程序更复杂。
  - 访问是顺序的。
  - 密度高于 NOR 设备，速度快一个数量级。
  - 坏块可能是一个问题；NAND 设备出厂时带有坏块，但在任何时候都可能出现。
- 传统上这些设备与数据存储相关。
- 自 1999 年以来，NAND 占据了闪存市场的十分之一。
- 无论底层设备使用何种方法，Linux 都可以使用相同的方法来访问它。
- 这里有一个 `http://www.linux-mtd.infrade.org/doc/nand.html` 的表，说明了 NAND 和 NOR 设备之间的差异：

## 28.3 驱动程序与用户模块

### 表 28.2：NOR 与 NAND 设备

| 特征 | NOR | NAND |
| --- | --- | --- |
| 接口 | 总线 | I/O |
| 单元大小 | 大 | 小 |
| 成本 | 高 | 低 |
| 读取时间 | 快 | 慢 |
| 编程时间（单字节） | 慢 | 慢 |
| 编程时间（多字节） | 慢 | 快 |
| 擦除时间 | 快 | 快 |
| 功耗 | 高 | 低，但需要 RAM |
| 可执行 | 是 | 否，但新的芯片可以部分 |
| 位操作 | 几乎严格 | 允许页限制 |
| 出厂时的坏块 | 否 | 是 |

## 28.4 闪存文件系统

- `initrd`（初始内存磁盘）
- 闪存文件系统
- 日志文件系统 JFFS
- 闪存转换层（FTL）
- 日志文件系统 JFFS2

## 28.5 实验

### 实验 1：在内存中模拟 MTD

- 如果你的系统上没有 MTD 设备，可以使用一些内置内核功能在内存中模拟它们。
- 首先，你必须确保内核中构建了所有正确的设施。进入内核源码目录，执行 `make xconfig` 并开启相应的 MTD 选项，同时包含 jff2 文件系统。

如果你已经将所有内容都作为模块处理，那么可能不需要重启就能生效，只要你运行了 `depmod`。无论如何，请重新编译、重启等，以进入现在包含了 MTD 和 JFFFS2 的内核。

我们将测试字符仿真接口。要做到这一点，你必须确保创建了设备节点：

```
$ mknod -m 666 /dev/mtd0 90 0
```

在此操作之前或之后，你都必须确保执行了：

```
$ /sbin/modprobe mtdram total_size=2048 erase_size=8
```

（或者留空选项以获取你编译到内核中的默认值。）如果你没有以模块形式执行这些，则不需要运行 `modprobe`。

你可以将其用作原始字符内存磁盘并对其进行读写。尝试使用 `dd`、`cat`、`echo` 等工具进行实验。

### 实验 2：jff2 文件系统和 MTD 块接口。

为了在 MTD 设备上放置 jff2 文件系统，最简单的方法是在另一个文件系统上创建一个文件系统镜像，然后将其拷贝过去。为了做到这一点，你必须使用 `mkfs.jff2` 工具，你可以从 `http://sourceware.org/jff2` 下载源码或二进制格式的工具。

如果你还没有在内核中构建它，则需要执行：

```
$ /sbin/modprobe mtdblock
```

你还需要创建正确的设备节点：

```
$ mknod -m 666 /dev/mtd0 b 31 0
```

（注意，你必须先完成上一个实验，并保持模块加载状态，本实验才能正常工作。）

向目录树（例如 `/dir_tree`）中填充一些文件和子目录；总大小应该小于或等于 MTD 内存磁盘的大小。在上面放置一个文件系统并使用以下命令将其拷贝到 MTD 块仿真器中：

```
$ mkfs.jff2 -d ./dir_tree -o /dev/mtdblock
```

（你可能想分开这些步骤，以便保留初始的文件系统镜像；即不要直接执行：

```
$ mkfs.jff2 -d ./dir_tree -o jff2.image
$ dd if=jff2.image of=/dev/mtdblock
```

现在你就可以挂载文件系统并尽情玩玩它了：

```
$ mkdir /mnt_jff2
$ mount -t jff2 /dev/mtdblock /mnt_jff2
```

注意，你可以随所欲地更改文件系统的内容，但在卸载 MTD 模块或重启时，更新将会丢失。不过，你可以将内容拷贝到镜像文件中并保存以便以便恢复。

注意，如果你开启了某些详细输出，你将看到如下消息：



```
Feb 20 09:02:48 p3 kernel: ram_read(pos:520192, len:4096)
Feb 20 09:02:48 p3 kernel: ram_write(pos:393216, len:12)
Feb 20 09:02:48 p3 kernel: ram_read(pos:262144, len:4096)
Feb 20 09:02:48 p3 kernel: ram_read(pos:266240, len:4096)
Feb 20 09:02:48 p3 kernel: ram_read(pos:270336, len:4096)
```

以及其他此类诊断信息，这将帮助你检查磁盘内部的情况。

- 注意，由于 `jffs` 是一种压缩文件系统，根据实际内容，你可以容纳远超标称的大小。

# 第 29 章 电源管理

![](img/134c18b05ee9bbbe93ba3f4335720ac1_288_0.png)

我们将讨论如何在 Linux 下使用 APM 或 ACPI 协议进行电源管理。我们将考虑系统可能处于的状态，以及电源管理功能有哪些。

| 节 | 页码 |
| :--- | :--- |
| 29.1 电源管理 | 273 |
| 29.2 ACPI 和 APM | 274 |
| 29.3 系统电源状态 | 274 |
| 29.4 回调函数 | 275 |
| 29.5 实验 | 276 |

## 29.1 电源管理

- 电源管理由作为设备加载一部分注册的回调函数处理。这些函数的地址作为函数指针提供在相应的结构体（如 `pci_driver`、`usb_driver` 等）中。

- 在较低层次，`device_driver` 结构体将包含这些函数的指针：

```c
struct device_driver {
    int (*probe) (struct device * dev);
    int (*remove) (struct device * dev);
    void (*shutdown) (struct device * dev);
    int (*suspend) (struct device * dev, pm_message_t state);
    int (*resume) (struct device * dev);
}
```

- 许多驱动程序编写时仅提供了这些函数中的某些，甚至一个都没有。这可能是因为硬件没有先进的电源功能。

- 更常见的原因是因为在急于让设备驱动程序运行的过程中，电源管理回调函数被搁之脑后，被视为以后再做的增强或优化。遗憾的是，它们并没有被编写得当，或者根本就没写。

- 内核开发者社区对此已经表达了相当大的沮丧，甚至尝试拒绝合并未能满足这些回调函数的驱动程序。

- `lesswatts` (`http://www.lesswatts.com`) 包含了许多关于工具、文档和方法的信息，可以让 Linux 更好地控制电源管理并减少整体功耗。

## 29.2 ACPI 和 APM

- 几乎所有的 x86 主板都支持 ACPI（高级配置与电源接口）。较旧的 APM（高级电源管理）接口已经相当过时，我们对此不再多说。

- 大区别在于，APM 将电源管理交给了 BIOS，而 ACPI 将其交给了操作系统。

- APM 和 ACPI 都要求系统处于某种状态。如果 ACPI 不可用且在使用 APM，则其中某些函数将变得不兼容。

## 29.3 系统电源状态

- 在 ACPI 下有状态的划分，G 代表全局，S 代表睡眠，这些状态包括：

| 状态 | 值 | 含义 |
| :--- | :--- | :--- |
| G | G0 | 全电源工作，用户代码运行。 |
| G | G1 | 软关闭，少量电源。 |
| G | G2 | 软关闭，最小电量。 |
| G | G3 | 关闭，除时钟外无供电。 |
| S | S0 | 工作，全电源，用户代码运行。 |
| S | S1 | 睡眠，低功率状态。 |
| S | S3 | 睡眠，深度睡眠。 |
| S | S4 | 休眠，一种特殊的睡眠状态，保存在非易失性存储中。 |
| S | S5 | 关闭，电源中断。 |

- ACPI 还提供了设备状态定义。范围从 D0 到 D3。所有设备都定义 D0 和 D3，但 D1 和 D2 是可选的。

| 值 | 含义 |
| :--- | :--- |
| D3 | 关闭。设备无电源。上下文丢失；恢复时必须初始化。 |
| D2 | 取决于类别。比 D1 节省更多电。设备可能会丢失部分上下文。 |
| D1 | 取决于类别。比 D2 保留更多上下文。 |
| D0 | 设备全电源，完全激活，保留所有上下文。 |

## 29.4 回调函数

- 以下函数是 ACPI 接口的一部分。如果 ACPI 不可用且在使用 APM，则其中某些函数将变为空操作（no-ops）。驱动程序不需要专门感知使用的是哪种方案；但它们必须处理挂起或恢复请求。

- 对于 PCI 设备，电源管理设施可以通过关联设备的 `pci_driver` 数据结构中元素指向的函数来实现。例如，对于 USB 我们有：

```c
struct usb_driver {
  struct module *owner;
  const char *name;
  int (*probe) (struct usb_interface *intf, const struct usb_device_id *id);
  void (*disconnect)(struct usb_interface *intf);
  int (*ioctl) (struct usb_interface *intf, unsigned int code, void *buf);
  int (*suspend) (struct usb_interface *intf, pm_message_t *message);
  int (*resume) (struct usb_interface *intf);
  const struct usb_device_id *id_table;
  struct device_driver *driver;
};
```

- 2.6 系列内核包含了一个通用接口，其主要函数和数据结构如下

```c
#include <linux/pm.h>
```

```c
struct pm_dev *pm_register(struct pm_dev_t type, unsigned long id, pm_callback callback);
void pm_unregister(struct pm_dev *dev);
void pm_access(struct pm_dev *dev);
void pm_dev_idle(struct pm_dev *dev);
int (*callback) (struct pm_dev *dev, pm_request_t rqst, void *data);

struct pm_dev {
  struct pm_dev_t type;
  unsigned long id;
  pm_callback callback;
  void *data;
  unsigned long flags;
  int state;
  int prev_state;
  struct list_head list_entry;
};
```

- 该接口现在被标记为已弃，不应在新代码中使用。

- 较新的基于设备的接口可以处理几何依赖关系，例如，必须在关闭 PCI 总线之前关闭所有 PCI 设备。此外，使用统一的设备模型更好，而且操作非常直观。

- 有关新旧接口的优秀描述，请参阅 `http://tree.celinuxforum.org/CellPubWiki/PmSubSystem`。

## 29.5 实验

### 实验 1：使用 powertop 监控功耗

- 可以从 `http://www.lesswatts.org/projects/powert/` 获取用于评估功耗的工具。

- `powertop` 可以监控 CPU 每秒唤醒的次数，并帮助减少不必要的活动以节省电力。它还可以跟踪总功耗并建议减少方法。

- 为了让 `powertop` 工作，必须在内核配置中设置 `CONFIG_TIMER_STATS`。

# 第 30 章 异步 I/O

![](img/134c18b05ee9bbbe93ba3f4335720ac1_292_0.png)

我们将讨论异步 I/O、它的功能接口以及在 Linux 下的实现方法。

- 30.1 什么是异步 I/O？ ... 277
- 30.2 Posix 异步 I/O API ... 278
- 30.3 Linux 实现 ... 279
- 30.4 实验 ... 281

**这些章节可以部分或全部被视为可选的。它们包含了背景参考资料、专有主题或高级课题。讲师可能会根据课堂经验和时间限制选择涵盖或不涵盖它们。**

## 30.1 什么是异步 I/O？



所有的 I/O 操作都是同步执行的；应用程序将阻塞，直到读取或写入完成，无论成功或失败。

注意，这并不意味着所有写入都会立即刷新磁盘，而只是与虚拟文件系统的交互已经完成。

但如果 I/O 请求可以被队列，并且程序执行与 I/O 请求的完成并行进行呢？这在 SMP 系统上以及使用 DMA（不涉及 CPU）时特别有用。当实现这一点时，它被称为异步 I/O，或 `AIO`。

为了让其能够正常工作，当 I/O 请求完成时必须有通知，并且代码中包含同步点或完成屏障。

此外，必须设置策略来决定队列请求是否被序列化，特别是当它们引用同一个文件描述符时。

你可以在打开文件时使用 `ASYNC` 标志来请求异步 I/O，或者在 `mount` 命令中使用 `-o async` 选项，但这并不会提供真正的异步 I/O。

# 30.2 Posix 异步 I/O API

POSIX 1.b 标准定义了一个基础数据结构 `aiocb`（AIO 控制块），以及一组可以在 `/usr/include/aio.h` 中执行的基础函数，这些函数由 `glibc` 提供。

数据结构如下：

```c
struct aiocb
{
    int aio_fildes;           /* 文件描述符。 */
    int aio_lio_opcode;      /* 要执行的操作。 */
    int aio_reprio;          /* 请求优先级偏移量。 */
    volatile *aio_buf;       /* 缓冲区位置。 */
    size_t aio_nbytes;       /* 传输长度。 */
    struct sigevent aio_sigevent;  /* 信号编号和值。 */
    __off64_t aio_offset;     /* 文件偏移量 */
};
```

此处我们省略了数据结构的其他成员。

`aio_fildes` 可以是任何文件描述符，但必须是有效的。

`aio_lio_opcode` 用于执行的操作。

`aio_reprio` 用于控制优先级。

`aio_buf` 指向缓冲区。

`aio_nbytes` 是传输长度。

`aio_sigevent` 控制在操作完成时发送的信号。

`aio_offset` 提供文件的偏移量。

这些基础函数并不是 `glibc` 的一部分，而是另一个库 `librt` 的。这些是：

```c
#include <aio.h>

void aio_init(struct aiocb);
int aio_read(struct aiocb);
int aio_write(struct aiocb);
int aio_error(struct aiocb);
size_t aio_return(struct aiocb);
int aio_fsync(struct aiocb);
int aio_cancel(int fd, struct aiocb);
```

# 30.3 Linux 实现

```c
struct aiocb *cb = malloc(sizeof(aiocb));
char *buf = malloc(nbytes);

fd = open(...);
cb->aio_fildes = fd;
cb->aio_nbytes = nbytes;
cb->aio_offset = offset;
cb->aio_buf = buf;

rc = aio_read(cb);

while (aio_error(cb) == EINPROGRESS) {
    // 等待
}
```

Linux 的原始 AIO 实现是由 `glibc` 完全在用户空间完成的。为每个待处理 AIO 请求的文件描述符启动了一个线程。

如果有大量此类请求，这种方法是昂贵的；内核内部真正的支持可以带来更好的性能。

2.6 内核包含了对 AIO 的支持；事实上，如果设置了某些标志，I/O 实际上是通过异步方法完成的

关于此实现的详细文档可以在 `http://ise.sourceforge.net/io/alionotes.txt`。

网络设备驱动已经充分利用了异步实现。然而，字符驱动（很少需要异步化）需要专门修改以利用这一新功能。这需要在 `file_operations` 跳表结构中提供新的函数：

```c
ssize_t (*aio_read) (struct kioc *iocb, struct iovec iov, unsigned long long,
	loff_t *pos);
ssize_t (*aio_write) (struct kioc *iocb, struct iovec iov, unsigned long long,
	loff_t *pos);
int (*aio_fsync) (struct kioc *iocb, int datasyncync);
```

因为 `glibc` 尚未利用 Linux 对 AIO 的完全支持。因此，即使你在驱动程序中放置了这些条目，永远永远被触发。（实际上，如果你没有普通的读写写条目，内核会调用异步接口，如果你想测试它们的话。）

然而，Linux 的新系统中有一个原生的用户空间 API 可以高效使用；这以前是不可能的。要使用它，你必须安装 `libaio-dev` 包，如果你想编译使用它的代码，需要安装 `libaio` 包。你的代码必须包含头文件 `/usr/include/libaio.h`。基础函数是：

```c
#include <libaio.h>
```

```c
io_setup (unsigned nr_events, aio_context_t ctx_id, struct iocb **iocbpp)
io_submit (aio_context_t ctx_id, long nr, struct iocb *iocb)
io_getevents (aio_context_t ctx_id, long min_nr, long nr, struct io_event *events, struct timespec *timeout);
io_destroy (aio_context_t ctx);
io_cancel (aio_context_t ctx_id, struct iocb *cb, struct io_event *result);
```

这些函数都有对应的 man 手页，我们不再对其进行完全描述。

在进行任何 I/O 工作之前，必须先设置一个上下文并包含之前的任何队列中的调用；否则内核可能不知道这些调用与谁关联。这是通过调用 `io_setup()` 来完成的，其中必须初始化上下文；例如：

```c
io_context_t ctx = 0;
rc = io_setup (maxevents, &ctx);
```

其中 `maxevents` 是可以接收的异步事件的最大数量。返回的句柄作为参数传递给其他函数。当你完成后，`io_destroy()` 函数将清除上下文。

`io_submit()` 函数用于提交异步请求，这些请求的 `iocb` 结构已经正确设置。

`io_getevents()` 函数用于检查状态，而 `io_cancel` 可用于尝试取消挂挂的请求。（注意：`events` 参数必须指向一个事件数组，其大小至少要等于你正在查找的最大事件数。文档对这一点说明得清楚，漏掉这一点是导致段错误的好方法。）

控制块结构本身如下：

```c
struct iocb {
void *data;      /* 在 io 完成事件中返回 */
unsigned key;   /* 用于标识请求 */

short	aio_list_opcode;
short	aio_reqrio;
aio_fildes;
int;

union {
struct io_iocb_common		c;
struct io_iocb_vector		v;
struct io_iocb_poll		poll;
struct io_iocb_sockaddr	saddr;
} u;
};

struct io_iocb_poll {
int events;
};		/* 结果码是结果标志的集合或负值 errno */

struct io_iocb_sockaddr {
struct sockaddr	*addr;
int		len;
};		/* 结果码是 sockaddr 的长度，或负值 errno */

struct io_iocb_common {
void *buf;
unsigned long nbytes;
long long      offset;
}; /* 结果码是读取的量或负值 errno */

struct io_iocb_vector {
    const struct iovec *vec;
    int                 nr;
    long long          offset;
}; /* 结果码是读取的量或负值 errno */
```



虽然你仅通过这些函数就可以完成工作，但在提交请求之前，在相应的位置插入所有正确的值可能会非常繁琐。头文件中有很多辅助函数，它们会为你完成大部分工作。遗憾的是，`man` 手页没有提到它们。其中有两个函数你绝对会想要使用：

```c
void io_prep_read(struct iocb *iocb, int fd, void *buf, size_t count, long long offset);
void io_prep_write(struct iocb *iocb, int fd, void *buf, size_t count, long long offset);
```

在以明显的方式调用这些函数后，你只需调用 `io_submit()` 来让你的 I/O 运行。

## 30.4 实验

### 实验 1：为字符驱动程序添加异步入口点

- 选取你之前的字符驱动程序之一，为 `aio_read()` 和 `aio_write()` 添加新的入口点。
- 为了测试这一点，你需要编写一个使用原生 Linux API 的用户空间程序。让它发送数量写/读请求并进行正确的同步。
- 我们还提供了一个使用 Posix API 的用户应用程序解决方案；注意，除非你注释掉普通的读/写入口点，否则它永远不会命中你的驱动程序，在这种情况下内核将回退到异步入口点。
- 确保在链接正确的库时进行编译；Linux API 使用 `-laio`，Posix API 使用 `-lrt`（在任何情况下你都可以使用这两者，因为它们不冲突）。

# 第 31 章

# I/O 调度

我们将考虑 I/O 调度以及 Linux 使用的各种算法。

- 31.1 I/O 调度 ........................................................................................ 283
- 31.2 可调参数 ................................................................................................................. 285
- 31.3 noop I/O 调度器 ................................................................................... 286
- 31.4 Deadline I/O 调度器 ............................................................................ 286
- 31.5 完全公平队列调度器 (CFQ) ..................................... 287
- 31.6 Anticipatory I/O 调度器 ................................................ 287
- 31.7 实验 ................................................................................................................ 288

## 31.1 I/O 调度

- I/O 调度器提供了通用块层与低层设备驱动程序之间的接口。VM 层和 VFS 层都会向块设备提交 I/O 请求；I/O 调度层负责在请求到达设备之前对其进行优先级排序。I/O 调度器根据不同的策略来决定请求的执行顺序，以优化吞吐量或延迟。
- noop 调度器不进行任何调度，简单地按照请求顺序处理，这适用于 SSD 等已经具备内部调度能力的设备。
- Deadline 调度器为每个请求设置一个截止时间，以防止请求饥饿。
- CFQ (Completely Fair Queue) 试图为每个进程公平地分配 I/O 带宽。
- Anticipatory 调度器在处理完一个读请求后稍作等待，以预测下一个相邻的读请求，从而减少磁头寻道。

## 31.2 可调参数

- 每个 I/O 调度器都通过 `sysfs` 暴露了一些参数，可以在运行时进行调整。
- 这些参数通常位于 `/sys/block/<device>/queue/` 目录下。

## 31.3 noop I/O 调度器

### noop I/O 调度器

- 这种简单的调度器主要关注磁盘利用率。对于给定的设备，维护单一队列。对于每个请求，都会确定该请求是否可以与任何现有的请求合并（向前或向后）。如果不能，则根据起始位置将请求插入队列。
- 为了防止请求过期，使用一种老化算法来确定一个 I/O 请求被新请求跳过的次数，并由一个阈值促使该请求被处理。
- noop 调度器对于非磁盘块设备（如内存盘）以及具有其自有的 I/O 调度软件和缓存机制的特殊硬件（例如某些 RAID 控制器）特别有用。通过让自定义的硬件/软件组合做出决策，该调度器的性能实际上可能优于更复杂的替代方案。

## 31.4 Deadline I/O 调度器

- Deadline I/O 调度器激进地重新排序请求，其目标同时是提高整体性能和防止单个请求出现长时间延迟（即饥饿）。
- 对于每一个请求，内核都会关联一个截止时间。读取请求的优先级高于写入请求。
- 维护着五个独立的 I/O 队列：
- 维护两个排序列表，一个用于读取，一个用于写入，并按起始块排序。
- 维护两个 FIFO（先进先出）列表，同样一个用于读取，一个用于写入。这些列表按提交时间排序。
- 第五个队列包含要发送到设备驱动本身的请求。这被称为分发队列（dispatch queue）。
- 请求究竟如何从前四个队列中取出并放入第五个队列（分发队列），是该算法的艺术所在。

### 可调参数 (Tunables)

- `read_expire`:
- `write_expire`:
- `writes_starved`:
- 我们应该优先处理多少次读取而非写入请求。（默认值 = 2）
- `fifo_batch`:
- `front_merges`:
- 向后合并比向前合并更常见，因为连续的请求通常会持续到下一个数据块。将此参数设置为 0 会禁用向前合并，如果你知道它们可能不需要，则可以获得性能提升。（默认值 = 1）
- 详细的文档可以在此处找到：`/usr/src/linux/Documentation/block/deadline-sched.txt`。

## 31.5 完全公平队列调度器 (CFQ)

### 31.5 完全公平队列调度器

- `cfq`（完全公平队列）方法的目标是在所有提交请求的进程之间平均分配 I/O 带宽。
- 理论上，每个进程都有自己的 I/O 队列，这些队列与分发队列协同工作，后者在到达设备的途中接收实际请求。实践中，队列数量是固定的（64个），并在提交请求时使用基于进程 ID 的哈希算法来选择队列。
- 请求的调度在所有队列上以轮询方式进行，每个队列按 FIFO 顺序工作。因此，工作被分散了。为了避免过度的寻道操作，在向设备发出实际 I/O 请求之前，会选择一整轮并将其排序到分发队列中。

### 可调参数 (Tunables)

- `quantum`
一轮服务中的最大队列长度。（默认值 = 4）；
- `queued`
每个队列的最小请求分配。（默认值 = 8）
- `fifo_expire_sync`
同步请求的 FIFO 超时。（默认值 = HZ/2）
- `fifo_expire_async`
异步请求的 FIFO 超时。（默认值 = 5 * HZ）
- `fifo_batch_expire`
FIFO 过期的速率。（默认值 = HZ/8）
- `back_seek_max`
最大向后寻道，单位为 KB。（默认值 = 16K）
- `back_seek_penalty`
向后寻道的惩罚。（默认值 = 2）

## 31.6 期待性 I/O 调度器 (Anticipatory)

- 期待性 I/O 调度器基于一种观察：磁盘读取通常会紧随对相邻扇区的其他磁盘读取。
当发出请求时，计时器开始工作，在过期之前，I/O 请求不会转发给驱动程序；即请求队列会暂时阻塞。在此期间，如果有另一个请求到达，它将被立即处理。
该算法是自适应的，因为它会根据实际的 I/O 请求负载不断调整其对“接近”的概念。
当没有更多邻近请求时，将继续处理正常的等待中的 I/O 请求。
基本目标是减少每个线程的响应时间。该方案在实现上与 deadline 调度器类似，可以认为是其变体。

### 可调参数 (Tunables)

- `antic_expire`:
在放弃之前，期待一个“良好的读取”（靠近最近完成的请求）的最长等待时间（毫秒）。（默认值 = HZ/150 = 6）
- `read_expire`:
读取请求持续多久后过期（毫秒），以及处理已过期请求的间隔。（默认值 = HZ/8 = 125）
- `read_batch_expire`:
一批读取在处理等待中的写入之前可以持续多长时间（毫秒）。它应该是 `read_expire` 的倍数。值越高，对读取的倾斜越越大。（默认值 = HZ/2=500）



- `write_expire` 和 `write_batch_expire`：

对写入起相同的功能。（默认值 = `HZ/4` = 250）

- `est_time`：

提供一些统计信息。

- 详细的文档可以在此处找到：`/usr/src/linux/Documentation/block/as-iosched.txt`。

## 31.7 实验比较 I/O 调度器

### 实验 1：编写一个脚本（如果你喜欢的话，也可以写程序），循环遍历磁盘上的 I/O 调度器，并进行可配置数量的并行读写。你可能需要将读取和写入分开测试。

- 测试读取时，确保是从磁盘而不是内存页读取的；你可以通过以下命令清除缓存：

```
$ echo 3 > /proc/sys/vm/drop_caches
```

在执行读取之前可以 `cat` 到 `/dev/null`。为了在获取时间信息之前确保所有读取完成，可以使用 `wait` 命令。

- 测试写入时，你可以同时多次拷贝文件（第一次读取后它就在内存中了）。为了在获取时间信息之前等待所有写入完成，可以使用 `sync` 命令。

## 第32章

# 块驱动程序

我们将介绍块驱动程序。我们将考虑块缓冲。我们将讨论它们是什么以及如何注册和注销。我们将讨论重要的 `gendisk` 数据结构。我们将讨论块驱动请求函数，并查看读写块设备与字符设备的何不同。

- 32.1 什么是块驱动程序？......................................................................... 289

- 32.2 缓冲................................................................................................................ 290

- 32.3 注册块驱动程序...................................................................... 290

- 32.4 `gendisk` 结构............................................................................... 292

- 32.5 请求处理............................................................................................... 293

- 32.6 实验...................................................................................... 296

块设备可能具有多个分区。在大多数情况下，分区号对应设备的次设备号（minor number），而整个设备共享同一个主设备号（major number）。节点的命名约定为：

# 主号 — 单元 — 分区

例如，`/dev/hdb4` 的主号为 `hd`，单元为 `b`（第二个），分区为 4。分区的细节包含在 `gendisk` 数据结构中。

块设备也可以使用可拆卸介质，如 CD-ROM 和软盘。

## 32.2 缓冲

- 文件存储在固定大小块的块设备上，尽管通过系统调用发出的 I/O 请求可以是任意字节数的。因此，块设备必须必须由一个所有设备共享的缓冲/缓存系统来控制。

- 块通过页缓存（page cache）进行缓存，给页面可能包含多个块设备缓冲区。

- 只有在以下情况下才会访问设备本身：

    - 在读取请求时，必须加载不在缓存中的块。

    - 如果缓存中的内容与 `O_SYNC` 标志不再匹配，则需要（最终）写入块。在这种情况下，该块必须被标记为脏（dirty）。注意，如果使用 `O_SYNC` 标志打开文件，则不允许任何延迟。

    - 周期性地，`pdflush` 系统进程会修改一段时间未使用的所有块，并将其刷回设备。其他事件也可能触发刷新，其目的是使缓存中的脏块数量保持最少，并确保最重要的块（即 deinodes 和 superblocks）保持最高的一致性。

- `sync` 命令写入缓存中所有修改过的缓冲区块。`fsync()` 系统调用写回单个文件的所有修改过的缓冲区块。

## 32.3 注册块驱动程序

- 块设备的注册通常在初始化例程期间完成，在许多方面与字符设备的注册非常相似。注销通常在清理例程中完成，字符设备一样。相应的函数如下：

```c
#include <linux/fs.h>
int register_blkdev(unsigned int major, const char *name);
unregister_blkdev(unsigned int major, const char *name);
```

- `register_blkdev()` 成功时返回 0，失败时返回 `-EBUSY`。提供主号 0 将生成一个作为返回值的动态分配。`major` 的值小于或等于 `MAX_BLKDEV=255`。

- `unregister_blkdev()` 成功时返回 0，失败时返回 `-EINVAL`。它检查 `major` 是否有效以及 `name` 是否与 `major` ，但不会检查你是否是正在注销的设备的所有者。

![](img/134c18b05ee9bbbe93ba3f4335720ac1_306_0.png)

- 还存在更现代的块设备注册和注销函数，`blk_register_region()` 和 `blk_unregister_region()`。

- 这些函数的使用较为复杂，可以在 John Corbet 在他的驱动发布系列文章中阅读：http://lwn.net/Articles/25711/

- `block_device_operations` 结构起的作用类似于字符驱动程序中 `file_operations` 结构的作用。它通过 `gendisk` 数据结构中的条目与设备关联，我们稍后会展示。

- `block_device_operations` 结构在 `/usr/src/linux/include/blkdev.h` 中定义如下：

```c
struct block_device_operations {
  int (*open) (struct block_device *, fmode_t);
  int (*release) (struct gendisk *, fmode_t);
  int (*ioctl) (struct block_device *, fmode_t, unsigned, unsigned long);
  int (*coactioctl) (struct block_device *, unsigned, unsigned long);
  int (*direct_access) (struct block_device *, sector_t,
              void (*, unsigned long long);
  unsigned int (*check_events) (struct gendisk *disk);
              unsigned int (clearing;);
  /* media_changed()) 已弃用，请改用 check_events() */
  int (*media_changed) (struct gendisk);
  void (*unlock_native_capacity) (struct gendisk *);
  int (*invalidate_disk) (struct gendisk);
  int (*getgeo) (struct block_device *, struct hd_geometry *);
  /* 此回调在持有 swap_lock 且有时持有 page table lock 时调用 */
  void (*swap_slot_free_notify) (struct block_device *, unsigned long);
  struct module *owner;
};
```

- 对于简单设备，不需要定义 `open()` 和 `release()`。

- 示例：

```c
static struct block_device_operations mydriver = {
  open = mydriver,
  release = mydriver,
  ioctl = mydriver,
};
```

## 32.4 gendisk 结构

- `gendisk` 结构定义在 `/usr/src/linux/include/genhd.h` 中并描述了。



```c
struct gendisk {
	int major;
	int minor;
	int capacity;
	char name[32];
	struct block_device_operations *fops;
	struct request_queue *queue;
	void *private_data;
	int flags;
	struct device *dev;
	struct object *obj;
	struct object *slice;
	struct list_head queue;
	atomic_t in;
#ifdef CONFIG_SMP
	struct disk_stats *dkstats;
#else
	struct disk_stats dkstats;
#endif
};
```

## 32.5 请求处理

- 以下函数用于分配、配置和释放 `gendisk`：

```c
#include <linux/genhd.h>

struct gendisk *alloc_disk(int minors);
void add_disk(struct gendisk *disk);
void put_disk(struct gendisk *disk);
void del_gendisk(struct gendisk *disk);
void set_disk_ro(struct gendisk *disk);
```

查看请求处理的最简单方法是查看一个平凡的请求函数：

```c
static void my_request(struct request_queue *q)
{
    struct request *rq;
    int size, res = 0;
    char *ptr;
    unsigned nr_sectors, sector;
    printk(KERN_INFO "entering routine\n");

    rq = blk_fetch_request(rq);
    while (rq) {
        if (!blk_fs_request(rq)) {
            printk(KERN_WARNING "This was not a normal fs request, skipping\n");
            goto done;
        }

        nr_sectors = blk_rq_cur_sectors(rq);
        sector = blk_rq_pos(rq);
        ptr = ramdisk + sector * sector_size;
        size = nr_sectors * sector_size;

        if ((ptr + size) > disk_size) {
            printk(KERN_WARNING "tried to go past end of device\n");
            goto done;
        }

        if (rq->data_dir(rq)) {
            printk(KERN_INFO "writing at sector %ld, %ud sectors\n", sector, nr_sectors);
            memcpy(ptr, rq->buffer, size);
        } else {
            printk(KERN_INFO "reading at sector %ld, %ud sectors\n", sector, nr_sectors);
            memcpy(rq->buffer, ptr, size);
        }

        done:
        if (!blk_end_request_cur(rq, res)) {
            rq = blk_fetch_request(rq);
        }
    }
    printk(KERN_INFO "leaving routine\n");
}
```

通过 `blk_fetch_request()` 从队列中剥离第一个请求，当没有更多请求时它返回 `NULL`。`blk_fs_request()` 函数检查交付的是什么类型的请求。对于普通文件系统请求，该结果为真，而诊断和其他类型的操作则不然。

实际拷贝是通过简单的 `memcpy()` 完成的。然而，注意使用了函数 `rq_data_dir()`，它会检查请求结构体中 `flags` 字段的第一位，该位在写入时被设置，在读取时被清除。

## 32.5. 请求处理

![](img/134c18b05ee9bbbe93ba3f4335720ac1_310_0.png)

- 2.6.31 内核对块驱动接口引入了更改，重构了 `request_queue_structure` 并引入了一些新函数。此外，函数 `blk_queue_hardsect_size()` 被 `blk_queue_logical_block_size()` 代替了。

- 这是一个旧版本请求函数的示例：

```c
static void my_request(struct request_queue *q)
{
    struct request *rq;
    int size;
    char *ptr;
    printk(KERN_INFO "entering request routine\n");

    while ((rq = elv_next_request(q))) {
        if (!blk_fs_request(rq)) {
            printk(KERN_INFO "This was not a normal fs request, skipping\n");
            end_request(rq, 0);
            continue;
        }
        ptr = ramdisk + rq->sector * q->hardsect_size;
        size = rq->current_nr_sectors * q->hardsect_size;
    }

    if ((ptr + size) > (ramdisk + disk_size)) {
        printk(KERN_ERR "tried to go past end of device\n");
        end_request(rq, 0);
        continue;
    }

    if (rq_data_dir(rq)) {
        printk(KERN_INFO "a write\n");
        memcpy(ptr, rq->buffer, size);
    } else {
        printk(KERN_INFO "a read\n");
        memcpy(rq->buffer, ptr, size);
        end_request(rq, 1);
    }

    printk(KERN_INFO "leaving request\n");
}
```

- 从队列中剥离第一个请求是通过 `elv_next_request()` 完成的，当没有请求时它会返回 `NULL`。当调用 `end_request()` 且第二个参数为 0（失败）或 1（成功）时，请求函数退出。

- 备注

## 32.6 实验

### 实验 1：构建块驱动

- 编写一个基础块设备驱动程序。

- 你需要至少实现 `open()` 和 `release()` 入口点，并包含一个请求函数。

- 你可以使用未分配的主设备号值并选择一个次设备号，或者尝试动态获取主设备号。假设你正在使用 `udev`，节点在加载驱动程序时会自动创建；否则，你将必须使用 `mknod` 命令手动添加节点。

- 跟踪节点被打开的次数。允许多次打开或独占使用。

- 编写程序使用标准的 Unix I/O 函数 `open()`、`read()`、`write()`、`close()` 从节点进行读取（和写入）。使用 `insmod` 加载模块后，使用此程序访问节点。

- 注意：确保你有足够的内存来处理创建的内存磁盘；解决方案分配了 128 MB。

### 实验 2：可挂载的读写驱动

- 扩展之前的练习，以便在你的设备上放置一个 ext3 文件（或其他类型）。

- 你可以通过以下命令在设备上放置文件系统：

```bash
mkfs.ext3 /dev/mydrv
mount /dev/mydrv /mnt
```

其中你提供设备节点和挂载点的相应名称。



作为一个额外的增强，尝试使用 `fdisk` 对设备进行分区。为此你可能需要一个额外的用于 `HDGETGEO` 的 `ioctl()`，并且必须包含 `linux/hd.h`。此 `ioctl` 返回一个指向以下结构的指针：

```c
struct bd_geometry {
    unsigned char heads;
    unsigned char sectors;
    unsigned short cylinders;
    unsigned long start;
};
```

记住总容量是 (扇区大小) x (柱面数) x (磁头数)。你还希望起始扇区使用值 4。

如果你使用的是较新的内核和 `udev`，分区节点在加载驱动程序时会自动创建；否则，你将必须手动添加它们。

## 索引

299

- DMA, 220
- 边缘触发, 69
- 启用与禁用, 70
- 异常 (exceptions), 66
- 故障 (faults), 66
- `free_irq()`, 74
- 处理程序 (handlers), 65, 73, 74
- 中断请求 (IRQ), 68
- `irq_desc`, 71
- `irqaction`, 72
- 电平触发, 69
- 可屏蔽 (maskable), 68
- MSI, 69
- MSI-X, 70
- 非可屏蔽 (onmaskable), 68
- 程序化异常 (programmed exceptions), 62
- `request_irq()`, 74
- 共享 (sharing), 66
- `synchronize_irq()`, 74
- 同步 (synchronous), 66
- 线程化的 (ithreaded), 181
- 上半部 (top halves), 173
- 陷阱 (traps), 66
- 用户空间处理程序 (user-space handlers), 182
- `io.getevents()`, 279
- `io.prep_read()`, 281
- `nio.prep_write()`, 281
- `io.setup()`, 279
- `io.submit()`, 279
- `ioioctl`, 280
- `ioocb`, 280
- `ioioctl()`, 119
- 内核模式 (kernel mode), 61, 63
- O(1) 调度器, 62
- 获取源 (obtaining source), 8
- 抢占 (preemption), 61
- 进程上下文 (process context), 63
- 调度 (scheduling), 61
- 调度模块 (scheduling modules), 62
- 用户模式 (user mode), 61, 63
- 内核地址 (kernel address), 146
- 内核并发，伪伪 (kernel concurrency, pseudo), 106
- 内核并发 (kernel concurrency), 106
- 内核调试器 (kernel debuggers), 88
- 内核同步方法 (kernel synchronization methods), 105
- 内核线程 (kernel threads), 174, 180
- 内核空间 (kernel-space), 146
- `kernel_thread()`, 181
- `KERNEL VERSION()`, 7
- `kernelnerops`, 86
- `kfree()`, 138
- `kgdb`, 88
- `kio`, 148, 149
- `klogd`, 255
- `kmalloc()`, 138
- `kmap()`, 150
- `kmem.cache_alloc()`, 143
- `kmem.cache_create()`, 141
- `kmem.cache_destroy()`, 141
- `kmem.cache_free()`, 143
- `kmem.cache_shrink()`, 141
- `kobjects`, 125
- `kprobes`, 91
- `krealloc()`, 139
- `thread_bind()`, 180
- `thread_create()`, 180
- `thread_rm()`, 180
- `thread_should_stop()`, 180
- `thread_stop()`, 180
- `kmap()`, 150
- `zkalloc(1)`, 139
- 定义命令, 121
- 定向传输 (directional transfers), 122
- 入口 (entry point), 120
- 无锁 (lockless), 121
- 类型宏 (type macros), 122
- 中断亲和性 (irq affinity), 69
- 中断平衡 (irqbalance), 69
- `jiffies`, 64, 96
- `jiffies.64`, 96
- `jprobe_return()`, 93
- `jjprobes`, 93
- `kcore`, 88
- `kgdb`, 88
- 内核 (kernel)
  - CFS 调度器, 62
  - 编译 (compiling), 83
  - 组件 (components), 59
  - 配置 (configuration), 81
  - 执行方法 (execution methods), 61
  - 中断上下文 (interrupt context), 63
  - 低功耗 (lesswatt), 274
  - `libaio`, 279
  - `LINUX_VERSION_CODE`, 7
  - 加载与卸载 (loading and unloading), 22
  - `lock_kernel()`, 110
  - `lspci`, 199
  - 内存 (memory)
    - DMA, 136
    - 高 (high), 136
    - 低 (low), 136
    - 区域 (zones), 136
  - 内存分配 (memory allocation), 183

300

- 内存屏 (memory barriers), 188, 192
- 内存缓存 (memory caches), 141
- 内存管理 (memory management), 59, 135
- 内存映射 (memory mapping), 146, 148, 153
- 微内核 (microkernel), 30
- 杂项设备 (miscellaneous devices), 55
- `mknod`, 42
- `mod.timer()`, 98
- `MODULE_DEVICE_TABLE()`, 203, 263
- `MODULE_FIRMWARE()`, 134
- 模块 (modules), 29
  - 退出 (exit), 30, 81
  - 初始化 (init), 30, 81
  - 初始化数据 (initdata), 81
  - 别名 (aliases), 80
  - 清理模块 (`cleanup_module()`), 31
  - 编译 (compiling), 34
  - 按需加载 (demand loading), 80
  - `depmod`, 32, 35, 80
  - 动态加载 (dynamic loading), 80
  - `EXPORT_SYMBOL()`, 77
  - `EXPORT_SYMBOL_GPL()`, 78
  - 导出 (exporting), 77
  - 释放空闲内存 (freeing unused memory), 81
  - `init_module()`, 31
  - `insmod`, 34
  - 许可证 (license), 78
  - 加载 (loading), 32, 81
  - `lsmod`, 32
  - `Makefile` (makefiles), 34
  - `modinfo`, 34
  - `modprobe`, 33, 34, 39, 80
  - `modprobe.conf`, 31
  - 模块工具 (module_utilities), 131
  - `MODULE_AUTHOR()`, 78
  - `MODULE_DESCRIPTION()`, 78
  - `module_exit()`, 30, 81
  - `module_init()`, 30, 81
  - `module_param()`, 33
  - 参数 (parameters), 33
  - 请求模块 (`request_module()`), 80
  - `rmod`, 32
  - 污染 (tainted), 30, 79
  - 卸载 (unloading), 81
  - 使用计数 (usage count), 56
- 单体内核 (monolithic kernel), 30
- `msleep()`, 97
- `msleep_interruptible()`, 97
- MTD, 267
  - `cramfs`, 270
  - 文件系统 (filesystems), 269
  - `itrd`, 270
  - `jfs`, 270
  - `jfs2`, 270
  - AND, 268
  - NOR, 268



- `ramfs`, 270

- `原始块模块 (raw block_modules)`, 269

- `原始字符模块 (raw character_modules)`, 269

- `mutex_init()`, 112

- `mutex_islocked()`, 112

- `mutex_lock()`, 112

- `mutex_interruptible()`, 112

- `可杀死 (killable)`, 112

- `mutex_trylock()`, 112

- `mutex_unlock()`, 112

- `互斥锁 (mutexes)`, 71, 106, 111

- `ndiswrapper`, 29

- `网络驱动程序 (network drivers)`, 254

- `轮询 (polling)`, 254

- `网络设备 (network devices)`, 18

- `网络驱动程序 (network drivers)`, 230

- `alloc.ethdev()`, 231

- `alloc_netdev()`, 231

- `载波状态 (carrier state)`, 253

- `关闭 (closing)`, 232

- `ether_setup()`, 231

- `ethtool`, 255

- `free_netdev()`, 231

- `ioctl()`, 253

- `加载与卸载 (loading and unloading)`, 230

- `mih`, 253

- `多播 (multicasting)`, 251

- `API`, 254

- `网络设备 (net device)`, 231, 235

- `网络设备操作 (net device ops)`, 235, 238

- `netdev_priv()`, 231

- `netif_carrier_off()`, 253

- `netif_carrier_ok()`, 253

- `netif_carrier_on()`, 253

- `netif_rx()`, 248

- `netif_start_queue()`, 232

- `netif_stop_queue()`, 232

- `netif_wake_queue()`, 232

- `打开 (opening)`, 232

- `轮询 (polling)`, 253

- `接收 (reception)`, 230, 248

- `套接缓冲区函数 (socket buffer functions)`, 242

- `套接缓冲区结构 (socket buffer_structures)`, 241

- `统计 (statistics)`, 249

## 316

- `TOE`, 254

- `传输 (transmission)`, 230, 247

- `禁用传输 (transmission disabling)`, 248

- `传输超时 (transmission timeouts)`, 248

- `TSO`, 254

- `网络层 (network layers)`, 227

- `网络数据包 (network packets)`, 228

- `网络化 (networking)`, 60

- `nvidia`, 21

- `O.DIRECT`, 149

- `objdump`, 86

- `oops 消息 (oops messages)`, 85

- `OpenUSE`, 5

- `PAE`, 138

- `页异常 (page faults)`, 137, 147

- `页帧号 (page frame number)`, 137

- `页帧号 (page frame numbers)`, 154

- `页帧表 (page tables)`, 137

- `偏移量 (PAGE_OFFSET)`, 136

- `污染 (tainted)`, 30

- `面恐 (panic)`, 85

- `PCI`, 199

- `BIOS`, 21

- `配置 (configuration)`, 81

- `PCI 寄存器 (PCI registers)`, 105

- `设备检测 (detection)`, 51

- `I/O 资源 (I/O resources)`, 106

- `注册驱动程序 (registering drivers)`, 127

- `PCI`, 70

- `PCI 设备 (PCI device)`, 104, 106

- `PCI Express (PCI express)`, 69

- `pci.get_device()`, 103, 38

- `pci.dev_id`, 104

- `pci.name()`, 105

- `pci.register_driver()`, 127

- `pci.unregister_driver()`, 128

- `pci 设备 (PCI device)`, 104

- `pci 设备 (PCI device)`, 109

- `pci 设备 (PCI device)`, 104

- `pci 设备 (PCI device)`, 109

- `pci 设备 (PCI device)`, 104

- `pci 设备 (PCI device)`, 104

- `优先级 (priority)`, 24

- `平台总线 (platform bus)`, 62

- `平台驱动程序 (platform drivers)`, 92

- `电源管理 (power management)`, 73

- `电源状态 (power states)`, 274

- `Red Hat`, 5

- `参考计数 (reference counting)`, 116

- `register_jprobe()`, 91

- `register_kprobe()`, 91

- `register_netdev()`, 230

- `中继通道 (relay channels)`, 156, 157

- `release_firmware()`, 134

- `request_firmware()`, 134

- `RPM`, 50

- `schedule()`, 62

- `Scientific Linux`, 5

- `SCSI 设备 (SCSI devices)`, 60

- `sem.init()`, 114

- `互斥锁 (semaphores)`, 71, 106

- `setpci`, 90

- `SLAB`, 143

- `内存分配器 (slab allocator)`, 141

- `睡眠 (sleeping)`, 97

- `独占 (exclusive)`, 166

- `软中断 (softirqs)`, 98

- `自旋锁 (spin_lock)`, 109

- `spin_lock_init()`, 109

- `spin_lock.irqsave()`, 110

- `spin_lock.irrestore()`, 110

- `spin_lock_trylock()`, 112

- `spin_lock_unlock()`, 112

- `自旋锁 (spin_locks)`, 109

- `spin_t`, 70

- `暂阶段 (staging)`, 125

- `同步 (sync)`, 66

- `系统fs (sysfs)`, 89

- `系统调用 (sys calls)`, 61

- `系统模型 (system model)`, 20
