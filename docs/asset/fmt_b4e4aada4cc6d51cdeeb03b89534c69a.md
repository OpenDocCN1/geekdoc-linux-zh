
# select 与 pselect 系统调用

```c
select—wait for I/O to be ready

#include <sys/select.h>

int select(
    int nfds,              /* highest fd + 1 */
    fd_set *readset,       /* read set or NULL */
    fd_set *writeset,      /* write set or NULL */
    fd_set *errorset,      /* error set or NULL */
    struct timeval *timeout /* time-out (microseconds) or NULL */
);
/* Returns number of bits set or -1 on error (sets errno) */
```

```c
pselect—wait for I/O to be ready

#include <sys/select.h>

int pselect(
    int nfds,                       /* highest fd + 1 */
    int fd_set *readset,            /* read set or NULL */
    fd_set *writeset,               /* write set or NULL */
    fd_set *errorset,               /* error set or NULL */
    const struct timespec *timeout, /* time-out (nanoseconds) or NULL */
    const sigset_t *sigmask         /* signal mask */
);
/* Returns number of bits set or -1 on error (sets errno) */
```

与我们 `ready` 中传入文件描述符数组不同，使用 `select` 时，你需要为想要测试的每个文件描述符在其中一个 `fd_set` 参数中设置一位 [4]。有四个宏用于操作集合：

*   `FD_ZERO()`—清空整个 `fd_set`

    ```c
    #include <sys/select.h>
    void FD_ZERO(
        fd_set *fdset           /* 要清空的 fd_set */
    );
    ```

*   `FD_SET()`—设置 `fd_set` 中的文件描述符

    ```c
    #include <sys/select.h>
    void FD_SET(
        int fd,                 /* 要设置的文件描述符 */
        fd_set *fdset           /* fd_set */
    );
    ```

*   `FD_CLR()`—清除 `fd_set` 中的文件描述符

    ```c
    #include <sys/select.h>
    void FD_CLR(
        int fd,                 /* 要清除的文件描述符 */
        fd_set *fdset           /* fd_set */
    );
    ```

*   `FD_ISSET()`—测试 `fd_set` 中的文件描述符

    ```c
    #include <sys/select.h>
    int FD_ISSET(
        int fd,                 /* 要测试的文件描述符 */
        fd_set *fdset           /* fd_set */
    );
    /* 如果已设置则返回 1，如果未设置则返回 0（无错误返回） */
    ```

你可以使用 0、1、2 或 3 个集合来调用 `select()`，这取决于你感兴趣等待什么（读取、写入或错误）。如果所有 `fd_set` 参数都是 `NULL`，`select()` 只会阻塞，直到超时或被信号中断；这并没有特别大的用处。

你用 `FD_ZERO()` 初始化一个集合，然后使用 `FD_SET()` 为你感兴趣的每个文件描述符设置一位，如下所示：

```c
fd_set set;

FD_ZERO(&set);
FD_SET(fd1, &set);
FD_SET(fd2, &set);
```

然后你调用 `select()`，它会阻塞（即使设置了 `O_NONBLOCK`），直到一个或多个文件描述符准备好进行读取或写入，或者发生错误。它会修改你传入的集合，这次为每个已准备就绪的文件描述符设置一位，并且你必须测试每个文件描述符以查看其是否已设置，如下所示：

```c
if (FD_ISSET(fd1, &set)) {
    /* 根据所在的 fd_set 对 fd1 执行某些操作 */
}
```

没有方法直接获取文件描述符的列表；你必须分别询问每一个。你知道哪个文件描述符已准备好是因为你测试的是哪个集合。因此，你不能用同一个集合作为多个参数，即使输入的集合是相同的。你需要不同的输出集合来获取结果。

只有在输入时已设置的一位，在输出时才会被设置，即使对应的文件描述符已准备就绪。也就是说，你只能得到你所提问的答案。

成功时，`select()` 返回所有集合中已设置的位的总数，这是一个几乎无用的数字，除非用它来双重检查你通过调用（可能在循环中）`FD_ISSET()` 得到的文件描述符数量。

第一个参数 `nfds` 不是输入时已设置的位数。它是 `select()` 应该考虑的集合的长度。也就是说，对于每个输入集合，所有已设置的位必须都在编号从 0 到 `nfds` − 1（包含两端）的文件描述符范围内。通常，你计算最大的文件描述符编号并加 1。如果你不想这样做，可以使用常量 `FD_SETSIZE`，它是集合能拥有的最大文件描述符数量。但是，由于这个数字相当大（例如 1024），给 `select()` 传入实际数量通常要高效得多。

`select()` 的最后一个参数是一个超时区间，以 `timeval` 结构的形式表示，我们在第 1.7.1 节中解释过。如果在该时间区间内没有任何事情发生，`select()` 将返回 0 值——没有错误也没有位被设置。请注意，`select()` 可能会修改该结构，因此在再次调用 `select()` 之前请重置它。

