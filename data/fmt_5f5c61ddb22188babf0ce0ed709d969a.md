
```
generic module VirtualizeTimerC(typedef precision_tag, int max_timers)
{
  provides interface Timer<precision_tag> as Timer[uint8_t num];
  uses interface Timer<precision_tag> as TimerFrom;
}
...
```

### 清单 9.19 VirtualizeTimerC 虚拟化单个计时器

接受一个精度为 `precision_tag` 的计时器，并将其虚拟化为 `timer_count` 个精度为 `precision_tag` 的计时器。计时器库还包含在精度之间进行转换的组件。

`HiiTimerMilliC` 接收一个中断驱动的硬件计时器 – `AlarmCounterMilliP` – 并将其转换为虚拟化计时器。它通过三个步骤完成此操作。第一步使用泛型组件 `AlarmToTimerC` 将中断驱动的 `Alarm` 转换为基于任务的 `Timer`：

```
AlarmToTimerC.Alarm -> AlarmCounterMilliP;
```

第二步将单个计时器虚拟化为多个计时器：

```
VirtualizeTimerC.TimerFrom -> AlarmToTimerC;
```

`HiiTimerMilliC` 然后导出参数化计时器接口：

```
TimerMilli = VirtualizeTimerC;
```

此外，计时器系统的某些方面需要能够访问时间基准，例如指定计时器在未来何时触发。因此 `HiiTimerMilliC` 接收一个硬件计数器并将其转换为本地时间组件，

```
CounterToLocalTimeC.Counter -> AlarmCounterMilliP;
```

然后导出接口：

```
LocalTime = CounterToLocalTimeC;
```

计时器库中的许多组件都是泛型，因为平台可能需要提供各种计时器。例如，根据计数器、比较寄存器及其位宽的数量，平台可能提供毫秒、微秒和 32 kHz 计时器。例如，一些平台使用的 `MSP430` 芯片家族的变体可以轻松提供 32 位毫秒和 32 kHz 计时器，同时保持非常低的中断负载。

泛型模块对于需要分配每个客户端状态的抽象来说非常有效，例如计时器。泛型模块允许你在实例化模块的配置中指定大小 – 客户端数量，而不是在模块本身内部指定。例如，如果 `VirtualizeTimerC` 不是泛型，那么在其代码内部就必须有一个带有适当键的 `uniqueCount()`。

> **编程提示 20**
>
> 在编写模块时，请考虑使其更通用和泛型。在大多数情况下，模块必须由配置包装后才有用，因此单例模块的优势很少。

### 9.4 练习

- 1. 使用 TinyOS 计时器库创建一个秒级粒度计时器抽象 `TimerSecondC`。如果你基于 `TimerMilliC` 进行虚拟化，那么底层计时器只需为所有秒级粒度计时器扫描一个计时器条目。请注意 `HifTimerSecondC` 参数化接口的唯一键。

- 2. 标准 TinyOS 集合层 `CTP`（位于 `tos/lib/net/ctp`）将数据包在多个跳数间路由到数据汇聚节点。`CTP` 的发送队列深度为 `C + F`，其中 `C` 是发送客户端的数量，`F` 是其用于转发的包池大小。这意味着客户端最多可获得可用链路吞吐量的 `1/(C+F)`。更改 `CtpForwardingEngineP` 和 `CollectionSenderP`，使其具有单独的客户端队列，该队列位于 `CtpForwardingEngineP` 队列的单个条目之上，导致客户端最多获得链路吞吐量的 `1/(C+F)`。

- 3. 为任意数量的客户端编写一个屏障。屏障是一种并发原语，阻塞直到所有线程到达它。在 TinyOS 中，由于没有线程，这意味着阻塞直到所有调用者到达它。编写一个分阶段接口 `Barrier`，它有一个命令 `wait` 和一个事件 `pass`。当所有客户端都调用 `wait` 时，屏障应向所有客户端发出 `pass` 信号。

# 10 设计模式

