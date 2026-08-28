# GLib／GTK+ 开发平台

























# 第1章

# 引言

本文是关于如何使用 C 语言上手 GLib/GTK+ 开发平台的指南。书中有时假设读者使用的是 Unix 类系统。

警告：这本“书”远未完成，你正在阅读的是 0.8 版本。如果你有任何意见，请随时通过 swilmet@gnome.org 联系我，感谢！

本书的源码位于地址：
https://github.com/swilmet/glib-gtk-book




部分章节内容基于 Havoc Pennington 于 1999 年编写的图书《GTK+/Gnome Application Development》，该书由 New Riders Publishing 出版，并根据开放出版许可（Open Publication License）授权。开放出版许可的最新版本可以在此处找到：
http://www.opencontent.org/openpub/


如果你喜欢本书，可以提供财务支持！
本指南作为自由/开源文档（Free/Libre document）发布并免费提供。它并非凭空产生，编写需要时间。通过捐赠，你可以表达对这项工作的认可，并帮助其未来的发展。

此处提供捐赠按钮：
https://people.gnome.org/-swilmet/glib-gtk-book/
感谢！

## 1.3 本书待办事项及 2019 年快速更新

- 使第 5 章（关于 GTK）更易于理解，并调整文档的其他部分以更好地整合该章节；
- GTK+ 已更名为 GTK，删除了加号。相应地调整文本；
- 不再推荐 Libuild，而是推荐 Flatpak¹ 和 Build-Stream²；
- 讨论 freedesktop.org³ 规范；
- 大多数核心 GNOME 模块现在已迁移到 Meson 编译系统（取代了 Autools）；
- 编写一个关于开发 C/GObject 库的章节；
- 讨论 Rust 编程语言。

## 1.4 什么是 GLib 和 GTK+？

简单来说，GLib 是一组库：GLib 核心、GObject 和 Gio。这三个库开发在名为 glib 的 Git 仓库中，因此当提到“GLib”时，它可以指“GLib 核心”，也可以指包括 GObject 和 Gio 在内的更集合。

GLib 为 C 语言提供了数据结构处理（链表、树、表……）、可移植性封装、事件循环、线程、模块动态加载以及实用函数。

依赖于 GLib 核心 GObject 简化了 C 语言中的面向对象编程和事件驱动编程范式。事件驱动编程不仅对图形用户界面（按键和鼠标点击等用户事件）有用，也适用于响应硬件事件（插入 USB 闪盘、连接第二个显示器、打印机电量低）或监听网络连接或其他者消息的软件。

依赖于 GLib 核心和 GObject 的 Gio 为输入输出提供了高级 API：读取本地文件、远程文件、网络流、与 D-Bus 的进程间通信等。

GLib 库可用于编写操作系统、库、命令行工具等。GLib 提供了比 POSIX 标准更高级的 API；使用 GLib 编写 C 程序更加舒适。

GTK+ 是构建在 GLib 之上的工具包，可用于开发具有图形用户界面（GUI）的应用程序。“组件”（widget）是一个 GUI 元素，例如按钮、文本、菜单等。还有一些特殊的组件被称为“容器”（containers），它们可以包含其他组件，以组装窗口中的元素。GTK+ 提供了大量的组件和容器。

¹https://flatpak.org/
²https://buildstream.build/
³https://www.freedesktop.org/

GTK+（或 GIMP Tool Kit）的第一版本主要由 Peter Mattis 于 1996 年为 GIMP（GNU Manipulation Program）编写，它迅速成为一个通用库。添加“+”是为了区分原始版本和增加了面向对象特性的新版本。GLib 起于 GTK+，但现在是一个独立的库。

GLib 和 GTK+ 的 API 使用 GTK-Doc 。源代码中写有特殊注释，GTK-Doc 提取它们并生成 HTML 页面。

尽管 GLib 和 GTK+ 是 C 语言编写的，但为 JavaScript、Python、Perl 等许多编程语言提供了语言绑定。起初，手动创建绑定，每当库的 API 更改时都需要更新。现在，语言绑定是通用的，因此在添加新函数等情况下会自动更新。这要得益于 GObject 内省（introspection）。GTK-Doc 注释中添加了特殊注解，以探索比语法能提供的更多信息，例如动态分配内容的所有权。因此，任何带有 GObject 内省的库都可以从许多编程语言中使用。此外，这些注释对 C 程序员也是很有用的，因为它是记录常用 API 的一种良好且充分的方法。

GLib 和 GTK+ 是 GNOME 项目的一部分，其总体目标是提供一个免费的桌面环境。桌面环境是一组软件应用程序，允许用户通过图形界面与计算机交互。GNOME 包含桌面面板、窗口管理器、文件管理器、文本编辑器等。GNOME 桌面设计得易于使用且高度可定制。

GNOME 桌面可在许多 Linux 发行版可用，如 Fedora、Ubuntu、Debian 等。它也适用于其他操作系统，如 Windows 和 macOS。对于想要简洁现代桌面体验的用户来说，GNOME 桌面是一个热门选择。

## 1.5 GNOME 的历史

GNOME 项目始于 1997 年，目标是为 Linux 创建一个免费开源的桌面环境。项目由包括 Jamie Vilain、Alexander Melo 和 Matthew Dexter 在内的开发者创立。早期，GNOME 是一个非常基础的桌面环境，但随着时间的推移，它变成了一个更强大、更复杂的系统。

20 00 年代，GNOME 经历了巨大的变革。项目引入了 GNOME 2。GNOME 2 变成了一个流行的桌面环境，现在仍被许多 Linux 发行版使用。2011 年，项目引入了 GNOME 3，它具有全新的界面和架构。GNOME 3 的设计更加现代且直观，并关注触控界面。2020 年，项目引入了 GNOME 40，对界面和性能进行了进一步改进。

如今，GNOME 是 Linux 世界最流行的桌面环境之一。它不断演进，定期添加新功能和改进。GNOME 项目致力于为所有人提供一个开源的桌面环境。

## 1.5 财务支持

如果你喜欢本书，可以提供财务支持！
本指南作为自由/开源文档发布并免费提供。它并非凭空产生，编写需要时间。通过捐赠，你可以表达对这项工作的认可，并帮助其未来的发展。

此处提供捐赠按钮：
https://people.gnome.org/-swilmet/glib-gtk-book/
感谢！

## 1.3 本书待办事项及 2019 年快速更新

- 使第 5 章（关于 GTK）更易于理解，并调整文档的其他部分以更好地整合该章节；
- GTK+ 已更名为 GTK，删除了加号。相应地调整文本；
- 不再推荐 Libuild，而是推荐 Flatpak¹ 和 Build-Stream²；
- 讨论 freedesktop.org³ 规范；
- 大多数核心 GNOME 模块现在已迁移到 Meson 编译系统（取代了 Autools）；
- 编写一个关于开发 C/GObject 库的章节；
- 讨论 Rust 编程语言。

## 1.4 什么是 GLib 和 GTK+？

简单来说，GLib 是一组库：GLib 核心、GObject 和 Gio。这三个库开发在名为 glib 的 Git 仓库中，因此当提到“GLib”时，它可以指“GLib 核心”，也可以指包括 GObject 和 Gio 在内的更集合。

GLib 为 C 语言提供了数据结构处理（链表、树、表……）、可移植性封装、事件循环、线程、模块动态加载以及实用函数。

依赖于 GLib 核心 GObject 简化了 C 语言中的面向对象编程和事件驱动编程范式。事件驱动编程不仅对图形用户界面（按键和鼠标点击等用户事件）有用，也适用于响应硬件事件（插入 USB 闪盘、连接第二个显示器、打印机电量低）或监听网络连接或其他者消息的软件。

依赖于 GLib 核心和 GObject 的 Gio 为输入输出提供了高级 API：读取本地文件、远程文件、网络流、与 D-Bus 的进程间通信等。

GLib 库可用于编写操作系统、库、命令行工具等。GLib 提供了比 POSIX 标准更高级的 API；使用 GLib 编写 C 程序更加舒适。

GTK+ 是构建在 GLib 之上的工具包，可用于开发具有图形用户界面（GUI）的应用程序。“组件”（widget）是一个 GUI 元素，例如按钮、文本、菜单等。还有一些特殊的组件被称为“容器”（containers），它们可以包含其他组件，以组装窗口中的元素。GTK+ 提供了大量的组件和容器。

¹https://flatpak.org/
²https://buildstream.build/
³https://www.freedesktop.org/

GTK+（或 GIMP Tool Kit）的第一版本主要由 Peter Mattis 于 1996 年为 GIMP（GNU Manipulation Program）编写，它迅速成为一个通用库。添加“+”是为了区分原始版本和增加了面向对象特性的新版本。GLib 起于 GTK+，但现在是一个独立的库。

GLib 和 GTK+ 的 API 使用 GTK-Doc 源代码中写有特殊注释，GTK-Doc 提取它们并生成 HTML 页面。

尽管 GLib 和 GTK+ 是 C 语言编写的，但为 JavaScript、Python、Perl 等许多编程语言提供了语言绑定。起初，手动创建绑定，每当库的 API 更改时都需要更新。现在，语言绑定是通用的，因此在添加新函数等情况下会自动更新。这要得益于 GObject 内省（introspection）。GTK-Doc 注释中添加了特殊注解，以探索比语法能提供的更多信息，例如动态分配内容的所有权。因此，任何带有 GObject 内省的库都可以从许多编程语言中使用。此外，这些注释对 C 程序员也是很有用的，因为它是记录常用 API 的一种良好且充分的方法。

GLib 和 GTK+ 是 GNOME 项目的一部分，其总体目标是提供一个免费的桌面环境。桌面环境是一组软件应用程序，允许用户通过图形界面与计算机交互。GNOME 包含桌面面板、窗口管理器、文件管理器、文本编辑器等。GNOME 桌面设计得易于使用且高度可定制。

GNOME 桌面可在许多 Linux 发行版可用，如 Fedora、Ubuntu、Debian 等。它也适用于其他操作系统，如 Windows 和 macOS。对于想要简洁现代桌面体验的用户来说，GNOME 桌面是一个热门选择。

GLib 库可用于编写操作系统、库、命令行工具等。GLib 提供了比 POSIX 标准更高级的 API；使用 GLib 编写 C 程序更加舒适。

GTK+ 是构建在 GLib 之上的工具包，可用于开发具有图形用户界面（GUI）的应用程序。“组件”（widget）是一个 GUI 元素，例如按钮、文本、菜单等。还有一些特殊的组件被称为“容器”（containers），它们可以包含其他组件，以组装窗口中的元素。GTK+ 提供了大量的组件和容器。

## 1.5 GNOME 的历史

GNOME 项目始于 1997 年，目标是为 Linux 创建一个免费开源的桌面环境。项目由包括 Jamie Vilain、Alexander Melo 和 Matthew Dexter 在内的开发者创立。早期，GNOME 是一个非常基础的桌面环境，但随着时间的推移，它变成了一个更强大、更复杂的系统。

20 00 年代，GNOME 经历了巨大的变革。项目引入了 GNOME 2。GNOME 2 变成了一个流行的桌面环境，现在仍被许多 Linux 发行版使用。2011 年，项目引入了 GNOME 3，它具有全新的界面和架构。GNOME 3 的设计更加现代且直观，并关注触控界面。2020 年，项目引入了 GNOME 40，对界面和性能进行了进一步改进。

如今，GNOME 是 Linux 世界最流行的桌面环境之一。它不断演进，定期添加新功能和改进。GNOME 项目致力于为所有人提供一个开源的桌面环境。

## 1.6 前提条件

本书假设你已经有一些编程实践。以下是推荐的前提条件，列出了参考书籍。

- 本文假设你已经熟悉 C 语言。参考书籍是《C 语言程序》，由 Brian Kernighan 和 Dennis Ritchie 编写 [1]。
- 学习还需要面向对象编程（OOP）。你应该熟悉继承、接口、虚方法或多态等概念。一本包含六十多条准则的好书是《Object-Oriented Design Heuristics》，由 Arthur Rust 编写 [2]。




