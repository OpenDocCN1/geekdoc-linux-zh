
# 5.18 阻塞问题

我们已经遇到了几种可能会阻塞的系统调用，例如 `read`、`write`、`pthread_cond_wait` 和 `waitpid`，而且书中还有更多，特别是在第 7 章和第 8 章中。UNIX 编程中最难的问题之一是你的应用程序可能需要阻塞在多个系统调用上，因为你不知道接下来会发生什么。我称之为**阻塞问题**。

对于接受文件描述符的阻塞系统调用，比如 `read` 和 `write`，你可以使用单个系统调用 `select` 或 `poll`（第 4.2 节）来阻塞，直到一个或多个文件描述符就绪。但这在通常情况下并没有帮助，因为你要等待的许多事情，例如进程、信号、消息、信号量和条件变量，并不与文件描述符相关联。是的，你可以通过写入一个专门为此目的建立的管道来通知阻塞在 `select` 或 `poll` 上的线程，比如说当消息到达时（我们将在下一节看到），但这无助于解决 `msgrcv` 或 `mq_receive` 本身正在阻塞等待消息这一事实。没有方法将消息等待系统调用直接关联到文件描述符。这不是一个通知问题，而是一个阻塞问题。

## 5.18.1 使用进程和线程的解决方案

从历史上看，解决阻塞问题的方法是创建一个子进程来进行阻塞。²⁴ 当它所阻塞的对象解除阻塞时，它随后会写入管道，向父进程指示已发生某个事件。管道是一个很好的选择，因为它们容易设置（我们将在下一章看到），并且由于它们使用文件描述符，父进程可以将它们整合到 `select` 或 `poll` 中。这在实质上是将父进程从阻塞在非文件描述符事件上转换为阻塞在文件描述符上。转换一切，在父进程中使用 `select` 或 `poll`，你就成功啦。

但在 UNIX 中，进程是非常重量级的对象——创建成本高，调度成本高，且数量有限。此外，两个进程共享相同的数据结构也很麻烦。如果事件发生时能够先将其排队，然后父进程在方便时再检查，那就太好了。使用共享内存和信号量在进程间设置事件队列是可行的，但进程间信号量可能太慢，特别是当事件发生得非常快时。

使用独立进程的另一个问题是，某些对象，如文件描述符，无法传递给现有进程（至少在可移植性方面不行）。它们只能通过继承来传递；因此，如果进程 `A` 负责阻塞 I/O 并且已经在运行，刚刚打开网络连接进程 `B` 无法让进程 `A` 等待新获得的文件描述符。

解决阻塞问题的较新方案是使用 POSIX 线程。一种简单的方法是为每个你想阻塞的对象（例如，消息队列、文件描述符集合、信号量）创建一个新线程。每个线程只是发出适当的阻塞系统调用（`O_NONBLOCK` 清除）。当系统调用返回时，线程向共享队列中添加一个事件（使用互斥锁进行保护），然后立即回到阻塞系统调用中。然后主线程只需要阻塞在一件事上：队列中是否存在事件。阻塞线程使用条件变量在队列变为非空时向主线程发出信号，正如第 5.17.4 节中的示例所示。

## 5.18.2 统一事件管理器原型

我将展示一种使用线程解决阻塞问题的通用方法，我称之为**统一事件管理器**（Unified Event Manager）。它是一组库函数，任何应用程序都可以使用。应用程序可以注册一个事件，这会导致库创建阻塞的线程。应用程序围绕等待单一事件队列组织。当事件出现时，应用程序将其从队列中取出，处理它，然后返回等待。

我不会在书中展示所有代码，但如果你想看，它就在网站上。它是一个原型，因为它对关键应用来说效率不够高，并且它使用了本书所有示例都使用的 `ec` 错误检查方法，而这本身也是一个原型。

我们从一个枚举开始，它涵盖了 UNIX 中几乎所有可等待的事件：

```c
enum UEM_TYPE { /* System V message */ UEM_SVMSG, /* POSIX message */ UEM_PXMSG, /* System V semaphore */ UEM_SVSEM, /* POSIX semaphore */ UEM_PXSEM, /* file-descriptor set -- read */ UEM_FD_READ,
                /* file-descriptor set - write */ UEM_FD_WRITE,
                /* file-descriptor set - error */ UEM_FD_ERROR,
                /* signal */ UEM_SIG,
                /* process */ UEM_PROCESS,
                /* heartbeat */ UEM_HEARTBEAT,
                /* none */ UEM_NONE
};
```

最后两个需要一些解释：`UEM_HEARTBEAT` 是一种以特定间隔获取定期事件的方式，而 `UEM_NONE` 在那里，因为拥有一个可以用来指示某物为空的值总是个好主意。

