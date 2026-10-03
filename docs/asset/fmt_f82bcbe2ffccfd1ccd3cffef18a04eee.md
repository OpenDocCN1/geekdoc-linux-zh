
# 配置本地构建环境

配置本地构建环境是在 Linux 上开发软件的必要步骤，这是因为 Linux 运行的目标平台非常多样。每个不同的硬件环境都可能有特定的局限性——例如，内存顺序是大端还是小端，或者对在特定目标处理器上运行的可执行文件有特殊要求——而且每个 Linux 发行版都会带有可能的软件环境——不同版本的实用程序和系统库——这些会随发布版本而变化。

由于 Linux 环境并不相似（与 UNIX 不同），有必要引入一系列工具以通用且抽象的方式处理这些差异。因此，感兴趣的第一个工具是 GNU Autoconf，它的存在以存在 `configure` 脚本为特征。当执行时，`configure` 脚本将自动确定你的系统中是否安装了必要的构建工具以及可用哪些版本，以应对任何特定要求。

尝试向 `configure` 脚本获取一些使用说明：

```bash
$ ./configure --help
configure hello_world 1.0 以适应各种系统。

Usage: ./configure [OPTION]... [VAR=VALUE].
```

输出为了简洁已进行缩减。

`configure` 程序的输出根据其配置情况列出了各种可能的选项和值。在这种情况下，大多数选项并不是必要的，因为示例中的 `configure` 脚本仅被指示判断你是否正确安装了必要的 GNU 工具链组件以供本章代码使用。后续示例（下一章中的示例）将利用 Autoconf 更强大的功能并讨论其相互关系。

通过运行包含的 `configure` 脚本来配置示例代码：

```bash
./configure
checking for gcc default... gcc
checking for C compiler default file name... a.out
checking whether the C compiler works... yes
checking whether we are cross compiling... no
checking for suffix of executables...
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ANSI C... none needed
checking for how to run the C preprocessor... -E
checking for egrep... grep -E
checking for ANSI C header files... yes
configure: creating ./config.status
```

`configure` 脚本会自动确定是否安装了必要的 GNU 工具，并通过由实际尝试编译一个极其简单的测试程序来验证它们是否正常工作。你将在书后的章节中学习更多关于编写 `configure` 脚本的知识。

你的输出可能会根据工作站的具体环境而有所不同。如果在此阶段出现任何错误，很有可能是因为你的系统中没有安装适当的工具。许多 Linux 发行版不再在安装过程中包含 GNU 工具链（GNU Toolchain），因此你可能需要安装任何缺失的工具。通常，供应商会在安装时提供一个“开发”（Development）选项，这将安装正确的工具（有关如何获取配置妥的基 Linux 系统的更多信息，请参阅“引言”）。

# 第 2 章：工具链

## 编译源码

示例源码附带的 README 文件向你概述了示例代码的目的。随后，它提到了可能存在的 `INSTALL` 文件，该文件描述了如何在你的工作站上编译和安装示例源码。与所有 Linux 软件一样，文档还解释了如何移除该软件，这在以后是不再需要的。

你可以使用以下命令编译并测试示例代码：

```bash
$ cd src
$ make
$ ./hello
Hello, World!
```

与大多数 UNIX 类系统一样，Linux 上大部分软件都在 `GNU make` 的控制下构建的。这个实用的工具读取 `Makefile` 并利用它来确定必须按什么顺序调用哪些命令，以便从给定的源代码（存储在示例源码的 `src` 子目录中）生成可运行的程序。`GNU make` 理解如何通过极少数特定指令构建大多数简单的可执行文件，尽管它并非无一不的。

`make` 调用的精确命令序列由依赖信息决定，这些信息指定在 `Makefile` 中。示例中，名为 `hello.c` 的源文件会自动编译成一个名为 `hello` 的可执行文件，然后你可以执行它。`make` 允许根据所需的操作指定不同的目标。例如，你可以使用 `make clean` 或 `make distclean` 来清理准备分发给开发者的源码。

示例 `Makefile` 包含如下的依赖规则：

