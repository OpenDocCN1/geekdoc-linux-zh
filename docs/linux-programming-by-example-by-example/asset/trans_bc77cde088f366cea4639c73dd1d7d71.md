

# 第 10 章 — 使用 db 进行 C 语言编程

```c
int main(void)
{
	DB *db;
	DBC *dbc;
	DBT key, value;
	int ret;

	ret = db_open("test.db", DB_BTREE,
			DB_CREATE, 0600, NULL, NULL, &db);
	if(ret) {
		perror("dbopen");
		exit(EXIT_FAILURE);
	}

	/* Create a cursor */
	ret = db->cursor(db, NULL, &dbc, 0);
	if(ret) {
		perror("cursor");
		exit(EXIT_FAILURE);
	}
	memset(&key, 0, sizeof(key));
	memset(&value, 0, sizeof(value));

	/* Move sequentially through the database */
	while((ret = dbc->c_get(dbc, &key, &value,
		DB_NEXT)) != DB_NOTFOUND) {
		printf("key/value is %s/%s\n", (char *)key.data,
			(char *)value.data);
	}

	/* Sync the database */
	db->sync(db, 0);

	/* Close the cursor */
	dbc->c_close(dbc);

	db->close(db, 0);
	exit(EXIT_SUCCESS);
}
```

该程序的输出如下所示：

![](img/be588b36b489136ce784030a08a1d3d4_246_0.png)

### 输出

```
$ ./cursor
key/value is five/Signals
key/value is four/Processes
key/value is one/Compiling Programs
key/value is three/About the Project
key/value is two/Controlling the Build Process
```

正如你所见，按顺序遍历数据库时，记录实际上是根据记录键排序存储的。在打开数据库并创建游标后，程序不断调用 `c_get` 从数据库中获取下一条记录，然后显示该键及其关联的值。当 `c_get` 返回 `DB_NOTFOUND` 时，表示没有更多可获取的记录。实际上并不需要调用 `sync`，因为数据没有发生任何更改，但这里包含它是为了展示其用法。请注意，在 `cursor` 关闭数据库之前，先关闭了数据库游标 `dbc`。虽然不是严格要求，但养成一种良好的习惯，确保 DB 接口分配的所有资源都正确返回给操作系统，是非常重要的。

> **注意**
> 虽然未在文中详细讨论，但我使用了该网站上提供的 addmore.c 程序向数据库中添加记录。它是本章 makefile 的一部分，因此你可以构建它以完成此示例。它会提示你每次输入五条记录。

### 接下来是什么？

本章向您介绍了 Berkeley 数据库，这是您将学习的一系列 Linux API 中的第一个。接下来的两章将展示如何使用 ncurses 控制字符模式屏幕的外观。您还将学习如何与鼠标交互、创建菜单以及绘制表单。

# 11 — 使用 ncurses 进行屏幕操作

本章介绍 ncurses（读音为“en-curses”），它是经典 UNIX 屏幕处理库 curses 的自由实现。ncurses 提供了用于屏幕控制和操作的简单高级接口。它还包含用于处理键盘和鼠标输入、创建和管理多个窗口，以及使用菜单、表单和面板的强大例程。本章的主题包括以下内容：

- ncurses 功能
- 术语和概念
- 初始化和终止例程
- 字符和字符串输出
- 字符和字符串输入

### ncurses 特性

ncurses 是“new curses”的缩写，是 Bell Labs 发行的 UNIX System V Release 4.0 (SVR4) 中附带的 curses 库的自由可再分发克隆版。“curses”这个名字源自短语“cursor optimization”，简明扼要地描述了 curses 的作用。

### 终端独立性

ncurses 概括了应用程序与其运行的屏幕或终端之间的接口。鉴于终端和屏幕有成百上千种变体，特别是它们拥有的不同功能以及调用这些功能的命令，UNIX 程序员需要一种方法来抽象屏幕操作。与其编写大量额外的代码来考虑不同的终端类型，不如说 ncurses 为程序员提供了统一且通用的接口。ncurses API 将程序员与底层硬件隔离开来。

### 能力

