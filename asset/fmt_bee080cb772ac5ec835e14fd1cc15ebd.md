
- Qt 和 K 应用框架编程实际上是伪装的 X Windows 编程。

- 不要混合 C++ 和 Java 编程。当你利用已经构建好的组件时，可以更快地开发应用。如果 C++ 没有，Java 就会，反之亦然。

- 企鹅原则 #1：不要在明天构建今天已经构建的东西。

# Linux 编程环境准备工作

# 第 2 章

## 本章内容

- 确定内核版本

- 理解环境变量

- 理解库

- 查找帮助

- 使用 `gcc` 编译程序

在为 Linux 开发应用之前，你需要了解内核版本、环境变量、库、查找帮助以及使用 `gcc` 编译程序。在开发 Linux 应用之前，你需要熟悉环境变量、共享库、静态链接和动态链接。不仅 Qt、K 等流行的工具包需要环境变量和共享库，你还需要了解 `make` 文件、`gcc` 选项以及内核版本。对于访问权限（见第 9 章）以及源码和对象代码。此外，开发 Linux 环境需要熟悉常用的目录（见第 14 章）。本章将为你提供开发所需的准备工作，了解工具是什么、在哪里以及如何使用。

### 确定内核版本

为了从我们将使用的工具中受益，你的 Linux 内核至少应该是 2.0 版本。要查看运行的内核版本，输入：

```
uname -r
```

`uname` 命令打印系统信息。`r` 参数请求发布版本。`dmesg` 命令也可以用于查看内核版本：

```
dmesg
```

### 查看安装的 gcc 版本

Qt 工具和 K 应用框架是 C++ 类库。你需要一个 C++ 编译器来开发 Qt 或 K。`gcc` 编译器随 Linux 提供，并可编译 C++ 程序。我们建议使用更高版本。要查看安装的 `gcc` 版本，输入：

```
gcc -v
```

`gcc` 版本越高，对标准 C++ 库的支持越好。标准 C++ 库有很多重要的类可以帮助开发。书中的示例利用了 `i` 类库、容器类以及标准 C++ 库中的许多工具类。

### 查看安装的 Java 版本

我们在书中介绍的若干快速应用开发技术都需要 Java 类库。由于 Java Swing 类的可用性，我们建议使用 Java 1.1.7 或更高版本。要查看安装的 Java 版本，输入：

```
java -version
```

### 什么是环境变量

环境变量是 shell 的变量，用于存储运行程序可以访问的重要信息。例如，Linux 程序或应用程序通常需要知道某些文件的位置、设备的默认设置、主机名、目录位置和其他信息。环境变量用于存储此类信息，以便任何执行中的程序可以使用。你可以随时使用 shell 命令手动设置环境变量的值。虽然这些变量通常在系统启动或用户登录时设置，但程序也可以在执行时设置它们。

Linux 应用开发大量使用环境变量。环境变量存储了共享库、静态库和共享目录。环境变量还存储了机器类型和主机名。最后，环境变量存储了编译 C++ 程序所需的文件位置。

### 检查环境变量

使用 `printenv` 命令检查环境变量的当前值。输入：

```
printenv
```

你将看到类似下面的示例输出：

```
LD_LIBRARY_PATH=/opt/kde/lib
RC_LANG=POSIX
LS_OPTIONS=-a N --color=tty -T 0
ignoreof=0
POVRAYOPT=/usr/lib/povray/include
QTDIR=/usr/lib/qt
OPENWINHOME=/usr/openwin
LESSKEY=/etc/lesskey.bin
LESSPEN=|lesspipe.sh %s
MANPATH=/usr/local/man:/man:/usr/X11R6/man:/usr/openwin/man
NNTPSERVER=news
KDEDIR=/kde
```

这是一个变量/值对列表。值通过等号（`=`）赋值给变量。例如，`LD_LIBRARY_PATH` 变量告诉程序可以在哪里找到额外的共享库。`QTDIR` 变量指定了 Qt 目录的位置。`KDIR` 变量指定了 KDE 目录的起始，因此执行任何程序或应用程序都可以访问环境变量。Linux 环境中的许多程序依赖于环境变量中设置的值，如果没有恰当设置环境变量，它们将无法执行。

### 重要的环境变量

以下环境变量对于应用程序开发很重要：

- `PATH`

- `LD_LIBRARY_PATH`

