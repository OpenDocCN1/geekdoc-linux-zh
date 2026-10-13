
图 21.1 KDE 的 KDevelop 是适用于 Linux 的快速原型设计和客户端构建工具。

按下回车键后，KDevelop 设置向导会运行几个简短的向导对话框，用于设置并确保构建环境稳定。然后你必须再次运行 `develop`（可以通过命令行或点击桌面面板“编程”菜单下的该项目来实现）。你将看到 KDevelop 的主窗口，并可以通过选择 KDevelop 的项目菜单并点击“新建（New）”菜单项来启动项目。

你可以通过逐步向导对话框来开始构建项目。当你点击“创建（Create）”按钮时，KDevelop 会自动生成 KDE 客户端源码目录中通常的所有文件（包括创建依赖关系并构建客户端二进制文件的配置脚本）。要测试你的客户端，你可以点击“构建（Build）”菜单项（或按 F8），或者直接点击“执行（Execute）”菜单项（或按 F9）。你可以使用 KDevelop 创建 KDE 客户端、`konqueror`浏览器的插件、KDE `kicker`面板小部件、KDE 桌面主题、基于 QT 库的客户端，甚至是 GNOME 的 程序。

## Trolltech 的 QT Designer

与 KDevelop 相关且包含在 Fedora Core 中的一个开发环境是 Trolltech 的 QT Designer。你可以使用此程序为跨平台应用程序构建用户界面“表单”。QT Designer 拥有复杂的界面，支持绘制窗口、按钮和其他客户端控件。你可以这样从终端窗口的命令行启动 QT Designer：

```
$ designer &
```

你也可以通过点击“更多编程工具（More Programming tools）”菜单下的菜单项启动原型设计环境。QT Designer 主窗口（如图 21.2 所示）提供了快速构建和预览图形化客户端的工具。在创建一个存放项目文件的目录后，通过选择“文件（File）、新建（New）”菜单创建一个新项目。然后，你可以选择 C++ 项目并以以 `.pro` 结尾的名字进行保存。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_750_0.png)

图 21.2 Trolltech 的 QT Designer 与 KDevelop 一样是适用于 Linux 和 X 的强大的原型构建工具。

接下来，你可以使用“文件（File）”菜单添加文件，但这次你需要选择一个窗口、小部件或布局，取决于你想添加到项目中的图形化界面。在设计完项目的 GUI 后，你可以使用“预览（Preview）”菜单预览你的设计。如果你已经添加了足够的必要代码，还可以测试新客户端的构建情况。首先导航到你的项目文件夹（使用 `cd` 命令），然后使用 `make` 和 `make` 命令，如下：

```
$ make -o Makefile myproject.pro
$ make
$ ./myproject
```

## 在 GNOME 中开发的 Glide 客户端

如果你倾向于使用 GNOME 和 GNOME 开发工具，Glade GTK++ GUI 构建器（`glade-2` 客户端）可以在构建项目基础骨架时为你节省精力和精力。你可以从桌面面板的“编程”菜单或从终端窗口的命令行启动 `glade-2`，如下：

```
$ glade-2 &
```

## 第 21 章 用于 Fedora 的 C/C++ 工具

> 提示

从 Glade 帮助中点击“内容（Contents）”菜单项以阅读构建客户端的步骤指南。

当你启动 Glade 时，会创建一个名为 Projects 的目录，你会看到主窗口（见图 21.3），它显示了一个新 X 客户端的框架。你可以在 http://glade.net 找到入门教程。使用这些元素创建一个应用程序并调优你的新客户端界面。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_751_0.png)

图 21.3 GNOME 客户端可以构建和预览图形化界面。

当你用 KDevelop 设置好项目后，就可以进行配置、构建和安装了。要开始该过程，执行：

```
$ ./autogen.sh
```

当你完成客户端构建后，可以在项目菜单中选择“源码（Source Code）”，Glade 将生成必要的脚本。

```
# make install
```

