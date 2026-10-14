

## 3.4.1 Read

Read 接口是 TinyOS 分阶段数据采集的基础接口。大多数传感器驱动程序都提供 Read，其定义通用：

```
interface Read<val_t> {
  command error_t read();
  event void readDone(error_t err, val_t val);
}
```

清单 3.25 Read 接口

例如，生成 16 位值的传感器驱动程序提供 Read<uint16_t>。如果 Read 的提供者在对 read 的调用返回 SUCCESS，则它将在未来发出 readDone，并将 Read 的结果作为 val 参数传回给事件处理程序。

## 3.4.2 Send

TinyOS 基础的分组传输接口 Send 也是一个分阶段操作。然而它稍微复杂一些，因为它需要传递一个待传输分组的指针：

```
interface Send {
  command error_t send(message_t* msg, uint8_t len);
  event void sendDone(message_t* msg, error_t error);

  command error_t cancel(message_t* msg);
  command void* getPayload(message_t* msg);
  command uint8_t maxPayloadLength(message_t* msg);
}
```

清单 3.26 分阶段 Send 接口

Send 的提供者定义 send 和 cancel 函数并可以发出 sendDone 事件。相反，Send 的使用者需要定义 sendDone 事件并可以调用 send 和 cancel 命令。当对 send 的调用返回 SUCCESS 时，msg 参数已被传递给提供者，后者将尝试发送该分组。当发送完成时，提供者发出 sendDone，并将指针传回给使用者。这种指针传递方式在需要传递较大数据项的分阶段接口中很常见。下一节将更详细地讨论内存管理。

## 3.5 模块内存分配、避免递归及其他细节

除了电量之外，对 mote 系统最宝贵的资源是 RAM。电量意味着无线电和 CPU 几乎必须一直处于关闭状态。当然，存在需要大量 CPU 或大量带宽的情况，例如密码学或二进制分发，但

![](img/53ede4f4266a5731b93bff15d85fa06a_60_0.png)

图 3.5 微控制器上的典型内存布局。由于没有内存保护，堆栈很容易溢出到堆或数据区。

出于必要性，这些情况必须是罕见的。相比之下，RAM 的全部意义在于它始终可用。今天大多数 mote 使用的微控制器的睡眠电流在很大程度上由 RAM 决定。

模块通过声明变量来分配内存，这些变量遵循 nesC 的作用域规则，完全私有化于组件。例如，CountingGetC 组件（清单 3.20，第 32 页）将 count 分配为 8 位模块级变量，成本为 1 字节 RAM。由于 TinyOS 使用分阶段操作且不提供线程，因此不存在长期存在的栈分配数据。因此，当 TinyOS 系统处于空闲状态时，这些模块变量代表了系统的整个软件状态。

通常，nesC 不鼓励通过 malloc 或其他 C 库调用进行动态内存分配。你可以调用它们，但大多数嵌入式微控制器缺乏内存保护，使得其使用特别危险。图 3.5 显示了微控制器上的典型内存布局。堆栈向下增长，堆向上增长，由于没有硬件内存保护，两者可能相撞，一旦发生，混乱不可避免。

相反，你应该将内存作为模块变量进行分配。例如，如果一个模块需要一个缓冲区来保存传感器读数，它应该静态分配该缓冲区。在其他情况下，创建可重用的抽象数据类型以及在通用组件中实现状态和操作是方便的，如 BitVectorC（清单 3.23，第 34 页）。最后，组件有时需要共享一个内存池。一个常见例子是一组共享分组缓冲区池的组件。共享池允许多个协作组件摊销其需求，特别是如果它们不太可能同时都需要大量内存。通过完全避免使用堆，运行时内存故障的唯一原因是堆栈。

为了避免堆栈溢出，TinyOS 程序应避免递归且不声明任何大的局部变量（例如数组）。在单个模块内避免递归很容易，但在像 nesC 这样的基于组件的语言中，很容易在组件边界之间无意中创建递归循环。例如，假设组件 A 使用 Read 接口反复采样由组件 B 提供的传感器，即 A 中的 readDone 事件处理程序调用 B 的 read 命令。如果 B 恰好是一个简单的传感器，它可能会选择在 read 命令的实现内部直接发出 readDone 事件。然而，这个程序现在包含了一个非预期的递归循环：A 调用 B 的 read 命令，该命令发出 A 的 readDone 事件，该事件调用 B 的 read 命令……