如果 `timeout` 参数是 `NULL`，则没有超时；这相当于无限的时间区间。如果它不是 `NULL` 但时间为零，`select()` 会执行测试并立即返回；你可以用此进行轮询，而不是等待。如果你的应用程序有其他工作要做，这样做是有意义的：你可以在其他工作进行时偶尔进行轮询，因为你的应用程序正在有效地利用 CPU，然后在完成工作且除了等待外无事可做时切换到阻塞模式（非零时间或 `NULL` 超时参数）。

程序员使用 `select()` 时常见的错误有三种：

*   将第一个参数 `nfds` 设置为最大编号的文件描述符，而不是该编号加一。
*   再次调用 `select()` 时使用它刚刚修改过的相同集合，没有意识到返回时只有代表已准备就绪文件描述符的位被设置。你必须在每次调用前重新初始化输入集合。
*   没有意识到“就绪”的含义。它并不意味着数据已就绪，而是意味着一个未设置 `O_NONBLOCK` 的 `read()` 或 `write()` 不会阻塞。返回零计数（EOF）、错误或数据都是可能的。文件描述符是否设置了 `O_NONBLOCK`（意味着它将永远不会阻塞）无关紧要；`select()` 仅在假设 `O_NONBLOCK` 清除时不会阻塞的情况下才认为它已就绪。

现在这里是一个好得多的 `ready` 实现：

```c
int readany2(int fds[], int nfds, int *whichp)
{
    fd_set set_read;
    int i, maxfd = 0;
    unsigned char c;

    FD_ZERO(&set_read);
    for (i = 0; i < nfds; i++) {
        FD_SET(fds[i], &set_read);
        if (fds[i] > maxfd)
            maxfd = fds[i];
    }
    ec_neg1( select(maxfd + 1, &set_read, NULL, NULL, NULL) );
    for (i = 0; i < nfds; i++) {
        if (FD_ISSET(fds[i], &set_read)) {
            c = 0; /* 返回值为 EOF */
            ec_neg1( read(fds[i], &c, 1) );
            *whichp = i;
            return c;
        }
    }
    /* “不可能”到达这里 */
    errno = 0;
    EC_FAIL;
    EC_CLEANUP_BGN
        return -1;
    EC_CLEANUP_END
}
```

这个版本非常高效。读取操作保持阻塞状态，没有轮询循环，也没有休眠。所有的等待都在 `select()` 中，当它返回时，我们可以读取字符并立即将其返回。

如果有另一个线程可能正在读取与阻塞式读取相同的文件描述符，那么有可能在代码执行到读取之前，`select()` 说已就绪的数据就消失了，这可能意味着它将永远阻塞。修复此问题的最简单方法可能是让读取变为非阻塞，如果它返回 -1 且 `errno` 设置为 `EAGAIN`，则循环回到 `select()`。

担心向终端的写入会阻塞是不寻常的。即使发生这种情况（因为驱动器的缓冲区满了），它通常也会很快自行清除。通常，阻塞的写入对于其他输出（如管道或套接字）更为关键。我将在后续章节中讨论它们。特别是，第 8.1.3 节中有一个示例，以使用套接字接受来自多个客户端连接的方式来典型地使用 `select()`。

如果读取集合中设置了位，你就读取；如果写入集合中设置了位，你就写入。如果错误集合中设置了位，你要做什么？这取决于文件描述符打开的是什么。对于套接字，“错误”或许最好称为“异常条件”，这转化为带外数据已就绪（第 8.7 节）。对于终端（本章的主题），没有标准的异常或错误条件，尽管实现可能会有些非标准的东西，你需要查阅该系统的文档。

`select()` 有一个更复杂的变体，称为 `pselect()`；它与 `select()` 的区别在于：

*   对于 `pselect()`，超时是一个 `timespec` 结构，以纳秒为单位测量，并且它不会被修改。
*   有一个第六个参数，是一个要在调用 `pselect()` 期间设置的信号掩码（第 9.1.5 节），并在返回时恢复旧掩码。出于第 9 章中解释的原因，如果你期望它被信号中断，你应该使用 `pselect()` 而不是 `select()`。（如果 `sigmask` 参数是 `NULL`，`select()` 和 `pselect()` 在信号处理方面的行为完全相同。）

`pselect()` 是 SUS 版本 3 新增的，因此它刚刚开始出现，你的系统可能还没有它。

## 4.2.4 poll 系统调用

```c
poll—等待 I/O 就绪

#include <poll.h>

int poll( 
  struct pollfd fdinfo[], /* 要测试的文件描述符信息 */ 
  nfds_t nfds, /* fdinfo 数组中的元素数量 */ 
  int timeout /* 超时时间（毫秒） */ 
); 
/* 返回就绪的文件描述符数量，出错时返回 -1（设置 errno） */
```

```c
struct pollfd—poll 的结构体

struct pollfd { 
  int fd; /* 文件描述符 */ 
  short events; /* 事件标志（见下表） */ 
  short revents; /* 返回的事件标志（见下表） */ 
};
```

`poll` 最初是设计用于 AT&T System V（第 4.9 节）中的 STREAMS I/O 设施的，但和 `select` 一样，它也可以用于打开任何类型文件的文件描述符。尽管名为 `poll`，但和 `select` 一样，它既可用于等待，也可用于轮询。大多数系统都支持 `poll`，但 Darwin 6.6 是个例外。

