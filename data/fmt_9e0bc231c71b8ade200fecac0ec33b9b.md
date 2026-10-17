
# 第 17 章 kobjects 和 sysfs

此函数将引用计数减 1，如果计数现在为 0，则调用提供的 `release()` 函数。正如那不详的 `WARN_ON()` 语句所示，提供的 `release()` 函数不能简单地是 `free()`，而必须是一个接受 `kref` 作为唯一参数且没有返回值的特殊函数。

与其让内核代码通过原子类型和简单的“get”和“put”封装函数来实现它自己的引用计数，不如鼓励开发者使用 `kref` 类型及其辅助函数，在内核中提供一种通用且已知的引用计数。

所有这些函数都定义在 `lib/kref.c` 中，并在 `<linux/kref.h>` 中声明。

## sysfs

sysfs 系统是一个内存中的虚拟文件系统，提供了内核对象层次结构的视图。它使用户能够像简单的文件系统一样查看系统的设备拓扑结构。通过属性（attributes），kobjects 可以导出文件，允许从内核读取内核变量并可选地写入。

尽管设备模型的本意是为了电源管理原因提供设备拓扑结构，但 sysfs 是一次巨大的跨越。为了方便调试，设备模型的开发者决定将设备导出为文件系统。这在以前位于 `/proc` 中，后来变成了系统对象层次结构的强力视图。索引化的 sysfs（通常称为驱动程序）早于对象（objects）。最终，sysfs 明确了新的对象模型将将是有益且可共享的。今天，每个运行 2.6 内核的系统以及几乎所有的系统都挂载了它。

sysfs 背后的魔法简单地通过每个 kobject 内部的 `d` 变量将 kobjects 绑定到目录项（dentry）。回想第 12 章“虚拟文件系统”，dentry 结构代表目录项。通过将 kobjects 与 dentries 链接，kobjects 轻而易举地映射到目录。将 kobjects 导出为文件系统就像在内存中构建节点树一样简单。等等！kobjects 可爱的设备模型已经形成了一棵树。由于 kobjects 映射到 dentries 且对象层次结构已经形成了内存中的树，sysfs 的实现变得轻而易举。

图 17.2 是挂载在 `/sys` 的 sysfs 文件系统的部分视图。

```
/sys/

- block/

  - fd0

    - hda0

    │   - dev

    │   - device -> ../../devices/pci000:00:00:00:01f.1/ide0/0.0

    │   └── hdal

       - ddev

       - size

       - start

       -└── stat

  - hda2

  - hda3

  - hda4

  - hda5

  - hda6

  - queue

  - hdc

  - hdd0

  - loop0

  - loop1

  - loop2

  - loop3

  - loop4

  - loop5

  - loop6

  - loop7

  - md0

- bus/

- class/

  - devices/

  - firmware/

  - power/
```

> 图 17.2 `/sys` 树的部分视图。

最重要的数据是 `devices`，它将设备模型导出到整个世界。目录结构是系统的实际设备拓扑结构。其他目录中的大部分数据只是数据目录的另一种组织形式。例如，`/sys/class/net/` 根据注册网络接口的高层概念来组织设备。在该目录内部可能是子设备 `eth0`，它包含了连接回 `devices` 中实际设备目录的设备链接。

看看你所访问的任何 Linux 系统上的 `/sys`。这种对系统设备的准确视图非常酷，而且 `class` 中的高层概念与 `devices` 中的低层物理设备以及 `bus` 中的实际驱动程序之间的相互连接非常有启发性。当你意识到这些数据是免费的，这些数据正是内核内部维护的系统表示时，整个体验会变得更加有回报。

- 如果你觉得 sysfs 有趣，你可能对 HAL（硬件抽象层）感兴趣，可以在 `http://freedesktop.org/` 找到它。HAL 基于类、设备和驱动程序的概念构建了内存数据库。

## 在 sysfs 中添加和移除 kobjects

初始化的 kobject 不会自动导出到 sysfs。要将 kobject 表示到 sysfs，使用 `kobject_add()`：

```c
int kobject_add(struct kobject *kobj);
```

kobject 在 sysfs 中的位置取决于它在对象层次结构中的位置。如果设置了 kobject 的父指针，kobject 将映射到其父目录的子目录。如果没有设置父指针，kobject 将映射到 `kset`。如果给定的 kobject 未设置父或 `kset`，则 kobject 将映射到根目录。这几乎是你想要的，因此在调用 `kobject_add()` 之前应该适当设置它们。无论如何，kobject 在 sysfs 中的目录名称由 `kobj->k_name` 给出。

与其分别调用 `kobject_init()` 和 `kobject_add()`，不如调用 `kobject_register()`：

```c
int kobject_register(struct kobject *kobj);
```

此函数同时初始化给定的 kobject 并将其添加到对象层次结构。移除 kobject 的表示通过 `kobject_del()` 实现：

```c
void kobject_del(struct kobject *kobj);
```

`kobject_unregister()` 函数结合了 `kobject_del()` 和 `kobject_put()`：

```c
void kobject_unregister(struct kobject *kobj);
```

所有四个函数都定义在 `lib/kernel.c` 中，并在 `<linux/kobject.h>` 中声明。

## 向 sysfs 添加文件

kobjects 映射到目录，完整的对象层次结构映射到完整的 sysfs 目录结构，但文件呢？如果没有提供实际数据，sysfs 并不是一个漂亮的树。

## 默认属性

一组默认文件通过 kobjects 和 ksets 中的 `ktype` 字段提供。因此，相同类型的 kobject 都有相同的默认文件填充其 sysfs 目录。`kobj_type` 结构包含一个成员 `default_attrs`，它是一个属性结构数组。属性将内核数据映射到文件中。

属性结构定义在 `<linux/sysfs.h>` 中：

```c
/* attribute 结构 - 属性将内核数据映射到 sysfs 文件 */

struct attribute {
    char *name;      /* 属性名称 */
    struct module *owner; /* owning module, if any */
    mode_t mode; /* permissions */
};
```

`name` 成员提供此属性的名称。这将是 sysfs 中生成的文件名。`owner` 成员指向一个代表所有者模块的结构体指针（如果有的话）。如果某个模块不拥有此属性，则该字段为 `NULL`。该成员是 `mode_t` 类型，用于指定 sysfs 中文件的权限。只读属性如果只是可读的，通常希望将其设置为 `S_IRUGO`。可写属性如果只是可写的，则希望将 `mode` 设置为 `S_IWUSR`。（`S_IRUGO | S_IWUSR`）。所有文件和目录都归用户 0 和组 0 所有。

尽管 `default_attrs` 列出了属性，但 `sysfs_ops` 描述了如何使用它们。定义在 `<linux/sysfs.h>` 中：

```c
struct sysfs_ops {
    /* 在读取 sysfs 文件时调用的方法 */
    ssize_t (*show) (struct kobject *obj,
                   struct attribute *attr,
                   char *buffer);
    /* 在写入 sysfs 文件时调用的方法 */
    ssize_t (*store) (struct kobject *obj,
                     struct attribute *attr,
                     char *buffer,
                     size_t count);
};
```
