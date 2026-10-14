

从编程的角度思考这个问题，收音机协议栈的接收部分需要经过以下步骤：

- 从收音机中读取数据包
- 检查数据包是否应发送确认
- 将收音机切换到发送模式
- 发送确认
- 将收音机恢复到接收模式

其中每个步骤通常都是一个独立的分阶段操作。例如在 CC2420 收音机上，每个操作都需要发送一条命令，通过 SPI 总线读取或写入数据。然而，这条 SPI 总线是多个芯片和子系统共享的：闪存存储驱动程序可能想在节点接收数据包的同时使用 SPI 总线读取数据。我们不能依赖 SPI 总线组件来调度多个未完成的请求，因为它可能会在收音机协议栈的两次操作之间插入一次大的闪存写入操作。我们需要一种方式让收音机协议栈请求对总线的独占访问，以便它能快速执行这五个操作，然后释放总线供其他模块使用。

还有许多其他情况，低级系统需要对硬件或软件资源进行独占访问，以保证正确性或延迟；我们稍后会介绍一些示例。

## 11.2.2 分阶段锁

TinyOS 通过分阶段锁支持对资源的独占访问。传统上，锁如互斥锁和信号量是阻塞式构造，用于保护临界区或共享数据结构。然而，由于 TinyOS 没有阻塞调用，其锁必须是分阶段的。组件调用命令请求电源锁，并在获取锁时接收事件。出于历史原因，锁接口被命名为 Resource：

```
interface Resource {
  async command error_t request();
  async command error_t immediateRequest();
  event void granted();
  async command void release();
  async command uint8_t getId();
}
```

Listing 11.13 The Resource interface

要获取锁，组件通常调用 request。在稍后的某个时间点，它会收到 granted 事件，表明它可以使用锁所保护的内容。命令 immediateRequest 是一种优化：它允许组件以单阶段操作获取空闲锁。如果 immediateRequest 返回 FAIL，则表示锁已被占用，组件必须调用 request。组件使用 release 命令释放锁。

需要加锁的抽象通常提供 Resource 接口。在未持有锁的情况下调用功能接口通常是被禁止的，可能会导致错误或不期望的系统行为。例如，这就是带有 MSP430 微控制器的节点为 SPI 总线提供的抽象：

```
generic configuration Msp430Spi0C() {
  provides interface Resource;
  provides interface SpiByte;
  provides interface SpiPacket;
  uses interface Msp430Spi0CConfiguration;
}
```

Listing 11.14 Msp430Spi0C signature

同样，这就是 ADC 的抽象：

```
generic configuration Msp430Adc12ClientC() {
  provides {
    interface Resource;
    interface Msp430Adc12SingleChannel;
    interface Msp430Adc12MultiChannel;
    interface Msp430Adc12Overflow;
  }
}
```

Listing 11.15 Msp320Adc12ClientC signature

## 11.2.3 锁内部结构

TinyOS 电源锁管理共享硬件资源的并发、能量和配置。电源锁有三个子组件：

- 一个 *arbiter*，控制锁定策略；
- 一个 *power manager*，控制能量策略；
- 以及一个或多个 *configurators*，为客户端配置硬件。

图 11.1 显示了这三个部分如何协同工作。arbiter 是控制的中心点。arbiter 从客户端接收锁请求，并根据这些请求调用 power manager 和 configurators。锁使用参数化接口和 unique() 来维护待处理的锁请求队列。每个锁客户端都有一个唯一的锁 ID，锁实现使用 uniqueCount() 来维护适当长度的队列。

