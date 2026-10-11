
```c
struct block_device_operations {
    int (*open)(struct block_device *, fmode_t);
    int (*release)(struct block_device *, fmode_t);
    int (*ioctl)(struct block_device *, fmode_t, unsigned int, unsigned long);
    // ... other operations
};
```

## 网络设备

网络设备处理网络通信。示例包括以太网、Wi-Fi 和蓝牙对适配器。

关键组件：

- `net_device_structure`结构: 表示一个网络接口。
- `net_device_ops`结构: 定义网络接口的操作。
- `sk_buff`: 表示一个网络数据包。

```c
struct net_device_ops {
    int (*ndo_open)(struct net_device *device);
    int (*ndo_stop)(struct net_device *device);
    netdev_tx_t (*ndo_start_xmit)(struct sk_buff *, struct net_device *device);
    // ... other operations
};
```

## 内核 I/O 子系统

内核 I/O 子系统为访问各种设备提供了统一接口。它处理如下任务：

- 文件系统管理: 创建、读取、写入和删除文件。
- 块设备管理: 管理块设备并处理块请求。
- 字符设备管理: 处理字符设备操作。
- 网络通信: 管理网络接口并处理网络数据包。
- 缓冲区管理: 为 I/O 操作分配和管理内存缓冲区。

## 用户态应用

用户态应用通过系统调用与 I/O 子系统交互。用于 I/O 操作的系统调用包括：

- `open`: 打开文件或设备。
- `close`: 关闭文件或设备。
- `read`: 从文件或设备读取数据。
- `write`: 向文件或设备写入数据。
- `ioctl`: 执行设备特定的控制操作。
- `socket`: 创建网络套接字。
- `send`: 通过网络套接字发送数据。
- `recv`: 通过网络套接字接收数据。

## I/O 调度

I/O 调度是一种通过重新排序 I/O 请求来优化块设备性能的技术。内核提供了不同的 I/O 调度器来高效处理块请求。

## 缓冲区缓存

缓冲区缓存是用于缓存磁盘的内存区域。它通过减少磁盘访问次数来提高 I/O 性能。

I/O 子系统是 Linux 内核的关键组件。它为管理硬件设备和与用户态应用交互提供了健壮且高效的机制。理解涉及 I/O 子系统的不同组件和概念对于开发高效可靠的设备驱动程序和应用至关重要。

# 第四章

## Linux 设备驱动编程中的 C++

在 Linux 设备驱动开发中，高效的数据结构对于管理硬件资源、处理中断和优化性能至关重要。列表、树和哈希表是该领域广泛使用的基础数据结构。本文探讨了这些数据结构及其在 C++ 的 Linux 设备驱动编程中的应用。

### 列表

列表是数据元素的线性集合，每个元素指向下一个元素。它的结构简单，但适用于多种用用例。

列表的类型：

- 单链表: 每个元素指向下一个元素。
- 双链表: 每个元素同时指向下一个和上一个元素。
- 环形链表: 最后一个元素指向第一个元素。

C++ 实现（单链表）：

```cpp
struct list_node {
    void *data;
    struct list_node *next;
};

struct list {
    struct list_node *head;
};

void list_init(struct list *list) {
    list->head = NULL;
}

void list_add(struct list *list, struct list, void *data) {
    struct list_node *new_node = (struct list_node*)malloc(sizeof(struct list_node));
    new_node->data = data;
    new_node->next = list->head;
    list->head = new_node;
}

void list_remove(struct list *list, void *data) {
    // 为了简洁省略了实现
}
```

#### 在设备驱动程序中的应用：

- 中断处理: 维护挂起中断列表。
- 设备队列: 管理对设备的请求。
- 资源管理: 跟踪已分配的资源。

### 树

树是一种层次化数据结构，每个节点都有零或多个子节点。它对于搜索、排序和组织数据非常高效。

树的类型：

- 二叉树: 每个节点最多有两个孩子。
- 二叉搜索树: 左孩子小于父节点，右孩子大于父节点的二叉树。
- AVL 树: 自平衡二叉搜索树。
- 红黑树: 自平衡的二叉搜索树。

C++ 实现（二叉搜索树）：

```cpp
struct tree_node {
    int data;
    struct tree_node *left;
    struct tree_node *right;
};

struct tree {
    struct tree_node *root;
};

void tree_insert(struct tree *tree, int data) {
    // 为了简洁省略了实现
}

struct tree_node *tree_search(struct tree *tree, int data) {
    // 为了简洁省略了实现
}
```

#### 在设备驱动程序中的应用：

- 设备层次结构: 表示设备树。
- 配置管理: 存储设备配置。
- 调度: 根据截止日期优先级任务。

### 哈希表

哈希表使用哈希函数将键映射到数组的索引。它提供了高效的插入、删除和搜索操作。

C++ 实现：

```cpp
#include <unordered_map>

std::unordered_map<int, void *> hash_table;

void hash_table_insert(int key, void *data) {
    hash_table[key] = data;
}

void *hash_table_lookup(int key) {
    auto it = hash_table.find(key);
    if (it != hash_table.end())
        return it->second;
    return NULL;
}
```

#### 在设备驱动程序中的应用：

- 缓存: 存储频繁访问的数据以便快速检索。
- 符号表: 将符号映射到其地址。
- 设备注册: 将设备名称与设备结构关联。

## 设备开发的注意事项

- 内存效率: 选择内存内存占用的数据结构。
- 性能: 考虑临界区操作的时间复杂度。
- 同步: 使用锁或其他同步机制保护数据结构免并发访问。
- 错误处理: 实现健壮的错误处理以防止数据损坏。

列表、树和哈希表是 Linux 驱动开发人员必备的工具。通过理解它们的优缺点，你可以为特定的用例选择合适的数据结构，从而开发出高效可靠的设备驱动程序。

指向分配区域。

```c
void kmalloc(size_t size, gfp_t flags);
```

- `size`: 要分配的内存块的大小（以字节为单位）。
- `flags`: 指定内存类型和分配行为的分配标志。

![](img/ac3ad875fcf65d3ecc3d8ea995c85f9e_88_0.png)

- `size`: 要分配的内存块的大小（以字节为单位）。

注意：对于小分配，`vmalloc()` 的效率可能低于 `kmalloc()`，并且更容易产生碎片。

```c
vfree()
```

释放由 `vmalloc()` 分配的内存。
