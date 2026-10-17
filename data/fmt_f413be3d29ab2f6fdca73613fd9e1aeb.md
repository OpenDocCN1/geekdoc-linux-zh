
# 设备驱动程序中的 Linux DMA

```c
struct dma_async_tx_descriptor *dmaengine_prep_slave_sg(
    struct dma_chan *chan, struct scatterlist *sgl,
    unsigned int sg_len, enum dma_data_direction direction,
    unsigned long flags);
```

```c
struct dma_async_tx_descriptor *dmaengine_prep_dma_cyclic(
    struct dma_chan *chan, void *buf, size_t buf_len,
    size_t period_len, enum dma_data_direction direction);
```

```c
struct dma_async_tx_descriptor *dmaengine_prep_interleaved_dma(
    struct dma_chan *chan, struct interleaved_template *xt,
    unsigned long flags);
```

外设驱动程序预计在调用 `dmaengine_prep_slave_sg()` 之前已经为 DMA 操作映射了离散列表 `scatterlist`，并且在 DMA 操作完成之前必须保持 `scatterlist` 映射。`scatterlist` 必须使用 DMA 设备进行映射。如果需要同步映射，则也必须调用 `dma_sync_*`。正常的设置看起来如下：

```
nr_sg = dma_map_sg(chan->device, sgl, sg_len);
desc = dmaengine_prep_slave_sg(chan, sgl, sg_len, direction, flags);
```

一旦准备好描述符，映射将其映射并提交。

## 提交事务
一旦描述符准备就，需要将其提交到 DMA 引擎队列中。

`dma_cookie_t dmaengine_submit(struct dma_async_tx_descriptor *desc)`

## 发起待处理请求并等待回调通知
如果 DMA 处于空闲状态，通过调用 `dma_issue_pending` 激活。在 DMA 操作完成后，触发任务let。

```
void dma_issue_pending(struct dma_chan *chan)
```

### CMA
在某些架构上，例如 ARM，还需要执行某些特定架构的工作。为了允许这一点，CMA 将调用以下函数：`void dma_contiguous_early_fixup(phys_addr_t base, unsigned long size);`

第二个要的工作是更改架构的 DMA 实现以使用整套机制。分配 CMA 内存时，使用：

`struct page *dma_alloc_from_contiguous(struct device *dev, int count, unsigned int align);`

其第一个参数是代表执行分配的设备。第二个参数指定了要分配的页数，而不是字节数或阶。返回值是系列分配的页中的第一个页。

# DMA 映射的类型

DMA 映射是分配 DMA 缓冲区和为该缓冲区生成设备可访问的地址的结合。DMA 映射有两种类型：

### 1. 一致性 DMA 映射 Coherent DMA Mappings
使用内核空间的非缓存内存映射，通常使用 `dma_alloc_coherent()` 分配。内核分配一个合适的缓冲区并为驱动程序设置映射。CPU 和设备可以同时访问它，因此必须位于缓存一致性内存区域。通常在模块加载的整个期间分配。缓冲区通常在驱动程序初始化时映射，在结束时取消映射，为了做到这一点，硬件保证设备和 CPU 可以并行访问数据，并在无需显式软件刷新的情况下看到彼此的更新。

如果处理器具有一致性架构，分配函数 `dma_alloc_coherent()` 不会使内存变为非缓存。它只会分配内存并为 CPU 创建物理到虚拟的映射。

如果架构是非一致的，`dma_alloc_coherent()` 将使内存变为非缓存，以保持一致性。此函数调用 `arm_dma_alloc()`，后者又调用 `__dma_alloc()`，它接受 `pgprot_t` 作为参数，这基本上是用于使该内存变为非缓存的页属性：

# 第 9 章

# 设备驱动程序中的 Linux DMA

```c
static inline void *dma_alloc_coherent(struct device *dev, size_t size,
dma_addr_t *dma_handle, gfp_t flag)
{
    return dma_alloc_attrs(dev, size, dma_handle, flag, 0);
}
static inline void *dma_alloc_attrs(struct device *dev, size_t size,
dma_addr_t *dma_handle, gfp_t flag,
unsigned long aptrs)
{
    struct dma_map_ops *ops = get_dma_ops(dev);
    void *cpu_addr;

    BUG_ON(!ops);

    if (dma_alloc_coherent(dev, size, dma_handle, &cpu_addr))
        return cpu_addr;

    if (!arch_dma_alloc_attrs(&dev, &flag))
        return NULL;
    if (!ops->alloc)
        return NULL;

    /* 非一致性架构，调用 arm_dma_alloc() */
    cpu_addr = ops->alloc(dev, size, dma_handle, flag, aptrs);
    debug_dma_alloc_coherent(dev, size, *dma_handle, cpu_addr);
    return cpu_addr;
}
```

```c
/*
 * 分配 DMA 一致性内存空间并返回该空间的内核重映射
 * 虚拟地址和总线地址。
 */
void *arm_dma_alloc(struct device *dev, size_t size, dma_addr_t *handle,
gfp_t gfp, unsigned long aptrs)
{
    pgprot_t prot = __get_dma_pgprot(atrs, PAGE_KERNEL);

    return __dma_alloc(dev, size, handle, gfp, prot, false,
        attrs, __builtin_return_address(0));
}
```

# 设备驱动程序中的 Linux DMA

分配并映射大型 `PAGE_SIZE` 或更大的 一致性 DMA 区域应该：

```
#include <linux/dma-mapping.h>
dma_addr_t dma_handle;
cpu_addr = dma_coherent(dev, size, &dma_handle);
```

`dma_coherent()` 函数为设备执行 DMA 分配非缓存内存。它分配页、CPU 视图的  `虚拟` 地址，并将第三个参数设置为设备的地址。缓冲区自动放置在设备访问的地方。参数 `dev` 是一个结构体指针。此函数可以在带有 `GFP_ATOMIC` 标志的中断文中调用。参数 `size` 是你想要分配的字节长度。`dma_coherent()` 返回两个值：用于 CPU 访问的 `cpu_addr` 和 DMA 地址 `dma_handle`。

CPU 虚拟地址和 DMA 地址都保证对齐到最小的 `PAGE_SIZE`，且大于等于请求的大小。

取消映射并释放这样的 DMA 区域，你调用：

`dma_free_coherent(dev, size, cpu_addr, dma_handle);`

其中 `dev` 和 `size` 与上述 `dma_coherent()` 调用相同，`cpu_addr` 和 `dma_handle` 是 `dma_coherent()` 返回给你的值。此函数可能在中断文中调用。

### 2. 流式 DMA 映射 Streaming DMA Mappings
使用缓存映射并根据操作清理或失效。`dma_map_single()` 和 `dma_unmap_single()`。这与一致性映射不同，因为它处理的是预先选择的地址，通常只为一次 DMA 传输映射并立即取消映射。
