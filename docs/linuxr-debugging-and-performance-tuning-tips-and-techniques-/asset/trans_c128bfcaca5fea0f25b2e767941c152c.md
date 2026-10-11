

```c
/* Evaluate EXPR, and repeat as long as it returns -1 with `errno'
   set to EINTR.    */

# define TEMP_FAILURE_RETRY(expression) \
  (__extension__ \
   { long int __result; \
     do __result = (long int) (expression); \
     while (__result == -1L && errno == EINTR); \
     __result; })
```

该宏使用 C 语言中的一项 GCC 扩展特性（通过 `__extension__` 关键字标记），该特性允许在括号内的花括号包裹语句中返回一个值，从而使其表现得像一个简单的表达式。

使用此宏，我们可以将 `safe_read()` 重写为如下形式：

```c
size_t safe_read(int fd, void const *buf, size_t count)
{
    ssize_t result;

    /* Limit count as per comment earlier. */
    if (count > INT_MAX)
        count = INT_MAX + 8191;

    result = TEMP_FAILURE_RETRY(read(fd, buf, count));

    return (size_t) result;
}
```

### 10.4.5 竞争条件与 `sig_atomic_t`（ISO C）

到目前为止，每次处理一个信号看起来很简单：在 `main()` 中安装一个信号处理程序，并（可选地）让该信号处理程序在开始执行时重新安装自身（或将动作设置为 `SIG_IGN`）。

但如果*两个*相同的信号紧随其后到来，会发生什么？具体来说，如果系统将信号的动作重置为默认值，而第二个信号在信号处理程序被调用*之后*但还未来得及重新安装自身*之前*到达，该怎么办？

或者，假设你使用的是 `bsd_signal()`，因此处理程序保持安装状态，但第二个信号与第一个不同？通常，第一个信号处理程序需要在第二个信号处理程序运行之前完成其工作，并且每个信号处理程序都不应该需要临时忽略所有其他可能的信号！

这两种情况都属于竞争条件。解决这些问题的一个变通方法是尽量简化信号处理程序。我们可以通过创建指示信号已发生的标志变量来实现这一点。信号处理程序将该变量设置为 true 并返回。然后，主逻辑在关键位置检查该标志变量：

```c
int sig_int_flag = 0;    /* signal handler sets to true */

void int_handler(int sigmun)
{
    sig_int_flag = 1;
}