当我们注册一个事件时，我们需要一个结构来跟踪阻塞系统调用所需的信息。例如，为了发出 `select`，我们需要文件描述符集合，所以这个结构为每个 `UEM_TYPE` 持有这种类型的所有数据：

```c
struct uem_reg {
    enum UEM_TYPE ur_type;          /* type of registration */
    pthread_t ur_tid;               /* thread ID */
    union {
        int ur_mqid;                /* System V message-queue ID */
        struct {
            int s_semid;            /* System V semaphore-set ID */
            struct sembuf *s_sops;  /* semaphore operations */
        } ur_svsem;
#ifndef POSIX_IPC
        mqd_t ur_mqd;               /* POSIX message-queue descriptor */
        sem_t *ur_sem;             /* POSIX semaphore */
#endif
        int ur_signum;              /* signal number */
        pid_t ur_pid;               /* process ID */
        long ur_usecs;              /* microseconds (for heartbeat) */
        fd_set ur_fdset;            /* file-descriptor set */
    } ur_resource;
    void *ur_data;                 /* data to be queued with event */
    size_t ur_size;                 /* size (used for various purposes) */
};
```

宏 `POSIX_IPC` 不是一个标准宏，而是我们在这个原型中使用的宏。它是从真正的特性测试宏中非常复杂地设置的，这在第 1.5.4 节中有解释。我们需要它，因为 Linux 和 FreeBSD 尚未支持 POSIX IPC。

当应用程序想要注册事件类型时，它调用形式为 `uem_register_E` 的函数，其中 `E` 是事件类型的缩写。例如，这里是注册等待进程终止的调用：

```c
ec_false( uem_register_process(pid, NULL) )
```

这是直接发出 `waitpid` 的替代方案，后者会阻塞。当进程 `pid` 终止时，包含其退出状态的事件将被放入队列，注册该事件的应用程序随后可以获取状态。我们很快就会看到这些细节。

以下是 `uem_register_process` 的代码：

```c
bool uem_register_process(pid_t pid, void *data)
{
	struct uem_reg *p;
	ec_null( p = new_reg() )
	p->ur_type = UEM_PROCESS;
	p->ur_resource.ur_pid = pid;
	p->ur_size = 0;
	p->ur_data = data;
	ec_rv( pthread_create(&p->ur_tid, NULL, thread_process, p) )
	return true;

EC_CLEANUP_BGN
	return false;
EC_CLEANUP_END
}
```

函数 `new_reg`，被所有的 `uem_register_E` 调用使用，只是分配一个结构。我们把它放在一个单独的函数中，以防有共同的初始化工作要做，但在当前设计中并没有。

```c
static struct uem_reg *new_reg(void)
{
	struct uem_reg *p;
	ec_null( p = calloc(1, sizeof(struct uem_reg)) )
	return p;

EC_CLEANUP_BGN
	return NULL;
EC_CLEANUP_END
}
```

注册信息只是传递给线程函数，它看起来像这样：

```c
static void *thread_process(void *arg)
{
	struct uem_event *e = NULL;

	pthread_cleanup_push(cleanup_handler, e);
	ec_null( e = calloc(1, sizeof(struct uem_event)) )
```

> 24. 这项技术大约由我母亲在 1953 年发明。在杂货店里，她会让一个孩子排在熟食柜台，另一个孩子排在鱼柜台，而她自己则购买那些不需要排队的商品。偶尔她也会遇到阻塞，不过，她于是又生了三个孩子。

该函数首先推入一个清理处理器（如 5.17.5 节所述）。然后，它分配一个事件结构体，以便当事件发生时（在此情况下为 `waitpid` 返回）将其加入队列。以下是所有线程使用的该事件结构体：

```c
struct uem_event {
    struct uem_reg *ue_reg;
    void *ue_buf;
    ssize_t ue_result;
    int ue_errno;
    struct uem_event *ue_next;
};
```

请注意，它指回注册结构体，后者包含该类所有事件的公共数据。`ue_buf` 成员用于需要返回数据的情况（例如消息），但在此案例中并无此类数据。我们确实有状态信息，并将其放入 `ue_result` 成员中。如果发生错误，`errno` 将存入 `ue_errno` 成员；接收该事件的应用程序需要将该成员与零进行比较，以检查等待该事件的函数是否返回了错误。`ue_next` 成员的存在使得 `uem_event` 结构体能够链接成事件队列。

该清理处理器与 5.17.5 节中的类似，除了它会调用 `uem_free`（此处未展示）来释放已分配的事件结构体：

```c
static void cleanup_handler(void *arg)
{
    (void)uem_free((struct uem_event *)arg);
}
```

