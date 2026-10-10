
```c
static pid_t my_pid;

SMIQ *smi_open_mq(const char *name, SMIENTITY entity, size_t msgsize)
{
    SMIQ_MQ *p = NULL;
    char mqname[SERVER_NAME_MAX + 100];
    struct mq_attr attr = {0};

    my_pid = getpid();
    ec_null( p = calloc(1, sizeof(SMIQ_MQ)) )
    p->sq_msgsize = msgsize + offsetof(struct smi_msg, smi_data);
    ec_null( p->sq_msg = calloc(1, p->sq_msgsize) )
    p->sq_entity = entity;
    p->sq_mqd_server = p->sq_clients[0].cl_mqd = (mqd_t)-1;
    if (strlen(name) >= SERVER_NAME_MAX) {
        errno = ENAMETOOLONG;
        EC_FAIL
    }
    strcpy(p->sq_name, name);
    make_mq_name_server(p, mqname, sizeof(mqname));
    attr.mq_maxmsg = 100;
    attr.mq_msgsize = p->sq_msgsize;
    if (p->sq_entity == SMI_SERVER) {
        (void)mq_unlink(mqname);
        ec_cmp( errno, ENOSYS )
        ec_neg1( p->sq_mqd_server = mq_open(mqname, O_RDONLY | O_CREAT,
                PERM_FILE, &attr) )
    } else {
        ec_neg1( p->sq_mqd_server = mq_open(mqname, O_WRONLY) )
        make_mq_name_client(my_pid, mqname, sizeof(mqname));
        ec_neg1( p->sq_clients[0].cl_mqd = mq_open(mqname,
                O_RDONLY | O_CREAT, PERM_FILE, &attr) )
    }
    return (SMIQ *)p;

EC_CLEANUP_BGN
    if (p != NULL)
        (void)smi_close_mq((SMIQ *)p);
    return NULL;
EC_CLEANUP_END
}
```

在初始化内部 SMI 队列之后，我们使用队列中 100 条消息的限制和作为第三个参数传入的消息大小来初始化 `mq_attr` 结构体。然后，如果我们是服务器，我们将丢弃任何现有的服务器队列并创建一个全新的队列。我们不为客户端执行此操作，尽管我们可能应该这样做，因为客户端的进程 ID 嵌入在队列名称中，不太可能被重用。

关闭函数如下所示，执行预期的操作：

```c
bool smi_close_mq(SMIQ *sqp)
{
    SMIQ_MQ *p = (SMIQ_MQ *)sqp;
    char msqname[SERVER_NAME_MAX + 100];

    if (p->sq_entity == SMI_SERVER) {
        make_mq_name_server(p, msqname, sizeof(msqname));
        (void)mq_close(p->sq_mqd_server);
        (void)mq_unlink(msqname);
    }
    else {
        make_mq_name_client(my_pid, msqname, sizeof(msqname));
        (void)mq_close(p->sq_mqd_server);
        (void)mq_unlink(msqname);
    }

    free(p->sq_msg);
    free(p);
    return true;
}
```

接下来是 `smi_send_getaddr_mq` 和 `smi_send_release_mq`：

```c
bool smi_send_getaddr_mq(SMIQ *sqp, struct client_id *client,
    void **addr)
{
    SMIQ_MQ *p = (SMIQ_MQ *)sqp;

    if (p->sq_entity == SMI_SERVER)
        p->sq_client = *client;
    *addr = p->sq_msg;
    return true;
}

bool smi_send_release_mq(SMIQ *sqp)
{
    SMIQ_MQ *p = (SMIQ_MQ *)sqp;
    mqd_t mqd_receiver;

    if (p->sq_entity == SMI_SERVER)
        ec_negl( mqd_receiver = get_client_mqd(p, p->sq_client.c_id) )
    else {
        mqd_receiver = p->sq_mqd_server;
        p->sq_msg->smi_client.c_id = my_pid;
    }
    ec_negl( mq_send(mqd_receiver, (const char *)p->sq_msg,
        p->sq_msgsize, 0) )
    return true;

    EC_CLEANUP_BGN
        return false;
    EC_CLEANUP_END
}
```

像之前对 FIFO 和 System V 消息队列一样，`smi_send_getaddr_mq` 只是保存客户端 ID（如果从服务器调用）并返回缓冲区地址。真正的工作在 `smi_send_release_mq` 中。服务器调用查找函数 `get_client_mqd` 获取消息队列描述符。它的参数由 `smi_send_getaddr_mq` 保存在 `SMIQ_MQ` 结构中。

客户端已经拥有服务器的描述符，并将它的进程 ID 放入消息中。（消息队列描述符不能像 System V 消息队列标识符那样在进程之间传递。）

接收对更简单，因为接收者已经拥有其消息队列的描述符：

