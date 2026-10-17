
这段代码看起来与普通文件系统无异，但`libfs` `get_sb_pseudo`方法确保了文件系统无法从用户空间挂载。这很简单：它需要设置在第 8 章中讨论过的`MS_NOUSER`标志。此外，会填充一个`super_block`实例，并为伪文件系统分配根 inode。

要使用伪文件系统，内核需要使用`kern_mount`或`kern_mount_data`挂载它。它可以用于收集 inode，而无需编写专门的数据结构来完成。例如，所有代表块设备的 inode 都被分组在一起。然而，该集合仅对内核可见，对用户空间不可见。

## 10.3 Sysfs

Sysfs 用于将内核对象导出到用户空间，不仅提供了不观测内核内部数据结构属性的能力，还提供了修改它们的能力。特别重要的是文件系统布局的高度层次化组织。sysfs 条目源于第 1 节引入的内核对象（objects），它们的层级顺序直接反映在 sysfs 目录中。由于系统的所有设备和总线都是通过对象组织的，sysfs 提供了系统硬件拓扑的表示。

在许多情况下，使用人类可读的字符串来导出对象，但经常通过 IOCTL 命令在内核与内核之间传递二进制数据。与其向内核发送晦涩的 ioctls（这需要一个 C 程序），不如从 sysfs 文件读取或向其写入值要简单得多。一个简单的命令就足够了。另一个优势是，简单的目录列表可以快速概述可以设置哪些选项。

与许多虚拟文件系统一样，sysfs 最初是基于 ramfs 的；其实现使用了内核其他地方的许多技术。请注意，sysfs 总是编译到内核中的。

> ⁵因此，从对象机制已知的大量连接的数据结构被直接传输到 sysfs，至少当对象导出到文件系统时是。

如果它被配置为活动；无法将其生成为模块。sysfs 路径为`/sys`。

内核提供了一些关于 sysfs 的文档，涉及相对于 kobject 框架的驱动模型等。可以在`Documentation/filesystems/sysfs.txt`和`Documentation/filesystems/sysfs-pci.txt`中找到。sysfs 作者的一篇概述文章可以在 2005 年渥太华 Linux 议会集中找到，地址为 [www.linuxysymposium.org/2005/linuxysymposium.procl.pdf](https://www.linuxysymposium.org/2005/linuxysymposium.procl.pdf)。

最后，请注意 kobjects 和 sysfs 之间的连接不会自动更新。独立的 kobject 实例默认不会集成到 sysfs 中。你需要调用`kobject_add`来让对象在文件系统中变为可见。如果 kobject 是内核子系统的成员，则注册是自主完成的。

### 10.3.1 概述

`struct kobject`、相关数据结构及其用法在第 1 节中已有描述；因此，这里的讨论仅限于对要点的回顾。特别地，重要的是记住：

- kobjects 被包含在层次化组织中；最重要的是，它们有一个父节点并包含在`kset`中。这决定了 kobject 在 sysfs 中的位置。如果存在父节点，会在父目录中创建一个新条目；否则，它被放置在所属 kset 的目录中（如果两种情况都失败，kobject 的条目直接位于顶层，但这是一个罕见情况）。
- 每个 kobject 都表示为 sysfs 中的一个目录。出现在此目录中的文件是对象的属性。用于导出和设置属性值是由所属子系统（class、driver 等）提供的。
- 总线、设备和类是使用 kobject 机制的主要内核对象；它们构成了 sysfs 的几乎所有条目。

### 10.3.2 数据结构

通常，我们首先描述 sysfs 使用的数据结构。

#### 目录条目

目录条目由`<sysfs.h>`中的`struct sysfs_dirnt`表示。它是 sysfs 的主数据结构；实现围绕它展开。每个 sysfs 节点由单个`sysfs_dirnt`实例表示。其定义如下：

```c
struct sysfs_dirnt {
    atomic_t s_count;
    atomic_t s_active;
    struct sysfs_dirnt *parent;
    struct sysfs_dirnt *sibling;
    const char *name;
    union {
        struct sysfs_dirnt *dir;
        struct sysfs_dirnt *link;
        struct sysfs_dirnt *attr;
        struct sysfs_dirnt *bin;
    } data;
    unsigned int flags;
    ino_t ino;
    umode_t mode;
    struct kobject *obj;
};
```
（注：OCR 中的结构定义跨越了页面；我根据标准内核头文件和提供的片段重构了该结构。）

# 第 10 章：没有持久化存储的文件系统

一旦与关联内部数据的操作完成，就会调用`sysfs_put_active`（相应的为`sysfs_put_active_two`）。

#### 属性

让我们关注表示属性的数据结构以及用于声明新属性的机制：

##### 数据结构

属性由以下数据结构定义：

```c
include/linux/<sysfs.h>
struct attribute {
    const char *name;
    struct module *owner;
    mode_t mode;
};
```

`name`为属性提供在 sysfs 中使用的名称（因此，属于对象的属性没有唯一的名称），而`mode`指定访问模式。`owner`指向属性所有者所属的模块实例。

也可以借助以下数据结构定义一组属性：

```c
<sysfs.h>
struct attribute_group {
    const char *name;
    struct attribute **attrs;
};
```

`name`是属性的名称，`attrs`指向由 NULL 条目结尾的属性实例数组。

请注意，这些数据结构提供了表示属性的方法，但没有指定如何读取或修改它们。这在第 10.3.4 节中介绍。选择表示与访问方法的分离是因为属于特定实体（例如驱动程序、设备类等）的属性是以类似的方式修改的，因此迁移这种属性是有意义的；子系统的显示和存储方法在内部与属性连接，但根据每个属性的不同而不同。实现细节留给各个子系统；sysfs 并不关心这些。

对于读写属性，需要两个标记为`show`和`store`的方法来允许；内核提供了以下数据结构将它们整合在一起：

```c
<sysfs.h>
struct sysfs_ops {
    ssize_t (*show)(struct kobject *, struct attribute *, char *page);
    ssize_t (*store)(struct kobject *, struct attribute *, const char *buf, size_t count);
};
```

声明新属性的代码负责提供一组合适的 show 和 store 操作。

二进制属性的情况有所不同：在这里，读取和修改数据的方法通常对于每个属性都是不同的。这反映在数据结构中，其中显式指定了读取、写入和内存映射的方法：

```c
<sysfs.h>
struct bin_attribute {
    struct attribute attr;
    size_t size;
    void *private;
    ssize_t (*read)(struct object *, struct bin_attribute *, char *buf, loff_t count);
    ssize_t (*write)(struct object *, struct bin_attribute *, const char *buf, loff_t count);
    int (*mmap)(struct object *, struct bin_attribute *attr, struct vm_area_struct *vma);
};
```

`size`表示与属性关联的二进制数据的大小，`private`（通常）用于指向实际存储数据的地方。

##### 声明新属性

声明子系统特定属性的可能分布在内核各处，但由于它们在实现方面共享基本结构，因此只需考虑一种实现即可作为底层机制的。例如，考虑通用磁盘代码如何定义一个统一属性以及读取和修改该属性关联方法的结构：

```c
<genhd.h>
struct disk_attribute {
    struct attribute attr;
    ssize_t (*show)(struct gendisk *, char *page);
```
