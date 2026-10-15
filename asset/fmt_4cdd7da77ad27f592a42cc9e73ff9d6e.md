
通过进入`/usr/bin/cusp`并运行`ldd`，rld 无法看到 cusp(1) 二进制文件的完整路径。`/etc/libmap.conf`规定对于`/usr/bin/cusp`的完整路径仅使用 libthread，因此当以普通名 cusp 请求`libthread.so.2`时，它会提供`libthread.so.2`。

如果你想让程序无论通过完整路径还是名称调用都使用备用库，只需在括号中提供程序名称，而不是该名称：

| cusp |
| libthread.so.2 | libkse.so.2 |
| libthread.so | libkse.so |

同样，你可以通过列出目录名称并在末尾加上斜杠，来为该目录下的所有程序选择备用库。在这个示例中，我们强制目录中的所有程序使用备用库：

| /home/oracle/bin/ |
| libthread.so.2 | libkse.so.2 |
| libthread.so | libkse.so |

使用`libmap.conf`允许你任意重映射共享库。虽然它最常用于线程库（偶尔用于 Linux 模式程序），但你也可以为你的程序施加你喜欢的任何库。当然，你也可以使用`LD_LIBRARY_PATH`来调整库，但那只影响拥有该变量的用户。

# 在错误的操作系统上运行软件

传统的软件是为特定的操作系统编写的，且仅在该操作系统上运行。许多人编写良好的软件使其能够在另一个系统中运行，这个过程被称为移植（porting）。作为管理员，你有几种方法可以在 FreeBSD 以外的平台上使用软件。最有效的方法是重新编译源代码以便在 FreeBSD 上原生运行。

如果这不可行，你可以在 Wine 等模拟器下运行非原生软件，或者通过重新实现软件原生平台的应用程序二进制接口 (ABI)。

# 重新编译

Ports 集合（Ports Collection）中的许多软件实际上最初为其他平台设计的移植程序。（这就是为什么它被称为 Ports 集合）。为 Linux、Solaris 或其他 Unix 类操作系统编写的软件通常可以在极少或完全不修改的情况下，从源代码重新编译，并在 FreeBSD 上完美运行。只需获取源代码并在 FreeBSD 机器上进行构建，你就可以在 FreeBSD 上原生运行外国软件。

重新编译在平台相似时效果最好。例如，FreeBSD 和 Linux 提供了许多相似的函数；它们都基于标准 C 函数构建，都使用相似的工具，都使用 GCC 编译器，等等。多年来，各种 Unix 类操作系统已经发生了分化。每个版本的 Unix 都实现了新功能、新库和新函数，如果某段软件需要这些函数，它就无法在其他平台上构建。POSIX 的引入部分程度上是为了缓解这个问题。使用仅符合 POSIX 标准的系统调用和库编写的软件，应该可以立即移植到任何其他 POSIX 兼容的操作系统，而大多数 Unix 供应商都符合 POSIX。问题在于确保开发者能够在他们首选的平台上运行软件。许多开源开发者非常在意他们的软件运行在他们首选的平台上。例如，Linux 特定的软件在上面的输出是不符合 POSIX 标准的。仅限 POSIX 的代码没有利用操作系统提供的任何特殊功能。

例如，FreeBSD 拥有极高效的数据读取系统队列`queue(2)`。其他 Unix 类操作系统使用`select(2)`和`poll(2)`代替。应用程序开发者面临的问题是，他们是使用`queue(2)`（这会让他们的软件在 FreeBSD 上极快，但在其他地方毫无用），还是使用`select(2)`和`poll(2)`让他们的软件可以在任何地方运行，尽管速度较慢。开发者可以投入更多时间平均支持`queue(2)`、`select(2)`和`poll(2)`，虽然这让用户很高兴，但从开发者的角度来看却糟糕。

FreeBSD 采取了折中方案。如果某段软件可以重新编译并在 FreeBSD 上正常运行，ports 团队就会实现它。如果软件需要微小补丁，ports 团队会将补丁包含在移植中，并将其发送给软件开发者。大多数开发者乐意接受允许他们支持另一个操作系统的补丁。即使他们可能没有可用的操作系统进行测试，或者可能不熟悉该操作系统，来自可靠来源的良好补丁通常会被接受。

## 外部软件库

虽然 ABI 重新实现解决了一个主要问题，但程序需要的不仅仅是 ABI。如果没有共享库、支持程序以及其他用户态，大多数程序将无法正常运行。无论你使用哪种 ABI，你都必须访问该平台的用户态。

要使用 SVR4 模式，你需要 Sun Solaris 2.5.1。旧版本的 Solaris 不再免费提供，因此 FreeBSD 项目无法为你提供这些。这并不是不可逾越的障碍，但它让使用 SVR4 模式变得稍微复杂了一些，且昂贵得多。如果你有光盘，请查看`/usr/ports/emulators/svr4_base`。

