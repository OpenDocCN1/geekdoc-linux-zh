
`main()` 函数显示在列表 15.3 的第 19–45 行。信号处理器被建立为 `catch_sig()`（第 25 行），信号掩码（第 26-28 行）和动作标志（第 29 行）。`malloc(3)` 并不依赖于全局堆、全局状态。

信号的异步性质意味着你必须在信号处理器中仅调用重入函数。否则，像 `SIGINT` 这样的信号可能会在程序执行 `malloc(3)`、`sprintf(3)` 或你自己的代码时到达。这会产生你需要计划的完整性问题。当信号处理器执行时，内存堆处于不稳定状态。如果信号处理器调用 `malloc(3)`，很可能会导致数据损坏或程序故障：`malloc(3)` 无法处理这种事件，因为它不是为重入设计的。

重入代码的一个特点是它本身不在静态或全局区域中保存任何状态。相反，调用者通过参数列表提供所有数据项。

以下是 POSIX.1 标准重入函数。带有星号的项未列在 POSIX.1 标准中，但在 AT&T SVID 标准中被列为重入。在在信号处理器中使用它们之前，请查阅本地文档。

# 第 15 章 • 信号

| `exit` | `fork` | `read` | `tcdrain` |
| `abort*` | `fstat` | `rename` | `tcflow` |
| `access` | `getgegid` | `rmdir` | `tcflush` |
| `alarm` | `getuid` | `setsigid` | `tcgetattr` |
| `cfgetispeed` | `getgid` | `setsigpid` | `tcgetprgrp` |
| `cfgetispeed` | `getgroups` | `setsid` | `tcsendbreak` |
| `cfsetpeed` | `getprgrp` | `setuid` | `tcsetattr` |
| `cfsisetpeed` | `getpid` | `sigaction` | `tcsetprgrp` |
| `chdir` | `getppid` | `sigaddset` | `time` |
| `chmod` | `getuid` | `sigdelset` | `times` |
| `chown` | `kill` | `sigemptyset` | `umask` |
| `chroot*` | `link` | `sigismember` | `uname` |
| `close` | `longjmp` | `sigismember` | `unset` |
| `create` | `lseek` | `sigfillset` | `unlink` |
| `dup` | `mkdir` | `sigismember` | `ustat*` |
| `dup2` | `open` | `sigpending` | `unlink` |
| `execle` | `pathconf` | `sigprocmask` | `utime` |
| `execve` | `pause` | `sigsuspend` | `wait` |
| `exit*` | `wait` | `sleep` | `waitpid` |
| `stat` | `sys` | `sysconf` | `write` |

## 避免重入代码问题

可靠的信号接口允许你控制何时产生某些信号。当信号处理程序必须调用非重入函数时，这种机制可以被你所用。该方法通过以下步骤实现：

1. 使用 `sigprocmask(2)` 阻塞感兴趣的信号。
2. 在应用程序的某些点，使用 `sigpending(2)` 检查信号是否处于挂起状态。
3. 在安全点调用 `sigsuspend(2)` 以允许信号的产生。

通过在应用程序的受控位点调用 `sigsuspend(2)`，你消除了 `malloc(3)` 等函数在信号发生时正在执行这一事实。这一过程确保了调用非重入函数是安全的。

## 信号处理程序中 errno 的重入问题

从技术上讲，列出的许多函数并不是纯重入的。其中许多函数具有修改全局外部变量 `errno` 值的能力。因此，你必须在信号处理程序中小心保护 `errno`。

![](img/84b5d55e12f9f19712b0bb181eee905f_345_0.png)

| 警告 |
| :--- |
| 许多重入函数能够修改外部变量 `errno`。为了保持纯重入性，务必在信号处理程序中保存并恢复 `errno`。 |

列表 15.2 中找到信号捕获函数代码在此重复如下：

```c
void
handler(int signo) {
++count; /* 增加计数 */
write(1,"Got SIGINT\n",11); /* 写入消息 */
}
```

该函数不是纯重入的，因为 `errno` 值可能会被写入 `write(2)` 的信号所干扰。这可以通过插入保存和恢复语句来于修正：

```c
void
handler(int signo) {
int e = errno; /* 保存 errno */
++count; /* 增加计数 */
write(1,"Got SIGINT\n",11); /* 写入消息 */
errno = e; /* 恢复 errno */
}
```

保存和恢复 `errno` 可以防止应用程序在信号处理程序返回时看到已更改的 `errno` 值。这类问题可能极其难以调试，因为它们通常取决于时机。

## 应用 EINTR 错误代码

除了使用 `sigsuspend(2)` 技术外，信号可以在任何时候被信号处理程序捕获。这限制了可用函数的选择，仅限于那些重入函数。因此，当必须调用非重入函数时，必须使用不同的技术。

信号处理程序可以向全局标记变量发布一个结果，随后由应用程序对其进行轮询。使用这种技术，不会产生重入问题，因为事件是同步的（轮询的），而不是异步的。以下示例显示了信号处理程序向全局变量 `gotSIGINT` 发布一个真值结果：

