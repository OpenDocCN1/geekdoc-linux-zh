
```c
                continue;

            }

            else {

                errno = ENOMSG;

                EC_FAIL

            }

        }

        else

            break;

    }

    if (p->sq_entity == SMI_SERVER)

        p->sq_msg->smi_client.c_idl = fd;

    return true;

EC_CLEANUP_BGN

    return false;

EC_CLEANUP_END

}
```

最后一个函数完全不需要做任何工作：

```c
bool smi_receive_release_skt(SMIQ *sqp)
{
    return true;
}
```

使用这种 `SMI` 实现方式，第 7 章中所有关于消息发送的示例都能在套接字上运行。我们在 7.15 节中已经将其性能与其他 `IPC` 方法进行了比较。

请注意，我们的 `SMI` 示例是为机器内部 `IPC` 设计的，使用的是普通的服务器名称。这意味着当名称进入 `ssi_open` 时，会被视为属于 `AF_UNIX` 域。你也可以同样轻松地使用 `SMI` 接口进行 `AF_INET` 域的消息传递（在机器之间），尽管如果你的名称是这样写的——以两个斜杠开头——那么只有 `SMI` 的套接字实现才能工作。

## 8.6 无连接套接字

到目前为止，我们所有的示例和 `SSI` 的实现都使用了 `SOCK_STREAM` 类型的已连接套接字。有一个调用 `listen` 和 `accept` 的服务器，以及一个或多个连接到该服务器的客户端。连接会保持打开状态，直到一方或另一方关闭它。

相比之下，无连接套接字不使用连接，因此不会调用 `listen` 和 `accept`。发送方指定它想要发送到的地址。接收方指定它想要接收到的地址，或者它从任何人处接收数据并被告知发送方的地址。接收方始终需要将自己 `bind` 到一个外部名称，因为这是发送方唯一能联系到它们的方式。因此，无连接套接字比已连接的套接字更具对称性；可能存在客户端/服务器关系，但有时将参与者视为对等方（`peers`）更有用。

### 8.6.1 关于数据报

无连接通信使用数据报（`datagrams`），它们是包含目标地址的独立数据块。系统不会尝试保持数据报的顺序，也没有任何保证它们一定会到达。相比之下，`SOCK_STREAM` 既保证顺序也保证到达。可以将数据报想象成一封邮寄信件或电子邮件，将 `SOCK_STREAM` 想象成电话通话。

在许多应用中，顺序和到达的不确定性并不重要。例如，假设应用程序用于预订图书馆书籍。屏幕上有一个表单，提交时会向图书馆服务器发送一个数据报，服务器则回复一个确认信息。如果两个预订请求相差一秒左右，重新排序数据报或许有点不公平，但由于读者彼此不知道对方的活动，因此不会有投诉。在极少数数据报根本未到达的情况下，读者将不会收到确认信息，并会再次提交表单。因此，在此应用中，使用数据报比仅为预订一本书而建立连接然后立即断开连接要高效得多。另一方面，如果读者打算交互式地浏览一段时间的书目目录，那么建立连接可能是最佳选择。

图 8.4 展示了两个对等方互相向对方的套接字发送数据报。请将其与图 8.1 进行对比，后者展示的是已连接的套接字。监听和接受的符号消失了，并且两个套接字都绑定到名称上，而不仅仅是服务器的套接字。

![](img/41b4c8f6d6a5c349eee321a301703d97_582_0.png)

### 8.6.2 sendto 和 recvfrom 系统调用

在我们之前的所有套接字示例中，我们使用 `write`（或 `writeall`）向套接字发送数据，这之所以有效，是因为我们有一个代表连接写入端的文件描述符。但是，如果套接字未连接，我们只有一个属于我们自己套接字的文件描述符；我们需要将目标指定为套接字地址，而不是文件描述符。因此，`write` 行不通。我们需要另一个名为 `sendto` 的系统调用，它接受一个套接字地址：

```c
sendto—send message to socket

#include <sys/socket.h>

ssize_t sendto(
    int socket_fd,             /* socket file descriptor */
    const void *message,        /* message to send */
    size_t length,             /* length of message */
    int flags,                 /* flags */
    const struct sockaddr *sa, /* target address */
    socklen_t sa_len           /* length of target address */
);  /* Returns number of bytes sent or -1 on error (sets errno) */
```

参数 `socket_fd` 是发送方的套接字；接收方通过参数 `sa` 和 `sa_len` 指定。`sendto` 成功返回并不意味着消息已到达，仅表示未检测到任何本地错误。