Linux 用户态是免费获取的。由于入门门槛非常低，我们将详细讨论 Linux 模式。一旦你彻底理解它的工作原理，就可以将这些知识应用于任何你想要使用的其他 ABI 兼容模式。

## 使用 Linux 模式

要安装 Linuxulator，选择一个需要 Linux 模式的软件并安装即可。Ports Collection（集合）非常智能，能够识别出某个软件需要 Linux 模式并选择合适的 Linux 版本进行安装。例如，我使用了 Adobe Reader (`/usr/ports/print/acrodev7`)。安装此端口会触发 Linux 模式的安装。

该端口下载大量的 Linux 系统文件并将它们安装在`/usr/compat/linux`中：Linux 程序将使用这个用户态而非 FreeBSD 用户态。

该端口还会加载 Linux 内核模块。要让 FreeBSD 在启动时自动加载该模块，请使用此`rc.conf`条目：

```
linux_enable="YES"
```

就这些了！你应该能够在无需任何进一步配置的情况下运行 Linux 程序。剩下的剩下的是 Linux 模式中一些微小的困扰和小缺陷了。遗憾的是，这类问题确实不少。

## 什么是 LINUX_BASE？

你会看到很多关于名为`linux_base`的引用。在历史上，你通过一个名为`linux_base`的端口安装 Linux 用户态，然后在这些文件之上安装软件。现代 FreeBSD 使这对用户来说是透明的，允许你安装所需的软件而无必担心依赖关系。你在`/usr/ports/emulators`中看到的各种`linux_base`端口是为开发者使用和兼容性测试设计的，而不是让你安装的！

## Linuxulator 用户态

正如`linux.ko`内核模块提供 Linux ABI 一样，Linuxulator 需要一个非常精量的 Linux 用户态。查看`/usr/compat/linux`，你会看到类似以下的内容：

```
# ls
bin etc lib media mnt opt proc sbin selinux srv sys usr var
```

看起来像 FreeBSD 的`/usr`目录，不是吗？如果你稍微研究一下，会发现，通常情况下，`/usr/compat/linux`的内容与你的核心 FreeBSD 安装是相当的。你会在两者中发现许多相同的程序。

一位 Linux 狂热者立即注意到，任何`linux_base`端口的特点是，其内容与典型的 Linux 安装相比非常精简。即每个基于 Linux 的端口只安装运行所需的内容。当你运行一个新端口的程序时，Ports Collection 会根据需要扩展 Linux 用户态。

尽可能情况下，Linux 中的程序会尝试留在`/usr/compat/linux`下，这有点像一个弱监狱（jail，第 9 章）。当你执行一个调用其他程序的 Linux 二进制文件时，Linux ABI 会首先检查`/usr/compat/linux`下是否存在该程序。如果该程序不存在，Linux 模式会在主系统中查找。例如，假设你有一个调用`ping(8)`的 Linux 二进制文件。ABI 首先在`/usr/compat/linux/`下搜索`ping`程序；截至本文撰写，它可以找到。ABI 随后检查主 FreeBSD 系统，找到`/bin/ping`并使用它。Linuxulator 大量利用这种回退机制来减小 Linux 模式用户态的大小。

另一种，假设一个 Linux 二进制文件想要调用`sh(1)`。Linux ABI 检查`/usr/compat/linux`，找到了`/usr/compat/linux/bin/sh`，并执行该程序而非 FreeBSD 原生的`/bin/sh`。

## 测试 Linux 模式

现在你已经了解 Linux 模式下安装了什么，测试功能就简单了。运行 Linux shell 并询问它运行在什么操作系统上：

```
# /usr/compat/linux/bin/sh
sh-3.005 -a
Linux stretchchimo.blackhelicopters.org 2.4.2 FreeBSD 7.0-CURRENT #7: Wed
Apr 23 21:00:44 EDT 2008 1686 1386 GNU/Linux
sh-3.005
```

当我们询问运行的是什么种类型的命令时，这个 shell 回答说是运行在一个名为 FreeBSD 的 Linux 2.4.2 内核之上。很酷，对吧？

然而，请记住，Linux 模式并不是完整的 Linux 用户态。你无法在默认的 Linuxulator 安装中交叉编译软件。你只能执行非常基础的任务。

## 识别和设置标记（Brands）

给软件二进制文件标记比给牛打标记容易，但远没有那么冒险。大多数现代 Unix 类类二进制文件都是 ELF 格式，其中包含注释空间。那里就是标记的地方。FreeBSD 根据该二进制文件上的标记为每个 ABI 分配标记。如果二进制文件没有标记，则假设它是 FreeBSD 二进制文件。FreeBSD 识别三种标记：FreeBSD、Linux 和 SVR4。使用`brandelf(1)`查看和更改标记：

```
# brandelf /bin/sh
File /bin/sh is of brand 'FreeBSD'
```

```
# brandelf /usr/compat/linux/bin/sh
File /usr/compat/linux/bin/sh is of brand 'Linux'
```

```
# brandelf /bin/ping
File /bin/ping is of brand 'SVR4'
```
