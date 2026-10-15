
If you have any questions about this material you can contact us @coopi.com.

- The provided solutions will time to contain functions and features not gained in the main task.
- This is done illustrate methods to do more than the minimum work to solve the problem and touch extra.
- If there is anything that must be used and not included in the material, its omission is a bug, not a feature, and should be brought to our attention.

GENTOO is neither of this package systems, and instead uses the port/emer system which involves compiling directly from source. If you are a GENTOO user, and have you won't need detailed instructions on how to install or find, so we won't need by offering it.

# 第 1 章 准备工作

## 1.3 内核版本

Linux 内核的 2.2 版本是：

2.2 Linux 内核树的最新补丁是：

稳定 Linux 内核的最新 -mm 补丁是：

对于课程，我们对运行的内核和内核源码有许多选择。我们将使用最新的 Linux 内核源码，版本为 2.6。

内核版本编号的设计设计由三个整数组成，前两个表示主发行版本，第三个表示次要版本；例如 2.6.1 或 2.4.31。此外，一个额外的字符串可以作为标识后缀，它不是内核版本号的一部分。例如，如果内核被命名为 2.6.0-rt10，我们就有 -rt10。

实验练习的设计适用于最新的 Linux 内核（截至本文编写为 2.6.31）以及微调（一直到 2.6.22 甚至更早的 2.6.18，并经过了一些微调）。它们也应该适用于所有同名的主要发行发行版内核。

```
VERSION = 2
PATCHLEVEL = 6
SUBLEVEL = 29
EXTRAVERSION = -rt10
```

由于 2.4 内核仍在在使用，我们将指出已发生变化的重要特性。然而，之前的几代生产内核（2.2, 2.0）之间的差异将仅出于历史目的提及。

在内核源码的 `Makefile` 中。

`/usr/src/linux/include/linux.h` 文件提供了几个宏让生活变得更简单：

![](img/5f0cab84232061dba742ffc69894b1f1_13_0.png)

```
#define KERNEL_VERSION_CODE 130630
#define KERNEL_VERSION_CODE(a,b,c) ((a) << 16) + ((b) << 8) + (c))
```

- 在本手册的此处你会发现像这样的框：
- 它们可能会突出 2.6 内核中出现的新、修改过的、正在积极开发或已弃用的特性。
- 它们也可能突出 2.4 内核中已过时且不应在新的版本中使用特性。

使用 `KERNEL_VERSION()` 宏定义 `LINUX_VERSION_CODE`。一个示例是

```
#define KERNEL_VERSION_CODE(a,b,c) ( (a) * 65536) + ((b) * 256) + (c) )
```

此头文件在编译期间构造，在原始源码中并不存在。

版本代码可以在此示例中处理：

外部模块编译所需的源码部分（`kernel-devel` 包）应该安装在你的系统上。

```
#include <linux/version.h>
#if KERNEL_VERSION_CODE < KERNEL_VERSION(2,6,0)
  call_usermodulehelper(cmd, arg, envp);
#else
  call_usermodulehelper(cmd, arg, envp);
#endif
```

内核版本的最新官方发布始终可以从 http://www.kernel.org 获取，这是由 Linus Torvalds 发布的最新内核。一些源码树也是如此，但在内核网站上没有获得同样的关注。内核树有三个阶段：内部、USB 和

- 这种显式方法是为了放弃对早期内核版本的向后兼容，以保持整洁和最高效率。
- 这种关注通常被外部设备驱动维护者认为是不方便的，因为如果需要安全补丁，它使得必须为旧头文件维护不同的内核源码。

一个特别提到的是 Linux-next 项目，其信息位于 http://www.kernel.org/next。它包含了下一个内核版本的实验性补丁集；即 2.6.31 作为 linux-next 树收集并调试适当的。

通过使用此字符串，你可以选择最新的内核版本：

```
Linux 内核的最新版本是：
稳定 Linux 内核树的最新补丁是：
稳定 Linux 内核树的最新快照是：
内核的最新 2.4 版本是：
```

```
2.6.30
2.2-rc7
2.6.31rc7-git
2.4.8
```

## 1.5 硬件

从 2.6 内核开始，采用了一种新方案，使用数字用于涉及安全和稳定性问题的小型补丁。无争议的补丁会被接受，并编号为 2.6.11.1、2.6.11.2、2.6.11.3 等。

某些设备驱动程序使用挂载在外部端口的简单设备。与其这样做，我们将使用机器作为网卡和输入设备，并利用内核的想法将我们的设备附加在已安装的设备之上，这具有良好的稳定性来支持开发过程，并保持生产环境不使用稳定的内核。运行此内核接受的任何类型的补丁可以在 `/usr/src/linux/Documentation/stable_rules.txt` 找到。

出现以下问题之一：

- 我的设备使用多少 I/O 端口，它们使用哪些地址？
- 我读取的是字节还是字，有多少个中断？
- 设备遵从什么标准？

## 1.4 平台

我们将尝试尽可能与平台无关。然而，我们将考虑不限制在 IA64、Alpha、SPARC、PPC 等上。

这些问题只能通过硬件规格和通过检查硬件来回答。当你编写驱动程序时，你必须有足够的知识通过探测设备来写出其规格，自从 Linux 变得非常成熟以来，出现了许多驱动程序，并更好地鼓励我们在如果你需要支持时对其进行配置，然后只是正确地做这种工作。

- Linux 内核的某些部分依赖于平台，需要理解其特殊性。
- 你现在可能在 x86 上工作。
- 大多数为 Linux 开发的人都集中在这个平台上。从硬件中获取尽可能的信息，但要准备好某些信息可能是错误或过时的，特别是当它是新的时候。这不是硬件和驱动程序保持同步，或者让市场主导的操作系统在稍后提问的为了。我们将尝试消除任何平台依赖性。所有解决方案都在 32 位和 64 位架构上经过了测试。

## 1.6 Linux 驱动项目

![](img/5f0cab84232061dba742ffc69894b1f1_14_0.png)

- 2.6.24 内核是 32 位 i386 和 64 位 x86 架构的合并。新名字简单就是 x86。这涉及代码的重大重组和重写，完成花费了一些时间。
- 许多文件被重新组织了；例如，不是使用 `/arch/i386/init.c` 而是 `arch/x86/init_32.c` 和 `arch/x86/init_64.c`。

驱动项目由 Greg Ross-Hartman 领导，他的网站位于 http://www.kernel.org/next/。新来者总是受欢迎的。项目的目标是将许多外部驱动引入主内核树。一个没有 Linux 驱动的列表位于 http://driverproject.org/wiki/bin/view/Main/OutOfDrivers。维护并签署 NDA（保密协议）的开发者。

`/usr/src/linux/Documentation` 目录包含了许多有用的项目。你可以以网页浏览、PostScript、可打印文档或富文本格式获取文档，这些将出现在 `/usr/src/linux/Documentation/DocBook` 目录。制作这些文档的时间比编译内核本身还要长！为了正确工作工作，你需要在系统上安装额外的软件。

## 1.7 文档与链接

关于内核文档的最佳来源是源代码本身。在许多情况下，在不查看代码（包括这一个）的情况下不要相信你看到的内容。

http://www.net/driver-posting

Jerry Carpenter 为 2.6 内核编写的一系列文章和演讲。

Linux Kernel Development, 第二版, Robert Love 编写, Novell Press 出版, 2005.
