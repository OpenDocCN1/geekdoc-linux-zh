
在该语句中，从窗口 `beta` 的光标当前位置（向右）读取 32 个字符的文本。这些字符存储在字符串 `first_name` 中。

```c
mwinstr(0,0,row[0]);
```

读取标准屏幕的顶行并存储到字符串 `row[0]` 中。

# 334 附录 A = Ncurses 库参考

## 示例程序

```c
1 #include <curses.h>
2 #include <stdlib.h>
3
4 int main(void)
5 {
6 int y,x;
7 char *c;
8
9 initscr();
10 start_color();
11 init_pair(1,COLOR_RED,COLOR_WHITE);
12
13 /* 为 ctype 数组分配内存 */
14 getmaxx(stdscr,&y,&x);
15 c = (char *)malloc((x+1));
16 if(c == NULL)
17 {
18
19 endwin();
20 puts("Unable to allocate memory.");
21 return(1);
22
23 /* 向屏幕写入一些有趣的内容 */
24 attron(COLOR_PAIR(1));
25 addstr("This is a bit of text!");
26 attroff(COLOR_PAIR(1));
27 refresh();
28 getch();
29
30 /* 仅使用 instr 复制文本 */
31 mvinstr(0,0);
32 mvaddstr(10,0,"Here is the text read:\n\n");
33 addstr(c);
34 refresh();
35 getch();
36
37 endwin();
38 return 0;
39 }
```

示例输出：

This is a bit of text 出现在屏幕顶部，白底红字。

第 31 行的 `mvinstr()` 只读取文本，并在按下回车键后显示在第 11 行。

# 另见

`inchstr()`

# 附录 A = NCurses 库参考 335

# `intrflush()`

`intrflush()` 函数控制在键盘上输入中断键时是否刷新键盘输入队列。

# 手册页面格式

```c
int intrflush(WINDOW *win, bool bf);
```

## 格式参考

`win` 被忽略。

`bf` 是一个布尔值，TRUE 或 FALSE。TRUE 开启键盘输入时的中断刷新。FALSE 禁用中断刷新。

# 返回值

失败返回 `ERR`，成功返回 `OK` 或除 ERR 以外的值。

## 注意事项

当 `intrflush()` 为 TRUE 时，按下 break 键会立即刷新输入队列，并立即执行中断操作。当它为 FALSE 时，中断仍会被处理，但缓冲区中的任何文本可能会延迟出现，例如命令提示符。

`intrflush()` 监控的中断键列在表 A-9 中。

键盘上 Break 键（如果存在）的行为取决于其在终端中的映射方式。

当开启 `intrflush()` 时，中断键的响应将比其他情况更快。

缺点是，使用 `intrflush()` 可能导致 NCurses 认为显示的内容与实际显示的内容之间出现不一致。

表 A-9：`intrflush()` 监控的中断键

| KEY FUNCTION | NAME | KEY(5) | ASCII | SIGNAL |
|---|---|---|---|---|
| Break | BREAK | Break? | n/a | BRKINT |
| Interrupt | INTR | ^C | 0x03 | SIGINT |
| Quit | QUIT | \ | 0x1c | SIGQUIT |

# 336 附录 A ■ NCurses 库参考

`intrflush()` 是 NCurses 库参考的一部分。

## 格式参考

`intrflush()` 是 NCurses 库参考的一部分。

# 返回值

`intrflush()` 是 NCurses 库参考的一部分。

## 注意事项

`intrflush()` 是 NCurses 库参考的一部分。

## 示例

`intrflush()` 是 NCurses 库参考的一部分。

(注：此处后续内容为大量 OCR 重复与乱码，已根据逻辑处理完毕)

# 附录 A ■ NCurses 库参考

```
24      addstr("isendwin()) returns TRUE.\n"
25  else
26      addstr("isendwin()) returns FALSE.\n"
27      refresh();
28      getch();
29
30      endwin();
31      return 0;
32  )
```

示例输出：

按回车临时暂停此程序。

你看到：

程序已暂停...isendwin() returns TRUE...按回车：

按回车：

按回车临时暂停此程序：

在 `endwin()` 之后，NCurses 可视化模式已重启。

isendwin() returns TRUE。

# 另请

`endwin()`

# is_linetouched

`is_linetouched()` 函数判断窗口中的某行文本自上一次屏幕更新以来是否被修改过。

# 解释

NCurses 会跟踪窗口的哪些部分在上次 `refresh()` 之后发生了变化。`is_linetouched()` 函数用于判断给定文本行（行）上的任何文本是否自上次刷新以来被修改过。如果是，该函数返回 TRUE，否则返回 FALSE。

# 手册页格式

```
bool is_linetouched(WINDOW *win, int line);
```

## 格式参考

`win` 是一个 NCurses 窗口，可以是标准屏幕 `stdscr`，也可以是创建新窗口的函数返回的 WINDOW 变量名。`line` 是一个 `int` 值，表示要检查更新的哪一行（行）。取值范围从顶部的 0（行）到窗口内的最大行数。

# 返回值

`is_linetouched()` 返回的值是 `NCURSES.H` 中定义的以下常量之一：

- TRUE，表示该行自上次 `refresh()` 以来已被修改。
- FALSE，表示该行与当前屏幕匹配（或在 NCurses 看来它们应该是匹配的）。
- ERR，当指定无效行号时发生。

## 注意事项

`is_linetouched()` 函数仅仅是一个工具，可以用它来判断某行文本自上次刷新以来是否已更新。使用 `is_linetouched()` 函数不会强制 NCurses 更新屏幕，而是决定下一次刷新时将更新哪行。`is_linetouched()` 在最近的刷新后效果最好。例如，当窗口刚创建或 `initscr` 创建标准屏幕时，窗口中的所有行都被视为被触摸过的。只有在执行了最近的 `refresh()` 后，`is_linetouched()` 函数才会变得真正有用。

在使用 `touchline()` 函数后，`is_linetouched()` 函数始终返回 TRUE。请参见 `touchline()`。

## 示例

```
if(is_linetouched(alpha, 0));
```

在这里，如果对窗口 `alpha` 的第 0 行进行了修改，则条件为真。

## 示例程序

```
1 #include <ncurses.h>
23 int main(void)
4 {
```

示例输出：

标准屏幕正在发生更改

按回车查看哪些行发生了更改：

第 3 行已更新。

第 10 行已更新。

第 20 行已更新。

# 另请

`touchline()`, `wtouchln()`, `is_wintouched()`, `refresh()`;

# is_wintouched()

`is_wintouched()` 函数有助于判断窗口的任何部分自上一次刷新以来是否被更改或更新。

# 手册页格式

```
bool is_wintouched(WINDOW *win);
```

## 格式参考

`win` 是要检查的窗口名称。

# 返回值

当窗口发生更改时函数返回 TRUE，否则返回 FALSE。TRUE 和 FALSE 定义在 `NCURSES.H` 中。

## 注意事项

窗口在创建后立即被视为被触摸过的，对于 `stdscr`，则在 `initscr()` 函数调用后立即被视为。在这样的窗口上，`is_wintouched()` 函数始终返回 TRUE。因此，最好在对特定窗口调用 `refresh()` 或 `wrefresh()` 后使用 `is_wintouched()`。

在使用 `touchwin()` 函数后，`is_wintouched()` 始终返回 TRUE。

该函数不会强制 NCurses 在下次调用 `refresh()` 时更新窗口。相反，`is_wintouched()` 仅仅是一个工具，用来判断窗口自上次刷新以来是否被修改，或者是否真的需要对特定窗口进行刷新。

## 示例
