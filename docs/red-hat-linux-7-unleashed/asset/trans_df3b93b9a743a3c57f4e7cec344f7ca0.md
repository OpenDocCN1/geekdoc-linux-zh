
# GNU egcs 编译器系统的新特性

*egcs*（发音为“eggs”）程序套件最初是 *gcc* 编译器的一个实验版本，其开发最初由 Cygnus Support（现为 Red Hat 的一部分）托管。从针对 Intel 的 Red Hat 5.1 开始，*egcs* 可以作为 Red Hat Linux 系统的一部分进行安装。

在最初开发时，Cygnus 将 *egcs* 描述为 *gcc* 开发过程中的一个实验性步骤。自 1997 年夏末首次发布以来，*egcs* 吸收了 *gcc* *并行*开发的许多最新发展和特性，并增加了许多自身的新发展，例如内置的 Fortran 77、Java 和 Objective C 前端。有些人建议将名称从“Experimental GNU Compiler System”（实验性 GNU 编译器系统）改为“Enhanced GNU Compiler System”（增强型 GNU 编译器系统）。

> 你需要使用 *egcs* 编译器的 *gcj* 前端来编译 Java 语言类。前端软件及相关包应随 Red Hat Linux 一起提供，但你可以通过访问 *http://sources.redhat.com/java/compiler.html* 了解更多关于 *egcs* Java 支持的信息。勇敢的 Linux 开发者可以通过 Red Hat 网站直接跳转到最新的 *egcs* 和 Java 支持软件的源代码树。

尽管一些 Linux 开发者可能认为 *egcs* 的开发代表了 *gcc* 编译器开发的分叉（或分裂），但 Cygnus 表示，*gcc* 和 *egcs* 开发者之间的合作将防止这种情况发生。根据 Cygnus 的说法，希望 *egcs* 的新编译器架构和特性有助于使 *gcc* 成为世界上最好的编译器。

1999 年 4 月，*egcs* 正式成为未来 GNU *gcc* 软件的一部分，并且根据 Cygnus 的说法，*egcs* 团队将负责推出未来的 GCC 版本。我们只能希望 Red Hat 能履行这一承诺。

当你使用 *egcs* 时，如果你尝试构建一个用 C++ 编写并在其 Makefile 中引用 *gcc* 的软件包，可能会出现问题。

## Linux C/C++ 编程工具

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_816_0.png)

Makefile 脚本可能包含构建过程中使用的程序和文件名称及位置。wxw Makefile 包含以下两个定义：

```
CC     = gcc
CXX    = gcc
```

如果你只安装了 gcc，这将正常工作；但如果你安装了 egcs 套件，你需要将 Makefile 中指定的 C++ 编译器名称更改为 g++，如下所示：

```
CC     = gcc
CXX    = g++
```

只需注意，如果你使用 egcs 来编译 C++ 源文件（扩展名为 .c、.cc 或 .cxx 的文件），你可能需要首先修复软件的 Makefile。

关于 egcs 以及 egcs 的最新更新、版本或特性新闻的更多信息，请访问 http://www.gnu.org/software/gcc/gcc.html。你将找到 egcs FAQ 以及指向最新稳定版 egcs 发布版或最新开发版本快照的链接。

## 额外资源

如果你想进一步了解 C 和 C++，你应该查阅以下书籍：

- *Sams Teach Yourself C in 21 Days*，作者 Peter Aitken 和 Bradley Jones，Sams Publishing 出版。
- *Sams Teach Yourself C++ for Linux in 21 Days*，作者 Jesse Liberty 和 David B. Horvath，CCP，Sams Publishing 出版。
- *C How to Program and C++ How to Program*，作者 H. M. Deitel 和 P. J. Deitel。
- *The C Programming Language*，作者 Brian Kernighan 和 Dennis Ritchie。
- *The Annotated C++ Reference Manual*，作者 Margaret Ellis 和 Bjarne Stroustrup。
- *Programming in ANSI C*，作者 Stephen G. Kochan。

## 总结

UNIX 是基于 C 语言构建的。C 是一种平台无关的、编译型、基于函数和能够推导新的、由程序员定义的数据结构的过程式语言。

C++ 通过提供面向对象设计和代码所需的必要特性来扩展 C 的能力。诸如 **gcc** 等 C++ 编译器可以正确编译 ANSI C 代码。C++ 还提供了一些特性，例如将函数与数据结构关联的能力，这些特性不需要使用完整的基于类的面向对象技术。由于这些原因，C++ 语言允许现有的 UNIX 程序随时间推移逐步向面向对象过渡。

