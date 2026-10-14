
- 5. 调用进程可以执行其他任务。当 I/O 变得可用时，内核为进程生成一个信号并调用第 1 步中建立的信号处理程序。
- 6. 信号驱动的 I/O 提供边缘触发通知（第 63.1.1 节）。进程可能被通知 I/O 可用，它应该尽可能地执行 I/O（例如，读取尽可能字节）。假设是非阻塞文件描述符，这意味着执行一个循环来执行 I/O 系统调用，直到某个调用因错误 `EAGAIN` 或 `EWOULDBLOCK` 失败为止。

在 Linux 2.4 及更早版本中，信号驱动的 I/O 可以用于套接字、终端、伪终端和其他类型设备的文件描述符。Linux 2.6 额外允许对管道和 FIFO 使用信号驱动的 I/O。在 Linux 2.6.25 中，信号驱动的 I/O 也可以用于 `notify` 文件描述符。

在接下来的页面中，我们将展示一个使用信号驱动 I/O 的示例，然后对上述某些步骤进行更详细的解释。

> 在历史上，信号驱动的 I/O 有时被称为*异步 I/O*，这反映在相关打开文件的标志（`O_ASYNC`）中。然而，*异步 I/O* 术语是指 POSIX I/O 规范提供的功能类型。当进程请求内核执行 I/O 操作时，如果内核*启动*了进程，它会立即将控制权交回调用进程；当 I/O 操作完成或发生错误时，进程会被通知。

`O_ASYNC` 在 POSIX.1 中规定，但未包含在 SLSv3 中，因为对该标志所需行为的规范被认为不足。若干 UNIX 实现（即使是较旧的）没有定义与 `fcntl` 使用的常量。相反，该常量命名为 `FASYNC`，而 `glibc` 将后者定义为 `O_ASYNC` 的同义词。

## 示例程序

列表 63-3 提供了一个使用信号驱动 I/O 的简单示例。该程序执行了上述步骤以在标准输入上启用信号驱动的 I/O，并将终端设置为 cbreak 模式（第 62.6.3 节），以便输入可以一次一个字符地可用。程序进入一个无限循环，在等待输入可用的同时执行增加变量 `cnt` 的“工作”。每当输入可用时，`SIGIO` 处理程序会设置标志 `gotSigio`，该标志由主程序监控。当程序看到此标志的数字 `gatSigio` 时，它读取可用的输入字符并将它们连同 `cnt` 的当前值一起打印。如果在输入中读取到哈希字符 `#`，程序终止。

以下是我们运行此程序并输入哈希字符 `#` x 次时所看到的示例：

```
$ .demo_sigio

cnt=37; read x

cnt=100; read x

cnt=159; read x

cnt=223; read x

cnt=288; read x

cnt=333; read #
```

### 列表 63-3: 在终端 altio/demo_sigio.c 上使用信号驱动的 I/O

```c
#include <signal.h>
#include <ctype.h>
#include <fcntl.h>
#include <termios.h>
#include <tty_functions.h>      /* ttySetC() 的声明 */
#include <tlpi_hdr.h>
```

```c
static volatile sig_atomic_t gotSigio = 0;
/* 接收 SIGIO 时设置为非零 */
```

```c
static void
sigioHandler(int sig)
{
    gotSigio = 1;
}
int
main(int argc, char *argv[])
{
    int flags, j, cnt;
    struct termios origTmios;
    char ch;
    struct sigaction sa;
    Boolean done;
```

```c
/* 为“I/O 可用”信号建立处理程序 */
sigemptyset(&sa.sa_mask);
sa.sa_flags = SA_RESTART;
sa.sa_handler = sigioHandler;
if (sigaction(SIGIO, &sa, NULL) == -1)
    exit("sigaction");
/* 设置所有者 */
if (fcntl(fd, F_SETOWN, getpid()) == -1)
    exit("fcntl");
/* 启用非阻塞 I/O */
flags = fcntl(fd, F_GETFL); /* 获取当前标志 */
if (fcntl(fd, F_SETFL, flags | O_ASYNC | O_NONBLOCK) == -1)
    exit("fcntl");
/* 将终端设置为 cbreak 模式 */
if (tcsetattr(STDIN_FILENO, TCSANOW, &origTmios) == -1)
    exit("tcsetattr");
while (1) {
    if (gotSigio) {
        while (read(STDIN_FILENO, &ch, 1) > 0) {
            if (ch == '#')
                goto done;
            cnt++;
            printf("cnt=%d; read x\n", cnt);
        }
        gotSigio = 0;
    }
}
done:
/* 恢复终端设置 */
if (tcsetattr(STDIN_FILENO, TCSAUSH, &origTmios) == -1)
    exit("tcsetattr");
exit(EXIT_SUCCESS);
```

## 在启用信号驱动 I/O 之前建立处理程序

由于 `SIGIO` 的默认动作是终止进程，我们应该在启用信号驱动 I/O 之前启用处理程序。

## 设置文件描述符所有者

通过使用以下 `fcntl()` 操作设置文件描述符的所有者：

```c
fcntl(fd, F_SETOWN, pid);
```

我们可以指定单个进程或整个进程组在 I/O 可用时接收信号。如果 `pid` 为正，则它被解释为进程 ID。如果 `pid` 为负，其绝对值指定进程组。

在较旧的 UNIX 实现中，使用 `ioctl()` 操作——`FSETOWN` 或 `SIOCSIGGRP`——来实现与 `F_SETOWN` 相同的功能。

`fcntl()` `F_GETOWN` 操作返回当文件描述符上可以进行 I/O 时接收信号的进程或进程组 ID：

```c
id = fcntl(fd, F_GETOWN);
if (id == -1)
    exit("fcntl");
```