- • 阅读关于数据结构和算法的书是有用的，但你可以并行学习它们。推荐书籍是 Steven Skiena 编写的《算法设计手册》[4]。
- • 如果你想在类 Unix 系统上开发软件，另一个前提条件是了解 Unix 的工作原理，并熟悉命令行、一些 shell 脚本以及如何编写 Makefile。一本书是 Pat Abrahams 写的《给急躁者的 UNIX》[5]。
- • 这不是强制要求的，但强烈建议使用像 Git 这样的版本控制系统。一本好书是 Scott Chacon 写的《Git》[6]。

## 1.7 为什么使用 C 语言？

GLib 和 GTK+ 库可以被 C 以外的其他编程语言使用。得益于 GObject Introspection，为各种语言提供了自动绑定。GNOME 官方绑定适用于语言：C++、JavaScript、Python 和 Vala。Vala 是一种基于 GObject 的新编程语言，它直接集成了类似于 C# 的语法。除了 GNOME 绑定外，GLib 和 GTK+ 可以在十多种编程语言中获得不同程度的支持。那么为什么以及何时选择 C 语言呢？对于在 Unix 系统上编写守护进程，C 是事实上的语言。但对于应用程序来说，它并不那么明显。为了回答这个问题，让我们先看看如何构建代码库。

### 1.7.1 将后端与前端分离

良好的做法是将用户界面与应用程序的其他部分分离开。由于多种原因，应用程序的图形界面往往是易变且不断变化的。在编写代码时计划并执行分离是理想的——你通常在你写完之后才会发现某些方面使用起来很不方便。不同的用户界面，例如命令行版本或基于 Web 的界面。

在实际操作中，这意味着任何应用程序都应该在前、接口和后端之间有彻底的分。后端应该包含所有的“硬部分”；算法和数据结构是应用程序完成的实际工作。将其视为一个被用户显示和操作的抽象“模型”（model）。

每个前端都应该是“视图”（view）和一个“控制器”（controller）。作为“视图”，前端不能忽略后端的更改，并相应地更新显示。作为“控制器”，前端必须允许用户向后端发送请求（这定义了前端的操作如何转化为更改）。

有很多方法可以约束自己以保持应用程序的独立。一些实用的想法：

> https://wiki.gnome.org/Projects/Vala

- • 将后端写成一个库。在开始，库可以是应用程序内部的并静态链接的，不需要 API/ABI 稳定性保证。当项目增长时，如果代码对其他程序有用，你可以轻松地将后端转换为共享库。
- • 从开始就至少编写两个前端；一个或两个可以是丑陋的原型，你只需要获得一个如何构建后端的想法。记住，前端应该是简单的；后端才是硬性部分。

C 语言是应用程序后端部分的良好选择。通过使用 GObject 和 GObject Introspection，你的库将适用于用各种编程语言编写的项目。另一方面，Python 或 JavaScript 库无法在其他语言中使用。对于前端来说，高级高级语言可能更方便，这取决于你已经精通哪些语言。

### 1.7.2 需要注意的其他方面

如果你对选择什么语言感到犹豫，这里有其他需要注意的方面。请注意，本文略有偏见，因为选择了 C 语言。

C 是一种静态类型语言：程序中的变量类型和函数原型在编译时都是已知的。编译器可以发现许多微小的错误，例如函数名中的拼写错误。在进行代码重构时，编译器也有极大的帮助，这对于程序的长期维护至关重要。例如，当你将一个类拆分为二时，如果使用初始代码没有更新，编译器会告诉你。通过测试驱动开发（TDD）并为所有内容编写测试，在 Python 等动态类型语言中编写大型代码库也是可行的。具有很高的覆盖率，单元测试会在重构代码时检测错误。但单元测试的执行速度比编译代码慢得多，因此测试也会影响程序的行为。所以，进行代码重构时运行所有测试并不方便。当然，编写单元测试对于 C 代码库也是良好的做法！然而，如果开发者对应用程序进行了良好的测试，编写代码 GUI 通常不是首要任务。

C 是一种显式类型语言：变量在代码中可见的。你通常不需要添加注释来解释变量的内容。了解变量的类型对于理解代码很重要，了解变量代表什么以及可以在其上调用函数。在相关问题上，self 对象显式地作为函数参数传递。因此，通过 self 指针访问属性时，你知道该属性的来源。某些面向对象的语言也为此目的使用，但它是可选的，类似于 C++ 或 Java。在后的情况下，一个实用的文本编辑器功能是进行不同的高亮。



使用了 GLib 库。GTK+ GIO 可以并行学习——一旦你开始使用 GTK+，你就会发现某些非 GUI 部分是基于 GIO 的。

因此，本书从 GLib 核心库开始（第 11 页部分），然后介绍 C 语言中的面向对象编程（第 35 页部分），最后是延伸阅读（第 66 页）。

## 1.9 开发环境

本节描述了在 Unix 系统上使用 GLib 和 GTK+ 进行编程时通常使用的环境。在 GNU/Linux 分发版上，可以通过安装单个包或包组来获取完整的开发环境，包括但不限于：

- 兼容 C89 的编译器，例如 GCC；
- GNU 调试器 GDB；
- GNU Make；
- Autotools (Autoconf, Automake 和 libtool);
- Linux 内核和 glibc 的 man页 (man-pages)

作为开发者，在使用 GLib 和 GTK+ 时，有几种解决方案：包名以以下后缀之一结尾：-devel、-dev 或 -doc。例如 Fedora、Ubuntu、Xamarin Studio、Geany 或 GNOME Builder 上的 glib2-devel 和 glib2-doc。

为了阅读 GLib 和 GTK+ 的 API 文，如果你安装了 -dev 或 -doc 包，Devhelp 是一个实用的应用程序。它们也可以在线查看：https://developer.gnome.org/glib/

# 第 2 章 GLib，核心库

GLib 是一个底层库，是 GTK+ 和 Gnome 等项目的基础。它提供了数据结构、实用函数以及事件循环和线程等基本功能。GLib 简单且适用于大多数类 Unix 系统和 Windows。本章涵盖了一些最常用的特性。GLib 非常简单，且概念很熟悉；因此我们将快速通过。关于 GLib 更完整的覆盖，请参见开发环境（见第 10 页第 1.9 节）。顺便说：如果你对实现有特定的疑问，请尽管查看源码。通常文档包含了足够的信息，但如果你遇到缺失的细节，请提交 bug。GLib 的各种设施旨在提供的接口；编码风格是半面向对象的，标识符带有 "g" 前缀以创建命名空间。GLib 有几个头文件：

- glib.h，主头文件；
- gmodule.h，用于模块的动态加载；
- glib-unix.h，用于 Unix 特有的 API；
- glib/gtype.h 和 glib/gchar.h，用于国际化；
- glib/gstr.h 和；
- glib/printf.h 和 glib/gio.h，避免引入整个 stdio。

## 2.1 基础

GLib 为许多标准和常用的 C 语言构造提供了替代方案。本节描述了 GLib 的基础类型定义、宏、内存分配例程和字符串实用函数。

### 2.1.1 类型定义

GLib 没有使用 C 的标准类型（int, long 等），而是为了各种目的定义了自身的类型。例如，gint32 保证为 32 位宽，这是标准 C89 类型无法保证的。guint 比 unsigned 更容易使用的类型。一些类型定义 (typedef) 仅为了一致性而存在；例如，gchar 始终等于标准的 char。

GLib 定义的最重要的原始类型：

- gint8, uint8, gint16, uint16, gint32, uint32, gint64, uint64 ——为你提供保证大小的整数。（如果是无符号的，则类型是有符号的。）
- gboolean 有助于让你的代码更具读性，因为 C89 没有 bool 类型。
- gchar, gshort, glong, glint, gfloat, gdouble 纯粹是视觉上的。
- gpointer 比 void * 更容易书写。（const gpointer 是不行的；如果你不知道为什么，请花时间读一本好的 C 语言书。）
- gsize 是无符号整数类型，可以容纳 `sizeof` 运算符。

### 2.1.2 常用宏

GLib 定义了许多在 C 程序中常用的熟悉的宏，如列表 2.1 所示。这些内容都是自言自懂的。MIN()/MAX() 返回参数中较小或较大的值。ABS() 返回其参数的绝对值。CLAMP(x, low, high) 意味着 x，除非 x 在范围 [low; high] 之外；如果 x 低于范围，则返回 low；如果 x 高于范围，则返回 high。除了列表 2.1 中所示的宏，TRUE/FALSE/NULL 被定义为通常的 1/0/(void*)0)。

还有许多 GLib 特有的宏，例如列表 2.2 所示的 gpointer 到 int 和 gpointer 到 uint 的转换。

```c
#include <glib.h>

MAX(a, b);
MIN(a, b);
ABS(x);
CLAMP(x, low, high);
```
列表 2.1: 熟悉的宏

```c
#include <glib.h>

GINT_TO_POINTER(p);
GPOINTER_TO_INT(p);
GUINT_TO_POINTER(p);
GPOINTER_TO_UINT(p);
```
列表 2.2: 用于在...存储整数的宏

```c
#include <glib.h>

g_return_if_fail(condition);
g_return_val_if_fail(condition, return_value);
```
列表 2.3: 前提条件检查


```c
#include <glib.h>
```

```c
g_assert(condition);
g_assert_not_reached();
```

# 列表 2.4：断言 (Assertions)

列表 2.3 显示了 GLib 的预测检查。如果 condition 为 FALSE，`g_return_if_fail()` 会打印警告并立即从当前函数返回。`g_return_val_if_fail()` 与此类似，但它允许你返回 return_value。这些宏非常有用——如果你大量使用它们，特别是与 GObject 的运行时检查结合使用时，你将减少一半在寻找错误指针和类型错误上花费的时间。

使用这些函数非常简单；这里有一个 GLib 哈希表实现的一个示例：

```c
void
g_hash_table_foreach (HashTable *hash_table,
GHFunc func,
gpointer user_data)
{
  gint i;
  g_return_if_fail (hash_table != NULL);
  g_return_if_fail (func != NULL);
  for (i = 0; i < hash_table->size; i++)
  {
    guint node_hash = hash_table->hashes[i];
    gpointer node_key = hash_table->keys[i];
    gpointer node_value = hash_table->values[i];
    if (HASH_IS_REAL (node_hash))
      (* func) (node_key, node_value, user_data);
  }
}
```

如果没有这些检查，将 NULL 作为参数传递会导致神秘的段错误。使用该库的人必须使用调试器来找出错误发生的地方，或者甚至可能深入研究 GLib 代码以查看哪里出了问题。有了这些检查，他们将得到一个友好的错误信息，告诉他们不允许传递 参数。

GLib 还有更传统的断言宏，如列表 2.4 所示。`g_assert()` 基本上与 `assert()` 相同，但它对 `G_DISABLE_ASSERT` 有响应，并在所有平台上行为一致。GLib 还提供了 `g_assert_not_reached()`；这是一个始终会失败的断言。断言可以退出程序，并（如果你的环境支持）转储核心文件（core file）用于调试。

致命断言（Fatal assertions）应该用于检查函数或库的内部一致性，而 `g_return_if_fail()` 旨在确保传递到程序模块公共接口的是合理的值。也就是说，如果断言失败，你通常会在包含该断言的模块中寻找 bug；如果 `g_return_if_fail()` 检查失败，你通常会在调用该模块的代码中寻找 bug。

这段来自 GLib 日历计算模块的代码显示了差异：

```c
GDate *
g_date_new_dmy(GDateDay day,
GDateMonth month,
GDateYear year)
{
  GDate *date;
  g_return_val_if_fail(g_date_valid_dmy (day, month, year), NULL);

  date = g_new (GDate, 1);

  date->julian = FALSE;
  date->dmy = TRUE;

  date->month = month;
  date->day = day;
  date->year = year;

  g_assert (g_date_valid (date));

  return date;
}
```

开始处的先置条件检查确保用户传递了日、月、年的合理值；结尾处的断言确保了在给定合理值的情况下，GLib 构造了一个合理的对象。

`g_assert_not_reached()` 应用于标记“不可能”的情况：一种常见的用法是检测未处理枚举中可能值的 switch 语句。

