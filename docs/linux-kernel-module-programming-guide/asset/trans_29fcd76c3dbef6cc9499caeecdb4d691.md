

```c
/* 因为我们 使用了 proc fs */
#include <linux/proc_fs.h>

/* 用于让进程睡眠并唤醒它们 */
#include <linux/sched.h>
#include <linux/wrapper.h>
```

```c
* 在 2.2.3 /usr/include/linux/version.h 中包含一个
* 用于此定义的宏，但 2.0.35 没有 - 所以如果需要，
* 我在这里在这里添加它。 */
#ifndef KERNEL_VERSION
#define KERNEL_VERSION(a,b,c) ((a)*65536+(b)*256+(c))
#endif
```

```c
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
#include <asm/uaccess.h>    /* 用于 get_user 和 put_user */
#endif
```

```c
* 在这里我们保留最后收到的消息，以证明
* 我们可以处理自己的输入 */
#define MESSAGE_LENGTH 80
static char Message[MESSAGE_LENGTH];
```

```c
* 因为我们使用了文件操作结构，所以我们不能使用
* 特定的 proc 输出机制 - 我们必须使用
* 标准的 read 函数，就是这个函数 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
```c
static ssize_t module_output(
/* 长度 */
    struct file *file,    /* 被读取的文件 */
    char *buf, /* 用于存放数据的缓冲区（在用户
    * 用户段中） */
    size_t len, /* 缓冲区长度 */
    loff_t *offset) /* 文件中的偏移量 - 忽略 */
#else
static int module_output(
    struct inode *inode, /* 读取的 inode */
    struct file *file,    /* 被读取的文件 */
    char *buf, /* 用于存放数据的缓冲区（在用户
    * 用户段中） */
    int len) /* 缓冲区长度 */
#endif
{
    static int finished = 0;
    int i;
    char message[MESSAGE_LENGTH+30];

/* 返回 0 表示文件结束 - 即我们此时
* 没有更多内容要说了。 */
    if (finished) {
        finished = 0;
        return 0;
    }

/* 如果你现在还不懂这个，那么你作为一个
* 内核程序员就没没救了。 */
    sprintf(message, "Last input:%s\n", message);
    for(i=0; i<len && message[i]; i++)
        put_user(message[i], buf+i);

    finished = 1;
    return i; /* 返回“读取”的字节数 */
}
```

```c
/* 当用户向 /proc 文件写入时，
 * 此函数从用户那里接收输入。 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t module_input(
    struct file *file,      /* 文件本身 */
    const char *buf,       /* 输入的缓冲区 */
    size_t length,          /* 缓冲区长度 */
    loff_t *offset)         /* 文件的偏移量 - 忽略 */
#else
static int module_input(
    struct inode *inode,   /* 文件的 inode */
    struct file *file,      /* 文件本身 */
    const char *buf,       /* 输入的缓冲区 */
    int length)          /* 缓冲区长度 */
#endif
#endif

{
    int i;

    /* 将输入放入 Message 中，这样 module_output 
 *     就能使用它了 */
    for(i=0; i<MESSAGE_LENGTH-1 && i<length; i++)
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
        get_user(Message[i], buf+i);
#else
        Message[i] = get_user(buf+i);
#endif

    /* 我们需要一个标准的、零终止的字符串 */
    Message[i] = '\0';

    /* 我们需要返回使用的输入
 *     字符数量 */
    return i;
}