你的实现可能会定义一些标志，但唯一重要的可移植标志是 `MSG_OOB`，它发送带外（紧急）数据；参见 8.7 节。

对于无连接套接字，长度为 `length` 字节的消息被视为不可分割的数据报。如果套接字通道已满，`sendto` 通常会阻塞，直到所有数据

将容纳；如果设置了 `O_NONBLOCK` 标志且数据无法容纳，则不会发送任何数据，返回 `−1`，并将 `errno` 设置为 `EAGAIN` 或 `EWOULDBLOCK`。

你可以在已连接的套接字上使用 `sendto`，但在这种情况下，目标套接字地址会被忽略，输出将直接发往 `socket_fd` 套接字，这与 `write` 的行为完全一致。相较于 `write` 的唯一优势是你可以指定标志，但如果只是需要这一点，直接使用 `send`（参见第 8.9.1 节）会更直观。

现在我们展示一个示例，该示例实现了图 8.4 所示的功能，并额外增加了每个对端读取传入数据的逻辑。对端 2 接收到消息后，对其进行少量修改，然后发送回给对端 1。对端 1 组装四条消息发送给对端 2，并显示收到的回复。注意，与已连接套接字的示例不同，这里两个对端都执行了 `bind`，且都没有调用 `listen`、`accept` 或 `connect`。

```c
#define SOCKETNAME1 "SktOne"

#define SOCKETNAME2 "SktTwo"

#define MSG_SIZE 100

int main(void)
{
    struct sockaddr_un sa1, sa2;

    strcpy(sa1.sun_path, SOCKETNAME1);

    sa1.sun_family = AF_UNIX;

    strcpy(sa2.sun_path, SOCKETNAME2);

    sa2.sun_family = AF_UNIX;

    (void)unlink(SOCKETNAME1);

    (void)unlink(SOCKETNAME2);

    if (fork() == 0) { /* 对端 1 */
    int fd_skt;

    size_t nread;

    char msg[MSG_SIZE];

    int i;

    sleep(1); /* 让对端 2 先启动 */

    ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
    ec_neg1( bind(fd_skt, (struct sockaddr *)&sa1, sizeof(sa1)) )
    for (i = 1; i <= 4; i++) {
        snprintf(msg, sizeof(msg), "Message #%d", i);

        ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
        (struct sockaddr *)&sa2, sizeof(sa2)) )

        ec_neg1( nread = read(fd_skt, msg, sizeof(msg)) )

        if (nread != sizeof(msg)) {
            printf("对端 1 收到短消息\n");

            break;

        }

    }

    printf("收到 \"%s\" 的回复\n", msg);

        }

        ec_neg1( close(fd_skt) )

        exit(EXIT_SUCCESS);
    }

    else { /* 对端 2 */

        int fd_skt;

        size_t nread;

        char msg[MSG_SIZE];

        ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )

        ec_neg1( bind(fd_skt, (struct sockaddr *)&sa2, sizeof(sa2) ) )

        ec_neg1( nread = read(fd_skt, msg, sizeof(msg)) )

        while (true) {
            if (nread != sizeof(msg)) {
                printf("对端 2 收到短消息\n");

                break;

            }

            msg[0] = 'm';

            ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
                     (struct sockaddr *)&sa1, sizeof(sa1)) )

            ec_neg1( close(fd_skt) )

            exit(EXIT_SUCCESS);
        }

    }

    EC_CLEANUP_BGN

        exit(EXIT_FAILURE);

    EC_CLEANUP_END
}
```

将两个进程放在同一个程序中并非常规做法；我们这样做只是为了简化示例。然而，我们不得不在子进程（对端 1）的开头插入对 `sleep` 的调用，以便让对端 2 先运行。虽然这不是控制执行顺序的最佳方式，但对于我们当前的目的来说是可行的。在实际应用中，确保服务器先于客户端启动通常不是问题。如果确实存在此问题，正确的同步方法见第 9.2 节。

输出如下：

```
收到 "message #1" 的回复

收到 "message #2" 的回复

收到 "message #3" 的回复

收到 "message #4" 的回复
```

对于数据报而言，`read` 并不是一个很好的选择，因为它无法告知我们数据是谁发送的。这对已连接套接字来说不是问题，因为每次从 `accept` 返回时都会为每个客户端提供一个单独的文件描述符，我们既可以对其进行 `read` 也可以进行 `write`。在刚才给出的示例中，对端 2 只是假定应该使用 `sendto` 发送给对端 1，但通常来说，应用程序比这要复杂得多。

确实，存在与 `sendto` 相反的操作，称为 `recvfrom`：