```c
switch (value)
{
  case FOO_ONE:
    break;

  case FOO_TWO:
    break;

  default:
    g_assert_not_reached ();
}
```

### 2.1.4 内存 (Memory)

GLib 封装了标准的 `malloc()` 和 `free()`，提供了自己的变体，如列表 2.5 所示。这些变体以多种方式工作：

```c
#include <glib.h>
```

```c
gpointer g_new(type, count);
gpointer g_new0(type, count);
gpointer g_realloc(mem, size);
gpointer g_strdup(gconst mem);
```

列表 2.5：GLib 内存分配

```c
#include <glib.h>
```

```c
void g_free(gpointer mem);
void g_free(count);
```

列表 2.6：分配宏

- `g_malloc()` 始终返回 `gpointer`，因此不需要转换返回值。
- `g_malloc()` 在底层 `malloc()` 失败时终止程序。
- `g_malloc()` 优雅地处理大小为 0 的情况，返回 NULL。
- `g_free()` 会忽略传递它的任何指针。

将 `g_malloc()` 与 `g_free()` 匹配，`malloc()` 与 `free()` 匹配（如果你使用 C++ 则与 `delete` 匹配），否则会出问题。对于那些对比 `gchar *` Better字符串感兴趣的人，还有一个 `GString` 类型。书中没有介绍，请参阅 API 文档获取更多信息。

### 2.1.5 字符串处理 (String Handling)

GLib 提供了许多处理函数；有些是 GLib 特有的，并解决了一些可移植性问题。它们与 GLib 的内存函数配合良好。

列表 2.7 显示了 GLib 为 `sprintf()` 函数提供的一个子集。在拥有该函数的平台上使用 `g_sprintf()`，在不支持的平台上提供实现。

注意不要使用会导致崩溃、产生安全漏洞的 `sprintf()` 函数。通过使用相对安全的 `g_snprintf()` 或 `g_strndprintf()`（见下文），你可以永远告别 `sprintf()`。

列表 2.8 显示了 GLib 丰富的字符串分配函数。意料不用的是，`g_strdup()` 和 `g_strnd` 会产生 `str` 或其前 `n` 个字符的分配拷贝。为了与 GLib 内存函数保持一致，它们在指针为 NULL 时返回 NULL。`printf()` 变体返回格式化字符串。`g_strnfill()` 返回长度为 `length` 并由 `fill_char` 填充的字符串。

`g_strndprintf()` 特别提到；它是处理这种常见代码以便的方法：

```c
gchar *str = g_malloc(256);
g_snprintf(str, 256, "%d printf-style %s", num, string);
```

相反你可以使用这种方法，而无需计算缓冲区正确长度：

```c
gchar *str = g_strdu_printf("%d printf-style %s", num, string);
```

```c
#include <glib.h>

gchar * g_strchug(gchar *string);
gchar * g_strchomp(gchar *string);
gchar * g_strstrip(gchar *string);
```

列表 2.9：原地字符串修改



```c
#include <glib.h>

double g_strtod (const gchar *nptr, const gchar **endptr);
const gchar * g_strerror (int errnum);
const gchar * g_strisignal (int signum);
```

Listing 2.10: 字符串转换

```c
#include <glib.h>

gchar * g_strcat (const gchar *string1, ...);
gchar * g_strjoin (const gchar *separator, ...);
```

Listing 2.11: 字符串拼接

Listing 2.9 中的函数在原地操作时可能非常：`g_strchop()` 和 `g_strchomp()` 用于“裁剪”（移除字符串末尾空格），或“修剪”（移除头部空格）。这两个函数在修改字符串的同时，还会返回该字符串；在某些情况下，使用返回值可能会很方便。有一个宏 `g_strstrip()`，它结合了这两个函数来同时处理头部和末尾空格。

Listing 2.10 显示了 GLib 封装的更多几个半标准函数。`g_strtod` 类似于 `strtod()` —— 它将 `nptr` 转换为 `double`，区别在于如果在用户的默认区域（locale）中转换失败，它还可能尝试将数字转换为 "C"。`.endptr` 被设置为第一个未转换的字符，即 NULL 标识之后的任何文本。如果转换失败，*`endptr` 被设置为 NULL，并调用 `g_strignal()`*。

`g_strerror()` 和 `g_strisignal()` 是它们的非 GLib 等效实现，但具有可移植性。它们返回 `errno` 或信号数量的字符串表示。

GLib 提供了一些用于拼接字符串的方便函数，如 Listing 2.11 所示。`g_strcat()` 返回新分配的字符串，该字符串由参数列表中的字符串拼接而成。最后一个参数必须是 `NULL`，以便 `g_strcat()` 知道何时何时停止。`g_strjoin()` 类似，但会在每个字符串之间插入分隔符。如果 `separator` 为 `NULL`，则不使用分隔符。

最后，Listing 2.12 总结了几个处理 NULL 终止字符串数组的例程。`g_split()` 在每个分隔符处拆分字符串，返回一个新分配的数组。`g_strjoin()` 用可选分隔符拼接数组中的每个字符串，`g_strfreev()` 释放数组中的每个字符串然后释放数组本身。

```c
#include <glib.h>

gchar ** g_split (const gchar *string, const gchar *delimiter, int max_tokens);
gchar * g_strjoin (const gchar *separator, gchar **str_array);
void g_strfreev (gchar **str_array);
```

Listing 2.12: 操作 NULL 终止字符串向量

```c
typedef struct _GList GList;
struct _GList
{
  gpointer data;
  GList *next;
};
```

Listing 2.13: GList 单元

```c
#include <glib.h>

GList * g_slist_append(GList *list, gpointer data);
GList * g_slist_prepend(GList *list, gpointer data);
GList * g_slist_insert(GList *list, gpointer data, gint position);
GList * g_slist_remove(GList *list, gpointer data, gconstpointer data);
```

Listing 2.14: 修改链表内容

## 2.2 数据结构

GLib 实现了许多常见的数据结构，因此你不需要在每次想要链表时都重复轮子。本节涵盖了 GLib 对链表、排序二叉树、N 叉树和哈表的实现。

### 2.2.1 列表

GLib 分提供了通用的单链表和双链表，分别为 `GList` 和 `GList`。它们通过 `gpointer` 实现；你可以使用它们来存储整数（通过 `GINT_TO_POINTER` 和 `POINTER_TO_INT` 宏）。`GList` 和 `GList` 的 API 几乎相同，但没有 `g_list_previous()` 函数。本节将讨论关于链表的所有内容。

一个 `GList` 单元如 Listing 2.13 所示的自解释结构。字段是公开的，你可以直接使用它们访问数据或遍历链表。在 GLib 实现中，空列表是 `NULL` 指针。向 GLib 函数传递 `NULL` 总是安全的，因为长度为 0。创建一个列表并添加一个元素的代码可能如下：

```c
*list = NULL;
gchar *element = g_strdup("string");
list = g_list_append(list, element);
```

GLib 列表具有显著的影响；空列表是一个特殊的 "nil" 值。`g_slist_prepend()` 运行良好 —— 它是常数操作 (O(1))，在链表头部添加一个新单元。Listing 2.14 显示了修改 `GList` 内容的基本函数。对于所有这些函数，你必须将返回值赋值给你的链表指针。注意 GLib 不存储链表尾部的指针。

```c
#include <glib.h>

typedef void (*GFunc) (gpointer data, gpointer user_data);
```

```c
list_slist_foreach (Glist *list, function_, list_data);
```

Listing 2.16: 在链表中访问数据

使用 `g_slist_append()` 构建列表是一个非常糟糕的主意；如果你需要特定顺序的项，请使用 `g_slist_prepend()` 然后使用 `g_slist_reverse()`。当你预见到向链列表中添加元素时，也可以保留一个指向最后一个元素的指针。以下代码可用于高效编辑：

```c
void
efficient_append(GList *list,
                       GList **list_end,
                       gpointer data)
{
    g_return_if_fail(list != NULL);
    g_return_if_fail(list_end != NULL);

    if (*list == NULL) {
        g_assert (*list_end == NULL);
        *list = g_slist_append(*list, data);
        *list_end = *list;
    } else {
        *list_end = g_slist_append(*list_end, data)->next;
    }
}
```

要使用此方法，你需要将列表及其成员存储在某处，并将它们的地址传递给 `efficient_append()`：

```c
GList* list = NULL;
GList* list_end = NULL;
```

```c
efficient_append(&list, &list_end, g_strdup("Foo"));
efficient_append(&list, &list_end, g_strdup("Bar"));
efficient_append(&list, &list_end, g_strdup("Baz"));
```

当然需要小心使用任何可能更改链表尾部而不更新 `list_end` 的链表函数。

对于访问列表元素，提供了 Listing 2.16 中的函数。这些函数都没有改变链表结构。`g_slist_foreach()` 将 `GFunc` 应用于链表的每个元素。

> 一个更方便的方法是使用 `GQueue` 类型：这是一种双端队列，保留了指向头部、尾部的指针以及双链表的长度。




在 `g_slist_foreach()` 中，你提供的 `GFunc` 会对列表中的每个 `list->data` 被调用，并将你传递给 `g_slist_foreach()` 的 `user_data`。`g_slist_foreach()` 类似于 Scheme 中的 "map" 函数。

例如，你可能有一个字符串列表，并且可能想要创建一个对字符串应用了转换的并行列表。以下是一些代码，使用了之前一个示例中的 `efficient_append()` 函数：

```c
typedef struct _AppendContext AppendContext;
struct _AppendContext
{
  GLList *list;
  GLList *list_end;
  const gchar *append;
};

static void
append_foreach(gpointer data,
               gpointer user_data)
{
  gchar *oldstring = data;
  AppendContext *context = user_data;

  efficient_append (&context->list,
                    &context->list_end,
                    g_strcat(oldstring, context->append, NULL));
}
```

```c
GLList *
copy_with_append (GLList *list_of_strings,
               const gchar *append)
{
  AppendContext context;

  context.list = NULL;
  context.list_end = NULL;
  context.append = append;

  g_slist_foreach(list_of_strings, append_foreach, &context);
  return context.list;
}
```

GLib 和 GTK+ 大量使用“函数指针和用户数据”这种用法。如果你有函数式编程经验，这非常类似于使用 lambda 表达式来创建闭包。闭包将函数与一组名称-值绑定的环境结合在一起。在这种情况下，“环境”就是你传递给 `append_foreach()` 的 `user_data`，而“闭包”则是函数指针和用户数据的组合。

有许多列表操作例程，除了 `g_slist_copy()` 之外，所有这些例程都会原地修改列表。这意味着你必须分配返回值并更新传入的指针，就像你在添加或删除列表元素时所做的一样。`g_slist_copy()` 返回一个新的分配列表，因此你可以继续使用这两个列表，并且必须释放这两个列表。

最后，有一些针对排序列表的规定，如列表 2.18 所示。要使用这些，你必须编写一个 `GCompareFunc`，这与标准 C `qsort()` 中的比较函数相同。

如果 `a < b`，`GCompareFunc` 应该返回负值；如果 `a > b` 返回正值；如果 `a == b` 则返回 0。

一旦你有了比较函数，就可以将元素插入到已经排序的列表中，或者按升序对列表排序。你甚至可以使用 `g_slist_find_custom()` 循环你的 GList 指针来查找列表元素。

小心排序列表：遗漏 `g_slist_insert_sorted()` 操作可能会非常低效。例如，`g_slist_insert_sorted` 是 O(n)，但如果你在循环中使用它来插入多个元素，循环将以二次时间 (O(n²)) 运行。最好先将所有元素插入到头部，然后调用 `g_slist_sort()`。`g_slist_sort()` 的运行复杂度为 O(n log n)。

你也可以使用 `GSequence` 数据结构来处理排序数据。`GSequence` 拥有列表的 API，但在内部是用二叉树实现的。

### 2.2.2 树

GLib 中有两种树：GTree 是你的基础平衡二叉树，用于存储按键排序的键值对；GNode 存储任意的树形结构数据，例如解析树或分类体系。

## GTree

