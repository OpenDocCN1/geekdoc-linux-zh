

# 引导：通知者链 (Notifier Chain)

阻塞通知者链（blocking notifier chain）在进程上下文中运行。如名所示，阻塞通知链中的调用可能会被阻塞，因为它们在进程上下文中运行。Linux 网络模块使用阻塞通知者链来通知其他模块服务质量（QoS）值的变化或新设备的添加。因此，对实时性要求不高的通知可以使用阻塞通知者链。

<include/linux/notifier.h> 定义了 Linux 通知链框架的关键数据结构和接口定义。关键数据结构 `struct notifier_block` 为发布者模块扩展事件提供了框架。期待这些事件的订阅者模块为扩展事件注册回调函数：

```
struct notifier_block {
 int (*notifier_call)(struct notifier_block *, unsigned long,void *);
 struct notifier_block *next;
 int priority;
};
```

`struct notifier_block` 包含一个用于回调函数的函数指针，该列表扩展了对多个订阅者的支持。`priority` 字段创建了一个通知请求的排序列表。

提供通知支持的模块（发布者）还必须维护一个列表头（list head）来管理和遍历通知列表。<include/linux/notifier.h> 文件将此阻塞通知链头的原型定义为 `struct blocking_notifier_head`。

```
struct blocking_notifier_head {
 struct rw_semaphore rwsem;
 struct notifier_block *head;
};
```

该结构体维护了一个指向订阅者列表的头指针和一个用于避免竞态条件的信号量。

Linux 通知链子系统还提供了接口函数，用于从列表头部添加和删除 `struct notifier_block` 对象。任何订阅者都可以使用 `block_notifier_chain_register` 应用程序接口（API）向发布者模块列表的头部添加。你可以使用 `blocking_notifier_chain_unregister` 从列表中删除，其中 *block* 是通知链的类型。

## 第 5 章 = USB 设备通知

### 笔记

网络驱动程序通常使用通知链框架。

`blocking_notifier_chain_register` 方法的操作方式类似于简单的链表程序。该方法根据通知者块中设置的优先级将 `struct notifier_block` 添加到 `blocking_notifier_head` 头部：

```
int blocking_notifier_chain_register(struct blocking_notifier_head *nh, struct notifier_block *nb);
```

你可以使用通知者框架提供的 `blocking_notifier_chain_unregister` 从列表头移除已注册的 `struct notifier_block` 回调：

```
int blocking_notifier_chain_unregister(struct blocking_notifier_head *nh, struct notifier_block *nb);
```

一旦你成功创建了通知链，当特定事件发生时，必须执行回调函数。`blocking_notifier_call_chain` 接口函数会调用已注册的回调函数。该接口函数获取通知头并遍历它以调用注册的函数。另一个参数 void 指针 *v* 会连同无符号长整数 `val` 传递给订阅者，用于指示事件类型：

```
int blocking_notifier_call_chain(struct blocking_notifier_head *nh, unsigned long val, void *v);
```

在了解通知链框架的概述后，现在你将看到 Linux USB 子系统如何使用通知链框架进行不同模块之间的通信。

## LINUX USB 通知

Linux-USB 通知框架是 uscore 功能的一部分，其核心功能是向其他模块（如文件系统或类框架）通信或移除 USB 设备/总线。你可以在 `linux/usb.h` 中找到 USB 通知框架的数据结构定义，并在 `/drivers/usb/core/notify.c` 中找到功能实现。

![](img/779a74a6577501a55983f193067274a3_77_0.png)

**图 5.1**
USB 通知的功能分解。

该框架的自上而下分解如图 5.1 所示。你可以将此框架可视化为管理列表的例程和处理通知的例程。

管理列表的例程是导出的作为接口。接口函数允许模块注册它们的回调函数，从而接收 USB 设备通知。

在了解 USB 通知模块的分解后，你现在将探索关键数据结构、API 和内部原理。

通知处理程序扩展了对四个事件的支持：USB 设备的添加、USB 总线的添加以及 USB 总线的移除。这些事件由 `linux/usb.h` 定义并在后续所示。它们源自 `usbcore`，随后被传递给其他 USB 模块：

```
/* 来自 usb core 的事件 **/
#define USB_DEVICE_ADD 0x0001 (代表 USB 设备的添加)
#define USB_DEVICE_REMOVE 0x0002 (代表 USB 设备的移除)
#define USB_BUS_ADD 0x0003 (代表 USB 总线的添加)
#define USB_BUS_REMOVE 0x0004 (代表 USB 总线的移除)
```

在使用通知者链时，过程的第一步是定义通知列表的头。USB 通知框架使用阻塞通知者链来传递设备通知，因为这些信息并不时间敏感。`notify.c` 声明了一个类型为 `struct blocking_notifier_head` 的通知列表头 `usb_notifier_list`，用于维护已注册回调列表的信息：

```
static BLOCKING_NOTIFIER_HEAD(usb_notifier_list);
```

其他例程使用此头通知链接来注册和管理通知列表。

现在你将查看作用于列表的函数。`usb_register_notify` 接口使用使用 `_notifier_chain_register` 函数将传递的 `notifier_block` 添加到头指针 `usb_notifier_list`。上一节讨论过的 `blocking_notifier_chain_register` 会根据 `struct_block` 中设置的优先级处理插入列表：

```
void usb_register_notify(struct notifier_block *nb)
{
 blocking_notifier_chain_register(&usb_notifier_list, nb);
EXPORT_SYMBOL_GPL(usb_register_notify);
}
```

`usb_unregister_notify` 接口函数允许其他子系统从 `usb_notifier_list` 中移除 `struct notifier_block` 对象，该例程内部使用 Linux 通知子系统提供的 `blocking_notifier_chain_unregister` 来移除该 `struct notifier_block` 对象。

```
void usb_unregister_notify(struct notifier_block *nb)
{
 blocking_notifier_chain_unregister(&usb_notifier_list, nb);
EXPORT_SYMBOL_GPL(unregister_notify);
}
```

通过这些接口例程，其他订阅者可以在 USB 子系统中注册它们的块。回顾之前的章节，该子系统发布四个事件：USB_DEVICE_ADD、USB_DEVICE_REMOVE、USB_BUS_ADD 和 USB_BUS_REMOVE。当这些事件发生时，发布者必须通知订阅者。为了实现这一点，Linux 框架使用了 `blocking_notifier_call_chain`。USB 通知模块导出以下例程来通知这些事件：

```
void usb_notify_add_device(struct usb_device *udev)
{
 blocking_notifier_call_chain(&usb_notifier_list, USB_DEVICE_ADD, udev);
}

void usb_notify_remove_device(struct usb_device *udev)
{
  /* 防止同时打开 us */
  mutex_lock(&ubsf_mutex);
  blocking_notifier_call_chain(&usb_notifier_list, USB_DEVICE_REMOVE, udev);
  mutex_unlock(&ubsf_mutex);
}
void usb_notify_add_bus(struct usb_bus *ubus)
{
blocking_notifier_call_chain(&usb_notifier_list, USB_BUS_ADD, ubus);
}
void usb_notify_remove_bus(struct usb_bus *ubus)
{
  blocking_notifier_call_chain(&usb_notifier_list, USB_BUS_REMOVE, ubus);
}
```

