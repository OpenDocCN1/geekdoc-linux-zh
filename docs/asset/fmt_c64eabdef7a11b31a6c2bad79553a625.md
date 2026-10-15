
注意，在某些平台（如 IBM PowerPC）上，即使 Linux 平台是 64 位的，`gcc` 编译器也会产生 32 位对象文件。32 位和 64 位编译环境的数据类型模型是不同的。32 位应用程序的 C 数据类型模型是 IL32 模型。`int` (I) 和 `long` (L) 以及指针 (P) 的字母表示这些数据类型都是 32 位类型。64 位的数据类型模型是 LP64 模型。除了 `int` 之外，`long` (L) 和指针 (P) 都会增长到 64 位。其余的整数类型和浮点类型也是如此。

### 3.12.2 最佳实践

将 32 位应用程序移植到 64 位应用程序的最佳实践方法建议分两个阶段进行。第一阶段是将应用程序移植从其当前运行的原生平台（AIX、Solaris 或 HP-UX）到 Linux。第二阶段是将移植后的 32 位应用程序迁移到 Linux 上的 64 位应用程序。

## 3.13 总结

分析应用程序是在实际移植步骤之前可以做的最重要的工作。如果极其仔细，它可以发现隐藏的陷阱，有助于完善整个项目计划。在某些情况下，应用程序可能使用了 Linux 尚未支持的平台特定功能。在这种情况下，移植人员必须寻找变通方案或等效方法。

## 3.13 总结

Linux 的功能。幸运的是，如今的 Linux 版本支持最常用的 API 标准，例如 POSIX 线程、大页（large pages）、异步 I/O、消息队列、64 位架构等。为源平台的原始功能寻找等效功能比以往任何时候都要简单。

以下是本章讨论的一些重要亮点：

- 文档《ISO/IEC 9945 (POSIX) 与 Linux 标准基础 (LSB) 冲突》详细阐述了对 Linux 标准的支持。
- Linux 支持三种库版本控制方法：内部、外部和符号版本控制。
- 通过原生 POSIX 线程库，Linux 现在支持更完整的 POSIX 线程实现，这使得多线程应用程序迁移到 Linux 更加容易。
- Linux 为使用 UNIX 平台大页支持的应用程序提供了大页支持。
- 字节序（endianness）等环境因素会根据具体情况影响这些待迁移的应用程序。只有当应用程序具有特定的例程，且这些程序在从与目标 Linux 平台架构不同的平台迁移时可能会影响，字节序才是一个考虑因素。
- 32 位到 64 位的应用程序迁移应被视为完全独立的迁移。如果待迁移的应用程序是 32 位程序，而迁移要求其在 Linux 上作为 64 位程序运行，请将它们视为两个独立的迁移项目——第一个是将 32 位应用程序迁移到 Linux，第二个是将已迁移的 32 位应用程序迁移到 Linux 64 位应用程序。

虽然本章概述了 Linux 2.6 提供的通用功能，但针对 Solaris、AIX 和 HP-UX 的迁移章节通过引用 Linux 与这些 UNIX 平台之间的差异和相似之处，更详细地讨论了这些技术特性。接下来是迁移章节。

## 第 4 章

![](img/b57bac67945e9ea199cd38621fd44ff2_126_0.png)

### 本章内容

- 4.1 准备工作 第 97 页
- 4.2 一般差异 第 100 页
- 4.3 编译器 第 104 页
- 4.4 链接器 第 137 页
- 4.5 将 Shell 脚本迁移到 Linux 第 146 页
- 4.6 国际化与本地化 第 147 页
- 4.7 Make 第 148 页
- 4.8 调试器 第 154 页
- 4.9 线程 第 155 页
- 4.10 信号 第 169 页
- 4.11 系统调用 第 179 页
- 4.12 系统库 第 186 页
- 4.13 Solaris 和 Linux API 第 187 页
- 4.14 科学库 第 199 页
- 4.15 大页支持 第 200 页
- 4.16 某些 Solaris 不可编程实践 第 200 页
- 4.17 总结 第 201 页

迁移是流程过程中对应用程序进行修改的步骤。在此阶段，应用程序大部分（如果不是全部）的技术方面和依赖关系已经在范围界定和分析步骤中揭示。现在唯一需要做的是修改源代码，使其在 Linux 平台上编译并运行。

在迁移过程中，软件开发人员和迁移人员可能会遇到他们熟悉的 UNIX 操作系统与 Linux 2.6 平台之间的若干差异。对于本章讨论的每个主题，将介绍最常见的差异，以解释哪些在 Linux 2.6 环境中有效，哪些无效。本章描述的 Solaris 环境主要基于版本 10，但也适用于较旧版本的 Solaris。尽管本章详细讨论了某些 Solaris 主题，但假设阅读本章的迁移工程师已经具有 Solaris 上的软件开发经验。

## 4.1 准备工作

在开始迁移工作之前，我们需要准备好工作环境。其中，我们还需要建立迁移、构建和代码系统。以下是包含每项工作详细任务的清单。

### 4.1.1 设置迁移系统

迁移系统供迁移工程师用于执行迁移工作。它包含了运行待迁移应用程序预期的 Linux 版本的迁移服务器。在某些情况下，服务器可以用于运行不影响整体性能的单元测试。以下是设置迁移系统的任务列表。

