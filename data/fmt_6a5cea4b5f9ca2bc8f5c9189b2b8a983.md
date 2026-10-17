
超时前等待消息完成的时间（如果为 0 则永久等待）

#### 描述

此函数向指定的端点发送简单的控制消息并等待消息完成或超时。

如果成功，返回 0，否则返回负错误代码。

不要在中断上下文中（如下半部处理程序）中使用此函数。如果你需要异步消息，或者需要从中断上下文中发送消息，请使用 `usb_submit_urb`

## usb_bulk_msg

### 名字

`usb_bulk_msg` — 构建批量 urb，发送它并等待完成

#### 概要

```
int usb_bulk_msg (struct usb_device * usb_dev, unsigned int pipe, void * data, int len, int * actual_length, int timeout);
```

#### 参数

- `usb_dev`

指向要发送消息的 USB 设备指针

- `pipe`

发送消息的端点 `pipe`

- `data`

指向要发送的数据指针

- `len`

要发送数据的字节长度

- `actual_length`

指向存储实际传输字节长度的位置指针

- `timeout`

超时前等待消息完成的时间（如果为 0 则永久等待）

#### 描述

此函数向指定的端点发送简单的批量消息并等待消息完成或超时。

如果成功，返回 0，否则返回负错误代码。实际传输的字节数将放在 `actual_length` 参数中。

不要在中断上下文中（如下半部处理程序）中使用此函数。如果你需要异步消息，或者需要从中断上下文中发送消息，请使用 `usb_submit_urb`

## 第 18 章 16x50 UART 驱动

### register_serial

### 名字

`register_serial` — 在运行时配置 16x50 串口

#### 概要

```
int register_serial (struct serial_struct * req);
```

#### 参数

`req`

请求结构体

#### 描述

配置请求指定的端口。如果端口存在且正在使用中，则返回错误。如果端口当前不在表中，则将其添加。

然后对端口进行探测，并在必要时自动检测 IRQ。如果此失败，则返回错误。

成功后，端口准备好就绪，并返回线路号。

## unregister_serial

### 名字

`unregister_serial` — 取消注册 16x50 串口

#### 概要

```
void unregister_serial (int line);
```

#### 参数

`line`

要取消注册的线路号

#### 描述

取消注册指定的线路，并释放该端口的资源。

## 第 19 章. Z8530 支持

### z8530_interrupt

### 名字

`z8530_interrupt` — 处理 Z8530 中断

#### 概要

```
void z8530_interrupt (int irq, void *dev_id, struct pt_regs * regs);
```

#### 参数

`irq`

中断号

`dev_id`

Z8530 设备

- `regs`

寄存器

#### 描述

一个正在发生中断的 Z8530 设备。我们为 Z8530 扫描并处理事件。我们为每个 Z8530 芯片使用回调函数。

### z8530_sync_open

### 名字

`z8530_sync_open` — 打开同步 PIO 的 Z8530

#### 概要

```
int z8530_sync_open (struct net_device * dev, struct z8530_channel * c);
```

#### 参数

`dev`

网络设备

`c`

要以同步 PIO 模式打开 Z8530 通道

#### 描述

设置 Z8530 设备。我们拉高 RTS/DTR 并开始网络操作。

### z8530_sync_close

### 名字

`z8530_sync_close` — 关闭同步 PIO 的 Z8530 通道

#### 概要

```
int z8530_sync_close (struct net_device * dev, struct z8530_channel * c);
```

#### 参数

`dev`

网络设备

`c`

要断的 Z8530 通道

#### 描述

关闭 Z8530 接口并切换其中断处理以忽略未来的事件。

### z8530_sync_dma_open

### 名字

`z8530_sync_dma_open` — 打开 DMA I/O 的 Z8530

#### 概要

```
int z8530_sync_dma_open(struct net_device * dev, struct z8530_channel * c);
```

#### 参数

`dev`

要附加的网络设备

`c`

要配置为同步 DMA 模式的 Z8530 通道

#### 描述

为 Z853x 设备设置双向同步 DMA。必须有两个 DMA 通道才能工作。我们假设使用 ISA 驱动的 I/O 以及 PC 的访问限制。

### z8530_sync_dma_close

### 名字

`z8530_sync_dma_close` — 关闭 DMA I/O

#### 概要

```
int z8530_sync_dma_close(struct net_device * dev, struct z8530_channel * c);
```

#### 参数

`dev`

网络设备

`c`

进入丢弃模式的 Z8530 通道

#### 描述

关闭 DMA 模式同步接口。停止 DMA 并释放缓冲区。

### z8530_sync_txdma_open

### 名字

`z8530_sync_txdma_open` — 打开 TX 驱动 DMA 的 Z8530

#### 概要

```
int z8530_sync_txdma_open (struct net_device * dev, struct z8530_channel * c);
```

#### 参数

- `dev`

要绑定的网络设备

- `c`

要在同步 DMA 模式下配置的 Z8530 通道。

#### 描述

为 Z8530 设备设置同步 DMA 传输。要使此工作，必须有一个可用的 ISA DMA 通道。接收端在 PIO 模式下运行，但其具有更大的 FIFO（先存缓冲区）。

## z8530_sync_txdma_close

#### 名称

`z8530_sync_txdma_close` — 关闭 TX 驱动的 DMA 通道

#### 概要

```
int z8530_sync_txdma_close (struct net_device * dev, struct z8530_channel * c);
```

#### 参数

- `dev`

要解绑的网络设备

- `c`

要移入丢弃模式的 Z8530 通道

#### 描述

关闭 DMA/PIO 分离模式的同步接口。停止 DMA 并释放缓冲区。

## z8530_describe

#### 名称

`z8530_describe` — 统一描述 Z8530 端口

#### 概要

```
void z8530_describe (struct z8530_dev * dev, char * mapping, unsigned long io);
```

#### 参数

- `dev`

要描述的 Z8530 设备

- `mapping`

持有映射类型的字符串（例如 "I/O" 或 "Mem"）

- `io`

涉及的端口值

#### 描述

以标准格式描述 Z8530。我们必须传递 I/O 值，因为端口偏移是不可预测的。此函数的主要目的是尝试获取一种通用格式的报告。

## z8530_init

#### 名称

`z8530_init` — 初始化 Z8530 设备

#### 概要

```
int z8530_init (struct z8530_dev * dev);
```

#### 参数

- `dev`

要初始化的 Z8530 设备。

#### 描述

配置 Z8530/Z85C30 或 Z85230 芯片。我们检查设备是否存在，识别类型并对其进行编程，以使其尽可能保持安静并正常运行。这一点非常重要，处于错误状态的 Z8530 有时会进入产生 10kHz 中断流之类的愚蠢模式。

我们设置中断处理程序以丢弃任何事件，以防在重置或设置期间产生这些事件。

返回 0 表示成功，或返回 errno 形式的负值表示问题。

## z8530_shutdown

#### 名称

`z8530_shutdown` — 关闭 Z8530 设备

#### 概要

```
int z8530_shutdown (struct z8530_dev * dev);
```

#### 参数

- `dev`

要关闭的 Z8530 芯片

#### 描述

我们设置中断处理器以屏蔽任何中断。然后重置芯片并等待 100uS 以确保重置完成。以防调用者随后尝试进行操作。

## z8530_channel_load

#### 名称
