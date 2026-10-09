
我们从图 13.1 调用 `daemonize` 来初始化守护进程。当它返回时，我们从图 13.6 调用 `already_running` 以确保只有一个守护进程的副本在运行。此时，`SIGHUP` 被忽略了，因此我们需要将处理重置为默认行为；否则，调用 `sigwait` 的线程可能永远看不到该信号。

阻塞所有信号（正如多线程程序建议的那样），并创建一个线程来处理信号。该线程唯一的工作是等待 `SIGHUP` 和 `SIGTERM`。当它接收到 `SIGHUP` 时，线程调用 `reread` 来重新读取其配置文件。当它接收到 `SIGTERM` 时，线程记录消息并退出。

回想图 10.1，`SIGHUP` 和 `SIGTERM` 的默认操作是终止进程。由于我们阻塞了这些信号，当向进程发送其中一个信号时，守护进程不会死亡。相反，调用 `sigwait` 的线程将返回，并指示已接收到信号。

### 示例

并不是所有的守护进程都是多线程的。图 13.8 中的程序展示了单线程守护进程如何捕获 `SIGHUP` 并重新读取其配置文件。

```c
#include "apue.h"
#include <syslog.h>
#include <errno.h>

extern int lockfile(int);
extern int already_running(void);

void
reread(void)
{
    /* ... */
}

void
sigterm(int signo)
{
    syslog(LOG_INFO, "got SIGTERM; exiting");
    exit(0);
}
void
sighup(int signo)
{
    syslog(LOG_INFO, "Re-reading configuration file");
    reread();
}
int
main(int argc, char *argv[])
{
    char *cmd;
    struct sigaction sa;
    if ((cmd = strchr(argv[0], '/')) == NULL)
        cmd = argv[0];
    else
        cmd++;

    /*
     * Become a daemon.
     */
    daemonize(cmd);

    /*
     * Make sure only one copy of the daemon is running.
     */
    if (already_running()) {
        syslog(LOG_ERR, "daemon already running");
        exit(1);
    }

    /*
     * Handles signals of interest.
     */
    sa.sa_handler = sigterm;
    sigemptyset(&sa.sa_mask);
    sigaddset(&sa.sa_mask, SIGHUP);
    sa.sa_flags = 0;
    if (sigaction(SIGTERM, &sa, NULL) < 0) {
        syslog(LOG_ERR, "can't catch SIGTERM: %s", strerror(errno));
        exit(1);
    }
    sa.sa_handler = sighup;
    sigemptyset(&sa.sa_mask);
    sigaddset(&sa.sa_mask, SIGTERM);
    sa.sa_flags = 0;
    if (sigaction(SIGHUP, &sa, NULL) < 0) {
        syslog(LOG_ERR, "can't catch SIGHUP: %s", strerror(errno));
        exit(1);
    }

    /*
     * Proceed with the rest of the daemon.
     */
    /* ... */
    exit(0);
}
```

图 13.8 守护进程重新读取配置文件的另一种实现

我们从图 13.1 调用 `daemonize` 来初始化守护进程。当它返回时，我们从图 13.6 调用 `already_running` 以确保只有一个守护进程的副本在运行。此时，`SIGHUP` 被忽略了，因此我们需要将处理重置为默认行为；否则，调用 `sigwait` 的线程可能永远看不到该信号。

## 13.7 客户端-服务器模型

并不是所有的守护进程都是多线程的。图 13.8 中的程序展示了单线程守护进程如何捕获 `SIGHUP` 并重新读取其配置文件。

阻塞所有信号，正如多线程程序建议的那样，并创建一个线程来处理信号。该线程唯一的工作是等待 `SIGHUP` 和 `SIGTERM`。当它接收到 `SIGHUP` 时，线程调用 `reread` 来重新读取其配置文件。当它接收到 `SIGTERM` 时，线程记录消息并退出。

回想图 10.1，`SIGHUP` 和 `SIGTERM` 的默认操作是终止进程。由于我们阻塞了这些信号，当向进程发送其中一个信号时，守护进程不会死亡。相反，调用 `sigwait` 的线程将返回，并指示已接收到信号。

