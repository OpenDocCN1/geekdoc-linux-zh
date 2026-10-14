
# 你需要帮助还是想要帮助？

XFree86 项目有九个不同的邮件列表，你可以使用它们来提问、接收新闻或向其他用户提供建议。访问 http://www.xfree86.org/mailman/listinfo 并选择你感兴趣的列表。许多新用户想要订阅 `Newbie` 邮件列表。关于 X 的通用讨论，请订阅 `Expert` 列表。你只需要点击所需列表的链接，然后输入你的电子邮件地址和密码。

这种方法也适用于新构建的 `bitmap`、`xclock`、`xmag`、`xbiff`、`xcalc`、`xeyes`、`xfontsel`、`xload`、`xman`、`xterm`。如果你安装了新的服务器、库和客户端，不需要修改 `LD_LIBRARY_PATH`。

# 资源信息

- http://www.xfree86.org——学习更多 XFree86 的起点。
- ftp://ftp.xfree86.org——获取最新 XFree86 二进制或源码发行的主要站点。
- http://www.xfree86.org/cvs/——使用 XFree86 公共 CVS 系统下载最新 XFree86 源码的指南。
- http://www.bastille-linux.org/java/vaio.html——Jay Beal 的 Sony 页面（从 Linux 笔记本页面链接）。
- http://cs.utexas.edu/users/kharker/linux-laptop/——笔记本页面，包含指向数百个关于让 Linux 和 XFree86 在笔记本电脑上运行解决方案的网站链接。
- http://www.matrox.com/mga/support/drivers/latest/home.cfm——Matrox Graphics 公司网站，提供了适用于 Matrox 产品线的最新 Linux XFree86 驱动链接——模范公司的网站！
- comp.os.linux.x——Usenet 新闻组，包含关于构建、安装、配置、管理和使用 XFree86 的许多答案。

# 第 18 章：基础 X11 编程

- 安装 XFree86 开发支持
- 使用基础编程工具
- 使用 `make`、`imake` 和 `xmkmf`
- 创建、构建和安装简单的客户端

![](img/078622fac3fd61e5a0c895da1d3eff96_368_0.png)

本章介绍了开始为 X Window 系统开发简单客户端时将需要的概念、软件工具和资源（如软件库）。你将获得 X 编程的概述，发现几个实用的实用程序，学习如何使用某些编程工具，然后查看如何构建简单的 X11 客户端。

为 X11 编程需要对可用资源有基本的了解，因为此类函数调用是由随 XFree86 提供的各种软件工具包提供的。为 X 编程的好处之一是可移植性，即你的代码在各种其他计算机平台上进行构建和编译的能力，无论操作系统或硬件如何。只要其他计算机支持 X11 且你的代码与硬件无关，你的程序应该在少少或没有更改的情况下在其他机器上生存并成功构建。

## 安装 XFree86 开发支持

如果你已经安装了 XFree86，但想开发用于 Linux 的程序，你必须确保也安装了运行良好的 C（可能还有 C++）开发系统。这意味着你可能需要安装 Linux 内内核头文件、`gcc` 编译器以及相关的开发软件库和文档。你需要 GNU 开发工具，例如汇编器、`ld` 链接器等。幸运的是，大多数 Linux 发行版通过某种形式的包管理器（如 Red Hat 的 `rpm` 命令、SUSE 的 `yet`（基于 rpm）或 Debian 的 `app-get` 系统）使安装开发支持变得非常容易。

## 核心编程工具

通过再次使用 `rpm` 命令及其查询选项来开发软件包，但此处带有列表选项，如下：

```
$ rpm -ql XFree86-devel-4.0.1-1 | less
```

当你将输出通过到 `less` 分页命令时，你可以浏览文件列表。你将看到 XFree86 开发文件的内容被安装在以下目录下：

- `/usr/X11R/bin`—九个二进制软件工具。
- `/usr/X11R/include/X11`—X11 `#include` 文件，包含定义、默认值以及默认函数的默认值。
- `/usr/X11R/include/bitmaps`—近 100 个在编程时可能使用的位图（注意，这些文件不是必须的，也不是专有的）。
- `/usr/X11R/include/X11/extensions`—包含扩展函数默认值和定义的 `#include` 文件。
- `/usr/X11R/include/X11/fonts`—包含字体编程信息的 `#include` 文件。
- `/usr/X11R/lib/X11/config`—包含规则集的文件（本地操作系统和其他操作系统所使用的默认定义）。你在构建配置文件和 `Makefile` 时会使用这些文件，它们有助于构建本地 X11 客户端。规则集信息在构建过程中将由 `xmkmf` 和 `make` 命令使用。
- `/usr/X11R/lib`—包含 X 客户端使用的函数的 X 软件库。该目录持有几个库，例如基础的 Xlib、Xt Intrinsics、X Toolkit 和 Athena Xaw 库。在 XFree86 4.0 及更高版本中，你还可以在此目录中找到 Xpm (X 像素映射图) 库。
- `/usr/X11R/man/man3`—描述 X11 函数的帮助页（man pages）。

安装 XFree86 开发包需要额外的 9MB 硬盘空间。普通的 Linux 开发工具可能需要 20MB 或更多的硬盘空间，这取决于你安装的工具和库的类型。

## 使用核心编程工具

设计和编写创建 X11 客户端的代码可能与设计和编写 Linux 命令（或为从命令行运行并使用命令行设计的命令）非常不同。许多 Linux 命令源于传统的 UNIX 对应物，并遵循与图形 X 客户端不同的设计和用法。这种命令被用作过滤程序的示例如下。此类命令的设计目的是接收来自另一个程序的输入，修改输入，然后通过标准输出、重定向的标准输出或另一个管道将输入以及修改后的数据作为输出。

# 第 10 章：基础 X11 编程

以下是一个使用过滤器作为命令行哲学的示例：

```
### find /usr/share/doc -name *.txt -print | xargs cat | tr ' ' '

'

| sort | uniq | egrep -av [[:digit:]] | egrep -av [[:punct:]]

| egrep -av [[:space:]] | egrep -av [[:ctrl:]]> mydict
```

在这个示例中，使用了 `xargs`、`tr`、`sort`、`uniq` 和 `egrep` 命令通过在 `/share/doc` 目录下所有文本文件中找到的快速构建一个名为 `mydict` 的字典（尽管没有拼写检查）。然后你可以这样将 `egrep` 命令添加到 `mydict` 文件的开头：

```bash
#!/bin/sh
/bin/egrep -i $ <<zzzz
```

将字符串 `zzzz` 添加到文件末尾，然后使用带有 `+x` 选项的 `chmod` 命令使文件变为可执行。你随后可以使用整个字典作为一个搜索字典本身的命令。例如，要查找包含 `expense` 的所有单词，使用以下命令：

```
### ./mydict expen

expable

expense

expensive

inexpensive
```
