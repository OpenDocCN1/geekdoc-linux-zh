
根据你的引导加载程序及其配置，可能不需要拥有 `/boot` 目录。这取决于你的引导加载程序是否能够在内核启动之前从根文件系统中检索内核镜像。在阅读完第 9 章后，你将能够决定是否应该使用 `/boot` 目录以及如何为目标系统使用它。当然，如有必要，你可以稍后重新设计根文件系统。

其余的目录——`/bin`、`/dev`、`/etc`、`/lib`、`/proc`、`/sbin`、`/sys` 和 `/usr`——是必需的。

在最极端的情况下，你可以决定省略 `/proc` 和 `/sys`，并在内核配置中不包含对相应虚拟文件系统的支持。然而，诸如 `ps`、`mount`、`ifconfig` 和 `modprobe` 等非常基本的命令需要访问 proc 文件系统。现在，越来越多的程序也在使用 sysfs 文件系统。因此，除非你的系统范围非常有限，否则如果你希望在没有 proc 和 sysfs 的情况下运行，就要准备好用直接访问内核系统调用接口的自定义 C 程序来替换脚本。

根目录中的两个目录，`/usr` 和 `/var`，拥有自己预定义的层级结构，很像根目录本身。我们在下面填充这两个目录的步骤中，将简要讨论这些层级结构。

## 令人困惑的相似性

根文件系统最令人困惑的方面之一是某些目录在用途上看似相似。特别是，新手经常问包含二进制文件的各个目录之间有什么区别，以及包含库的各个目录之间有什么区别。

在根文件系统中，二进制文件主要有四个目录：`/bin`、`/sbin`、`/usr/bin` 和 `/usr/sbin`。二进制文件放置的目录很大程度上取决于其在系统中的作用。对普通用户和系统管理员都必不可少的二进制文件位于 `/bin`。对系统管理必不可少但普通用户绝不会使用的二进制文件位于 `/sbin`。相比之下，大多数非必需的用户二进制文件位于 `/usr/bin`，大多数非必需的系统管理工具位于 `/usr/sbin`。

关于库位置的逻辑类似。用于启动系统并运行最基本命令的库位于 `/lib`，而 `/usr/lib` 包含所有其他库。通常，软件包会在 `/usr/lib` 中创建子目录来容纳它们自己的库。例如，Perl 5.x 软件包拥有一个 `/usr/lib/perl5` 目录，其中包含所有与 Perl 相关的库和模块。

查看你 Linux 工作站根文件系统在这些目录中的实际内容，将向你展示分发版的设计者应用这些标准的实际示例。

为了处理根文件系统，让我们移动到为此目的创建的目录：

```bash
$ cd ${PRJROOT}/rootfs
```

现在创建你的系统所需的核心根文件系统目录：

```bash
$ mkdir bin dev etc lib proc sbin sys tmp usr var
$ chmod 1777 tmp
```

请注意，我们没有创建 `/boot`。我们稍后会回过头来，如果需要就创建它。另外，请注意我们将 `/tmp` 目录的权限更改为“粘滞位”开启的状态。目录权限字段中的这个位确保在 `/tmp` 目录中创建的文件只能由创建它们的用户删除。虽然大多数嵌入式 Linux 系统是单用户系统，如前所述，但有些情况下，嵌入式应用程序必须以非 root 权限运行。例如，我们在第 10 章中讨论的 OpenSSH 包就是这样一种应用程序。因此，有必要遵循关于根文件系统权限位的一些基本规则。

然后你可以继续创建 `/usr` 层级结构：

```bash
$ mkdir usr/bin usr/lib usr/sbin
```

在一个功能完整的根文件系统中，`/usr` 目录通常包含更多的条目。你可以通过在工作站上输入 `ls -al /usr`（也许加上 `-r` 进行递归输出）轻松证明这一点。你会发现一些对非嵌入式系统的常规用户活动有用的目录，例如 `man`、`src` 和 `local`。FHS 包含一个部分，详细说明了该目录的布局。然而，对于大多数嵌入式 Linux 系统而言，我们创建的这三个目录就足够了。

最后创建的条目在 `/var` 目录中：

```bash
$ mkdir var/lib var/lock var/log var/run var/tmp
$ chmod 1777 var/tmp
```

在这里，非嵌入式系统上该目录也包含更多的条目。像 `cache`、`mail` 和 `spool` 这样的目录对工作站或服务器有用，但很少有嵌入式系统需要这些目录。我们创建的目录是大多数嵌入式 Linux 系统中常见应用程序正常运行所需的最基本集合。当然，如果你需要诸如提供网页服务或打印等功能，你可能希望添加一些提供这些功能的应用程序所需的额外目录。请参阅 FHS 和应用程序提供的文档，以了解你的实际需求。

现在根文件系统骨架已就绪，让我们将各种软件组件放置到适当的位置。

## 使用不同的根文件系统结构运行 Linux

正如我们在前面的讨论中说过的，构建根文件系统的规则在 FHS 中。尽管大多数 Linux 应用程序和分发版依赖于这些规则，但 Linux 内核本身并不强制执行这些规则。事实上，内核源代码对根文件系统的结构假设很少。由此推断，你可以构建一个拥有非常不同的根文件系统结构的嵌入式 Linux 系统。然后，你必须修改大多数软件包的默认设置，使它们符合你的新结构。确实，某些常规的“桌面”导向的分发版曾试图模仿 Apple 的文件系统布局。有些甚至采取了更极端的措施，构建完全没有根文件系统的嵌入式 Linux 系统。

不用说，我们不鼓励你走上这条路。我们之前概述的根文件系统规则是被所有致力于 Linux 系统的开源和自由软件开发者认可和同意的。使用其他规则构建你的嵌入式 Linux 系统，将使你与大多数开源和自由软件包及其开发者隔绝，并且在过程中不必要地忽视了一个有用的事实标准。

## 库

在第 4 章中，我们讨论了如何构建、安装和使用 GNU C 库及其替代品用于应用程序开发。在这里，我们将讨论如何将这些相同的库安装到目标的根文件系统中，以便你开发的应用程序在运行时可以使用它们。我们不会讨论 diet libc，因为它主要用作静态库。

### glibc

正如我们之前所说的，glibc 包包含许多库。查看你的 `$TARGET_PREFIX/lib` 目录，可以看到在包的构建过程中安装的所有库列表。该目录主要包含四种类型的文件：

**实际的共享库**

这些文件的命名格式为 `libLIBRARY_NAME-GLIBC_VERSION.so`，其中 LIBRARY_NAME 是库的名称，GLIBC_VERSION 是你正在使用的 glibc 包的版本。例如，glibc 2.3.6 的数学库名为 `libm-2.3.6.so`（数学库的名称只是“m”）。

很多人不知道 `.so` 文件也是可以返回有用信息的可执行 ELF 二进制文件。例如：

```bash
/lib/libc-2.5.so
GNU C Library stable release version 2.5, by Roland McGrath et al.
Copyright (C) 2006 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.
There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE.
Compiled by GNU CC version 4.1.2 (Ubuntu 4.1.2-0ubuntu4).
Compiled on a linux >>2.6.15.7<< system on 2007-04-04.
Available extensions:
   crypt add-on version 2.1 by Michael Glad and others
   GNU Libid by Simon Josefsson
   GNU Libiconv by Per Bothner
   NIS(NIS+)/NIS+ NSS modules 0.19 by Thorsten Kukuk
```

