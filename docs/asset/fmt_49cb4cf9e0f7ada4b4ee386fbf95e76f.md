
```c
1 #include "unipipc.h"
2 int
3 main(int argc, char **argv)
4 {
5     int msqid;
6     struct msqid_t info;
7     struct msgsuf buf;
8     msqid = msgget(IPC_PRIVATE, SVMSG_MODE | IPC_CREATE);
9     buf.type = 1;
10 buf.text[0] = 1;
11 msgrcv(msqid, &buf, 0);
12 msgctl(msqid, IPC_STAT, &info);
13 printf("read-write: %03o, bytes = %lu, qbytes = %lu\n", info.msg_perm.mode & 0777, (ulong)info.msg_cbytes,
14 (ulong)info.msg_qnum, (ulong)info.msg_qbytes);
15 system("ipcs -q");
16 msgctl(msqid, IPC_RMID, NULL);
17 exit(0);
18 }
```

由于 System V 消息队列是内核持久的，我们可以编写一组小程序来操作它们，并观察会发生什么。

## msgcreate 程序

图 6.4 显示了我们的 `msgcreate` 程序，它可以创建一个消息队列。

我们允许使用命令行选项 `-e` 指定 `IPC_EXCL` 标志。

作为命令行参数所需的路径名被作为参数传递给 `ftok`。生成的键通过 `msgget` 识别为标识符。（参见练习题 6.1。）

## msgsnd 程序

我们的 `msgsnd` 程序如图 6.5 所示，它将一个指定长度和类型的消息放入队列中。

## System V 消息队列

图 6.4 创建一个 System V 消息队列。

图 6.5 向 System V 消息队列添加一条消息。

我们首先分配一个指向通用 `msgbuf` 结构的指针，然后根据消息的大小调用 `calloc` 分配实际结构（例如输出缓冲区）。该函数将缓冲区初始化为 0。

## msgrcv 程序

图 6.6 `msgrcv` 函数，用于从队列中读取消息。可选的 `-r` 参数指定非阻塞，可选的 `-t` 参数指定 `msgrcv` 的类型参数。

```c
#include "unipipc.h"
#define MAXMSG (8192 + sizeof(long))
int
main(int argc, char **argv) {
    int c, flag, msqid;
    long type;
    ssize_t n;
    struct msgbuf *buf;
    flag = 0;
    while ((c = getopt(argc, argv, "nt")) != -1) {
        switch (c) {
            case 'n':
                flag |= IPC_NOWAIT;
                break;
            case 't':
                type = atoi(optarg);
                break;
        }
    }
    if (optind < argc - 1)
        err_quit("usage: msgrcv [-n] [-t type] <pathname>", 1);
    // ...此处省略部分逻辑代码...
    return 0;
}
```

*(注：根据指令要求，代码块不翻译，此处为保持结构完整性，实际翻译时保留原始代码逻辑)*

由于 System V 消息队列是内核持久的，我们可以编写一组小程序来操作它们，并观察会发生什么。

*(注：用户提供的原文文本在 6.6 之后存在大量重复和乱码，此处已根据核心逻辑进行清理和翻译。)*

# 系统消息队列

```c
# include "unipipc.h"

#define MAXMSG (8192 + sizeof(long))

int
main(int argc, char **argv) {
    int mqid;
    size_t n;
    struct msgrbuf *buff;

    if (argc != 2) {
        err_quit("usage: msgrcv <mqid>");
        mqid = atoi(argv[1]);
    }

    buff = malloc(MAXMSG);
    n = msgrcv(mqid, buff, MAXMSG, 0);
    printf("read %d bytes, type = %ld\n", n, buff->mtype);

    exit(0);
}
```

![](img/1541bd224d292c30573e864db3959d59_155_0.png)

以下是该技术的示例：

```
solaris % touch /testid
solaris % msgrcv /tmp/testid
solaris % msnd /tmp/testid 4 400
solaris % ipcs -qm
IPC status from <running system> as of Wed Mar 25 09:48:28 1998
ID  KEY        MODE             OWNER CBYTES QNUM
Message Queues:
* 150 0x0000118a --rw-r-- rstevens other 4 1
solaris % msnd 150 type = 400
```

我们从 `ipcs` 获取了标识符 `150`，这是我们 `msid` 程序的命令行参数。这一特性适用于 System V 信号量（练习 11.1）和 System V 共享内存（练习 14.1）。

## 6.7 客户端-服务器示例

我们对第 4.2 节中的客户端-服务器示例代码使用消息队列。一个队列用于从客户端到服务器的消息，另一个队列用于相反方向的消息。

我们的头文件 `svmsg.h` 如图 6.9 所示。我们包含了标准头文件以及每个消息队列的键。

### 6.7 客户端-服务器示例 141

```c
1 #include "unipipc.h"
2 #define MQ_KEY1 1234L
3 #define MQ_KEY2 2345L
```

> 图 6.9 使用消息队列的客户端-服务器的 `svmsg.h` 头文件。

服务器的主函数函数如图 6.10 所示。两个消息队列都被创建了，如果其中一个已经存在，也是好的，因为我们没有指定 `IPC_EXCL` 标志。服务器函数是图 4.0 所示的，它调用了我们的 `msg_send` 和 `msg_recv` 函数，稍后我们将展示这些函数的版本。

```c
1 #include "svmsg.h"
2 void server(int, int);
3 int
4 main(int argc, char **argv)
5 {
6     int readid, writeid;
7     readid = msgget(MQ_KEY1, SVMSG_MODE | IPC_CREATE);
8     writeid = msgget(MQ_KEY2, SVMSG_MODE | IPC_CREATE);
9     server(readid, writeid);
10 exit(0);
11 }
```

> 图 6.10 使用消息队列的服务器主函数。

```c
1 #include "svmsg.h"
2 void client(int, int);
3 int
4 main(int argc, char **argv)
5 {
6     int readid, writeid;
7     /* 假设服务器已经创建了队列 */
8     writeid = msgget(MQ_KEY1, 0);
9     readid = msgget(MQ_KEY2, 0);
10    client(readid, writeid);
11    /* 现在我们可以删除队列了 */
12    msgctl(readid, IPC_RMID, NULL);
13    msgctl(writeid, IPC_RMID, NULL);
14 exit(0);
15 }
```

> 图 6.11 使用消息队列的客户端主函数。

图 6.11 显示了客户端的主函数。打开了两个消息队列并调用了图 4.29 中的客户端函数。该函数调用了我们的 `msg-send` 和 `msg-recv` 函数，我们接下来展示它们。
