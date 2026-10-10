
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

下一个重要的函数是处理通过端点（Endpoint）发送的控制请求。控制请求的处理是中断例程序的一部分。如图 13.4 所示，gadget 框架处理控制请求并将通过注册的 `setup` 回调将控制传递给类驱动程序。

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

# 第 14 章

## 类驱动 (CLASS DRIVER)

本章内容

- 基础知识：类驱动
- 类驱动：设计
- 简单复合类驱动：回环 (Loopback)

通用串行总（USB）设备通常根据它们支持的功能来命名，例如 USB 音频设备或 USB 存储设备。USB 设备的功能在类驱动层中实现。这些类由 USB 工作组定义，并可以在 `http://www.usb.org/developers/devclass_docs#approved` 找到。有时，一个设备可以支持多个功能驱动程序，被称为复合设备（composite device）。

Linux 支持提供单一的功能型驱动程序，例如大容量存储设备。最近，Linux gadget 引入了一个复合框架（composite framework），使得 gadget 框架能够支持多个功能。图 14.1 展示了在 Linux USB gadget 子系统中，类驱动以及 gadget 和外设设备控制器 (PDC) 驱动所起的作用。

复合框架位于功能型驱动程序和 gadget 驱动之间，如图 14.2 所示。

![](img/779a74a6577501a55983f193067274a3_202_0.png)

图 14.1

gadget 子系统不同层之间的交互。

![](img/779a74a6577501a55983f193067274a3_202_1.png)

图 14.2

复合 gadget 子系统。

本章最初探讨类驱动和复合框架的基础数据结构，随后探讨复合功能型驱动的内部流程。最后，它分析了一个简单的复合功能型驱动程序的实现。

### 基础知识：类驱动

类驱动负责根据由 USB 描述符确定的 USB 设备功能。类驱动使用的重要数据结构是描述符数据结构。这些数据结构定义在内核源码的 `include/linux/usb/ch9.h` 文件中。

`struct usb_device_descriptor`、`struct usb_config_descriptor`、`struct usb_interface_descriptor` 和 `struct usb_endpoint_descriptor` 会由类驱动传递给 gadget 驱动。根据 USB 规范第 9 章定义的描述符允许向主机描述设备描述。

```c
struct usb_device_descriptor {
	__u8 bLength;
	__u8 bDescriptorType;
	__le16 bcdUSB;
	__u8 bDeviceClass;
	__u8 bDeviceSubClass;
	__u8 bDeviceProtocol;
	__u8 bMaxPacketSize;
	__le16 idVendor;
	__le16 idProduct;
	__le16 bcdDevice;
	__u8 iManufacturer;
	__u8 iProduct;
	__u8 iSerialNumber;
	__u8 bNumConfigurations;
} __attribute__((packed));
struct usb_config_descriptor {
	__u8 bLength;
	__u8 bDescriptorType;
	__le16 wTotalLength;
	__u8 bNumInterfaces;
	__u8 bConfigurationValue;
	__u8 iConfiguration;
	__u8 bmAttributes;
	__u8 bMaxPower;
} __attribute__((packed));
struct usb_interface_descriptor {
	__u8 bLength;
```

```c
	__u8 bDescriptorType;
	__u8 bInterfaceNumber;
	__u8 bAlternateSetting;
	__u8 bEndpoints;
	__u8 bInterfaceClass;
	__u8 bInterfaceSubClass;
	__u8 bInterfaceProtocol;
	__u8 iInterface;
} __attribute__ ((packed));
struct usb_endpoint_descriptor {
	__u8 bLength;
	__u8 bDescriptorType;
	__u8 bEndpointAddress;
	__u8 bAttributes;
	__le16 wMaxPacketSize;
	__u8 interval;
	/* 注意：这些仅用于音频端点 */
	/* bLength 中使用 USB_ENDPOINT*_SIZE 而不是 sizeof。 */
	__u8 bRefresh;
	__u8 Synch;
} __attribute__
```

另一个重要的框架是复合框架，它位于 gadget 驱动之上。为了支持多个功能，复合框架提供了配置的方法以及维护它们的数据结构。复合框架使用 `struct_function` 和 `struct_configuration`。它们定义在 `include/usb/composite.h` 中。

```c
struct usb_function {
	const char *name;
	struct gadget_strings **strings;
	struct descriptor_header **descriptors;
	struct descriptor_header *config;
	int (*bind)(struct usb_configuration);
	void (*unbind)(struct usb_configuration);
};
struct usb_configuration {
	const char *label;
	struct gadget_strings **strings;
	struct descriptor_header **descriptors;
	int (*setup)(struct usb_configuration);
	u8 bConfigurationValue;
	u8 iConfiguration;
	u8 bmAttributes;
	u8 bMaxPower;
	struct usb_composite_dev *cdev;
	struct list_head list;
	struct list_head functions;
	u8 next_interface_id;
	unsigned highspeed:1;
	unsigned fullspeed:1;
	struct usb_function *interface[MAX_CONFIG_INTERFACES];
};
```

这些回调函数的功能与上一章过的 gadget 回调函数相似。复合框架还定义了接口函数来注册并将复合信息添加到 gadget 框架中。

- `int usb_composite_register(struct usb_composite_driver *);`
- `void usb_composite_unregister(struct usb_composite_driver *);`
- `int usb_add_function(struct usb_configuration *, struct usb_function *);`
- `int usb_add_config(struct usb_composite_dev *, struct usb_configuration *)`

### 类驱动：设计

功能型驱动层位于 gadget 驱动层之上，实现实际的 USB 设备功能。功能型驱动也被称为类驱动。USB组通过 USB 类规范定义 USB 设备功能。与 gadget 子系统的其他层一样，功能型驱动源码位于 `drivers/usb/gadget/`，源文件根据其支持的类或功能命名。

