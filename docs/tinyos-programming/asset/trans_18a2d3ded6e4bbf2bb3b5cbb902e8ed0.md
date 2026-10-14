

请注意，你必须通过调用 DisseminationC.StdControl 来启动分发。有关分发的更多详细信息，请参阅 TEP 118：分发 [18]。

### A.2.4 二进制重编程

第四种常见的通信抽象是二进制重编程。这实际上并不是一种抽象，因为应用程序不会主动使用它发送数据包。相反，它是一种自动运行的服务。它使管理员能够在 TinyOS 网络中安装新的二进制映像。这些二进制文件存储在闪存上，并且可以进行安装。请注意，如果新映像没有安装二进制重编程功能，那么你就无法卸载它！

Deluge（位于 tos/lib/net/Deluge）是标准的二进制分发实现 [9]。它构建在基础分发之上，用于安装大型（许多 kB）数据项。Deluge 没有提供用于控制其行为的 TinyOS API，而是附带命令行工具，这些工具将必要的报文注入网络。更多细节请参阅 TinyOS 文档中的 Deluge 手册。

## A.3 时间

TinyOS 有两个定时器接口：Timer 和 Alarm。Timer 是同步的，在任务上下文中运行；Alarm 是异步的，涉及直接处理硬件中断。大多数情况下，应用程序使用 Timer。一些底层系统（如 MAC 协议）或需要精确定时的应用程序使用 Alarm。此外，节点可以通过 LocalTime 接口访问其本地时间。节点的本地时间从启动时开始计算，因此不同节点通常不具有相同的时间。

基本的 Timer 抽象是 TimerMilliC：

```
generic configuration TimerMilliC() {
  provides interface Timer<TMilli>;
}
```

可以通过 LocalTimeMilliC 获取本地时间：

```
generic configuration LocalTimeMilliC() {
  provides interface LocalTime<TMilli>;
}
```

由于 Alarm 通常是一种 HAL（硬件抽象层）而非 HIL（硬件无关层）抽象（第 12 章），因此没有提供 Alarm 的标准组件。我们在第 6.1 节和第 13 章中介绍了定时。有关定时器和时间的更多详细信息，请参阅 TEP 102：定时器 [25]。

## A.4 传感

TinyOS 中的传感器遵循 TEP 109：传感器与传感器板 [5] 中描述的命名约定。通常，它们以实际的传感器芯片命名。因此，几乎没有“标准”的传感器组件名称，因为节点可能具有的传感器集合取决于其硬件。不过，TEP 109 还描述了传感器应提供哪些接口，因此通常很容易编写与具体传感器无关的代码。

传感器通常提供一个或多个 TEP 114：SIDs：源与宿无关驱动程序 [28] 中描述的通用传感接口。

TinyOS 提供了两个完全由软件实现的“模拟”传感器。第一个 ConstantSensorC 接受一个常量作为参数，并始终返回该值。第二个 SineSensorC 从正弦函数返回一个值，该函数的输入在每次采样时递增。各平台还有一个 DemoSensorC，它要么实例化这些软件传感器之一，要么是对特定硬件传感器的封装。

```
generic module ConstantSensorC(typedef width_t @integer(), uint32_t val) {
  provides interface Read<width_t>;
}
```

```
generic module SineSensorC() {
  provides interface Read<uint16_t>;
}
```

```
generic configuration DemoSensorC() {
  provides interface Read<uint16_t>;
}
```

我们在第 6.2 节和第 13 章中介绍了传感器。

## A.5 存储

TinyOS 提供了三种基本的存储抽象。配置存储（Config storage）用于小型随机访问变量，例如配置常量。日志存储（Log storage）用于仅追加写入以及随机访问、顺序读取。块存储（Block storage）用于大型随机访问数据项。第 6.5 节更详细地介绍了它们的用途和权衡。

TinyOS 有一些脚本，可以根据 XML 规范生成命名存储卷的布局。布局本质上就是每个卷的起始偏移量及其长度。存储客户端将卷 ID 作为参数，从而可以访问这些生成的常量。更多细节请参阅 TEP 103：永久数据存储（Flash）[4]。

```
generic configuration BlockStorageC( volume_id_t volume_id ) {
  provides interface BlockRead;
  provides interface BlockWrite;
  provides interface StorageMap;
}
```

```
generic configuration LogStorageC( volume_id_t volume_id, bool circular ) {
  provides interface LogRead;
  provides interface LogWrite;
}
```

