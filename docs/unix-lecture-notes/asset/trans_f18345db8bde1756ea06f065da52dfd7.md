

它表现。 我们将看到我们可以使用这个接口来执行诸如抑制字符回显和在不等待按下 Enter 键的情况下传输字符等操作。

more? 提示无法消失的问题更难解决，也需要理解如何控制终端。 一种替代方案是学习更多 VT100 转义序列并使用它们来擦除 more? 提示。 另一种替代方案是将所有行的副本写入离屏缓冲区，并在用户按下 Enter 键时清除屏幕然后替换屏幕内容。 这是一种比第一种更容易的解决方案，但它并不是真正的 more 命令的行为方式。

## 1.11.6 more 程序的第三次尝试

我们的最终版本，并非正确版本，将解决上述一些问题。

第一个问题是我们如何确定终端窗口的实际大小。 这个问题有两个解决方案。 如果用户的环境包含环境变量 COLUMNS 和 LINES，那么程序可以使用它们的值来确定终端窗口中的列数和行数，如以下代码片段所示，该片段将 LINES 值存储在变量 num_lines 中。

```
int     num_lines;
char    *endptr;
char    *linestr = getenv("LINES");
if ( NULL != linestr ) {
    num_lines = strtol(linestr, &endptr, 0);
    if ( errno != 0 ) {
        /* handle error and exit */
    }
    if ( endptr == linestr ) {
        /* not a number so handle error and exit */
    }
}
```

代码不完整——应该用适当的代码填充错误处理部分。 我们稍后会讨论错误处理。 但如果 LINES 变量未放入用户的环境中，上述代码将无法工作，并且如果用户在程序启动后调整窗口大小，也将无法工作。

更好的解决方案是使用更高级的函数，该函数将在第 4 章中更深入地介绍，名为 ioctl()。 函数 ioctl() 是 I/O Control 的缩写。 它旨在对外围设备执行许多操作，而不仅仅是终端。 它的原型是

```
#include <sys/ioctl.h>
int ioctl(int d, int request, ...);
```

注意参数列表中的 "..."。 这是 C 表示可变数量参数的记号。 第一个参数是文件描述符。 文件描述符在第 2 章中介绍。 第二个参数，整数类型，是一个命令。 以下参数是命令的参数，并且取决于给定的命令。 获取当前终端窗口的行数和列数的 ioctl() 调用有三个参数：

```
ioctl(tty_file_descriptor, TIOCGWINSZ, &window_structure)
```

其中 tty_file_descriptor 是我们终端的文件描述符，TIOCGWINSZ 是一个表示“获取终端窗口大小结构”的命令，而 window_size_structure 是类型为 struct winsize 的变量。 winsize 结构定义在头文件中，当你在代码中包含 <sys/ioctl.h> 头文件时会自动包含该头文件。 将使用此 ioctl 的代码为

```
struct winsize window_arg;
int     num_rows, num_cols;

fp_tty = fopen("/dev/tty", "r");
if ( fp_tty == NULL )
    exit(1);
if (-1 == ioctl(fileno(fp_tty), TIOCGWINSZ, &window_arg))
    exit(1);
num_rows = window_arg.ws_row;
num_cols = window_arg.ws_col;
```

ioctl 中使用的 fileno() 函数在第 2 章中介绍；它将 FILE* 转换为文件描述符。 文件描述符也在第 2 章中解释。 我们将在 do_more_of() 和 get_user_input() 函数的最后一个版本中使用以下 get_tty_size() 函数：

```
void get_tty_size(FILE *tty_fp, int* numrows, int* numcols)
{
    struct winsize window_arg;
    if (-1 == ioctl(fileno(tty_fp), TIOCGWINSZ, &window_arg))
    exit(1);
    *numrows = window_arg.ws_row;
    *numcols = window_arg.ws_col;
}
```

尽管 ioctl() 函数是标准的，应该在任何 UNIX 系统上都可用，但它实现的具体命令可能不可用。 特别是，TIOCGWINSZ 命令可能不可用。 当你编写依赖于不保证存在的特性的代码时，最好通过用预处理器指令将其括起来以有条件地编译它。 上述函数最好使用以下方式编写

```
void get_tty_size(FILE *tty_fp, int* numrows, int* numcols)
{
#ifdef TIOCGWINSZ
    struct winsize window_arg;
    if (-1 == ioctl(fileno(tty_fp), TIOCGWINSZ, &window_arg))
    exit(1);
    *numrows = window_arg.ws_row;
    *numcols = window_arg.ws_col;
```

