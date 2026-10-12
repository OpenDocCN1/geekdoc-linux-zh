
```c
#include <ncurses.h>
int main(void)
{
initscr();
addstr("Hello World");
refresh();
getch();
endwin();
return 0;
}
```

示例输出：

```
Hello World
```

# 194 附录 A = Ncurses 库

```c
addstr("Red text on a cyan background.\n");
refresh();
getch();
endwin();
return 0;
}
```

示例输出：

默认颜色已设置为：

青色背景上的红色文字。

上述文字显示为青色背景上的红色文字。

# 另见

`COLORS`, `init_pair()`, `use_default_colors()`

# attr_get()

`attr_get()` 函数用于读取窗口中使用了哪些文本属性。返回的值将与已知属性进行比较（通过逻辑或）。该函数还会确定是否使用了窗口颜色，以及如果使用了，是哪种颜色对。

# 手册页格式

```c
int attr_get(attr_t *astrs, short *pair, void *opts);
int watt_get(WINDOW *win, attr_t *astrs, short *pair, void *opts);
```

## 格式参考

`attrs` 是 Ncurses 类型 `attr_t` 变量的地址，一个长整型（与 `ctypes` 相同）。它用于存储来自窗口的属性信息。核心的 `attrs` 是一个位字段，其字段根据窗口中激活的属性进行设置。附录 C 描述了 `ctypes` 字段。

`pair` 是一个短整型值的内存地址，用于存储用于窗口着色的颜色对编号。

`NULL` 占位符表示 `opts` 参数。`opts` 目前尚未定义，但预留供以后使用。

关于 `win` 参数的信息，请参阅本附录中的 `w` 前缀条目。

# 返回值

函数在成功或失败时返回 `OK` 或 `ERR`。

## 注意事项

`attrs` 参数由 NCurses 的 `attr_t` 变量类型声明：

```c
attr_t ats;
```

在这一行代码中，变量 `ats` 是根据 `attr_t` 类型创建的。`attrib` 和 `pair` 参数都是内存地址。它们可以用指针变量表示，也可以用带有 `&` 一元操作操作符的普通变量表示。

可以将 `attrib` 或 `pair` 替换为 `NULL`，在这种情况下，`attr_get()` 将不会返回该特定块的信息。

`pair` 的值仅返回颜色编号。它不会告诉你是哪些颜色被分配给了该颜色编号。为此，你需要使用 `pair_content()` 函数。

在我的实验中，我能够让 `attr_get()` 从给定的窗口返回文本和颜色。该函数似乎优先考虑属性，如 `A_BOLD`、`A_BLINK` 等。当这些属性与颜色信息共存时，只返回属性值。当属性从窗口中移除时，则返回颜色信息。（这可能是 NCurses 处理终端的 `ncv`（no_color_video）能力的影响。当终端描述说（具有此能力）颜色与给定的视频属性不匹配时，它将仅使用颜色。）

要要专门检索窗口的背景属性，请使用 `getbkgd()` 函数。`Getbkgd()`。

## 示例

```c
attr_get(&a, &cp, NULL);
```

此语句返回 `stdscr` 中使用的属性，并将其保存在变量中。如果使用了颜色对，将保存在 `cp` 变量中。

## 示例程序

```c
#include <ncurses.h>
int main(void)
{
    attr_t attributes;
    short cpair;
    initscr();
    attrset(A_BOLD | A_REVERSE | A_BLINK);
    attr_get(&attributes, &cpair, NULL);
    addstr("Attributes active in this window:\n");
    if(attributes & A_COLOR) printf("Color w/ pair\n%d\n", cpair);
    if(attributes & A_REVERSE) addstr("Reverse\n");
    if(attributes & A_BLINK) addstr("Blink\n");
    if(attributes & A_DIM) addstr("Dim\n");
    if(attributes & A_BOLD) addstr("Bold\n");
    refresh();
    getch();
    endwin();
    return 0;
}
```

示例输出：

| 此窗口中激活的属性： |
| :--- |
| Reverse |
| Blink |
| Bold |

# 另见

附录 C, `attrset()`, `COLOR_PAIR()`, `getbackgd()`

# attroff()

`attroff()` 函数用于关闭一个或多个文本属性。这些属性之前通过 `attron()`、`attrset()` 或类似的属性函数应用。

# 手册页格式

```c
int wattroff(WINDOW *win, int attrs);
int wattroff(WINDOW *win, int attrs);
int attr_off(attr_t attrs, void *opts);
int watt_off(WINDOW *win, attr_t attrs, void *opts);
```

## 格式参考

`attrs` 在某些调用中是 `int`，在另一些中是 `attr_t`。但在 NCurses 中它们实际上是相同的东西。它通常是 `ncurses.h` 中定义的一个或多个属性常量，并列在本附录后面的任何 `attrset()` 列表中。在使用 `attroff()` 函数后，任何显示的文本都将移除命名的属性；其他属性亦然。

可以在单个 `attroff()` 函数中指定多个属性，方法是在每个属性之间用 `|`（逻辑或）隔开。`COLOR_PAIR(n)` 也被视为文本属性，其中 `n` 是程序早些由 `init_pair()` 函数定义的颜色对。`NULL` 在 `attron()` 函数中用作未定义的占位符。关于 `win` 参数的信息，请参阅本附录中的 `w` 前缀条目。

# 返回值

根据文档说明，返回值为“不重要”。

## 注意事项

新属性仅应用于 `attron()` 函数之后显示的新文本。这些属性是之前 `attron()` 或 `attrset()` 函数设置的补充。使用 `attron()` 应用新的 `COLOR_PAIR` 值将替换之前定义的文本颜色。一次只能使用一个 `COLOR_PAIR`；`COLOR_PAIR` 属性不能组合，其他属性可以。

属性影响 `addch()`、`addstr()` 和 `printw()` 函数的输出。另参考 `attrset()` 的注意事项。

## 示例

```c
attron(A_BOLD);
```

此语句从任何新文本中移除粗体属性。

```c
watton(warning,COLOR_PAIR(1));
```

此语句设置分配为 1 的颜色。

```c
attron(A_BOLD | A_REVERSE);
```

此语句从任何新文本中移除粗体和反转属性。

## 示例程序

请参阅 `attrset()` 条目获取示例程序。

# 另见

第三章，`attrset()`

# attron()

`attron()` 函数为任何放入屏幕的文本启用文本属性。

# 手册页格式

```c
int attron(int attrs);
int watron(WINDOW *win, int attrs);
int attron_on(attr_t attrs, void *opts);
int watron_on(WINDOW *win, attr_t attrs, void *opts);
```

## 格式参考

`attrs` 通常是 `NCURSES.H` 中定义的一个或多个属性常量，每个都是长整型。在使用 `attroff()` 函数后，命名的属性将应用于任何显示的文本。设置新属性不会影响之前的文本。属性值列表请参阅 `attrset` 条目。

# 200 附录 A = NCurses 库参考

# 参见

第 3 章，附录 C，`attrset()`, `chgat()`

# attrset()

`attrset()` 函数为后续的所有文本输出函数设置属性。使用 `attrset()` 后显示的文本将忽略之前通过 `attrset()` 或 `attron()` 分配的任何属性，而是使用由 `attrset()` 指定的新属性。

## 手页格式

```
int attrset(int attrs);
int watset(WINDOW *win, int attrs);
int attr_set(attr_t attrs, short pair, void *opts);
int watset(WINDOW *win, attr_t attrs, short pair, void *opts);
```
