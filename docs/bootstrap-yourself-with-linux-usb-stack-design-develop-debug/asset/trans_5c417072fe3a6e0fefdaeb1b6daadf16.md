

# Bootstrap 基础：电源管理

```c
struct dev_pm_message_t {
    int power_state;
    unsigned int;
    unsigned int;
    unsigned long;
    enum dpm_state;
#ifdef CONFIG_PM_SLEEP
    struct list_head;
    struct completion;
    unsigned long;
#endif
#ifdef CONFIG_PM_RUNTIME
    struct timer_list;
    unsigned long;
    struct work_struct;
    wait_queue_head_t;
    spinlock_t;
    atomic_t;
    atomic_t;
    unsigned int;
    unsigned int;
    unsigned int;
    unsigned int;
    unsigned int;
    unsigned int;
    enum rpm_request;
    enum rpm_status;
    int;
    unsigned long;
    unsigned long;
    unsigned long;
#endif
    can_wakeup:1;
    should_wakeup:1;
    async_suspend:1;
    status: /* 由 PM 核心拥有 */
    entry:
    completion;
    wakeup_count;
    suspend_timer;
    timer_expires;
    wait_queue;
    usage_count;
    child_count;
    disisable_depth:3;
    ignore_children:1;
    idle_notification:1;
    request_pending:1;
    deferred_resume:1;
    run_wake:1;
    untime_auto:1;
    request;
    untime_status;
    untime_error;
    active_jiffies;
    suspended_jiffies;
    accounting_timestamp;
};
```

该数据结构还维护了电源核心所需的设备电源管理状态，包括设备电源管理和设备运行时电源管理。这些状态定义在 include/linux/pm.h 文件中。

```c
enum dpm_state {
  DPM_INVALID,
  DPM_ON,
  DPM_PREPARING,
  DPM_RESUMING,
  DPM_SUSPENDING,
  DPM_OFF,
  DPM_OFF_IRQ;
};
```

```c
enum rpm_status {
  RPM_ACTIVE = 0,
  RPM_RESUMING,
  RPM_SUSPENDED,
  RPM_SUSPENDING;
};
```

本节探讨了在使用框架时需要的一些关键电源管理框架数据结构。下一节将探讨 Linux USB 主机电源管理的关键电源管理函数，以及 Linux USB 电源管理框架的活动图。

# Linux USB 电源管理

Linux-USB 电源管理框架是 usbcore 功能的一部分。它的功能是处理 Linux USB 主机框架内的低功耗状态。你可以在 <linux/usb.h> 中找到电源管理框架的数据结构定义，功能实现分布在 <./drivers/usb/core/hcd.c>、<./drivers/usb/core/driver.c>、<./drivers/usb/core/usb.c>、<./drivers/usb/generic.c> 和 <./drivers/usb/core/hub.c> 模块中。只有当 CONFIG_USB_SUSPEND、CONFIG_PM_RUNTIME 和 CONFIG_SUSPEND 是配置的一部分时，usbcore 才能使用该电源管理框架。

图 7.1 展示了 Linux USB 主机电源管理框架的简单自上而下分解。你可以直观地看到框架由 USB 特有的电源管理例程和 Linux 特有的电源管理例程组成。

# Linux USB 电源管理

![](img/779a74a6577501a55983f193067274a3_107_0.png)

**图 7.1**
USB 主机电源管理的自上而下分解。

USB 特有的电源管理例程处理 USB 请求，例如电源管理特定的 USB 控制传输以及主机和集线器特定的请求。USB 主机电源管理还向 Linux 电源管理框架注册回调，以处理系统特定的电源管理事件，例如系统低功耗挂起模式。后续章节将探索 USB主机电源管理框架的关键 USB 数据结构、API 和活动序列。

USB 电源管理框架定义了基于 `struct dev_pm_ops` 的对象 `struct usb_device_pm_ops`，用于向电源管理核心注册回调。Linux 电源管理核心使用这些回调来控制 USB 框架。

