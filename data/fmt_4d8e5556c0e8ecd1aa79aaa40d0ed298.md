
# 第 18 章

你的驱动程序可以提供这些函数的组合，以便向内核表示设备的功能。可用函数如下表所示。

| 函数 | 描述 |
| :--- | :--- |
| `lseek` | `lseek` 在用户空间视角下更改位置。具体来说，它会修改 `file->pos`；我们稍后会讨论。成功时返回新位置，失败则用负值标识。 |
| `read` | `read` 从应用程序视角看，将数据写回用户空间。返回值为正表示读取的字节数。负值表示错误。 |
| `write` | `write` 将数据馈给设备，返回值与 `read` 相同。 |
| `readdir` | `readdir` 严格用于文件系统查找目录内容 |
| `poll` | `poll` 允许应用程序获取设备事件通知；BSD UNIX 中的 `select` 在 Linux 中已废弃，应该使用 `poll`。 |
| `ioctl` | `ioctl` 或 I/O 控制允许应用程序通过 `ioctl` 系统调用控制设备行为或从设备获取数据。 |
| `mmap` | `mmap` 实现设备地址空间到用户空间的映射。这可以用于直接访问内部缓冲区或外围设备内存空间。 |
| `open` | `open` 在应用程序打开设备时被调用。这是唯一对字符和块设备都有默认实现的函数，如果你不需要知道设备何时打开，可以留空不定义。 |
| `flush` | `flush` 自然地刷新缓冲区数据。由于字符设备没有缓冲区，此项仅对块设备有意义。 |
| `release` | `release` 在设备关闭时被调用。 |
| `fsync` | `fsync` 同步内存状态与设备状态，写入输出缓冲区中的脏数据。在完成之前不能返回。此项仅与块设备相关。 |
| `async` | `async` 在应用程序通过 `fcntl` 设备行为时被调用。 |
| `lock` | `lock` 允许用户锁定文件——仅对文件系统真正有意义。 |
| `readv` | `readv` 根据 `iovec` 描述的缓冲区向量从设备读取数据。 |

| 方法 | 描述 |
| :--- | :--- |
| `writev` | `writev` 类似于 `readv`，它从 `iovec` 描述的缓冲区中写入数据 |
| `sendpage` | `sendpage` 用于一次写入一个页，通常与网络文件系统配合使用 |
| `get_unmapped_area` | `get_unmapped_area` 用于确定设备的哪些部分没有映射内存 |

单个设备可能永远不需要定义上述所有方法。完全取决于你如何定义对你的设备设备有意义的操作，并对未实现的方法设置为 `NULL`。

当字符设备向内核注册时，它的 `file_operations` 结构体和名称会被添加到 `device_struct` 结构的全局 `chrdev` 数组中，其中主设备号（major number）对其进行索引。这就是字符设备切换表。

```c
struct device_struct {

    const char *name;

    struct file_operations *fops;

};
```

因此，通过查找 `chrdevs [YOUR_MAJOR] -> fops`，内核知道如何与设备通信以及它支持哪些入口点（见图 18-2）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_773_0.png)

图 18-2

# 示例驱动程序：`schar`

让我们来看一个字符设备驱动示例，我们称之为 `schar`。该驱动通过假从一个按恒定间隔轮询的设备提供数据，以自己的方式实现了读写功能。轮询机制由内核定时器管理，我们将在下一节中详细解释。

`schar.c` 开始于定义我们 `file_operations` 结构体实现函数的前声明。然后我们填充它的内容。

# 设备驱动程序

```c
/* _fops 的前声明 */

static ssize_t schar_read(struct file *file, char *buf, size_t count, loff_t *offset);

static ssize_t schar_write(struct file *file, const char *buf, size_t count, loff_t *offset);

static unsigned int char_poll(struct file *file, poll_table *wait);

static int char_ioctl(struct inode *inode, struct file *file, unsigned int cmd, unsigned long arg);

static int schar_mmap(struct file *file, struct vm_area_struct *vma);

static int schar_open(struct inode *inode, struct file *file);

static int schar_release(struct inode *inode, struct file *file);

static struct file_operations schar_fops = {

    read = schar_read,

    write = schar_write,

    poll = schar_poll,

    ioctl = schar_ioctl,

    open = schar_open,

    release = schar_release,

};
```

有些人喜欢将 `file_operations` 结构体放在模块开头，而另一些人则喜欢放在底部。后者的方法可以让我们避免在文件开头放置函数原型。这纯粹是喜好问题。不要担心任何包含文件；我们会在后续过程中解决这些问题。

# `MSG` 宏

在深入研究 `schar` 源码之前，我们需要介绍在整个章中使用的 `MSG` 宏。这是打印调试语句的替代方式，被证明非常有用。我们没有在代码中散布丑陋的 `#ifdef` 语句，而是将 `MSG` 的定义放在 `schar.h` 中：

