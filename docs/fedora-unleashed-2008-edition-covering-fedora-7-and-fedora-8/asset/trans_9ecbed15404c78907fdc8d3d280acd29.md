

需要了解 make 使用的特殊语法；以下章节将带你熟悉基础的 make 设置。

## 使用 Makefile

make 命令通过使用 makefile 自动构建和更新应用程序。makefile 是一个文本文件，其中包含有关传递给编译器预处理器、编译器、汇编器和链接器的选项的说明。makefile 还规定了其他事项，例如为特定的代码模块必须编译哪些源代码文件（以及编译器命令行），以及构建程序需要哪些代码模块——这种机制称为依赖项检查。

make 机制的美感在于其灵活性。你可以使用简单的 makefile，也可以编写复杂的 makefile，其中包含大量宏、规则或命令，这些命令可以在单个目录中工作，也可以递归遍历你的文件系统以构建程序、更新你的系统，甚至充当文档管理系统。make 命令适用于几乎所有程序，包括 TeX 等文本处理系统。

你可以使用 make 来编译、构建和安装软件包，使用如此简单的命令：

```
# make install
```

你可以使用默认的 makefile（通常称为 Makefile，大写 M），或者你可以使用 make 的 -f 选项来指定任何 makefile，例如 MyMakefile，像这样：

```
# make -f MyMakefile
```

根据你的 makefile 的内容，可能还有其他可用的选项。

## 使用宏和 Makefile 目标

使用带有宏的 make 可以使程序具有可移植性。宏使其他操作系统的用户能够通过指定本地值（例如所需软件工具的名称、位置或路径名）来轻松配置程序构建。在下例中，宏定义了编译器的名称（CC）、安装程序（INS）、程序应安装到的位置（INSdir）、链接器应查找所需库的位置（LIBdir）、所需库的名称（LIBs）、源代码文件（SRC）、中间目标代码文件（OBS）以及最终程序的名称（PROG）：

```
# 骨架程序的示例 makefile
CC= gcc
INS= install

INSdir= /usr/local/bin
LIBdir= -L/usr/X11R6/lib
LIBs= -lXm -lSM -lICE -lXt -lX11
SRC= skel.c
OBS= skel.o
PROG= skel

skel:  $(OBJS)
    $(CC) -o $(PROG) $(SRC) $(LIBDIR) $(LIBS)

install: $(PROG)
    $(INS) -g root -o root $(PROG) $(INSIDIR)
```

**注意**
上一个示例中缩进的行是使用制表符（tabs）而不是空格进行缩进的。这一点非常重要，请牢记！人类很难看出其中的区别，但 make 可以分辨出来。如果刚开始在 Linux 下构建程序时，make 报告了令人困惑的错误，你应该检查项目的 makefile 是否使用了制表符以及其他正确的格式。

使用前面示例中的 makefile，你可以像这样构建程序：

```
# make
```

要构建 makefile 的指定组件，可以在命令行上使用目标定义。要仅构建程序，你可以使用带有 skel 目标的 make，像这样：

```
# make skel
```

如果你对目标的任何元素进行了更改，例如源代码文件，make 会自动重建目标。这是使用 make 管理开发项目的便利性的一部分。要在一步中构建并安装程序，你可以指定 install 目标，像这样：

```
# make install
```

较大的软件项目可能在 makefile 中包含许多传统目标，例如：

- test——对最终软件运行特定测试
- man——使用 man 宏处理 include 或 troff 文档
- clean——删除剩余的目标文件
- archive——清理、归档并压缩整个源代码树
- bugreport——自动收集并发送构建或错误日志的副本

大型应用程序可能需要数百个源代码文件。编译和链接这些应用程序可能是一项复杂且容易出错的任务。make 实用程序帮助你组织从多个源文件构建复杂应用程序的可执行形式的过程。

## 使用 autoconf 实用程序配置代码

make 命令只是 Fedora 包含的多个编程自动化实用程序之一。还有其他实用程序，例如 **p**ake（触发并行 make）、i**make**（一种依赖项驱动的 makefile 生成器，用于构建 X11 客户端）、auto**make**，以及较新的工具之一 auto**conf**，后者构建可用于配置程序源代码包的 shell 脚本。

