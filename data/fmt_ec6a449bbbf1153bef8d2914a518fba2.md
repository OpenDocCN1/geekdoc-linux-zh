
```
generic module BitVectorC(uint16_t max_bits) {
    provides interface BitVector;
}
```

### A.6.2 QueueC

`QueueC` 提供了具有固定最大大小的项目队列的抽象。它接受两个参数：它存储的项目的类型和队列的最大大小。`Queue` 接口具有在队列末尾入队项目、从队列头部出队项目以及检查队列大小的命令。它还允许随机访问查找：你可以扫描队列。

```
generic module QueueC(typedef queue_t, uint8_t QUEUE_SIZE) {
    provides interface Queue<queue_t>;
}
```

### A.6.3 BigQueueC

`QueueC` 的 `uint8_t` 参数将其最大大小限制为 255。对于大多数用途来说，这已经足够，因此为了支持更大的大小而浪费额外的字节在内部字段上是不值得的。然而，有时组件需要更大的队列。例如，`printf` 库（第 250 页）有一个要发送的字节队列，通常长于 255。因此 TinyOS 还有 `BigQueueC`，它本质上与 `QueueC` 相同，只是它有一个 16 位大小参数并提供接口 `BigQueue`：

```
generic module BigQueueC(typedef queue_t, uint16_t QUEUE_SIZE) {
  provides interface BigQueue<queue_t> as Queue;
}
```

### A.6.4 PoolC

`PoolC` 是 TinyOS 最接近动态内存分配器的东西。它接受两个参数：要分配的对象类型，以及数量。然后组件可以动态地从池中分配和释放这些对象。但由于最大池大小是在编译时设置的，内存泄漏会导致池耗尽，而不是导致堆和栈碰撞。

由于它执行分配，你向 `PoolC` 指定一个类型，但其命令使用指向该类型的指针。例如，如果你分配一个 `message_t` 缓冲区池，那么对 `Pool` 的调用会传递 `message_t*`。

```
generic configuration PoolC(typedef pool_t, uint8_t POOL_SIZE) {
  provides interface Pool<pool_t>;
}
```

你可以在池之间交换数据项。例如，如果你有两个单独的 `message_t` 池 `P1` 和 `P2`，从 `P1` 分配 `M1` 并从 `P2` 分配 `M2` 是可以的，然后将 `M1` 释放到 `P2` 并将 `M2` 释放到 `P1`。这种行为对于 `Receive` 的缓冲区交换语义至关重要。如果组件接收到一个想要转发的包，它会从其池中分配一个缓冲区并将此新缓冲区返回给链路层。下一个包——其缓冲区来自池——可能会去到另一个组件，该组件有自己的池。因此，转发包的伪代码看起来像这样：

```
receive(m):
    if (!forward(m)):
        return m
    setHeaders(m)
    queue.put(m)
    m2 = pool.get()
    return m2
```

### A.6.5 StateC

`StateC` 提供了状态机的抽象。当多个组件需要共享全局状态时很有用（例如子系统是否打开或关闭）。

```
generic configuration StateC() {
    provides interface State;
}
```

### A.7 实用工具

TinyOS 提供了用于多个常用函数和抽象的组件。

#### A.7.1 随机数

`RandomC` 提供接口 `Random`，组件可以使用它来生成随机数。`RandomC` 还提供接口 `Init` 和 `ParameterInit`，以便组件可以重新初始化 `RandomC` 的随机种子。默认情况下，`RandomC` 的种子初始化为节点 ID+1。

TinyOS 包含两个随机数生成器：`RandomMlcgC`（乘法线性同余生成器）和 `RandomLfsrC`（线性反馈移位寄存器生成器）。`RandomLfsrC` 更快，但 `RandomMlcgC` 产生更好的随机数。默认情况下，`RandomC` 引用 `RandomMlcgC`。

```
configuration RandomC {
    provides interface Init;
    provides interface ParameterInit<uint16_t> as SeedInit;
    provides interface Random as Random;
}
```

