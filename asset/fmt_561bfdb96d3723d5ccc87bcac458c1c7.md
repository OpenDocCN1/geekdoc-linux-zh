
- 程序通过在传递给 `mq_notify()` 的 `sigevent` 结构的 `sigev_notify` 字段中指定 `SIGEV_THREAD` 来请求线程通知。线程的启动函数 `threadFunc()` 指定在 `sigev_notify` 字段中。①。

- 启用消息通知后，主程序无限暂停 ➁；定时通知通过在单独线程中调用 `threadFunc()` 传递 ③。

- 我们本可以将 `mqd` 设置为全局变量，使其在 `threadFunc()` 中可见。然而，我们采用了另一种方法来说明这种替代方案：我们将消息队列描述符的地址放在传递给 `mq_notify()` 的 `sigev_value.sival_ptr` 字段中 ④。当随后调用 `threadFunc()` 时，它作为参数传递。

我们必须将指向消息队列描述符的指针分配给 `sigev_value.sival_ptr`，而不是描述符本身的（某种转换版本），除了规定不是数组类型外，SUSv3 未对表示 `mqd_t` 数据类型的类型性质或大小提供保证。

# 52.7 Linux 特有功能

Linux 的 POSIX 消息队列实现提供了许多未标准但非常有用的功能。

## 通过命令行显示和删除消息队列对象

在第 51 章中，我们提到 POSIX IPC 对象被实现为虚拟文件系统中的文件，这些文件可以使用 `ls` 和 `rm` 进行列出和删除。为了对 POSIX 消息队列执行此操作，我们必须使用如下格式的命令来挂载消息队列文件系统：

```bash
# -t mqueue source target
```

源（source）可以是任何名称（通常指定字符串 `none`）。它的唯一意义是是它会出现在 `/proc/mqueue` 中，并被 `df` 命令显示。目标（target）是消息队列文件系统的挂载点。

接下来的 shell 会话显示了如何通过为文件系统创建一个挂载点来挂载消息队列文件系统并显示其内容。

```bash
$ su Privilege is required for mount
Password:
# mkdir /dev/mqueue
# mount -t mqueue none /dev/mqueue
$ exit Terminate root shell session
```

接下来，我们显示新挂载在 `/proc/mqueue` 中的记录，然后显示挂载目录的权限：

```bash
$ /proc/mqueue | grep mqueue
one /dev/mqueue mqueue rw 0 0
$ ls -ld /dev/mqueue
drwxrxr-x 2 root root 40 Jul 26 12:09 /dev/mqueue
```

从 `ls` 命令的输出中需要注意的一点是，消息队列文件系统在挂载时，自动设置了粘滞位（sticky bit）（我们从 `ls` 显示的其他执行权限字段中的 `t` 看到这一点）。这意味着非特权进程只能删除自己创建的消息队列。

接下来，我们创建一个消息队列，使用 `ls` 显示它在文件系统中可见的，然后删除该消息队列：

```bash
$ ./msg_created -c /newq
$ ls /dev/mqueue
newq
$ rm /dev/mqueue/newq
```

## 关于消息队列的信息

我们可以显示消息队列文件系统的内容。这些虚拟文件中的每一个都包含有关关联消息队列的信息：

```bash
$ ./msg_create -c /mq Create a queue
$ ./msg_send /mq abcdefg Write 7 bytes to the queue
$ cat /dev/mqueue/mq
QSIZE:7 NOTIFY:0 NOTIFY_PID:0
```

`QSIZE` 是队列中数据总字节数的计数。其余字段与消息通知有关。如果 `NOTIFY_PID` 不为零，则具有指定进程 ID 的进程已注册了该队列的消息通知，其余字段提供了有关通知类型的信息：

- `NOTIFY` 是一个对应于 `sig_notify` 常量之一的值：0 代表 `SIG_SIGNAL`，1 代表 `SIG_NONE`，或 2 代表 `SIG_THREAD`。

- 如果通知是 `SIG_SIGNAL`，则 `SIGNO` 字段表示用于消息通知的递送哪个信号。

接下来的 shell 会话阐明了这些字段中出现的信息：

