
# 1. kset 结构说明

在这个列表中，一个 `kset` 是该 `kset` 中所有对象的链表，`list_lock` 是保护该列表中该条目的自旋锁（关于自旋锁的讨论，请参见第 10 章“内核同步方法”），`kobj` 是表示该集合基类的的 `kobject`，而 `uevent_points` 指向一个描述该 `kset` 中 `kobject` 热插拔行为的结构体。用户事件（User events）是一种用于与用户空间通信关于设备从系统中热插拔和热移除信息的机制。

# Kobjects, Ksets 和 Ktypes 之间的相互关系

目前为止讨论的这几个结构之所以令人困惑，并不是因为它们的数量（只有三个）或复杂性（它们都相当简单），而是因为它们都是相互关联的。在 `kobject` 的世界里，很难在不讨论其他的情况下讨论其中一个。然而，在掌握每个结构的基础上，你可以对它们之间的关系建立稳固的理解。

核心对象是 `kobject`，由 `struct kobject` 表示。`kobject` 为内核数据结构引入了基本的对象属性——例如引用计数、父子关系和命名。`kobject` 结构以一种标准统一的方式提供了这些功能。`kobjects` 本身并不特别有用。相反，

# 第 17 章 设备与模块

`kobjects` 通常嵌入在其他数据结构中，使得包含这些结构的结构拥有了 `kobject` 的特性。

`Kobjects` 与特定的 `ktype` 关联，该 `ktype` 由 `struct kobj_type` 表示，并由 `kobject` 内部的 `ktype` 变量指向。`ktypes` 定义了相关 `kobjects` 的某些默认属性：销毁行为、sysfs 行为和默认属性。`ktype` 结构并不广为人知；请不要将 `ktypes` 看作一种分组，而将其看作一组共享的操作。

然后 `kobjects` 被分组为集合，称为 `ksets`，由 `struct kset` 表示。`Ksets` 提供两个功能：首先，它们嵌入的 `kobject` 当一组 `kobjects` 的基类；其次，`ksets` 聚合了相关的 `kobjects`。在 sysfs 中，对象是文件系统中的目录。相关的目录——例如某个给定目录的所有子目录——可能位于同一个 `kset` 中。

![](img/d256a511e487ca9115a860fa084e781d_378_0.png)

# 管理与操作 Kobjects

掌握 `kobjects` 及其伙伴的基本原理后，是时候查看用于管理和操作 `kobjects` 的导出接口了。大多数时候，驱动程序编写者不需要直接处理 `kobjects`。相反，`kobjects` 被嵌入在某些类特定的结构中（正如你在字符设备结构中看到的那样），由相关的驱动子系统在“幕后”管理。尽管如此，`kobjects` 并不打算隐藏，你可以通过驱动代码或驱动子系统本身发生的情况看到它们。

使用 `kobject` 的第一步是声明并初始化它。`kobjects` 通过函数 `kobject_init` 进行初始化，该函数在 `<linux/kobject.h>` 中声明。

# 设备模型 353

```c
void kobject_init(struct kobject *kobj, struct ktype *ktype);
```

该函数的第一个参数是要待初始化的 `kobject`。在调用此函数之前，`kobject` 必须被清零。这通常发生在嵌入 `kobject` 的较大函数的初始化期间。如果没有，简单地调用 `memset()` 即可解决：

```c
memset(kobj, 0, sizeof(*kobj));
```

在清零后初始化父对象和 `kset` 是安全的。例如

```c
kobj = kmalloc(sizeof(*kobj), GFP_KERNEL);

if (!kobj)
    return -ENOMEM;

memset(kobj, 0, sizeof(*kobj));

kobj->kset = my_kset;

kobject_init(kobj, my_ktype);
```

这种多步操作由 `kobject_create()` 自动处理，它返回一个新分配的 `kobject`：

```c
struct kobject *kobject_create(void);
```

用法非常简单：