```
configuration RandomMlcgC {
    provides interface Init;
    provides interface ParameterInit<uint16_t> as SeedInit;
    provides interface Random as Random;
}
```

```
configuration RandomLfsrC {
    provides interface Init;
    provides interface ParameterInit<uint16_t> as SeedInit;
    provides interface Random as Random;
}
```

#### A.7.2 Leds

`LedsC` 提供了三个 LED 的抽象。虽然一些平台有超过或少于三个，但出于历史原因，`Leds` 接口有三个。此外，拆分 LED

将同一个接口实例化为三个实例会产生大量额外的布线。除了 `LedsC` 之外，还有一个 `NoLedsC`，可以作为空替换插入：对 `NoLedsC` 的调用不执行任何操作。

```
configuration LedsC {
  provides interface Leds;
}
```

```
configuration NoLedsC {
  provides interface Leds;
}
```

#### A.7.3 循环冗余校验

循环冗余校验（CRCs）是检查数据是否已损坏的一种简单方法。在数据之后，你附加一个 CRC。读取数据的人可以重新计算数据的 CRC 并检查它是否与附加的 CRC 匹配。如果两者不匹配，则数据或 CRC 本身存在位错误。由于 CRC 通常比数据短得多，因此假设数据已被损坏。CRCs 在网络中被大量使用，以检查数据包的有效性。当然，由于 CRCs 比数据本身短，因此损坏的数据包通过 CRC 检查是可能的，但可能性很小。

CRC 值与加密哈希不同。CRCs 的目的是检测突发位错误。通常，n 位 CRC 总能检测到小于 n 位的单次错误突发。相比之下，加密强度高的哈希具有熵特性，使得检测到（或未能检测到）任何类型错误的机会是均匀的。

```
module CrcC {
  provides interface Crc;
}
```

模块 `CrcC` 可以在 `tos/system` 中找到。

#### A.7.4 Printf

有时，在调试时，让 mote 发送简单的文本消息会非常有用。TinyOS 有一个 `printf` 库——类似于 C 标准库函数——用于此目的。你可以在组件中使用 `printf`，而 `printf` 库会通过串行端口发送适当的包。你必须通过 `PrintfC` 的 `SplitControl.start` 启动 `printf` 库。

```
configuration PrintfC {
  provides (
    interface SplitControl as PrintfControl;
    interface PrintfFlush;
  )
}
```

有关使用 `printf` 库的更多详细信息，请参阅 TinyOS 网站上的教程。

### A.8 低功耗

在大多数情况下，TinyOS 会自动将系统和硬件置于可能的最低功耗状态。对于外设，这通常通过电源锁实现（第 11.2 节）。例如，当应用程序从闪存芯片写入或读取时，TinyOS 会自动将其打开，执行操作，然后在完成后将其关闭。

通信是此行为的主要例外。由于通信子系统，例如无线电和串行端口，需要能够接收和发送，TinyOS 需要应用程序通过 `SplitControl` 接口明确告知它何时可以安全地打开和关闭它们。

然而，在无线电的情况下，有许多技术可以用来节省电量。例如，而不是始终保持无线电开启，TinyOS 可以让它大部分时间处于关闭状态，定期将其打开足够长的时间以听是否有数据包。发送方多次发送数据包，直到接收方唤醒、听到它并确认它，或者超时发生。

关于如何设置这些间隔的完整讨论超出了本书的范围。重要的接口是 `LowPowerListening`，一些（但不是全部）无线电提供。`LowPowerListening` 允许应用程序设置无线电的检查间隔以及它期望接收方使用的检查间隔。TinyOS 有一个教程，介绍如何在编写低功耗应用程序时使用此接口，第 12.2.3 节也简要举例说明了其用法。

[18] P. Levis and G. Tolle. TEP 118: Dissemination. www.tinyos.net/ tinyos-2.x/doc/.
