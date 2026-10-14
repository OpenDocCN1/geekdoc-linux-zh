
正如我们前面所见，TinyOS 在以 C 结尾的组件（可外部使用的抽象）和 P（内部实现）之间做出区分。一旦你为可外部使用的组件编写了签名，更改它就非常困难：可能有任意数量的其他组件依赖于它，更改会导致编译错误。相比之下，由于内部实现仅由该软件抽象中的更高层配置进行连接，其签名要灵活得多。例如，更改 `LedsC` 的签名将破坏几乎所有 TinyOS 代码，但对 `LedsP` 的内部更改（并在 `LedsC` 中更改其连接）对用户来说应该是不可见的。

> 编程提示 11 如果一个组件本身是一个可用的抽象，其名称应以 C 结尾。如果它旨在成为更大抽象的内部和私有部分，其名称应以 P 结尾。永远不要从你的包（目录）外部连接 P 组件。

让我们看一个完整的（但非常简单）示例，说明所有这些问题是如何在 `RandomC` 中解决的。

如上所示，`RandomC` 映射到特定的实现 `RandomMlcgC`。`RandomMlcgC` 是一个配置，其主要目的是公开随机数实现（`RandomMlcgP`）并将其连接到启动序列（我们在下面进一步讨论组件初始化）：

```
configuration RandomMlcgC {
  provides interface Init;
  provides interface ParameterInit<uint16_t> as SeedInit;
  provides interface Random;
}
implementation {
  components RandomMlcgP, MainC;

  MainC.SoftwareInit -> RandomMlcgP; // Auto-initialize
  Init = RandomMlcgP; // Allow for re-initialization

  SeedInit = RandomMlcgP;
  Random = RandomMlcgP;
}
```

列表 4.13 `RandomMlcgC` 签名

`RandomMlcgP` 是一个软件实现。具有硬件随机数生成器的平台可以使用不同的 `RandomMlcgP`。因为这种不同的实现可能具有不同的签名——例如它可能需要通过抽象层访问寄存器——它也可能需要不同的 `RandomMlcgC`，以解决这些依赖关系并呈现完整的抽象。

简而言之，配置 `RandomC` 将标准数字生成器映射到特定算法 `RandomMlcgC`。配置 `RandomMlcgC` 将特定实现封装为完整的抽象。`RandomMlcgP` 是乘性线性同余生成器的软件实现。同样，还有 `RandomLfsrC`，它是线性反馈移位寄存器随机数生成器。就像 `RandomMlcgC` 一样，`RandomLfsrC` 是一个配置，它导出 `RandomLfsrP` 的接口并将其连接到启动序列。这种命名层次结构意味着系统如果关心使用哪一个，可以连接到特定的随机数生成器，也可以连接到 TinyOS 提供的通用随机数生成器（`RandomC`）。应用程序可以通过定义自己的 `RandomC` 来更改默认随机数生成器，该 `RandomC` 映射到不同的算法。TinyOS 开发者可以更改和改进 `RandomMlcgP`，而不必担心破坏应用程序代码。最后，平台实现者可以用经过优化的平台特定版本替换 `RandomMlcgC`，只要它具有与 `RandomMlcgC` 相同的签名即可。

## 4.2.2 组件初始化

`RandomMlcgP` 提供 `Init` 接口以使用节点的标识符（`TOS_NODE_ID`）为随机数生成器播种。`TOS_NODE_ID` 是 TinyOS 程序中的全局常量。TinyOS 教程描述了在将程序安装到 mote 上时如何设置它。`SeedInit` 使用特定种子启动生成器：

```
module RandomMlcgP {
  provides interface Init;
  provides interface ParameterInit<uint16_t> as SeedInit;
  provides interface Random;
}
implementation {
  uint32_t seed;

  /* Initialize the seed from the ID of the node */
  command error_t Init.init() {
    seed = (uint32_t)(TOS_NODE_ID + 1);
    return SUCCESS;
  }

  /* Initialize with 16-bit seed */
  command error_t SeedInit.init(uint16_t s) {
    seed = (uint32_t)(s + 1);
    return SUCCESS;
  }
  ...
}
```

`RandomMlcgC` 以两种不同的方式连接 `RandomMlcgP.init`：

```
MainC.SoftwareInit -> RandomMlcgP; // Auto-initialize
Init = RandomMlcgP.Init; // Allow for re-initialization
```

