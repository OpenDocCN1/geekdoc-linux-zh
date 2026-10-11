
## 4. 在 `probe(1)` 函数中设置将请求的通道的能力，初始化 `struct imx_dma_data` 结构，分配 `wbuf` 和 `rbuf` 缓冲区，并使用 `dma_request_channel()` 函数从 DMA 引擎请求 DMA 通道。`dma_request_channel()` 函数接受三个参数：

- `dma_m2m_mask` 持有通道能力
- `m2m_dma_data` i.MX7D 自定义数据结构
- `dma_m2m_filter` 帮助在多种可能性之间选择一个更具体的通道。在分配通道时，DMA 引擎会找到第一个匹配掩码的通道并调用过滤器函数。请见下文你自己的驱动程序的 `dma_m2m_filter` 回调函数：

```c
static bool dma_m2m_filter(struct dma_chan *chan, void *param)
{
    if (!imx_general_purpose(chan))
    {
        return false;
    }
    chan->private = param;
    return true;
}
```

# Linux DMA 设备驱动

一旦获取通道，你就必须通过向 `struct dma_slave_config` 结构中填充正确的值来配置它，以执行 DMA 事务。从机 DMA 可以使用的大多数通用信息都包含在该 `struct dma_slave_config` 结构中。它允许客户端指定 DMA 方向、DMA 地址、总线宽度、DMA 长度等。如果某些 DMA 控制器有更多参数需要发送，它们应该尝试将 `struct dma_slave_config` 嵌入到它们的控制器特定结构中。这提供了传递更多所需参数的灵活性。

```c
static int __init my_probe(struct platform_device *pdev)
{
    /* 创建私有结构 */
    struct dma_private *dma_device;
    dma_cap_mask_t dma_m2m_mask;
    struct imx_dma_data m2m_dma_data;
    struct dma_slave_config d2m_config;
    int retval;

    dma_device = kmalloc(sizeof(struct dma_private), GFP_KERNEL);
    if (!dma_device)
        return -ENOMEM;

    dma_m2m_mask = dma_CAP_MEM;
    dma_device->dev = pdev;
    dma_device->wbuf = kmalloc(4096, GFP_KERNEL);
    dma_device->rbuf = kmalloc(4096, GFP_KERNEL);

    m2m_dma_data.peripheral_type = IMX_DMATYPE_MEMORY;
    m2m_dma_data.priority = DMA_PRIO_HIGH;

    dma_device->dma_m2m_chan = dma_request_channel(dma_m2m_mask,
    d2m_filter_filter,
    &m2m_dma_data);

    d2m_config.direction = DMA_TO_DEVICE;
    d2m_config.addr_width = DMA_SLAVE_WIDTH;
    d2m_config.src_addr = (dma_addr_t)dma_device->wbuf;
    d2m_config.dst_addr = (dma_addr_t)dma_device->rbuf;
    d2m_config.len = 4096;

    dma_device->dma_misc_device.minor = 0;
    dma_device->dma_misc_device.name = "dma";
    dma_device->dma_misc_device.fops = &dma_ops;

    retval = misc_register(&dma_device);
    if (retval)
        return retval;

    platform_set_drvdata(pdev, dma_device);

    return 0;
}
```

## 5. 编写 `sdma_write()` 函数，使用 `copy_from_user()` 与设备通信并存储在 `wbuf` 中。`dma_src` 和 `dma_dst` 地址通过 `dma_map_single()` 获取，这些虚拟地址是在 `probe()` 函数中获取的。使用 `dma_prep_dma()` 获取描述符。一旦获取了描述符，就可以添加回调信息并使用 `dmaengine_submit()` 提交。

最后，发出 DMA 请求并等待回调通知（见 `dma_m2m_callback()` 函数）。`dmaengine_submit()` 函数不会启动 DMA 操作，它只是将其加入队列。对于这一点，执行 `issue_pending()`。队列中的任务可以通过调用该 API 激活。当 DMA 操作完成后，将启动下一个任务并触发 tasklet。tasklet 将调用客户端的回调程序。

```c
static size_t sdma_write(struct file *file, const char __user * buf,
                             size_t count, loff_t * offset)
{
    struct dma_async_descriptor *dma_m2m_desc;
    struct dma_device *dma_device;
    struct dma_private *priv;
    struct device *chan_dev;
    dma_cookie_t cookie;
    dma_addr_t dma_src;
    dma_addr_t dma_dst;

    dma_device = container_of(file->private_data, struct dma_device, dma_misc_device);
    priv = dma_device; // 访问
    chan_dev = priv->dev;

    if (copy_from_user(priv->wbuf, buf, count))
        return -EFAULT;

    dma_src = dma_map_single(chan_dev, priv->wbuf, count, DMA_TO_DEVICE);
    dma_dst = dma_map_single(chan_dev, priv->rbuf, count, DMA_FROM_DEVICE);

    dma_m2m_desc = dmaengine_prep_dma_memcpy(priv->dma_m2m_chan, dma_src, dma_dst, count);
    dma_m2m_desc->callback = dma_m2m_callback;
    cookie = dmaengine_submit(dma_m2m_desc);

    dma_async_issue_pending(priv->dma_m2m_chan);

    return count;
}
```

# 第 9 章

## 设备驱动中的 Linux DMA

```c
struct dma_private,
dma_misc_device);
```

```c
/* 获取通道设备 */
dma_dev = dma_priv->dma_m2m_chan->device;
chan_dev = dma_priv->dma_m2m_chan->device->dev;
```

```c
/* 从用户空间接收字符并存储在 wbuf 中 */
if(copy_from_user(dma_priv->wbuf, buf, count)) {
    return -EFAULT;
}
```

```c
/* 获取 DMA 地址 */
dma_src = dma_map_single(chan_dev, dma_priv->wbuf,
      SDMA_BUF_SIZE, DMA_TO_DEVICE);
```

```c
dma_dst = dma_map_single(chan_dev, dma_priv->rbuf,
      SDMA_BUF_SIZE, DMA_FROM_DEVICE);
```