- `QTDIR`

- `KDEDIR`

- `MANPATH`

# 第 2 章 + Linux 编程环境准备

`PATH` 环境变量包含重要可执行文件的目录（路径）以及与可执行相关的信息。路径设置不当是导致找不到命令、找不到库和核心转储类型错误的最主要原因。

动态链接器 `ld.so` 将检查 `LD_LIBRARY_PATH` 以及 `ld.so.conf` 的内容，以确定共享库的位置。在许多安装中，`ld.so.conf` 文件位于 `/etc` 目录。它包含了常用系统级共享库的路径。如果你希望将用户特定的共享库添加到共享库路径，请使用 `LD_LIBRARY_PATH` 变量。`ld.so.conf` 文件通常用于所有用户必须可用的系统级共享库。

`QTDIR` 和 `KDIR` 是 Qt 和 KDE 开发中重要的环境变量。它们包含了指向重要的 Qt 和 KDE 开发库文件的路径。

最后，`MANPATH` 环境变量包含重要系统级帮助页的路径。Linux 手页包含的内容并不总是足够有用，但在其他时候，它们包含了恰恰所需的信息。确保 `MANPATH` 包含正确的目录将非常有帮助。表 2-1 包含了常用的环境变量。

# 表 2-1

常用环境变量

| 名称 | 描述 |
| --- | --- |
| `HOME` | 你的家目录的完整路径。 |
| `PATH` | 命令搜索的目录列表。 |
| `MAIL` | 你的邮箱完整路径。 |
| `USER` | 你的用户 ID。 |
| `SHELL` | 你的登录 shell 的完整路径。 |
| `TERM` | 你所使用的终端类型。 |
| `MANPATH` | 存储 man 页目录的变量。 |
| `LD_LIBRARY_PATH` | 存储共享库目录的变量。 |
| `QTDIR` | 存储 Qt 库目录的变量。 |
| `KEDIR` | 存储 KDE 文件目录的变量。 |

# 访问环境变量

访问环境变量有两种简单方法。第一种是通过 `main()` 函数的第三个参数在 C++ 程序中访问环境变量。第二种方法使用 `setenv()` 和 `getenv()` 函数。如果调用 `main()` 时使用了第三个参数，那么它对你的程序可用，并可访问环境变量。如果没有使用第三个参数，可以使用 `getenv()` 和 `setenv()` 函数。

使用 `main()` 的第三个参数：

```
int main(int argc, char argv[], char *envp)
```

`main` 的第一个参数是 `argc`。`argc` 参数包含程序拥有的命令行参数数量。这个数字包含了程序本身的名字。例如，如果我们指定程序 `penguin` 并带上如下所示的单个命令行参数：

```
penguin -help
```

那么 `argc` 的值为 2。程序名 `penguin` 计为一个，`-help` 计为一个。

```
argv[0] 可能包含 penguin
argv[1] 可能包含 -help
```

像 C++ 数组一样，第一个元素从零开始。

# 列表 2-1：一个列出环境变量的程序

```
// 列表 2-1
// 此程序显示环境变量。

#include <iostream>
#include <string>

int main(int argc, char argv[], char *envp[])
{
    int N = 0;
    while (envp[N] != '\0')
```

你将看到类似下面的示例输出：

```
LD_LIBRARY_PATH=/opt/kde/lib
RC_LANG=POSIX
LS_OPTIONS=-a N --color=tty -T 0
ignoreof=0
POVRAYOPT=/usr/lib/povray/include
QTDIR=/usr/lib/qt
OPENWINHOME=/usr/openwin
LESSKEY=/etc/lesskey.bin
LESSPEN=|lesspipe.sh %s
MANPATH=/usr/local/man:/man:/usr/X11R6/man:/usr/openwin/man
NNTPSERVER=news
KDEDIR=/kde
```

这是一个变量/值对列表。值通过等号（`=`）赋值给变量。例如，`LD_LIBRARY_PATH` 变量告诉程序可以在哪里找到额外的共享库。`QTDIR` 变量指定了 Qt 目录的位置。`KDIR` 变量指定了 KDE 目录的起始，因此执行任何程序或应用程序都可以访问环境变量。Linux 环境中的许多程序依赖于环境变量中设置的值，如果没有恰当设置环境变量，它们将无法执行。

# 列表 2-2：显示 HOME 变量的程序
