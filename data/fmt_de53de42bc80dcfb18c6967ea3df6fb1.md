
# 常见处理器架构

尽管有很多微控制器架构，例如`Intel8051`、`Freescale（Motorola）68HC11`和`Microchip PIC`，但有两种架构在联网设备中显示更为常见：`ARM`和`MIPS`。在使用反汇编器、构建工具和调试器时，了解处理器架构是非常重要的。

`ARM`是一种许可架构，被许多微处理器、微控制器和`SoC`制造商使用，例如德州仪器（`Texas Instruments`）、`Apple`、`三星`等。`ARM`核心根据预期应用需求被分为多种配置（`Profiles`）。`ARM`核心提供`32`位和`64`位架构，并可以配置为大端或小端。表 20-1 展示了通常使用这些配置的类型和应用。

| 配置 | 说明 | 示例应用 |
|---|---|---|
| `Application`（应用） | 配置中最强大的类型。其主要特点是带有`MMU`（内存管理单元），使其能够运行`Linux`和`Android`等功能丰富的操作系统。 | 手机、平板电脑、顶盒 |
| `Real-time`（实时） | 为需要实时性能特征的应用设计。具有低中断延迟和内存保护功能。不包含`MMU`。 | 网络路由器和交换机、摄像头、汽车 |
| `Microcontroller`（微控制器） | 为尺寸和性能要求的嵌入式系统设计。具有低中断延迟、内存保护和嵌入式内存。 | 工业控制、可编程灯 |

## 表 20-1 ARM 配置²

`MIPS`最后归属于已破产的`Wave Computing`公司，目前已转而支持`RISC-V`；然而，重组之前签署的许可协议似乎仍然有效。`MIPS`已授权给`Broadcom`、`Cavium`等多家制造商。与`ARM`类似，`MIPS`有`32`位和`64`位变体，可以在大端或小端模式下运行。它常见于无线接入点和小型家用路由器等网络设备。

### 串口接口

串口接口通过通信通道以串行方式与对端每次通信一个比特。由于每次只传输一个比特，因此集成电路（`IC`）所需的引脚较少。相比之下，并行接口通信一次传输多个比特，需要更多引脚（每个位一个引脚）。嵌入式系统中使用了多种串行协议，但我们只讨论通用异步收发器（`UART`）、串行外设接口（`SPI`）和集成电路（`I²C`）协议。

## UART

通用异步收发器（`UART`）协议允许两个设备通过通信通道进行串行通信。`UART`常用于连接控制台，以便人类与设备进行交互。虽然大多数设备没有外部可用的串行通信接口，但许多设备拥有在开发和测试期间使用的内部接口。在进行设备测试时，我曾在内部访问的串口接口上发现过经过认证和未经过认证的控制台。

`UART`通信需要三个引脚，通常四个引脚一组出现（见图 20-1）。你可能会在板卡上看到标签，但通常这些焊盘或插头没有标签，需要自行发现。虽然图 20-1 显示了一个很好的例子，其中插头作为串口通信的候选者非常明显，但引脚的布局并不总是那么直观，可能会混杂在较多的引脚中。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_693_0.png)

**图 20-1** Ubiquiti ER-X 上未标记的四位串口组

定位并连接内部串口的主要原因是尝试获取未打算让系统用户访问的信息。例如，`Web`强制界面通常不会直接提供文件系统的访问，但基于`Linux`的系统的串口控制台将赋予用户访问文件系统的权限。当串口经过认证时，你必须暴力破解凭据，或尝试通过更改启动过程（可能通过使用`JTAG`调试端口）来绕过认证。

为了发现串口焊盘，可以使用`Joe Grand`开发的`JTAGulator`等工具对信号进行暴力破解，得出焊盘布局和波特率。以下是对**图 20-1**所示所示`Ubiquiti ER-X`进行`UART`识别测试的示例，使用`JTAGulator`识别了标记引脚。涉及步骤如下：

