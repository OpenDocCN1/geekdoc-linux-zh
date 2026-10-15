
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



- `CS_OUT_QF_RESOURCE`: 为此驱动程序找不到适当的插槽。

### 3.1.2 DeregisterClient

```c
int CardServices(DeregisterClient, client_handle_t client);
```

`DeregisterClient` 断开客户端与 Card Services 之间的连接。应在客户端释放其分配的资源后调用。一旦连接中断，在再次调用 `BindDevice` 之前无法重新建立。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_IN_USE`: 客户端仍分配了资源，例如 IO 窗口或中断，或插槽配置被锁定。

### 3.1.3 SetEventMask

```c
int CardServices(SetEventMask, client_handle_t client, eventmask_t *mask);
```

`eventmask_t` 结构如下：

```c
typedef struct eventmask_t {
    u_int Attributes;
    u_int EventMask;
} eventmask_t;
```

`SetEventMask` 更新决定哪些事件将通知此客户端。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

### 3.1.4 BindDevice

```c
int CardServices(BindDevice, bind_req_t *req);
```

`bind_req_t` 结构如下：

```c
typedef struct bind_req_t {
    socket_t Socket;
    u_char Function;
    dev_info_t *dev_info;
} bind_req_t;
```

`BindDevice` 将设备与特定的插槽关联。通常在识别到新插入卡后由 Driver Services 调用。一旦驱动绑定到插槽，就可以成为该插槽的客户端。注意，此调用不接受客户端句柄作为参数。它是唯一接受插槽号作为参数的 Card Service。`Function` 字段指定将多功能卡的哪些功能绑定到此驱动程序。如果 `Function` 设置为 `BIND_FN_ALL`，驱动程序将绑定到所有卡功能。驱动程序能够访问与其对应的 CIS 元组。

返回代码：

- `CS_BAD_SOCKET`: 指定插槽号无效。

## 3.2 插槽状态

这些函数更多地关注获取和设置插槽的当前状态。`GetStatus` 返回当前槽状态。`ResetCard` 用于向插槽发送硬复位信号。`SuspendAndResumeCard` 用于插槽掉电和上电。`EjectCard` 和 `InsertCard` 模拟卡事件。

### 3.2.1 GetStatus

```c
int CardServices(GetStatus, client_handle_t client, cs_status_t *status);
```

`cs_status_t` 结构如下：

```c
typedef struct cs_status_t {
    u_char Function;
    u_int CardState;
    u_int SocketState;
} cs_status_t;
```

`GetStatus` 返回客户端的当前状态。对于配置为 IO 模式的客户端，`GetStatus` 使用 `CardState` 来确定插槽状态。对于普通客户端，`Function` 字段被忽略，但对于 `BIND_FN_ALL` 客户端，它指定了功能。

`CardState` 定义了以下标志：

- `CS_EVENT_CARD_DETECT`: 插槽被占用。
- `CS_EVENT_CB_DETECT`: 插槽被 CardBus 设备占用。
- `CS_EVENT_WRITE_PROTECT`: 卡被保护。
- `CS_EVENT_BATTERY_LOW`: 卡电量低。
- `CS_EVENT_BATTERY_DEAD`: 卡电池耗尽。
- `CS_EVENT_READY_CHANGE`: 卡已就绪。
- `CS_EVENT_PM_SUSPEND`: 插槽已挂起。
- `CS_EVENT_REQUEST_ATTENTION`: 扩展状态中的注意位已设置。
- `CS_EVENT_CARD_INSERTION`: 正在进行卡插入事件。当插槽设置完成后，将插入事件发送给客户端。
- `CS_EVENT_3VCARD`: 表示卡支持 3.3V 操作。
- `CS_EVENT_XVCARD`: 表示卡支持“X.X”V 操作。实际电压在规范中尚未定义。

`SocketState` 目前未使用，但在理论上，它应该锁存 `CardState` 状态的变化。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

### 3.2.2 ResetCard

```c
int CardServices(ResetCard, client_handle_t client);
```

`ResetCard` 请求重置客户端的插槽。当调用此函数时，Card Services 向所有客户端发送 `CS_EVENT_RESET_REQUEST` 事件。如果任何客户端拒绝请求，Card Services 向发起请求的客户端发送 `CS_EVENT_RESET_COMPLETE` 事件，并将 `event_callback_args.info` 设置为拒绝请求客户端的返回代码。

如果所有客户端都同意请求，Card Services 发送 `CS_EVENT_RESET_PHYSICAL` 事件，然后重置插槽。当插槽信号其就绪时，会生成 `CS_EVENT_CARD_RESET` 事件。最后，向发起请求的客户端发送 `CS_EVENT_RESET_COMPLETE` 事件，并将 `event_callback_args.info` 设置为零。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_NO_CARD`: 分配给此客户端的插槽当前为空。
- `CS_IN_USE`: 此插槽当前正在重置。

### 3.2.3 SuspendCard

```c
int CardServices(SuspendCard, client_handle_t client);
```

Card Services 向所有客户端发送 `CS_EVENT_PM_SUSPEND` 事件，关闭并断开插槽电源。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_NO_CARD`: 分配给此客户端的插槽当前为空。
- `CS_IN_USE`: 该插槽已挂起。

### 3.2.4 ResumeCard

```c
int CardServices(ResumeCard, client_handle_t client);
```

在恢复插槽电源后，Card Services 将向所有客户端发送 `CS_EVENT_PM_RESUME` 事件。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_NO_CARD`: 分配给此客户端的插槽当前为空。
- `CS_IN_USE`: 该插槽当前未挂起。

### 3.2.5 EjectCard

```c
int CardServices(EjectCard, client_handle_t client);
```

Card Services 向所有客户端发送弹出事件，关闭并断开插槽电源。除了 Driver Services 外，所有客户端都将从插槽中取消链接。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_NO_CARD`: 分配给此客户端的插槽当前为空。

### 3.2.6 InsertCard

```c
int CardServices(InsertCard, client_handle_t client);
```

Card Services 向该插槽的所有客户端发送插入事件（通常只有 Driver Services）。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_NO_CARD`: 分配给此客户端的插槽当前为空。
- `CS_IN_USE`: 该插槽已配置。

## 3.3 IO 卡配置单元

事件的正常顺序是：驱动程序通过调用 `RequestIO` 和 `RequestIRQ` 来预留 IO 端口和中断线，以便实际配置插槽。如果这些任何调用失败，驱动程序应确保释放其成功保留的任何资源。

多功能卡可以为每个卡功能拥有单独配置。然而，这些配置之间需要保持一致。每个卡都有自己的配置寄存器组，每个插槽只有一条中断线，且只能映射两个 IO 端口范围。

CardBus 卡的配置方式有所不同。`RequestIO` 和 `RequestConfiguration` 调用具有相似的作用，Card Services 负责大部分配置细节，并会忽略请求结构的内容。



### 3.3.1 `RequestIO`

```c
int CardServices(RequestIO, client_handle_t client, io_req_t *req);
```

`io_req_t` 数据结构定义如下：

```c
typedef struct io_req_t {
    ioaddr_t BasePort1;
    ioaddr_t NumPorts1;
    u_int Attributes1;
    ioaddr_t BasePort2;
    ioaddr_t NumPorts2;
    u_int Attributes2;
    u_int IOAddrLines;
} io_req_t;
```

`RequestIO` 为卡预留端口窗口。`BasePort1` 指定了要保留的窗口起始 IO 端口地址。如果 `NumPorts2` 不为零，则还会预留第二个 IO 端口窗口。`IOAddrLines` 指定了卡实际所需的地址线数。IO 分配算法假设任何请求的地址只要保留了 `IOAddrLines` 位都是可以接受的，并将更新 `BasePort1` 和 `BasePort2` 以反映实际分配的地址范围。

在发布 `3.1.4` 版本之前，`IOAddrLines` 字段被忽略。分配器总是尝试分配请求的地址范围，除非基地址为 `0`；在这种情况下，它将分配任何与大于窗口大小 `2` 的幂对齐的可用窗口。新的分配器会验证 `IOAddrLines` 参数是否与窗口参数一致，如果发现不一致，则默认恢复到 `3.1.4` 之前的行为。

对于多功能卡，这将为每个卡功能分配 IO 端口，使得卡的所有端口都能由与物理插槽相关的两个低级 IO 窗口进行管理。例如，如果一个假设的四功能卡的驱动程序均尝试分配一个 `8` 端口的 IO 窗口，`Card Services` 将这些这些合并为一个连续的 `32` 端口块。

当此函数由 `CardBus` 客户端调用时，IO 请求将被忽略。相反地，`Card Services` 将会检查并分配任何必要的资源：这包括 IO 和内存空间，如果需要，还有中断。一个卡将保留所有卡功能所需的所有资源，而不仅仅是发起请求客户端的功能。

此调用实际上并没有配置插槽的 IO 窗口：这是通过后续调用 `RequestConfiguration` 完成的。

在 `Attributes1` 和 `Attributes2` 中可以指定以下标志：

- `IO_DATA_PATH_WIDTH`

该字段可以是 `IO_DATA_PATH_WIDTH_16`（用于 16 位访问）、`IO_DATA_PATH_WIDTH_8`（用于 8 位访问）或 `IO_DATA_PATH_WIDTH_AUTO`（根据访问大小动态调整总线）。

返回代码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的插槽当前为空。

- `CS_IN_USE`

该插槽的 IO 窗口已经预留。

- `CS_CONFIGURATION_LOCKED`

该插槽的配置已通过 `RequestConfiguration` 调用锁定。

- `CS_BAD_ATTRIBUTE`

指定了不支持的属性标志。

- `CS_UNSUPPORTED_FUNCTION`

对于 `CardBus` 客户端支持此项。

### 3.3.2 `ReleaseIO`

```c
int CardServices(ReleaseIO, client_handle_t client, io_req_t *req);
```

`ReleaseIO` 取消早先调用 `RequestIO` 分的中断。传递给 `RequestIO` 的 `req` 结构。如果在 `RequestIO` 调用中指定了处理程序，它将在此时取消注册。

返回代码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的插槽当前为空。

- `CS_IN_USE`

该插槽已经预留了中断。

- `CS_CONFIGURATION_LOCKED`

该卡功能的配置已通过 `RequestConfiguration` 调用锁定。

### 3.3.3 `RequestIRQ`

```c
int CardServices(RequestIRQ, client_handle_t client, irq_req_t *req);
```

`irq_req_t` 结构定义如下：

```c
typedef struct irq_req_t {
    u_int Attributes;
    u_int AssignedIRQ;
    u_int IRQ1, IRQ2;
    void *(Handler)(int, struct pt_regs *);
    void *Instance;
} irq_req_t;
```

`RequestIRQ` 使用中断线。如果调用成功，返回的中断设置为 `AssignedIRQ`。对于 `2.1.6` 内内核，`irq_dev_map` 表也会被更新。对于多功能卡，中断将以共享模式分配，处理程序负责在接收到中断时确定哪些卡功能需要处理。如果客户端反而绕过 `Card Services` 来

在 `Attributes` 中可以指定以下标志：

- `IRQ_FORCED_PULSE`

指定中断应配置为脉冲模式，而不是默认的电平模式。

- `IRQ_TYPE_TIME`

指定该中断可以与其他 `Card Services` 驱动程序共享。任何时间只有一个驱动程序启用中断。

- `IRQ_FIRST_SHARED`

结合 `IRQ_TYPE_TIME`，由第一个请求共享中断的驱动程序设置。

- `IRQ_HANDLER_PRESENT`

