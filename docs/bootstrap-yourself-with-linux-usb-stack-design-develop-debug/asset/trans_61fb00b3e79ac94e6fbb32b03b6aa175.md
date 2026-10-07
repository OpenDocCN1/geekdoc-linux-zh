

# 第 6 章 = 设备文件系统

```c
NULL, &ubsfs_devices_fops,
listuid, listgid;
```

```c
--cut--
}
```
```c
static const struct file_operations ubsfs_devices_fops = {
    llseek = usb_device_lseek,
    read = usb_device_read,
    poll = usb_device_poll,
};
```

在成功创建文件后，你定义定义文件操作以提供对文件的访问。`drivers/usb/core/devices.c` 文件实现了设备文件所需的的文件操作回调。

Linux 设备文件是只读的。`read` 回调将文件中的信息转储到用户空间。你可以阅读第 16 章“USB 虚拟文件系统”，以了解更多关于设备的内容以及如何使用文件信息。

# 总结

Linux 设备驱动使用 Linux 内核的 VFS 基础设施将对设备的控制扩展到用户空间。Linux USB 子系统的 VFS 文件导出了关于设备的信息，并允许你从用户空间开发应用程序。下一章将探索 Linux 主机子系统的 USB 电源管理框架及其用法。

# 更多阅读

本章简要涵盖了 Linux VFS。你可以在内核包的 `Documentation/filesystems/vfs.txt` 中阅读更多关于 Linux VFS 框架的内容。此外，你可以阅读第 16 章学习如何使用 ubsfs 文件。此外，`Documentation/usb/proc_usb_info.txt` 解析了如何在用户空间使用 USB 文件系统。

# 第 7 章

# 电源管理

本章内容：

- 启动基础：电源管理
- Linux USB 电源管理
- 设置 Linux-USB 电源管理

电源管理是任何嵌入系统的关键需求之一。USB 规范为通用串行总（USB）设备和 USB 主机定义了电源管理方法。USB 设备通过进入全局或接口层面的挂起模式来节省能量。挂起发生在没有总线活动时，有时取决于设备类的实现。要恢复挂起的主机，USB 设备可以使用远程唤醒（remote wakeup）。并不是所有设备都支持远程唤醒；该功能通过配置描述符传递给主机。

USB 主机电源管理很大取决于主机系统软件（Microsoft Windows 和 Linux）的电源管理框架。Linux 内核实现了必要的电源管理框架，使外设子系统作为 Linux USB 系统能够有效管理电源。本章从 Linux 电源管理的快速启动开始，随后探索 Linux USB 主机子系统的电源管理内部机制和活动序列，最后提供其用的实操环节。

# 启动基础：电源管理

Linux 电源管理有两种电源管理模型：系统睡眠模型和运行时电源管理模型。在系统睡眠模型中，整个系统通过与各种总线、设备或类驱动程序交互进入低功耗模型。系统运行时，单个驱动程序也可以进入节能模式，这被称为运行时电源管理。

电源管理发生在不同的阶段，每个阶段都有在启动下一阶段之前执行的回调函数。这些阶段涉及总线、设备和类驱动程序回调（dev->bus->pm, dev->type->pm, dev->class->pm）。在挂起操作期间，回调按以下顺序调用：类、设备，然后总线。在恢复期间，回调顺序反转，变为总线、设备，然后类。下节将探索这些电源管理操作和实用函数，这些对于后续理解 Linux USB 至关重要。

第一个注册电源管理回调的重要数据结构是 `struct dev_pm_ops`，它定义在内核源码包的 `include/linux/pm.h` 中。实现电源管理的驱动程序使用这个数据结构。

# 注意

并不强制要求实现每一个回调。

```c
struct dev_pm_ops {
    int (*prepare)(struct device *dev);
    void (*complete)(struct device *dev);
    int (*suspend)(struct device *dev);
    int (*resume)(struct device *dev);
    int (*freeze)(struct device *dev);
    int (*thaw)(struct device *dev);
    int (*poweroff)(struct device *dev);
    int (*restore)(struct device *dev);
    int (*suspend_noirq)(struct device *dev);
    int (*resume_noirq)(struct device *dev);
    int (*freeze_noirq)(struct device *dev);
    int (*thaw_noirq)(struct device *dev);
    int (*poweroff)(struct device *dev);
    int (*restore)(struct device *dev);
};
```

# 启动基础：电源管理

```c
struct dev_pm_ops {
    int (*suspend)(struct device *dev);
    int (*resume)(struct device *dev);
    int (*idle)(struct device *dev);
};
```

`struct dev_pm_ops` 也包含了运行时电源管理。

# 注意

新的电源管理框架仅在 2.6.32 中引入。

- int (*suspend)(struct device *dev)
`runtime_suspend` 回调将设备带入低功耗模式以停止系统通信。这仅对激活设备执行。

- int (*resume)(struct device *dev)
`runtime_resume` 回调将设备恢复到正常状态。这仅对已挂起的设备执行。

- int (*idle)(struct device *dev)
`runtime_idle` 回调将空闲设备设置为低功耗模式以停止与系统通信。

电源管理框架还定义了与设备管理的接口函数。这些接口函数定义在 `include/linux/pm.h` 中，并从 `drivers/base/power.c` 导出。这里列出了电源管理的一些接口函数。

- int runtime_suspend(struct device *dev)
`runtime_suspend` 方法通过调用 `runtime_suspend` 回调来挂起传入的设备。成功时返回 0，返回 `-EBUSY` 等相应的错误码。

- int runtime_resume(struct device *dev)
`runtime_resume` 方法通过调用 `runtime_resume` 回调来恢复传入的设备。成功时返回 0，返回 `-EAGAIN` 等错误码。

- int runtime_idle(struct device *dev)
`runtime_idle` 方法通过调用 `runtime_idle` 回调通知挂起设备。成功时返回 0，返回 `-EINPROGRESS` 等错误码。

- void runtime_enable(struct device *dev)
当设备启动时，所有设备的运行时电源管理都是禁用的。`runtime_enable` 方法通过减少电源管理信息数据结构中的 `disable_depth` 字段启用设备的运行时电源管理。

- void runtime_disable(struct device *dev)
`runtime_disable` 方法禁用设备的运行时电源管理并取消所有待处理的电源操作。内部，该方法增加电源管理信息 `disable_depth` 字段以记录禁用调用。

- int runtime_set_active(struct device *dev)
`runtime_set_active` 方法将设备及其子设备的状态设置为电源管理激活状态。当设备信息的运行时错误和禁用深度字段不为 0，或者父设备未激活且设置了 `Ignore Children` 字段时，该方法将失败。在这种情况下，方法返回相应的错误码，如 `-EAGAIN` 或 `-EBUSY`。