```c
#define DEBUG

#ifdef DEBUG

#define MSG(string, args...) printk(KERN_DEBUG "schar: " string, ##__ARGS__)

#else

#define MSG(string, args...)

#endif
```

它保持了代码的整洁，并在每个语句前加上了模块名称。如果你愿意，可以轻松地定义一个事件位图并获得精细控制的日志。`schar` 很简单，所以一切都很合理。定义 `DEBUG` 会实际上让 `MSG` 变成一个空操作（no-op）。有时，在调试语句中包含更多信息是有利的，特别是对于较大的设备驱动程序。我们可能想要包含行号和文件名信息，以便快速在源码中定位特定消息。它看起来像这样：

```c
#define MSG(string, args...) printk(KERN_DEBUG "schar:%FILE:%__LINE__: ", string, ##__ARGS__)
```

选择哪种取决于你；书中的所有模块都使用前者，因为它们的复杂性不需要这些额外信息。

# 注册设备

与 `hello` 模块一样，`schar` 自然也有一个 `init_module` 入口点。它执行许多不同的操作——分配内存、初始化定时器和变量等——但目前我们将只关注设备注册。

```c
int init_module(void)

{

    int res;

    if (schar_name == NULL)

        schar_name = "schar";

    /* 向内核注册设备 */

    res = register_chrdev(CHAR_MAJOR, schar_name, &schar_fops);

    if (res) {

        MSG("can't register device with kernel\n");

    }

    return res;

}
```

`schar_name` 可以作为参数传递给模块——我们稍后会看到。现在，我们检查是否指定了名称，如果没有，则进行设置。`SCHAR_MAJOR` 的定义如下。动态分配的优点在于我们不需要知道任何信息。缺点（至少在这个语境下）是我们将必须创建新的设备。我们将使用静态数字。

```c
#define SCHAR_MAJOR 42
```

```c
int major = 0, res;

res = register_chrdev(CHAR_MAJOR, schar_name, &schar_fops);

if (res < 0) {

    MSG("can't register device with kernel\n");

} else {

    major = res;

    MSG("device registered with major %d\n", major);

}
```

切换动态分配将留给读者练习。

# 模块计数

内核需要跟踪每个模块的使用信息。如果不这样做，它如何知道移除模块是安全的？我们绝对不希望驱动在正在拷贝文件时被移除；这会使文件系统处于不可靠的状态。

有两个可以修改计数的宏：`MOD_IN_USE_COUNT` 和 `MOD_DEC_USE_COUNT`；前者增加计数，后者减少计数。驱动程序程序员有责任维护计数以防止模块被意外移除。内核只允许卸载计数为零的模块。`MOD_IN_USE_COUNT` 宏会评估计数，但由于内核在尝试移除之前会进行检查，因此它很少需要。

# 打开与释放

模块现在加载并保持运行，直到有人打开设备。`schar_open` 在进程打开设备时被调用。在这里，模块计数增加以防止移除。

```c
static int schar_open(struct inode *inode, struct file *file) {

    /* 增加计数 */

    MOD_IN_USE_COUNT;

    return 0;

}
```

这告诉内核该模块现在被多一个进程使用。如果用户执行 `rmod module_name`，内核会对计数大于零（意味着正在使用）的模块返回 `-EBUSY`。因此，模块负责更新计数。我们在 `schar_open` 中增加计数。进程关闭设备时，我们减少计数以保持平衡。

传递给 `schar_open` 的 `file` 参数是返回应用程序的文件描述符的内核描述。文件结构包含了设备打开模式的信息。例如，这段代码测试了设备是否可读。

```c
if (file->mode & FMODE_READ) {

    MSG("opened for reading\n");

}
```

它还包含了从哪里启动下一次读取的信息等。这些都是与本模块（实际上与大多数其他模块）相关的部分：

```c
struct file {

    ...

    mode_t f_mode;

};
```

# 第 18 章

```c
loff_t          f_pos;

unsigned int   f_flags;

...

n);
```

`f_mode` 是打开设备时的模式，用于读取、写入或两者兼有。`f_flags` 提供了更多信息，其中与设备模式相关，例如 `O_NONBLOCK` 或 `O_NDELAY`。这些标志是由用户空间应用程序传递给 `open` 调用的，用于控制设备在读和写时的行为。你可以在 `asm/fcntl.h` 中找到所有相关信息。`f_pos` 是下一次读或写操作将执行的位置。

