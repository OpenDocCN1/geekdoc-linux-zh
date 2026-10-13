
但我提到的这些“序列号”是什么？它们是识别特定问答对的手段。在传输流中，它们是识别特定问答对以及检测丢失数据包的方法。在上电时，`VCM` 和 `Kuro Box` 将内部序列计数器初始化为 1（0 是预留值）。当一端发送包时，它将 `TXSN` 字段设置为当前的序列号（如果计数器溢出，则重置为 1）。如果数据包需要响应，它将 `IRSN` 字段设置为其响应的包的序列号（非零 `IRSN` 隐式表示这是一个响应而非请求）。

这种简单的系统允许一端保留挂起请求的历史，并跟踪哪些响应属于哪些请求（必要时，实现超时和重试）。

一个例子最容易地说明这一点。假设你定义命令 99 为“获取当前姿态”，定义命令 100 为“获取 GPS 位置”。此外，假设 `VCM` 的当前序列号为 56，`Kuro Box` 的序列号为 80。假设 `Kuro Box` 想尽快知道姿态和位置。它可能会发送以下包：

- `CMD=100` (获取位置), `TXSN=80`, `IRSN=0`, 无 `BODY`

- `CMD=99` (获取姿态), `TXSN=81`, `IRSN=0`, 无 `BODY`

`GPS` 位置 `V` `VCM` 需要时间来获取，因此姿态可能在位置数据之前就准备就绪。假设这种情况发生，`VCM` 将响应：

- `CMD=99` (获取姿态), `TXSN=56`, `IRSN=81`, `BODY` 中包含姿态数据

- （稍后当数据可用时）`CMD=100` (获取位置), `TXSN=57`, `IRSN=80`, `BODY` 中包含位置数据

由于某种原因 `VCM` 没有对这些包中的任何一个响应，`Kuro Box` 可以记录哪些序列号是挂起的，并在一段时间后重新发送请求。

# 自下而上，自学指南

`VCM` 板上的步进电机输出端标记为 `SAP1` 到 4（步进 A 1 到 4）和 `SBP1` 到 4（步进 B 1 到 4）。你应该根据情况将相位线连接到 `SxPx` 线，并将电机的公共线连接到 `+24V` 线路。在 `VCM` 上，我使用一个 9 位端子块来将这些信号引出板外。

注意！请观察步进驱动线上的串联电阻。我指定的零欧姆电阻仅是位符；你应该根据你的驱动电压以及步进电机的线圈电阻和额定电流，替换合适的限流电阻。

这段代码和硬件设计用于对两个四相单极步进电机（步进 A 和步进 B）进行非常简单的控制。步进函数默认由 100 Hz 的软件定时器驱动。对于廉价步进电机来说，这是一个中等速度，也是我的一种相当安全的随机选择。然而，硬件能够支持更高的步进频率。当你增加步进频率时，应该注意以下两个问题：

- 在不详述详细力学机制的情况下，步进电机无法从零启动并立即以其最大额定频率开始运行。如果你打算充分发挥电机的性能，就需要实现“加速曲线”（acceleration profiles）。简而言之，这意味着你需要对电机进行速度变化，而不是直接跳到新的步进频率，而是让频率向目标速度逐渐增加。加速曲线需要针对电机和正在驱动的机械负载进行校准。

- 随着步进频率的增加，扭矩会减小。需要巧妙的硬件设计才能从给电机中榨出最大的性能。

这种特定的设计在上述这两个方面都不及极限——例如，你有足够的余量来增加步进频率。

参考 `stepper.c`，你会看到软件会跟踪每个步进电机的绝对位置，并在步进速度间隔处进行检查。如果 `Kuro Box` 要求的运行与当前位置不符，则相应的电机将向前或向后步进。串口接口代码监听“seek to...”数据包并相应地更新目标值。

# 第 112 页 第 3 章

`VCM` 代码假设步进电机的上电位置是已知的绝对零位置。寻找零参考点通常通过在电机的驱动轴（或其操作的机构）上安装硬件零位置检测器来实现。例如，在软驱驱动器中，道 0 传感器是一个光电开关（或在旧的驱动器中是一个微动，磁头在步进到道 0 时会进入）。

`VCM` 固件支持两种数据包类型：`CMD_STEP_A` 和 `CMD_STEP_B`（定义在 `vccmpack.h` 中）。如果你在 `scmd` 目录下构建 `Kuro Box` 程序，你将看到 `Kuro Box` 输出来自 `VCM` 的状态信息，每隔四个数据包发送一次 `VCM` 命令，让两个步进电机寻找到随机位置。请注意，`Kuro Box` 侧的代码是简单快速的；它只是一个概念验证，因为我们的重点在设计中的 `VCM` 侧。

