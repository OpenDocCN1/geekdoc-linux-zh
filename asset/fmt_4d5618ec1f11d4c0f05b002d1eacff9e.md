
- 独立的 `info`-程序：(`info-stnd`)。一个独立的 Info 阅读程序。

- `Texinfo`：(`texinfo`)。GNU 文档格式。

- `install-info`：(`texinfo`) 调用 `install-info`。更新 `info/dir` 目录项。

- `makeinfo`：(`texinfo`) 优先使用。翻译 `Texinfo` 源码。

- (...部分行已删除...)

将此列表内容与图 23-1 所示的屏幕进行比较，可以发现 `info` 仅显示在 `Ctrl++-j` 字符之后的行。在你的系统中，`/usr/share/info` 目录包含此文件以及其他文件，其中包含了每个主题的文本。通常，这些 `info` 文件以压缩格式存储。在使用 `info` 文件时，你并不需要了解这些细节。

你可以使用几个单字母命令来导航 `info` 文件。学习这些命令最好的方法是在图 23-1 所示的初始 `info` 目录中输入 `h`。在阅读帮助屏幕后，输入 `d` 返回到主题的初始目录。

从图 23-1 的目录屏幕中，输入 `m`，然后输入菜单项名称（用星号显示）。例如，要查看 GCC 的帮助，输入 `m`；然后输入 `gcc` 并按回车。随后，`info` 系统会显示 GCC 的顶层项目，如图 23-2 所示。

![](img/b418dfc0d37b54b9876d5e801170c507_747_0.png)

图 23-2：Info 窗口，显示 GCC 的顶层帮助。

你可以通过输入 `m` 后紧跟图 23-2 所示的任一菜单项来进一步探索。

## 第 23 章：Linux 中的软件开发

顺便，你可能想在图 23-2 所示的屏幕中输入 `m`，然后 `copy`，再按回车。该操作将显示 GNU 通用公共许可证 (GPL)，如图 23-3 所示。

```
www.gnu.org/software/gcc/info/ 
Edit View Terminal Go Help
File: gcc.info Node: Copying. Next: GNU Free Documentation License, Prev: G
GNU Project, Up: Top

GNU GENERAL PUBLIC LICENSE
****************

Version 2, June 1991
Copyright (C) 1989, 1991 Free Software Foundation, Inc.
59 Temple Place - Suite 330, Boston, MA 02111-1307, USA

 允许复制和分发本文档的逐字副本，但不允许对其进行修改。
Preamble
大多数软件的许可证设计旨在剥夺你共享和更改它的自由。相比之下，GNU 通用公共许可证是为了保证你共享和更改自由软件的自由——确保软件对所有用户都是免费的。此通用公共许可证适用于自由软件基金的大多数软件以及任何其他作者承诺的程序。
```

图 23-3：Info 窗口，显示 GNU 通用公共许可证 (GPL) 的第一页。

GPL 涵盖了 Linux 和 `gcc` 编译器。GPL 要求分发源代码（这就是为什么所有发行版都带有源码）。在“GNU 许可证的影响”部分中，你了解到只要这些程序只与 GNU 库链接，你仍然可以使用 GNU 工具开发商业应用程序并以二进制格式分发应用程序（无源码）。

任何时候，你可以输入 `d` 返回到图 23-1 所示的 `info` 主题目录。从该屏幕，你可以获取其他 GNU 工具的帮助，如 `make` 和 GNU 调试器。

退出请输入 `q`。如果你在 Emacs 编辑器中访问 `info`，按 `Ctrl+X` 然后按 `Ctrl+C` 退出 Emacs 编辑器。

### 运行 GNU 和 C++ 编译器

Linux 中最重要的软件开发工具是 GCC，它是 GNU C 和 C++ 编译器。事实上，GCC 可以编译三种语言：C、C++ 和 Objective-C（一种为 C 添加了面向对象扩展的语言）。你使用相同的 `gcc` 命令来编译和链接 C 和 C++ 源文件。GCC 编译器支持 ANSI 标准 C，使得将任何 ANSI 程序移植到 Linux 变得简单。此外，如果你曾在其他 UNIX 系统上用过 C 编译器，那么你会发现 GCC 非常如归。

### 运行 GCC

