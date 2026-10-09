
```c
    *ptr++ = 0; /* 使用完毕后将其清零 */

    exit(0);

}
```

图 18.18 调用 `getpass` 函数

# 第 18.11

当调用 `getpass` 的程序处理明文密码后，为了安全起见，程序应该在内存中将其清除。如果程序生成了其他人可能读取的核心文件，或者某些其他进程以某种方式读取了我们的内存，它们可能会读取到明文密码。我们所说的“明文”是指我们在 `getpass` 提示时输入的密码。UNIX 系统会修改此明文密码，将其转换为“加密”密码。例如，密码文件（第 6.2 节）中的 `pw_passed` 字段包含的是加密后的密码，而不是明文密码。

## 18.11 非规范模式

非规范模式通过关闭 `termios` 结构中 `c_lflag` 字段的 `ICANON` 标志指定。在非规范模式下，输入数据不会被组造成行。以下特殊字符（第 18.3 节）不会被处理：`ERASE`, `KILL`, `EOF`, `EOL`, `EOL2`, `CR`, `REPRINT`, `STATUS` 和 `WERASE`。

正如我们所说，理解非规范模式很容易：系统一次返回最多一行。但如果它一次返回一个字节，读取开销将过大。（回想图 3.6，它显示了一次读取一个字节的开销。每当我们返回的数据量翻倍时，系统开销就会减半。）系统无法一次返回多个字节，因为在开始读取之前，我们不知道需要读取多少数据。

解决方案是告诉系统，在读取了指定数量的数据或在过了给定的时间后返回。这种技术使用了 `termios` 结构中 `c_cc` 数组的两个变量：`MIN` 和 `TIME`。数组中的这两个元素通过名称 `MIN` 和 `VIME` 来标识。

`MIN` 指定了读取等待之前的最小字节数。`TIME` 指定了等待数据到达的时间（以十分为单位）。共有四种情况：

### 情况 A：MIN > 0, TIME > 0

`TIME` 指定了一个字节间定时器，该器仅在接收到第一个字节时启动。如果在定时器过期之前接收了 `MIN` 个字节，则读取 `MIN` 个字节。如果在接收到 `MIN` 个字节之前定时器过期，则读取所有接收到的字节。（如果定时器过期，至少会返回一个字节，因为定时器在接收到第一个字节之前不会启动。）在这种情况下，调用者会一直调用直到接收到第一个字节。如果在调用 `read` 时数据已经可用，则就像数据在读取后立即接收到一样。

### 情况 B：MIN > 0, TIME = 0

在接收到 `MIN` 个字节之前读取不会返回。这可能导致读取无限阻塞。

## 终端 I/O

### 情况 C：MIN == 0, TIME > 0

`TIME` 指定了一个读取定时器，该定时器在调用 `read` 时启动。（对比情况 A，在 A 中，非零的 `TIME` 代表字节间定时器，在接收到第一个字节之前不会启动。）当接收到单个字节或定时器过期时，读取返回。如果定时器过期，`read` 返回 0。

### 情况 D：MIN == 0, TIME == 0

如果有可用数据，`read` 返回最多请求数量的字节数。如果没有可用数据，`read` 立即返回 0。

意识到在所有这些情况情况下，`MIN` 只是一个最小值。如果程序请求了超过 `MIN` 字节的数据，可能会接收到请求的全部数量。这也适用于 `MIN` 为 0 的情况 C 和 D。

图 18.19 总结了非规范输入的四种情况。在图中，`nbytes` 是 `read` 的第三个参数（返回的最大字节数）。

