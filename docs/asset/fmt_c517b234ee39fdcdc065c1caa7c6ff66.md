
作为开发者，你可能写过很多非平凡的程序。你熟悉 `make` 和 `Makefile`。也许，你想过为什么 KDE 的 `Makefile` 总是那么大，而你通常只需要 30 行或可能 50 行。这一章讨论了为什么 KDE 的 `Makefile` 这么大，以及你如何无需大量工作就能获得自动构建过程。

# 第 10 章：自动化构建过程

## 10.1 KDE 运行在 Linux 上

KDE 运行在 Linux 上这一事实是 KDE `Makefile` 如此复杂的最重要原因。即使 Linux 并不总是平等的。例如，许多 socket 函数的声明与 Linux/Intel 中的不同。除了这些，KDE 还运行在 FreeBSD、Solaris 和 HPUX 上。用户甚至让它在 IRIX、True64（原 Digital UNIX）以及其他 UNIX 变体上运行。

此外，在 Linux 下存在三个不同的标准 X 变体：`XFree86`、`AcceleratedX` 和 `MetrX`（注：原文可能笔误，应为 Metrix 或类似项，此处保留原意）。在商业 UNIX 变体中，这些 X 服务器是私有协议。

简单来说，KDE 必须可移植的。KDE 通过使用 `autoconf` 和 `automate` 绕过这些困难。

在检索所有信息后，它从 `Makefile.in` 文件在每个目录生成 `Makefile`。这将被 `make` 使用。此外，它在主目录创建一个名为 `config.h` 的文件，该文件应被需要特定系统的源码通过 `#include` 包含。

我们编写 `Makefile.in` 而不是 `Makefile`。然而，即使是 `Makefile.in` 往往也很长且复杂。这就是为什么我们使用另一个工具来自动创建 `Makefile.in`。

## 10.2 automake

`automake` 处理这项任务。它从 `Makefile.am` 生成 `Makefile.in`。通过 `automate` 我们终于达到了想要的位置。它非常简单。查看 `ktsp-0.2.0/Makefile.am`：

```make
SUBDIRS = ktsp po
```

```make
# 不是 GNU 软件包。你可以删除此行，如果
# 我们拥有 GNU 软件包所需的所有文件
AUTOMAKE_OPTIONS = foreign
```

它只有两项。第一个指定 `ktsp-0.2.0` 的子目录。第二个项目说明尽管它根据 GPL 许可，但它并不是真正的 GNU 软件包，不需要自由软件基金会（FSF）的所有文件。就是这样，`automake` 由此生成了 412 行的 `Makefile.in`。

### 10.2 automake

```make
# kde_cgdir cgi 可执行文件应该存放的地方。
# kde_confdir 配置文件应该存放的地方。
# kde_mimed MIME 类型应该存放的地方。
# kde_toolbardir 通用工具栏图标应该存放的地方。
# kde_wallpaperdir 通用壁纸应该存放的地方。
```

```make
#为 Qt 和 KDE 设置包含路径
INCLUDES=$(all_includes)
```

```make
# 声明你想安装的子目录
# 如果没有子目录，请将其注释掉
SUBDIRS=doc
```

```make
###### 这部分非常针对 ktsp 特有
# 你可以在这里添加更多。这一个会被安装
bin_PROGRAMS=ktsp
```

```make
# ktsp 应该编译哪些源。
ktsp_SOURCES=main.cpp ktsp gda.C point.C random.C tspga.C tspio.C
view.C canvas.C tspialog.C graphicdialog.C graph.C graphdisplay.C
actionsdisplay.C runsdisplay.C
```

```make
ktsp_METASOURCE=USE_AUTOMOC
```

```make
# 库搜索路径。
ktsp_LDFLAGS=$(all_libraries) $(RPATH)
```

```make
# 需要链接的库。注意顺序。先是那些
# 依赖于后续库的库。
ktsp_LDADD=$(LIB_KFILE)
```

