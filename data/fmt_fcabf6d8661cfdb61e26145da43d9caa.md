
重要的数据结构是 `struct usb_device`，内核用它来表示 USB 设备。该数据结构持有 USB 设备的关键信息，包括描述符和端点细节。

`devnum` 成员变量持有分配给设备的编号。

```c
int devnum;
```

`devpath` 成员变量持有一个表示设备 ID 的字符串值。

```c
char devpath[16];
```

## 第 9 章：通用驱动

`state` 成员变量持有设备的状态信息。设备的状态使用接口函数 `usb_set_device_state` 设置。状态可以包含如 `USB_STATE_NOT_ATTACHED`、`USB_STATE_ATTACHED`、`USB_STATE_POWERED`、`USB_STATE_ADDRESS` 和 `USB_STATE_CONFIGURED` 等值。

```c
enum usb_device_state state;
```

`speed` 成员变量持有设备的速度信息。它可以包含如 `USB_SPEED_LOW`、`USB_SPEED_FULL`、`USB_SPEED_HIGH` 和 `USB_SPEED_UNKNOWN` 等值。

```c
enum usb_device_speed speed;
```

该数据结构还持有从 USB 设备检索的描述符和端点信息。

```c
struct usb_device_descriptor descriptor;
struct usb_host_config *config;
struct usb_host_config *actconfig;
struct usb_host_endpoint *ep_in[16];
struct usb_host_endpoint *ep_out[16];
```

在探索了关键基础设施数据结构后，现在查看管理这些驱动程序的接口方法。

- `int usb_register_driver(struct usb_driver *, struct module *, const char *)`
  该方法向 USB 核心注册 USB 接口驱动程序。返回状态码。
- `void usb_unregister_driver(struct usb_driver *)`
  该方法从 USB 核心注销 USB 接口驱动程序。
- `int usb_register_driver(struct usb_driver *, struct module *, const char *)`
  该方法向 USB 核心注册 USB 接口驱动程序。返回状态码。
- `void usb_unregister_driver(struct usb_driver *)`
  该方法从 USB 核心注销 USB 接口驱动程序。
- `int usb_register_dev(struct usb_interface *intf, struct usb_device_id *id)`
  该方法向 USB 核心注册 USB 设备。返回状态码。
- `void usb_unregister_dev(struct usb_interface *intf)`
  该方法从 USB 核心注销 USB 设备。

## Linux USB usbcore-generic 驱动框架

- `void usb_free_urb(struct urb *urb)`
  此方法释放事务后分配的内存。

**注意**

除非设置了 `URB_FREE_BUFFER` 传输标志，否则与 URB 关联的传输缓冲区不会被释放。

- `struct urb *usb_get_urb(struct urb *urb)`
  每当 URB 从设备驱动程序传输到主机控制器驱动程序时，此方法会增加 URB 的引用计数。
- `int usb_submit_urb(struct urb *urb, gfp_t mem_flags);`
  此方法为端点提交一个异步传输请求。URB 在中断上下文中提交。当提交成功时，返回 0；如果失败，返回一个负值。
- `int usb_unlink_urb(struct urb *urb);`
  此方法取消之前为某个端点提交的 URB。当取消 URB 成功时，将调用完成处理程序并传递一个表示请求已取消的状态码。
- `void usb_kill_urb(struct urb *urb);`
  该方法取消传输请求，并等待其完成。该方法保证所有完成处理程序均已结束，且 URB 完全处于空闲状态并可重用。

## Linux USB usbcore-generic 驱动框架

`usbcore-generic` 层提供了在 `usbcore` 模块之上实现 USB 设备驱动程序并管理设备的本质框架。它位于 `usbcore` 模块中主机控制器驱动接口（`HCI`）之上，并作为前层软件层的接口。框架源码位于 `/drivers/usb/core` 文件夹中。如 `/drivers/usb/core/urb.c`、`/drivers/usb/core/generic.c`、`/drivers/usb/core/driver.c`、`/drivers/usb/core/usb.c` 和 `/drivers/usb/core/message.c` 等文件可以视为该框架的一部分。

## 第 9 章：通用驱动

![](img/779a74a6577501a55983f193067274a3_136_0.png)

**图 9.2**
`usbcore-generic` 框架的简单分解。

图 9.2 展示了 `usbcore` 模块中 `usbcore-generic` 层的简单分解。你可以将 `usbcore-generic` 框架理解由三个重要功能组成：URB 管理、USB 设备驱动管理和 USB 设备管理。`usbcore-generic` 框架包含了管理从设备驱动程序和用户空间应用程序提交的 URB 的核心数据结构和例程。配合 hub 和主机控制器驱动（`HCD`）框架，`usbcore` 执行设备枚举，设备使用 `struct usb_device` 驱动进行管理，并使用 `struct usb_bus` 数据结构。该框架还提供了处理接口驱动需求和注册的例程。

