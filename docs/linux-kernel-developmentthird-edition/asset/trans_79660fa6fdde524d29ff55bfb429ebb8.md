

## `sysfs_ops` 变量

`sysfs_ops` 变量指向一个 `sysfs_ops` 结构体。该结构体描述了 `sysfs` 文件在读取和写入时的行为。关于此变量的详细信息将在“向 `sysfs` 添加文件”一节中进一步阐述。

最后，`default_attrs` 指向一个 `attribute` 结构体数组。这些结构体定义了与该 kobject 关联的默认 `attributes`（属性）。属性代表与给定对象相关的特性。如果该 kobject 被导出到 `sysfs`，这些属性将作为文件导出。数组中的最后一个条目必须是 `NULL`。

## Ksets

Ksets（kset 的复数形式）是内核对象集合（kernel object sets）的缩写，是 kobjects 的聚合集合。Ksets 作为一组内核对象的基础容器类工作，将相关的 kobjects（例如“所有块设备”）汇集在一起。Ksets 听起来可能与 ktypes 相似，从而引发“为什么要同时拥有两者？”的问题。Ksets 将相关的内核对象分组在一起，而 ktypes 则使内核对象（无论功能上是否相关）能够共享通用的操作。保留这种区分是为了允许具有相同 ktype 的 kobjects 被分组到不同的 ksets 中。也就是说，Linux 内核中只有少数几个 ktypes，但有许多 ksets。

`kset` 指针指向 kobject 关联的 kset。Ksets 由 `kset` 结构体表示，该结构体在 `<linux/kobject.h>` 中声明：

```c
struct kset {
    struct list_head    list;
    spinlock_t          list_lock;
    struct kobject      kobj;
    struct kset_uevent_ops    *uevent_ops;
};
```

在该结构体中，`list` 是此 kset 中所有 kobjects 的链表，`list_lock` 是保护此链表项的自旋锁（关于自旋锁的讨论，请参阅第 10 章“内核同步方法”），`kobj` 是代表此集合基础类的 kobject，`uevent_ops` 指向一个描述此 kset 中 kobjects 热插拔行为的结构体。Uevent 是用户事件（user events）的缩写，是一种与用户空间通信的机制，用于传递系统中设备热插拔和热移除的信息。

## Kobjects、Ktypes 和 Ksets 的相互关系

迄今为止讨论的少数几个结构体之所以令人困惑，并非因为它们的数量（只有三个）或复杂性（它们都相当简单），而是因为它们彼此相互关联。在 kobjects 的世界里，很难在讨论其中一个结构体时不提及其他的。然而，在涵盖了每个结构体的基础知识后，您可以对它们的关系建立牢固的理解。

重要的核心对象是 kobject，由 `struct kobject` 表示。Kobject 为内核数据结构引入了基本对象特性——如引用计数、父子关系和命名。`kobject` 结构体以标准统一的方式提供这些特性。Kobjects 本身并不特别有用。相反，对象通常嵌入在其他数据结构中，使那些包含它们的结构体具备 kobject 的特性。

对象与特定的 ktype 相关联，ktype 由 `struct kobj_type` 表示，并由 kobject 内部的 `ktype` 变量指向。Ktypes 定义相关 kobjects 的一些默认特性：销毁行为、`sysfs` 行为和默认属性。ktype 结构的命名并不太贴切；思考 ktypes 时，不要将其视为分组，而应视为一组共享的操作。

Kobjects 随后被分组到称为 ksets 的集合中，ksets 由 `struct kset` 表示。Ksets 提供两个功能。首先，其嵌入的 kobject 作为一组 kobjects 的基础类。其次，ksets 聚合相关的 kobjects。在 `sysfs` 中，kobjects 是文件系统中的独立目录。相关目录——例如，给定目录的所有子目录——可能位于同一个 kset 中。

图 17.1 描绘了这些数据结构之间的关系。

![](img/48bc90306f7476ca73ca7a99267ff690_378_0.png)

## 管理和操作 Kobjects

