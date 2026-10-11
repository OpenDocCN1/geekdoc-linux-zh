
## 3.4 文件结构管理

`file->count` 是一个引用计数，由 `get_file()`（通常由 `fget()` 调用）递增，并由 `fput()` 和 `put_filp()` 递减。`fput()` 与 `put_filp()` 的区别在于，`fput()` 执行更多常规文件所需的工作，例如释放 flock 锁、释放 dentry 等；而 `put_filp()` 仅操作文件表结构，即在 `files_lock` 自旋锁的保护下，递减计数，将文件从 `anon_list` 中移除，并将其添加到 `free_list`。

如果子线程是通过在 `clone()` 系统调用的克隆标志参数中设置 `CLONE_FILES` 而创建的，那么 `tsk->files` 可以在父进程和子进程之间共享。这一点可以在 `kernel/fork.c:copy_files()`（由 `do_fork()` 调用）中看到，当设置了 `CLONE_FILES` 时，它只会递增 `file->count`，而不是按照传统 UNIX **fork**(2) 的惯例去复制文件描述符表。

当文件被打开时，为其分配的文件结构会被安装到 `current->files->fd[fd]` 槽位中，并且位图 `current->files->open_fds` 中对应的 `fd` 位会被置位。这一切都是在 `current->files->file_lock` 读写自旋锁的写保护下完成的。当描述符被关闭时，`current->files->open_fds` 中的 `fd` 位会被清除，并且 `current->files->next_fd` 会被设置为等于 `fd`，作为下一次该进程想要打开文件时查找第一个未使用描述符的提示。

文件结构在 `include/linux/fs.h` 中声明：

```c
struct fown_struct {
	int pid;        /* pid or -pgpr where SIGIO should be sent */
	uid_t uid, eid; /* uid/euid of process setting the owner */
	int signum;    /* posix.1b rt signal to be delivered on IO */
};

struct file {
	struct list_head	f_list;
	struct dentry	*f_dentry;
	struct vfsmount	*f_vfsmnt;
	struct file_operations	*f_op;
	atomic_t		f_count;
	unsigned int	f_flags;
	mode_t		f_mode;
	loff_t f_pos;
	unsigned long f_reada, f_ramax, f_raend, f_ralen, f_rawin;
	struct fown_struct f_owner;
	unsigned int f_uid, f_gid;
	int f_error;
	unsigned long f_version;
	/* needed for tty driver, and maybe others */
	void *private_data;
};
```

让我们来看看 `struct file` 的各个字段：