Red Hat Linux 包含许多使 C/C++ 程序员生活更轻松的工具。有用于创建程序的编辑器、用于编译它的 **gcc** 和 **egcs**、用于创建库的 **ar**、用于控制源文件的 RCS 和 CVS、用于构建代码的 **make**、用于调试的 **gdb** 和 **xgdb**，以及用于确定效率低下之处的 **gprof**。充分利用这个环境吧！

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_820_0.png)
![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_820_1.png)

# Shell 脚本

## 本章内容

- 创建和执行 Shell 程序 785
- 变量 788
- 位置参数 789
- 内置变量 790
- 特殊字符 791
- 表达式比较 794
- 迭代语句 802
- 条件语句 807
- 其他语句 811
- 函数 811

当你从命令行输入命令时，你是一次输入一个命令并接收系统的响应。时不时地，你需要依次执行多个命令，并获取最终结果。你可以使用 *shell 程序*或 *shell 脚本*来实现。shell 程序是使用文本编辑器放入文件中的一系列 Linux 命令和实用工具。当你执行 shell 程序时，命令由 Linux 依次解释和执行。

你可以在 Linux 下编写 shell 程序并像执行其他命令一样执行它们。如果其他 shell 程序在搜索路径中，你也可以从一个 shell 程序内部执行其他 shell 程序。shell 程序与其他编程语言类似，拥有自己的语法。你可以定义变量、分配各种值等。这些功能将在本章中讨论。

随本书附带的 Red Hat Linux CD-ROM 中包含了许多功能强大、灵活且强大的 shell。这些 shell 拥有许多内置命令、可配置的命令行提示符，以及命令行历史记录和编辑等特性。表 25.1 列出了每个 shell，及其描述和在 Red Hat Linux 文件系统中的位置。

**表 25.1 Red Hat Linux 中的 Shell**

| 名称 | 描述 | 位置 |
|---|---|---|
| ash | 一个小 shell（类似 sh） | /bin/ash |
| ash.static | 不依赖软件库的 ash 版本 | /bin/ash.static |
| bash | Bourne Again Shell | /bin/bash |
| bsh | 指向 ash 的符号链接 | /bin/bsh |
| csh | C shell，指向 tesh 的符号链接 | /bin/csh |
| ksh | 公共领域的 Korn shell | /bin/ksh, /usr/bin/ksh |
| pdksh | 指向 ksh 的符号链接 | /usr/bin/pdksh |
| rsh | 受限 shell（用于网络操作） | /usr/bin/rsh |
| sh | 指向 bash 的符号链接 | /bin/sh |
| tesh | 兼容 csh 的 shell | /bin/tesh |
| zsh | 兼容 csh、ksh 和 sh 的 shell | /bin/zsh |

## 创建和执行 Shell 程序

假设你想在每次登录时设置一组别名。与其在每次登录时输入所有别名，不如使用诸如 vi 这样的文本编辑器将它们放入文件中，然后执行该文件。

这是我的 myenv 文件中包含的内容，这是一个为此目的创建的示例文件（用于 bash）：

```
#!/bin/sh
alias 11='ls -1'
alias dir='ls'
alias copy='cp'
```

myenv 可以通过多种在 Linux 下执行。

你可以使用 chmod 命令使 myenv 可执行，如下所示，然后像执行其他原生 Linux 命令一样执行它：

```
# chmod +x myenv
```

这开启了 myenv 的可执行权限。在你执行 myenv 之前，需要确保另一件事——它必须在搜索路径中。你可以通过执行以下命令获取搜索路径：

```
# echo $PATH
```

如果包含 myenv 文件的目录不在当前搜索路径中，你必须将目录名称添加到搜索路径中。

现在，你可以像 Linux 命令一样从命令行执行文件 myenv：

```
# myenv
```

### 注意
你的 shell 程序的第一行应以井号 (#) 开头，这告诉 shell 该行是注释。在井号后面，你必须有一个感叹号 (!)，这告诉 shell 运行感叹号后面的命令，并使用文件的其余部分作为该命令的输入。这是所有 shell 脚本编程的通用做法。例如，如果你为 bash 编写了一个 shell 脚本，你的脚本第一行将包含 #!/bin/bash。