有了 `usbcore-generic` 框架中的这些功能，你需要理解 `usbcore-generic` 框架的两个重要活动：与 `usbcore-generic` 的 USB 驱动注册，以及 URB 的生命周期和数据如何在主机的类驱动/用户应用程序与 USB 设备之间流转。

图 9.3 插示了使用 `usb_register` 接口函数与 `usbcore` 进行设备驱动程序注册的过程。

作为注册的一部分，`usbcore-generic` 更新内核设备驱动程序，包含其探测（`probe`）和断开（`disconnect`）回调方法。随后，它向内核框架注册设备驱动程序。注册成功后，注册路由将更新 USB 设备文件系统。

### Linux USB usbcore-generic 驱动框架

| 用户空间应用程序 | 内核框架 | 类驱动 | usbcore-设备文件系统 | usbcore-generic | HCD |
| --- | --- | --- | --- | --- | --- |
| | | | 当 USB 设备驱动程序注册到 usbcore 时 | | | |
| | | | `usb_register` | | | |
| | | | `struct usb_driver*` | | | |
| | | | `usb_register_driver` | | | |
| | | | `driver_register` | | | |
| | | | `struct device_driver*` | | | |
| | | | `usb_create_newid_file` | | | |
| | | | `struct usb_driver*` | | | |
| | | | `driver_create_file` | | | |
| | | | | `usb_create_removeid_file` | | | |
| | | | | `struct usb_driver*` | | | |
| | | | | `driver_create_file` | | | |

**图 9.3**
接口驱动程序注册时的活动序列。

当设备详情与 `struct usb_driver` 信息匹配时，内核框架会调用由 `usbcore-generic` 框架注册的 `usb_probe_interface` 回调方法，如图 9.4 所示。

该探测例程反过来调用 USB 驱动程序注册的回调。USB 驱动程序准备设备并与接口关联。

当设备断开或取消绑定（`unbound`）时，内核框架调用 `usbcore-generic` 框架的 `usb_unbind_interface` 方法，如图 9.5 所示。

当内核框架触发 USB 解绑定时，`usbcore-generic` 会断开接口并取消绑定。当 USB 解绑定触发时，接口数据结构设置为空闲。

## 第 9 章：通用驱动

| 用户空间应用程序 | 内核框架 | 类驱动 | usbcore-设备文件系统 | usbcore-generic | HCD |
| --- | --- | --- | --- | --- | --- |
| | | | 当设备详情与 `struct usb_driver` 信息匹配时 | | |
| | | | 内核框架调用由 usbcore-generic 框架注册的 `usb_probe_interface` 回调方法，如图9.4 所示。 | | |
| | | | 这种探测例程反过来调用 USB 驱动程序注册的回调。USB 驱动程序准备设备并与接口关联。 | | |
| | | | 当设备断开或取消绑定时，内核框架调用 usbcore-generic 框架的 `usb_unbind_interface` 方法，如图9.5 所示。 | | |
| | | | 当内核框架触发 USB 解绑定时，usbcore-generic 会断开接口并取消绑定。 | | |

**图 9.4**
探测成功时的活动序列。

| 用户空间应用程序 | 内核框架 | 类驱动 | usbcore-设备文件系统 | usbcore-generic | HCD |
| --- | --- | --- | --- | --- | --- |
| | | | 当设备详情与 `struct usb_driver` 信息匹配时 | | |
| | | | 内核框架调用由 usbcore-generic 框架注册的 `usb_probe_interface` 回调方法，如图9.4 所示。 | | |
| | | | 这种探测例程反过来调用 USB 驱动程序注册的回调。 | | |
| | | | 接口在断开或取消绑定时，内核框架调用 usbcore-generic 框架的 `usb_unbind_interface` 方法，如图9.5 所示。 | | |
| | | | | 当内核框架触发 USB 解绑定时，usbcore-generic 会断开接口并取消绑定。 | |

**图 9.5**
解绑定时的活动序列。

| 用户空间应用程序 | 内核框架 | 类驱动 | usbcore-设备文件系统 | usbcore-generic | HCD |
| --- | --- | --- | --- | --- | --- |
| | | | 当设备详情与 `struct usb_driver` 信息匹配时 | | |
| | | | | 内核框架调用由 usbcore-generic 框架注册的 `usb_probe_interface` 回调方法，如图9.4 所示。 | | |
| | | | | 这种探测例程反过来调用 USB 驱动程序注册的回调。 | | |
| | | | | 接口在断开或取消绑定时，内核框架调用 usbcore-generic 框架的 `usb_unbind_interface` 方法，如图9.5 所示。 | | |
| | | | | | 当内核框架触发 USB 解绑定时，usbcore-generic 会断开接口并取消绑定。 | | |

