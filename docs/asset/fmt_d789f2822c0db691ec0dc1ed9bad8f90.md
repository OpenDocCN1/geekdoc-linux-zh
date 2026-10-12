
文件描述符（其数量比整数多）用于唯一标识进程内已打开的文件。这假设内核能够在用户进程中的描述符与内部使用的结构之间建立联系。实现此操作所需的元素包含在每个进程的任务结构体（`task structure`）中。

```c
<sched.h>
struct task_struct {
    /* file system info */
    int link_count, total_link_count;
    ...
    /* filesystem information */
    struct fs_struct *fs;
    /* open file information */
    struct files_struct *files;
    /* namespaces */
    struct nsproxy *nsproxy;
};
```

整数元素 `link_count` 和 `total_link_count` 用于在查找循环链链接时防止无限循环，正如我将在 8.4.2 节中演示的那样。

进程与文件系统相关的数据存储在 `fs` 中。这些数据包括例如当前工作目录以及 `chroot` 限制信息，我将在第 8.3.4 节中讨论这些。

由于内核允许同时运行多个模拟独立系统的容器，每个对容器而言是是“全局”的资源都被内核封装，并为每个容器单独管理。虚拟文件系统也受到影响，因为每个容器可能面临不同的层级结构。相关信息包含在 `ns_proxy->mnt_namespace` 中（见第 8.3.4 节）。

`files` 包含了下节中检查的进程描述符。

#### 相关文件

任务结构中的元素类型为 `files_struct`。其定义如下：

```c
<sched.h>
struct files_struct {
    atomic_t count;
    struct fdtable *fdt;
    struct fdtable fdtab;

    int next_fd;
    struct embedded_fd_set close_on_exec_init;
    struct embedded_fd_set open_fds_init;
    struct file * fd_array[NR_OPEN_DEFAULT];
};
```

`next_fd` 表示打开新文件时将使用的文件描述符编号。`close_on_exec_init` 和 `open_fds_init` 是位图。`close_on_exec` 包含一个所有在执行时将关闭的文件描述符的设置位。`open_fds_init` 是初始的文件描述符集。`struct embedded_fd_set` 只是封装在特殊结构中的一个 `unsigned long`。

```c
<file.h>
struct embedded_fd_set {
    unsigned long fds_bits[1];
};
```

`fd_array` 包含了每个打开文件的 `struct file` 实例；我稍后会讨论这个结构。

默认情况下，每个进程允许打开 `NR_OPEN_DEFAULT` 个文件。这在 `include/linux/sched.h` 中定义，默认设置为 `BITS_PER_LONG`。在 32 位系统上，因此初始文件数量为 32；64 位系统可以同时处理 64 个文件。如果进程尝试同时打开更多文件，内核必须增加用于 `files_struct` 元素的内存空间，以管理与该进程关联的所有文件信息。

最重要的信息包含在 `fdtab` 中。内核为此目的定义了另一个数据结构。

```c
<file.h>
struct fdtable {
    unsigned int max_fds;
    struct file **fd;      /* current fd array */
    fd_set *close_on_exec;
    fd_set *open_fds;
    struct rcu_head rcu;
    struct files_struct *free_files;
    struct fdtable *next;
};
```

`struct files_struct` 中包含了该结构的一个实例以及指向该实例的指针，因为使用了 RCU 机制来允许对这些结构进行无锁读取，从而提高速度。在我回到如何做到这一点之前，我需要介绍这些元素的含义：

`max_fds` 指定了进程可以处理的文件对象和文件描述符的当前最大数量。没有根本性的上限，因为这两个值都可以增加（只要它们没有超过 Rlimit 指定的值 —— 但与文件结构无关）。尽管始终使用相同数量的文件对象和文件描述符，但内核必须定义不同的最大值。这是由于关联数据结构的管理方式导致的。我将解释这一点，但首先必须澄清结构中的剩余成员：

```c
<fs.h>
struct file {
    struct list_head fu_list;
    struct path f_path;
#define f_dentry f_path.dentry
    const file_operations *f_op;
    atomic_t count;
    unsigned int flags;
    f_mode mode;
    loff_t f_pos;
    struct f_struct *f_owner;
    struct ra ra;
    struct address_space *mapping;
};
```

这些元素的含义如下：

- `max_fds` 指定了进程可以处理的文件对象和文件描述符的当前最大数量。没有根本性的上限，因为这两个值都可以增加（只要它们没有超过 Rlimit 指定的值 —— 但与文件结构无关）。尽管始终使用相同数量的文件对象和文件描述符，但内核必须定义不同的最大值。这是由于关联数据结构的管理方式导致的。我将解释这一点，但首先必须澄清结构中的剩余成员：

- `f_op` 指向文件操作。

- `count` 是文件的引用计数。

- `flags` 是文件的标志位。

- `mode` 是文件访问模式。

- `f_pos` 是文件的当前偏移量。

- `f_owner` 指向打开文件的进程。

- `ra` 包含预读信息。

- `mapping` 指向地址空间。

`path` 结构定义为：

```c
<name.h>
struct path {
    struct vfsm_mount *mnt;
    struct dentry *dentry;
};
```

`fdtable` 定义如下：

```c
<file.h>
struct fdtable {
    struct vfsm_mount *mnt;
    struct dentry *dentry;
};
```

`fdtable` 提供了文件名和 inode 之间的连接。我将在 8.5 节中讨论这一点。

#### 增加限制

当内核打开文件或执行某些比初始提供的更多 `files_struct` 项的操作时，调用 `expand_file`。该函数检查是否需要扩大，如果是，则调用 `expand_fdtable`。该函数 —— 略微简化 —— 实现如下。

```c
fs/file.c
static int expand_fdtable(struct file_struct *files, int nr)
{
    struct ftable *new_fdt, *cur_fdt;

    spin_lock(&files->file_lock);
    new_fdt = alloc_fdtable(nr);
    spin_unlock(&files->file_lock);

    copy_fdtable(new_fdt, files->fddt);
    rcu_assign_pointer(files->fddt, new_fdt);
    if (cur_fdt->max_fds > NR_OPEN_DEFAULT)
        free_fdtable(cur_fdt);

    return 1;
}
```

## 第8章：虚拟文件系统

### 8.3.4 文件操作

文件不仅需要能够存储信息，还允许对这些信息进行操作。从用户的角度来看，操作是通过标准库函数完成的。这些函数指示内核执行系统调用，然后由系统调用执行所需的操作。当然，接口对于不同的文件系统实现可能有所不同。VFS（虚拟文件系统）层提供了抽象操作，将通用的文件对象与底层文件系统的低级机制连接起来。

用于抽象文件操作的结构必须尽可能通用，以便适用于广泛范围的目标文件。同时，它不能包含许多对某种特定文件类型有用但对其他类型无用的特化操作。尽管如此，为了充分利用各种文件（普通文件、设备文件等）的能力，必须满足它们的特殊需求。

每个文件都包含一个指向 `file_operations` 结构的指针，该结构持有所有可能的文件操作的函数指针。该结构定义如下：
