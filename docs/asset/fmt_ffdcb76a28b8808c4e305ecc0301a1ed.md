
```bash
dnl 查找应该在分发包中的源文件。
AC_INIT(firstcups).
```

另一个常用命令是 `AC_CONFIG_HEADER`，它指定了要生成的头文件名，并包含了 `configure` 脚本的所有定义。

```bash
dnl 生成一个 config.h 文件。
AC_CONFIG_HEADER(config.h).
```

`AC_PROG_CC` 命令紧随在检查任何库或头文件之前。它基本上决定了使用哪个 C 编译器及其位置。如果你的系统有供应商提供的 C 编译器 (`cc`) 和 GNU C 编译器 (`gcc`)，`AC_PROG_CC` 命令将选择编译器。

```bash
dnl 查找 C 编译器。
AC_PROG_CC
```

在发布 `AC_PROG_CC` 命令后，我们可以使用 `AC_CHECK_LIB` 和 `AC_CHECK_HEADER` 命令检查库。对于 CUPS，我们必须确定是否需要 `socket` 和 `nsl` 库：

```bash
dnl 如果需要，获取网络库。
AC_CHECK_LIB(socket,
if test "$uname" != "IRIX"; then
  LIBS="-lsocket $LIBS"
else
  echo "Not using -lsocket since you are running IRIX"
fi)
```

```bash
AC_CHECK_LIB(nsl,gethostbyaddr,
if test "$uname" != "IRIX"; then
  LIBS="-lnsl $LIBS"
else
  echo "Not using -lnsl since you are running IRIX"
fi)
```

然后我们可以检查 cups 库和头文件：

```bash
dnl 查找 cups 库和头文件。
AC_CHECK_LIB(cups,cupsPrintFiles)
AC_CHECK_HEADER(cups/cups.h, AC_DEFINE(HAVE_CUPS))
```

```bash
dnl 如果没有 CU，则停止。
if test $ac_cv_lib_cups_cupsPrintFiles= no -o $ac_cv_header_cups_h= no;
then
  AC_MSG_ERROR(Could not find CU.)
fi
```

# CUPS 编程第13章概述

`AC_DEFINE` 命令在你的程序中定义 C 常量。它通常出现在 `config.h` 头文件中。`AC_MSG_ERROR` 命令显示错误消息并停止配置脚本。防止用户在安装所需文件之前编译你的程序。

最后，`AC_OUTPUT` 命令为程序生成 Makefile：

```bash
dnl 生成 Makefile
AC_OUTPUT(Makefile)
```

## config.h 头文件

尽管 `config.h` 头文件是配置过程的可选部分，但简单的软件会使用它。这是因为每个库和头的检查都会为源文件创建一个定义；如果没有 `config.h` 头文件来保存它们，这些定义会被添加到 Makefile 中的编译器选项。对于某些程序，这些定义会让命令变得非常长！

`config.h` 头文件是从名为 `config.in` 的源文件构建的。列表 13.3 显示了我们示例 CUPS 的 `config.in` 文件。

### 列表 13.3 config.in 源文件

```c
/* 此文件自动生成。请勿手动编辑！ */
#undef HAVE_LIBC
#undef HAVE_CUPS_H
```

你可以看到，`config.in` 文件并不多。任何 `AC_DEFINE` 定义都使用预处理器的 `#undef` 命令包含。如果相应的名称在 `configure` 脚本中有定义，`#undef` 将被 `#define` 替换。

## Makefile

拼图的最后一块是 Makefile。该文件由 `make` 程序制作，将各种源文件编译成一个或多个程序。`configure` 脚本可以从 `Makefile.in` 文件为你生成 Makefile。列表 13.4 显示了我们示例应用的 `Makefile.in` 文件。

### 列表 13.4 Makefile.in 源文件

```make
# C 编译器选项
CC = @CC@
CFLAGS = @CFLAGS@
LIBS = @LIBS@
```

### 列表 13.4 续

```make
# 源文件
SRCS = firstcups.c
```

```make
# 对象文件
OBJS = $(SRCS:.c=.o)
```

```make
# 生成 firstcups 应用
firstcups$(OBJS)
	$(CC) $(CFLAGS) -o firstcups $(OBJS) $(LIBS)
```

```make
# 依赖
$(OBJS): config.h Makefile
```

`configure` 脚本中的每个值都使用 `@NAME@` 法插入 Makefile。Makefile 的开头设置了 C 编译器 (`cc`)、C 编译器选项 (`CFLAGS`) 以及要使用的库 (`LIBS`)：

```make
# C 编译器选项
CC = @CC@
CFLAGS = @CFLAGS@
LIBS = @LIBS@
```

