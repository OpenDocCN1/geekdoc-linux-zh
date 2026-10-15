
`read()` 调用将阻塞（从而调用进程也会阻塞），直到它接收到第一个字节。`TIME` 指定一个字节间计时器，该计时器仅在接收到第一个字节后才被激活。换句话说，在用户键入之前，计时器处于非活动状态。每次接收到一个字节后，计时器都会重置为 0。一旦用户开始键入，如果在计时器过期之前接收到 `numbytes_to_read` 和 `MIN` 中较小者数量的字节，`read()` 将返回这些字节。请记住，计时器在每个字节后都会重置。如果在接收到 `MIN` 字节之前计时器过期，`read()` 将返回它已接收到的任何字节。（如果计时器过期，至少会返回一个字节，因为计时器要到接收到第一个字节后才开始。）如果在调用 `read()` 时已有数据可用，则相当于数据在 `read()` 之后立即接收。这意味着如果线路规程（在终端驱动程序内部）的输入队列中已有足够数据，`read()` 可以立即返回。

### 情况 2. `MIN > 0`, `TIME == 0`

`read()` 不会在接收到 `MIN` 字节之前返回。将 `TIME` 设置为零意味着计时器被关闭。实际上它被赋予无限的时间，这可能导致 `read()` 无限期阻塞，等待输入。`numbytes_to_read` 和 `MIN` 中较小者数量的字节将被返回给用户进程。这意味着如果 `numbytes_to_read < MIN`，则 `read()` 要等到接收到 `MIN` 字节才满足，但它只向调用者提供 `numbytes_to_read`。如果 `numbytes_toread > MIN`，则 `read()` 在接收到 `MIN` 字节时返回，并向调用者提供 `MIN` 字节。

### 情况 3：`MIN == 0`，`TIME > 0`

与情况 1 不同，`TIME` 指定一个在调用 `read()` 时启动的定时器。它不是字节间定时器。在这种情况下，当收到单个字节或定时器到期时，`read()` 返回。如果定时器到期，`read()` 返回 0，否则返回读取的字节数。如果在处理 `read()` 调用之前终端输入队列中已有字符，则会立即将队列中的字符数与 `numbytes_to_read` 字节之间的较小值传递给 `read()`，以满足该调用，并且 `read()` 将返回实际读取的字节数。

### 情况 4：`MIN == 0`，`TIME == 0`

请求的字节数（即 `numbytes_to_read`）与当前可用字节数中的较小值将返回给调用者，而无需等待更多字节输入。如果没有可用字符，`read()` 返回 0，表示未读取任何数据。否则返回实际读取的字节数。在这两种情况下，`read()` 都会立即返回。

为了演示，首先，在非规范模式下，我们将设置 `min = 0` 和 `time = 30`。你会看到，如果在 3 秒（30 个十分之一秒）内输入一个字符，它会立即被传递，但如果在 3 秒内没有输入字符，`read()` 将返回一个 `EOF` 字符。每隔 3 秒输入一些字符，然后让 3 秒过去。你会看到程序终止。

```
$ stty -icanon min 0 time 30 ; transpose
```

你可能还会发现你的 shell 终止了。在执行此操作之前，请确保你设置了 `IGNOREEOF` 环境变量，以免丢失 shell。如果你看到重复出现的“Use exit to logout”形式的提示，请使用 `reset` 关闭终端设置。

接下来，测试将 `min` 和 `time` 设置为非零值的效果。输入以下命令序列：

```
$ stty -icanon min 4 time 30 ; transpose
```

等待至少 3 秒，注意什么都不会发生。程序正在等待输入。没有超时，`read()` 尚未返回。现在输入一个字符并等待几秒。你将在 3 秒后看到它的转置输出，这证明 `read()` 在延迟了 30 个时间单位后仅返回了 1 个字符。现在输入 4 个字符，看看程序打印它们的转置输出有多快。驱动程序会等待 3 秒以输入最小数量的字符；如果在 3 秒内输入完成，它将返回，否则它会在 3 秒后返回，并返回已输入的字符数。使用 Ctrl-C 终止进程并重新开启规范模式。

这些实验证明，在关闭规范模式的情况下，你可以精确地控制输入。到目前为止，我们一直使用 `stty` 命令来控制终端驱动程序。在程序中，你可以改用 `tcgetattr()` 和 `tcsetattr()`。以下是一个程序清单，它允许你在非规范模式下为 `MIN` 和 `TIME` 参数指定特定值，从而测试各种终端设置组合的效果。

```
Listing canon_mode_test.c
#include <stdio.h>
#include <stdlib.h>
#include <termios.h>
#include <fcntl.h>
#include <string.h>
#include <unistd.h>

#define SLEEP_TIME 2

/**
 * Gets input under the mode specified by the values of iscanon, vmin, and
 * vtime. See the notes or the termios man page for the meaning of the vmin
 * and vtime parameters.
 */
void get_response( int iscanon, int vmin, int vtime);

/* Sets the VMIN value to vmin, VTIME to vtime, turns off icanon */
void set_non_canonical(int vmin, int vtime);

/* if how == 0 this saves the termios state for later restoring   */
/* if how == 1 this restores the termios state from the saved state */
/* CANNOT CALL with how == 1 before first calling with how == 0   */
void tty_mode(int how);

int main(int argc, char* argv[])
{
    int bNoCanon = 1;  /* default is non-canonical mode */
    int vmin     = 1;  /* default is one char */
    int vtime    = 0;  /* default is to force reads to wait for vmin chars */
    int ch;
    char optstring[] = ":hcm:t:";

    while (1) {
        ch = getopt(argc, argv, optstring);
        if ( -1 == ch )
            break;
        switch (ch) {
        case 'h':
            printf("Usage: %s [-hbc] [ -m MIN ] [ -t TIME ]\n",argv[0]);
            printf("  -h : help\n");
            printf("  -c : turn on canonical mode\n");
            printf("  -m : set VMIN value \n");
            printf("  -t : set VTIME value \n");
            exit(0);
        case 'c':
            bNoCanon = 0;  /* meaning canonical mode is ON */
            break;
        case 'm':
            vmin = strtol(optarg, NULL, 0);
            break;
        case 't':
            vtime = strtol(optarg, NULL, 0);
            break;
```

case '?' :

    break;

case ';' :

    break;

default:

    fprintf(stderr, " ");

}

/* Report on state that we will put terminal in */

if ( bNoCanon )

    printf("Canonical mode off\n");

else

    printf("Canonical mode on\n");

printf("VMIN set to %d\n",vmin);

printf("VTIME set to %d\n",vtime);

/* save current terminal state */

tty_mode(0);
```
