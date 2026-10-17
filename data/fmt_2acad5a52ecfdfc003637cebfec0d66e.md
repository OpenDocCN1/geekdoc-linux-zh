
VFS 对底层实现的每次请求都会导致创建一个新的 dentry 对象来持有该请求。这些对象存储在缓存中，以便在下次需要时可以更快地访问，并更快速地执行操作。缓存是如何组织的？它包含以下组件用于在内存中组织 dentry 对象：

- 1. 一个包含所有 dentry 对象的哈希表 (`dentry_hashtable`)。
- 2. 一个 LRU（最近未使用使用）列表，其中不再被使用的 dentry 在从内存中移除之前会获得一段宽限期。

回想，哈希表是按照经典模式实现的。`fs/dcache.c` 中的函数 `d_hash` 用于确定 dentry 的哈希位置。

处理 LRU 列表稍微复杂一些。该列表由全局变量 `dentry_used` 管理，对象通过 `struct dentry` 中的 `d_lru` 元素链接。

当 dentry 对象的使用计数器（`d_count`）达到 0 时，它们会被放置在 LRU 列表中——这表示没有分配正在活动使用该 dentry。新条目始终放置在列表开头。换句话说，条目在列表中位置越靠后，停留的时间越长——这就是经典的修剪机制。`prune_dcache` 函数不时调用，例如当文件系统被卸载或内核需要更多内存时。旧对象会被移除并释放。注意，它可以临时在未使用的列表中留存 dentry 对象，尽管它们正在被使用且使用计数器大于 0。这是因为内核进行了一些优化：当一个在未使用列表中的 dentry 重新被使用时，它不会被立即从未使用列表中移除，因为这涉及到锁操作且为了提高性能。像 `prune_dcache` 这样本就昂贵的操作弥补了这一点：当它们遇到使用计数为正数的对象时，它们将其从列表中移除，但不会释放它。

由于 LRU 列表同时存在于哈希表中，因此可以通过搜索条目的查找操作找到它们。一旦找到条目，它就会从 LRU 列表中移除，因为现在现在处于活动状态。使用计数器会加增。

# Dentry 操作

`dentry_operations` 结构持有指向各种特定文件系统操作的函数指针，这些操作可以在 dentry 对象上执行。结构定义如下：

```
<dcache.h>
struct dentry_operations {
    int (*revalidate)(struct dentry *, struct nameidata*);
    int (*d_hash)(struct dentry *, struct qsort*);
    int (*compare)(struct dentry *, struct qsort *, struct qsort*);
    int (*delete)(struct dentry*);
    void (*release)(struct dentry*);
    void (*input)(struct dentry *, struct inode*);
    char (*d_name)(struct dentry *, char *, int);
};
```

- `d_input` 从不再使用的 dentry 对象中移除 inode（在默认实现中，使用计数器递减，条目从各种列表中移除，直到计数器达到 0）。
- `d_delete` 在最后一个引用被移除后调用。
- `release` 在 dentry 对象最终被删除之前调用。
- `d_hash` 计算用于将对象放入哈希表的哈希值。
- `compare` 比较两个 dentry 的文件名。
- `revalidate` 对于网络文件系统特别相关。它检查内存中由单个 dentry 对象设置的结构是否仍然反映当前状况。

# 标准函数

内核提供了几个简化 dentry 对象处理的函数。它们的实现大部分列表管理和数据结构处理的练习，所以我不会花精力讨论它们的代码。然而，显示它们的原型并描述其作用是很重要的，因为我们在讨论 VFS 时会经常遇到它们。以下函数需要一个 `struct dentry` 指针作为参数。每个函数执行一个操作。

- 当内核的部分使用 dentry 实例时，需要调用 `dget`。调用 `dget` 会增加对象的引用计数；这相当于获取了对它的引用。
- `dput` 是 `dget` 的对应项：当内核中的用户不再需要 dentry 实例时，必须调用它。

该函数减少 dentry 对象的计数计数。如果计数降到零，如果可用，将调用 `dentry_operations->d_delete` 方法。此外，该实例将通过 `d_drop` 从全局 dentry 哈希表中取消哈希，并从 LRU 列表中移除并置于未使用的列表中。

