
```c
dma_unmap_single(dma_m2m_chan->device->dev, dma_src, SDMA_BUF_SIZE,
DMA_MEM_TO_MEM);
dma_unmap_single(dma_m2m_chan->device->dev, dma_dst, SDMA_BUF_SIZE,
DMA_MEM_TO_MEM);
```

```c
/* 检查 DMA 之后两个缓冲区是否保持相同值 */
if (*rbuf) != (*wbuf) {
    pr_info("buffer copy failed!\n");
    return -1;
}
pr_info("buffer copy passed!\n");
pr_info("rbuf is %s\n", rbuf);
pr_info("wbuf is %s\n", wbuf);

return count;
```

```c
struct file_operations dma_fops = {

    open: sdma_open,

    release: sdma_release,

    write: sdma_write,

};
```

```c
static struct miscdevice dma_miscdevice = {
    .minor = MISC_DYNAMIC_MINOR,
    name = "sdma_test",
    .fops = &dma_fops,
};
```

```c
int __init_sdma_init_module(void) {
    int retval;
    retval = misc_register(&dma_miscdevice);
    if (retval) return retval;
    pr_info("mydev: got minor %i\n", dma_miscdevice.minor);
    return 0;
}
```

```c
module_init(sdma_init_module);
module_exit(sdma_cleanup_module);
```

```c
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto Liberal liberal@arroweurope.com");
MODULE_DESCRIPTION("这是一个用于内存拷贝的 SDMA 驱动程序");
```

# sdma_m2m.ko 目标演示

打开 `minicom` 并执行启动。按下 `RESET SW2` 开始启动序列。按任意键停止 `U-Boot` 启动，然后使用 `"run netboot"` 命令进行网络启动。

`U-Boot > run netboot` /* 开始网络启动 */

```bash
root@imx6qsabres:~# insmod sdma_m2m.ko /* 加载模块 */
root@imx6qsabres:~# echo abcdefg > /dev/sdma_test /* 向 wbuf 写入值，启动从 wbuf 拷贝到 rbuf 的 DMA 事务并比较两个缓冲区的值 */
root@imx6qsabres:~# rmmod sdma_m2m.ko /* 移除模块 */
```

# DMA 分散/聚合映射

分配的缓冲区在物理内存中可能是碎片化的，不需要连续分配。这些分配的物理内存块映射到调用虚拟空间中的连续缓冲区，从而能够轻松访问分配的物理内存。多种方法可以通过 DMA 发送多个缓冲区的内容。它们可以一次映射发送，也可以通过分散/聚合发送，或者一次性发送所有。许多设备接受指针数组和长度的分散列表（`scatterlist`）。分散列表项的大小为一个页。分散/聚合 I/O 允许系统对分散在物理内存中的缓冲区执行 I/O 操作。例如，用户空间中创建的大多页缓冲区：应用程序看到连续的虚拟地址范围，但这些地址背后的物理页显然不相邻。如果要把该缓冲区通过一次 I/O 操作写入设备，必须执行以下两种操作之一：(1) 将数据拷贝到连续缓冲区，或 (2) 设备必须能够处理物理地址列表，从每个段中获取正确数量的数据。分散/聚合 I/O 避免了将数据拷贝到连续缓冲区的需求，可以极大提高 I/O 操作的效率。

例如，用户空间中创建的大多页缓冲区：应用程序看到连续的虚拟地址范围，但这些地址背后的物理页显然不相邻。如果该缓冲区通过单次 I/O 操作写入设备，必须执行以下两种操作之一：(1) 将数据拷贝到连续缓冲区，或 (2) 设备必须能够处理物理地址列表，从每个段中获取正确数量的数据。分散/聚合 I/O 避免了将数据拷贝到连续缓冲区的需求，可以极大提高 I/O 操作的效率。

分散列表结构（`scatterlist`）的定义如下：

```c
struct scatterlist {
    unsigned long page;
    unsigned int offset;
    dma_addr_t dma_addr;
    unsigned int length;
};
```

首先，创建一个分散列表：

```c
struct scatterlist sg;
```

初始化一个分散列表：

这里，`sg` 指向已分配的缓冲区。

```c
void scatter_init_table(struct scatterlist *sg, int count);
```

这里，`nents` 是分配缓冲区的数量。

```c
void scatter_init_table(struct scatterlist *sg, int count);
```

这里，`buf` 是分配的缓冲区，`bufen` 是分配缓冲区的长度。

映射缓冲区以获取物理地址：

```c
void dma_map_single(struct device *dev, void *ptr, size_t size, dma_direction_t direction);
```

这里，`dev` 是设备指针。

```c
void dma_map_single(struct device *dev, void *ptr, size_t size, dma_direction_t direction);
```

这里，`ptr` 是缓冲区指针。

```c
void dma_map_single(struct device *dev, void *ptr, size_t size, dma_direction_t direction);
```

这里，`size` 是缓冲区大小。

```c
void dma_map_single(struct device *dev, void *ptr, size_t size, dma_direction_t direction);
```

这里，`direction` 是 DMA 方向。

```c
void dma_map_single(struct device *dev, void *ptr, size_t size, dma_direction_t direction);
```

```c
例如，用户空间中创建的大多页缓冲区：应用程序看到连续的虚拟地址范围，但这些地址背后的物理页显然不相邻。如果该缓冲区通过单次 I/O 操作写入设备，必须执行以下两种操作之一：(1) 将数据拷贝到连续缓冲区，或 (2) 设备必须能够处理物理地址列表，从每个段中获取正确数量的数据。分散/聚合 I/O 避免了将数据拷贝到连续缓冲区的需求，可以极大提高 I/O 操作的效率。
```

### 8.2 分散/聚合 DMA 实验

`sdma_m2m.ko` 目标演示

打开 `minicom` 并执行启动。按下 `RESET SW2` 开始启动序列。按任意键停止 `U-Boot` 启动，然后使用 `"run netboot"` 命令进行网络启动。

# DMA 驱动

```c
init_table(sg2, 3);

sq_set_buf(&sg2[0],fbox, SDMA_BUF_SIZE);

sq_set_buf(&sg2[1],fbox2, SDMA_BUF_SIZE);

sq_set_buf(&sg2[2],fbox3, SDMA_BUF_SIZE);

dma_map_sq(NULL, sg2, 3, DMA_FROM_DEVICE);

sq_init_table(sg3, 1);

sq_set_buf(sg3, dma_src_coherent, SDMA_BUF_SIZE);

dma_map_sq(NULL, sg3, 1, DMA_TO_DEVICE);

sq_init_table(sg4, 1);

sq_set_buf(sg4, dma_dst_coherent, SDMA_BUF_SIZE);

dma_map_sq(NULL, sg4, 1, DMA_FROM_DEVICE);
```

5. 在 `dma_write()` 中获取通道描述符，将 DMA 操作添加到待处理队列，发布 DMA 请求，并等待回调通知：

```c
```
