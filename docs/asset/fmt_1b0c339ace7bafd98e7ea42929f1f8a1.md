
#include <stdlib.h>

#include <sys/stat.h>

#include <unistd.h>

```c
#include <linux/stat.h>
```

```c
#define FIFO_FILE "MYFIFO"

int main(void) {
    FILE *fp;
    char readbuf[80];
    /* 如果 FIFO 不存在则创建它 */
    umask(0);
    mkod(FIFO_FILE, S_IFIFO|0666, 0);
    while(1) {
        fp = fopen(FIFO_FILE, 'r');
        fgets(readbuf, 80, fp);
        printf("Received string: %s\n", readbuf);
        fclose(fp);
    }
    return(0);
}
```

由于 FIFO 默认是阻塞的，请在编译后在后台运行服务器：
- `$ fifoserver&`

我们将稍后讨论 FIFO 的阻塞行为。首先，考虑以下我们服务器的简单客户端前端：

********************************************************************
节选自《Linux 程序员指南 - 第6章》
(C)opy 1994-1995, Scott Burkett
********************************************************************
MODULE: fifocient.c
********************************************************************/

```c
#include <stdio.h>
#include <stdlib.h>
#define FIFO_FILE "MYFIFO"
int main(int argc, char *argv[]) {
    FILE *fp;
    if ( argc != 2) {
        printf("USAGE: fifocient [string]\n");
        exit(1);
    }
```

## 2.4 System V IPC

```c
if((fp = fopen(FIFO_FILE, "w")) == NULL) {
    perror("fopen");
    exit(1);
}
fputs(argv[1], fp);
fclose(fp);
return(0);
}
```

### 2.3.4 FIFO 上的阻塞行为

通常，FIFO 会发生阻塞。换句话说，如果 FIFO 以读取模式打开，进程将一直“阻塞”，直到有其他进程对其进行写入。这种行为同样反。如果这种行为不可接受，可以在 `open()` 中使用 `_NONBLOCK` 标志 来禁用默认的阻塞行为。

在我们简单的服务器案例中，我们只是把它推到了后台，让它在那里阻塞。另一种方法是跳转到另一个虚拟控制台并运行客户端，通过切换查看产生的结果。

### 2.3.5 著名的 SIGPIPE 信号

最后一点，必须有一个读取者和一个写入者。如果进程尝试向一个没有读取者的管道写入数据，内核将发送 `SIGPIPE` 信号。这在管道涉及两个以上进程时至关重要。

# System V IPC

## 2.4.1 ipc 命令

`ipc` 命令可用于从内核中移除 IPC 对象。虽然可以通过代码中的系统调用移除 IPC 对象（我们稍后会看到方法），但在许多情况下，特别是开发环境中，往往需要手动移除 IPC 对象。其用法如下：

```
ipcrm <msg | sem | shm> <IPC ID>
```

只需指定要删除的对象是消息队列 (`msg`)、信号量集 (`sem`) 还是共享内存段 (`shm`) 即可。IPC ID 可以通过 `ipc` 命令获取。你必须指定对象的类型，标识符在相同类型中是唯一的（回想我们之前对此的讨论）。

## 2.4.2 消息队列

### 2.4.2.1 基本概念

消息队列可以最好地描述为内核地址空间内部的一个链表。消息以不同的方式发送到队列并从队列中取出。每个消息队列（当然）由一个 IPC 标识符唯一标识。

### 2.4.2.2 内部和用户态数据结构

完全理解 System V IPC 等复杂主题的关键，在于熟悉存在于内核内部的各种内部数据结构。对于最原始的操作，直接访问其中一些结构是必要的，而其他结构则位于更低层次。

消息缓冲区（Message buffer）我们访问的第一个结构是 `msgbuf` 结构。这个数据结构可以被视为消息数据的模板。定义这种类型的结构由程序员决定，你务必理解实际上存在一个名为 `msgbuf` 的结构类型。它在 `linux/msg.h` 中的定义如下：

```c
/* message buffer for msnd and msgrcv calls */
struct msgbuf {
    long mtype;      /* type of message */
    char mtext[1];   /* message text */
};
```

`msgbuf` 结构中有两个成员：

**mtype**
消息类型，用正数表示。这必须是一个正数！

**mtext**
消息数据本身。

分配消息类型的能力，本质上赋予了你在单队列上对消息进行多路复用的能力。例如，客户端进程可以分配一个消息编号，该编号可以作为从服务器进程发送出的消息的类型。服务器本身可以使用另一个数字，客户端可以使用该数字向其发送消息。在另一种场景下，应用程序可以将错误消息标记为类型 1，将请求标记为类型 2。这种可能性是无限的。