![](img/779a74a6577501a55983f193067274a3_207_0.png)

**图 14.3** Linux USB gadget 功能层的简要拆解。

图 14.3 提供了 gadget 子系统功能层的简要拆解。

从图 14.3 中，你可以推断出功能层由决定 USB 特性的例程组成。其中一个例程管理 USB 描述符，一组例程管理 USB 设备实现的存储或鼠标功能，而其他例程则与 Linux 文件系统交互，以 `gadgetfs` 的形式将内部数据结构导出到用户空间。

功能层的另一个重要框架是**复合驱动程序框架**（composite driver framework），它是可选的。

在给定的基础设施上，你可以构建一个支持多个功能的复合设备。复合基础设施可以支持单配置和多配置设备，这些设备支持多个功能，且并不要求每个配置必须包含多个一个功能。图 14.4 展示了复合驱动框架的功能拆解。

复合框架提供了添加配置、功能的方法，以及维护这些内容的数据结构。后续章节将专门关注复合框架以及复合框架中发生的活动序列。

![](img/779a74a6577501a55983f193067274a3_208_0.png)

图 14.4

Linux USB gadget 复合驱动层的简要拆解。

![](img/779a74a6577501a55983f193067274a3_208_1.png)

图 14.5

复合驱动的简单控制流。

图 14.5 提供了使用复合层时的简单控制流。

复合框架包含三个与类驱动层（class driver layer）不同的活动序列：使用复合框架注册 gadget 框架、向功能层添加配置、以及向配置添加功能。下一节将详细探讨这些活动。

图 14.6 展示了在功能初始化和退出期间发生的典型调用序列。在复合框架中，复合驱动程序充当功能驱动程序与 gadget 驱动程序之间的接口。

![](img/779a74a6577501a55983f193067274a3_209_0.png)

**图 14.6** 复合驱动初始化期间的活动序列。

复合驱动程序模块将 `struct usb_composite_driver` 注册到复合框架。随后，复合框架又注册到 gadget 框架以进行后续活动；取消注册时也遵循类似的序列。

注册成功后触发的下一个活动序列是驱动程序与 gadget 驱动程序之间的交互。对于复合驱动，`bind` 回调会将复合驱动配置添加到复合框架中，如图 14.7 所示。

然后，配置将使用 `add_function` 绑定它想要支持的功能，如图 14.8 所示。

一旦成功添加了功能，设备就准备好对复合驱动进行枚举。主机决定从复合驱动中选择哪种配置。实现特定功能的特定例程将接管功能程序流。下一节将探讨复合驱动。

![](img/779a74a6577501a55983f193067274a3_210_0.png)

**图 14.7** 添加复合配置期间的活动序列。

### 简单复合类驱动：回环（LOOPBACK）

为了让你更好地理解复合驱动函数的流程，本节将探讨回环复合函数，该函数是 gadget 框架的一部分，位于 `drivers/usb/gadget/f_loopback.c`。在 gadget 框架中，`drivers/usb/gadget/zero.c` 复合驱动使用了回环功能。

你可以通过向功能层添加配置并向配置添加功能来启动复合驱动。开发过程中，`gadgetfs` 导出内部数据结构以方便复合框架。`f_loopback.c` 创建了 `struct usb_configuration` 结构。

```c
static struct usb_configuration loopback = {
    .name = "loopback",
    .descriptors = 
    .bConfigurationValue = 1,
```

![](img/779a74a6577501a55983f193067274a3_218_0.png)

图 14.8

添加复合功能期间的活动序列。

然后，配置将使用 `add_function` 绑定它想要支持的功能，如图 14.8 所示。

一旦成功添加了功能，设备就准备好对复合驱动进行枚举。主机决定从复合驱动中选择哪种配置。实现特定功能的特定例程将接管功能程序流。下一节将探讨复合驱动。

# 第 15 章 LINUX USB OTG 驱动

实现部分（`drivers/usb/gadget/inode.c`）为部分在内核空间和部分用户空间开发驱动提供了更多见解。复合框架（composite framework）还提供了工具，允许你启用和禁用功能驱动。你可以在 `drivers/usb/gadget/composite.c` 中探索这些内容。

## 第三部分 USB OTG

![](img/779a7a6577501a55983f19306774a3_0.png)

### 引导基础：OTG 驱动

通用总线（USB）随插用（OTG）规范是 USB 2.0 规范的补充，于 2000 年初出现，目的是让 USB 设备支持最小主机能力，从而使数字相机、手机和打印机等 USB 设备能够相互连接，如图 15.1 所示。

切换角色的嵌入设备被称为双角色设备（dual role device），其特性包括最小 USB 主机能力、会话请求协议（SRP）、主机协商协议（HNP）以及 VBUS 上的 8mA 电流。你应该阅读关于这些协议以及角色切换如何实现的 OTG 规范；该主题超出了本章的范围。Linux 拥有支持 OTG 设备的简单基础设施，类似于外设控制器（PDC），OTG 框架负责处理和响应 SRP 和 HNP 等 OTG 协商。

![](img/779a7a6577501a55983f19306774a3_0.png)

**图 15.1 典型设置（引用：`http://www.usb.org/developers/`）。从宏观上来说，OTG 框架的功能控制 USB 接收器以满足 OTG 要求。本章为 Linux USB 子系统提供了一个基本的引导会话。

### 引导基础：OTG 驱动

OTG 框架的数据结构定义在 `include/usb/otg.h` 中，源代码维护在 `drivers/usb/otg/` 中。OTG 框架使用 `struct otg_transceiver` 作为数据结构来持有管理 OTG 请求的方法。
