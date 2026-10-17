
```c
drivers/base/bus.c
kobj_set_name(&bus->devices.kobj, "devices")
bus->devices.parent = &bus->subystems;
retval = kset_register(&bus->devices);

kobj_set_name(&bus->drivers.kobj, "drivers")
bus->drivers.parent = &bus->subystems;
bus->drivers.type = &driver_type;
retval = kset_register(&bus->drivers);
```

## 设备注册

注册设备包含两个独立步骤，如图 6-22 所示：初始化设备的数据结构，将其引入设备网络。

![图 6-22：device_register 代码流程](https://example.com/a80e0e530e25bf9e2dff130fff42a_485.png)

`device_initialize` 主要通过 `kobj_set(dev, dev_subsys)` 将新设备添加到设备子系统中。

`device_add` 需要稍多努力。首先，通过 `dev->parent` 指定的父子关系被带到通用对象层级中：

```c
drivers/base/core.c
int device_add(struct device *dev)
{
    struct device *parent = NULL;
    ...
    parent = get_device(dev->parent);
    kobj_parent = get_device_parent(dev);
    dev->parent = kobj_parent;
    ......
}
```

在设备子系统中注册设备只需要调用 `kobj_add`，因为子系统成员已经在 `device_initialize` 中设置过。

```c
drivers/base/core.c
kobj_set_name(&dev->kobj, "%*s", dev->bus_id);
error = device_add(&dev->kobj);
```

之后，`bus_add_device` 在 sysfs 中添加链接——一个在总线上指向设备，另一个目录中指向子系统。`bus_attach` 尝试自动探测设备。如果找到匹配的驱动程序，设备将被添加到 `bus->klist_devices` 中。设备也会添加到父级的子列表中，即设备知道其父级，但父级并不知道该设备。

```c
drivers/base/core.c
error = bus_add_device(dev);
bus_attach_device(dev);
if (klist_add_tail(&dev)->node_parent, &parent->klist_children))
}
```

# 第 6 章：设备驱动

## 注册驱动程序

在执行了一些性检查和初始化工作后，`driver_register` 会调用 `bus_add_driver` 将新驱动程序添加到总线上。驱动程序首先被赋予一个名称，然后注册到通用数据结构框架中。

```c
drivers/base/bus.c
int bus_add_driver(struct device_driver *drv)
{
	struct bus *bus = bus_get(drv->bus);
	int error = 0;

	error = kobject_set_name(&drv->kobj, "%s", drv->name);
	drv->kobj.kset = &bus->drivers;
	error = kobject_register(&drv->kobj);
}
```

如果总线支持自动探测（autoprobe），`driver_attach` 会遍历总线上的所有设备，并通过驱动程序的 `match` 函数检查该驱动程序是否负责其中任何设备。最后，该驱动程序被添加到总线注册的所有驱动程序列表中。

```c
drivers/base/bus.c
if (drv->bus->drivers_autoprobe)
	error = driver_attach(drv);
klist_add(&drv->node_bus, &bus->klist_drivers);
```

## 6.7.2 PCI 总线

PCI 是外设相互连接（peripheral interconnect）的缩写，是由英特尔开发的一种标准总线。它迅速在组件制造商和架构供应商中成为一种非常流行的总线，这并不是由于巧妙的营销策略，而是基于其技术优势。它的设计目的是为了对抗影响（编程）世界最糟糕的疾病之一——ISA 总线。制定以下目标是为了弥补 ISA 总线设计的固有缺陷，并实现：

- 支持对具有大数据流的多媒体应用进行高带宽传输。
- 对连接的外围设备进行简单且易于自动配置。
- 平台无关性；即不依赖于特定的处理器类型或系统平台。

PCI 规范存在多个版本，随着最新技术的发展，不断增加了新的功能——例如，最近的重大“更新”之一是支持热插拔（即在总线运行时添加和移除设备）。

> ISA 代表标准架构总线（standard architecture bus）。该总线是由一个大型硬件供应商协会开发的，以响应 IBM 希望通过保护专利和专有的微通道（microchannel）来支持设备制造。ISA 总线系统是一种非常简单的设计，便于扩展卡的使用；事实上，它简单到让业余爱好者在总线编程和驱动程序寻址方面存在严重缺陷，这是由于当时完全不同的计算机技术解决方案，部分由于总线设计，这种设计绝不能被认为是具有前瞻性的。

由于 PCI 规范的处理器无关性，该总线不仅用于 IA-32 系统（以及它们或或少的继承者 IA-64 和 AMD64），还用于其他当代架构，如 PowerPC、Alpha 或 SPARC——这是为了享受为该总线生产的廉价扩展卡所带来的收益。

### PCI 系统布局

在讨论内核中如何实现 PCI 之前，让我们检查该总线基础的主要原理。需要更详细描述的读者请参阅许多硬件技术教科书（例如，[BH01]）。

### 设备识别

系统任一 PCI 总线上的每个设备都通过一组三个数字来标识。

- 线号（bus number）是设备所在总线的编号；通常从 0 开始编号。PCI 规范允许每个系统最多有 255 条总线。
- 设备号（device number）是总线内的唯一标识符。总线上最多可以连接 32 个设备。不同总线上的设备具有相同的设备号。
- 功能号（function number）用于识别单块插卡上具有多个（经典意义上的）扩展设备的设备。例如，出于空间考虑，两个网卡可以安装在一块插卡上，其中不同的接口由不同的功能号指定。笔记本电脑中使用多功能芯片，它们连接到 PCI 并在最小的空间内集成了广泛的扩展（IDE 控制器、USB 控制器、调制解调器、网络等）；这些扩展必须通过功能号隔开。PCI 标准定义一个设备上的最大功能单元数量为八个。

每个设备都通过一个 16 位数字唯一标识，其中 8 位留给线号，5 位留给设备号，3 位留给功能号。驱动程序无需担心这个紧凑的数据结构网络，它包含了相同的信息，但从 C 语言的角度来看更容易处理。

### 地址空间

三个地址空间支持与 PCI 设备进行通信。

- I/O 空间由 32 位描述，因此为与设备通信的端口地址提供了最大 4 GB 的空间。
- 取决于处理器类型，数据空间可用 32 或 64 字节；后者在具有相应字长的 CPU 上支持。系统中的设备分布在两个内存区域中，并具有唯一的地址。
- 配置空间（configuration space）包含有关设备类型和特性的详细信息，以消除危险的探测。

地址空间根据处理器类型映射到系统虚拟内存的不同位置，以便内核和设备驱动程序访问相应的资源。

### 配置信息

与其许多前代产品相比，PCI 总线是一个无跳线器（jumper-free）系统。换句话说，扩展设备可以完全配置。扩展设备可以通过软件在无人工干预的情况下完全配置；每个设备都有一个 256 字节的配置空间，其中包含设备特殊特性和要求的信息。这些信息的结构（或应该）定义在图 6-23 中，该图展示了 PCI 要求的布局。

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |

|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

| Vendor ID | Device ID | Cmd Reg | Status | Rev | D | Class Code | Cache Line | Latency Timer | Header | BIST | | | | |

| base address 0 | | base address 1 | | base address 2 | | base address 3 | | | | | | |
