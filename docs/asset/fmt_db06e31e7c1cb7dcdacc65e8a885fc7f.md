
- 代表调用 `msgget(2)` 系统调用的应用程序创建消息，始于对内核 `ipcget()` 例程的调用。每个消息队列标识符（`msgmni`）都会有一个 `ipc_perm` 结构可用。

- 一旦分配了结构，系统会根据调用进程的 UID 和 GID 以及调用代码传递的权限模式位初始化结构成员，然后设置 `IPC_ALLOC` 位以表示 `ipc_perm` 结构已被分配。`ipcget()` 代码与之前说明的相同——这是同一个函数！——所以我们这里不再赘述。如果 `ipcget()` 成功返回，应用程序代码就拥有了有效的消息队列标识符，可以发送和接收消息，并可以运行消息控制 `msgctl(2)` 操作。

消息发送 `msgsnd(2)` 调用要求应用程序构造一条消息，设置消息类型字段并创建消息正文（例如，文本消息）。

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

`msgrcv` 支持代码稍微不那么麻烦，因为现在我们是在队列中查找消息（而不是将消息放入队列）。内核不需要为 `msgrcv` 分配资源。接收消息的内核代码路径的常规流程涉及在遍历队列中所有消息时检查操作权限。

- 如果请求的消息类型与队列中的消息匹配，代码将消息类型复制到用户提供的位置，并将消息数据复制到用户提供的位置。

- 接下来，代码更新 `msqid_ds` 结构字段，从 `msg_cbytes` 中减去消息大小，在 `msg_lrpid` 中设置 PID，在 `msg_rtime` 中设置时间，释放消息资源，释放消息头（`msg` 结构），并释放资源映射条目。

- 如果代码遍历完所有消息后未找到匹配的类型，则返回“无消息”错误。

当该序列完成时，应用程序代码将在 `msgrcv(2)` 系统调用提供的缓冲区中获得消息类型和数据。

应用程序可使用的唯一剩余可调用例程是 `msgctl(2)` 系统调用。控制功能很直接；通常涉及检索或设置消息队列的 `ipc_perm` 结构中的值。

- 当使用 `IPC_RMID` 标志调用 `msgctl(2)` 时（表示调用者希望从系统中删除该消息队列），内核会遍历队列上的消息链表，释放与每条消息关联的内核资源。

- 内核会向在消息队列上睡眠的进程（线程）发送唤醒信号。这些进程最终会收到一个 `EIDRM` 错误（ID 已删除）。

- 系统只是将 `msqid_ds` 结构标记为可用，然后返回。

### 10.5 POSIX IPC

POSIX 标准及相关应用程序编程接口（API）的演进，产生了一套行业标准接口，它们提供与 System V IPC 相同类型的设施：共享内存、信号量和消息队列。它们在形式和功能上与 System V 对应设施非常相似，但在实现上却有很大不同。

所有三种 IPC 设施的 POSIX 实现都建立在 POSIX IPC 名称的概念之上，这些名称本质上看起来像文件名，但不一定是文件系统中的实际文件。这种 POSIX 名称约定提供了必要的抽象，即一个文件描述符，以便使用 Solaris 文件内存映射接口 `mmap(2)`，所有 POSIX IPC 机制都构建在该接口之上。这与 System V IPC 函数截然不同，后者需要键值来获取所需 IPC 资源的正确标识符。在 System V IPC 中，用于生成键值的常见方法是 `ftok(3C)`（文件到键）函数，它根据文件的路径名生成键值。POSIX 消除了键的使用，进程通过文件名约定来获取所需资源。

POSIX IPC 代码不需要（也没有可用的）内核可调参数。打开文件数量和内存地址空间的每进程限制是 POSIX IPC 中唯一潜在的限制因素。

表 10-8 列出了三种 IPC 设施的 POSIX API。

**表 10-8 _POSIX IPC 接口_**

| 信号量 | 消息队列 | 共享内存 |
|---|---|---|
| `sem_open` | `mq_open` | `shm_open` |
| `sem_close` | `mq_close` | `shm_unlink` |
| `sem_unlink` | `mq_unlink` |  |
| `sem_init` | `mq_getattr` |  |
| `sem_destroy` | `mq_setattr` |  |
| `sem_wait` | `mq_send` |  |
| `sem_trywait` | `mq_receive` |  |
| `sem_post` | `mq_notify` |  |
| `sem_getvalue` | `mq_getvalue` |  |

POSIX 接口在 Solaris 上构建和运行使用任何 POSIX IPC 设施的代码时，需要链接 `libposix4.so` 共享对象库。在 POSIX 库中，有几个由公共接口调用的通用例程，用于支持 POSIX IPC 对象名称约定。这些例程*不是*公共接口，*不得*由应用程序直接调用。

- `__pos4obj_open()`：打开/创建一个 POSIX 命名对象。如果在 `xxx_open(3R)` 调用中设置了 `O_CREAT` 标志，则在该文件不存在时创建它。如果同时设置了 `O_EXCL` 和 `O_CREAT`，则当对象名已存在时打开将失败。

- `__pos4obj_name()`：限定 POSIX 对象名的路径名。POSIX 标准要求传给 `xx_open(3R)` 例程的 name 参数以 `/`（斜杠）字符开头，并且路径名中不再有其他斜杠字符。该例程确保传入的参数符合规则，然后去除开头斜杠。它由 `__pos4obj_open()` 调用，并返回去除斜杠后的路径字符串给打开代码。
