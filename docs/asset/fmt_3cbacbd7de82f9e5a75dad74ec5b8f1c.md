
```c
struct file_operations {
    struct module *owner;
    loff_t (*read)(struct file *file, loff_t *pos);
    ssize_t (*write)(struct file *file, char __user *buf, size_t count, loff_t *pos);
    ssize_t (*ioctl)(struct file *file, const __user *buf, unsigned int cmd, unsigned long arg);
    int (*mmap)(struct file *file, struct vm_area_struct *vma);
    int (*open)(struct file *file, struct inode *inode, int filp);
    int (*release)(struct file *file, struct inode *inode, int flags);
    int (*flush)(struct file *file, int *wait);
    int (*fsync)(struct file *file, struct inode *inode, int datasync);
    int (*direct_map)(struct file *file, struct page *page, pgo_t offset, size_t len);
    ssize_t (*read_iter)(struct file *file, struct ki_iter *iter);
    ssize_t (*write_iter)(struct file *file, struct ki_iter *iter);
    struct file_operations (*_갈)(struct file *file, loff_t *pos);
    ssize_t (*update_size)(struct file *file, size_t count, loff_t *pos);
    int (*special_open)(struct file *file, struct inode *inode, struct file_operations *fop);
    int (*special_release)(struct file *file, struct inode *inode, int flags);
    int (*flush_lock)(struct file *file, struct inode *inode, int flags);
    int (*set_size)(struct file *file, struct inode *inode, size_t count);
    int (*get_size)(struct file *file, struct inode *inode);
};
```

除了第一个字段 `owner` 用于引用计数外，它是驱动程序条目的跳转表。

该结构还用于字符设备以外的其他用途，例如文件系统，某些条目也用于这些领域。后续讨论的 `file` 和 `inode` 结构也是如此。

文件操作结构使用如下代码进行初始化：

```c
struct file_operations fops = {
    owner = THIS_MODULE,
    open = my_open,
    release = my_release,
    read = read,
    write = my_write,
    lock = my_lock,
};
```

根据 C 语言标准，初始化哪些字段是无关的，任何未指定的字段将填充为零。

这些操作与 `dev_init()` 函数关联，该函数将指向 `file_operations` 结构的指针放在正确的顺序中。每对设备拥有的设备节点进行相应的调用时，工作将传递给驱动程序；例如，对设备节点调用 `open` 将调用上述的方法。

# 第 4 章 字符设备

## 4.8 驱动入口点

`struct module *owner;`

该结构体中唯一一个不是方法的字段。指向拥有该结构体的模块，用于引用计数，并在模块正在加载时移除该模块以避免竞态条件。通常设置为 `THIS_MODULE`。

如果使用 `KERNEL_GFP`，内存分配块将是可用的；如果使用 `GFP_ATOMIC`，请求是非阻塞的。我们将详细讨论内存分配。

设备中的位置通过修改 `vpos` 的值来更新，`vpos` 指向当前值。返回成功读取的字节数；如果由于原因返回负值，则返回 `-1`。

```c
loff_t (*read)(struct file *file, loff_t *offset, int);
```

```c
size_t (*write)(struct file *file, const char *user, size_t size,
loff_t *offset);
```

这更新文件的读/写位置，并返回新位置。注意在 32 位架构上 `loff` 是 64 位的。

写入数据，返回写入的字节数。负值表示错误：可能是设备末尾且不是错误。如果设备未就绪且进程未设置阻塞标志，你也可以选择阻塞。

如果如果人们想在设备上禁止寻道，如上所示，可以在文件结构体中使用 `FMOD_SEEK`，最好在 `open()` 方法中使用：

关于使用用户指针也适用相同的考虑。这里应该使用：

```c
file_f *f_mode = file->f_mode & ~FMOD_SEEK;
```

```c
int bytes = copy_from_user(vpos, user_buf, buf);
```

```c
size_t (*release)(struct file *file, char *user, size_t size, loff_t *pos);
```

从数据中读取，返回读取的字节数。负值表示错误：可能是设备末尾且不是错误。如果数据未就绪且进程设置了非阻塞标志，你也可以选择阻塞。

```c
int (*open)(struct inode *inode, struct file *file, int mode);
```

一个简单的 `read()` 可能看起来如下：

**应该** 用于设备节点；仅用于目录，并由文件系统驱动程序使用，驱动程序使用 `file_operations` 结构。

```c
ssize_t my_read(struct file *file, char __user *, size_t, loff_t *pos) {
```

```c
unsigned int (*locked)(struct inode *inode, struct file *file, struct file_table *);
```

```c
int bytes = copy_from_user(vpos, user_buf, buf);
```

检查设备是否可读、可写或某些特殊用户。在用户空间中，通过 `poll()` 和 `select()` 调用访问它。返回描述设备状态的负值。

```c
  if (bytes < 0) {
    return -EFAULT; // READING buffer
  }
  return bytes;
}
```

在这种情况下，`read` 方法从内核态的缓冲区 `ptr` 拷贝到用户态的缓冲区 `buf`。但不能使用 `memcpy()`，因为在内核空间中解引用用户指针是不恰当的；该地址可能没有指向有效的内存页，可能是因为它尚未分配，或者已经被交换出。

必须使用 `copy_to_user()` 和 `copy_from_user()` 函数，它们会处理这些问题。取决于方向，我们将看到更多使用额外拷贝的高级技术，包括内存映射、原始 I/O。

内核栈是动态分配的，因此每个任务的栈是有限的。这必须通过以下方式完成：

- 如果设备未就绪，检查硬件。
- 如果需要，设备设备号。
- 使用文件的 `private_data` 设置任何数据结构。

```c
struct kmem_cache *slab;
char *buffer = kmalloc(size, GFP_KERNEL);
```

```c
kfree(buffer);
```

限制为 1024 页，在 x86 上为 4 MB。

## 4.9 文件和节点结构

```c
int (*flush)(struct file *file);
```

当驱动打开其文件描述符时执行并等待设备上的挂起操作。很少使用。如果失败，则返回 NULL。

```c
int (*dir_notify)(struct file *file, unsigned long arg);
```

当调用 `fcntl()` 时调用，以报告设备变化。驱动程序未使用。

```c
int (*release)(struct inode *inode, struct file)
```
