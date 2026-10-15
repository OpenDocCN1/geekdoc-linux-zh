
用于构建 `configure` 程序的工具统称为 GNU autotools。本书仅对这套强大的配置/编译系统进行概述。如需更详细的信息，请参阅 [Vaughan]。

## 6.2.1 概述

使用 GNU autotools 为你的源代码进行配置（outfitting your source code）的通用步骤如下：

1. 在顶层源码目录下创建一个 `configure.ac` 文件。该文件不仅定义了 autotools 的行为，而且通过宏展开创建 `configure` 脚本。
2. 在每个运行编译器或安装程序的子目录下创建一个 `Makefile` 文件。
3. 运行 `gettext` 进行本地化，运行 `inttool` 获取额外支持，运行 `libtool` 构建你的库。
4. 运行 `aclocal` 将库中必要的宏收集到 `aclocal.m4` 文件中。
5. 运行 `autoconf` 为你的包所需的预处理器宏创建 `config.in` 模板。
6. 运行 `automate` 从每个 `Makefile.am` 构建一个不同的 `Makefile.in` 模板。
7. 使用 `autoconf` 对 `configure.ac` 结合 `aclocal` 中的宏运行 `m4` 处理器以创建 `configure` 脚本。

对于大多数源码发行版，你不需要执行这些步骤中的任何一步，因为开发者已经完成了一切工作。然而，如果你拿到开发者代码（例如 CVS），情况就会不同，因为你可能需要其他几个包和完整的 autotools 才能达到运行 `./configure` 的程度。`configure` 脚本会检查你的系统是否满足构建该包所需的必要条件。如果成功，`configure` 会从 `.in` 模板创建多个文件（例如从 `config.in` 创建 `config.h`）。

注意，GNU autotools 系统中的 Makefile 同样来自 `.in` 模板，因此是可以丢弃的。此外，一个名为 `automake` 的程序会生成 `Makefile.in` 模板和 `Makefile.am` 文件。如果一切顺利，`configure` 会在所有相关的子目录下留下 `Makefiles`。顶层 `Makefile` 包含 `all`、`install` 和 `distclean` 等目标；运行 `make` 来构建其中任何一个目标也会在每个子目录的 `Makefile` 上运行。

鉴于目前对 autotools 的简化描述，你可以看到这个过程远非易事。这些工具（以及它们生成的文件）协同工作，形成一个复杂且强大的系统，就像时钟里的齿轮一样。与其进行数百页的解释，本书包含了一份日常 autotools 的配方。我们讨论的示例是一个名为 `example` 的虚构 GNOME 包。它的发行树包含源码的 `src` 子目录和包含图像数据的 `pixmaps` 子目录。

### 6.2.2 configure.ac

配置过程的核心是 `configure.ac`，它位于软件发行版的顶层目录下。有几个工具读取并处理 `configure.ac` 内部的调用，包括 `autoconf`（用于创建 `configure` 脚本）。

注意：`configure.ac` 这个名字出现的时间并不长，你可能会看到 `configure.in`。你可能会觉得 `m4` 宏语法有些奇怪。你应该始终记住，`configure.ac` 不包含规则，而是由 `m4` 展开为 shell 脚本的宏调用。

当你查看 `configure.ac` 时，请记住以下规则：

- 不要在宏名和它的左括号之间留有空格。
- 不要在宏参数与其逗号分隔符之间留有空格，也不要在最后一个参数和右括号之间留有空格。
- `m4` 通常会处理其输入，直到没有可展开的内容为止。
- `m4` 不处理方括号 `[ ]` 内的任何内容。
- 注释以井号 `#` 开头。

```bash
# initialization ==========

AC_INIT(Example, [0.1], [example@example.com], [example])

AC_CONFIG_SRDIR([src/main])

AC_CONFIG_HEADER(config.h)

AM_INIT_AUTOMAKE

AM_MAINTAINER_MODE

# 基础编译器设置 ==========

AC_PROG_CC

AC_HEADER_STDC

# 处理某些本地化 ==========

AM_TEMPLATE((GETTEXT_PACKAGE), [Package name for gettext])

GETTEXT_PACKAGE=QUOTED(GETTEXT_PACKAGE, "GETTEXT_PACKAGE")

AC_SUBST(GETTEXT_PACKAGE)

ALL_LANGUAGES="de es"

AM_GLIB_INIT_GETTEXT

AC_PROG_INIT

# 导出编译器/链接器选项 ==========

AC_SUBST(CFLAGS)

AC_SUBST(CPPFLAGS)

AC_SUBST(DFLAGS)

# 查找 GNOME ==========

GNOME_MODULES="libgnomeui-2.0 >= 2.0.0"

PKG_CHECK_MODULES(GNOME, $GNOME_MODULES)

AC_SUBST(GNOME_CFLAGS)

AC_SUBST(GNOME_LIBS)

# 生成文件 ==========

AC_CONFIG_FILES(

  Makefile

  src/Makefile

  pixmaps/Makefile

  po/Makefile.in

)

AC_OUTPUT
```

`configure.ac` 文件以下展开展开：

```bash
AC_INIT(name, version, email, short_name)
```

其中 `name` 是包的全名，`version` 是版本号，`email` 是联系地址，`short_name` 是包的主程序。括号中的每个项都用于禁用进一步展开。对于 GNOME 应用，请使用传递给 `gnome_program_init()` 的参数。

```bash
AC_CONFIG_SRDIR(path) 定义源目录；它定义了实际源码目录中文件的相对路径。
```

```bash
AC_CONFIG_HEADER(header_file) 指定 configure 生成的 C 预处理器目标文件。通常，header_file 是 config.h。
```

下一次部分是 `AM_INIT_AUTOMAKE`，用于初始化 autotools，以及 `AM_MAINTAINER_MODE` 用于启用某些选项。现在你准备好进行编译器设置了。

```bash
AC_PROG_CC

AC_HEADER_STDC
```

下一节使用 `AM_TEMPLATE(GETTEXT_PACKAGE)` 定义 `GETTEXT_PACKAGE`。如果你需要 `config.h`，你应该用变量来指定它。然后使用：

```bash
GETTEXT_PACKAGE=QUOTED(GETTEXT_PACKAGE, "GETTEXT_PACKAGE")

AC_SUBST(GETTEXT_PACKAGE)

ALL_LANGUAGES="de es"

AM_GLIB_INIT_GETTEXT

AC_PROG_INIT
```

是时候为编译器导出一些变量了。使用 `AC_SUBST` 处理 `CFLAGS`（编译器选项）、`CPPFLAGS`（预处理器选项，如包含路径）和 `DFLAGS`（链接器选项）。

下部分使用 pkg-config 检查 GNOME 版本号是否足够：

```bash
GNOME_MODULES="libgnomeui-2.0 >= 2.0.0"

PKG_CHECK_MODULES(GNOME, $GNOME_MODULES)
```

`PKG_CHECK_MODULES` 的第一个参数非常重要；`PKG_CHECK_MODULES` 的展开会将 `GNOME_CFLAGS` 设置为 `pkg-config--cflags` 的输出（`GNOME_LIBS` 类似）。因此，接下来的两个导出 GNOME 编译器和链接器选项：

```bash
AC_SUBST(GNOME_CFLAGS)

AC_SUBST(GNOME_LIBS)
```

现在你准备好告诉 autotools 生成哪些文件了：

```bash
AC_CONFIG_FILES(

  Makefile

  src/Makefile

  pixmaps/Makefile

  po/Makefile.in

)

AC_OUTPUT
```
