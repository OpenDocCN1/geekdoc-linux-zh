

`message_t` 类型用于声明 TinyOS 网络协议的包缓冲区，如 TEP 111 中所述：message_t [15]。

## A.2.1 单跳

TinyOS 有四个标准的单跳通信组件，全部以 AM 类型作为参数，一个 8 位数字，用于标识不同的包类型。主动消息地址为 16 位。TinyOS 定义了宏 TOS_BCAST_ADDR 用于 AM 广播地址，并且节点可以通过 AMPacket 接口找到其本地地址。

AMSenderC 发送数据包。AMReceiverC 针对发往该节点的包发出接收信号，包括广播地址；AMSnooperC 针对未发往该节点的包发出接收信号；AMSnoopingReceiverC 无论寻址如何都发出所有包的接收信号。AM 接口会自动丢弃未通过链路层 CRC 检查的包。PacketAcknowledgements 接口允许发送方请求链路层确认并在发送后检查是否收到确认：可以在 Send.sendDone 中调用 PacketAcknowledgements.wasAcked。

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
```

```
interface AMPacket;
}
```

默认情况下，射频栈处于关闭状态。你必须打开它才能发送和接收数据包。最简单的方法是通过 SplitControl 接口将其置于全功率（始终开启）模式。下面的低功耗部分（第 251 页）展示了如何将其打开到低功耗状态，其中节点会定期唤醒以监听数据包。对于全功率控制，请在 ActiveMessageC 上连接并调用 SplitControl.start。

```
configuration ActiveMessageC {
  provides {
    interface SplitControl;
    // interfaces elided here
  }
}
```

有关这些组件及其接口的更多详细信息，请参阅 TEP 116：Packet Protocols [16]。AM 组件通常位于 tos/system 中。

上述组件全部用于无线电通信：对于通过串口连接的 mote 也有这些组件的版本：SerialActiveMessageC、SerialAMSenderC 和 SerialAMReceiverC。这些组件在 TEP 113：Serial Communication [7] 中有描述。请注意，串行栈不执行地址过滤，因此没有嗅探功能。

## A.2.2 多跳收集

收集协议为将自身广告为数据汇点的节点构建路由树。通常，汇点节点通过串行电缆或其他介质连接到 PC，尽管有时它们会将接收到的所有数据记录到非易失性存储中。虽然在良好条件下收集协议可以达到 99.9% 或更好的可靠性，但它们不保证可靠性：发送方不会收到其数据包是否到达的反馈。

收集实现可以在 tos/lib/net 中找到。例如，收集树协议（CTP）实现可以在 tos/lib/net/ctp 中找到，而 MultihopLQI 实现可以在 tos/lib/net/lqi 中找到。

要发送数据包，程序实例化一个 CollectionSenderC。要将节点配置为基站，它应连接到 CollectionControlC 以调用 RootControl.setRoot 以及实例化相关的 CollectionReceiverC 服务。收集客户端采用收集标识符，类似于 AM 类型。

```
generic configuration CollectionSenderC(collection_id_t collectid) {
  provides {
    interface Send;
    interface Packet;
  }
}
```

```
generic configuration CollectionReceiverC(collection_id_t collectid) {
  provides {
```

