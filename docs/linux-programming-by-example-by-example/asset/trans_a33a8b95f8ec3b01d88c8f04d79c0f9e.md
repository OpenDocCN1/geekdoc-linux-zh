

# **输出**

必要的函数声明和变量定义在 <curses.h> 中声明。由于没有启动代码，需要通过调用 initscr 来初始化 ncurses 的数据结构。（通常，你会希望保存它返回的 WINDOW * 以便后续使用。）使用 printfw 函数（将在下一节中详细介绍），程序在调用 refresh 之后会向窗口显示一些输出，这样输出才会实际显示在屏幕上。经过三秒的暂停后，将在下一节“ncurses 终止”中介绍的 endwin 调用将终止程序并释放 initscr 分配的资源。

```
endwin();
exit(0);
}
```

![](img/be588b36b489136ce784030a08a1d3d4_260_0.png)

```
$ ./initcurs
```

![](img/be588b36b489136ce784030a08a1d3d4_260_1.png)

# ncurses 终止

在退出基于 ncurses 的应用程序之前，您需要返回 ncurses 分配的内存资源，并将终端重置为其原始的、非 ncurses 状态。初始化函数会分配内存资源，并将终端状态重置为对 ncurses 友好的模式。

相应地，您需要释放已分配的内存，并将终端重置为 pre-ncurses 模式。终止函数 endwin 和 delscreen 完成了这项工作。当您使用完一个 SCREEN 后，在将另一个终端设置为当前终端之前，请调用 endwin，然后调用 delscreen 以释放分配给该终端的 SCREEN 资源，因为 endwin 不会释放由 newterm 创建的屏幕的内存。

然而，如果您没有调用 *newterm*，而只使用了 *curscr* 和 *stdscr*，那么在退出前只需调用一次 *endwin* 即可。*endwin* 将光标移动到屏幕的左下角，并将终端重置为非可视化的、pre-*ncurses* 状态。分配给 *curscr* 和 *stdscr* 的内存没有被释放，因为您的程序可以通过调用 *endwin* 暂时挂起 *ncurses*，执行其他处理，然后调用 *refresh* 来恢复屏幕。

# 示例

![](img/be588b36b489136ce784030a08a1d3d4_261_0.png)

下面这个示例程序 *newterm* 演示了使用 *newterm* 和 *delscreen* 进行 *ncurses* 初始化和终止。

```
/*
 * newterm.c -curses initialization and termination
 */
#include <stdlib.h>
#include <curses.h>

int main(void)
{
    SCREEN *scr;

    if((scr = newterm(NULL, stdout, stdin)) == NULL) {
        perror("newterm");
        exit(EXIT_FAILURE);
    }

    if(set_term(scr) == NULL) {
        endwin();
        delscreen(scr);
        perror("set_term");
        exit(EXIT_FAILURE);
    }

    printf("This curses window created with newterm\n");
    refresh();
    sleep(3);

    printf("Going bye-bye now\n");
    refresh();
}

    sleep(3); 
    endwin(); 
    delscreen (scr); 
    exit(0);
```

该程序的输出与图 11.3 非常相似。在这个程序中，newterm 初始化了 curses 子系统，假装正在与另一个终端交互。然而，输入和输出仍然会来自并去往标准位置，因此 stdout 和 stdin 分别是 outfd 和 infd 的 FILE 指针。

但是，在程序使用 scr 之前，必须先将其设置为当前终端，因此需要调用 set_term。如果调用失败，您必须确保调用 endwin 和 delscreen 以释放与 scr 相关的内存，因此在调用 err_quit 之前增加了相应的代码。在向“终端”发送一些输出后，程序使用必需的 delscreen 调用关闭 curses 子系统。

## 输出

ncurses 有许多用于向屏幕和窗口发送输出的函数。重要的是要理解，C 语言的标准输出例程不能与 ncurses 的窗口一起使用，因为 ncurses 接管了终端上的输出。幸运的是，ncurses 的 I/O 例程与标准 I/O（<stdio.h>）例程的行为非常相似，因此学习曲线相对平缓。就本讨论而言，ncurses 的输出例程被分为字符、字符串和杂项类别。以下各节将详细讨论这些类别中的每一个。

### 字符输出

ncurses 的核心字符输出函数是 addch，其原型在 <ncurses.h> 中定义为 int addch (chtype ch);