```c
bool smi_receive_getaddr_mq(SMIQ *sqp, void **addr)
{
    SMIQ_MQ *p = (SMIQ_MQ *)sqp;
    mqd_t mqd_receiver;
    ssize_t nrcv;

    if (p->sq_entity == SMI_SERVER)
        mqd_receiver = p->sq_mqd_server;
    else
        mqd_receiver = p->sq_clients[0].cl_mqd;

    ec_negl( nrcv = mq_receive(mqd_receiver, (char *)p->sq_msg,
        p->sq_msgsize, NULL) )
    *addr = p->sq_msg;
    return true;

    EC_CLEANUP_BGN
        return false;
    EC_CLEANUP_END
}
```

```c
bool smi_receive_release_mq(SMIQ *sqp)
{
    return true;
}
```

## 7.7.3 对 POSIX 消息队列的批评

POSIX 消息队列系统调用比 System V 调用具有稍微更干净的接口，并且更好地集成到 UNIX 的其他部分中，但它们仍然使用自己的描述符而不是文件描述符，因此不能使用 `select` 和 `poll`。作为补偿，有一个通知功能，但使用起来非常棘手，因为我们将在第 9 章中看到，因为它基于信号，而信号总是很难使用。

POSIX 消息队列的主要问题（实际上所有 POSIX IPC 都是）是它没有广泛可用，但当然，这不属于对设计的批评。

表 7.1 更详细地比较了 POSIX 和 System V 消息队列：

**表 7.1** POSIX 与 System V 消息队列

| 标准 | POSIX | System V |
| :--- | :--- | :--- |
| 标准化了吗？ | 是 | 是 |
| 在 UNIX 认证系统中是强制的吗？ | 否 | 是 |
| 在所有主要 UNIX 系统中可用吗？ | 否 | 是 |
| 消息限制？ | 非常少；可设置 | 很多；只有一个可设置；难以管理 |
| 线程安全（根据 SUS3）？ | 是 | 是 |
| 消息优先级？ | 是 | 是 |
| 接收非最高优先级消息？ | 否 | 是 |
| 通知？ | 是 | 否 |

## 表 7.1 POSIX 与 System V 消息队列。（续）

| 标准 | POSIX | System V |
| :--- | :--- | :--- |
| 是否使用文件描述符？ | 否 | 否 |
| 效率如何？ | 取决于实现 | 取决于实现 |
| 每条消息有两个用户-内核副本吗？¹ | 是 | 是 |
| 队列名称的可移植性问题？ | 有 | 无 |

¹ 这意味着数据从用户空间复制到内核空间，或反之。

尽管有这些优缺点混杂的情况，为什么 POSIX 实时小组在 System V 消息已经存在了超过 10 年之久时，还要发明一种新的消息系统？而且，既然他们确实这么做了，为什么结果并不更好呢？

以下是我的回答：

- 虽然 POSIX 小组对现有的 System V 方法确实有很多不满，但他们需要新标准的主要原因是，许多主要系统已经拥有一个不适合实时应用的 System V 实现，而在同一接口下同时拥有两个实现是非常困难的。他们需要一种方式让实现者能够重新开始。

- 但是，在 POSIX 流程内没有实际的方法要求任何特定的性能水平，因此对于许多系统（如果不是大多数系统）来说，两种消息队列（如果确实存在两种的话）的效率大致相同。

- POSIX IPC 名称的可移植性问题是由规范不足造成的，这是为了允许广泛的实现所必需的，包括速度极快的内存队列，而不需要进行任何文件系统查找。

- POSIX 小组对实现缺失并不负责。很可能最负责任的方面是，到 20 世纪 90 年代中期，许多（如果不是大多数）应用程序开发者都专注于网络应用，他们使用套接字（第 8 章）来处理这些应用，而对处理非网络消息的替代方式兴趣不大。因此，像 Sun 这样资金雄厚的机构实现了 POSIX 选项包，而像 BSD 和 Linux 社区这样较小的机构则发现了更紧迫的事情去做。

### 7.8 关于信号量

本节解释信号量的一般特性，并展示如何使用文件和消息来实现它们。System V 和 POSIX 信号量系统调用将在第 7.9 节和第 7.10 节中介绍。

### 7.8.1 信号量的基本用法

我们在第 5.17.3 节中已经遇到过互斥锁。更一般地说，信号量是一个计数器，用于防止两个或多个进程或线程同时访问共享资源。然而，它仅仅是建议性的：如果一个进程或线程在访问共享资源之前不检查信号量，可能会导致混乱。

在 UNIX 中，“信号量”一词通常指由信号量系统调用操纵以同步进程的对象。“互斥锁”一词通常指一种轻量级的对象，用于同步线程，这正是我们在第 5.17.3 节中讨论的内容。在本节中，我将只讨论信号量。

二进制信号量只有两种状态：锁定和解锁。通用信号量有无限（或至少非常大）数量的状态。它是一个计数器，当获取它（“锁定”）时减 1，当释放它（“解锁”）时加 1。如果它是零，试图获取它的进程必须等待另一个进程增加其值——它永远不能变为负数。（如果一个信号量只能取两个值 0 和 1，那么它就是一个二进制信号量。）通用信号量通常通过两个操作来访问，我们可以抽象地称之为 `semwait` 和 `sempost`（有时也称为 P 和 V）。我们可以尝试用 C 语言编写这些代码：

