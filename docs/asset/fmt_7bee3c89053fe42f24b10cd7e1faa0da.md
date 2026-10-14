
图 4.1 `wait_queue_t` 结构

**32–33** `WAIT_FLAG_EXCLUSIVE` 是目前定义的唯一标志。它决定了进程是排他地还是非排他地等待。当进程排他地等待时，只有它会被唤醒。所有在等待队列上非排他等待的进程将同时被唤醒（见 `_wake_up_common()`，第 4.7.3 节）。

**34** 这是一个指向代表等待进程的 `task_struct` 的指针。

**35** 这是链接字段，维护了这些结构的双向链表。

**36–39** 这些是调试字段，只有在定义了 `WAITQUEUE_DEBUG` 时才包含。它们的使用在后续章节中将会看到。

**41** 该结构在代码中被引用为 `wait_queue_t`。

#### 4.1.1.2 等待队列条目

为了允许多个进程等待同一个事件，使用了链式数据结构 `wait_queue`（见图 4.1，来自 `<linux/wait.h>`）。等待队列由结构体链表组成。

```c
struct __wait_queue {
    unsigned int flags;
    #define WAIT_FLAG_EXCLUSIVE 0x01
    struct task_struct* task;
    struct list_head task_list;
    #if WAITQUEUE_DEBUG
    long magic;
    long waker;
    #endif
};
typedef struct __wait_queue wait_queue_t;
```

图 4.1 `wait_queue_t` 结构

**32–33** `WAIT_FLAG_EXCLUSIVE` 是目前定义的唯一标志。它决定了进程是排他地还是非排他地等待。当进程排他地等待时，只有它会被唤醒。所有在等待队列上非排他等待的进程将同时被唤醒（见 `_wake_up_common()`，第 4.7.3 节）。

**34** 这是一个指向代表等待进程的 `task_struct` 的指针。

**35** 这是链接字段，维护了这些结构双向链表。

**36–39** 这些是调试字段，只有在定义了 `WAITQUEUE_DEBUG` 时才包含。它们的使用在后续章节中将会看到。

**41** 该结构在代码中被引用为 `wait_queue_t`。

或者不是。此外，`hlt_counter` 是一个标志位，指示当前是否允许停止 CPU。

- 82 禁用了可屏蔽中断，以便在下一行的测试可以在不受中断干扰的情况下安全地进行。这些中断将通过作为第 84 行调用的宏的一部分，或者在第 86 行重新启用。`_cli()` 宏只是汇编指令 `CLI` 的一个 C 语言封装器（见第 12.8.2 节）。
- 83 检查当前（空闲）进程的 `need_resched` 字段，因为在 `cpu_idle()` 中的测试与前一行禁用中断之间的微小时间窗口内，该字段可能已被中断处理程序设置过。
- 84 如果该字段未被设置，则启用中断并停止处理器，直到重置行被激活或请求了可屏蔽中断（有关此宏的描述，请参阅第 12.8.2 节）。
- 86 如果 `need_resched` 标志已被设置，则重新开启中断，并返回到 `cpu_idle()`（第 3.4.1 节）。这只是汇编指令 `STI` 的一个 C 语言封装器（见第 12.8.2 节）。

## 等待队列

由于某种原因，进程可能无法使用 CPU（中央处理单元），即使它是空闲的。通常情况下，这种状态下的进程正在等待某个事件。这可能是一个物理资源，如打印机或调制调器，也可能是在等待某个事件，例如按下键盘或等待从磁盘交付请求的数据。

在 Linux 中，等待的进程被保留在等待队列中，每个事件一个队列。例如，等待键盘输入的进程将通过代表键盘的数据结构中的一个指针进行链接。当按下按键时，中断处理程序会在等待队列中搜索适当的条目，然后将其从队列中移除。通过这一点，它找到代表等待进程的 `task_struct`，将其状态更改为 `TASK_RUNNING`，并将其移动到运行队列。

## 4.1 等待队列数据结构

这里使用了两种主要的数据结构：一个表示等待队列本身，另一个表示等待队列中的单个条目。还有许多宏用于检查这些结构中（可选的）调试字段。

### 4.1.1 声明和初始化等待队列条目

本节将检查表示等待队列中单个条目的数据结构，以及此类条目是如何声明和初始化的。在内核中，为等待队列创建新条目是非常频繁的事件，因此为此有很多宏和函数。一个用于声明新条目，另一个用于填充现有条目中的字段。

### 4.1.1.1 等待队列条目

为了允许多个进程等待同一个事件，使用了链式数据结构 `wait_queue`（见图 4.1，来自 `<linux/wait.h>`）。等待队列由一个结构体链表组成。

```c
struct __wait_queue {
    unsigned int flags;
    #define WAIT_FLAG_EXCLUSIVE 0x01
    struct task_struct* task;
    struct list_head task_list;
    #if WAITQUEUE_DEBUG
    long magic;
    long waker;
    #endif
};
typedef struct __wait_queue wait_queue_t;
```

图 4.1 `wait_queue_t` 结构

**32–33** `WAIT_FLAG_EXCLUSIVE` 是目前定义的唯一标志。它决定了进程是排他地还是非排他地等待。当进程排他地等待时，只有它会被唤醒。所有在等待队列上非排他等待的进程将同时被唤醒（见 `_wake_up_common()`，第 4.7.3 节）。

**34** 这是一个指向代表等待进程的 `task_struct` 的指针。

**35** 这是链接字段，维护了这些结构双向链表。

**36–39** 这些是调试字段，只有在定义了 `WAITQUEUE_DEBUG` 时才包含。它们的使用在后续章节中将会看到。

**41** 该结构在代码中被引用为 `wait_queue_t`。

## 等待队列数据结构

```c
#define __WAIT_QUEUE_HEAD_INITIALIZER(name) { \
    lock:           WAIT_QUEUE_RW_LOCK_UNLOCKED, \
    task_list:      {(name).task_list, \
                  &(name).task_list}, \
                 __WAIT_QUEUE_DEBUG_INIT(name)
} \
#define DECLARE_WAIT_QUEUE_HEAD(name) \
    wait_queue_head_t name = __WAIT_QUEUE_HEAD_INITIALIZER(name)
```

图 4 初始化等待队列头

147–150 此宏被传递给 `wait_queue_head_t` 并初始化为空状态。

148 锁列表被初始化为 `__WAIT_QUEUE_RW_LOCK_UNLOCKED`（见第 4.4 节等待锁）。

149 `task_list`（一个 `struct list_head`）的两个指针字段都被初始化为 `task_list` 字段本身，这是通过这些通用指针字段链接列表的标准做法。

150 可选的调试字段通过 `__WAIT_QUEUE_DEBUG_INIT()` 宏初始化（见第 4.1.3.1 节）。这些字段有两种形式，取决于是否开启调试。

152–153 此宏是等待队列的名称，它声明了一个名为 `name`、类型为 `wait_queue_head_t` 的变量，并通过调用第 147 行的 `__WAIT_QUEUE_INITIALIZER()` 进行初始化。

### 4.1.2.3 初始化现有等待队列

图 4.7 源自 `<linux/wait.h>` 的函数是一个现有 `wait_queue_head_t` 类型结构体的指针，并初始化为空状态。

```c
static inline void init_wait_queue_head(wait_queue_head_t *q) \
{
#if WAIT_QUEUE_DEBUG \
    if (!q) \
        WQ_BUG(); \
#endif \
```