```make
# 这个选项你可以省略。只有使用 'make dist' 时，
# 才需要它
noinst_HEADERS=ktsp.h gda.h point.h random tspga.h tspio.h view.h
canvas.h tspialog.h graphicdialog.h graph.h graphdisplay.h actionsdisplay.h
-runsdisplay.h
```

```make
# 如果执行 'make distclean'，这些文件会被删除。如果你想在
# 'make clean' 时也删除它们，请使用 CLEANFILES
DISTCLEANFILES=$(ktsp_METASOURCES)
```

```make
# 生成 messages.po。将此文件移动到 ../po/ 并运行 'make merge'，
# -x 是为了跳过 kdelibs 中已经翻译过的消息
messages:
$(XGETTEXT)-C -ki18n -x $(included)/kde.pot $(ktsp_SOURCES) && mv
messages.po=../po/ktsp.po
```

```make
kdelnkdir=$(kde_appdirs)/Applications
kdelnk_DATA=ktsp.kdelnk
```

```make
icondir=$(kde_icondir)
icon_DATA=ktsp.xpm
```

```make
# 仅在这里安装数据。脚本等文件使用 install-exec-local。
```

```make
# 二进制目录已经通过 automake 安装了
# 使用 mkinstaldirs，而不是 \
$(mkinstaldirs) $(kde_minidir)
$(INSTALL,DATA) $(srcdir)/mini-ktsp.xpm $(kde_minidir)/ktsp.xpm
$(INSTALL,DATA) $(srcdir)/run.xpm $(kde_toolbardir)/run.xpm
```

```make
# 移除你在 install-data-local 或 install-exec-local 中安装的所有内容
uninstall-local:
-rm -f $(kde_minidir)/ktsp.xpm
```

开头的注释告诉我们关于 10 个路径的符号名称，在 `Makefile` 中应该使用这些名称，而不是显式编写路径。正因为如此，KDE 可以在不同系统的不同路径下存在且安装仍然能够正常工作。

大多数项目都是显而易懂的。有些项目足够有趣，值得我们仔细观察。在我们指定了子目录、程序名称和源文件后，我们得到了这一行：

```make
ktsp_METASOURCE=USE_AUTOMOC
```

这一行与 Qt 元编译器 `moc` 有关。

源文件必须通过 `moc` 从包含 `Q_OBJECT` 的头文件创建。它可以像其他文件一样被编译。在书开头，我们提到过：

```bash
moc mysource.cpp mysource.h
```

从头文件中创建源文件。如果我们自动化这个过程，我们无法将 `*.cpp` 文件插入到 `Makefile.am`；它们在开始时并不存在。`moc` 工具帮助了我们。它是一个搜索所有 `Q_OBJECT` 头文件的脚本，并将相应的项插入到 `Makefile` 中。

程序本身、程序代码以及 `ktsp.kdelnk` 将通过 `make install` 自动安装。此外，我们想要安装一个小图标（例如在 KPanel 菜单和 KTSp 窗口标题栏中）以及一个工具栏图标。`Makefile.am` 的最后几行为此目的。

查看其他子目录下的 `Makefile.am`。它们都很容易理解。只要你不需要 `automake`/`autoconf` 的其他功能，`Makefile.am` 中的更改都非常简单。稍后我会回到这个文件。

## 10.3 新项目

在大多数情况下，如果你需要其他功能，将会变得困难得多——必须在 `config.h` 和或 `acl.m4` 文件中进行更改。`automake`/`autoconf` 的细节超出了本文范围。所以，如果你想提供给 KDE，这就是你的地址。

事实上，KDE 艺术家欢迎他人加入。如果你有这些技能并想提供给 KDE，这就是你的地址。

我们如何开始一个新项目？最简单的方法是使用现有的项目。最佳做法是下载。

## 10.4 图标和其他文件

除了源代码，KDE 项目还有另一组用于 GUI 的重要文件。你已经学习了翻译和在线。图标是每个程序都需要的 GUI 元素。有一个代表程序本身的图标。我们需要两种变体：用于桌面和面板的普通尺寸；以及用于程序窗口标题栏、面板菜单和任务栏的小尺寸图标。

### 10.4.1 图标和小尺寸图标