```c
void semwait(int *sem)
{
    while (*sem <= 0)
        ; /* do nothing */
    (*sem)--;
}

void sempost(int *sem)
{
    (*sem)++;
}
```

> P 和 V 是 E. W. Dijkstra 用来表示荷兰语短语 *proberen te verlagen*（“尝试减少”）和单词 *verhogen*（“增加”）的缩写。有些书说 P 代表 *prolagen*，但这不是一个词，即使在荷兰语中也不是。它是完整短语的缩写。

信号量必须通过调用 `sempost` 进行初始化；否则，它初始时没有内容可以获取。例如，如果信号量计数的是空闲缓冲区数量，且初始时有五个缓冲区，我们需要先调用五次 `sempost`。或者，我们可以直接将信号量变量设置为五。

既然费心编程实现了 `semwait` 和 `sempost`，我现在必须指出它们无法正常工作，原因有三：

- 由 `sem` 指向的信号量变量通常不在进程之间共享，因为进程拥有不同的数据段。（尽管它可以在共享内存中。）

- 这些函数不是原子执行的——内核可以在任何时候中断进程。可能会发生以下场景：进程 1 完成了 `semwait` 中的 `while` 循环，但在递减信号量之前被中断；进程 2 进入 `semwait`，发现信号量等于 1，完成其 `while` 循环并将信号量减为 0；进程 1 恢复执行并将信号量减为 –1（非法值）。

- 如果 `sem` 为零，`semwait` 会执行所谓的忙等待。这是一种愚蠢的 CPU 使用方式。

因此，`semwait` 和 `sempost` 不能仅在用户空间中编程。信号量必须由内核提供，内核可以进程间共享数据，可以执行原子操作，并且当进程阻塞时可以将 CPU 交给就绪进程。

### 7.8.2 使用文件和消息实现信号量

在第 2.4.3 节中，我展示了如何使用 `open` 制作一个简单的二进制信号量。这种方法对于只访问共享资源几次的进程来说是合适的，例如正在写入邮件箱文件的电子邮件程序，但对于高强度使用来说开销太大。我们希望有一种信号量，其检查和设置所需的时间更短。

消息队列也可以用作信号量：发送操作向队列添加一条消息，等效于 `sempost`；接收操作从队列移除一条消息，等效于 `semwait`。当队列为空时，接收操作会阻塞，这等效于信号量为零。

然而，任何支持消息的 UNIX 系统（System V 或 POSIX 种类）也都独立地支持信号量，且效率更高。

## 7.9 System V 信号量

System V 和 POSIX 信号量都不使用像 `semwait` 和 `sempost` 这样简单的机制。它们的系统调用更复杂，尽管 POSIX 信号量复杂得并不多。我将在第 7.10.3 节中一起批评这两种机制。

我将从 System V 开始。这些系统调用太复杂，我无法完全描述。不过，我会确保解释得足够多，以便我们能够实现 `semwait` 和 `sempost`；其余部分，请参阅系统的文档或 [SUS2002]。

第 7.4 节中的信息适用于这些系统调用，因此我们无需专门讨论密钥、标识符、所有权等。

System V 信号量机制有趣的地方在于，系统调用不仅操作单个信号量，而且一次操作整个数组。通过一次原子操作，你可以对几个信号量执行 `semwait`，并对另外几个执行 `sempost`。在实践是否你真的想要这样做是值得商榷的，但如果你需要，它是存在的。在大多数示例中，我们将一次只操作一个信号量，尽管我们稍后会使用一组两个信号量，只是为了方便。

在我们继续之前，有一个评论：System V 信号量太复杂了！在任何使用信号量的程序中，都必须能够证明对共享资源的访问是排他的，不会发生死锁，也不会发生饥饿（永远无法获得访问权）。仅靠测试通常是不够的，因为事情非常依赖时序；必须使用分析。对于普通的 `semwait` 和 `sempost` 来说，这已经足够困难了。使用 System V 系统调用并充分发挥其功能时，分析可能是不可能的。

### 7.9.1 System V 信号量系统调用

与 System V 消息队列一样，你从 `X_get` 调用开始：

**semget**—获取信号量集标识符

```c
#include <sys/sem.h>

int semget(
    key_t key,        /* Key */
    int nsems,        /* size of set */
    int flags          /* flags */
);
/* Returns identifier or -1 on error (sets errno) */
```

不出所料，`semget` 将 `key` 转换为表示一组信号量的 ID。如果 `flags` 中的 `IPC_CREAT` 位被置位，若该组尚不存在，则会被创建。该组中包含 `nsems` 个信号量，编号从零开始。

信号量并不能立即使用——必须通过调用 `semctl` 对其进行初始化。为什么 `semget` 不将它们初始化为零是个谜，但 SUS 并没有要求这样做，[^7] 而且许多实现也不这样做。以下是 `semctl` 的说明：

```c
semctl—control semaphore set

#include <sys/sem.h>
int semctl(
 int semid, /* identifier */
 int semnum, /* semaphore number */
 int cmd, /* command */
 union semun arg /* argument for command */
);
/* Returns value or 0 on success; -1 on error (sets errno) */
```
