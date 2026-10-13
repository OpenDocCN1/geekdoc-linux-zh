
# 额外资源

UNIX 和 Linux 是基于 C 语言构建的。C 是一种平台无关的编译型、基于函数和数据结构的过程化语言。如果你对学习更多 C 和 C++ 感兴趣，你应该寻找以下书籍：

- 《Teach Yourself C in 21 Days》，Peter Aitken 和 Bradley Jones 著，Sams Publishing
- 《Teach Yourself C++ for for Linux in 21 Days》，Jesse Liberty 和 David Horvath 著，Sams Publishing
- 《C How to Program》，Harvey M. Deitel 和 Paul J. Deitel 著，Deitel Associates
- 《The Programming Language》，Brian W. Kernighan 和 Dennis Ritchie 著，Prentice Hall
- 《Annotated C++ Manual》，Bjarne Stroustrup 和 Stephen E. Kochan 著，Sams Publishing
- 《Programming in ANSI Base Document》

## 参考

- http://gcc.gnu.org/java/compile.html—关于 GCC 支持的更多信息
- http://www.gnu.org/software/autoconf/autoconf.html—关于 GNU 项目的 autoconf 工具以及如何构建可移植项目的更多信息
- http://sourceforge.net—Red Hat 导航主页，一种源码分析
- http://www.trolltech.com/products/tools.html—Trolltech 关于 Qt Designer 以及若干个你可以配合使用的自动化工具（包括翻译器）的页面
- http://glade.gnome.org—Glade 开发者工具主页
- http://www.kdevelop.org—托管 KDevelop 最新版本 KDE 图形开发环境的网站

# 第 34 章：Mono

在 Linux 上使用 C 和 C++ 编程时，你将使用这些命令中的许多：更偏于使用 GNOME 及其开发工具，那么 Glade GTK+ GUI 构建器（`glade-2`）可以在构建程序的基本骨架时为你节省时间和精力。你可以再次使用“文件（File）”菜单来添加文件，但这次你需要根据你想要添加到项目中的图形界面，选择窗口、小部件（`widget`）或对话框。在设计完程序的 GUI 后，你可以使用“预览（Preview）”菜单预览你的设计。如果你已经添加了足够的必要代码，还可以测试新客户端的构建版本。你可以导航到项目文件夹（使用 `cd` 命令），然后使用 `qmake` 和 `make` 命令进行构建，如下所示：

```
$ qmake -o Makefile myproject.pro
$ make
$ ./myproject
```

## 用于 GNOME 开发的 Glade 客户端

从桌面面板的“编程（Programming）”菜单或从终端窗口的命令行启动 Glade-2，如下：

```$ glade-2 &```
当启动 Glade 时，你的主目录下会创建一个名为 Projects 的目录，你会看到一个主窗口，以及两个浮动的调板和属性窗口（参见图 33.3，该图显示了一个主窗口添加了日历小部件的基本 GNOME 客户端）。你可以使用 Glade 的“文件（File）”菜单保存空项目，然后通过从“调板（Palette）”窗口点击并添加用户界面元素来开始构建你的客户端。例如，你可以先点击调板窗口的 Gnome 按钮，然后点击你新客户端的主窗口。一个带有菜单和工具栏的窗口就会出现——这就是新 GNOME 客户端的基础框架！

![](img/c4a0ea5ab3561ff33a8da88887702720_893_0.png)

**图 33.3** GNOME Glade 客户端可用于为自定义 GNOME 程序构建和预览图形界面。

当你完成客户端构建后，可以从项目窗口“文件（File）”菜单选择“构建源代码（Build Source Code）”，Glade 会为项目构建必要的源代码和脚本。然后你可以执行项目目录下的 `autogen.sh` 脚本来构建项目脚本，如下：

```
$ autogen.sh
```

在设置项目后，对于 KDevelop 项目，你已经准备好配置、构建和安装你的项目。要开始该过程，请执行以下：

```bash
# make install
```

在使用快速原型设计工具时，你必须添加代码为你的新 KDE 或 GNOME 客户端填充操作功能。但 develop、designer 和 glare 可以帮助节省精力和精力。使用这些环境创建一个可运行的应用程序，然后微调你新客户端的用户界面。

## 相关的 FEDORA 和 LINUX 命令

在 Linux 上使用 C 和 C++ 编程时，你将使用这些命令中的许多：

- `ar`—GNU 归档工具
- `as`—GNU 汇编器
- `autoconf`—GNU 配置脚本
- `CVS`—一个提供图形界面的 KDE 客户端
- `cv`—一个项目版本控制系统
- `designer`—Trolltech 用于 Qt 库的图形原型设计工具
- `gcc`—GNU/C++ 编译器
- `gdb`—GNU 调试器
- `glade-2`—用于构建 GTK+ 客户端的 GNOME 图形开发环境
- `gprof`—GNU 性能分析器
- `kde`—用于构建 GNOME 或终端的 KDE C/C++ 开发环境
- `make`—一种 BSD 项目管理命令
- `patch`—Larry Wall 的补丁实用
- `pmake`—一种管理命令
- `rcs`—一组用于管理程序的程序
- `split`—源文件检查器
- `xmake`—一个用于 X 的 shell 脚本，用于创建本地 makefile