要创建和销毁 GTree，使用列表 2.9 所示的构造函数和析构函数。`GCompareFunc` 与为 GList 的 qsort()-风格比较函数相同；在这种情况下，它被用于比较树中的键。`g_tree_new_full()` 有助于对动态分配的键值使用简单的内存管理。

GTree 结构体是一个不透明的数据类型。其内容仅通过公共函数访问和修改。

```c
#include <glib.h>
```

typedef guint (* GCompareFunc) (gconstpointer a, gconstpointer b);
typedef gboolean (* GDataFunc) (gconstpointer a,
                              gconstpointer b,
                              gpointer user_data);

```

```c
GTree * g_tree_new (GCompareFunc key_compare_func);
```

```c
GTree * g_tree_new_full (GCompareFunc key_compare_func,
                        GDataFunc data_func,
                        GDataNotify data_destroy_func);
```

```c
void g_tree_destroy (GTree *tree);
```

```c
#include <glib.h>
```

```c
guint g_slist_length(GList *list);
GLList * g_slist_concat(GList *list1, GList *list2);
GLList * g_slist_reverse(GList *list);
GLList * g_slist_copy(GList *list);
```

列表 2.17: 操作链表列表

```c
#include <glib.h>
```

```c
typedef guint (*GCompareFunc)(const gpointer a, const gpointer b);
```

```c
GList * g_slist_insert_sorted(GList *list, gpointer data, GCompareFunc func);
GList * g_slist_sort(GList *list, GCompareFunc compare_func);
GList * g_slist_find_custom(GList *list, gpointer data, GCompareFunc func)
```

列表 2.18: 排序列表



```c
#include <glib.h>

GNode * g_node_new (gpointer data);
```

Listing 2.25: 创建一个 GNode

```c
#include <glib.h>

GNode * g_node_insert (GNode *parent, glint position, GNode *node);
GNode * g_node_insert_before (GNode *parent, GNode *sibling, GNode *node);
GNode * g_node_prepend (GNode *parent, GNode *node);
```

Listing 2.26: 构建 GNode 树

```c
#include <glib.h>

g_node_append (parent, node);
g_node_insert_data (parent, position, data);
g_node_insert_data_before (parent, sibling, data);
g_node_prepend_data (parent, data);
g_node_append_data (parent, data);
```

Listing 2.27: 构建一个 GNode

```c
#include <glib.h>

void g_node_destroy (GNode *root);
void g_node_unlink (GNode *node);
```

Listing 2.28: 销毁一个 GNode

```c
#include <glib.h>
```

```c
G_NODE_IS_ROOT(node);
G_NODE_IS_LEAF(node);
```

Listing 2.29: GNode 的谓词函数

```c
#include <glib.h>

guint g_node_n_nodes (GNode *root, GTraverseFlags flags);
GNode * g_node_get_root (GNode *node);
gboolean g_node_is_ancestor (GNode *node, GNode *descendant);
gint g_node_depth (GNode *node);
GNode * g_node_find (GNode *root,
    GTraverseFlags flags,
    gpointer data);
```

Listing 2.30: GNode 属性

g_node_unlink() 移除一个节点并使其成为根节点；即它将子树转换为一个独立的节点。

有两个宏用于检测 GNode 树的顶部和底部，如列表 2.29 所示。根节点定义为没有父节点或兄弟节点的节点。叶节点没有子节点。

你可以请求 GLib 报告关于 GNode 的有用信息，包括子节点数量、根节点、深度以及包含特定数据指针的节点。这些函数在列表 2.30 中所示。

GTraverseType 是一个枚举，有四个可能的值。以下是它们的含义：

- G_PRE_ORDER 先访问当前节点，然后依次递归每个子节点。
- G_POST_ORDER 顺序递归每个子节点，然后访问当前节点。
- G_IN_ORDER 首先递归节点最左边的子节点，然后访问节点本身，再递归节点的其他子节点。这并不好用；主要用于二叉树。
- G_LEVEL_ORDER 访问每个深度的第一个节点：每个子节点；子节点的节点；子节点的节点的子节点；以此此类推。也就是说，它先访问深度为 0 的每个节点，然后是深度为 1 的每个节点，然后深度为 2 的每个节点，等。

GNode 的树遍历函数有一个 GTraverseFlags 参数。这是一个位字段，用于改变遍历的性质。目前只有仅叶节点、仅非叶节点或所有节点：

- G_TRAVERSE_LEAVES 意味着只遍历叶节点。
- G_TRAVERSE_NON_LEAVES 意味着只遍历非叶节点。
- G_TRAVERSE_ALL 仅仅是 (G_TRAVERSE_LEAVES | G_TRAVERSE_NON_LEAVES) 的快捷方式。

```c
#include <glib.h>

typedef glint (*GNodeTraverseFunc) (GNode *node, gpointer data);
typedef void (*GNodeForEachFunc) (GNode *node, gpointer data);
```

```c
void g_node_traverse (GNode *root,
                    GTraverseFlags order,
                    GTraverseFlags flags,
                    gint max_depth,
                    GNodeTraverseFunc,
                    gpointer data);
```

```c
void g_node_child_foreach (GNode *node,
                             GTraverseFlags flags,
                             GNodeForEachFunc func,
                             gpointer data);
```

```c
guint g_node_max_height (GNode *root);
void g_node_reverse_children (GNode *node);
gint g_node_n_children (GNode *node);
gint g_node_child_position (GNode *node, GNode *child);
GNode * g_node_nth_child (GNode *node, guint n);
GNode * g_node_last_child (GNode *node);
```

Listing 2.31: 访问 GNode

列表 2.31 显示了一些 GNode 函数。它们非常直观；大部分操作都是对节点子节点列表的操作。使用了两个类型定义：GNodeTraverseFunc 和 GNodeForEachFunc。调用这些函数时会传入一个被访问节点的指针和用户数据。GNodeTraverseFunc 可以返回 TRUE 来停止遍历；因此你可以使用 g_node_traverse() 按值进行搜索。

### 2.2.3 哈希表 (Hash Tables)

HashTable 是一个简单的哈希表，提供常数时间查找的关联数组。要创建和销毁 GHashTable，你需要提供一个 GHashFunc，它在通过哈希时返回一个正整数。每个返回的整数（对表的大小取模）对应哈希中的一个“槽”或“桶”。GHashTable 通过在每个槽中存储键值对链表来处理冲突。你的 GHashFunc 返回的值必须在可能值的范围内分布均匀，否则表将退化为链表。GHashFunc 必须足够快速，因为每次查找都会使用它。

此外，还需要 GHashEqualFunc 在哈希冲突导致同一槽中存在多个对时测试键的相等性。如果你使用基础构造函数 g_hash_table_new()，请记住 GLib 没有办法销毁表中的数据；它只销毁表本身。如果键和值需要释放，请使用 g_hash_table_new_full()；销毁会在每个键上调用。

```c
#include <glib.h>

typedef guint (*GHashFunc) (gpointer key);
typedef gboolean (*GHashEqualFunc) (gpointer a, gpointer b);
typedef void (*GDestroyNotify) (gpointer data);
```

```c
GHashTable * g_hash_table_new (GHashFunc hash_func, GHashEqualFunc key_equal_func);

GHashTable * g_hash_table_new_full (GHashFunc hash_func,
                             GHashEqualFunc key_equal_func,
                             GDestroyNotify key_destroy_func,
                             GDestroyNotify value_destroy_func);
```

```c
void g_hash_table_destroy (GHashTable *hash_table);
```

Listing 2.32: GHashTable 构造函数和析构函数

```c
#include <glib.h>
```

```c
guint g_int_hash (gpointer key);
gboolean g_int_equal (gpointer key1, gpointer key2);
guint g_direct_hash (gpointer key);
gboolean g_direct_equal (gpointer key1, gpointer key2);
guint g_str_hash (gpointer key);
gboolean g_str_equal (gpointer key1, gpointer key2);
```

Listing 2.33: 写的哈希/比较函数

现用的哈希表销毁。

对于常见的键：整数、指针、字符串和其他 GLib 类型，提供了现成的哈希和比较函数。最常见的列在列表 2.33 中。整数的函数接受 int 指针而不是 int 本身。如果你向 g_hash_table_new() 传递 NULL 作为哈希参数，将使用 direct_hash()。如果你传递 NULL 作为相等函数，则使用简单指针（等同于 g_direct_equal()），但没有函数。

操作哈希表是简单的。程序在 2.34 中总结。插入不会复制键或值；它们按照你提供的方式进入表，替换任何相同键的键值对（“相同”由你的哈希和相等函数定义）。如果这是一个问题，你需要在插入之前进行查找或删除。如果动态分配键或值，请小心。如果你提供了 GDestroyNotify 函数，这些将在替换旧的键值对后自动调用。

简单的 g_hash_table_lookup 返回找到与键关联的值，如果没有则返回 NULL。这并不总是如此。例如，NULL 本身可能是一个有效值。如果你使用字符串作为键，特别是动态分配的字符串，知道键在表中可能是不够的；你可能想要获取表表示键 "foo" 的精确 gchar。针对这种情况提供了第二个查找函数：g_hash_table_lookup_extended() 如果查找成功则返回 TRUE；如果返回 TRUE，它会将找到的键和值放在给定的位置。

```c
#include <glib.h>

gboolean g_hash_table_insert (GHashTable *hash_table, gpointer key, gpointer value);
gboolean g_hash_table_remove (GHashTable *hash_table, gpointer key);
gpointer g_hash_table_lookup (GHashTable *hash_table, gpointer key);
gboolean g_hash_table_lookup_extended (GHashTable *hash_table, gpointer lookup_key, gpointer *orig_key, gpointer *value);
```

Listing 2.34: 操作 GHashTable

![](img/078dc1c39b3622bb7d98dea5203cc81_31_0.png)

图 2.1: 事件驱动应用程序的结构，带有主循环

## 2.3 主事件循环

如今的应用程序通常是事件驱动的。对于 GUI 应用程序，许多事件源：按键、鼠标点击、触摸手势、来自另一个应用程序的消息、文件系统的变化、网络连接或断开等。

应用程序需要响应这些事件。例如，当文本输入获得焦点时按下按键，字符应该被插入并显示在屏幕上。

但事件驱动编程也适用于守护进程。进程间通信也发生在守护进程和应用程序之间。当数据包到达网络接口时，守护进程可以接收事件。打印机守护进程可以在打印机连接、断开、缺纸等时接收事件。挂载守护进程可以监听插入的 USB 内存。另一个守护进程可以监听外部显示器以重新配置屏幕等。

事件驱动程序的结构不像处理程序。处理程序要执行的工作在开始时就已经确定了。它分析输入，对其进行某些计算并输出报告。例如，Unix 命令和脚本就是处理程序。

那么，如何构建一个需要响应任何时候到达的各种事件的应用程序呢？正如标题所示……当然带有主事件循环！那是 GLib 的另一个重要部分；提供了事件驱动编程的核心支持，带有主事件循环抽象、线程的可移植实现以及线程之间的异步通信。事件循环监听某些事件源。优先级与


每个事件的源。当一个事件到达时，事件循环会将其分发给应用程序。随后，可以在同一个线程或另一个线程中处理该事件。图 2.1 显示了什么是主循环（main loop）的高层视图。

一个事件驱动应用程序的 `main()` 函数看起来如下：

```c
gint
main (gint argc,
    gchar *argv[])
{
    /* 创建主窗口并附加信号回调。 */

    /* 运行主事件循环。 */
    gtk_main();

    return 0;
}
```

GTK+ 循环比 GLib 事件抽象稍微高一级。`gtk_main()` 运行主循环，直到调用了 `gtk_main_quit()`。`gtk_main_quit()` 通常在点击关闭按钮或激活 Qt 菜单动作的函数回调中被调用。

回调函数是在发送信号时被调用的函数。系统系统是由 GObject 库实现的。通过 `g_signal_connect()` 实现对信号的监听：

```c
static void
button_clicked_cb (GtkButton *button,
    gpointer user_data)
{
    MyObject *self = user_data;
    /* 执行一些事情 */
}
```

```c
static void
create_button (MyObject *self)
{
    GtkButton *button;
    /* 创建按钮 */

    /* 附加信号回调 */
    g_signal_connect(button,
        "clicked",
        G_CALLBACK(button_clicked_cb),
        self);
}
```

当回调返回时，它会阻塞主循环。因此，为了不冻结界面，有两种解决方案：

- 1. 长时操作（尤其是 I/O）可以在另一个线程中启动。
- 2. 长时操作可以拆分成更小的块，每个块在独立的循环迭代中运行。

```c
#include <glib.h>