- 1. 通过检查板卡定位你认为可能是`UART`的插头或焊盘。（在板卡上看到二到四个焊盘/引脚分组是一个好信号，但如前所述，它们可能与其他功能焊盘/引脚混杂。）
- 2. 使用万用表探测板卡，或通过识别`IC`并查询数据表来发现目标电压。
- 3. 通过测量已知地（如底壳地）与易连引脚之间的电阻（欧姆），发现一个易连接的地（即已知地与目标引脚之间有效为 0 欧姆）。
- 4. 如果足够幸运找到了插头，将板卡连接到你的`JTAGulator`，或者在板卡上焊接一个插头然后连接（见图 20-2）。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_695_0.png)

**图 20-2** `JTAGulator`与`Ubiquiti ER-X`之间的连接

- 5. 验证`JTAGulator`固件版本 ❶。可以对比仓库 `https://github.com/grandideastudio/jtagulator/releases` 上的代码检查版本。如果版本不是最新，请按照 `www.youtube.com/watch?v=xlXwy-weG1M` 操作。
- 6. 启用`UART`模式 ② 并设置目标电压 ③。
- 7. 运行识别 ④。
- 8. 成功后，寻找回车、换行或可读文本等合理响应。
- 9. 运行波特率 ⑤ 验证结果（同步）。

```
Welcome to JTAGulator. Warning: Use of this tool may affect target!
Interfaces: UART, GPIO, SWD
General Commands:
Set I/O voltage
Display information
JTAGulator FW 1.1 Designed by Joe Grand
Main: jtagulator.com
Source: grandideastudio
Current I/O voltage: Undefined
Enter new/O voltage (1.2 - 3.3, 0 for off): 3.3
New I/O set: 3.3
Ensure JTAG is NOT connected to target!
UART pin naming is from the target's perspective.
Enter text string to output (prefix \x) [CR]:
Enter starting channel [0]
Enter ending channel [1]
Are any pins known [y/N]: N
Possible permutations: 2
Enter text string to output (prefix \x) [CR]:
Enter delay before checking for target response (in ms) [1000]: 0
Ignore non-printable characters [y/N]: N
Bring channels before each permutation? [y/N]: N
Press spacebar to begin (any key to abort)...
TAGulating! Press any key to abort...
D: 0
RXD: 1
Baud: 9600
Data: ...
TXD: 0
RXD: 1
Baud: 14400
Data: ...
TXD: 0
RXD: 1
Baud: 19200
Data: ...
TXD: 0
RXD: 1
Baud: 28800
Data: ...
TXD: 0
RXD: 1
Baud: 31250
Data: ...
TXD: 0
RXD: 1
Baud: 38400
Data: ...
TXD: 0
RXD: 1
Baud: 57600
Data: ...
TXD: 0
RXD: 1
Baud: 76800
Data: ...
```

`UART` scan complete.

`UART>` p

Note: `UART` pin naming is from the target's perspective.

Enter X to disable either pin, if desired.

Enter `TXD` pin [0]:

Enter `RXD` pin [1]

Enter baud rate [0]: 57600 y

Enable local echo? [y/N]

Entering `UART` passthrough: Press Ctrl-X to exit...

Welcome to EdgeOS ubnt tty1

通过登录、访问或使用 `Ubiquiti` 产品，你承认你已阅读并理解 `Ubiquiti` 许可协议（可在 `Web` 界面获取，默认地址 `http://192.168.1.1`），并同意受其条款约束。

如果测试成功，你现在应该能够与串口控制台交互。在连接串口控制台的情况下重启设备通常会非常有启发性。由于由于文本太长无法在此列出，我提供了启动消息的片段：

- 处理器是 `MT-7621A` (`MIPS`)：

`ASIC MT7621A DualCore (MAC to MT7530 Mode)`

- 它可以通过 `U-Boot` 进行重新编程：

请选择系统操作：

1: 通过 `TFTP` 将系统代码加载到 `SDRAM`。