构建以源代码形式分发的许多 Linux 软件包需要使用 GNU 的 auto**conf** 实用程序。该程序构建了一个名为 *configure* 的可执行客户端脚本，执行时会自动检查并根据安装在目标主机（你的 Linux 系统）上的软件资源或*依赖项*（如编程工具、库和相关实用程序）来定制客户端的源代码构建。

以源代码形式下载的许多 Linux 命令和 X 图形客户端包含 *configure* 脚本。要配置源代码包、构建软件，然后安装新程序，root 用户可以像这样使用该脚本（在解压缩源代码并导航到生成的构建目录后）：

```
# ./configure ; make ; make install
```

autoconf 程序使用名为 *configure.in* 的文件，其中包含基本的*规则集*，即一组宏。*configure.in* 文件是使用 auto**scan** 命令创建的。构建正确执行的 *configure* 脚本还需要一个名为 *Makefile.in* 的 makefile 模板。虽然手动创建依赖项检查 *configure* 脚本是可以的，但你可以通过使用图形化项目开发工具（如 KDE 的 K**de**velop 或 GNOME 的 **Glade**）轻松克服任何复杂的依赖项。（更多信息，请参见本章后面“图形化开发工具”部分。）

## 使用 Subversion 管理软件项目

虽然 make 可用于管理软件项目，但大型软件项目需要文档管理、源代码控制、安全性以及修订跟踪，因为源代码在其开发过程中会经过一系列变更。Subversion 为这种大型软件项目管理提供源代码版本控制实用程序。

Subversion 系统用于跟踪文件多个版本的更改，并可用于在项目范围内回溯或分支文档版本。它还可以用于预防或解决由多个开发人员对源代码文件所做的冲突条目或更改。使用 Subversion 进行源代码控制要求在 **svn** 命令行上使用至少以下五个命令选项：

- **checkout**—签出修订版本
- **update**—使用其他开发人员所做的更改更新你的源代码
- **add**—将新文件添加到存储库
- **delete**—从存储库中删除文件
- **commit**—将更改发布给其他存储库开发人员

请注意，其中一些命令要求你使用额外的字段，例如文件名。对于 commit 命令，你应始终尝试传递 -m 参数（允许你提供描述更改的消息），后跟关于你的更改的一些信息。例如：

```
svn commit -m "This fixes bug 204982."
```

Subversion 最令人印象深刻的功能之一是其离线工作能力——任何本地 Subversion 签出都会自动隐藏一个 .svn 目录，其中包含所有已签出文件的副本。得益于这一点，你无需联系服务器即可将当前文件与签出的文件进行对比——这一切都在本地运行。

# 调试工具

调试既是一门科学，也是一门艺术。有时，最简单的工具——代码列表——是最好的调试工具。然而在其他时候，你需要使用其他调试工具。其中三个工具是 splint、gprof 和 gdb。

## 使用 splint 检查源代码

splint 命令类似于传统的 Unix lint 命令：它静态检查源代码中的潜在问题，并且还有许多其他附加功能。即使你的 C 代码符合 C 标准并能干净地编译，它可能仍然包含错误。splint 执行多种类型的检查，并可以提供广泛的错误信息。例如，这个简单的程序可能可以干净地编译甚至运行：

```
$ gcc -o tux tux.c
$ ./tux
```

但 splint 命令可能会指出源代码中存在一些严重问题：

```
$ splint tux.c
Splint 3.1.1 --- 17 Feb 2004

tux.c: (in function main)
tux.c:2:19: Return value (type int) ignored: putchar(t[+i++])+...
Result returned by function call is not used. If this is intended, can cast result to (void) to eliminate message. (Use -retvalint to inhibit warning)
Finished checking --- 1 code warning
```

你可以使用 splint 命令的 -strict 选项，像这样，以获得更详细的报告：

```
$ splint -strict tux.c
```

GCC 还支持通过使用广泛的警告（通过 -Wall 和 -pedantic 选项）进行诊断：