Makefile 的其余部分是静态的，并将 `firstcups` 程序与 `firstcups.c` 源文件关联。

## 整合一切

在创建了 `config.in`、`config.h.in` 和 `Makefile.in` 源文件后，运行 `autoconf` 命令来生成 `configure` 脚本：

```bash
autoconf
```

然后使用以下命令运行 `configure` 脚本：

```bash
./configure
creating cache ./config.cache
checking for gcc... gcc
checking whether the C compiler (gcc) works... yes
checking whether the C compiler (gcc) is a cross-compiler... no
checking whether we are using GNU C...
checking whether gcc accepts -g... yes
checking for socket in -lsocket... no
checking for gethostaddr in -lnsl... yes
checking for cupsPrintFiles in -lcups... yes
```

# CUPS 编程第 13 章概述

检查如何运行 C 预处理器... gcc -E

检查 cups/cups.h... 是的

更新缓存 ./config.cache

创建 ./config.status

创建 Makefile

创建 config.h

这将生成 `config.h` 和 `Makefile` 文件。最后，运行以下命令

```
make ENTER
gcc -g -O2 -c firstcups.o firstcups.c
gcc -g -O2 -o firstcups.o -lcups -lnsl
```

来构建 `firstcups` 程序。

## 许可问题

两个 CUPS 库采用不同的条款许可。如果你正在编写仅供内部使用的软件，或者你将将以源代码的形式向公众发布你的软件，这些许可可能不会对你产生影响。然而，如果你打算分发你的软件，理解它们之间的区别是非常关重要的。

`cups` 库根据 GNU 库通用公共许可证 (`LGPL`) 的条款进行许可。该许可允许你通过提供源代码或使用 GNU 软件许可，将你的程序与 `cups` 库链接。`LGPL` 也是 GNU C 以及其他可用库允许程序员以任何他们认为适当的条款开发软件的许可。

`cupsimage` 根据 GNU 通用公共许可证 (`GPL`) 的条款进行许可。与 `LGPL` 不同，该许可要求使用 `cupsimage` 库的所有程序都按照 `GPL` 的条款提供。除其他要求外，`GPL` 要求分发你软件的源代码。

这些许可的完整文本可在附录 F，“通用 Unix 打印系统许可协议”中找到。如既往，如果你不确定如何将这些许可应用于你的软件，应该咨询律师。你也可以联系 Easy Software Products 以寻求建议，或为你的软件协商不同的许可条件。

### 总结

CUPS 拥有两个库和八个头文件，它们提供了 CUPS 的所有接口。`cups` 库提供了基本的客户端函数，并被所有 CUPS 程序使用。`cupsimage` 库提供成像功能，并被栅化过滤器和打印机驱动程序使用。

由于操作系统的差异，你可能需要也不需要配合 CUPS 使用额外的网络库。管理这些差异的最简单方法是使用 GNU `autoconf` 软件来定位必要的库并配置你的源代码。

CUPS 库以两种许可提供。`cups` 库根据 `LGPL` 提供，以便在开发和分发软件时提供最大的灵活性。`cupsimage` 库根据 `GPL` 提供，并要求使用该库的软件也必须根据 `GPL` 分发。

# 第 14 章

# 使用 CUPS API 函数

# 使用 CUPS 编程

本章将向你展示如何使用 CUPS API 函数获取可用打印机列表、提交打印作业，并从你的应用程序中管理打印作业。你还将学习如何从应用程序访问 PostScript 打印机描述 (`PPD`) 文件，并使用它们显示打印机特定选项并为特定打印机自定义你的输出。

## 打印服务

CUPS 提供了许多函数来管理打印机、类、作业和选项。

## 管理打印机和类

CUPS 同时支持打印机和打印机类。第 13 章中的第一个 CUPS 程序“CUPS 编程概述”引入了两个 CUPS 函数：`cupsDefault()` 和 `cupsGetPrinters()`，它们检索了当前默认打印机和打印机列表。第三个函数 `cupsGetClasses()` 可用于从服务器检索打印机类列表。

`cups-default` 函数不接受任何参数，并返回当前默认打印机或类的名称。如果没有定义默认打印机或类，则返回一个 `NULL` 指针：

`cupsDefault()` 返回的字符串存储在静态缓冲区中，每次调用时都会被覆盖。

`cupsClasses()` 函数检索打印机类列表并接受单个参数，即指向 `char` 变量的指针。它返回类的数量：

```
int i;
int num_classes;
char **classes;

num_classes = cupsGetClasses(&classes);
if (num_classes == 0)
    puts("No printer classes found.");
else
{
    printf("%d printer class(es) were found:\n", num_classes);
```

