
- 对应用程序列表中注册为就绪的那些描述符执行有限量的 I/O 操作（也许以轮询方式遍历它们，而不是在每次调用 `epoll_wait()` 后都从列表开始开始！）。当相关的非阻塞 I/O 系统调用因 `EAGAIN` 或 `EWOULDBLOCK` 错误失败时，可以将描述符从列表中移除。

尽管这需要额外的编程工作，但这种方法除了防止文件描述符饥饿外还有其他优点。例如，我们可以在上述循环包含其他步骤，如处理定时器和使用 `sigwaitinfo()`（或类似函数）接收信号。

在使用信号驱动 I/O 时也会出现饥饿，因为它也提供了一种边缘触发通知机制。然而，饥饿考虑并不一定适用于采用水平触发通知机制的应用。这是因为我们可以结合水平触发使用阻塞文件描述符，并使用一个持续检查描述符就绪状态的循环，在对就绪描述符执行 I/O 之前，再次检查就绪描述符。

## 63.5 等待信号和文件描述符

有时，进程需要等待某个文件描述符上的 I/O 变得可行或等待信号的传递。我们可能会尝试使用 `select()` 执行此类操作。

### 63-7 使用 select() 阻塞信号的错误方法:

```
sigatomic_t gotSig = 0;

void handler(int sig) {
    gotSig = 1;
}

int main(int argc, char *argv[]) {
    struct sigaction sa;
    ...
    sa.sa_handler = handler;
    sigemptyset(&sa.mask);
    sa.sa_flags = 0;

    /* 如果信号到达怎么办？ */
    ready = select(nfds, NULL, NULL);
    if (ready > 0) {
        printf("%d 文件描述符就绪\n", ready);
    } else if (ready == -1 && errno == EINTR) {
        if (gotSig)
            printf("收到信号\n");
    } else {
        /* 其他错误 */
    }
}
```

此代码的问题在于，如果信号在调用 `select()` 之前到达了（这存在竞态条件）。我们现在查看解决问题的办法。

从 2.6.27 版本开始，Linux 提供了一种可以同时等待信号和文件描述符的进一步技术：22.11 中描述的 `signfd` 机制

### 63.5.1 pselect() 系统调用

`pselect()` 执行的任务与 `select()` 类似。主要的语义区别在于额外的参数 `sigmask`，它指定了调用阻塞期间取消屏蔽的信号。

```
#include <sys/select.h>

int pselect(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds,
             struct timespec *timeout, const sigset_t *sigmask);
    返回就绪的文件描述符数量，超时返回 0，错误返回 -1
```

更精确地说，假设有以下 `pselect()` 调用：

```
ready = pselect(nfds, &readfds, &writefds, &exceptfds, timeout, &sigmask);
```

此调用等价于原子性地执行以下步骤：

```
sigset_t ormask;
sigprocmask(SIG, SETMASK, &ormask);
ready = select(nfds, &readfds, &writefds, &exceptfds, timeout);
sigprocmask(SIG, SETMASK, &ormask, NULL);  /*恢复信号掩码 */
```

## 列表 63-8: 使用 pselect()

```c
sigset_t emptyset, blockset;
struct sigaction sa;

sigemptyset(&blockset);
sigaddset(&blockset, SIGUSR1);

if (sigprocmask(SIG_BLOCK, blockset, NULL) == -1)
    errexit("sigprocmask");

s.sa_action = handler;
sigemptyset(&sa.sa_mask);
s.sa_flags = SA_RESTART;
if (sigaction(SIGUSR1, &sa, NULL) == -1)
    errexit("sigaction");

sigemptyset(&emptyset);
ready = pselect(nfds, &readfs, NULL, NULL, NULL, &emptyset);
if (ready == -1)
    errexit("pselect");
```

## poll() 和 epoll_wait() 系统调用

