
```c
void bomb(void) {

    addstr("Unable to allocate memory for new window.\n");

    refresh();

    endwin();

    exit(1);

}
```

第 12 行的 `start_color()` 函数初始化了颜色但没有错误检查：我假设你的终端支持颜色，并且 `start_color()` 不失败。在你的“实际”程序中，请始终使用 `has_colors()` 并测试 `start_color()` 是否返回 `OK`，再处理颜色。

程序定义了四个颜色对，每个颜色对都通过 `wattr()` 函数分配给特定的窗口。示例输出如图 8-2 所示。如你看到的，四个窗口是独立映射且边界清晰的（尽管在书中没有颜色）。

![](img/b0e33f0db107583cf9267e27aa42f380_123_0.png)

图 8-2：为四个窗口着色

## 别再重复我了！

在列表 8-6 中 quad 系列程序的第三个版本增加了一个 while 循环，以向你展示 NCurses 及其窗口的另一个方面。

### 列表 8-6：quad3.c

（注意：提供的原始文本中 quad3.c 的代码是不完整的。）

## 第 8 章 窗口，无处不在的窗口！103

### 8-6（续）

```c
41    wbkgd(d,COLOR_PAIR(4));
40    mvwaddstr(d,0,0,"This is window D\n\n");
42    wrefresh(d);

44    /* 更新每个窗口 */
45    do

47    {
48        ch = getch(a);
49        waddch(b,ch);
50        waddch(c,ch);
51        waddch(d,ch);
52        wrefresh(b);
53        wrefresh(c);
54        wrefresh(d);
55    } while(ch != '~');

57    endwin();
58    return 0;

60
61    void bomb(void)
62    {
63        addstr(NULL, "Unable to allocate memory for new window.\n");
64        refresh();
65        endwin();
66        exit(1);
67    }
```

简而言之：

- 第 45 行到 54 行是新的；创建了一个输入循环。`get()` 函数会自动显示输入，这在这里很有用，可以避免标准屏幕的闪烁预览。`get()` 函数在第 47 行中使用。它从窗口 `a` 读取一个字符输入，该字符也会显示在窗口 `a` 上。其余的函数在其他窗口上显示相同的字符。

> 注意：尽管 Ncurses 仅使用一个输入队列，但可以从特定窗口读取输入。这样做主要是为了修改文本，因为某些输入函数可以通过各种窗口进行过滤。请参阅附录 A 中 `get()` 的条目。

## 练习

编写一个 NCurses 程序，创建两个并排的窗口。当你在第一个窗口输入字时，文本也会出现在第二个窗口中，但应用了 rot13 算法（rot13 是一种简单的加密，字母和 N 交换，B 和 O，C 和 P，以此类推）。

我的解决方案可以在这本书的配套页面找到：www.c-for-dummies.com/ncurses/.

# 第 9 章

## 子窗口

子窗口是 NCurses 中奇特而有趣的生物。从一个角度来看，它们正如你想象的那样：窗口中的小窗口。但同时，由于 NCurses 实现子窗口的方式，它们并不像那样。

我曾对 NCurses 的子窗口概念感到困惑。事实上，互联网上的许多文档声称子窗口是有 Bug 的应该避免。这并不准确。通过正确的理解，子窗口是 NCurses 中节省时间的工具，完全不需要避免。

### 子窗口的问题

子窗口在 NCurses 中就像真实的窗口，它们共享相同的数据结构。你像创建全窗口一样使用 `WINDOW` 变量来创建子窗口。控制或操作窗口的 NCurses 函数也会控制和操作子窗口（有少数例外）。但子窗口并不是真实窗口。

子窗口与真实窗口的主要区别在于子窗口共享内存。因此，当你向子窗口放入一个字符时，也将该字符放入了父窗口。

例如，在图 9-1 中，屏幕上有两个窗口。较小的窗口是子窗口，它具有与父窗口不同的颜色属性。父窗口显示 Hello，而子窗口显示 Dad。这同样存在于父窗口中。内存是共享的。

