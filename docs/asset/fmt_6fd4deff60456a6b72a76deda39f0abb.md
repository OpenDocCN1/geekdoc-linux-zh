
# Linux 程序员指南：第 8 章

```c
int echo()
int noecho()
```

设置 `echo()` 以显示用户输入的字符，设置 `noecho()` 则保持静默。

```c
int halfdelay(t)
```

类似于带有 `t` 秒延迟的 `cbreak()`。

```c
int nodelay(win, bf)
```

终端将设置为非阻塞模式。如果没有输入准备就绪，`getch()` 将返回 `ERR`。如果设置为 `FALSE`，`getch()` 将等待到按下键为止。

```c
int timeout(t)
int wtimeout(win, t)
```

建议使用这些函数代替 `halfdelay(t)` 和 `nodelay(win, bf)`。`getch()` 的结果取决于 `t` 的值。如果 `t` 为正数，读取将阻塞 `t` 毫秒；如果 `t` 为零，则不阻塞；当 `t` 为负数时，程序阻塞直到输入可用。

```c
int notimeout(win, bf)
```

如果 `bf` 为 `TRUE`，`getch()` 将使用一个特殊的计时器（长度为一秒）来解释以键开头的输入序列（如 `ESC` 等）。

```c
int typeahead(fd)
```

如果 `fd` 为 -1，则不进行预读检查，否则 `ncurses` 将使用文件描述符 `fd` 代替这些检查。

```c
int intrflush(win, bf)
```

当 `bf` 设置为 `TRUE` 时，在终端上按下中断键（`quit`, `break` ...）将刷新所有输出到 `tty` 驱动程序队列。

```c
void noqiflush()
void qflush()
```

（注意：尚未实现。）

## 终端属性

`int baudrate()`

返回以 `bps` 为单位的终端速度。

`char erasechar()`

返回当前的删除字符。

`char killchar()`

返回当前的终止字符。

`int has_ic()`

`int has_il()`

如果终端具有插入/删除字符的能力，则 `has_ic()` 返回 `TRUE`；`has_il()` 在终端具有插入/删除行的能力时返回 `TRUE`。否则函数返回 `ERR`。（注意：尚未实现。）

`char *longname()`

返回的指针用于访问当前终端的描述。

`ctype termattrs()`

（注意：尚未实现。）

`char *termname()`

返回用户环境变量中的 `TERM` 内容。（注意：尚未实现。）

## 使用选项

现在我们已经看到了窗口选项和终端模式，现在是时候描述它们了。

首先，在 `Linux` 上你应该启用小键盘。这将允许使用 `PC` 键盘上的光标键和数字小键盘。

现在有两种类型的输入：

1. 程序希望用户输入一个键，然后根据该键调用一个函数。（例如，诸如“按 `'q'` 退出”并等待 `q`）

2. 程序希望用户在屏幕上的掩码中输入一个字符串。例如：目录或数据库中的地址。

对于第一种情况，我们使用以下选项和模式，`while` 循环将正常工作。

程序将挂起直到按下按键。如果按键是 `q`，我们调用相应的函数，否则我们等待其他输入。

`switch` 语句可以扩展，直到我们获得符合愿望的输入。使用 `KEY_` 宏来检查特殊键，例如键盘上的光标键。对于文件查看器，循环可以像这样：

对于第二种情况，我们只需要 `echo()`，用户输入的字符将打印到屏幕上。要让字符打印在您想要的位置，请使用 `move(...)` 或 `wmove(...)`。

或者，我们可以打开一个带有掩码的窗口（使用与窗口不同的颜色即可），并要求用户输入字符串：

> 出版者备注：缺少示例。

请查看示例目录下的 `c` 文件以获取更多解释。

## 更新终端

如概述所述，`ncurses` 窗口是内存中的图像。这意味着在完成 `refresh` 之前，窗口的任何更改都不会打印到物理屏幕上。这优化了到屏幕的输出，因为你可以进行很多操作，然后调用 `refresh` 将其打印到屏幕。否则，每次更改都会打印到终端，并降低程序的性能。

