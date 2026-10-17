
```c
struct cpufreq_governor {
    char name[CPUFREQ_NAME_LEN];
    int (*target)(struct cpufreq_policy *policy);
    unsigned int sampling_rate;
    struct device *dev;
    int (*_stopmethod)(void);
    int (*setpolicy)(struct cpufreq_policy *policy);
    unsigned int max_frequency;
    unsigned int next_frequency faster than this nano secs in we
    performance governor;
    struct list_head governor_list;
};
```

其中 `cpufreq_governor` 结构应该先填充，它的看起来如下：

```
// 两个者中都需要需要的 -
// 在两者中定义一个
// 如果可能，应该定义 -
// 可选 -
```

`init()` 函数指向初始化，该初始化将为每个 CPU 运行，并以 `cpufreq_policy` 结构作为参数。此函数可以激活 cpufreq 支持。

- `CPU_REQ_START`: 为此 CPU 开始。
- `CPU_REQ_STOP`: 为此 CPU 结束操作。

### 32.4. 调度器 (GOVERNORS)

填充 `cpufinfo.min_freq` 和 `cpufinfo.max_freq` 字段（单位为 kHz）、（在调度器之间切换所需）以及其他字段。

这里的主要字段是 CPU 编号、最小和最大频率、当前频率以及策略：

`verify()` 函数用于验证任何要设置的策略。它可以使用结构体表。

### 32.5 实验：CPU 通知器 (CPU Notifiers)

编写一个模块，为频率转换和策略链注册回调函数。打印出什么事件触发了回调，以及传递给回调函数的数据结构中的某些信息。你可以通过为 `/sys/devices/system/cpu/cpufreq` 选择值来测试这一点。更简单的是你可以添加调度器。

## 第 33 章 异步 I/O (ASYNCHRONOUS I/O)

### 33.1 什么是异步 I/O？

普通的 I/O 操作是同步执行的；应用程序将阻塞直到读取或写入完成（无论成功或失败）。注意，这并不意味着写入将缓冲到磁盘，或者与虚拟文件系统的交互已经完成。但如果 I/O 请求被队列起来，程序执行与 I/O 并行继续呢？这在 SMP 系统和使用不涉及 CPU 的 DMA 时特别有用。当完成这种情况时，被称为异步 I/O，或 AIO。此外，可以设置策略来决定请求是否序列化，特别是当它们引用同一个文件描述符时。在打开文件或使用 `mount` 命令时可以使用 `ASYNC` 标志请求异步 I/O，但这不会提供真正的异步 I/O。POSIX 标准定义了一个数据结构 `aioc` 作为 AIO 控制块，以及一组在其执行的基本函数。这些在 `<sys/aio.h>` 中定义并声明，并提供：

数据结构包括：

```c
struct aioc {
    int ai_fd;             /* 文件描述符 */
    int ai_aio;          /* 要执行的操作。 */
    struct aioc *ev;      /* 请求指针 */
    void *ai_buf;        /* 缓冲区位置。 */
    size_t ai_bytes;      /* 缓冲区长度。 */
    union sigevent sig;   /* 信号编号和值。 */
    off64_t ai_offset;     /* 文件偏移 */
};
```

其中我们有一个有效的文件描述符，但允许调用 `lseek()`。

`aio_fileno` 用于 `io_list()` 函数并存储要执行的操作类型。

`aio_req` 用于控制优先级。

`aio_buf` 指向要读取或写入数据的缓冲区。

`aio_event` 包含了操作完成时发送的信号。

`aio_offset` 给出了应执行 I/O 的文件偏移；这是必要的，因为并行执行 I/O 会违反当前位置的概念。

基本函数实际上不属于 glibc，而是属于另一个库 `librt`。这些函数是：

```c
#include <aio.h>
void aio_init(struct aioc *aio);
int io_read(struct aioc *cb);
```

典型的代码片段可能有

```c
struct aioc *cb = malloc(sizeof(struct aioc));
char *buf = malloc(bytes);
...
fd = open(filename, O_RDONLY);
cb->aio_fileno = fd;
cb->ai_bytes = bytes;
cb->ai_offset = offset;
cb->ai_buf = buf;
```

```c
rc = io_read(cb);
while (aio_error(cb) != EINPROGRESS) {
}
```

其中我们使用 `aio_error()` 函数调用直到控制块上的请求完成。

### 33.3 Linux 实现

Linux 的原始 AIO 实现是由 glibc 完全在用户空间完成的。为每个有挂起 AIO 请求的文件描述符都会启动一个线程。

这种方法是昂贵的，但如果有大量的请求，成千上万个；内核内部的支持可以带来更好的性能。glibc 完成实现的重要部分，但内核在内核中执行更高效。

2.6 内核对 AIO 有完全支持；事实上，所有的 I/O 都通过异步方法进行，如果没有设置标志，则为原生 I/O。

关于此实现的详细描述可以在此处找到：http://linuxsource.org/aio.html。

块设备和字符设备已经充分利用了异步实现。然而，驱动程序（通常需要异步）需要修改以利用这些新功能。这意味着在 `file_operations` 结构体中提供新函数：

```c
size_t (*aio_read(struct kioc *ioc, struct iovec *ev, unsigned long int loff_pos);
```

## 第 33 章 异步 I/O

### 33.3. LINUX 实现

```c
size_t (*aio_write)(struct kiocb *ioc, struct ioc_event *ioev, unsigned long len);
```

```c
int (*aio_fsync)(struct kiocb *ioc, int datasync);
```

由于这个 glibc 仍然没有充分利用 Linux 的全功能内核级 AIO（异步 I/O），因此，即使你在驱动程序中放置了条目，它们永远也不会被触发。（实际上，如果你在内核中同时有普通的读写条目和异步条目，如果你想测试它们，可以如下）：

然而，Linux 中提供了一个带有新系统调用的用户空间 API，可以被高效地使用；这并非不可实现。你必须使用安装的 `Libaio` 软件包，如果你想使用它编译代码，则需要安装 `libaio-dev` 软件包。你需要包含头文件 `<linux/libaio.h>`。基础函数有：

```c
#include <linux/libaio.h>
int aio_setup(long nr_events, struct ioc_ctx *ctx);
int aio_submit(struct ioc_ctx *ctx, long n, struct ioc_cb **ioccb);
int aio_get_events(struct ioc_ctx *ctx, long min_nr, long max_nr, struct ioc_event *events);
int aio_destroy(struct ioc_ctx *ctx);
int aio_cancel(struct ioc_ctx *ctx, struct ioc_b *ioc, struct ioc_event *event);
```

这些函数非常多，所以我们不再详细描述它们。

在进行任何 I/O 操作之前，必须设置一个队列调用所属的上下文（context），否则内核将不知道它们与谁关联。这是通过调用 `aio_setup()` 完成的，该上下文必须初始化，例如：

```c
struct ioc_ctx ctx;
long rc = aio_setup(maxevents, &ctx);
```
