
-   服务实例：用于标识各个服务的标识符构成一个本地键空间。
-   调度器：调度器使用的标识符通常取自全局键空间。

## 10.4 命名空间：键映射

### 意图

将键从一个键空间映射到另一个键空间。允许你将全局共享名称转换为本地优化名称，或有效地对另一个键空间进行子集划分。

### 动机

命名空间之间的映射通常很有用：它允许节点使用全局稀疏的命名空间以方便跨应用通信，同时使用内部紧凑的命名空间以提高效率。

Drip流行病传播协议使用键空间和键映射模式，允许用户在运行时配置参数。组件使用全局键空间向DisseminatorC泛型组件注册参数，从而可以以与应用程序无关的方式命名该参数。用户通过使用流行病传播协议发送一个键值对来修改参数，该协议将更改分发到每个节点。Drip为每个键值对维护一个特殊的“滴流”计时器，并通过本地键空间访问以提高效率。键映射将全局键映射到本地键。

当某个基于服务实例模式的服务访问另一个同样基于服务实例模式的服务提供的资源子集时，键映射对于两个本地键空间之间的映射也很有用。

例如，BlockStorageC、LogStorageC和ConfigStorageC组件（第6.5节）的Atmel AT45db实现使用各自的本地键空间来标识其各自的客户端。这三者都构建在更低层的At45dbC组件之上，该组件也使用自己的本地键空间来标识其客户端。因此，例如BlockStorageC的每个客户端都间接是At45dbC的客户端。键映射将BlockStorageC的客户端标识符映射到At45dbC的客户端标识符。

```
DisseminationEngineP.TrickleTimer[key] ->
DisseminationTimerP.TrickleTimer[TIMER_ID];
...
```

在这个例子中，用户可以生成一个新的配置值，并基于DISS_CONFIG键进行分发。DisseminatorEngineP使用全局键来引用该值，但DisseminationTimerP可以使用本地键来引用其为“滴流”计时器维护的状态。该连接在编译时简化为一个简单的switch语句，它以正确的本地键调用DisseminationTimerP。

BlockStorageP在闪存芯片卷上提供简单的读/写抽象。在内部，BlockStorageC是使用BlockStorageP组件提供的服务实例模式来实现的。BlockStorageP的每个客户端也是At45dbC的客户端（这简化了BlockStorageC的实现）。由于At45dbC还有其他客户端，BlockStorageC必须将BlockStorageP标识符映射到At45dbC标识符：

```
generic configuration BlockStorageC(volume_id_t volId) {
  provides interface BlockWrite;
  provides interface BlockRead;
}
```

```
implementation {
  enum {
    BLOCK_ID = unique(UQ_BLOCK_STORAGE),
    AT45DB_ID = unique(UQ_AT45DB)
  };
}
```

```
components BlockStorageP, At45dbC;
BlockWrite = BlockStorageP.BlockWrite[BLOCK_ID];
BlockRead = BlockStorageP.BlockRead[BLOCK_ID];
BlockStorageP.Resource[BLOCK_ID] -> At45dbC.Resource[AT45DB_ID];
...
```

假设BLOCK_ID为2，AT45DB_ID为4。那么，当对BlockRead[2]（或BlockWrite[2]）接口的请求到来时，BlockStorageP会对其Resource[2]接口发出请求。键映射按预期将该请求转换为对At45dbC.Resource[4]的请求。

### 已知用途

-   Drip分发协议——如上所述——使用键映射。
-   用于ST M25P和Atmel AT45DB系列闪存芯片的TinyOS存储系统（后者如上所述）使用键映射。

### 后果

键映射使用nesC连接使组件能够透明地在不同键空间之间进行映射。与键空间一样，键映射必须在编译时固定。

键映射在编译时转换为一个switch。因此它不消耗任何RAM；其速度取决于用于编译nesC输出的C编译器的行为。