- 1. 安装带有待迁移应用程序所需 Linux 发行版的服务器。设置所有必要的家目录和构建环境目录。
- 2. 检查需要安装在服务器上的的任何已知补丁。
- 3. 确保安装包含编译器和调试器。
- 4. 安装应用程序所需的第三方产品和许可证。安装这些产品所需的任何先决条件或补丁。
- 5. 在构建服务器上为用户和系统管理员设置访问。
- 6. 使用迁移环境作为测试机设置策略。这些策略必须包括在迁移服务器上可以测试和不可以测试的内容。

取决于不同小组之间的工作划分情况，在由独立小组设置服务器的情况下，迁移工程师仍需要提供环境规范。

### 4.1.2 设置代码管理系统

代码管理系统由一个管理应用程序更改的工具组成。最常用的工具是 CVS，但其他工具如 Subversion¹ 和 Arch² 也日益流行。以下是设置变更管理系统的任务：

- 1. 安装管理工具。
- 2. 安装方便迁移工程师使用工具的脚本。
- 3. 确保存在易于获取的 HOWTO 和常见问题解答。这些文档应包含如何使用工具的示例。
- 4. 将应用程序提交到代码管理系统。

在应用程序快照提交到代码管理系统后，该代码应仅用于迁移。

¹ http://subversion.tigris.org
² www.gnu.org/software/arch

### 4.1.3 设置构建系统

构建系统是执行应用程序自动化构建的地方。虽然开始迁移工作之前可能不需要，但在迁移 Makefile 之前建立它是良好的做法。该系统需要能够检出源代码并启动应用程序的每日构建。在代码足够稳定以产生最小错误的情况下每日构建是良好的做法，以确保当天提交的代码没有导致任何构建中断。如果确实发生了中断，将更容易找到原因。以下是设置构建系统的任务：

- 1. 开发可以检查应用程序代码并启动每日构建的脚本。
- 2. 在迁移 Makefile 后，测试这些脚本。做好遇到错误，因为迁移工作可能刚刚开始。
- 3. 将脚本添加到 crontab 文件中以调度每日构建。
- 4. 编写一个解析产生的错误的脚本，以便自动化报告系统通知相关人员。

## 4.2 一般差异

随着 HP-UX、Solaris、AIX 和 Linux 等主流操作系统都采纳了 ISO 和 POSIX 等标准的规定，平台间的迁移似乎应该是简单的。事实上，在应用程序编程接口（API）方面，这些操作系统有许多共同点。如果应用程序都严格按照这些标准编写，那么它们在平台间的迁移将是一项易举的任务。遗憾的是，需要迁移的应用程序通常不符合理想状况（即完全可移植）。应用程序的不可移植性不仅源于非标准 API，还源于使用了源平台提供的新的可选标准，而目标平台尚未实现这些标准。有时，对标准的解释可能会不同，因为某些标准留下了解释空间，导致了不同的实现方式。

## 4.2 通用差异

当厂商在标准处于草案阶段时在其平台上实现标准时，这种情况经常发生。这导致编写或编译应用程序时使用的是草案标准。这看起来无害的，因为应用程序在编写和构建的源平台上可以正常编译和运行，但生成的应用程序并不具有移植性。

在本节，我们将讨论 Solaris 和 Linux 之间的差异和相似之处。

### 4.2.1 C语言

Sun 的 C 编译器在 Solaris 10 更早的操作系统上支持 ISO/IEC 9899:1999 (C99) 指定的大多数语言特性。然而，在 Solaris 10 中，编译器完全符合 C99 标准。GCC 完全支持两个版本的 C 标准：C90 和 1995 年发布的 1990 年标准的修订版（称为 C99）。对 C99 的支持尚未完成。欲需更多细节，请访问 http://gcc.gnu.org/c99status.html。默认情况下，GCC 符合 C99 标准加上 GNU 扩展（包括一些 C99 特性）。要在 GCC 中选择 C90，请使用选项之一 `-ansi`、`-std=iso9899:1990`。要在 GCC 中选择 C95，请使用选项 `-std=iso9899:199409`。要选择 C99，请使用选项 `-std=iso9899:1999`。

### 4.2.2 C++语言

Sun 最新的 C++ 编译器支持 1998 ISO C++ 国际标准，ISO IS14882:1998。对于 Linux，`g++` 是一个调用 GCC 的程序，默认语言设置为 C++，并自动指定链接到 C++ 库。GNU `g++` 严格符合 1998 ISO/ANSI C++ 标准。

Sun 的编译器随带了基于 RogueWave 标准 C++ 库第2 版的 C++ 标准库以及 Tools.h++ 7.0 版。另一方面，GNU `g++` 带有运行时库 `libstdc++`。

### 4.2.3 GNU C/C++语言

在本文写作时，Solaris 10 目前已可用 GCC 3.4.2 版本（www.sun.com/software/solaris/freeware）。如果你的应用程序可以在 Solaris 上使用 GCC 构建，那么它极有可能在 Linux 上同样可行。请注意，不同版本的 GCC 有时符合不同的语言规范，特别是 C++ 标准。因此，使用不同版本的 GCC 重新编译可能不会成功。

### 4.2.4 Java语言

从 Blackdown Java SDK (www.blackdown.org) 可以提供了 Linux 环境。在本文写作时，Blackdown 已发布 Java 1.4.2 版本，并正在开发 1.5 发布版本。其他 Linux Java SDK 实现也可以从 Sun 和 IBM 网站下载。有关 Linux 中 Java 环境的更多信息，请参阅第 2 章“范围（Scoping）”。

### 4.2.5 线程

Solaris 支持两种线程接口：POSIX 线程（通常称为 pthreads）和 Solaris 线程。现代 Linux 发行版支持 POSIX 线程 API 标准。如果你使用 Solaris，在将其移植到 Linux 时，必须更改应用程序。或者，你可以使用 Solaris 兼容线程库 (STL) 从 Solaris 线程 API 迁移到 POSIX 线程库。欲需 STL 的更多信息，请访问 http://sourceforge.net/projects/sctl/