typedef gboolean (* GSourceFunc)(gpointer user_data);

gint g_idle_add(GSourceFunc function, gpointer data);
gint g_timeout_add(gint interval, GSourceFunc function, gpointer data);
gboolean g_source_remove(gint source_id);
```

列表 2.35：空闲（Idles）和超时（timeouts）

对于第二种解决方案，GLib 提供了 `g_idle_add()` 和 `g_timeout_add()` 函数（见列表 2.35）。当主循环空闲时，会调用空闲函数，即主循环没有其他可要做的事。超时函数按固定间隔被调用。`GSource` 的布尔返回值允许继续或停止。如果继续，主循环将在下一次空闲时间或超时时再次调用该函数。你可以通过调用 `g_source_remove()` 手动移除 `GSourceFunc`，该函数接收由 `g_idle_add()` 或 `g_timeout_add()` 返回的源 ID 参数。你必须注意在执行计算的对象被销毁时移除 `GSourceFunc`。你可以将源 ID 作为一个属性存储在对象中，如果源 ID 不同于 0，则在析构函数中调用 `g_source_remove()`。（请参阅 GObject 库以了解如何在 C 中创建你自己的类。）

## 2.4 其他特性

一些尚未提到的核心应用支持：

- GError - 一种错误报告系统，类似于其他语言中的异常。
- `g_log()` 机制，允许你使用可配置的日志级别可插拔的打印程序打印警告、消息等。

工具类：

- 命令行选项解析器。
- 单元测试框架。
- 计时器功能。
- 日历/日期算术函数，例如 `g_path_get_basename()` 和 `g_path_is_absolute()`。
- 一个简单的 XML 解析器。
- 兼容 Perl 的正则表达式。

一些较小的工具类：

- `G_MAXFLOAT` 等。
- 字节序转换。
- `G_DIR_SEPARATOR`。
- `va_list` 宏。
- `G_VAR_COPY` 宏。
- `G_VAR_FREE` 宏。
- `G_CALLBACK_FREE` 宏。
- 宏操作操作

     。。



，，同样，，一些有趣的数据类型：

- 字符串和数组。
- G - - 映射到 的的标识符。
- GVariant - 存储值的通用类型，以及该类型的信息。

## 第二部分

## C 语言面向面向编程

## 介绍到第二部分

既然你已经熟悉了 GLib 库，下一步是？面向对象编程（OOP）在 C 语言中。

每个 GTK+ 组件都是 GObject 的基类子类。为了学习目的，这部分从 GObject 开始。GObject 增加了引用计数、继承、虚函数、接口等功能。

但为什么最初要遵循面向对象的风格？面向对象的代码使得学习更容易。

这部分包含两个章节：

- 第 3 章将解释如何编写你自己的半 OOP 类；
- 第 4 章将解释 GObject 的基础知识。

> ¹ C 中的全局变量可以是定义在 *.c 文件顶部的 **static** 变量，可以被该 *.c 文件中的任何函数访问。这有时很有用，但应该避免。

## 第 3 章

## C 语言中的半面向对象编程

在前章中已经解释了 GLib 核心库使用了半面向对象的编码风格。本节将解释它的含义，以及如何用这种风格编写自己的代码。

面向对象的主要思想之一是将相关的数据和行为放在一起¹。在 C语言中，数据存储在结构体中，而行为通过函数实现。为了将它们放在一起，我们将它们放在同一个 *.c 文件中，并将公共函数放在相应的 *.h 文件（头文件）中。

另一个重要的 OOP 是将所有数据隐藏在其类内部，这意味着结构体的完整定义应该存在于 *.c 文件中，而头文件只包含一个类型定义。类的用户不应该感知实现细节，而是只依赖于外部接口，即头文件和公共文档中的内容。这样，只要 API 不发生变化，类的实现就可以更改而不影响类的用户。

## 3.1 头文件示例

列表 3.1 第 38 页显示了一个简单拼写检查器的头文件示例。这是一个虚拟的代码；如果你现在在 GTK+ 程序中需要拼写检查器，你会使用 gspell 库²。

### 3.1.1 项目命名空间

首先是使用命名空间“MyApp”。头文件中的每个符号都带有项目命名空间的前缀。

为你的代码选择一个命名空间是一个良好的习惯，可以避免链接时的符号冲突。对于库来说这尤为重要，但对于应用程序来说也有一个更好。


```c
#ifndef MYAPP_SPELL_CHECKER_H
#define MYAPP_SPELL_CHECKER_H

#include <glib.h>

G_BEGIN_DECS
typedef struct _MyAppSpellChecker MyAppSpellChecker;

MyAppSpellChecker *
    myapp_spell_checker_new      (const gchar *language_code);

void
    myapp_spell_checker_free      (MyAppSpellChecker *checker);

gboolean
    myapp_spell_checker_check_work (MyAppSpellChecker *checker,
                                     const gchar *word,
                                     gsize word_length);

GSList *
    myapp_spell_checker_get_suggestions (MyAppSpellChecker *checker,
                                         const gchar *word,
                                         gsize word_length);

G_END_DECS
#endif /* MYAPP_SPELL_CHECKER_H */
```
列表 3.1: myapp-spell-checker.h

对于每个代码库必须是唯一的；例如，你不能在你的应用程序或库中重用 "G" 或 "Gtk" 命名空间！

### 3.1.2 类命名空间

此外，还有一个带有类名的命名空间，这里是 "SpellChecker"。如果你一致地遵循这一约定，符号名称将更具预测性，这使得 API 更易使用。符号的名称将始终是 "项目命名空间" + "类名" + "符号名"。

### 3.1.3 小写、大写还是驼峰命名？

根据符号类型，其名称可能是大写、小写或驼峰命名（CamelCase）。GLib 世界的约定是：

- 常量使用大写字母，无论是 #define 还是枚举值；
- 结构体（struct）枚举类型使用驼峰命名；
- 函数、变量、结构体字段等使用小写；

### 3.1.4 头文件保护 (Include Guard)

该头文件包含典型的头文件保护：

```c
#ifndef MYAPP_SPELL_CHECKER_H
#define MYAPP_SPELL_CHECKER_H
```

```c
/* ... */ /* MYAPP_SPELL_CHECKER_H */

#endif 保护头文件在同一个 *.c 文件中被多次包含。
```

### 3.1.5 C++ 支持

G_BEGIN_DECLS/G_END_DECLS 对允许该头文件被 C++ 代码包含。这对于库来说更为重要，但在应用程序代码中添加宏也是一种良好的做法，即使应用程序没有使用 C++。这样，应用程序类就可以很容易地移动到库中（很难注意到缺少了 G_BEGIN_DECLS 和 G_END_DECLS 宏）。而且如果有需要，应用程序可以渐进地迁移到 C++。

### 3.1.6 #include

在 C 代码库中，组织 #include 的方法有多种。GLib/GTK+ 的约定是，在 *.c 文件中包含头文件不应该要求预先包含另一个头文件。

> ^3这是一个通用的经验法则，但存在例外：例如，包含 glib/i18n-lib.h 需要定义 GETTEXT_PACKAGE，后者通常存在于 config.h 头文件中。

myapp-spell-checker.h 包含以下 #include：
```c
#include <glib.h>
```

因为 glib.h 需要用于 G_BEGIN_DECLS 和 G_END_DECLS 宏，GLib 基础类型定义（char, gboolean 等）以及 GList。

如果删除了 myapp-spell-checker.h 中的 #include，每个包含 myapp-spell-checker.h 的 *.c 文件都将预先包含 glib.h，否则编译器将无法编译该 *c 文件。但我们不想为该类的用户增加这样的要求。

### 3.1.7 类型定义

MyAppSpellChecker 类型定义如下：
```c
typedef struct _MyAppSpellChecker MyAppSpellChecker;
```

结构体 _MyAppSpellChecker 将 myapp-spell-checker.c 文件中声明。当你在另一个文件中使用 MyAppSpellChecker 时，你不应该知道该结构体包含什么，而应该使用类的公共函数。OOP 最佳实践的例外是当调用函数会导致性能问题时，例如用于计算机图形的低级数据结构（坐标、矩形等）。但请记住：过早优化是万恶之源（Donald Knuth 说）。

### 3.1.8 对象构造函数

myapp_spell_checker_new() 是类的构造函数。它接收一个语言代码参数——例如 "en_US"，并返回类的实例，也称为对象。该函数简单地动态分配结构体并返回指针。该返回值随后被用作该类剩余函数的第一个参数。在 Python 等语言中，该第一个参数被称为 self 参数，因为它引用了“自身”，即它自己的类。其他面向对象的语言如 Java 和 C++ 拥有此关键字来访问对象数据。

注意 myapp_spell_checker_new() 可以被多次调用以创建不同的对象。每个对象持有自己的数据。这与全局变量的根本区别：如果数据存储在全局变量中，则最多只有一个实例⁴。

### 3.1.9 对象析构函数

myapp_spell_checker_free() 是类的析构函数。它通过释放内存和释放其他分配的资源来销毁对象。

> ⁴除非

### 3.1.10 公有函数

myapp_spell_checker_check_work 和 myapp_spell_checker_get_suggestions 提供了该类的可用功能。




```
GList *suggestions = NULL;

g_return_val_if_fail (checker != NULL, NULL);
g_return_val_if_fail (word != NULL, NULL);
g_return_val_if_fail(word_length >= -1, NULL);

if (word_length == -1)
    length = strlen(word);

if (strncmp(word, "punchiness", word_length) == 0)
    suggestions = g_list_prepend(suggestions,
        g_strdup("punchiness"));

return suggestions;
}
```

列表 3.2: myapp-spell-checker.c

## 3.2.1 #include 的顺序

在文件的顶部，有一组常见的 #include 列表。一个值得注意的细节是，包含顺序并不是随机选择的。在某个 *.c 文件中，最好先包含对应的 *.h 文件，然后是其他头文件。通过先包含 `myapp-spell-checker.h`，如果 `myapp-spell-checker.h` 中缺少某个 `#include`，编译器将报告错误。正如第 3.1.6 节（第 39 页）所解释，头文件应该包含尽可能少的 #include，以便其被其他文件包含。

此外，由于 `glib.h` 已经包含在 `myapp-spell-checker.h` 中，因此没有在 `myapp-spell-checker.c` 中再次包含它。

## 3.2.2 GTK-Doc 注释

公共 API 使用 GTK-Doc 注释进行文档。GTK-Doc 注释以 `/**` 开始，下一行是待记录的符号名称。当我们引用符号时，根据类型有特殊的语法可以使用：

- 函数参数以 `$` 为前缀。
- 结构体或枚举名称以 `#` 为前缀。
- 常量——例如枚举值——以 `%` 为前缀。
- 函数以 `()` 结尾。

GTK-Doc 可以解析这些特殊注释并生成 HTML 页面，可以通过 Devhelp 等 API 浏览器进行轻松导航。但代码中的格式化注释并不是 GTK-Doc 需要的全部，它还需要集成到项目的构建系统（例如 Autotools）中，并配合其他列出不同页面、通过符号列表描述整体结构，并可选地提供以 DocBook XML 格式编写的其他内容。这些文件通常存在 `docs/reference/` 目录下。

> 除非你有 `config.h` 文件，情况下你应该先包含 `config.h`，然后是对应的 *.h，最后是其他头文件。

详细描述如何集成 GTK-Doc 代码超出了本书的范围。对于这一点，你应该参考 GTK-Doc 手册 [9]。

