
`int border(ls, rs, ts, bs, tl, tr, bl, br)` `int border(win, ls, rs, ts, bs, tl, bl, br)` `int box(win, vert, hor)`

在窗口边缘绘制一个边框（`stdscr` 或 `in`）。在下表中，你可以看到字符以及在调用 `box(...)` 时参数为 `0` 时的默认值。在图中，你可以通过框中的字符看到其位置。

`int vline(ch, n)` `int wvline(win, ch, n)` `int hline(ch, n)` `int whline(win, ch, n)`

这些函数从光标位置开始绘制垂直线或水平线。`ch` 是使用的字符，`n` 是绘制的字符数量。

光标位置不会移动。

### 8.6.5 背景字符

```
void bkgdset(ch) void wbkdset(win, ch)
```

设置屏幕或窗口的背景字符和属性。`ch` 中的属性将与窗口中的每个非空字符进行按位或运算。背景随后成为窗口的一部分，且不会因输入或输出滚动而改变。

```
int bkgdch(ch) int wbkdch(win, ch)
```

将更改背景字符和属性为。

## 8.7 输入

`int getch()` `int getch(win)` `int mvgetch(y, x)` `int mvgetch(win, y, x)`

`ch()` 将根据是否设置了延迟模式从终端读取输入。如果开启了延迟，`getch()` 将等待直到按下按键，否则它将返回输入缓冲区中的按键，如果缓冲区为空则返回 `ERR`。`mvgetch(...)` 和 `mvgetch(...)` 将光标移动到位置 `y,x`。第一个从终端读取到窗口 `win` 的前 `w` 个字符，`getch()` 和 `mvgetch(...)` 是与 `stdscr` 相关的终端读取的。

在启用了 `keypad(...)` 的情况下，当按下按键时，`getch()` 将返回一个在 `ncurses.h` 中定义的 `KEY *` 宏代码。当按下 `ESCAPE` （这可能是功能键的开头）时，`ncurses` 将启动第二个计时器。如果按键剩余的操作在此秒内未完成，则返回按键。否则，返回函数值。（如有必要，使用 `timeout()` 来禁用第二个计时器）。

```
int ungetch(ch)
```

将字符 `ch` 放回输入缓冲区。

`int getstr(str)` `int wgetstr(win, str)` `int mvgetstr(y, x, str)` `int mvgetstr(win, y, x, str)` `int getwstr(str, n)`

这些函数将系列调用 `getch()` 直到接收一行。

字符被放置在 `str` 中（因此在调用 `getstr(...)` 之前忘记为你的字符指针分配内存）。如果启用了回显（`echo`），字符串将回显（使用 `noecho()` 回显），并且删除字符将被解释。

```
ctype inch() ctype winch(win) ctype mwinch(y, x) ctype mvwinch(win, y, x)
```

## 8.8 选项

这些函数从屏幕或窗口返回一个字符。由于返回值的类型是 `ctype`，因此包含了属性信息。这些信息可以使用第 96 页表 8.4 上的 `A *` 常数从字符中提取。

```
int instr(str) int instr(str, n) int winstr(win, str) int winstr(win, str, n int mvinstr(y, x, str) int mvinnstr(y, x, str, n) mvwinstr(win, y, x, str) int mvinnstr(win, y, x, str, n)
```

从屏幕或窗口返回一个字符字符串。（注意：尚未实现。）

```
int chstr(chstr) int inchstr(chstr, n) int winchstr(win, chstr) int winchstr(win, chstr, n) int mvinstr(y, x, chstr) int mvinchstr(y, x, chstr, n) mvwinstr(win, y, x, chstr) int mvinchstr(win, y, x, chstr, n)
```

从屏幕或窗口返回一个 `ctype` 字符串。在字符串中，每个字符包含了属性信息。（注意：尚未实现，`inchstr` 未包含在 `ncurses` 库中。）

### 8.7.1 格式化输入

```
int scanf(fmt, ...) int wscanf(win, fmt, ...) int mvscanw(y, x) int mvscanw(win, y, x)
```

