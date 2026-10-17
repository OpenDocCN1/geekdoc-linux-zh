
标志参数的宏与 `open` 相同（例如，`O_CREAT`），而不是像与 `msgget` 使用的那样特殊的宏（例如，`IPC_CREAT`）：

- 根据你是想只接收消息、只发送消息还是两者都做，你必须指定 `O_RDONLY`、`O_WRONLY` 或 `O_RDWR` 之一。
- 如果你想如果队列尚不存在则创建队列，你指定 `O_CREAT`。在这种情况下，你提供四个参数，如语法框中第二种形式所示。
- 如果你想当队列已经存在时函数失败，你指定 `O_EXCL`。
- 如果你想消息队列描述符是非阻塞的，你指定 `O_NONBLOCK`，这意味着如果队列分别是满的或空的，`mq_send` 和 `mq_receive` 将返回 −1，并将 `errno` 设置为 `EAGAIN`。默认行为是阻塞的。

当设置了 `O_CREAT` 并且实际上创建了队列时，`perms` 参数的解释类似于文件和 System V 消息队列上的权限，具有通常的 `S_` 标志（第 2.3 节）。读和写权限分别意味着接收和发送消息的能力，而执行权限没有任何意义。与文件一样，队列具有用户 ID 和组 ID，它们由创建该队列的进程的有效 ID 设置。随后，`owner`、`group` 和 `other` 位与有效用户 ID 和组 ID 的关系与文件相同。

此外，如果指定了 `O_CREAT` 并且创建了一个队列，且 `attr` 参数不为 `NULL`，则会从提供的 `mq_attr` 结构体中设置两个属性：`mq_maxmsg` 和 `mq_msgsize`。这两个属性分别表示队列所能容纳的最大消息数量以及单条消息的最大尺寸。标准并未对这两个属性规定具体的上限值，但如果空间不足，`mq_open` 将返回 -1，并将 `errno` 设置为 `ENOSPC`。大多数实现都会使用链表来实现队列，因此无论数值多少，`mq_open` 都不会因空间耗尽而失败，因为新创建的队列是空的。如果 `attr` 参数为 `NULL`，这两个属性将被设置为实现定义的值。

如果阅读前几段时让你感到头晕目眩，并且你假设 `mq_open` 与 `open` 完全一样，那么只要你不要假设它返回一个文件描述符，你就可能一切正常。

你使用 `mq_close` 来关闭一个打开的消息队列：

```c
#include <mqueue.h>

int mq_close(
   mqd_t mqd                /* 消息队列描述符 */
);
/* 成功返回零，错误返回 -1（设置 errno） */
```

与 System V 消息队列类似，POSIX 消息队列会持续存在，直到它们被删除或内核重启。你通过类似 `unlink` 的调用删除一个 POSIX 消息队列：

```c
#include <mqueue.h>

int mq_unlink(
   const char *name          /* POSIX IPC 名称 */
);
/* 成功返回 0，错误返回 -1（设置 errno） */
```

就像 `unlink` 一样，`mq_unlink` 会立即使该名称消失，但队列的实际销毁会推迟到所有打开的消息队列描述符被关闭之后。（回想一下，在 System V 消息队列中，使用 `msgctl` 删除队列是立即生效的，并且可能具有破坏性。）因此，如果你愿意，一旦所有需要该队列的进程都打开了它，你就可以调用 `mq_unlink` 将其删除，就像你有时对临时文件做的那样。

好吧，准备好发送消息了吗？正如你可能猜测的那样，你调用 `mq_send`：

```c
#include <mqueue.h>

int mq_send(
          mqd_t mqd,             /* 消息队列描述符 */
          const char *msg,       /* 消息 */
          size_t msgsize,        /* 消息大小 */
          unsigned priority      /* 优先级 */
      );
/* 成功返回 0，错误返回 -1（设置 errno） */
```

`mq_send` 将大小为 `msgsize` 的消息放入队列中，将其位置排在所有具有 `优先级` 较低的消息之前，但排在具有相同 `优先级` 的消息之后（换句话说，正如你所期望的那样）。优先级从 0 到至少 31；你可以使用 `sysconf` 获取实际的最大值（见第 1.5.5 节）。

如前所述，如果队列已满，`mq_send` 将阻塞，除非设置了 `O_NONBLOCK` 标志。