/* 如果文件当前被某人打开 */
```c
int AlreadyReady_open = 0;

/* 想要我们文件的进程队列 WaitQ */
static struct wait_queue WaitQ = NULL;

/* 当 /proc 文件被打开时调用 */
static int module_open(struct inode *inode,
struct file *file)

/* 如果文件的标志包含 O_NONBLOCK，意味着
* 进程不想等待该文件。
* 在这种情况下，如果文件已经打开，我们
* 应该返回 -EAGAIN，意味着“你必须
* 重试”，而不是阻塞一个会
* 保持唤醒的进程。 */
if ((file->flags & O_NONBLOCK) && Already_Open)
return -EAGAIN;

/* 这里是 MOD_INC_USE_COUNT 的正确位置，
* 因为如果进程在循环中（而该循环
* 在内核模块内部），则
* 不能被移除。 */
MOD_INC_USE_COUNT;

/* 如果文件已经打开，则等待它不再打开 */
while (Already_Open)
{
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
int i, is_sig=0;
#endif
/* 此函数让当前进程（包括我们的
* 系统调用）进入睡眠。
* 执行将在调用后恢复，可能是有人
* 调用了 wake_up(&WaitQ)（只有 module_close
* 在文件关闭时这样做），或者向进程
* 发送了信号如 Ctrl-C */
interruptible_sleep_on(&WaitQ);

/* 如果我们是因为信号而唤醒的，
* 则返回 -EINTR（系统调用失败），
* 这允许进程被杀死或停止。 */
/* Emmanuel Papakis:
* 这是一个更新。信号
* 现在包含在两个字（64位）中，
* 存储在包含两个 long 的结构中。
* 我们必须检查。 Pomerantz:
* 没有人承诺不会使用超过 64 位，
* 或者这段代码在 16 位的
* Linux 下任何情况下都能工作。 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
for(i=0; i<WORDS && !is_sig; i++)
    is_sig = current->signal[i] &
      current->blocked[i];
if (is_sig) {
#else
    if (current->signal & current->blocked) {
    /* 在这里放置 MOD_DEC_USE_COUNT 很重要
    * 因为对于那些永远不会关闭的
* 进程，如果我们在这里不减少计数，
* 将留下正数计数，我们只能通过
* 重启机器将其置零。 */
MOD_DEC_USE_COUNT;
return -EINTR;
}
/* 如果到达这里，Already_Open 必须为 0 */
/* 打开文件 */
Already_Open = 1;
return 0; /* 允许访问 */
}

/* 当 /proc 文件关闭时调用 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
int module_close(struct inode *inode, struct file *file)
#else
void module_close(struct inode *inode, struct file *file)
#endif
{
/* 将 Already_Open 零，这样 WaitQ 中的
* 一个进程就能将 Already_Open
* 置回 1 并打开文件。其他进程
* 在 Already_Open 回到 1 时回到睡眠。 */
Already_Open = 0;

/* 唤醒 WaitQ 中的所有进程，如果有人
* 在等待该文件，他们就可以拥有它。 */
module_wake_up(&WaitQ);

MOD_DEC_USE_COUNT;

#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
return 0;    /* success */
#endif
}

/* 此函数决定是否允许操作
*（返回 0）或不允许（返回非零，
* 表示为什么不允许）。
* 操作可以是以下值之一：
* 0 执行（运行“文件”——在我们案例中没有意义）
* 2 写入（输入内核模块）
* 4 读取（从内核模块输出）
* 这是检查文件权限的真实函数。ls -l 返回的权限
* 仅供参考，可以在这里覆盖。 */
static int module_permission(struct inode *inode, int op)
{
/* 我们允许所有人从我们的模块读取，
* 但只有 root (uid 0) 可以对其写入 */
if (op == 4 || (op == 2 && current->euid == 0))
return 0;

/* 如果是其他任何情况，拒绝访问 */
return -EACCES;
}
```

```c
/* 注册为 /proc 文件的结构，带有
* 指向所有相关函数的指针。********* */

/* 我们 proc 文件的文件操作。这里
* 我们放置了有人尝试对我们的文件进行操作时
* 所调用的所有函数的指针。NULL 表示我们不想处理某些情况。 */
static struct file_operations File_Ops_4_Our_Proc_File = {
    NULL, /* lseek */
    module_output, /* 从文件“读取” */
    module_input, /* 向文件“写入” */
    NULL, /* readdir */
    NULL, /* select */
    NULL, /* ioctl */
    NULL, /* mmap */
    module_open, /* 当 /proc 文件被打开时调用 */
}
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    NULL, /* flush */
#endif
    module_close /* 当被关闭时调用 */
};
```

```c
/* 我们 proc 文件的 inode 操作。我们需要它是因为
* 这样我们就有地方指定要使用的文件操作
* 结构以及我们用于权限的函数。
* 也可以指定当对 inode 执行任何其他操作时
* 调用的函数（尽管我们没这样做，直接放了 NULL）。 */
static struct inode_operations In_Ops_4_Our_Proc_File = {
};
```

