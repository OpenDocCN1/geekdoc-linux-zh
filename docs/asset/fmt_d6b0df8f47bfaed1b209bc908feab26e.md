
```c
            if (bytesread <= 0)
                break;
            totalbytes += bytesread;
        }
    }
    return totalbytes;
}
```

程序 4.12 中的 `whichready` 函数存在问题，因为如果 `fd1` 和 `fd2` 都就绪，它总是选择 `fd1`。`copyfiles` 函数从 `fromfd1` 拷贝字节到 `tofd1`，从 `fromfd2` 拷贝到 `tofd2`，而无需对字节在两个方向上的可用性做任何假设。该函数返回错误或文件结束。

程序 4.13 中的 `copyfiles` 函数可以泛化为监控多个描述符的输入。命令处理器在监控来自不同客户端请求时可能会遇到此类问题。程序无法预测哪个源将产生输入，因此必须使用像 `select` 这样的方法。此外，监控的描述符集是动态的——程序必须从监控中移除某个源。

# 程序 4.15 waitfdtimed.c

一个等待给定时间以便从已打开的文件描述符获取输入数据的函数。

```c
#include <errno.h>
#include <string.h>
#include <sys/select.h>
#include <sys/time.h>
#include "restart.h"
#define MILLION 100000000L
#define D_MILLION 10000000.0
static int gettimedout(struct timeval end, struct timeval *timeout) {
    gettimeofday(timeout, NULL);
    timeout->tv_sec = end.tv_sec - timeout->tv_sec;
    timeout->tv_use = end.tv_use - timeout->tv_use;
    if (timeout->tv_sec >= MILLION) {
        timeout->tv_sec++;
        timeout->tv_use -= MILLION;
    }
    if (timeout->tv_use < 0) {
        timeout->tv_sec--;
        timeout->tv_use += MILLION;
    }
    if ((timeout->tv_sec == 0) && (timeout->tv_use == 0)) {
        errno = ETIMED;
        return -1;
    }
    return 0;
}
struct timeval addcurrenttime(double seconds) {
    struct timeval newtime;
    gettimeofday(&newtime, NULL);
    newtime.tv_sec += (int)seconds;
    newtime.tv_use += (int)((seconds)*D_MILLION + 0.5);
    if (newtime.tv_use >= MILLION) {
        newtime.tv_sec++;
        newtime.tv_use -= MILLION;
    }
    return newtime;
}
int waitfdtimed(int fd, struct timeval end) {
    struct fd_set readset;
    int retval;
    struct timeval timeout;
    if ((fd < 0) || (fd >= FD_SETSIZE)) {
        errno = EINVAL;
        return -1;
    }
    FD_ZERO(&readset);
    FD_SET(fd,&readset);
    if (gettimedout(end,&timeout) == -1)
        return -1;
    while ((retval) = select(fd + 1,&readset,NULL,NULL,&timeout)) == -1
    && (errno == EINTR)) {
        if (gettimedout(end,&timeout) == -1)
            return -1;
        FD_ZERO(&readset);
        FD_SET(fd,&readset);
    }
    if (retval == 0) {
        errno = ETIME;
        return -1;
    }
    if (retval == -1)
        return -1;
    return 0;
}
```

# 程序 4.16 readtimed.c

一个从打开的文件描述符进行定时读取的函数。

```c
#include <sys/time.h>
#include "restart.h"
size_t readtimed(int fd, void *buf, size_t nbyte, double seconds) {
    struct timeval timed;
    timed = addcurrenttime(seconds);
    if (waitfd(fd, &timed) == -1)
        return (size_t)(-1);
    return r_read(fd, buf, nbyte);
}
```

# 练习题 4.17

当从秒的小数部分设置 `time.tv_usec` 时，为什么有必要测试它是否大于或等于百万？该值等于百万会有什么后果？

答案：

由于该值被舍入到最近的微秒，像 `0.99999999` 这样的分数在乘以 `MILLION` 时可能会舍入为百万。当 `tv_usec` 字段不严格小于百万时，使用 `struct timeval` 值的函数操作是不指定的。

# 练习题 4.18

简化程序 4.15 的一种方法是每当 `select` 被信号中断时，都使用相同的超时时间重新启动。这样做有什么问题？

答案：

如果你的程序定期接收信号，且信号之间的时间间隔小于超时间隔，那么 `waitfdtimed` 永远不会超时。

POSIX 的 2000 版本引入了名为 `pselect` 的新版本 `select`。`pselect` 函数与 `select` 函数相同，但它使用更精确的超时结构 `struct timespec`，并允许在等待 I/O 可用期间阻塞或取消信号。`struct timespec` 结构在第 9.1.4 节中讨论。然而，在编写时（2003年3月），没有任何测试操作系统支持 `pselect`。

