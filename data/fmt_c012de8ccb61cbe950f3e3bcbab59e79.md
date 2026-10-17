
```c
    kill(pid2, SIGINT);

    printf("killing 3...\n");

    kill(pid3, SIGINT);

    exit(0);

}
```

书中的所有系统中，行为都是相同的：额外的读者会饿饿写入者。运行程序会得到：

```
child 1: obtained lock on file

child 2: obtained lock on file

child 3: cannot set lock: Resource temporarily unavailable

child 3: to block in write-lock...

parent: obtained read lock while write lock is pending

killing 1...

child 1: exit after pause

killing 2...

child 2: exit after pause

killing 3...

child 3: cannot write file: Interrupted system call
```

## 14.2 大多数系统将 `fd_set` 类型定义为包含整数数组的结构。数组中的每个位对应一个描述符。`FD` 宏封装了该数组，用于开启或关闭特定的位。定义为包含数组的结构而不是简单的数组的原因是为了允许使用赋值语句 `fd_set`。

## 14.3 大多数系统允许你在包含 `<sys/select.h>` 之前定义 `FD_SETSIZE`。例如，我们可以写：

```c
#define FD_SETSIZE 2048

#include <sys/select.h>
```

来定义 `fd_set` 类型以容纳 2048 个描述符。这在 FreeBSD 5.2.1、Mac OS 10.3 和 Solaris 9 上均有效。

## 14.4 下表列出了具有相似功能的函数。

- `FD_ZERO`
- `FD_SET`
- `FD_CLR`
- `FD_ISSET`

没有对应 `memset` 的 `FD_xxx` 函数。对于信号，集合的指针总是第一个参数，数字是第二个参数。对于描述符集，描述符是第一个参数，集合的指针是下一个参数。

## 14.5 `getmsg()` 返回多达五类型的信息：数据本身、数据的长度、控制信息、控制信息的长度以及标志。

## 14.6 图 C.15 显示了使用 `select` 的实现。

### 图 C.15. 使用 `select` 实现 `sleep_us`

```c
#include "apue.h"

#include <sys/select.h>

void

sleep_us(unsigned int nusecs)

{

    struct timeval tval;

    tval.tv_sec = nusecs / 1000000;

    tval.tv_usec = nusecs % 1000000;

    select(0, NULL, NULL, NULL, &tval);

}
```

图 C.16 显示了使用 `poll` 的实现。

### 示例 C.16. 使用 `poll` 实现 `sleep_us`

```c
#include <poll.h>

void

sleep_us(unsigned int nusecs)

{

    struct pollfd dummy;

    int timeout;

    if ((timeout = nusecs / 1000) <= 0)

        timeout = 1;

    poll(&dummy, 0, timeout);

}
```

BSD `sleep(3)` 管理页状态，`usleep` 设置定时并在每次调用时执行系统调用。它与调用进程的其他定时器正确交互，并且如果捕获了信号则不会被中断。

## 14.7 不 我们希望 `TELL_WAIT` 创建一个临时文件，并使用 1 个字节父进程锁，1 个字节子进程锁。`WAIT_CHILD` 让父进程等待获取子字节的锁，而 `TELL_PARENT` 让子进程释放子字节的锁。然而，问题是调用 `fork` 会释放子进程中所有的锁，因此子进程无法拥有任何自己的锁。

## 14.8 解决方案如图 C.17 所示。

### 图 C.17. 使用非阻塞写入计算管道容量

```c
#include "apue.h"

#include <fcntl.h>

int

main(void)

{

    int i, n;

    int fd[2];

    if (pipe(fd) < 0)

        err_sys("pipe error");

    set_fl(fd[1], O_NONBLOCK);

    /*

    每次写入 1 字节直到管道填满。

    */

    for (n = 0; ; n++) {

        if ((i = write(fd[1], "a", 1)) != 1) {

            printf("write ret %d.\n", i);

            break;

        }

    }

    printf("pipe capacity = %d\n", n);

    exit(0);

}
```

| 平台 | 管道容量 (字节) |
|---|---|
| FreeBSD 5.2.1 | 16384 |
| Linux 2.4.22 | 4096 |
| Mac OS X 10.3 | 8192 |
| Solaris 9 | 9216 |

下表显示了在我们平台上计算的值。

这些值与相应的 `PIPE_BUF` 值不同，因为 `PIPE_BUF` 定义为可以原子地写入管道的最大数据量。在这里，我们计算的是管道不考虑任何原子性限制的数据量。

## 14.10 图 14.32 程序是否更新输入文件的最后访问时间取决于操作系统以及该文件所在的文件系统类型。