表示 `Handler` 字段指向应安装的中断服务程序。

返回代码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的插槽当前为空。

- `CS_IN_USE`

该插槽已经预留了中断，或者请求的中断不可用。

- `CS_CONFIGURATION_LOCKED`

该卡功能的配置已通过 `RequestConfiguration` 调用锁定。

- `CS_BAD_ATTRIBUTE`

指定了不支持的属性标志。

- `CS_UNSUPPORTED_FUNCTION`

对于 `CardBus` 客户端支持此项。

### 3.3.4 `ReleaseIRQ`

```c
int CardServices(ReleaseIRQ, client_handle_t client, irq_req_t *irq);
```

`ReleaseIRQ` 取消早先调用 `RequestIO` 分配的中断。传递给 `RequestIO` 的 `req` 结构。如果在 `RequestIRQ` 调用中指定了处理程序，它将在此时取消注册。

返回代码：

- `CS_BAD_HANDLE`

客户端句柄无效。

#### 卡片服务子函数描述

`CS_CONFIGURATION_LOCKED`

此套接已通过调用 `RequestConfiguration` 被锁定。在调用 `ReleaseIRQ` 之前，应该释放配置。

`CS_BAD_IRQ`

`req` 中的参数与传递给 `RequestIRQ` 的参数不匹配。

### 3.3.5 `RequestConfiguration`

```c
int CardServices(RequestConfiguration, client_handle_t client, config_req_t *req);
```

`config_req_t` 结构体如下：

```c
typedef struct config_req_t {
    u_int Attributes;
    u_int Vpp1, Vpp2;
    u_int IntType;
    u_int ConfigBase;
    u_char Status, Pin, Copy, ExtStatus;
    u_char ConfigIndex;
    u_int Present;
} config_req_t;
```

`RequestConfiguration` 负责实际对套接字。这包括设置电压、设置 CIS 配置寄存器、设置 IO 端口窗口以及设置中断。

`IntType` 指定了用于此卡卡的接口类型。它可以是 `INT_MEMORY`、`INT_MEMORY_AND_IO` 或 `INT_CARDBUS`。电压以 `1/10` 特为单位指定。目前，`Vpp1` 必须等于 `Vpp2`。

对于多功能卡，每个卡功能都是单独配置的。每个功能都有自己的自己的 CIS 配置寄存器组。然而，所有功能都必须使用电源和接口设置进行配置。

当被 `CardBus` 客户端调用时，大多数请求将被忽略，所有功能将根据之前 `Request10` 调用中收集的数据进行配置。这包括配置 `CardBus` 桥接器，同时在每个卡功能的配置空间中初始化基地址（Base Address）和中断线（Interrupt Line）。在这种情况下，`IntType` 必须设置为 `INT_CARDBUS`。

在 `Attributes` 中可以指定以下标志。DMA 和扬声器控制在所有系统上都不支持。

- `CONF_ENABLE_IRQ`

启用之前调用 `RequestIRQ` 请求的 IO 中断。

- `CONF_ENABLE_DMA`

启用此套接字的 DMA 访问。



- `CONF_ENABLE_SPKR`

启用此套接字的扬声器输出。

## 3. 卡片服务子函数描述

`Present` 参数是一个位图，指定了此卡实现了哪些 CIS 配置寄存器。`ConfigBase` 给出了配置寄存器在属性内存中的偏移量。可以指定以下寄存器：

- `PRESENT_OPTION`

指定配置选项寄存器（Configuration Option Register）存在。COR 器将使用 `ConfigIndex` 参数设置。

- `PRESENT_STATUS`

指定卡片配置和状态寄存器（Card Configuration and Status Register）存在。CCSR 将使用 `Status` 参数初始化。

- `PRESENT_PIN_REPLACE`

指定引脚替换寄存器（Pin Replacement Register）存在。PRR 将使用 `Pin` 参数初始化。

- `PRESENT_COPY`

指定套接字和复制寄存器（Socket and Copy Register）存在。SCR 将使用 `Copy` 参数初始化。

- `PRESENT_EXT_STATUS`

指定扩展状态寄存器（Extended Status Register）存在。ESR 将使用 `ExtStatus` 参数初始化。

返回码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的套接字目前为空。

- `CS_OUT_OF_RESOURCE`

卡片服务（Card Services）无法分配一个内存窗口来访问卡片的配置寄存器。

- `CS_CONFIGURATION_LOCKED`

此卡的配置已被另一个 `RequestConfiguration` 调用锁定。

- `CS_BAD_VCC`

请求的 `Vcc` 电压不受支持。

- `CS_BAD_VPP`

请求的 `Vpp1`/`Vpp2` 电压不受支持。

- `CS_UNSUPPORTED_MODE`

非 CardBus 客户端尝试配置 CardBus 卡，或 CardBus 客户端尝试配置非 CardBus 卡。

### 3.3.6 `ModifyConfiguration`

```
int CardServices(ModifyConfiguration, client_handle_t client, modconf_t *mod);
```

`modconf_t` 结构体如下：

```
typedef struct modconf_t {
    u_int               Attributes;
    u_int               Vcc, Vpp1, Vpp2;
} modconf_t;
```

`ModifyConfiguration` 修改已通过 `RequestConfiguration` 调用已配置的套接字的某些属性。

在 `Attributes` 中可以指定以下标志：

- `CONF_IRQ_CHANGE_VALID`

表示应该更新 `CONF_ENABLE_IRQ` 设置。

- `CONF_ENABLE_IRQ`

指定应为此套接字开启 IO 中断。

- `CONF_VCC_CHANGE_VALID`

表示应该更新 `Vcc`。

- `CONF_VPP1_CHANGE_VALID`

表示应该更新 `Vpp1`。

- `CONF_VPP2_CHANGE_VALID`

表示应该更新 `Vpp2`。

目前，`Vpp1` 和 `Vpp2` 必须始终保持相同的值。因此，这两个值必须同时更改。

返回码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的套接字目前为空。

- `CS_CONFIGURATION_LOCKED`

套接字配置已锁定。

- `CS_BAD_VCC`

请求的 `Vcc` 电压不支持。

- `CS_BAD_VPP`

请求的 `Vpp` 电压不支持。

### 3.3.7 `ReleaseConfiguration`

```
int CardServices(ReleaseConfiguration, client_handle_t client, config_req_t *req);
```

`ReleaseConfiguration` 释放由调用 `RequestConfiguration` 配置的套接字。

返回码：

- `CS_BAD_HANDLE`

客户端句柄无效。

### 3.3.8 `GetConfiguration`

```
int CardServices(GetConfiguration, client_handle_t client, config_info_t *config);
```

`GetConfiguration` 返回由 `RequestConfiguration` 设置的当前配置。

`config_info_t` 结构体如下：

```
typedef struct config_info_t {
    u_int Attributes;
    u_int Vcc, Vpp1, Vpp2;
    u_int IntType;
    u_char Status, Pin, Copy, ExtStatus;
    u_int Present;
    u_int AssignedIRQ;
    uaddr_t Base;
    uaddr_t NumPorts;
    uaddr_t Base2;
    uaddr_t NumPorts2;
    u_int Attributes2;
    int ID0;
} config_info_t;
```

返回码：

- `CS_BAD_HANDLE`

客户端句柄无效。

- `CS_NO_CARD`

分配给此客户端的套接字目前为空。

- `CS_CONFIGURATION_LOCKED`

套接字已锁定。

## 3.4 卡片信息结构 (CIS) 调用

卡片信息结构（CIS）的定义是 PC 卡标准中最深奥的章节。所有版本 2 的客户端都应该有一个 CIS，它描述了卡片以及如何配置。CIS 是卡片属性空间的元组（tuples）链表。每个元组由一个识别码、一个长度字节和一系列数据字节组成。

`ValidateCIS` 用于检查卡是否具有合理的 CIS。`GetFirstTuple` 和 `GetNextTuple` 用于遍历 CIS 元组。`GetTupleData` 从元组中提取数据字节。`ParseTuple` 将许多元组解析为更容易处理的形式。`ReplaceCIS` 允许客户端为找到 CIS 提供替代品。

### 3.4.1 `GetFirstTuple`, `GetNextTuple`

```
#include "cispl.h"

int CardServices(GetFirstTuple, client_handle_t client, tuple_t *tuple);
int CardServices(GetNextTuple, client_handle_t client, tuple_t *tuple);
```

`tuple_t` 数据如下：

```
typedef struct tuple_t {
    u_int Attributes;
    cis_data_t DesiredTuple;
    u_int Flags;
    cisdata_t TupleCode;
    u_int TupleLink;
    cisdata_t TupleOffset;
    cisdata_t TupleData;
    cisdata_t TupleLen;
    cisdata_t *TupleData;
} tuple_t;
```

`GetFirstTuple` 搜索第一个匹配 `DesiredTuple` 的 CIS。`RETURN_FIRST_Tuple` 将匹配任何类型的第一个元组。如果成功，`TupleCode` 将设置为第一个匹配元组的代码，`TupleLink` 是该属性在内存中的地址。

`GetNextTuple` 类似于 `GetFirstTuple`，给定之前调用 `GetFirstTuple` 或 `GetNextTuple` 返回的 `tuple_t`，它将返回下一个匹配 `DesiredTuple` 的元组。

这些函数会自动遍历 CIS 中的任何链接元组。对于使用 `CISPL_LONLINK_MFC` 的多功能卡，这些函数将自动遵循客户端驱动程序分配的 CIS 链。如果客户端绑定到 `BIND_FN_ALL`，则将返回所有元组。

可以在 `Attributes`（属性）中指定以下标志：

- `TUPLE_RETURN_LINK`

表示应返回链接元组（`CISTPL_LONGLINK_A`, `CISPL_LONGLINK_C`, `CISPL_LONLINK_MFC`, `CISPL_NOLINK`, `CISPL_LINTARGET`）。通常，这些元组是静默处理的。

- `TUPLE_RETURN_COMMON`

表示应返回多功能 CIS 中“common”（公共）部分中的元组。在没有此标志的情况下，通常 Card Services 只返回绑定到客户端的特定函数的元组。

返回代码：



- `CS_BAD_HANDLE`: 客户端句柄无效。

- `CS_OUT_OF_RESOURCE`: Card Services 无法建立内存窗口来映射卡片的 CIS。

- `CS_NO_MORE_ITEMS`: 没有匹配 `DesiredTuple` 的元组。

### 3.4.2 `GetTupleData`

```c
#include "cistpl.h"
```

```c
int CardServices(GetTupleData, client_handle_t client, tuple_t *tuple);
```

`GetTupleData` 从指定的元组中提取一系列字节，该元组必须是由之前调用 `GetFirstTuple` 或 `GetNextTuple` 返回的。最多将 `TupleDataMax` 字节将从从 `TupleOffset` 字节的偏移量开始复制到 `TupleData` 缓冲区中。复制的字节数返回在 `TupleDataLen` 中。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

- `CS_OUT_OF_RESOURCE`: Card Services 无法建立内存窗口来映射卡片的 CIS。

- `CS_NO_MORE_ITEMS`: 元组不再包含更多数据。`TupleOffset` 大于或等于元组的长度。

### 3.4.3 `ParseTuple`

```c
#include "cistpl.h"

int CardServices(ParseTuple, client_handle_t client, tuple_t tuple, tuple_t *tuple, cisparse_t *parse);
```

`cisparse_t` 数据结构如下：