### 4.2.6 标准比较

几乎所有的 Linux 发行版都认可标准化和移植性提供的价值，并与各种 Linux 实现者/维护者合作以满足这些标准。主要的 Linux 标准基础 (LSB) 是由自由标准组织 (FSG) 监督的项目。LSB（目前其最新版本为 LSB 3.0）高度基于 IEEE POSIX 和 Open Group Single Unix (SUS) 标准，但它也记录了 Linux 不兼容 UNIX 或 POSIX 的地方。大多数主要的 Linux 发行版都已通过了 LSB 认证。

LSB 除了提供源代码 API 规范外，还为几种常见的 Linux 硬件平台的每个提供了二进制接口 (ABI) 规范。ABI 的目标是确保该硬件平台上不同 Linux 发行版之间的二进制移植性（对于 LSB 可移植的应用程序）。发行商必须通过 ABI 以及 API 的认证。ISV 还可以使用 FSG 提供的工具将其应用程序认证为“LSB 可移植”。

尽管 Linux 内部存在标准化，但 Linux 本身并未完全符合 IEEE POSIX 或 Open Group SUS 规范³。这意味着在这些通用商业 UNIX 标准下可能完全移植的应用程序，为了成功迁移到 Linux 可能仍需要一些工作。然而，对于完全不符合任何标准或使用 Solaris 特有 UNIX 扩展的应用程序来说，这项工作将少得多。

表 4-1 提供了基于 LSB 规范版本 2.0.1 的 Solaris 10 与 Linux 支持的标准的符合性对比。

表 4-1
Solaris 和 Linux 标准

| 标准 | Solaris 10⁴ | Linux 2.6 (GNU libc)⁵ |
| :--- | :--- | :--- |
| ISO/IEC 9945-1:2001, POSIX 系统 API (POSIX.1) | 是（包括许多实时扩展(选项)） | 部分（在某些 API 和一些实时扩展上存在细微差异） |
| ISO/IEC 9945-2:2001, POSIX 系统 API (POSIX.1) | 是 | 部分 |
| X/Open 移植性指南 3 (XPG3) | 是 | 部分 |
| X/Open 移植性指南 4 (XPG4) | 是 | 是 |
| X/Open 移植性指南 4 版本 2 (XPG42) | 是 | 是 |
| System V 定义 (SVID) | 是 | 是 |
| 64位模型 | 是 | 是 |

# 第 4 章 • 迁移 Solaris

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -flteval=[any|2}] | -mfpmath=unit (特定于 i386 和 x86-64) | 控制浮点表达式的求值方式。 |
| -fnonstd | N/A | -fns 和 -ftrap 的宏。 |
| -fns={no|yes} | N/A | 开启 -SPARC 非标准浮点模式。 |
| -fprecision=p | -fsingle-precision-constant | 将浮点控制字（Control Word）中的舍入精度模式位初始化为单精度、双精度或扩展精度。GCC 没有直接对应的等效选项，但 -fsingle-precision-constant 强制编译器将浮点常量视为单精度，而不是将其转换为双精度。 |
| -round=r | -frounding-math | 设置 IEEE 754 舍入模式。默认的 IEEE 模式是舍入最近值。Linux上的情况也是如此，但没有选择该模式的选项。在 GCC 中考虑使用 -frounding-math。 |
| -fsimple=[n] | N/A | 优化器对浮点算术做出简化假设。GCC 没有完全匹配的选项。对于不符合 IEEE 或 ISO 的浮点优化，考虑这些标志：-ffloat-store, -ffast-math, -fno-math-error, -funsafe-math-optimizations, -ffinite-math-only, -fno-trapping-math。 |
| -fsingle | -fsingle-precision-constant | 强制编译器以单精度而非双精度对 float 表达式求值。 |
| -fstore | -ffloat-store | 使浮点变量不存储在寄存器中。 |

## 4.3 编译器