`sch_open` 的下一步是设置定时器；我们将在下一节中讨论这一点。`sch_open` 结束时打印从传递给它的 inode 中提取的打开设备的设备号（major number）和次设备号（minor number）。目前我们不需要使用它，但稍后我们将检查使用这些信息来区分驱动不同实例的模块。我们在第 3 章中讨论过的 inode（索引节点），它们用于识别磁盘和内存上的文件，并可以包含访问时间、大小、文件系统类型等信息。`stat` 结构通过从 inode 中提取信息来获取数据，并在内核外部运行。在 `linux/fs.h` 中查找详细信息，并注意文件类型在联合体 `u` 中是如何定义的。Linux 支持所有的文件系统！

`schar_release` 仅仅是将使用计数减 1。没有其他需要要做的，因为 `sch` 不会为每次打开分配任何内存，也没有其他需要更新的状态信息。

```c
static int schar_release(struct inode *inode, struct file *file)

{

    MOD_DEC_USE_COUNT;

    MSG("schar_release\n");

    return 0;

}
```

# 读取设备

`schar_read` 假装从设备读取数据——实际上，它从一个内部数据队列读取并将其传回用户空间。`schar` 保留了一个全局变量来跟踪数据队列；当数据可用时，`schar_pool` 存储剩余的字节数。这意味着如果如果在 `schar_pool` 为零或负数时调用了 `schar_read`，则读取进程必须处于非活动状态，直到数据可用。

```c
static ssize schar_read(struct file *file, char *buf, size_t count)

{

    loff_t *offset;

    /* 如果请求的数据较少，此处将进程置睡眠 */

    while (count > schar_pool) {

        MSG("putting process with pid %u to sleep\n", current->pid);

        /* 进入睡眠，但在信号时唤醒 */

        interruptible_sleep_on(&schar_wq);

        if (signal_pending(current)) {

            MSG("pid %u got signal\n", (unsigned)current->pid);

        }

    }

    /* 告诉 vfs 信号 */

    return -EINTR;

}

/* 从我们的缓冲区拷贝数据 */

if (copy_to_user(buf, schar_buffer, count))

    return -EFAULT;

    schar_pool -= count;

    schar_data_read += count;

    MSG("want to read %u bytes, %ld bytes in queue\n", (unsigned)count,

    schar_pool);

/* 返回已写入的数据 */

file->f_pos += count;

return count;

}
```

这看起来可能有点棘手，但让我们一步步来。`count` 是读取进程的数据量。如果 `count` 大于 `schar_pool`，读者将无法满足，我们必须挂起读取进程，直到请求的数据可用。`interruptible_sleep` 改变进程状态并将其添加到 `schar_wq` 等待队列。我们稍后会查看队列；它们为我们提供了一种将读取进程设置为非运行状态的方法，并让调度器选择新进程执行。数据从我们的内部缓冲区提供，并在 `copy_to_user` 的帮助下拷贝回应用程序，这个概念稍后会详细介绍。

在 `schar_read` 结束时，我们从池 `schar_length` 中减去 `count` 字节，并返回字节数。在这种情况下，我们返回 `count`，因为我们假装向应用程序写入了与其请求的完全相同的数据。这在 `dd` 等工具中运行良好，因为我们可以指示它请求我们想要的精确字节数。尝试稍后在 `schar` 上运行，你就会明白我们的意思了；在我们的系统中，`cp` 以 4 字节为块请求数据，并一直持续直到读取 0 字节。你可以向 `schar` 喂尽可能多的数据，而 `cp` 会一直请求更多。

如果 `schar_read` 现在看起来不太合逻辑，不要担心。我们将在接下来的章节中逐一查看它的每一个方面。

# 当前任务 (Task)

在 `schar_read` 中多次提到了 `current` 宏。它是以任务结构（task structure）的形式表示当前运行进程的宏。我们对 `schar_read` 执行的任务是当前正在从设备读取的进程。任务结构有许多元素；完整列表可以在 `linux/sched.h` 中找到，但让我们看看我们这里直接或间接使用的字段：

```c
struct task_struct {

    volatile long state;

    ...

    pid_t pid;

    ...
```

```c
struct signal_struct *sig;

sigset_t blocked;

struct sig_pending pending;

...
```

正如你所见，如果你检查 `linux/sched.h`，`state` 表示进程的状态（运行、停止或睡眠）。`pid` 是进程 ID。`sig` 持有信号信息，`blocked` 是阻塞的信号掩码，`pending` 是待处理的信号。最后，通过 `signal_pending` 检查是否发生了信号。

# 等待队列 (Wait Queues)

我们使用等待队列在没有数据时让任务睡眠，并在有新数据时唤醒它。这释放了系统并允许调度器选择另一个进程运行。由于我们需要显式调用这些函数来唤醒它，我们稍后会讨论等待队列的实现：

```c
struct wait_queue {

    struct task_struct *task;

    struct wait_queue *next;

};
```