几乎所有其他输出函数都通过调用 addch 来完成工作。它在当前窗口（通常是 stdscr）的光标当前位置显示字符 ch，并将光标推进到下一个位置。如果这样做会导致光标越过右边界，光标会自动换行到下一行的开头。如果光标位于窗口的底部，它会向上滚动一行。如果 ch 是制表符、换行符或退格符，光标会相应移动。其他控制字符使用 ~X 符号表示，其中 X 是该字符，插入符（~）表示它是一个控制字符。如果您需要发送字面控制字符，请使用函数 `echochar(ctype ch)`。

> **注意**
> ncurses 文档将在 `ctype` 格式中键入的字符称为“伪字符”。ncurses 将伪字符声明为无符号长整数，利用这些字符的高位来携带附加信息，例如视频属性。伪字符和普通 C 字符（char 类型）之间的区别意味着处理每种类型的函数在行为上存在细微差异。本章在适当的时候和地点会指出这些差异。

如前所述，`mvaddch` 在将光标移动到所需位置后向指定窗口添加一个字符；`mvwaddch` 结合了针对特定窗口的移动和输出操作，`waddch` 在用户指定的窗口中显示一个字符。`echochar` 函数及其针对特定窗口的对应函数 `wechochar` 将一次 `addch` 调用与一次 `refresh` 或 `wrefresh` 调用结合在一起。当与非控制字符一起使用时，这种组合可以带来显著的性能提升。

使用 `ctype` 字符和字符串（接下来讨论）的 ncurses 例程的一个特别有用的功能是，在显示之前，可以逻辑“或”（OR）各种视频属性与要输出的字符或字符串。这些属性的部分列表包括：

- `A_NORMAL`—正常显示模式
- `A_STANDOUT`—使用终端的最佳突出显示模式
- `A_UNDERLINE`—下划线
- `A_REVERSE`—使用反视频
- `A_BLINK`—闪烁文本
- `A_DIM`—半强度显示
- `A_BOLD`—额外强度显示
- `A_INVIS`—字符将不可见
- `A_CHARTEXT`—创建一个位掩码来提取字符

然而，取决于终端模拟器或屏幕的硬件功能，并非所有属性都可能可行或一定会正确显示。有关更多详细信息，请参阅 `curs_attr(3)` 手册页。

除了控制字符和增强了视频属性的字符外，字符输出函数还显示行图字符（来自 ASCII 字符集高半部分的字符，128–255），例如绘框字符和各种特殊符号。完整的列表可在 `curs_addch(3)` 手册页中找到。这里列出了几个常见的行图字符：

- `ACS_ULCORNER`—左上角
- `ACS_LLCORNER`—左下角
- `ACS_URCORNER`—右上角
- `ACS_LRCORNER`—右下角
- `ACS_HLINE`—水平线
- `ACS_VLINE`—垂直线

到目前为止描述的函数有效地向窗口“追加”字符，而不扰乱已存在其他字符的位置。另一组例程将字符插入现有窗口文本中的任意位置。这些函数包括 `insch`、`winsch`、`mvinsch` 和 `mvwinsch`。

遵循本章前面讨论的命名约定，这些函数中的每一个都在光标下方的字符之前（前面）插入一个字符，并将后续字符向右移动一个位置。如果最右边的字符位于右边界上，它将丢失。然而，请注意，插入操作后光标位置不变。插入操作在 `curs_insch(3)` 手册页中有完整记录。上述函数的原型如下列表所示：

```
int addch ( chtype ch );
int waddch ( WINDOW *win, chtype ch );
int mvaddch ( int y, int x, chtype ch );
int mvwaddch ( WINDOW *win, int y, int x, chtype ch );
int echochar ( chtype ch );
int wechochar ( WINDOW *win, chtype ch );
int insch ( chtype ch );
int winsch ( chtype ch );
int mvinsch ( int y, int x, chtype ch );
int mvwinsch ( WINDOW *win, int y, int x, chtype ch );
```

除非另有说明，所有返回整数的函数在成功时返回 OK，在失败时返回 ERR（OK 和 ERR 分别是定义在 `ncurses.h` 中的常数之一）。参数 win、y、x 和 ch 分别是显示字符的窗口、定位光标的 y 和 x 坐标，以及要显示的字符（包括可选属性）。

