
- 用户空间（Userspace）：频率可以由用户空间程序手动或动态地设置。
- 按需（Onemand）：频率根据 CPU 负载的策略进行动态调整。调度器能够快速切换频率。
- 保守（Conservative）：与按需类似，频率是逐渐增加或减少的，而不是一次性完成。这种模式更适用于笔记本电脑。

频率的变化通过通知器链广播，任何内核组件都可以注册回调函数，当这些事件发生时会被调用。

回调函数的第三个参数是一个指向类型为的数据结构的指针：

策略通知器链在设置策略时被调用。首先，它们带有事件 `CPUREQ_ADJUST` 被调用，如果我们需要，它可以限制频率，例如，为了避免空闲时出现过热问题。

Linux 中的频率缩放是一个适用于所有架构的统一框架，在实现新策略方面非常模块化。

第二个事件是当设置值 `CPUREQ_COMPATIBLE` 时。更改应只在应用策略之前进行。

第三个事件是设置 `CPUREQ_COMPATIBLE` 时（此处原文可能有误）。

## 第 32 章：CPU 频率缩放

### 32.4 调度器 (Governors)

性能（Performance）和节电（Powersave）调度器是 Linux 内核内置的，分别将频率设置为最高或最低可能。

更多的调度器可用，并且可以通过或不通过内核模块添加。

你必须向调度器注册：

```c
#include <cpufreq.h>
```

```c
int cpufreq_register_driver (struct cpufreq_driver *data);
int cpufreq_unregister_driver (struct cpufreq_driver *data);
```

其中 `cpufreq` 结构应该填充的内容：

# 第 33 章

## 异步 I/O

此 CPU 的最大和最小限制已经更改。

回调函数可以使用以下方式调用 CPU 频率驱动程序：

```c
int cpufreq_driver_target(struct cpufreq_policy, unsigned int target_freq,
                   unsigned int relation);
```

其中 `relation` 可以是 `CPUFREQ_REL_L`（尝试选择一个大于等于目标频率的新频率）或 `CPUFREQ_REL_B`（尝试选择一个小于等于当前频率的新频率）。

### 32.5 实验室

#### 实验 1：CPU 频率通知器

编写一个模块，为 CPU 频率转换和策略通知器链注册回调函数。

打印出什么事件触发了回调，以及传递给回调函数的数据结构中的某些信息。

你可以通过为 `/sys/devices/system/cpu/cpu0/cpufreq` 中的某些条目选择值来测试。更简单的是，你可以将“CPU 频率监控器”应用程序添加到任务栏，并轻松地切换调度器（governors）和频率。

![](img/4e539a55ab31f2c9df39e648783d8023_184_0.png)

我们将讨论异步 I/O、其功能接口以及在 Linux 下实现方法。

- 33.1 什么是异步 I/O? . . . 345
- 33.2 Posix 异步 I/O API . . . 346
- 33.3 Linux 实现 . . . 347
- 33.4 实验室 . . . . 348

## 33.1 什么是异步 I/O？

所有的普通 I/O 操作都是同步执行的；应用程序将阻塞，直到读取或写入完成（无论成功还是失败）。

注意，这并不意味着所有的写入都会立即刷新到磁盘，只有在与虚拟文件系统的交互完成后才会如此。

但如果 I/O 请求被队列化，并且程序执行与 I/O 请求的完成并行进行呢？这在 SMP（对称多处理）系统和使用 DMA（不涉及 CPU）时特别有用。当实现这一点时，被称为异步 I/O，或 AIO。

# 第 33 章：异步 I/O

## 33. LINUX 实现

为了使其正常工作，当 I/O 请求完成时必须有通知，并且必须维护同步点或完成处理程序。

```c
int io_read(struct aioc *cb);
int io_list(int mode, struct aioc *cblist, int n, struct event *sig);
int io_error(const struct aioc *cb);
time_t io_return(const struct aioc *cb);
int io_pread(int fd, struct aioc *cb);
int io_suspended(const struct aioc *cb, struct cblist, int n);
int io_canceled(int fd, struct aioc *cb);
```

此外，可以设置策略来决定队列请求是否序列化，特别是当它们引用同一个文件描述符时。

你可以在打开文件时使用 `ASYNC` 标志请求异步 I/O，或者在 `mount` 命令中使用 `-async` 选项，但这并不会提供真正的异步 I/O。

## 33.2 Posix 异步 I/O API

POSIX 标准定义了一个数据结构 `aioc`，作为 AIO 控制块，以及一组可以在其上执行的基础函数。这些函数在 `/include/aio.h` 中定义并给出原型，并提供了：

数据结构包括：

```c
struct aioc
{
    int aio_fd;        /* 文件描述符。 */
    int aio_lio;      /* 要执行的操作。 */
    void *aio_buf;     /* 缓冲区位置。 */
    size_t aio_bytes; /* 传输长度 */
    struct sigevent aio_sig; /* 信号和值。 */
    off_t aio_offset; /* 文件偏移量 */
};
```

其中我们列出的是数据的有效文件描述符（但必须使用 `lseek()` 用的名称）。

`aio_lio` 被 `io_list()` 函数使用，并存储要执行的操作类型。

`aio_reqrio` 用于控制调度优先级。

`aio_buf` 指向要从中读取或写入写入数据的缓冲区。

`aio_event` 包含在操作发生时是否向内核发送了信号。

`aio_offset` 给出了应执行 I/O 的文件偏移量；这是必要的，因为 I/O 操作是相对于当前进程的视图并行执行的。

基础函数实际上不是 `glibc` 的一部分，而是另一个库 `librt` 的部分。这些函数是：

```c
#include <aio.h>
void aio_init(struct aioc *aio);
int aio_read(struct aioc *cb);
```

一个典型的代码片段可能：

```c
struct aioc *cb = malloc(sizeof(struct aioc));
char *buf = malloc(bytes);
fd = open("", ...);
cb->aio_fd = fd;
cb->aio_bytes = bytes;
cb->aio_offset = offset;
cb->aio_buf = buf;
rc = aio_read(cb);
while (aio_error(cb) == EINPROGRESS) {
```

其中我们使用 `aio_error()` 函数调用来等待控制块上请求的完成

## 33.3 Linux 的实现

Linux 原始 AIO 实现是由 glibc 在用户空间完成的。对于每个挂起 AIO 的文件描述符，都会启动一个线程。然而，如果有成千上万个请求，这种方法的成本将很高；glibc 执行了部分实现，其他部分在内核中更高效地执行。2.6 内核对 AIO 有完全支持：事实上，I/O 是通过异步方法完成的，如果没有设置标志，则产生普通 I/O 结果。关于此实现的详细描述可以查阅：http://www.kernel.org/aio

阻塞和选择驱动程序已经利用了这种实现。驱动程序（通常需要异步）需要修改以利用这一点。这意味着在文件操作中有了新函数：

```c
size_t (*aio_read)(struct aioc *ioc, struct iovec *io, unsigned long long, loff_t *pos);
size_t (*aio_write)(struct aioc *ioc, struct iovec *io, unsigned long long);
int (*aio_fsync)(struct aioc *ioc, int datasync);
```
