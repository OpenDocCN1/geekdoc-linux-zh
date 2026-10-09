
## 附录 C

### 第 14 章解答

来定义 `fd_set` 类型以容纳 2048 个描述符。遗憾的是，事情不再那么简单了。在现代系统中使用这种技术，我们需要做几件事：

1. 在包含头文件之前，我们需要定义任何阻止我们包含 `<sys/select.h>` 的符号。某些系统可能使用单独符号保护 `fd_set` 类型的定义。我们也需要定义这个。
   例如，对于 FreeBSD 8.0，我们需要定义 `_SYS_SELECT_H_` 以防止包含 `<sys/select.h>`，并定义 `_FD_SET` 以防止包含 `fd_set` 数据类型的定义。
2. 有时，为了兼容旧版应用程序，`<sys/types>` 定义了 `fd_set` 的大小，因此我们需要包含它，然后取消定义 `FD_SET`。
3. 我们需要重新定义 `FD_SETSIZE`，设置为我们使用的描述符数量。
4. 我们需要取消定义第 1 步中定义的符号。
5. 最后，包含 `<sys/select.h>`。

在运行程序之前，我们需要配置 `FD_SET` 以允许尽可能多的描述符。

14.4 下表列出了具有类似功能的函数。

| FD_ | 成员 |
|---|---|
| `FD_ZERO` | add |
| `FD_CLR` | del |
| `FD_ISSET` | is |

这些 `xxx` 函数对应于 `fill`。对于 `set`，第一个参数是数量。

14.5 C.16 显示了实现：

```c
#include "apue.h"

#include <sys/select.h>

void

sleep_us(unsigned n) {

    struct timeval tval;

    tval.tv_sec = n / 1000000;

    tval.tv_usec = n % 1000000;

    select(0, NULL, NULL, NULL, &tval);

}
```

使用 `poll`

```c
#include <poll.h>

sleep_us(int n) {

    struct pollfd dummy;

    int timeout;

    if ((timeout = n / 1000) <= 0) {

        timeout = 1;

    }

    poll(&dummy, 0, timeout);

}
```

使用 `select`

```c
#include <apue.h>

#include <fcntl.h>

int main(void) {

    int i, n;

    int fd[2];

    if (pipe(fd) < 0) {

        err_sys("pipe");

    }

    fcntl(fd[1], O_NONBLOCK);

    /* 直到管道写满 1 字节 */

    for (n = 0; ++n++) {

        if ((i = write(fd[1], "a", 1)) != 1) {

            printf("write %d\n", i);

            break;

        }

    }

    printf("pipe capacity = %d\n", n);

    exit(0);

}
```

非阻塞写入

C.17 显示了实现

下表显示了我们的平台计算的值。

| 平台 | 管道容量（字节） |
|---|---|
| FreeBSD 8.0 | 65,536 |
| Linux 3.2 | 65,536 |
| Mac OS X 10.6.8 | 16,384 |
| Solaris 10 | 16,384 |

这些值可能与 `PIPE_BUF` 值不同，因为 `PIPE_BUF` 被定义为可以原子地写入管道的数据量。在这里，我们计算不受任何原子性限制的数据量。

14.10 程序 14.27 更新访问时间取决于操作系统和文件系统。在所有四个平台上，当文件位于默认文件系统中，访问时间都会更新。

### 第 15 章

1. 15.1 如果管道从未关闭，读取者永远看不到文件结束。分页程序将永久读取输入。

2. 15.2 父进程在写入最后一行后终止。读取端在父进程终止时会自动关闭。但父进程可能领先子进程一个缓冲区，因为子进程（程序）正在等待我们查看输出。如果我们运行一个启用了交互式命令行编辑的 shell（如 Korn），shell 在我们的父进程终止时可能会更改终端模式。这无疑会干扰分页程序，分页程序也修改了终端模式。（大多数分页程序在等待下一页时会将终端设置为非规范模式）

3. 15.3 `popen` 函数返回文件指针，因为执行了 shell。但 shell 无法执行不存在的命令，因此它在标准错误上打印

