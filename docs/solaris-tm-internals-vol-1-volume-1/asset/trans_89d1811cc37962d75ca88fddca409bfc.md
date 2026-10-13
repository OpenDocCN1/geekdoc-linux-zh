
描述每个消息队列的内核数据结构是 `msqid_ds` 结构。

```c
struct msqid_ds {
        struct ipc_perm msg_perm;        /* operation permission struct */
        struct msg *msg_first;            /* ptr to first message on q */
        struct msg *msg_last;             /* ptr to last one on q */
        ulong       msg_qbytes;           /* current # bytes on q */
        ulong       msg_qnum;             /* # of messages on q */
        ulong       msg_cbytes;           /* max # of bytes on q */
        pid_t       msg_lspid;            /* pid of last msgsnd */
        pid_t       msg_lrpid;            /* pid of last msgrcv */
        time_t      msg_stime;            /* last msgsnd time */
        long        msg_spad1;            /* reserved for time_t expansion */
        time_t      msg_rtime;            /* last msgrcv time */
        long        msg_spad2;            /* time_t expansion */
        time_t      msg_ctime;            /* last change time */
        long        msg_spad3;            /* time expansion */
        kcondvar_t  msg_cv;
        kcondvar_t  msg_qnum_cv;
        long        msg_pad[3];           /* reserve area */
};
```

**头文件** _<sys/msg.h>_

前面的结构字段描述基本不言自明。权限由创建消息队列的进程建立，并可通过 `msgctl(2)` 系统调用更改。内核指针 `msgque` 指向分配给保存所有系统 `msqid_ds` 结构的内核空间起始位置。它只是一个 `msqid_ds` 结构数组，`msgque` 指向数组中的第一个结构；数组中的结构总数等于可调参数 `msgmni`。每个结构大小为 112 字节。

消息队列中的消息以链表形式维护，链表的根位于 `msqid_ds` 数据结构中（`msg_first` 指针），指向消息的消息头。内核还维护一个消息头链表，其根为内核指针。

```c
struct msg {
        struct msg  *msg_next;     /* ptr to next message on q */
        long        msg_type;      /* message type */
        ushort_t    msg_ts;        /* message text size */
        short       msg_spot;       /* message text map address */
};
```

**头文件** _<sys/msg.h>_

内核消息结构（实际上，消息头结构是更准确的名称）大小为 12 字节，正如我们所说，每个消息队列上的每条消息都有这样一个结构（可调参数 `msgql`）。分配的最后一块内核内存用于消息队列同步锁。同步方法是由互斥锁保护的条件变量，定义在 `msglock` 结构中，为每个消息队列创建（每个消息队列标识符一个）。

条件变量是允许进程（线程）在互斥锁保护下测试特定条件是否为真的手段。互斥锁确保条件可以被原子地检查，并且在第一个线程测试条件时，没有其他线程可以改变该条件。线程将阻塞，持有互斥锁直到条件改变状态（变为真），此时线程可以继续执行。一个很好的例子是队列上的消息。如果不存在消息，线程在条件变量上阻塞（睡眠）。当消息出现在队列中时，系统发送广播，线程被唤醒，准备从队列中取出消息。

关于内核锁定的最后一点。所有版本的 Solaris，直到并包括 Solaris 2.5.1，在内核消息队列模块中执行非常粗粒度的锁定。具体来说，一个内核互斥锁被初始化以保护消息队列的内核代码和数据。因此，在多处理器平台上使用消息队列的应用程序不能很好地扩展。这种情况在 Solaris 2.6 中发生变化，它实现了更细粒度的锁定机制，允许更大的并发性。改进后的消息队列内核模块已被向后移植，并可作为 Solaris 2.5 和 2.5.1 的补丁使用。

图 10.2 说明了消息队列模块初始化完成后各部分的总体布局，以及上述内核指针。

![](img/220ae4af07df2fe8e5be69d27f885d1b_497_0.png)

