
# 第2章 | Linux 系统的实用视角

之所以有两个独立的程序，是因为 `getty` 和 `login` 都可以单独使用，例如，通过 SSH 进行远程登录并不使用终端，而是使用 `login`：每个新连接由一个名为 `ssh` 的程序处理，该程序会启动 `login` 进程。

图形登录在概念上与上述描述没有区别。区别在于运行的不是 `getty`/`login` 程序，而是名为显示管理器（display manager）的图形登录程序，在验证通过后，该进程启动图形 shell。

在树莓派中，显示管理器是 `LightDM`，图形 shell 是 `LXDE`（轻量级 X11 桌面环境）。与大多数 Linux 发行版一样，图形桌面环境基于 X Window 系统（X11），该项目始于 MIT，现在由 XOrg 基金会管理。

## 2.4 内核管理与编程

Linux 系统的管理员不需要了解 Linux 内核的内部工作原理，但需要熟悉用于配置操作系统的工具，包括通过内核模块为内核添加功能，以及编译自定义内核。

### 2.4.1 可加载内核模块和设备驱动程序

如上所述，内核是模块化的，可以使用可加载内核模块（LKM）在运行时加载功能。此功能被用于配置系统硬件的驱动程序。因此，管理员需要熟悉模块系统的主要概念，并基本理解设备驱动程序的作用。

要将模块插入 Linux 内核中，可以使用 `insmod(8)` 命令。`insmod` 通过 `init_module()` 系统调用将 LKM 加载到内存。

`init_module()` 系统调用在加载 LKM 后立即调用 LKM 的初始化程序。`insmod` 使用 `module_init()` 宏向 `init_module()` 传递内核中初始化程序的地址。

LKM 作者设置模块的 `init_module` 来调用内核函数，注册 LKM 包含的子程序。例如，字符驱动的 `init_module` 程序可能会调用 `register_chdev` 内核程序，传递它意图驱动的设备的主、从号以及自身的 `open()` 程序地址作为参数。`register_chdev` 记录当内核想要打开特定设备时，应调用我们 LKM 中的 `open()` 程序。

当 LKM 被卸载时（例如通过 `rmmod(8)` 命令），将通过 `module_exit()` 宏调用 LKM 的清理程序。

在实践中，管理员将希望使用更智能的 `modprobe(8)` 命令来自动处理模块依赖。最后，可以使用 `lsmod(8)` 命令列出所有加载的内核模块。

好奇的细节可见 `kernel/module.c` 中的 `init_module`、`load_module` 和 `do_init_module`。

### 2.4.2 Linux 内核模块的结构

作为管理员，你有时需要为系统添加新设备，而你的 Linux 发行版标准内核没有为该设备提供驱动程序。这意味着你必须将该驱动程序添加到内核中。

一个简单的内核模块非常容易。以下模块将在加载和卸载时向内核打印一些信息。

## 基于树莓派的 Linux 操作系统基础

然而，请注意内核模块并不是应用程序；它是供内核使用的代码段。如你所见，这里没有 `main()` 函数。此外，内核模块：

- 不是按顺序执行的：内核模块通过其初始化函数注册自身来处理请求，该函数运行后即结束。它能够处理的请求类型在模块代码中定义。这与图形用户界面（GUI）应用程序中常用的事件驱动编程模型非常相似。
- 不具备自动资源管理能力（内存、文件句柄等）：在模块代码中分配的任何资源都必须在模块卸载时显式地释放。
- 无法访问常用的用户空间系统调用，例如 `print()`。但是，有一个 `printk()` 函数可以将信息输出到内核日志中，并可以从用户空间进行查看。
- 内核模块可以同时被多个不同的程序/进程使用，因为它们是内核的一部分。因此，在编写内核模块时，必须非常小心，以确保模块在被中断时其行为是一致且正确的。
- 必须对资源非常敏感：由于模块是内核代码，它的执行在 CPU 周期和内存使用方面都与内核运行时竞争。你必须意识到，你的模块不应该破坏系统的整体性能。

宏 `module_init` 和 `module_exit` 用于标识在模块加载和卸载时应该运行哪些子程序。模块的其他功能取决于模块的用途，但内核中将特定模块连接到通用 API（文件系统 API）的通用机制是一个带有函数指针的结构体（`struct`），其工作方式类似于 Java 或 C++ 中的对象接口声明。例如，文件系统 API 在 `include/linux/fs.h` 中提供了 `file_operations`，如下所示：

```
Listing 2.4.2: file_operations from <include/linux/fs.h>
```c

struct file_operations {

    struct module *owner;

    loff_t (*seek)(struct file *, loff_t, int);

    ssize_t (*read)(struct file *, char __user *, size_t, loff_t *);

    ssize_t (*write)(struct file *, const char __user *, size_t, loff_t *);

    ssize_t (*read_iter)(struct read_iter *, struct kiocb *, loff_t);

    ssize_t (*write_iter)(struct write_iter *, struct kiocb *, loff_t);

    int (*open)(struct file *, struct dir_context *);

    int (*shared)(struct file *, struct dir_context *);

    int (*poll)(struct file *, struct poll_table *);

    long (*locked_ioctl)(struct file *, unsigned int, unsigned long);

    long (*ioctl)(struct file *, unsigned int, unsigned long);

    void * (*mmap)(struct file *, struct vm_area_struct *);

    unsigned long long mmap_supported_structs;

    int (*open)(struct inode *, struct file *);

    int (*flush)(struct file *, struct filp *f_id);

    int (*release)(struct inode *, struct file *);

    int (*fsync)(struct file *, loff_t, int datasync);

};

```

```
int (*fsasync)(int, struct file *, int);

int (*lock)(struct file *, struct file_lock *);

size_t (*sendpage)(struct file *, struct page *, int, size_t, loff_t *, int);

unsigned long (*unmapped_area)(struct file *, unsigned long, unsigned long, unsigned long, unsigned long);

int (*check_flags)(int);

int (*struct file *, int, struct file_lock *);

size_t (*splice_write)(struct pipe_inode_info *, struct file *, loff_t *, size_t, unsigned int);

size_t (*splice_read)(struct file *, loff_t *, struct pipe_inode_info *, size_t, unsigned int);

int (*struct file *, long, struct file_lock *, **);

long (*fallocate)(struct file *, int, loff_t offset, loff_t len);

void (*show_file_info)(struct seq_file *m, struct file *f);

#include <linux/fs.h>

unsigned (*map_capacities)(struct file *);

size_t (*copy_file_range)(struct file *, loff_t, struct file *, loff_t, unsigned int);
```