如果在调用 `dput` 时对象包含在哈希表中，则将通过 `kfree` 从内存中删除。

- `d_drop` 从全局 dentry 哈希表中取消 dentry 实例的哈希。如果使用计数降到零，它会自动从 `dput` 调用，但如果缓存对象需要失效，也可以手动调用。`__d_drop` 是 `d_drop` 的变体，不处理锁。
- `d_delete` 取消 dentry 对象的哈希。如果对象仅剩一个用户，还会调用 `dentry_iput` 以减少与 dentry 关联的 inode 的使用计数。

# 第8章：虚拟文件系统

某些辅助函数更为复杂，因此最好检查它们的原型¹¹²

```c
cdcache.h
extern void d_instantiate(struct dentry *, struct inode *);
struct dentry * d_alloc(struct dentry *, const struct qstr *);
struct dentry * d_alloc_anon(struct inode *);
struct dentry * d_splice_alias(struct inode *, struct dentry *);
static inline void d_add(struct dentry *entry, struct inode *inode);
struct dentry * d_lookup(struct dentry *, struct qstr);
```

- `d_instantiate` 将一个 dentry 实例与一个 inode 关联。这意味着设置 `d_inode` 字段并将 dentry 添加到由 `inode->i_dentry` 链头的列表中。
- `d_add` 使用 `d_instantiate` 初始化 dentry 对象。此外，该对象会被添加到全局 inode 哈希表 `dentry_hashtable` 中。
- `d_alloc` 为 `struct dentry` 的新实例分配内存，正如其名称所示。各个字段会被初始化，如果存在父节点，则从父节点获取新的超级块（superblock）。此外，新的 dentry 会被添加到由 `parent->dsub` 链头的父目录列表中。
- `d_alloc_anon` 为 `struct dentry` 实例分配内存，但不会与父节点建立任何连接——这就是为什么与 `d_alloc` 不同，它不需要此类参数。新的 dentry 会被添加到两个列表中：由 `super->s_anon` 链头的匿名 dentry 超块特定列表，以及与 inode 关联的所有 dentry 列表（由 `inode->i_dentry` 链头）。
- 如果 inode 已经包含了由之前的 `d_alloc_anon` 调用部分配的断开连接的 dentry，则将使用该拷贝而不是创建新实例。
- `d_splice_alias` 将断开连接的 dentry 接到 dentry 树中。该函数所需的 `inode` 参数用于连接该 inode。对于代表目录之外任何文件系统对象的 inode，只需调用 `d_add` 即可。对于目录，该函数会确保只存在一个 dentry，这需要更多的管理工作，我不打算在此详细讨论了。
- `d_lookup` 获取目录的 dentry 实例，并搜索一个表示特定名称文件的 dentry 对象。

## 8.4 与 VFS 对象的操作

上述描述的数据结构是操作 VFS 层的基础。我们将在接下来的节中对其进行检查。让我们首先关注文件系统的挂载和卸载（以及文件系统注册，这是这些操作的前提）。我将介绍涉及文件以及所有通过相同接口表示的其他对象的最重要且最有趣的函数。

我们从标准库用于与内核通信的系统调用开始介绍。

### 8.4.1 文件系统操作

¹²更多辅助函数定义在 `<dentry.h>` 中，并在 `fs/dcache.c` 中实现。由于它们不被频繁使用，我在这里不再讨论它们，但请参考与其相关的文档以获取更多信息。

虽然文件操作是所有应用程序的标准功能set的一部分，但对文件系统的操作仅限于少数系统程序，即 `mount`（挂载）和 `umount`（卸载）操作³用于挂载和卸载文件系统。

另一个重要方面也被考虑在内。文件系统在内核中是以模块化形式实现的；这意味着它们可以作为模块编译进内核（第7章），或者通过在编译内核时不支持某个特定的文件系统版本来完全忽略它们——考虑到大约有50个文件系统，在内核中保留所有文件系统的代码是没有意义的。

因此，每个文件系统在使用之前都必须向内核注册，以便 Linux 拥有可用文件系统的概览并能够调用所需的模块。

## 注册文件系统
