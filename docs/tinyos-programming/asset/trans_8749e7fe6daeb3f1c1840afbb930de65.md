

```
implementation {
    uint8_t bits[(77 + 7) / 8];
    ...
}
```

通用组件采用代码复制方法有两个原因：简单性和类型。如果通用模块不采用代码复制方法，那么将只有一个适用于组件所有实例的代码副本。当通用组件可以接受类型作为参数时，这会变得困难，因为分配大小、偏移量和其他考虑因素可能使真正单一的副本不可行。即使是非类型参数也可能产生此类问题，因为它们可用于指定数组大小、switch case 值等。出于类似原因，C++ 模板会为每组不同的模板参数创建一份代码副本。

最后，即使在实例之间共享代码是可能的，也需要在所有函数中添加一个参数，类似于面向对象语言中的 this 指针。该参数将指示正在执行的实例。此外，所有变量访问都必须从该指针偏移。在本质上，函数的执行时间和成本可能会显著改变（偏移而非常量访问）。为了提供简单、易于理解且运行时间高效的组件，nesC 采用代码复制方法，牺牲了可能的代码大小减少。

代码复制同样适用于配置和模块。复制一个模块会将可执行代码和变量复制到最终应用程序中。复制一个配置会复制组件和布线语句，可能导致进一步的组件实例化：

```
generic configuration DoubleBitVectorC(uint16_t maxBits) {
    provides interface Init;
    provides interface BitVector as Bits1;
    provides interface BitVector as Bits2;
}
implementation {
    components new BitVector(maxBits) as BV1;
    components new BitVector(maxBits) as BV2;

    Init = BV1; // Calling Init.init initializes
    Init = BV2; // both bitvectors
    Bits1 = BV1;
    Bits2 = BV2;
}
```

Listing 8.1 Instantiation within a generic configuration

实例化 DoubleBitVectorC 将创建并布线两个位向量。简而言之，通用模块定义了一段可重复的执行逻辑，而通用配置定义了组件之间可重复的组合模式。正如第 9 章将展示的那样，通用配置可以非常强大，并且通常是服务实现中最复杂的部分。

与标准组件不同，泛型只能由实例化它们的配置命名。例如，在 MyAppC 的情况下，没有其他组件可以布线到它实例化的 BitVectorC。泛型对 MyAppC 是私有的。使其可访问的唯一方法是通过布线其接口——在 MyAppC 的情况下，位向量仅对 MyAppP 可访问。使一个实例普遍可用的方法之一是创建一个单例配置并导出必要的接口。例如，假设你需要一个位向量来跟踪 37 个系统服务中的哪些正在运行或未运行。你希望许多组件能够访问此向量，但 BitVectorC 是一个泛型。因此你编写如下组件：

```
configuration SystemServiceVectorC {
  provides interface BitVector;
}
implementation {
  components MainC, new BitVectorC(37);
  MainC.SoftwareInit -> BitVectorC;
  BitVector = BitVectorC;
}
```

Listing 8.2 The fictional component SystemServiceVectorC

现在许多组件可以引用这个特定的位向量。SystemServiceVectorC本可以导出 BitVectorC.Init 而不是将其布线到 MainC，但那样只是要求在其他地方执行此布线。虽然你可以通过在一个配置中实例化它来将泛型制作成单例，但反之则不成立：组件要么可实例化，要么不可实例化。

## 8.2 Writing generic modules

如上例所示，通用模块（配置）的正文只是一个可以使用泛型的参数作为类型、常量等的模块（配置）。另一个例子是队列实现，QueueC：

```
generic module QueueC(typedef queue_t, uint8_t queueSize) {
  provides interface Queue<queue_t>;
}
implementation {
  queue_t queue[queueSize];
  uint8_t head = 0, tail = 0, size = 0;

  command queue_t Queue.head() {
    return queue[head];
  }
  ...
```

Listing 8.3 QueueC excerpt