# 使用 CUPS API 函数 第 14 章

```
for (i = 0; i < num_classes; i++))
    printf("%s\n", classes[i]);
}
```

同样，`cupsGetPrinters()` 函数检索打印机列表：

```
int i;
int num_printers;
char **printers;
```

```
num_printers = cupsGetPrinters(&printers);
if (num_printers == 0)
    puts("No printers found.");
else
{
    printf("%d printer were found:\n", num_printers);
    for (i = 0; i < num_printers; i ++)
        printf("%s\n", printers[i]);
}
```

`GetClasses()` 和 `cupsGetPrinters()` 都返回一个使用 `malloc()` 函数分配的字符串数组。在释放字符串使用的内存之前，你必须释放打印机或类名称的字符串，然后释放数组指针。如果打印机或类的数量为 0，不要尝试释放数组：

```
if (num_classes > 0)
{
    for (i = 0; i < num_classes; i ++)
        free(classes[i]);
}
```

```
if (num_printers > 0)
{
    for (i = 0; i < num_printers; i ++)
        free(printers[i]);
    free(printers);
}
```

列表 14.1 显示了如何结合这些函数来显示默认打印机或类以及可用打印机。

# 列表 14.1 结合这些函数显示默认打印机或类以及可用打印机

# 列表 14.2 继续

在调用 `cupsJobs()` 获取激活的打印任务后，我们在循环中显示任务列表。

输出结果如下：

**.showjobs ENTER**

找到 4 个任务：

| Job ID | 目标 | Title | 用户 | Size |
| --- | --- | --- | --- | --- |
| 42 | LaserJet | Test Page | mike | 12k |
| 43 | DeskJet | showdeeds.c | mike | 2k |
| 44 | StylusColor | Test Page | mike | 12k |
| 45 | StylusPhoto | showjobs.c | mike | 1k |

## 探索打印机选项

打印机选项是 CUPS 不同于传统的 LPD 软件的特性之一。CUPS API 将选项作为 `cups_option_t` 结构体数组暴露。`cups_option_t` 结构包含一个名称和一个值字符串，API 函数会根据需要将它们转换为相应的 IPP 属性类型。

### 添加选项

CUPS 提供了几个管理打印机选项的函数。第一个是 `cupsAddOption()`。它向选项数组中添加单个选项：

```
#include <cups/cups.h>
...
int    num_options;
cups_option_t *options;
...
num_options = 0;
options = NULL;

num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
```

名称字符串是选项的名称，且不区分大小写；也就是说，“name" 和 "NAME" 是相同的。

值字符串是该选项的值。值数组之间用逗号（,）分隔，并使用减号（-）。

`num_options` 和 `options` 参数分别是当前选项的数量以及 `cups_option_t *` 变量的引用。

每次调用 `cupsAddOption()` 都会返回作为整数类型的新选项数量。`options` 指针将更新为指向更新后的数组。

添加多个相同名称的选项只会创建一个该选项的副本，并保留之前的值。不要假设调用 `cupsAddOptions()` 20 次会产生一个包含 20 个选项的数组。

### 添加多个选项

`cupsAddOption()` 向数组添加单个选项，而 `cupsParseOptions()` 函数将添加字符串中传递的零或多个选项：

```
#include <cups/cups.h>
int    num_options;
```

# 第三部分 使用 CUPS 编程

```
cups_option_t *options;
...
num_options = 0;
options = NULL;
```

```
num_options = cupsParseOptions("name=value name2=value2", num_options, &options);
```

字符串中的选项用空格分隔。字符串中的值用单引号（')或双引号（”）包围，或者使用反斜杠（\）在值包含空格。`lp` 和 `lpr` 命令以及许多 CUPS 过滤器和打印机驱动经常使用 `cupsParseOptions()` 函数。

### 获取选项值

在构建选项数组后，你可以使用 `cupsGetOption()` 函数获取命名选项的当前值：

```
#include <cups/cups.h>
...
int num_options;
cups_option_t *options;
const char *value;
...
value = cupsGetOption("name", num_options, options);
```

名称字符串是选项的名称。`num_options` 和 `options` 参数分别是选项的数量和指向 `cups_option_t` 结构的指针。

如果选项已定义，`cupsGetOption()` 函数返回当前选项值；如果选项未定义，则返回 `NULL`。

### 释放选项使用的内存

在使用完选项数组后，调用 `cupsFreeOptions()` 函数来释放已使用的内存：

```
#include <cups/cups.h>
...
int num_options;
cups_option_t *options;
...
cupsFreeOptions(num_options, options);
```

`num_options` 和 `options` 参数分别是选项的数量和指向 `cups_option_t` 结构的指针。

## 管理目标