另外，不要被赋予消息数据元素（mtext）的过于描述性的名称所误导。该字段不仅限于持有字符数组，可以是任何形式的任何数据。该字段本身是完全任意的，因为该结构是由应用程序程序员定义的。考虑此重新定义：

```c
struct my_msgbuf {
    long mtype;           /* Message type */
    long request_id;     /* Request identifier */
    struct client_info;  /* Client information structure */
};
```

在这里我们看到了消息类型，和之前一样，结构的其余部分被另外两个元素替换了，其中一个是另一个结构！这就是消息队列的魅力所在。内核完全不对数据进行任何转换。任何信息都可以被发送。

然而，存在一个内部限制，即给定消息的最大 own。在 Linux 中，这在 `linux/msg.h` 定义如下：

```c
#define MSGMAX 4056 /* /= 4056 * /* max size of message (bytes) * */
```

消息的总大小不超过 4,056 字节，包括长度为 4 字节（long）的 `mtype` 成员。内核 `msg` 结构在 `msg` 结构的框架内存储队列中的每条消息。它在 `linux/msg.h` 中的定义如下：

```c
/* one structure for each message */
struct msg {
    struct msg *msg_next;      /* next message on queue */
    long msg_type;             /* message text address */
    char *msg_spot;            /* message text size */
    short msg_ts;
};
```

**msg_next**
这是指向队列中下一条消息的指针。它们在内核地址空间内以单链表的形式存储。

**msg_type**
这是消息类型，分配给用户态结构 `msgbuf` 的类型。

**msg_spot**
指向消息体开头的指针。

**msg_ts**
消息类型或正体的长度。

三种类型的 IPC 对象每种都有一个由内核维护的内部数据结构。对于消息队列，这是 `msqid_ds` 结构。内核创建、存储并维护整个系统中创建的每一个消息队列实例。它在 `linux/msg.h` 中的定义如下：

```c
/* one msqid_ds for each queue on the system */
struct msqid_ds {
    struct ipc_perm msg_perm;
    struct msg *msg_first;      /* first message on queue */
    struct msg *msg_next;      /* last message in queue */
    time_t msg_stime;           /* last msgsnd time */
    time_t msg_rime;           /* last msgrcv time */
    time_t msg_ctime;           /* last change time */
    struct wait_queue *wait_send;
    struct wait_queue *wait_recv;
    int msg_qnum;
    long msg_qbytes;
    key_t msg_qid;
    pid_t msg_lspid;
};
```

虽然你很少需要关心 `msqid_ds` 结构的大部分成员，但这里有一个总结表：

| 成员 | 描述 |
| :--- | :--- |
| msg_perm | 队列的权限信息 |
| msg_first | 指向队列中第一条消息的指针 |
| msg_next | 指向队列中最后一条消息的指针 |
| msg_stime | 上一次 `msgsnd` 系统调用的时间 |
| msg_rime | 上一次 `msgrcv` 系统调用的时间 |
| msg_ctime | 上一次更改队列控制结构的时间 |
| wait_send | 等待发送消息的进程队列 |
| wait_recv | 等待接收消息的进程队列 |
| msg_qnum | 队列中当前的消息数量 |
| msg_qbytes | 队列允许的最大字节数 |
| msg_qid | 队列的键 |
| msg_lspid | 上一次发送消息的进程 PID |

# System V IPC

## 2.4.2 系统调用：msgsnd()

一旦我们获取了队列标识符，就可以开始对其进行操作了。要向队列投送消息，你将使用 `msgsnd` 系统调用：

系统调用：`msgsnd()`；

```
原型定义：int msgsnd ( int msqid, struct msgbuf *msg, int msgsz, int msgflg);
返回值：成功时返回 0
错误时返回 -1：errno = EAGAIN (队列已满，且设置了 IPC_NOWAIT)
EACCES (权限被拒绝，无写权限)
EFAULT (msg 地址不可访问 - 无效)
EIDRM (消息队列已被删除)
EINTR (在等待写入时接收到信号)
EINVAL (无效的消息队列标识符、非正消息类型或无效的消息大小)
ENOMEM (没有足够的内存拷贝缓冲区)
```

备注：

`msgsnd` 的第一个参数是我们的队列标识符，由之前的 `msgget` 调用返回。第二个参数 `msgbuf` 是指向已解码并加载的消息缓冲区的指针。`msgsnd` 参数包含消息的字节大小，不包括消息本身的长度（4字节长度）。`msgflg` 参数可以设置为 0（忽略），或：

### IPC_NOWAIT

如果队列已满，则消息将不会写入队列，控制权返回给调用进程。如果未指定此参数，调用进程将挂起（阻塞），直到消息可以写入为止。

让我们为发送消息创建另一个封装函数：

