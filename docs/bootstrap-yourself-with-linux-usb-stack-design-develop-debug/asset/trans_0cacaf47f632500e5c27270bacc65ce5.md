

# Linux USB Gadget Driver

![](img/779a74a6577501a55983f193067274a3_162_0.png)

**图 11.2**
Linux USB gadget 框架的简单表示。

实现了特定硬件的例程，允许访问寄存器、内存空间和中断。你可以在第 12 章“外设控制器驱动”中探索更多关于 USB 控制器驱动的内容。

# Gadget 驱动

gadget 驱动与上一节讨论的第 9 章驱动/USB 设备框架类似。gadget 层处理大多数与 USB 协议相关的需求，并传递特定于类的请求。该层位于硬件层和类层之间，提供了必要的 USB 协议抽象。你可以在第 13 章“Gadget 驱动”中探索关于 gadget 驱动的更多内容。

# 类驱动

类驱动或功能驱动实现了实际的设备功能。gadget 驱动处理了大部分 USB 功能，但 gadget 层会传递特定于类的请求。类驱动也处理 USB 特定的请求，以及功能实现。USB 工作组 (DWG) 定义了各种 USB 类规范，你可以在 http://www.usb.org/developers/devclass_docs#approved 引用这些规范。第 13 章将更详细地介绍类驱动。

# 总结

Linux USB gadget 子系统是一个简单的三层架构，实现了 USB 设备规范。本章对 Linux USB gadget 栈进行了简要概述，这将帮助你理解接下来的三章。

# 更多阅读

本章捕述了 USB 设备栈的简单通用架构。收集来自不同厂商的 USB 栈架构，并将其与本章中的架构进行比较。你也可以参考 http://www.linux-usb.org/gadget/ 获取 Linux USB 设备栈的概述。Linux 文档 `Documentation/usb/gadget_serial.txt` 提供了关于 gadget 架构的更多机会。

# 第 12 章

# 外设设备控制器驱动

本章内容

- 引导基础要素：平台驱动
- Linux USB 外设控制器驱动
- USB 设备控制器驱动

在 Linux USB gadget 子系统中，USB 外设设备控制器 (PDC) 驱动是最低的驱动层，更接近硬件。该层与 USB PDC 硬件交互，并将硬件功能扩展到其他驱动层。因此，它充当 USB 驱动层与平台驱动之间的接口，用于控制 USB 设备控制器。你需要完全理解 USB PDC 和平台，才能开发 USB 驱动。

有趣的是，USB PDC 驱动执行的 USB 特有任务极少，大多数 USB 特有任务是在 PDC 驱动之上的硬件或 USB 层完成的。因此，USB PDC 驱动的功能与其他直接与硬件交互的内核模块类似。根据平台的设置，USB 设备控制器通过平台提供的任何不同接口连接到平台硬件。PDC 驱动使用平台驱动框架或 PCI 驱动框架作为基础来开发驱动。

# 第 12 章 = 外设控制器驱动

从顶层概述来看，PDC 驱动的主要功能是在平台探测（probe）设备成功时分配必要的资源（如内存和中断请求 IRQs），并在设备断开时释放分配的资源。因此，成功的 PDC 驱动允许 USB 控制器为其他 USB 驱动叶节点就绪，并释放平台资源。

本章进一步探讨了在开发 PDC 驱动之前应该了解的 Linux 平台驱动框架。后续章节将探索 PDC 驱动的功能划分、驱动的活动流以及示例 PDC 驱动的实现。

# 引导基础要素：平台驱动

USB 设备控制器硬件使用私有接口连接到平台。以最小复杂性开发设备驱动非常重要。Linux 平台驱动是一种伪总线通用驱动模型，通过简单的驱动框架连接到私有接口。平台驱动框架提供了直接访问平台硬件总线的权限。大部分 USB PDC 驱动都是基于平台驱动框架开发的。以下章节将探索平台驱动框架的基础，使能够理解并开发 USB PDC 驱动。

`linux/platform_device.h` 文件包含了平台驱动框架的定义和声明。平台驱动通过两个主要数据结构导出其功能：`struct platform_device` 和 `struct platform_driver`。

`platform_device` 数据结构表示设备，包含用于识别设备的成员以及表示分配给设备的资源集（如 IRQ 和内存）的字段。`Name` 字段有助于在探测成功识别分配的资源。

```
struct platform_device {
    const char *name;
    int id;
    struct device dev;
    u32 num_resources;
    struct resource * resource;
};
```

# 引导基础要素：平台驱动

通常，`struct platform_device` 作为模块初始化的一部分被安装，并注册到平台驱动框架上。平台驱动框架通过 `probe` 方法将带有分配资源的 `struct platform_device` 对象传递给驱动，此时资源被重映射到设备驱动数据结构中。

下一个关键数据结构是 `struct platform_driver`。它类似于标准的 Linux 驱动模型，提供了识别和管理设备的方法。你必须为设备注册处理程序，以处理来自平台驱动框架的调用。在这些处理程序中，`probe` 和 `remove` 方法是设备驱动运行所特定的。

```
struct platform_driver {
    int (*probe)(struct platform_device);
    int (*remove)(struct platform_device);
    void (*shutdown)(struct platform_device);
    int (*suspend)(struct platform_device, pm_message state);
    int (*resume)(struct platform_device);
    struct device;
};
```

在成功初始化平台驱动后，必须使用 `platform_driver_register` 方法。该方法与设备连接类似。

```
int platform_driver_register(struct platform_driver *);
```

当资源被命名时，可以通过名称检索它。`platform_get_resource_byname` 和 `platform_get_irq_byname` 允许通过名称获取。

```
int platform_driver_probe(struct platform_device *dev, const char *)
```

# 注意

使用 `platform_driver_probe` 减少运行时占用。此外，如果注册了设备。

# 第 12 章 = 外设控制器驱动

当你编写设备驱动时，清理和释放资源是设备驱动的一部分。可以使用平台框架的 `platform_device_unregister` 方法来清理并释放。

```
void platform_device_unregister(struct platform_device *);
```

一旦成功探测设备，设备驱动必须获取分配的资源。平台框架提供了 `platform_get_resource` 接口来检索资源。这里可以检索的资源类型有：

```
#define IRESOURCE_TYPE_BITS      0x0000F00   /* 资源类型 */
#define IRESOURCE_IO_10         0x0000100
#define IRESOURCE_MEM           0x0000200
#define IRESOURCE_IRQ          0x0000400
#define IRESOURCE_DMA          0x0000800
```

```
struct resource *platform_get_resource(struct platform_device *, unsigned int type, const char *)
struct resource *platform_get_resource_byname(struct platform_device *, unnsigned int, const char *)
```

成功时，该方法返回分配给设备的资源；如果失败，则返回负错误码。平台框架还提供了获取分配给设备的 IRQ 的程序。

```
int platform_get_irq(struct platform_device *dev, unsigned int num)
int platform_get_irq_byname(struct platform_device *dev, const char *name)
```

PDC 与硬件紧密相关；请求 IRQ 和安装中断处理程序是驱动层的重要部分。Linux 驱动框架提供了在 `<linux/interrupt.h>` 中声明的 `request_irq` 接口函数用于安装中断处理程序。在安装成功时返回 0，失败时返回负错误代码。当设备不再被使用时，应让其他驱动可用。你必须使用 `free_irq` 释放设备共享的 IRQ。