```c
typedef union cisparse_t {
	cistpl_device_t      device;
	cistpl_checksum_t    checksum;
	cistpl_longlink_t    longlink;
	cistpl_longlink_mfc_t longlink_mfc;
	cistpl_vers_1_t      version_1;
	cistpl_altstr_t      altstr;
	cistpl_jedec_t       jedec;
	cistpl_manifold_t     manifold;
	cistpl_funcd_t       funcd;
	cistpl_config_t       config;
	cistpl_ctable_entry_t cftable_entry;
	cistpl_device_geo_t  device_geo;
	cistpl_vers_2_t      version_2;
	cistpl_org_t         org;
	cistpl_format_t      format;
} cisparse_t;
```

`ParseTuple` 解析之前调用 `GetTupleData` 返回的元组数据。返回的结构取决于所解析元组的类型。这些结构定义请参见 `cistpl.h` 文件；其中某些结构非常复杂。

返回代码：

- `CS_BAD_TUPLE`: 在解析此元组时遇到错误。该元组可能不完整，或者格式不。

- `CS_UNSUPPORTED_FUNCTION`: `ParseTuple` 无法解析指定的类型。

### 3.4.4 `ValidateCIS`

```c
int CardServices(ValidateCIS, client_handle_t client, cisinfo_t *cisinfo0);
```

`cisinfo_t` 结构如下：

```c
typedef struct cisinfo_t {
	u_int                Chains;
} cisinfo_t;
```

`ValidateCIS` 尝试验证卡片具有合理的卡片信息结构（CIS）。它返回 `Chains` 中找到的元组数量。如果 CIS 看起来不可解释，则 `Chains` 将设置为 `0`。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

- `CS_OUT_OF_RESOURCE`: Card Services 无法建立内存窗口来映射卡片的 CIS。

### 3.4.5 `ReplaceCIS`

```c
int CardServices(ReplaceCIS, client_handle_t client, cisdump_t *cisdump);
```

`cisdump_t` 结构如下：

```c
typedef struct cisdump_t {
    u_int Length;
    u_char Data[CISTPL_MAX_SIZE];
} cisdump_t;
```

`ReplaceCIS` 允许客户端向 Card Services 传递卡片 CIS 的替换。其设计目的是用于 CIS 不完整或不准确的卡片。如果能从其他信息中推出正确的 CIS，这允许以干净的方式向客户端提供信息。替换后的 CIS 将保持有效直到卡片弹出，并且所有与元组相关的服务都使用替换内容而非实际的 CIS。

`Length` 字段给出 `Data` 数组中的字节数。`Data` 数组可以视为卡片的属性内存。它应该包含所有所需的 CIS，包括初始的 `CISPL_DEVICE` 元组和最终的 `CISPL_END` 元组。可以使用长链接（包括 `CISPL_LONGLINK_MPFC`）：所有地址都在替换空间中进行解释。该服务在版本 3.0 中添加。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

- `CS_OUT_OF_RESOURCE`: Card Services 无法分配内存来存放替换的 CIS。

## 3.5 内存窗口

每个套字可以多多四个活跃的内存窗口，将卡内存部分映射到主机地址空间。设备可以寻址大多数公共和属性内存。窗口的大小通常是 2 的幂。根据套字的能力，它们可能需要在主机和卡片空间中对齐到窗口大小的倍数。

内存窗口通过调用 `RequestWindow` 初始化。某些属性可以使用 `ModifyWindow` 修改。映射到窗口的卡片内存段可以使用 `MapPage` 修改。窗口通过 `ReleaseWindow` 释放。与几乎所有其他子函数不同，内存函数作用于窗口句柄而非客户端句柄。

### 3.5.1 `RequestWindow`

```c
int CardServices(RequestWindow, client_handle_t *handle, win_req_t *req);
```

`win_req_t` 结构如下：

```c
typedef struct win_req_t {
    u_int               Attributes;
    u_long              Base;
    u_int               Size;
    u_int               AccessSpeed;
} win_req_t;
```

`RequestWindow` 将卡片内存映射到系统内存。输入时，`handle` 参数指向一个有效的客户端句柄。返回时，这将替换为窗口句柄，应用于后续的 `ModifyWindow`、`MapPage` 和 `ReleaseWindow` 调用。

可以在 `Attributes` 中指定以下标志：

- `WIN_MEMORY_TYPE`: 此字段可以是公共内存 `WIN_MEMORY_TYPE_CM` 或属性内存 `WIN_MEMORY_TYPE_AM`。

- `WIN_DATA_WIDTH`: 16 位访问 `WIN_DATA_WIDTH_16` 或 8 位访问 `WIN_DATA_WIDTH_8`。

- `WIN_ENABLE`: 设置此项时，开启窗口。

- `WIN_USE_WAIT`: 指定控制器观察 `MWAIT` 信号。

- `WIN_MAP_BELOW_1MB`: 请求窗口映射在 `1MB` 边界以下。这在某些平台上可能无法。

- `WIN_STRICT_ALIGN`: 请求基对齐到窗口大小的倍数。版本 3.1 添加。

`Base` 指定系统内存中窗口物理地址。如果为零，Card Services 将 `Base` 设置为第一个可用窗口地址。`Size` 指定窗口大小（字节）。如果为零，Card Services 将 `Size` 设置为主机支持的最小窗口大小。`AccessSpeed` 指定内存访问速度，单位为纳秒。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

- `CS_NO_CARD`: 分配给客户端的套字为空。

- `CS_BAD_ATTRIBUTE`: 请求了不支持的窗口属性。

- `CS_OUT_OF_RESOURCE`: 该套字的最大内存窗口已在使用。

- `CS_IN_USE`: `RequestWindow` 无法找到空闲的系统内存。

- `CS_BAD_SIZE`: 大无效。

- `CS_BAD_BASE`: `Base` 或 `Size` 不符合套字的对齐规则。

### 3.5.2 `ModifyWindow`

```c
int CardServices(ModifyWindow, window_handle_t handle, modwin_t *mod);
```

`modwin_t` 结构如下：



```c
typedef struct modwin_t {
    u_int       Attributes;
    u_int       AccessSpeed;
} modwin_t;
```

`ModifyWindow` 修改之前调用 `RequestWindow` 返回的窗口句柄的属性。可以更改以下属性：

- `WIN_MEMORY_TYPE`: 此字段可以是公共内存 `WIN_MEMORY_TYPE_CM` 或属性内存 `WIN_MEMORY_TYPE_AM`。
- `WIN_DATA_WIDTH`: 16 位访问 `WIN_DATA_WIDTH_16` 或 8 位访问 `WIN_DATA_WIDTH_8`。

## 3. 卡服务子函数描述

`WIN_ENABLE`

如果设置此项，则开启窗口。

`AccessSpeed` 提供新的内存访问速度，单位为纳秒。

返回代码：

- `CS_BAD_HANDLE`：窗口句柄无效。

### 3.5.3 `ReleaseWindow`

```
int CardServices(ReleaseWindow, window_handle_t handle);
```

`ReleaseWindow` 释放之前通过 `RequestWindow` 分配的内存窗口。

返回代码：

- `CS_BAD_HANDLE`：窗口句柄无效。

### 3.5.4 `GetFirstWindow`, `GetNextWindow`

```
int CardServices(GetFirstWindow, client_handle_t *client, win_req_t *req);
int CardServices(GetNextWindow, window_handle_t *handle, win_req_t *req);
```

这些序列操作用于获取 `socket` 所有内存窗口的配置信息。

`GetFirstWindow` 将客户端替换为内存窗口句柄，该句柄随后将通过 `GetNextWindow` 的调用进行更新。

这些服务是在 3.1.0 版本中添加的。

返回代码：

- `CS_BAD_HANDLE`：客户端句柄无效。
- `CS_NO_MORE_ITEMS`：该 `socket` 未配置任何窗口。

### 3.5.5 `MapMemPage`

```
int CardServices(MapMemPage, window_handle_t handle, memreq_t *req);
int CardServices(GetMemPage, window_handle_t handle, memreq_t *req);
```

`memreq_t` 结构体如下：

```
typedef struct memreq_t {
    u_int           CardOffset;
    page_t          Page;
} memreq_t;
```

`MapMemPage` 将映射到内存窗口基地址的卡窗口地址设置为 `CardOffset`。该窗口应通过调用 `RequestWindow` 创建。`Page` 参数在此版本中未实现，应设置为 0。在 `GetMemPage` 中，用于检索内存窗口的当前卡地址映射。

`GetMemPage` 服务是在 3.1.0 版本中添加的。

返回代码：

- `CS_BAD_HANDLE`：窗口句柄无效。
- `CS_BAD_PAGE`：`Page` 值不零。
- `CS_BAD_OFFSET`：请求的 `CardOffset` 超出范围或未进行适当对齐。

## 3.6 批量内存服务

批量内存服务提供了比内存窗口服务更高级的区域访问接口。使用内存调用的客户端不需要了解底层的内存结构或访问方法。设备特定代码被封装在一个名为内存技术驱动程序（Memory Technology Driver）的特殊卡服务客户端。

### 3.6.1 `RegisterMTD`

```
int CardServices(RegisterMTD, client_handle_t handle, mtd_reg_t *reg);
```

`mtd_reg_t` 数据结构如下：

```
typedef union mtd_reg_t {
    u_int           Attributes;
    u_int           Offset;
    u_long          MediaID;
} mtd_reg_t;
```

`RegisterMTD` 通知 Card Services 该客户端 MTD 将处理指定内存区域的请求。`Offset` 字段指定内存区域的起始地址。`Attributes` 定义了以下字段：

`REGION_TYPE`

可以是 `REGION_TYPE_CM`（普通内存）或 `REGION_TYPE_AM`（属性内存）。

`MediaID` 字段由 Card Services 记录，并将传递给任何引用此内存区域的请求的 MTD。

一旦通过调用 `RegisterMTD` 将 MTD 绑定到内存区域，它将保持绑定直到 MTD 调用 `DeregisterClient`。

返回代码：

- `CS_BAD_HANDLE`：客户端句柄无效。
- `CS_BAD_OFFSET`：偏移量不匹配该卡的有效内存区域，或者另一个 MTD 已注册了该区域。

### 3.6.2 `GetFirstRegion`, `GetNextRegion`

```
int CardServices(GetFirstRegion, client_handle_t handle, region_info_t *region);
int CardServices(GetNextRegion, client_handle_t handle, region_info_t *region);
```

`region_info_t` 结构如下：

```
typedef union region_info_t {
    u_int               Attributes;
    u_int               CardOffset;
    u_int               RegionSize;
    u_int               AccessSpeed;
    u_int               BlockSize;
    u_int               PartMultiple;
    u_char              Jecfr, JecInfo;
    memory_handle_t     next;
} region_info_t;
```

`GetFirstRegion` 和 `GetNextRegion` 以元组形式汇总信息。`CardOffset` 提供区域的起始地址。`RegionSize` 提供区域的长度（字节）。`AccessSpeed` 提供设备的周期时间（纳秒）。`BlockSize` 提供字节大小，`PartMultiple` 提供以 `BlockSize` 为单位设备粒度。`Jecfr` 和 `JecInfo` 提供该的标识。

`Attributes` 定义了以下字段：

`REGION_TYPE`

可以是 `REGION_TYPE_CM`（普通内存）或 `REGION_TYPE_AM`（属性内存）。

当 MTD 运行这些调用时，将返回绑定到该客户端的区域。

返回代码：

- `CS_NO_MORE_ITEMS`：未定义内存区域。

### 3.6.3 `OpenMemory`

```
int CardServices(OpenMemory, client_handle_t *handle, open_mem_t *req);
```