```makefile
all: hello
hello: hello.c
```

不需要告诉 GNU 如何将 `hello.c` 源编译为可执行文件，因为它已经理解 C 源文件的依赖关系意味着需要相应地调用 C 编译器和其他工具。事实上，GNU 使用了默认文件扩展名，并利用这些扩展来确定各种类型源码的默认规则。

在某些情况下，`Makefile` 可能是由另一个自动化工具生成的。这通常是生成 `configure` 脚本过程的一部分，旨在产生能够广泛移植到各种类型 Linux 机器的软件。然后，`Makefile` 将自动使用 `configure` 脚本检测到的 GNU 工具，并根据配置过程中给出的任何额外选项运行，例如使用特定的交叉编译器为运行在不同于你工作站的处理器架构上的软件构建软件。

自由软件基金建议你使用自动配置工具，因为它们抽象了构建日常 Linux 应用的复杂性。因此，在构建和使用许多 Linux 应用时，你不需要了解关于源码的任何信息。更重要的是，对于那些想要从源码构建你的应用程序的人来说，情况也应该是如此。

## GNU 工具链的组件

前一节介绍了用于构建 Linux 软件的几乎通用的“configure, make”序列。正如你所见，通过恰当结合 `Autoconf` 和 `GNU make`，仅需几个命令即可从源码构建应用程序。你将在本章稍后部分发现，如何通过使用如 Eclipse 等图形开发环境来简化整个过程，将整个构建周期缩短到单次点击。

自动化是软件开发的重要组成部分，因为它简化了重复循环，并通过消除潜在的错误可能提高了可重现性。许多开发者（包括作者在内）已经学会了，要让 Linux 软件始终尽可能简单是多么困难，在浪费了数几个小时调试那些并不存在的“bug”之后，结果发现这些“bug”实际上是由于应对过于复杂的构建过程而产生的副作用。

虽然你应该始终努力使用现有的自动化工具，但仅依赖它们并不是良好的做法。对 GNU 工具链的各个部分至少有一个概述是非常重要的，以便你能处理工具无法为你提供帮助的情况。因此，本章的剩余部分将关注构建过程背后的各个工具，教你每个工具的作用以及它们如何融入整个 GNU 工具链中。

## GNU 编译器集

GNU 编译器集（以前称为 GNU C Compiler）诞生于 1987 年。GNU 项目的创始人理查·斯尔曼（Richard Stallman）想创建一个满足他最近定义的“自由软件”概念的编译器，并能够用于构建 GNU 项目的其他软件。GNU C 编译器在自由软件社区中流行起来，并在多年来因其稳健性和可移植性而闻名。它是全球范围内厂商发布的多个用于 Linux 及其他操作系统的集成开发工具的基础。

GCC 不再是一个主要供 GNU 项目用于其自身软件的小型编译器。今天，它包含了对许多不同语言的支持——包括 C 和 C++，但 Ada、Fortran、Objective C 甚至还有 Java。事实上，现代 Linux 系统可以自豪地支持除 GNU 工具直接支持的语言以外的许多种语言。Perl、Python 和 Ruby 作为脚本语言的日益兴起，以及 mono 可移植 C 实现的持续开发，在实际上已经稀释了在 Linux 上“编程”的可能含义，但那是另一个条目了。

本章重点介绍 GCC 作为编译器的用法。在 C 语言中，理解本章涵盖的概念是至关重要的，即使你并不打算在项目中使用 GCC，或者你将 GCC 用于其他目的。你应该能够学习本章涵盖的通用概念，并在文档和第三方资源的帮助下将它们应用于其他工具。

除了其广泛的语言支持外，GCC 是许多开发者的青睐，因为它已被移植到如此广泛的硬件（基于不同的架构）。标准 GCC 包括对 20 多个处理器家族的支持，包括许多工作站和服务器使用的 Intel IA32 ("x86") 和 AMD64 处理器。GCC 还支持高端 SPARC 和 POWER/PowerPC 处理器，以及日益增支持 Linux 的嵌入式处理器和其他设备。如果它是商用的，GCC 就能自豪地编译代码

