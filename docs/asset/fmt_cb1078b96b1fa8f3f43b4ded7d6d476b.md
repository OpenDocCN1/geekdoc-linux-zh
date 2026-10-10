
```c
static int clients_find(SMIQ_FIFO *p, pid_t pid)
{
    int i, avail = -1;

    for (i = 0; i < MAX_CLIENTS; i++) {
        if (p->sq_clients[i].cl_pid == pid)
            return i;
        if (p->sq_clients[i].cl_fd == -1 && avail == -1)
            avail = i;
    }
    if (avail != -1)
        p->sq_clients[avail].cl_pid = pid;
    return avail;
}
```

如果没有更多客户端可以处理，此函数返回 -1。

最后的内部函数用于创建 FIFO 名称。服务器的名称是固定的，而客户端的包含其进程 ID，正如第 7.2.2 节中较早的示例所示。

```c
static void make_fifo_name_server(const SMIQ_FIFO *p, char *fifo_name,
                                  size_t fifoname_max)
{
    snprintf(fifo_name, fifoname_max, "/tmp/smiq_fifo-%s", p->sq_name);
}

static void make_fifo_name_client(pid_t pid, char *fifo_name,
                                  size_t fifoname_max)
{
    snprintf(fifo_name, fifoname_max, "/tmp/smiq_fifo%d", (long)pid);
}
```

现在我们准备好查看 `smi_open_fifo`：

```c
SMIQ *smi_open_fifo(const char *name, SMIENTITY entity, size_t msgsize)
{
    SMIQ_FIFO *p = NULL;
    char fifoname[SERVER_NAME_MAX + 50];

    ec_null( p = calloc(1, sizeof(SMIQ_FIFO)) )
    p->sq_msgsize = msgsize + offsetof(struct smi_msg, smi_data);
    ec_null( p->sq_msg = calloc(1, p->sq_msgsize) )
    p->sq_entity = entity;
```

## 7.3 (来自代码的隐式上下文)

```c
if (strlen(name) >= SERVER_NAME_MAX) {
    errno = ENAMETOOLONG;
    EC_FAIL
}
strcpy(p->sq_name, name);
make_fifo_name_server(p, fifoName, sizeof(fifoName));
if (p->sq_entity == SMII_SERVER) {
    client5_bgp(p);
    if (mkfifo(fifoName, PERM_FILE) == -1 && errno != EEXIST)
        EC_FAIL
    ec_negI( p->sq_fd_server = open(fifoName, O_RDONLY) )
    ec_negl( p->sq_fd_server_w = open(fifoName, O_WRONLY) )
} else {
    ec_negI( p->sq_fd_server = open(fifoName, O_WRONLY) )
    make_fifo_name_client(getpid(), fifoName, sizeof(fifoName));
    (void)unlink(fifoName);
    ec_negI( mkfifo(fifoName, PERM_FILE) )
    ec_negl( p->sq_clients[0].cl_fd =
             open(fifoName, O_RDONLY | O_NONBLOCK) )
    ec_false( setblock(p->sq_clients[0].cl_fd, true) )
    ec_negI( p->sq_clients[1].cl_fd = open(fifoName, O_WRONLY) )
}
return (SMIq *)p;

EC_CLEANUP_BGN
if (p != NULL) {
    free(p->sq_msg);
    free(p);
}
return NULL;
EC_CLEANUP_END
```

如果你已经理解了第 7.2.2 节中的示例，这段代码应该是易于理解的。但实际打开 FIFO 的部分值得回顾一下。对于服务器，打开其 FIFO 的顺序是：

```c
ec_negI( p->sq_fd_server = open(fifoName, O_RDONLY) )
ec_negl( p->sq_fd_server_w = open(fifoName, O_WRONLY) )
```

如果没有写入者，第一个调用将阻塞，这是没问题的，因为没有写入者时服务器本来也就没有什么事可做。然而，客户端打开其 FIFO 的顺序更复杂：

```c
ec_negI( p->sq_clients[0].cl_fd =
         open(fifoName, O_RDONLY | O_NONBLOCK) )
ec_false( setblock(p->sq_clients[0].cl_fd, true) )
ec_negI( p->sq_clients[1].cl_fd = open(fifoName, O_WRONLY) )
```

