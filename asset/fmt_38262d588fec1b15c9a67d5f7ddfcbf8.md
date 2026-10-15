
3. 从消息等待队列中的第一条消息开始，调用 `testmsg()` 检查消息类型是否匹配所需类型。`sys_msgrcv()` 继续搜索，直到找到匹配的消息或整个等待队列遍历完毕。如果搜索模式为 `SEARCH_LESSEQUAL`，则搜索队列中类型小于或等于 `msgtype` 的第一个消息。

4. 如果找到消息，`sys_msgrcv()` 执行以下子步骤：

    1. 如果消息大小大于期望大小且 `msgflg` 指示不允许错误，则解锁全局消息队列自旋锁并返回 `E2BIG`。

    2. 将消息从消息等待队列中移除并更新消息队列统计信息。

    3. 唤醒所有在发送者等待队列上睡眠的任务。上一步中从队列中移除消息使得其中一个发送者有可能继续推进。进入最后一步。

5. 如果在消息等待队列中未找到符合接收者条件的消息，则检查 `msgflg`。如果设置了 `IPC_NOWAIT`，则解锁全局消息队列自旋锁并返回 `ENOMSG`。否则，按如下方式将接收者加入接收者等待队列：

    1. 分配一个 `msgr` 数据结构并将其添加到等待队列头部。

    2. 将 `msgr` 的 `r_task` 字段设置为当前任务。

    3. 将 `r_msgtype` 和 `r_mode` 字段分别初始化为期望的消息类型和模式。

    4. 如果 `msgflg` 指示 `MSG_NOERROR`，则将 `msgr` 的 `r_maxsize` 字段设置为 `msgsz` 的值；否则设置为 `INT_MAX`。

    5. 将 `r_msg` 字段初始化为指示尚未接收到任何消息。

    6. 初始化完成后，将接收任务的状态设置为 `TASK_INTERRUPTIBLE`，解锁全局消息队列自旋锁，并调用 `schedule()`。

    7. 接收者被唤醒后，检查 `msgr` 的 `r_msg` 字段。该字段用于存储流水线消息，或在发生错误时存储错误状态。如果 `r_msg` 字段包含所需消息，则进入最后一步。否则，重新锁定全局消息队列自旋锁。

7. 获取自旋锁后，重新检查 `r_msg` 字段，以确定在等待自旋锁期间是否已接收到消息。如果消息已接收，则执行最后一步。

8. 如果 `r_msg` 字段保持不变，则表示任务是被唤醒以重试。在这种情况下，将 `msgr` 出队。如果该任务有悬置的信号，则解锁全局消息队列自旋锁并返回 `EINTR`。否则，函数需要返回重试。

9. 如果 `r_msg` 字段显示在睡眠过程中发生了错误，则解锁全局消息队列自旋锁并返回该错误。

10. 在验证用户缓冲区 `msg` 的地址有效后，将消息类型加载到 `msg` 的 `mtype` 字段中，并调用 `store_msg()` 将消息内容复制到 `msg` 的 `mtext` 字段中。最后，由函数 `free_msg()` 释放该消息的内存。

#### 消息特定结构

消息队列的数据结构定义在 `msg.c` 中。

##### `struct msg_queue`

```c
/* one msg_queue structure for each present queue on the system */
struct msg_queue {
       struct kern_ipc_perm q_perm;
};
```

### Linux 内核 2.4 内部机制

##### `struct msg_queue`

```c
time_t q_ostime;		/* last msgsnd time */
time_t q_otime;		/* last msgcvt time */
time_t q_ctime;		/* last change time */
unsigned long q_cbytes;	/* current number of bytes on queue */
unsigned long q_gnum;		/* number of messages in queue */
unsigned long q_qbytes;	/* max number of bytes on queue */
pid_t q_lspid;		/* pid of last msgsnd */
pid_t q_lrpid;		/* last receive pid */

struct list_head q_messages;
struct list_head q_receivers;
struct list_head q_senders;
};
```

##### `struct msg_msg`

```c
/* one msg_msg structure for each message */
struct msg_msg {
	struct list_head m_list;
	long m_type;
	int m_ts;		/* message text size */
	struct msg_msgseg* next;
	/* the actual message follows immediately */
};
```

##### `struct msg_msgseg`

```c
/* message segment for each message */
struct msg_msgseg {
	struct msg_msgseg* next;
	/* the next part of the message follows immediately */
};
```

##### `struct msg_sender`

```c
/* one msg_sender for each sleeping sender */
struct msg_sender {
	struct list_head list;
	struct task_struct* tsk;
};
```

##### `struct msg_receiver`

```c
/* one msg_receiver structure for each sleeping receiver */
struct msg_receiver {
	struct list_head r_list;
	struct task_struct* r_tsk;
	int r_mode;
	long r_msgtype;
	long r_maxsize;
	struct msg_msg* volatile r_msg;
};
```

##### `struct msqid64_ds`

```c
struct msqid64_ds {
__kernel_ipc64_perm msg_perm;
__kernel_time_t msg_stime; /* last msgsnd time */
unsigned long __unused1;
__kernel_time_t msg_rtime; /* last msgrcv time */
unsigned long __unused2;
__kernel_time_t msg_ctime; /* last change time */
unsigned long __unused3;
unsigned long msg_cbytes; /* current number of bytes on queue */
unsigned long msg_qnum; /* number of messages in queue */
unsigned long msg_qbytes; /* max number of bytes on queue */
__kernel_pid_t msg_lspid; /* pid of last msgsnd */
__kernel_pid_t msg_lrpid; /* last receive pid */
unsigned long __unused4;
unsigned long __unused5;
};
```

##### `struct msqid_ds`
