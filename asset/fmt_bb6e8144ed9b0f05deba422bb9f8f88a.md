
该麦克风通电代码当然特定于`mts300` 传感器。然而，它实际上对使用相同传感器的其他平台来说相当可移植，因为它通过硬件无关的`GeneralIO` 和`I2CPacket` 接口访问所需的低级硬件功能（数字 I/O 引脚和 I²C 总线）。`GeneralIO` 接口提供配置、读取和写入典型微控制器数字 I/O 引脚的命令：

```
interface GeneralIO {
    async command void set();
    async command void clr();
    async command void toggle();
    async command bool get();
    async command void makeInput();
    async command bool isInput();
    async command void makeOutput();
    async command bool isOutput();
}
```

Listing 13.6  The `GeneralIO` digital I/O pin interface

在 TinyOS 中，I²C 总线通常通过共享驱动程序访问，因此 I²C 总线用户首先通过`Resource` 接口请求访问（在`MicrophoneC` 中命名为`I2CResource`）。`I2CPacket` 接口为 I²C 总线主设备提供发送读写数据包的命令（`I2CPacket` 接受一个`addr_size` 类型参数以区分具有 7 位与 15 位总线地址的 I²C 实现）：

```
interface I2CPacket<addr_size> {
async command error_t read(I2c_flags_t flags, uint16_t addr, uint8_t length, uint8_t* data);
async event void readDone(error_t error, uint16_t addr, uint8_t length, uint8_t* data);

async command error_t write(I2c_flags_t flags, uint16_t addr, uint8_t length, uint8_t* data);
async event void writeDone(error_t error, uint16_t addr, uint8_t length, uint8_t* data);
}
```

清单 13.7 用于总线主设备的`I2CPacket` 接口

虽然`MicrophoneC` 具有很强的可移植性，但将其连接到用于访问麦克风的特定硬件资源的布线必然是平台特定的：

```
components MicaBusC, new Atm128I2CMasterC() as I2CPot;
MicrophoneC.MicPower -> MicaBusC.PW3;
MicrophoneC.MicMuxSel -> MicaBusC.PW6;
MicrophoneC.I2CResource -> I2CPot;
MicrophoneC.I2CPacket -> I2CPot;
```

`Atm128I2CMasterC` 是提供对`ATmega128` I²C 总线访问的组件。`MicaBusC` 抽象了各种 mica 系列 mote 在共享相同的 51 针传感器板连接器方面的差异，使得编写可移植到所有 mica 系列 mote 的传感器板实现变得更容易。

关闭麦克风电源要简单得多。`MicPower` I/O 引脚只需清除并设为输入即可：

```
command error_t SplitControl.stop() {
//Power off microphone
call MicPower.clr();
call MicPower.makeInput();

//And let our caller know we're done-post a task as one should not
//signal events directly from commands
post stopDone();
return SUCCESS;
}

task void stopDone() {
signal SplitControl.stopDone(SUCCESS);
}
```

### 13.5 总结

就这样！你已经看到了如何构建应用程序，从第 6.1 章中最简单的防盗版本到像`SoundLocalizer` 这样中等复杂度的系统。你还看到了 nesC 的组件和执行模型，以及 TinyOS 的组件库如何帮助你构建应用程序结构并创建可重用的抽象（库、服务、设备驱动程序）。请记得查看 www.tinyos.net 以获取 TinyOS 和 nesC 的最新发展和文档。

现在就看你去编写一些有用且有趣的传感器网络应用程序了！

## 第四部分

## 附录和参考文献

## 附录 TinyOS API

本附录给出了主要 TinyOS 接口及其提供组件的摘要。它仅涵盖硬件无关的 HIL 接口和跨多个硬件平台通用的抽象。在几乎所有情况下，TinyOS 增强提案（TEP）都更深入地描述了这些抽象，我们在适当的地方引用了它们。具有分阶段接口的应用程序级抽象通常是泛型，用户必须实例化它们。为简洁起见，此列表显示了相关组件的签名：你可以在你的 TinyOS 分发版中阅读这些接口。

### A.1 启动

mote 的启动过程封装在`MainC` 组件中，该组件在所有系统服务初始化后发出`Boot.booted` 事件。需要启动时初始化的组件应将其连接到`MainC` 的`SoftwareInit`：`MainC` 的`SoftwareInit.init` 命令在硬件初始化之后但在发出`booted` 之前被调用。

```
configuration MainC {
  provides interface Boot;
  uses interface Init as SoftwareInit;
}
```

我们在第 6.1 节中介绍了启动。TinyOS 启动过程在 TEP 107：TinyOS 2.x Boot Sequence [14] 中有描述。

### A.2 通信

TinyOS 提供了四种基本通信抽象：主动消息（AM，单跳、不可靠通信）、集合（多跳、不可靠地向数据汇点交付）和传播（多跳、可靠地向网络中每个节点交付），以及串行通信（通过串行线路的不可靠交付）。我们在第 6.3、6.4 和 7.1.1 节中介绍了通信。

`message_t` 类型用于声明 TinyOS 网络协议的包缓冲区，如 TEP 111 中所述：`message_t` [15]。

#### A.2.1 单跳

TinyOS 有四个标准的单跳通信组件，全部以 AM 类型作为参数，一个 8 位数字，用于标识不同的包类型。主动消息地址为 16 位。TinyOS 定义了宏`TOS_BCAST_ADDR` 用于 AM 广播地址，并且节点可以通过`AMPacket` 接口找到其本地地址。

`AMSenderC` 发送数据包。`AMReceiverC` 针对发往该节点的包发出接收信号，包括广播地址；`AMSnooperC` 针对未发往该节点的包发出接收信号；`AMSnoopingReceiverC` 无论寻址如何都发出所有包的接收信号。AM 接口会自动丢弃未通过链路层 CRC 检查的包。`PacketAcknowledgements` 接口允许发送方请求链路层确认并在发送后检查是否收到确认：可以在`Send.sendDone` 中调用`PacketAcknowledgements.wasAcked`。

```
generic configuration AMSenderC(am_id_t AMId) {
    provides {
        interface AMSend;
        interface Packet;
        interface AMPacket;
        interface PacketAcknowledgements as Acks;
    }
}
```

```
generic configuration AMReceiverC(am_id_t AMId) {
    provides {
        interface Receive;
        interface Packet;
        interface AMPacket;
    }
}
```

```
generic configuration AMSnooperC(am_id_t AMId) {
    provides {
        interface Receive;
        interface Packet;
        interface AMPacket;
    }
}
```

```
generic configuration AMSnoopingReceiverC(am_id_t AMId) {
    provides {
        interface Receive;
        interface Packet;
    }
}
```