```c
struct kobject *kobj;

kobj = kobject_create();

if (!kobj)
    return -ENOMEM;
```

大多数 `kobjects` 用户应该倾向于使用 `kobject_create()` 或相关的辅助函数，而不是直接操作结构。

# 引用计数

`kobjects` 提供的主要功能之一是统一引用计数系统。初始化后，`kobject` 引用被设置为 1。只要引用计数不为零，对象就会继续存在于内存中并可能被固定。任何持有对象引用的代码都会引用计数。当代码完成对对象的操作时，引用计数递减。增加引用计数是通过获取对象的引用来实现的，当引用达到零时，对象可以销毁并释放任何关联内存。

# 增加和递减引用计数

增加引用计数通过 `kobject_get()` 完成，该函数在 `<linux/kobject.h>` 中声明：

```c
struct kobject *kobject_get(struct kobject *kobj);
```

该函数返回指向 `kobject` 的指针，失败时返回 `NULL`。递减引用计数通过 `kobject_put()` 完成，该函数同样在 `<linux/kobject.h>` 中声明：

```c
void kobject_put(struct kobject *kobj);
```

如果提供的 `kobject` 的引用计数达到零，将调用 `kobject` 指向的释放函数，释放任何关联内存，且该对象不再有效。

# Krefs

在内部，`kobject` 引用计数由 `kref` 结构提供，该结构定义在 `<linux/kref.h>` 中：

```c
struct kref {
    atomic_t refcount;
}
```

该成员是一个用于持有引用计数的原子变量。使用结构体仅是为了提供类型检查。在使用 `kref` 之前，你必须通过 `kref_init()` 对进行初始化：

```c
void kref_init(struct kref *kref)
{
    atomic_set(&kref->refcount, 1);
}
```

如你所示，此函数将内部的 `atomic_t` 初始化为 1。通常，`krefs` 在初始化后立即以 1 的引用计数被固定；这是跨 `kobjects` 的通用行为。要获取 `kref` 的引用，使用在 `<linux/kref.h>` 中声明的 `kref_get`：

```c
void kref_get(struct kref *kref)
{
    atomic_inc(&kref->refcount);
}
```

此函数增加引用计数。它没有返回值。要释放 `kref` 的引用，使用在 `<linux/kref.h>` 中声明的 `kref_put`：

```c
int kref_put(struct kref *kref, void (*release)(struct kref *))
{
    if (atomic_dec_and_test(&kref->refcount)) {
        release(kref);
        return 1;
    }

    return 0;
}
```

此函数将引用计数减一，如果计数为零则调用提供的释放函数。正如著名的 `WARN_ON()` 语句所示，`kref_put` 关心的是返回值，除非该释放是最后的引用，否则返回 0。

# sysfs

sysfs 文件系统是一种内存虚拟文件系统，提供了 `kobject` 层次结构的视图。它允许用户以简单的文件系统形式查看系统的设备拓扑。通过属性，对象可以导出文件，以便读取和可选写入内核变量。

尽管设备模型最初的意图是为了电源管理原因，但 sysfs 出现了。为了方便调试，设备模型的开发者决定将树形结构导出为文件系统。事实证明这是非常有用的，起初替代了以前出现在 `/proc` 中的设备相关文件，并作为对系统层次结构的强大视图。事实上，最初名为 `drivers` 的 sysfs 预言了新的设备模型是有益的，而 `object` 也随之诞生。每天，带有 2.6 内核的系统都在 `/sys` 挂载了许多系统。

图 17.2 是挂载在 `/sys` 的 sysfs 文件系统的部分视图。

## 第 17 章 设备与模块

```text
block
  loop0 -> ../devices/virtual/block/loop0
  md0 -> ../devices/virtual/block/md0
  nbd0 -> ../devices/virtual/block/nbd0
  ram0 -> ../devices/virtual/block/ram0
  xvda -> ../devices/vbd-51712/block/xvda

bus
  platform
  serio

class
  bdi
  block
```
