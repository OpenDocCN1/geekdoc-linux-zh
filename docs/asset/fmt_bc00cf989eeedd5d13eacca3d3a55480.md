
### 列表 7-7：arrowkeys.c

```c
1 #include <ncurses.h>
2
3 int main(void)
4 {
5 int ch;
6
7 initscr();
8
9 keypad(stdscr, TRUE);
10 do
11 {
12 ch = getch();
13 switch(ch)
14 {
15 case KEY_DOWN:
16 addstr("Down\n");
17 break;
18 case KEY_UP:
19 addstr("Up\n");
20 break;
// (续)
21 case KEY_LEFT:
22 addstr("Left\n");
23 break;
24 case KEY_RIGHT:
25 addstr("Right\n");
26 default:
27 break;
28 
29 }
30 refresh();
31 while(ch != '\n');
32
33 endwin();
34 return 0;
35 }
```

在你的计算机键盘上找到方向键。当你按下每个方向键时，你会看到屏幕上显示出该键的方向，如图 7-1 所示。

> **注意**，其他按键也会显示。这是因为 `getch()` 处于模式，这就是它的行为方式。

> **注意** 你可能需要关闭数字小键盘，才能使用标准 PC 键盘上 8、4、6 和 2 键上的方向键。

**图 7-1：** ARROWSKEYS.C 源代码的输出

# 第 7 章 ■ 键盘狂热！ 85

## 键盘上的布局

当 `keypad()` 函数激活了键盘的额外按键后，你可以使用 `NCURSES.h` 中的定义来帮助程序读取按键。

要确定哪些键对你可用，请参考表 7-1。更完整的列表可以在附录 D 中找到。

你可能想要运行一些测试以确保程序中的 NCurses 可以访问功能键。例如，要检查功能键 5，你应该使用：

```c
ch == KEY_F(5)
```

作为比较条件。记住，`ch` 必须是 `int` 类型，而不是 `char`（这是一个常见错误）。

此外请注意，你的操作系统可能仍然会从你的程序中夺取功能键。如果是这样，使用 NCurses 中的 `raw()` 函数将功能键直接传递给你的程序。有关 `raw()` 函数的更多信息请参阅附录 A。

## 高亮菜单栏

结合本书到为止学到的知识，你现在应该能够使用 NCurses 玩出花样。其中之一就是华酷的移动条系统，类似于图 7-2 所示。

### 表 7-1：某些特殊键定义

| 定义 | 键盘按键 |
| :--- | :--- |
| `KEY_UP` | 光标向上方向键 |
| `KEY_DOWN` | 光标向下方向键 |
| `KEY_LEFT` | 光标向左方向键 |
| `KEY_RIGHT` | 光标向右方向键 |
| `KEY_HOME` | Home 键 |
| `KEY_NPAGE` | 下页或分页 |
| `KEY_PPAGE` | 上页或上一页 |
| `KEY_END` | End 键 |
| `KEY_BACKSPACE` | 退格键 |
| `KEY_F(n)` | 功能键 n |

操作菜单系统涉及按下键盘上的向上或向下方向键。当你这样做时，高亮条会向上或向下移动以选择菜单项目。按下 Enter 键可选择该项目。

考虑到 Ncurses 的工作方式，华酷界面的源代码其实并不困难。列表 7-8 显示了实现一种的方法。

### 列表 7-8：menubar.c

```c
1 #include <ncurses.h>
2 #define MENUMAX 6
3
4 void drawmenu(int item)
5 {
6 int c;
7 char mainmenu[] = "Main Menu";
8 char menu[MENUMAX][21] = { /* MENUMAX 的 6 个项目 */
9 "Answer E-mail",
10 "Off to the Web",
11 "Word processing",
12 "Financial management",
13 "Maintenance",
14 "Shutdown",
15 };
16 
17 clear();
18 addstr(mainmenu);
19 for(c=0;c<MENUMAX;c++)
20 {
21 if(c==item)
22 attron(A_REVERSE) /* 高亮选择 */
23 mvaddstr(3*(c+2),20,menu[c]);
24 unattroff(A_REVERSE); /* 取消高亮 */
25 }
26 }
```