```c
static int gotSIGINT = 0; /* 当 SIGINT 到达时为真 */
static void
catch_SIGINT(int signo) {
    gotSIGINT = 1; /* 发布标记 */
}
```

应用程序的这部分非常简单，不会产生重入问题。困难在于，当程序被阻塞等待系统调用完成时，它永远没有机会轮询 SIGINT 事件。下述语句说明了程序的另一部分，它将无限等待，直到标准输入上到达数据：

```c
int z;
char buf[256];
z = read(0,buf,sizeof(buf)); /* 获取终端输入 */
```

当我们在等待输入时，信号处理程序仍然可以通过给变量 `gotSIGINT` 赋值 1 来发布它。然而，应用程序无法跳出 `read(2)` 函数来测试事件。相反，应用程序将无限等待，直到所有数据到达或接收到文件结束。

为了避免这种困难，UNIX 的设计者提供了以下解决方案：当信号处理程序返回时，某些系统调用会返回 `EINTR` 错误。这允许程序检查信号是否发生：

```c
int z;
char buf[256];
z = read(0,buf,sizeof(buf));
if (z == -1 && errno == EINTR) {
    // 处理信号中断的情况
}
```

*(注：由于原文后半部分存在大量重复描述，已根据语意整合翻译并确保逻辑连贯。)*

## 总结

本章展示了信号处理函数及其的一些陷阱。下一章将向你展示如何编写代码来高效地处理许多打开的文件描述符的输入和输出。这是编写服务器程序的一项基本技能。

# 第 16 章

## 高效的 I/O 调度

许多应用程序被设计为与单个用户交互。对于这些程序，响应这一个用户的随心所欲是简单的事情。然而，当你设计服务器程序时，该服务器的每个用户都必须获得立即响应，就像只有一个用户一样。如果你的服务器在系统调用内部等待另一个用户的输入，这将变得是不可能的。因此，在与多个客户端执行 I/O 操作时，需要一种不同的设计策略。

在本章中，你将研究如何执行：

- 非阻塞 I/O
- 使用 `select(2)` 的 I/O
- 使用 `poll(2)` 的 I/O

## 非阻塞 I/O

进程在执行 I/O 时，由于以下一个或多个原因的原因会被进入睡眠状态：

- 读请求必须等待输入数据到达。
- 写请求必须等待之前写入的数据写入介质。
- 必须打开设备，例如等待载波信号的调制解调器终端线，或等待读取器的 FIFO。
- 文件上启用了强制性锁，导致在读或写系统调用时等待锁定。

从概念上说，解决这个问题的最简单方案是不让进程进入睡眠。当 I/O 无法完成时，系统调用返回一个错误，指示它此时无法成功。这就是非阻塞 I/O。

## 以非阻塞模式打开文件

向 UNIX 内核指定你想使用非阻塞 I/O 的方法之一是通过带有 `O_NONBLOCK` 标志的 `open`：

```c
#include <fcntl.h>
int open(const char *path, int flags, ...);
```

其中 `flags` 参数包含 `O_NONBLOCK` 以非阻塞模式打开。

`O_NONBLOCK` 标志防止 `open(2)` 调用在由于某些原因必须等待时挂起调用进程的执行。这种情况可能会发生，例如终端线具有现代载波时。提供了 `O_NONBLOCK` 标志后，`open` 调用立即返回。

随后，在使用 `O_NONBLOCK` 标志完成 `open(2)` 后，其他 I/O 操作也受到非阻塞规则的限制。这将在后续章节中进一步解释。

以下显示了进程如何在非阻塞 I/O 模式下打开其终端线：

```c
int fd;                               // 终端文件描述符
fd = open("/dev/tty",O_RDWR|O_NONBLOCK);
if (fd == -1) {
    perror("open(2)");                   // 报告错误
    abort();                                // 终止运行。
// fd 以非阻塞 I/O 模式打开
```

一旦文件描述符以这种方式打开，对 `read(2)` 的调用将不再在等待输入时挂起程序的执行。

## 设置非阻塞模式

另一种选择非阻塞 I/O 模式是在文件或设备打开后调用 `fcntl(2)` 的服务：

```c
#include <fcntl.h>
int fcntl(int fd, int cmd, ...);
```

其中 `cmd` 是以下标志之一：

| 标志 | 说明 |
| :--- | :--- |
| `F_GETFL` | 获取标志 |
| `F_SETFL` | 设置标志 |

命令 `F_SETFL` 允许你在文件打开后启用 `O_NONBLOCK` 标志。然而，为了做到，你通常希望使用命令 `F_GETFL` 来获取当前生效的标志。

下面的示例显示了如何在已打开的文件描述符 `fd` 上启用 `O_NONBLOCK`：

```c
int fd;      /* 打开的文件描述符 */
int fl;      /* fd 的标志 */
fl = fcntl(fd,F_GETFL,0);
if ( fl == -1 ) { /* 报告失败 */
    perror(fcntl(F_GETFL));
    exit(13);
}
if (fcntl(fd,F_SETFL,fl|O_NONBLOCK) == -1 ) { /* 报告失败 */
    perror(fcntl(F_SETFL));
    exit(13);
}
```