| Sun Studio 10 | GNU GCC 3.4.2 | | |
|---|---|---|
| -ftrap=t[... | -...] | 设置启动时生效的 IEEE 陷阱模式，但不安装 SIGFPE 处理器。GCC 没有直接对应的等效选项，但 -fno-trapping-math 会禁用所有用户可见的陷阱，包括除以 0、溢出、下溢、不精确结果和无效操作。 |
| -G | -shared | 生成共享对象而非动态链接的可执行文件。 |
| -g | -g | 生成调试所需的额外符号表信息。 |
| -H | -H | 向标准错误打印编译期间包含的每个文件的路径。 |
| -hname | -hname, -Wl,-somename | 为共享动态库指定名称，以便拥有不同版本的库。 |
| -I[-|dir] | -I[-|dir] | 将 dir 添加到搜索 #include 文件的目录列表中。 |
| -i | N/A | 将选项传递给链接器以忽略任何 LD_LIBRARY_PATH 或 LD_LIBRARY_PATH64 设置。 |
| -KP | -fPIC | 生成用于共享库的位置无关代码（大模型）。 |
| -Kpic | -fpic | 与 -fPIC 相同，但在 SPARC 上将全局偏移表的大小限制为 8K，在 m68k 和 PPC (32,64) 上限制为 32K。386 上不存在此限制。为基于 IBM PowerPC 的架构生成的代码始终是位置无关的。 |
| -keeptmp | -save-temps | 保留编译期间创建的临时文件而不是自动删除。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -Ldir | -Ldir | 将目录 *dir* 添加到 ld 搜索存档库的目录列表中。按照命令行上指定的顺序对目录进行搜索。 |
| -lname | -lname | 将存档文件 *name* 添加到链接文件列表中。ld 会在搜索扩展名为 .a 的库之前，先在目录中搜索扩展名为 .so 的库。链接器将在命令行指定的 location仅搜索一次存档。出现在命令行后后位置的对象文件中的未定义符号不会导致链接器再次搜索该存档。 |
| -mc | N/A | 移除对象文件中 .comment 部分中的重复字符串。 |
| -misalign | Implicit | 已过时。查看 -xmalign=1i。对于 IA-32，此选项是不必要的，因为处理器会自动处理对齐。 |
| -misalign2 | Implicit | 已过时。查看 -xmalign=2i。对于 IA-32，此选项是不必要的，因为处理器会自动处理对齐。 |
| -mr[,string] | N/A | 移除 .comment 部分中的所有字符串。 |
| -mt | -pthread -D_REENTANT | 宏选项，展开为 -D_REENTR-thread。在 Linux 上，pthread 增加了对 pthread 库多线程的支持。 |
| -native | -mcpu=cpu_type | -target=native 的同义词。生成在主机系统性能最好的代码。GCC 没有直接对应的等效选项，但你可以使用 -mcpu 指定你主机系统的类型。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -nofstore | Implicit | 效果与 -fstore 相反。GCC 有选项 -ffloat-store。 |
| -O | -O3 | 使用默认优化级别。 |
| -o filename | -o filename | 指定输出文件名。 |
| -P | -E | 仅通过预处理器运行源文件。 |
| -q | -p | 使编译器以单精度而非双精度对 float 表达式求值。 |
| -Rdir[:dir] | -wl,-rpath | 将冒号分隔的目录列表传递给链接器。 |
| -s | -s | 从二进制文件中删除所有符号。 |
| -S | -S | 生成源文件的汇编代码。 |
| -U | -U | 取消宏定义。 |
| -V | -v | 打印名称和版本。 |
| -v | -v | 打印名称和版本。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| - | 控制编译器识别 C99 实现的功能。 |
| -xcache=[c] | N/A | 定义供优化使用的缓存属性。 |
| -xchar=[o] | -fsigned-char | 将 char 类型视为符号或无符号。 |
| -xchar_byte_order=[o] | N/A | 通过指定的字节顺序放置多字节字符常量来生成整数常量。 |
| -xcheck=[o] | N/A | 添加堆栈溢出的运行时检查。 |
| -xchip=[c] | -march | 指定优化器使用的目标处理器。 |
| -xcode=[v] | N/A | 指定代码地址空间。GCC 中没有完全匹配的选项。然而 -xcode=pic13 等于 -fpic，-xcode=pic32 等于 -fPIC。 |
| -xcrossfile=[n] | -junit-at-a-time | 启用跨源文件的优化和内联。 |
| -xcsi | N/A | 允许 C 编译器接受不符合 ISO C 源代码字符要求的本地位置源码。 |

# 第 4 章 • 迁移 Solaris

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -xexplicitpar | N/A | 根据 #pragma MP 指令规范生成并行代码。 |
| -xF | -freorder-functions, -freorder-blocks, -freorder-blocks -and-partition | 链接器对函数和变量进行优化重排序。 |
| -xhelp=f | --help -v | 显示在线帮助信息。 |
| -xhwcprof | N/A | 启用编译器对基于硬件计数器的剖析的支持。 |
| -xildoff | N/A | 开启增量链接器并强制使用 ld。 |
| -xildon | N/A | 开启增量链接器并强制在增量模式下使用 ild。 |
| -xinline=list | N/A | 尝试仅内联可选列表中指定的函数。 |
| -xipo={a} | -funit-at-a-time | 使用 -xipo=1 时，编译器跨所有源文件执行内联。使用 -xipo=2 时，编译器执行过程间别名分析以及内存分配和布局优化，以提高缓存性能。 |
| -xipo-archive | N/A | 允许编译器在生成可执行文件之前，对传递给链接器的由 -xipo 编译且存储在存档库 (a) 中的对象文件进行优化。 |
| -xjobs=n | N/A | 设置编译器为完成工作所创建的进程数。 |
| -xldscope={v} | N/A | 更改 extern 符号定义的默认链接器作用域。 |
| -xlibmieee | N/A | 在异常情况下强制数学函数例程返回 IEEE 754 风格的返回值。 |

