
```c
int maxx, maxy;

int y, x;

/* 初始化 ncurses */

initscr();

/* 绘制一个漂亮的边框 */

box(stdscr, ACS_VLINE, ACS_HLINE);

mvaddstr(stdscr, 1, 1, "INPUT: ");

refresh();

/* 读取字符直到遇到换行符 */

noecho();

while ((c = getch()) != '\n') {

    i++;

    getyx(stdscr, y, x);

    /* 在右边界处 */

    if (x == 79) {

        mvaddch(stdscr, y + 1, c);

    } else {

        waddch(stdscr, c);

    }

}

refresh();

echo();

refresh();

/* 打印字符计数 */

getmaxx(stdscr, maxx, maxy);

mvprintintw(stdscr, max - 2, "characters read: %d\n", i);

curs_set(0);

refresh();

/* 查看屏幕的时间 */

sleep(3);

/* 关闭 ncurses */

endwin();

return 0;

}
```

## 编程环境与接口

你首先注意到的点之一是 `nreadkey.c` 的长度大约是 `readkey.c` 的两倍。额外的代码处理了设置屏幕、定位光标等需求。要查看这些额外代码是否值得，请使用以下命令编译 `nreadkey.c`：

```bash
$ gcc nreadkey.c -lncurses -o nreadkey
```

运行该程序，输入 `./nreadkey`。图 29-6 显示了输入与之前为 `readkey` 输入相同文本后的结果。

基于 ncurses 的程序还可以读取从 `stdin` 管道传输的输入。图 29-7 显示了命令 `cat /etc/passwd | ./nreadkey` 的结果。

## 图 29-6
基于 ncurses 的 TUI

![](img/10f390c781aed9212971eac7c34e3f1c_780_0.png)

## 图 29-7
显示管道到基于 ncurses 程序的输入

![](img/10f390c781aed9212971eac7c34e3f1c_780_1.png)

## 在 Linux 中进行编程

正如你在配合 `rread.c` 程序使用的命令管道中所示（见列表 29-2），输入在第一行末尾被截断，因为 `/etc/passwd` 以换行符结束，而 `rread.c` 使用换行符来表示输入结束。

> 注意：有关关于 ncurses 的更多信息（包括下载信息），请访问 ncurses FAQ：http://invisible-island.net/nurses.faq.html。

## 使用 S-Lang 创建文本模式界面

S-Lang 由 John Davis 创建，是创建 TUI 的另一种替代方案。除了提供屏幕操作和控制例程外，S-Lang 还包含一个嵌入式的 S-Lang 解释器、一个简化某些编程部分的内置（内在）例程大型库，以及各种预定义的数据类型和数据结构。列表 29-4 显示与列表 29-3 相同的程序，进行了相应的更新以反映使用 S-Lang 代替 ncurses。

## 列表 29-4
使用 S-Lang 读取输入和写入输出

```c
/*
 * rereadkey.c - 基于 S-Lang 的简单 UI
 */
#include <stdio.h>
#include <string.h>
#include <slang/slang.h>
int main(int argc, char *argv[]) {
 int i = 0;
 unsigned int ch;
 /* 开始 slang */
SLang_get_terminfo();
SLang_init_tty(1, 0, 1);
SLmg_init_smg();
 /* 绘制一个漂亮的边框 */
SLmg_draw_box(0, 0, 24, 80);
SLmg_gotorc(1, 1);
SLmg_write_nchars("INPUT: *", 7);
SLmg_refresh();
 /* 读取 (1)字符直到遇到换行符 */
while(1) {
 i++;
 ch = SLang_getkey();
 if (ch == 13)
 break;
 if (SLmg_get_column() == 79)
 SLmg_gotorc(2, 1);
```
```c
SLsmg_write_char(ch);
SLsmg_refresh();
/* 打印字符计数 */
SLsmg_gotorc(22, 1);
SLsmg_write_nchars("characters read: ", 17);
SLsmg_printf("%d", i);
SLsmg_refresh();
/* 查看屏幕的时间 */
sleep(3);
/* 关闭 s-lang */
SLsmg_reset_msg();
SLang_reset_tty();
return 0;
}
```
要编译此程序，使用以下命令：

```bash
$ gcc rereadkey.c -lncurses -o rereadkey
```
输入 `./nreadkey`。图 29-6 显示了与之前为 `readkey` 输入相同文本后的结果。

## 图 29-6
基于 ncurses 的 TUI

| ncurses |
| :--- | :--- |
| INPUT: | characters read: |

## 在 Linux 中进行编程

正如你在配合 `rread.c` 程序使用的命令管道中所示，输入在第一行末尾被截断，因为 `/etc/passwd` 以换行符结束，而 `rread.c` 使用换行符来表示输入结束。

> 注意：有关关于 ncurses 的更多信息（包括下载信息），请访问 ncurses FAQ：http://invisible-island.net/nurses.faq.html。

## 使用 S-Lang 创建文本界面

-Lang 由 John Davis 创建，是创建 TUI 的另一种替代方案。除了提供屏幕操作和控制例程外，S-Lang 还包含一个嵌入式的 S-Lang 解释器、一个简化某些编程部分的内置（内在）例程大型库，以及各种预定义的数据类型和数据结构。列表 29-4 显示与列表 29-3 相同的程序，进行了相应的更新以反映使用 S-Lang 代替 ncurses。

## 列表 29-4
使用 S-Lang 读取输入和写入输出

```c
/*
 * rereadkey.c - 基于 S-Lang 的简单 UI
 */
#include <stdio.h>
#include <string.h>
#include <slang/slang.h>
int main(int argc, char *argv[]) {
 int i = 0;
 unsigned int ch;
 /* 开始 slang */
SLang_get_terminfo();
SLang_init_tty(1, 0, 1);
SLmg_init_smg();
 /* 绘制一个漂亮的边框 */
SLmg_draw_box(0, 0, 24, 80);
SLmg_gotorc(1, 1);
SLmg_write_nchars("INPUT: *", 7);
SLmg_refresh();
 /* 读取 (1)字符直到遇到换行符 */
while(1) {
 i++;
 ch = SLang_getkey();
 if (ch == 13)
 break;
 if (SLmg_get_column() == 79)
 SLmg_gotorc(2, 1);
```
```c
SLsmg_write_char(ch);
SLsmg_refresh();
/* 打印字符计数 */
SLsmg_gotorc(22, 1);
SLsmg_write_nchars("characters read: ", 17);
SLsmg_printf("%d", i);
SLsmg_refresh();
 /* 查看屏幕的时间 */
sleep(3);
 /* 关闭 s-lang */
SLsmg_reset_msg();
SLang_reset_tty();
return 0;
}
```
要编译此程序，使用以下命令：

```bash
$ gcc rereadkey.c -lncurses -o rereadkey
```
