

## Linux 内核 2.4 内部机制

### struct msg_queue

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

### struct msg_msg

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

### struct msg_msgseg

```c
/* message segment for each message */
struct msg_msgseg {
	struct msg_msgseg* next;
	/* the next part of the message follows immediately */
};
```

### struct msg_sender

```c
/* one msg_sender for each sleeping sender */
struct msg_sender {
	struct list_head list;
	struct task_struct* tsk;
};
```

### struct msg_receiver

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

### struct msqid64_ds

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

### struct msqid_ds

```c
struct msqid_ds {
struct ipc_perm msg_perm;
struct msg *msg_first; /* first message on queue,unused */
struct msg *msg_last; /* last message in queue,unused */
__kernel_time_t msg_stime; /* last msgsnd time */
__kernel_time_t msg_rtime; /* last msgrcv time */
__kernel_time_t msg_ctime; /* last change time */
unsigned long msg_lbytes; /* Reuse junk fields for 32 bit */
unsigned long msg_qbytes; /* dito */
unsigned short msg_cbytes; /* current number of bytes on queue */
unsigned short msg_qnum; /* number of messages in queue */
unsigned short msg_qbytes; /* max number of bytes on queue */
__kernel_ipc_pid_t msg_lspid; /* pid of last msgsnd */
__kernel_ipc_pid_t msg_lrpid; /* last receive pid */
};
```

### struct msg_setbuf

```c
struct msg_setbuf {
unsigned long qbytes;
uid_t uid;
gid_t gid;
};
```

### 消息支持函数

#### newque()

newque() 为新消息队列描述符（struct msg_queue）分配内存，然后调用 ipc_addid()，为新消息队列描述符保留一个消息队列数组条目。消息队列描述符的初始化如下：

- 初始化 `kern_ipc_perm` 结构。
- 消息队列描述符的 `q_cstime` 和 `q_rtime` 字段初始化为 0。`q_ctime` 字段设置为 CURRENT_TIME。
- 此队列消息允许的最大字节数（q_cbytes）设置为 MSGMNB，队列当前使用的字节数（q_cbytes）初始化为 0。
- 消息等待队列（q_messages）、接收方等待队列（q_receivers）和发送方等待队列（q_senders）均初始化为空。

在调用 ipc_addid() 之后的所有操作都在持有全局消息队列自旋锁的情况下执行。释放自旋锁后，newque() 调用 msg_buildid()，该函数直接映射到 ipc_buildid()。ipc_buildid() 使用消息队列描述符的索引创建一个唯一的消息队列 ID，然后将其返回给 newque() 的调用者。

#### freeque()

当消息队列即将被删除时，会调用 freeque() 函数。该函数假设调用函数已经锁定了全局消息队列自旋锁。它释放与该消息队列相关的所有内核资源。首先，它调用 ipc_rmid()（通过 msg_rmid()）从全局消息队列描述符数组中移除消息队列描述符。然后它调用 expunge_all() 唤醒所有接收者，并调用 ss_wakeup() 唤醒在此消息队列上睡眠的所有发送者。随后释放全局消息队列自旋锁。存储在此消息队列中的所有消息被释放，消息队列描述符的内存也被释放。

#### ss_wakeup()

ss_wakeup() 唤醒给定消息发送者等待队列中等待的所有任务。如果此函数由 freeque() 调用，则队列中的所有发送者都会出队。

#### ss_add()

ss_add() 接收一个消息队列描述符和一个消息发送者数据结构作为参数。它使用当前进程填充消息发送者数据结构中的任务字段，将当前进程的状态更改为 TASK_INTERRUPTIBLE，然后将消息发送者数据结构插入给定消息队列的发送者等待队列头部。

#### ss_del()

如果给定的消息发送者数据结构（`mss`）仍在相关的发送者等待队列中，则 `ss_del()` 将 `mss` 从队列中移除。

#### expunge_all()

`expunge_all()` 接收一个消息队列描述符（`msgq`）和一个整数值（`res`）作为参数，其中 `res` 指示唤醒接收者的原因。对于与 `msgq` 关联的每个睡眠接收者，`r_msg` 字段被设置为指示的唤醒原因（`res`），并唤醒相关的接收任务。当消息队列被移除或执行了消息控制操作时，会调用此函数。

#### load_msg()

当进程发送消息时，`sys_msgsnd()` 函数首先调用 `load_msg()` 函数将消息从用户空间加载到内核空间。消息在内核内存中表示为数据块的链表。与第一个数据块关联的是一个 `msg_msg` 结构，该结构描述了整体消息。与 `msg_msg` 结构关联的数据块大小限制为 `DATA_MSG_LEN`。数据块和结构在一个连续的内存块中分配，该内存块最大可以是一个内存页的大小。如果完整消息无法装入第一个数据块，则分配额外的数据块并将其组织成一个链表。这些额外的数据块大小限制为 `DATA_SEG_LEN`，并且每个都包含一个关联的 `msg_msgseg` 结构。`msg_msgseg` 结构和关联的数据块在一个连续的内存块中分配，该内存块最大可以是一个内存页的大小。此函数在成功时返回新 `msg_msg` 结构的地址。

#### store_msg()

`store_msg()` 函数由 `sys_msgrcv()` 调用，用于将接收到的消息重新组装到调用者提供的用户空间缓冲区中。`msg_msg` 结构以及任何 `msg_msgseg` 结构描述的数据被顺序复制到用户空间缓冲区。

#### free_msg()

`free_msg()` 函数释放消息数据结构 `msg_msg` 和消息段的内存。

#### convert_mode()

`convert_mode()` 由 `sys_msgrcv()` 调用。它接收指定消息类型（`msgtyp`）的地址和一个标志（`msgflg`）作为参数。它根据 `msgtyp` 和 `msgflg` 的值向调用者返回搜索模式。如果 `msgtyp` 为 null，则返回 `SEARCH_ANY`。如果 `msgtyp` 小于 0，则 `msgtyp` 被设置为其绝对值并返回 `SEARCH_LESSEQUAL`。如果 `msgflg` 中指定了 `MSG_EXCEPT`，则返回 `SEARCH_NOTEQUAL`。否则返回 `SEARCH_EQUAL`。

#### testmsg()

`testmsg()` 函数检查消息是否满足接收者指定的条件。如果以下任一条件为真，则返回 1：