当然，接收消息的调用是 `mq_receive`：

```c
#include <mqueue.h>

ssize_t mq_receive(
         mqd_t mqd,             /* 消息队列描述符 */
         char *msg,             /* 消息缓冲区 */
         size_t msgsize,        /* 消息缓冲区大小 */
         unsigned *priority     /* 返回的优先级或 NULL */
      );
/* 返回消息大小，错误时返回 -1（设置 errno） */
```

`mq_receive` 获取最高优先级中最旧的消息，由于 `mq_send` 的定义方式，这等同于获取队列中的第一个消息。

`msgsize` 参数有点棘手：它是 `msg` 参数指向的缓冲区的大小，正如你所预期的那样，但它必须至少等于 `mq_msgsize` 属性（参见上面的 `mq_open`），否则 `mq_receive` 将失败，*即使队首的消息足够小可以容纳*。这实际上是一个优秀的设计选择：立即发现缓冲区过小的问题，而不是需要恰好合适的测试数据来暴露 bug。接收到消息的实际大小是函数的返回值。

如果优先级参数不为 `NULL`，它将获取接收到消息的优先级。接收到的消息会从队列中移除；没有方法只是窥视它。如果队列为空，除非设置了 `O_NONBLOCK`，否则 `mq_receive` 将阻塞。`mq_send` 和 `mq_receive` 的变体允许阻塞的调用超时：

```c
#include <mqueue.h>
#include <time.h>

int mq_timesend(
        mqd_t mqfd,                          /* 消息队列描述符 */
        const char *msg,                     /* 消息 */
        size_t msgsize,                      /* 消息大小 */
        unsigned priority,                   /* 优先级 */
        const struct timespec *tmout         /* 超时 */
);
/* 成功返回 0，错误返回 -1（设置 errno） */
```

```c
#include <mqueue.h>
#include <time.h>

size_t mq_timedreceive(
        mqd_t mqfd,                          /* 消息队列描述符 */
        char *msg,                           /* 消息缓冲区 */
        size_t msgsize,                      /* 消息缓冲区大小 */
        unsigned *priority,                   /* 返回的优先级或 NULL */
        const struct timespec *tmout         /* 超时 */
);
/* 返回消息大小，错误时返回 -1（设置 errno） */
```

超时仅在该调用会阻塞且 `O_NONBLOCK` 未设置时适用。当该时间段结束时，函数返回 -1，并将 `errno` 设置为 `ETIMEDOUT`。这两个函数是超时节选项（`_POSIX_TIMEOUTS`）的一部分，并且是 SUS3 中新增加的。

如我所说，处理多个消息队列，或者将消息队列与可能阻塞的其他事物（如终端或网络连接）结合使用是很棘手的，因为你不能用 `select` 或 `poll` 测试消息队列描述符。然而，你可以安排当消息到达时通过信号进行通知，然后你就可以调用 `mq_receive` 而不用担心阻塞问题。（参见第 5.18 节了解另一种解决方案。）你使用 `mq_notify` 来设置此功能。

```c
#include <mqueue.h>

int mq_notify(
             mqd_t mqd,                  /* 消息队列描述符 */
             const struct sigevent *ep    /* 通知 */
);
/* 成功返回 0，错误返回 -1（设置 errno） */
```

当一个进程或线程被注册时，如果在由 `mqd` 指定的空队列上收到消息，它会收到一个信号，除非有一个或多个进程或线程已经阻塞在 `mq_receive` 中，在这种情况下，其中一个 `mq_receive` 调用将返回。

只能注册一个进程或线程；尝试注册第二个进程或线程将导致错误。当发出信号或调用 `mq_notify` 且第二个参数为 `NULL` 时，进程或线程将被取消注册。

对于非空队列上的消息到达，没有通知，因此仅靠 `mq_notify` 无法确保进程在每次消息到达时都收到信号。例如，它可能会在空队列上收到消息时收到信号，但随后第二条消息可能在第一条消息被接收之前到达，这不会触发通知，因为队列此时不再是空的。因此，应用程序需要执行类似以下的操作：

- 在调用 `mq_notify` 后，重复调用设置了 `O_NONBLOCK` 的 `mq_receive`，直到队列为空。
- 当收到信号时，立即再次调用 `mq_notify`，然后执行上一步。