```c
int send_message(int qid, struct msgbuf *qbuf) {
    int result, length;
    /* 消息本质上是结构体的大小减去 sizeof(mtype) */
    length = sizeof(struct msgbuf) - sizeof(long);
    if((result = msgsnd(qid, qbuf, length, 0)) == -1) {
        return (-1);
    }
    return(result);
}
```

这个小函数尝试将位于传递地址 (qbuf) 处的消息发送到由队列标识符 (qid) 指定的消息队列。以下是利用我们到目前为止开发的两个封装函数的代码片段：

```c
#include <stdio.h>
#include <stdlib.h>
#include <linux/ipc.h>
#include <linux/msg.h>
```

```c
main() {
    int qid;
    key_t msgkey;
    struct msqgbuf {
        long mtype;      /* 消息类型 */
        int request;     /* 工作请求号 */
        double salary;   /* 员工工资 */
    } msg;
    /* 生成我们的 IPC key 值 */
    msgkey = ftok('.', 'm');
    /* 打开/创建队列 */
    if ((qid = msgget(msgkey)) == -1) {
        perror("open_queue");
        exit(1);
    }
    /* 加载带有任意测试数据的消息 */
    msg.mtype = 1;          /* 消息类型必须为正数 */
    msg.request = 1;        /* 数据元素 #1 */
    msg.salary = 1000.00;   /* 数据元素 #2（我的年薪！） */
    /* 发送出去！ */
    if ((msgsnd(qid, &msg, 0)) == -1) {
        perror("send_message");
        exit(1);
    }
}
```

在创建/打开我们的消息队列后，我们继续向消息缓冲区加载测试数据（这里缺少字符数据是为了说明我们关于发送二进制信息的观点）。快速调用 `send.message` 将我们的消息分发到消息队列中。

现在队列中有一条消息了，使用 `ipc` 命令查看队列的状态。现在让我们转向从队列中检索消息的消息。要实现这一点，使用 `msgrcv()` 系统调用。

```
系统调用：msgrcv(int msqid,
原型定义：int msgrcv(int msqid, struct msqgbuf *msgp, int msgsz,
long mtype, int msgflg);
返回值：拷贝到消息缓冲区的字节数（消息长度）
错误时返回 -1：errno = E2BIG（消息大于 msgsz，无 MSG_NOERRNO）
```

```
EACCES (无读权限)
EFAULT (msgp 指的地址无效)
EIDRM (检索期间队列被删除)
EINTR (被到达的信号中断)
EINVAL (msqid 无效，大小小于 0)
ENOMSG (设置了 IPC_NOWAIT，且队列中不存在满足请求的消息)
```

备注：

显然，第一个参数用于指定在消息检索过程中使用的队列（应该由早前的 `msgget` 调用返回）。第二个参数 `(msgp)` 代表用于存储检索到的消息的消息缓冲区变量地址。第三个参数 `(msgsz)` 代表消息缓冲区结构的大小，不包括 `mtype` 成员的长度。再次，这可以计算为：

```
msgsz = sizeof(struct msgbuf) - sizeof(long);
```

第四个参数 `(mtype)` 指定要从队列中检索的消息类型。内核将在队列中搜索匹配的最旧消息，并将其副本返回到 `msgp` 指向的地址。存在一个特殊情况：如果传递的 `mtype` 参数值为 0，内核将返回队列中最旧的消息。如果 `mtype` 参数不为 0且设置了 `IPC_NOWAIT`，但队列中没有满足请求的消息，则会返回错误。

（注：此处原文部分存在逻辑重复，翻译时已根据语义通顺性进行了必要的逻辑组织）

备注：

显然，第一个参数用于指定在消息检索过程中使用的队列（应该由早前的 `msgget` 调用返回）。第二个参数 `(msgp)` 代表用于存储检索到的消息的消息缓冲区变量地址。第三个参数 `(msgsz)` 代表消息缓冲区结构的大小，不包括 `mtype` 成员的长度。再次，这可以计算为：

```
msgsz = sizeof(struct msgbuf) - sizeof(long);
```

第四个参数 `(mtype)` 指定要从队列中检索的消息类型。内核将在队列中搜索匹配的最旧消息，并将其副本返回到 `msgp` 指向的地址。存在一个特殊情况：如果传递的 `mtype` 参数值为 0，内核将返回队列中最旧的消息。如果 `mtype` 参数不为 0且设置了 `IPC_NOWAIT`，但队列中没有满足请求的消息，则会返回错误。

（注：原文后半部分存在较多文本重复和逻辑混乱，翻译已尽量保持原意并进行校顺）

显然，第一个参数用于指定在消息检索过程中使用的队列（应该由早前的 `msgget` 调用返回）。第二个参数 `(msgp)` 代表用于存储检索到的消息的消息缓冲区变量地址。第三个参数 `(msgsz)` 代表消息缓冲区结构的大小，不包括 `mtype` 成员的长度。再次，这可以计算为：

```
