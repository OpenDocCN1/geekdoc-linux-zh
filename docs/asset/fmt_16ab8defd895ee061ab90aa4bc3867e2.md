
### 6.2.3 Makefile 模板

`automate` 工具从 `Makefile.am` 构建 `Makefile.in`，该文件由以下定义组成：

- 要编译的程序。
- 头文件和库的要求。
- 当前目录中需要通过 `make install` 安装的文件，以及安装到哪里。
- 任何需要的子目录。

### 顶层 Makefile.am

这是示例程序的顶层 `Makefile.am`：

```makefile
## Process this file with automate to produce Makefile.in

SUBDIRS = src pixmaps po

desktopdir = $(datadir)/applications

desktop_in_files = example.desktop.in

desktop_DATA = $(desktop_in_files:.desktop.in=)

@INTLTOOL_DESKTOP_RULE@
```

```makefile
EXTRA_DIST = example.desktop.in \
inttool-extract.in \
inttool-merge.in \
inttool-update.in

DISTCLEANFILES = inttool-extract \
inttool-merge \
inttool-update
```

```makefile
clean-local:
rm -f example.desktop
rm -f po./inttool-merge-cache
```

在在顶部是 `SUBDIRS`，其他子目录应该是合理的。请注意，如果你向源码分发中添加了目录，你需要在 `configure.ac` 和顶层 `Makefile.am` 中添加它。

`example.desktop` 中的菜单项定义（见第 6.3 节）来自 `example.desktop.in`。你需要更多关于如何自动化的定义来生成相应的 Makefile：

- 1. 将 `desktop` 设置为安装目录。`automate` 知道以 `ar` 结尾的安装目录变量。
- 2. `_inttool_files` 列表设置了文件传递给 `example.desktop.in` 的输入文件。
- 3. `_DAFF` 后缀表示该文件没有进一步的编译或处理。然而，你可能会被这部分搞困惑：

```
$($desktop_inttool_files:=.desktop)
```

这意味着“扩展 `$desktop_inttool_files`，但将 `.desktop.in` 替换为 `.desktop`”。
- 4. `@INTLOOL_DESKTOP_RULE` 插入 `inttool` Makefile 规则，将 `.desktop.in` 转换为 `.desktop`。关于 `gettext` 和 `inttool` 的更多信息，请参见第 6.5 节。

接下来 `Makefile.am` 中的下一个是 `EXTRA_DIST`，它是在打包源码分发时要包含的文件列表（标准文件列表见第 6.2.7 节）。

`DISTCLEANFILES` 变量是运行 `distclean` 时要删除的文件列表。

最后，有一个普通的 `make` target `clean-local`，用于删除从模板生成的文件，并将 `automate` 和 `autoconf --clean-local` 作为标准目标的依赖（列表见第 6.2.10 节），因此，运行 `make clean` 会执行 `clean-local`。

> 注意
> 诚实地说，你应该使用 `CLEANFILES` 来制作 `make clean` 序列，就像 `DISTCLEANFILES` 一样。这种稍微不传统的方法是为了教学目的。

# GNOME 2 官方开发者指南

### 源码目录 Makefile.am

这是 `src/Makefile.am`，使用 `automate` 生成 `Makefile.in`：

```makefile
## INCLUDES = -DGNOMELOCATEDIR=\*"\$$(datadir)/locale/*" \
-DG_GNOM_DOMAIN=\*"Example*" \
-I$(top_srcdir) \
$ (GNOME_CFLAGS)
```

### 6.2.3 Makefile 模板

```makefile
LIBS = $(GNOME_LIBS)

bin_PROGRAMS = example

example_SOURCES = main.c
```

标准变量 `INCLUDE` 包含了预处理器选项，例如包含路径和宏定义：

- `GNOMELOCALEDIR` 是本地化文件的最终目标（注意第一个和最后一个引号前的反斜杠）。
- 你在第 1.4.6 节见过 `G_LOG_DOMAIN`（用于消息日志）。
- `-IS$(top_srcdir)` 包含了顶层分发目录，以便你的程序可以包含 `config.h`。
- `$(GNOME_CFLAGS)` 包含了 GNOME 的选项。记得 `configure.ac` 将 `GNOME_CFLAGS` 输出为 `pkg-config --flags` 命令的输出。

`LIBS` 是链接器对象的标准变量。`GNOME_LIBS` 来自 `configure`，就像上面提到的 C flags一样。

通过这些选项，你必须指定要构建的程序、安装位置以及编译的源码。`bin` 组件使得 `make install` 应将可执行文件放在用户配置的二进制目录，而 `_PROGRAMS` 表示链接器必须从程序对象文件中创建程序。

`example_SOURCES` 设置告诉 `automate` 从一组源文件为程序形成目标。它是一个程序名；`_SOURCES` 是另一个特殊后缀，表示接下来的源文件是 `example` 的基础。`automate` 工具定义了从这些源文件创建对象文件的规则。

### Pixmap 目录 Makefile.am

`pixmaps/Makefile.am` 展示了创建一个 Makefile 来将文件复制到用户配置的目录是多么简单：

```makefile
# 使用 automate 处理此文件以生成 Makefile.in

pixmapsdir = $(datadir)/pixmaps

pixmaps_DATA = example.png
```

### 6.2.4 额外工具

如果你想用 GNU `gettext` 支持本地化，运行 `gettext` 在你的分发中设置基础设施。其中，该程序初始化用于翻译文件的 `po` 目录。

你可以使用 `inttoolize` 为 `inttool-utilities` 添加支持。此设置程序对于转换 GConf `.schemas` 文件、菜单项 `(.desktop)` 和 GnomeVFS `.keys` 文件是必要的。关于如何使用 `getintl` 和 `inttoolize`，请参考第 6.5 节。

要构建你的动态库，运行 `libtool` 将 `libtool` 添加到你的分发中。参考 `libtool` info 页面了解如何将其到你的源码中。

### 6.2.3 Makefile 模板

# 6.2.5 aclocal 和 m4

在处理 `Makefile.am` 和 `configure.ac` 中的宏之前，你必须运行 `aclocal` 从系统库中收集宏定义并放入 `aclocal.m4`。在理想的系统中，你不需要提供任何参数，因为 GNOME 运行

```
aclocal -I /opt/gnome
```

警告：不要忘记 `-I` 和路径 之间的空格。

# 6.2.5 aclocal

在处理 `Makefile.am` 和 `configure.ac` 中的宏之前，你必须运行 `aclocal` 从系统库中收集宏定义并放入 `aclocal.m4`。在理想的系统中，你不需要提供任何参数。

### 6.2.6 autoheader

在处理 `Makefile.am` 和 `configure.ac` 中的宏之前，你必须运行 `aclocal` 从系统库中收集宏定义并放入 `aclocal.m4`。在理想的系统中，你不需要提供任何参数。

### 6.2.7 automake 和标准文件

要构建你的动态库，运行 `libtool` 将 `libtool` 添加到你的分发中。参考 `libtool` info 页面了解如何将其到你的源码中。

```
automake --missing
```
