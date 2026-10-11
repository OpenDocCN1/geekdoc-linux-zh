
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

- `owner`: 指向拥有该子系统模块的指针。只有驱动程序需要将其设置为`THIS_MODULE`，文件系统可以很高兴地忽略它，因为它们的模块计数在挂载/卸载时受控，而驱动程序需要在打开/释放时进行控制。

- `llseek`: 实现`lseek(2)`系统调用。通常省略并使用`fs/read_write.c:default_llseek`，它会做正确的事情（TODO：强制那些目前将其设置为`NULL`的人使用`default_llseek` -- 这样我们可以在`llseek()`中节省一个`if()`）。

- `read`: 实现`read(2)`系统调用。文件系统可以使用`mm/filemap.c:generic_file_read()`来处理常规文件，并使用`fs/read_write.c:generic_read_dir()`（它只是返回`-EISDIR`）来处理目录。

- `write`: 实现`write(2)`系统调用。文件系统可以使用`mm/filemap.c:generic_file_write()`来处理常规文件，并在此处忽略目录。

- `readdir`: 由文件系统使用。对于常规文件被忽略，并为目录实现`readdir(2)`和`getdents(2)`系统调用。

- `poll`: 实现`poll(2)`和`select(2)`系统调用。

- `ioctl`: 实现特定于驱动程序或文件系统的ioctls。请注意，通用的文件ioctls，如`FIBMAP`、`FIBGETBSZ`、`FIONREAD`是由更高层实现的，因此它们永远不会读取`f_op->ioctl()`方法。

- `mmap`: 实现`mmap(2)`系统调用。文件系统可以使用`generic_file_mmap`来处理常规文件，并忽略目录。

- `open`: 在`open(2)`时由`dentry_open()`调用。文件系统很少使用这个，例如coda尝试在打开时本地缓存文件。

- `flush`: 在该文件的每次`close(2)`时调用，不一定是最后一次（参见下面的`release()`方法）。唯一使用此功能的文件系统是NFS客户端，用于刷新所有脏页。请注意，这可以返回一个错误，该错误将被传回触发`close(2)`系统调用的用户空间。

- `release`: 在此文件的最后一个`close(2)`时调用，即当`file->f_count`变为`0`时。尽管定义上返回`int`，但其返回值被VFS忽略（参见`fs/file_table.c:__fput()`）。

- `fsync`: 直接映射到`fsync(2)`/`fdatasync(2)`系统调用，最后一个参数指定它是`fsync`还是`fdatasync`。围绕此操作，VFS几乎不做任何工作，除了将文件描述符映射到文件结构（`file = fget(fd)`以及`inode->i_sem`信号量的down/up）。Ex2文件系统目前忽略最后一个参数，对`fsync(2)`和`fdatasync(2)`执行完全相同的操作。

- `fasync`: 当`file->f_flags & FASYNC`发生变化时调用此方法。

- `lock`: POSIX`fcntl(2)`文件区域锁定机制中文件系统特定的部分。这里唯一的bug是，因为它在独立于文件系统的部分（`posix_lock_file()`）之前被调用，如果它成功但标准的POSIX锁代码失败，那么在文件系统依赖的层面上永远不会解锁。

- `ready`: 实现`ready(2)`系统调用。

- `writenv`: 实现`writenv(2)`系统调用。

### 3.5 超级块和挂载点管理

在Linux下，已挂载文件系统的信息存储在两个独立的结构中 - `super_block`和`vfsmount`。这样做的原因是Linux允许将同一个文件系统（块设备）挂载到多个挂载点，这意味着同一个`super_block`可以对应多个`vfsmount`结构。

让我们首先看看在`include/linux/fs.h`中声明的`struct super_block`：
