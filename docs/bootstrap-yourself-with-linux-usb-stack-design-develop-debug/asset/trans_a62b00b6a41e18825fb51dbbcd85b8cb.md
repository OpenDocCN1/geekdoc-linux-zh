

## Gadget 驱动：设计

![](img/779a74a6577501a55983f193067274a3_193_0.png)

**图 13.6**
USB OUT 传输中的活动序列。

一旦配置成功，类驱动程序（class driver）就会为数据传输做好准备。它分配必要的缓冲区并请求一个 `struct usb_request` 对象；随后，它使用 `usb_ep_queue` 将其放入 gadget 框架（gadget framework）。类驱动程序知道预期数据的大小，并将其视为提交给 gadget 框架的 `struct usb_request` 的一部分，它在框架中被入队。gadget 框架在中断例程序（interrupt routine）中接收请求。一旦收集到请求的数据，控制权就会通过完成例程序（complete routine）传回类驱动程序。`struct usb_request` 现在包含了接收到的数据、实际读取的数据以及请求状态。然后，类驱动程序从请求中提取信息并进行处理。

第 13 章 = Gadget 驱动

## IN 传输

当 USB 主机通过 IN 传输启动通信时，设备必须响应主机的请求。图 13.7 描述了 IN 传输期间发生的活动序列。

类驱动程序准备要传输的数据，并映射到使用 `usb_ep_alloc_request` 分配的 `struct usb_request`。类驱动程序将 `usb_request` 放入 gadget 框架进行传输。之后，gadget 框架使用硬件驱动程序传输数据。一旦传输-

![](img/779a74a6577501a55983f193067274a3_194_0.png)

**图 13.7**
USB IN 传输中的活动序列。

## Gadget 驱动：实现

传输完成后，gadget 驱动程序调用完成回调（complete callback）将传输状态传递给类驱动程序。前面的章节展示了典型情况下 Linux gadget 框架的活动序列。你可以探索在错误场景下发生的其他路径。下一节将探讨一个实际的 gadget 驱动。

### GADGET 驱动：实现

要开发一个 gadget 驱动，你需要了解硬件，因为 gadget 驱动的某些部分特定于底层 USB 设备控制器。下节将结合第 12 章中针对瑞萨 USB 控制器的 PDC 驱动，继续探讨 gadget 驱动的实现。以下代码基于内核源码中的 `drivers/usb/gadget/r8a66597-`。

该过程的第一步是为关键数据结构 `struct usb_ep_ops` 和 `struct usb_gadget_ops` 定义回调函数，这允许你控制 gadget 硬件。gadget 驱动不需要支持所有的端点和 gadget 数据结构；这可能是由于硬件不可用。

```c
static struct usb_ep_ops r8a66597_ep_ops = {
  .enable = r8a66597_enable,
  .disable = r8a66597_disable,
  .alloc_request = r8a66597_alloc_request,
  .free_request = r8a66597_free_request,
  .queue = r8a66597_queue,
  .deque = r8a66597_deque,
  .set_halt = r8a66597_set_halt,
  .set_wedge = r8a66597_set_wedge,
  .fifo_flush = r8a66597_fifo_flush,
};

static struct usb_gadget_ops r8a66597_gadget_ops = {
  .get_frame = r8a66597_get_frame,
};
```

这些数据结构在 PDC 驱动的探测（probe）函数期间注册到 `struct r8a66597` 中定义的 `struct usb_gadget`。下一步是实现导出的接口函数，即 `usb_gadget_register_driver` 和 `usb_gadget_unregister_driver`。前面的章节展示了这两个接口函数的活动序列。图 13.2 展示的 `usb_gadget_register_driver` 负责绑定 gadget 驱动并启动 gadget 控制器。此外，注意功能驱动程序传递给 `usb_gadget_register_driver` 的 `struct_gadget_driver` 对象应该支持两个基础回调——bind 和 setup，以便 gadget 驱动能够正常工作。

```c
int usb_gadget_register_driver(struct usb_gadget_driver *driver)
{
    if (!driver || driver->speed != USB_SPEED_HIGH ||
        !driver->bind || !driver->setup)
        return -EINVAL;
    retval = driver->bind(&r8a66597->gadget);
    if (retval) {
        printk(KERN_ERR, "bind to driver error (%d)\n", retval);
        dev_dev(&r8a66597->gadget.dev);
        goto error;
    }
    r8a66597_set(r8a66597, VBSE, INTEN);
}
EXPORT_SYMBOL(usb_gadget_register_driver);
```

如图 13.3 所示，`usb_gadget_unregister_driver` 将 gadget 驱动从功能驱动程序中解绑定并关闭 gadget 控制器。

```c
int usb_gadget_unregister_driver(struct usb_gadget_driver *driver)
{
    if (driver != r8a66597->driver || !driver->unbind)
        return -EINVAL;
    driver->unbind(&r8a66597->gadget);
    init_controller(r8a66597);
    disable_controller(r8a66597);
    device_del(&r8a66597->gadget.dev);
    r8a66597->driver = NULL;
    return 0;
}
EXPORT_SYMBOL(usb_gadget_unregister_driver);
```

下一个重要的函数是处理通过端点（Endpoint）发送的控制请求。控制请求的处理是中断例程序的一部分。如图 13.4 所示，gadget 框架处理控制请求并将通过注册的 setup 回调将控制传递给类驱动程序。

```c
static void irq_control_stage(struct r8a66597 *r8a66597)
{
  // ... 内部实现 ...
  spin_lock(r8a66597->lock);
  case CS_WRND:
    if (setup_packet(r8a66597, &ctrl)) {
      spin_unlock(&r8a66597->driver);
      if (r8a66597->setup(r8a66597->gadget, &ctrl) < 0) {
        spin_lock(&r8a66597->driver);
        r8a66597_set(r8a66597, VBSE, INTEN);
      }
    }
}
```

（注：由于原文 OCR 存在大量重复和错误，上述翻译已根据逻辑流和代码上下文进行了清理。）

