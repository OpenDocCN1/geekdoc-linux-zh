

## 安装 z/VM 并创建
Linux 或 z/OS 客户机

本章介绍执行 z/VM 安装所需概念和步骤。然后本章讨论在 z/VM 下创建 Linux 和 z/OS 测试，从您使用 HMC 创建 LPAR 完成的那一刻起，到客户机系统运行起来的那一点为止。

有关使用 HMC 为您的 LPAR 包装资源的信息，请参阅 *Hardware Management Console V7 Handbook*，SG24-7491 和 *IBM System Storage DS8000 Series: Architecture and Implementation*，SG24-6786。

**目标**

完成本章后，您应该能够：

- 在您的 LPAR 上安装 z/VM 操作系统
- 理解 z/OS 与 z/VM 之间的安装差异
- 在 z/VM 上为 Linux 虚拟机设置环境
- 在 z/VM 虚拟机中安装 Linux
- 创建并运行客户机 z/OS 系统

## 4.1 与 z/OS 相比的 z/VM 初始安装

本节面向 z/OS 系统程序员，他们对 z/VM 经验很少或没有。本节应帮助您了解安装 z/VM 系统的基础知识。

现有的 z/OS 和 z/VM 站点通常从现有运行系统执行其安装或升级任务。

z/VM 站点通常使用现有的虚拟机从 z/VM DDR（磁带交付）或 DVD 交付安装新的 z/VM 系统。截至 2008 年 1 月，z/VM 基础操作系统和基础选项可通过 ShopzSeries 在线订购进行互联网交付，在提供服务的国家/地区。有关更多信息，请参阅以下 Web 地址：

```
http://www.vm.ibm.com/buy/edelivery/
```

z/OS 站点使用现有的 z/OS 映像进行安装，使用 IBM 提供的安装方法之一，目前为 ServerPac、CBPDO 或 SystemPac®。

IBM 仅提供一种交付类型来安装 z/VM，尽管媒体类型（DVD 或磁带）有选项。

如前所述，IBM 为 z/OS 提供的可用安装方法目前为 ServerPac、CBPDO 或 SystemPac。本节描述每一种。

名为 ServerPac 的 z/OS 安装方法是一种“软件交付包，由 IBM 已执行 SMP/E 安装步骤和部分 SMP/E 后安装步骤的产品和服务组成”（根据 z/OS V1R9.0 Planning for Installation，GA22-7504-17）。该包是一组通过初始测试的集成产品。此方法涉及使用 CustomPac Installation Dialog 的使用，允许客户自定义诸如命名数据集和卷、以及在安装期间构建的磁盘集中放置数据集等方面。客户可以选择

要么安装一个可 IPL 的 z/OS 映像（包括必要的辅助数据集、页、SMF 等），要么仅安装产品并在稍后建立这些辅助设施。

### CBPDO

Custom-Built Product Delivery Option（CBPDO）交付由未安装且未集成的服务组成，没有对话框或工具来协助安装过程。客户必须使用 SMP/E 执行此操作。

### SystemPac

最后一种替代方案 SystemPac 是集成产品（甚至 ISV 产品）的完整交付，完全按照客户的规格。它包含一个可 IPL 的系统，包括所有必要的辅助数据集。它有两种格式可用：全卷和按数据集转储。这种类型的交付可能是新 z/OS 客户的唯一选择。

### 其他交付

请咨询您的 IBM 服务代表了解其他交付类型或包。某些类型或包具有更定制化的性质，可能无法在每个地区或国家/地区订购。

### 4.1.4 将 z/VM 安装与 z/OS 安装类型进行比较

相比之下，SystemPac 全卷格式类型的交付与客户首次安装操作系统时的 z/VM 交付类似。

SystemPac 交付和 z/VM DDR（磁带）交付（假设首次安装）都意味着使用独立（从磁带初始程序加载）版本的 IBM Device Support Facility（ICKDSF）来格式化磁盘卷，以及 DFSMSDSS 用于 z/OS 或 DDR 用于 z/VM 来恢复卷。这些活动是从硬件管理控制台（HMC）执行的。相比之下，对于已经熟悉 z/OS 的人来说，从 DVD 交付安装 z/VM 似乎是最简单的方法。

通过使用 z/VM DVD 交付，您有能力启动一个 RAMDISK 操作系统，加载到 System z 处理器内存中。该系统在功能上等同于 z/VM 本身，并且是从 HMC 使用 Integrated 3270 Console 设施调用的。从该操作系统内部，您执行大部分剩余的安装活动：

1. 调用可执行文件 INSTPLAN 来指定要安装哪些产品，使用哪种语言以及目标 DASD 的类型和卷序列号（volsers）。