```c
recvfrom—从套接字接收消息

#include <sys/socket.h>

ssize_t recvfrom(
  int socket_fd,                /* 套接字文件描述符 */
  void *buffer,                 /* 接收消息的缓冲区 */
  size_t length,                /* 缓冲区长度 */
  int flags,                    /* 标志 */
  struct sockaddr *sa,          /* 发送方地址 */
  socklen_t *sa_len            /* 地址长度 */
);

/* 返回接收的字节数、0 或 -1（出错时设置 errno） */
```

`recvfrom` 的前三个参数与 `read` 类似。此外，它还包含一个 `flags` 参数以及两个用于接收发送方套接字地址的参数。

在调用之前，你必须将 `sa` 设置为足以容纳发送方套接字地址的值，并将 `sa_len` 设置为该存储空间的大小。返回时，`sa_len` 会被设置为地址的实际大小。然后，如果你愿意，可以直接将 `sa` 和 `sa_len` 传递给 `sendto` 以进行回复。

与 `sendto` 类似，`recvfrom` 对于无连接套接字总是返回完整的消息。如果 `O_NONBLOCK` 未设置，它将等待接收；如果已设置，则返回 `−1`，并将 `errno` 设置为 `EAGAIN` 或 `EWOULDBLOCK`。

如果你想知道源地址，也可以使用 `recvfrom` 配合已连接的套接字，但正如之前解释的那样，在调用 `sendto` 时该地址会被忽略，因此你无法用它做太多事情。获取文件描述符对应套接字地址的另一种方法是调用 `get-sockname`（参见第 8.9.2 节）。

以下是你可以与 `recvfrom` 一起使用的三个可移植标志：

| 标志 | 描述 |
| :--- | :--- |
| `MSG_OOB` | 接收带外数据（如果有）；参见第 8.7 节。 |
| `MSG_PEEK` | 返回消息，但保留该消息未读，供下一次 `read`、`recvfrom` 或其他输入操作使用。 |
| `MSG_WAITALL` | 仅适用于已连接套接字，使 `recvfrom` 阻塞直到请求的完整长度可用，除非同时设置了 `MSG_PEEK`，或者调用被信号、连接终止或错误中断。对无连接套接字无效，因为消息总是不可分割的。 |

以下是重构后的示例，它使用 `recvfrom`，并包含多个对端向同一套接字发送数据，因此采用客户端/服务器架构：

```c
#define SOCKETNAME_SERVER "SktOne"

#define SOCKETNAME_CLIENT "SktTwo"

static struct sockaddr_un sa_server;

#define MSG_SIZE 100

static void run_client(int nclient)
{
    struct sockaddr_un sa_client;

    int fd_skt;

    ssize_t nrecv;

    char msg[MSG_SIZE];

    int i;

    if (fork() == 0) {  /* 客户端 */
    sleep(1);  /* 让服务器先启动 */

    ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )

    snprintf(sa_client.sun_path, sizeof(sa_client.sun_path),
        "%s-%d", SOCKETNAME_CLIENT, nclient);

    (void)unlink(sa_client.sun_path);

    sa_client.sun_family = AF_UNIX;

    ec_neg1( bind(fd_skt, (struct sockaddr *)sa_client,
        sizeof(sa_client)) )

    for (i = 1; i <= 4; i++) {
    snprintf(msg, sizeof(msg), "Message #%d", i);

    ec_neg1( sendto(fd_skt, msg, sizeof(msg), 0,
        (struct sockaddr *)sa_server, sizeof(sa_server)) )

    ec_neg1( nrecv = read(fd_skt, msg, sizeof(msg)) )
    if (nrecv != sizeof(msg)) {
        printf("客户端收到短消息\n");

        break;
    }

    printf("收到 \"%s\" 的回复\n", msg);
    }

    ec_neg1( close(fd_skt) )
    exit(EXIT_SUCCESS);
    }

return;

EC_CLEANUP_BGN

  exit(EXIT_FAILURE);

EC_CLEANUP_END
}

static void run_server(void)
{
  int fd_skt;
  ssize_t nrecv;
  char msg[MSG_SIZE];
  struct sockaddr_storage sa;
  socklen_t sa_len;
  ec_neg1( fd_skt = socket(AF_UNIX, SOCK_DGRAM, 0) )
  ec_neg1( bind(fd_skt, (struct sockaddr *)&sa_server, sizeof(sa_server)) )
  while (true) {
    sa_len = sizeof(sa);
    ec_neg1( nrecv = recvfrom(fd_skt, msg, sizeof(msg), 0,
