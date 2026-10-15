
# Linux 内核中的数据结构

Linux 内核对很多数据结构提供不同的实现方法，比如，双向链表，B+树，具有优先级的堆等等。

这部分考虑这些数据结构和算法。

* [双向链表](https://github.com/MintCN/linux-insides/blob/master/DataStructures/dlist.md)
* [基数树](https://github.com/MintCN/linux-insides/blob/master/DataStructures/radix-tree.md)

## 双向链表

Linux 内核提供了自己的双向链表实现，你可以在`include/linux/list.h`中找到它。我们将从双向链表数据结构开始讨论“Linux 内核中的数据结构”。为什么？因为它在内核中非常流行，只需尝试[搜索](http://lxr.free-electrons.com/ident?i=list_head)一下即可。

首先，让我们看一下主要结构：

```
struct list_head {
    struct list_head *next, *prev;
};
```

你可以注意到，它与许多你见过的链表实现不同。例如，来自[glib](http://www.gnu.org/software/libc/)的这个双向链表结构：

```
struct GList {
  gpointer data;
  GList *next;
  GList *prev;
};
```

通常，链表结构包含一个指向数据项的指针。而 Linux 内核的链表实现并不包含。所以主要问题是——`链表在哪里存储数据？`内核中链表的实际实现是——`侵入式链表`。侵入式链表不将数据包含在节点中——节点只包含指向前一个和后一个节点的指针，并且链表节点是添加到链表中的数据的一部分。这使得数据结构具有通用性，因此它不再关心条目数据类型。

例如：

```
struct nmi_desc {
    spinlock_t lock;
    struct list_head head;
};
```

让我们看一些示例来理解`list_head`在内核中是如何使用的。正如我已经写过的，链表在内核中有很多，真的很多不同的地方被使用。让我们看看例如杂项字符驱动程序。来自`drivers/char/misc.c`的杂项字符驱动程序 API 用于编写处理简单硬件或虚拟设备的小型驱动程序。这些驱动程序共享主设备号：

```
#define MISC_MAJOR              10
```

但拥有自己的次设备号。例如，你可以通过以下命令查看：

```
ls -l /dev |  grep 10
crw-------   1 root root     10, 235 Mar 21 12:01 autofs
drwxr-xr-x  10 root root         200 Mar 21 12:01 cpu
crw-------   1 root root     10,  62 Mar 21 12:01 cpu_dma_latency
crw-------   1 root root     10, 203 Mar 21 12:01 cuse
drwxr-xr-x   2 root root         100 Mar 21 12:01 dri
crw-rw-rw-   1 root root     10, 229 Mar 21 12:01 fuse
crw-------   1 root root     10, 228 Mar 21 12:01 hpet
crw-------   1 root root     10, 183 Mar 21 12:01 hwrng
crw-rw----+  1 root kvm      10, 232 Mar 21 12:01 kvm
crw-rw----   1 root disk     10, 237 Mar 21 12:01 loop-control
crw-------   1 root root     10, 227 Mar 21 12:01 mcelog
crw-------   1 root root     10,  59 Mar 21 12:01 memory_bandwidth
crw-------   1 root root     10,  61 Mar 21 12:01 network_latency
crw-------   1 root root     10,  60 Mar 21 12:01 network_throughput
crw-r-----   1 root kmem     10, 144 Mar 21 12:01 nvram
brw-rw----   1 root disk      1,  10 Mar 21 12:01 ram10
crw--w----   1 root tty       4,  10 Mar 21 12:01 tty10
crw-rw----   1 root dialout   4,  74 Mar 21 12:01 ttyS10
crw-------   1 root root     10,  63 Mar 21 12:01 vga_arbiter
crw-------   1 root root     10, 137 Mar 21 12:01 vhci
```

现在让我们仔细看看链表在杂项设备驱动程序中是如何使用的。首先，让我们看一下`miscdevice`结构：

```
struct miscdevice
{
      int minor;
      const char *name;
      const struct file_operations *fops;
      struct list_head list;
      struct device *parent;
      struct device *this_device;
      const char *nodename;
      mode_t mode;
};
```

我们可以在`miscdevice`结构中看到第四个字段——`list`，它是已注册设备的链表。在源代码文件的开头，我们可以看到`misc_list`的定义：

```
static LIST_HEAD(misc_list);
```

它展开为具有`list_head`类型的变量的定义：

```
#define LIST_HEAD(name) \
    struct list_head name = LIST_HEAD_INIT(name)
```

并使用`LIST_HEAD_INIT`宏初始化它，该宏设置前一个和后一个条目：

```
#define LIST_HEAD_INIT(name) { &(name), &(name) }
```

现在让我们看一下`misc_register`函数，它用于注册一个杂项设备。在开始时，它使用`INIT_LIST_HEAD`函数初始化`miscdevice->list`：

```
INIT_LIST_HEAD(&misc->list);
```

这与`LIST_HEAD_INIT`宏做相同的事情：

```
static inline void INIT_LIST_HEAD(struct list_head *list) {
    list->next = list;
    list->prev = list;
}
```

在下一步中，设备通过`device_create`函数创建后，我们将其添加到杂项设备链表中：

```
list_add(&misc->list, &misc_list);
```

内核的`list.h`提供了这个 API 用于向链表添加新条目。让我们看一下它的实现：

```
static inline void list_add(struct list_head *new, struct list_head *head) {
    __list_add(new, head, head->next);
}
```

它只是调用内部函数`__list_add`，并带有 3 个给定的参数：

* `new` - 新条目；
* `head` - 链表头，新条目将插入在其后；
* `head->next` - 链表头之后的下一个条目。

`__list_add`的实现非常简单：

```
static inline void __list_add(struct list_head *new,
                  struct list_head *prev,
                  struct list_head *next)
{
    next->prev = new;
    new->next = next;
    new->prev = prev;
    prev->next = new;
}
```

这里我们在`prev`和`next`之间设置新条目。因此，我们在开始时使用`LIST_HEAD_INIT`宏定义的`misc`链表将包含指向`miscdevice->list`的前一个和后一个指针。

还有一个问题：如何获取链表的条目。有一个特殊的宏：

```
#define list_entry(ptr, type, member) \
    container_of(ptr, type, member)
```

它接收三个参数：

* `ptr` - `list_head`结构指针；
* `type` - 结构类型；
* `member` - 结构中`list_head`的名称；

例如：

```
const struct miscdevice *p = list_entry(v, struct miscdevice, list)
```

之后，我们可以通过`p->minor`或`p->name`等访问任何`miscdevice`字段。让我们看一下`list_entry`的实现：

```
#define list_entry(ptr, type, member) \
    container_of(ptr, type, member)
```

正如我们所见，它只是用相同的参数调用`container_of`宏。乍一看，`container_of`看起来很奇怪：

```
#define container_of(ptr, type, member) ({                      \
    const typeof( ((type *)0)->member ) *__mptr = (ptr);    \
    (type *)( (char *)__mptr - offsetof(type,member) );})
```

首先，你可以注意到它由花括号中的两个表达式组成。编译器将评估整个花括号块，并使用最后一个表达式的值。

例如：

```
#include <stdio.h>

int main() {
    int i = 0;
    printf("i = %d\n", ({++i; ++i;}));
    return 0;
}
```

将打印`2`。

下一个点是`typeof`，它很简单。正如你从其名称中可以理解的，它只是返回给定变量的类型。当我第一次看到`container_of`宏的实现时，对我来说最奇怪的是`((type *)0)`表达式中的零。实际上，这个指针魔法计算给定字段相对于结构地址的偏移量，但因为我们这里有`0`，它将是零偏移加上字段宽度。让我们看一个简单的例子：

```
#include <stdio.h>

struct s {
        int field1;
        char field2;
        char field3;
};

int main() {
    printf("%p\n", &((struct s*)0)->field3);
    return 0;
}
```

将打印`0x5`。



The next `offsetof` macro calculates offset from the beginning of the structure to the given structure's field. Its implementation is very similar to the previous code:

```
#define offsetof(TYPE, MEMBER) ((size_t) &((TYPE *)0)->MEMBER) 
```

Let's summarize all about `container_of` macro. `container_of` macro returns address of the structure by the given address of the structure's field with `list_head` type, the name of the structure field with `list_head` type and type of the container structure. At the first line this macro declares the `__mptr` pointer which points to the field of the structure that `ptr` points to and assigns `ptr` to it. Now `ptr` and `__mptr` point to the same address. Technically we don't need this line but its useful for type checking. First line ensures that that given structure (`type` parameter) has a member called `member`. In the second line it calculates offset of the field from the structure with the `offsetof` macro and subtracts it from the structure address. That's all.

Of course `list_add` and `list_entry` is not the only functions which `<linux/list.h>` provides. Implementation of the doubly linked list provides the following API:

* `list_add`
* `list_add_tail`
* `list_del`
* `list_replace`
* `list_move`
* `list_is_last`
* `list_empty`
* `list_cut_position`
* `list_splice`

and many more.

# Radix tree

# Linux 内核中的数据结构

## 基数树

正如你所知道的 Linux 内核通过许多不同库以及函数提供各种数据结构以及算法实现。这个部分我们将介绍其中一个数据结构 [Radix tree](http://en.wikipedia.org/wiki/Radix_tree)。Linux 内核中有两个文件与 `radix tree` 的实现和 API 相关：

* [include/linux/radix-tree.h](https://github.com/torvalds/linux/blob/master/include/linux/radix-tree.h)
* [lib/radix-tree.c](https://github.com/torvalds/linux/blob/master/lib/radix-tree.c)

首先说明一下什么是 `radix tree`。Radix tree 是一种 `压缩 trie`，其中 [trie](http://en.wikipedia.org/wiki/Trie) 是一种通过保存关联数组（associative array）来提供 `关键字-值（key-value）` 存储与查找的数据结构。通常关键字是字符串，不过也可以是其他数据类型。

trie 结构的节点与 `n-tree` 不同，其节点中并不存储关键字，取而代之的是存储单个字符标签。关键字查找时，通过从树的根开始遍历关键字相关的所有字符标签节点，直至到达最终的叶子节点。下面是个例子：

```
+-----------+
               |           |
               |    " "    |
               |           |
        +------+-----------+------+
        |                         |
        |                         |
   +----v------+            +-----v-----+
   |           |            |           |
   |    g      |            |     c     |
   |           |            |           |
   +-----------+            +-----------+
        |                         |
        |                         |
   +----v------+            +-----v-----+
   |           |            |           |
   |    o      |            |     a     |
   |           |            |           |
   +-----------+            +-----------+
                                  |
                                  |
                            +-----v-----+
                            |           |
                            |     t     |
                            |           |
                            +-----------+ 
```

这个例子中，我们可以看到 `trie` 所存储的关键字信息 `go` 与 `cat`，压缩 trie 或 `radix tree` 与 `trie` 所不同的是，所有只存在单个孩子的中间节点将被压缩。

Linux 内核中的 Radix 树将值映射为整型关键字，Radix 的数据结构定义在 [include/linux/radix-tree.h](https://github.com/torvalds/linux/blob/master/include/linux/radix-tree.h) 文件中：

```
struct radix_tree_root {
         unsigned int            height;
         gfp_t                   gfp_mask;
         struct radix_tree_node  __rcu *rnode;
}; 
```

上面这个是 radix 树的 root 节点的结构体，它包括三个成员：

* `height` - 从叶节点向上计算出的树高度。
* `gfp_mask` - 内存分配标识。
* `rnode` - 子节点指针。

这里我们先讨论的结构体成员是 `gfp_mask`：

Linux 底层的内存申请接口需要提供一类标识（flag）- `gfp_mask`，用于描述内存申请的行为。这个以 `GFP_` 前缀开头的内存申请控制标识主要包括，`GFP_NOIO` 禁止所有 IO 操作但允许睡眠等待内存，`__GFP_HIGHMEM` 允许申请内核的高端内存，`GFP_ATOMIC` 高优先级申请内存且操作不允许被睡眠。

接下来说的结构体成员是 `rnode`：

```
struct radix_tree_node {
        unsigned int    path;
        unsigned int    count;
        union {
                struct {
                        struct radix_tree_node *parent;
                        void *private_data;
                };
                struct rcu_head rcu_head;
        };
        /* For tree user */
        struct list_head private_list;
        void __rcu      *slots[RADIX_TREE_MAP_SIZE];
        unsigned long   tags[RADIX_TREE_MAX_TAGS][RADIX_TREE_TAG_LONGS];
}; 
```

这个结构体中包括这几个内容，节点与父节点的偏移以及到树底端的高度，子节点的个数，节点的存储数据域，具体描述如下：

* `path` - 从叶节点
* `count` - 子节点的个数。
* `parent` - 父节点的指针。
* `private_data` - 存储数据内容缓冲区。
* `rcu_head` - 用于节点释放的 RCU 链表。
* `private_list` - 存储数据。

结构体 `radix_tree_node` 的最后两个成员 `tags` 与 `slots` 是非常重要且需要特别注意的。每个 Radix 树节点都可以包括一个指向存储数据指针的 `slots` 集合，空闲 `slots` 的指针指向 `NULL`。Linux 内核的 Radix 树结构体中还包含用于记录节点存储状态的标签 `tags` 成员，标签通过位设置指示 Radix 树的数据存储状态。

至此，我们了解到 radix 树的结构，接下来看一下 radix 树所提供的 API。

## Linux 内核基数树 API

我们从数据结构的初始化开始看，radix 树支持两种方式初始化。

第一个是使用宏 `RADIX_TREE`：

```
RADIX_TREE(name, gfp_mask);
```

正如你看到，只需要提供 `name` 参数，就能够使用 `RADIX_TREE` 宏完成 radix 的定义以及初始化，`RADIX_TREE` 宏的实现非常简单：

```
#define RADIX_TREE(name, mask) \
         struct radix_tree_root name = RADIX_TREE_INIT(mask)

#define RADIX_TREE_INIT(mask)   { \
        .height = 0,              \
        .gfp_mask = (mask),       \
        .rnode = NULL,            \
} 
```

`RADIX_TREE` 宏首先使用 `name` 定义了一个 `radix_tree_root` 实例并用 `RADIX_TREE_INIT` 宏带参数 `mask` 进行初始化。宏 `RADIX_TREE_INIT` 将 `radix_tree_root` 初始化为默认属性并将 `gfp_mask` 初始化为入参 `mask`。第二种方式是手工定义 `radix_tree_root` 变量，之后再使用 `mask` 调用 `INIT_RADIX_TREE` 宏对变量进行初始化。

```
struct radix_tree_root my_radix_tree;
INIT_RADIX_TREE(my_tree, gfp_mask_for_my_radix_tree); 
```

`INIT_RADIX_TREE` 宏定义：

```
#define INIT_RADIX_TREE(root, mask)  \
do {                                 \
        (root)->height = 0;          \
        (root)->gfp_mask = (mask);   \
        (root)->rnode = NULL;        \
} while (0) 
```

宏 `INIT_RADIX_TREE` 所初始化的属性与 `RADIX_TREE_INIT` 一致。

接下来是 radix 树的节点插入以及删除，这两个函数：

* `radix_tree_insert`
* `radix_tree_delete`

第一个函数 `radix_tree_insert` 需要三个入参：

* radix 树 root 节点结构
* 索引关键字
* 需要插入存储的数据

第二个函数 `radix_tree_delete` 除了不需要存储数据参数外，其他与 `radix_tree_insert` 一致。

radix 树的查找实现有以下几个函数：The search in a radix tree implemented in two ways:

* `radix_tree_lookup`
* `radix_tree_gang_lookup`
* `radix_tree_lookup_slot`

第一个函数 `radix_tree_lookup` 需要两个参数：

* radix 树 root 节点结构
* 索引关键字

这个函数通过给定的关键字查找 radix 树，并返关键字所对应的结点。

第二个函数 `radix_tree_gang_lookup` 具有以下特征：

```
unsigned int radix_tree_gang_lookup(struct radix_tree_root *root,
                                    void **results,
                                    unsigned long first_index,
                                    unsigned int max_items); 
```

函数返回查找到记录的条目数，并根据关键字进行排序，返回的总结点数不超过入参 `max_items` 的大小。

最后一个函数 `radix_tree_lookup_slot` 返回结点 slot 中所存储的数据。

## 链接

* [Radix tree](http://en.wikipedia.org/wiki/Radix_tree)
* [Trie](http://en.wikipedia.org/wiki/Trie)
