
## bin86
- `bin86` - (Version 0.4, 70K) 该软件包为实模式 806 指令提供了汇编器和链接器。在实模式下运行的程序（包括 LILO 和内核的引导代码）需要安装此软件包才能从源码构建。

## ctags
- `ctags` - (Version 2.0.3, 77K) 更好的 tags 为所有可能的标签类型生成标签：宏定义、枚举值（在 enum... 中）、函数和方法定义、enum/struct/union 标签、外部原型（可选）、typedef 和变量声明。它远没有包含 `#if` 预处理器条件构造的代码那么欺骗得多，因为它使用了条件路径选择算法来解决复杂的选择，并在该算法失败时使用回退算法。还可以打印源文件中发现的所选对象的列表。

## egcs
- `egcs` - (Version 1.0.2, 2,968K) 一个旨在集成高性能和稳定开发环境所需的所有优化和功能的编译器。

## egcs-c++
- `egcs-c++` - (Version 1.0.2, 1,965K) 该软件包为 GNU C 编译器增加了 C++ 支持。它包含了大多数 C++ 规范的支持，包括模板和异常处理。它不包含标准 C++ 库，该库可以单独获得。

## egcs-g77
- `egcs-g77` - (Version 1.0.2, 2,569K) 该软件包增加了用 GNU 编译器编译 Fortran 77 程序的支持。

## egcs-objc
- `egcs-objc` - (Version 1.0.2, 1,648K) 该软件包为 GNU C 编译器增加了 Objective C。Objective C 是 C 语言的一种面向对象的派生，主要用于运行 NeXTSTEP 的系统。此软件包不包含标准 Objective 类。

## expect
- `expect` - (Version 5.24, 2,297K) Expect 是一个用于自动化交互应用程序（如 telnet, ftp, passwd, fsck, login, tip 等）的工具。它让脚本控制另一个程序与其交互变得简单。

## f2c
- `f2c` - (Version 19970805, 819K) `f2c` 是 Fortran 到 C 的翻译和构建程序。它可以翻译 fortran 源码，转换为 C，然后使用 `gcc` 编译为可执行文件。

## fort77
- `fort77` - (Version 1.11a, 11K) 这是 `f2c` 的 C 翻译驱动。

## gcc
- `gcc` - (Version 2.7.3, 2,046K) GNU 编译器 - 一个功能全 ANSI 编译器，同时也支持 K&R。`GCC` 提供了许多传统上由其他工具提供的检查（如 lint），产生调试信息，并可以对结果代码进行许多不同的优化。这还包含了 C++ 和 Objective 编译器的后端。

## C.4 开发

通过 C 代码向新的系统库添加接口非常简单，这使得 Python 在自定义设置中易于使用。

此 Python 软件包包含了大多数标准 Python 模块，以及用于与 Tk 和 RPM 的 Tk 组件集接口的模块。

- `python-devel` – (Version 1.5.1, 2,878K) Python 解释器相对容易通过动态加载扩展进行扩展，并嵌入到其他程序中。此包包含了完成这两项任务所需的头文件和库。

- `python-docs` – (Version 1.5.1, 2,611K) 此包包含关于 Python 语言和解释器的文档，由纯 ASCII 和 LaTeX 源代码混合组成。

- `tcl` – (Version 8.0.2, 5,438K) TCL 是一种简单的脚本语言，设计用于嵌入到其他应用程序中。此包包含了 `tcl`，这是一个 `tcl` 应用程序的简单示例。Tcl 在编写与其紧密相关的 TK 组件集等小型图形应用程序方面非常强大。

- `tclx` – (Version 8.0.2, 1,938K) T 是一组扩展，使其更适用于 Unix 编程任务。它添加或增强了对文件、网络访问、调试、数学和列表目录的支持。它可以同时与 `tcl` 和 `tk/tcl` 使用。

- `tix` – (Version 4.1.0.6, 2,706K) T 是 Tk 组件集的一个插件，许多复杂组件是由 `tk` 块构建的。额外的组件包括选择框、文件选择器、笔记本窗口、粘贴窗口、数字旋钮控件和分级列表框。

