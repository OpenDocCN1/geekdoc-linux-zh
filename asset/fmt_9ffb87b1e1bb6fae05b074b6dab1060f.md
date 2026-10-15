
```
dnl 检查程序。
AC_PROG_CC
dnl 检查头文件。
AC_CHECK_HEADERS(readline.h)
dnl 检查库。
AC_CHECK_LIB(readline, rl1_bind,
RLIB="-readline -lcurses",
[,
-incurs)
AC_SUBST(RLIB)
AC_OUTPUT(Makefile)
```

`AC_CHECK_LIB` 宏检查我们是否可以链接一个调用 `rl1_bind` 的测试程序。`AC_CHECK_LIB` 的参数是：

```
... 找到时的动作，未找到时的动作，其他库>
```

如果带有 `-readline` 编译成功，该宏会设置变量 `RLIB`。在这种情况下，我们还需要链接 `curses` 库，因此它作为 `<其他库>` 参数出现。我们使用空方括号表示在库缺失时不采取任何操作。

```
* config.h 由 configure 自动生成 *

config.h
/* 设置编译时选项 */

/* 如果你有 readline 库，则设置此项 */
#define HAVE_READLINE 1
```

如果我们查看头文件，可以看到 `#define` 行已更改，以反映我们确实拥有 `readline`。

在调试配置脚本时，清除配置缓存是一个好主意。这是一个名为 `config.cache` 的文件，`configure` 用它记录多次运行之间的测试结果。你可以安全地删除它，并强制 `configure` 重新执行所有测试。当你更改 `configure.in` 文件并运行 `autoconf` 时，养成这是一个良好的习惯。

```
$ rm config.cache
$ autoconf
$ ./configure
creating cache ./config.cache
checking how to run the C preprocessor... cc -E
checking for ANSI C header files... yes
checking for deadline/deadline.h... yes
checking for rl_bind_key in -deadline... yes
updating cache ..config.cache
creating ./config.status
creating Makefile
creating config.h
config.h unchanged
```

现在我们可以看到，通过调用 `AC_OUTPUT(Makefile)`，我们已经从 `Makefile.in` 中生成了一个名为 `Makefile` 的 makefile，并且其中包含了适当的库定义：

```
# Generated automatically from Makefile.in by configure.
```

```
RLIB = -deadline -lncurses
dvdstore.o
$(CC) -o dvdstore dvdstore.o dvd_pg.a $(RLIB)
```

与 `autoconf` 类似，`automake` 程序会根据模板 `Makefile.am` 文件在文件中生成标准的 `Makefile.in`。其核心思想是使 makefile 中 make 宏和规则的使用标准化。如果你有兴趣进一步学习，请查看 `automake` 的 info 文件。

通过使用 `autoconf` 和 `configure`，我们能够创建可移植的源码并将其分发给用户，希望他们能够在安装了不同工具集和库的广泛系统中运行该程序。

# 源 RPM 包 (Source RPM Packages)

如前所述，源 RPM (source RPM) 是一种特殊的 RPM，它包含了应用程序的源代码、RPM 创建者需要应用到 RPM 的任何补丁，以及一个将应用程序构建为二进制 RPM 的规范文件。

安装时，源 RPM 通常会将源代码（通常是 tarball 格式）放在 `/usr/src/packages/SOURCES`，并将规范文件放在 `/usr/src/packages/SPECS` 中：具体位置可能随发行版而异；另一个常见位置是 `/var/rpm` 及其子目录。

让我们来看一个源 RPM 示例，在本例中是 SuSE 6.3 中的 XBoard ，即 `xboard.spec`。

# 第27 章

如果我们使用 `rpm` 程序列出内容，可以看到源码、补丁和规范：

```
$ rpm -q -l -p xboard.rpm
xboard-4.0.0.diff
xboard-4.0.0.tar.gz
xboard.spec
$
```

我们可以通过安装 RPM，将文件提取到 `/usr/src/packages/SOURCES`（或 `rpm` 配置为放置它们的地方）：

