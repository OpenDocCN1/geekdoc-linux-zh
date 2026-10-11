
```c
struct usb_endpoint_descriptor {
    u8 bLength;
    u8 bDescriptorType;

    u8 bEndpointAddress;
    u8 bAttributes;
    le16 wMaxPacketSize;
    u8 bInterval;

    /* 注意：这些仅存在于音频端点中 */
    /* 在长度、描述符大小中使用 USB_DT_ENDPOINT_SIZE */
    u8 brefresh;
    u8 bSyncAddress;
} __attribute__((packed));
```

你可以使用以下代码片段从当前 USB 接口备选（altsetting）包含的 IN 和 OUT 端点描述符中获取 IN 和 OUT 端点地址：

```c
struct usb_host_interface *altsetting = intf->cur_altsetting;
int ep_in, ep_out;
```

> /* 在此接口备选中有两个 `usb_host_endpoint` 结构。每个 `usb_host_endpoint` 结构都包含一个 `usb_endpoint_descriptor` */

`ep_in = altsetting->endpoint[0].desc.bEndpointAddress;`

`ep_out = altsetting->endpoint[1].desc.bEndpointAddress;`

# USB 请求块 (URB)

主机与设备之间的任何通信都是通过使用 USB 请求块 (`urbs`) 异步完成的：

- 一个 URB 包含了执行任何 USB 事务并传回数据和状态的所有相关信息。
- URB 的执行本质上是一个异步操作，即 `usb_submit_urb()` 调用在队列了请求的操作后立即返回。
- 可以在任何时候通过 `usb_unlink_urb()` 取消一个 URB 的传输。
- 每个 URB 都有一个完成处理程序（completion handler），在操作成功完成或取消后会被调用。URB 还包含一个上下文指针，用于向完成处理程序传递信息。
- 设备的每个端点本地都支持请求队列。你可以填充该队列，以便当驱动程序处理另一个完成操作时，USB 硬件仍然可以传输数据到端点。这最大化地利用了 USB 带宽，并支持在使用周期性传输模式时向设备（或从设备）无缝流传输数据。

以下是 `urb` 结构的一些重要字段：

```c
struct urb
{
    // (IN) 设备和管道指定端点队列
    struct usb_device *dev;              // 指向关联 USB 设备的指针
    unsigned int *pipe;                  // 端点信息

    unsigned int transfer_flags;         // URB_ISO_ASAP, URB_SHORT_NOT_OK, 等

    // (IN) 所有都需要完成例程
    void *context;                       // 完成例程序的上下文
    usb_complete_t complete;            // 指向完成例程序的指针

    // (OUT) 每次完成后的状态
                                // 返回的状态

    // (IN) 数据传输的缓冲区
    void *transfer_buffer;               // 关联的数据缓冲区
    u32 transfer_length;                 // 数据长度
    int number_of_packets;               // iso_frame_desc 的大小

    // (OUT) 有时仅使用 CTRL/BULK/INTR transfer_buffer 的部分
    u32 actual_length;                   // 实际数据缓冲区长度
    // (IN) CTRL 的设置阶段（传递 struct usb_ctrlrequest）
    unsigned char *setup_packet;        // 设置包（仅限控制）

    // 仅用于周期性传输 (ISO, INTERRUPT)
    // (IN/OUT) 除非未设置 URB_ISO_ASAP，否则会设置 start_frame
    int start_frame;                     // 起帧
    int interval;                        // 间隔

    // ISO：数据包是“尽力而为”的；每个包都可以
    int error_count;                      // 错误数量
    struct urb_iso_packet_descriptor iso_frame_desc[0];
};
```

USB 驱动程序必须使用其声明的接口中相应端点描述符的值创建一个“管道”。

通过调用 `usb_alloc_urb()` 分配 URB：

```c
struct urb *usb_alloc_urb(int isframes, int mem_flags);
```

返回值指向分配的 URB 的指针，如果分配失败则返回 0。参数 `isframes` 指定我们等待的同步传输次数。对于 CTRL/BULK-INT，请使用 0。参数 `mem_flags` 持有静态内存分配标志，允许你控制（以及其他方面）底层块是否可能阻塞。

要释放 URB，使用 `usb_free_urb()`：

```c
void usb_free_urb(struct urb *urb);
```

中断传输是周期性的，并在 2 的幂次间隔内（1, 2, 4 等单位）发生。全速和低速设备的单位是帧（frames），高速设备是微帧（microframes）。你可以使用 `usb_fill_int_urb()` 宏来填充 INT 传输字段。当使用 `usb_fill_int_urb()` 函数用正确的信息填充写入 `urb` 后，你应该将 `urb` 的完成回调指向你自己的回调函数。该函数在中断上下文中调用，因此必须注意不要在此时进行过多的处理。`usb_submit_urb()` 会修改 `urb->interval` 为小于或等于请求间隔值的实现值。

通过使用函数 `usb_submit_urb()` 提交 URB：

```c
int usb_submit_urb(struct urb *urb, int mem_flags);
```

参数 `mem_flags`、`GFP_ATOMIC` 控制底层块是否可以阻塞。它返回一些错误代码，如下：

- `ENOMEM`。
- `ENODEV`。
- `EPIPE`。
- `EAGAIN`。
- `EBIG`。
- `EINVAL`。
- `INPROGRESS`。

提交后，`urb->status` 会发生变化以反映你仍在等待完成处理程序。有两种方法可以取消 URB。异步取消请调用 `usb_unlink_urb()`：

```c
int usb_unlink_urb(struct urb *urb);
```

`usb_unlink_urb()` 函数从内部列表中移除并释放所有分配的内存。返回状态。同步取消 URB 请调用 `usb_kill_urb()`：

```c
void usb_kill_urb(struct urb *urb);
```

`usb_kill_urb()` 函数执行 `usb_unlink_urb()` 的所有操作，并且等待 URB 被返回且完成处理程序结束。在完成处理程序中，你应该检查 `urb->status` 以检测 USB 错误。由于 URB 中包含了上下文参数，你可以向完成处理程序传递信息。

# USB 设备应用程序

在第一个 USB 实验中，你将学习如何创建一个功能完整的 HID 设备以及如何使用 HID 报告发送和接收数据。对于本实验，你将使用 Curiosity32MX470 开发板：

Curiosity PIC32MX470 开发板采用 PIC32MX 系列 (`PIC32MX470512H`)，120MHz CPU、512KB Flash、128KB RAM、全速 USB 以及多种扩展选项。

Curiosity 开发板集成了编程器/调试器、带有多个 LED、RGB 等级和开关。每个板提供来自 MicroElectronika 的两个 MicroBus® 扩展槽、I/O 扩展接头和 Microchip X32 接头，方便寻求加速原型开发的客户。本章的应用程序使用 Windows 版本的工具开发，并包含本书 GitHub 的 `PIC32MX_labs.zip` 文件中，该文件位于 `linux_5.4_USB_drivers` 文件夹。以下是工具的版本：

- 开发环境：`MPLAB® X IDE v5.10`
- C 编译器：`MPLAB® XC32 v2.15`