从队列中移除事件的应用程序也负责调用 `uem_free`。

将事件放入队列的实际工作由 `queue_event` 完成，线程在 `waitpid` 返回时调用它。请注意，即使 `waitpid` 报告了错误，事件仍会被加入队列，这正是应用程序了解此类错误的方式。

```c
static pthread_mutex_t uem_mtx = PTHREAD_MUTEX_INITIALIZER;
static pthread_cond_t uem_cond_event = PTHREAD_COND_INITIALIZER;
static struct uem_event *event_head = NULL;

static bool queue_event(struct uem_event *e)
{
    struct uem_event *cur;

    ec_rv( pthread_mutex_lock(&uem_mtx) )
    if (event_head == NULL)
        event_head = e;
    else {
        for (cur = event_head; cur->ue_next != NULL; cur = cur->ue_next)
            /* 同一错误只入队一次 */
            if (e->ue_errno != 0 &&
                cur->ue_reg->ur_type == e->ue_reg->ur_type &&
                cur->ue_errno == e->ue_errno) {
                ec_rv( pthread_mutex_unlock(&uem_mtx) )
                uem_free(e);
                return true;
            }
        cur->ue_next = e;
    }
    ec_rv( pthread_cond_signal(&uem_cond_event) )
    ec_rv( pthread_mutex_unlock(&uem_mtx) )
    return true;

EC_CLEANUP_BGN
    (void)pthread_mutex_unlock(&uem_mtx);
    return false;
EC_CLEANUP_END
}
```

此函数遵循 5.17.4 节中关于使用条件变量发出事件信号的模式。然而，如果调用 `queue_event` 的线程持续收到错误，则可能会重复生成错误事件（`ue_errno` 非零）。例如，如果传递给 `waitpid` 的进程 ID 无效，`waitpid` 将一直返回，直到线程被取消。这本身已经浪费了 CPU 时间，但我们更不希望事件队列中填满成千上万报告相同内容的事件。因此，在将错误事件入队之前，我们确保队列中尚未存在与其完全相同的事件。（这可能不是最佳方法，但这只是一个原型，对吧？）

如果事件需要入队，语句 `cur->ue_next = e;` 将其加入队列，随后我们发出条件信号，解锁互斥锁并返回。基本上这就是整个库的内容，只是有一组注册函数（如 `uem_register_process`），由于它们所做的几乎相同，仅在阻塞的系统调用上有所不同，故此处不再展示。也就是说，`uem_register_svmsg` 启动一个包含 `msgrcv` 调用的线程，`uem_register_pxmsg` 启动一个包含 `mq_receive` 调用的线程，等等。它们都使用 `queue_event`。

使用该库的应用程序看起来类似于这样：

```c
struct uem_event *e;
...
ec_false( uem_register_process(pid, NULL) )
ec_false( uem_register_pxmsg(mqd, NULL) )
...
while (true) {
    ec_null( e = uem_wait() )
    if (e->ue_errno != 0)
        ... /* 显示错误 */
    else
        switch (e->ue_reg->ur_type) {
            case UEM_PXMSG:
                ... /* 处理接收到的消息 */
                break;
            case UEM_PROCESS:
                ... /* 处理来自已终止进程的状态 */
                break;
            ...
        }
}
```

这里最重要的是，无论需要处理多少种不同类型的事件，应用程序都只在一个地方阻塞，即对 `uem_wait` 的调用。以下是 `uem_wait` 的代码；请注意，与 `queue_event` 一样，它遵循 5.17.4 节中的条件变量模式：

```c
struct uem_event *uem_wait(void)
{
    struct uem_event *e = NULL;

    ec_rv( pthread_mutex_lock(&uem_mtx) )
    while (event_head == NULL)
        ec_rv( pthread_cond_wait(&uem_cond_event, &uem_mtx) )
    e = event_head;
    event_head = event_head->ue_next;
    ec_rv( pthread_mutex_unlock(&uem_mtx) )
    return e;

EC_CLEANUP_BGN
    (void)pthread_mutex_unlock(&uem_mtx);
    return NULL;
EC_CLEANUP_END
}
```

当谓词为真（即队列中存在事件）时，它从队列中移除该事件并返回指向该事件的指针。调用者有责任通过调用 `uem_free` 来释放内存，正如我之前提到的。

除了一些额外的记录细节和其余的注册函数外，这就是整个系统了。它解决了阻塞问题！

由于高度依赖线程，这种方法的好坏取决于底层线程实现。线程必须快速、轻量且充足，并且必须严格遵循 POSIX 标准。否则，开销将过大，宝贵的系统资源将被消耗，并且应用程序中会出现许多细微的 bug，由于多线程的原因，这些 bug 将非常难以查找。
