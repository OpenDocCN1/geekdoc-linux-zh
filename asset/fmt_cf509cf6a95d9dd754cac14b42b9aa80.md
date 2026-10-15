
所有的 I/O 操作都是同步执行的；应用程序将阻塞，直到读取或写入完成，无论成功或失败。

注意，这并不意味着所有写入都会立即刷新磁盘，而只是与虚拟文件系统的交互已经完成。

但如果 I/O 请求可以被队列，并且程序执行与 I/O 请求的完成并行进行呢？这在 SMP 系统上以及使用 DMA（不涉及 CPU）时特别有用。当实现这一点时，它被称为异步 I/O，或 `AIO`。

为了让其能够正常工作，当 I/O 请求完成时必须有通知，并且代码中包含同步点或完成屏障。

此外，必须设置策略来决定队列请求是否被序列化，特别是当它们引用同一个文件描述符时。

你可以在打开文件时使用 `ASYNC` 标志来请求异步 I/O，或者在 `mount` 命令中使用 `-o async` 选项，但这并不会提供真正的异步 I/O。

# 30.2 Posix 异步 I/O API

POSIX 1.b 标准定义了一个基础数据结构 `aiocb`（AIO 控制块），以及一组可以在 `/usr/include/aio.h` 中执行的基础函数，这些函数由 `glibc` 提供。

数据结构如下：

```c
struct aiocb
{
    int aio_fildes;           /* 文件描述符。 */
    int aio_lio_opcode;      /* 要执行的操作。 */
    int aio_reprio;          /* 请求优先级偏移量。 */
    volatile *aio_buf;       /* 缓冲区位置。 */
    size_t aio_nbytes;       /* 传输长度。 */
    struct sigevent aio_sigevent;  /* 信号编号和值。 */
    __off64_t aio_offset;     /* 文件偏移量 */
};
```

此处我们省略了数据结构的其他成员。

`aio_fildes` 可以是任何文件描述符，但必须是有效的。

`aio_lio_opcode` 用于执行的操作。

`aio_reprio` 用于控制优先级。

`aio_buf` 指向缓冲区。

`aio_nbytes` 是传输长度。

`aio_sigevent` 控制在操作完成时发送的信号。

`aio_offset` 提供文件的偏移量。

这些基础函数并不是 `glibc` 的一部分，而是另一个库 `librt` 的。这些是：

```c
#include <aio.h>

void aio_init(struct aiocb);
int aio_read(struct aiocb);
int aio_write(struct aiocb);
int aio_error(struct aiocb);
size_t aio_return(struct aiocb);
int aio_fsync(struct aiocb);
int aio_cancel(int fd, struct aiocb);
```

# 30.3 Linux 实现

```c
struct aiocb *cb = malloc(sizeof(aiocb));
char *buf = malloc(nbytes);

fd = open(...);
cb->aio_fildes = fd;
cb->aio_nbytes = nbytes;
cb->aio_offset = offset;
cb->aio_buf = buf;

rc = aio_read(cb);

while (aio_error(cb) == EINPROGRESS) {
    // 等待
}
```

Linux 的原始 AIO 实现是由 `glibc` 完全在用户空间完成的。为每个待处理 AIO 请求的文件描述符启动了一个线程。

如果有大量此类请求，这种方法是昂贵的；内核内部真正的支持可以带来更好的性能。

2.6 内核包含了对 AIO 的支持；事实上，如果设置了某些标志，I/O 实际上是通过异步方法完成的

关于此实现的详细文档可以在 `http://ise.sourceforge.net/io/alionotes.txt`。

网络设备驱动已经充分利用了异步实现。然而，字符驱动（很少需要异步化）需要专门修改以利用这一新功能。这需要在 `file_operations` 跳表结构中提供新的函数：

```c
ssize_t (*aio_read) (struct kioc *iocb, struct iovec iov, unsigned long long,
	loff_t *pos);
ssize_t (*aio_write) (struct kioc *iocb, struct iovec iov, unsigned long long,
	loff_t *pos);
int (*aio_fsync) (struct kioc *iocb, int datasyncync);
```

因为 `glibc` 尚未利用 Linux 对 AIO 的完全支持。因此，即使你在驱动程序中放置了这些条目，永远永远被触发。（实际上，如果你没有普通的读写写条目，内核会调用异步接口，如果你想测试它们的话。）

然而，Linux 的新系统中有一个原生的用户空间 API 可以高效使用；这以前是不可能的。要使用它，你必须安装 `libaio-dev` 包，如果你想编译使用它的代码，需要安装 `libaio` 包。你的代码必须包含头文件 `/usr/include/libaio.h`。基础函数是：

```c
#include <libaio.h>
```

```c
io_setup (unsigned nr_events, aio_context_t ctx_id, struct iocb **iocbpp)
io_submit (aio_context_t ctx_id, long nr, struct iocb *iocb)
io_getevents (aio_context_t ctx_id, long min_nr, long nr, struct io_event *events, struct timespec *timeout);
io_destroy (aio_context_t ctx);
io_cancel (aio_context_t ctx_id, struct iocb *cb, struct io_event *result);
```

这些函数都有对应的 man 手页，我们不再对其进行完全描述。

在进行任何 I/O 工作之前，必须先设置一个上下文并包含之前的任何队列中的调用；否则内核可能不知道这些调用与谁关联。这是通过调用 `io_setup()` 来完成的，其中必须初始化上下文；例如：

```c
io_context_t ctx = 0;
rc = io_setup (maxevents, &ctx);
```

其中 `maxevents` 是可以接收的异步事件的最大数量。返回的句柄作为参数传递给其他函数。当你完成后，`io_destroy()` 函数将清除上下文。

`io_submit()` 函数用于提交异步请求，这些请求的 `iocb` 结构已经正确设置。

`io_getevents()` 函数用于检查状态，而 `io_cancel` 可用于尝试取消挂挂的请求。（注意：`events` 参数必须指向一个事件数组，其大小至少要等于你正在查找的最大事件数。文档对这一点说明得清楚，漏掉这一点是导致段错误的好方法。）

控制块结构本身如下：

```c
struct iocb {
void *data;      /* 在 io 完成事件中返回 */
unsigned key;   /* 用于标识请求 */

short	aio_list_opcode;
short	aio_reqrio;
aio_fildes;
int;

union {
struct io_iocb_common		c;
struct io_iocb_vector		v;
struct io_iocb_poll		poll;
struct io_iocb_sockaddr	saddr;
} u;
};

struct io_iocb_poll {
int events;
};		/* 结果码是结果标志的集合或负值 errno */

struct io_iocb_sockaddr {
struct sockaddr	*addr;
int		len;
};		/* 结果码是 sockaddr 的长度，或负值 errno */

struct io_iocb_common {
void *buf;
unsigned long nbytes;
long long      offset;
}; /* 结果码是读取的量或负值 errno */

struct io_iocb_vector {
    const struct iovec *vec;
    int                 nr;
    long long          offset;
}; /* 结果码是读取的量或负值 errno */
```