## 图 10.2 *System V 消息队列结构*

## 10.4.2 消息队列的内核实现

我们将逐步介绍消息队列创建以及消息发送和接收所涉及的内核流程，因为这些代表了消息队列活动的大部分。

- 代表调用 `msgget(2)` 系统调用的应用程序创建消息，始于对内核 `ipcget()` 例程的调用。每个消息队列标识符（`msgmni`）都会有一个 `ipc_perm` 结构可用。
- 一旦分配了结构，系统会根据调用进程的 UID 和 GID 以及调用代码传递的权限模式位初始化结构成员，然后设置 IPC_ALLOC 位以表示 `ipc_perm` 结构已被分配。（`ipcget()` 代码与之前说明的相同——这是同一个函数！——所以我们这里不再赘述。）如果 `ipcget()` 成功返回，应用程序代码就拥有了有效的消息队列标识符，可以发送和接收消息，并可以运行消息控制（`msgctl(2)`）操作。

消息发送（`msgsnd(2)`）调用要求应用程序构造一条消息，设置消息类型字段并创建消息正文（例如，文本消息）。

- 当首次进入消息发送内核支持代码的代码路径时，代码会执行一些常规清理工作——例如递增处理器统计信息以宣布正在执行消息队列系统调用。`cpu_sysinfo` 结构维护一个 `msg` 计数器，反映已执行的消息队列系统调用总数。
- 代码验证调用进程对消息队列的访问权限，并根据可调参数 `msgmax` 检查消息大小。
- 接下来，代码将消息类型字段从用户地址空间复制到内核中的指定区域。

消息发送流程的其余部分最好用伪代码表示。

```
if (message queue no longer exists)
        return EIDRM error
if (current bytes on queue + bytes in new msg > msgmax)
        if (IPC_NOWAIT is set)
                return EAGAIN
        else
                set MSGWAIT flag in msqid_ds.msg_perm.mode
                call cv_wait_sig() /* put the caller to sleep until space is
                                      available on the queue */
/* on wakeup, code will read msqid_ds.msg_perm.mode to see
   set EIDRM if it's
   been removed */
        allocate space for message from resource map (msgmap)
        if (space not available)
                if (IPC_NOWAIT)
                        return EAGAIN error
                else
                        call cv_wait_sig() /* sleep waiting for space */
/* once the wakeup is issued, the necessary resources are
   available for putting the message on the queue */
        copy message data from user space to kernel space (map area)
        increment msqid_ds.msg_qnum
        msqid_ds.msg_cbytes += new message size
        msqid_ds.msg_lspid = PID of caller
        msqid_ds.msg_stime = current time

        update message header msg_type, msg_ts (text size) and msg_spot (map location pointer)
        adjust the queue pointers (msg_first, msg_next, msg_last)
return success to calling program
```

msgrcv 支持代码稍微不那么麻烦，因为现在我们是在队列中查找消息（而不是将消息放入队列）。内核不需要为 msgrcv 分配资源。接收消息的内核代码路径的常规流程涉及在遍历队列中所有消息时检查操作权限。

- 如果请求的消息类型与队列中的消息匹配，代码将消息类型复制到用户提供的位置，并将消息数据复制到用户提供的位置。
- 接下来，代码更新 msqid_ds 结构字段，从 msg_cbytes 中减去消息大小，在 msg_lrpid 中设置 PID，在 msg_rtime 中设置时间，释放消息资源，释放消息头（msg 结构），并释放资源映射条目。
- 如果代码遍历完所有消息后未找到匹配的类型，则返回“无消息”错误。

当该序列完成时，应用程序代码将在 `msgrcv(2)` 系统调用提供的缓冲区中获得消息类型和数据。

应用程序可使用的唯一剩余可调用例程是 `msgctl(2)` 系统调用。控制功能很直接；通常涉及检索或设置消息队列的 `ipc_perm` 结构中的值。

