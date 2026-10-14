
## 使用 Ubuntu 提供的 C 语言管理工具

注意

上一个示例中的缩进行使用的是制表符（`tabs`），而不是空格。记住这一点非常重要！人很难看出这种区别，但 `make` 可以。如果你首次在 Linux 下开始构建程序时，报告生成了混淆的错误，请检查项目的 `Makefile` 是否使用了制表符和其他正确的格式。

使用前一个示例中的 `myfile`，你可以这样构建程序：

```bash
matthew@seymour:$ sudo make
```

要构建 `Makefile` 的简单组件，你可以在命令行上使用目标定义。要仅构建程序，你可以配合 `skel` 目标使用它，如下：

```bash
matthew@seymour:$ sudo make skel
```

如果你对目标对象的任何元素（例如源文件）进行了任何更改，`make` 会自动重新构建该目标。这一功能是使用 `make` 管理开发项目的便利性之处。要一步构建并安装程序，你可以指定目标 `install`：

```bash
matthew@seymour:$ sudo make install
```

较大的软件项目可能在 `Makefile` 中有许多传统目标，例如：

- `test`——在最终软件上运行特定测试。
- `man`——处理 `man` pages 的 `include` 或 `troff` 文档。
- `clean`——删除任何剩余的对象文件。
- `archive`——清理、存档并压缩整个源代码树。
- `bugreport`——自动收集并维护构建或错误日志的副本。

大型应用程序可能需要数百个源代码文件。编译和链接这些应用程序可能是一个复杂且容易出错的任务。`make` 工具帮助你组织从许多源文件构建复杂应用程序的可执行形式的过程。

## 使用 autoconf 工具配置代码

`make` 命令只是 Ubuntu 包含的几种编程自动化工具之一。还有其他工具，例如 `make`（可触发并行 make）、`cmake`（一种依赖驱动的 `Makefile` 生成器，用于构建 X11 客户端）、`automate` 以及较新的工具之一 `autoconf`，它用于构建用于配置程序源码包的 shell 脚本。

构建以源码形式分发的许多 Linux 软件包需要 GNU 的 `autoconf` 工具。该程序构建一个名为 `configure` 的可执行 shell 脚本，执行该脚本时，会自动检查并根据目标主机（你的 Linux 系统）上安装的软件资源或依赖（例如编程工具、库和相关程序）来定制客户端的源码构建。

许多以源码下载的 Linux 命令和 X 图形客户端包含 `configure` 脚本。要配置源码包、构建软件并安装程序，root 用户可能如下使用该脚本（在解压并进入生成的二进制目录后）：

```
matthew@seymour:- ./configure; make; sudo make install
```

`autoconf` 程序使用名为 `configure.in` 的文件，其中包含了基本的规则集或宏。构建正确的配置脚本还需要 `Makefile` 模板，名为 `Makefile.in`。虽然可以手动创建依赖检查配置脚本，但你可以轻松地完成。

其他 UNIX 系统上可用的 C 和 C++ 编译器。查看 `gcc` 的 `man` 页面或信息以获取选项列表和描述。

> 注意

GNU C 编译器是 GNU 编译器集（GNU Compiler Collection）的一部分，该集合还包括其他语言的编译器。

当使用 `gcc` 编译 C 程序时，编译过程分为几个步骤：

- 1. 首先，C 预处理器会解析文件。为此，它会顺序读取行（包括头文件）并执行宏替换。

> 注意

如果你遵循严格的 ANSI 规则，大多数 C 程序都可以用 C++ 编译器编译。例如，你可以用 GNU C++ 编译器编译标准的 `hello.c` 程序（每个人的第一个程序）。通常，你将文件命名为 `hello.cc`、`hello.C`、`hello.c++` 或 `hello.cxx`。GNU C++ 编译器接受这些名称中的任何一个。

## 图形化开发工具

Ubuntu 包含了许多用于 X 的图形化原型设计和开发环境。如果你想为 KDE 或 GNOME 构建客户端软件，你可能会发现 `Devel`、`Qt Designer` 和 `Glade` 程序非常有帮助。你可以使用这些程序中的每一个为交互式窗口客户端构建图形化框架，并可以使用其中每一个来自动生成支持程序自定义界面所需的骨架代码。