```bash
$ ./mq_notify_sig /mq &
[1] 18158
$ cat /dev/mqueue/mq
QSIZE: NOTIFY:0 SIGNO:0 NOTIFY_PID:10158
$ kill 1
[1] Terminated ./mq_notify_sig /mq
$ ./mq_notify_thread /mq &
[2] 18160
$ cat /dev/mqueue/mq
QSIZE: NOTIFY:2 SIGNO:0 NOTIFY_PID:18160
```

使用 `SIGUSR1` (x86 上的信号 10)

## 使用备用 I/O 模型使用消息队列

在 Linux 系统中，消息队列描述符实际上是一个文件描述符。我们可以使用 I/O 多路复用系统调用（`select()` 和 `poll()`）或 `epoll` API 监控此文件描述符（有关这些 API 的更多细节请参见第 63 章）。这允许我们避免在尝试同时在消息队列和文件描述符上等待输入时遇到的遇到的困难（见第 46.9 节）。然而，此功能并非标准；SUSv3并不要求消息队列描述符必须实现为文件描述符。

## 消息队列限制

SUSv3 定义了 POSIX 消息队列的两个限制：

### `MQ_PRIO_MAX`

我们在第 52.5.1 节描述了此限制，它定义了消息的最大优先级。

### `MQ_OPEN_MAX`

实现可以定义此限制以指示一个进程可以打开的消息队列的最大数量。SUSv3 将此限制限制为至少 `POSIX_MQ_OPEN_MAX` (8)。Linux 没有定义此限制，因为 Linux 将消息队列描述符限制为文件描述符（第 52.7 节），适用的限制是适用于文件描述符和消息队列描述符总和的限制。（换句话说，每个进程和系统范围的文件描述符限制。）有关适用限制的更多细节，请参见第 36.3 节对 `RLIMIT_NOFILE` 资源限制的讨论。

除了 SUSv3 指定限制外，Linux 还提供了许多 `/proc` 文件用于查看和（在特权下）更改控制 POSIX 消息队列使用的限制。以下三个文件位于 `/proc/sys/fs/mqueue`:

（此限制规定了 `mq_max` 的上限。在 Linux 上，这是队列中可以存在的消息的最大数量。默认值为 10。）

52-6. 将列表 52-6 (`mq_notify_sig.c`) 中信号处理程序的使用替换为 `sigwaitinfo()` 的使用。从 `sigwaitinfo()` 返回后，显示返回的 `siginfo_t` 结构中的值。程序如何从 `sigwaitinfo()` 返回的 `siginfo_t` 结构中获取消息队列描述符？

52-7. 在列表 52-7 中，可以将 `buffer` 改为全局变量并仅分配一次内存（在主程序中）吗？解释你的答案。

# 53 POSIX semaphore

本章描述了 POSIX semaphore，它们允许进程和线程对共享资源的访问进行同步。在第 47 章中，我们描述了 System V semaphore，并假设读者熟悉该章节开头介绍的通用信号量概念和使用信号量的理由。在本章中，我们将对 POSIX semaphore 和 System V semaphore进行比较，以阐明这两个信号量 API 的相同与不同之处。

## 53.1 概述

SUSv3 规定了两种类型的 POSIX semaphore：

- 命名信号量（Named semaphores）：这种信号量有一个名称。通过使用相同的名称调用 `sem_open()`，不相关的进程可以访问同一个信号量。

- 无命名信号量（Unnamed semaphores）：这种信号量没有名称；相反，它位于内存中一个约定的位置。无命名信号量可以在进程之间或一组线程之间共享。当在进程之间共享时，信号量必须存在于一个（System V、POSIX 或 `mmap()`）共享内存区域。当在线程之间共享时，信号量可以存在于线程共享的内存区域中（例如在堆上或全局变量中）。

POSIX semaphore 的工作方式与 System V semaphore 类似，即 POSIX 信号量是一个整数，其值不允许低于 0。如果进程尝试将信号量的值减到 0 以下，那么根据所使用的函数，该调用要么阻塞，要么失败并返回一个错误，指示当前无法执行该操作。

某些系统没有提供 POSIX semaphore 的完整实现。一个典型的限制是仅支持无命名的线程共享信号量。Linux 2.4 的情况就是如此；有了 Linux 2.6 和提供了 NPTL 的 glibc，就可以获得 POSIX semaphore 的完整实现。
