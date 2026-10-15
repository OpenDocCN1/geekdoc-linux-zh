
## 格式参考

`event` 是 `MEVENT` 结构体的地址，将用于存储有关鼠标事件的信息。详细信息请见 `MEVENT`。

## 返回值

捕获到事件时返回 `OK`，如果没有可见事件则返回 `ERR`。

## 注意事项

`getmouse` 监控的事件类型由 `mousemask()` 函数预先确定的。请见 `mousemask()`。
实际上是 `get()` 函数读取了何时发生了过鼠标事件。`getmouse()` 函数用于将该事件的信息放入 `MEVENT` 结构中，以便程序进行处理。

## 示例

```
getmouse(&me);
```

此语句读取了最近的鼠标事件，并将事件信息存储在变量 `me` 引用的 `MEVENT` 结构中。

## 示例程序

```c
#include <ncurses.h>

int main(void)
{
    MEVENT mort;
    int ch;
7
8  initscr();
9  nocho();
10  keypad(stscr, TRUE);
11
12  mousemask(BUTTON1_CLICKED, NULL);
13  while(1)
14  {
15    ch = getch();
16    if (ch == KEY_MOUSE)
17     {
18      getmouse(&mort);
19      move(0,0);
20      cleol();
21      printf("Mouse clicked at %d, %d",mort.y,mort.x);
22      refresh();
23      continue;
24     }
25     if (ch == '\n')
26      break;
27    }
28  endwin();
29  return 0;
30 }
```
示例输出：
点击鼠标按钮将显示其位置：
`Mouse clicked at 10,14`

## 参见

第 13 章, `NCURSES_MOUSE_VERSION`, `MEVENT`, `mousemask()`, `ungetmouse()`

## `getstr()`

`getstr()` 函数从终端读取一行文本，以换行符或回车键（Enter）作为输入结束。

## 帮助页格式

```
int getstr(char *str);
int getstr(char *str, int n);
int wgetstr(WINDOW *win, char *str);
int wgetstr(WINDOW *win, char *str, int n);
int mvgetstr(int y, int x, char *str);
int mvgetstr(WINDOW *win, int y, int x, char *str);
int mvgetstr(int y, int x, char *str, int n);
```
`mvgetstr(WINDOW *win, int y, int x, char *str`

## 格式参考

`str` 是一个字符指针，代表输入字符串。

## 返回值

成功时返回 `OK`。

## 注意事项

`getstr()` 读取的缓冲区大小由调用者决定。如果输入超过缓冲区大小，则会被截断。

## 示例

```
char str[80];
getstr(str);
```

此示例将读取字符串并存储在变量 `str` 数组中。

## 292 附录 A = NCurses 引用

此语句读取光标在虚拟屏幕上的位置，并保存到 `row` 和 `col` 变量中。

## 示例程序

```c
#include <ncurses.h>

int main(void)
{
    WINDOW *win;
    int vy, vx, stdy, stdx, winy, winx;
    initscr();
    nocho();
    win = newwin(5,20,10,30);
    box(win,0,0);
    waddstr(win, "This is 'win'");
    wrefresh(win);
    getx(win,winy,winx);
    getx(stdscr,stdy,stdx);
    getx(vy,vx);
    printf("In Window win, the cursor is at %d,%d.\n", winy,winx);
    printf("On the standard screen, the cursor is at %d,%d.\n", stdy,stdx);
    printf("On the virtual screen, the cursor is at %d,%d.\n", vy,vx);
    refresh();
    getch();
    getx(vy,vx);
    printf("Now on the virtual screen, the cursor is at %d,%d.\n", vy,vx);
    refresh();
    getch();
    leaveok(win,TRUE);
    wrefresh(win);
    getx(win,winy,winx);
    getx(vy,vx);
    printf("In Window win, the cursor is now at %d,%d.\n", winy,winx);
    printf("On the virtual screen, the cursor is at %d,%d.\n", vy,vx);
    refresh();
    getch();
    endwin();
    return 0;
}
```

## 293 附录 A = NCurses 引用

示例输出：

在窗口 `win` 中，光标位于 0.13。
在标准屏幕上，光标位于 0.0。
在虚拟屏幕上，光标位于 10.43。

按回车键。

现在在虚拟屏幕上，光标位于 3.0。

再次按回车键。

在窗口 `win` 中，光标现在位于 0.13。
在虚拟屏幕上，光标现在位于 -1,-1。

## 另请参

`leaveok()`, `gettyx()`, `setsys()`

## `getwin()`

## 手册页格式

```c
WINDOW *getwin(FILE *file);
```

## 格式参考

`file` 是一个 `FILE` 变量，代表在磁盘上打开用于读取的文件。该文件应该是之前使用 `putwin()` 函数保存的窗口。

## 返回值

成功时，会创建一个窗口并返回代表该窗口的 `WINDOW` 指针。失败时，返回 `NULL`。

## 注意事项

`getwin()` 是 `putwin()` 的配套函数，后者将 `WINDOW` 数据保存到磁盘。

## 294 附录 A = NCurses 引用

窗口将在屏幕上的相同位置和大小恢复。甚至光标也会放置在它保存时的位置。当通过 `getwin()` 加载保存的窗口时，所有的文本属性都会恢复。相同的颜色对

## 示例

```c
nextwin = getwin(wfp);
```

该语句根据之前保存到磁盘并由 `wfp` 文件指针引用的数据创建一个名为 `footnote` 的新窗口。

## 示例程序

此程序假设文件 `WINDOW.DAT` 已经保存到磁盘。请参见 `putwin()`。

```c
1 #include <ncurses.h>
2 #include <stdlib.h>
3
4 #define FILENAME "window.dat"
5
6 void bomb(char *message);
7
8 int main(void)
9 {
10 FILE *wfile;
11 WINDOW *win;
12 int r;
13
14 initscr();
15 start_color();
16 initpair(1,COLOR_WHITE,COLOR_RED);
17
18 addstr("Press Enter to read the window from disk:\n");
19 refresh();
20 getch();
21
22 /* open the file */
23 wfile = fopen(FILENAME,"r");
24
25 if(wfile==NULL)
26 bomb("Error reading file\n");
27
28 /* write the window's data */
29 win = getwin(wfile);
30 if(win == NULL )
```
```c
bomb("Unable to read/create window\n");
close(wfile);
refresh(win);
getch();
endwin();
```
