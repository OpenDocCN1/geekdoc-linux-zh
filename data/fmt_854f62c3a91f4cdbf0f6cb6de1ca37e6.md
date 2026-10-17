
#### 6.4.4 核心函数集

本文并不打算成为 NCurses 的全面教程。关于这一点，你应该查阅多个在线参考手册或教程之一。此处的目标是解释核心库的底层概念并描述其提供的许多函数。下面是用于终端配置、光标移动、输出和输入的最重要、最基本、代表性的函数集合。

##### 配置函数

- `initscr()` 初始化 curses 库并创建逻辑屏幕。
- `endwin()` 关闭 curses 并重置屏幕。
- `wrefresh(win)` 将逻辑窗口 `win` 中的内容绘制到物理显示中。记住 `refresh()` 与 `wrefresh(stdscr)` 相同。
- `clear()` 清屏。
- `keypad(stdscr,TRUE)` 启用功能键和键盘键的使用（箭头、F1、...）

##### 输出和光标移动

- `move(r,c)` 将光标移动到屏幕位置 `(r,c)`。
- `getyx(win,y,x)` 获取当前光标位置。这是一个宏，因此 `y` 和 `x` 不必按地址传递。
- `addch(c)` 在当前光标位置绘制字符 `c` 到屏幕上，并将光标推进到字符末尾。如果 `c` 是制表符、换行符或退格符，光标会在窗口内适当移动。它在到达右边界时换行。
- `addstr(str)` 在当前光标位置绘制字符字符串 `str` 到屏幕上，并将光标推进到字符串末尾。它等价于对字符串中的每个字符调用 `addch()`。
- `addnstr(str, n)` 类似于 `addstr()`，但最多写入 `str` 的 `n` 个字符。如果 `n` 为 `-1`，则整个字符串将被添加，直到能容纳在行内的最大字符数，或直到遇到终止空字符。因此，`addstr(str)` 与 `addnstr(str,-1)` 相同。
- `mvaddch(y,x,c)` 将光标移动到屏幕上的位置 `(y,x)` 并在该位置绘制字符，同时将光标推进到字符末尾。
- `addchstr(str)` 类似于 `addstr(str)`，但：光标不推进，它不执行任何检查（如换行符、退格符或回车符），它不将其他控制字符扩展为 ^-转义，并且如果字符串跨越右边界则截断字符串，而不是将其换行到新行。
- `printw(fmt, ...)` 与 C 中的 `printf()` 相同，但打印到当前光标位置。

##### 输入

- `getch()` 从窗口读取一个字符。
- `getstr(str)` 读取字符直到收到换行符并存储（不含换行符）在 `str` 中（由调用者分配）
- `scanw(fmt, ...)` 与 C 中的 `scanf()` 相同 – 类似于调用 `getstr()`，传递给 `sscanf()`。

##### 窗口函数

- `win = newwin(l,c,y,x)` 创建一个新窗口，拥有 `l` 行、`c` 列，其左上角位于 `(y,x)`。返回指向新窗口的指针。
- `mvwin(win,y,x)` 将 `win` 指向的窗口移动到位置 `(y,x)`
- `win = dupwin(oldwin)` 复制 `oldwin`，返回指向新窗口的指针。
- `delwin(win)` 删除窗口 `win`，释放其所有资源。
- `putwin(win, filep)` 将 `win` 指向的窗口关联的所有数据写入 `filep` 指向的 `FILE` 流。底层写入失败时返回 `ERR`。
- `win = getwin(filep)` 读取由 `putwin` 存储到文件中的所有窗口数据，并使用该数据创建并初始化一个新窗口。这返回指向新窗口的指针。

##### 概要

`initscr()` 函数将终端初始化为 curses 模式。它在某些实现中也可能清除屏幕。这必须始终首先调用。它初始化 NCurses 系统并为 `stdscr` 和 `curscr` 窗口以及一些其他数据结构分配内存。当程序结束时，它应始终调用 `endwin()` 以重置终端并释放 curses 资源。

初始化 curses 之后，有几个函数可用于配置终端。通常会用 `clear()` 清屏，如果程序想要接收键盘和功能键的按键，则应调用 `keypad(stdscr, TRUE)`。上面未显示的其他函数包括影响终端驱动处理模式的函数 – `raw()` 和 `cbreak()`、`echo()` 和 `noecho()`，以及 `halfdelay()`。我们稍后会讨论这些。

输出函数可以分为三个系列：

`addch()` 在光标位置打印一个字符并移动光标

`addstr()` 在光标位置打印一个字符串并移动光标

