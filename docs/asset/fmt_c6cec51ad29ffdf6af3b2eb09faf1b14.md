
# 第 18 章 在用户空间和内核空间之间传输

## 18.9. 中继通道 (RELAY CHANNELS)

```c
if (rc != size)
    DEATH("写入失败");
exit(EXIT_SUCCESS);
```

```c
}
static void exit_void(void)
{
    dev_del(my_dev);
    unregister_chr_region(first, count);
    printk(KERN_INFO "设备已注册\n");
}
```

这是一个带有 `mmap()` 入点的简单驱动程序

```c
/* 带有 mmap() 的示例字符设备驱动 */
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/access.h>
#include <linux/slab.h>
#include <linux/dev.h>
/* 模块相关 */
/* 文件操作 file_operations */
/* copy(to,from_user) */
/* mmap_iter, mmap_exit */
/* kmalloc */
/* cdev 工具类 */
/* remap_pfn_page */
```

```c
module_init(void);
module_exit(void);
MODULE_AUTHOR("Jerry Cooperstein");
MODULE_DESCRIPTION("模块描述名称");
MODULE_LICENSE("GPL v2")
```

## 18.9 中继通道

人们可能会产生内核空间和用户空间之间传输信息的需求，但并非所有需求都是相同的。人们可能需要双向传输、效率或保证。也可能正在处理单个设备，并且数据量大或小。

内核填充中继通道缓冲区，对数据格式没有特殊的竞争限制。用户通过系统调用或 `mmap()` 在数据文件上访问数据（每个通道对应一个文件），这些文件被视为普通的管道。

对于每个中继通道，每个 CPU 都有一个缓冲区。在每个缓冲区中，有一个或多个子缓冲区。

当一个子缓冲区填满了一块数据，或者使用下一个缓冲区（如果可用）时，消息会在子缓冲区之间合并（消息的大小不应大于子缓冲区）。如果可以分配空间，则子缓冲区为满。

缓冲区可以设置为覆盖模式或非覆盖模式（默认模式）；在内核模式下，内核客户端将阻塞，直到读取者清空缓冲区。

```c
static dev_t dev;
static int registered_count = 1;
static int my_major = 700, my_minor = 0;
static struct cdev cdev_dev;
```

```c
static int my_mmap(struct file *file, struct vm_area_struct *vma)
{
    printk(KERN_INFO "进入 mmap 函数:\n");
    if (remap_pfn_range(vma->vm_area, vma->vm_start, vm_start, vma->vm_end - vma->vm_start, vma->vm_prot))
    {
        return -EAGAIN;
    }
```

```c
return 0;
```

```c
// 不要使用 * 扰 open, release 和 read
```

```c
static struct file_operations mydev_fops
{
    .owner = THIS_MODULE,
    .mmap = my_mmap,
}
```

```c
static int my_init(void)
{
    first = register_chrdev(my_major, count, &mydev_fops);
    cdev_dev;
```

当用户空间应用程序调用 `read()` 系统调用时，必须移除子缓冲区末尾的任何填充并执行排空操作。这比仅仅使用 `reads` 更高效，但也更复杂。

以下是可以在中继通道上使用的系统调用列表：

- `open`/`close`: 打开和关闭已有的缓冲区。如果没有其他进程（内核客户端）正在使用，则释放通道（计数减1）。
- `read()`: 从通道中消耗字节。在非覆盖模式下，内核客户端同时写入是没问题的，但在覆盖模式下会发生不可预测的结果。子缓冲区将通过填充进行补齐。
- `mmap()`, `munmap()`: 必须映射整个缓冲区，且没有排空操作。
- `sendfile()`: 排空一次读取。
- `poll()`: 当到达子缓冲区时，会通知应用程序，并设置 `POLLIN`、`POLLRDNORM`、`POLLERR` 标志。

## 18.11. 从内核访问文件

```c
int mode,
struct rchan_buf *buf,
int (*is_global);
```

该机制的工作可以使用其他方法完成，例如使用 `/proc` 文件系统、`ioctl()`（可以从内核直接打开文件或真实设备），或者最糟糕的情况下，使用中继通道提供了一种清晰（且被批准）的方法，并被强烈考虑。

```c
int (remove_buf_file(struct rchan *chan));
```

当切换到新的子缓冲区时会调用 `subbuf_start()`。当缓冲区映射或取消映射时，调用 `buf_mapped()` 和 `buf_unmapped()`。

`create_buf_file` 创建并删除与中继通道关联的文件。注意，如果参数不为零，则在多个 CPU 上将只有一个文件：在这种情况下，你需要考虑到任何竞态条件。该参数提供了用户权限并指定父目录。文件必须通过此方法创建/删除。

## 18.10 中继 API

对于这些文件应该放在哪里没有严格要求。一个方便的地方是 `debugfs`。在这种情况下：

打开和关闭中继通道通过以下方式完成：

```c
#include <linux.h>
struct rchan relay_open(const char *filename,
                               size_t parent,
                               size_t buf_size,
                               size_t n_buffers,
                               struct rchan *callbacks,
                               void *private);
```

```c
.create_buf_handler(const char *filename,
                               struct rchan *parent,
int mode,
int (*is_global);
```

```c
void relay_close(struct rchan *chan)
```

```c
debugfs_create_file(filename, parent, buf,
                                     relay_file_operations);
```

```c
static int remove_buf_handler(struct dentry *dentry)
```
每个 CPU 关联一个文件；例如，如果 `filename="my_chan"`，文件将命名为 `"my_chan.0, my_chan.1..."`，它们出现在指定的父目录下；如果是 `NULL`，它们将出现在文件系统中。

```c
return 0;
```
每个 `n` 个子缓冲区的大小均为 `buf_size`，因此缓冲区的总大小为 `n * buf_size`。内核写入的内容不应大于 `buf_size` 且不能跨越缓冲区。

```c
struct rchan_relay_callbacks {
```