```
$ rpm -i xboard.rpm
```

# 构建 RPM 包 (Building an RPM Package)

RPM 包是分发我们自己的应用程序的理想方式。对于用户来说易于操作，支持简单的安装、卸载、查询和依赖解析。那么，我们该如何制作属于自己的 RPM 呢？

创建自己的 RPM 最简单的方法是“走捷径”。RPM 创建者有许多选项可用，其中许多选项很少被使用。本着开源的精神，我们可以“借用”创建另一个 RPM 时使用的规范和技术来制作我们自己的。

由于 RPM 的创建可能非常复杂（甚至可能专门写一本书），我们在本章中将坚持使用简单的示例，即将一个合理的应用程序作为源码或二进制进行分发。我们将更深奥的选项以及通过补丁派生的包支持留给感兴趣读者。更多信息请查看 `rpm` 程序的帮助页或 RPM HOWTO（通常位于 `/usr/doc` 中）。

为我们的 DVD 商店应用程序 `dvdstore` 创建一个 RPM。

RPM 创建过程的核心是规范文件 (spec file)，将其命名为 `dvdstore.spec`。规范文件包含多个部分，描述了应用程序如何构建、如何安装以及它的依赖项。

当我们创建一个 RPM 时，`rpm` 程序将通过许多步骤，对于每个步骤我们都能对其进行某些控制。我们将使用规范文件的部分来规定我们希望发生的情况。

通常情况下，`rpm` 程序将使用 `/usr/src/packages`（或 `/var/lib/rpm`）树进行操作。源码 tarball 存储在 `SOURCES` 中，spec 文件在 `SPECS` 中，RPM 包将在 `RPMS` 中创建，二进制 RPM 包在 `RPM` 中。应用程序在 `BUILD` 的子目录下构建。

给定一个规范文件，`rpm` 程序将在 `SOURCES` 中查找源码 tarball，将其解压到 `BUILD` 的子目录中，进入该目录，构建应用程序，安装它并创建 RPM 包。

我们将给出由规范文件控制的流程概述。

规范文件的第一部分包含描述应用程序的项目——它提供了哪些功能以及它需要哪些内容：

```
# spec file for package dvdstore (Version 1.1)

Vendor: Wrox Press
Distribution: Any
Name: dvdstore
Release: 1
Packager: neil1@tilde.co.uk
Copyright: 2000 by Wrox Press
Group: Applications/Media
Provides: dvdstore
Requires: postgres-6.5
Autoreprov: on
Version: 1.1
Summary: DVD Rental Store Application
Source: dvdstore-1.1.tar.gz
```

这里的大多数项目都是自言自明的。RPM 包的名称格式为：

`Name-Version.architecture`

其中 `architecture` 对于源 RPM 为 `src`，对于不特定平台的 RPM 为 `no`，对于基于 Intel 机器的二进制 RPM 为 `i386`。

`Group` 项目用于引导包安装程序。它指定了包应该归类的类别。

下一个部分是自由格式（但强制性）部分，用于描述应用程序，通常提供作者详情和联系方式：

```
@description
DVD Store Application
```

一个用于管理 DVD 商店的应用程序，包括会员、租赁、还和预约。

此版本需要 PostgreSQL 6.5。

作者：Neil Matthew 和 Richard Stones

后续部分包含 RPM 构建过程使用的命令，用于准备源码、执行构建并安装应用程序：

`%prep`

`%build`

`%install`

`%prep` 部分用于为构建准备源码，并在必要时应用任何补丁。有一个用于解压源码 tarball 的 make 脚本。对于我们的应用程序这足够了。

`%build` 部分包含如何构建应用程序的指令。对于简单的 make 足够了，对于复杂的应用程序，可能会调用与特定构建相关的参数的 `configure` 脚本，例如用于制作具有特殊选项的二进制 RPM。

`%install` 部分包含本地安装应用程序的指令。