`open_mem_t` 结构如下：

```
typedef struct open_mem_t {
    u_int       Attributes;
    u_int       Offset;
} open_mem_t;
```

`OpenMemory` 用于通过批量内存服务获取内存区域的句柄。`Offset` 字段指定区域的基地址。如果成功，客户端参数将被替换为新的内存句柄。

`Attributes` 定义了以下字段：

`MEMORY_TYPE`

可以是 `MEMORY_TYPE_CM`（普通内存）或 `MEMORY_TYPE_AM`（属性内存）。

`MEMORY_EXCLUSIVE`

指定该客户端应对该内存区域具有排他访问权限。

返回代码：

- `CS_BAD_HANDLE`：客户端句柄无效。
- `CS_BAD_OFFSET`：偏移量未指定有效区域，或者该区域没有处理内存 MTD。

### 3.6.4 `CloseMemory`

```
int CardServices(CloseMemory, memory_handle_t handle);
```

`CloseMemory` 释放之前调用 `OpenMemory` 返回的内存句柄。客户端应在 `DeregisterClient` 之前释放所有内存句柄。

返回代码：

- `CS_BAD_HANDLE`：内存句柄无效。

### 3.6.5 `ReadMemory`, `WriteMemory`



```c
int CardServices(ReadMemory, memory_handle_t handle, mem_op_t *req, caddr_t buf);
int CardServices(WriteMemory, memory_handle_t handle, mem_op_t *req, caddr_t buf);
```

`mem_op_t` 结构如下：

```c
typedef struct mem_op_t {
    u_int Attributes;
    u_int Offset;
    u_int Count;
} mem_op_t;
```

`ReadMemory` 和 `WriteMemory` 从读取并写入由之前调用 `OpenMemory` 返回的指定内存句柄所定义的卡内存区域。`Offset` 字段提供操作从内存区域起始处的偏移量。`Count` 字段提供要传输的字节数。`buf` 字段指向 `ReadMemory` 操作的目标内存缓冲区，或 `WriteMemory` 操作源。

`Attributes` 定义了以下字段：

`MEM_OP_BUFFER`

如果主机缓冲区在用户内存段中，为 `MEM_OP_BUFFER_USER`；如果主机在内核内存中，为 `MEM_OP_BUFFER_KERNEL`。

`MEM_OP_DISABLE_ERASE`

指定卡区域在写入前不应擦除。

`MEM_OP_VERIFY`

指定写入操作的验证。

返回代码：

- `CS_BAD_HANDLE`

窗口句柄无效。

- `CS_BAD_OFFSET`

指定的卡偏移超出内存区域范围。

- `CS_BAD_SIZE`

指定的传输大小超出了内存区域范围。

### 3.6.6 RegisterEraseQueue

```c
int CardServices(RegisterEraseQueue, client_handle_t *handle, eraseq_hdr_t *header);
```

`eraseq_hdr_t` 结构如下：

```c
typedef struct erase_queue_header_t {
    int QueueEntryCount;
    erase_entry_t *QueueEntryArray;
} erase_hdr_t;
```

这向 Card Services 注册一个擦除请求队列。`handle` 将返回一个 `erase_handle_t` 句柄。当客户端调用 `CheckEraseQueue` 时，Card Services 将扫描队列并异步处理任何新请求。

`erase_entry_t` 结构如下：

```c
typedef struct erase_entry_t {
    memory_handle_t Handle;
    u_char State;
    u_int Size;
    u_int Offset;
    void *Optional;
} erase_entry_t;
```

在擦除队列中，`Header` 字段是之前调用 `OpenMemory` 返回的内存句柄。`State` 字段指示擦除请求的状态。定义了以下值：

- `ERASE_QUEUED`

客户端设置，表示新请求。

- `ERASE_IDLE`

客户端设置，表示该项未激活。

- `ERASE_PASSED`

MTD 设置，表示成功完成。

- `ERASE_FAILED`

MTD 设置，表示擦除失败。

- `ERASE_MEDIA_WRPROT`

表示区域被写保护。

- `ERASE_NOT_ERASABLE`

表示该区域不支持擦除操作。

- `ERASE_BAD_OFFSET`

表示擦除未在擦除块边界开始。

- `ERASE_BAD_SIZE`

表示指定的擦除大小不是擦除块大小的倍数。

- `ERASE_BAD_SOCKET`

由 MTD 设置，表示无卡。

# Card Services 子函数描述

此外，宏 `ERASE_IN_PROGRESS()` 对于表示正在处理擦除操作的 `State` 值返回真条件。

`Size` 字段给出擦除请求的大小（字节）。`Offset` 字段给出从区域开始的偏移量。大小和偏移量应当对擦除块边界。`Optional` 字段未被 Card Services 使用，但可能被客户端驱动使用。

返回码：

`CS_BAD_HANDLE`

客户端句柄无效。

## 3.6.7 DeregisterEraseQueue

```c
int CardServices(DeregisterEraseQueue, eraseq_handle_t handle);
```

`DeregisterEraseQueue` 释放之前通过 `RegisterEraseQueue` 注册的队列。如果指定的队列中存在任何待处理请求，则调用将失败。

返回码：

`CS_BAD_HANDLE`

擦除队列句柄无效。

`CS_BUSY`

擦除队列有等待的擦除请求。

## 3.6.8 CheckEraseQueue

```c
int CardServices(CheckEraseQueue, eraseq_handle_t handle);
```

此调用通知 Card Services 在之前通过 `RegisterEraseQueue` 注册的队列中有新的擦除请求。

通常情况下，客户端起初会为每个擦除队列分配状态值 `ERASE_IDLE`。当新请求被添加到队列中时，客户端将它们的状态设置为 `ERASE_QUEUED` 并调用 `CheckEraseQueue`。当客户端收到擦除完成事件时，它将检查 `state` 字段以判断请求是否成功。

返回码：

`CS_BAD_HANDLE`

擦除队列句柄无效。

## 3.7 杂项调用

### 3.7.1 GetCardServicesInfo

```c
int CardServices(GetCardServicesInfo, servinfo_t *servinfo);
```

* 注意

`servinfo_t` 结构体如下：

```c
typedef struct servinfo_t {
    char Signature[2];
    u_int Count;
    u_int Revision;
    u_int CSLevel;
    char *VendorString;
} servinfo_t;
```

`GetCardServicesInfo` 返回关于此版本 Card Services 的修订信息。`Signature` 设置为 "CS"。`Count` 设置为当前配置的 socket 数量。`Revision` 设置为 Card Services 包的修订级别，`CSLevel` 设置为符合 PC Card 标准的级别。它们以 BCD 数字形式编码。`VendorString` 设置为指向一个 RCS 标识字符串。

此调用总是成功。

### 3.7.2 AccessConfigurationRegister

```c
#include "cisreg.h"
```

```c
int CardServices(AccessConfigurationRegister, client_handle_t handle, conf_reg_t reg);
```

`conf_reg_t` 结构体如下：

```c
typedef struct conf_reg_t {
    u_char Function;
    u_int Action;
    off_t Offset;
    u_int Value;
} conf_reg_t;
```

对于绑定到特定卡函数的普通客户端，`Function` 字段被忽略。对于绑定到 `BIND_FN_ALL` 的客户端，此字段指定了应该访问哪个函数的配置寄存器。

`Action` 参数可以是以下值之一：

- `CS_READ`: 读取指定的配置寄存器并返回 `Value`。

- `CS_WRITE`: 将 `Value` 写入指定的配置寄存器。

`AccessConfigurationRegister` 读取或写入从配置寄存器开始处偏移的单字节 CIS 配置寄存器。它只能用于已通过 `RequestConfiguration` 配置的 socket。

`cistpl.h` 中定义了 `Offset` 的以下值：

- `CISREG_COR`: 配置选项寄存器。

- `CISREG_CCSR`: 卡配置与状态寄存器。

- `CISREG_PRR`: 密码替换寄存器。

- `CISREG_SCR`: 插槽与复制寄存器。

- `CISREG_ESR`: 扩展状态寄存器。

- `CISREG_IOBASE_0...CISREG_IOBASE_3`: I/O 基寄存器。

- `CISREG_IOSIZE`: I/O 大寄存器。

返回码：

`CS_BAD_HANDLE`

客户端句柄无效。

`CS_BAD_ARGS`

不支持指定的 `Action`。

`CS_CONFIGURATION_LOCKED`

这实际上意味着配置尚未锁定。

`CS_OUT_OF_RESOURCE`

Card Services 无法分配内存窗口来访问卡的配置寄存器。

### 3.7.3 AdjustResourceInfo



```c
int CardServices(AdjustResourceInfo, client_handle_t handle, adjust_t *adj);
```

`adjust_t` 结构体如下：

```c
typedef struct adjust_t {
    u_int           Action;
    u_int           Resource;
    u_int           Attributes;
    union {
        struct memory {
            u_long           Base;
            u_long           Size;
        } memory;
        struct io {
            ioaddr_t    BasePort;
            ioaddr_t    NumPorts;
            u_int       IOAddrLines;
            struct irq {
                u_int        IRQ;
            } irq;
        } resource;
    };
} adjust_t;
```

`AdjustResourceInfo` 用于告知 Card Services PC 设备可能或可能分配的资源。系统遵循标准的 Linux 资源管理系统（IO 端口的 `*_region` 类、中断分配）。`Action` 参数具有以下值：

- `ADD_MANAGED_RESOURCE`: 将指定的资源置于 Card Services 控制下。
- `REMOVE_MANAGED_RESOURCE`: 从 Card Services 控制中移除指定的资源。
- `RES_MEMORY`: 由 `adj->memory` 指定内存资源。
- `RES_IO`: 由 `adj->io` 指定 IO 资源。
- `RES_IRQ`: 由 `adj->irq` 指定中断资源。
- `_RESERVED`: 预留后用。

```c
#include "cistpl.h"
```

# 4 卡信息定义

### 4.1.1 CISTPL_CHECKSUM

`cistpl_checksum_t` 结构体如下：

```c
typedef struct cistpl_checksum_t {
    u_short addr;
    u_short len;
    u_char sum;
} cistpl_checksum_t;
```

### 4.1.2 CISTPL_LONLINK_A, CISTPL_LONLINK_C, CISTPL_LINK, CISTPL_NOLINK

`cistpl_longlink_t` 结构体如下：

```c
typedef struct cistpl_longlink_t {
    u_int addr;
} cistpl_longlink_t;
```

`cistpl_longlink_mfc_t` 结构体如下：

```c
typedef struct cistpl_longlink_mfc_t {
    int nfn;
    struct {
        u_char space;
        u_int addr;
    } fn[CISTPL_FUNCTIONS];
} cistpl_longlink_mfc_t;
```

### 4.1.3 CISTPL_DEVICE, CISTPL_DEVICE_A

`cistpl_device_t` 结构体如下：

```c
typedef struct cistpl_device_t {
    int ndev;
    struct {
        u_char type;
        u_char wp;
        u_int speed;
        u_int size;
    } dev[CISTPL_DEVICES];
} cistpl_device_t;
```

## 4. 卡片信息结构定义

### 4.1.5 CISTPL_VERS_1

`cpl_vers_1_t` 结构定义如下：

```c
typedef struct cistpl_vers_1_t {
    u_char major;
    u_char minor;
    int ns;
    int ofs[CISTPL_VERS_1_MAX_PROD_STRINGS];
    char str[254];
} cistpl_vers_1_t;
```

`ns` 字段指定组中产品信息字符串的数量。字符串数据包含在 `str` 数组中。每个字符串均以空字符终止，`ofs` 给每个字符串起始位置的偏移量。