在第一种连接中，`RandomMlcgC` 将 `RandomMlcgP.init` 连接到 TinyOS 启动序列 `MainC`。TinyOS 启动时，它调用 `MainC` 的 `SoftwareInit.init`，因此调用 `RandomMlcgP` 的 `Init.init`。在第二种连接中，它将自己的 `RandomMlcgC.Init` 等同于 `RandomMlcgP.Init`。如果某个组件调用 `RandomMlcgC` 的 `Init.init`，实际上调用的是 `RandomMlcgP` 的 `Init.init`。

第一种连接确保 `RandomMlcgP` 在应用程序启动前已被正确播种。如果应用程序通过调用 `RandomMlcgC.Init` 或 `RandomMlcgC.SeedInit` 重新播种，也不会造成损害。但通过连接到 `MainC`，`RandomMlcgC` 确保应用程序 应用程序或协议、或系统 不必记住初始化 `RandomMlcgC`。

这种技术——“自动连接”初始化——在许多 TinyOS 抽象中使用。TinyOS 1.x 中一个非常常见的错误就是忘记初始化。这通常发生在多个组件可能初始化同一个组件的情况下。这种方法很浪费，但由于初始化只发生一次，所以不是什么大问题。更大的问题是，一个组件经常依赖于别人来初始化。例如，想象两个无线电协议栈 A 和 B。A 初始化定时器系统，B 没有。程序员编写了一个使用无线电协议栈 A 的应用程序，并且忘记初始化定时器系统。因为无线电协议栈 A 会初始化，所以一切正常。程序员随后决定切换到无线电协议栈 B，然后什么都不工作：应用程序和协议栈都不会初始化定时器，因此系统就挂起了。

使用自动连接初始化的组件的 `init` 命令按任意顺序调用 参见下文第 4.4 节。对于软件初始化——设置字段等——这通常无关紧要 `Init` 不应调用除另一个 `Init` 之外的任何东西。硬件初始化是一个更棘手的问题，通常按平台处理。有关更多详细信息，请参阅 TEP 107 [14]。

编程提示 12 在软件抽象的顶层配置中将 `Init` 自动连接到 `MainC`。

## 4.3 组件分层

`RandomC` 展示了即使是简单的抽象，例如随机数生成器，也可以在其内部具有多个层。一方面，这种编程风格使组件小而可重用：对于熟悉它们的人来说，构建新系统只是组合现有构建块并可能添加一点新逻辑的简单问题。另一方面，这意味着要深入到组件内部——弄清楚它到底做什么——对于不熟悉代码的人来说可能非常令人沮丧。`RandomC` 是这种分层的良好示例。程序员想要找到随机数生成器的实现 模块代码，必须查看三个文件。`RandomC` 指向 `RandomMlcgC`，而 `RandomMlcgC` 指向 `RandomMlcgP`。

### 4.3.1 可扩展性

实际上，这些间接层并非 nesC 特有：任何具有复杂库的系统都有它们。区别在于这些层是如何编写的。在 C 代码中，你可能会看到一系列简单的包装函数 例如 `printf` 作为向 `fprintf` 传递 `stdout` 作为文件流的调用：你遍历可执行代码。在 nesC 代码中，你通过配置遍历命名空间映射。第一次尝试深入到函数底部时，这种差异可能会有点令人困惑，但很快就会习惯。你也可以使用 nesC 的 `nesdoc` 工具在应用程序的连接中导航并找到接口最终的实现位置——有关更多信息，请参阅 TinyOS 教程。

正如其他语言，尤其是面向对象的语言一样，nesC 软件设计在实现有多简单以及使用或重用它们有多容易之间存在张力。`C++` 标准模板库以此而闻名：它功能强大、通用且高效，但理解其实现并非易事。将系统的所有功能放在单个模块中意味着用户无需追踪调用链。但这意味着修改系统需要替换或复制整个文件。这会导致代码复制，从而大大增加软件错误的生命周期 如果复制的代码中有错误，你需要更改所有副本，而几乎总是会忘记其中一个。因此，许多 TinyOS 核心抽象，例如定时器和通信，往往由许多小型组件组成。这使得系统在初次阅读时更难理解，但一旦理解，就很容易调整、替换或修改。

### 4.3.2 硬件特异性
