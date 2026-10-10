

## 第 9 章. PCMCIA 和 Compact Flash

### 本章内容

- 什么是 PCMCIA/CF？ 258
- Linux-PCMCIA 子系统 260
- 主机控制器驱动程序 262
- PCMCIA 核心 263
- 驱动程序服务 263
- 客户端驱动程序 264
- 整合各个部件 271
- PCMCIA 存储 272
- 串行 PCMCIA 272
- 调试 273
- 查看源代码 275

如今流行的技术，例如无线和有线以太网、*通用分组无线业务*（GPRS）、*全球定位系统*（GPS）、微型存储和调制解调器，普遍采用 PCMCIA（*个人电脑存储卡国际协会*的缩写）或 *CF*（*紧凑闪存*）卡的形式。大多数笔记本电脑和许多嵌入式设备都支持 PCMCIA 或 CF 接口。因此，它们可以立即利用这些技术。在嵌入式系统中，PCMCIA/CF 插槽提供了一种技术升级路径，而无需重新设计电路板。例如，一种低成本版本的互联网设备可以使用 PCMCIA 拨号调制解调器，而一种高端版本则可以支持 WiFi。

Linux 内核支持多种架构上的 PCMCIA 设备。在本章中，让我们探讨内核中针对 PCMCIA/CF 主机适配器和客户端设备的支持情况。

### 什么是 PCMCIA/CF？

PCMCIA 是一种 16 位数据传输接口规范，最初用于内存卡。CF 卡更小，但兼容 PCMCIA，常用于 PDA 和数码相机等手持设备。CF 卡只有 50 个引脚，但可以使用无源 CF 转 PCMCIA 适配器插入笔记本电脑的 68 针 PCMCIA 插槽中。PCMCIA 和 CF 一直局限于笔记本电脑和手持设备领域，尚未进入台式机和更高端的机器市场。

PCMCIA 规范现在已经发展以支持更高速率的形式，即 32 位 *CardBus* 卡。当指代 PCMCIA 或 *CardBus* 设备时，使用 *PC 卡* 这一术语。*CardBus* 更接近 PCI 总线，因此内核已将 *CardBus* 设备的支持从 PCMCIA 层移至 PCI 层。PCMCIA 行业标准组织的最新技术规格是 *ExpressCard*，它与 *PCI Express* 兼容，这是一种基于 PCI 概念的新总线技术。我们将在下一章讨论 PCI 时，详细讲解 *CardBus* 和 *ExpressCard*。

PC 卡有增加厚度的三种规格：*Type I*（3.3 毫米）、*Type II*（5 毫米）和 *Type III*（10.5 毫米）。

图 9.1 显示了笔记本电脑上的 PCMCIA 总线连接，图 9.2 则展示了嵌入式设备上的 PCMCIA。您可能已经注意到，PCMCIA 主机控制器在 PCMCIA 卡与系统总线之间起桥接作用。笔记本电脑及其衍生产品通常有一个连接到 PCI 总线的 PCMCIA 主机控制器芯片，而一些嵌入式控制器则在其芯片内部集成了 PCMCIA 主机控制器。该控制器将卡的内存映射到主机 I/O 和内存窗口，并将卡产生的中断路由到合适的处理器中断线上。

![](img/07cc6f9c8c74622020874f66bfb53dc4_240_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_241_0.png)

图 9.2. 嵌入式系统上的 PCMCIA。

![](img/07cc6f9c8c74622020874f66bfb53dc4_241_1.png)

### Linux-PCMCIA 子系统

Linux-PCMCIA 支持在基于 Intel 的笔记本电脑以及 ARM、MIPS 和 PowerPC 等架构上均可用。PCMCIA 子系统包括 PCMCIA 主机控制器的设备驱动程序、不同卡片的客户端驱动程序、一个辅助热插拔的守护进程、用户态工具，以及一个与所有这些组件交互的*Card Services*（卡片服务）模块。

图 9.3 展示了构成 Linux-PCMCIA 子系统的各个模块之间的交互。

![](img/07cc6f9c8c74622020874f66bfb53dc4_242_0.png)

### 旧的 Linux-PCMCIA 子系统