这些系列调用 `getch()` 直到接收到一行。

`int getch()` 将从终端读取输入，方式取决于是否设置了延迟模式。如果开启了延迟，`getch()` 将等待直到按下按键，否则它将返回输入缓冲区中的按键，如果缓冲区为空则返回 `ERR`。`mvgetch(...)` 和 `mvgetch(...)` 将光标移动到位置 `y,x`。第一个从终端读取到窗口 `win` 的前 `w` 个字符，`getch()` 和 `mvgetch(...)` 是与 `stdscr` 相关的终端读取的。

在启用了 `keypad(...)` 的情况下，当按下按键时，`getch()` 将返回 `ncurses.h` 中定义的 `KEY *` 宏代码。当按下 `ESCAPE`（这可能是功能键的开头）时，`ncurses` 将启动第二个计时器。如果按键剩余的操作在此秒内未完成，则返回按键。否则，返回函数值。（如有必要，使用 `timeout()` 来禁用第二个计时器）。

```
int ungetch(ch)
```

将字符 `ch` 放回输入缓冲区。

`int getstr(str)` `int wgetstr(win, str)` `int mvgetstr(y, x, str)` `int mvgetstr(win, y, x, str)` `int getwstr(str, n)`

这些函数将系列调用 `getch()` 直到接收到一行。

字符被放置在 `str` 中（因此在调用 `getstr(...)` 之前忘记为你的字符指针分配内存）。如果启用了回显（`echo`），字符串将回显（使用 `noecho()` 回显），并且删除字符将被解释。

```
ctype inch() ctype winch(win) ctype mwinch(y, x) ctype mvwinch(win, y, x)
```

## 8.8 选项

这些函数从屏幕或窗口返回一个字符。由于返回值的类型是 `ctype`，因此包含了属性信息。这些信息可以使用第 96 页表 8.4 上的 `A *` 常数从字符中提取。

```
int instr(str) int instr(str, n) int winstr(win, str) int winstr(win, str, n int mvinstr(y, x, str) int mvinnstr(y, x, str, n) mvwinstr(win, y, x, str) int mvinnstr(win, y, x, str, n)
```

从屏幕或窗口返回一个字符字符串。（注意：尚未实现。）

```
int chstr(chstr) int inchstr(chstr, n) int winchstr(win, chstr) int winchstr(win, chstr, n) int mvinstr(y, x, chstr) int mvinchstr(y, x, chstr, n) mvwinstr(win, y, x, chstr) int mvinchstr(win, y, x, chstr, n)
```

从屏幕或窗口返回一个 `ctype` 字符串。在字符串中，每个字符包含了属性信息。（注意：尚未实现，`inchstr` 未包含在 `ncurses` 库中。）

### 8.7.1 格式化输入

```
int scanf(fmt, ...) int wscanf(win, fmt, ...) int mvscanw(y, x) int mvscanw(win, y, x)
```

(注：此处原文中存在多处重复文本)

PC键盘上的按键和数字小键盘区域。

`keypad(stdscr,TRUE);`

现在，有两种主要的输入类型。

程序要求用户输入一个按键，然后根据该键调用相应的函数。（例如，类似于“按下 'q' 退出”并等待 `q`）

程序要求用户在屏幕上的掩码区域内输入一个字符字符串。例如：目录或数据库中的一个地址。

对于第一种类型，我们使用以下选项和模式，`while`循环将正常工作。

```c
char c;
noecho(); timeout(-1); nodelay(); cbreak(); keypad(stdscr,TRUE);
while(c=getch()){
 switch(c){
  'q': your_quit_function(); default: break;
 }
}
```

程序将挂起直到按下按键。如果按键是 `q`，我们调用退出函数，否则等待其他输入。

`switch`语句可以不断扩展，直到我们有一个符合愿望的输入函数。可以使用 `KEY *` 宏来检查特殊键，例如