每个基于 Glib 的库都应该有 GTK-Doc 文档。但为应用程序的内部代码编写 GTK-Doc 文档也是有。正如文本 1.7.1 节（第 7 页）所解释的，从应用程序的前端准备其后端是一个良好的做法，将后端编写为内部库，或者稍后作为共享库。因此，即使后端仍然是一个内部静态链接库，也建议使用 GTK-Doc 文档其公共 API。当代码库变得越来越时，拥有一个可用类的概览非常有帮助——特别是对于新手来说——可以让他们在不需要理解其实现的情况下知道如何使用某个类。

## 3.2.3 GObject Introspection 注解

`myapp_spell_checker_get_suggestions()` 函数的 GTK-Doc 注释包含了针对返回值的 GObject Introspection 注解：

```
/**
 * Returns: (transfer full) (element-type utf8): 建议列表
 * */
```

返回类型是 `GList *`，这不足以让语言绑定知道列表包含什么以及如何释放。`(transfer full)` 意味着调用者必须完全释放返回值：列表本身及其元素。`(element-type utf8)` 列表包含 UTF-8 字符串。

对于值，如果传输注解是 `(transfer container)`，调用者需要释放数据结构而非其元素。如果传输注解是 `(transfer none)`，所有权不转移，因此调用者无需释放返回值。

还有许多其他 GObject Introspection (GI) 注解，仅举几个：

- `(nullable)`：值可以为 NULL
- `(out)`：输出参数，即返回值的参数。

你可以看到，GI 注解不仅对语言绑定有用，也为 C 程序员收集有用信息。完整的 GI 注解列表请参见 GObject Introspection wiki [10]。

## 3.2.4 静态与非静态函数

在示例代码中，你可以看到 `load_dictionary()` 函数被标记为 `static`。静态函数是一个良好的做法，因为它们可以在同一个 *.c 文件中使用。相反，公共函数应该是非静态的，并在头文件中具有原型。

可以通过 `-Wmissing-prototypes` GCC 警告确保代码遵循此约定⁶。

此外，与公共函数相反，静态函数不需要项目和类命名名前缀（此处为 `myapp_spell_checker`）。

## 3.2.5 防御性编程

每个公共函数都对其参数进行了检查。在函数开始处检查参数是一个良好的做法，防止后续出错。例如，使用 `g_return_val_if_fail` 是实现此点的常用方法。

## 3.2.6 代码风格

最后，解释一些关于代码风格的内容。与 Linux Kernel不同，行长度没有真正的限制。基于 GObject 代码可能有非常长的行，特别是当参数对齐时。某些编辑器可以配置为这样做。

对于函数调用，将所有参数放在同一行会让代码更易读：

```
function_call (one_param,
               another_param,
               yet_another_param);
```

> ⁶当使用 Autools 时，`AX_COMPILER_FLAGS` 宏开启（以及其他）GCC 标志。

> ⁷在 `myapp-spell-checker.h` 中，函数名缩进了两个空格而不是与返回类型在同一行，因为页面水平空间不足。

> ⁸http://cscope.sourceforge.net/





# 第 4 章

## GObject 简析

在上一节中，我们学习了如何在 C 语言中编写半面向对象的代码。这就是 GLib 中类的实现方式。GObject 在面向对象编程方面更进了一步，包含了继承、接口、虚函数，而且 GObject 还通过信号（signals）和属性（properties）简化了事件驱动编程范式。

在编写 GLib/GTK+ 应用时，建议创建自己的 GObject 类。遗憾的是，代码有些冗长，因为 C 语言并不是面向对象的。某些功能需要编写模板代码（Boilerplate code），但不要担心，有工具和脚本可以生成这些模板代码。

然而，本章相比于上一节后退了一步，它只是对 GObject 的简要介绍；它将解释如何使用现有的 GObject 类（如所有的 GTK+ 控件和 Gio 中的类）时所需的要要知识。它不会解释如何创建你自己的 GObject 类，因为这在 GObject 参考手册中已经有详细介绍，而本书的目标不是重复参考手册的所有内容，而是作为一份入门指南。

关于 GObject 的更多深入信息以及如何知道创建子类，GObject 参考文档包含了介绍性章节：“Concepts”（概念）和“Tutorial”（教程），地址如下：

```
https://developer.gnome.org/gobject/stable/
```

为了解释这些概念，部分示例取自 GTK+ 或 Gio。在阅读时，鼓励你并行打开 Devhelp，查看 API 参考，并亲眼观察基于 GObject 的库是如何文档化的。目标是让你变得独立，能够学习任何新的 GObject 类，无论是在 Gio、GTK+ 还是其他库中。

## 4.1 继承

OOP（面向对象编程）的一个重要概念是继承。类可以是父类的子类。子类继承父类的特性，扩展或覆盖它的行为。

GObject 库提供了 GObject 基类。Gio GTK+ 中的所有类直接或间接自 GObject 基类。在查看基于 GObject 的类时，文档（使用 GTK-Doc 编写）始终包含一个对象层次结构（Object Hierarchy）。例如，GtkApplication 具有以下层次结构：

- GObject
- GApplication
- GtkApplication

这意味着当你创建一个 GtkApplication 对象时，你也可以访问 GApplication（在 GIO 中实现）和 GObject 的函数、信号和属性。当然，g_application.* 函数的第一个参数变量类型为 "GtkApplication *"，而不是 "Gtk Application *"。为了将变量转换为正确的类型，推荐的方法是使用 G_APPLICATION() 宏。例如：

```
GtkApplication *app;
```

```
g_application_mark_busy (G_APPLICATION (app));
```

## 4.2 GObject 宏

每个 GObject 类都提供一组标准宏。上一节演示的 G_APPLICATION() 宏是 GApplication 类提供的标准宏之一。

并不是所有的标准 GObject 宏都会在这里解释，仅解释对基础方式使用 GObject 有用的宏。其他宏更高级，通常只在派生 GObject 类、创建属性或信号、或覆盖虚函数时有用。

每个 GObject 类都定义了一个格式为 `NAMESPACE_CLASSNAME(object)` 的宏，它将变量强制转换为类型 "NamespaceClassname " 并在运行时检查该变量是否正确包含一个 NamespaceClassname 对象或其子类。如果变量为 NULL 或包含不兼容的对象，它会在控制台打印一条关键警告消息并返回 NULL。

标准的类转换也有效，但大多数时候不推荐，如下所示：

GtkApplication *app;

```
/* 不推荐写法 */
g_application_mark_busy ((GtkApplication *) app));
```

另一个在使用 GObject 时有用的宏是 `NAMESPACE_IS_CLASSNAME(object)`，如果变量是 NamespaceClassname 对象或其子类，它返回 TRUE。

## 4.3 接口

通过 GObject 可以创建接口（Interfaces）。接口只是一个 API，它不包含实现。一个 GObject 类可以实现一个或多个接口。如果一个 GObject 类有 GTK-Doc 文档，文档将包含特定的“Implemented Interfaces”（已实现的接口）。

例如，GTK+ 包含了 GtkOrientable 接口，该接口由许多控件实现，并允许设置方向：水平或垂直。

上一节解释的两个宏也适用于接口。一个关于 Gtkvgrid 的示例：

```
Gtkwidget *vgrid;

vgrid = gtk_grid_new();
gtk_orientable_set_orientation(GTK_ORIENTABLE(vgrid),
                                     GTK_ORIENTATION_VERTICAL);
```

因此，当你在某个 GObject 类中搜索某个功能时，该功能可能位于三个地方：

- 在 GObject 类本身中；
- 在对象层次结构中的某个父类中；
- 或者在某个已实现的接口中。

## 4.4 引用计数

GObject 类的内存管理依赖于引用计数（Reference Counting）。一个 GObject 类有一个计数器：

- 当对象被创建时，计数器等于一；
- g_object_ref() 增加计数器；
- g_object_unref() 减少计数器；
- 如果计数器达到零，对象会被释放。

这允许将 GObject 存储在多个地方。

### 4.4.1 使用弱引用避免引用循环

如果 A 引用对象 B，而对象 B 引用对象 A，就会产生引用循环，对象将永远无法释放。为了避免这个问题，引入了弱引用（Weak References）的概念。调用 g_object_ref() 时，它是强引用（Strong Reference）。所以在一个方向上是强引用，而在另一个方向上必须是弱引用。

在图中，我们可以看到 A 对 B 有强引用，而对象 B 对 A 有弱引用。弱引用可以通过 `g_object_add_weak_ref()` 或 `g_object_weak_ref()` 创建。就像强引用一样，在需要时释放引用，通常在类的析构函数中。弱引用必须通过 `g_object_weak_pointer()` 或 `g_object_weak_unref()` 移除。

### 4.4.2 浮动引用

当一个 GObject 继承自 GInitially 时（GtkWidget 的情况），对象初始有一个浮动引用（Floating Reference）。必须调用 `g_object_ref_sink()` 将该浮动引用转换为普通的强引用。

当 GObject 继承自 GInitially 时，意味着该对象被包含在某种容器中。容器随后接管浮动引用的所有权，调用 `g_object_ref_sink()`。这允许简化代码，消除在将对象放入容器后调用 `g_object_unref()` 的需求。

列表1 显示了如何管理普通 GObject 的内存。对比列表 2，它展示了派自 GInitially 的 GObject 如何管理内存。区别在于后者不需要调用 `g_object_unref()`，从而缩短了代码。

因此，知道一个 GObject 是否继承自 GInitially 是重要的。为此，你需要查看对象层次结构，例如 GtkEntry：

```
GObject
 GInitially
  GtkWidget
   GtkEntry
```

## 4.5 信号与属性

GObject 可以发射信号（Signals）。结合 GLib 主循环（之前在第2.3节，第31页解释过），这是事件驱动编程的基础。信号的一个示例是用户点击按钮。应用程序连接一个回调函数，以便在事件发生时执行所需的操作。

GObject 的另一个概念是属性（Properties），它与信号相关。属性本质上是一个实例变量，并带有一个“notify”信号，该信号在值变化时被发射。属性的一个很好的示例是复选按钮的状态，即描述按钮当前是否被选中的布尔值。当状态改变时，会发送“notify”信号。




要创建你自己的信号或属性，必须创建一个 GOObject 的子类。正如本章引言中所，这超出了本书的范围，但你应该意识到，创建你自己的信号或属性是完全可能的，并且是推荐的。事实上，创建一个 GOObject 信号或属性是实现**观察者模式** [3] 的良好方法；即通过连接函数回调，让一个或多个对象观察另一个对象的状态变化。发射信号的对象并不知道哪些对象接收了它。GOObject 负责维护要调用的回调列表。因此，添加信号允许类之间进行解耦。

### 4.5.1 将回调函数连接到信号

为了让这些内容更具体，如果你查看 GtkButton 的文档，你会发现它提供了 "clicked" 信号。为了在信号发射时执行所需的操作，必须预先连接一个或多个回调函数。

要将回调连接到信号，可以使用 `g_signal_connect()` 函数，或者其他的 `g_signal_connect_*` 函数之一：

- g_signal_connect()
- g_signal_connect_after()
- g_signal_connect_swapped()
- g_signal_connect_data()
- g_signal_connect_object()
- 以及一些高级函数。

代码列表 4.3 第 52 页显示了 GtkButton::clicked 信号。当使用 `g_signal_connect()` 时，回调函数的原型必须与信号的原型相同。某些信号具有更多参数，某些信号则返回一个值。如果回调原型不兼容，就会发生糟糕的事情，出现随机的 bug 或崩溃。

代码列表 4.4 第 53 页展示了如何使用 `g_signal_connect()` 的示例。使用 `G_CALLBACK()` 是必要的，因为 `g_signal_connect()` 是通用的：它可以被用于连接到任何 GOObject 类的任何信号，因此函数指针需要进行类型转换。

连接回调函数有两种命名规范：

- 函数名以 "cb" 结尾，是 "callback" 的缩写。例如，在上面的代码示例中使用了 `button_clicked_cb()`。
- 函数名以 "on" 开头。例如：`on_button_clicked()`。

通过这些命名规范之一——加上始终作为最后一个参数的 `gpointer user_data` 参数——可以很容易识别出一个函数是否是回调。

> 引用 GOObject 信号的规范是 "ClassName::signal-name"。这是在 GTK-Doc 注释中记录的方式。