```c
static struct dev_pm_ops usb_bus_pm_ops = {
    .runtime_suspend = usb_runtime_suspend,
    .runtime_resume = usb_runtime_resume,
    .runtime_idle = usb_runtime_idle,
};
static const struct dev_pm_ops usb_device_pm_ops = {
    .prepare = usb_dev_prepare,
    .complete = usb_dev_complete,
    .suspend = usb_dev_suspend,
    .resume = usb_dev_resume
    .freeze = usb_dev_freeze,
    .thaw = usb_dev_thaw,
    .poweroff = usb_dev_poweroff,
    .restore = usb_dev_restore;
};
```

USB 电源管理框架支持空闲设备的自动挂起和恢复。为了让另一个主机框架使用此功能，Linux USB 主机电源管理框架导出接口。这些例程允许其他 USB 模块向 usbcore 通信挂起和恢复请求。

- `int usb_enable_autosuspend(struct usb_device *udev)`
`usb_enable_autosuspend` 接口为 USB 设备启用电源管理。它通过将 `autosuspend_disabled` 标志设置为 0 来启用自动挂起。当设备变为空闲且自动挂起延迟超时时，将挂起。

- `int usb_disable_autosuspend(struct usb_device *udev)`
`usb_disable_autosuspend` 例程通过将 `autosuspend_disabled` 标志的值设置为 true，防止 USB 设备进入低功耗挂起模式。

- `int usb_autopm_get_interface(struct usb_interface *intf)`
- `int usb_autopm_get_interface_async(struct usb_interface *intf)`
这两个接口例程都会增加电源管理的使用计数器，并在设备处于挂起状态时执行自动恢复。这两个接口例程的主要区别是，异步方法可以在原子上下文中运行。

- `void usb_autopm_put_interface(struct usb_interface *intf)`
- `void usb_autopm_put_interface_async(struct usb_interface *intf)`
`_put` 例程减少设备的电源管理使用计数器，如果计数器为 0，则尝试自动挂起设备。与之前的同步例程一样，你可以在原子上下文中执行此同步例程。

- `int usb_autopm_get_interface_no_resume(struct usb_interface *intf)`
- `int usb_autopm_put_interface_no_suspend(struct usb_interface *intf)`

`no_resume` 和 `no_suspend` 接口例程增加设备电源管理的使用计数器。你可以在原子上下文中执行这些例程。

除了这些接口例程，自动挂起和自动恢复框架由模块参数控制。你可以从用户空间修改这些模块参数来控制电源管理。后续章节将探讨自动挂起和自动恢复的活动序列，以及控制器的电源管理。

图 7.2 展示了 USB 运行时电源管理的抽象活动。电源管理从向电源管理核心注册回调开始。注册成功后，Linux USB 框架使用接口 `pm_runtime_set_active` 和电源管理启用功能来激活运行时框架。

| USB Device | Hub Driver | Generic usbcore | USB Host Power Management | PM Core | USB sysfs | Class Driver |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | | USB Power Management | | | |
| | | | Register dev_pm_ops | | | |
| | | | usb_probe_interface, usb_driver claim_interface | | | |
| | | | pm_runtime_set_active | | | |
| | | | struct device | | | |
| | | | pm_runtime_enable | | | |
| | | | struct device | | | |
| | | | usb_autosuspend_device | | | |

**图 7.2**
USB 运行时电源管理的初始化序列。

![](img/779a74a6577501a55983f193067274a3_109_0.png)

# 第 7 章 电源管理

| USB Device | Hub Driver | Generic uscore | USB Power Management | PM Core | USB sysfs | Class Driver | User Space |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

![](img/779a74a6577501a55983f193067274a3_110_0.png)

图 7.3
设备运行时挂起期间的活动序列。

一旦自动电源管理框架注册并正确设置，你就可以通过写入必要的文件从用户空间管理该框架。两个主要文件 `power/autosuspend` 和 `power/level` 对于挂起和恢复 USB 设备是必要的。图 7.3 展示了活动序列，


