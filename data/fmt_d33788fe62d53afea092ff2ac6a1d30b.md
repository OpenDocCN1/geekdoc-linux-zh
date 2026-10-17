
Ubuntu 包含许多用于在 X 会话期间使用的图形化原型设计和开发环境。如果你想为 KDE 或 GNOME 构建客户端软件，你可能会发现 `KDevelop`、`Qt Designer` 和 `Glade` 程序非常有帮助。你可以使用这些程序中的每一个来构建交互式 `windowing` 客户端的图形框架，并且可以使用它们中的每一个自动生成支持程序自定义界面的必要代码骨架。

## 使用 KDevelop 客户端

你可以从应用程序菜单启动 `KDevelop` 客户端（如图 26.1 所示），或从终端窗口的命令行像这样启动：

```
$ kdevelop &
```

按下 Enter 后，`KDevelop` 设置向导会运行，并引导你完成几个简短的向导对话框，以设置并确保稳定的构建环境。然后你必须再次运行 `kdevelop`（从命令行或通过单击桌面面板的 Programming 菜单下的菜单项）。然后你将看到主 `KDevelop` 窗口，并可以通过选择 `KDevelop` 的 Project 菜单并单击 New 菜单项来开始你的项目。

![](img/8f9e74e2b343ff525bebfb720a3d8441_650_0.png)

## FIGURE 26.1 KDE's KDevelop is a rapid prototyping and client-building tool for use with Linux.

你可以开始通过逐步操作向导对话框来构建你的项目。当你点击 Create 按钮时，`KDevelop` 会自动生成通常存在于 KDE 客户端源目录中的所有文件（包括 `configure` 脚本，该脚本检查依赖项并构建客户端的 `makefile`）。要测试你的客户端，你可以先点击 Build 菜单的 Make 菜单项（或按 `F8`），也可以直接点击 Execute 菜单项（或按 `F9`），客户端会随之自动构建。你可以使用 `KDevelop` 来创建 KDE 客户端、`Konqueror` 浏览器的插件、`KDE` `kicker` 面板小程序、`KDE` 桌面主题、基于 `Qt` 库的客户端，甚至是 GNOME 的程序。

## The Glade Client for Developing in GNOME

如果你更喜欢使用 GNOME 及其开发工具，`Glade` `GTK+` `GUI` 构建器可以帮助你在为程序构建基本骨架时节省时间和精力。你可以从桌面面板的 Programming 菜单启动 `Glade`。

当你启动 `Glade` 时，会在你的主目录中创建一个名为 `Projects` 的目录，并且你会看到一个主窗口，以及两个浮动的 Palette 和 Properties 窗口（见图 26.2），其中显示了一个基本 GNOME 客户端，其主窗口中添加了日历部件）。你可以使用 `Glade` 的 File 菜单保存空白项目，然后通过点击并从 Palette 窗口添加用户界面元素开始构建你的客户端。例如，你可以先点击 Palette 窗口的 Gnome 按钮，然后点击创建你新客户端的主窗口。一个带有菜单和工具栏的窗口会出现——这是一个新 GNOME 客户端的基本框架！

![](img/8f9e74e2b343ff525bebfb720a3d8441_651_0.png)

FIGURE 26.2 You can use the GNOME Glade client to build and preview a graphical interface for a custom GNOME program.

### Related Ubuntu and Linux Commands

你在为 Linux 编程 C 和 C++ 时会用到以下许多命令：

- `ar`—The GNU archive development tool
- `as`—The GNU assembler
- `autoconf`—The GNU configuration script generator
- `cvs`—A KDE client that provides a graphical interface to a CVS project
- `cvs`—A project revision control system
- `designer`—Trolltech’s graphical prototyping tool for use with Qt libraries and X
- `gcc`—The GNU C/C++ compiler system
- `gdb`—The GNU interactive debugger
- `glade 2`—The GNOME graphical development environment for building GTK+ clients
- `gprof`—The GNU program profiler
- `kdevelop`—The KDE C/C++ graphical development environment for building KDE, GNOME, or terminal clients
- `make`—A GNU project management command
- `patch`—Larry Wall’s source patching utility
- `splint`—The C source file checker
- `svn`—The Subversion revision control system

### Reference

如果你有兴趣了解更多关于 C 和 C++ 的知识，你应该查找以下书籍：

- Sams Teach Yourself C in 21 Days, by Peter Aitken and Bradley Jones, Sams Publishing
- Sams Teach Yourself C++ for Linux in 21 Days, by Jesse Liberty and David B. Horvath, Sams Publishing
- C How to Program and C++ How to Program, both by Harvey M. Deitel and Paul J. Deitel, Deitel Associates
- The C Programming Language, by Brian W. Kernighan and Dennis M. Ritchie, Prentice Hall
- The Annotated C++ Reference Manual, by Margaret A. Ellis and Bjarne Stroustrup, ANSI Base Document
- Programming in ANSI C, by Stephen G. Kochan, Sams Publishing

还有许多优秀的网站提供更多信息：

- `http://gcc.gnu.org/java/compile.html`—More information about GCC’s Java support.
- `http://www.gnu.org/software/autoconf/autoconf.html`—More information about the GNU Project’s autoconf utility and how to build portable software projects.
- `http://www.trolltech.com/products/qt/tools.html`—Trolltech’s page for Qt Designer and a number of programming automation tools (including translators) that you can use with Ubuntu.
- `http://glade.gnome.org`—Home page for the Glade GNOME developer’s tool.
- `http://www.kdevelop.org`—Site that hosts the KDevelop Project’s latest versions of the KDE graphical development environment, KDevelop.

## 第27章：Mono

### 本章内容

- 为什么使用 Mono？
- 命令行上的 Mono
- 在 Mono 库上构建
- 参考

尽管微软将其设计用于 Windows，但微软的 `.NET` 平台已扩展到涵盖众多操作系统。不，这并不是微软罕见地让客户选择最适合其操作系统的迹象——相反，`.NET` 的传播归功于 `Mono` 项目，它是 `.NET` 的免费重新实现，采用 GPL 许可发布。

由于潜在的专利问题，大多数发行版花了很长时间才集成 `Mono`，但现在它已经到来并且运行良好。更重要的是，`Mono` 支持 `C#` 和 `Visual Basic .NET`，以及完整的 `.NET 1.0` 和 `1.1` 框架（以及大部分 `2.0` 框架），使其学习快速且使用高效。

### 为什么使用 Mono？