# 4.5 poll 函数

`poll` 函数与 `select` 类似，但它是按文件描述符而不是条件类型来组织信息的。因此，一个文件描述符的所有可能事件存储在 `struct pollfd` 中。相比之下，`select` 按事件类型组织信息，并为读、写和错误条件设有单独的掩码。`poll` 函数是 POSIX:XSI 的一部分，起源于 Unix System V。

`poll` 函数接受三个参数：`fds`、`nfds` 和 `timeout`。`fds` 是 `struct pollfd` 数组，代表文件描述符的监控信息。`nfds` 是要监控的描述符数量。`timeout` 是 `poll` 在返回之前应等待接收事件的时间（毫秒）。如果 `timeout` 值为 -1，则 `poll` 永远不会超时。如果整数是 32 位，最大超时时间约为 3 分钟。

### 概要

```c
#include <poll.h>
int poll(struct pollfd fds[], int nfds, int timeout);
```

> POSIX:XSI

`poll` 函数在超时时返回 0。如果成功，返回发生事件的描述符数量。如果失败，返回 -1 并设置 `errno`。下表列出了 `poll` 的强制错误。

| errno | 原因 |
| :--- | :--- |
| EAGAIN | 内部结构分配失败，但后续请求可能成功 |
| EINTR | poll 过程中捕获到信号 |
| EINVAL | nfds 大于 OPEN_MAX |

`struct pollfd` 结构包含以下成员：

```c
int fd; /* 文件描述符 */
short events; /* 请求的事件 */
short revents; /* 返回的事件 */
```

`fd` 是描述符编号，根据表 4.2 列出的事件通过逻辑或标志位构造 `revents`。

（注：OCR 文本存在大量重复和损坏，已根据提供的逻辑进行了重构。）

# 程序 4.17 monitorpoll.c

一个使用 `poll` 监控文件描述符数组的函数。

```c
#include <errno.h>
#include <poll.h>
#include <stdlib.h>
#include <unistd.h>
#include "restart.h"
#define BUFSIZE 1024
void doccommand(char *, int);
void monitorpoll(int fd[], int numfds) {
  char buf[BUFSIZE];
  int bytesread;
  int i;
  int numnow = 0;
  struct pollfd *pollfd;
  for (i=0; i < numfds; i++) {
    if (fd[i] >= 0)
      nnow++;
  }
  if ((pollfd = (struct pollfd *)calloc(numfds, sizeof(struct pollfd))) == NULL) {
    return;
  }
  for (i = 0; i < numfds; i++) {
    pollfd[i]->fd = fd[i];
    pollfd[i]->revents = 0;
  }
  while (nnow > 0) {
    nnow = poll(pollfd, numfds, -1);
    if (nnow == -1 && (errno == EINTR)) {
      continue;
    } else if (nnow == -1) {
      break;
    }
    for (i = 0; i < numfds && numnow > 0; i++) {
      if (pollfd[i]->revents & (POLLNORM | POLLIN)) {
        bytesread = r_read(fd[i], buf, BUFSIZE);
        nnow--;
        if (bytesread > 0)
          doccommand(buf, bytesread);
        else
          bytesread = -1;
      } else if (pollfd[i]->revents & (POLLERR | POLLHUP)) {
        bytesread = -1;
      } else {
        bytesread = 0;
      }
      if (bytesread == -1) {
        close(fd[i]);
        pollfd[i]->fd = -1;
        nnow--;
      }
    }
  }
  for (i = 0; i < numfds; i++) {
    if (fd[i] >= 0)
      close(fd[i]);
  }
  free(pollfd);
}
```

## 4.6 文件表示

在 C 程序中，文件通过文件指针或文件描述符进行指定。ISO C 的标准 I/O 库函数（`fopen`, `scanf`, `fprintf`, `read`, `write`, `fclose` 等）使用文件指针。UNIX I/O 函数（`open`, `read`, `write` 和 `ioctl`）使用文件描述符。文件指针和文件描述符提供了用于执行设备无关输入输出的逻辑标识。标准输入、标准输出和标准错误的符号名称分别为 `stdin`、`stdout` 和 `stderr`。这些符号名称定义在 `stdio.h` 中。标准输入、标准输出和标准错误的符号名称分别为 `STDIN_FILENO`、`STDOUT_FILENO` 和 `STDERR_FILENO`。这些符号名称定义在 `unistd.h` 中。

### 示例 4.19

解释库函数与系统调用之间的区别。

答案：