# 第 15 章

15.1 如果管道的末端从不关闭，读取器永远看不到文件结束标志（EOF）。分页程序将永久阻塞在从标准输入读取的状态。

15.2 父进程在将行写入管道后立即终止。当父进程终止时，管道的读端会自动关闭。父进程的运行可能比子进程快一个缓冲区，因为子进程（分页器）正在等待我们查看输出。如果我们正在运行启用了交互式命令行编辑的 shell（例如 Korn shell），当我们的父进程终止且 shell 打印提示符时，shell 可能会更改终端模式。这无疑会干扰分页器程序，而分页器程序（大多数程序在等待输入以处理到下一页时，会将终端设置为非规范模式。）

15.3 `open` 函数返回一个文件指针，因为 shell 已经执行了。shell 无法执行不存在的命令，因此它打印

```
sh: line 1: ../ No such file or directory
```

标准错误并以退出状态 127 终止。`pclose` 在返回 `wait` 的同时返回命令的终止状态。

15.4 当父进程终止时，通过 shell 查看其终止状态。对于 Bourne shell、Bourne-again shell 和 Korn shell，使用命令 `echo $?`。打印的数字是 128 加上号。

15.5 首先添加声明

然后使用 `dup` 将管道描述符与标准 I/O 流关联，并将集合设置为行缓冲。执行此从标准输入读取的循环：

`write` 和 `read` 的 `while` 循环被替换为

```c
if (puts(line, pout) == EOF);
```

```c
err_sys("puts error to pipe");

if (fgets(line, MAXLINE, fpin) == NULL) {

    err_msg("child closed pipe");

    break;

}
```

15.6 系统函数调用 `wait`，第一个终止的子进程是 `popen` 生成的子进程。由于它不是系统创建的子进程，它会再次调用 `wait` 并阻塞直到 `sleep` 完成。然后 `system` 返回。当它 `close wait` 时，会返回一个错误，因为仍有数据需要等待。然后 `close` 返回一个错误。

15.7 `select` 函数指示描述符是可读的。当所有数据读取完成后，它返回 0 表示文件结束。但使用 `poll`（假设是 STREAMS 管道），会返回 `POLLUP` 事件，且该事件在仍有数据可读时就会返回。一旦我们读取了所有数据，`read` 返回 0 表示文件结束。数据被读取后，仅有 `POLLIN` 事件是不够的，然后我们等待 `read` 接收文件结束通知（`read` 的返回）。

对于指向已被读取器关闭的管道的输出描述符，`select` 指示该描述符是可写的。当我们调用 `write` 时，会产生 `SIGPIPE` 信号。如果我们忽略此信号，`write` 将返回 `EPIPE` 错误。然而，使用 `poll` 时，如果管道是 STREAMS，`poll` 将返回描述符的 `POLLUP` 事件。

15.8 子进程在父进程标准错误出现的任何地方对标准错误进行任何写入。要将错误传回父进程，请在 `cmdstring` 中使用 shell 重定向 `2->1`。

15.9 `popen` 函数进行 `fork`，子进程执行 shell。shell 执行命令。当 `cmdstring` 终止时，shell 正在等待此事的发生。shell 退出，父进程等待它。

15.10 技巧是打开两次 FIFO：一次用于读取，一次用于写入。当我们使用为写入打开的描述符时，当客户端数量从 1 变为 0 时，保持该描述符打开状态可以防止生成文件结束。两次打开 FIFO 需要注意，因为要求是非阻塞的。我们必须先进行非阻塞的只读打开，然后进行阻塞的只写打开。（如果尝试先进行非阻塞的只写打开，它将返回错误）。然后我们关闭读取描述符的非阻塞。图 C.18 显示了此代码。

### 图 C.18. 不阻塞地打开用于读写的 FIFO

```c
#include "unistd.h"

#include <fcntl.h>

#define FIFO "temp.fifo"

int

main(void)

{

    int fdread, fdwrite;

    unlink(FIFO);

    if (mkfifo(FIFO, FILE_MODE) < 0)

        err_sys("mkfifo error");

    if ((fdread = open(FIFO, O_RDONLY | O_NONBLOCK)) < 0)

        err_sys("open error for reading");

    if ((fdwrite = open(FIFO, O_WRONLY)) < 0)

        err_sys("open error for writing");

    fcntl(fdread, F_SETFL, 0);

    exit(0);
}
```

# 15.11

从活动队列中随机读取消息会干扰客户端-服务器协议，因为客户端请求或服务器的响应都会丢失。要读取队列，进程只需要知道队列的标识符，并且队列允许全员可读访问即可。

