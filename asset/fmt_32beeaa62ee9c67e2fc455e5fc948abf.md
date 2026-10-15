
`struct page * alloc_page(unsigned int gfp_mask)`

`unsigned long __get_free_page(unsigned int gfp_mask)`

这些函数的功能与它们的兄弟相同，但为`order`传递了零（$2^0$ = 一个页）。

# 清零页

如果你需要返回的页填充为零，请使用函数：

`unsigned long get_zeroed_page(unsigned int gfp_mask)`

此函数的工作与`__get_free_page()`相同，但分配的页随后会被清零。这对于提供给用户空间的页非常有用，因为分配页中的随机垃圾并不那么随机——它可能并不是随机的。现在已经理解了内核如何管理内存——通过页、区域等——让我们来看看内核实现的、允许你在内核中分配和释放内存的接口。

内核提供了一种请求内存的低级机制，以及若干个访问内存的接口。所有这些接口都以页为粒度分配内存，并在`<linux/gfp.h>`中声明。核心函数是：

`struct page *alloc_pages(unsigned int gfp_mask, unsigned int order);`

这分配了$2^{order}$（即`1 << order`）个连续页，并返回指向第一个页结构结构的指针；如果出错则返回`NULL`。我们将在后面的章节中查看`gfp_mask`参数。你可以使用函数将页转换为逻辑地址：

`void page_address(struct page *page);`

它返回指向物理页当前所在逻辑地址的指针。如果你不需要实际的`struct_page`，可以调用：

`unsigned long __free_pages(unsigned int gfp_mask, unsigned int order);`

此函数的工作原理与`alloc_pages()`相同，只是它直接返回第一个请求页的逻辑地址。因为页是连续的，其他页只需跟随第一页即可。

## 第11 章 内存管理

该函数返回一个至少为`size`字节的内存区域指针。分配的内存区域在物理上是连续的。出错时，它返回`NULL`。内核分配总是会成功，除非可用内存不足。因此，你必须在所有调用`kmalloc()`后检查是否为`NULL`并妥善处理错误。

让我们来看一个例子。假设你需要为一个虚拟的`dog`结构体动态分配足够的空间：

```c
struct dog *ptr;
ptr = kmalloc(sizeof(struct dog), GFP_KERNEL);
if (!ptr) {
    /* 处理错误 */
}
```
