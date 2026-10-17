
`msgnum_t` 类型持有消息队列中的消息数；`msglen_t` 类型持有消息队列允许的字节数。两种类型都必须至少与 `unsigned short` 大。

## 15.4.1 访问消息队列

`msget` 函数返回与 `key` 参数的消息队列标识符。如果 `key` 是 `IPC_PRIVATE` 或 `msgflg & IPC_CREATE` 为非零且没有已关联的消息队列或标识符，则创建该标识符。

### 语法

```c
#include <sys/msg.h>

int msget(key_t key, int msgflg);
```

### POSIX:XI

如果成功，`msget` 返回对应消息队列标识符的非负整数。如果失败，`msget` 返回 `-1` 并设置 `errno`。下表列出了 `msget` 的强制错误。

| errno | 原因 |
| --- | --- |
| EACCES | 键存在消息队列，但权限被拒绝 |
| EEXIST | 键存在消息队列，但 ((msgflg & IPC_CREATE) && (msgflg & IPC_EXCL)) != 0 |
| ENOENT | 键不存在消息队列，但 (msgflg & IPC_CREATE) == 0 |
| ENOSPC | 将超过系统范围的消息队列限制 |

## 示例 15.14

创建一个新的消息队列。

```c
#define PERMS (S_IRUSR) | S_IWUSR

int mqid;

if ((msqid = msgget(IPC_PRIVATE, PERMS)) == -1)
    perror("Failed to create new message queue");
```

在用 `msgget` 访问消息队列后，程序使用 `msgsnd` 将消息插入队列。`msqid` 标识消息队列，`msggrp` 参数指向一个用户定义的缓冲区，该缓冲区包含要发送的消息，如文所示。`msgsz` 参数指定消息文本的实际大小。`msgflg` 参数指定了在各种情况下采取的操作。

### 语法

```c
#include <sys/msg.h>

int msgsnd(int msqid, const void *msgp, size_t msgsz, int msgflg);
```

### POSIX:XI

如果成功，`msgsnd` 返回 `0`。如果失败，`msgsnd` 返回 `-1` 并设置 `errno`。下表列出了 `msgsnd` 的强制错误。

| errno | 原因 |
|---|---|
| EACCES | 拒绝调用者执行该操作 |
| EAGAIN | 操作将阻塞进程，但 (msgflg & IPC_NOWAIT) != 0 |
| EIDRM | msqid 已从系统中移除 |
| EINTR | msgsnd 被信号中断 |
| EINVAL | msqid 无效，消息类型 < 1，或 msgsz 超出范围 |

`msgsz` 参数指向一个用户定义的缓冲区，其第一个成员必须是指定消息类型的 `long`，后面是消息文本的空间。该结构如下。

```c
struct mymsg {
    long mtype; /* 消息类型 */
    char mtext[1]; /* 消息文本 */
};
```

) mymsg_t;

