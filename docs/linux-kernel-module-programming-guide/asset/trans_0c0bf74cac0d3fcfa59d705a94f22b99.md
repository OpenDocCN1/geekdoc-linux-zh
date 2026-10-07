

因为读和写是从用户的角度来看的——如果一个进程从内核读取某些内容，那么内核就需要输出它；如果一个进程向内核写入某些内容，那么内核就会将其接收为输入。

这里的另一个有趣点是 `module_permission` 函数。每当进程尝试对 `/proc` 文件进行操作时，该函数就会被调用，并且它可以决定是否允许访问——它仅基于操作以及对 `current` 的使用（在 `current` 中是一个指向包含正在运行进程信息的结构体的指针），但也可以基于我们喜欢的任何内容，例如其他进程对同一文件进行的操作，或者我们最后收到的输入。

使用 `put_user` 和 `get_user` 的原因是 Linux 内存（在 Intel 架构下，在其他处理器上可能不同）是分段的。这意味着指针本身并不引用内存中的唯一位置，而仅引用内存段中的位置，你需要知道是哪一个内存段才能使用它。内核有一个内存段，每个进程也有一个。

进程可以访问的唯一内存段是它自己的，因此在编写编写作为进程运行的普通程序时，不需要考虑段的问题。当你编写内核模块时，通常需要访问内核内存段，这由系统自动处理。然而，当内存缓冲区的内容需要在当前运行的进程和内核之间传递时，内核函数 `put_user` 和 `get_user` 宏允许你访问该内存。

## procs.c

```c
/* procfs.c - 在 /proc 中创建一个“文件”，允许
* 同时输入和输出。 */
```

```c
/* Copyright (C) 1998-1999 by Ori Pomerantz */
```

```c
/* 必要的头文件 */
```

```c
/* 内核模块的标准头 */
#include <linux/kernel.h> /* 我们正在进行内核工作 */
#include <linux/module.h>  /* 具体来说，一个模块 */

/* 处理 CONFIG_MODVERSIONS */
#if CONFIG_MODVERSIONS==1
#define MODVERSIONS
#include <linux/modversions.h>
#endif

/* 因为我们使用了 proc fs，所以这是必要的 */
#include <linux/proc_fs.h>

/* 在 2.2.3 的 /usr/include/linux/version.h 中包含
* 此项的宏，但 2.0.35 没有——所以如果有需要
* 我在这里添加它。 */
#ifndef KERNEL_VERSION
#define KERNEL_VERSION(a,b,c) ((a)*65536+(b)*256+(c))
#endif

#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
#include <asm/uaccess.h> /* 用于 get_user 和 put_user */
#endif

/* 模块函数 ********************* */

/*
* 在这里保留最后收到的消息，以证明
* 我们可以处理我们的输入 */
#define MESSAGE_LENGTH 80
static char Message[MESSAGE_LENGTH];

/* 因为我们使用了文件操作结构体，我们不能
* 使用特殊的 proc 输出机制——我们必须
* 使用标准的 read 函数，即下述这个函数 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t module_output(
    struct file *file,      /* 读取的文件 */
    char *buf,              /* 存放数据的缓冲区（在
        * 用户段中） */
    size_t len,             /* 缓冲区长度 */
    loff_t *offset)            /* 文件中的偏移量 - 忽略 */
#else
static int module_output(
    struct inode *inode,    /* 读取的 inode */
    struct file *file,      /* 读取的文件 */
    char *buf,              /* 存放数据的缓冲区（在
        * 用户段中） */
    int len)                /* 缓冲区长度 */
#endif
{
    static int finished = 0;
    int i;
    char message[MESSAGE_LENGTH+30];

    /* 返回 0 表示文件结束，我们没有
     * 更多信息。否则，进程将
     * 继续从这里读取。 */
    if (finished) {
        finished = 0;
        return 0;
    }

    /* 我们使用 put_user 从内核内存段
     * 拷贝字符串到调用我们的进程内存段。
     * get_user 用于反向操作。 */
    sprintf(message, "Last input:%s", Message);
    for(i=0; i<len && message[i]; i++)
        put_user(message[i], buf+i);

    /* 注意，这里假设 message 的大小
     * 低于 len，将被截断。在实际
     * 情况中，如果 message 大于
     * len，我们会在填充 len+1 个
     * 字节时返回 len。 */
    finished = 1;

    return i; /* “读取”的字节数 */
}

/* 当用户向 /proc 文件写入时，
* 此函数接收输入。 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static ssize_t module_input(
    struct file *file, /* 文件本身 */
    const char *buf, /* 输入缓冲区 */
    size_t length, /* 缓冲区长度 */
    loff_t *offset) /* 文件的偏移量 - 忽略 */
#else
static int module_input(
    struct inode *inode, /* 文件的 inode */
    struct file *file, /* 文件本身 */
    const char *buf, /* 输入缓冲区 */
    int length) /* 缓冲区长度 */
#endif
{
    int i;

    /* 将输入放入 Message 中，module_output
     * 之后可以使用它 */
    for(i=0; i<MESSAGE_LENGTH-1 && i<length; i++)
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
get_user(Message[i], buf+i);
#else
copy_from_user(Message[i], buf);
#endif
    Message[i] = '\0';
    return i;
}

/* 模块函数 ********************* */

/* 此函数决定是否允许访问——
* 它仅基于操作以及对 current 的使用
*（在 current 中是一个指向正在运行进程信息的结构体），
* 但也可以基于我们喜欢的任何内容，例如其他进程对同一文件的操作，
* 或者我们最后收到的输入。 */
static int module_permission(struct inode *inode, int op)
{
    /* 操作可以是以下之一：
    * 0 - 执行
    * 2 - 写入
    * 4 - 读取 */
    if (op == 4 || (op == 2 && current->euid == 0))
        return 0;

    /* 如果是其他操作，拒绝访问 */
    return -EACCES;
}

/* 文件被打开——我们并不真正关心这个，
* 但意味着我们需要增加
* 引用计数。 */
int module_open(struct inode *inode, struct file *file)
{
    MOD_INC_USE_COUNT;
    return 0;
}

/* 文件被关闭——再次，只有因为
* 引用计数才有趣。
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
int module_close(struct inode *inode, struct file *file)
{
    MOD_DEC_USE_COUNT;
    return 0; /* 成功 */
}
#else
void module_close(struct inode *inode, struct file *file)
{
    MOD_DEC_USE_COUNT;
}
#endif

/* 注册为 /proc 文件的结构，包含
* 当有人尝试对我们的文件进行操作时调用的所有函数指针。
* NULL 表示我们不想处理某些操作。 */
static struct file_operations Ops_4_Our_Proc_File =
{
    NULL, /* lseek */
    module_output, /* 从文件“读取” */
    module_input, /* 向文件“写入” */
    NULL, /* readdir */
    NULL, /* select */
    NULL, /* ioctl */
    NULL, /* mmap */
    module_open, /* 有人打开了文件 */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
    NULL, /* flush 在 2.2 版本中添加 */
#endif
    module_close, /* 有人关闭了文件 */
    /* 等等等（它们都在
    * /usr/include/fs.h 中给出）。由于我们没有在这里
    * 放置任何内容，系统将保留默认数据，
    * 在 Unix 中是零（作为指针时为 NULL）。 */
};
```