Linux 2.6.16 增加了一个新的系统调用 `poll()`，它与 `select()` 的关系类似于 `pselect()` 与 `select()` 的关系。同样，从内核 2.6.19 开始，Linux 还包含了 `epoll_wait()`，提供了类似于 `epoll_wait()` 的扩展。详情请参见 `poll(2)` 和 `epoll_wait(2)` 手册页。

### 63.5.2 自管道技巧 (The Self-Pipe Trick)

由于 `pselect()` 并没有广泛实现，可移植应用程序必须采用其他策略，在同时等待信号和对文件描述符调用 `select()` 时避免竞态条件。一种常见的解决方案是：

- 1. 创建管道，并将其读端和写端标记为非阻塞。
- 2. 在监控所有感兴趣的文件描述符的同时，将管道的读端包含在传递 `select()` 的 `readfs` 集中。
- 3. 为感兴趣的信号安装处理函数。当该信号处理函数被调用时，它向管道写入一个字节的数据。请注意关于信号处理函数的以下几点：
    - 管道的写端在第一步中被标记为非阻塞，以防止信号到达得过快，导致重复调用信号处理函数填满管道，从而导致信号处理函数的 `write()`（以及进程本身）被阻塞。（对满管道进行写入失败没有关系，因为之前的写入已经指示了信号的送达。）
    - 信号处理函数在创建管道后安装，以防止在管道创建之前送达信号可能导致的竞态条件。
    - 在信号处理函数内部使用 `write()` 是安全的，因为它是 426 页表 21-1 中列出的异步信号安全函数之一。
- 4. 将 `select()` 置于循环中，这样当它被信号处理函数中断时，它可以重启。（以这种方式重启并不是绝对必要的；它仅仅意味着我们可以通过检查 `readfds` 来检查信号的到达，而不是检查 `EINTR` 错误返回）。
- 5. 在 `select()` 调用成功完成后，我们可以通过检查管道读端的文件描述符是否设置在 `readfds` 中来确定信号是否到达。
- 6. 每当信号到达时，读取管道中所有的字节。由于可能会有多个信号到达，请使用循环读取字节，直到（非阻塞的）`read()` 因错误 `EAGAIN` 失败。在清空管道后，执行响应信号送达必须采取的任何操作。

这种技术通常被称为自管道技巧（self-pipe trick），列表 63-9 显示了演示该技术的代码。

该技术的变体同样可以用于 `poll()` 和 `epoll_wait()`。

## 列表 63-9: 使用自管道技巧

```c
static int fd[2]; /* 管道的文件描述符 */

static void
handler(int sig) {
    int savedErrno; /* 以防我们修改 'errno' */
    if (write(fd[1], "x", 1) == -1 && errno != EAGAIN)
        errExit("write");
    errno = savedErrno;
}

int
main(int argc, char *argv[]) {
    fd_set ready, nfds, flags;
    struct timeval timeout;
    struct timeval *pto;
    struct sigaction sa;
    char ch;

/* ... 为 select() 初始化 'timeout', 'readfds' 和 'nfs' ... */

if (pipe(pfd) == -1)
    errExit("pipe");

FD_SET(pfd[0], &readfds);      /* 将管道端添加到 'readfds' */
nfs = max(nfs, pfd[0] + 1);     /* 如果需要，调整 'nfs' */

flags = cntl(pfd[0], F_GETFL);      /* 使读端非阻塞 */
if (flags == -1)
    errExit("cntl-F_GETFL");
flags |= O_NONBLOCK;

if (cntl(pfd[0], F_SETFL, flags) == -1)   /* 使写端非阻塞 */
    errExit("cntl-F_SETFL");

flags = cntl(pfd[1], F_GETFL); 
if (flags == -1)
    errExit("cntl-F_GETFL");
flags |= O_NONBLOCK;

if (cntl(pfd[1], F_SETFL, flags) == -1)   /* 使写端非阻塞 */
    errExit("cntl-F_SETFL");

if (ready == -1)
    errexit("pselect");

if (ready > 0 && FD_ISSET(pfd[0], &readfds)) {
    /* 处理信号到达 */
    while (read(pfd[0], &ch, 1) > 0) {
        /* 清空管道 */
    }
} else {
    ready = pselect(nfds, &readfs, NULL, NULL, NULL, &emptyset);
}
```