在使用 `select` 时，你设置的是位掩码；而在使用 `poll` 时，你设置的是 `pollfd` 结构体，为你想要监控的每个文件描述符设置一个。对于每个文件描述符，你需要在 `events` 字段中设置标志，以监控每种事件（例如，读取、写入）。当 `poll` 返回时，每个结构体的 `revents` 字段中会设置相应的位，以指示发生了哪些事件。因此，与 `select` 不同，该调用不会干扰输入，你可以重复使用它们。

如果你正在尝试测试一个值非常大的文件描述符，`poll` 可能比 `select` 更高效。为了解释原因，假设你想测试文件描述符 1000。`select` 必须测试从 0 到 1000 的所有位，而你可以为 `poll` 构建一个仅包含一个元素的数组。`select` 的另一个问题是，集合的大小是根据潜在的文件描述符数量确定的，而某些内核被配置为允许非常大数量的文件描述符。拥有 10,000 位的位掩码非常低效。

`timeout` 参数以毫秒为单位，而不是像 `select` 和 `pselect` 那样使用 `timeval` 或 `timespec` 结构体。如果 `timeout` 为 –1，`poll` 将阻塞，直到列出的某个文件描述符上至少发生了一个请求的事件。如果为 0，与 `select` 和 `pselect` 一样，`poll` 仅测试文件描述符并返回，可能返回值为 0，这表示未发生任何事件。如果 `timeout` 为正数，`poll` 最多阻塞该时间段。（因此，与 `select` 和 `pselect` 一样，0 和正数的情况实际上是相同的。）

表 4.1 列出了 `poll` 的事件标志。要理解它们的含义，你需要知道 `poll` 区分“正常”数据、“优先级”数据和“高优先级”数据。这些术语的具体含义取决于文件描述符打开的对象。

| 表 4.1 poll 系统调用的事件标志 |
|---|---|
| 标志 | 含义 |
|---|---|
| `POLLRNORM` | 正常数据已准备好读取 |
| `POLLRDBAND` | 优先级数据已准备好读取 |
| `POLLIN`* | 等同于 `POLLRNORM` \| `POLLRDBAND` |
| `POLLPRI`* | 高优先级数据已准备好读取 |
| `POLLWRNORM` | 正常数据已准备好写入 |
| `POLLOUT`* | 等同于 `POLLWRNORM` |
| `POLLWRBAND` | 可以写入优先级数据 |
| `POLLERR`* | 发生 I/O 错误；仅在 `revents` 中设置（即不在输入中设置） |
| `POLLHUP`* | 设备断开连接（不再可写，但可能可读）；仅在 `revents` 中设置 |
| `POLLNVAL`* | 无效的文件描述符；仅在 `revents` 中设置 |

*   非 STREAMS 最常用的标志；`POLLPRI` 通常仅用于套接字。

除非处于特殊情况，否则你可以认为 `POLLIN` \| `POLLPRI` 等同于 `select` 的 read，`POLLOUT` \| `POLLWRBAND` 等同于 `select` 的 write。注意，使用 `poll` 时，你不需要专门询问异常情况——无论输入标志如何，如果表中最后三个标志适用，它们都会被设置。

如果你已经设置好了 `pollfd` 数组，但只是想禁用对某个文件描述符的检查，你可以将其 `fd` 字段设为 –1。

下面是使用 `poll` 实现的 `readany` 版本（来自第 4.2.2 节）。（第 4.2.3 节有一个使用 `select` 的版本。）

```c
#define MAXFDS 100

int readany3(int fds[], int nfds, int *whichp)
{
   struct pollfd fdinfo[MAXFDS] = { { 0 } };
   int i;
   unsigned char c;

   if (nfds > MAXFDS) {
      errno = E2BIG;
      EC_FAIL
   }
   for (i = 0; i < nfds; i++) {
      fdinfo[i].fd = fds[i];
      fdinfo[i].events = POLLIN | POLLPRI;
   }
   ec_negl( poll(fdinfo, nfds, –1) )
   for (i = 0; i < nfds; i++) {
      if ((fdinfo[i].revents & (POLLIN | POLLPRI))) {
         c = 0; /* EOF 的返回值 */
         ec_negl( read(fdinfo[i].fd, &c, 1) )
         *whichp = i;
         return c;
      }
   }
   /* *不可能* 到达这里 */
   errno = 0;
   EC_FAIL

   EC_CLEANUP_BGN
      return -1;
   EC_CLEANUP_END
}
```

### 关于 `readany3` 的评论：

*   将结构体初始化为全零是个好主意，这就是 `fdinfo` 数组声明中发生的事情，以防实现定义了我们要知道的额外字段。此外，如果我们需要使用调试器查看结构体，将未显式初始化的字段（例如 `revents`）设为零而不是垃圾值，会使显示更易于阅读。
*   我们的程序限制为最多 100 个文件描述符。将其改为动态分配数组将是一个简单的改进。
*   严格来说，对 `revents` 的测试假设 `flags` 使用不同的位，这在 SUS 中似乎没有明确说明，但对于 `poll` 来说这是一个安全的假设。
