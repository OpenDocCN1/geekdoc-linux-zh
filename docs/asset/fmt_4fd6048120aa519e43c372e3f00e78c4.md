
# MT6573 Linux 设备模型客户文档

## 文档修订历史

| 版本 | 日期 | 作者 | 描述 |
| :--- | :--- | :--- | :--- |
| 0.1 | 2010-01-21 | CC Hwang | 初始草 |

## 图表列表

# 1 引言

## 1.1 软件环境

本文讨论的驱动程序基于 `Linux Kernel 2.6.35` 和 `Android 2.3`。

## 1.2 功能性

通过阅读本文，你可以了解如何向 Linux 模型注册新的设备驱动程序，以及如何控制模块初始化序列以确保程序的正常运行。

# 2 架构

## 2.1 架构

从 BSP 的角度来看，整个系统由三部分组成：总线、驱动程序和设备，如下所示。

![](img/fde35a0d174d3624cc9d9b30b2222353_4_0.png)

Linux 中有多种总线，例如 `USB` 和 `I2C`。对于每条总线，可能有多个设备和驱动程序连接上面。驱动程序满足匹配设备的需求，使 Linux 能够正确在设备上运行。匹配过程发生在驱动程序或设备注册到总线时，这将在后文中解释。

## 2.2 设备/驱动匹配流程

当设备或驱动程序注册到指定的总线时，就会发生设备/驱动匹配流程。当一个设备注册到总线时，将扫描总线上的所有驱动程序，以检查是否有匹配的驱动程序可以为新设备的服务，反之亦然。

对于每条总线，都有一个关联的匹配函数。该匹配函数将用于第一步扫描所有设备/驱动程序。不同总线的匹配规则，取决于设备/驱动程序的名称或属性。如果找到了匹配的设备/驱动程序，将使用驱动程序的探测（`probe`）函数来验证指定的设备硬件确实存在，并检查是否可以从系统中获取所需的资源，以便驱动程序能够处理设备属性。之后，驱动程序就可以开始服务设备。

![](img/fde35a0d174d3624cc9d9b30b2222353_5_0.png)

# 3 平台总线

平台总线是 Linux 中的一种伪总线，用于以最少的基础设施连接总线上的设备，例如用于许多系统上芯片处理器上集成外围设备，它被广泛应用于 Mediate 提供的 Linux 软件包中。平台总线的匹配函数通过名称匹配设备和驱动程序。

## 3.1 平台设备

平台设备是指作为独立实体出现在系统的设备，例如集成到系统上芯片平台中的控制器。

```
struct platform_device {
    const char *name;
    u32 id;
    struct device *dev;
    u32 num_resources;
    struct resource *resource;
};
```

平台设备持有指向资源数组的指针，并可能包含资源数组中的元素数量。资源可以是一个 `IRQ` 线、一段内存等。有时，平台设备的字段可能不足以进行设备初始化。在这种情况下，`dev` 字段中的 `platform_data` 是足够的设备信息载体的良好选择。以下是一个示例：

```
struct platform_device android_usb_device = {
    .name = "android_usb",
    .id = -1,
    .dev = {
        platform_data = &android_usb_pdata,
    }
};
```

```
struct android_usb_platform_data android_usb_data = {
    .vendor_id = 0x0bb4,
    .product_id = 0x0001,
    .product_name = "Android Phone",
    .manufacturer_name = "MediaTek",
    .serial_number = "MT123456789",
};
```

所示，任意类型的平台数据（`platform data`）可用于将设备信息附加到平台设备。

```
struct android_usb_platform_data {
    /* USB 设备描述符字段*/
    __u16 vendor_id;
    /* 默认产品 ID. */
    __u16 product_id;
    /* 当启用 adb 的产品 ID. */
    __u16 adb_product_id;
    __u16 version;
    char *product_name;
    char *manufacturer_name;
    char *serial_number;
    /* 质存储功能的 LUN 数量 */
    int nlnuns;
};
```

另一个例子是 `UART`，它演示了资源的使用。

```
static struct resource mt6573_resource_uart1[] = {
    {.start = UART1_BASE,
     .end = MT6573_BASE + MT6573_UART_SIZE - 1,
     .flags = IORESOURCE_MEM},
    {.start = MT6573_UART1_IRQ_LINE,
     .flags = IORESOURCE_IRQ},
};
```

```
static struct platform_device mt6573_device_uart[] = {
    .name = "mt6573-uart",
    .id = 0,
    .num_resources = ARRAY_SIZE(mt6573_resource_uart1),
    .resource = mt6573_resource_uart1,
};
```

如 `UART` 示例所示，资源分为两类：内存和 `IRQ` 线，表示模块所使用的内存区域和 `IRQ` 线。还要注意，`id` 字段表示设备实例，如果不使用设备实例则为 `-1`。

在分配相关资源和平台数据后，通过以下操作将平台设备注册到总线：

```
int platform_device_register(struct platform_device *pdev);
int platform_add_devices(struct platform_device **pdevs, int ndev);
```

## 3.2 平台驱动程序

平台驱动程序遵循标准的模型约定，其中许多是相同的。

```
struct platform_driver {
    int (*probe)(struct platform_device *);
    int (*remove)(struct platform_device *);
    void (*shutdown)(struct platform_device *);
    int (*suspend_late)(struct platform_device *, struct pm_message_t state);
    int (*suspend_early_late)(struct platform_device *, struct pm_message_t state);
    int (*resume_early)(struct platform_device *);
    int (*resume)(struct platform_device *);
    struct device_driver;
};
```

当设备/驱动程序注册到总线并发现匹配项时，探测（`probe`）函数用于验证设备硬件的存在。使用以下命令注册平台驱动程序：

```
int platform_driver_register(struct platform_driver * drv);
```

# 4 模块初始化序列

事实上，设备/驱动在探测（`probing`）后可以正常工作，模块初始化序列强调的是探测函数被调用的顺序，而不是模块初始化函数本身。

在 `ALPS` 的设计中，驱动注册是在驱动模块初始化函数中完成的，这些分布在所有设备驱动中；而所有的设备注册都放在一个共同的地方，即 `alps/mediatek/platform/mt6573/kernel/core/mt6573_devs.c` 中的 `mt6573_board_init`，用于控制系统中所有平台设备/驱动的探测序列。

基于前章节建立的基础知识，很清楚，当设备和驱动之间找到匹配时，探测函数将被调用。可以认为，`mt6573_board_init` 在 `mt6573_board_init` 被调用之前已经注册。并且探测序列将由设备注册序列控制。另外请注意，为了“减少占用”，初始化后不再需要的数据应该放在模块初始化函数中，而不是探测函数中。只有运行时需要的数据才应该放在探测函数中。

|  |  |
|---|---|
| Device1 |  |
| `platform_device_register(device1)` | `probe (driver1)` |
| Device2 |  |
| `platform_device_register(device2)` | `probe (driver2)` |
| Device3 |  |
| `platform_device_register(device3)` | `probe (driver3)` |

若要推迟驱动探测，可以通过推迟设备注册或驱动注册来实现。
