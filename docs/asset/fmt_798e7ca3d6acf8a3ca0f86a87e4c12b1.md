
| 字段 | 描述 |
| --- | --- |
| 管理 IP 地址 (Admin IP Address) | 此字段包含一个可用于管理目的、与 nPartition 中运行的操作系统通信的 IP 地址。此字段需要管理员通过 nPartition 命令行接口手动设置。如果设置了此值，分区管理器（Partition Manager）等管理工具能够与复杂系统中的每个 nPartition 通信，以收集系统特定信息，如操作系统类型和版本。 |
| 启动路径 (Boot Paths) | 此字段允许指定三个启动路径。主启动路径、高可用备用路径和备用启动路径都存储在此字段中。PCD 仅用于 HP 9000 nPartition 服务器上存储启动路径。HP Integrity nPartition 服务器使用不同的存储位置。由于这种差异，在管理 HP 9000 nPartition 服务器时，复杂系统中所有 nPartition 的启动路径都是可见的。然而，HP Integrity nPartition 服务器上的管理工具能够读取运行管理工具的那个 nPartition 的启动路径。 |

## nPartition 管理范式

HP nPartition 服务器支持三种管理范式。这些范式允许管理员以最适合其环境的模式管理 nPartition。这三种管理范式如下：

- 本地管理（Local Management）是管理 nPartition 最常用的范式，因为它是第一代 nPartition 服务器上支持的范式。本地管理意味着登录到复杂系统中的一个 nPartition，并直接在该 nPartition 上执行管理工具。使用本地管理，管理员有能力更改整个复杂系统，也可以将管理能力限制为仅影响本地 nPartition。
- 通过 nPartition 进行远程管理（Remote Management via an nPartition）允许管理员从中央管理站管理复杂系统。这使得管理更加高效，因为管理员不需要登录到每个要管理的 nPartition 并启动相应的管理工具。相反，管理工具可以从单一位置执行，并定向到每个要管理的 nPartition。此外，nPartition 上需要运行子集管理组件。
- 通过管理处理器（MP）进行远程管理（Remote Management via the MP）允许管理员在不向 nPartition 上运行任何管理组件的情况下，完全配置 nPartition 服务器。此外，这种管理提供了与通过 nPartition 进行远程管理相似的益处，以及从中央管理站管理复杂系统的能力。最后，这种管理范式还提供了一种即使在复杂系统中没有活跃的 nPartition 的情况下也能执行系统管理的方法。

## 本地 nPartition 管理范式

图 4-2 显示了本地 nPartition 管理范式。该范式适用于所有 HP nPartition 服务器。本地 nPartition 管理涉及登录到复杂系统中的一个 nPartition 并在本地 nPartition 上执行管理任务。这种架构开箱即用非常简单，因为只需要操作单个系统（nPartition）即可执行 nPartition 管理。然而，这种管理没有充分利用 HP nPartition 服务器提供的远程管理能力；该主题将在后续章节中讨论。

用于 HP 9000 nPartition 服务器的 nPartition 管理应用程序使用专有接口与 MP 通信以配置任务。此接口允许 nPartition 管理工具从复杂系统内的任何 nPartition 配置整个复杂系统。nPartition 管理工具对一个 nPartition 到另一个 nPartition 的配置更改提供了一些限制

# 第 4 章 nPartition 服务器

例如，不允许从另一个 nPartition 移除活跃的 nPartition。然而，从复杂系统中的任何 nPartition 都允许大多数操作。这提供了一个简单且灵活的管理模型，管理员可以登录到单个 nPartition 并执行若干影响其他 nPartition 的任务。在管理共享的 HP nPartition 服务器时，应考虑这种简单性和灵活性带来的影响。