## 14.1 高级 I/O

### 14.1 引言

本章涵盖了许多被归类为“高级 I/O”的话题和函数：非阻塞 I/O、记录锁定、I/O 复用（`select` 和 `poll` 函数）、异步 I/O、`readadv` 和 `writev` 函数以及内存映射 I/O（`mmap`）。在描述第 15 章和第 17 章中的进程间通信以及后续章节中的许多示例之前，我们需要涵盖这些主题。

### 14.2 非阻塞 I/O

在第 10.5 节中，我们说系统调用分为两类：“慢”调用和其他所有调用。慢系统调用是可能会永久阻塞的调用。它们包括：

- 如果某些文件类型（管道、终端设备和网络设备）不存在数据，读取可能会阻塞。
- 如果数据无法被这些相同的文件类型立即接受，写入可能会永久阻塞（例如管道没有空间、网络流量控制）。
- 在某些文件类型上等待某些条件的打开可能会阻塞（例如打开终端设备时等待连接的调制解调器接听，或者以只写模式打开 FIFO，而没有其他进程以读模式打开 FIFO）。
- 对启用了强制记录锁定的文件的读取和写入。
- 特定的 `ioctl` 操作。
- 一些进程间通信函数（第 15 章）。

我们也提到过，与 I/O 相关的系统调用并不被认为是慢的，尽管读取或写入磁盘文件可能会阻塞调用者。

非阻塞 I/O 允许我们使用 I/O 操作（如 `open`、`read` 或 `write`）而不会永久阻塞。如果操作无法完成，调用将立即返回错误，指示该操作本应阻塞。

有两种方法为给描述符指定非阻塞 I/O：

1. 如果我们调用 `open` 获取描述符，可以指定 `O_NONBLOCK` 标志（第 3.3 节）。
2. 对于已经打开的描述符，我们调用 `fcntl` 来开启 `O_NONBLOCK` 文件状态标志（第 3.14 节）。图 3.12 显示了一个我们可以调用的函数，用于开启描述符的任何文件状态标志。

版本的 System V 使用 `O_NDELAY` 来指定非阻塞模式。System V 版本在没有数据可读时，`read` 函数返回值为 0。由于这种使用返回值 0 来提供非阻塞的方法与 Unix 系统惯例（用 0 表示文件结束）相冲突，POSIX 选择了提供不同的名称和语义。与这些其他 System V 版本不同，当我们从 `read` 收到 0 时，并不知道是调用阻塞了还是遇到了文件末尾。我们将看到，POSIX 要求如果从非阻塞描述符中没有数据可读，则返回 -1 并将 `errno` 设置为 `EAGAIN`。来自 System V 的平台同时支持旧的 `O_NDELAY` 和 POSIX 的 `O_NONBLOCK`，但在本文中我们将仅使用 POSIX.1 特性。较旧的 `O_NDELAY` 是为了向后兼容，不应在新应用程序中使用。

4.3BSD 为 `fcntl` 提供了 `FNDEL` 标志，其语义是不同的。它不仅会影响描述符的文件状态标志，还会改变终端或套接字的标志，这会影响该终端或套接字的所有用户，而不仅仅是共享同一个文件表的用户（4.3BSD 的非阻塞 I/O 在终端和套接字上工作的）。如果对非阻塞描述符的操作无法不阻塞的情况下完成，4.3BSD 会返回 `EBLOCK`。如今，基于 BSD 的系统提供了 POSIX.1 的 `O_NONBLOCK` 标志并返回 `EAGAIN`。这些系统使用与其他 POSIX 兼容系统一致的非阻塞语义：文件状态标志的变化会影响同一个文件表条目的所有用户，但与通过其他文件表条目访问同一设备的操作是独立的（参见图 3.7 和 3.9）。

#### 示例

让我们来看一个非阻塞 I/O 的例子。图 14.1 中的程序从标准输入读取多达 500,000 字节，并尝试将其写入标准输出。首先将标准输出设置为非阻塞。输出在一个循环中进行，每次写入的结果都会打印在标准错误上。`clear_fl` 函数与我们在图 3.12 中展示的 `set_fl` 函数类似。这个新函数简单地清除一个或多个标志位。

