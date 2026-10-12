
该结构体很大，但系统中只有三个区域，因此也只有这三个结构体实例。让我们来看看其中更重要的字段。

`lock` 字段是一个自旋锁，用于保护该结构体免受并发访问。请注意，它仅保护该结构体本身，而不是该区域内驻留的所有页面。特定的锁并不保护单个页面，尽管内核的某些部分可能会锁定恰好驻留在这些页面中的数据。

`watermark` 数组持有该区域的最小、低和高水位线。内核使用水位线来设定每个区域合适的内存消耗基准，并随着水位线相对于空闲内存的变化而调整其激进程度。

不出所料，`name` 字段是一个以 NULL 结尾的字符串，表示该区域的名称。内核在启动期间在 `mm/page_alloc.c` 中初始化此值，这三个区域分别被命名为 DMA、Normal 和 HighMem。

> <sup>2</sup> Linux 的高端内存与 DOS 中的高端内存无关，后者旨在绕过 DOS 和 x86 “实模式”处理器状态的局限性。

## 获取页面（Getting Pages）

现在，在理解了内核如何通过页面、区域等机制管理内存之后，让我们看看内核实现了哪些接口，以便您在内核中分配和释放内存。

内核提供了一种请求内存的低级机制，以及几个访问它的接口。所有这些接口都以页面大小的粒度分配内存，并在 `<linux/gfp.h>` 中声明。核心函数是

```c
struct page * alloc_pages(gfp_t gfp_mask, unsigned int order)
```

这会分配 $2^{\text{order}}$（即 $1 \ll \text{order}$）个连续的物理页面，并返回指向第一个页面的 page 结构的指针；出错时返回 NULL。我们稍后会在另一章节中讨论 `gfp_t` 类型和 `gfp_mask` 参数。你可以使用以下函数将给定的页面转换为其逻辑地址

```c
void * page_address(struct page *page)
```

这返回指向给定物理页面当前驻留的逻辑地址的指针。如果你不需要实际的 `struct page`，你可以调用

```c
unsigned long __get_free_pages(gfp_t gfp_mask, unsigned int order)
```

该函数的工作方式与 `alloc_pages()` 相同，除了它直接返回请求的第一个页面的逻辑地址。由于页面是连续的，其他页面紧随其后。

如果你只需要一个页面，有两个函数作为包装器实现，以节省你的一些输入：

```c
struct page * alloc_page(gfp_t gfp_mask)
unsigned long __get_free_page(gfp_t gfp_mask)
```

这些函数的工作方式与其姊妹函数相同，但传递的 order 为零（$2^0 =$ 一个页面）。

## 获取已清零的页面（Getting Zeroed Pages）

如果你需要返回的页面填充为零，请使用函数

```c
unsigned long get_zeroed_page(unsigned int gfp_mask)
```

该函数的工作方式与 `__get_free_page()` 相同，除了分配的页面随后被清零——每个字节的每一位都被清除。这对于提供给用户空间的页面非常有用，因为分配页面中的随机垃圾并不那么随机；它可能包含敏感数据。在返回给用户空间之前，必须将所有数据清零或进行其他清理，以确保系统安全不受损害。表 12.2 列出了所有低级页面分配方法。

表 12.2 低级页面分配方法

| 函数 | 描述 |
| :--- | :--- |
| `alloc_page(gfp_mask)` | 分配单个页面并返回指向其 page 结构的指针 |
| `alloc_pages(gfp_mask, order)` | 分配 $2^{\text{order}}$ 个页面并返回指向第一个页面 page 结构的指针 |
| `__get_free_page(gfp_mask)` | 分配单个页面并返回指向其逻辑地址的指针 |
| `__get_free_pages(gfp_mask, order)` | 分配 $2^{\text{order}}$ 个页面并返回指向第一个页面逻辑地址的指针 |

## 释放页面

一组函数允许你释放不再需要的已分配页面：

```c
void __free_pages(struct page *page, unsigned int order)
void free_pages(unsigned long addr, unsigned int order)
void free_page(unsigned long addr)
```

你必须小心，只释放你分配过的页面。传递错误的 `struct page` 或地址，或者错误的 `order`，都可能导致内存损坏。请记住，内核信任自身。与用户空间不同，如果你要求内核这样做，它会毫不犹豫地让自己挂起。

让我们看一个例子。在这里，我们要分配八个页面：

```c
unsigned long page;

page = __get_free_pages(GFP_KERNEL, 3);

if (!page) {
    /* 内存不足：你必须处理此错误！ */
    return -ENOMEM;
}

/* 现在 'page' 是八个连续页面中第一个页面的地址 ... */
在我们使用完这八个页面后，这里将它们释放：
free_pages(page, 3);
/*
 * 我们的页面现在已释放，
 * 我们不应再访问存储在 'page' 中的地址
 */
```

`GFP_KERNEL` 参数是 `gfp_mask` 标志的一个例子。稍后将会讨论。请注意对 `__get_free_pages()` 调用后的错误检查。内核内存分配可能会失败，你的代码必须检查并处理此类错误。这可能意味着要撤销你之前所做的所有事情。因此，通常在例程开始时分配内存往往更有意义，这样更容易处理错误。否则，当你尝试分配内存时，要退出可能已经相当困难。

当你需要物理连续的页面大小的块时，这些低级页面函数非常有用，特别是当你只需要正好一个或两个页面时。对于更通用的字节大小分配，内核提供了 `kmalloc()`。

## `kmalloc()`

`kmalloc()` 函数的操作类似于用户空间中熟悉的 `malloc()` 例程，除了额外的 `flags` 参数外。`kmalloc()` 函数是一个简单的接口，用于以字节大小的块获取内核内存。如果你需要完整的页面，之前讨论的接口可能是更好的选择。然而，对于大多数内核分配，`kmalloc()` 是首选接口。

该函数在 `<linux/slab.h>` 中声明：

```c
void * kmalloc(size_t size, gfp_t flags)
```

该函数返回一个指向内存区域的指针，该区域长度至少为 `size` 字节。² 分配的内存区域是物理连续的。出错时，它返回 `NULL`。除非可用内存不足，否则内核分配总是成功的。因此，在所有对 `kmalloc()` 的调用之后，你必须检查 `NULL` 并适当处理错误。

让我们看一个例子。假设你需要动态分配足够的空间给一个虚构的 `dog` 结构体：

```c
struct dog *p;
p = kmalloc(sizeof(struct dog), GFP_KERNEL);
if (!p) /* 处理错误 ... */
```
