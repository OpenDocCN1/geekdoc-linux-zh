
```
printf("This is an curses window\n");

refresh();

sleep(3);

printf("Going bye-bye now\n");

refresh();

sleep(3);

endwin();

exit(0);

}
```

我们在第 6 行包含了 `<curses.h>` 以获取必要的函数声明和变量定义。在任何其他输出存根的情况下，我们立即在第 11 行通过调用 `initscr()` 来初始化 curses（否则，你想要检查它的返回值）。在第 16 行和第 20 行，我们使用 `printf` 函数（将在下一节中详细介绍）向窗口显示一些输出，并在第 17 行和第 21 行刷新显示，以便输出内容实际出现在屏幕上。在第二秒钟停顿后（第 18 行和第 22 行），我们终止程序，调用 `endwin()`（第 23 行）来释放分配的资源。

# 列表 27.2 newterm.c

```c
1 /*
2 * Listing 27.2
3 * newterm.c - curses 初始化和终止
4 * */
5 #include <stdlib.h>
6 #include <curses.h>
7 #include <errno.h>

9 int main(void)
10 {

    SCREEN scr;

    if((scr = newterm(NULL, stdout, stdin)) == NULL) {
        perror("newterm");
        exit(EXIT_FAILURE);
    }

    if(set_term(scr) == NULL) {
        perror("set_term");
        endwin();
        delscreen(scr);
        exit(EXIT_FAILURE);
    }

    printf("This curses window created with newterm(\n");
    refresh();
    sleep(3);

    printf("Going bye-bye now\n");
    refresh();
    sleep(3);
    endwin();
    delscreen(scr);

    exit(0);
}
```

该程序与第一个程序非常相似。（注：原文中存在大量重复的句子，此处根据逻辑意图翻译并已去重。）

# 使用 nurses 进行屏幕操作
第 27 章 445

位置；如果最右侧的字符在右边界上，它将丢失。但请注意，在插入操作后光标位置不会改变。插入操作在 `insch(3)` 手册中有详尽记录。我们到目前为止提到的函数原型如下所示：

```
int addch(chtype ctype);
int wch(WINDOW *win, ctype ctype);
int mvaddch(int y, int x, ctype ctype);
int mvaddwch(WINDOW *win, int y, int x, ctype ctype);
int echochar(chtype ctype);
int wechochar(WINDOW *win, ctype ctype);
int insch(chtype ctype);
int winsch(WINDOW *win, ctype ctype);
int mvinsch(int y, int x, ctype ctype);
int mvinsch(WINDOW *win, int y, int x, ctype ctype);
```

除非另有说明，所有函数在成功时返回整数 `OK`，失败时返回 `ERR`（`OK`、`ERR` 以及其他常量定义在 `<nurses.h>` 中）。参数 `y`、`x` 和 `ch` 分别是字符将显示的窗口、定位光标的 `y` 和 `x` 坐标，以及要显示的字符（包括可选属性）。提醒一下，带有 "w" 前缀的例程将移动指针的操作（指定窗口和 `(y, x)` 位置）与输出操作结合。

# 字符串例程

nurses 的字符串例程的行为通常与字符例程相似，区别在于它们处理的是伪字符字符串或普通的空字符终止字符串。同样，nurses 的设计者创建了一种标准符号来帮助程序员区分这两类函数。包含 `chr` 的函数名对伪字符进行操作，而仅包含 `str` 的名称则使用 C 风格（空字符终止）字符串。处理伪字符字符串的函数部分列表包括

```
int addch(const ctype *chstr);
int addchstr(const ctype *chstr, int n);
int wch(WINDOW *win, const ctype *chstr);
int cochstr(WINDOW *win, const ctype *chstr, int n);
int mvaddch(int y, int x, const ctype *chstr);
int mvaddwch(int y, int x, const ctype *chstr, int n);
int winsch(WINDOW *win, int y, int x, const ctype *chstr);
int mvinschstr(WINDOW *win, int y, int x, const ctype *chstr, int n);
```

所有列出的函数都将 `chstr` 拷贝到从光标位置开始的目标窗口，且光标不会移动（这与字符输出函数不同）。如果字符串比当前行能容纳的还要长，它会在右边界被截断。