如果没有 `O_NONBLOCK` 标志，客户端在打开时会阻塞，等待服务器为写入而打开 FIFO。但是，除非服务器收到消息，否则它不会这样做，因为只有那时它才知道这个特定客户端的存在。这就导致了死锁！解决方案，如代码所示，是以非阻塞方式打开 FIFO，这意味着它会返回一个有效的文件描述符，而无需等待写入者。然后我们必须清除 `O_NONBLOCK` 标志（即设置为阻塞模式），以便后续的读取操作会阻塞，这是我们期望的行为。（`setblock` 使用 `fcntl` 系统调用，来自于第 4.2.2 节。）在第 7.2.2 节的示例中，我们不需要这样做，因为客户端只有在向服务器发送消息之后才打开自己的 FIFO。在这里行不通，因为 SMI 函数是独立的，有特定的任务要完成。（有时模块化需要额外的工作。）

这里是配套的 `smi_close_fifo` 函数：

```c
bool smi_close_fifo(SMIO *sqp)
{
    SMIO_FIFO *p = (SMIO_FIFO *)sqp;

    clients_end(p);
    (void)close(p->sq_fd_server);
    if (p->sq_entity == SMI_CLIENT) {
        char filename[SERVER_NAME_MAX + 50];

        make_fifo_name_client(getpid(), filename, sizeof(filename));
        (void)unlink(filename);
    }
    else
        (void)close(p->sq_fd_server_w);
    free(p->sq_msg);
    free(p);
    return true;
}
```

注意客户端会删除其 FIFO，但服务器保留其 FIFO，以便将来可以在服务器未运行的情况下启动客户端。

这里是 `smi_send_getaddr_fifo`，除了保存客户端 ID 并返回缓冲区地址外，它几乎什么也不做：

```c
bool smi_send_getaddr_fifo(SMIO *sqp, struct client_id *client,
               void **addr)
{
    SMIO_FIFO *p = (SMIO_FIFO *)sqp;
    if (p->sq_entry == SMI_SERVER)
        p->sq_client = *client;
    *addr = p->sq_msg;
    return true;
}
```

真正的工作在 `smi_send_release_fifo` 中：

```c
bool smi_send_release_fifo(SMIO *sqp)
{
   SMIO_FIFO *p = (SMIO_FIFO *)sqp;
   ssize_t nwrite;

   if (p->sq_entry == SMI_SERVER) {
      int nclient = clients_find(p, p->sq_client.c_idl);
      if (nclient == -1 || p->sq_clients[nclient].cl_fd == -1) {
         errno = EADDRNOTAVAIL;
         EC_FAIL
      }
      ec_neg1( nwrite = write(p->sq_clients[nclient].cl_fd, p->sq_msg,
         p->sq_msgsize) )
   }
   else {
      p->sq_msg->smi_client.c_idl = (long)getpid();
      ec_neg1( nwrite = write(p->sq_fd_server, p->sq_msg,
         p->sq_msgsize) )
   }
   return true;

   EC_CLEANUP_BGN
      return false;
   EC_CLEANUP_END
}
```

这里没有什么特别之处，这些内容在第 7.2.2 节的早期示例中已经出现过。`smi_receive_getaddr_fifo` 完成了接收消息的所有工作：

```c
bool smi_receive_getaddr_fifo(SMIO *sqp, void **addr)
{
   SMIO_FIFO *p = (SMIO_FIFO *)sqp;
   ssize_t nread;

   if (p->sq_entry == SMI_SERVER) {
      int nclient;
      char ffname[SERVER_NAME_MAX + 5];

      while (true) {
         ec_neg1( nread = read(p->sq_fd_server, p->sq_msg,
            p->sq_msgsize) )
         if (nread == 0) {
            errno = ENETDOWN;
            EC_FAIL
         }
         if (nread < offsetof(struct smi_msg, smi_data)) {
            errno = EBIG;
            EC_FAIL
         }
         if ((nclient = clients_find(p,
            (pid_t)p->sq_msg->smi_client.c_idl)) == -1) {
            continue; /* 客户端未被通知 */
         }
         if (p->sq_clients[nclient].cl_fd == -1) {
            make_fifo_name_client((pid_t)p->sq_msg->smi_client.c_idl,
            fifo_name, sizeof(fifo_name));
            ec_negl(p->sq_clients[nclient].cl_fd =
            open(fifo_name, O_WRONLY))
         }
         break;
      }
   } else
      ec_negl( nread = read(p->sq_clients[0].cl_fd, p->sq_msg,
      p->sq_msgsizes) )
   *addr = p->sq_msg;
   return true;

   EC_CLEANUP_BGN
   return false;
   EC_CLEANUP_END
}
```

这里棘手的一个部分是：