# 15.13

我们从不在共享内存段中存储实际地址，因为服务器和所有客户端可能在不同的地址挂载该段。相反，当共享内存段中构建链表时，列表指针应该存储为相对于该段的偏移量。

# 15.14

图 C.19 显示了父进程和子进程之间的交替。

| 父进程设置为 | 子进程设置为 | 共享设置为 | 返回 |
| :--- | :--- | :--- | :--- |
| 0 | 0 | 0 | 父进程 |
| | 1 | 1 | 子进程 |
| 2 | 2 | 2 | 父进程 |
| | 3 | 3 | 子进程 |
| 4 | | 4 | 父进程 |

# 第 16 章

16.1 图 C.20 显示了字节序。

16.3 对于每个我们将监听的端点，我们需要找到正确的地址。16.4 当请求到达时，我们使用 `select` 并处理它。16.5 在主过程中，我们将使用 `signal` 安装处理程序。派生子进程服务后，父进程关闭新描述符并恢复。最后，我们需要一个 `SIGCHLD` 信号处理程序，如下：

```c
void

sigchld(int signo)

{
```

### 图 C.21. 启用和禁用异步 socket

16.6 为了启用异步 socket，我们需要使用 `F_SETOWN` `fcntl` 命令建立所有权，并使用 `FIOASYNC` `ioctl` 命令启用异步信号。禁用异步 socket，我们需要禁用信号。`fcntl` 和 `ioctl` 命令的原因是为了寻找可移植的方法。代码所示图 C.21。

```c
#include "apue.h"

#include <errno.h>

#include <fcntl.h>

#include <sys/socket.h>

#include <sys/ioctl.h>

#if defined(BSD) || defined(MACOS) || defined(SOLARIS)

#include <sys/filio.h>

#endif

int

setasync(int sockfd)

{

    int n;

    if (fcntl(sockfd, F_SETOWN, getpid()) < 0)

        return(-1);

    n = 1;

    if (ioctl(sockfd, FIOASYNC, &n))

        return(-1);

    return(0);

}

int

clarasync(int sockfd)

{

    int n;

    n = 0;

    if (ioctl(sockfd, FIOASYNC, &n))

        return(-1);

    return(0);

}
```

## 第 18 章

18.1 注意，必须使用换行符（line feed character）结束重置命令，而不是回车符（return），因为终端处于非规范模式。

18.2 为 128 个字符中的每一个构建一个表，并根据用户的规范设置高位（校验位）。它使用 8 位 I/O，并处理校验位的生成。

18.3 如果你恰好使用的是窗口终端，你不需要登录两次。你可以在两个独立的窗口之间进行此实验。在 Solaris 下，将标准输入重定向自运行 `vi` 的终端窗口并执行 `stty`。这显示 `vi` 将 `MIN` 设置为 1，将 `TIME` 设置为 1。调用 `read` 将等待至少有一个字符输入，但在输入该字符后，`read` 只会等待十分之一秒的额外字符就会返回。

## 第 19 章

19.1 `telnetd` 和 `login` 两个服务器都以超级用户权限运行；对它们的调用以及 `chmod` 操作均成功。

19.2 执行 `pty -n stty -a` 会防止从端设备的 `termios` 和 `winsize` 结构被初始化。

19.3 遗憾的是，`font` 的 `F_SETTL` 命令不允许更改读写状态。

19.4 有三个进程组：(1) 登录 shell，(2) `pty` 父进程和 (3) `cat` 进程。第一个进程组构成一个会话，以登录从端作为会话组。第二个会话只包含第一个进程。第一个进程（登录 shell）是一个后台进程，其他的是前台进程组。

19.5 首先，`cat` 在接收到来自行规程的文件结束符（EOF）时终止。PTY 从端终止，这导致 PTY 主设备终止。在这一轮中，向子进程发送了文件结束符，因此子进程在下次读取 PTY 主设备时终止。父进程向其发送 `SIGTERM`；最后，父进程在结束时退出(0)，因此子进程功能正常运行。

程序的输出输出见图 8.29

| 进程 | 状态 |
| :--- | :--- |
| `cat` | e = 270, chars = 274, stat = 0: |
| `pty` | e = 262, chars = 40, stat = 15: F X |
| `pty` | e = 288, chars = 188, stat = 0: |

19.6 这可以通过 `echo` 命令和 `date(1)` 命令在子 shell 中完成：

```sh
#!/bin/sh

echo "Script started on "$(date);

pty "$SHELL":/bin/sh";

echo "Script done on "$(date)" | tee script
```