```c
refresh()
refresh(win)
```

`refresh()` 将内容拷贝到终端，`wrefresh(win)` 将窗口图像拷贝到终端并执行操作。

```c
int wrefresh(win)
int doupdate()
```

`wnoutrefresh(win)` 将窗口 `win` 拷贝到虚拟屏幕。这意味着实际上没有向终端输出输出，虚拟屏幕看起来就像程序员想要的那样。`doupdate()` 将执行向终端的输出。程序可以更改多个窗口，为每个窗口调用 `wnoutrefresh(win)`，然后调用 `doupdate()` 一次更新物理屏幕。

例如，我们有一个有两个窗口的程序。我们通过修改某些文本行来更改两个窗口。我们可以编写带有 `wrefresh(win)` 的 `changewin(win)`。

这将导致 `curses` 更新两次终端并减慢我们的执行速度。使用 `doupdate()`，我们 `changewin(win)`，我们的主函数将获得更好的性能。

```c
int redrawwin(win)
int redrawnlin(win, bline, nlines)
```

在向其中写入新内容之前，如果应该丢弃某些行或整个屏幕，请使用这些函数（可能是当行被清除等时候）。

```c
int touchwin(win)
int touchline(win, start, count)
```

## Linux 程序员指南：第 8 章

当窗口开启时，可以使用以下函数对内容进行滚动。

（注意：如果在窗口的最后一行打印新行，窗口也会发生滚动。因此，请小心使用 `scrollok(...)`，否则将得到不可理的结果。）

```c
int scroll(win)
```

此函数将窗口（以及数据结构中的行）向上滚动一行。

```c
int scroll(win)
int wscroll(win, n)
```

这些函数将根据整数 `n` 的值向上或向下滚动窗口。如果 `n` 为正，窗口将向上滚动 `n` 行；如果 `n` 为负，则窗口将向下滚动 `n` 行。

```c
int setscrollreg(t, b)
int wsetscrollreg(win, t, b)
```

设置软件滚动区域。

以下代码可以解释如何实现屏幕文本滚动的效果。

另请示例目录中的 `.c` 文件。

> 注意

> 出版者备注：代码缺失。

我们有一个 18 行 66 列的窗口，想要在其中滚动文本。`S[]` 是包含文本的字符数组。`Max_s` 是 `s[]` 中最后一行的行号。`Clear_line` 将从当前光标位置到行尾打印空白字符，使用窗口的当前属性（而不是 `A_NORMAL` 那样）。`Beg` 是当前屏幕上显示的 `s[]` 的最后一行。`Scroll` 是一个枚举，用于告诉函数执行的操作：显示文本的下一行或上一行。

## 填充 (Pads)

```c
WINDOW *newpad = *subpad(orig, nlines, ncols, begy, begx)
int prerefresh(pad, pminrow, pmincol, sminrow, smincol, smaxrow, smaxcol)
int pnoutrefresh(pad, pminrow, pmincol, sminrow, smincol, smaxrow, smaxcol)
int pechochar(pad, ch)
```

## 软标签 (Soft-Labels)

```c
int slk_init(int fmt)
int slk_set(int labnum, char *label, int fmt)
int slk_refresh()
int slk_noutrefresh()
char *slk_label(int labnum)
int slk_clear()
int slk_restore()
int slk_touch()
int slk_attr(ctype attr)
int slk_attrset(ctype attr)
int slk_attroff(ctype attr)
```

这些函数对应 `attron(attr)`, `attrset(attr)` 和 `attroff(attr)`。尚未实现。

## 杂杂

```c
int beep()
int flash()
char *unctrl(ctype c)
char *keyname(int c)
int filter()
```

（注意：尚未实现。）

```c
void use_env(bf)
int putwin(WINDOW *win, FILE *filep)
```

（注意：尚未实现。）

```c
WINDOW *getwin(FILE *filep)
```

（注意：尚未实现。）

```c
int delay_output(int ms)
int flushinp()
```

## 低级访问