```
sh: line 1: ../aout: No such file or directory
```

并以退出状态 127 终止。`pclose` 返回由 `waitpid` 返回的命令终止状态。

4. 15.4 当父进程终止时，使用 shell 查看其终止状态。对于 Bourne shell、Bourne-again shell 和 Korn shell，命令是 `echo $?`。打印的数字是 128 加上信号号。

5. 15.5 首先添加声明

```c
FILE *fpin, *fpout;
```

### 选练习解答

然后使用 `fdopen` 将管道描述符与标准 I/O 流关联，并在 `while` 循环从标准输入读取之前，将流设置为缓冲模式：

`while` 循环中的 `write` 和 `read` 被替换为

```c
if (fputs(line, fpout) == EOF)

    err_sys("fputs error to pipe");

if (fgets(line, MAXLINE, fpin) == NULL) {

    err_msg("child closed pipe");

    break;

}
```

- **15.6** 系统函数调用了 `wait`，第一个终止的子进程是由 `popen` 生成的子进程。由于它不是系统创建的子进程，它会再次等待并阻塞直到 `sleep` 完成。然后系统返回。当 `poll` 调用 `wait` 时，会返回错误，因为没有更多的子进程需要等待。因此随后返回一个错误。

- **15.7** 尽管细节随平台而异（见图 C.19），`select` 表明描述符是可读的。在读取所有数据后，`read` 返回 0 表示文件结束。但 `poll`，返回的是 `POLLUP` 事件，这可能在仍有数据可读时发生。然而，一旦我们获取了所有数据，`read` 返回 0 表示文件结束。在读取完所有数据后，返回了 `POLLIN` 事件，尽管我们发送了 `read` 来接收文件结束的通知（返回值为 0）。

| 操作 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|
| 写端关闭的管道读端执行 `select` | R/E | R | R/W | R/E |
| 写端关闭的管道读端执行 `poll` | R/HUP | HUP | INV | HUP |
| 读端关闭的管道写端执行 `select` | R/E | R | R/W | INV |
| 读端关闭的管道写端执行 `poll` | R/HUP | W/ERR | INV | HUP |

图 C.19 使用 `select` 和 `poll` 的管道行为

图 C.19 显示的条件包括 R（可读）、W（可写）、E（异常）、HUP（挂断）、ERR（错误）和 INV（无效文件描述符）。当输出描述符指向一个被读者关闭的管道时，`select` 表明描述符是可写的。当我们调用 `write` 时，会产生 `SIGPIPE` 信号。如果我们忽略此信号或从信号处理程序返回，`write` 将失败且 `errno` 设置为 EPIPE。但然而，对于 `poll`，行为随平台而异。

## 附录 C

### 第 15 章解答

15.8 子进程写入标准错误的任何内容都会出现在父进程标准错误出现的地方。要将标准错误传回父进程，请在 `cmdstring` 中包含 shell 重定向 `2>&1`。

15.9 `popen` 函数创建一个子进程，并由子进程执行 shell。shell 反而调用 `fork`，shell 的子进程执行命令字符串。当字符串结束时，shell 正在等待此处。然后 shell 退出，这正是 `pclose` 中的 `waitpid` 所等待的。

15.10 技巧是打开两次 FIFO：一次用于读取，一次用于写入。我们从不使用用于写入的描述符，但保持该描述符打开可以防止当客户端数量从 1 变为 0 时产生文件结束。打开两次 FIFO 需要一些小心，因为需要是非阻塞打开。我们必须先进行一个非阻塞的只读打开，然后进行一个阻塞的只写打开。（如果尝试先进行非阻塞写打开，它会返回错误。）然后我们关闭读取描述符的非阻塞状态。图 C.20 显示了此代码。

```c
#include "apue.h"

#include <fcntl.h>

#define FIFO "temp.fifo"

int fd_read = open(FIFO, O_RDONLY | O_NONBLOCK);

int fd_write = open(FIFO, O_WRONLY);

fcntl(fd_read, F_SETFL, 0);
```