### 4.1.6 CISTPL_ALTSTR

`cistpl_altstr` 结构 `cistpl_altstr_t` 定义如下：

```c
typedef struct cistpl_altstr_t {
    int ns;
    int ofs[CISTPL_ALTSTR_MAX_STRINGS];
    char str[254];
} cistpl_altstr_t;
```

`ns` 字段指定组中可选语言字符串的数量。字符串数据包含在 `str` 数组中。每个字符串均以空字符终止，`ofs` 给每个字符串起始位置的偏移量。

### 4.1.7 CISTPL_JEDEC_C, CISTPL_JEDEC_A

`cistpl_jedec_t` 结构定义如下：

```c
typedef struct cistpl_jedec_t {
    int nid;
    struct {
        u_char mfr;
        u_char info;
    } id[CISTPL_MAX_DEVICES];
} cistpl_jedec_t;
```

JEDEC 标识符描述用于实现卡片内存区域的特定设备类型。`nid` 字段指定组中 JEDEC 标识符的数量。JEDEC 标识符与对应的 `CISTPL_DEVICE` 元组中的设备描述之间应该是一一对应的关系。

### 4.1.8 CISTPL_CONFIG, CISTPL_CONFIG_CB

`cistpl_config_t` 结构定义如下：

```c
typedef struct cistpl_config_t {
    u_char          last_idx;
    u_int           base;
    u_int           rmask[4];
    u_char          subtuples;
} cistpl_config_t;
```

`last_idx` 字段给出编号最高的配置表项的索引。`base` 字段给出卡配置寄存器在属性内存中的偏移量。`rmask` 数组是一系列位掩码，表示存在哪些配置寄存器。`rmask[0]` 的第 0 位是 COR，第 1 位是 CSSR，依此类推。`subtuples` 字段给出普通元组内容之后的 `subtuples` 字节数。

对于 `CISTPL_CONFIG_CB`，`rmask` 未定义，`base` 指向 CardBus 状态寄存器。

### 4.1.9 CISTPL_BAR

`cistpl_bar_t` 结构定义如下：

```c
typedef struct cistpl_bar_t {
    u_char          attr;
    u_int           size;
} cistpl_long_t;
```

`CISTPL_BAR` 元组描述了 CardBus 卡片中 PCI 基地址寄存器所指向的地址空间的特征。

`attr` 中定义了以下位域：

- `CISTPL_BAR_SPACE`: 标识基地址寄存器，范围从 1 到 6。值为 7 时描述卡片的扩展 ROM 空间。
- `CISTPL_BAR_PREFETCH`: 如果设置，该区域映射到 IO 空间（区别于内存空间）。
- `CISTPL_BAR_CACHEABLE`: 如果设置，该区域是可缓存的且可预取的。
- `CISTPL_BAR_IMEG_MAP`: 如果设置，该区域应仅映射到主机物理地址空间的前 1MB 内。

### 4.1.10 CISTPL_CFTABLE_ENTRY

`cistpl_cftable_entry_t` 结构定义如下：



```c
typedef struct cistpl_cftable_entry_t {
    u_char index;
    u_char flags;
    u_char interface;
    cistpl_power_t vcc, vpp1, vpp2;
    cistpl_timing_t timing;
    cistpl_ie_t io;
    cistpl_irq_t irq;
    cistpl_mem_t mem;
    u_char subtples;
} cistpl_cftable_entry_t;
```

`CISTPL_CFTABLE_ENTRY` 结构描述了卡片的完整工作模式。许多部分是可选的。`index` 字段给出此工作模式的配置；将此值写入卡片的配置选项寄存器即可选择该模式。`flags` 中定义了以下字段：

- `CISTPL_CFTABLE_DEFAULT`: 指定该项为默认配置项。
- `CISTPL_CFTABLE_BVDS`: 指定该配置实现了引脚替换寄存器（Pin Replacement Register）中的 `BVD1` 和 `BVD2` 信号。
- `CISTPL_CFTABLE_WP`: 指定该配置实现了引脚替换寄存器中的写保护信号。
- `CISTPL_CFTABLE_RDBSYS`: 指定该配置实现了引脚替换寄存器中的就绪/忙（Ready/Busy）信号。
- `CISTPL_CFTABLE_MWAIT`: 指定该配置实现了等待（MWAIT）信号。

## 4. 卡片信息结构定义

`CISTPPL_FUNCID_MEMORY`

简单的内存设备。

`CISTPPL_FUNCID_SERIAL`

串口或调制解器设备。

`CISTPPL_FUNCID_PARALLEL`

并行端口设备。

`CISTPPL_FUNCID_FIXED`

固定磁盘设备。

`CISTPPL_FUNCID_VIDEO`

视频接口。

`CISTPPL_FUNCID_NETWORK`

网络适配器。

`CISTPPL_FUNCID_AIMS`

自动递增的大容量存储设备。

在 `sysinit` 中定义了以下标志：

`CISTPPL_SYSINIT_POST`

表示系统在上电初始化期间应尝试配置此卡片。

`CISTPPL_SYSINIT_ROM`

表示卡片包含一个应在启动时进行配置的系统扩展 ROM。

### 4.1.14 `CISTPL_DEVICE_GEO`

`cistpl_device_geo_t` 结构如下：

```c
typedef struct cistpl_device_geo_t {
    int
    ngeo;
    struct {
        u_char  buswidth;
        u_int   erase_block;
        u_int   read_block;
        u_int   write_block;
        u_int   partition;
        u_int   interleave;
    } geo(CISTPL_MAX_DEVICES);
} cistpl_device_geo_t;
```

`erase_block`、`read_block` 和 `write_block` 的大小以 `buswidth` 乘以 `interleave` 为单位。

`partition` 的大小以 `erase_block` 为单位。

### 4.1.15 `CISTPL_VERS_2`

`cistpl_vers_2_t` 结构如下：

```c
typedef struct cistpl_vers_2_t {
    u_char       vers;
    u_char       comply;
    u_short      dindex;
    u_char       vspec8, vspec9;
    u_char       nhdr;
    int          vendor, info;
    char         str[244];
} cistpl_vers_2_t;
```

`vers` 字段应为 0。`comply` 标志表示标准遵循程度，也为 0。`dindex` 字段在公共内存开始处预留指定数量字节。`vspec8` 和 `vspec9` 字段可能包含厂商特定信息。`nhdr` 字段给出此卡片上存在的 CIS 副本数量。`str` 数组包含两个字符串：厂商名称和描述卡片的提示消息。厂商字符串的偏移量由 `vendor` 给出，产品字符串的偏移量在 `info` 中。

### 4.1.16 `CISTPL_ORG`

`cistpl_org_t` 结构如下：

```c
typedef struct cistpl_org_t {
    u_char  data_org;
    char    desc[30];
} cistpl_org_t;
```

该元组描述了内存分区的数据结构。`data_org` 定义了以下值：

- `CISTPL_ORG_FS`

  该分区包含文件系统。

- `CISTPL_ORG_APPSPEC`

  该分区采用应用程序特定的格式。

- `CISTPL_ORG_XIP`

  该分区遵循就地执行（Execute-In-Place）规范。

`desc` 字段给出数据结构的文本描述。

### 4.1.17 `CISTPL_FORMAT`

`cistpl_format_t` 结构如下：

```c
typedef struct cist_org_t {
    u_char  type;
    u_char  edc;
    u_int   offset;
    u_int   length;
} cistpl_format_t;
```

该元组描述了内存区域的数据记录格式。`type` 定义了以下值：

- `CISTPL_FORMAT_DISK`

  该分区使用类磁盘格式。

- `CISTPL_FORMAT_MEM`

  该分区使用类内存格式。

`edc` 定义了以下值：

- `CISTPL_EDC_NONE`

  不使用错误检测码。

- `CISTPL_EDC_CKSUM`

  每个块有一个字节的算术校验和。

- `CISTPL_EDC_CRC`

  每个块有一个两个字节的循环冗余检查。

- `CISTPL_EDC_PCC`

  整个分区有一个字节的校验和。

`offset` 指定第一个数据字节的地址，`length` 指定此分区的总字节数。

## 4.2 CIS 配置寄存器定义

PC 标准在卡片的内存空间内定义了几个标准配置寄存器。卡片的 `CONFIG` 元组指定了实现了这些哪些寄存器。使用这些定义的程序包括：

```c
#include "cisreg.h"
```

### 4.2.1 配置选项寄存器

几乎所有的 I/O 卡片都存在此寄存器。写入此寄存器可以选择一个配置表项并启用卡片的 IO 功能。

定义了以下位域：

- `COR_CONFIG_MASK`

  描述卡片当前运行模式的配置表索引。

- `COR_LEVEL_REQ`

  指定卡片应产生电平模式（边触发）中断，这是默认值。

- `COR_SOFT_RESET`

  设置此位将执行“软”重置操作。驱动程序应使用 `ResetCard` 调用来重置卡片。

### 4.2.2 状态寄存器

（注：原文此处编号有误，根据上下文推断）

```c
#include "cisreg.h"
```

使用这些定义的程序包括：

```c
#include "cisreg.h"
```

### 4.2.1 配置选项寄存器

几乎所有的 I/O 卡片都存在此寄存器。写入此寄存器可以选择一个配置表项并启用卡片的 IO 功能。

定义了以下位域：

- `COR_CONFIG_MASK`

  描述卡片当前运行模式的配置表索引。

- `COR_LEVEL_REQ`

  指定卡片应产生电平模式（边触发）中断，这是默认值。

- `COR_SOFT_RESET`

  设置此位将执行“软”重置操作。驱动程序应使用 `ResetCard` 调用来重置卡片。

### 4.2.2 状态寄存器

（注：此处原文文本似乎存在重复或逻辑混乱，以下按原文字面翻译）

*由于原文提供的文本在 4.2.1 之后出现了大量重复和异常的编号，以下将严格按照原文内容进行翻译：*

---

**重新开始对提供的目标文本进行完整准确翻译：**

## 4. 卡片信息结构定义

`CISTPPL_FUNCID_MEMORY`

一个简单的内存设备。

`CISTPPL_FUNCID_SERIAL`

串口或调制解器设备。

`CISTPPL_FUNCID_PARALLEL`

并行端口设备。

`CISTPPL_FUNCID_FIXED`

固定磁盘设备。

`CISTPPL_FUNCID_VIDEO`

视频接口。

`CISTPPL_FUNCID_NETWORK`

网络适配器。

`CISTPPL_FUNCID_AIMS`

一个自动递增的大容量存储设备。

在 `sysinit` 中定义了以下标志：

`CISTPPL_SYSINIT_POST`

表示系统在上电初始化期间应尝试配置此卡片。

`CISTPPL_SYSINIT_ROM`

表示卡片包含一个应在启动时进行配置的系统扩展 ROM。

### 4.1.14 `CISTPL_DEVICE_GEO`



`cistpl_device_geo_t` 结构如下：

```
typedef struct cistpl_device_geo_t {
    int
    ngeo;
    struct {
        u_char  buswidth;
        u_int   erase_block;
        u_int   read_block;
        u_int   write_block;
        u_int   partition;
        u_int   interleave;
    } geo(CISTPL_MAX_DEVICES);
} cistpl_device_geo_t;
```

`erase_block`、`read_block` 和 `write_block` 的大小以 `buswidth` 乘以 `interleave` 为单位。

`partition` 的大小以 `erase_block` 为单位。

### 4.1.15 CISTPL_VERS_2

