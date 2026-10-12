
当为每个 `verch` 或 `horch` 指定 `0` 时，将使用默认的 ACS 字符：`verch` 使用 `ACS_VLINE`，`horch` 使用 `ACS_HLINE`。关于这些字符的更多信息，请参阅附录 B。

## 返回值

`box()` 始终返回 `int` `0` 或 `OK`。

## 注意事项

用于绘制框角的字符如表 A-2 所示。

`box()` 函数等同于 `border()` 函数：

```
wborder(win,verch,verch,horch,horch,0,0,0,0)
```

没有 `box()` 函数。

同时也请参考 `border()` 的注意事项，因为相同信息适用于这两个函数。

## 示例

```
box(stdscr,0,0);
```

此函数使用默认的线条绘制字符在标准屏幕窗口周围绘制一个框。

```
box(table, '*', '*');
```

此函数使用星号作为水平和垂直线，在窗口 `table` 周围绘制一个框。

表 A-2：`box()` 中使用的 ACS 线条绘制字符

| 位置 | ACS 字符 | 位置 | ACS 字符 |
|---|---|---|---|
| 左上 | `ACS_ULCORNER` | 左下 | `ACS_LLCORNER` |
| 右上 | `ACS_URCORNER` | 右下 | `ACS_LRCORNER` |

## 示例程序

```
#include <ncurses.h>

int main(void)
{
    initscr();
    box(stdscr,0,0);
    mvaddstr(1,1,"Ta-da!");
    refresh();
    getch();

    endwin();
    return 0;
}
```

示例输出：该程序在整个屏幕周围绘制一个框，并将 `Ta-da!` 单词放在框内第 1 行第 1 列。

## 另请参

第 14 章，附录 B，`border()`, `hline()`, `vline()`

## `can_change_color()`

`can_change_color()` 函数确定终端是否可以重新定义其颜色集。如果是，则可以使用 `color_content()` 函数创建新的颜色值，用于 NCurses 的各种颜色属性函数。

## 手册页格式

```
bool can_change_color(void);
```

## 格式引用

该函数没有参数。

## 返回值

`can_change_color()` 返回一个布尔值，`TRUE` 或 `FALSE`，取决于终端是否可以重新定义颜色。

## 注意事项

此命令返回 `TRUE` 的终端包括 Linux 控制台、`xterm-88color`、`xterm-256color`、`PuTTY` 或终端描述中包含 `ccc` 的任何设备。

## 示例

```
r = can_change_color();
```

在该语句中，如果 `r` 的值等于 `TRUE`，终端上的颜色值可以更改；否则为 `FALSE`。

```
if(can_change_color())
```

如果颜色值可以更改，则该条件为真。

## 示例程序

```
include <ncurses.h>
int main(void)
{
bool tf;
initscr();
tf = can_change_color();
if(tf == TRUE)
addstr('This terminal can change the standard colors.\n');
else
addstr('This terminal cannot change the colors.\n');
refresh();
getch();
endwin();
return 0;
}
```

示例输出：

This terminal can change the standard colors.

或：

This terminal cannot change the colors.

## 另请参

`start_color()`, `color_content()`, `TRUE`

## `cbreak()`

`cbreak()` 函数修改输入，激活所谓的 `cbreak` 模式（回显模式）。这增加了你的程序可用的字符数量，并在一定程度上加快了输入速度。

## 解释

NCurses 通过终端读取键盘输入。这被称为“熟输入模式”`cooked input mode`，因为输入由终端进行缓冲，且在键盘上输入的某些字符会被拦截并用于某些用途。这发生在文本传递给你的 NCurses 程序之前。

缓冲指的是文本读取的方式。终端使用行缓冲，它存储一行文本并在遇到 `\n` 后将其发送给 NCurses。

特殊字符包括例如，用于命令提示符处删除一行文本的 `Killchar`，或用于删除文本的 `Erase` 键。

`cbreak` 模式禁用了行缓冲以及对 `Killchar` 和 `Erasechar` 的按键捕获。

## 手册页格式

```
int cbreak(void);
int nocbreak(void);
```

## 格式引用

`cbreak()` 命令激活 `cbreak` 模式。

`nocbreak()` 命令恢复熟输入模式（正常）。

## 返回值

成功返回 `OK`，失败返回 `ERR`。

## 注意事项

`cbreak()` 和 `nocbreak()` 的设置是可继承的。也就是说，当你的程序启动时，这些设置可能是开启或关闭的。确保你的程序使用 `cbreak()` 模式输入的唯一方法是在代码中调用 `cbreak()` 函数。`nocbreak()` 亦然。

`cbreak()` 设置会覆盖 `raw`。尽管如此，请尝试只使用 `cbreak()` 或 `raw()` 函数，不要同时使用。请参见 `raw()`。

`218` 附录 A NCurses 库引用

`nocbreak()` 函数还会禁用（撤销）由 `halfdelay()` 设置的任何延迟。

## 示例

```
nocbreak()
```

在这里设置了 `cbreak` 模式。

## 示例程序

```
#include <ncurses.h>
int main(void)
{
bool tf;
initscr();
tf = can_change_color();
if(tf == TRUE)
addstr('This terminal can change the standard colors.\n');
else
addstr('This terminal cannot change the colors.\n');
refresh();
getch();
endwin();
return 0;
}
```

## `219` 附录 A NCurses 库引用

## 另请参

`raw()`, `halfdelay()`

## `chgat()`

`chgat()` 函数从光标位置更改属性。

## 手册页格式

```
int chgat(int n, attr_t attr, void *opts);
int wchgat(WINDOW *win, int n, attr_t attr, void *opts);
int mvchgat(int y, int x, int n, attr_t attr, void *opts);
int wmwchgat(WINDOW *win, int y, int x, int n, attr_t attr, void *opts);
```

## 格式引用

`n` 是 `chgat()` 影响的字符数。当 `n` 为 `-1` 时，从光标位置到行尾的所有文本都会受到影响。

`attr` 是 `attr_t` 类型，表示要应用的属性。`owncolor` 是短整数，表示颜色对编号而不是颜色参数。

`opts` 参数。

## 返回值

根据文档说明，返回值“不重要”。

## 注意事项

简单的 `refresh()` 不会更新屏幕上的新属性。因此，需要对相同行应用 `touchline()` 函数，或对整个窗口应用 `touchwin()` 函数，才能看到 `chgat()` 的效果。

# 附录 A ■ NCurses 库参考

```
mvchgat(0,0,4,0,NULL);
mvchgat(1,12,10,0,2,NULL);
mvchgat(2,23,6,A_UNDERLINE,0,NULL);
mvchgat(3,30,6,A_BOLD,0,NULL);
touchwin(stdscr);
refresh();
getch();
endwin();
return 0;
```

# 输出示例：

这是极其无聊的第一行

这是极其无聊的第二行

这是极其无聊的第三行

这是极其无聊的第四行

按下回车键，新属性将应用于文本：在第一行中，单词以白色背景上的红色字体显示；在第二行中，单词 `incredibly` 以蓝色背景上的白色字体显示；在第三行中，单词 `boring` 带有下划线；在最后一行，单词 `fourth` 以粗体文本显示。

## 另参

`attrset()`, `attron()`

## `clear()`

`clear()` 函数清除屏幕或命名窗口，在每个屏幕位置写入空白或空格字符。此外，`clear()` 函数会调用 `clearok()`，以确保屏幕被擦除并在下次调用 `refresh()` 函数时被完全重写。（参见 `clearok()`）

## 手页格式