# 用户界面编程
第四部分

四个接受 `n` 参数的例程——`addchnstr()`、`waddchnstr()`、`mvaddchnstr()` 和 `mvaddwnstr()`——会复制最多 `n` 个字符，并在右边界处停止。如果 `n` 为 -1，则将复制整个字符串，但根据需要会在右边界处进行截断。

下一组字符串输出函数处理空字符终止字符串。与前一组不同，这些函数会移动光标。此外，字符串输出会在右边界处换行，而不是被截断。否则，它们的行为与其类似的 `chtype` 对应函数一致。

```
int dcstr(const char *str);
int addstr(const char *str, int n);
int wadstr(WINDOW *win, const char *str);
int waddstr(WINDOW *win, const char *str, int n);
int mvaddstr(int y, int x, const char *str);
int mvaddstr(WINDOWS *win, int y, int x, const char *str); // 注意：OCR 有重复的 mvaddstr，可能是 mvaddwnstr 或类似
int mvaddstr(WINDOWS *win, int y, int x, const char *str, int n);
```

记住，这些例程中的 `str` 是标准的、空字符的字符数组。

我们查看的下一组也是最后一组输出例程是输出相关的：用于绘制边框和线条、清除和设置背景、控制输出选项、移动光标以及向 curses 窗口发送格式化输出。

# 杂项输出例程

要设置窗口的背景属性，使用 `bkgd()`，其原型为

```
int bkgd(const maint ch);
```

`ch` 是字符与一个或多个出的视频属性的逻辑或（OR）组合。要获取当前的背景设置，请调用 `getbkgd(WINDOW *win)`；其中 `win` 是目标窗口。设置和获取窗口背景函数的完整描述可以在 `curs_bkgd(3)` 页面中找到。

至少有七个函数可以在 curses 窗口中绘制边框、框和线条。`box()` 调用是最简单的，它使用一个字符绘制垂直线，另一个字符绘制水平线，在指定窗口周围画一个框。它的原型如下：

```
int box(WINDOW *win, chtype verch, chtype horch);
```

`ver` 设置用于绘制垂直线的伪字符，`horch` 用于绘制水平线。

```
int border(WINDOW *win, chtype ls, chtype rs, chtype ts, chtype bs, chtype tl, chtype tr);
```

## 使用 ncurses 进行屏幕操作

```c
clear();
waddch(stdscr, 'X');
waddch(stdscr, 'Y', A_REVERSE);
mvwwaddch(stdscr, 2, 1, 'Z', A_BOLD);
refresh();
sleep(3);
app_exit();
```

如你在第 14 行和 15 行所示，`addch()` 输出指定的字符并移动光标。第 15 行和 16 行说明了如何将视频属性与要显示的字符结合起来。我们还在第 16 行演示了一个典型的以 "mv-" 前头的函数。在刷新屏幕后，通过短时间的暂停可以让你查看结果。请注意，在调用 `refresh` 之前，屏幕上不会显示任何变化。第 21–25 行使用窗口特定的例程并以 `stdscr` 为目标窗口重复了该过程。

列表 27.4 简要演示了字符串输出函数。

### 列表 27.4 cursstr.c

```c
/*
 * 列表 27.4
 * cursstr.c - curses 字符串输出函数
 */
#include <stdlib.h>
#include <curses.h>
#include <errno.h>
#include <unistd.h>
int main(void)
{
    int xmax, ymax;
    WINDOW *tmpwin;
    app_init();
    getmaxx(stdscr, ymax, xmax);
    addstr("Using the *str() family\n");
    nhline(ACS_HLINE, xmax);
    mvaddstr(3, 0, "This string appears in full\n");
    nmvaddstr(5, 0, "This string is truncated\n", 15);
    refresh();
    sleep(3);
    if((tmpwin = newwin(0, 0, 0, 0)) == NULL) {
        err_quit("newwin");
    }
    mvwaddstr(tmpwin, 1, 1, "This message should appear in a new window");
    wbox(tmpwin, 0, 0);
    touchwin(tmpwin);
    wrefresh(tmpwin);
    sleep(3);
    delwin(tmpwin);
    app_exit();
}
```

