
# 设备驱动程序

你的驱动程序可以提供这些函数的组合，以便向内核表示设备的功能。可用函数如下表所示。

| 函数 | 描述 |
| :--- | :--- |
| `lseek` | `lseek` 在用户空间视角下更改位置。具体来说，它会修改 `file->pos`；我们稍后会讨论。成功时返回新位置，失败则用负值标识。 |
| `read` | `read` 从应用程序视角看，将数据写回用户空间。返回值为正表示读取的字节数。负值表示错误。 |
| `write` | `write` 将数据馈给设备，返回值与 `read` 相同。 |
| `readdir` | `readdir` 严格用于文件系统查找目录内容 |
| `poll` | `poll` 允许应用程序获取设备事件通知；BSD UNIX 中的 `select` 在 Linux 中已废弃，应该使用 `poll`。 |
| `ioctl` | `ioctl` 或 I/O 控制允许应用程序通过 `ioctl` 系统调用控制设备行为或从设备获取数据。 |
| `mmap` | `mmap` 实现设备地址空间到用户空间的映射。这可以用于直接访问内部缓冲区或外围设备内存空间。 |
| `open` | `open` 在应用程序打开设备时被调用。这是唯一对字符和块设备都有默认实现的函数，如果你不需要知道设备何时打开，可以留空不定义。 |
| `flush` | `flush` 自然地刷新缓冲区数据。由于字符设备没有缓冲区，此项仅对块设备有意义。 |
| `release` | `release` 在设备关闭时被调用。 |
| `fsync` | `fsync` 同步内存状态与设备状态，写入输出缓冲区中的脏数据。在完成之前不能返回。此项仅与块设备相关。 |
| `async` | `async` 在应用程序通过 `fcntl` 设备行为时被调用。 |
| `lock` | `lock` 允许用户锁定文件——仅对文件系统真正有意义。 |
| `readv` | `readv` 根据 `iovec` 描述的缓冲区向量从设备读取数据。 |

# 第 18 章

| 方法 | 描述 |
| :--- | :--- |
| `writev` | `writev` 类似于 `readv`，它从 `iovec` 描述的缓冲区中写入数据 |
| `sendpage` | `sendpage` 用于一次写入一个页，通常与网络文件系统配合使用 |
| `get_unmapped_area` | `get_unmapped_area` 用于确定设备的哪些部分没有映射内存 |

单个设备可能永远不需要定义上述所有方法。完全取决于你如何定义对你的设备设备有意义的操作，并对未实现的方法设置为 `NULL`。

当字符设备向内核注册时，它的 `file_operations` 结构体和名称会被添加到 `device_struct` 结构的全局 `chrdev` 数组中，其中主设备号（major number）对其进行索引。这就是字符设备切换表。

```c
struct device_struct {
    const char *name;
    struct file_operations *fops;
};
```

因此，通过查找 `chrdevs [YOUR_MAJOR] -> fops`，内核知道如何与设备通信以及它支持哪些入口点（见图 18-2）。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_773_0.png)
图 18-2

# 示例驱动程序：`schar`

让我们来看一个字符设备驱动示例，我们称之为 `schar`。该驱动通过假从一个按恒定间隔轮询的设备提供数据，以自己的方式实现了读写功能。轮询机制由内核定时器管理，我们将在下一节中详细解释。

`schar.c` 开始于定义我们 `file_operations` 结构体实现函数的前声明。然后我们填充它的内容。

## 设备驱动程序

```c
/* _fops 的前声明 */

static ssize_t schar_read(struct file *file, char *buf, size_t count, loff_t *offset);

static ssize_t schar_write(struct file *file, const char *buf, size_t count, loff_t *offset);

static unsigned int char_poll(struct file *file, poll_table *wait);

static int char_ioctl(struct inode *inode, struct file *file, unsigned int cmd, unsigned long arg);

static int schar_mmap(struct file *file, struct vm_area_struct *vma);

static int schar_open(struct inode *inode, struct file *file);

static int schar_release(struct inode *inode, struct file *file);

static struct file_operations schar_fops = {
    read = schar_read,
    write = schar_write,
    poll = schar_poll,
    ioctl = schar_ioctl,
    open = schar_open,
    release = schar_release,
};
```

有些人喜欢将 `file_operations` 结构体放在模块开头，而另一些人则喜欢放在底部。后者的方法可以让我们避免在文件开头放置函数原型。这纯粹是喜好问题。不要担心任何包含文件；我们会在后续过程中解决这些问题。

## `MSG` 宏

在深入研究 `schar` 源码之前，我们需要介绍在整个章中使用的 `MSG` 宏。这是打印调试语句的替代方式，被证明非常有用。我们没有在代码中散布丑陋的 `#ifdef` 语句，而是将 `MSG` 的定义放在 `schar.h` 中：

```c
#define DEBUG

#ifdef DEBUG

#define MSG(string, args...) printk(KERN_DEBUG "schar: " string, ##__ARGS__)

#else

#define MSG(string, args...)

#endif
```

它保持了代码的整洁，并在每个语句前加上了模块名称。如果你愿意，可以轻松地定义一个事件位图并获得精细控制的日志。`schar` 很简单，所以一切都很合理。定义 `DEBUG` 会实际上让 `MSG` 变成一个空操作（no-op）。有时，在调试语句中包含更多信息是有利的，特别是对于较大的设备驱动程序。我们可能想要包含行号和文件名信息，以便快速在源码中定位特定消息。它看起来像这样：

```c
#define MSG(string, args...) printk(KERN_DEBUG "schar:%FILE:%__LINE__: ", string, ##__ARGS__)
```

选择哪种取决于你；书中的所有模块都使用前者，因为它们的复杂性不需要这些额外信息。

## 注册设备

与 `hello` 模块一样，`schar` 自然也有一个 `init_module` 入口点。它执行许多不同的操作——分配内存、初始化定时器和变量等——但目前我们将只关注设备注册。

```c
int init_module(void)
{
    int res;

    if (schar_name == NULL)
        schar_name = "schar";

    /* 向内核注册设备 */

    res = register_chrdev(CHAR_MAJOR, schar_name, &schar_fops);

    if (res) {

        MSG("can't register device with kernel\n");

    }

    return res;

}
```

`schar_name` 可以作为参数传递给模块——我们稍后会看到。现在，我们检查是否指定了名称，如果没有，则进行设置。`SCHAR_MAJOR` 的定义如下。动态分配的优点在于我们不需要知道任何信息。缺点（至少在这个语境下）是我们将必须创建新的设备。我们将使用静态数字。

```c
#define SCHAR_MAJOR 42
```

```c
int major = 0, res;

res = register_chrdev(CHAR_MAJOR, schar_name, &schar_fops);

if (res < 0) {

    MSG("can't register device with kernel\n");

} else {

    major = res;

    MSG("device registered with major %d\n", major);

}
```