| TIME > 0 | MIN > 0 | MIN == 0 |
| :--- | :--- | :--- |
| | A: 在定时器过期前返回 [MIN, nbytes]；如果定时器过期则读取 [1, MIN]。 | C: 在定时器过期前返回 [MIN, nbytes]；如果定时器过期则读取 0。 |
| | (TIME = 字节间定时器。调用者无限等待。） | (TIME = 读取定时器。) |
| TIME == 0 | B: 可用时返回 [MIN, nbytes]。（调用者无限等待。） | D: 立即返回 [0, nbytes]。 |

图 18.19 非规范输入的四种情况

-- 非规范输入的四种情况

请注意，POSIX.1 采用的 `VMIN` 和 `VTIME` 值与 `VEOF` 和 `VEOL` 相同。事实上，Solaris 这样做是为了兼容旧版本的 System V。然而，这产生了移植性问题。在进入非规范模式时，我们必须恢复 `VEOF` 和 `VEOL` 的值。如果 `VMIN` 等于 `VEOF` 且我们不恢复这些值，当我们把 `MIN` 设置为典型值 1 时，文件结束驱动 Control-A 会触发。解决此问题简单的方法是在进入非规范模式时保存整个 `termios` 结构，并在返回规范模式时恢复。

### 示例

图 18.20 中的程序定义了 `tty_break` 和 `tty_raw` 函数，将终端设置为中断模式（break mode）和原始模式（raw mode）（break 和 raw 术语源于 Version 7 驱动）。我们可以通过调用 `tty_reset` 函数将终端重置为原始状态（调用这两个任一函数之前的状态）。

如果我们调用了 `tty_break`，则需要在调用 `tty_raw` 之前调用 `tty_reset`。在调用 `tty_raw` 后调用 `tty_break` 也是如此。这增加了在遇到任何错误时终端处于可用状态的概率。

额外提供了两个函数：`tty_break` 和 `tty_raw`，将终端设置为中断模式和原始模式。（break 和 raw 术语源于 Version 7 驱动）。我们可以通过调用 `tty_reset` 函数将终端重置为原始状态（调用这两个任一函数之前的状态）。

如果我们调用了 `tty_break`，则需要在调用 `tty_raw` 之前调用 `tty_reset`。在调用 `tty_raw` 后调用 `tty_break` 也是如此。这增加了在遇到任何错误时终端处于可用状态的概率。

```c
void
tty_atexit(void)      /* can be set up by atexit(tty_atexit) */
{
    if (ttysavefd >= 0)
        tty_reset(ttysavefd);
}

struct termios *
tty_termios(void)      /* let caller see original tty state */
{
    return(&save_termios);
}
```

图 18.20 将终端模式设置为 cbreak 或 raw

我们对 cbreak 模式的定义如下：

- 非规范模式。正如我们在本节开头提到的，这种模式关闭了某些输入字符处理。它没有关闭信号处理，因此用户可以使用触发终端生成信号的任何字符。请注意，调用者可以捕获这些信号；否则，信号可能会终止程序，导致终端仍留留在 cbreak 模式。（注：此处原文为 "the terminal will be left in cbreak mode"）

作为一个一般规则，每当我们编写一个改变终端模式的程序时，都应该捕获所有信号。这允许我们在终止之前重置终端模式。

- 关闭回显（Echo off）。

- 逐字节输入。为了实现这一点，将 `MIN` 设置为 1，`TIME` 设置为 0。这是图 18.19 中的情况 B。在至少有一个字节可用之前，`read` 将不会返回。

我们将 raw 模式定义如下：

- 非规范模式。我们还关闭了对产生信号的字符的处理（`ISIG`）以及扩展输入字符的处理（`IEXTEN`）。此外，我们通过关闭 `BRKINT` 来禁用 BREAK 字符产生信号。

- 关闭回显（Echo off）。

- 我们禁用了输入时的 CR 到 NL 映射（`ICRNL`）、奇偶校验检测（`INPCK`）、输入时对第八位的剥离（`ISTRIP`）以及输出流控制（`IXON`）。

- 八字节字符（`CS8`），并禁用奇偶校验（`PARENB`）。

- 禁用所有输出处理（`OPOST`）。

- 逐字节输入（`MIN` = 1, `TIME` = 0）。

图 18.21 中的程序列出了 raw 和 cbreak 模式。

```c
#include "apue.h"

static void
sig_catch(int signo)
{
    printf("signal caught\n");
    tty_reset(STDIN_FILENO);
    exit(0);
}

int
main(void)
{
    int i;
    char c;

    if (signal(SIGINT, sig_catch) == SIG_ERR) /* catch signals */
        err_sys("signal(SIGINT) error");

    if (signal(SIGQUIT, sig_catch) == SIG_ERR)
        err_sys("signal(SIGQUIT) error");

    if (signal(SIGTERM, sig_catch) == SIG_ERR)
        err_sys("signal(SIGTERM) error");

    if (tty_raw(STDIN_FILENO) < 0)
        err_sys("tty_raw error");

    while ((i = read(STDIN_FILENO, &c, 1)) == 1) {
        if ((c & 255) == 0177) /* ASCII DELETE */
            break;
        printf("%%o\n", c);
    }

    if (tty_reset(STDIN_FILENO) < 0)
        err_sys("tty_reset error");

    if (i <= 0)
        err_sys("read error");

    if (tty_break(STDIN_FILENO) < 0)
        err_sys("tty_break error");

    printf("\nenter break mode characters, terminate with SIGINT\n");

    while ((i = read(STDIN_FILENO, &c, 1)) == 1) {
        c = 255;
        printf("%%o\n", c);
    }

    if (tty_reset(STDIN_FILENO) < 0)
        err_sys("tty_reset error");

    if (i <= 0)
        err_sys("read error");

    exit(0);
}
```

18.21 测试 raw 和 break 终端模式

运行图 18.21 中的程序，我们可以看到这两个终端模式下发生了什么：

```
$ ./a.out
Enter raw mode characters, terminate with DELETE
4
33
133
61
70
176
type DELETE
Enter cbreak mode characters, terminate with SIGINT
1
type Control-A
10
type backspace
signal caught type interrupt key
```

在 raw 模式下，输入的字符是 Control-D (04) 和特殊功能键 F7。在所使用的终端上，此功能产生了五个字符：ESC (033), (0133), 1 (061), 8 (070) 和 ~ (0176)。注意，由于每个字符后关闭了输出处理，cbreak 模式下并没有禁用特殊字符处理（例如，Control-D 作为文件结束符和退格不会被特殊处理），但终端生成的信号仍然会被处理。

## 18.12 终端窗口大小

大多数 UNIX 系统提供了一种方法来跟踪当前终端窗口的大小，并在大小变化时通知内核前台进程组。内核为每个终端和伪终端维护一个 `winsize` 结构。

```c
struct winsize {
    unsigned short row;      /* 行 */
    unsigned short col;       /* 列 */
    unsigned short wcol;     /* 宽 */
    unsigned short wrow;     /* 宽 */
};
```

`winsize` 的规则如下：

- 我们使用 `TIOCGWZ` 获取当前值。
- 我们使用 `TIOCWIN` 存储新值。

每当大小变化时，都会向前台组发送 `SIGWINCH`。

### 示例

运行 18.22 中的程序向我们展示

```
$ ./a.out
35 rows, 80 columns
SIGWINCH received: initial size
40 rows, 123 columns
SIGWINCH received: again
42 rows, 33 columns
type interrupt key to terminate
```