[Stevens et al., 2004] 描述了 I/O 多路复用和信号驱动 I/O，特别强调了这些机制在 socket 中的用法。[Gammo et al, 2004] 是一篇比较 `select()`、`poll()` 和 `epoll` 性能的论文。

一个特别有趣的在线资源是 http://www.kegel.com/c10k.html。该页面由 Dan Kegel 编写，题为“C10k 问题”，探索了 Web 服务器开发者在同时为数万客户端提供服务时面临的问题。该网页包含了许多指向相关信息的链接。

## 63.7 练习

- 63-1. 修改列表 63-2 中的程序 (`poll_pipes.c`)，使用 `select()` 替换 `poll()`。
- 63-2. 编写一个 echo 服务器（第 60.2 和第 60.3 节），同时处理 TCP 和 UDP 客户端。为了实现这一点，服务器必须同时创建一个监听 TCP socket 和一个 UDP socket，然后使用本章描述的技术之一监控这两个 socket。
- 63-3. 第 63.5 节提到 `select()` 不能用于同时等待信号和文件描述符，描述了一种使用信号处理程序和管道的解决方案。当程序需要同时等待文件描述符和 System V 消息队列的输入时，也存在相关问题（因为 System V 消息队列不使用文件描述符）。一种解决方案是 fork 一个单独进程，处理队列中的每条消息并将其发送到管道，该管道包含在父进程监控的描述符列表中。编写一个使用此方案通过 `select()` 监控终端和消息队列输入的程序。
- 63-4. 第 63.52 节中对自管道（self-pipe）技术描述的最后一步指出，程序应该先排空管道，然后执行响应信号应采取的任何操作。如果这些子步骤反过来执行会发生什么？
- 63-5. 修改列表 63-9 中的程序 (`self_pipe.c`)，使用 `epoll()` 替换 `select()`。
- 63-6. 编写一个程序，使用 `epoll_create()` 创建一个 epoll 实例，并立即使用 `epoll_wait()` 等待返回的文件描述符。在这种情况下，当 `epoll_wait()` 是一个带有感兴趣列表的 epoll 描述符时会发生什么？为什么这可能有用？
- 63-7. 假设我们有一个 epoll 文件描述符监控多个文件描述符，且所有都已就绪。如果我们执行的一系列 `epoll_wait()` 调用中 `maxvents` 远小于就绪文件描述符的数量（例如 `maxvents` 为 1），且在调用之间不对就绪描述符执行所有 I/O 操作，每次调用 `epoll_wait()` 返回哪个描述符？编写一个程序来确定答案。（为了实验目的，只需在 `epoll_wait()` 系统调用之间不执行 I/O 即可。）为什么这可能有用？
- 63-8. 修改列表 63-3 中的程序 (`demo_sigio.c`)，使用实时信号替换 SIG10。修改信号处理程序以接受 `siginfo_t` 参数，并显示该结构 `si_fd` 和 `si_code` 字段的值。

## 伪终端 (PSEUDOTERMINALS)

伪终端是一个提供 IPC 通道的虚拟设备。在通道的一端是一个期望连接到终端设备的程序。在另一端是一个程序通过使用通道发送输入和读取输出来驱动该终端导向型程序。

本章描述了伪终端的使用，展示了它们如何被应用于终端仿真器、script(I) 程序以及如 ssh 等提供网络登录服务的程序中。

### 64.1 概述

图 64 展示了伪终端帮助我们解决的问题之一：我们如何让位于一台主机上的用户能够操作通过网络连接的另一台主机上的终端导向型程序（例如 `vi`）。