- **`f_list`**：此字段将文件结构链接到其中一个（且仅一个）列表中：a) 如果对应的 inode 不是匿名的，则链接到该文件系统上所有打开文件的 `sb->**`s_files`** 列表中，此时由 `dentry_open()`（由 `filp_open()` 调用）将文件链接到此列表；b) `fs/file_table.c` 中的 **`free_list`**，包含未使用的文件结构；c) `fs/file_table.c` 中的 **`anon_list`**，当通过 `get_empty_filp()` 创建新的文件结构时，它会放在此列表中。所有这些列表都由 **`files_lock`** 自旋锁保护。
- **`f_dentry`**：与此文件对应的 dentry。dentry 在 nameidata 查找期间由 `open_namei()`（或者更确切地说是它调用的 `path_walk()`）创建，但实际的 file->**`f_dentry`** 字段是由 `dentry_open()` 设置为包含找到的 dentry 的。
- **`f_vfsmnt`**：指向包含该文件的文件系统的 `vfs` 挂载结构的指针。这是由 `dentry_open()` 设置的，但在 nameidata 查找期间由 `open_namei()`（或者更确切地说是它调用的 `path_init()`）作为一部分找到。
- **`f_op`**：指向 **`file_operations`** 的指针，其中包含可以在此文件上调用的各种方法。这是从 inode->**`i_fop`** 复制而来的，后者在 nameidata 查找期间由特定于文件系统的 `s_op->read_inode()` 方法放置在那里。我们将在本节的稍后部分详细查看 **`file_operations`** 方法。
- **`f_count`**：由 `get_file`/**`put_filp`**/**`fput`** 操作的引用计数。
- **`f_flags`**：来自 `open(2)` 系统调用的 **`O_XXX`** 标志，由 `dentry_open()` 复制到此处（经过 `filp_open()` 的轻微修改），在清除 **`O_CREAT`**、**`O_EXCL`**、**`O_NOCTLY`**、**`O_TRUNC`** 之后——永久存储这些标志没有意义，因为它们不能被 **`F_SETFL`** 修改（或被 **`F_GETFL`**/**`fcntl(2)`** 查询）。
- **`f_mode`**：用户空间标志和模式的一个组合，由 `dentry_open()` 设置。转换的目的是将读和写访问存储在单独的位中，以便可以进行诸如 (`f_mode & FMODE_WRITE`) 和 (`f_mode & FMODE_READ`) 这样的简单检查。
- **`f_pos`**：文件的当前位置，用于下一次对文件的读取或写入。在 i386 上，其类型为 **`long long`**，即 64 位值。
- **`f_reada, f_ramax, f_raend, f_ralen, f_rawin`**：用于支持 `readahead`——对于凡人来说太复杂了，无法讨论 :)
- **`f_owner`**：文件 I/O 的所有者，通过 **`SIGIO`** 机制接收异步 I/O 通知（参见 `fs/fcntl.c`：**`kill_fasync`**）。
- **`f_uid, f_gid`** – 当文件结构在 `get_empty_filp()` 中创建时，设置为打开该文件的进程的用户 ID 和组 ID。如果文件是套接字，则被 `ipv4` netfilter 使用。
- **`f_error`**：用于 NFS 客户端返回写错误。它在 `fs/nfs/file.c` 中设置，并在 `mm/fiemap.c`：**`generic_file_write`**() 中检查。
- **`f_version`** – 用于使缓存失效的版本控制机制，每当 **`f_pos`** 变化时递增（使用全局事件）。
- **`private_data`**：每个文件的私有数据，可由文件系统（例如 coda 在此存储凭据）或设备驱动程序使用。在存在 devfs 的情况下，设备驱动程序可以使用此字段来区分多个实例，而不是使用编码在 `file->f_dentry->d_inode->i_rdev` 中的经典次要设备号。

现在让我们看看 **file_operations** 结构，其中包含可以在文件上调用的方法。让我们回顾一下，它是从 `inode->i_fop` 复制而来的，而 `inode->i_fop` 是由 `s_op->read_inode()` 方法设置的。它声明在 `include/linux/fs.h` 中。

```c
struct file_operations {
	struct module *owner;
	loff_t (*llseek) (struct file *, loff_t, int);
	ssize_t (*read) (struct file *, char *, size_t, loff_t *);
	ssize_t (*write) (struct file *, const char *, size_t, loff_t *);
	int (*readdir) (struct file *, void *, filldir_t);
	unsigned int (*poll) (struct file *, struct poll_table_struct *);
	int (*ioctl) (struct inode *, struct file *, unsigned int, unsigned long);
	int (*mmap) (struct file *, struct vm_area_struct *);
	int (*open) (struct inode *, struct file *);
	int (*flush) (struct file *);
	int (*release) (struct inode *, struct file *);
	int (*fsync) (struct file *, struct dentry *, int datasync);
	int (*fasync) (int, struct file *, int);
	int (*lock) (struct file *, int, struct file_lock *);
	ssize_t (*readv) (struct file *, const struct iovec *, unsigned long, loff_t *);
	ssize_t (*writev) (struct file *, const struct iovec *, unsigned long, loff_t *);
};
```

- **owner**: 指向拥有该子系统模块的指针。只有驱动程序需要将其设置为 THIS_MODULE，文件系统可以很高兴地忽略它，因为它们的模块计数在挂载/卸载时受控，而驱动程序需要在打开/释放时进行控制。
- **llseek**: 实现 `lseek(2)` 系统调用。通常省略并使用 `fs/read_write.c:default_llseek`，它会做正确的事情（TODO：强制那些目前将其设置为 NULL 的人使用 default_llseek -- 这样我们可以在 `llseek()` 中节省一个 `if()`）。
- **read**: 实现 `read(2)` 系统调用。文件系统可以使用 `mm/filemap.c:generic_file_read()` 来处理常规文件，并使用 `fs/read_write.c:generic_read_dir()`（它只是返回 `-EISDIR`）来处理目录。
- **write**: 实现 `write(2)` 系统调用。文件系统可以使用 `mm/filemap.c:generic_file_write()` 来处理常规文件，并在此处忽略目录。
- **readdir**: 由文件系统使用。对于常规文件被忽略，并为目录实现 `readdir(2)` 和 `getdents(2)` 系统调用。
- **poll**: 实现 `poll(2)` 和 `select(2)` 系统调用。
- **ioctl**: 实现特定于驱动程序或文件系统的 ioctls。请注意，通用的文件 ioctls，如 `FIBMAP`、`FIBGETBSZ`、`FIONREAD` 是由更高层实现的，因此它们永远不会读取 `f_op->ioctl()` 方法。
- **mmap**: 实现 `mmap(2)` 系统调用。文件系统可以使用 `generic_file_mmap` 来处理常规文件，并忽略目录。
- **open**: 在 **open(2)** 时由 `dentry_open()` 调用。文件系统很少使用这个，例如 coda 尝试在打开时本地缓存文件。
- **flush**: 在该文件的每次 **close(2)** 时调用，不一定是最后一次（参见下面的 `release()` 方法）。唯一使用此功能的文件系统是 NFS 客户端，用于刷新所有脏页。请注意，这可以

