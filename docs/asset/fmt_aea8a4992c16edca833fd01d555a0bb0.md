
换句话说，你的内核拒绝加载，因为你的模块版本字符串（更准确地说，版本字符串）不匹配。从 `vermagic` 开始：当链接到 `init/vermagic.c` 文件时，版本数据会以静态字符串的形式插入你的模块对象中。

程序执行、调用了哪个函数、参数是什么以及返回什么。这对于找出诸如程序尝试访问的文件等问题来说是一个无价之宝工具。在最后，你会看到一行看起来像 `write(1, "hello", 5)` 的代码。这就是 `printf()` 前面的样子。你可能对此并不熟悉，因为大多数人使用免费的库函数（如 `open`、`fopen`、`fclose`）。正是因为如此，导致了至少发生了 2 次 `write`。第二部分专门介绍系统调用（如 `kill()` 和 `read()`）。第三部分介绍库调用，你可能对这些更熟悉（如 `cosh()` 和 `random()`）。

你可以编写模块来替换内核的系统调用，我们稍后会介绍这一内容。黑客利用这一点创建后门或木马，但你也可以编写自己的模块来做更多良善的事，例如内核 `tee` 模块，它每当有人尝试删除你系统上的文件时，它就会记录。

## 3.1.3. 用户空间与内核空间

内核拥有对资源的所有访问权限，无论该资源是显卡、硬盘还是内存。程序经常会竞争同一个资源。正如我刚刚看到的，`updatedb` 正在更新 `locate` 数据库。我的视觉和 `updatedb` 都在使用硬盘连接。内核需要保持秩序井然，而不是让用户随心所欲地访问任何东西。为此，CPU 可以在不同的模式下运行。每个模式对系统操作都有不同程度的自由度。Intel x86 架构有 4 种这种模式，被称为“环”（rings）。Unix 使用两个环：最高的环（ring 0，也称为“监视模式”，其中允许任何操作发生）和最低的环（称为“用户模式”）。回想关于库函数与系统调用的讨论。通常情况下，你在用户模式下使用库函数。库函数调用一个或多个系统调用，这些系统调用根据库函数的行为执行，但在监视模式下执行，因为它们是内核本身的一部分。一旦系统调用完成任务，执行权就会传回用户空间。

## 3.1.4. 命名空间

当你写一个较小的 C 程序时，你使用的变量既方便又对读者有意义。另一方面，你编写的例程将是一个更大问题的一部分，全局变量可能属于其他人的全局变量；某些变量名会发生冲突。当程序有许多不足以区分意义的全局变量时，就会出现命名空间污染。在大型项目中，必须努力记住保留名称，并找到开发出一套唯一变量名和符号的方案。

在编写内核代码时，最小的模块也将链接到整个内核，因此这绝对是一个问题。处理此问题的最好方法是将变量声明为 `static`，并为它们使用定义良好的前缀。按照惯例，所有前缀都是小写的。如果你不想将一切都声明为 `static`，另一个选项是声明符号表并将其注册到内核。我们稍后会提到这一点。

文件 `/proc/kallsyms` 存储了内核知道的所有符号，由于它们共享内核的代码空间，因此你的模块可以访问这些符号。

## 3.1.5. 代码空间

内存管理是一个非常复杂的主题——O'Reilly 的《理解 Linux 内核》中大部分内容都在讲内存管理！我们并不打算成为内存管理专家，但在甚至开始考虑编写模块之前，我们需要知道几个因素。

如果你考虑过 `segfault`（段错误）的真正含义，你可能会对指针实际上指向内存位置的方式感到惊讶。至少不是真实的地址。当进程被创建时，内核会留出部分物理内存并将其交给该进程，用于其执行代码、变量、栈、堆以及计算机科学家熟悉的其他内容 [5]。这部分内存从 `0x0000000` 开始，延伸到它需要的任何大小。`0xffff978` 将访问真实物理内存中的不同位置！进程将访问一个名为 `0xffff978` 的索引，该索引指向该特定进程留留内存区域的某种偏移。在大多数情况下，像我们的 `Hello, World` 程序这样的进程可以访问另一个进程的空间，尽管我们稍后会讨论其他方法。

内核有它自己的内存空间。由于模块可以从内核中动态插入和移除（作为一个自主对象），内核的代码空间与其自身的空间有所不同。因此，如果你因为一个差一错误（off-by-one error）而修改了内核数据，内核就会崩溃。这比听起来的还要糟糕，所以最好要谨慎。我想指出，上述结论对于任何使用单体内核的操作系统都是成立的。微内核有自己的代码库。Hurd 和 QNX Neutrino 是两个微内核的例子。

## 3.1.6. 设备驱动程序

一类模块是设备驱动程序，它为卡或串口等硬件提供功能。在 Unix 上，每件硬件都由位于 `/dev` 中的文件表示，该文件提供了与硬件通信的手段。设备驱动可以将 `/dev/sound` 设备文件连接到像 `mpblaster` 这样的用户程序，使其在不知道安装了什么种声卡的情况下使用它。

### 3.1.6.1. 主号和次号

让我们来看看设备文件。这里是代表主硬盘分区的设备文件：

```
ls -l /dev/hda*

br-rw---- 1 root disk 3, 1 Jul 5 2000 /dev/hda1
br-rw---- 1 root disk 3, 2 Jul 5 2000 /dev/hda2
br-rw---- 1 root disk 3, 3 Jul 5 2000 /dev/hda3
```

注意输出中逗号分隔的数字。第一个数字是主号（major number），第二个数字是次号（minor number）。主号告诉你使用的是哪个驱动程序。次号则用于区分由同一驱动程序的不同硬件。

# 第 4 章 字符设备文件

## 4.1. 字符设备驱动

### 4.1.1. `file_operations` 结构

`file_operations` 结构定义在 `linux/fs.h` 中，它包含了指向驱动程序定义的函数指针，这些函数负责对设备执行各种操作。结构中的每个字段都对应驱动程序定义的用于处理请求操作的函数地址。

例如，每个字符驱动程序都需要定义一个从设备读取的函数。`file_operations` 结构持有执行该操作的模块函数地址。以下是内核 2.6.5 版本的定义：

```c
struct file_operations {
    struct module *owner;
    loff_t(*llseek) (struct file *, loff_t, int);
    ssize_t(*read) (struct file *, char __user *, size_t, loff_t);
    ssize_t(*write) (struct file *, struct ki_ack *, char __user *, size_t, loff_t);
    ssize_t(*aio_write) (struct file *, const char __user *, size_t, loff_t);
    ssize_t(*aio_read) (struct file *, const char __user *, size_t, loff_t);
    int (*add_seek) (struct file *, void *, filldir_t);
    unsigned int (*poll) (struct file *, struct poll_table_struct *);
    int (*ioctl) (struct inode *, struct file *, unsigned int);
    int (*mmap) (struct file *, struct vm_area_struct *);
    int (*open) (struct inode *, struct file *);
    int (*flush) (struct file *);
    int (*release) (struct inode *, struct file *);
    int (*fsync) (struct file *, struct destroy *, int datasync);
    int (*aio_fsync) (struct ki_ack *, int datasync);
    int (*fasync) (struct file *, int, struct file_lock *);
    int (*lock) (struct file *, const struct file_lock *);
    ssize_t(*readv) (struct file *, const struct iovec *, unsigned long, loff_t);
    ssize_t(*writev) (struct file *, struct iovec *, unsigned long, loff_t);
    ssize_t(*sendfile) (struct file *, loff_t, size_t, read_actor_t, __user *);
```