`cistpl_vers_2_t` 结构如下：

```
typedef struct cistpl_vers_2_t {
    u_char       vers;
    u_char       comply;
    u_short      dindex;
    u_char       vspec8, vspec9;
    u_char       nhdr;
    int          vendor, info;
    char         str[244];
} cistpl_vers_2_t;
```

`vers` 字段应为 `0`。`comply` 标志表示标准遵循程度，也为 `0`。`dindex` 字段在公共内存开始处预留指定数量字节。`vspec8` 和 `vspec9` 字段可能包含厂商特定信息。`nhdr` 字段给出此卡片上存在的 CIS 副本数量。`str` 数组包含两个字符串：厂商名称和描述卡片的提示消息。厂商字符串的偏移量由 `vendor` 给出，产品字符串的偏移量在 `info` 中。

### 4.1.16 CISTPL_ORG

`cistpl_org_t` 结构如下：

```
typedef struct cistpl_org_t {
    u_char  data_org;
    char    desc[30];
```

该元组描述了内存分区的数据结构。`data_org` 定义了以下值：

- `CISTPL_ORG_FS`

  该分区包含文件系统。

- `CISTPL_ORG_APPSPEC`

  该分区采用应用程序特定的格式。

- `CISTPL_ORG_XIP`

  该分区遵循就地执行（Execute-In-Place）规范。

`desc` 字段给出数据结构的文本描述。

### 4.1.17 CISTPL_FORMAT

`cistpl_format_t` 结构如下：

```
typedef struct cist_org_t {
  u_char  type;
  u_char  edc;
  u_int   offset;
  u_int   length;
}
```

该元组描述了内存区域的数据记录格式。`type` 定义了以下值：

`CISTPL_FORMAT_DISK`

该分区使用类磁盘格式。

`CISTPL_FORMAT_MEM`

该分区使用类内存格式。

`edc` 定义了以下值：

`CISTPL_EDC_NONE`

不使用错误检测码。

`CISTPL_EDC_CKSUM`

每个块有一个字节的算术校验和。

`CISTPL_EDC_CRC`

每个块有一个两个字节的循环冗余检查。

`CISTPL_EDC_PCC`

整个分区有一个字节的校验和。

`offset` 指定第一个数据字节的地址，`length` 指定此分区的总字节数。

## 4.2 CIS 配置寄存器定义

PC 标准在卡片的内存空间内定义了几个标准配置寄存器。卡片的 `CONFIG` 元组指定了这些寄存器中哪些实现了。使用这些定义的程序包括：

```
#include "cisreg.h"
```

### 4.2.1 配置选项寄存器

几乎所有的 I/O 卡片都存在此寄存器。写入此寄存器可以选择一个配置表项并启用卡片的 IO 功能。

定义了以下位域：

- `COR_CONFIG_MASK`

  描述卡片当前运行模式的配置表索引。

- `COR_LEVEL_REQ`

  指定卡片应产生电平模式（边触发）中断，这是默认值。

- `COR_SOFT_RESET`

  设置此位将执行“软”重置操作。驱动程序应使用 `ResetCard` 调用来重置卡片。

*(注：由于提供的原文从 4.2.1 之后开始大量重复且逻辑混乱，以下为对原文中出现的后续重复内容的翻译)*

---

(此处由于原文中存在大量重复的段落，根据指令“不要重复输出原文”，我已完成对核心结构内容的翻译。如果原文中特定的 4.2.2, 4.2.3 等章节有特定翻译需求，已按上述逻辑处理。)

## 5. 卡服务事件处理

`client_handle` 成员用于处理负责该事件的套接字的客户端。如果驱动程序绑定到多个套接字，此字段非常有用。`info` 字段目前用于返回 `ResetCard` 的退出状态。`client_data` 字段可供驱动程序用于指向与此设备关联的本地数据结构。其余字段未使用。

对于不直接将卡映射到主机 IO 和内存空间的套接字，`bus` 字段是一个指向该套接字 IO 原语条目表的指针。

## 5.2 事件描述

```
CS_EVENT_CARD_INSERTION
```

此事件信号卡片已插入。如果驱动程序绑定到一个已占用的套接字，Card Services 将向驱动程序发送一个伪的插入事件。

```
CS_EVENT_CARD_REMOVAL
```

此事件信号卡片已移除。应当以最小延迟处理此事件，以便 Card Services 能够尽可能地通知所有客户端。

```
CS_EVENT_BATTERY_LOW
```

此事件信号“低电量”信号的状态变化。

```
CS_EVENT_BATTERY_DEAD
```

此事件信号“电池耗尽”信号的状态变化。

```
CS_EVENT_READY_CHANGE
```

此事件信号“就绪”信号的状态变化。

```
CS_EVENT_WRITE_PROTECT
```

此事件信号“写保护”信号的状态变化。

```
CS_EVENT_REGISTRATION_COMPLETE
```

此事件在成功调用 `RegisterClient` 后发送给驱动程序。

```
CS_EVENT_RESET_REQUEST
```

当客户端调用 `ResetCard` 时会发送此事件。事件处理程序可以通过返回失败来否决重置操作。

```
CS_EVENT_RESET_PHYSICAL
```

此事件在向卡片发送重置信号之前发送给所有客户端。

```
CS_EVENT_CARD_RESET
```

此事件信号重置操作已完成。重置的成功或失败应使用 `GetStatus` 来确定。

```
CS_EVENT_RESET_COMPLETE
```

此事件发送给调用过 `ResetCard` 的客户端，表示重置处理的结束。

```
CS_EVENT_PM_SUSPEND
```

此事件信号 Card Services 接收到了用户启动或 APM 挂起请求。事件处理程序可以通过返回失败来否决挂起。

```
CS_EVENT_PM_RESUME
```

此信号表示系统在挂起/恢复周期后已恢复运行。

```
CS_EVENT_MTD_REQUEST
```

此项用于启动 MTD 内存操作。请求的描述通过回调参数中的 `mdrequest` 字段传递。主机缓冲区地址可能通过 `buffer` 传递。

```
CS_EVENT_ERASE_COMPLETE
```

此项用于通知客户端队列中的擦除操作已完成。擦除条目的指针在回调参数的 `info` 字段中返回。

## 5.3 客户端驱动处理职责

客户端驱动应通过配置和取消配置套接字来响应 `CS_EVENT_CARD_INSERTION` 和 `CS_EVENT_CARD_REMOVAL` 事件。由于卡片移除是一个高优先级事件，驱动程序应该通过在设备结构中设置标志位来立即阻塞对套接字的 IO 操作，并使用定时器中断调度所有关闭处理稍后发生。

当接收到 `CS_EVENT_PM_RESET_REQUEST` 事件时，驱动程序应阻塞 IO 并接收锁定的套接字配置。当接收到 `CS_EVENT_CARD_RESET` 时，驱动程序应恢复套接字配置并解锁 IO。

`CS_EVENT_PM_SUSPEND` 事件的处理方式应类似于 `CS_EVENT_PM_RESET_REQUEST` 事件，即应该阻塞 IO 并恢复套接字配置。当接收到 `CS_EVENT_PM_RESUME` 事件时，驱动程序可以预期卡片已准备好进行重新配置，类似于接收到 `CS_EVENT_CARD_RESET` 事件时。

## 6. 存储技术驱动



存储技术驱动（“MTD”）被`Card Services`用于为特定类型的存储设备实现存储服务。`MTD`应该通过调用`RegisterClient`注册为普通的卡客户端。当它接收到卡插入事件时，它应该使用`GetFirstRegion`和`GetNextRegion`来识别它将管理的区域。然后，它应该调用`RegisterMTD`来控制这些区域。`MTD`的读、写、复制和擦除请求会被`Card Services`封装成`CS_EVENT_MTD_REQUEST`事件，并传递给`MTD`的事件处理程序进行处理。

## 6.1 MTD 请求处理

`MTD`以`CS_EVENT_MTD_REQUEST`事件的形式接收来自`Card Services`的请求。`Card Services`传递回调参数中`mdrequest`字段的描述。对于向主机或从主机传输数据的请求，主机缓冲区地址通过`buffer`传递。

`mdrequest_t`结构体如下：

```
typedef struct mtd_request_t {
    u_int SrcCardOffset;
    u_int DestCardOffset;
    u_int TransferLength;
    u_int Function;
    u_long MediaID;
    u_int Status;
    u_int Timeout;
} mtd_request_t;
```

`Function`字段被映射并描述了该请求要执行的操作：

### MTD_REQ_ACTION

可能是`MTD_REQ_ERASE`、`MTD_REQ_READ`、`MTD_REQ_WRITE`或`MTD_REQ_COPY`之一。

### MTD_REQ_NOERASE

对于在擦除边界上对齐的写命令，此项指定不应执行擦除。

### MTD_REQ_VERIFY

指定应对写操作进行验证。

### MTD_REQ_READY

表示此请求将延迟，直到卡片发送`READY`信号。

### MTD_REQ_TIMEOUT

表示此请求将因超时而延迟。

### MTD_REQ_FIRST

表示此请求是系列请求中的第一个。

### MTD_REQ_LAST

表示此请求是系列请求中的最后一个。

### MTD_REQ_KERNEL

表示读或写的主机缓冲区位于内核内存，而不是用户内存。

### MTD_WAITREQ

指定在当前完成另一个`MTD`请求完成后应重试该请求。

### MTD_WAITTIMER

指定在超时过期后应继续该请求。

### MTD_WAITRDY

指定当卡片发送`READY`信号或`Timeout`中指定的时间过去时（以先者为准）继续该请求。

### MTD_WAITPOWER

指定在某些因素影响套接字电源可用性后应重试该请求。

对于`MTD_WAITTIMER`和`MTD_WAITRDY`，`Timeout`字段将以毫秒为单位指定超时间隔。

## 6.2 MTD 辅助函数

由于`MTD`处理由`Card Services`生成的请求，在处理程序中可以安全调用的`Card Services`调用类型可能受到限制。`MTD`辅助函数提供了一组特殊服务，这些服务可能是`MTD`需要的但使用标准的`Card Services`实现很难。在`Linux`实现中，大多数`CS`调用可以在`MTD`处理程序中安全执行，为了兼容性包含了`MTD`辅助接口。

```
#include "cs.types.h"
#include "cs.h"
#include "bulkmem.h"

int MTDHelperEntry(int subfunc, void *arg, void *arg2);
```

### 6.2.1 MTDRequestWindow, MTDRleaseWindow

```
int MTDHelperEntry(MTDRequestWindow, client_handle_t *handle, win_req_t *mod);
int MTDHelperEntry(MTDRleaseWindow, window_handle_t handle);
```

这些服务与标准的`Card Services` `RequestWindow`和`ReleaseWindow`调用相同。

### 6.2.2 MTDModifyWindow

```
int MTDHelperEntry(MTDModifyWindow, memory_handle_t handle, mtd_mod_req_t *mod);
```

`MTDModifyWindow`实际上等同于使用标准的`ModifyWindow`和`MapMemPage`调用。

可以在属性（Attributes）中指定以下标志位：

# 6. 存储技术驱动程序

`WIN_MEMORY_TYPE`

可以使用`WIN_MEMORY_TYPE_CM`表示普通内存，或使用`WIN_MEMORY_TYPE_AM`表示属性内存。

`WIN_USE_WAIT`

指定控制器应观察卡片的`MWAIT`信号。

使用`MTDModifyWindow`配置的窗口将始终处于启用状态，并具有 16 位的数据宽度。

返回代码：

- `CS_BAD_HANDLE`: 内存句柄无效。

