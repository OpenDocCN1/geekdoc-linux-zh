
# Linux PCMCIA 程序员指南

本文描述了如何为 Linux PCMIA Card Services 接口编写内核设备驱动程序。它还介绍了如何编写与 Card Services 通信的用户态工具。本文文档的最新版本可以在 <http://pcmia-cs.sourceforge.net>。

# 7 驱动服务接口

# 8 Card Services 客户端驱动的结构

# 9 Socket 驱动层

# 10 更多信息的获取途径 73

# 1 引言

Linux 内核 PCMCIA 系统包含三个主要组件。最底层是 Socket 驱动。接下来是 Card Services 模块。特定卡的驱动层叠在 Card Services 之上。有一个特殊的 Card Services 客户端，称为 Card Services，它在用户态实用程序与内核设施之间提供了连接。

Socket 驱动松地基于 Socket Services API。有两个 Socket 驱动模块：`tcic` 模块支持 Datasbook TICC-2 族主机控制器；`i82365` 族以及各种兼容控制器，包括 Cirrus、VLSI、Ricoh 和 Vadem 芯片。此外，`i82365` 模块实现了遵循“Yenta”寄存器级规范的 CardBus 控制器。

Card Services 是该包中最大的组件。它提供了一个类似于 DOS Card Services 的 API，并针对 Unix 环境进行了适配。Linux 的实现部分基于 Solaris 接口规范。它在 `pcmia_core` 模块中实现。实现了大多数版本 2.1 的功能，以及一些 PC Card 95 的功能。

驱动层使用用户伪设备来从实用程序访问某些 Card Services 功能。它负责跟踪所有的客户端驱动，并将驱动与物理插槽进行匹配。它实现在 `da` 模块中。

本文描述了指向 Card Services 和 Driver Services 模块的接口，以及指向 Driver Services 的用户接口。它供客户端设备驱动开发者使用。Linux PCMCIA-HOWTO 描述了如何安装和使用 Linux PCMCIA 支持。可以在 <http://pcmcia-cs.sourceforge.net> 获取。

## 1.2 致谢

感谢所有帮助测试和调试此软件、并帮助驱动开发的 Linux 用户。我还应该感谢 Linux Torvalds、Donald Becker、Alan Cox 和 Bjorn Ekwall 在 Linux 内核开发方面的帮助。我特别感谢 Michael Bender 在关于 Solaris 实现的许多有用讨论。

# 2 基础概念

## 2.1 Socket 接口

PC Card 总线有两种工作模式：“仅内存”和“内存与 IO”。第一种模式由原始 Version 1.0 规范定义，仅支持简单的内存卡。第二种模式在 Version 2.0 中定义，重新定义了少量内存卡控制信号以支持 IO 端口寻址和中断信号。

PC Card 设备有两个空间：“属性内存”和“通用内存”。接口可以寻址每种高达 16MB 的内存。属性内存通常用于存储描述信息和配置寄存器。通用内存可能包括内存卡的批量存储，或者在 IO 卡的情况下设备缓冲区。所有符合标准的卡都应该在属性内存中有一个卡信息结构（CIS），它描述了卡的情况以及如何配置它。

独立的控制信号允许卡片向系统发送其状态。这些信号包括卡存在检测、就绪/忙忙、写入、电源、电池和允许死卡。

“内存与 IO”接口模式允许卡片访问高达 64K 的 IO 端口。它还允许卡片发出 IO 中断，并将一个卡输出路由到主系统的扬声器。在这种模式下，某些内存控制信号是不可用的，因为这些引脚用于携带额外的 IO 卡信号。在某些卡上，这些信号可以从属性内存中的特殊配置寄存器“引脚替换寄存器”读取。

## 2.2 Socket 控制器

Socket 控制器充当 PC Card 设备与系统总线之间的桥梁。有多种控制器，但它们共享相同的基础功能。Socket 软件层负责处理主机控制器的所有细节。

Socket 控制器的工作是将主机内存和 IO 空间中的地址窗口映射到卡空间中的地址窗口。支持的控制器每个插槽至少支持四个内存窗口和两个 IO 窗口。