```c
/* Normal GObject */
a_normal_gobject = normal_gobject_new();
/* a_normal_gobject 现在的引用计数为 1. */

container_add(container, a_normal_gobject);
/* a_normal_gobject 现在的引用计数为 2. */

/* 我们不再需要 a_normal_gobject，所以对其进行取消引用。 */
g_object_unref(a_normal_gobject);
/* a_normal_gobject 现在的引用计数为 1. */
```

代码列表 4.1：普通 GObject 的内存管理。

```c
/* GInitiallyUnowned 对象, 例如一个 GtkWidget */
widget = gtk_entry_new();
/* widget 现在有一个浮动引用。 */

tk_container_add(container, widget);
/* container 调用了 g_object_ref_sink()，获取了
 * 浮动引用的所有权。代码被简化了，
 * 因为我们不能调用 g_object_unref()。 */
```

代码列表 4.2：继承自 GInitiallyUnowned 的 GObject 的内存管理。

```c
void
user_function (GtkButton *button,
               gpointer user_data);
```

代码列表 4.3：GtkButton::clicked 信号的原型。

```c
static void
button_clicked_cb (GtkButton *button,
  gpointer user_data)
{
  MyClass *my_class = MY_CLASS (user_data);

  g_message ("Button clicked!");
}

static void
create_button (MyClass *my_class)
{
  GtkButton *button;

  /* 创建按钮 */
  /* ... */

  /* 连接回调函数 */
  g_signal_connect(button,
    "clicked",
    G_CALLBACK (button_clicked_cb),
    my_class);
}
```

代码列表 4.4：如何连接到信号

C 语言允许编写不同的但兼容的回调函数，尽管这并不被普遍认为是一种好做法：

- 如果最后一个或多个函数参数没有被使用，可以省略。但如上文所述，`gpointer user_data` 参数允许轻松识别出该函数实际上是一个回调。
- 参数的类型可以修改为兼容的类型：例如继承层次结构中的另一个类，或者在上面的示例中，将 "pointer" 替换为 "MyClass"（但这样做会导致代码不够健壮，因为没有调用 `MY_CLASS()` 宏）。

### 4.5.2 断开信号处理器

在代码列表 4.4 中，每当按钮对象发射 "clicked" 信号时，`button_clicked_cb()` 就会被调用。如果当 `my_class` 释放后按钮仍然存，信号将再次发射，这会产生一个小问题……在 `MyClass` 的析构函数中，必须断开信号处理器（回调）。如何做到这一点？

```c
#include <glib.h>

struct _MyTextView {
    GObject parent_instance;
    GObject *spell_checker;
    gulong added_to_handler_id;
};
#define MY_TYPE_TEXTVIEW (my_textview_get_type())
static GType my_textview_get_type(void);
typedef struct _MyTextView MyTextView;
#define MY_TEXTVIEW(obj) (MyTextView *)(obj)

static void
word_added_to_personal_cb (Object *spell_checker,
                 gchar *word,
                 gpointer user_data)
{
  MyTextView *text_view = MY_TEXTVIEW(user_data);

  g_message("Word '%s' has been added to dictionary.", word);
}

MyTextView *
my_textview_new (GObject *spell_checker)
{
  MyTextView *text_view;

  text_view = g_object_new (MY_TYPE_TEXTVIEW, NULL);

  text_view->spell_checker = g_object_ref (spell_checker);

  text_view->added_to_handler_id = g_signal_connect(spell_checker,
    "word-added-to-personal",
    G_CALLBACK (word_added_to_personal_cb),
    text_view);

  return text_view;
}

void
my_textview_free (MyTextView *text_view)
{
  if (text_view == NULL)
    return;

  if (text_view->spell_checker != NULL &&
      text_view->added_to_handler_id != 0)
    g_signal_handler_disconnect (text_view->spell_checker,
      text_view->added_to_handler_id);

  /* 这里将值置为 0 是没有必要的，因为
   * text_view 将会被释放，这只是为了有一个完整的示例。 */
  text_view->added_to_handler_id = 0;

  /* 在减少引用计数后，如果程序的其他部分仍然引用
   * spell_checker，则它可能仍然存活。 */
  g_clear_object (&text_view->spell_checker);

  g_free (text_view);
}
```

在代码列表 4.4 中，每当按钮对象发射 "clicked" 信号时，`button_clicked_cb()` 就会被调用。如果当 `my_class` 释放后按钮仍然存，信号将再次发射，这会产生一个小问题……在 `MyClass` 的析构函数中，必须断开信号处理器（回调）。如何做到这一点？

`g_signal_connect()` 函数返回一个 ID，稍后可以使用 `g_signal_handler_disconnect()` 用来断开处理器。

> 引用 GOObject 信号的规范是 "ClassName::signal-name"。这是在 GTK-Doc 注释中记录的方式。




基础 `g_signal_handler_disconnect()` 函数已用于教学目的。

另请注意，如果 MyTextView 是一个 GObject 类，那么将可以使用 `g_signal_connect_object()` 连接到拼写检查器信号，这样就完全不再了在 MyTextView 析构函数中手动断开信号处理程序。这是学习如何创建 GObject 类的另一个（小）理由。

### 4.5.3 属性 (Properties)

如果你查看过 GTK+ 或 GIO API 参考文档，你可能会注意到某些 GObject 类具有一个或多个属性。在 GObject 语文中，实例变量（也称为“属性”）是不同的，因为它具有额外的有趣的属性。

正如之前在第 4.5 节第 50 页开头所说，属性的一个很好的例子是按钮的状态，这是一个描述按钮是否被勾中的布尔值。如果你已经了解了一点 GTK+，你可能发现 `GtkCheckButton` 组件提供了一个复选按钮。但如果你想找到我所说的那个属性，就会遇到一个陷阱，因为该属性实现在父类 GtkToggleButton 中：GtkToggleButton::active 属性⁶

## "notify" 信号

属性除了表示值之外的主要特性是——当属性值改变时，GObject 类会发射 `GObject::notify` 信号。

有一种 GObject 信号连接尚未解释，并用于 `GObject::notify` 信号：发射信号时，可以提供一个细节（detail）。在 notify 信号的情况下，细节是值改变的属性名称。由于所有属性只有一个信号，得益于细节，可以连接一个回调函数，仅在特定属性发生变化时接收通知。在连接回调函数时不提供细节，那么当对象的任何属性变化时回调都会被调用，这通常不是我们想要的。

通过示例会变得更清晰。列表 4.6 第 57 页展示了如何连接到 notify 信号。与连接到 `GObject::activate` 信号相比，使用 `GtkToggleButton::toggled` 信号实际上更方便。在现实世界中，有更好的用例需要连接到 notify 信号，但至少列表 4.6 在具有有限 GTK+ 知识的情况下希望是可以理解的（如果你同时查看 Devhelp 中的文档）。

> ⁵ 双关语在此（Pun intended）。
⁶ 信号使用 Gtk-Doc 以 "ClassName::signal-name" 的形式记录，属性则以 "ClassName:property-name" 的形式记录。
⁷ 也是双关语。

```c
/* 如果你查看 notify 信号文档，第一个参数
 * 类型是 GObject，而不是 GtkCheckButton。由于 GtkCheckButton 是
 * GObject 的子类，C 语言允许直接编写 GtkCheckButton。 */
static void
check_button_notify_cb (GtkCheckButton *check_button,
                           GParamSpec *pspec,
                           gpointer user_data)
{
    /* 每当 check_button 的任何属性变化时都会调用此函数。 */
}

static void
check_button_notify_cb (GtkCheckButton *check_button,
                           GParamSpec *pspec,
                           gpointer user_data)
{
    MyWindow *window = MY_WINDOW (user_data);
    boolean active;

    active = gtk_toggle_button_get_active (GTK_TOGGLE_BUTTON (check_button));
    gtk_widget_set_visible (window->side_panel, active);
}

static GtkWidget *
create_check_button (MyWindow *window)
{
    GtkWidget *check_button;

    check_button = gtk_check_button_new_with_label ("Show side panel");
}

/* 不带细节的连接。 */
g_signal_connect (check_button,
                 "notify",
                 G_CALLBACK (check_button_notify_cb),
                 NULL);

/* 带细节的连接，仅当
 * * GtkToggleButton:active 属性变化时进行通知。 */
g_signal_connect (check_button,
                 "notify::active",
                 G_CALLBACK (check_button_notify_active_cb),
                 window);

    return check_button;
}
```

列表 4.6：连接到 notify 信号以监听属性变化。

## 属性绑定 (Property Bindings)

属性的另一个有用方面是两个属性可以绑定：当一个属性变化时，另一个就会更新。这可以通过 "notify" 信号实现，但使用 `g_object_bind()` 函数要简单得多。

```c
static GtkWidget *
create_check_button (MyWindow *window)
{
    GtkWidget *check_button;

    check_button = gtk_check_button_new_with_label ("Show side panel");

    /* 不带细节的连接。 */
    g_signal_connect (check_button,
                 "notify",
                 G_CALLBACK (check_button_notify_cb),
                 NULL);

    /* 带细节的连接，仅当
     * * GtkToggleButton:active 属性变化时进行通知。 */
    g_signal_connect (check_button,
                 "notify::active",
                 G_CALLBACK (check_button_notify_active_cb),
                 window);

    return check_button;
}
```

列表 4.7：绑定两个属性。

## 第三部分

## GTK+

## 第5 章

## 5.1 main() 函数和 EditApp

虽然在 schema 中没有体现，但 GTK+ 应用程序的入口——正如每个 C 程序一样——是 main() 函数。要创建一个 GTK+ 应用，在 main() 中主要的事情是创建一个 GApplication 实例或其子类。在 schema 中我们看到 GerritApp 是 GtkApplication 的子类，因此 main() 函数创建了一个 GerritApp。

GApplication 是 Gio 库的一部分，实现了与用户界面无关的功能……图 5.1 第 61 页展示了 gedit 的代码架构。

¹https://wiki.gnome.org/Apps/Gedit
²https://wiki.gnome.org/Projects/GtkSourceView

![](img/078dc81c39b3622bb7d98dea523cc81_61_0.png)

图 5.1：gedit 编辑器的简化版代码架构




进程唯一性（Process uniqueness）有几个优点，这里举几个具体的例子：

- 对于具有标签页文档界面的应用程序，当在像 Nautilus 的管理器中点击文件时，可以在新标签页中打开文件，而不是为每个文件创建一个新窗口。为了这项工作，需要某种形式的进程间通信；

- 应用程序不需要同步其状态和不同进程。为了便于解释，假设在 gedit 中用户创建了自定义的“构建工具”，用于编译当前文件或项目。gedit 将自定义构建工具保存在 XML 文件中，并显示在菜单中以执行它们的命令。在 Linux 上，该 XML 文件例如保存在用户的 `~/.local/share/` 目录下。如果没有唯一性，如果其中一个 gedit 进程修改了自定义工具，其他 gedit 进程将必须重新加载 XML 文件，并且需要确保没有竞态条件（两个不同的进程同时修改同一个 XML 文件）。有了唯一性，这个问题就不存在了，gedit 窗口共享相同的应用程序状态，开发者可以假设每个用户只有一个进程可以修改 XML 文件³；用户仍然有手动编辑 XML 文件的可能性，但在那种情况下应用程序是单例运行的，且用户应该通过 GTK（提供这些工具）来修改工具。

GApplication 的另一个重要特性是运行主事件循环。GLib 主循环在第 2.3 节第 31 页中描述。使用 GApplication，这通过 `g_application_run()` 函数实现。gedit 中 `main()` 函数的简化版本如下：

```
int
main (int argc,
    char**argv)
{
GEditApp *app;
int status;

/* 在此处初始化 i18n (国际化)。 */

app = gedit_application_new();
status = g_application_run(G_APPLICATION (app), argc, argv);
g_object_unref(app);

return status;
}
```

Gedit 基本上所做的是在如果没有 GApplication 子类的情况下在 `main()` 中需要完成的工作。这包括：

