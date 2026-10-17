
这是信号量的置位操作（有时称为 'give'、'signal' 或 'V'）。它通常在任务离开临界区域时调用。信号量的值会加1 并进行测试。如果该值不是正数，则允许信号量等待队列中的第一个任务运行。`rt_sem_signal` 不阻塞调用者任务。

## 返回值

- 0 - 成功
- `SEM_ERR` - `sem` 指向一个无效信号量。

`int rt_sem_wait(SEM* sem);`

这是信号量的取信号操作（有时称为 'take'、'wait' 或 'P'）。它通常在任务进入临界区域时调用。信号量的值会减1 并进行测试。如果仍然是非负数，`rt_sem_wait` 将立即返回。否则，调用者任务被阻塞并入队。入队可能按优先级顺序或先入优先（FIFO）进行。当信号量被删除时，任何阻塞在该信号量上的任务都将允许运行。

### 用于嵌入式和实时应用的 Linux

`rt_mbx_receive_until` 等待直到一个绝对时间。

`rt_mbx_receive_timed` 等待多达 `delay` 内部计数次数。

## 返回值

- - >= 0 - 从邮箱箱接收到的字节数。
- -`EINVAL` - `mbx` 未指向有效的邮箱箱。

# 消息处理函数

这组函数实现了一种直接的任务到任务消息传递机制。

消息内容被限制为单个整数。

```
RT_TASK* rt_send (RT_TASK* task, unsigned int msg);
RT_TASK* rt_send_if (RT_TASK* task, unsigned int msg);
```

将消息 `msg` 发送给任务 `task`。`rt_send` 会阻塞调用任务，直到目标任务 `task` 接收到消息为止。如果有多个任务向该任务发送消息，它们将根据编译选项 `MSG_PRIORD` 按照优先级顺序或 FIFO（先先出）顺序队列。`rt_send_if` 不阻塞。

## 返回值

- - Success – `task`（指向接收消息任务的指针）
- 0 – `rt_send`: 任务在接收消息前被杀死。
  `rt_send_if`: 任务未准备好接收消息
- - `MSG_ERR` – 任务引用了无效的任务。

```
RT_TASK* rt_send_until (RT_TASK* task, unsigned int msg, RTIME time);
RT_TASK* rt_send_timed (RT_TASK* task, unsigned int msg, RTIME delay):
```

# RTAI 应用程序接口 (API)

`rt_send` 的定时版本。这些函数在指定的时间间隔过期后返回，无论 `msg` 是否成功发送。

## 返回值

- - Success – `task`（指向接收消息任务的指针）
- 0 – 操作超时。消息未送达。
- - `MSG_ERR` – 任务引用了无效的任务。

`RT_TASK* rt_receive (RT_TASK* task, unsigned int *msg);`

`RT_TASK* rt_receive_if (RT_TASK* task, unsigned int *msg);`

从指定的 `task` 处获取消息。如果 `task` 等于 0，则调用者接受来自任何任务的消息。如果有待处理的消息，`rt_receive` 将立即返回。否则，调用者任务将被阻塞并进入队列。（队列可能根据编译选项 `MSG_PRIORD` 按照优先级顺序或 FIFO 顺序进行。）`msg` 指向调用者提供的缓冲区。`rt_receive_if` 无论是否有待处理的消息都会立即返回。

## 返回值

- - Success – `task`（指向发送消息任务的指针）
- 0 – `rt_receive`: 任务在发送消息前被杀死。
  `rt_receive_if`: 没有发送任何消息。
- - `MSG_ERR` – 任务引用了无效的任务。

`RT_TASK* rt_receive_until (RT_TASK* task, unsigned int *msg, RTIME time);`

`RT_TASK* rt_receive_timed (RT_TASK* task, unsigned int *msg, RTIME delay);`

### 用于嵌入式和实时应用的 Linux

`rt_receive` 的定时版本。这些函数在指定的时间间隔过期后返回，无论 `msg` 是否被完全接收。

## 返回值

