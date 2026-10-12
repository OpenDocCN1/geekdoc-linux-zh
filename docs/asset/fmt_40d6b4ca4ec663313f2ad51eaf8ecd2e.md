
本教程将介绍允许你执行高级 I/O 的系统和技术。这将是《系统编程》系列中浏览最高的。文章中的大部分代码将用 `C` 语言编写，但你也会看到 `Go` 的示例。

请记住，高级文件 I/O 的概念和原理比标准 I/O 更复杂。有疑问时，请查看源码或尝试自己编写以解决任何歧义并让事情变得更清晰。

## 阻塞与非阻塞 I/O

存在两类系统：常见的系统，如 `read()` 和 `write()`，它们是可以阻塞的。

程序可以等待的另一个场景是输入。另一个领域是网络编程，它与文件 I/O 相关，因为当你的文件系统发生问题时，它最可能在网络相关问题上等待“未来”——那些记得过 `NFS` 相关问题的朋友会理解的！

教程文件可用：

`files.co.uk`

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
```

```c
int main(int argc, char const** argv) {
    char buf[20];
    int n = read(0, buf, 4);
    if(n > 0)
        printf("You typed: %s", buf);
    return 0;
}
```

### 一个简单的示例

让我们从一个简单的示例开始。`sample.c` 展示了一个由于下面的代码而可能被阻塞的文件 I/O 操作。上面的 `C` 代码将导致程序阻塞在如下位置：

```c
int n = read(0, buf, 4);
```

程序会等待用户输入——如果用户不按回车键，程序将永远等下去；这被认为不是良好的做法。尽管阻塞是由用户引起的，但它仍被视为阻塞。

如果你更改了代码，`diff` 工具的输出将不会被阻塞，并且始终会在完全完成其任务后退出。

```bash
$ gcc simpleNBc.c
fcntl(0, F_SETFL, O_NONBLOCK);
sleep(10);
```

如你所示，让 `sample.c` 以非阻塞方式运行的开销很小——如果你想在没有程序的情况下尝试，你可能需要编写更多但简单的代码，但 `simple.c` 不会阻塞你的系统。

### 一些实用的系统

这里介绍几乎的所有技术都可以通过某些系统调用来实现。这部分将介绍你需要注意的一些重要系统调用。你已经熟悉了 `fcntl()` 调用，它可以通用控制文件描述符，包括非阻塞 I/O。现在是时候解释以下：

```c
fcntl(0, F_SETFL, fcntl(0, F_GETFL) | O_NONBLOCK)
```

首先，应该明确 `F_SETFL`、`F_GETFL` 和 `O_NONBLOCK`。`F_GETFL` 命令告诉 `fcntl` 返回状态标志的当前值。返回的状态使得内部文件描述符处于状态标志，我们在现有的标志基础上添加 `O_NONBLOCK` 标志。`O_NONBLOCK` 标志允许将描述符设置为非阻塞模式，这是通过 `fcntl` 函数的参数指定的。正如你理解的，`F_SETFL` 命令需要三个参数，而 `fcntl(2)`

# 优衡利

高级文件 I/O 的概念和原理比标准 I/O 更复杂。有疑问时...

*(注：由于您提供的原始文本后半部分存在大量重复的段落和乱码，译文已剔除重复部分。)*

`timeval` 和 `timespec` 结构之间的区别在于前者使用秒和微秒，而后者使用秒和纳秒。如你所见，`timespec` 结构比 `timeval` 结构更精确。

下面的 `C` 代码是 `pollEx.c` 的一部分，它说明了 `poll()` 函数的使用：

这两个系统调用允许程序监控多个文件，并等待直到其中一个或多个文件可以进行某种 IO 操作。因此，程序不需要自己编写代码来识别每个文件描述符的状态。如果发生错误，该函数将返回 -1。

```c
retval = poll(fds, 1, 2500)
```

`poll` 系统调用类似于 `select()`，它等待多个文件事件。同样，`poll()` 系统调用等同于 `select()`。通常情况下，每当你需要清除或记住某个参数或整个调用的目的时，其 man 页（帮助手册）应该是你获取信息的首选地方。

`pollfd` 结构用于 `poll()` 保存文件描述符列表。它返回一个整数，出错时为 -1，或者返回准备好 IO 的描述符数量。第二个参数是超时时间。执行 `pollEx()` 会产生如下类的输出：

```
$ /pollEx
23
0: Input given
43
1: Input given
2: No input given
```

`select()` 和 `poll()` 都实现了一种异步通信模式，因为应用本身必须询问才能进行通信并处理数据。

## 两个简单的示例

现在是展示一些简单代码的时候。包含在 `select()` man 页中的代码是 `selectEx` 的一部分，展示了如何使用 `select()`：

```c
tv.tv_sec = 0;
tv.tv_usec = 0;
retval = select(1, &fds, NULL, NULL, &tv);
```

编译 `selectEx` 在不提供任何输入的情况下执行，会产生输出：

```
$ /selectEx
No data within seconds.
```

## 死锁检测器

你应该避免死锁。有时可能会出现问题，并发生意外的死锁。解决方案是防止死锁。`simple.c` 显示了一个可能发生死锁的情况，但这是由于用户没有按回车键。最罕见的死锁通常发生在进程 `A` 等待由进程 `B` 持有的资源时。

```c
#include <fcntl.h>
#include <errno.h>
#include <stdio.h>
#include <unistd.h>

