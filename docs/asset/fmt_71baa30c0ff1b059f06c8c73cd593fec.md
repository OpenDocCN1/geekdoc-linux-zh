
程序可以通过从 0 循环到 `seminfo.semmni` 并使用 `SEM_STAT` 和计数器作为参数调用 `semctl()` 来提供所有数组的信息。`IPC_SET` 允许将信号量数组的所有者和模式设置为新值。此命令需要 `semid_ds` 结构作为参数，但实际上使用了 `sem_perm` 组件。如果调用者是数组的所有者或创建者，或者超级用户调用了 `semctl`，则 `IPC_RMID` 会删除信号量数组。`sys_semctl` 的其余命令列于表 5.8。

## 表 5.8 sys_semctl() 的命令。

| 命令 | 返回值和功能 |
|---|---|
| GETVAL | 信号量的值 |
| GETPID | 上一次修改信号量的进程进程号 |
| GETCNNNT | 等待信号量增加的进程数 |
| GETZCNT | 等待值为 0 的进程数 |
| GETALL | 数组中所有信号量的值，存储在 `semun.array` 字段中 |
| SETVAL | 设置信号量的值 |
| SETALL | 设置信号量的值 |

## 5.5.3 消息队列

消息由字节序列组成。此外，System V 中的 IPC 消息包含一个类型代码。进程向消息队列发送消息并可以接收消息，如果需要，可以将接收限制为指定类型的消息。消息按照它们进入消息队列的顺序被接收。LINUX 下的实现基础是 `msgid_ds` 结构。

```c
struct msgid_ds {
    struct ipc_perm msg_perm;      /* 访问权限 */
    struct msg *msg_first;         /* 队列中的第一个消息 */
    struct msg *msg_last;          /* 队列中的最后一个消息 */
    time_t msg_stime;              /* 上次结束的时间 */
    time_t msg_ctime;              /* 上次更改的时间 */
    struct wait_queue *qwait;      /* 等待队列的进程 */
    struct wait_queue *rwait;      /* 等待发送的进程 */
    short msg_cbytes;               /* 队列当前字节数 */
    short msg_qnum;                /* 队列中的消息数 */
    short msg_qbytes;              /* 队列字节数最大值 */
    short msg_lspid;               /* 上一次发送者的进程号 */
    short msg_lprid;               /* 上一次接收者的进程号 */
};
```

除了管理信息外，该结构还包含自己的两个队列：`wait` 和 `await`。如果队列已满，进程进入 `wait` 队列——即在不超出消息队列允许的最大字节数的情况下，无法再发送消息。队列包含了等待写入消息队列的消息。

消息队列实现为线性列表，其第一个元素由 `msg_first` 引用，最后一个元素由 `msg_last` 引用。`msg` 指针用于辅助执行发送操作：使用此指针，可以在队列中插入新消息，而无需扫描队列元素来找到最后一个。

消息存储在 `msg` 结构中。

```c
struct msg {
    struct msg *msg_next;          /* 队列中的下一条消息 */
    long msg_type;                 /* 消息类型 */
    char *msg_spot;                /* 消息文本地址 */
    time_t msg_time;               /* msgsnd 类型 */
    short msg_len;                 /* 消息长度 */
};
```

LINUX 将消息紧接在该结构之后存储，这意味着 `msg_spot` 指针不在不可预测的位置。

与信号量一样，现在需要用于初始化、发送和接收消息、返回信息以及释放消息队列函数。虽然执行的操作相对简单，但访问保护和统计数据的更新使得情况变得复杂。相关的库函数调用系统调用 `ipc`，该调用将请求传递给适当的内核函数。`sys_msgget` 函数使用 IPC 获取函数的标准参数创建消息队列。

```c
int sys_msgget(key_t key, int msgfig);
```

参数 `key` 是强制性键，`msgsbuf` 与 `setmsg` 中的标志位相同（见表 5.6）。使用 `sys_msgsnd()` 函数发送消息。

