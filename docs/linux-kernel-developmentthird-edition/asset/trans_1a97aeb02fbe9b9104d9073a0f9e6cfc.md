
尽管 `default_attrs` 列出了默认属性，但 `sysfs_ops` 描述了如何使用它们。`sysfs_ops` 成员是指向同名字结构体的指针，该结构体定义在 `<linux/sysfs.h>` 中：

```c
struct sysfs_ops {
    /* method invoked on read of a sysfs file */
    ssize_t (*show) (struct kobject *kobj,
                struct attribute *attr,
                char *buffer);

    /* method invoked on write of a sysfs file */
    ssize_t (*store) (struct kobject *kobj,
                struct attribute *attr,
                const char *buffer,
                size_t size);
};
```

当从用户空间读取 sysfs 条目时，会调用 `show()` 方法。它必须将由 `attr` 指定的属性值复制到由 `buffer` 提供的缓冲区中。缓冲区长度为 `PAGE_SIZE` 字节；在 x86 架构上，`PAGE_SIZE` 为 4096 字节。成功时，函数应返回实际写入 `buffer` 的数据字节数；失败时返回负错误码。

写入时会调用 `store()` 方法。它必须从 `buffer` 读取 `size` 个字节，并存入由属性 `attr` 表示的变量中。缓冲区的大小始终为 `PAGE_SIZE` 或更小。成功时，函数应返回从 `buffer` 读取的数据字节数；失败时返回负错误码。

由于这组函数必须处理 *所有* 属性上的文件 I/O 请求，通常它们需要维护某种通用映射，以调用特定于每个属性的处理程序。

## 创建新属性

通常，kobject 关联的 ktype 提供的默认属性就足够了。事实上，ktype 的目的就是为 kobjects 提供通用操作。在 kobjects 之间共享 ktype 不仅简化了编程，还提供了代码整合，并为相关对象的 sysfs 目录提供统一的外观和体验。

尽管如此，某些特定的 kobject 实例往往有其特殊性。它想要甚至需要自己的属性——也许是提供不被更通用的 ktype 共享的数据或功能。为此，内核提供了 `sysfs_create_file()` 接口，用于在默认集合之上添加新属性：

```c
int sysfs_create_file(struct kobject *kobj, const struct attribute *attr);
```

此函数将 `attr` 指向的 `attribute` 结构体与 `kobj` 指向的 kobject 关联起来。在调用之前，给定的属性应已填写完毕。成功时此函数返回零，否则返回负错误码。

请注意，kobject 的 ktype 中指定的 `sysfs_ops` 将被调用以处理此新属性。现有的默认 `show()` 和 `store()` 方法必须能够处理新创建的属性。

除了创建实际文件外，还可以创建符号链接。在 sysfs 中创建符号链接很容易：

```c
int sysfs_create_link(struct kobject *kobj, struct kobject *target, char *name);
```

此函数在从 `kobj` 映射的目录中创建一个名为 `name` 的链接，指向从 `target` 映射的目录。成功时此函数返回零，否则返回负错误码。

### 销毁属性

通过 `sysfs_remove_file()` 处理属性移除：

```c
void sysfs_remove_file(struct kobject *kobj, const struct attribute *attr);
```

调用返回后，给定的属性将不再出现在给定 kobject 的目录中。使用 `sysfs_create_link()` 创建的符号链接可以通过 `sysfs_remove_link()` 移除：

```c
void sysfs_remove_link(struct kobject *kobj, char *name);
```

返回后，从 `kobj` 映射的目录中的符号链接 `name` 被移除。这四个函数均声明在 `<linux/kobject.h>` 中。`sysfs_create_file()` 和 `sysfs_remove_file()` 函数定义在 `fs/sysfs/file.c` 中。`sysfs_create_link()` 和 `sysfs_remove_link()` 函数定义在 `fs/sysfs/symlink.c` 中。

### sysfs 约定

sysfs 文件系统目前是*用于*实现之前保留给设备节点上 `ioctl()` 调用或 proc 文件系统的功能的地方。代替这些已弃用的内核接口，如今的内核开发人员将此类功能实现为适当目录中的 sysfs 属性。例如，不要使用设备节点上的新 `ioctl()`，而是在驱动程序的 sysfs 目录中添加一个 sysfs 属性。这种方法避免了使用晦涩且类型不安全的 `ioctl()` 参数以及 `/proc` 的杂乱无章。

然而，为了保持 sysfs 的整洁和直观，开发人员必须遵循某些约定。首先，sysfs 属性应每个文件导出一个值。值应为基于文本的，并映射到简单的 C 类型。目标是避免我们在 `/proc` 中看到的当前高度结构化或高度混乱的数据表示。每个文件提供一个值使得从命令行进行读写变得简单，并使 C 程序能够轻松地将内核数据从 sysfs 读入其自身的变量中。在“每文件一个值”规则导致数据表示低效的情况下，允许在一个文件中放置多个相同类型的值。请适当分隔；简单的空格可能最有意义。最终，将 sysfs 属性视为映射到单个内核变量（通常如此），并记住从用户空间（特别是 shell）操作的便捷性。

其次，在 sysfs 中组织数据时要保持清晰的层次结构。正确设置 kobjects 的父子关系，使它们在 sysfs 树中直观地映射。将属性与正确的 kobject 关联，并记住 kobject 层次结构不仅存在于内核中，也作为导出树存在于用户空间中。保持 sysfs 树有序且具有层次性。

最后，请记住 sysfs 提供的是内核到用户的服务，因此它是某种用户空间 ABI。用户程序可以依赖 sysfs 目录和文件的存在、位置、值和行为。不鼓励以任何方式修改现有文件，并且修改给定属性的*行为*但保留其名称和位置无疑是自找麻烦。

这些简单的约定应使 sysfs 能够提供丰富且直观的用户空间接口。正确使用 sysfs，用户空间开发人员就可以拥有一个简单、整洁，强大且直观的内核接口。

## 内核事件层

内核事件层在 kobjects 之上实现了一个内核到用户的通知系统。在 2.6.0 发布后，人们认识到需要一种机制将事件从内核推送给用户空间，特别是对于需要更集成和异步系统的桌面系统。这个想法是让内核将事件推送到堆栈的上层：硬盘满了！处理器过热！分区已挂载！

早期版本的事件层来来去去，不久之后，整个事件机制就紧密地绑定在 kobjects 和 sysfs 上。事实证明，结果相当不错。内核事件层将事件建模为*信号*从对象发出——具体来说，是从 kobjects 发出。由于 kobjects 映射到 sysfs 路径，每个事件的*源*就是一个 sysfs 路径。如果相关事件涉及您的第一个硬盘，`/sys/block/sda` 就是源地址。内部地，在内核中，我们将事件建模为源自后备 kobject。

每个事件被赋予一个*动词*或*动作*字符串来表示该信号。这些字符串是描述发生什么的术语，如 *modified*（修改）或 *unmounted*（卸载）。

最后，每个事件都有一个可选的负载。内核事件层不向用户空间传递提供负载的任意字符串，而是将负载表示为 sysfs 属性。

内部地，内核事件通过 netlink 从内核空间传出到用户空间。Netlink 是一种高速多播套接字，用于传输网络信息。使用 netlink 意味着从用户空间获取内核事件就像阻塞在套接字上一样简单。意图是用户空间实现一个系统守护进程，该进程监听套接字，处理任何读取事件，并将事件传输到系统堆栈的上层。对此类用户空间守护进程的一个可能提案是将事件集成到 D-BUS[^2] 中，它

[^2]: 有关 D-BUS 的更多信息可在 http://dbus.freedesktop.org/ 获取。

