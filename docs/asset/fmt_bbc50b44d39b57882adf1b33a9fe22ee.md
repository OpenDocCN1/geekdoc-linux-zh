
# 462 附录 A ■ Ncurses 库参考

```c
slk_init(0);
initscr();
start_color();
init_pair(1,COLOR_RED,COLOR_YELLOW);

for(x=0;x<LCOUNT;x++)
slk_set(x+1, labels[x], CENTER);
slk_refresh();
getch();

slk_color(1);
slk_touch();
slk_refresh();
getch();

endwin();
return 0;
```

软标签出现。按回车键，它们将应用颜色重新出现。如果没有在第 24 行调用 `slk_touch()`，则会看到新的颜色属性。（注释掉该行并重新编译以查看。）

## 另参

`slk_refresh()`, `touchwin()`

# `standend()`

`standend` 函数用于关闭文本属性。

## Man Page 格式

```c
int standend(void);
int standend(WINDOW win)
```

### 格式参考

该函数没有参数。

关于 `win` 参数的信息，请参阅本附录中的 `wentry` 条目。

## 返回值

根据文档，返回值为“无意义”。

# 463 附录 A ■ NCurses 库参考 463

## 注意

虽然 `standout()` 似乎是 `standout()` 的逻辑成对函数，但它的功能不仅仅是关闭 `standout` 文本属性；它会关闭所有文本属性，甚至是颜色。

`standout()` 等同于以下代码：

```c
attrset(A_NORMAL);
```

### 示例

```c
standout();
```

该语句恢复后续在标准屏幕上显示的所有文本的普通文本属性。

### 示例程序

示例程序和示例输出请参考 `standout()` 函数条目（后文）。

## 另参

第 3 章，`attrset()`, `atroff()`

# `standout()`

`standout()` 函数激活显示在屏幕上的文本的 `standout` 属性。

## Man Page 格式

```c
int standout(void);
int standout(WINDOW *win);
```

### 格式参考

该函数没有参数。

关于 `win` 参数的信息，请参阅本附录后后的 `w` 条目。

## 返回值

根据文档，返回值为“无意义”。

# 464 附录 A ■ NCurses 库参考

## 注意

在大多数终端上，`standout` 以反显色视频模式显示文本，例如白色背景上的黑色文字。

此函数等同于以下代码：

```c
attron(A_STANDOUT);
```

事实上，`standout()` 函数可能只是一个使用 `attron(A_STANDOUT)` 函数作为定义的宏。

`standout()` 是一个较老的 C 函数，因此我建议避免使用它。请改用 `atattr()` 或 `attrset()`。

### 示例

```c
wstandout(output);
```

该语句为后续写入窗口 `output` 的任何文本激活 `standout` 属性。

### 示例程序

```c
#include <ncurses.h>

int main(void)

{
initscr();
addstr("*Yes, I must admit that ");
standout();
addstr("Chris");
standout();
addstr("* is my favorite pupil.");
refresh();
getch();

endwin();
return 0;
}
```

# 示例输出:

Yes, I must admit that Chris is my favorite pupil.

## 另参

第 3 章，`attrset()`, `attron()`

# `start_color()`

`start_color()` 函数用于可以显示彩色文本的终端，允许 NCurses 访问这些颜色能力。在 `start_color()` 初始化 NCurses 中的颜色之前，无法使用任何 NCurses 文本或背景颜色函数。

## Man Page 格式

```c
int start_color(void);
```

### 格式参考

该函数没有参数。

## 返回值

成功时返回 `OK`，意味着你的程序可以使用颜色函数和颜色属性。失败时返回 `ERR`。

## 注意

最初可以使用 `has_colors()` 函数来确定终端是否能够设置文本颜色。`start_color()` 传统上出现在 `initscr()` 或 `newterm()` 函数之后。

应用到窗口或窗口背景的颜色是以颜色对（color pairs）的形式创建的。参见 `init_pair()`。

颜色的应用类似于其他属性。参见 `attrset()`, `attron()`, `bkgd()`。也可以通过使用逻辑或构建一个 `ctypes` 字符，然后使用任何的 `ctypes` 字符函数将其置于窗口。

可以使用 `init_color()` 函数创建自定义颜色，尽管不是所有终端都支持它。另见 `can_change_color()` 函数。

终端可用的颜色数量可以通过检查 `COLORS` 常数找到。参见 `COLORS`。

另参阅本附录的 `COLORS` 条目以获取 NCurses 常数列表。

可用的颜色对数量可以通过检查 `COLOR_PAIRS` 常数找到。

### 示例

```c
start_color();
```

该函数为 NCurses 程序初始化颜色。

### 示例程序