```c
struct msgsbuf {
    long mtype;                    /* 消息类型 */
    char mtext[1];                 /* 消息文本 */
};
```

```c
int sys_msgsnd(int mqid, struct msgsbuf *msgp, int msgsz, int msgfig);
```

参数 `msgsz` 是 `mtext` 中文本的长度，不能大于 `MSGMAX`。如果消息队列中的字节数超过 `msgmnb` 的值，进程将阻塞。可以通过设置 `IPC_NOWIT` 标志来防止这种情况。另一个操作消息队列的函数是 `sys_grcv()`。

```c
int sys_grcv(int mqid, char *msgp, int msgsz, long msgtyp);
```

要接收的消息在 `msgtyp` 中指定。如果 `msgtyp` 为零，则选择消息队列中的第一条消息。如果大于零，则读取该类型的第一个条消息。然而，如果设置了 `MSG_EXCEPT` 标志，则接收小于或等于 `msgtyp` 的类型的第一个消息。

该函数与 `sys_semctl()` 非常相似。

```c
int sys_msgctl(int nsqid, int cmd, struct msgid_ds *buf);
```

命令 `IPC_INFO` 输出 `msginfo` 结构中与消息队列相关的值的最大值。这些最大值列在表 5.9 中。与之前一样，LINUX 只使用这些值中的一部分。

每个组件的宏定义在 `msg.h` 中。`IPC_INFO` 命令是为 ics 程序设计的 `IPC_GET` 变体。它提供了 `msgpool` 中使用的等待队列数量、`msgmap` 中的消息数以及系统通过 `msgctl` 存储的消息总数。

`IPC_STAT` 将引用消息队列的 `msg_id` 复制到内存区域。类似于 `SEM_STAT`，`MSG_STAT` 允许将系统内部消息队列表的索引作为参数。这一 Linux 功能也被 ics 命令使用。

`IPC_SET` 允许修改消息队列的所有者、模式和可能的最大字节数。没有超级权限的进程不得将此值设置得高于 `MSGMNB` (16 384)。在该限制下，

## 表 5.9 msginfo 的组件。

| 组件 | 值 |
|---|---|
| msgmni | 128 | 消息队列最大数量 |
| msgmax | 4056 | 消息最大大小（字节） |
| msgmnb | 16 384 | 消息队列最大大小的标准值（字节） |
| msgmap | 16 384 | 忽略 - “消息表”中的条目数 |
| msgpool | 2048 | 忽略 - “消息池”的大小 |
| msgctl | 16 384 | 忽略 - “系统消息头”的数量 |
| msgszs | 16 | 忽略 - 消息段的大小 |
| msgseg | 0xffff | 忽略 - 最大段数 |

正常流程是，在将此值设置为高后，通过向队列发送消息来分配无法交换到次级存储器的内核内存。消息队列的所有者或创建者以及超级用户可以通过 `IPC_RMID` 删除队列。

在 Linux 2.0 下，消息队列承担与内核守护进程通信的任务。该守护进程负责自动加载内核例程通过消息请求的内核模块。

## 5.5.4 共享内存

共享内存是进程间通信最快的形式。使用共享区域的进程可以通过通常读写数据的机器指令来交换数据。在所有其他方法中，这只能通过递归系统调用将数据从一个进程的内存区域拷贝到另一个进程的内存区域。共享内存的缺点是进程需要使用额外的同步机制来确保不会发生竞态条件。只有通过增加编程努力才能实现更快的通信。通过其他系统调用执行同步可以实现可移植的实现，但会降低速度优势。另一种可能性是利用用于条件设置位值的机器码指令。由于这种操作发生在机器指令内部，因此操作无法被中断中断。这些指令为实现互斥系统提供了一种非常简单且快速的方法。第 4.2.2 节已经解释了内存区域的共享使用有多么复杂。自 2.0 版本以来，通过 `mmap()`，这种机制也可以用于实现共享内存应用程序。