引用 Gang of Four 的话，设计模式是“在特定上下文中为通用设计问题定制的通信对象和类的描述”。[3] 在我们迄今为止看到的组件中，我们看到了几种反复出现的模式，例如使用参数化接口来实现具有多个客户端的服务（`VirtualizeTimerC`，第 9.1.3 节），或一个组件包装另一个组件（`RandomC`，第 4.2 节）。在本章中，秉承 Gang of Four 原始设计模式工作的精神，我们尝试基于在 TinyOS 开发期间的观察来形式化其中一些模式。

本章介绍了八种 nesC 设计模式：三种行为型（涉及组件交互）：`Dispatcher`、`Decorator` 和 `Adapter`；三种结构型（涉及应用程序的结构）：`Service Instance`、`Placeholder` 和 `Facade` 以及两种命名空间（管理诸如消息类型等标识符）：`Keyspace` 和 `Keymap`。每个模式的介绍遵循《设计模式》一书的模型。每个模式都有一个 Intent，简要描述其目的。随后是更深入的 Motivation，提供来自 TinyOS 的示例。`Applicable When` 提供使用条件简明列表，组件图显示了模式中组件交互的结构。¹ 除了我们通常的组件图约定外，我们将折叠子框附加到组件以显示相关代码片段（浮动的折叠框代表某些其他、未命名组件中的源代码）。图后跟 Participants 列表，解释每个组件的角色。`Sample Code` 显示示例 nesC 实现，`Known Uses` 指出 TinyOS 中模式的一些使用。`Consequences` 描述模式如何实现其目标，并指出使用时需要考虑的问题。最后，`Related Patterns` 与其他相关模式进行比较。

### 10.1 行为型：Dispatcher

#### Intent

基于标识符在操作集合中动态选择。提供一种通过添加或更改操作轻松扩展或修改系统的方式。

¹ 此图因 `Keyspace` 模式不涉及组件交互而被省略。

#### 动机

在高层次上，传感器网络应用会根据环境输入（如传感器读数或网络数据包）执行操作。输入的呈现组件并不关心操作的细节。我们需要能够轻松地扩展和修改应用程序关心的输入，以及与输入相关联的操作。

例如，一个节点可以接收多种类型的活动消息（数据包）。活动消息（AM）有一个 8 位类型字段，用于区分协议。洪泛协议使用一种 AM 类型，而按需路由协议使用另一种。`ActiveMessageC` 是信号数据包到达的组件，不应需要知道协议执行何种处理或应用程序是否支持该协议。`ActiveMessageC` 只负责传递数据包，而更高层的通信服务则响应它们关心的部分。

解决此问题的传统方法是使用函数指针或对象，在运行时动态注册为回调。在许多情况下，尽管在运行时注册，操作集合在编译时是已知的。因此这些回调可以用编译到可执行文件中的分发表来替换，具有两个好处。首先，这允许更好的跨函数分析和优化，其次它节省 RAM，因为无需存储指针或回调结构。

这样的分发表可以通过在 `ActiveMessageC` 中使用 `switch` 语句为活动消息示例构建。但这非常不灵活：对应用程序中使用的协议的任何更改都需要对系统组件进行更改。

TinyOS 中更好的方法是使用 `Dispatcher` 模式。`Dispatcher` 使用基于数据标识符的参数化接口调用操作。在 `ActiveMessageC` 的情况下，接口是 `Receive`，标识符是活动消息类型字段。`ActiveMessageC` 与应用程序处理哪些消息或这些处理程序执行何种处理无关。添加新的处理程序只需要一次对 `ActiveMessageC` 的连线。如果应用程序未为某种类别连线接收处理程序，`ActiveMessageC` 默认执行空操作。

调度器模式的另一个例子是为 TinyOS 1.x 实现的 Mate 虚拟机的调度器。每个指令都是一个单独的组件，提供 `MateBytecode` 接口。调度器通过使用参数化 `MateBytecode` 接口分派到指令组件来执行特定字节码。通过更改调度器的连线，可以轻松更改指令集。

#### 适用场景

- 组件需要支持可外部自定义的一组操作。
- 一个原始整数类型可以标识要执行的操作。
- 所有操作都可以用单一接口实现。

然而，分发器通常被封装在通用配置中以简化其使用。组件不是连线到参数化接口，而是连线到接收参数作为参数的通用配置。例如，而不是直接连线到 `ActiveMessageC` 以接收数据包，应用程序实例化一个 `AMReceiverC`：