## 编译单个源文件

正如你已经发现的，在 Linux 上构建软件涉及许多协同工作的工具。GCC 是一个非常灵活且强大的现代 C 编译器，但归根结底它只是一个 C 编译器。它非常擅长解析 C 源并为特定的处理器族生成汇编代码，但由于缺乏能够目标机器的内置汇编器或链接器，它实际上无法生成可执行程序。

这种设计是有刻意的。遵循 UNIX 哲学，`gcc` 只做一件事并将其做好。GCC 支持广泛的不同目标，但它依赖外部工具来执行汇编和链接阶段，这将导致编译代码首先由汇编器转换为目标代码，然后由链接器链接到可以被特定系列 Linux 目标机器加载并执行的合适容器文件。

为了测试这一点，你可以创建一个著名的“Hello World”示例：

```c
/*
 * Professional Linux Programming - Hello World
 */

#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
    printf("Hello, World!\n");
    exit(0);
}
```

你可以使用以下命令来编译并测试这段代码：

```bash
$ gcc -o hello hello.c
$ ./hello
Hello, World!
```

默认情况下，`gcc` 驱动程序会执行将 `hello.c` 源码编译为可执行二进制文件所需的所有步骤。这包含了实际的 C 编译器（`cc`，它是 GCC 的内部组成），以及外部的 GNU 汇编器和链接器工具，这些工具将根据 GCC 编译器的输出生成可执行代码。由于历史原因，生成的可执行文件默认命名为 `.out`，但你通常会像代码所示，使用 `gcc` 的 `-o` 选项指定你自己的名称。

## 编译多个源文件

大多数应用程序都基于许多独立的源文件，这些文件被单独编译，然后链接在一起形成最终的可执行文件。这简化了开发工作，允许不同的团队处理项目的不同部分，同时鼓励了代码重用。在本书的后后的部分，你将学习 Linux 内核是如何由数百个独立的源文件组成的，以及图形化 GNOME 桌面应用程序是如何从许多组件构建的——目前，我们将通过将两个源文件编译成一个程序来实现。

`gcc` 驱动程序不仅理解如何将单个源文件编译为可执行程序，还能通过代表你适当调用 GNU 链接器将多个不同的对象文件链接在一起。当给定多个对象文件（`.o`）作为输入参数时，GCC 会自动执行此操作，生成单个可执行输出。为了测试这一点，你可以从两个单独的源文件创建一个程序，它们将被链接成一个可执行文件。

从一个包含简单消息打印函数的单 `message.c` 开始：

```c
#include <stdio.h>

void goodbye_world(void)
{
    printf("Goodbye, World!\n");
}
```

示例中的 `goodbye_world` 函数构成了一个简单的软件库，可以被其他源代码调用。该函数依赖标准 C 库运行时来实际执行必要的低级 IO，以便向终端打印消息。C 库将在后的链接阶段可用。由于这段代码没有形成一个完整的程序（没有 `main` 函数），如果你尝试像上一个示例那样对其进行编译和链接，GCC 将报错：

```bash
$ gcc -o goodbye message.c
/usr/lib/gcc/i686-linux-gnu/4.0.3/.../.../lib/crt1.o: in function
`_start`:sysdeps/i386/elf/start:S.115: undefined reference to `main`
collect2: ld returned 1 exit status
```

相反，必须指示 GCC 不要执行任何额外的链接阶段，并在其借助 GNU 汇编器将源文件汇编为对象代码后结束。由于在这种情况下链接器没有执行，对象文件将包含 Linux 机器加载并执行此代码作为程序所需的必要信息，但它之后会被链接到程序中。

使用 `gcc` 的 `-c` 标志来编译辅助库代码：

```bash
gcc -c message.c
```

这将指示 `gcc` 驱动程序调用其内部的 C 编译器并将输出传递给外部的 GNU 汇编器。该过程的输出是一个名为 `message.o` 的文件，它包含了适合链接到更大程序中的对象代码。