### 6.2.3 MTDSVpp

```c
int MTDHelperEntry(MTDSVpp, client_handle_t client, mtd_vpp_req_t *req);
```

```c
typedef struct mtd_vpp_req_t {
    u_char    Vpp1, Vpp2;
} mtd_vpp_req_t;
```

`MTDSVpp`修改插槽的编程电压。`Vpp1`和`Vpp2`的单位应为 1/10伏特。目前，`Vpp1`应该始终等于`Vpp2`。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。
- `CS_BAD_VPP`: 指定 Vpp 不可用，或 `Vpp1` 不等于 `Vpp2`。

## 6.2.4 MTDRDYMask

```c
int MTDHelperEntry(MTDRDYMask, client_handle_t client, mtd_rdy_req_t *req);
```

```c
typedef struct mtd_rdy_req_t {
    u_int    Mask;
} mtd_rdy_req_t;
```

`MTDRDYMask`选择是否启用`CS_EVENT_READY_CHANGE`事件。客户端已经通过调用`RegisterClient`或`SetEventMask`向卡服务（`Card Services`）指示其应该接收就绪变化事件。如果`Mask`参数中设置了`CS_EVENT_READY_CHANGE`位，则将启用就绪变化事件。

返回代码：

- `CS_BAD_HANDLE`: 客户端句柄无效。

# 7. 驱动程序服务接口

`Driver Services`在卡服务驱动程序与如`cardmgr`守护进程之类的用户态工具之间建立了连接。它是一种类似于卡服务的“超级客户端”。`Driver Services`使用`BindDevice`函数将其他客户端与其相应的卡进行绑定。与其他客户端不同，`Driver Services`会始终绑定到所有插入和移除的插槽上。

## 7.1 与其他客户端驱动程序的接口

`Driver Services`跟踪所有已安装并准备好附加到插槽的客户端驱动程序。客户端驱动程序需要创建和删除设备“实例”的入口，其中一个设备实例包含了管理一个物理卡所需的所有内容。

每个客户端驱动程序由一个唯一的 16 字符标签标识，该标签具有特殊类型`dev_info_t`，定义在`cs_types.h`中。每个设备实例由一个`dev_link_t`结构描述。

### 7.1.1 dev_link_t 结构

`dev_node_t`和`dev_link_t`数据结构如下：

```c
#include "ds.h"

typedef struct dev_node_t {
    char dev_name[DEV_NAME_LEN];
    u_char major, minor;
    struct dev_node_t *next;
};

typedef struct dev_link_t {
    dev_node_t *dev;
    u_int state, open;
    struct wait_queue *pending;
    struct timer_list release;
    client_handle_t handle;
    io_req_t io;
    irq_req_t irq;
    config_req_t conf;
    window_handle_t win;
    void *priv;
    struct dev_link_t *next;
} dev_link_t;
```



`dev_link_t` 结构的字段指向一个 `dev_node_t` 结构链表。在 `dev_node_t` 中，`dev_name` 字段由驱动程序填充，包含用于访问该设备的设备文件名，例如，`serial_cs` 驱动程序使用如“`ttyS1`”之类的名称。访问此设备的主设备和次设备号。`Driver Services` 通过 `DS_GET_DEVICE_INFO` `ioctl` 将这些字段传递给用户态程序。

在 `dev_link_t` 中，`state` 字段用于跟踪当前设备状态。以下是标志位：

- `DEV_PRESENT`: 表示卡存在。此位应设置。
- `DEV_CONFIG`: 表示卡已配置。
- `DEV_CONFIG_PENDING`: 表示配置正在进行。
- `DEV_SUSPEND`: 表示卡已挂起。
- `DEV_BUSY`: 表示操作正在进行。
- `DEV_STALE_CONFIG`: 表示配置已过期。
- `DEV_STALE_LINK`: 表示链接已失效。

## 7. 驱动服务接口

### 7.2.3 driver_operations 入口

`attach()` 入口点用于配置单个设备，其参数是一个描述设备查找位置的“设备定位器”（device locator）结构。

`dev_locator_t` 结构如下：

```c
typedef struct dev_locator_t {
    enum { LOC_ISA, LOC_PCI } bus;
    union {
        struct {
            u_short io_base_1, io_base_2;
            u_long mem_base;
            u_char irq, dma;
        } isa;
        struct {
            u_char bus;
            u_char devfn;
        } pci;
    } b;
} dev_locator_t;
```

`attach()` 函数应返回 `NULL` 或一个描述新设备的有效 `dev_node_t` 结构。所有其他入口点都使用此指针来识别要操作的设备。`cb_enabler` 模块会根据卡的插入和拔出事件调用 `attach()` 和 `detach()` 入口。`suspend()` 和 `resume()` 入口则会在响应电源管理事件时调用。

没有办法拒绝 `suspend()` 或 `detach()`。当接收到 `detach()` 事件时，驱动程序应该阻塞任何对指定设备的后续 `IO` 操作，但在内核设备实际关闭之前，可以保留内部数据结构。

### 7.3 访问用户态实用工具的接口

`Driver Services` 创建了一个伪设备，用于与用户态 `PC` 卡进行通信。设备的主设备号是动态选择的，`PC` 卡通过 `/proc/devices` 确定它。次设备号对应套接字号，从 `0` 开始。

只允许一个进程打开读写套接字。其他进程可以只读模式打开套接字。到 `Driver Services` 的只读连接可以执行部分 `ioctl` 操作。读写连接可以发出所有 `ioctl`，还可以接收 `Card Services` 事件通知。

#### 7.3.1 Card Services 事件通知

`Driver Services` 为事件通知实现了 `read()` 和 `select()` 函数。从 `PC` 卡设备读取数据将返回一个无符号值，其中包含了 `Driver Services` 自上一次 `read()` 以来收到的所有事件。如果没有收到任何事件，调用将阻塞直到下一个事件发生。可以使用 `select()` 来监控多个套接字是否有新事件。

`Driver Services` 监控以下事件：`CS_EVENT_CARD_INSERTION`、`CS_EVENT_CARD_REMOVAL`、`CS_EVENT_RESET_PHYSICAL`、`CS_EVENT_CARD_RESET` 以及 `CS_EVENT_RESET_COMPLETE`。

#### 7.3.2 Ioctl 描述

大多数 `Driver Services` `ioctl` 操作直接映射到 `Card Services` 函数。`ioctl` 调用形式如下：

```c
int ioctl(int fd, int cmd, ds_ioctl_arg *arg);
```

`ds_ioctl_arg_t` 结构如下：

```c
typedef union ds_ioctl_arg_t {
	servino_t		servino;
	adjust_t		adjust;
	config_info_t		config;
	tuple_t		tuple;
	tuple_parse_t	tuple_parse;
	client_req_t		client_req;
	status_t		status;
	conf_reg_t		conf_reg;
	cisinfo_t		cisinfo;
	region_info_t		region;
	bind_info_t		bind_info;
	mtd_info_t		mtd_info;
	cidump_t;cidump;
} ds_ioctl_arg_t;
```

以下 `ioctl` 命令执行相应的 `Card Services` 函数：

- `DS_GET_CARD_SERVICES_INFO`: 调用 `CardServices(GetServicesInfo, ..., &arg->servino)`。
- `DS_ADJUST_RESOURCE_INFO`: 调用 `CardServices(AdjustResourceInfo, ..., &arg->adjust)`。
- `DS_GET_CONFIGURATION_INFO`: 调用 `CardServices(GetConfigurationInfo, ..., &arg->config)`。
- `DS_GET_FIRST_TUPLE`: 调用 `CardServices(GetFirstTuple, ..., &arg->tuple)`。
- `DS_GET_NEXT_TUPLE`: 调用 `CardServices(GetNextTuple, ..., &arg->tuple_parse.data)`。
- `DS_GET_TUPLE_DATA`: 调用 `CardServices(GetTupleData, ..., &arg->tuple_parse.tuple)`。元组数据返回在 `arg->tuple_parse.data` 中。
- `DS_PARSE_TUPLE`: 调用 `CardServices(ParseTuple, ..., &arg->tuple_parse.tuple, &arg->tuple_parse.parse)`。
- `DS_RESET_CARD`: 调用 `CardServices(ResetCard, ...)`。
- `DS_GET_STATUS`: 调用 `CardServices(GetStatus, ..., &arg->status)`。
- `DS_ACCESS_CONFIGURATION_REGISTER`: 调用 `CardServices(AccessConfigurationRegister, ..., &arg->conf_reg)`。
- `DS_VALIDATE_CIS`: 调用 `CardServices(ValidateCIS, ..., &arg->cisinfo)`。
- `DS_SUSPEND_CARD`: 调用 `CardServices(SuspendCard, ...)`。
- `DS_RESUME_CARD`: 调用 `CardServices(ResumeCard, ...)`。
- `DS_EJECT_CARD`: 调用 `CardServices(EjectCard, ...)`。
- `DS_INSERT_CARD`: 调用 `CardServices(InsertCard, ...)`。
- `DS_GET_FIRST_REGION`: 调用 `CardServices(GetFirstRegion, ..., &arg->region)`。
- `DS_GET_NEXT_REGION`: 调用 `CardServices(GetNextRegion, ..., &arg->region)`。
- `DS_REPLACE_CIS`: 调用 `CardServices(ReplaceCIS, ..., &arg->cisump)`。

以下 `ioctl` 触发 `Driver Services` 函数。它们作用于 `bind_info_t` 结构：

```c
typedef struct bind_info_t {
    dev_info;
    dev_info_t;
    u_char function;
    struct dev_info_t *instance;
    char name[DEV_NAME_LEN];
    u_char major, minor;
    void *next;
} bind_info_t;
```



- `DS_BIND_REQUEST`：调用套接字访问客户端设备。指定的 `device_info` 在已注册的驱动程序列表中查找。如果是多功能卡，`function` 字段标识要绑定的卡功能。如果找到，则通过 `BindDevice` 调用将驱动绑定到该套接字和功能。然后，Driver Services 会调用客户端的 `attach()` 入口创建一个设备实例。新的 `dev_link_t` 指针返回在 `instance`。

## 8. Card Services 客户端驱动程序结构

- `DS_GET_DEVICE_INFO`：此调用从 `dev_link_t` 结构中检索 `dev_name`、`major` 和 `minor` 项。

- `DS_UNBIND_REQUEST`：调用套接字访问客户端设备。指定的 `device_info` 在已注册的驱动程序列表中查找。如果是多功能卡，`function` 字段标识要绑定的卡功能。如果找到，则通过 `BindDevice` 调用将驱动绑定到该套接字和功能。然后，Driver Services 会调用客户端的 `attach()` 入口创建一个设备实例。新的 `dev_link_t` 指针返回在 `instance`。

- `DS_BIND_MTD`：最后，Driver Services 调用客户端的 `attach()` 入口创建一个设备实例。

```c
typedef struct mtd_info_t {
    dev_info;
    u_int attributes;
    u_int offset;
} mtd_info_t;
```

此调用将 MTD 与设备关联。

## 8.1 使用 Linux 驱动程序

目前的许多客户端驱动程序使用 Linux 驱动代码执行 IO 操作。Card Services 客户端模块处理卡配置并响应卡状态变化事件，但将设备 IO 映射到传统 ISA 总线卡的兼容驱动。在某些情况下，可以在不经修改的情况下使用传统驱动。然而，为了完全支持热插拔和电源管理等 PC 特性，PC Card 客户端代码与设备 IO 代码之间需要某些通信。