```c
#include "apue.h"
#include <errno.h>
#include <fcntl.h>

char buf[500000];

int
main(void) {
    int ntwrite;
    char *ptr;

    ntwrite = read(STDOUT_FILENO, buf, sizeof(buf));
    fprintf(stderr, "read %d bytes\n", ntwrite);

    set_fl(STDOUT_FILENO, O_NONBLOCK); /* 设置非阻塞 */
    ptr = buf;
    while (ntwrite > 0) {
        errno = 0;
        ntwrite = write(STDOUT_FILENO, ptr, ntwrite);
        fprintf(stderr, "write = %d, errno = %d\n", ntwrite, errno);

        if (ntwrite > 0) {
            ptr += ntwrite;
            ntwrite -= ntwrite;
        }
    }

    clr_fl(STDOUT_FILENO, O_NONBLOCK); /* 清除非阻塞 */
    exit(0);
}
```

图 14.1 大非阻塞写入

如果标准输出是一个普通文件，预计写入将执行一次：

```bash
$ ls -l /etc/services                               # 打印文件大小
-rw-r--r-- 1 root      677959 Jun 23 2009 /etc/services
$ ./a.out < /etc/services > temp.file               # 尝试普通文件
read 500000 bytes
write = 500000, errno = 0               # 单次写入
$ ls -l temp.file                               # 验证输出文件大小
-rw-rw-r-- 1 sar       500000 Apr 1 13:03 temp.file
```

如果标准输出是一个终端，预计写入有时会返回部分计数，有时会返回错误。这就是我们看到的：

```bash
$ ./a.out < /etc/services 2>stderr.out
$ cat stderr.out
read 500000 bytes
write = 100000, errno = 0
write = 100000, errno = 0
write = 100000, errno = 0
write = 100000, errno = 0
write = 100000, errno = 0
write = -1, errno = EAGAIN
```

## fcntl 记录锁

让我们复习第 3.14 节中 `fcntl` 函数的原型。

```c
#include <fcntl.h>
fcntl(int fd, int cmd, ... /* struct flock *flockptr */);
    返回：如果成功则返回所需的 cmd 值（见下文），出错时返回 -1
```

对于记录锁，`cmd` 为 `F_GETLK`、`F_SETLK` 或 `F_SETLKW`。第三个参数（我们称之为 `flockptr`）指向 `flock` 结构指针。

```c
struct flock {
    short l_type;   /* F_RDLCK, F_WRLCK, 或 F_UNLC */
    short l_whence; /* SEEK_SET, SEEK_CUR, 或 SEEK_END */
    off_t l_start;  /*相对于 l_whence 的字节偏移 */
    off_t l_len;    /* 字节长度；0 表示锁到文件尾 */
    pid_t l_pid;    /* 在 F_GETLK 时返回 */
};
```

该结构描述了：

- 区域类型：`F_RDLCK`（共享读锁）、`F_WRLCK`（斥写锁）或 `F_UNLC`（解锁区域）。
- 要锁或解锁区域的起始偏移量（`l_start` 和 `l_whence`）。
- 区域的字节大小（`l_len`）。
- 持锁并可能阻塞当前进程的进程 ID（`l_pid`），仅在 `F_GETLK` 时返回。

对于要锁或解锁区域的规范有许多规则适用：

- 指定区域起始偏移量的元素与 `lseek` 函数的最后两个参数（第 3.6 节）相似。事实上，`l_whence` 是 `SEEK_SET`、`SEEK_CUR` 或 `SEEK_END`。
- 锁可以从当前文件结束开始并扩展到之外，但不能在文件开始之前开始或扩展。
- 如果 `l_len` 为 0，则意味着锁延伸到文件可能的偏移量。这允许我们锁定文件中任何位置开始的区域，直到并包括任何追加到文件中的数据。（我们不需要尝试猜测文件中可能会追加多少字节）。