`KEY_UP` `KEY_RIGHT` `KEY_A1` `KEY_B2` `KEY_C1`

`KEY_DOWN` `KEY_LEFT` `KEY_A3` `KEY_C3`

用于键盘上的方向键。对于文件查看器，循环可以像这样：

```c
int loop=TRUE; char c; enum {UP,DOWN,RIGHT,LEFT};
noecho(); timeout(-1); nodelay(); cbreak(); keypad(stdscr,TRUE);
while(loop=TRUE){
 c=getch()){switch(c){ KEY_UP: case 'u':
 case 'U': scroll_s(UP); break;
 8.9. 清除窗口和行
 case_DOWN: case 'd';
 case 'D': scroll_s(DOWN); break;
 case KEY_LEFT: case 'l';
 case 'L': scroll_s(LEFT); break;
 case KEY_RIGHT: case 'r';
 case 'R': scroll_s(RIGHT); break;
case 'q':
case 'Q': loop=FALSE; default: break;
}
```

对于第二种类型，我们只需要设置 **echo()**，用户输入的字符将打印到屏幕上。要让字符打印在你指定的位置，请使用 **move(...)** 或 **move(...)**。

或者，我们可以打开一个带有掩码的窗口（使用与窗口颜色不同的颜色即可），并要求用户输入字符串：

```c
WINDOW *maskin; WINDOW *maskin; char *ptr=(char *)malloc(255);
mainwin=newwin(3,37,9,21); maskwin=newwin(1,21,10,35); ...
mainwin=werase(maskwin);
box(mainwin,0,0); mvwaddstr(mainwin,1,Inputstring); ...
wnoutref(mainwin); wnoutref(maskwin); doudate(ate); ...
mvwgetstr(maskwin,0,0,ptr); ...
delwin(maskwin); delwin(mainwin); endif(); free(ptr);
```

请参考示例目录中的 `input.c` 获取更多详细说明。

## 8.9 清除窗口和行

- `int erase()` `intwin(werase(...)` 和 `erase()` 将空白复制到 `win` 或 `stdscr` 窗口的每个位置。例如，当你为窗口设置属性并调用 `erase()` 时，窗口会被着色。当我定义除黑底白以外的其他属性时，`COLOR PAIRS` 出现了一些问题，所以我写了自己的 `erase` 函数（这是对 `WINDOW` 结构的低级访问）：

```c
void NewClear(WINDOW *win)
{
int y,x;
for ( y = 0; y <= win->_maxy ; y++)
for ( x = 0; x < win->_maxx; x++)
(ctype*) win->line[y][x] = ' 'attrs; win->_curx = win->_cury = 0;
touchwin(win);
}
```

问题在于，`ncurses` 在清空屏幕时没有利用窗口属性。例如，在 `libctrl.c` 中，`BLANK` 定义为

#define BLANK ' 'A_NORMAL

这导致在行被清除时，其他窗口属性会丢失。

与 `erase()` 相同，但还会设置 `clearok()`（屏幕将在下次刷新时清空）。

`int clrtobot()` `int wclrtobot(win)`

清除当前光标所在的行（从光标右侧一个字符开始）和光标下方的行。

`int clrtoeol()` `int wclrtoeol(win)`

从光标位置到当前行末尾清除当前行。

## 8.10 更新终端

如概述所述，`ncurses` 窗口是内存中的图像。这意味着在完成刷新之前，窗口的任何更改都不会打印到物理屏幕上。这优化了屏幕输出，因为你可以进行大量操作，然后一次性刷新并打印到屏幕。否则，每次更改都会打印到终端，从而降低你程序的性能。

`int refresh(win)` `int wrefresh(win)`

`refresh(win)` 将 `stdscr` 复制到终端，而 `wrefresh(win)` 将窗口图像复制到 `stdscr`，然后鼠标光标看起来和 `stdscr` 一样。

`int outrefresh(win)` `int doudate()`