在掌握了 kobjects 及其相关对象的基本内部机制后，是时候查看用于管理和操作 kobjects 的导出接口了。大多数时候，驱动程序编写者无需直接处理 kobjects。相反，kobjects 嵌入在特定的类结构中（如您所见，字符设备结构即是如此），并由相关的驱动子系统在“幕后”进行管理。尽管如此，kobjects 并非旨在保持隐藏，它们可能会渗透到驱动程序代码中，或者您可能正在直接修改驱动子系统本身。

使用 kobject 的第一步是声明和初始化它。Kobjects 通过函数 `kobject_init()` 进行初始化，该函数在 `<linux/kobject.h>` 中声明：

```c
void kobject_init(struct kobject *kobj, struct kobj_type *ktype);
```

该函数的第一个参数是要初始化的 kobject。在调用此函数之前，kobject 必须被清零。这通常在 kobject 嵌入的较大函数的初始化过程中完成。如果不是，调用一次简单的 `memset()` 即可实现：

```c
memset(kobj, 0, sizeof (*kobj));
```

在清零之后初始化父对象和 kset 是安全的。例如：

```c
struct kobject *kobj;

kobj = kmalloc(sizeof (*kobj), GFP_KERNEL);
if (!kobj)
    return -ENOMEM;
memset(kobj, 0, sizeof (*kobj));
kobj->kset = my_kset;
kobject_init(kobj, my_ktype);
```

这种多步操作由 `kobject_create()` 自动处理，该函数返回一个新分配的 kobject：

```c
struct kobject * kobject_create(void);
```

使用很简单：

```c
struct kobject *kobj;

kobj = kobject_create();
if (!kobj)
    return -ENOMEM;
```

大多数 kobjects 的使用应优先采用 `kobject_create()` 或相关的辅助函数，而不是直接操作结构体。

## 引用计数

Kobjects 提供的主要特性之一是统一的引用计数系统。初始化后，kobject 的引用计数被设置为 1。只要引用计数不为零，对象就继续在内存中存在，并被称为已固定（pinned）。持有对象引用的代码首先会提升引用计数。当代码处理完对象后，引用计数会递减。提升引用计数被称为获取（get）对象的引用，递减引用计数被称为释放（put）对象的引用。当引用计数达到零时，对象可以被销毁，并释放任何关联的内存。

### 增加和减少引用计数

增加引用计数是通过 `kobject_get()` 完成的，该函数在 `<linux/kobject.h>` 中声明：

```c
struct kobject * kobject_get(struct kobject *kobj);
```

此函数返回指向 kobject 的指针，或在失败时返回 `NULL`。

减少引用计数是通过 `kobject_put()` 完成的，该函数同样在 `<linux/kobject.h>` 中声明：

```c
void kobject_put(struct kobject *kobj);
```

如果提供的 kobject 的引用计数达到零，将与 kobject 关联的 ktype 所指向的释放函数会被调用，任何关联的内存将被释放，并且对象不再有效。

### Krefs

内部而言，kobject 的引用计数由 `kref` 结构体提供，该结构体在 `<linux/kref.h>` 中定义：

```c
struct kref {
    atomic_t refcount;
};
```

唯一的成员是一个原子变量，用于保存引用计数。使用结构体仅仅是为了提供类型检查。在使用 `kref` 之前，必须通过 `kref_init()` 对其进行初始化：

```c
void kref_init(struct kref *kref)
{
    atomic_set(&kref->refcount, 1);
}
```

如您所见，此函数仅将内部的 `atomic_t` 初始化为 1。因此，`krefs` 在初始化时即被固定，引用计数为 1；这与 kobjects 的行为相同。

要获取 `kref` 的引用，请使用 `kref_get()`，该函数在 `<linux/kref.h>` 中声明：

```c
void kref_get(struct kref *kref)
{
    WARN_ON(!atomic_read(&kref->refcount));
    atomic_inc(&kref->refcount);
}
```

此函数会增加引用计数。它没有返回值。要丢弃对 `kref` 的引用，请使用 `kref_put()`，该函数在 `<linux/kref.h>` 中声明：

```c
int kref_put(struct kref *kref, void (*release)(struct kref *kref))
{
    WARN_ON(release == NULL);
    if (atomic_dec_and_test(&kref->refcount))
        release(kref);
    return atomic_read(&kref->refcount);
}