- `tk` – (Version 8.0.2, 5,214K) Tk 是一个 Windows 组件集，设计用于与 `tcl` 脚本语言紧密配合工作。它允许你仅需比编写文本界面多花一点时间，就能编写出具有全功能 GUI 的简单程序。Tcl/Tk 应用程序可以在 Windows 和 Macintosh 平台上运行。

- `tkinter` – (Version 1.5.1, 639K) 一个基于 Tcl/Tk 的 Python 图形界面，被许多配置工具使用。

- `umb-scheme` – (Version 3.2, 1,122K) UMB Scheme 是《IEEE Scheme 编程语言标准》（1990年12月）中描述语言的实现。

- `xlispat` – (Version 3.50, 2,751K) 一种用于 X-Windows 的 Lisp 编程语言实现，带有用于高级统计计算的扩展。

## C.4.4 库

本节包含各种库的软件包。某些库是系统正常运行必需的，而另一些库仅在你编写的程序中使用其功能时才需要。

- `cracklib` – (Version 2.7, 69K) 检查密码的安全性相关特征——长度、唯一性、是否在单词数据库中等。

- `e2fsprogs-devel` - (Version 1.10, 225K) 开发 extxt2 文件系统特定程序所需的库和头文件。

- `faces-devel` - (Version 1.6.1, 22K) 这是 xface 开发环境。它包含了用于 xface 开发的静态库和头文件。

- `gdbm-devel` - (Version 1.7.3, 70K) 这些是 `gdbm`（GNU数据库系统）的开发库和头文件。如果你计划使用 `gdbm` 数据库进行开发，则需要这些。

- `glib` - (Version 3.0, 2.047K) GIF 加载和保存共享库及工具。

- `glibc` - (Version 2.0.7, 15,304K) 包含系统中程序使用的标准库。为了节省磁盘空间和内存，通用代码保留在一个地方共享。此包包含了最重要的共享库、标准 C 库和数学库。没有它，Linux 系统将无法运行。它包含了语言（locale）数据库。

- `glibc-devel` - (Version 2.0.7, 20K) 这些库具有程序执行的调试信息。只有在对共享库进行调试时才需要。

- `glibc-devel` - (Version 2.0.7, 11,612K) 开发使用标准 C 库（几乎所有程序都使用）的程序，系统需要这些头文件来创建可执行文件。

- `gpm-devel` - (Version 1.13, 23K) 此包允许你开发利用鼠标的文本模式程序。

- `inn-devel` - (Version 1.7.2, 129K) 该库是连接到 IN，如 tint 等程序所需的。

- `libgr-devel` - (Version 2.0.13, 307K) 此包是开发处理 `libgr` 支持的各种图形格式程序所需的。

- `jpeg-devel` - (Version 6b, 228K) 此包是开发处理 jpeg 图像程序所需的，包括文档。

- `libpng-devel` - (Version 1.0.1, 227K) 使用 PNG 库开发所需的头文件和静态库。

- `libstdc++-devel` - (Version 2.8.0, 107K) 这是标准 C++ 库的 GNU 实现。此包包含了 C++ 开发所需的头文件和库。

- `libtiff-devel` – (Version 3.4, 1,372K) 此包是开发处理 tiff 图像程序所需的。

- `ncurses-devel` – (Version 4.2, 5,795K) 此包包含了开发使用 `ncurses` 程序所需的头文件和库。

- `newt-devel` – (Version 0.25, 66K) 这些是开发使用 `newt` 程序的头文件和库。Newt 是一个文本模式窗口工具包，提供了许多组件和堆叠窗口。

- `postgresql-devel` – (Version 6.3.2, 1,003K) 此包包含开发 PostgreSQL 的头文件和库。

- `python-devel` – (Version 1.5.1, 2,878K) Python 解释器相对容易通过动态加载扩展进行扩展，并嵌入到其他程序中。此包包含了完成这两项任务所需的头文件和库。

- `readline-devel` – (Version 2.2, 256K) 该库允许你读取和编辑命令行输入。

- `rpm-devel` – (Version 3.2, 1,122K) 此包包含了开发 RPM 软件包所需的头文件和库。