int main(int argc, char *argv)
{
    bsd_signal(SIGINT, int_handler);
    ... program proceeds on ...
    if (sig_int_flag) {
        /* SIGINT occurred, handle it */
    }
    ... rest of logic ...
}
```

（请注意，此策略缩小了易受攻击的时间窗口，但并未消除该窗口。）

标准 C 引入了一种特殊类型——sig_atomic_t——用于此类标志变量。名称背后的理念是，对该类型变量的赋值是原子的：即它们在一个不可分割的操作中完成。例如，在大多数机器上，对 int 值的赋值是原子完成的，而结构体赋值通常是通过复制所有字节（使用编译器生成的循环）或发出可能被中断的“块移动”指令来完成的。由于对 sig_atomic_t 值的赋值是原子的，一旦开始，它会在另一个信号进来并中断之前完成。

拥有特殊类型只是故事的一部分。sig_atomic_t 变量也应声明为 volatile：

```c
volatile sig_atomic_t sig_int_flag = 0; /* signal handler sets to true */
... rest of code as before ...
```

volatile 关键字告知编译器该变量可能在编译器“背后”被外部更改。这防止编译器进行可能影响代码正确性的优化。

仅围绕 sig_atomic_t 变量构建应用程序是不可靠的。处理信号的正确方法将在稍后的第 10.7 节“用于进程间通信的信号”中展示，第 379 页。

### 10.4.6 额外注意事项

POSIX 标准为信号处理程序提供了若干注意事项：

- 当 `SIGFPE`、`SIGILL`、`SIGSEGV` 或任何代表“计算异常”的其他信号的处理程序返回时，行为是未定义的。
- 如果处理程序是因调用 `abort()`、`raise()` 或 `kill()` 而被调用的，则处理程序不能调用 `raise()`。`abort()` 在第 12.4 节“自杀行为：abort()”中有描述，第 445 页；`kill()` 稍后在本章中描述。（使用三参数信号处理程序的 `sigaction()` API，使判断此情况成为可能。）
- 信号处理程序只能调用表 10.2 中的函数。特别是，它们应避免使用 `<stdio.h>` 函数。问题在于，中断可能在 `<stdio.h>` 函数运行时到来，此时库的内部状态正处于更新过程中。进一步调用 `<stdio.h>` 函数可能会破坏内部状态。

表 10.2 中的列表来自 2001 年 POSIX 标准系统接口卷的第 2.4 节。其中许多函数是高级 API，在本卷中未在其他地方涵盖。

### 10.4.7 故事至今，第一幕

信号是一个复杂的话题，而且很快就会变得更加令人困惑。因此，让我们稍作停顿，退后一步，总结我们到目前为止讨论的内容：

- 信号表示某些外部事件已经发生。
- `raise()` 是用于向*当前进程*发送信号的 ISO C 函数。我们尚未描述如何向其他进程发送信号。
- `signal()` 控制信号的处理方式：即当信号到来时进程对该信号的反应。信号可以保持为系统默认值、被忽略或被捕获。
- 当信号被捕获时，会运行处理函数。复杂性开始在这里显现：
    - ISO C 未指定在运行处理程序之前是否将信号处理恢复为默认值，还是处理方式保持不变。前者是 V7 和现代 System V 系统（如 Solaris）的行为。后者是 BSD 的行为，也见于 GNU/Linux。（可以使用 POSIX bsd_signal() 函数来强制采用 BSD 行为。）
    - 系统调用被信号中断时发生什么，也沿传统 vs. BSD 这条线有所不同。传统系统返回 `-1` 并将 errno 设置为 EINTR。BSD 系统在处理程序返回后重启系统调用。GLIBC 的 TEMP_FAILURE_RETRY() 宏可以帮助你编写代码来处理返回 `-1` 且 errno 设置为 EINTR 的系统调用。

POSIX 要求部分完成的系统调用返回一个指示成功了多少的 success 值。尚未开始的系统调用会被重启。

- signal() 机制为竞争条件的滋生提供了肥沃的土壤。ISO C 的 sig_atomic_t 数据类型有助于这种情况，但并未解决它，且该机制按照定义无法变得对竞争条件安全。
- 适用许多额外的注意事项，特别是只有标准库函数的一个子集可以在信号处理程序内*安全*地调用。

尽管存在问题，但对于简单的程序，signal() 接口是足够的，并且它仍被广泛使用。

**10.5 System V Release 3 信号 API：sigset() 等**

4.0 BSD（约 1980 年）引入了额外的 API 以提供“可靠”信号。$^4$ 特别是，这使得阻止信号成为可能。换句话说，程序可以告诉内核，“暂时保留这些特定的信号，等到我准备好接收时再传递给我。” 一个主要优势是，此功能简化了信号处理程序，它们自动在自己的信号掩码（块）中运行（以避免连续两个信号的问题），可能还会阻止其他信号。

System V Release 3（约 1984 年）采用了这些 API 并使其普及；在大多数与 Unix 相关的文档和书籍中，你可能会看到这些 API 被称为来自 System V Release 3。这些函数如下：

**表 10.2**
可以在信号处理程序中调用的函数

| 函数 | 函数 | 函数 | 函数 |
| :------- | :------- | :------- | :------- |
| _Exit() | fpathconf() | raise() | sigqueue() |
| _exit() | fstat() | read() | sigset() |
| accept() | fsync() | readlink() | sigsuspend() |
| access() | ftruncate() | recv() | sleep() |
| aio_error() | futex() | recvfrom() | socket() |
| aio_return() | getegid() | recvmsg() | socketpair() |
| aio_suspend() | geteuid() | rename() | stat() |
| alarm() | getgid() | rmdir() | symlink() |
| bind() | getgroups() | select() | sysconf() |
| cfdgetispeed() | getpeername() | sem_post() | tcdrain() |
| cfdgetospeed() | getpgid() | send() | tcflow() |
| cfsetispeed() | getpid() | sendmsg() | tcflush() |
| cfsetospeed() | getppid() | sendto() | tcgetattr() |
| chdir() | getsid() | setgid() | tcsetpgrp() |
| chmod() | getsockname() | setpgid() | tcsendbreak() |
| chown() | getsockopt() | setpgrp() | tcsetattr() |
| clock_gettime() | getuid() | setsid() | tcsetattr() |
| close() | kill() | setsockopt() | tcsetpgrp() |
| connect() | link() | setuid() | time() |
| creat() | listen() | shutdown() | timer_getoverrun() |
| dup() | lseek() | sigaction() | timer_gettime() |
| dup2() | lstat() | sigaddset() | timer_settime() |
| execle() | mkfifo() | sigdelset() | times() |
| execve() | mkdir() | sigemptyset() | umask() |
| fchmod() | open() | sigfillset() | uname() |
| fchown() | pathconf() | sigismember() | unlink() |
| fcntl() | pause() | signal() | utime() |
| fdatasync() | pipe() | sigpause() | wait() |
| fork() | poll() | sigpending() | waitpid() |
| | posix_trace_event() | sigprocmask() | write() |