每个内存窗口由主机地址空间中的基地址、卡地址空间中的基地址以及窗口大小定义。某些控制器在内存窗口的对齐规则上有所不同，但所有控制器都支持大小至少为 4K 且为 2 的幂、且基地址是窗口大小倍数的窗口。每个窗口都可以编程指向属性内存或通用内存。

# 3. Card Services 子函数描述

IO 窗口与内存窗口的区别在于，落在窗口内的主机地址在传递给 IO 卡之前不会被修改。从本质上讲，主机空间和卡地址空间中窗口的基地址始终是相等的。IO 窗口没有对齐或大小限制；IO 窗口可以在 4K IO 地址空间内的任何边界开始和结束。

PC 卡定义了从卡到控制器的单路中断服务。控制器负责将此中断路由到适当的中断请求（`Irq`）线。所有支持路由卡中断的控制器都可以将其路由到几乎任何空闲的中线上。由于路由是在控制器中进行的，卡本身并不知道它使用的是哪种中断。

所有 PC 控制器都可以响应卡状态的变化产生中断。这些中断与由 IO 卡生成的 IO 中断不同，并使用独立的中断线。产生中断的信号包括卡检测、就绪/忙；写保护、电池电量低和电池耗尽。

# 3. Card Services 子函数描述

Card Services 的通用形式：

```c
#include "cs_types.h"
#include "cs.h"

int CardServices(int subfunc, void *arg1, void *arg2, ...);
```

某些 Card Services 函数需要额外的 #include 语句。特定的子函数决定了预期的参数数量。返回代码 `CS_SUCCESS` 表示调用成功。其他返回代码标识错误。

## 3.1 客户端管理函数

使用卡函数的设备驱动程序被称为“客户端”。设备驱动程序在使用其他服务之前，应该使用 `RegisterClient` 调用获取客户端句柄。大多数 Card Services 函数将此此客户端句柄作为参数。在卸载之前，驱动程序还应该通过 `DeregisterClient` 取消注册。

### 3.1.1 RegisterClient

```c
int CardServices(RegisterClient, client_handle_t *client, client_reg_t *reg);
```

`client_reg_t` 数据结构如下：

```c
typedef struct client_reg_t {
    dev_info_t *dev_info;
    Attributes;
    u_int EventMask;
    (*event_handler)(event_t event, int priority, event_callback_args_t event_callback, event_callback_args_t *args);
    u_int Version;
} client_reg_t;
```

`RegisterClient` 在客户端驱动程序与 Card Services 之间建立链接，并将客户端连接到适当的插槽。Card Services 使用 dev_info 参数匹配客户端与插槽及函数；这种对应通常由 Driver Services 通过调用 `BindDevice` 建立。如果成功，将在 client 中返回一个客户端句柄。

在 `Attributes` 中中可以指定以下标志：

- `INFO_MASTER_CLIENT`: 仅供 Driver Services 使用。此外，指定当卡从此插槽拔出时，此客户端不应自动取消绑定。
- `INFO_IO_CLIENT`: 指定此客户端是 IO 驱动程序。
- `INFO_MTD_CLIENT`: 指定此客户端是内存技术驱动程序（MTD）。
- `INFO_MEM_CLIENT`: 指定此客户端是内存卡驱动程序。
- `INFO_CARD_SHARE`: 为了兼容性而包含，无作用。
- `INFO_CARD_EXCL`: 为了兼容性而包含，无作用。

`EventMask` 指定此客户端应该接收哪些事件的通知。当 `EventMask` 中的事件被处理时，Card Services 将调用 `event_handler` 入口。`event_handler_args` 结构是传递给事件处理程序的结构模板。`Version` 参数标识该驱动程序期望的 Card Services 级别；目前被忽略。

驱动程序在调用 `RegisterClient` 之前应该准备好处理 Card Services 事件。此调用将始终生成一个 `CS_REGISTRATION_COMPLETE` 事件，如果插槽当前被占用，还可能生成一个人工的 `CS_CARD_INSERTION` 事件。

返回代码：
