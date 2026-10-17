
设备模型涉及“device（设备）”、“driver（驱动）”和“bus（总线）”术语：

- `device`：挂载到总线的物理或虚拟对象。
- `driver`：探测并绑定设备并执行某些管理的软件实体。
- `bus`：作为其他设备连接点的设备。

设备模型围绕三个数据结构组织：

1. `bus_type` 结构，表示一种总线（例如 USB, PCI, I2C）。
2. `device_driver` 结构，表示处理特定总线上某些设备的驱动。
3. `device` 结构，表示连接到总线的设备。

# 第 2 章 Linux 设备与驱动器模型

## 总线核心驱动

内核支持的每个总线都有通用总线驱动。总线是处理器与多个设备之间的通道。对于设备模型，所有设备都通过总线连接，即使是虚拟的“platform”总线。

总线驱动分配 `bus_type` 结构并将其注册到内核的总线列表中。`bus_type` 结构（在内核源码树的 `<linux/device.h>` 中声明）表示一种总线（USB, PCI, I2C 等）。系统中总线的注册是通过使用 `bus_register()` 函数完成的。`bus_type` 结构声明如下：

```c
struct bus_type {
    const char *name;
    const char *dev_name;
    struct device *dev_root;
    struct device_attribute *dev_attrs;
    const struct attribute_group **bus_groups;
    const struct attribute_group *dev_groups;
    const struct attribute_group *drv_groups;

    int (*match)(struct device *dev, struct device_driver *drv);
    int (*uevent)(struct device *dev, struct kobj_uevent *env);
    int (*probe)(struct device *dev);
    int (*remove)(struct device *dev);
    void (*shutdown)(struct device *dev);
    int (*online)(struct device *dev);
    int (*offline)(struct device *dev);

    int (*suspend)(struct device *dev, struct pm_message_t state);
    int (*resume)(struct device *dev);

    const struct dev_pm_ops *pm_ops;

    struct iommu_ops *iommu_ops;

    struct subsys_private *p;
    struct lock_class_key lock_key;
};
```

新总线通过 `bus_register()` 注册，该函数定义在内核源码树的 `drivers/base/platform.c` 中：

```c
struct bus_type platform_bus_type = {
    .name = "platform";
    .dev_groups = platform_dev_groups,
    .match = platform_match,
    .uevent = platform_uevent,
    .pm = &platform_dev_pm_ops,
};
EXPORT_SYMBOL_GPL(platform_bus_type);
```

```c
int __init_platform_bus_init(void)
{
    int error;
    early_platform_cleanup();
    error = device_register(&platform_bus);
    if (error)
        return error;
    error = bus_register(&platform_bus_type);
    if (error)
        device_unregister(&platform_bus);
    return error;
}
```

`bus_register()` 函数将总线注册到 kobject 体系中，并创建一个 `/sys/bus/platform/` 目录，该目录包含两个子目录：`devices` 和 `drivers`。

`struct bus_type` 成员之一是一个指向 `subs_private` 结构的指针，它定义在内核源码树的 `drivers/base/base.h` 中：

```c
struct subs_private {
    struct kset kset;
    struct kset *devices_kset;
    struct list_head interfaces;
    struct mutex mutex;

    struct kset *drivers_kset;
    struct klist klist_devices;
    struct klist klist_drivers;
    struct blocking_notifier_head bus_notifier;
    unsigned int in_drivers_autoprobe:1;
    struct bus_type *bus;

    struct kset glue_dirs;
    struct class *class;
}
```

`subs_private` 结构中的 `klist_devices` 成员是系统中位于该特定类型总线上的设备列表。该列表由 `device_register()` 函数更新，当总线控制器驱动程序扫描总线上的设备时（在初始化期间或设备热插拔时），会被该函数。

`subs_private` 结构中的 `klist_drivers` 成员是能够处理该总线上设备的驱动程序列表。该列表由 `driver_register()` 函数更新，该函数在驱动程序初始化自身时被调用。

当新设备插入系统时，总线控制器驱动程序检测到该设备并调用 `device_register()`。当设备被总线控制器驱动程序注册后，设备结构的 `parent` 成员将指向总线控制器设备，以构建物理设备列表。程序将遍历与总线相关的驱动程序列表，查找是否存在可以处理该设备的驱动程序。`bus_type` 结构中提供的 `match` 函数用于检查给定驱动程序是否能处理给定设备。当找到可以处理该设备的驱动程序时，设备结构的 `driver` 成员将指向相应的设备驱动程序。

当内核模块被插入内核且驱动程序调用 `driver_register()` 时，程序将遍历与总线相关的设备列表，使用 `match` 函数查找是否有驱动程序可以处理这些设备。当找到匹配项时，该设备将与驱动程序关联，并调用驱动程序的 `probe()` 函数。这就是我们所说的“绑定（binding）”。

驱动程序何时尝试绑定设备？

- 1. 当驱动程序注册时（如果设备已经存在）。
- 2. 当设备创建时（如果驱动程序已经注册）。

总结来说，总线驱动程序在系统中注册总线：

- 1. 允许注册总线控制器驱动程序，其作用是检测设备并配置它们的资源。
- 2. 允许注册设备驱动程序。
- 3. 匹配设备和驱动程序。

### 总线控制器驱动程序

对于特定的总线类型，可能有由不同供应商提供的许多不同的总线控制器。这些控制器中的每一个都需要相应的总线控制器驱动程序。在设备模型维护中，总线控制器驱动程序的作用与其他任何设备驱动程序类似，即它使用 `driver_register()` 函数将自己注册到总线模型。在大多数情况下，这些总线控制器设备是系统的自治实体，在内核初始化调用 `of_platform_populate()` 时被发现，该函数会遍历设备树（DT），在运行时查找并将这些“平台控制器设备”注册到总线。

### 设备驱动程序

每个驱动程序都使用 `driver_register()` 向总线核心驱动程序注册自己。之后，设备模型核心会尝试将其与设备绑定。当检测到可以由特定驱动程序处理的设备时，会调用驱动程序的 `probe()` 成员，并可以从设备树中获取设备配置数据。

每个驱动程序负责为设备模型核心实例化并注册 `device_driver` 结构实例（定义在内核源码树的 `include/linux/device.h` 中）。`device_driver` 结构定义如下：