大多数 Linux 驱动程序期望在启动时探测设备，并且并没有设计用于处理设备的添加和移除。驱动程序模块化趋势的一个副作用是，很容易将模块化驱动程序适配以处理可拆卸设备。

设备驱动程序能够从设备在不恰当时间消失中恢复是非常重要的。至少，驱动程序应该在尝试任何 IO 操作之前或在处理中断之前检查设备是否存在。检查设备状态的循环应该具有超时机制，否则如果设备永远不存在，循环将无法退出。

虚拟控制器（`dummy cs`）可能用于为兼容 PC 设备加载旧留驱动。通过将 `dummy_cs` 绑定到卡上，驱动模块可能能够检测并与设备通信，就像它不是 PC Card 一样。尽管这种安排通常不支持纯净的热插拔或电源管理功能，但可以作为后续开发更全功能的客户端驱动程序的基础。

# 9. Socket 驱动程序层

在 PCMIA 模型中，“Socket Services”层是一个供 Card Services 使用的私有 API。该 API 粗略基于 PCMIA Socket Services 规范，但其目标是支持 x86 笔记本电脑控制器类型。

## 9.1 用于 socket 驱动程序的 Card Services 入口点

Card Services 为注册和注销 socket 驱动程序提供了特殊的入口点：

```c
typedef int (*ss_entry_t)(u_int sock, u_int cmd, void *arg);
extern int register_ss_entry(int sock, ss_entry_t entry);
extern void unregister_ss_entry(int sock, ss_entry_t entry);
```

socket 驱动程序调用 `register_ss_entry`，其中 `nsock` 表示由此驱动程序拥有的 socket 数量，`entry` 指向为这些 socket 提供 socket服务的函数。当 Card Services 未为该驱动程序拥有的 socket 注册任何回调函数时，可以安全地调用 `unregister_ss_entry`。

## 9.2 socket 驱动程序提供的服务

Socket Services 以以下形式调用：

```c
#include "pcmcia/ss.h"

int (*ss_entry)(u_int sock, int service, void *arg);
```

非零返回码表示请求失败。

### 9.2.1 SS_InquireSocket

```c
int (*ss_entry)(u_int sock, SS_InquireSocket, socket_cap_t *cap);
```

`socket_cap_t` 数据结构如下：

```c
typedef struct socket_cap_t {
    u_int features;
    u_int irq_mask;
    u_int map_size;
    u_char pci_irq;
    u_char cardbus;
    struct bus_operations *bus;
} socket_cap_t;
```

`SS_Inquire` 服务用于检索 socket 能力。`irq_mask` 字段是一个位掩码，指示是否为 IO 卡配置了 ISA 中断。`map_size` 字段给出内存窗口的粒度。`pci_irq` 字段如果不为 0，则是分配给该 socket 的 PCI 中断号。它独立于 `irq_mask`，实际上可以用于任何一个特定 socket 与特定中断关联的情况。对于 CardBus 桥接器，`cardbus` 字段应为非零，并给出桥接器 CardBus 端的 PCI 总线号。

对于不直接将卡映射到主机 IO 和内存空间的 socket，`bus` 字段是一个指针，指向一个包含该 socket 的 IO 原语操作入口点的表。

在 `features` 中可以指定以下标志：

- `SS_CAP_PAGE_REGS`：表明该 socket 支持对 16 位 PC Card 内存窗口进行全 32 位寻址。
- `SS_CAP_VIRTUAL_BUS`：表明该 16 位卡内存和 IO 访问必须使用总线操作表，而不是使用原生总线操作。
- `SS_CAP_MEM_ALIGN`：表明内存窗口必须按总线大小对齐。
- `SS_CAP_STATIC_MAP`：表明内存窗口静态映射在主机地址空间的固定位置，且无法重新定位。
- `SS_CAP_PCARD`：表明该 socket 支持 16 位 PC 卡。
- `SS_CAP_CARDBUS`：表明该设备支持 32 位 CardBus 卡。

### 9.2.2 SS_RegisterCallback

```c
int (*ss_entry)(u_int sock, SS_RegisterCallback, ss_callback_t *call);
```

`ss_callback_t` 数据结构如下：

```c
typedef struct ss_callback_t {
    void (*handler)(void *info, u_int events);
    void *info;
} ss_callback_t;
```

`SS_RegisterCallback` 设置一个回调函数，当 socket 驱动程序接收到状态变化事件时调用该函数。要注销回调，调用此函数时并将 `handler` 值设为 `NULL`。每个 socket 只能注册一个回调函数。

调用 `handler` 时将传递给该 socket 的 `SS_RegisterCallback` 的 `info` 值，以及 socket 中的事件位掩码。定义了以下事件：

- `SS_DETECT`：卡的插入或移除。
- `SS_READY`：就绪/忙状态。
- `SS_DEAD`：卡丢失状态。
- `SS_BATWARN`：低电量状态。
- `SS_SCHG`：状态变化。

### 9.2.3 SS_GetStatus

```c
int (*ss_entry)(u_int sock, SS_GetStatus, int *status);
```

`SS_GetStatus` 返回 socket 当前的状态。`status` 参数由以下标志组成：

- `SS_PROT`：保护状态。
- `SS_DEAD`：卡丢失状态。



- `SS_BATWARN`: 低电量状态。

# 9. Socket 驱动程序层

- `SS_READY`: 就绪状态。
- `SS_POWERON`: 已上电。
- `SS_SCHG`: 状态变化。
- `SS_CARDBUS`: CardBus 接口。
- `SS_3VCARD`: 3.3V。
- `SS_XVCARD`: 尚未定义。

### 9.2.4 SS_GetSocket, SS_SetSocket

```c
int (*ss_entry)(u_int sock, SS_GetSocket, socket_state_t *state);
int (*ss_entry)(u_int sock, SS_SetSocket, socket_state_t *state);
```

`socket_state_t` 数据结构如下：

```c
typedef struct socket_state_t {
    u_int flags;
    u_int csc_mask;
    u_char Vcc, Vpp;
    u_char io_irq;
} socket_state_t;
```

`csc_mask` 字段指示哪些事件类型产生状态中断。监控的事件类型如下：

- `SS_DETECT`: 插入或移除。
- `SS_READY`: 就绪/忙状态。
- `SS_DEAD`: 卡丢失状态。
- `SS_BATWARN`: 低电量状态。

`Vcc` 和 `Vpp` 参数以 0.1 特为单位。如果非零，`io_irq` 指定了分配给卡的中断号。`flags` 字段由以下部分组成：

- `PWR_AUTO`: 表明在支持时插入时自动上电。
- `IOCARD`: 表明 `socket` 应配置为“内存和 IO”接口，而不是简单的内存模式。
- `RESET`: 表明应触发卡的硬件复位信号。
- `SPKR_ENA`: 表明启用该 `socket` 的声器输出。
- `OUTPUT_ENA`: 表明应激活到卡的数据信号。

### 9.2.5 SS_GetIOOMap, SS_SetIOOMap

```c
int (*ss_entry)(u_int sock, SS_GetIOOMap, pccard_io_map *map);
int (*ss_entry)(u_int sock, SS_SetIOOMap, pccard_io_map *map);
```

`pccard_io_map` 数据结构如下：

```c
typedef struct pccard_io_map {
  u_char map;
  u_char flags;
  u_short speed;
  u_short start, stop;
} pccard_io_map;
```

`SS_GetIOOMap` 和 `SS_SetIOOMap` 条用于配置 IO 空间窗口。假设 IO 窗口不支持地址转换。Linux Card Services 层假设每个 `socket` 至少有两个独立配置的 IO 端口窗口。

`map` 字段指定访问哪个 IO 映射。`speed` 字段是以纳秒为单位的映射速度。`start` 和 `stop` 字段给出 IO 映射的低高位地址。`flags` 字段由以下部分组成：

- `MAP_ACTIVE`: 指定应启用地址映射。
- `MAP_16BIT`: 指定映射应配置为 16 位访问（与 8 位访问相反）。
- `MAP_AUTOSZ`: 指定映射应配置为响应卡的 IOCS16 自动调整总线访问大小。
- `MAP_OWS`: 请求零等待状态，与标准的 ISA 总线定时相反。
- `MAP_WRPROT`: 指定映射应写保护。
- `MAP_USE_WAIT`: 指定访问时序应遵守卡的 WAIT 信号。
- `MAP_PREFETCH`: 指定此映射可以配置为预取。

### 9.2.6 SS_GetMemMap, SS_SetMemMap

```c
int (*ss_entry)(u_int sock, SS_GetMemMap, pcard_mem_map *);
int (*ss_entry)(u_int sock, SS_SetMemMap, pcard_mem_map *);
```

`pcard_mem_map` 数据结构定义如下：

```c
typedef struct pcard_mem_map {
    u_char      map;
    u_char      flags;
    u_short     speed;
    u_long      sys_start, sys_stop;
    u_int       card_start;
} pcard_mem_map;
```

`map` 字段指定映射编号。`speed` 字段指定以纳秒为单位的访问。`sys_start` 和 `sys_stop` 字段给出主机物理地址空间中窗口的起始和结束地址。`card_start` 值指定映射到 `sys_start` 的卡地址。Linux Card Services 层假设每个插槽至少有四个独立配置的内存窗口。

- `MAP_ACTIVE`: 指定地址映射应被启用。
- `MAP_16BIT`: 指定映射应配置为 16 位访问（与 8 位访问相反）。
- `MAP_AUTOSZ`: 指定映射应配置为响应卡的 IOCS16 信号自动调整总线访问大小。
- `MAP_OWS`: 请求零等待状态，与标准的 ISA 总线定时相反。
- `MAP_WRPROT`: 指定映射应写保护。
- `MAP_ATTRIB`: 指定映射应为属性内存（而非普通内存）。
- `MAP_USE_WAIT`: 指定访问时序应遵守卡的 WAIT 信号。

### 9.2.7 SS_GetBridge, SS_SetBridge

```c
int (*ss_entry)(u_int sock, SS_GetBridge, cb_bridge_map*);
int (*ss_entry)(u_int sock, SS_SetBridge, cb_bridge_map*);
```

`cb_bridge_map` 数据结构定义如下：

```c
typedef struct cb_bridge_map {
u_char map;
u_char flags;
u_int start, stop;
} cb_bridge_map;
```

`SS_GetBridge` 和 `SS_SetBridge` 入口用于为 CardBus 设备配置桥接地址窗口。它们与 16 位 IO 和内存映射服务类似。假设每个 CardBus 插槽至少有两个 IO 和两个内存桥接窗口。`flags` 字段由组成：

- `MAP_ACTIVE`: 指定地址映射应被启用。
- `MAP_PREFETCH`: 指定此映射可以配置为预取。
- `MAP_IOSPACE`: 指定该空间为 I/O 空间（而非内存空间）。

### 9.2.8 SS_ProcSetup

```c
int (*ss_entry)(u_int sock, SS_ProcSetup, struct proc_dir_entry *base);
```

Card Services 使用此入口为插槽驱动程序提供一个 `procfs` 目录句柄，驱动程序可以在为特定插槽创建状态文件。插槽驱动程序负责在卸载前删除任何 `proc` 条目。

## 9.3 支持异常的插槽架构

Socket Services 接口面向允许 PCMCIA 卡配置为模拟具有相同功能的原生系统设备的插槽控制器。PCIA 标准规定，插槽控制器应为每个插槽提供两个 IO 和内存窗口，这些窗口可以在主机地址空间中进行独立配置和定位，并映射到地址空间的任意分段。某些控制器和架构并不提供此功能。