- * Success – `task`（指向接收消息任务的指针）
- * 0 – 操作超时。未接收到消息。
- * `MSG_ERR` – 任务引用了无效的任务。

# 远程过程调用 (RPC)

尽管这种机制被称为“消息过程调用”，但实际上它只是上述消息处理的全双工版本。

```
RT_TASK *rt_rpc (RT_TASK *task, unsigned int msg, unsigned int *reply);
RT_TASK *rt_rpc_if (RT_TASK *task, unsigned int msg, unsigned int *reply);
```

执行远程过程调用。RPC 类似于一对发送/接收操作。`rt_rpc` 将消息 `msg` 发送给任务，然后等待接收到回复。调用者任务始终会被阻塞并进入队列。（队列可能根据编译选项 `MSG_PRIORD` 按照优先级顺序或 FIFO 顺序进行。）接收者任务可以使用任何 `rt_receive_` 函数获取消息。它可以使用 `rt_return` 发送答案。`reply` 指向调用者提供的缓冲区。`rt_rpc_if` 不阻塞。

## 返回值

- * Success – `task`（指向接收消息任务的指针）
- * 0 – 任务未准备好接收消息（`rt_rpc_if`）或接收者任务在接收消息前被杀死。
- * `MSG_ERR` – 任务引用了无效的任务。

# RTAI 应用程序接口 (API)

`RT_TASK *rt_rpc_until (RT_TASK*task, unsigned int msg, unsigned int *reply, RTIME time);`

`RT_TASK *rt_rpc_timed (RT_TASK*task, unsigned int msg, unsigned int *reply, RTIME delay);`

`rt_rpc` 的定时版本。这些函数在指定的时间间隔过期后返回，无论 `msg` 是否成功发送。

## 返回值

- - Success – `task`（指向接收消息任务的指针）
- - 0 – 操作超时。消息未送达。
- - `MSG_ERR` – 任务引用了无效的任务。

`RT_TASK *rt_return (RT_TASK*task, unsigned int result);`

将结果传回任务。如果之前调用 `rt_rpc*` 的任务没有等待答案（即已杀死或超时），则此返回消息将被静静丢弃。

## 返回值

- - Success – `task`（指向接收消息任务的指针）
- - 0 – 消息未送达。
- - `MSG_ERR` – 任务引用了无效的任务。

`RT_TASK* rt_isrpc (RT_TASK *task);`

在接收消息后，任务可以通过调用 `rt_isrpc` 来确定是否在等待回复。

### 用于嵌入式和实时应用的 Linux

## 返回值

- * Success – 任务。
- * 0 – 消息由 `rt_send_*` 发送。
- * 非零 – 任务正在等待 `rt_return`。

# 模块 rtai_fifos

`#include <rtai_fifos.h>`

`rtai_fifos` 提供了实时任务之间的点对点通信机制。Linux 进程可以使用 `/dev/fifo<n>` 设备。

`int rtf_create (unsigned int fifo, int size);`

创建一个大小为 `size` 的实时缓冲区（fifo）。Linux 进程可以使用 `/dev/fifo<n>` 设备。

## 返回值

- - Success – `size`（即传递给 `rtf_create` 的参数）
- - `ENODEV` – 缓冲区无效。
- - `ENOMEM` – 无法分配内存。

`int rtf_destroy (unsigned int fifo);`

关闭之前通过 `rtf_create` 创建的实时缓冲区（fifo）。Linux 进程可以使用 `/dev/fifo<n>` 设备。

## 返回值

- - Success – 缓冲区打开的次数。
- - `ENODEV` – 缓冲区无效。
- - `EINVAL` – 缓冲区未打开。

`int rtf_reset (unsigned int fifo);`

移除缓冲区（fifo）中所有已发布但尚未被移除的数据。

## 返回值

- - Success – 0。
- - `ENODEV` – 缓冲区无效。
- - `EINVAL` – 缓冲区未打开。

`int rtf_resize (unsigned int fifo, int size);`
