
- 在人们仍在使用非 Linux 操作系统以保护其对遗留软件的投资的世界里，Linux 必须通过支持大量不同的文件系统来提供互操作性——其中大多数本身不值得存在，但仅为了与现有的非 Linux 操作系统兼容而存在。

- 文件编写者的接口必须非常简单，以便人们可以通过编写它们的只读版本来尝试逆向工程现有的专有文件系统。因此，Linux VFS 使实现只读文件系统变得非常容易；95% 的工作是通过添加完整的写支持来完成它们。作为一个具体的例子，我在大约 10 小时内为 Linux 编写了只读的 `BFS` 文件系统，但花费了数周时间才完成它以获得完整的写支持（甚至今天，一些纯粹主义者声称它不完整，因为“它没有碎片整理支持”）。

- `VFS` 接口是导出的，因此所有 Linux 文件系统都可以作为模块实现。

让我们考虑在 Linux 下实现文件系统所需的步骤。实现文件系统的代码可以是动态加载的模块，也可以是静态链接到内核中的，而在 Linux 下实现它的方式非常透明。只需填充一个 `struct file_system_type` 结构，并使用 `register_filesystem()` 函数向 `VFS` 注册它，如下一个来自 `fs/bfs/inode.c` 的示例所示：

```c
#include <linux/module.h>
#include <linux/init.h>

static struct super_block *bfs_read_super(struct super_block *, void *, int);

static DECLARE_FSTYPE_DEV(bfs_fs_type, "bfs", bfs_read_super);

static int __init init_bfs_fs(void)
{
    return register_filesystem(&bfs_fs_type);
}

static void __exit exit_bfs_fs(void)
{
    unregister_filesystem(&bfs_fs_type);
}

module_init(init_bfs_fs)
module_exit(exit_bfs_fs)
```

`module_init()` / `module_exit()` 宏确保，当 `BFS` 编译为模块时，函数 `init_bfs_fs()` 和 `exit_bfs_fs()` 分别转变为 `init_module()` 和 `cleanup_module()`；如果 `BFS` 静态链接到内核中，`exit_bfs_fs()` 代码会消失，因为它是不必要的。

`struct file_system_type` 在 `include/linux/fs.h` 中声明：

```c
struct file_system_type {
    const char *name;
    int fs_flags;
    struct super_block *(*read_super)(struct super_block *, void *, int);
    struct module *owner;
    struct vfsmount * kern_mnt; /* For kernel mount, if it's FS_SINGLE fs */
    struct file_system_type * next;
};
```

其字段解释如下：

- `name`：人类可读的名称，出现在 `/proc/filesystems` 文件中，并用作按键查找文件系统的键；此相同名称用于 `mount(2)` 中的文件系统类型，并且应该是唯一的；显然，只能有一个具有给定名称的文件系统。对于模块，`name` 指向模块的地址空间并且不会复制：这意味着如果模块已卸载但文件系统仍已注册，`cat /proc/filesystems` 可能会触发内核崩溃（`oops`）。

- `fs_flags`：一个或多个（按位或运算）标志：用于只能挂载在块设备上的文件系统的 `FS_REQUIRES_DEV`，用于只能有一个超级块的文件系统的 `FS_SINGLE`，用于不能通过用户空间意味着通过 `mount(2)` 系统调用挂载的文件系统的 `FS_NOMOUNT`；不过，它们可以通过 `kern_mount()` 接口在内部挂载，例如管道。

- `read_super`：指向在挂载操作期间读取超级块的函数的指针。此函数是必需的；如果未提供，挂载操作（无论是来自用户空间还是内核）将始终失败，除非在 `FS_SINGLE` 情况下，它将在 `get_sb_single()` 中尝试解引用 `fs_type->kern_mnt->mnt_sb` 中的 `NULL` 指针（`fs_type->kern_mnt = NULL`）时触发 `Oops`。

- `owner`：指向实现此文件系统的模块的指针。如果文件系统静态链接到内核中，则此值为 `NULL`。您不需要手动设置它，因为宏 `THIS_MODULE` 会自动执行正确的操作。

- `kern_mnt`：仅用于 `FS_SINGLE` 文件系统。这是由 `kern_mount()` 设置的（`TODO`：如果未设置 `FS_SINGLE`，`kern_mount()` 应拒绝挂载文件系统）。

- `next`：链接到由 `file_systems`（参见 `fs/super.c`）为头的单向链表中。该列表由 `file_systems_lock` 读写自旋锁保护，函数 `register/unregister_filesystem()` 通过从列表中链接和解除链接条目来修改它。

`read_super()` 函数的任务是填充超级块的字段，分配根 `inode` 并初始化与此挂载实例关联的文件系统私有信息。因此，通常 `read_super()` 会执行以下操作：

- 使用缓冲缓存 `bread()` 函数从通过 `sb->s_dev` 参数指定的设备读取超级块。如果预计立即读取几个后续元数据块，则使用 `breada()` 安排异步读取额外的块是有意义的。

- 验证超级块是否包含有效的魔数，并且整体看起来是否“正常”。

- 初始化 `sb->s_op` 以指向 `struct super_block_operations` 结构。此结构包含实现诸如“读取 `inode`”、“删除 `inode`”等操作的文件系统特定函数。

- 使用 `d_alloc_root()` 分配根 `inode` 和根 `dentry`。

- 如果文件系统不是只读挂载的，则将 `sb->s_dirty` 设置为 `1`，并将包含超级块的缓冲区标记为脏（`TODO`：为什么我们要这样做？我在 `BFS` 中这样做是因为 `MINIX` 也这样做了...）。

### 3.3 文件描述符管理

在 Linux 下，用户文件描述符和内核 `inode` 结构之间存在多个间接层。当进程发出 `open(2)` 系统调用时，内核返回一个小的非负整数，该整数可用于此文件的后续 I/O 操作。此整数是指向 `struct file` 指针数组的索引。每个文件结构通过 `file->f_dentry` 指向一个 `dentry`。每个 `dentry` 通过 `dentry->d_inode` 指向一个 `inode`。

每个任务包含一个字段 `task->files`，它是指向在 `include/linux/sched.h` 中定义的 `struct files_struct` 的指针。

### 3.4 文件结构管理

`file->count` 是一个引用计数，由 `get_file()`（通常由 `fget()` 调用）递增，并由 `fput()` 和 `put_filp()` 递减。`fput()` 与 `put_filp()` 的区别在于，`fput()` 执行更多常规文件所需的工作，例如释放 `flock` 锁、释放 `dentry` 等；而 `put_filp()` 仅操作文件表结构，即在 `files_lock` 自旋锁的保护下，递减计数，将文件从 `anon_list` 中移除，并将其添加到 `free_list`。

如果子线程是通过在 `clone()` 系统调用的克隆标志参数中设置 `CLONE_FILES` 而创建的，那么 `tsk->files` 可以在父进程和子进程之间共享。这一点可以在 `kernel/fork.c:copy_files()`（由 `do_fork()` 调用）中看到，当设置了 `CLONE_FILES` 时，它只会递增 `file->count`，而不是按照传统 UNIX `fork(2)` 的惯例去复制文件描述符表。
