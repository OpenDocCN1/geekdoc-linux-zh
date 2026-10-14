

# 6.3.2 接收数据包

MovingC 使用硬编码常量作为检查间隔和加速度方差阈值。如果这些值在某些环境下不合适（例如，移动车辆可能存在背景振动），则必须更改代码并使用新值重新编译，然后重新安装到传感器网络中。更好的方法是修改一次代码以允许远程配置，使用 AM 数据包，其负载如下（也在 antitheft.h 中声明）：

```
typedef nx_struct settings {
  nx_uint16_t accelVariance;
  nx_uint16_t accelInterval;
} settings_t;
```

AM 数据包的接收由 TinyOS Receive 接口提供（前面也见过）：

```
interface Receive {
  event message_t* receive(message_t* msg, void* payload, uint8_t len);
}
```

清单 6.15 Receive 接口

如第 3.5.1 节所述，Receive.receive 的实现会接收一个数据包缓冲区，它们可以简单地返回该缓冲区，也可以保留该缓冲区，只要返回不同的缓冲区即可。在 MovingC 的情况下，我们选择第一种方案，因为在我们从数据包中读取设置后，就不再需要这些设置了：

```
uses interface Receive as Settings;
...
uint16_t accelVariance = ACCEL_VARIANCE;

event message_t *Settings.receive(message_t *msg,
    void *payload, uint8_t len) {
  if (len >= sizeof(settings_t)) { // Check the packet seems valid
    // Read settings by casting payload to settings_t, reset check interval
    settings_t *settings = payload;
    accelVariance = settings->accelVariance;
    call TheftTimer.startPeriodic(settings->accelInterval);
  }
  return msg;
}

task void checkAcceleration() {
...
if (variance > accelVariance * ACCEL_NSAMPLES)
        call Leds.led2On(); /* ALERT! ALERT! */
        reportTheft()
    }
}
```

清单 6.16 防盗：更改设置

## 6.3.3 选择通信栈

迄今为止看到的代码中没有指定用于盗窃报告的通信栈，也没有指定区分盗窃报告和设置更新的 AM 类型。此信息在配置中指定，通过将组件连接到表示所需通信栈的组件来实现：这些组件具有兼容的签名，使得在栈之间切换变得容易：

```
configuration ActiveMessageC {
  provides interface SplitControl;
  ...
}
generic configuration AMSenderC(am_id_t id) {
  provides interface AMSend;
  ...
}
generic configuration AMReceiverC(am_id_t id) {
  provides interface Receive;
  ...
}

configuration SerialActiveMessageC{
  provides interface SplitControl;
  ...
}
generic configuration SerialAMSenderC(...){
  provides interface AMSend;
  ...
}
generic configuration SerialAMReceiverC(...){
  provides interface Receive;
  ...
}
```

清单 6.17 基于串行与无线电的 AM 组件

ActiveMessageC 包含 SplitControl 接口，用于启动和停止通信栈。使用特定 AM 类型实例化 AMSenderC 会创建一个组件，该组件提供 AMSend 接口，可为传输队列单个数据包，与所有其他 AMSenderC 实例无关。这简化了使用 AMSend 的模块的工作：只要它们一次只发送一个数据包，就能确保总能将数据包入队。最后，使用 AM 类型 k 实例化 AMReceiverC 并将 Receive 接口连接到你的代码，会自动将类型为 k 的接收数据包分发到你的 Receive.receive 事件处理程序。

防盗应用程序使用基于无线电的通信（mts300 传感器板在物理上通过串行连接进行接口）：

```
enum { AM_THEFT = 42, AM_SETTINGS = 43 };
...
components ActiveMessageC;
components new AMSenderC(AM_THEFT) as SendTheft;
components new AMReceiverC(AM_SETTINGS) as ReceiveSettings;
MovingC.CommControl -> ActiveMessageC;
```

```
MovingC.Theft -> SendTheft;
MovingC.Settings -> ReceiveSettings;
```

## 6.4 多跳网络：收集、传播和基站

 mote 网络通常比一组彼此在直接无线电范围内的 mote 复杂得多（在当前 mote 上通常只有 30m/100ft）。相反，多跳网络使用 mote 在发送方和接收方不在直接无线电范围内时中继消息。此外，一个或多个基站 mote 物理连接到 PC 级设备，通常由线路供电，将信息在更广阔的世界之间中继。因此，作为一个整体，传感器网络应用程序有三个部分（图 6.2）：

- Mote 代码：网络中 mote 上运行的代码。mote 之间的交互以发送和接收无线电消息的形式进行。
- 基站代码：在基站 mote 上运行的代码。它通过无线电消息与其它 mote 交互，并通过串行连接与 PC 交换数据包。
- PC 代码：在 PC 上运行的代码。

TinyOS 提供了两种基本的多跳网络抽象：树形收集和传播。在树形收集中，mote 组织成以特定 mote 为中心的路由树，根节点通常是基站 mote。树中发送的所有消息都会自动流向根节点（例如，沿图 6.2 中所示的链路）。收集树通常用于从传感器网络收集信息（例如传感器数据）。

传播在整个 mote 网络中高效地分发一个值（可以是包含多个字段的结构）。此外，任何 mote 都可以更新该值，整个网络最终会稳定到最近更新的值。传播通常用于 mote 应用程序的运行时配置。

在本节的其余部分，我们将修改 AntiTheft，使其使用收集和传播而不是 ActiveMessageC 来进行盗窃报告和配置。特别地，我们展示

![](img/53ede4f4266a5731b93bff15d85fa06a_118_0.png)

图 6.2 一个典型的传感器网络。