消息类型必须大于 `0`。用户可以根据应用程序所需的 {分配消息类型。

以下是将字符串消息发送到消息队列所需的步骤：

- 1. 分配一个缓冲区 `mbuf`，其类型为 `mysmsg_t` 且大小为 `sizeof(mysmsg_t) + strlen(message)`
- 2. 将消息拷贝到 `mbuf->mtext` 成员中。
- 3. 在 `mbuf->mtype` 成员中设置消息类型。
- 4. 发送消息。
- 5. 释放 `mbuf`。

记得检查错误并在发生错误时释放 `mbuf`。此代码在稍后讨论的程序 15.9 提供。

程序可以使用 `msgrcv` 从消息队列中移除消息。`msqid` 参数标识消息队列，`msgp` 参数指向一个用户定义的缓冲区，用于存放获取的消息。`msgp` 的格式如上文 `msgsnd` 所示。`mssz` 参数指定消息文本的实际大小。`msgtyp` 参数可供接收者用于消息选择。`msgflig` 指定了在各种条件下要采取的操作。

## 概览

```c
#include <sys/msg.h>

ssize_t msgrcv(int msqid, void *msgp, size_t msgsz,
               long msgtyp, int msgflig);
```

POSIX:XSI

如果成功，`msgrcv` 返回消息文本的字节数。如果失败，`msgrcv` 返回 `(size_t) -1` 并设置 `errno`。下表列出了 `msgrcv` 的强制错误。

| errno | cause |
| :--- | :--- |
| E2BIG | msgp 中 `mtext` 成员的值大于了 `msgsize` 且 `(msgflig & MSG_NOERERROR) == 0` |
| EACCES | 调用者被拒绝操作 |
| EIDRM | msgid 已从系统中移除 |
| EINTR | msgrcv 被信号中断 |
| EINVAL | msgid 值无效 |
| ENOSQ | 队列不包含请求类型的消息且 `(msgflg & IPC_NOWAIT) != 0` |

表 15.4 显示了 `msgrcv` 如何使用 `msgtyp` 参数来决定从队列中移除消息的顺序。

使用 `msgctl` 释放或更改由 `msgid` 标识的消息队列的权限。`cmd` 参数指定了如表 15.5 所示的操作。`msgctl` 函数使用其 `buf` 参数来写入或读取状态信息，取决于 `cmd`。

## 表 15.4. POSIX:XSI 的 `msgtyp` 参数值决定了 msgrcv 从队列中移除消息的顺序。

| msgtyp | action |
| :--- | :--- |
| 0 | 从队列移除第一条消息 |
| > 0 | 从队列中移除类型为 `msgtyp` 的第一条消息 |
| < 0 | 移除小于等于 `msgtyp` 绝对值的最小类型的第一条消息 |

## 表 15.5. `msgctl` 的 `cmd` 参数的 POSIX:XSI 值。

| cmd | description |
| :--- | :--- |
| IPC_RMID | 移除消息队列 `msgid` 并销毁对应的 `msgid_ds` |
| IPC_SET | 从 `buf` 设置 `msgid_ds` 数据结构的成员 |
| IPC_STAT | 将 `msgid_ds` 数据结构的成员拷贝到 `buf` 中 |

## 概览

```c
#include <sys/msg.h>

int msgctl(int mqid, int cmd, struct mqid_ds *buf); POSIX_XSI
```

如果成功，`msgctl` 返回 `0`。如果失败，`msgctl` 返回 `-1` 并设置 `errno`。下表列出了 `msgctl` 的强制错误。

| errno | cause |
| :--- | :--- |
| EACCES | cmd 为 IPC_STAT 且调用者没有读取权限 |
| EINVAL | mqid 或 cmd 无效 |
| EPERM | cmd 为 IPC_RMID 或 IPC_SET 且调用者没有权限 |

程序 15.9 包含了访问消息队列的实用程序，与程序 15.6 类似，但由于不需要初始化或同步，所以更简单。每个进程在访问消息队列之前都应该调用 `initqueue` 函数。`msgprint` 函数的语法类似于 `printf`，用于处理队列中的格式化消息。`msgprint` 和 `msgwrite` 为每条消息分配内存并在调用 `msgsnd` 后释放这些内存。`removequeue` 函数移除消息队列及其关联的数据结构。`msgqueue.h` 头文件包含了这些函数的原型声明。如果成功，这些函数返回 `0`。如果失败，这些函数返回 `-1` 并设置 `errno`。

## 程序 15.9 msgqueue.c

访问并输出到消息队列的实用函数。

```c
#include <errno.h>
#include <stdio.h>
#include <stdarg.h>
#include <stdlib.h>
#include <string.h>
#include <sys/msg.h>
#include <sys/stat.h>
#include "msgqueue.h"

#define PERM (S_IRUSR | S_IWUSR)

typedef struct {
    long mtype;
    char mtext[1];
} msmsg_t;

static int queueid;

int initqueue(int key) {
    /* initialize the message queue */
    queueid = msgget(key, PERM | IPC_CREAT);
    if (queueid == -1)
        return -1;
    return 0;
}

int msprintf(char *fmt, ...) { /* output a formatted message */
    va_list ap;
    char ch;
    int error = 0;
    int len;
    msmsg_t *msgsg;
    va_start(ap, fmt); /* set up the format for output */
    len = vsnprintf(&ch, 1, fmt, ap); /* how long would it be? */
    if ((msgsg = (msmsg_t *)malloc(sizeof(msmsg_t) + len)) == NULL)
        return -1;
    memcpy(msgsg->mtext, ch, len); /* copy into the buffer */
    msgsg->mtype = 1; /* message type is always 1 */
    if (msgsnd(queueid, msgsg, len + 1, 0) == -1)
        error = errno;
    free(msgsg);
    if (error) {
        errno = error;
        return -1;
    }
    return 0;
}

int msgwrite(void *buf, int len) { /* output buffer of specified length */
    int error = 0;
    msmsg_t *msgsg;
    if ((msgsg = (msmsg_t *)malloc(sizeof(msmsg_t) + len)) == NULL)
        return -1;
    memcpy(msgsg->mtext, buf, len);
    msgsg->mtype = 1; /* message type is always 1 */
    if (msgsnd(queueid, msgsg, len, 0) == -1)
        error = errno;
    free(msgsg);
    if (error) {
        errno = error;
        return -1;
    }
    return 0;
}

int removequeue(void) {
    return msgctl(queueid, IPC_RMID, NULL);
}
```

## 示例 15.15

为什么程序 15.9 的 `msprintf` 函数在 `malloc` 中使用了 `len`，在 `msgsnd` 中使用了 `len+1`？

答案：`vsnprintf` 函数返回格式化的字节数，不包括字符串终止符，因此我们需要额外的字节作为字符串终止符。`msmsg_t` 中已经包含一个。

程序 15.10 将消息队列的内容输出到标准输出，可以通过重定向保存到文件。`msgsave` 接收一个命令行参数并调用程序 15.9 的 `initqueue` 函数来访问队列。程序向标准输出输出队列内容，直到发生错误。程序 15.10 在完成后不会释放消息队列。

程序 15.11 从标准输入读取行并发送到消息队列。程序接收一个命令行参数并调用 `initqueue` 来访问相应的消息队列。程序 15.11 在开始拷贝之前发送一个包含进程 ID 的信息消息。你应该能够运行多个程序 15.11 以及单个程序 15.10。由于程序都没有自动移除功能，完成后请务必执行 `ipcrm` 命令。

## 示例 15.16

为什么程序 15.10 即使没有捕获任何信号，也使用了 `restart` 库中的 `r_write`？

答案：除了被信号中断外，`r_write` 会继续写入所有请求的字节。

## 示例 15.17

如何修改这些程序以便区分不同进程的消息？

答案：修改程序 15.9 中的函数，将进程 ID 作为消息类型发送。修改程序 15.10 输出消息的同时输出消息类型。

## 程序 15.10 msgsave.c

一个从消息队列拷贝消息到标准输出的程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/msg.h>
#include "msgqueue.h"
#include "restart.h"

#define MAXSIZE 4096

typedef struct {
    long mtype;
    char mtext[MAXSIZE];
} msmsg_t;

int main(int argc, char *argv[]) {
    int id;
    int key;
    msmsg_t mysmsg;
    int size;
    if (argc != 2) {
        fprintf(stderr, "Usage: %s key\n", argv[0]);
        return 1;
    }
    key = atoi(argv[1]);
    if ((id = initqueue(key)) == -1) {
        perror("Failed to initialize message queue");
        return 1;
    }
    for ( ; ; ) {
        if ((size = msgrcv(id, &mysmsg, MAXSIZE, 0, 0)) == -1) {
            perror("Failed to read message queue");
            break;
        }
        if (r_write(STDOUT_FILENO, mysmsg.mtext, size) == -1) {
            perror("Failed to write to standard output");
            break;
        }
    }
    return 1;
}
```

# 程序 15.11 msgqueuein.c

一个将标准输入发送到消息队列的程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/msg.h>
#include <unistd.h>
#include "msgqueue.h"
#include "restart.h"

#define MAXLINE 1024

int main(int argc, char *argv[]) {
    char buf[MAXLINE];
    int key;
    int size;
```

```c
if (argc != 2) {
    fprintf(stderr, "Usage: %s key\n", argv[0]);
    return 1;
}
key = atoi(argv[1]);
if (initqueue(key) == -1) {
    perror("Failed to initialize message queue");
    return 1;
}
if (msgrprintf("This is process %ld\n", (long)getpid()) == -1) {
    perror("Failed to write header to message queue");
    return 1;
}
for ( ; ; ) {
    if ((size = readline(STDIN_FILENO, buf, MAXLINE)) == -1) {
        perror("Failed to read from standard input");
        break;
    }
    if (msgrwrite(buf, size) == -1) {
        perror("Failed to write message to standard output");
        break;
    }
}
return 0;
```