## 4.3 编译器

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -xlibmil | N/A | 内联某些库例程以加快执行速度。 |
| -xlibmopt | N/A | 启用编译器使用优化过的数学例程库。 |
| -xlic_lib=superf | N/A | 链接 Sun 提供的性能库。 |
| -xlicinfo | N/A | 返回有关许可系统的信息。 |
| -xlinkopt[=level] | N/A | 指示编译器对可重定位对象文件进行链接时优化。 |
| -xloopinfo | N/A | 显示并行化循环的信息。 |
| -xM | -M | 显示可能的依赖关系。 |
| -xMl | (-MM) | 显示类似于 -xM 的依赖关系，但排除 /usr/include 文件。-MM 选项对 GCC 有类似作用，但 GCC 会避免对系统目录文件或直接/间接包含此类头文件的生成依赖。 |
| -xMerge | N/A | 将数据段合并为段。 |
| -xmaxopt=[v] | N/A | 将 pragma opt 的级别限制为指定的级别。 |
| -xmemalign=ab | N/A | 指定最大假设内存对齐以及未对齐数据访问的行为。GCC 没有完全匹配的选项，但针对各种支持的平台提供了多个关于内存对齐的选项。对于 i386 和 x86-64，例如 GCC 提供了 -align-double, -m96bit-long-double, m128bit-long-double, mpreferred-stack-boundary=num。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
|--- |--- |--- |
| -xnativeconnect | N/A | 允许共享库与 Java 代码建立接口。 |
| -xnolib | -nostdlib | 默认不链接任何库。 |
| -xnolibmil | N/A | 不内联数学库例程。GCC 没有完全匹配的选项，但有 -fno-default-inline 和 -fno-inline。 |
| -xnolibmopt | N/A | 防止编译器使用优化过的数学库。 |
| -xO[1|2|3|4|5] | -01,-02,-03 | 选择优化级别。GCC 没有第四和第五优化级别。 |
| -xopenmp=[i] | N/A |  Open OpenMP 指令启用显式并行化。GNU C、C++ 和 FORTRAN 编译器的 OpenMP 实现正在开发中。 |
| -xP | N/A | 为所有 K&R C 函数打印原型。 |
| -xpagesize=n | N/A | 设置栈和堆的优选页大小。 |
| -xpagesize_heap=n | N/A | 设置内存中堆的页大小。 |
| -xpagesize_stack=n | N/A | 设置内存中栈的页大小。 |
| -xparallel | N/A | 等于 -xautopar,-xdepend,-explicitpar 的宏。 |
| -xpch=v | Default | 激活预编译头文件功能。要使用 GCC 创建预编译头文件，只需像编译其他文件一样编译它。GCC 将搜索以 .gch 结尾的预编译头文件。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -xpchstop=[file/<include>] | N/A | 停止查找预编译头文件的位置。 |
| -xpentium | -mtune=cpu | 针对 Pentium 处理器生成代码。 |
| -xpg | -pg | 为 gprof 收集数据。 |
| -prefetch=[val] | N/A | 为支持预取的架构启用指令。 |
| -prefetch_auto_type=a | N/A | 控制自动预取的激进程度。 |
| -prefetch_level=1 | N/A | 使用 -prefetch-auto 决定预取频率。 |
| -xprofile=collect | -fprofile | 收集并保存执行频率数据以供后续剖析使用。 |
| -xprofile=use | -fprofile-use | 使用执行频率数据。 |
| -xprofile=tcov | -fcoverage | 为 tcov 生成剖析信息。 |
| -xprofile_map | N/A | 指定生成 profile 文件的映射路径。 |
| -xreduction | N/A | 在并行化期间处理归约。 |
| -xregs=r, ...] | -freg | 指定寄存器的使用。 |

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
| --- | --- | --- |
| -restrict=[o] | N/A | 将指针参数视为受限指针。GCC 识别 restrict 关键字。 |
| -xs | N/A | 允许 dbx 调试。 |
| -xsafe=mem | N/A | 这种功能在 i386 处理器上提供。 |
| -xsb | N/A | 为源码创建额外的符号信息。 |
| -xsbfast | N/A | 为源码创建数据库。 |
| -xsfpconst | -fshort-double | 将浮点常量表示为单精度。GCC 没有完全匹配，但 -fshort-double 使双精度相同。 |
| -xspace | -Os | 优化代码大小的并行化。 |
| -xstrconst | Default | 将字符串字量插入文本段的只读数据段而不是默认数据段。GCC 的默认行为是 -fwritable-strings。 |
| -xtarget=t | -march=cpu | 指定目标指令集和优化。 |
| | -mtune=cpu | |
| -xtemp=dir | N/A | 设置编译器使用的临时目录。GCC 使用环境变量 TMPDIR 设置临时目录。 |

# 第4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 | GNU GCC 3.4.2 | 说明 |
|---|---|--|
| -YI, dir | -Idir | 更改搜索包含文件的默认目录。 |
| -YP, dir | -Ldir | 更改查找文件的默认目录。 |
| -YS, dir | -B | 更改启动对象文件的默认目录。 |
| -Z11 | N/A | 为 lock_lint 创建程序数据库，但不生成可执行代码。 |

## 4.3.3 C++ 编译器选项

表 4-3 对比了 Sun Studio 10 的 C++ 选项与 G++ 3.4.2 的 C++ 选项。

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
|---|---|--|
| -386 | -march=i386 | 与 -xtarget=386 相同。 |
| -486 | -march=i486 | 与 -xtarget=486 相同。 |
| -a | N/A | 与 -xa 相同。 |
| -Bbinding | -Wl,-Bstatic -Wl,-dn -Wl,-non-shared | 指定链接时的库绑定是符号的、动态（共享）还是静态的（非共享）。 |
| -cg{89|92} | N/A | 与 -xcg{89|92} 相同。 |
| -compat[{4|5}] | N/A | 设置编译器的主版本兼容模式。 |
| +d | -fno-default-inline | 防止展开 C++ 内联函数。 |