Linux-PCMCIA 子系统最近经历了一次大规模重构。若要使 PCMCIA 在 2.6.13 及更新的内核上工作，您需要 *pcmciautils* 包（[http://kernel.org/pub/linux/utils/kernel/pcmcia/howto.html](http://kernel.org/pub/linux/utils/kernel/pcmcia/howto.html)），它取代了早期内核使用的 *pcmcia-cs* 包（[http://pcmcia-cs.sourceforge.net](http://pcmcia-cs.sourceforge.net)）。内核内部编程接口和数据结构也发生了变化。早期内核依赖名为 *cardmgr* 的用户空间守护进程来支持热插拔，但新的 PCMCIA 实现使用 *udev* 来处理热插拔，就像其他总线子系统一样。因此，在新的配置中，您不需要 *cardmgr*，并且应确保其未被启动。迁移指南位于 [http://kernel.org/pub/linux/utils/kernel/pcmcia/cardmgr-to-pcmciautils.html](http://kernel.org/pub/linux/utils/kernel/pcmcia/cardmgr-to-pcmciautils.html)。

图 9.3 包含以下组件：

- 实现与 PCMCIA 主机控制器通信的低层例程的主机控制器设备驱动程序。您的手持设备和笔记本电脑具有不同的主机控制器，因此使用不同的主机控制器驱动程序。主机控制器支持的每个 PCMCIA 插槽都称为一个*插座*（socket）。
- PCMCIA 客户端驱动程序（**图 9.3** 中的 *XX_cs*），它们响应如卡片插入和弹出等插座事件。这是您在尝试为 PCMCIA 卡片启用 Linux 支持时最可能需要实现的驱动程序。*XX_cs* 驱动程序通常与非 PCMCIA 特定的通用驱动程序（**图 9.3** 中的 *XX*）协同工作。就 **图 9.3** 而言，如果您的设备是 PCMCIA IDE 磁盘，那么 *XX* 是 IDE 磁盘驱动程序，*XX_cs* 是 *ide_cs* 驱动程序，*XX* 的依赖层是文件系统层，*XX* 的应用程序是访问数据文件的程序。*XX_cs* 配置通用驱动程序（*XX*），使用诸如 IRQ、I/O 基地址和内存窗口等资源。
- 为主机控制器驱动程序和客户端驱动程序提供服务的 PCMCIA 核心。核心提供了一个基础设施，简化驱动程序实现，并增加了一层间接性，使客户端驱动程序独立于主机控制器。无论您是在基于 XScale 的手持设备上使用蓝牙 CF 卡，还是在基于 x86 的笔记本电脑上使用，都可以使用相同的客户端驱动程序。
- 一个*驱动程序服务*模块（*ds*），为客户端驱动程序提供注册接口和总线服务。
- *pcmciautils* 包，包含 *pccardctl* 等工具，用于控制 PCMCIA 插座的状态并在不同的卡片配置方案之间进行选择。

图 9.4 将内核模块叠加在图 9.1 之上，说明了 Linux-PCMCIA 子系统如何在 PC 兼容系统与硬件交互。

**图 9.4. PCMCIA 驱动程序组件与 PC 硬件的关系。**

![](img/07cc6f9c8c74622020874f66bfb53dc4_243_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_244_0.png)

在接下来的部分中，让我们更仔细地查看构成 Linux-PCMCIA 子系统的组件。为了更好地理解这些组件的作用及其交互，我们将把一张 PCMCIA WiFi 卡插入笔记本电脑，并在“整合各个部件”一节中跟踪代码流程。

### 主机控制器驱动程序

虽然通用卡片驱动程序（XX）负责处理由卡片功能（例如，当 PCMCIA 网卡接收数据分组时产生的接收中断）生成的中断，但主机控制器驱动程序负责处理由卡片插入和弹出等事件触发的总线特定中断。

图 9.2 显示了一个围绕具有内置 PCMCIA 支持的嵌入式控制器设计的嵌入式设备的框图。即使您使用的是内核 PCMCIA 层支持的控制器，您也可能需要根据电路板的设计来微调主机控制器驱动程序（例如，配置用于检测卡片插入事件或切换插座电源的 GPIO 线）。例如，如果您正在将内核移植到基于 StrongARM 的手持设备，请修改 `drivers/pcmcia/sa1100_assab6.c` 以适合您的硬件。

本章不涵盖主机控制器设备驱动程序的实现。

