
此外，高级硬件无关 API 与能够使程序利用所有硬件能力的 API 之间存在张力。例如，并非所有无线电都有多个信道频率。一些系统可能希望利用此功能，并愿意假设它们使用特定的无线电芯片来实现这一点。其他系统可能希望保持硬件无关。

TinyOS 使用组件分层来实现这一点。让我们以数据包通信为例。平台需要提供的顶层组件称为`ActiveMessageC`，并且是硬件无关的。¹ `ActiveMessageC`几乎总是位于芯片特定组件之上的配置，该组件提供额外的接口。例如，这是 micaz mote 的`ActiveMessageC`实现，该 mote 具有 CC2420 无线电芯片：

```
configuration ActiveMessageC {
  provides {
    interface SplitControl;
```

¹ TinyOS 使用“主动消息” [29]，通常缩写为 AM，作为其网络抽象 参见第 6.3 节。

硬件无关的`ActiveMessageC`并未导出`CC2420Packet`、`RadioBackoff`、`LowPowerListening`或`PacketLink`。`ActiveMessageC`所做的是一种非常常见的配置用法。`ActiveMessageC`并未增加任何功能：它所做的只是导出`CC2420ActiveMessageC`的接口，并因此在全局命名空间中为它们提供不同的、替代的名称。调用`CC2420ActiveMessageC`的`AMSend.send`与调用`ActiveMessageC`的`AMSend.send`相同。区别在于调用方可以做出的假设类型。例如，如果你将一个组件连接到`ActiveMessageC.AMSend`和`CC2420ActiveMessageC.CC2420Packet`，你可能会遇到严重的问题。可能某个平台有两个无线电，其中一个是 CC2420，但`ActiveMessageC`并未指代 CC2420。在这种情况下，组件将访问不存在的协议字段，混乱是必然的。

> 编程提示 13 在使用分层抽象时，组件不应跨越多个抽象层进行连接：它们应连接到单一层。

### 4.4 多重连接

并非所有连接都是一对一的。例如，以下是组件`CC2420TransmitC`的一部分，这是一个封装了 CC2420 无线电发送路径的配置：

```
configuration CC2420TransmitC {
  provides interface Init;
  provides interface AsyncControl;
  provides interface CC2420Transmit;
  provides interface CsmaBackoff;
  provides interface RadioTimeStamping;
}
implementation {
  components CC2420TransmitP;
  components AlarmMultiplexC as Alarm;
  Init = Alarm;
  Init = CC2420TransmitP;
  // further wirings elided
}
```

列表 4.17 `CC2420TransmitC`的`Init`上的扇出

这种连接意味着`CC2420TransmitC.Init`同时映射到`Alarm.Init`和`CC2420TransmitP.Init`。这意味着什么？在类 C 语言中绝对没有类似的对应物。在 nesC 中，像这样的多重连接意味着当一个组件调用`CC2420TransmitC`的`Init.init`时，它会同时调用`Alarm`的`Init.init`和`CC2420TransmitP`的`Init.init`。两次调用的顺序是未定义的。

#### 4.4.1 扇入和扇出

这种能够进行多重连接的能力看起来可能很奇怪。在这种情况下，你有一个单一的调用点，`CC2420TransmitterC's Init.init`，它扇出到两个被调用者。也有扇入，这其实只是“多个人调用同一个函数”的花哨说法。但“扇入”和“扇出”名称的相似性很重要，因为 nesC 接口是双向的。例如，来自 C 的视角，将两个组件连接到`RandomC.Random`似乎并不奇怪：两个不同的组件可能都需要生成随机数。在这种情况下，由于`Random`只有命令，所有函数都是扇入。有多个调用者对应一个被调用者，就像一个库函数一样。

但由于 nesC 接口是双向的，如果在接口的命令上存在扇入，那么当该组件在接口上发出事件时，就存在扇出（多个被调用者）。以电源控制接口`StdControl`和`SplitControl`为例。`StdControl`是单阶段的：它只有命令。`SplitControl`如其名所示是分阶段的：命令有完成事件：

```
interface StdControl {
  command error_t start();
  command error_t stop();
}
interface SplitControl {
  command error_t start();
  event void startDone(error_t error);
  command error_t stop();
  event void stopDone(error_t error);
}
```

列表 4.18 `StdControl`和`SplitControl`初始化接口

对于`StdControl`，服务在`start`（`stop`）返回时就已启动（停止），而对于`SplitControl`，服务只有在`startDone`被发出时才保证已启动。

在此连接中，`StdControl`上存在扇入：

```
components A, B, C;
A.StdControl -> C;
B.StdControl -> C;
```

那么`A`或`B`都可以调用`StdControl`来启动或停止`C`。然而，在此连接中，也存在完成事件，因此在`SplitControl`上同时存在扇入和扇出：

```
components A, B, C;
A.SplitControl -> C;
B.SplitControl -> C;
```

`A`或`B`都可以调用`SplitControl.start`。当`C`发出`SplitControl.startDone`事件时，不过，两者都已连接到它，因此`A`的`SplitControl.startDone`和`B`的`SplitControl.startDone`被调用。实现没有办法确定是谁调用了`start`命令。²

总之，接口不是一对一的关系。相反，它们是 n 到 k 的关系，其中 n 是用户数量，k 是提供者数量。任何提供者的信号都会在所有 n 个用户上调用事件处理程序，而任何用户调用命令都会在所有 k 个提供者上调用该命令。

#### 4.4.2 多重连线的用途

在实践中，多重连线允许实现独立于其所依赖的组件数量。请记住`MainC`（第 3.8 节清单，第 26 页）将启动序列抽象为两个接口，`SoftwareInit`和`Boot`。`MainC`在启动时调用`SoftwareInit.init`，以便在执行开始前初始化软件组件。`MainC`然后在整个启动序列结束后发出`Boot.booted`信号。许多组件都需要初始化。例如，在非常简单的应用程序`RadioCountToLeds`中，有十个组件连接到`MainC.SoftwareInit`。与其使用许多`Init`接口并按某种顺序调用它们，`MainC`只需调用一次`SoftwareInit`，而此调用会扇出到所有已连接到它的组件。

轶事：历史上，多重连线源于 TinyOS 组件可以被视为硬件芯片的想法。在此模型中，接口是芯片上的引脚集合。术语“连线”源于这一想法：连接一个芯片上的引脚到另一个芯片。尽管如此，在硬件中，你可以轻松地将 N 个引脚连接在一起。例如，芯片上的一个通用 IO 引脚可能有多个可能的触发器，或者总线有多个通过片选引脚控制的终端设备。事实证明，字面地采用这一隐喻存在几个问题。当 TinyOS 迁移到 nesC 时，这些问题被解决了。具体来说，考虑以下配置：

```
configuration A {
  uses interface StdControl;
}

configuration B {
  provides interface StdControl;
  uses interface StdControl as SubControl; // Called in StdControl
}

configuration C {
  provides interface StdControl;
}

A.StdControl -> B.StdControl;
A.StdControl -> C.StdControl;
B.SubControl -> C.StdControl;
```

清单 4.19 “连线”隐喻为何只是隐喻
