
其中 `maxevents` 是可以创建的最大异步事件数量。返回的句柄随后作为其他函数的参数。当你完成后，`aio_destroy()` 将擦除该上下文。

`aio_submit()` 函数用于提交异步请求，这些请求有其相应的结构体。

`aio_get_events()` 函数用于检查状态，而 `aio_cancel()` 可用于取消挂起的请求。（`event` 参数指向一个结构数组，其大小至少等于你查看的最大事件数量。文档对此点的描述并不清晰，这是导致段错误（`segmentation faults`）的好方法。）

控制块通过以下方式初始化：

```c
struct ioc_b {
  void *data;           /* 在完成事件中返回 *
  unsigned long *ptr;  /* 用于标识请求 *
  short aio_lio_info;
  short aio_reqrio;     /* 两者均不是 *
```

```c
int aio_fildes;
```

```c
union {
  struct ioc_b_common  c;
  struct ioc_b_vector  v;
  struct ioc_b_poll   poll;
  struct ioc_b_sockaddr saddr;
} u;
```

```c
struct ioc_b_poll {
  int events;
  int code; /* code 是结果标志集或负 errno *"
```

虽然你可以通过这些函数和结构体来工作，但在提交请求之前在所有位置插入正确的值是非常繁琐的。内核中有许多辅助函数可以为你节省大量工作。遗憾的是，手册页（`man pages`）没有提到它们，特别是应该使用哪一个：

```c
void aio_prep_read(struct ioc_b *ioc, int fd, size_t count, long offset);
void aio_prep_write(struct ioc_b *ioc, int fd, size_t count, long offset);
```

在以显而的方式调用这些函数后，你只需调用 `aio_submit()` 来获取你的 I/O 请求。
最终，`glibc` 函数将完成必要的封装工作，以便允许使用 AIO API。到那时，如果需要可移植性，原生的 Linux 应用应该以一种直接的方式实现可移植性。

## 33.4 实验

### 实验 1：为字符驱动程序添加异步入口点

选取你之前编写的字符驱动程序之一，为 `aio_read()` 和 `aio_write()` 添加新的入口点。

为了测试这一点，你需要编写一个使用原生 Linux API 的用户空间程序。让它发送数量的写读请求并进行正确的同步。

我们还提供了一个使用 Posix API 的用户应用程序解决方案；注意，除非你注释掉内核中的普通读写入口点，否则它永远不会命中你的驱动（此时内核将回退到异步入口点）。

确保在链接正确库时进行编译；对于 Linux API 使用 `-laio`，对于 Posix API 使用 `-lrt`（在任何情况下你都可以使用两者，因为它们不会产生冲突）。

# 第 34 章

## I/O 调度

![](img/5f0cab84232061dba742ffc69894b1f1_186_0.png)

我们考虑 I/O 调度以及 Linux 使用的各种算法。

- 34.1 I/O 调度 . . . . . . . . . . . . . . . . . . . . . . 351
- 34.2 算法 . . . . . . . . . . . . . . . . . . . . . . 352
- 34.3 调度 . . . . . . . . . . . . . . . . . . . . . . 353
- 34.4 截止调度 . . . . . . . . . . . . . . . . . . . . . . 354
- 34.5 完全公平调度 . . . . . . . . . . . . . . . . 355
- 34.6 预期调度 . . . . . . . . . . . . . . . . . . . . . . 355
- 34.7 实验 . . . . . . . . . . . . . . . . . . . . . . 356

### 34.1 I/O 调度

我们考虑 I/O 调度以及 Linux 使用的各种算法。

I/O 调度提供了通用块层与低层驱动程序之间的接口。调度器负责在 I/O 请求提交到磁盘之前对其进行排序。任何调度算法都必须满足某些（有时是相互冲突的）需求：

- 硬件访问时间应被最小化，调度器根据策略将请求提交到磁盘。对于尽可能合并的请求，调度器是有效的。
- 对于设备，为每个请求维护一个队列，如果它可以与任何现有请求合并（在前或后）。如果请求没有合并，它将被放置在起始位置的队列中。
- 为了防止请求饥饿，算法截止时间（`deadline`）决定了 I/O 请求被新请求跳过的次数，阈值会促使请求被处理。
- 写操作可以利用低延迟；在某些情况下，确定性可能很重要。
- 调度器应该以公平的方式共享带宽；读操作几乎总是需要等待。
- 预期调度会导致更好的并行性和系统响应性。

具体的调度器名称各不相同，可以通过命令行进行选择：

```bash
/sys/block/<device>/queue/isched
```

例如，使用：`linux --elevator=[anticipatory|cfq|deadline|noop]`

```bash
$ ls -l /sys/block/sda/queue/isched
```

```
T-------root 4096 Mar 27 17:42 antic_expire
T-------root 4096 Mar 27 17:42 est_time
T-------root 4096 Mar 27 17:42 read_batch_expire
T-------root 4096 Mar 27 17:42 read_expire
T-------root 4096 Mar 27 17:42 write_batch_expire
T-------root 4096 Mar 27 17:42 write_expire
```
