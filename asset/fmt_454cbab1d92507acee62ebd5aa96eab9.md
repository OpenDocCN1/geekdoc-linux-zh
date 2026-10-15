
为了说明链表的使用，让我们实现一个示例。该示例还作为理解下一节中讨论的工作队列概念的基础。假设你的内核驱动程序需要从入口点执行一项繁重任务。一个例子是强制调用线程进入睡眠等待的任务。自然，你的驱动程序不希望阻塞直到任务完成，因为这会降低依赖它的应用的响应速度。因此，每当驱动程序需要执行这项昂贵的工作时，它通过将该例程添加到工作函数链表中来延迟执行。实际工作由内核线程执行，该线程遍历列表并在后台执行工作函数。驱动程序将工作函数提交到列表的尾部，而内核线程从列表头部开始处理，从而确保先排队的任务先完成。当然，驱动的其余部分需要设计得适合这种延迟执行方案。然而，在理解此示例之前，请注意我们将使用列表 3.5 中的工作队列接口以更简单的方式实现相同的任务。

首先让我们介绍示例中使用的关键驱动数据结构：

```c
static struct _mydrv_wq {
    struct list_head mydrv_worklist; /* 工作列表 */
    spinlock_t lock;                 /* 保护列表 */
    wait_queue_head_t todo;          /* 同步提交者
                                       和工作线程 */
} mydrv_wq;

struct _mydrv_work {
    struct list_head mydrv_workitem; /* 工作链 */
    void (*worker_func)(void *);      /* 要执行的工作 */
    void *worker_data;                /* worker_func 的参数 */
    /* ... */                          /* 其他字段 */
} mydrv_work;
```

`mydrv_wq` 对于所有工作提交都是全局的。其成员包括指向工作列表头的指针，以及一个用于提交工作的驱动函数和执行工作的内核线程之间通信的等待队列。列表辅助函数不保护对列表成员的访问，因此你需要使用并发机制来串行化同时的指针引用。这是通过自旋锁完成的，自旋锁也是 `mydrv_wq` 的一部分。驱动程序初始化例程 `mydrv_init()`（见列表 3.2）初始化自旋锁、链表头和等待队列，并启动工作线程。

### 列表 3.2. 初始化数据结构

```c
static int __init
mydrv_init(void)
{
    /* 初始化锁以保护免受
       并发列表访问 */
    spin_lock_init(&mydrv_wq.lock);

    /* 初始化等待队列以便提交者
       和工作线程之间通信 */
    init_waitqueue_head(&mydrv_wq.todo);

    /* 初始化链表头 */
    INIT_LIST_HEAD(&mydrv_wq.mydrv_worklist);

    /* 启动工作线程。参见列表 3.4 */
    kernel_thread(mydrv_worker, NULL,
                CLONE_FS | CLONE_FILES | CLONE_SIGHAND | SIGCHLD);
    return 0;
}
```

在检查执行已提交工作的工作线程之前，让我们看看工作提交流程本身。列表 3.3 实现了一个函数，内核的其他部分可以使用它来提交工作。它使用 `list_add_tail()` 将工作函数添加到列表的尾部。查看图 3.1 以了解工作列表的物理结构。

图 3.1. 工作函数链表。

![](img/07cc6f9c8c74622020874f66bfb53dc4_74_0.png)

### 列表 3.3. 提交稍后执行的工作

```c
int
submit_work(void (*func)(void *data), void *data)
{
    struct _mydrv_work *mydrv_work;

    /* Allocate the work structure */
    mydrv_work = kmalloc(sizeof(struct _mydrv_work), GFP_ATOMIC);
    if (!mydrv_work) return -1;

    /* Populate the work structure */
    mydrv_work->worker_func = func; /* Work function */
    mydrv_work->worker_data = data; /* Argument to pass */
    spin_lock(&mydrv_wq.lock);     /* Protect the list */

    /* Add your work to the tail of the list */
    list_add_tail(&mydrv_work->mydrv_workitem,
                  &mydrv_wq.mydrv_worklist);

    /* Wake up the worker thread */
    wake_up(&mydrv_wq.todo);

    spin_unlock(&mydrv_wq.lock);
    return 0;
}
```

要从驱动程序入口点提交工作函数 `void job(void *)`，请执行以下操作：

```c
submit_work(job, NULL);
```

提交工作函数后，代码列表 3.3 会唤醒工作线程。代码列表 3.4 中展示的工作线程通用结构与上一节讨论的标准内核线程类似。该线程使用 `list_entry()` 遍历列表中的所有节点。`list_entry()` 返回嵌入列表节点内部的容器数据结构。请仔细查看代码列表 3.4 中的相关代码行：

```c
mydrv_work = list_entry(mydrv_wq.mydrv_worklist.next,
                        struct _mydrv_work, mydrv_workitem);
```

`mydrv_workitem` 嵌入在 `mydrv_work` 内部，因此 `list_entry()` 返回指向相应 `mydrv_work` 结构的指针。传递给 `list_entry()` 的参数分别是嵌入的列表节点地址、容器结构的类型以及嵌入列表节点的字段名。

执行已提交的工作函数后，工作线程使用 `list_del()` 将相应节点从列表中移除。请注意，在已提交的工作函数执行期间，`mydrv_wq.lock` 会被释放并重新获取。这是因为工作函数可能会进入睡眠状态，如果新调度的代码试图获取同一个自旋锁，可能会导致潜在的死锁。

### 代码列表 3.4：工作线程