> 除非另有说明，否则此描述基于 Sun Studio 10 C++ 用户指南。

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
| --- | --- | --- |
| -d(y|n) | -Wl,-Bstatic -Wl,-static | 指定动态链接（默认）或静态链接。 |
| -dalign | 有多种对齐选项可用；请参考 GNU GCC 手册。⁸ | 控制编译器对数据对齐的假设。 |
| -dryrun | ### | 打印传递的选项但不进行编译。 |
| +e(0|1) | N/A | 控制虚表生成。 |
| -erroff[=t] | 查看 GNU GCC 中的 -W 选项以请求或抑制警告。 | 抑制 C++ 编译器警告信息，且对错误没有影响。 |
| -errrtags[=a] | 查看 GNU GCC 中的 -W 选项以请求或抑制警告。 | 为 C++ 编译器前端每个可以抑制的警告消息显示消息标签。 |
| -errwarn[=t] | 查看 GNU GCC 中的 -pedantic 选项以请求或抑制警告。 | 使 C++ 编译器针对给定的警告消息以失败状态退出。 |
| -fast | -0x | 调整可执行文件以获得最大运行时性能的起点。 |
| -features=a [a...] | N/A | 启用/禁用逗号分隔列表列表中命名的各种 C++ 语言特性。 |
| -filt[=filter [,filter..] | N/A | 控制编译器通常应用于链接器和编译器错误消息的过滤。 |
| -flags | --help | 显示每个编译器选项的简要描述。 |

> 8 http://gcc.gnu.org/onlinedocs/

# 第4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
| --- | --- | --- |
| -fnonstd | N/A | 导致浮点溢出、除以零和无效操作异常启用硬件陷阱。 |
| -fns={yes|no} | N/A | 开启 SPARC 非标准浮点模式。 |
| -fprecision=p | -fsingle-precision -constant（见注释） | 将浮点控制字（Control Word）中的舍入精度位初始化为单精度、双精度或扩展精度。GCC 没有直接对应项，但 -fsingle-precision-constant 强制编译器将浮点常数视为单精度而不是转换为双精度。 |
| -fround=r | -frounding-math（见注释） | 设置 IEEE 754 舍入模式。默认 IEEE 模式是舍入最近值。Linux 上也是如此，但没有选择模式的选项。在 GCC 中考虑 -frounding-math。 |
| -fsimple=[n] | N/A | 允许优化器对浮点算术做出简化假设。GCC 没有精确匹配项。对于不符合 IEEE 或 ISO 的浮点优化，考虑这些标志：-ffloat-store, -ffast-math, -fno-math-error, -funsafe-math-optimizations, -finite-math-only, -fno-trapping-math。 |
| -fstore | -ffloat-store | 导致浮点变量不存储在寄存器中。 |
| -ftrap=t,[t...] | -fno-trapping-math（见注释） | 在启动时设置 IEEE 陷阱模式，但不安装 SIGFPE 处理器。GCC 没有直接对应项，但 -fno-trapping-math 禁用所有用户可见的陷阱，包括除零、溢出、下溢、不精确结果和无效操作。 |

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
|---|---|---|
| -G | -Wl,-shared | 构建动态库而非可执行文件。 |
| -g | -g | 生成调试信息，禁用内联。 |
| -g0 | N/A | 生成调试信息，不禁用内联。 |
| -H | -H | 向标准错误打印编译期间包含每个文件的路径。 |
| -h[ ]name | -hostname, -Wl,-soname, -name | 为共享库命名以具有不同的版本。 | |
| -help | --help -v | 显示在线帮助。 |
| -I- | -I- | 更改包含搜索规则。 |
| -i | N/A | 忽略任何 LD_LIBRARY_PATH 设置。 |
| -inline | N/A | 尝试仅内联指定的函数。 |
| -instances=a | -fno-implicit-templates, | 控制模板实例的放置和链接。 |
| -instlib=filename | -fno-implicit-templates, -frepo | 强制内联生成模板实例。 |
| -KP | -fPIC | 生成位置无关代码（大模型）。 |
| -pic | -fpic | 生成位置无关代码（小模型）。 |
| -keeptmp | -ftemps | 保留编译期间临时文件。 |
| -libmee | N/A | 强制 IEEE 754 返回值。 |
| -libmil | -xlib | 异常情况的 -xlib。 |

# 第4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
| --- | --- | --- |
| -library=l,... | -nostdlib（见注释） | 将指定的库链接到对象文件。 |
| -mc | N/A | 获取迁移到对象文件中的对齐信息。 |
| -misalign | (implicit)（见注释） | 迁移到旧版本的字节对齐。 |
| -migration | N/A | 编译多线程的字符串。 |
| -mt | -D_REENTANT -pthread | 编译多线程支持。 |
| -native | -march=cpu-type | 使用主机特定的代码进行优化。 |
| -noex | -fnoforce-eh-specs（见注释） | 禁用异常。 |
| -nofstore | (implicit)（见注释） | 浮点表达式的精度与 -store 含义相反。 |
| -nolib | -nostdlib | 不与系统库链接。 |
| -nolbim | -fno-default-inline | 在命令行中取消了默认的内联。 |

# 第 4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -ptv | N/A | 等于 -verbose=template。开启模板实例化详细模式。 |
| -Qoption | N/A | 将选项传递给编译阶段。 |
| -qoption | N/A | 等于 -Qoption。 |
| -qp | -p/-profile | 等于 -p。 |
| -Qproduce | -E, -c, -S | 使 CC 驱动产生产生为 sourcetype (i, .o, .s) 的输出。 |
| -qproduce | -E, -c, -S | 等于 -qproduce。 |
| -Rpathname | -Wl, -rpath | 将动态库搜索路径构建到执行文件中。此选项传递给 l.ld。 |
| -readme | N/A | 等于 -xhelp=readme。 |
| -S | -S | 编译并仅生成汇编代码。 |
| -s | -s | 从执行文件中剥除符号表。 |
| -sb | N/A | 替换为 -xsb。为源码浏览器创建额外的符号。这是 Sun 的 IDE 特有的。 |
| -sbfast | N/A | 等于 -xsfast。仅产生源码浏览器信息；不进行编译。 |
| -staticlib=[l,...] | -static (见注释) | 指定哪些 C++ 库要静态链接。g++ 中没有完全匹配的项，但有 -static，它等同于 -staticlib=all。 |
| -sync_stdio=[yes|no] | N/A | 开启/关闭 iostreams 和 stdio 之间的同步。 |
| -temp-path | -save-temps | 定义临时文件的目录。 |
| -template-opt=[opt,...] | N/A (见注释) | 启用/禁用各种模板选项。g++ 中没有完全匹配的项，但有 -frepo, -fno-implicit-templates。 |

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -time | -Q, -ftime-report | 报告每个编译组件消耗的时间和资源。 |
| -U | -U | 删除预处理器符号名称的初始定义。 |
| -unroll=n | -funroll-loops (见注释) | 等于 -xroll=n。展开 n 个循环。g++ 没有完全匹配的项，但有 -ffunroll-loops。 |
| -V | --version | 等于 -verbose-version。打印名称和版本号。 |
| -v | -v | 等于 -verbose-diags。打印每次编译的命令行。 |
| -vdelx | N/A | 生成对 _vector_delex 的调用而非 _vector_delete_。此选项已弃用。 |
| -verbose=v[v...] | --version, -v | 控制输出的详细程度。g++ 没有完全匹配的项，但 -v 和 --version 部分提供了相同的功能。 |
| +w | -Wabi, -Wctor-dtor-privacy, -Whon-virtual-dtor | 识别可能产生意想不到后果的代码。g++ 专门为 C++ 提供了各种警告选项。 |
| +w2 | 见注释 | 产生带有 +w 且降低可移植性的技术违规的警告。请查看 g++ 中 +w 的注释。 |
| -w | -w | 抑制大多数警告信息。 |
| -Xm | N/A | 等于 -features=dollar。允许将 $ 符号作为非初始标识符。 |
| -xa | -fprofile-arcs -ftestest-coverage | 输出 tcov 工具的信息。在 Linux 上，使用 GNU 版本的 gcov 处理输出。 |

# 第 4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -xalias_level=[n] | N/A | 编译器使用此选项来确定可以进行哪些假设以执行基于类型的别名分析的优化。 |
| -xar | N/A | 创建归档库。 |
| -xarch=isa | -march=isa | 指定目标指令集架构。 |
| -xautopar | N/A | 开启多处理器的自动并行化。 |
| -xbuiltin=[%all | %none] | N/A | 在性能有利时替换内联函数或内联系统函数。 |
| -xcache=c | N/A | 定义优化器使用的缓存属性。 |
| -xcg89 | N/A | 等于 -xtarget=ss2。 |
| -xcg92 | N/A | 等于 -xtarget=ss1000。 |
| -xchar=[o] | -fsigned-char or -fsigned-char | 将 char 类型视为有符号或无符号。 |
| -xcheck=[i] | N/A | 为栈溢出添加运行时检查。 |
| -xchip=c | -march | 指定优化器使用的目标处理器。 |
| -xcode=a | N/A | 指定代码地址空间。GCC 中没有完全匹配的项。然而，-xcode=pic13 等于 -fpic。 |
| -xcrossfile=[n] | -finline-at-time | 启用跨文件的优化和内联。 |
| -xdepend=[yes|no] | -loop-optimize, -falign-loops | 分析循环的迭代间依赖和重构。 |
| -xdumpMacros=[value,value...] | -g, -D | 提供宏定义和使用实例等信息。 |

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -xe | -fsyntax-only | 检查源文件的语法和语义，但不产生任何对象代码或可执行代码。 |
| -xf=[...] | N/A | 允许链接器对函数和变量进行最优重排序。 |
| -xhelp=flags | --help | 显示在线帮助。 |
| -xhelp=readme | N/A | 显示 readme 文件的内容。 |
| -xia | N/A | 链接相应的运行时库并设置浮点环境。 |
| -xildoff | N/A | 关闭增量链接器。 |
| -xildon | N/A | 开启增量链接器。 |
| -xinline=[func_spec] | N/A | 指定用户编写的程序是否可以被内联。 |
| -xipo={0|1|2} | -fprocedural-optimization | 启用跨文件的优化。执行执行过程间优化。 |
| -xjobs=n | N/A | 设置编译器完成工作的进程数。 |
| -xlang=[language] | N/A | 包含相应的运行时库并确保语言环境。 |
| -xldscope | N/A | 改变符号的作用范围。 |
| -xmie | N/A | 为特殊情况强制 IEEE 754 风格的返回值。 |
| -xlib | N/A | 优化器内联某些库。 |
| -xlibopt | N/A | 使用经过优化的数学库。 |
| -xlib=sunperf | N/A | 链接 Sun 提供的性能库。 |

# 第 4 章 • 迁移 Solaris 应用程序

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -xlicinfo | N/A | 返回许可系统的信息。 |
| -xlinkopt[=level] | N/A | 指示编译器对可重定位对象文件进行链接优化。 |
| -xM | -M | 显示 Makefile 依赖。 |
| -xMm | -MM (见注释) | 类似于 XM，但排除了来自 /usr/include 的直接或间接包含的头文件。 |
| -x | N/A | 将数据合并到文本段。 |
| -xmopt[=v] | N/A | 限制指定的 opt 级别。 |
| -xmemalign=ab | N/A | 指定假设的内存对齐和访问行为。 |
| -xnativeconnect | N/A | 启用共享库与 Java 代码。 |
| -xnolib | -nostdlib | 不链接任何默认库。 |
| -xnolilib | N/A | 不内联数学库。GCC 没有完全匹配的项，但有 -fno-default-inline 和 -fno-inline。 |
| -xnolibmpt | N/A | 防止编译器使用优化的数学库。 |
| -x0level | -01, -02, -03 | 选择优化级别。GCC 没有第四和第五级优化级别。 |

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 描述 |
| --- | --- | --- |
| -xopenmp=[i] | N/A | 使用 OpenMP 显式并行化。GNU C、C++ 和 FORTRAN 编译器的 OpenMP 实现开发中。 |
| -xpagesize=n | N/A | 设置栈和堆的页大小。 |
| -xpagesize_heap=n | N/A | 设置堆的大小。 |
| -xpagesize_stack=n | N/A | 设置栈的大小。 |
| -xpch=v | Default (见注释) | 激活预编译头文件功能。要在 GCC 中创建预编译头文件，只需像编译其他文件一样编译它即可。GCC 会搜索附加 .gch 的预编译头文件。 |
| -xpchstop=file | N/A | 指定预编译头文件有效前缀的最后一个包含文件。 |
| -xpg | -pg | 准备对象代码以供 gprof 收集数据。 |
| -xport64=[v] | N/A | 警告代码从 32 位迁移到 64 位架构时的常见问题。 |
| -xprefetch=[a,...] | N/A | 在支持预取的的架构上启用预取指令。 |
| -xprefetch_auto_type=a | | 决定是否对于 -xprefetch_level 选项指示的循环生成缩预取，方式与生成直接内存访问的预取相同。 |
| -xprefetch_level=[i] | N/A | 控制通过 -prefetch=auto 确定的自动插入预取指令的激进程度。 |

## Sun Studio 10 C++ GCC C++ 3.4.2 说明

| 选项 | 说明 |
| :--- | :--- |
| -xprofile=collect -fprofile-generate | 收集并保存执行频率数据，用于后续运行以提高性能。 |
| -xprofile=use -fprofile-use | 使用之前执行生成并保存的执行频率数据。 |
| -xprofile_ircache={path} | N/A | 在使用阶段提高编译时间。 |
| -xprofile_pathmap | N/A | 为使用 -xprofile=use 编译的对象文件定位分析数据。 |
| -xregs=r[, r ...]} -ffixed-reg -fcall-used-reg -fcall-saved-reg | 指定生成代码的寄存器用法。 |
| -xrestrict=[t] -argument-alias -argument-noalias -fargument-noalias-global | 将指针值的函数参数视为受限指针（restricted pointers）。注意 GCC 识别 ISO C99 关键字 restrict 并执行相应的优化。 |
| -xs | N/A | 允许在没有对象文件的情况下使用 dbx 进行调试。此选项会将所有调试信息拷贝到执行文件中。 |
| -xsafe=mem | N/A | 允许使用投机加载指令。i386 处理器不提供此类功能。 |
| -xsb | N/A | 为源码浏览器创建额外的符号信息。这是 Sun IDE 特有的功能。 |
| -xsbfast | N/A | 为源码浏览器创建数据库。 |
| -xspace -Os | 不对增加代码大小的循环进行优化或并行化。 |
| -xtarget=t -march=cpu-type -mtune=cpu-type | 指定指令集和优化的目标平台。 |