### 列表 7-8（续）

```c
// （代码逻辑）
```

```c
// 列表 7-7：arrowkeys.c
...
3 int main(void)
4 {
5 int ch;
6
7 initscr();
8
9 keypad(stdscr, TRUE);
10 do
11 {
12 ch = getch();
13 switch(ch)
14 {
15 case KEY_DOWN:
16 addstr("Down\n");
17 break;
18 case KEY_UP:
19 addstr("Up\n");
20 break;
// (续)
21 case KEY_LEFT:
22 addstr("Left\n");
23 break;
24 case KEY_RIGHT:
25 addstr("Right\n");
26 default:
27 break;
28 
29 }
30 refresh();
31 while(ch != '\n');
32
33 endwin();
34 return 0;
35 }
```

```c
// 列表 7-8：menubar.c
1 #include <ncurses.h>
2 #define MENUMAX 6
3
4 void drawmenu(int item)
5 {
6 int c;
7 char mainmenu[] = "Main Menu";
8 char menu[MENUMAX][21] = { /* MENUMAX 的 6 个项目 */
9 "Answer E-mail",
10 "Off to the Web",
11 "Word processing",
12 "Financial management",
13 "Maintenance",
14 "Shutdown",
15 };
16 
17 clear();
18 addstr(mainmenu);
19 for(c=0;c<MENUMAX;c++)
20 {
21 if(c==item)
22 attron(A_REVERSE) /* 高亮选择 */
23 mvaddstr(3*(c+2),20,menu[c]);
24 unattroff(A_REVERSE); /* 取消高亮 */
25 }
26 }
```

*注：列表 7-8 的 OCR 在源码处截断了，我合并了可用部分。*

# 需要窗口参数的命令

在本书到为止，你已经体验了使用 `stdscr` 指代终端窗口的命令。以下是一些示例：

```
getmaxxy(win,row,col)
getyx(win,y,x)
keypad(win,bf)
odelay(win,bf)
```

这些命令中的每一个都需要一个 `win` 或窗口（window）参数，这样 NCurses 才能知道屏幕上哪个窗口是它引用的窗口。本书之前的章节使用 `stdscr` 来表示标准屏幕，这是 NCurses 创建的唯一窗口。也可以使用其他窗口名称，即你自行创建的新窗口名称。（更多内容将在几节后介绍。）

## 伪命令（Pseudo Commands）

NCurses 中几乎所有的文本输出函数都需要一个 `win` 参数，指定将输出发送到哪个窗口。作为 `win` 参数，`stdscr` 并不被频繁使用，因为许多命令文本输出函数已经针对与 `stdscr` 的配合进行了定制；这些文本输出函数以写在 `NCURSES.H` 文件中的特殊宏的形式存在。

例如，向屏幕添加一个字符的 `addch()` 函数实际上是一个宏。实际的函数名为 `waddch()`，其格式如下：

```
waddch(win,ch);
```

`addch` 宏（或伪函数）在 `NCURSES.H` 中看起来如下：

```
#define addch(ch)
nwaddch(stdscr,ch)
```

因此，你在程序中任何时候使用 `addch()`，编译器都会在后台将其替换为适当基于窗口的函数 `waddch()`，并指定 `stdscr` 为命名窗口。

伪函数已用于本书教程到目前为止介绍的所有字符输出和文本输出函数。使用较短的、非窗口版本的函数并没有错；我的目的仅仅是告诉你，无论你是否在使用函数的窗口版本，NCurses 它的命令始终引用的是一个特定的窗口。

惊喜吧！

# 第 8 章 = 窗口，窗口无处不在！

你的伪函数的（真实）版本与该伪函数的名称相同。
