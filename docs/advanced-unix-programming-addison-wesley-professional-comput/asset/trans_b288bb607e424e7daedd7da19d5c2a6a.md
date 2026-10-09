
else {
    errno = ENOTSUP;
    EC_FAIL
}

EC_CLEANUP_BGN
    return -1;
EC_CLEANUP_END
}

另外两个函数非常琐碎：

```c
int ssi_get_server_fd(SSI *ssip)
{
    return ssip->ssi_fd;
}
```

```c
bool ssi_close_fd(SSI *ssip, int fd)
{
    EC_negII (close (fd) );
    FD_CLR(fd, &ssip->ssi_fd_set);
    reset_fd_hwim(ssip, fd);
    return true;

    EC_CLEANUP_BGN
        return false;
    EC_CLEANUP_END
}
```

这就是完整的实现。对于已连接的套接字（`SOCK_STREAM`），我们在后续的示例中都不必再使用任何原始系统调用。

## 8.5 SMI 的套接字实现

将第 7 章中介绍的简单消息接口（SMI）实现为使用套接字，并据此将其与那里展示的其他五种实现方式进行对比，这很有趣。我们将使用前一节中的 SSI 函数，而不是直接调用各种与套接字相关的系统调用，因此这项任务相当简单。

本节假设你非常熟悉第 7 章及其中的 SMI 实现；如果不熟悉，请跳过本节，直到你有时间读完第 7 章——否则读起来会很难理解。

对于套接字来说，内部结构体 `SMIQ_SKT` 很简单，这主要是因为其他实现方式所承担的记录客户端的工作，在这种情况下是由 `accept` 系统调用完成的，而且我们已经有了 SSI 来处理许多细节：

```c
typedef struct { /* entity */
    SMIENTITY sq_entity;
    SSI *sq_ssi; /* structure for SSI */
    struct client_id sq_client; /* client ID */
    size_t sq_msgsize; /* msg size */
    struct smi_msg *sq_msg; /* msg buffer */
} SMIQ_SKT;
```

打开 `SMIQ_SKT` 的工作不多，因为 `ssi_open` 承担了大部分工作：

```c
SMIQ *smi_open_skt (const char *name, SMIENTITY entity, size_t msgsize)
{
    SMIQ_SKT *p = NULL;

    ec_null ( p = calloc (1, sizeof (SMIQ_SKT)))
    p->sq_msgsize = msgsize + offsetof (struct smi_msg, smi_data);
    ec_null ( p->sq_msg = calloc (1, p->sq_msgsize))
    p->sq_entity = entity;
    ec_null ( p->sq_ssi = ssi_open (name, entity == SMI_SERVER))
    return (SMIQ *)p;

EC_CLEANUP_BGN
    (void) smi_close_skt ((SMIQ *)p);
    return NULL;
EC_CLEANUP_END
}
```

关闭过程也是如此：

```c
bool smi_close_skt (SMIQ *sqp)
{
    SMIQ_SKT *p = (SMIQ_SKT *)sqp;
    SSI *ssip;

    if (p != NULL) {
        ssip = p->sq_ssi;
        free (p->sq_msg);
        free (p);
        if (ssip != NULL)
            ec_false ( ssi_close (ssip))
    }

    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

正如我们在第 7 章中看到的其他几种实现方式，`smi_send_getaddr_skt` 所要做的全部工作就是，如果由服务器调用，则保存 `client_id`，并返回消息地址：

```c
bool smi_send_getaddr_skt(SMIQ *sqp, struct client_id *client,
void **addr)
{
    SMIQ_SKT *p = (SMIQ_SKT *)sqp;

    if (p->sq_entity == SMI_SERVER)
        p->sq_client = *client;
    *addr = p->sq_msg;
    return true;
}
```

`smi_send_release_skt` 将消息（使用 2.9 节中的 `writeall`）写入客户端的文件描述符（如果来自服务器），或者写入服务器套接字文件描述符（如果来自客户端）：

```c
bool smi_send_release_skt(SMIQ *sqp)
{
    SMIQ_SKT *p = (SMIQ_SKT *)sqp;
    int fd;

    if (p->sq_entity == SMI_SERVER)
        ec_negl( fd = p->sq_client.c_idl )
    else
        ec_negl( fd = ssi_get_server_fd(p->sq_ssi) )
    ec_negl( writeall(fd, p->sq_msg, p->sq_msgsize) )
    return true;

EC_CLEANUP_BGN
    return false;
EC_CLEANUP_END
}
```

对于服务器而言，服务器接收消息意味着必须等待一个就绪的文件描述符，SSI 通过 `ssi_wait_server` 为我们处理了这一点。服务器还必须将就绪的文件描述符保存在消息的 `client_id` 部分，以便调用者（服务器）知道该回复谁。客户端所做的只需调用 `ssi_get_server_fd` 来获取服务器的套接字文件描述符：

```c
bool smi_receive_getaddr_skt(SMIQ *sqp, void **addr)
{
    SMIQ_SKT *p = (SMIQ_SKT *)sqp;
    size_t /*nremain,*/ nread;
    int fd;

    *addr = p->sq_msg;
    while (true) {
        if (p->sq_entity == SMI_SERVER)
            ec_neg1( fd = ssi_wait_server(p->sq_ssi) )
        else
            ec_neg1( fd = ssi_get_server_fd(p->sq_ssi) )
        ec_neg1( nread = readall(fd, p->sq_msg, p->sq_msgsize) )
        if (nread == 0) {
            if (p->sq_entity == SMI_SERVER) {
                ec_false( ssi_close_fd(p->sq_ssi, fd) )
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

使用这种 SMI 实现方式，第 7 章中所有关于消息发送的示例都能在套接字上运行。我们在 7.15 节中已经将其性能与其他 IPC 方法进行了比较。

请注意，我们的 SMI 示例是为机器内部 IPC 设计的，使用的是普通的服务器名称。这意味着当名称进入 `ssi_open` 时，会被视为属于 `AF_UNIX` 域。你也可以同样轻松地使用 SMI 接口进行 `AF_INET` 域的消息传递（在机器之间），尽管如果你的名称是这样写的——以两个斜杠开头——那么只有 SMI 的套接字实现才能工作。

## 8.6 无连接套接字

到目前为止，我们所有的示例和 SSI 的实现都使用了 `SOCK_STREAM` 类型的已连接套接字。有一个调用 `listen` 和 `accept` 的服务器，以及一个或多个连接到该服务器的客户端。连接会保持打开状态，直到一方或另一方关闭它。

相比之下，无连接套接字不使用连接，因此不会调用 `listen` 和 `accept`。发送方指定它想要发送到的地址。接收方指定它想要接收到的地址，或者它从任何人处接收数据并被告知发送方的地址。接收方始终需要将自己 `bind` 到一个外部名称，因为这是发送方唯一能联系到它们的方式。因此，无连接套接字比已连接的套接字更具对称性；可能存在客户端/服务器关系，但有时将参与者视为对等方（peers）更有用。

### 8.6.1 关于数据报

无连接通信使用数据报（datagrams），它们是包含目标地址的独立数据块。系统不会尝试保持数据报的顺序，也没有任何保证它们一定会到达。相比之下，`SOCK_STREAM` 既保证顺序也保证到达。可以将数据报想象成一封邮寄信件或电子邮件，将 `SOCK_STREAM` 想象成电话通话。

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

