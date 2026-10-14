

```
int register_chrdev_region(dev_t from, unsigned count, const char *name);
int alloc_chrdev_region(dev_t *dev, unsigned baseminor, unsigned count, const char *name);
```

这两个函数之间的选择取决于你是否知道设备的主设备号。如果已知设备的主设备号，可使用 `register_chrdev_region`；如果希望动态分配一个主设备号，则使用 `alloc_chrdev_region`。

其次，我们应该为字符设备初始化数据结构 `struct cdev`，并将其与设备号关联起来。要初始化 `struct cdev`，可以通过类似下面的代码序列来实现。

```
struct cdev *my_cdev = cdev_alloc();
my_cdev->ops = &my_fops;
```

不过，常见的用法模式是将 `struct cdev` 嵌入到你自己的设备专用结构体中。在这种情况下，我们需要使用 `cdev_init` 进行初始化。

```
void cdev_init(struct cdev *cdev, const struct file_operations *fops);
```

初始化完成后，我们可以通过 `cdev_add` 将字符设备添加到系统中。

```
int cdev_add(struct cdev *p, dev_t dev, unsigned count);
```

若要查找使用该接口的示例，可以参见第 9 节中描述的 `ioctl.c`。

## 6.4 注销设备

我们不能允许内核模块在 root 用户心血来潮时就被 rmmod 卸载。如果设备文件正被一个进程打开，而我们又移除了内核模块，那么使用该文件将导致调用原先相应函数（读/写）所在的内存位置。如果幸运的话，那里没有加载其他代码，我们只会看到一条难看的错误信息。如果不幸的话，另一个内核模块被加载到了同一位置，这意味着会跳转到内核中另一个函数的中间。这样做的结果是无法预料的，但肯定不会是什么好事。

通常，当你不允许某件事发生时，你会从本该执行该操作的函数中返回一个错误码（负数）。对于 `cleanup_module` 来说这不可能，因为它是一个 void 函数。不过，有一个计数器用来跟踪有多少进程正在使用你的模块。你可以通过命令 `cat /proc/modules` 或 `lsmod` 查看第 3 个字段来看到它的值。如果该值不为零，`rmmod` 将失败。注意，你不需要在 `cleanup_module` 中检查该计数器，因为系统调用 `sys_delete_module` 会替你执行检查，该调用定义在 `include/linux/syscalls.h` 中。你不应该直接使用这个计数器，但 `include/linux/module.h` 中定义了一些函数，可以让你增加、减少和显示这个计数器：

- `try_module_get(THIS_MODULE)`：增加当前模块的引用计数。
- `module_put(THIS_MODULE)`：减少当前模块的引用计数。
- `module_refcount(THIS_MODULE)`：返回当前模块的引用计数值。

保持计数器准确非常重要；如果你搞丢了正确的使用计数，你将永远无法卸载该模块；现在只能重启了，各位。在模块开发过程中，这种情况迟早会发生在你身上。

## 6.5 chardev.c

下一个代码示例创建了一个名为 `chardev` 的字符驱动程序。你可以转储它的设备文件。

```
cat /proc/devices
```

（或者用程序打开该文件），驱动程序会将设备文件被读取的次数写入该文件中。我们不支持向该文件写入（如 `echo "hi" > /dev/hello`），但会捕获这些尝试并告知用户该操作不受支持。如果你看不出我们对读入缓冲区的数据做了什么，也不必担心；我们对它做的并不多。我们只是读入数据并打印一条消息，确认已收到数据。

在多线程环境下，如果没有任何保护，对同一内存的并发访问可能会导致竞态条件，并且无法保证性能。在内核模块中，多个实例访问共享资源时也可能出现这个问题。因此，一种解决方案是强制独占访问。我们使用原子比较并交换（CAS，Compare-And-Swap）来维护状态 `CDEV_NOT_USED` 和 `CDEV_EXCLUSIVE_OPEN`，以判断该文件当前是否已被某人打开。CAS 会将某个内存位置的内容与期望值进行比较，只有在两者相同时，才将该内存位置的内容修改为期望值。更多并发细节请参阅第 12 节。

