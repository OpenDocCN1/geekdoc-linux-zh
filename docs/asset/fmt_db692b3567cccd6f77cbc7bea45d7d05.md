
```c
/**
 * mkcq.c – 创建 SysV IPC 消息队列
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    int qid;         /* 队列标识符 */
    key_t key;      /* 队列键 */

    key = 123;

    /* 创建队列 */
    if((qid = msgget(key, IPC_CREAT | 0666)) < 0) {
        perror("msgget:create");
        exit(EXIT_FAILURE);
    }
    printf("created queue id = %d\n", qid);

    /* 再次打开队列 */
    if((qid = msgget(key, 0)) < 0) {
        perror("msgget:open");
        exit(EXIT_FAILURE);
    }
    printf("opened queue id = %d\n", qid);

    exit (EXIT_SUCCESS);
}
```

该程序在我的系统上产生的输出如下所示：

![](img/be588b36b489136ce784030a08a1d3d4_394_0.png)

### 输出

```
$ ./mkq
created queue id = 384
opened queue id = 384
```

如果第一个 `msgget` 调用成功，`mkq` 将显示新创建的队列 ID，然后第二次调用 `msgget`。如果第二个调用成功，`mkq` 也会报告这一点，但第二个调用只是打开现有队列，而不是创建新队列。注意，第一个调用使用标准八进制表示法指定了所有用户的读写权限。

> **注意**

> 与 `open` 函数的行为不同，创建 System V IPC 结构时，进程的 `umask` 不会修改结构的访问权限。如果你未设置访问权限，默认模式为 0，这意味着甚至结构的创建者都没有读或写访问权限！

### 向队列写入消息

如前所述，要向队列底部添加新消息，请使用 `msgsnd` 函数，其原型如下：

```
int msgsnd(int msgid, const void *ptr, size_t nbytes, int flags);
```

如果成功，`msgsnd` 返回 0；如果失败，它返回 -1 并将全局错误变量 `errno` 设置为以下值之一：

- `EAGAIN`

- `EACCES`

- `EFAULT`

- `EIDRM`

- `EINTR`

- `EINVAL`

- `ENOMEM`

> `errno` 值的值和解释列于表 6.1 “系统调用错误代码”，第 125 页。

`msgid` 参数必须是之前调用 `msgget` 返回的队列 ID。`nbytes` 是发布消息中的字节数，该消息不应以空字符结尾。`ptr` 是指向 `msgbuf` 结构的指针，该结构由消息类型和构成消息的数据字节组成。`msgbuf` 在 `<sys/msg.h>` 中定义如下：

```c
struct msgbuf {
    long mtype;
    char mtext[1];
};
```

这个结构声明实际上只是一个模板，因为 `mtext` 的大小必须调整为所存储数据的长度，这对应于传递给 `nbytes` 参数的值，减去任何终止空字符。`mtype` 可以是任何大于零的 `long` 整数。调用进程还必须对队列具有写访问权限。最后，`flags` 变量为 0 或 `IPC_NOWAIT`。`IPC_NOWAIT` 导致行为类似于传递给 `open` 系统调用的 `O_NONBLOCK` 标志：如果队列中单个消息的总数或队列的字节大小等于系统指定的限制，`msgsnd` 立即返回并将 `errno` 设置为 `EAGAIN`。因此，直到至少读取一个消息之前，你将无法向队列中添加更多消息。

如果 `flags` 为 0，并且队列中的最大消息数已达上限或已写入队列的数据总字节数已达上限，则 `msgsnd` 调用将阻塞（不返回），直到该条件清除为止。要清除该条件，必须从队列中读取消息，队列必须被删除（这将 `errno` 设置为 `EIDRM`），或者捕获信号且处理程序返回（这将 `errno` 设置为 `EINTR`）。

> **提示**

> 可以根据应用需求扩展 `msgbuf` 结构模板。例如，如果你想传递一个由整型和 10 字节字符数组组成的消息，只需按如下方式声明 `msgbuf`：

```c
struct msqbuf {
    long mtype;
    int i;
    char c[10];
};
```

`msqbuf` 只是一个 `long` 后跟消息数据，你可以按自己的意愿进行格式化。此示例中声明的结构大小为 `sizeof(msqbuf) – sizeof(long)`。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_396_0.png)

此程序 `qsnd` 向已存在的队列底部添加消息。将队列 ID 作为程序唯一的命令行参数传递。

```c
/*
 * qsnd.c - 向先前打开的队列发送消息
 */
#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

#define BUFSZ 512

struct msg {                        /* 消息结构 */
    long msg_type;
    char msg_text[BUFSZ];
};

int main(int argc, char *argv[])
{
    int qid;                        /* 队列标识符 */
    int len;                        /* 发送数据的长度 */
    struct msg pmsg;                /* 指向消息结构的指针 */

    /* 期望在命令行上传递队列 ID */
    if(argc != 2) {
        puts("USAGE: qsnd <queue ID>");
        exit(EXIT_FAILURE);
    }
    qid = atoi(argv[1]);

    /* 获取要添加到队列的消息 */
    puts("Enter message to post:");
    if(fgets(pmsg.msg_text, BUFSZ, stdin) == NULL) {
        puts("no message to post");
        exit(EXIT_SUCCESS);
    }

    /* 将消息与此进程关联 */
    pmsg.msg_type = getpid();
    /* 将消息添加到队列 */
    len = strlen(pmsg.msg_text);
    if(msgsnd(qid, &pmsg, len, 0) < 0) {
        perror("msgsnd");
        exit(EXIT_FAILURE);
    }
    puts("message posted");

    exit(EXIT_SUCCESS);
}
```

该程序的一次示例运行产生了以下输出。注意，该程序使用 `mkq` 返回的队列 ID。

### 输出

```
$ ./mkq
created queue id = 640
opened queue id = 640
$ ./qsnd 640
Enter message to post:
**this is test message number one**
message posted
```

回忆一下，第一个命令创建了一个队列 ID 为 640 的新队列。第二个命令 `qsnd 640` 提示输入要发布的消息

![](img/be588b36b489136ce784030a08a1d3d4_397_0.png)

将键入的响应（以**粗体**显示）直接存储到之前声明的 `msgstructure` 中。如果 `msgsnd` 成功完成，它会显示一条确认消息。请注意，`qsnd` 将消息类型设置为调用进程的 PID。这使得你稍后可以使用 `msgrcv` 仅检索该进程发布的那些消息。

### 读取排队消息

要从队列中拉取一条消息，请使用 `msgrcv`，其语法如下：