## 使用 KDevelop 客户端

你可以从应用程序的菜单启动 `KDevelop` 客户端（如图39.1 所示），或者从窗口命令行启动，例如：

```bash
mathew@seymour:-$ kdevelop &
```

按下回车键后，将运行 `KDevelop` 设置向导，引导你通过几个简短的向导来设置并确保环境稳定。然后你必须再次运行 `kdevelop`（可以通过命令行运行，也可以通过点击桌面面板“编程”菜单下的项目）。随后你将看到 `KDevelop` 主窗口，并通过选择 `KDevelop` 的项目菜单并点击“新建”菜单项来启动项目。

![](img/e5934b384118c0ba38d424f9d13b7b0a_763_0.png)

图 39.1 KDE 的 Kdevelop 是一种用于 Linux 的快速原型设计和客户端构建工具。

你可以通过逐步对话向导开始构建项目。当你点击 `Create` 按钮时，`KDevelop` 会自动生成 KDE 客户端源目录中通常包含的所有文件（包括检查依赖关系并构建客户端 `Makefile` 的 `configure` 脚本）。要测试你的项目，你可以先点击 `Build` 菜单项（或按 `F8`），或点击 `Execute` 菜单项（或按 `F9`），客户端将自动构建。你可以使用 `KDevelop` 创建 KDE 客户端、`Konqueror` 浏览器插件、`KDE` 面面板、`KDE` 桌面主题、基于 `Qt` 库的客户端，甚至是 GNOME 的程序。

## 用于 GNOME 开发的 Glade 客户端

如果你更喜欢 GNOME 及其开发工具，`Glade GTK+ GUI` 构建器将帮助你节省时间并有效地构建程序的基础骨架。你从桌面面板的“编程”菜单启动 `Glade`。

当你启动 `Glade` 时，你的主目录下会创建一个名为 `Projects` 的目录，你会看到一个主窗口以及两个浮动的调板（`Palette`）和属性（`Properties`）窗口（图 39.2 显示了一个添加了日历小组件的基本 GNOME 客户端）。你可以使用 `Glade` 的 `File` 保存空项目，并通过从 `Palette` 窗口点击并添加用户界面元素开始构建你的客户端。例如，你可以先点击调板上的 `Gnome` 按钮，然后点击创建新客户端的主窗口。会出现一个带有菜单和工具栏的窗口——这是新 GNOME 客户端的基础框架。

![](img/e5934b384118c0ba38d424f9d13b7b0a_764_0.png)

图 39.2 你可以使用 GNOME `Glade` 客户端为自定义 GNOME 程序构建并预览图形界面。

## 参考文献

- `www.cprogramming.com`—一个学习 C 和 C++ 的有用网站。
- `http://gcc.gnu/`—GNU 编译器集的主页。
- `www.gnu.org/software/autoconf/autoconf.html`—关于 GNU 项目的 `autoconf` 实用以及如何构建可移植软件项目的更多信息。
- `http://qt.nokia.com/`—Qt 网站。
- `http://glade.gnome.org`—Glade Gnome 开发者工具的首页。
- `kde.org`—托管 `KDevelop` 项目最新版本 KDE 图形开发环境 `KDevelop` 的网站。
- *The C Programming Language*，Brian W. Kernighan 和 Dennis M. Ritchie 著，Prentice Hall 出。
- *The Annotated C++ Reference Manual*，Margaret A. Ellis 和 Bjarne Stroustrup 著，ANSI Base Document。
- *Programming in ANSI C*，Stephen G. Kochan 著，Sams Publishing 出。
- *Sams Teach Yourself C in 21 Days*，Peter Aitken 和 Bradley Jones 著，Sams Publishing 出。
- *Sams Teach Yourself C++ for Linux in 21 Days*，Jesse Liberty 和 David B. Horvath 著，Sams Publishing 出。
- *C How to Program and C++ How to Program*，Harvey M. Deitel 和 Paul J. Deitel 著，Deitel Associates 出。

本页特意留空

## 第40 章 使用 Mono

## 为什么要用 Mono？

- `MonoDevelop`
