

## 引导：USB 监控

usbmon 的工作方式与其他任何设备一样：它通过文件操作扩展其资源（挂钩的信息）。对于 USB 开发人员来说，没有必要深入研究该模块的实现细节。为了扩展理解，请参考本章末尾的“更多阅读”部分。

`drivers/usb/mon.c` 定义了数据结构 `mon_event`，当主机控制器发生以下任何一种事件时，该结构会映射 URB 信息：提交 URB、完成 URB 或发生错误。

```c
struct mon_event {
    list_head e_link;
    int type;
    unsigned long id;
    unsigned int timestamp;
    int busnum;
};
```

`busnum` 变量表示发生 URB 事件的 USB 总线。Linux 内核为每个总线线分配一个从 1 开始的唯一编号。

## 使用 Linux USB 进行调试

`devnum`变量表示发生 URB 事件的设备。Linux 内核为每个 USB 设备分配一个从 1 开始的唯一编号。`epnum`变量表示处理 URB 的端点，其值从 0 开始。

`is_in`变量表示 URB 事件的方向，`true` 表示 IN（入）传输，`false` 表示 OUT（出）传输。`xtype`变量表示 USB 上支持的不同传输类型。该变量可以分别存储批量（bulk）、中断（interrupt）、等时（isochronous）或控制（control）传输。

`length`成员映射 URB 中传输的数据长度。这可能是实际的缓冲区长度，也可能是传输长度。`status`成员表示 URB 传输的状态。该字段对于非等时 URB 传输有效。返回状态基于 `linux/errno.h` 中定义的值。

`interval`变量表示时间受限传输（如中断传输和等时传输）的传输周期。它基于设备配置。`start_frame`成员专用于等时传输，表示等时传输的初始帧。`error_count`变量也专用于等时传输，表示等时传输中的错误次数。

`setup_flag`变量指示该数据结构对象是否为数据包包/设置包（setup packet），并可以持有以下值：0（已捕获 Setup 数据）、-（无法捕获 Setup 包）和 Z（无效）。

`data_flag`变量指示该数据结构对象是否包含数据作为事件信息的一部分。它可以持有以下值：0（数据可用）、<=（IN 完成）、>=（OUT 提交）、L（长度为 0）和 Z（无效）。

`numdesc`成员映射了 URB 结构中的 `number_of_packets`，表示等时包的数量。由于这是用于 USB 传输的调试机制，不需要从 URB 挂钩完整的数据。因此，usmon 的文本版本仅映射了部分 URB 数据。以下成员根据传输类型捕获/持有数据：

```c
struct mon_iso_desc isodes[ISODESC_MAX];
unsigned char setup[SETUP_MAX];
unsigned char data[DATA_MAX];
```

从前面的宏中，你可以理解数据字段仅包含部分数据。usmon 的二进制版本为 URB 提供完整信息。然而，这些额外数据大多是特定类别的，针对这些模块的专用数据包分析器比 usmon 更有效。例如，针对大存储（mass storage）和 SCSI 等类有特定类的数据包监控器。

在对处理 usmon URB 事件的数据结构有了简要概述后，后续章节将关注 usmon 内部的序列流、它如何挂钩信息以及如何与用户空间共享挂钩信息。

## USB 监控器原理

与其他任何模块一样，usmon 通过文件系统将 Linux 内核细节扩展到用户空间。由于 usmon 模块用于调试，因此它使用了 debugfs。

## USB 监控器：usbmon

`usb_mon_operations` 使用 usbcore 导出的回调方法。

```c
struct usb_mon_operations {
    void (*submit)(struct usb_bus *bus, struct urb *urb);
    void (*submit_error)(struct usb_bus *bus, struct urb *urb, int err);
    void (*complete)(struct usb_bus *bus, struct urb *urb, int status);
    void (*unlink)(struct usb_bus *bus, struct urb *urb);
};
```

