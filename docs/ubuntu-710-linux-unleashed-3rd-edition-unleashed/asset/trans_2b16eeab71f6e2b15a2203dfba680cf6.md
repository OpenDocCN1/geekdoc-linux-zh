
## 使用 Makefile

你需要学习 make 使用的特殊语法；以下章节将引导你完成一个基本的 make 设置。

make 命令通过 makefile 自动构建和更新应用程序。makefile 是一个文本文件，其中包含关于应将哪些选项传递给编译器预处理器、编译器、汇编器和链接器的说明。makefile 还规定（除其他事项外）对于特定代码模块，必须编译哪些源代码文件（以及编译器命令行），以及构建程序需要哪些代码模块——这种机制称为依赖检查。

make 命令的美妙之处在于它的灵活性。你可以将 make 与简单的 makefile 一起使用，也可以编写包含大量宏、规则或命令的复杂 makefile，这些宏、规则或命令可以在单个目录中工作，也可以递归遍历你的文件系统以构建程序、更新系统，甚至充当文档管理系统。make 命令几乎适用于任何程序，包括诸如 TeX 之类的文本处理系统。

你可以使用 make 通过如下简单命令来编译、构建和安装软件包：

```
# make install
```

你可以使用默认的 makefile（通常称为 Makefile，大写 M），也可以使用 make 的 -f 选项来指定任意 makefile，例如 MyMakefile，如下所示：

```
# make -f MyMakefile
```

根据 makefile 的内容，可能还有其他选项可用。

## 使用宏和 Makefile 目标

将 make 与宏一起使用可以使程序具有可移植性。宏允许其他操作系统的用户通过指定本地值（例如任何所需软件工具的名称和位置或路径名）来轻松配置程序构建。在以下示例中，宏定义了编译器名称 (CC)、安装程序 (INS)、程序应安装的位置 (INSDIR)、链接器应查找所需库的位置 (LIBDIR)、所需库的名称 (LIBS)、源代码文件 (SRC)、中间目标代码文件 (OBS) 以及最终程序名称 (PROG)：

```
# a sample makefile for a skeleton program
CC= gcc
INS= install
INSDIR= /usr/local/bin
LIBDIR= -L/usr/X11R6/lib
LIBS= -lXm -lSM -lICE -lXt -lX11
SRC= skel.c
OBJS= skel.o
PROG= skel
```

```
skel: $(OBJS)
    $(CC) -o $(PROG) $(SRC) $(LIBDIR) $(LIBS)

install: $(PROG)
    $(INS) -g root -o root $(PROG) $(INSDIR)
```

### 注意

前一示例中的缩进行使用的是制表符，而不是空格。这一点很重要，请务必记住！人很难看出区别，但 make 可以分辨。如果你在 Linux 下初次构建程序时 make 报告了令人困惑的错误，请检查你项目的 makefile 是否使用了制表符以及其他正确的格式。

使用前一示例中的 makefile，你可以像这样构建程序：

```
# make
```

要构建 makefile 的指定组件，你可以在命令行中使用目标定义。若要仅构建程序，你可以将 make 与 skel 目标一起使用，如下所示：

```
# make skel
```

如果你对目标对象的任何元素（例如源代码文件）做了任何更改，make 会自动重新构建该目标。这一特性是使用 make 管理开发项目便利性的体现。要一步完成构建和安装程序，你可以指定 install 目标，如下所示：

```
# make install
```

较大的软件项目可能在 makefile 中包含许多传统目标，例如：

- test — 对最终软件运行特定测试
- man — 使用 man 宏处理 include 或 troff 文档
- clean — 删除所有剩余的目标文件
- archive — 清理、归档并压缩整个源代码树
- bugreport — 自动收集构建或错误日志的副本并通过邮件发送

大型应用程序可能需要数百个源代码文件。编译和链接这些应用程序可能是一项复杂且容易出错的任务。make 实用程序可帮助你组织从许多源文件构建复杂应用程序可执行形式的过程。
