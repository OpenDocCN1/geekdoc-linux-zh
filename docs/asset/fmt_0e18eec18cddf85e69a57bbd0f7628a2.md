
在前面的代码列表中，`readkey.c` 从 `stdin` 读取输入直到遇到换行符（当你按下 Enter 键时产生）。然后它显示输入的文本和读取的字符数（计数包括换行符）并退出。

这是它的工作原理：

```
$ ./readkey
INPUT: There are three primary means of creating programs that interact with users at the command line
There are three primary means of creating programs that interact with users at the command line
characters read: 96
```

由于本书的格式限制，文本换行很奇怪。你可以使用 `cat` 命令从 `stdin` 为 `readkey.c` 提供输入：

```
$ cat /etc/passwd | ./readkey
INPUT:root:x:0:0:root:/bin/bash
characters read: 28
```

在这种情况下，你只看到 `/etc/passwd` 的第一行，因为文件的每一行都以换行符结束。应该明确，程序化地与命令行是简单的，但并不用户友好。

## 使用 ncurses 创建文本模式界面

使用 `S-Lang` 和 `ncurses` 进行屏幕处理可以创建更美的程序，但正如你预期的那样，界面更好的代价是更复杂的代码。`ncurses`（意为新的 curses）是经典 UNIX 屏幕处理库的重新实现。`curses` 一词源于 `cursor optimization`（光标优化），这简洁地描述了 curses 库的作用：以最快的方法重绘屏幕并将光标放在正确的位置。

## 772 第 VI 部分 在 Linux 中编程

`ncurses` 为屏幕控制和鼠标输入提供了简单的高级接口。它包含了处理键盘和鼠标输入、创建和管理多个窗口、使用菜单、表单强大例程。`ncurses` 通过通用应用程序与屏幕或终端之间的接口工作。

考虑到数以百计的终端、屏幕和终端程序，以及它们拥有的不同功能（更不用说这些功能的不同命令），UNIX 程序员很快开发出了抽象屏幕的方法。与其为各种终端类型编写大量额外代码，`ncurses` 为程序员提供了统一且通用的接口。`ncurses` API 为程序员屏蔽了底层硬件。

`ncurses` 为字符应用程序提供了许多与图形应用程序类似的功能——多个窗口、表单、菜单和面板。`ncurses` 窗口可以独立管理，可以包含相同或不同的内容，可以滚动或显示隐藏。表单允许程序员创建易于使用的数据和显示窗口，简化了通常困难且特定于应用程序的编码任务。面板扩展了 `ncurses` 处理重叠和堆叠窗口的能力。菜单提供了菜单，再次具有更简单、通用的编程接口。

为了让你了解 `ncurses` 的工作原理以及使用它所涉及的代码，列表 28-3 显示了列表 28-2 中引入的 `readkey.c` 程序（现在命名为 `nreadkey.c`），它已适配以与 `ncurses` 工作。

```
#include <stdio.h>
#include <curses.h>

int main(int argc, char *argv[])
{
    int c, i = 0;
    int maxx, maxy;
    int y, x;

    /* 启动 ncurses */
    initscr();

    /* 画一个漂亮的框 */
    box(stdscr, ACS_VLINE, ACS_HLINE);
```

## 第 28 章 编程环境与接口 773

```
mvaddstr(stdscr, 1, 1, "INPUT: **");
refresh();

/* 读取字符直到遇到换行符 */
nocho();
while ((c = getch()) != '\n') {
    i++;
    getx(stdscr, y, x);
    /* 在右侧边界 */
    if (x == 79) {
        mvaddch(y + 1, 1, c);
    } else {
        waddch(stdscr, c);
    }
}
refresh();
echo();
refresh();

/* 打印字符计数 */
getmaxxy(stdscr, max, maxy);
mwprintw(stdscr, max - 2, 1, "*characters read: %d\n", i + 1);
curs_set(0);
refresh();

/* 查看屏幕的时间 */
sleep(3);

/* 关闭 ncurses */
endwin();

return 0;
```

你首先注意到的是 `nreadkey.c` 的长度大约是 `readkey.c` 的两倍。额外的代码处理了设置屏幕、定位光标等需求。为了查看这些额外代码是否值得，可以使用以下命令编译 `nreadkey.c`：

```
$ gcc nreadkey.c -lncurses -o nreadkey
```

运行该程序，输入 `./nreadkey`。图 28-5 显示了输入之前为 `readkey.c` 输入相同文本后的结果。

基于 `ncurses` 的程序还可以读取从 `stdin` 管道传输的输入。图 28-6 显示了命令 `cat /etc/passwd | ./nreadkey` 的结果。

![](img/a123b4f2456cac935474ae2401b95b01_805_0.png)

图 28-5：基于 ncurses 的 TUI。

![](img/a123b4f2456cac935474ae2401b95b01_805_1.png)

图 28-6：显示管道到基于 ncurses 程序的输入。

正如你在配合 `readkey.c` 程序使用命令管道（见列表 28-2）所示，输入在第一行末尾被截断，因为 `/etc/passwd` 中的每一行都以换行符结束，而 `readkey.c` 使用换行符表示输入结束。

> 如需更多关于 `ncurses` 的信息（包括下载信息），请访问 ncurses 网页：http://dquery.his.com/ncurses/ncurses.html。

## 使用 S-Lang 创建文本模式接口

`S-Lang` 由 John Davis 创建，是创建 TUI 的替代方案。除了提供屏幕操作和光标控制程序外，`S-Lang` 还包含一个嵌入式的 `S-Lang` 解释器、一个简化某些编程部分的内置（固有）程序大型库，以及各种数据类型和数据结构。列表 28-4 显示了与列表 28-3 相同的程序，但进行了相应的更新以使用 `S-Lang` 代替 `ncurses`。

### 列表 28-4：使用 S-Lang 读取输入和写入输出

```
/*
  * spreadkey.c -一个基于 S-Lang 的简单 UI
*/
#include <stdio.h>
#include <string.h>
#include <slang/slang.h>

int main(int argc, char *argv[])
{
    int i = 0;
    unsigned int ch;

    /*  s-lang *//
    SLtt_get_terminfo();
    SLng_init_tty(-1, 0, 1);
    SLmg_init_smg();

    /* 绘制一个边框 *//
    SLmg_draw_box(0, 0, 24, 80);
    SLmg_gotorc(1, 1);
    SLmg_write_nchars("*INPUT: ", 7);
    SLmg_refresh();

    /* 读取字符直到换行符 *//
    while(1)
    {
        i++;
        ch = SLng_getkey();
        if (ch == 13)
            break;
        if (SLmg_get_column() == 79)
            SLmg_gotorc(2, 1);
        SLmg_write_char(ch);
        SLmg_refresh();
    }

    /* 打印字符计数 *//
    SLmg_gotorc(22, 1);
    SLmg_write_nchars("characters read: ", 17);
    SLmg_printf("%d", i);
    SLmg_refresh();

    /* 查看屏幕的时间 *//
    sleep(3);

    /* 关闭 s-lang *//
    SLmg_reset_smg();
    SLng_reset_tty();

    return 0;
}
```

使用以下命令编译此程序：

```
$ gcc sreadkey.c -lslang -o sreadkey
```
