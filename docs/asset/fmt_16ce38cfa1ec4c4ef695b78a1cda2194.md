
## 表 8.2. POSIX 保证异步信号安全的函数。

| `_Exit` | `getpid` | `sigaddset` |
|---|---|---|
| `_exit` | `getppid` | `sigdelset` |
| `accept` | `gethostname` | `sigemptyset` |
| `access` | `getsockopt` | `sigfillset` |
| `aio_error` | `getuid` | `sigmemown` |
| `aio_return` | `kill` | `signal` |
| `aio_suspend` | `link` | `sigpause` |
| `alarm` | `listen` | `sigpending` |
| `bind` | `lseek` | `sigprocmask` |
| `cfgetispeed` | `lstat` | `sigqueue` |
| `cfgtpeed` | `mkdir` | `sigset` |
| `cfsetispeed` | `mkfifo` | `sigsuspend` |
| `cfsetspeed` | `open` | `sleep` |
| `chdir` | `pathconf` | `socket` |
| `chmod` | `poll` | `sockpair` |
| `chown` | `pipe` | `stat` |
| `clock_gettime` | `poll` | `symlink` |
| `close` | `posix_trace_event` | `sysconf` |
| `connect` | `raise` | `tcdrain` |
| `create` | `tcflow` | |

| `dup` | `read` | `tcflush` |
|---|---|---|
| `n dup2` | `readlink` | `tcgetattr` |
| `execle` | `recv` | `tcgetpgrp` |
| `execve` | `recvfrom` | `tcsendbreak` |
| `fchmod` | `recvmsg` | `tcsetattr` |
| `fchown` | `rename` | `tcgetpgrp` |
| `fcntl` | `rmdir` | `time` |
| `fdatasync` | `select` | `timer_getoverrun` |
| `fork` | `sem_post` | `timer_gettime` |
| `fpathconf` | `send` | `timer_settime` |
| `fstat` | `sendmsg` | `times` |
| `fsync` | `sendto` | `umask` |
| `truncate` | `setgid` | `uname` |
| `getgid` | `setpgid` | `unlink` |
| `getuid` | `setid` | `utime` |
| `getgid` | `setsockopt` | `wait` |
| `getgroups` | `setuid` | `waitpid` |
| `getpeername` | `shutdown` | `write` |
| `getpgrp` | `sigaction` | |

信号处理非常复杂，但这里有一些实用的规则：

- 当有疑问时，在程序中显式地重启库调用，或者使用附录 B 中的重启库。
- 检查信号处理程序中使用的每个库函数，确保它在异步信号安全（async-signal safe）函数列表中。
- 仔细分析更改外部变量的信号处理程序与访问该变量的其他程序代码之间潜在的交互。阻塞信号以防止意外的交互。
- 在适当的情况下保存并恢复 `errno`。

## 8.7 使用 siglongjmp 和 sigsetjmp 进行程序控制

程序有时使用信号来处理并非致命但可能发生在程序许多地方的错误。例如，用户可能希望在中止长时间计算或被阻塞长时间的 I/O 操作时避免终止程序。程序对 Ctrl-C 的响应应该在开始处（或某个指定位置）结束。当程序具有嵌套的提示符或菜单，并且在用户输入响应时应从头开始时，也会发生类似的情况。面向对象的语言通常通过抛出异常并在其他地方捕获异常来处理这些情况。C 程序通过间接或直接使用信号来处理这类问题。

在间接方法中，`SIGINT` 的信号处理程序在响应 Ctrl-C 时设置一个标志。程序测试该标志，如果标志被设置，则返回到预期的终止点。间接方法是复杂的，因为程序可能需要通过多个层层函数返回。在每次返回时，程序都会针对这种特殊情况测试该标志。

在直接方法中，信号处理程序直接跳回终止点。这种跳转需要展开程序栈。`sigjmp` 和 `siglongjmp` 一对函数提供了这种能力。`sigjmp` 函数对于一个语句标签（label）是匿名的，而 `siglongjmp` 函数相当于 `goto` 语句。主要的区别在于 `sigjmp` 和 `siglongjmp` 配对处理栈和信号状态。

调用 `sigjmp` 是为了要返回的点。`sigjmp` 在程序中提供一个标记。调用者必须提供一个类型为 `sigjmp_buf` 的缓冲区 `env`，`sigjmp` 初始化跳转到标记所需的信息。如果 `savemask` 非零，信号掩码存在 `env` 缓冲区中。当程序直接调用 `sigjmp` 时，它返回 0。从信号处理程序跳转的 `sigjmp` 使用相同的 `sigjmp_buf` 变量执行 `siglongjmp`，使得程序带有 `val` 值从 `sigjmp` 返回。

### 概要 (Synopsis)