`wnoutrefresh(win)` 仅将窗口复制到 `stdscr`。这意味着虚拟屏幕 `stdscr` 并没有向终端输出任何内容，但它看起来就像程序员想要的那样。`doudate(win)` 执行向终端的输出。程序可以更改多个窗口，调用 `wnoutrefresh(win)`，最后调用 `doudate()` 刷新屏幕。

## 8.11 窗口属性和颜色

| 定义 | 属性 |
| :--- | :--- |
| A NORMAL | 属性 (ctype) 正常模式 |
| A STANDOUT | 突出显示 |
| A UNDERLINE | 下划线 |
| A REVERSE | 反转视频 |
| A BLINK | 闪烁 |
| A DIM | 变暗半亮 |
| A BOLD | 粗体或特亮 |
| A ALTCHARSET | 使用替代字符集 |
| A INVIS | 不可见 |
| A PROTECT | ??? |
| A CHARTEXT | 实际字符 |
| A COLOR | 颜色 |
| A PAIR(n) | 设置颜色对为 n |
| NUMBER(a) | 获取属性 a 的颜色对 |

表 8.4 ncurses 属性

| 定义 | 属性 |
| :--- | :--- |
| COLOR BLACK | 黑色 |
| COLOR RED | 红色 |
| COLOR | 绿色 |
| COLOR YELLOW | 黄色 |
| COLOR BLUE | 蓝色 |
| COLOR MAGENTA | 品红色 |
| COLOR CYAN | 青色 |
| COLOR WHITE | 白色 |

表 8.5 ncurses 颜色

## 8.11 窗口属性和颜色

`hascolors()`。`startcolor()` 将初始化 `COLORS`（终端支持的最大颜色）以及 `COLOR PAIR`（你可以定义的颜色对最大数量）。属性可以使用 OR 运算符 `|` 组合，这样你可以产生粗体闪烁输出。当你为窗口设置属性 `attr` 时，打印到该窗口的所有字符将具有该属性，直到你更改窗口属性。在滚动或移动窗口或其他操作时，它不会丢失。

当你为 `ncurses` 和 `BSD curses` 编写程序时，要小心颜色，因为 `BSD curses` 不支持颜色。（此外，旧的 `SYS V` 版本 `curses` 也不支持颜色）。因此编译所有库时需要使用 `#lidef` 操作。

具有 `colors()` 函数的终端，在此之前需要用 `startcolor()` 初始化颜色。

`bool has_colors()`

如果终端可以重新定义颜色，则返回 `TRUE`。

`int startcolor()`

颜色初始化。在使用颜色之前，必须调用此函数！

`int initpair(pair, fg, bg)`

当你将颜色作为窗口的属性使用时，你首先需要使用 `initpair(...)` 定义一个颜色对。`fg` 是颜色对的前景颜色，`bg` 是颜色对的背景颜色。这是一个从 1 到 `COLORPAIRS-1` 的值（没有无错，但 0 留给白底黑字）。一旦你就可以像属性一样使用 `pair`。

例如当你想在蓝色屏幕上显示红色字符时，执行：

```
init_pair(1,COLOR_RED,COLOR_BLUE);
```

现在使用 `wattr(...)` 将窗口设置为我们的新颜色对：

`wattr(win,COLOR_PAIR(1));` 或者，将颜色对与其他属性结合，例如：

```
wattr(win,A_BOLD)COLOR_PAIR(1));
wattr(win,A_STANDOUT)COLOR_PAIR(1));
```

第一个将调用颜色对并设置 **BOLD**（加粗），第二个将开启突出模式（standout），这样你在蓝色屏幕上就会红色高亮。

```
int contentpair(pair, f, b)
```

返回 `pair` 中的前景颜色和背景颜色。

```
int initcolor(color, r, g, b)
```

更改颜色 `color` 的颜色分量 `r`、`g` 和 `b`。`r`、`g` 和 `b` 的值范围从 1 到 `COLORS1`。

```
int contentcolor(color, r, g, b)
```

获取 `color` 的颜色分量 `r`、`g` 和 `b`。