发送的信号以及通知的其他属性由传递给 `mq_notify` 的 `sigevent` 结构体的内容决定，如第 9.5.6 节所述。

最后，你可以获取和设置消息队列属性：

```c
#include <mqueue.h>

int mq_getattr(
             mqd_t mqd,                      /* 消息队列描述符 */
             struct mq_attr *attr             /* 属性 */
);
/* 成功返回 0，错误返回 -1（设置 errno） */
```

![](img/41b4c8f6d6a5c349eee321a301703d97_465_0.png)

`mq_getattr` 根据队列的当前状态填充结构体（与 `mq_open` 一起展示）。最有用的属性可能是成员 `mq_curmsgs`，它包含队列中当前的消息数量。

`mq_setattr` 设置或清除 `mq_flags` 成员中的 `O_NONBLOCK` 标志；按照标准，它对其他方面没有影响。（实现中可能还有其他非移植的标志可以设置。）因此，对于 `O_NONBLOCK` 标志，`mq_setattr` 用于消息队列描述符，就像 `fcntl` 用于文件描述符一样。如果 `oldattr` 非 `NULL`，则用它来获取返回的旧属性。

## 7.7.2 SMI 的 POSIX 消息队列实现

现在是 SMI 函数的第三个实现。首先，这是内部消息队列，它与 FIFO 的内部队列几乎相同，因为它要处理类似问题：

```c
#define MAX_CLIENTS 20

typedef struct {
    SMIENTITY sq_entity;          /* entity */
    mqd_t sq_mqd_server;         /* server message-queue descriptor */
    char sq_name[SERVER_NAME_MAX];/* server name */
    struct client_info {
        mqd_t cl_mqd;            /* client message-queue descriptor */
        pid_t cl_pid;            /* client process ID */
    } sq_clients[MAX_CLIENTS];
    struct client_id sq_client;  /* client ID */
    size_t sq_msgsize;           /* msg size */
    struct smi_msg *sq_msg;      /* msg buffer */
} SMIQ_MQ;
```

与 FIFO 一样，为了避免为每条消息打开客户端消息队列的开销，服务器将跟踪它知道的每个客户端，并查找已打开队列的存储的消息队列描述符。在许多实际服务器中，这其实不是那么大的负担，因为它们几乎总是想跟踪其客户端。客户端只使用数组的第一个元素来存储其自身的消息队列描述符，但我们不关心在这个示例中浪费的空间。

有两个函数将 SMI 服务器名称和客户端进程 ID 转换为 POSIX IPC 名称：

```c
static void make_mq_name_server(const SMIQ_MQ *p, char *mqname,
           size_t mqname_max)
{
    snprintf(mqname, mqname_max, "/smmq-%s&", p->sq_name);
}

static void make_mq_name_client(pid_t pid, char *mqname,
           size_t mqname_max)
{
    snprintf(mqname, mqname_max, "/smimq-c%d", pid);
}
```

这些名称看起来像是在根目录中，但在 Solaris 上并非如此，如 7.6.2 节所述。

接下来是一个由服务器使用的函数，用于根据客户端的进程 ID 获取其消息队列描述符，这是客户端在消息中发送给服务器的内容：

```c
static mqd_t get_client_mqd(SMIQ_MQ *p, pid_t pid)
{
    int i, avail = -1;
    char mqname[SERVER_NAME_MAX + 100];

    for (i = 0; i < MAX_CLIENTS; i++) {
        if (p->sq_clients[i].cl_pid == pid)
            return p->sq_clients[i].cl_mqd;
        if (avail == -1 && p->sq_clients[i].cl_pid == 0)
            avail = i;
    }

    errno = ECONNREFUSED;
    ec_negl_t avail )
    p->sq_clients[avail].cl_pid = pid;
    make_mq_name_client(pid, mqname, sizeof(mqname));
    ec_negl( p->sq_clients[avail].cl_mqd = mq_open(mqname, O_WRONLY) )
    return p->sq_clients[avail].cl_mqd;

EC_CLEANUP_BGN
    return (mqd_t) -1;
EC_CLEANUP_END
}
```

该函数首先在数组中查找是否已经见过该客户端，如果是这样，它已经拥有消息队列描述符。如果没有，它会以写方式打开队列并保存描述符供下次使用。

现在我们准备好第一个 SMI 函数 `smi_open_mq`：