如果你更改子窗口中的文本，你也会更改父窗口中的文本。同样，父窗口也可以更改子窗口中的文本。只有当你假设子窗口是一个普通窗口时，这才会令人困惑和沮丧。它并不是。

认为子窗口仅仅是引用父窗口特定部分的方便方法是。图 9-2 展示了使用子窗口引用屏幕区域的示例。图 9-2 底部框出的区域偶尔会被重写或更新。与其进行大量的复杂的定位计算，只需在适当的位置创建一个子窗口；然后使用该窗口作为引用。这就是使用子窗口定义屏幕区域的一个示例。

只要你将子窗口视为父窗口特定部分的引用，你就能很好地使用子窗口。但当你认为子窗口是独立的、唯一的（就像真实窗口一样），你会遇到各种麻烦。

![](img/b0e33f0db10758cf9267e27aa42f380_128_0.png)

图 9-1：一个子窗口

main（大小不定的窗口）

| | | | 窗口的顶部 | 期望的 |
|---|---|---|---|---|
| | | | 显示 | |
| C7D0044 | Lorem ipsum sit amet, consectetuer elit, sed diam nonummy tincidunt ut laoreet dolore erat volutpat. | | | 滚动 | |
| | | | | 文本 |
| C7D0045 | Ut ad minim veniam, quis nostrud ullamco suscipit ut aliquip ea comm consequat. | | | | |
| C7D0046 | Ipsum dolor sit amet, consectetuer elit, sed diam nonummy nibh | | | | |
| C7D0047 | Tincidunt ut laoreet magna erat volutpat. Ut ad minim veniam. | | | | |
| C7D000A | Quis nostrud exercitation ullamco suscipit ut aliquip ea commando consequat. | | | | |

**图 9-2：** 一个实用的子窗口示例

| 事件 | 时间戳 |
|---|---|
| | 45,84 K |
| 2008年6月18日 星期三 @ 21:30 | 67,494 K |
| 2008年6月18日 星期三 @ 23:47 | 8,777 K |
| 昨天 @ 04:51 | 23 K |
| | >1 K |
| 子窗口 "A" 显示信息 | 子窗口 "B" 显示信息 |
| | |

## 创建子窗口

子窗口具有真实窗口的所有基本属性：名称、大小、位置、唯一坐标等。因为它们与父窗口共享内存，所以子窗口必须完全位于父窗口内部。自然，子窗口是通过自己的函数创建的：

```c
subwin(win, rows, cols, y)
derwin(win, rows, cols, x)
```

这些函数唯一的区别在于最后的参数。对于 `subwin()`，`y` 和 `x` 是相对于屏幕的坐标；对于 `derwin()`，`y` 和 `x` 是相对于父窗口的。创建后，子窗口可以像任何其他窗口一样被引用、在面向窗口的命令中命名、删除或像普通窗口一样受到影响。子窗口甚至可以拥有自己的子窗口。

## 你的子窗口

子窗口完全存在于父窗口内部。在某种程度上，将它们视为父窗口的特定部分是有帮助的，尽管子窗口维护自己的光和文本，并且

```c
subwin(win, rows, cols, y)
```

`subwin()` 函数创建子窗口。对于 `subwin()`，`y` 和 `x` 是相对于屏幕的坐标；对于 `derwin()`，`y` 和 `x` 是相对于父窗口的。正如图 9-1 代码所示，当 `subwin()` 成功时，创建了一个窗口，子窗口同样存在于父窗口中。

图 9-1：kid1

```c
#include <curses.h>
int main(void)
{
    WINDOW *sonny;
    initscr();
    start_color();
    init_pair(1,COLOR_WHITE,COLOR_BLUE);
    init_pair(2,COLOR_RED,COLOR_YELLOW);
    /* 创建子窗口 */
```