## 4.3 编译器

| Sun Studio 10 C++ | GCC C++ 3.4.2 | 说明 |
| :--- | :--- | :--- |
| -xthreadvar=[o] | N/A (见注释) | 控制线程局部变量的实现。GCC 使用关键字 __thread__ 支持线程本地存储。 |
| -xtime | -Q, -ftime-report | 报告每个编译组件消耗的时间和资源。 |
| -xtrigraphs [{yes|no}] | -trigraphs | 决定编译器是否识别 ISO 标准定义的三字符序列（trigraph sequences）。 |
| -xunroll=n | -funroll-loops -funroll-all-loops -flop-optimize (见注释) | 建议优化器展开 n 次。G++ 没有完全匹配的选项，但有 -funroll-all-loops,-flop-optimize。 |
| -xustr={ascii_utf16_ushort|no} | -fexeccec-charset=s -fwide-exec-charset=s -finput-charset=s | 支持使用 ISO10646 字符串字量的国际化应用。 |
| -xvector [{yes|no}] | -multivec (见注释) | 自动生成调用向量库函数。在 PowerPC 平台上，GCC 通过 -multivecget支持 Altive 指令集。 |
| -xvis[{yes|no}] | N/A | 启用 VIS 指令集软件开发包中定义的汇语言模板。这是 Sun 的特定功能。 |
| -xwe | -pedantic-errors | 将警告转换为错误。 |
| -Yc,path | N/A | 指定组件 c 所在的新目录 dir。c 可以由 -W 选项下列出的代表组件的任意字符组成。 |
| -z[ ]arg | -Wl, option, -Xlinker option | 链接器选项。 |

### 4.3.4 GNU g++ 中的模板实例化

根据“使用 GNU 编译器集”文档，GNU g++ 编译器提供了两种自动模板实例化方法——Borland 或 Cfront 模型。在 GNU/Linux 或 Solaris 等 ELF 系统上使用 GNU ld 2.8 或更高版本时，g++ 支持 Borland 模型。在其他系统中，g++ 不实现自动实例化方法。对于所有使用模板实例化的应用程序，最佳方法是修改代码包含模板定义，使其在一个或多个实例化点可用；通常只需在每个模板头文件的末尾添加 #include <temp_methods.c>。

示例 4-1 显示了使用此方法的示例代码。

#### 示例 4-1：GNU G++ 中的模板实例化

##### main.C
```cpp