POSIX 标准并没有区分库函数和系统调用。传统上，库函数是存放在名为库的函数集合中的普通函数，通常是因为它们是有用的、被广泛使用的或规范的一部分（如 C 语言）。系统调用是向操作系统请求服务的行为。它涉及对操作系统的陷阱（trap）并通常涉及上下文切换。系统调用与特定的操作系统相关。许多库函数（如 `read` 和 `write`）实际上是系统调用的封装器。也就是说，它们将参数重新组织成适当的依赖系统的格式，然后调用底层的系统调用来执行实际操作。

尽管实现方式不同，但版本的 UNIX 在处理进程内的文件描述符和文件指针时遵循类似的实现。本节的剩余部分提供了文件描述符（UNIX I/O）和文件指针（ISO C）工作原理的示意模型。我们使用这种方法来解释重定向（第 4.7 节）和继承（第 4.6.3 节、6.2 节和第7 章）。

### 4.6.1 文件描述符

`open` 函数将文件或物理设备与程序中使用的逻辑句柄关联。文件或物理设备由字符字符串指定（例如 `/home/my.dat` 或 `/dev/tty`）。句柄是一个整数，可以被认为是一个特定进程的文件描述符表。它包含进程中每个打开文件的条目。文件描述符表是进程区域的一部分，但程序无法通过使用文件描述符的函数访问它。

### 示例 4.20

图 4.2 显示了程序执行后文件描述符表的示意图。

```
myfd = open("/home/ann/my.dat", O_RDONLY);
```

`open` 函数在文件描述符表中创建一个条目，该条目指向系统文件表中的一个条目。`open` 函数返回值 3，表示文件描述符条目位于进程文件描述符表的第三位置。

# 图 4.2 示例 4.20 代码执行后，类 UNIX 操作系统中文件描述符表、系统文件表和内存中 inode 表之间关系的示意图。

![](img/74e4d4cf6f07ca029fcde95b6b423fe7_155_0.png)

系统文件表每个由系统中的所有进程共享，每个活跃的打开文件都有一个条目。每个系统文件表条目包含文件偏移量、访问模式指示（即读、写或读写）以及指向它的文件描述符表条目数量计数。

多个系统文件表条目可能对应同一个物理文件。这些条目中的每一个都指向内存中 inode 表中的同一个条目。内存中 inode 表包含系统中每个活跃文件的条目。当程序打开一个当前未打开的特定物理文件时，调用会在该表中为该文件创建一个条目。图 4.2 显示文件 `/home/ann/my.dat` 在示例 4.20 代码执行之前已经被打开了，因为系统文件表中有两个指向 inode 表中条目的指针。（图中标记 B 标明了较早的指针。）

### 练习题 4.21

当显示图 4.2 所示的文件描述符表的进程执行 `close(myfd)` 函数时会发生什么？

答案：

操作系统删除文件描述符表中的第四个条目以及系统文件表中对应的条目。（更详细的讨论请参见第 4.6.3 节。）如果操作系统也删除了 inode 表条目，将导致系统文件表中留下悬空的指针 B。因此，inode 表必须包含一个指向它的系统文件条目的计数。当进程执行 `close` 函数时，操作系统会递减 inode 条目中的计数。如果 inode 条目为 0，操作系统将从内存中删除该 inode 条目。（考虑到短期内可能还会访问，操作系统可能不会立即删除该条目。）

### 练习题 4.22

系统文件表包含一个给出文件当前位置的偏移量。如果两个进程打开了同一个文件，每个进程都有自己的文件偏移量，并独立于另一个进程读取整个文件。如果进程打开同一个文件进行写入，会发生什么？如果文件偏移量存储在 inode 表中而不是系统文件表中，会发生什么？

答案：

写入操作是相互**的。由于每个进程都有单独的文件偏移量，每个用户都可以覆盖另一个用户写入的内容。另一方面，如果偏移量存储在 inode 表而不是系统文件表中，那么来自不同活跃打开的写入将是连续的。

### 练习题 4.23

假设一个进程打开一个文件进行读取并派生子进程。父子进程都可以读取该文件。这两个进程的读取之间有什么关系？写入呢？

答案：

子进程接收派生时父进程文件描述符表的副本。进程共享系统文件表条目，因此共享文件偏移量。这两个进程读取文件的不同部分。如果没有其他进程打开，写入将追加到文件末尾，写入数据不会丢失。4.6.3 节详细讨论了这种情况。

### 4.6.2 文件指针与缓冲

ISO 标准 I/O 库使用文件指针而不是文件描述符作为 I/O 句柄。文件指针指向进程区域中名为 `FILE` 的数据结构。

### 示例 4.24

以下代码段打开输出文件 `/home/ann/my.dat` 然后向文件写入一个字符串。

```
FILE *myfp;
```
