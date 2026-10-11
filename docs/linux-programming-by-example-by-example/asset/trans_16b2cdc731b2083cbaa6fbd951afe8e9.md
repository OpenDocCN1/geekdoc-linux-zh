

将键入的响应（以**粗体**显示）直接存储到之前声明的 msgstructure 中。如果 `msgsnd` 成功完成，它会显示一条确认消息。请注意，`qsnd` 将消息类型设置为调用进程的 PID。这使得你稍后可以使用 `msgrcv` 仅检索该进程发布的那些消息。

## 读取排队消息

要从队列中拉取一条消息，请使用 `msgrcv`，其语法如下：

```c
int msgrcv(int msqid, void *ptr, size_t nbytes, long type, int flags);
```

如果成功，`msgrcv` 会从队列中移除返回的消息。参数与 `msgsnd` 接受参数相同，不同之处在于 `msgrcv` 会用消息类型和最多 `nbytes` 的数据填充 `ptr` 结构体。额外的参数 `type` 对应于前面讨论的 msg 结构体中的 `msg_type` 成员。`type` 的值决定了返回哪条消息，如以下列表所示：

- 如果 `type` 为 0，则返回队列中的第一条消息（最顶层的消息）。
- 如果 `type` 大于 0，则返回第一条 `msg_type` 等于 `type` 的消息。
- 如果 `type` 小于 0，则返回第一条 `msg_type` 为小于或等于 `type` 绝对值的最小值的消息。

`flags` 的值也控制着 `msgrcv` 的行为。如果返回的消息大于 `nbytes`，且 `flags` 中设置了 `MSG_NOERROR` 位，则消息会被截断为 `nbytes`（但不会产生消息已被截断的通知）。否则，`msgrcv` 返回 -1 以指示错误，并将 `errno` 设置为 `E2BIG`。消息也保留在队列中。

如果 `flags` 中设置了 `IPC_NOWAIT` 位，`msgrcv` 立即返回，如果没有指定类型的消息可用，则设置 `errno` 为 `ENOMSG`。否则，`msgrcv` 阻塞，直到之前为 `msgsnd` 描述的相同条件之一发生。

> **注意**
> `type` 参数的负值可用于创建 LIFO（后进先出）类型的队列，通常称为堆栈。传入负值使您可以按与放入队列顺序相反的顺序检索给定类型的消息。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_398_0.png)

以下程序 `qrd` 从一个已创建并填充的队列中读取一条消息。要读取的队列 ID 作为命令行参数传入。

```c
/*
 * qrd.c - Read all message from a message queue
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>

#define BFSZ 512

struct msg { /* Message structure */
    long msg_type;
    char msg_text[BFSZ];
};

int main(int argc, char *argv[]) {
    int qid; /* The queue identifier */
    int len; /* Length of message */
    struct msg pmsg; /* Pointer to a message structure */

    /* Expect the queue ID passed on the command-line */
    if (argc != 2) {
        puts("USAGE: qrd <queue ID>");
        exit(EXIT_FAILURE);
    }
    qid = atoi(argv[1]);

    /* Retrieve and display a message from the queue */
    len = msgrcv(qid, &pmsg, BFSZ, 0, 0);
    if (len > 0) {
        printf("reading queue id: %05d\n", qid);
        printf("\tmessage type: %05d\n", pmsg.msg_type);
        printf("\tmessage text: %s\n", pmsg.msg_text);
    } else {
        perror("msgrcv");
        exit(EXIT_FAILURE);
    }

    exit(EXIT_SUCCESS);
}
```

该程序的一次运行输出如下。与之前一样，它使用由 `mkq` 创建的队列 ID，并读取由 `qsnd` 示例发布的那条消息。

![](img/be588b36b489136ce784030a08a1d3d4_400_0.png)

**输出**

```
$ ./mkq
created queue id = 640
opened queue id = 640
$ ./qsnd 640
Enter message to post:
this is test message number one
message posted

$ ./qrd 640
reading queue id: 00640
message type: 14308
    message text: this is test message number one
```

从代码列表中可以看出，从消息队列中读取比写入更容易，并且需要更少的代码。示例程序中特别值得注意的是，它从队列顶部获取第一条消息，因为它传递了 `type` 为 0。在这种情况下，由于消息写入进程的 PID 是已知的或可以轻易发现（`14308`），`qrd` 本可以传递 `type` 为 14308 并从队列中获取相同的消息。

## 删除消息队列

`msgctl` 函数提供了对消息队列的一定控制。其原型如下：

```c
int msgctl(int msqid, int cmd, struct msqid_ds *buf);
```