包含 sx1000芯片组的第二代 HP nPartition 服务器使用智能平台管理接口（IPMI）协议作为 MP 与管理应用程序之间的接口。IPMI 是一种行业标准协议，旨在促进低级系统管理。对于包含 sx1000 芯片组及后续芯片集的 HP nPartition 服务器，HP-UX、Microsoft Windows 和 Linux 操作系统支持 IPMI 接口。在 HP nPartition 服务器的实现中，IPMI 支持两种与 MP 通信的传输机制：第一种块传输（BT），第二种是 LAN。这些通常被称为基于 BT 的 IPMI（IPMI/BT）和基于 LAN 的 IPMI（IPMI/LAN）。IPMI/BT 传输通过 nPartition 上的内核驱动程序与 MP 通信。nPartition 使用 MP 的 LAN 接口进行通信。

虽然 nPartition 管理在不同代 HP nPartition 服务器之间保持非常相似，但增加了一些增强功能。与图 4-2 以及使用 IPMI 接口相关的最显著增强是一个名为“nPartition 配置特权”（nPartition configuration privilege）的功能。可以通过列表 4-1 所示的方法在 MP 上启用此功能。nPartition 配置特权仅支持基于 sx1000 芯片组及后续芯片集的 HP nPartition 服务器。第一代 nPartition 服务器不支持此功能。

列表 4-1 启用 nPartition 配置特权

```
欢迎来到 rx620 管理服务器

(c) 1995-2003 惠普公司保留所有权利

版本 A501

MP 主菜单：

CO: 控制台
VFP: 虚拟面板（分区状态）
CM: 命令菜单
```

# HP 虚拟服务器环境

```
MP> cm
```

输入`HE`获取命令列表

```
MP:CM> parperm
```

此命令配置 nPartition 配置特权。

警告：当 nPartition 配置特权未限制时，分区发布的配置命令可能会影响另一个分区的配置。当此特权受限时，分区发布的配置命令无法影响未分配给该分区的硬件的分配。限制 nPartition 配置特权不会限制跨分区的处理器分配。

当前 nPartition 配置特权未限制。

您是否要限制分区配置（防止分区更改平台配置）？(Y/N)

-> 分区配置已禁用

```
MP:CM>
```

当 nPartition 配置特权启用（受限）时，只有来自请求源 PCD 数据结构的更改生效。因此，一个 nPartition 上的管理员无法更改 SCD 或其他 nPartition 的 PCD。为了更改 SCD 以及本地 nPartition 以外的 PCD 数据结构，管理员必须使用基于 LAN 的 IPMI 接口；将在下一节描述。

在图 4-2 中，紧邻 IPMI 或 HP 专有内核接口组件上方的是 nPartition 提供者。nPartition 提供者是一个实现基于网络的企业管理（WBEM）标准接口的软件组件。由于 HP nPartition 服务器提供了用于 nPartition 配置的行业标准 WBEM 接口，第三方管理工具能够与它们集成。

nPartition 提供者组件旁边是即时容量提供者。与 nPartition 提供者类似，即时容量提供者为 HP nPartition 服务器暴露了用于管理未许可组件的行业标准接口。

基础架构通过即时容量提供者（instant capacity provider）对 SCCD 和 PCD 数据结构的所有更改进行验证，以确保系统符合未授权资源的数量。在包含未授权组件的凸上，nPartition 配置更改必须通过运行 HP-UX 的 nPartition 进行。nPartition 提供者与即时容量提供者之间的接口被设计为：如果操作系统不是 HP-UX，则拒绝对带有未授权资源的凸进行任何配置更改。对于未购买未授权即时容量组件的系统，即时容量提供者将应用所有配置更改。

图 4-2 中 nPartition 提供者和即时容量提供组件上方是 WBEM 或 Windows 管理规范（WMI）服务器。当 nPartition 提供者运行在 HP-UX 和 Linux 操作系统上时，它在 WBEM 服务器的 Pegasus 开实现下运行。在 Microsoft Windows 操作系统上，nPartition 提供者利用 WMI 服务器。这使得 nPartition 提供者可以作为 Microsoft Windows 操作系统现有框架的一部分运行。
