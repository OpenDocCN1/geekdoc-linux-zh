

# 摘要

电源管理对于嵌入式系统至关重要，特别是对于电池供电设备。本章开头探讨了 Linux电源管理框架的数据结构，这些结构对于理解 Linux USB电源管理框架非常重要，随后介绍了 Linux USB 主机电源管理框架的细节。本章以从用户空间配置 Linux USB 主机电源管理的细节结束。下一章将探讨集线器系统的软件需求及其实现。

# 扩展阅读

USB 规范定义了 USB 系统的电源管理要求。你需要理解 Linux 内核的电源管理框架；Documentation/power/*.txt 进一步的见解。此外，Documentation/usb/power-management.txt 和 Documentation/usb/persist.txt 提供了有关 Linux USB电源管理框架的信息。

# 第 8 章

# 集线器 (Hub)

本章内容

- 基础知识：Linux USB 集线器
- Linux USB 集线器框架

通用串行总线（USB）标准支持主机连接 127 个物理设备。但典型的主机计算机支持的端口数量有限，因此只能连接少数设备。USB 规范定义了一种被称为*集线器设备*（hub device）的模型，允许主机扩展其端口并连接多个设备。USB 集线器控制器与根集线器集成，以提供一个或多个连接点。图 8.1 展示了典型的根集线器、集线器和设备之间的关系。

Linux USB 框架作为 `usb` 模块的一部分支持 USB 集线器，并为主控制器提供虚拟根集线器框架。Linux 集线器框架提供了 USB 2.0 规范第 11 章“USB 规范”所需的功能，例如集线器事件和变更请求。该框架在枚举过程中也起着作用，并在设置地址、连接/断开、重置以及 Linux USB 集线器的对等（OTG）功能和电源管理中发挥作用。

接下来的章节将探讨 Linux USB 集线器框架所需的关键数据结构。随后将介绍集线器框架与其他 Linux USB 主机框架子系统的功能和活动序列。

# 第 8 章 = 集线器

![](img/779a74a6577501a55983f193067274a3_118_0.png)

**图 8.1** 物理层面的主机、集线器和设备关系。（参考 USB 2.0 规范图 5-5）

# 基础知识：Linux USB 集线器

集线器提供了 USB 设备与 USB 主机之间必要的电气接口。Linux USB 框架提供了集线器功能；框架的关键数据结构位于 drivers/usb/core/hub.h。数据结构 `struct usb_hub_descriptor`、`struct usb_tt` 管理与线器相关的事务，而 drivers/usb/core/hub.c 中的 `struct usb_hub` 用于内部信息。

集线器描述符衍生自 USB 规范第 9 章定义的通用 USB 设备框架描述符。集线器描述符定义在 USB 规范第 11 章。它们定义了集线器设备的特征以及集线器支持的端口数量。

USB 规范表 11-13 详细描述了 USB 集线器描述符。在 drivers/usb/core/hub.h 中定义的数据结构 `struct usb_hub_descriptor` 包含了这些关于集线器描述符的信息。

```c
struct usb_hub_descriptor {
    u8 bDescriptorLength;
    u8 bDescriptorType;
```

# 基础知识：Linux 集线器

bNbrPorts 成员包含有关集线器支持的下游端口数量的信息。

```c
__u8 bNbrPorts;
__u16 wHubCharacteristics;
__u8 bPwOn2PwrGode;
__u8 bHubContCurrent;
```

DeviceRemovable 成员变量指示端口是否连接了可插拔设备。Linux USB 框架在 include/usb.h 中定义了 USB_MAXCHILDREN。Linux USB 框架支持 31 个设备。

```c
__u8 DeviceRemovable[(USB_MAXCHILDREN + 1) / 8];
__u8 PortPwrMask[(USB_MAXCHILDREN + 1) / 8];
__attribute__((packed));
```

集线器在高速模式下运行时负责管理全速/低速设备；集线器的事务转换器（TT）部分执行此功能。该数据结构仅对集线器框架中的集线器可见。

```c
struct tt {
    struct usb_device *hub;
    int think_time;
    spinlock_t lock;
    struct list_head clear_list;
    struct work_struct clear_work;
};
```

Linux 集线器框架使用数据结构处理事件。图 8.2 展示了事件和变更信息。core/hub.c 中定义的 `struct usb_hub` 管理这些信息。

# 第 8 章 = 集线器

![](img/779a74a6577501a55983f193067274a3_120_0.png)

```c
struct usb_hub {
    list_head event_list;
    unsigned long event_bits;
    unsigned long change_bits;
    unsigned long busy_bits;
    unsigned long removed_bits;
    struct usb_hub_descriptor *descriptor;
    struct tt tt;
};
```

**图 8.2** 集线器事件与系统软件的关系。（参考 USB 2.0 规范图 11-20）

在涵盖了集线器的基础数据结构后，接下来的部分将探讨集线器框架的关键接口函数。

- void usb_set_device_state(struct usb_device *udev, enum usb_device_state new_state)

此接口函数允许 usbcore 和主机控制器驱动程序（HCD）将设备的当前状态更改为指定状态。函数接收新状态以及应用该状态的设备指针。设备切换到 USB_STATE_NOTATTACHED 时，必须在锁保护下执行状态更改。其他框架不应直接设置状态，而应该使用此接口函数。

- int usb_hub_clear_tt_buffer(struct urb *urb)

此接口函数用于清除高速集线器中的控制/批量 TT 状态。高速主机控制器通知集线器驱动程序某些分割（split）事务失败，需要清除事务转换器的内部状态。此接口函数在中断上下文中。

- int usb_reset_device(struct usb_device *udev)

此接口函数在通知注册的接口驱动程序后重置 USB 设备。函数执行端口重置，重新分配设备地址并设置配置。当重置后描述符发生变化时，集线器框架收到的通知就像设备已断开并重新连接一样。内部，usb_reset_and_verify_device 执行 USB 端口重置以重新初始化设备。

- void usb_queue_reset_device(struct usb_interface *iface)

此接口函数在原子上下文中重置 USB 设备。通过此方法的重置会被延迟到工作队列，但功能等同于调用 usb_reset_device。

## Linux USB 集线器框架

Linux USB 集线器框架是 uscore 模块的一部分，实现在文件 drivers/usb/core/hub.c 中。部分集线器协议和驱动数据结构定义在 drivers/usb/core/hub.h 中，部分主机控制器驱动程序可见。集线器框架实现了一个集线器守护进程，即内核线程 khud，负责处理集线器事件。uscore 集线器框架包含四项功能，如图 8.3 所示。

