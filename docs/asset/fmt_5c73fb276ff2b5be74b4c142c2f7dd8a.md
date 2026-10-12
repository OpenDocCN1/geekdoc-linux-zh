
```c
#include <ncurses.h>
#include <stdlib.h>

int main(void) {
    int y,x;
    char *c;

    initscr();
    start_color();
    init_pair(1, COLOR_RED, COLOR_WHITE);

    /* 为 ctypes 数组留出成员 */
    getmaxx(stdscr,y,x);
    c = calloc((x+1), sizeof(char));
    if (c == NULL) {
        endwin();
        puts("Unable to allocate memory.");
        return(1);
    }

    /* 在屏幕上写一些有趣的内容 */
    attron(COLOR_PAIR(1));
    addstr("This is a bit of text!");
    attroff(COLOR_PAIR(1));
    refresh();
    getch();

    /* 使用 inchstr 复制文本 */
    mvinchstr(0,0,c);
    mvaddstr(10,0,"Here is the ctypes read:\n");
    addch(c);
    refresh();
    getch();

    endwin();
    return 0;
}
```

# 318 附录 A ■ NCurses 参考

示例输出：

在白色背景上显示红色文字：

```
This is a bit of text!
```

# 另请参照

附录 C, `inch()`, `addchstr()`

# `init_color()`

`init_color()` 函数允许你重新定义 NCurses 可用于文本属性的颜色。对于支持此函数的终端，你可以通过调整单个红、绿、蓝值来创建颜色，理论上可以创建出十十亿种可能的颜色。

# 手册页格式

```c
int init_color(short color, short r, short g, short b);
```

## 格式参考

`c` 是表示要更改颜色编号的 `short` 类型。`c` 的有效值范围从 0 到 `COLOR` 的值。（参见 `COLOR`）。

`r`, `g`, 和 `b` 是表示所创建颜色的红、绿、蓝色调强度的 `short int`。取值范围从 0 到 1000，其中 0 是黑色，1000 是红、绿或蓝的满强度。

# 返回值

失败时返回 `ERR`，否则返回 `OK`。

## 注意事项

使用 `can_change_color()` 函数确定终端是否具有重新定义其设置颜色的能力。当 `can_change_color()` 返回 `TRUE` 时，可以使用 `init_color()` 函数。

# 附录 A NCurses 参考

当所有三个颜色参数（红、绿、蓝）都被设置为相同的值时，结果为灰色调。值越小，灰色越深；值越高，灰色越浅。

NCurses 使用的默认颜色与表 A-7 所示的 `init_color()` 语句有关。

`color_content()` 函数用于确定 NCurses 的红、绿、蓝颜色值，这与 `init_color()` 函数相反。参见本附录其他部分的 `color_content()`。

## 示例

```c
init_color(5,1000,500,0);
```

该语句定义 NCurses 中的颜色 5 为一种橙色调。满强度的红色和半强度的绿色等于橙色。

```c
init_color(6,1000,500,0);
```

该语句定义颜色 6 为紫色。

## 示例程序

```c
1 #include <ncurses.h>
2
3 #define NEW_COLOR 1
4 #define RED 1000
5 #define GREEN 750
6 #define BLUE 750
7
8 int main(void)
9 {
10     initscr();
11     start_color();
12     if(!can_change_color(NEW_COLOR))
13         addstr("*This probably won't work, but anyway:\n");
14
15     init_color(NEW_COLOR,RED,GREEN,BLUE);
16
17     init_pair(1,NEW_COLOR,COLOR_BLACK);
18     attrset(COLOR_PAIR(1));
19     printf("This is the new color %d.\n",NEW_COLOR);
20     refresh();
21     getch();
22
23     endwin();
24     return 0;
25 }
```

# 320 附录 A ■ NCurses 颜色

表 A-7: NCurses() 函数的值

| COLOR | INIT COLOR() | 常量名称 |
|---|---|---|
| 0 | init_color(0,0,0,0); | COLOR_BLACK |
| 1 | init_color(0,1000,0,0); | COLOR_RED |
| 2 | init_color(0,0,1000,0); | COLOR_GREEN |
| 3 | init_color(0,1000,1000,0); | COLOR_YELLOW |
| 4 | init_color(0,0,0,1000); | COLOR_BLUE |
| 5 | init_color(0,0000,000); | COLOR_MAGENTA |
| 6 | init_color(0,0,1000); | COLOR_CYAN |
| 7 | init_color(1000,1000); | COLOR_WHITE |

示例输出：

在白色背景上显示新颜色 1

# 另请参照

第3章, `can_change_color()`, `color_content()`

# `init_pair()`

`init_pair()` 函数将颜色组合分配给文本属性。`COLOR_PAIR(n)` 用于将颜色组合应用于整个文本背景。

# 手册页格式

```c
int init_pair(short pair, short f, short b);
```

## 格式参考

`pair` 是表示要更改颜色编号的 `short` 类型。有效值的范围从 0 到 `COLOR` 的值。`COLOR_PAIR(n)` 中的 `n` 是 `pair` 创建的颜色组合。

# 附录 A NCurses 参考 321

当三个颜色参数（红、绿、蓝）都被设置为相同的值时，结果为灰色调。值越小，灰色越深；值越高，灰色越浅。

NCurses 使用的默认颜色与表 A-7 所示的 `init_color()` 语句有关。

`color_content()` 函数用于确定 NCurses 的红、绿、蓝颜色值，这与 `init_color()` 函数相反。参见本附录其他部分的 `color_content()`。

# 返回值

颜色组合创建时返回 `OK`，否则返回 `ERR`。

## 注意事项

在使用此函数之前必须使用 `start_color()` 函数。`start_color()` 初始化 NCurses 颜色。颜色组合取值范围从 1 到 `COLOR-1`。这是因为颜色编号 0 被留作默认文本颜色（通常是黑底白字）。参见附录其他部分的 `assume_default_colors()` 函数。

## 示例

```c
init_pair(1,COLOR_WHITE,COLOR_BLUE);
```

该语句创建一个新的属性 `COLOR_PAIR(1)`，它在蓝色背景上显示白色文字。

```c
init_pair(13,4,2);
```

在这里，创建了 `COLOR_PAIR(13)`。颜色对应于 4 和 2，即绿色背景上的蓝色文字。（参见 `COLORS`。）

表 A-8: NCurses 颜色常量

| COLOR | 常量名称 |
|---|---|
| 0 | COLOR_BLACK |
| 1 | COLOR_RED |
| 2 | COLOR_GREEN |
| 3 | COLOR_YELLOW |
| 4 | COLOR_BLUE |
| 5 | COLOR_MAGENTA |
| 6 | COLOR_CYAN |
| 7 | COLOR_WHITE |

# 322 附录 A ■ NCurses 参考

## 示例程序