通常，`msqid` 是现有队列的队列 ID。`cmd` 可以是以下之一：

- `IPC_RMID` — 移除队列 `msqid`。
- `IPC_STAT` — 用队列的 `msqid_ds` 结构体填充 `buf`。`IPC_STAT` 允许你查看队列的内容而不移除任何消息。由于这是一种非破坏性读取，你可以将其视为类似于 `msgrcv`。
- `IPC_SET` — 允许你更改队列的 UID、GID、访问模式以及队列允许的最大字节数。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_401_0.png)

以下程序使用 `msgctl` 调用删除命令行传入其 ID 的队列。

```c
/*
 * qctl.c - Remove a message queue
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int qid;
    struct msqid_ds dsbuf;

    if(argc != 2) {
        puts("USAGE: qctl <qid>");
        exit(EXIT_FAILURE);
    }
    qid = atoi(argv[1]);

    if((msgctl(qid, IPC_RMID, NULL)) < 0) {
        perror("msgctl");
        exit(EXIT_FAILURE);
    }

    printf("queue %d removed\n", qid);
    exit(EXIT_SUCCESS);
}
```

## 输出

```
$ ./mkq
created queue_id = 1280
opened queue_id = 1280
$ ipcs -q
------- Message Queues -------
key        msqid   owner perms   used-bytes messages
0x0000007b 1280    kwall 666     0          0

$ ./qctl 1280
queue 1280 removed
$ ipcs -q
------- Message Queues -------
key        msqid   owner perms   used-bytes messages

```

程序输出显示指定的队列已被删除。`mkq` 创建队列。`ipcs` 调用确认队列已创建。使用 `mkq` 显示的队列 ID，`qctl` 调用 `msgctl`，指定 `IPC_RMID` 标志以删除队列。再次运行 `ipcs` 确认 `qctl` 已移除队列。

在几个示例程序中使用的 `ipcs` 命令显示了系统执行时所有现有的 System V IPC 结构的数量和状态。`ipcrm` 命令将删除在命令行上指定类型和 ID 的 IPC 结构。更多信息请参阅手册页。图 17.2 显示了 `ipcs` 命令的输出。

![](img/be588b36b489136ce784030a08a1d3d4_402_0.png)

图 17.2：`ipcs` 显示当前存在的所有 System V IPC 对象。

图 17.2 显示至少每个类型的 IPC 对象都存在一个。当前正在使用三个共享内存段、一个消息队列和两个信号量（信号量将在下一节讨论）。每个对象的关键值、标识符、所有者/创建者以及权限都清晰列出。相对于每种对象类型的统计数据显示在输出的最后之一或两列中，具体取决于对象类型。

## 信号量

信号量控制对共享资源的访问。它们与你目前看到的其他 IPC 手段大不相同，因为它们不使进程间共享信息，而是同步访问那些不应同时被访问的共享资源。在这方面，信号量操作更接近文件或记录锁定，但应用于比文件更多的资源。本节只讨论最简单的信号量类型，即二元信号量。二元信号量取两个值之一：当资源被锁定且其他进程不应访问时为 0，当资源未锁定时为 1。

- 有关文件和记录锁定的更多信息，参见第 182 页的"文件锁定"。

信号量的工作原理非常像繁忙路口的交通灯。当一个进程需要访问受控资源（如文件）时，它首先检查信号量的值，就像司机检查交通灯是否变绿一样。如果信号量值为零，对应红灯，则表示资源正在使用中，因此进程阻塞，直到资源变得可用（即，信号量的值变为非零）。在 System V IPC 的术语中，这种阻塞被称为等待。如果信号量为正值，对应路口的绿灯，则表示相关资源可用，因此进程递减信号量，对资源执行操作，然后递增信号量以释放"锁"。

## 创建信号量

当然，在你能够递增或递减信号量之前，它必须存在。创建新信号量或访问现有信号量的函数调用是 `semget`，在 `sys/sem.h` 中定义原型如下（你还需要包含 `sys/ipc.h` 和 `sys/types.h`）：

```c
int semget(key_t key, int nsems, int flags);
```

`semget` 返回与 `nsems` 个信号量集合相关联的信号量标识符。如果 `key` 为 `IPC_PRIVATE`，或者 `key` 尚未被使用且 `flags` 中设置了 `IPC_CREAT` 位，则创建一个新的信号量集合。与共享内存段和消息队列一样，`flags` 也可以与权限位（八进制）进行按位或运算，以设置信号量的访问模式。然而请注意，信号量具有读和修改权限，而不是读和写权限。信号量使用"修改"的概念而不是