ncurses 为基于字符的应用程序提供了许多与图形 X Window 应用程序中发现的功能相似的特性：多个窗口、表单、菜单和面板。ncurses 的窗口可以独立管理，可以包含相同或不同的文本，可以滚动也可以不滚动，并且可以被隐藏。vi 编辑器和流行的文件管理器 Midnight Commander 都是使用 ncurses 编写的。

表单使程序员能够创建易于使用的数据输入和显示窗口，从而简化了通常困难且具有特定应用性质的编码任务。面板扩展了 curses 处理重叠和堆叠窗口的能力。通过调用应用程序选项为用户提供简单接口的菜单，可以很容易地使用 ncurses 简单通用的菜单编程接口来实现。本书使用的版本是 4.2，尽管 5.0 版本目前正处于 beta 阶段。

### 使用 ncurses 编译

要使用 ncurses 编译程序，您需要它的函数和变量定义，因此在源代码中包含 `<curses.h>`：

```c
#include <curses.h>
```

许多 Linux 系统将 `/usr/include/curses.h` 设置为指向 `/usr/include/ncurses.h` 的符号链接，因此理论上您可以包含 `<ncurses.h>`。但是，为了获得最大的可移植性，请使用 `<curses.h>`，因为尽管难以置信，但 ncurses 并不适用于所有 UNIX 和类 UNIX 平台。您还需要链接 ncurses 库，因此在链接时使用 `-lcurses` 选项，或者将 `-lncurses` 添加到 make 变量 `LDFLAGS` 或环境变量 `LDFLAGS` 中：

```
$ gcc curses_prog.c -o curses_prog -lcurses
```

默认情况下，ncurses 程序中的调试跟踪是禁用的。要启用调试，请链接 ncurses 的调试库 `libncurses_g.a`，并在代码中调用 `trace(N)` 或将环境变量 `$NCURSES_TRACE` 设置为 N，其中 N 是一个正的非零整数。这样做会将调试输出强制写入当前目录下名为 `trace` 的文件。N 的值越大，调试输出越详细，体积也就越大。`<ncurses.h>` 中记录了 N 的有用值。例如，标准跟踪级别 `TRACE_ORDINARY` 为 31。

### 示例

![](img/be588b36b489136ce784030a08a1d3d4_249_0.png)

#### 示例

1. 这是最简单的 ncurses 程序。它只是启动和停止 ncurses 子系统；不生成任何输出。

```c
/*
 * simple.c Simple ncurses program
 */
#include <curses.h>

int main(void)
{
	initscr();
	endwin();
	return 0;
}
```

![](img/be588b36b489136ce784030a08a1d3d4_249_1.png)

### 输出

要编译并运行它，请键入以下内容：

```
$ gcc simple.c -o simple -lncurses
$ ./simple
```

2. 下一个示例使用了调试库，并进行了几次额外的函数调用来生成输出：

![](img/be588b36b489136ce784030a08a1d3d4_249_2.png)

### 示例

```c
/*
 * debugit.c ncurses program calling trace()
 */
#include <curses.h>

int main(void)
{
	initscr();
	trace(TRACE_CALLS);
	printw("set debug level to TRACE_CALLS");
	refresh();
	endwin();
	return 0;
}
```

编译此程序的命令行如下：

```
$ gcc debugit.c -o debugit -lncurses_g
$ ./debugit
```

如果您速度真的很快，可能会看到消息在屏幕上闪烁！*trace* 调用会导致所有 ncurses 函数调用被写入当前目录中的 *trace* 文件。此处摘录了该文件的一部分：

![](img/be588b36b489136ce784030a08a1d3d4_251_0.png)

### 输出

```
TRACING NCURSES version 4.2 (990213)
printw("set debug level to TRACE_CALLS", ...) called
called waddnstr(0x80675f8,"set debug level to TRACE_CALLS",-1)
..., current (A_NORMAL)
return 0
called wrefresh(0x80675f8)
clearing and updating from scratch
ClrDate() called
ClearScreen() called
screen cleared
updating screen from scratch
return 0
TransformLine(0) called
TransformLine(1) called
...
TransformLine(24) called
return 0
called endwin()
return 0
```

> **提示**
> ncurses 软件包附带一个名为 *tracemunch* 的脚本，可将调试信息压缩并总结为更易于阅读、对人类更友好的格式。