要在更大的程序中使用消息函数 `goodbye_world`，你可以创建一个简单的包装程序，其中包含一个调用 `goodbye_world` 的 `main` 函数：

```c
#include <stdlib.h>

void goodbye_world(void);

int main(int argc, char **argv)
{
    goodbye_world();
    exit(0);
}
```

该文件包含了外部消息打印函数的声明，其为一个不接受参数的 `void` 函数。正如你所知，声明是必要的，因为否则 GCC 会假设任何未声明的外部函数都是整数类型，并将其声明为该类型。这可能会在编译期间产生不必要的警告。你通常会遵循最佳实践，将这些定义存放在你的对象头文件中，正如你之前可能做过的那样。

你可以使用 GCC 编译这个包装程序：

```bash
gcc -c main.c
```

现在你有两个对象文件，命名为 `message.o` 和 `main.o`，它们包含了可以在你的 Linux 工作站上执行的对象代码。要从这些代码创建 Linux 可执行程序，你需要再次调用一次 GCC 来为你执行链接阶段：

```bash
gcc -o goodbye message.o main.o
```

GCC 识别对象代码上的 `.o` 扩展，并理解如何代表你调用外部链接器。记住，除非你在命令行上指定所需的执行文件名称，否则 GCC 默认将所有可执行文件命名为 `a.out`。成功将多个源文件编译并链接到单个可执行文件后，你可以按照正常方式执行程序：

```bash
./goodbye
Goodbye, World!
```

之前的步骤也可以简化为单个命令，因为 GCC 具有将多个源文件编译为单个可执行文件的内置知识：

```bash
gcc -o goodbye message.c main.c
./goodbye
Goodbye, World!
```

## 使用外部库

GCC 经常与包含标准例的外部软件库一起使用，这些库为运行在 Linux 上的 C 程序提供了许多功能。这是 C 语言设计的一个副作用，作为一种轻量级语言，它依赖标准化的外部库例来执行基本活动。

### 专业 Linux 编程 - 三角函数

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define MAX_INPUT 25

int main(int argc, char **argv) {
    char input[MAX_INPUT];
    double angle;

    printf("给我一个角度（弧度）=> ");
    if (!fgets(input, MAX_INPUT, stdin)) {
        perror("发生错误。\n");
    }
    angle = strtod(input, NULL);

    printf("sin(%e) = %e\n", angle, sin(angle));
    printf("cos(%e) = %e\n", angle, cos(angle));
    printf("tan(%e) = %e\n", angle, tan(angle));

    return 0;
}
```

### 共享与静态

Linux 系统上的库有两种不同的变体：共享和静态。后者是旧 UNIX 时代的遗留，在当时，所有软件库都静态链接到使用这些库例的代码上。每当应用程序针对静态链接库进行编译时，任何被引用的库例代码都会直接包含在生成的程序二进制文件中。这导致应用程序可执行文件非常大，每个文件都包含标准例的副本。

现代 Linux (UNIX) 系统在大多数情况下使用共享库方法。共享库包含与其静态对应项相同的例，但这些例并没有直接插入到每个链接它们的程序中。相反，共享库包含每个库例的单一全局版本，该版本在所有应用程序之间共享。该背后的机制非常复杂，但它们依赖于现代计算机的虚拟内存能力，允许包含库例的物理内存在多个独立的用户程序之间共享。

共享库不仅减少了 Linux 应用程序的文件大小和内存占用，还提高了系统安全性。在当今的世界，软件中新的安全漏洞每天都会被发现，而修复的速度与你更新的速度一样快。当系统库中存在问题时，大量的应用程序可能会突然变成安全噩梦。通过尽可能地使用共享库资源，你可以帮助确保你的软件处于最新状态，而无需重新构建你的应用程序——全局库更新也会自动修复你的应用程序。

使用共享库的进一步益处是，被许多不同程序同时使用的单个共享库更有可能保留在内存中，并在需要时立即可用，而不是停留在交换分区或磁盘上。这可以帮助进一步缩短某些现有大型 Linux 应用程序的加载时间。

## 示例共享库