```
#include <setjmp.h>

void siglongjmp(sigjmp_buf env, int val);

int setjmp(sigjmp_buf env, int savemask);
```

POSIX：`siglongjmp` 没有定义的错误。`setjmp` 在直接调用时返回 0，在由 `siglongjmp` 调用时返回 `val` 参数。C 标准库提供了 `setjmp` 和 `longjmp` 用于上述跳转类型，但这些函数对信号掩码的操作取决于 `savemask`。`sigjmp` 函数允许程序指定重置哪些信号。仅当 `savemask` 的值非零时，`siglongjmp` 函数恢复信号掩码。`siglongjmp` 的 `val` 参数指定了 `sigjmp` 返回的点。

### 程序 8.12 sigjmp.c

设置信号处理程序的代码，在输入 Ctrl-C 时返回到主循环。

```c
#include <jmp.h>
#include <signal.h>
#include <stdio.h>
#include <unistd.h>
static sigjmp_buf jmpbuf;
static volatile sig_atomic_t jumpok = 0;
/* ARGUMENT */
static void handler(int signo) {
    if (jumpok == 0) return;
    siglongjmp(jmpbuf, 1);
}
int main(void) {
    struct sa act;
    act.sa_flags = 0;
    act.sa_handler = handler;
    if ((sigemptyset(&act.sa_mask)) == -1 ||
        (signal(SIGINT, &act, NULL) == -1)) {
        perror("Failed to set SIGINT handler");
        return 1;
    }
    fprintf(stderr, "This is process %ld\n", (long)getpid());
    if (sigsetjmp(jmpbuf, 1))
        fprintf(stderr, "Returned to main loop due to ");
    jumpok = 1;
    for ( ;
        /* 主循环在这里 */
}
```

程序 8.12 显示了如何设置 `SIGINT` 信号处理程序，在输入 Ctrl-C 时使程序返回主循环。在调用 `siglongjmp` 之前使用 `sigjmp` 以建立返回点。`sigaction` 的调用应该出现在 `sigsetjmp` 之前，以便其只调用一次。为了防止信号处理程序在程序执行 `sigjmp` 之前调用 `siglongjmp`，程序 8.12 使用了标志 `jumpok`。信号处理程序会测试此标志。

通常在执行读取或写入时，进程阻塞直到 I/O 完成。某些性能敏感型应用程序倾向于启动请求并继续执行，允许 I/O 操作与程序执行异步进行。旧的异步 I/O 方法使用 `SIGFOLLOW` 或 `SIGIO` 在 I/O 可用时通知进程。这些信号的机制通过 `ioctl` 设置。本节讨论了随 POSIX:RT 实时扩展引入的更新版本 POSIX:AIO 异步 I/O。

POSIX:AIO 通过四个主要函数扩展了其对异步 I/O 的定义。`aio_read` 函数进程对打开的文件描述符队列读取请求。`aio_write` 函数在异步 I/O 操作完成后返回其状态，`aio_error` 函数返回错误状态。第五个函数 `aio_cancel` 允许取消正在进行的异步 I/O 操作。

`aio_read` 和 `aio_write` 函数接收单个参数 `aiocb`，它是指向异步 I/O 控制块的指针。`aio_read` 从 `aiocb->aio_files` 关联的文件在 `aiocb->aio_buf` 指定的缓冲区中读取 `aiocb->aio_bytes`。当请求被队列时，函数返回。`aio_write` 函数的行为类似。

### 概要 (Synopsis)

```
#include <aio.h>
int aio_read(struct aiocb *aiocb);
int aio_write(struct aiocb *aiocb);
```

POSIX:AIO

如果请求成功队列，`aio_read` 和 `aio_write` 返回 0。如果失败，这些函数返回 `errno`。下表列出了异步 I/O 的强制性错误。

| errno | 原因 |
| :--- | :--- |
| `EAGAIN` | 系统没有资源 |
| `EBADF` | 无效的文件描述符 |
| `EFBIG` | `aio_offset` 超过最大值 |
| `ECANCELED` | 因为 `aio_cancel` 被取消 |
| `EINVAL` | `aiocb` 的无效成员 |
| `EOVERFLOW` | `aio_offset` 超过最大值 |

在 `aio_read` 和 `aio_write` 返回之前发生的错误带有 B 标记。这些状态随 -1 返回。返回后发生的错误带有 A 标记。这些错误通过调用 `aio_error` 返回。

`aiocb` 结构至少包含以下成员：

```c
int                 aio_fd;         /* 文件描述符 */
volatile void *     aio_buf;         /* 缓冲区位置 */
size_t              aio_nbytes;     /* 传输长度 */
off_t               aio_offset;     /* 文件偏移 */
int                 aio_reprio;     /* 请求优先级 */
struct sigvent     aio_sigvent;   /* 信号编号和值 */
int                 aio_opcode;     /* 操作 */
```

