
``` 
$ ./configure ; make ; sudo make install
```

`autoconf`程序使用一个`configure.in`文件，其中包含基础规则集或一组宏。`configure.in`文件是通过`autoscan`命令创建的。构建一个执行正常的`configure`脚本还需要一个 make 模板即`Makefile.in`。虽然可以手动创建检查依赖的`configure`脚本，但你可以使用图形化项目开发工具（如 KDE 的 Kdevel 或 GNOME 的 Glade）轻松解决依赖问题。（更多信息请参阅本章后文“图形化开发工具”部分。）

# 使用 Subversion 管理软件项目

虽然可以使用`make`管理软件项目，但大型软件项目需要文档管理、源码控制和修订跟踪，因为源码在开发过程中会经历一系列更改。Subversion 为这类大型软件项目管理提供了源码版本控制工具。

Subversion 系统用于跟踪多个版本文件的更改，并可用于项目范围内的文档版本回溯或分支处理。它可以防止或解决多个开发人员对源码文件引起的冲突条目或更改。使用 Subversion 进行源码控制需要在`sv`命令行上至少使用以下五个命令选项：

- `checkout`--检出版本
- `update`--使用其他开发者所做的更改更新你的源码
- `add`--将新文件添加到存储库
- `delete`—从存储库删除文件
- `commit`—将更改发布给存储库的其他开发者

# 第 26 章 Ubuntu 的 C/C++ 编程工具

请注意，这些命令可能需要你使用额外的字段，例如文件名。在使用`commit`命令时，应始终尝试传递`-m`参数（让你提供一个描述更改的消息），后跟上一些关于你更改的信息。例如：

```
svn commit -m "This fixes bug 204982."
```

Subversion 最令人印象深刻的特性之一是它的离线工作能力——任何隐藏在其中的本地 Subversion 检出都包含了所有已检出文件的副本。得益于此，你可以将当前文件与已检出的文件进行对比，而无需联系服务器——这一切都是在本地运行。

# 调试工具

调试既是科学也是艺术。有时，最简单的工具——代码列表——就是最好的调试工具。但在其他情况下，你需要使用其他的调试工具。其中三个是`splint`、`gdb`和`gdb`（注：原文此处重复了 gdb）。

## 使用 splint 检查源码

`splint`命令与传统的 Unix `lint`命令类似：它静态地检查源码中可能的问题，并且还具有许多额外功能。即使你的 C 代码符合 C 标准并能够顺利编译，它可能仍然包含错误。`splint`执行许多类型的检查并可以提供详尽的错误信息。例如，这个简单的程序可能可以编译通过并运行：

```
$ gcc -o tux tux.c

./tux
```

但`splint`命令可能会指出源码中的一些严重问题：

```
$ splint tux.c

Splint 3.1.1 — 17 Feb 2004
```

```
tux.c: (in function main)

tux.c:2:19: Return value (type int) ignored: putchar(t[++j]) ...
```

函数调用的返回值未被使用。如果这是刻意为之的，可以将结果强制类型为`(void)`以消除消息。（使用`-retvalint`抑制警告）

```
Finished checking — 1 code warning
```

你可以像这样使用`splint`命令的`-strict`选项来获取更详细的报告：

```
$ splint -strict tux.c
```

GCC 还通过使用大量的警告来支持诊断（通过`-Wall`和`-pedantic`选项）：

## 使用 GNU C 编译器

```
$ gcc -Wall tux.c
tux.c:1: warning: return type defaults to 'int'
tux.c: In function 'main'
tux.c:2: warning: implicit declaration of function 'putchar'
```

## 使用 gprof 跟踪函数时间

当你使用`gcc`编译 C 程序时，编译过程分为几个阶段：

- 1. 首先，C预处理器解析文件。为此，它顺序读取行、包含头文件并执行宏替换。
- 2. 编译器解析后的代码以确定语法是否正确。在此过程中，它构建符号表并创建中间格式。大多数符号都被分配了特定的内存地址，但在其他模块定义的符号没有。
- 3. 编译的最后阶段链接将不同的文件和库连接起来，并通过解决之前未解决的符号。

如果你遵循严格的 ANSI 标准，大多数 C 程序可以使用 C++ 编译器编译。例如，你可以使用 C++ 编译器编译标准的`hello.c`程序（每个第一个程序）。通常，你将文件命名为`hello.cc`、`hello.C`、`hello.c++`或`hello.cxx`。GNU C++ 编译器接受这些名称。

# 图形化开发工具

Ubuntu 包含了一些用于 X 会话的图形化原型开发环境。如果你想为 KDE 或 GNOME 构建客户端软件，可能会发现 KDevelop、Qt Designer 和 Glade 程序非常有帮助。你可以使用这些程序中的任何一个来构建交互式窗口的图形框架，并可以使用它们自动生成支持程序自定义界面所需的代码骨架。

## 使用 KDevlop

你可以从应用程序菜单启动 KDevlop 客户端（如图 26.1 所示），也可以从终端窗口的命令行启动，如下：

```
$ kdevlop &
```