> 注意，如果可以在同一台机器上为同一个用户运行多个图形会话（这是支持的），或者至少共享主目录的底层存储（例如通过 NFS 挂载），那么这一点就不成立了。但 GNOME 和大多数应用程序都不支持这一点，用户同时对同一个主目录最多打开一个图形会话。在物理机器上，这是由 GDM（GNOME 显示管理器）和 D-Bus 强制的。对于 NFS 挂载，并不强制执行，但如果同一个用户在不同的计算机上打开了多个图形会话，某些程序可能会异常。尽管 GApplication 进程唯一性被记录为按会话划分，但在实践中我们可以简单地说它是按用户划分。

- 正确配置 `GtkApplication` 对象，例如赋予应用程序 ID；

- 将回调连接到某些信号⁴，例如在需要时创建 `EditWindow`（编辑窗口）；

- 实现应用程序级别的 GAction。`GAction` 是 GIO 的一个类，代表用户可以触发的操作。应用程序范围的操作例如退出应用程序，或打开首选项对话框（因为设置适用于整个应用程序）。

当你启动一个新的 Gtk+ 应用程序时，你可能不会直接看到需要 `GtkApp` 子类的必要，因为 `main()` 函数中的代码加上回调函数仍然很小。但当功能增加并变得更复杂时，在某个时刻将代码移动到 `GtkApplication` 子类是一个好主意。或者创建一个子类。当需要存储额外数据时，子类 特别有用。

## 5.2 EditWindow

`EditWindow` 是 `GtkApplicationWindow` 的子类。我们没有在 schema 中看到它，但 `GtkApplicationWindow` 是 `GtkWindow` 的子类，后者是一个顶级部件。顶级部件不能包含在另一个部件中。`GtkApplication` 包含在 `GtkApplication` 中，但 `GtkApplication` 不是 `GtkWidget` 的子类。

在 schema 中，“1”和“...”符号表示一个 `EditApp` 包含一个或多个 `EditWindow` 对象，且一个 `EditWindow` 恰好由一个 `EditApp` 获取（一个 `EditWindow` 不能包含在多个 `EditWindow` 对象中，反正每个也只有一个 EditApp 实例）。

`EditWindow` 负责创建主 UI，创建其他部件并将它们组装在 `GtkGrid` 容器中。`EditWindow` 做的另一件事是实现对当前窗口有影响的 Action，例如关闭窗口或保存当前文档。在实现 GAction 时，`EditWindow` 将大部分工作委托给包含在 `EditWindow` 中的其他类。

在主窗口顶部通常有一个 `GtkHeaderBar` 显示标题、一些按钮和一个“汉堡菜单”。或者，应用程序也可以拥有传统的菜单和工具栏。

除了标题栏外，`EditWindow` 还创建了一个 `EditStatusbar` 并将其添加到窗口底部。它创建了两个 `GtkPanel`，一个在窗口左侧，另一个在底部（`EditStatusBar` 之上）。每个面板可以包含多个元素。例如，侧边面板包含一个集成的文件浏览器，底部面板可以包含终端或其他东西⁵。

> ⁴ 注意在 GObject 子类中，与其使用 `g_signal_connect()` 等方法将回调连接到父类的信号，不如直接重写虚函数。
⁵ 当前代码实际上已经不再包含 `Panel` 类了，但在早期的版本中是有。在图中添加 `EditPanel` 是为了展示应用程序中面板的可能实现方式。如果你的应用程序只包含一个元素，则不需要一个类，你可以直接将元素添加到窗口中。`geditWindow` 也创建了 `EditNotebook`。

## 5.3 EditNotebook 以及它包含的内容

`EditNotebook` 是 `GtkNotebook` 的子类，显示标签页并包含其内容。在类中，我们可以看到一个标签页是 `GtkGrid`。更准确地说，`EditNotebook` 实际上包含了 `EditView`。但 `EditTab` 可以包含其他部件，例如位于窗口顶部的栏。`editView` 是 `GtkSourceView` 的子类，其本身是 `GtkTextView` 的子类。此外，`GtkSourceView` 库为源代码增加了功能，例如语法高亮。`GtkTextView` 遵循模型-视图-控制器模式。`GtkBuffer` 是模型，即包含数据。

## 5.4 为何以及何时创建 GTK+ 子类

如果我们查看 `EditTab`，它通过组合包含一个 `editView`。`editView` 是 `GtkSourceView` 的子类，因为 `editView` 是 `GtkSourceView`；也就是说，`editView` 操作与 `GtkSourceView` 相同的基础数据。此外，它允许 `EditTab` 将某些工作委托给其他。通常，这正是发生或应该发生的情况。

当 GTK+ 应用程序代码库仍然很小时，例如如果你开始编写一个 `editView` 的等效类，你可以直接在 `EditTab` 中创建一个 `GtkSourceView` 对象，并将 `GtkSourceView` 对象存储在实例变量中。那么在实现新功能时，你可以添加几乎仅使用 `GtkSourceView` 实例的函数。你也可以让静态函数直接接收 `GtkSourceView` 参数而不是 `EditTab` 自参数。你还可以存储只对 `GtkSourceView` 相关函数有用的数据。如果 `EditTab` 很小（例如 500 行代码）并且不包含很多列表变量，没有问题。另一方面，如果 `EditTab` 变得很大（例如超过 2000 行代码），那么很可能该类应该将其部分工作委托给新类；在我们的案例中，就是 `editView`。注意，一个类有 2000 行代码可能是可以的，对于何时应该划分并没有明确的界限。但如果生成的 `editView` 类至少包含数百行非模板代码，那么进行重构可能是一个好主意。

面向对象编程的核心是将数据和行为封装在一起，并将工作委托给其他类。当我们想要给现有类添加更多行为以及可能与新增行为相关的额外数据时，类继承是合理的。`editView` 是 `GtkSourceView` 的子类，因为 `editView` 是 `GtkSourceView`；也就是说，`editView` 操作与 `GtkSourceView` 相同的基础数据。此外，它允许 `EditTab` 将某些工作委托给其他。
工作，目标是拥有更小、更易于管理的类。更小体现在方面：代码更少，实例变量更少。

因此，在 GTK+ 应用程序生命周期内，程序员经常需要重构代码，创建新类，委托更多工作。当应用程序代码移动到底层库时，可能会发生相反的情况；例如，如果 GeditView 的所有功能都添加到 GtkSourceView 类中；在这种情况下，Gedit 子类就再没有意义了。

## 5.5 复合控件 (Composite Widgets)

复合控件是容器，它们已经将一组有用的子控件封装在一个良好的包中。实现一个复合控件是简单的⁶，你只需要：

- 1. 派生一个容器，如 GtkGrid、GtkBin 或 GtkWindow；
- 2. 在类的构造函数中，创建子控件并将它们添加到容器中。

在 gedit 的类架构中，复合控件是 GtkGrid（GeditPanel 和 GeditTab）以及 GeditWindow 的子类。

GeditWindow 是 GtkBin 的间接子类，因此它最多只能包含一个子控件。这就是为什么 GeditWindow 使用 GtkGrid 作为其子控件，以便 GtkGrid 可以反过来包含所有的窗口元素。

默认情况下，GeditTab 只有一个子控件，即包含 GeditView 的 GtkScrolledWindow。但 GeditTab 有一个函数可以在顶部添加 GtkInfoBar，用于显示错误消息等。

因此，GtkGrid 是一个通用容器，它最初不包含任何子控件，而复合控件是一个特殊的容器，它已经包含了特定的子控件。编写复合控件是编写应用程序的一种方便方法。

> ⁶一旦你知道了如何对 GObject 类进行派生。

## 第四部分

## 扩展阅读

## 第6 章

## 扩展阅读

到这里，你应该已经了解 GLib 核心和 GObject 的基础知识。你不需要了解 GLib 核心和 GObject 的*一切*就可以继续学习，至少具备基本的理解就能让你更轻松地学习 GTK+ 以及 Gio（即基于 GObject 的库）。

## 6.1 GTK+ 和 GIO

GTK+ 和 GIO 可以并行学习。
你应该能够使用 GIO 中的任何 GObject 类，只需阅读类描述并快速浏览函数列表，即可了解该类提供了哪些功能。其他有趣的内容中，GIO 包括：

- GFile 用于处理文件和目录。
- GSettings 用于存储应用程序设置。
- DBus - 用于 D-Bus 进程间通信系统的高级 API。
- GSubprocess 用于启动子进程并与它们异步通信。
- GCancellable、GAsyncResult 和 GTask 用于使用或实现异步和可取消的任务。
- 许多其他功能，带有 I/O 流、网络支持或应用程序支持。

对于使用 GTK+ 构建图形化应用程序，不要恐慌，参考文档有一份“入门指南”（Getting Started guide），可以通过 Devhelp 获取，或在网上访问：`https://developer.gnome.org/gtk3/stable/`

读完“入门指南”后，快速浏览整个 API 参考文档，以熟悉可用的控件、容器和基类。某些控件拥有庞大的 API，因此也有一些外部教程，例如针对 GtkTextView 和 GtkTreeView 的。查看文档页面：`http://www.gtk.org`

还有关于各种 GLib/GTK+ 主题的系列小型型教程：
https://wiki.gnome.org/HowDoI

## 6.2 编写自己的 GObject 类

第 4 章解释了如何使用现有的 GObject 类，这对于学习 GTK+ 非常有用，但它没有解释如何创建你自己的 GObject 类。编写自己的对象允许拥有引用计数，你可以创建自己的属性和信号，你可以实现接口，重写虚拟函数（如果虚拟函数未与信号关联）等。

正如第 4 章开头介绍的那样，如果你想了解关于 GObject 的更深入的信息，可以查看 `https://developer.gnome.org/object/` 参考文档中的“Concepts”和“Tutorial”章节。

## 6.3 构建系统 (Build System)

对于在不同系统中安装应用程序，基础的 Makefile 是不够的。需要更复杂的解决方案：Autotools 和 Meson。

GNOME 和 GTK+ 历史上使用 Autotools，但截至2017 年的一些模块（包括 GTK+）正在迁移到 Meson。对于新项目，推荐使用 Meson。

### 6.3.1 Autotools

Autotools 由三个部分组成：Autools、Automake 和 Libtool。它基于 shell 脚本和 make。

宏用于各种用途（用户文档、代码覆盖率等）。关于该主题的最新书籍是 John Calcote 写的 Autotools。Autotools 以困难著称。

### 6.3.2 Meson

Meson 是一种新的构建系统，比 Autotools 更容易学习，而且构建更快。一些 GNOME 模块已经在使用 Meson。更多信息请访问：
http://mesonbuild.com

## 6.4 编程最佳实践

建议遵循 GNOME 编程指南¹。
以下列表与 GLib/GTK+ 无关，但对任何项目都有帮助。编写高质量的代码对于防止错误和长期维护软件非常重要。

- *Code Complete*，Steve McConnell 著。
- *Object-Oriented Design Heuristics*，Arthur Riel 著。

> ¹尽管 *Code Complete* 由微软出版社出版，这本书与微软无关。作者有时解释与开源、Linux 相关的内容，人们可能会

# 参考文献

- [1] Brian KERIGNAN 和 Dennis RITCHIE, *C语言语言*, 第二版，Prentice Hall, 1988.
- [2] Arthur RIEL, *Object-Oriented Design Heuristics*, Addison-Wesley, 1996.
- [3] GAMMA E., HELM R., JOHNSON R., VLISSIDES J., *设计模式: 面向对象软件元素*, Addison-Wesley, 1994.
- [4] Steven SKIENA, *算法设计手册*, 第二版，Springer, 2008.
- [5] Paul ABRAHAMS, *给急迫者的Unix*, 第二版，Addison-Wesley, 1995.
- [6] Scott CHACON, *Pro Git*, https://git-scm.com/book
- [7] John CALCOTE, *Autotools – GNU Autoconf 和 Libtool 的实实践者指南*, No Starch Press, 2010.
- [8] Steve MCCONNELL, *Code Complete – 软件构造的实践手册*, Microsoft Press, 2004.
- [9] GTK-Doc 手册, https://developer.gnome.org/gtk-doc-manual/
- [10] GObject Introspection, https://wiki.gnome.org/Projects/GObjectIntrospection
- [11] GNOME 编程指南, https://developer.gnome.org/programming-guidelines/stable/