第 16 行的 `getmaxxy()` 调用获取了 `stdscr` 的列数和行数——该例程的语法不需要 `ymax` 和 `xmax` 指针。由于我们调用 `mvwaddstr()` 时传入的值 `n=15`，我们想要打印的字符串会在 "truncated" 中的字母 "t" 之前被截断。我们在第 25 行创建了新窗口 `tmpwin`，其尺寸与当前屏幕相同。我们在新窗口中写入了一条消息（第 28 行），在其周围绘制了一个边框（第 29 行），并调用 `refresh()` 将显示在屏幕上。在退出之前，我们对窗口调用了 `delwin()` 以释放其资源（第 34 行）。

列表 27.5 演示了如何使用线条图形字符以及 `box()` 和 `wbox()` 调用。请特别注意第 17–24 行。某些输出例程在输出后会移动光标，而另一些则不会。同样注意，线条绘制族函数（如 `cline()`）是从上到下、从左到右绘制的，在使用它们时要注意光标的位置。

### 列表 27.5 cursbox.c

```c
/*
 * 列表 27.5
 * cursbox.c - curses 框绘制函数
 */
#include <stdlib.h>
#include <curses.h>
#include <errno.h>
#include <unistd.h>
int main(void)
{
    int ymax, xmax;
    app_init();
    getmaxx(stdscr, ymax, xmax);
    mvaddch(0, 0, ACS_ULCORNER);
    hline(ACS_HLINE, xmax - 2);
    mvaddch(ymax - 1, 0, ACS_LLCORNER);
    vline(ACS_VLINE, xmax - 2);
    mvaddch(0, xmax - 1, ACS_URCORNER);
    vline(ACS_VLINE, ymax - 2);
    mvvline(1, xmax - 1, ACS_VLINE, ymax - 2);
    mvaddch(ymax - 1, xmax - 1, ACS_LCORNER);
    mvprintw(ymax / 3 - 1, (xmax - 30) / 2, "border drawn the hard way");
    refresh();
    sleep(3);
    clear();
    box(stdscr, ACS_VLINE, ACS_HLINE);
    mvprintw(ymax / 3 - 1, (xmax - 30) / 2, "border drawn the easy way");
    refresh();
    sleep(3);
    clear();
    wborder(stdscr, ACS_VLINE, ACS_HLINE, A_BOLD);
    mvprintw(ymax / 3 - 1, (xmax - 30) / 2, "border drawn with wborder");
    refresh();
    sleep(3);
    app_exit();
}
```

正如你所预期的，第 23 行的 `mvvline()` 调用在绘制垂直线之前移动了光标。毕竟，`box()` 返回的是一个简单的边框。`wborder()` 函数比 `box()` 更详细，但允许对用于绘制边框的字符进行更精细的控制，它受底层硬件的支持。使用 ncurses 需要……（注：原文此处似乎不完整，翻译已根据上下文保持连贯）。

# 用户界面编程
第四部分

# 列表 27.6 续

```
31 }
32 echo();
33 str[i] = '\0';
34 pwin;
35 wrefresh(pwin);
36 mvprintw(pwin, 1, 1, "You typed: %s\n", str);
37 box(pwin, ACS_VLINE, ACS_HLINE);
38 wrefresh(pwin);
39 sleep(3);

41 delwin(pwin);
42 app_exit();
43 }
```

在我们成功初始化 ncurses 子系统后

# 列表 27.7 cursgstr.c

```
1 /*
2 * 列表 27.7
3 * cursgstr.c 字符串输入函数
 */
5 #include <stdlib.h>
6 #include <curses.h>
7 #include <errno.h>
8 #include <string.h>
9 #include "utilfns.h"

11 int main(int argc, char *argv[])
12 {
    int c, i = 0;
    char str[20];
    char *pstr;

    app_init();
```

# 使用 ncurses 进行屏幕操作

```
crmode();
printf("File to open: *");
refresh();
getstr(str);
printf("You typed: %s\n", str);
refresh();
sleep(3);
if((pstr = malloc(sizeof(char) * 20)) == NULL)
    err_quit("malloc");
printf("Enter your name: *");
refresh();
getstr(pstr, 20);
printf("You entered: %s\n", pstr);
refresh();
sleep(3);
free(pstr);
app_exit();
```
