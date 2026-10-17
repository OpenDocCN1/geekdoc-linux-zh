
| 3.1: | 92 `#define USB_REQ_ENPTION` | 0x0E |
| 3.1: | 93 `#define USB_REQ_ABORT` | 0x0F |
| 3.1: | 94 `#define USB_REQ_SIZE` | 0x10 |
| 3.1: | 95 `#define USB_REQ_HANDAKE` | 0x11 |
| 3.1: | 96 `#define USB_REQ_PIPE` | 0x12 |
| 3.1: | 97 `#define USB_REQ_CONNECTION` | 0x13 |
| 3.1: | 98 `#define USB_REQ_SECURITY` | 0x14 |
| 3.1: | 99 `#define USB_REQ_WRITE` | 0x15 |
| 3.1: | 100 `#define USB_REQ_LOOPBACK` | 0x16 |
| 3.1: | 101 `#define USB_REQ_READ` | 0x17 |
| 3.1: | 102 `#define USB_REQ_LOOPBACK` | 0x18 |
| 3.1: | 103 `#define USB_REQ_SET` | 0x19 |
| 3.1: | 104 `#define (missing text)` | 0x1A |
| 3.1: | 105 `#define USB_REQ_DATA` | 0x1B |
| 3.1: | 106 `#define (missing text)` | 0x1C |
| 3.1: | 107 `#define (missing text)` | 0x1D |
| 3.1: | 108 `#define (missing text)` | 0x1E |
| 3.1: | 109 `#define (missing text)` | 0x1F |

## 27.6 Linux 下的 USB

USB 有三层层：
- 主机控制器驱动 (`OHCI`, `UHCI`, `EHCI`)
- USB 核心
- 设备驱动![](img/134c18b05ee9bbbe93ba3f4335720ac1_276_0.png)

## 27.7 注册设备

USB 设备通过以下函数进行注册和注销：

```c
#include <linux/usb.h>

int usb_register(struct usb_driver *drv);
void usb_deregister(struct usb_driver *drv);
```

- `usb_register()` 成功返回 0，失败返回负数。
- 在注册之前，所有重要的 `usb_driver` 结构体必须完全初始化。

```c
struct usb_driver {
    const char *name;
    int (*probe)(struct usb_interface *int, const struct usb_device_id *id);
    void (*disconnect)(struct usb_interface *int);
    int (*ioctl)(struct usb_interface *int, unsigned code, void *buf);
    int (*suspend)(struct usb_interface *int, pm_message_t *message);
    int (*resume)(struct usb_interface *int);
    int (*reset_resume)(struct usb_device_id *id);
    const struct usb_device_id *ids_table;
    struct usb_dynids *dynids;
    struct usb_bdrv_wrap drvwrap;
    unsigned int no_dynamic_autosuspend;
    unsigned int supports_autosuspend;
    unsigned int soft_unbind;
};
```

- `name`：驱动模块。它在所有 USB 驱动中是唯一的，并在加载时显示在 `/sys/bus/usb/drivers`。
- `probe` 指向检查设备的函数，在新设备添加到 USB 总线时调用。如果驱动可以根据传递它的 `usb_device_id` 结构体接管设备，则例程序应初始化设备并返回零。如果驱动不接管，应返回负值。
- `disconnect` 指向设备从 USB 总线移除时调用的函数，而 `suspend` 和 `resume` 指向用于电源管理的函数。
- 仅使用了主要字段；还有其他选项。我们可以有一个：

```c
static struct usb_driver my_usb_my_usb = {
    .name = "my_usb_device",
    .id_table = my_usb_id_table,
    .probe = my_usb_probe,
    .disconnect = my_usb_disconnect,
};
```

## 27.7. 注册 USB 设备

- `id_table` 指向一个类型为 `usb_device_id` 的标识结构，定义在 `/usr/src/linux/include/linux/devicetree.h`：

```c
struct usb_device_id {
    /* which fields to match against? */
    __u16 match_flags;

    /* Used for product specific matches; range is inclusive */
    __u16 idVendor;
    __u16 idProduct;
    __u16 bcdDevice_lo;
    __u16 bcdDevice_hi;

    /* Used for device class matches */
    __u8 bDeviceClass;
    __u8 bDeviceSubClass;
    __u8 bDeviceProtocol;

    /* Used for interface class matches */
    __u8 bInterfaceClass;
    __u8 bInterfaceSubClass;
    __u8 bInterfaceProtocol;

    /* not matched against */
    kernel_ulong_t driver_info;
};
```

- `match_flags` 设置了结构体中其他字段应该与设备进行匹配的内容。通常这不会直接设置；它由我们讨论的 `USB_DEVICE` 宏初始化。
- `idVendor` 是设备唯一的 USB 厂商 ID，由 USB 控制机构分配。`idProduct` 是产品 ID，由厂商设置。
- `bcdDevice_lo`, `bcdDevice_hi` 是厂商确定的产品数的低位和高位。
- `bDeviceClass`, `bDeviceSubClass`, `bDeviceProtocol` 由 USB 控制机构分配，描述整个设备，包括所有接口。
- `bInterfaceClass`, `bInterfaceSubClass`, `bInterfaceProtocol` 描述单个接口。
- `driver_info` 可供驱动程序在调用 `probe()` 时用于区分不同的设备。
- `usb_device_id` 表通常使用以下宏初始化：

```c
USB_DEVICE(vendor, product)
USB_DEVICE_VER(vendor, product, hi)
USB_DEVICE_INFO(class, subclass, protocol)
USB_INTERFACE_INFO(class, subclass, protocol)
```

以直观的方式进行。因此，对于只控制某个厂商中一个设备的简单驱动程序，你可能会有：

```c
static struct usb_device_id my_usb_id_table = {
    { USB_DEVICE(MY_VENDOR_ID, MY_VENDOR_PRODUCT_ID) },
    { /* Null terminator (required) */ }
};
MODULE_DEVICE_TABLE(usb, my_usb_id_table);
```

`MODULE_DEVICE_TABLE` 宏对于用户空间热插拔工具执行其工作是必要的。

你可能已经回调函数没有直接引用 `usb_driver` 结构，而是指向一个类型为 `usb_interface` 的结构。可以通过以下函数在两个结构之间切换：