```c
if ((nclient = clients_find(p, (pid_t)mp->smi_client)) == -1) (
    continue; /* 客户端未被通知 */
)
```

如果 `clients_find` 返回 −1，这意味着服务器从客户端收到了消息，但无法在 `sq_clients` 数组中获取一个槽位，因此无法打开响应 FIFO。由于无法响应，甚至无法发送错误消息。示例代码直接忽略了错误，让客户端保持阻塞状态。一些替代方案包括：

- 向客户端发送信号，并修改 `smi_open_fifo` 以安排捕获该信号。
- 使用一个整型变量保存用于打开 FIFO 的紧急文件描述符，以便可以发送错误消息。
- 至少修改客户端，使其超时而不是永远保持阻塞状态。

剩下一个函数，但它根本不需要做任何事情：

```c
bool smi_receive_release_fifo(SMIQ *scp)
{
    return true;
}
```

这就是整个实现。即使存在我所讨论的局限性，它仍然是一个可移植性高、可靠性合理的 SMI 函数实现，你可以立即在自己的应用程序中开始使用它，至少用于原型设计。以后，你可以使用其他实现，因为接口是相同的。

## 7.4 System V IPC (进程间通信)

如第 1.1.7 节所述，用于消息、信号量和共享内存的系统调用有两组。较旧的一组通常称为 System V IPC，而较新的一组称为 POSIX IPC。本章将讨论这两者，首先是 System V 和 POSIX 消息，然后是两种类型的信号量，最后是共享内存。本节解释适用于所有 System V IPC 机制的一些通用概念；稍后，在第 7.6 节中，将解释通用的 POSIX IPC 概念。

### 7.4.1 System V IPC 对象

System V IPC 对象有三种类型：消息队列、信号量集和共享内存段。它们不是文件——甚至不是特殊文件——而是拥有自己的命名方案、生命周期规则和权限系统的对象。以下是 System V IPC 对象的主要特征：

- 它们仅存在于单个机器内。不能用于跨网络通信。
- 它们的寿命与内核相同——重启时会被销毁。
- 你使用一个在对象生命周期内固定的整数标识符来访问对象。知道该标识符的任何进程都可以直接使用它来访问对象——无需先打开对象。这与文件描述符不同，文件描述符是进程的属性，当进程结束时就会消失。（System V IPC 也有键，我将在下一节解释。）
- 没有 i 节点（i-nodes）或路径名，因此传统的文件和目录操作系统调用，如 `unlink`、`stat`、`read` 或 `write` 均无法使用。

这三种对象都有形式为 Xget 和 Xctl 的系统调用，其中 X 为 msg、sem 或 shm。因此，这六个调用分别是 `msgget`、`semget`、`shmget`、`msgctl`、`semctl` 和 `shmctl`。当讨论内容适用于这三种对象时，我将继续使用术语 Xget 和 Xctl 来指代“get”和“ctl”调用。

只剩下另外五个调用：用于发送和接收消息的 `msgsnd` 和 `msgrcv`，用于操作信号量集的 `semop`，以及用于附加和分离共享内存段的 `shmat` 和 `shmdt`。

## 7.4.2 标识符、键和 ftok 系统调用

当创建 System V IPC 对象时，内核会分配一个标识符，因此通常情况下，该标识符的值在每次重启后都会不同。为了方便不同的进程获取它们需要共享的对象的标识符，还存在永久的 `keys`，其值永远不会改变。进程可以在使用 Xget 创建对象时指定一个键，或者如果对象已经存在，直接使用 Xget 通过键获取标识符。然而，键并不能真正识别特定对象，就像路径名识别文件那样，因为对象的生命周期仅持续到下一次重启。下次，相同的键将用于生成一个新的对象，该对象可能具有不同的标识符。

键的类型为 `key_t`，虽然各种系统调用将其用作算术类型，但该类型并不一定要求是算术类型，因此这是一个安全的假设。如果需要，你完全可以像下面这样为程序定义键值：

```c
#define MSGQ_KEY    1234
#define SEM_KEY     1235
#define SHM_KEY1    1236
#define SHM_KEY2    1237
```

然后，任何使用 `MSGQ_KEY` 作为参数调用 `msgget` 的进程都将获得指向同一消息队列的标识符。

使用键的问题是，需要一种全球性的管理方案来分配它们，以避免应用程序之间出现冲突。这显然是不可行的，因此另一层抽象允许通过 `ftok` 系统调用从路径名生成键。

`ftok`—生成 System V IPC 键