使用 `gcc` 命令运行 GCC。默认情况下，当你对源文件使用 `gcc` 命令时，`gcc` 会预处理、编译并链接生成可执行文件。然而，你可以使用 GCC 选项在中间阶段停止此过程。例如，你可能通过 `-c` 选项调用 `gcc` 来编译源文件并生成对象文件，但不执行链接。

使用 GCC 编译和链接几个 C 文件非常简单。假设你想编译并链接一个由两个源文件组成的程序。以下列表显示了文件 `area.c`（计算通过命令行指定半径的圆面积的主程序）：

```
#include <stdio.h>
#include <stdlib.h>

/* 函数原型 */
double area_of_circle(double r);

int main(int argc, char **argv) {
    if (argc < 2) {
        printf("Usage: %s\n", argv[0]);
        exit(1);
    } else {
        double radius = atof(argv[1]);
        double area = area_of_circle(radius);
        printf("Area of circle with radius %f = %f\n", radius, area);
    }
    return 0;
}
```

（注：此处原文代码块内容似乎不完整，已按要求保留原样不翻译）

（注：由于提供的文本中存在多处逻辑截断和重复描述，此处翻译严格遵循“不要漏掉任何行”且“不要重复输出原文”的原则，对可见文本片段进行了对应翻译。）

*(注：由于提供的原始文本在后部分出现了大量逻辑重复和截断，以下译文主要基于可见的有效信息进行。)*

# 第 23 章：Linux 中的软件开发 719

| 选项 | 含义 |
| --- | --- |
| `-o FILE` | 生成指定的输出文件（用于指定执行文件的名称） |
| `-OO` | 不进行优化 |
| `-O or -O1` | 优化生成的代码 |
| `-O2` | 进一步优化 |
| `-O3` | 执行比 `-O2` 更多的优化 |
| `-pedantic` | 如果使用了任何非 ANSI 标准扩展，则生成错误 |
| `-pg` | 在程序中添加额外代码，以便在运行时它会生成 `gprof` 程序可以使用的信息，用于显示程序各个部分的计时细节 |
| `-shared` | 生成共享对象文件（通常用于创建共享库） |
| `-UMACRO` | 取消指定的宏 (`MACRO`) |
| `-v` | 显示 GCC 的版本号 |
| `-w` | 不生成任何警告信息 |
| `-WI,OPTION` | 将 `OPTION` 字符串（包含多个用逗号分隔的选项）传递给链接器。例如，创建一个名为 `libXXX.so` 的共享库，请使用以下标志：`-WI,-soname.libXXX.so` |

### 使用 GNU make 实用

当应用程序由多个源文件组成时，通过手动输入 `gcc` 命令来编译和链接文件是不方便的。此外，你不希望在每次修改单个源文件时都编译每个文件。在这种情况下，GNU `make` 实用非常有帮助，因为 `make` 可以只编译那些真正需要编译的文件。

`make` 实用通过读取和解释 `makefile` 来工作：`makefile` 是你根据指定语法准备的文本文件。`makefile` 描述了哪些文件构了一个程序，并解释了如何编译和链接这些文件以构建程序。每当你更改一个或多个文件时，`make` 都会确定哪些文件应该重新编译，并为这些文件和项目的构建发布相应的命令。

事实上，`make` 实用程序在 POSIX.2 标准（IEEE 标准 1003.2-1992）的 shell 和工具第 6.2 节中有规定。GNU `make` 符合 POSIX.2 标准。

### 学习 Makefile 命名

默认情况下，GNU `make` 按照顺序查找名为以下之一的 `makefile`：

- `GNUmakefile`
- `makefile`
- `Makefile`

在 UNIX 系统中，将 `Makefile` 作为 `makefile` 的名称是习惯，因为它出现在目录列表的开头，那里大写名称出现在小写名称之前。

当你从互联网下载软件时，通常会发现一个 `Makefile` 与源文件在一起。要构建软件，只需在 shell 提示符处输入 `make`，`make` 就会处理构建软件的所有步骤。

如果你的 `makefile` 没有标准名称（如 `Makefile`），你必须使用 `-f` 选项来指定 `makefile` 的名称。例如，如果你的 `makefile` 称为 `webprog.mak`，你必须使用以下命令行运行 `make`：

```
make -f webprog.mak
```

GNU `make` 还接受其他几个命令行选项，这些选项在本章的“如何运行 make”部分总结。

### 理解 makefile