`printw()` 打印类似 `printf()` 的格式化输出并移动光标

因此，`addch()` 添加一个字符，`addstr()` 添加一个字符串，而 `printw()` 打印格式化文本。对于其中每一个，都有许多变体，下面会进行描述。

光标可以通过 `move()` 函数在不输出的情况下移动。它的当前位置可以使用 `getyx()` 获取。`mvaddch()` 函数代表了一类在输出操作之前先移动光标的函数。总的来说，对于每个输出函数如 `addch()`，都有一个对应的形式为 `mvaddch()` 的函数。例如，存在 `mvaddstr()` 函数和 `mvprintw()` 函数。

基本输入函数是 `getch()` 和其字符串对应函数 `getstr()`，以及类似 `scanf()` 的 C 风格 `scanw()`。请注意 `getch()` 没有参数，但 `getstr()` 期望一个指向已分配缓冲区的指针，用来存储输入的文本。

最后，以上所有函数都作用于标准屏幕 `stdscr`。它们都是宏。对于其中每一个，都有一个作用于任意窗口的函数，并且命名约定使得很容易猜出它们。例如，`wgetch(win)` 是一个从当前窗口 `win` 读取字符的输入函数，而 `getch()` 被定义为 `wgetch(stdscr)`。类似地，`waddch(win,ch)` 在 `win` 中的光标位置放置一个字符，而 `addch(ch)` 被定义为 `waddch(stdscr,ch)`。

可以使用 `newwin()` 创建窗口，它在堆上分配内存并返回指向它的指针。如果 `newwin()` 对 `lines` 或 `columns` 中的任一个传入 `0`，则该维度被设置为它能容纳的最大值并适合终端窗口。函数确保在所有情况下新窗口都不会超出终端屏幕的边界。可以使用 `mvwin()` 移动窗口；你必须刷新才能看到变化。这不会从屏幕上擦除旧窗口，你必须自己处理。你可以使用 `dupwin()` 复制一个窗口，并使用 `delwin()` 删除一个窗口。

#### 6.4.5 关于窗口和刷新的重要要点

- 当你对屏幕进行更改时，调用 `refresh()` 或 `wrefresh()` 是一个好主意，但你应该牢记几个重要点。
- `addch()` 和 `addstr()` 系列的函数向屏幕写入字符串和字符时总是会自行调用 `wrefresh()`，因此在添加字符串或字符时无需刷新。`printw()` 函数并非如此。
- 当向屏幕绘制许多窗口时，如果对每个窗口调用 `wrefresh()`，可能会导致输出突发和性能不佳。`wrefresh()` 函数实际上调用了两个函数，`wnoutrefresh()` 和 `doupdate()`。调用 `wnoutrefresh(win)` 将 `win` 指向的 `WINDOW` 复制到逻辑屏幕上，而 `doupdate()` 将逻辑屏幕复制到物理屏幕上。因此，最好为每个要写入屏幕的窗口调用 `wnoutrefresh(win)`，然后再进行一次 `doupdate` 调用。
- `getch()` 和 `getstr()` 系列的输入函数如果窗口自上次刷新以来已被移动或修改，将会对给定窗口调用 `wrefresh()`。如果 `echo` 打开，则会自动进行刷新，因为这是一种修改。明确地说，`getch()` 将调用 `refresh()`，而 `wgetch(win)` 将调用 `wrefresh(win)`。这可能对程序的行为产生严重后果，因为光标会移动到 `wgetch(win)` 正在调用的窗口中，并且刷新也可能产生意想不到的后果。
- 最后，作为一条通用规则，你永远不应编写混合使用标准屏幕 `stdscr` 和其他窗口的 NCurses 程序。作用于标准屏幕的输入、输出和刷新函数会以意想不到的方式与其他窗口交互。如果你想编写简单的程序，就不要在其中使用窗口，反之，如果你觉得程序会从使用窗口中受益，那么就不要使用任何作用于标准屏幕的函数。

#### 6.4.6 几个简单程序

遵循传统，我们从一个 hello-world 程序开始。

```
Listing 6.1: helloworld.c

Listing. helloworld.c

#include <ncurses.h>

int main()

{

    initscr();                /* initialize the library */

    printw("Hello World !!!\n");  /* print at cursor */

    refresh();                /* update screen (unnecessary) */

    getch();                  /* wait for a keypress */

    endwin();                 /* clean up and quit curses */

    return 0;

}
```

输入调用 `getch()` 用来防止屏幕在我们看到之前就消失。下一个程序更有趣一些。
