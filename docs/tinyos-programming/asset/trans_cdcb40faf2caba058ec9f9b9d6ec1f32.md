
正确的唯一键。这意味着 `unique()` 只在一个文件中被调用；只要所有组件都使用 `TimerMilliC` 分配定时器，就不会发生键匹配错误。`TimerMilliC` 的实现非常简单：

```
generic configuration TimerMilliC() {
  provides interface Timer<TMilli>;
}
implementation {
  components TimerMilliP;
  Timer = TimerMilliP.TimerMilli[unique(UQ_TIMER_MILLI)];
}
```

清单 9.5 TimerMilliC 通用配置

`TimerMilliP` 是一个单例配置，它将 `HiiTimerMilliC` 自动连接到启动序列，并导出 `HiiTimerMilliC` 的参数化接口：

```
configuration TimerMilliP {
  provides interface Timer<TMilli> as TimerMilli[uint8_t id];
}
implementation {
  components HiiTimerMilliC, MainC;
  MainC.SoftwareInit -> HiiTimerMilliC;
  TimerMilli = HiiTimerMilliC;
}
```

清单 9.6 TimerMilliP 将 HiiTimerMilliC 自动连接到 Main.SoftwareInit

`TimerMilliC` 封装了一种接线模式——通过调用 `unique` 连接到定时器服务——供其他组件使用。当一个组件实例化 `TimerMilliC` 时，它会创建一份 `TimerMilliC` 代码的副本，其中包含对 `unique(UQ_TIMER_MILLI)` 的调用。以下代码：

```
components X, new TimerMilliC();
X.Timer -> TimerMilliC;
```

本质上等同于：

```
components X, TimerMilliP;
X.Timer -> TimerMilliP.TimerMilli[unique(UQ_TIMER_MILLI)];
```

让我们逐步了解一个创建定时器的应用程序的完整接线路径。`BlinkAppC` 将 `BlinkC` 模块连接到它的三个定时器：

```
configuration BlinkAppC()
implementation {
  components MainC, BlinkC, LedsC;
  components new TimerMilliC() as Timer0;
  components new TimerMilliC() as Timer1;
  components new TimerMilliC() as Timer2;

BlinkC -> MainC.Boot;
MainC.SoftwareInit -> LedsC;

BlinkC.Timer0 -> Timer0;
BlinkC.Timer1 -> Timer1;
BlinkC.Timer2 -> Timer2;
BlinkC.Leds -> LedsC;
}
```

清单 9.7 Blink 应用程序

`HiiTimerMilliC` 配置将其 `Timer` 接口连接到 `VirtualizeTimerC` 定时器虚拟化组件（见第 9.1.3 节）。因此，将 `BlinkC.Timer0` 连接到 `Timer0` 就建立了如下接线链：

```
BlinkC.Timer0 -> Timer0.Timer
enum { K = unique (UQ_TIMER_MILLI) };
Timer0.Timer = TimerMilliP.TimerMilli[K]
TimerMilliP.TimerMilli[K] = HiiTimerMilliC[K]
HiiTimerMilliC[K] = VirtualizeTimerC.Timer[K]
```

清单 9.8 Blink 中完整的模块到模块接线链（BlinkC 到 VirtualizeTimerC）

`BlinkC` 和 `VirtualizeTimerC` 是两个模块；中间的组件都是配置。当 nesC 编译这段代码时，所有中间层都将被剥离，`BlinkC.Timer0.start` 将成为对 `VirtualizeTimerC.Timer[...].start` 的直接函数调用。

TinyOS 的许多基本服务都使用这种模式：通用配置为参数化接口管理一个键空间（一组标识符，见第 10.3 节）。有时映射比 `TimerMilliC` 更复杂，正如我们下面描述 `BlockStorageC`（TinyOS 的非易失性存储抽象之一）时会看到的那样。

## 9.2.2 CC2420SpiC

另一个使用通用配置的更复杂示例是 `CC2420SpiC`。该组件提供通过 SPI 总线访问 CC2420 无线电的功能。当无线电协议栈软件想要与无线电交互时，它会调用该组件实例上的方法。例如，如果信道空闲，让 CC2420 发送数据包涉及到写入无线电的一个寄存器（TXONCCA）。为了写入该寄存器，协议栈通过总线发送一小串字节，这些字节基本上表示“我正在向寄存器号 X 写入值 Y”。总线的高速意味着诸如此类的小操作可以同步完成，而不会产生任何显著的并发问题。

除了小的寄存器读写之外，该芯片还支持访问接收和发送缓冲区（它们是 128 字节的内存区域），以及无线电的配置存储器，后者存储诸如加密密钥和本地地址（用于确定是否发送确认）等信息。这些操作可能需要一些时间，因此是分阶段的。例如，在协议栈写入 TXONCCA 发送数据包之前，它必须首先使用 `CC2420Fifo` 接口对数据包内容执行一次分阶段写入（接收和发送缓冲区是 FIFO 存储器）。

所有操作归结为四个接口：

- **CC2420Strobe**：访问命令寄存器。写入命令寄存器会告诉无线电采取某个动作，例如发送数据包、清除其数据包缓冲区或切换到发送模式。该接口有一个单一命令 `strobe`，用于写入寄存器。
- **CC2420Register**：访问数据寄存器。这些寄存器既可读也可写，存储硬件配置、寻址模式和空闲信道评估阈值等信息。该接口支持单阶段的读写操作。
- **CC2420Ram**：访问配置存储器。该接口支持读写操作，均为分阶段操作。
- **CC2420Fifo**：访问接收和发送 FIFO 内存缓冲区。该接口支持读写操作，均为分阶段操作。虽然可以写入接收缓冲区，但 CC2420 仅出于调试目的支持此操作。

需要与 CC2420 交互的组件会实例化一个 `CC2420SpiC` 实例：

```
generic configuration CC2420SpiC() {

    provides interface Resource;

    provides interface CC2420Strobe as SPLUSHRX;
    provides interface CC2420Strobe as SPLUSHTX;
    provides interface CC2420Strobe as SNOP;
    provides interface CC2420Strobe as SRXON;
    provides interface CC2420Strobe as SRXFOPF;
    provides interface CC2420Strobe as STXON;
    provides interface CC2420Strobe as STXONCCA;
    provides interface CC2420Strobe as SXOSCON;
    provides interface CC2420Strobe as SXOSCOFF;

    provides interface CC2420Register as FSCTRL;
    provides interface CC2420Register as IOCFG0;
    provides interface CC2420Register as IOCFG1;
    provides interface CC2420Register as MDCTRL0;
    provides interface CC2420Register as MDCTRL1;
    provides interface CC2420Register as TXCTRL;

    provides interface CC2420Ram as IBEEREADR;
    provides interface CC2420Ram as PANID;
```