下一个重要活动是类驱动或用户应用程序通过设备系统提交 URB。图 9.6 插示了提交 URB。

`usbcore-generic` 框架分配 URB，用必要信息更新它，并通过 `usb_hcd_submit` 将其提交给 `HCD`。URB 根据传输类型进行更新，因为 ISO 等传输需要时间。完成后将在 `HCD` 框架中清理。

**注意**

不要在完成例程中睡眠，因为它是为硬件中断设计的。你需要在获取自旋锁的情况下尽可能少的工作。

在探索了 `usbcore` 的核心之后，本节将解释如何开发 USB 设备驱动程序并将其集成。

## 开发 USB 设备驱动程序

Linux 框架中有许多 USB 设备驱动实现。`usbbfs`、`usbtest` 和类驱动是存在的许多驱动中的突出代表。内核中还有一个骨架驱动程序 `/drivers/usb/usb-skeleton.c`。以下分析使用该骨架驱动进行开发。

USB 设备驱动开发的第一步是声明并初始化 `struct usb_driver` 回调方法，如下：

```c
static struct usb_driver skel_driver = {
    .name = "skeleton",
    .probe = skel_probe,
    .disconnect = skel_disconnect,
    .suspend = skel_suspend,
    .resume = skel_resume,
    .pre_reset = skel_pre_reset,
    .post_reset = skel_post_reset,
    .id_table = skel_table,
    .supports_autosuspend = 1
};
```

在上述的初始化中，`probe`、`disconnect` 和 `id_table` 是获取和释放设备所需的强制字段。

```c
static struct usb_device_id skel_table[] = {
    { USB_DEVICE(USB_SKEL_VENDOR_ID, USB_SKEL_PRODUCT_ID) },
    { /* 结束项 */ }
};
```

```c
MODULE_DEVICE_TABLE(usb, skel_table);
```

## 开发 USB 设备驱动程序

`id_table` 存储了将目标设备与设备驱动程序匹配的信息，通常包括厂商 ID（`vendor ID`）和产品 ID（`product ID`）。

一旦 `usb_driver` 结构体被正确初始化，你就可以使用 `usb_register` 接口函数向 `usbcore` 模块注册它。这使得内核设备框架能够在 `id_table` 匹配时回调 `probe` 函数。

```c
static int __init usb_skel_init(void)
{
    /* 向 USB 子系统注册此驱动程序 */
    result = usb_register(&skel_driver);
    --cut--
}
```

当设备退出或从内核中卸载时，使用 `usb_deregister` 从 `usbcore` 模块中移除该驱动程序。

```c
static void __exit usb_skel_exit(void)
{
    /* 从 USB 子系统中注销此驱动程序 */
    usb_deregister(&skel_driver);
}
```

在定义入口和退出例程后，你需要创建设备驱动程序的 `probe` 函数。`probe` 例程执行设备驱动程序所需的初始化，并使用 `usb_set_intfdata` 接口函数将接口设置到驱动程序。在完成所有成功步骤后，使用 `usb_register_dev` 接口例程将设备或接口驱动注册到 `usbcore` 模块。

```c
static int skel_probe(struct usb_interface *interface, const struct usb_device_id *id)
{
    --cut--
    --cut--
    dev = kzalloc(sizeof(dev), GFP_KERNEL);
    if (!dev) {
        err("Out of memory");
        goto error;
    }
    --cut-
    --cut--
```

```c
dev->udev = usb_get_interface_usb_dev(interface_to_usbdev(interface));
dev->interface = interface;
```

```c
iface_desc = interface->cur_altsetting;
for (i = 0; i < iface_desc->desc.bNumEndpoints; ++i) {
    endpoint = &iface_desc->endpoint[i].desc;
```

--cut-

`usb_set_intfdata(interface, dev);`

```c
/* 现在可以注册设备了，因为它已经准备就绪 */
retval = usb_register_dev(interface, &skel_class);
```

--cut-
--cut-

成功注册后允许驱动程序接管接口并开始与设备通信。

当设备断开或取消绑定时，会调用 `disconnect` 回调方法。`disconnect` 回调应该释放已获取的资源并返回之前获取的接口。成功释放资源后，驱动程序应该通过接口函数从 `usbcore` 中注销。