int lockFile(int fd, int limit)
{
    int try = 0;
    struct lock;
    lock.l_type = F_WRLCK;
    lock.l_whence = 0;
    lock.l_start = 0;
    lock.l_len = 0;

    for (try = 0; try < limit; ++try)
    {
        if (0 == fcntl(fd, F_SETLCK, &lock))
            break;
        if ((errno != EAGAIN) && (errno != EACCES))
            break;
    }
}
```

![](img/453752f2a570e8fff106aca09a3ea2e3_42_0.png)

### 教程

## 系统编程

阅读各种异步 I/O 系统函数的描述是值得的。

2. `mtsouk@mail:~/docs/article/working/SPAdIO.LUD164/code (seh)`

`AIO_READ(3)` Linux 程序员手册 `AIO_READ(3)`

`NAME`

`aio_read` - 异步读取

`SYNOPSIS`

```c
#include <aio.h>

 aio_read(struct aiocb *aiocbp);

链接时使用 -lrt。
```

`DESCRIPTION`

`aio_read()` 函数将由 `aiocbp` 指定的缓冲区请求的 I/O 请求。该函数是 `read(2)` 的异步等效版本。调用的参数

```
read(fd, buf, count);
对应（按顺序）于 aiocbp 指向结构中的 `aio_fildes`、`aio_buf` 和 `aio_bytes` 字段。（`aiocb` 结构的描述请参见 aio(7)）。
```

数据从 `aiocbp->offset` 偏移量开始读取。

| `volatile aio_buf;` | / 缓冲区位置 * |
| :--- | :--- |
| `size_t` | / 传输长度 * |
| `int, aio_errno;` | / 请求优先级 * |
| `struct aio_sigevent;` | / 通知方法 * |
| `int, aio_lio_opcode;` | / 要执行的操作；仅限 lio_list1() * |

当 `B` 等待由进程 `A` 持有的资源时。当使用以下方式进行 `locking(fd)` 时，死锁文件（此处可能指代 `deadlock.c` 逻辑）使这种有效技术变得有效：

```c
fcntl(fd, F_SETLK, &lock)
```

当锁被成功锁定时，`lockFile()` 函数返回 0。执行 `deadlock.c` 将产生以下输出：

```
$ /deadlock_deadlock.c
File deadlock is successfully locked!
```

请注意，你需要复制 `deadlock.c` 并执行它。之所以这样做是因为你第一个实际上可以锁定该文件时：

```
$ /deadlock_deadlock.c
File deadlock cannot be locked!
```

务必阅读 `deadlock.c` 的源代码。
