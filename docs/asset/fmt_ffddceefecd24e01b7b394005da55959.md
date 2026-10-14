
然后你可以使用 `ifaddr` 的值来初始化 `struct sockaddr` 结构中的 `sin_addr`。同样的更改也适用于客户端，只是客户端通常使用特定地址而不是 `INADDR_ANY`。

## 7.7 消息队列

消息队列是两个进程之间传输数据的另一种方式。正如你所预期的，创建消息队列有两种方法：System V 方法和 POSIX 方法。每种方法都略有不同，但原理是相同的。

两种消息队列都强调固定大小、基于优先级的消息。接收者必须精确读取传输的字节数；否则，从消息队列的读取将失败。这为应用程序提供了某种程度的保证，确保进程正在与相同版本的消息结构进行通信。

每个 API 实现优先级的方式略有不同。System V API 允许接收者在优先处理传入消息时具有位级灵活性，而 POSIX API 则强制执行严格的优先级排序。

### 7.7.1 System V 消息队列

创建或挂载消息队列的函数是 `msgget`，它接受一个整数作为消息队列的用户自定义键（key），就像 System V 的共享内存 API 一样。该函数返回一个系统定义的队列键，用于后续对队列的读写。以下是 `msgget` 的原型：

```c
int msgget(key_t key, int msgflg);
```

正如本章前面提到的，`key` 参数可以是一个从不改变的应用定义键。`msgget` 返回的值是系统定义的消息队列标识符，用于该进程的所有读写操作。该键可以被宏 `IPC_PRIVATE` 替换。使用此值作为键将始终创建一个新的消息队列。`msgget` 返回的消息队列 ID 在进程间是有效的，不像文件描述符。因此，消息队列 ID 可以在父子进程以及对等进程之间共享。

`msgget` 的 `msgrflag` 参数与传递给 `open` 系统调用的标志非常相似。事实上，低 9 位与 `open` 调用使用的权限位相同。其他允许的标志还包括 `IPC_CREAT` 和 `IPC_EXCL`：`IPC_CREAT` 用于创建新的消息队列；如果消息队列已存在，它将返回现有队列的消息 ID。当指定 `IPC_CREAT` 配合 `IPC_EXCL` 时，如果消息队列存在，它会导致 `msgget` 失败。这种行为与 `open(2)` 系统调用使用的 `O_CREAT` 和 `O_EXCL` 标志相同。

消息队列没有对应的 `close` 函数，因为队列不消耗文件描述符。ID 对所有进程都可见，操作系统不会按进程来跟踪消息队列。

进程可以使用 `msgctl` 函数移除消息队列，正如其名称所示，除了移除消息队列外，还可以执行许多操作：

```c
int msgctl(int mqid, int cmd, struct msgid_ds *buf);
```

移除消息队列的 `cmd` 参数是 `IPC_RMID`，在这种情况下 `buf` 参数可以为 `NULL`。更多细节请参考 `msgctl(2)`。

读取和写入消息队列通过以下函数完成：

```c
int msnd(int qid, void *msg, size_t mgsz, int msgflg);

size_t msgrcv(int qid, void *msg, size_t mgsz, int msgflg);
```

System V 消息队列允许变长，前提是发送者和接收者对大小和优先级达成一致。你可以在列表 7-10 中看到所有这些技术的演示。

列表 7-10 `sysv-msgq.c`：使用 System V API

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/msg.h>
#include <sys/wait.h>
#include <sys/types.h>
#include <sys/ipc.h>
#include <errno.h>

struct message {
    long mtype;
    char mtext[128];
};

void producer(int mqid) {
    // 注意我们发送这些消息的消息。
    struct message msg;
    msg.mtype = 1;
    strcpy(msg.mtext, "type 1 - first");
    msgsnd(mqid, &msg, sizeof(mtext), 0);
    msg.mtype = 2;
    strcpy(msg.mtext, "type 2 - second");
    msgsnd(mqid, &msg, sizeof(mtext), 0);
    msg.mtype = 1;
    strcpy(msg.mtext, "type 1 - third");
    msgsnd(mqid, &msg, sizeof(mtext), 0);
}

void consumer(int qid) {
    struct message msg;
    int r;
    int i;
    for (i = 0; i < 3; i++) {
        // -2 接受类型为2或更小的消息。
        r = msgrcv(qid, &msg, sizeof(mtext), -2, 0);
        printf("%s\n", msg.mtext);
    }
}

int main(int argc, char *argv[]) {
    // 创建私有的（无名的）消息队列。
    int mqid;
    mqid = msgget(IPC_PRIVATE, S_IRREAD | S_IWRITE);
    if (mqid == -1) {
        perror("msgget");
        exit(1);
    }

    pid_t pid = fork();
    if (pid == 0) {
        consumer(mqid);
        exit(0);
    }
    else {
        int status;
        producer(mqid);
        wait(&status);
    }

    // 移除消息队列。
    int r = msgctl(mqid, IPC_RMID, 0);
    if (r)
        perror("msgctl");
    return 0;
}
```

注意，类型 1 的消息最先被接收。数字越小优先级越高，越先接收。因此，你接收消息的顺序与发送顺序不同。若要按照发送顺序（FIFO FIFO）接收消息，请在 `msgrcv` 的 `type` 参数中使用 0。

当 `msgrcv` 的 `type` 参数为非零值时，消息按优先级接收，如下所示：

- 正数——仅接受该类型的消息。
- 负数——仅接受指定类型绝对值或更小值的消息。

Linux 还添加了 `MSG_EXCEPT` 标志，它不属于任何标准的一部分。当 `type` 为正数且在 `msgrcv` 的 `flags` 参数中设置了 `MSG_EXCEPT` 时，其效果是反转选择——即，不再接收类型为 N 的消息，`msgrcv` 将接受除类型 N 外的任何消息。

### 7.7.2 POSIX 消息队列

POSIX API 在功能上与 System V API 相似，但消息队列是紧密按照 POSIX 文件模型建模的。在文件模型中，消息队列具有名称，且必须遵循与文件名相同的规则。消息队列可以像文件一样被打开、关闭、创建和取消（`unlink`）。在 Linux 中，消息队列会消耗文件描述符，就像打开的文件一样。对于熟悉 POSIX 文件 API 的程序员来说，POSIX 消息队列 API 应该会非常直观。

#### 7.7.2.1 创建、打开、关闭和删除 POSIX 消息队列

POSIX 没有为消息队列提供创建函数。相反，通过使用带有 `O_CREAT` 标志的 `mq_open` 函数来创建消息队列。
`mq_open` 定义如下：

```c
mq_t mq_open(const char *name, int oflag, ...);
```