你需要使用这些快速原型设计工具为你的 KDE 或 GNOME 客户端填充代码。但 KDevelop、`designer` 和 `glade` 可以节省精力和。

## 相关 Fedora Linux 命令

- 在 Linux 上使用 C 和 C++ 编程时，你会使用以下许多命令：

- `ar`: GNU 归开发工具

- `as`: GNU 汇编器

- `autoconf`: GNU 配置脚本生成器

- `cervisia`: 一个为 CVS 项目提供图形界面的 KDE 客户端

- `CVS`: 项目版本控制系统

- `designer`: 适用于 QT 库和 X 的 Trolltech 图形原型设计工具

- `gcc`: GNU C/C++ 编译器系统

- `gdb`: GNU 交互式调试器

- `glade-2`: 构建 GTK+ 客户端的 GNOME 图形开发环境

- `gprof`: GNU 程序分析器

- `develop-`: 用于构建 KDE、GNOME 或终端客户端的 KDE C/C++ 图形开发环境

- `make`: Gnome 项目管理命令

- `patch`: Larry Wall 的源码还原工具

- `pmake`: BSD 项目管理命令

- `rc`: 用于管理项目文档的程序集

- `splint`: C 源文件检查器

- `xkmmf`: 一种用于 X 的脚本，用于构建 X 客户端创建本地 Makefile

如果你对学习更多 C 和 C++ 感感兴趣，你应该以下书籍：

- 《Sams Teach Yourself C in 21 Days》，Peter Aitken 和 Bradley Jones 著，Sams Publishing

- 《Sams Teach Yourself C++ for Linux in 21 Days》，Jesse Liberty 和 David B. Horvath 著，Sams Publishing

- 《How to Program》和《C++ How to Program》，均为 Harvey M. Deitel 和 Paul J. Deitel 著

- 《The C Programming Language》，Brian W. Kernighan 和 Dennis M. Ritchie 著

- 《The Annotated C Reference Manual》，Margaret A. Ellis 和 Bjarne Stroustrup 著

- 《Programming in ANSI C》，Stephen G. Kochan 著

## 参考

http://gcc.gnu.org/java/compile.html—更多关于 egcs Java 支持的信息

http://www.gnu.org/software/autoconf/autoconf.html—更多关于 GNU 项目的 autoconf 工具以及如何构建可移植软件项目的信息

http://sourcenav.sourceforge.net/~—Red's navigator 客户端主页，这是一种源代码分析工具

http://www.trolltech.com/products/qt/tools.html—Trolltech 关于 QT Designer 以及你可以在 Fedora 上使用的多种编程自动化工具（包括翻译器）的页面

http://glade.gnome.org/~—Glade GNOME 开发者工具主页

http://www.kdevelop.org/—托管 KDE 项目最新版本 KDE 图形开发环境 Kdevelop 的网站

# 第 22 章

## Shell 脚本

## 本章内容

- 本书包含的 Shell

- Shell 命令行

- 编写、创建和执行 Shell 脚本的基础

- 使用 bash 创建并执行简单的 Shell 程序

- 在 Shell 脚本中使用变量

- 位置参数

- 内置变量

- 特殊字符

- 表达式比较

- 迭代语句

- 条件语句

- break 和 exit 语句

- 在 Shell 脚本中使用函数

- 参考

许多计算机用户通过桌面的外观和易用性来判断操作系统的质量。各种商用 Linux 发行版（如 Red Hat, Inc.）以及开发者项目（如 GNOME 和 KDE）在为 Linux 操作系统制作凝聚、一致的软件界面方面取得了巨大进展。然而，除了嵌入式设备实现外，所有的 Linux 发行版都提供 Linux 内核，可能还带有一个基于文本的控制台，或者内核的命令行界面。

点击式界面的粉丝可能不习惯熟练使用命令行。Linux 命令行被称为 shell，是 Linux 操作系统的不可或缺且本质的组成。在某些情况下或特定的硬件上，shell 可能是与 Linux 交互的唯一方式（例如通过拨号或网络远程访问服务器）。