注意在用 `F_SETFL` 命令调用 `fcntl(2)` 时，`O_NONBLOCK` 标志与变量 `fl` 中接收到的标志进行了按位或运算。

## 执行非阻塞 I/O

一旦文件描述符处于非阻塞 I/O 模式，你就可以配合常规的 `read(2)` 和 `write(2)` 调用使用它。当 `read(2)` 没有准备好返回的输入，或者 `write(2)` 无法写入输出时，`errno` 中返回的错误代码将是 `EAGAIN`。

> 注意
> `EAGAIN`—资源临时不可用。使用非阻塞 I/O 时返回此错误，表示没有可读的输入，或者此时无法写入输出。

列表 16.1 展示了一个在 FIFO 上使用非阻塞 I/O 的程序。

### 列表 16.1 nblockio.c—一个以非阻塞/O 模式读取 FIFO 的程序

```c
11: /* nblockio.c */
2: #include <stdio.h>
3: #include <unistd.h>
4: #include <fcntl.h>
5: #include <errno.h>
6:
7: int
8: main(int argc, char **argv) {
9:    int z;      /* 读取的字节数 */
10:   int fd;      /* 打开的文件描述符 */
11:   char buf[256]; /* 缓冲区 */
12:
13:   /* 终端线 */
14:   fd = open("/dev/tty",O_RDWR|O_NONBLOCK);
15:   if (fd == -1) { /* 报告失败 */
16:     perror("open(2)");
17:     exit(13);
18:   }
19:   /* fd 以非阻塞 I/O 模式打开 */
20:   while ( z = read(fd,buf,sizeof(buf)) == -1 && errno == EAGAIN ) {
21:
22:     if ( z >= 0) { /* 成功 */
23:       printf("INPUT! %s\n", buf);
24:     } else { /* 失败 */
25:       perror("read(2)");
26:     }
27:   }
28:   return 0;
29: }
```

编译该程序并创建 FIFO：

```bash
$ make nblockio
mkfifo fifo
cc -Wall nblockio.c -o nblockio
```

以下显示了示例会话：

```bash
$ ./nblockio &
echo BOO >fifo
$ GOT INPUT! BOO
[1] Exited          nblockio
```

上面的输出显示了 `nblockio` 程序从 FIFO 读取了数据。由于使用了 `O_NONBLOCK` 标志，`read(2)` 在没有数据可用时没有阻塞程序，而是返回了 `EAGAIN` 错误。当 `echo` 写入 FIFO 后，`read` 成功读取到数据并继续执行。

### 警告

运行此程序会消耗大量的 CPU：

```bash
$ ./nblockio &
```

运行此程序会消耗大量的 CPU：

```bash
$ ./nblockio &
```

为了避免意外留下它，请在后台运行它：

```bash
$ ./nblockio &
echo BOO >fifo
$ GOT INPUT! BOO
[1] Exited          nblockio
```

为了显示任务结束状态，按下回车：

```bash
$ ./nblockio &
echo BOO >fifo
$ GOT INPUT! BOO
[1] Exited          nblockio
```

上面的输出显示了 `echo` 命令通过 `write(2)` 写入了 FIFO。

```bash
$ ./nblockio &
echo BOO >fifo
$ GOT INPUT! BOO
[1] Exited          nblockio
```

上面的输出显示了 `nblockio` 程序读取了数据。由于使用了 `O_NONBLOCK` 标志，`read(2)` 在没有数据可用时没有阻塞程序，而是返回了 `EAGAIN` 错误。当 `echo` 写入 FIFO 后，`read` 成功读取到数据并继续执行。

## 文件描述符集与 select(2) 系统调用

你必须操作文件描述符集。

为了操作文件描述符集，这些是文件描述符的集合，可以更容易一次性指定多个文件描述符。下面的提要显示了用于操作文件描述符集的可用宏：

```
#include <sys/types.h>
```

```
FD_ZERO(fd_set *set)               /* 宏 */
FD_SET(int fd, fd_set *set)      /* 宏 */
FD_CLR(int fd, fd_set *set)      /* 宏 */
int FD_ISSET(int fd, fd_set *set) /* 返回 int 的宏 */
FD_SIZE /* 定义参数 fd 的最大值 */
```

在使用文件描述符集之前，你必须对其进行初始化。这通过 `FD_ZERO()` 宏完成：

```
fd_set fdset1;                   /* 文件描述符 1 */
FD_ZERO(&fdset1);                 /* 初始化 fdset1 */
```

通过 `FD_ZERO()` 初始化文件描述符集会使其包含“空集”。也就是说，集合中不包含任何文件描述符。

集合中最高的文件描述符的值是 `FD_SIZE`。如果文件描述符编号超过此值或为负，则 `FD_SET()`、`FD_CLR()` 和 `FD_ISSET()` 宏的行为未定义。

要向集合中添加文件描述符，使用 `FD_SET()` 宏。要将文件描述符 `fd` 添加到 `fdset1`，你可以写：
```