结构的前三个成员与普通的读取或写入函数参数相似。`aio_offset` 指定了 I/O 在文件中的起始位置。实现（POSIX_PRIORITY_SCHEDULING）降低返回优先级。`aio_sigvent` 字段指定了如何通知完成。如果 `aio_sigvent.sigev_notify` 值为 `SIGV_NONE`，则操作系统在 I/O 完成时不产生信号。在 `aio_sigvent.sigev_sign` 中，`aio_opcode` 被列出函数（未讨论）用于处理多个 I/O 请求。

`aio_error` 和 `aio_return` 函数返回由 `aiocb` 指定的 I/O 操作的状态。使用 `aio_error` 监控异步 I/O 的进度。当操作完成后，调用 `aio_return` 获取读取或写入的字节数。

### 概要 (Synopsis)

```
size_t aio_return(struct aiocb *aiocb);
int aio_error(const struct aiocb *aiocb);
```

POSIX：：

当 I/O 操作成功完成时，`aio_error` 返回 0；如果 I/O 操作仍在执行则返回 `EINPROGRESS`。如果操作失败，`aio_error` 返回错误代码。该状态对应相应的读取或写入函数本应返回的 `errno` 值。`aio_return` 函数返回底层完成 I/O 操作的状态。一旦调用了 `aio_return`，在对此缓冲区启动另一个异步操作之前，不应对同一个 `aiocb` 再调用 `aio_return` 或 `aio_error`。如果异步操作未完成，`aio_return` 是未定义的。

POSIX 异步 I/O 可以使用或不使用信号，取决于 `aiocb` 结构中 `sigev_notify` 字段的设置。程序 8.13 和 8.14 阐释了如何实现

异步 I/O。其核心思想是设置一个信号处理器，在初始 I/O 操作启动后完成所有工作。

程序 8.13 是一个将一个文件复制到另一个文件的程序。从第一个文件的读取通过异步 I/O 完成，而写入第二个文件通过普通的 I/O 完成。如果输入是可能会长时间阻塞的管道或网络连接，而输出是普通文件，这种方法就是合适的。程序接受文件名作为参数，并将第一个参数用于读取，第二个参数用于写入。程序设置了一个信号处理器，并通过重新读取来启动第一次读取。当异步拷贝完成并调用 `getdone` 时，信号会作为例例行程序被设置。主程序调用 `dowork` 并检查异步拷贝是否完成。拷贝完成后，程序将显示复制的字节数或错误信息。

程序 8.14 包含了用于异步 I/O 的信号处理器以及初始化例程。`initread` 设置了用于异步读取的 `struct aiocb` 结构体，并在其修改时保存输出文件描述符。它初始化了所有全局变量，并通过调用 `restart` 启动第一次读取。程序 8.14 记录了发生的第一个错误和传输的总字节数。`doneflag` 类型为 `sig_atomic_t`，可以被信号处理器原子性地访问。变量 `globalerror` 和 `totalbytes` 仅在 I/O 完成后可用，因此它们永远不会被信号处理器和主程序并发访问。主程序使用异步 I/O 在执行其他工作的同时复制文件。

## Program 8.13 asyncsignal.c

```c
#include <errno.h>
#include <fcntl.h>
#include <signal.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/stat.h>
#include "asyncsignal.h"
#define BLOCKSIZE 1024
#define MODE (S_IRUSR | S_IWUSR | S_IROTH)
void dowork(void);
int main(int argc, char *argv[]) {
    char buf[BLOCKSIZE];
    int done = 0;
    int error;
    int fd1;
    int fd2;
    /* open file descriptors for I/O */
    if (argc != 3) {
        fprintf(stderr, "Usage: %s filename filename2\n", argv[0]);
        return 1;
    }
    if ((fd1 = open(argv[1], O_RDONLY)) == -1) {
        fprintf(stderr, "Failed to open %s\n", argv[1], strerror(errno));
        return 1;
    }
    if ((fd2 = open(argv[2], O_WRONLY | O_CREAT | O_TRUNC, MODE)) == -1) {
        fprintf(stderr, "Failed to open %s\n", argv[2], strerror(errno));
        return 1;
    }
    if (itsignal(SIGRTMAX) == -1) {
        perror("Failed to initialize signal");
        return 1;
    }
    if (initread(fd1, fd2, SIGRTMAX, buf, BLOCKSIZE) == -1) {
        perror("Failed to initiate the first read");
        return 1;
    }
    for (;;) {
        dowork();
        if (!done) {
            if ((error = getdone())) {
                fprintf(stderr, "Failed to copy file: %s\n", strerror(error));
            } else
                fprintf(stderr, "Copy successful, %d bytes\n", getbytes());
        }
    }
```
