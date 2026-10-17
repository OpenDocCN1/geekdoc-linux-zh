
# 设备驱动程序

## 4. 内核缓冲区与模块验证

上面的实际函数是 `printk` 和 `sprintf`。列表显示我们目前运行着启用了模块版本的 SMP 内核。为了解析这些名称，模块必须包含 `linux/modversions.h` 文件。

命名空间是另一个你之前可能没有特别注意的问题，除非你工作过大型项目。在开发驱动程序时，你应该小心污染全局内核命名空间。避免冲突的一种极佳方法（绝大多数内核开发者采用）是为导出的函数加上你的驱动程序的前缀。尽管如此，只导出会被其他驱动程序使用的函数和变量是另一个重要的实践。将全局变量和函数声明为 `static`（静态）虽然很完美地解决了问题，但会有其他副作用。变量和函数通过 `EXPORT_SYMBOL` 宏显式导出，该宏会将它们添加到内核符号表中。如果你将版本拆分为多个模块或以其他方式暴露内部供他人使用，通常需要担心这个。当然，将全局命名空间污染降到最低始终是一个好主意。语法非常直接：

| 宏 | 描述 |
| :--- | :--- |
| `EXPORT_SYMBOL(name)` | 导出变量或函数名 |
| `EXPORT_SYMBOL_NOVERS(name)` | 导出变量或函数名，但即使定义了也不包含版本控制 |
| `EXPORT_NO_SYMBOLS` | 不导出任何符号。 |

声明必须在任何函数之外进行——例如在包含文件中或模块代码的末尾。这些宏定义在头文件中。

数据类型

...（后续重复内容已省略）

# 4. 我们可以在内核缓冲区中看到来自我们模块的消息。为了证明模块已加载，可以运行 `lsmod`（列出模块）。它会列出当前插入的模块。

```
# lsmod

Module Size Used by

...

hello 176 0 (unused)
```

5. 出乎意料的是，`hello` 与其他模块一起列出了。`lsmod` 还会列出每个加载模块的大小和使用计数。我们稍后会详细介绍使用计数。现在，让我们再次移除 `hello` 模块。`rmmod`（移除模块）命令将一个模块从内核中卸载。

```
# rmmod hello

# dmesg | tail

Good-bye, kernel!
```

## 工作原理

这里这里引入了一些新内容。`linux/module.h`（以及其他文件）调用了 `linux/config.h`，后者包含了内核编译时选择的选项和定义。这对我们来说特别有用，我们可以确定内核是针对 SMP 编译的，即 `CONFIG_SMP_MODVERSIONS`；如果经过配置，则会定义 `MODVERSIONS` 并包含 `linux/modversions.h` 以访问版本信息。

正如我们所看到的，当模块加载和卸载时，内核缓冲区会打印一条短消息。我们定义的执行此操作的两个函数是完成模块的全部。`init_module` 在加载时被调用，负责设置初始数据结构、初始化硬件以及执行在设备首次调用之前需要完成的任何其他任务。由于上述只是简单的框架，此处没有具体工作。大多数操作都是双向的，因此 `cleanup_module` 负责关闭设备并释放设备可能占据的任何资源。

就是这样！我们构建了一个模块并成功地将其插入内核。现在我们克服了对 Linux 内核的恐惧，可以开始学习更有实质的内容了。

## 字符设备

虽然上一节中的 `hello` 模块已经简单到极致了，但它实际上并没有做任何事情。一旦它被加载，你就可以与之交互，但它不会向用户空间应用程序导出任何函数。作为进一步的的第一步，让我们看看字符驱动驱动的示例框架。

字符驱动设备是以字符（字节）作为输入输出基本单位操作的设备。它们以顺序或随机的方式被访问。其他类型的设备是块驱动的，其中连续的数据块是 I/O 的基本单位；以及包驱动的（例如网络接口卡），其中 I/O 的基本单位是包。块驱动可以进行随机访问，而字符驱动则不能。

## 第 18 章

设备必须向内核注册自身，并提供相关信息，以便当应用程序想要与设备交互时内核能够调用正确的函数。`register_chdev` 处理此工作，并以以下语法被调用：

```
int register_chdev(unsigned int major, const char *name, struct file_operations *fops)
```

如果失败，返回值为负；成功则返回非负值（正整数或零），内核函数正是如此。使用 `0` 作为主号（major number）调用该函数将提供动态主号分配。在这种情况下，设备将使用下一个可用的主号注册，并返回该号。使用动态分配并不困难，但为了访问设备，如果上次加载模块时主号发生了变化，你需要创建特殊文件。因如此，我们将在本章中使用一系列预留的主号。

主号 42-127 留给本地设备，因此不供生产模块使用。请咨询 `Documentation/devices.txt` 了解更多信息，以及如果你确实需要，如何获取官方主号。

第二个参数 `name` 仅用于注册，没有其他用途。`/proc/devices` 文件仅仅是显示在那里的名称。文件操作结构（file operations structure）是最有趣的部分。它定义了驱动程序如何与外部世界通信——具体由哪些它自己处理，哪些由内核处理。该结构定义在 `linux/fs.h` 中，是一系列指向函数的指针。这个概念用于内核的许多地方，并在不同层及其交互方式之间提供了一种抽象形式。

## 文件操作

正如本章开头提到的，对字符和块设备的访问通过文件系统进行。本章与设备类型无关——它直接相关文件系统（例如硬盘驱动程序）或完全无关（可能是并行端口驱动程序）。设备驱动需要注册一组文件操作，以定义它们提供的特定实现。下面是带有定义原型的文件操作结构。列出了所有可能的函数类型，尽管没有任何内核模块需要定义所有类型。你会发现这些函数名称是熟悉的，它们镜像了我们在第 3 章中讨论过的低级设备访问函数。当内核识别出满足该请求需要完成的任务时，这些函数实际上是这些低级调用的终点。

```c
struct file_operations {
    struct module *owner;
    loff_t (*llseek)(struct file *, loff_t, loff_t);
    size_t (*read)(struct file *, char *, size_t, struct file_t *);
    size_t (*write)(struct file *, const char *, size_t, struct file_t *);
    int (*readdir)(struct file *, void *, fildir_t);
    unsigned int (*ioctl)(struct file *, struct poll_table_struct *);
    int (*poll)(struct file *, struct inode *, unsigned int);
    int (*mmap)(struct file *, struct vm_struct);
    int (*open)(struct inode *, struct file *);
    int (*flush)(struct inode *, struct file);
    int (*release)(struct inode *, struct file *);
    int (*fsync)(struct file *, int);
    int (*async)(struct file *, int);
    int (*lock)(struct file *, int);
    ssize_t (*readv)(struct file *, struct iovec, unsigned long);
    ssize_t (*writev)(struct file *, const struct iovec, unsigned long);
    ssize_t (*sendpage)(struct file *, page *, size_t, loff_t *);
    unsigned long (*get_unmapped)(struct file *, unsigned long);
};
```