以下是 `scmd` 程序的示例输出：

```
root@KURO-BOX:/mnt/share/article/scmd~/ .scmd
IBM developers Kuro Box to VCM Demo App #2-Stepper Demo
Waiting for VCM to start...
Rx packet (TXSN 01, BLEN 005)-MTIME 0x000005b8, FLAGS1 0x00
Rx packet (TXSN 02, BLEN 005)-MTIME 0x00000b70, FLAGS1 0x00
Rx packet (TXSN 03, BLEN 005)-MTIME 0x00001128, FLAGS1 0x00
Rx packet (TXSN 04, BLEN 005)-MTIME 0x000016e0, FLAGS1 0x00
Tx2 packets: CMD_STEP_A->000000167, CMD_STEP_B->FFFFFFF9
Rx packet (TXSN 05, BLEN 005)-MTIME 0x000001c9, FLAGS1 0x00
Rx packet (TXSN 06, BLEN 005)-MTIME 0x00000250, FLAGS1 0x00
Rx packet (TXSN 07, BLEN 005)-MTIME 0x00002808, FLAGS1 0x00
Rx packet (TXSN 08, BLEN 005)-MTIME 0x000002dc, FLAGS1 0x00
Tx2 packets: CMD_STEP_A->FFFFFFFF, CMD_STEP_B->0000004A
Rx packet (TXSN 09, BLEN 005)-MTIME 0x00000378, FLAGS1 0x01
Rx packet (TXSN 0a, BLEN 005)-MTIME 0x00000390, FLAGS1 0x00
Rx packet (TXSN 0b, BLEN 005)-MTIME 0x000003e8, FLAGS1 0x00
Rx packet (TXSN 0c, BLEN 005)-MTIME 0x000044a0, FLAGS1 0x00
Tx2 packets: CMD_STEP_A->FFFFFFFF, CMD_STEP_B->FFFFFFFF
Rx packet (TXSN 0d, BLEN 005)-MTIME 0x000004a5, FLAGS1 0x00
Rx packet (TXSN 0e, BLEN 005)-MTIME 0x00000510, FLAGS1 0x00
Rx packet (TXSN 0f, BLEN 005)-MTIME 0x000005c8, FLAGS1 0x00
Rx packet (TXSN 10, BLEN 005)-MTIME 0x000005b0, FLAGS1 0x00
Tx2 packets: CMD_STEP_A->FFFFFFFF, CMD_STEP_B->00000013
Rx packet (TXSN 11, BLEN 005)-MTIME 0x000005b4, FLAGS1 0x00
Rx packet (TXSN 12, BLEN 005)-MTIME 0x00000612, FLAGS1 0x00
Rx packet (TXSN 13, BLEN 005)-MTIME 0x000006ca, FLAGS1 0x00
```

（注：OCR 文本在后页包含大量的重复噪声/伪影，已过滤以提供连贯的文档流。）

只需将传感器安装在需要的地方，并将它们布线到 `I2C` 总线即可。对于 `MPC23008`，它有三位用户可配置的地址；整个设备地址字节为 `100xxxR`，其中 `xxx` 是地址引脚 `A2` 到 `A0`，`R` 是读/写位。请注意，无论选择何种 `A2/A0` 组合，`MPC23008` 之间都不存在地址冲突的可能性。有趣的是，如果你参考 `MPC9800` 系列的数据表，你会发现该器件还提供两种型号，采用五引脚 `SOT23`（表面贴装晶体管）封装形式。这种微型封装没有空间放置外部地址选择引脚，因此微芯科技（Microchip）提供了一个硬接线地址为 000 的型号，另一个地址为 101（二进制）的型号。再次，这种做法在 `I2C` 传感器中很常见。

`MPC9801` 还具有恒温器模式（此选项经常提供在数字温度传感器设备上）。此功能由单个开漏输出组成，当感测温度落在可编程范围之外时，输出将变为有效，且它的运行完全独立于 `I2C` 逻辑，因此即使在微控制器崩溃时你也可以将其作为硬件故障保护。也许更，你甚至可以关闭微控制器以节省功率，并让温度传感器 IC 运行，以便在发生不合理的温度波动时关闭并唤醒微控制器。