如图所示，通过允许网络通信，socket 提供了解决此问题所需的部分机制。然而，我们无法直接将终端面向型程序的标准输入、输出和错误连接到 socket。这是因为终端面向型程序期望连接到终端——以便能够执行第 34 节和第 62 节描述的终端导向型操作。此类操作包括将终端设置为非规范模式、开启或关闭回显（echoing）以及设置终端前台进程组。如果程序尝试在 socket 上执行这些操作，相关的系统调用将失败。

此外，终端面向型程序期望终端驱动程序对其输入和输出进行某些类型的处理。例如，在规范模式下，当终端驱动程序在行首看到文件结束字符（通常是 Control-D）时，它会导致下一次 `read()` 返回无数据。

最后，终端面向型程序必须有一个控制终端。这允许程序通过打开 `/dev/tty` 获取控制终端的文件描述符，并使得为程序生成作业控制和终端相关成为可能（例如 SIGTSTP、SIGTIN 和 SIGINT）。

从这些描述可以清楚地看出，终端面向型程序的定义非常广泛。它涵盖了我们通常在交互式会话中运行的大量程序。

![img/9979af2ec677a84a39c7b1fd105c84a1419_0.png](图-64 问题：如何通过网络操作终端导向型程序)

## 伪终端主端和从端 (The pseudoterminal master and slave)

伪终端是一个提供 IPC 通道的虚拟设备。在通道的一端是一个期望连接到终端设备的程序。在另一端是一个程序通过使用通道发送输入和读取输出来驱动该终端导向型程序。

本章描述了伪终端的使用，展示了它们如何被应用于终端仿真器、script(I) 程序以及如 ssh 等提供网络登录服务的程序中。

### 64.1 概述

图4展示了伪终端帮助我们解决的问题之一：我们如何让位于一台主机上的用户能够操作通过网络连接的另一台主机上的终端导向型程序（例如 `vi`）。

如图所示，通过允许网络通信，socket 提供了解决此问题所需的部分机制。然而，我们无法直接将终端面向型程序的标准输入、输出和错误连接到 socket。这是因为终端面向型程序期望连接到终端——以便能够执行第 34 节和第 62 节描述的终端导向型操作。此类操作包括将终端设置为非规范模式、开启或关闭回显以及设置终端前台进程组。如果程序尝试在 socket 上执行这些操作，相关的系统调用将失败。

此外，终端面向型程序期望终端驱动程序对其输入和输出进行某些类型的处理。例如，在规范模式下，当终端驱动程序在行首看到文件结束字符（通常是 Control-D）时，它会导致下一次 `read()` 返回无数据。

最后，终端面向型程序必须有一个控制终端。这允许程序通过打开 `/dev/tty` 获取控制终端的文件描述符，并使得为程序生成作业控制和终端相关信号成为可能（例如 SIGTSTP、SIGTIN 和 SIGINT）。

从这些描述可以清楚地看出，终端面向型程序的定义非常广泛。它涵盖了我们通常在交互式会话中运行的大量程序。

![img/9979af2ec677a84a39c7b1fd105c84a1419_0.png](图-64 问题：如何通过网络操作终端面向程序)

## 程序如何使用伪终端 (How programs use pseudoterminals)

伪终端是一个提供 IPC 通道的虚拟设备。在通道的一端是一个期望连接到终端设备的程序。在另一端是一个程序通过使用通道发送输入和读取输出来驱动该终端导向型程序。

伪终端是一对连接设备：伪终端主端和伪终端从端（有时称为 pty）。伪终端提供的 IPC 通道类似于管道——两个进程可以操作主端和从端。关于伪终端的关键点在于从端看起来就像一个标准终端。可以应用于终端的所有操作也可以应用于伪终端从端。其中某些操作对伪终端没有意义（例如设置波特率或校验），但伪终端会忽略忽略它们。

![img/9979af2ec677a84a39c7b1fd105c84a1420_0.png](图 64-2 通过伪终端通信的程序)
