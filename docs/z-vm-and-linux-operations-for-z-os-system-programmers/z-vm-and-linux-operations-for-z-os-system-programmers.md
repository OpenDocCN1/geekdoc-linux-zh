# Z OS 系统程序员的 Z VM 和 Linux 操作

## 前言

本IBM® Redbooks®出版物从z/OS®程序员或系统程序员的角度讨论z/VM®和Linux®操作。虽然已有其他书籍涵盖了许多这些主题，但本书针对每个主题提供了足够的信息，向对这两种环境都陌生的读者介绍IBM System z®上的z/VM和Linux操作。

本书面向正转向System z环境下的z/VM和Linux的z/OS程序员和系统程序员，他们希望获得一份对照指南作为帮助。

本书基于我们在System z上使用System z10™企业版、z/VM 5.3版 RSU 0701和Novell® SUSE® Linux Enterprise Server (SLES) 10的经验。

## 本书编写团队

本书由来自世界各地的专家团队在国际技术支持组织波基普西中心编写而成。

Lydia Parziale是纽约波基普西市ITSO团队的项目负责人，在技术管理方面拥有国内和国际经验，包括软件开发、项目领导和战略规划。她的专业领域包括电子商务开发和数据库管理技术。Lydia是PMP和IBM认证IT专家，拥有技术管理MBA学位，已在IBM工作超过20年，涉足多个技术领域。

Omar Badreddin是IBM渥太华高级研究中心的研究员，也是软件工程复杂性降低研究小组(CRuiSE)的成员。Omar拥有五年IBM软件工程师的工作经验，并曾举办多次ITSO研讨会。他的专业领域包括虚拟化、建模、BPM、SOA和软件全球化。

Roy P Costa是IBM国际技术支持组织波基普西中心的咨询系统程序员。他在z/VM系统操作和编程方面拥有超过25年的经验。Roy与System z上的Linux打交道已有五年多，并撰写了多本Redbooks。

特别感谢IBM Redbooks出版物《*大型机入门：z/VM基础*》（SG24-7316）的作者，该书于2007年11月出版：
Edi Lopes Alves, Eli M Dow, Klaus Egeler, Jason Herne, Clive Jordan, Eravimangalath P Naveen, Manoj S Pattabiraman, 和 Kyle Smith

## 成为一名出版作者

加入我们为期两到六周的驻场项目吧！帮助撰写一本关于特定产品或解决方案的书，同时获得前沿技术的实践经验。你将有机会与IBM技术专家、业务合作伙伴和客户合作。

你的努力将有助于提高产品接受度和客户满意度。此外，你还将结识IBM开发实验室的相关人员，提高你的工作效率和市场价值。

了解更多关于驻场项目的信息，浏览驻场项目索引，并在以下网址在线申请：
ibm.com/redbooks/residencies.html

## 欢迎评论

您的评论对我们非常重要！

我们希望我们的书籍尽可能对您有帮助。请通过以下任一方式将您关于本书或其他IBM Redbooks的评论发送给我们：

- 使用在线**联系我们**的Redbooks评论表单，网址为：
ibm.com/redbooks

- 将您的评论通过电子邮件发送至：
redbooks@us.ibm.com

- 将您的评论邮寄至：
IBM Corporation, International Technical Support Organization
Dept. HYTD Mail Station P099
2455 South Road
Poughkeepsie, NY 12601-5400

## 为什么选择System z上的z/VM和Linux？

在本章中，我们探讨在System z上使用z/VM和Linux的好处，以及如何利用这些好处。

## 目标

完成本章后，您应该能够：

- 列出z/VM能为您的IT部门提供的好处
- 理解为什么公司要对System z上的z/VM和Linux进行投资

![](img/b0a4b9056f819dccd4781a5105c92d45_16_0.png)





## 1.1 为什么选择 z/VM？

z/VM 通过虚拟化优化利用率，为企业充分发挥其 IT 资源的能力提供了可能。凭借超过 40 年的经验，z/VM 已成为虚拟化领域的领导者。本节讨论了利用 z/VM 经验来支持您的 IT 基础设施的好处。

### 1.1.1 z/VM 的虚拟机功能

z/VM 为计算机操作系统提供了一种独特的方法。它为每个用户提供一个独立的工作环境，称为虚拟机（VM）。虚拟机使用虚拟化技术通过共享真实机器的资源来模拟真实机器的存在，这些资源包括处理器、存储、内存和输入/输出（I/O）资源。

操作系统和应用程序可以在虚拟机中作为客户机运行。例如，您可以在同一台 z/VM 系统上运行多个 Linux 和 z/OS 映像，该系统同时也在支持各种应用程序和用户。因此，开发、测试和生产环境可以共享一台物理计算机。

z/VM 的虚拟机功能使您能够执行以下任务：

- 测试可能导致真实机器操作异常终止的程序，而不会影响同时运行的生产工作处理。
- 测试操作系统的新的发行版。

为虚拟机提供的隔离使系统导向程序和远程处理应用程序，例如，可以在虚拟机上进行测试，同时生产工作正在进行；这种测试不会导致真实机器异常终止。

可以在现有发行版执行生产工作的同时生成和测试操作系统的新的发行版。这使得新的发行版能够更快地安装并投入生产。在 z/VM 下能够同时运行多个操作系统，可以使安装能够继续运行仅在旧版本下运行的程序（例如仅限于特定发行版且不经济转换的程序），同时运行最新发行版。

- 测试新的操作系统。
现有操作系统可以与生成和测试新的操作系统并发地处理生产工作。在投入生产使用之前，可以获得对新系统的经验，而无需将真实机器专用于此功能。
- 与生产工作并发地执行操作系统维护。
可以在正常生产操作进行的同时安装和测试操作系统的程序临时修复（PTF）。
- 为主要操作系统提供备份设施。
生成的 z/VM 系统不依赖于型号，如果满足最低硬件要求，可以在各种服务器型号上运行。这使得具有较少实际存储、较少通道、较少直接访问设备和较少单元记录设备的小型服务器型号能够为大型型号提供备份（通常性能较低）。
- 与生产工作处理并发地进行操作员培训。
真实机器无需专用于培训额外或新的操作员，或在安装新的操作系统时提供初始培训。操作员错误不会导致真实机器操作终止。
- 在安装额外的通道和 I/O 设备之前模拟新的系统配置。
可以通过使用模拟的 I/O 配置而不是真实的 I/O 配置来确定通道和 I/O 设备的相对负载。使用一台真实机器即可获得生成和操作多个客户机的 I/O 配置的经验。
- 测试客户编写的系统出口。
可以在不干扰生产工作的情况下测试客户编写的系统出口。
- 为客户操作系统提供相同的硬件配置
相同硬件的一致性意味着在任何地方使用相同的驱动程序，因此无需测试许多不同的驱动程序。这减少了对不同客户系统的测试和配置量。





### 1.1.2 z/VM 提供经过验证的系统完整性、安全性和可靠性

z/VM 建立在系统完整性和安全性基础上，并融合了许多用于可靠性和可用性的设计特性：

- 完整性和安全性：
  - z/VM 支持来宾使用受支持的 IBM 服务器提供的加密功能。
  - IBM 将纠正由未经授权的程序引入系统的任何完整性漏洞。
  - 通过 z/VM 的 TCP/IP 提供 Kerberos 身份验证和安全套接层（SSL）支持。
  - 集成访问控制和身份验证服务可通过添加 RACF® for z/VM 功能或其他外部安全管理器来增强。
- 可用性和可靠性：
  - 在应用程序恢复方面，z/VM 提供服务以允许恢复与资源管理器不完整的交互。
  - 在自动化操作方面，z/VM 提供多个级别的自动化系统管理支持。一个例子是可编程操作员。对于更高程度的自动化，可以添加 IBM SystemView® Host Management Facilities/VM。 可编程操作员和 Host Management Facilities/VM 都可以与 z/VM 上的 IBM NetView® 交互，而 NetView 又可以与 z/OS 上的 NetView 交互。
  - z/VM 提供双工数据，并在主副本和备份副本之间进行透明的持续同步，并在主副本出现错误时自动透明切换到备份副本。
  - 在线配置更改消除了许多以前需要停机的情况。
  - z/VM 系统可以连接以提高服务器和用户可用性。
  - 从故障中快速重启可减少对用户的影响。

## 1.2 为什么选择 Linux？

System z 上的 Linux 旨在帮助简化您的 IT 基础设施：减少服务器蔓延；控制软件许可费用；并最大限度地减少在管理和维护服务器时对人工干预的需求。

#### 开源

IBM 出于以下几个原因致力于开源作为许可和开发模式：

- IBM 客户和合作伙伴要求为所有 IBM 平台、产品和解决方案提供开源软件（包括 Linux）支持。
- 开源软件由于其广泛的传播和使用，通常会成为行业标准。
- 开源社区内的创新通常以高于封闭源社区的速度和数量发生。

#### Linux 技术中心（LTC）

IBM 是开源社区的主要贡献者，全球有超过 250 名开发人员全职从事许多计划。其中一项计划是 Linux 技术中心（LTC），它通过开发和贡献技术、实用程序、工具和代码来启用 Linux 的企业能力。

要了解有关 LTC 的更多信息，请访问：

http://oss.software.ibm.com/linux

## 1.3 为什么 Linux 和 z/OS 与 z/VM 一起使用？

本节介绍将 z/VM 与 System z 上的 Linux 和 z/OS 结合使用。因为 z/VM 提供高度灵活的测试和生产环境，所以它是部署完全功能的操作系统（如 Linux）到 System z 或 z/OS 的简便方法。这允许通过服务器整合实现服务器简化。

### 1.3.1 服务器简化

随着公司的增长，其 IT 基础设施也在增长。这导致大多数公司增加了独立服务器、存储设备和应用程序的数量。增加可能导致巨大的效率问题和系统管理难题。

增长及其结果促使公司采用虚拟化进行服务器简化。简单来说，*虚拟化* 提供了一种方法，可帮助将大量独立的小型机器整合到一台更大的服务器上，从而简化管理并更有效地使用系统资源。然后可以对资源进行优先级排序并分配给在任何给定时间最需要的 workload。结果，您可以减少为单个 workload 峰值过度配置的需求。有关更多信息，请参阅：
http://www-03.ibm.com/systems/z/advantages/virtualization/index.html

#### System z 之外的服务器简化

由于能够在 System z 上运行 Linux，信息技术部门能够通过将多个服务器场整合到一台运行 z/VM 和 System z 上 Linux 的 System z 上来简化其流程。这带来硬件节省和电力节省，并简化了基础设施的管理，释放各种 IT 资源，以便您可以专注于关键任务。

使用虚拟化，启动 Linux 系统所需的时间仅为几分钟，而不是等待新硬件和安装过程完成数天。因为每个 Linux 映像都在其自己的虚拟系统中运行，所以 Linux 映像不会影响周围的其他系统。

#### System z 内部的服务器简化

服务器简化并不总是必须发生在 System z 之外。有时最好的地方是直接在大型机内部，这意味着将其他操作系统（如 z/OS）从其他逻辑分区（LPAR）上移出并移动到运行 z/VM 的单个 LPAR 上。几个好处是可以：

- 释放 LPAR 以用于更关键的环境
- 快速启动和关闭测试和开发环境
- 有助于降低升级成本，因为您可以释放 LPAR 而无需购买另一台 System z

z/VM 使您能够拥有一个备用系统来尝试想法或隔离任务。因为 z/VM 能够在虚拟机中提供几乎无限的备用系统，所以它允许您的 IT 部门有效地使用其 System z 的全部功能。让一个系统看起来像许多系统的优势在于，您可以创建生产系统的精确副本来测试新程序、服务和流程。这是一种相对廉价的方式来拥有自己的测试系统（或您想要的任意多个测试系统）。这也是测试新功能的安全方式，因为您的真实生产系统及其应用程序和数据会受到保护，不会受到如果在主机系统上测试新功能可能造成的任何损害。





### 1.3.2 作为 z/VM 客户机运行 Linux 的十大理由

将 Linux 操作系统作为 z/VM 的客户机运行是一个明智的选择。请考虑以下 z/VM 为 Linux 客户机环境提供的优势¹：

- **共享资源**
  在同一 z/VM 系统上运行的多个 Linux 映像之间可以共享资源。这些资源包括处理器周期、内存、存储设备和网络适配器。
- **服务器硬件整合**
  在单个 System z 服务器上运行数十或数百个 Linux 实例可为客户节省空间以及管理实际硬件所需的人员。
- **虚拟化**
  虚拟机环境具有高度灵活性和适应性。新的 Linux 客户机可以快速轻松地添加到 z/VM 系统中，而无需专用资源。这对于复制服务器非常有用，同时也为用户提供了一个高度灵活的测试环境。有关更多优势，请参阅第 10 页的 2.1.1 节“虚拟化的优势”。
- **System z 优势**
  在 z/VM 上运行 Linux 意味着 Linux 客户机或客户机可以透明地利用 z/VM 对 System z 硬件架构和 RAS 功能的支持。

  z/VM 支持集成 Linux 设施（IFL）处理器，这对于在 System z 上运行的 Linux 工作负载来说可能是一种价格极具吸引力的硬件功能。
- **z/VM 连接性**
  使用客户机局域网和虚拟交换机（VSWITCH），z/VM 可在同一处理器上运行 Linux 和其他操作系统的虚拟机之间提供高性能通信。实现高速 TCP/IP 连接的底层技术是虚拟通道到通道（CTC）适配器支持和 VM IUCV（用户间通信载体）。使用 HiperSockets™ 简化网络可以节省成本并减少布线、集线器、交换机和路由器。它还可以帮助减少维护工作。
- **Minidisk 驱动程序**
  Linux on System z 包含一个 minidisk 设备驱动程序，可访问 z/VM 支持的所有 DASD 类型。
- **内存中数据**
  VM 利用 z/Architecture® 提供的内存中数据性能提升。
- **调试**
  VM 提供了一个丰富的调试环境，对于诊断 Linux 内核和设备驱动程序中的问题特别有价值。
- **控制和自动化**
  z/VM 对调度、自动化、性能监控和报告以及虚拟机管理的长期支持可用于 Linux 虚拟机。
- **水平扩展**
  扩展 Linux 工作负载容量的有效方法是向 z/VM 系统添加更多 Linux 客户机。

## 向 z/OS 系统程序员介绍 z/VM

本章首先简要讨论虚拟化的基础知识。然后概述 z/VM 的概念和功能。本章还提供了有关每个主题的更多详细信息的参考列表。

当您成为 z/VM 系统程序员或系统管理员时，您必须了解虚拟化的概念以及 z/VM 如何实现虚拟化。

## 目标

完成本章后，您应该能够：

- 了解虚拟化的基本概念以及 z/VM 如何利用它
- 描述 z/VM 的两个组件：控制程序（CP）和对话监视系统（CMS）
- 使用 z/VM 的基本导航技能和命令

### 2.1 虚拟化概述

虚拟化是指计算机系统能够共享物理资源，例如内存、存储、网络适配器和处理器，从而表现得好像是许多不同的系统一样。

今天，最常见的虚拟化领域是服务器、网络和存储。虚拟化还可以应用于非物理资源，例如应用程序、中间件，甚至虚拟资源本身，例如虚拟化一群虚拟服务器。

#### 2.1.1 虚拟化的优势

管理 IT 系统的成本增长速度快于这些系统的新硬件成本，因为这些系统的复杂性需要越来越多的人来管理它们。管理层的主要关注点是在提高收入水平的同时控制成本。

实施虚拟化可以成为管理计算基础设施的关键第一步，通过以下方式实现：

- 降低现有基础设施的成本
- 降低向该基础设施添加资源的复杂性
- 在多个数据中心构建异构基础设施，使这些中心更能响应业务需求

虚拟化的优势因目标和所选特定虚拟化技术以及现有 IT 基础设施而异。即使在简单服务器整合中使用虚拟化，用户在某种程度上也能实现以下许多优势。

#### 更高的资源利用率

虚拟化能够动态共享物理资源和资源池，从而实现更高的资源使用率，尤其是在可变工作负载的情况下，其平均需求低于整个专用资源。

#### 更低的管理成本

虚拟化可以通过以下方式提高员工生产力：减少必须管理的物理资源数量；隐藏部分资源复杂性；通过自动化、更好的信息和集中化简化常见管理任务；并实现工作负载管理自动化。
虚拟化还使通用工具能够在多个平台上使用。




#### 2.1.2 虚拟化的工作原理

虚拟化使得对多个（通常是异构的）系统进行直接开箱即用的基础系统管理成为可能。

如图 2-1 所示，分区和虚拟化涉及一种从物理到逻辑的思维转变，将 IT 资源视为逻辑池而不是独立的物理实体。这涉及到整合和池化 IT 资源，并为同构和异构的服务器、存储、分布式系统和网络提供单一系统映像。

![](img/b0a4b9056f819dccd4781a5105c92d45_27_0.png)

硬件分区涉及为不同的操作系统分配独立的处理器，每个操作系统运行其特定的应用程序。软件分区则采用基于软件的虚拟机监控程序（hypervisor），使各个操作系统能够在任意或所有处理器上运行。

> ¹ z/VM 不将 Windows® 作为客户操作系统运行，因为 Windows 不是大型机操作系统。图 2-1 显示了在 z/VM 或 VMware 上运行的操作系统；它没有显示同时在两者上运行的操作系统。

虚拟机监控程序是允许在宿主计算机上同时运行多个操作系统的虚拟化平台。虚拟机监控程序技术起源于 System/360 Model 67，后来演变成 IBM VM/370，即 z/VM 的前身。创建逻辑分区（LPAR）涉及对固件（基于硬件的虚拟机监控程序）进行分区，以将操作系统与处理器隔离。

#### 2.1.3 大型机上的虚拟化

通常，IBM 大型机可以通过以下三种方式进行分区：

-   基本模式：此模式也称为本机模式，将整个物理系统用作单一系统。此模式可以在系统激活期间选择，是最少使用的操作模式。在基本模式下，不支持逻辑分区（LPAR）。

    > 注意：在 z9® 和 z10 大型机上，不再支持基本模式，因此您必须至少定义一个 LPAR。

-   LPAR 模式：在这种逻辑分区模式（LPAR 模式）下，单个大型机系统被逻辑地划分为多个分区。LPAR 模式可以在系统激活期间选择，是大型机上最常用的模式。根据机器不同，LPAR 模式可以提供基本模式下不可用的附加功能，并且这些功能可以在操作系统的支持下加以利用。

-   z/VM 客户机：IBM z/VM 客户机实现是软件级分区。z/VM 操作系统运行在 LPAR 上，或者（在较旧的硬件上）运行在完整的大型机（基本模式）上。然后，在 z/VM 系统之上创建虚拟机（VM），以承载其他客户机系统。

### 2.2 z/VM 概述

习惯一个新的操作系统（OS）通常意味着要了解在另一个 OS 中你所熟悉的操作有哪些不同的执行方式。然而，有时某个 OS 与其他任何 OS 都截然不同，因此在真正开始探索其功能和特性之前，先了解一下新 OS 的一些基本概念是值得的。

乍一看，z/VM 可能与其他操作系统有很大不同。但是，在了解了基本概念之后，驾驭并利用此 OS 的功能就变得容易了。z/VM 的强大之处在于它能够为企业提供高度灵活的测试和生产环境，以部署其按需业务解决方案。z/VM 利用 IBM z/Architecture，并凭借对多种操作平台（例如 Linux on System z、z/OS、z/OS.e、VSE/ESA™、z/VSE™ 等）的广泛支持，帮助企业满足对多用户服务器解决方案日益增长的需求。

有关更多信息，请参阅以下网站：

http://www.vm.ibm.com/index.html

在本节中，我们将解释什么是 z/VM，以及 Version 5 Release 3 中可用的功能和组件。在您开始接触 z/VM 的过程中，这些入门主题将对您阅读本书大有裨益。有关更详细的介绍，请参阅 IBM Redbooks 出版物《*新大型机入门：z/VM 基础*》，SG24-7316。

#### 2.2.1 z/VM 的历史

在 20 世纪 60 年代初，一小部分大学科学家致力于研究分时计算机系统的构想。所创建的系统运行在当时 IBM 的处理器上，提供了分时功能，但使用环境更偏向批处理。

虚拟机的想法始于 20 世纪 60 年代中期，当时的工作是开发一种控制程序（CP），该程序可以将真实的磁盘分区为迷你盘（minidisk），并处理每个虚拟机的单元记录输入/输出（I/O）设备。在此期间，会话监控系统（CMS）作为用于文件和程序操作的监控系统而被开发。这两个系统并没有整合在一起，而是各自拆分为独立的组件。CP 在机器层面为每个用户提供独立的计算环境。CMS 则提供不需要担心资源分配或共享的单用户服务。

由于虚拟机控制程序需要模拟当时的计算机系统，每个虚拟机都需要具备计算机的所有组件。每个虚拟机都必须拥有唯一的计算机标识、安全的位置、输入和输出设备，以及内存和存储。排队工作（到 I/O 设备）是通过将输入或输出假脱机到设备来完成的。输入在卡片打孔机上准备；卡片上被打上孔。卡片被送入读卡器，读卡器感知打孔的位置，并以电子方式将信息存储在计算机的内存中。计算完成后，输出会被发送到输出设备，例如击打式打印机或基本控制台。

时至今日，我们仍能在 z/VM 系统中看到这些设备留下的印迹。





由于每台虚拟机都有自己的设备并且每个设备都必须具有可寻址性，因此对每台机器分配相同的默认设备地址和设备类型，如下所示：

- 地址 0009 为 3215 控制台
- 地址 000C 为 2540 读卡机
- 地址 000D 为 2540 冲孔机
- 地址 000E 为 1403 打印机

除了 I/O 设备外，每台机器都必须有中央处理器和内存来运行程序，以及存储来保存数据。处理器（虚拟 CPU）、内存（虚拟存储）和磁盘（迷你磁盘）构成了每台虚拟机所需的组件。

当我们登录到 z/VM 用户 ID（我们唯一的机器标识符）并输入我们的密码（我们的安全位置）时，我们实际上是在启动计算机系统的过程。我们首先与 CP 建立联系，在那里我们获得运行系统所需的硬件。接下来，当我们启动我们的系统，例如 CMS、Linux、z/OS 或另一个 z/VM 系统时，我们会对已存在于磁盘上的系统进行初始程序加载（IPL）。我们可能会将输入分发到我们的冲孔机、读卡机，或将输出分发到我们的打印机或控制台。

多年来，IBM 承担了这项开发工作。随着 IBM 宣布更新的处理器，如 system/360 和 system/370，VM 的工作继续进行，但并未被视为客户会广泛使用的系统。作为基础 system/370 操作系统，MVS™ 继续其开发工作。由于可用的处理器原型很少，人们意识到 VM 为 MVS 开发人员提供了必要的处理器仿真平台。VM 成为许多客户中受欢迎的系统，他们发现该系统的编程简便性和多功能性对他们的业务有益。

到 1980 年代，VM 安装数量增长，更多业务流程和应用程序被开发用于在 VM 上运行。客户的欢迎带来了 VM 的增强编程产品，如 REXX™ 和 Pipelines，此后已被移植到其他操作系统。随着新 IBM 处理器和架构的开发，VM 保持同步，提供了新的功能来利用这些特性。

随着其他技术和系统的出现，z/VM 变得不再是前端直接用户界面，而更多的是 IBM 虚拟化技术平台。现在，随着 Linux 的流行以及对 z/VM 虚拟化能力的认可，它再次证明了其在 System z 操作系统产品组合中的地位。

与早期计算机一样，z/VM 已从其早期根源发展而来，现在提供了更多功能和服务，尽管虚拟机的基本原理并没有发生显著变化。

图 2-2 显示了 z/VM 如何演变到今天的版本的 timeline。

![](img/b0a4b9056f819dccd4781a5105c92d45_31_0.png)

图 2-2 z/VM 历史

#### 2.2.2 关于 z/VM

z/VM 为每个用户提供一个单独的工作环境，称为虚拟机。虚拟机模拟专用真实机器的存在，包括处理器功能、内存、网络和输入/输出（I/O）资源。操作系统和应用程序可以在第二层作为 guest 在虚拟机上运行。例如，您可以在同一 z/VM 系统上运行多个 Linux 和 z/OS 映像，每个映像都在自己的虚拟机上。

因此，开发、测试和生产环境可以并排运行，共享相同的资源。

虚拟机可以使用自己的真实硬件资源（例如，磁带驱动器）；然而，在大多数情况下，它从 z/VM 管理的虚拟硬件池中共享。这些设备的虚拟地址可能与实际设备的真实地址相同也可能不同。因此，虚拟机只知道在现实世界中存在或不存在的虚拟硬件。

#### 2.2.3 第一级与第二级 guest 系统

第一级 z/VM 意味着它是直接安装在真实硬件之上的基础操作系统。第二级系统是在 z/VM 中启动的用户，其中操作系统可以在第一级 z/VM 上执行。

换句话说，第一级 z/VM 操作系统直接位于硬件之上，但该第一级 z/VM 系统的 guest 是虚拟化的；参见第 18 页的图 2-3。通过从第一级虚拟化硬件，我们能够使用少量实际真实硬件创建并使用尽可能多的 guest。

在这些虚拟机中运行的操作系统通常称为 guest。您可能会遇到的其他短语包括：

- 运行第一级，这意味着直接在硬件上运行（这就是基础 z/VM 所做的）。
- 运行第二级、在 z/VM 下运行，或运行在（z/VM 之上），这意味着作为第二级 guest 运行。





#### 图 2-3 LPAR 配置示例

![](img/b0a4b9056f819dccd4781a5105c92d45_33_0.png)

用户目录（USER DIRECT）是一个文件，其中包含有关系统中所有来宾的所有信息。它通常由磁盘 2CC 上的 MAINT 用户拥有。

> z/OS 类比：用户目录可以看作是安全系统中所有用户定义的等价物，或 SYS1.UADS 数据集的内容。

创建用户定义时，我们必须指定 CP 特权类、用户可以访问的最小和最大虚拟内存，以及 VM 将运行的模式（例如 ESA/XA）以及它需要的 I/O 设备。

第 19 页的示例 2-1 显示了用户目录中名为 IBMUSER1 的用户的条目。

#### 示例 2-1 用户 IBMUSER1 的 USER DIRECT 条目

```
USER IBMUSER1 USER1PW 32M 128M G
INCLUDE IBMDFLT
MACH XA
IPL CMS
MDISK 191 3390 1823 010 LX6RES MR
```

示例 2-1 中 USER DIRECT 中 z/VM 来宾定义的条目具有以下含义：

- 1. USER 行设置此虚拟机的用户 ID，即 IBMUSER1。密码为 USER1PW。此机器被定义为在登录时具有 32 MB 的默认内存存储。该用户可以通过使用 DEFINE STORAGE 命令将内存分配增加到最多 128 MB。最后一个值表示用户 ID 的 CP 类别（在我们的示例中，G 代表普通用户权限）。
- 2. 包含默认配置文件以显示常见用户属性，如第 20 页的示例 2-2 所示。
- 3. 以扩展架构（XA）模式运行此虚拟机。
- 4. 在登录时（初始程序加载），自动初始化对话监视系统（CMS）。
- 5. 为用户建立一个迷你磁盘。在我们的示例中，这建立了在 DASD 卷 LX6RES 上从柱面 1823 开始的 10 个柱面的 3390 DASD 卷上的虚拟地址 191 的迷你磁盘，并具有多写访问权限。

> 注意：DEFINE STORAGE 命令会中断；它可以重置来宾操作系统。

如果某些目录控制语句对多个用户重复，则可以使用目录配置文件来节省目录中的空间。因为您可以在单个 z/VM 映像上潜在地创建数百个 Linux z/VM 用户 ID，所以您可以创建一个配置文件来定义许多用户 ID 共有的内容。我们在 TCPIP 用户 ID 中包含的配置文件显示在第 20 页的示例 2-2 中。

#### 示例 2-2 包含配置文件 IBMDFLT

```
PROFILE IBMDFLT
SPOOL 000C 2540 READER *
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
LINK MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
LINK MAINT 019E 019E RR
LINK MAINT 0402 0402 RR
LINK MAINT 0401 0401 RR
LINK MAINT 0405 0405 RR
```

示例 2-2 中显示的以下语句位于 IBMDFLT 配置文件中：

- 1. SPOOL 语句定义用户的虚拟 spool 设备。您选择的选项会修改与虚拟读卡机、打印机、穿孔机或控制台相关的操作功能。
- 2. 提供对驻留在其他用户磁盘上的文件的访问权限，在本例中为包含 CMS、工具和帮助文件的 MAINT 磁盘。

### 2.3 z/VM 的组件

z/VM 由以下组件和设施（基础产品）组成：

- Control Program（CP）
- Conversational Monitor System（CMS）
- Transmission Control Protocol/Internet Protocol（TCP/IP）for z/VM
- Advanced Program-to-Program Communication/Virtual Machine（APPC/VM）
- Virtual Telecommunications Access Method（VTAM®）Support（AVS）
- Dump Viewing Facility
- Group Control System（GCS）
- Hardware Configuration Definition（HCD）and Hardware Configuration Manager（HCM）for z/VM
- Language Environment®
- Open Systems Adapter Support Facility（OSA/SF）
- Restructured Extended Executor/Virtual Machine（REXX/VM）
- Transparent Services Access Facility（TSAF）
- Virtual Machine Serviceability Enhancements Staged/Extended（VMSES/E）

除了基础产品外，z/VM 还提供以下可选产品：

- Data Facility Storage Management Subsystem for VM（DFSMS/VM™）
- Directory Maintenance Facility for z/VM（DirMaint™）
- Performance Toolkit for VM
- RACF Security Server for z/VM
- Remote Spooling Communications Subsystem（RSCS）Networking for z/VM

在以下各节中，我们讨论每个组件并提供指向参考资料的指针，您可以在其中了解有关每个主题的更多信息。

#### 2.3.1 Control Program

Control Program（CP）主要是一个真实机器资源管理器。CP 为每个用户提供一个称为虚拟机的独立工作环境。每个虚拟机都是真实系统的功能等价物，共享真实的处理器功能、存储、控制台和输入/输出（I/O）设备资源。

当您首次登录 z/VM 时，CP 控制工作环境。z/VM 的许多设施立即为您提供。例如，您可以使用 CP 命令执行各种系统管理任务。然而，在 z/VM 上完成的大多数工作需要对话监视系统（CMS）。从此环境中，可以加载（IPL）并在用户 ID 内运行来宾操作系统（如 z/OS）。

CP 提供连接性支持，允许应用程序程序相互交换信息并访问驻留在同一 z/VM 系统或不同 z/VM 系统上的资源。

CP 在第 33 页的第 2.4 节“Control Program（CP）”中进一步讨论。

z/OS 类比：CP 是 z/OS 内核或监督程序的等价物。

#### 2.3.2 Conversational Monitor System

Conversational Monitor System（CMS）是一个单用户操作系统（您与一个用户、一个键盘和一个监视器交互）。CMS 可以帮助您执行各种各样的任务。例如，您可以编写、测试和调试用于 CMS 或来宾系统基础产品上的应用程序，如以下任务所述：

- 运行在 CMS 或来宾系统上开发的应用程序
- 创建和编辑数据文件




- 以批处理方式处理作业
- 在 CMS 与客户机系统之间共享数据
- 与其他系统用户通信
- 提供用于存储数据的有用文件系统

#### CMS 文件系统

在 CMS 中，*文件*是数据的基本单位。CMS 中的文件是唯一的，不能使用其他操作系统进行读取或写入。在 CMS 中创建文件时，您需要使用文件标识符（file ID）为其命名。文件标识符由以下三个字段组成：

- 文件名（fn）：最多包含八个字母数字字符
- 文件类型（ft）：最多包含八个字母数字字符
- 文件模式（fm）：包含一个字母字符

> **z/OS 类比：** CMS 文件类似于 z/OS 上的顺序数据集或 UNIX® System Services 上的 z/OS 文件。

当您使用 CMS 命令和程序修改、更新或引用文件时，必须使用文件标识符字段来标识文件。各种 CMS 命令允许您仅输入文件名，或输入文件名和文件类型；其他命令还要求您输入文件模式。

在 z/VM 下，您的文件可以存储在共享文件系统（SFS）中，SFS 是一种采用层次目录结构的共享文件空间。根据您的系统配置，您可以选择使用 CMS 和 SFS 两种方法来存储文件。您可以将希望共享的文件存储在 SFS 文件空间中；其他文件可以存储在迷你磁盘上。

z/VM OpenExtensions（POSIX 支持）包含另一种类型的文件，称为字节文件系统（BFS）文件。BFS 文件像 UNIX 系统一样按层次结构组织。所有文件都是某个*目录*的成员。每个目录又依次是层次结构中更高级别另一个目录的成员。层次结构的最高级别是 BFS 文件空间。通常，用户会将全部或部分 BFS 文件空间挂载为根目录。

z/VM 将整个文件层次结构视为一个字节文件系统。每个字节文件系统都是可挂载的文件系统。*根*文件系统是第一个挂载的文件系统。后续文件系统可以挂载在根文件系统内的任何目录上，或挂载在任何已挂载文件系统内的目录上。

字节文件系统中的所有文件都称为 BFS 文件。BFS 文件是面向字节的，而不是面向记录的，如迷你磁盘或共享文件系统中的 CMS 记录文件。您可以将 BFS 文件复制为 CMS 记录文件，也可以将 CMS 记录文件复制到字节文件系统中。

有关 CMS 的进一步讨论，请参阅第 35 页的 2.5 节“会话监控系统（CMS）”。

#### 2.3.3 TCP/IP

z/VM 的 TCP/IP 将大型机服务器的功能和资源带到了 Internet。使用 z/VM 的 TCP/IP 协议套件，您可以从 z/VM 系统访问多个供应商的网络环境。

z/VM 的 TCP/IP 允许 z/VM 系统在 TCP/IP 开放网络中充当其他中央计算机的对等体。应用程序可以在 z/VM、Linux 和其他环境之间透明地共享。用户可以通过来自多家供应商的广泛系统发送消息、传输文件、共享打印机以及访问远程资源。

z/VM 的 TCP/IP 提供以下类型的功能和接口：

- 连接和网关功能，处理物理接口和数据路由
- 服务器功能，向客户端提供服务（即发送或传输文件）
- 客户端功能，向网络中任意位置的服务器请求特定服务
- 网络状态和管理功能，检测并解决网络问题
- 应用程序编程接口，允许您编写自己的客户端/服务器应用程序

z/OS 类比：z/VM 的 TCP/IP 具有与 z/OS 相同的功能。

#### 2.3.4 APPC/VM VTAM 支持（AVS）

APPC/VM VTAM 支持（AVS）是一个虚拟电信访问方法（VTAM）应用程序，在系统网络架构（SNA）网络中为 VM 和非 VM 系统之间提供高级程序到程序通信（APPC）服务。

AVS 和 VTAM 在 z/VM 系统上的同一个组控制系统（GCS）组中运行。AVS 和 VTAM 共同使 APPC/VM 应用程序在一个


TSAF 或通信服务（CS）集合用于与以下应用程序通信：

- 驻留在 SNA 网络中其他 VM 系统内的其他 APPC/VM 应用程序
- 驻留在 SNA 网络中非 VM 系统中的 APPC 应用程序

z/OS 类比：此功能与 z/OS 中的功能相同。

#### 2.3.5 Dump 查看设施

Dump 查看设施（DVF）帮助您交互式诊断系统问题。使用此设施，您可以从虚拟机转储中交互式显示、格式化和打印数据，并显示和格式化记录的跟踪数据。

BLOCKDEF 实用程序使您能够显示、格式化和打印控制块信息。VIEWSYM 命令可让您显示症状记录，从而在问题发生时更易于识别重复问题。

z/OS 类比：DVF 与 z/OS 中的交互式问题控制系统（IPCS）类似。

#### 2.3.6 组控制系统（GCS）

组控制系统（GCS）在扩展架构（XA）或扩展通用（XC）模式虚拟机中代替 CMS 运行。它是一个虚拟机监视器，提供多任务服务，允许在虚拟机中同时保持大量任务处于活动状态。

GCS 的一个功能是支持原生 SNA 网络。SNA 网络依赖于 ACF/VTAM、VTAM SNA 控制台支持（VSCS）以及其他网络应用程序来管理终端、控制器和处理器之间的链路集合。GCS 为 ACF/VTAM、VSCS 和其他组件提供服务，从而消除了您对 VTAM 通信网络应用程序（VM/VCNA）和 VSE 等第二个操作系统的需求。

#### 2.3.7 z/VM 的 HCD 和 HCM

z/VM 的硬件配置定义（HCD）和硬件配置管理器（HCM）提供了一个全面的 I/O 配置管理环境，与 z/OS 操作系统提供的环境类似。

HCM 在通过 TCP/IP 网络连接连接到 z/VM 系统的基于 Windows 的个人计算机上运行。HCM 提供图形用户界面和命令来帮助您配置系统。您向 HCM 提供所需的 I/O 配置信息，HCM 处理这些信息并将其传递给 HCD。

HCD 在 z/VM 服务器虚拟机中运行，并执行创建和更改您的 I/O 配置的硬件和软件方面的任务。

尽管 HCM 为 HCD 提供主要用户界面，但如果 HCM 不可用，HCD 也为某些 I/O 配置任务提供在 z/VM 主机上的备份用户界面。

z/VM 的原始动态 I/O 配置功能仍然有效。这些功能由一组系统操作员命令组成，用于在系统继续运行的同时更改硬件服务器的 I/O 配置，或管理服务器中所有逻辑分区的硬件 I/O 配置。

您可以选择使用这些命令或使用 HCM 和 HCD 来管理您的 I/O 配置。但是请注意，使用 HCM 和 HCD 与原始动态 I/O 配置功能不兼容。您应为 z/VM 系统的任何给定 IPL 选择一种方法使用。

z/OS 类比：z/VM 的 HCD 和 HCM 在 z/OS 中功能相同。

#### 2.3.8 Language Environment

Language Environment 为用 C/C++、COBOL 或 PL/I 语言编写的程序提供运行时环境。Language Environment 帮助您创建混合语言应用程序，并为您提供一致的方法来访问常用、频繁使用的服务。

Language Environment 由以下功能组成：

- 基本例程，支持启动和停止程序、分配存储、与用不同语言编写的程序通信，以及指示和处理条件。
- 常用库服务，例如数学服务和日期时间服务，这些服务通常被系统上运行的程序所需要。这些功能通过可调用服务的库得到支持。
- 运行时库的语言特定部分是一致的。由于许多语言特定例程调用 Language Environment 服务，因此跨语言的行为是一致的。





z/OS 类比：Language Environment 的功能与 z/OS 中的相同。

#### 2.3.9 OSA/SF

Open Systems Adapter-Express（OSA-Express）和 Open Systems Adapter-Express2（OSA-Express2）是集成硬件功能，允许 System z 平台直接为本地局域网（LAN）和广域网（WAN）上的客户端提供工业标准连接。

Open Systems Adapter Support Facility（OSA/SF）是随 z/VM 提供的基于主机的工具，可让您自定义 OSA 的操作模式。您可以通过 CMS 用户 ID、通过对 OSA/SF API 的 REXX 调用，或通过基于 Java™ 的图形用户界面（GUI）访问 OSA/SF。

z/OS 类比：OSA/SF 的功能与 z/OS 中的相同。

#### 2.3.10 REXX/VM

REXX/VM 包含 REXX/VM 解释器，用于处理类英语的重构扩展执行器（REXX）编程语言。它还包含 SAA® REXX 编程语言的 z/VM 实现。REXX/VM 为 CMS 和 GCS 组件中的 REXX/VM 解释器提供单一源代码库。REXX/VM 解释器利用 31 位寻址。

REXX/VM 解释器有助于提高您组织的生产率。使用 REXX，您可以编写定制的应用程序和命令过程、定制 CMS 命令，并创建新的 XEDIT 宏。

z/OS 类比：REXX/VM 与 z/OS 中的 REXX 存在细微差异。例如，z/VM 上的默认 REXX 环境为 CMS，而在 z/OS 中则为 TSO。

#### 2.3.11 TSAF

Transparent Services Access Facility（TSAF）提供 VM 系统集合内的通信服务，而无需使用 VTAM。TSAF 在 CMS 虚拟机中运行。

最多八个安装并运行 TSAF 的 VM 系统可以组成一个 TSAF 集合。TSAF 集合中一个 VM 系统上的 APPC/VM 程序可以与集合中其他 VM 系统上的其他 APPC/VM 程序通信。路由对应用程序是透明的。应用程序之间的通信就像应用程序运行在同一系统上一样进行。

#### 2.3.12 VMSES/E

Virtual Machine Serviceability Enhancements Staged/Extended（VMSES/E）可帮助您安装 z/VM 和其他启用 VMSES/E 的产品，并应用纠正或规避所报告问题的代码更改。VMSES/E 处理源代码和目标代码。

VMSES/E 还可帮助您定义、构建和管理保存的段。VMFSGMAP 命令提供保存段映射接口，让您在系统上实际构建之前修改保存段定义并查看保存段布局。

z/OS 类比：VMSES/E 在概念上与 SMP/E 相似。

下一节提供 z/VM 可选功能的概述。

#### 2.3.13 DFSMS/VM

Data Facility Storage Management Subsystem for VM（DFSMS/VM）可让您更高效地控制数据和存储资源。

z/OS 类比：DFSMS/VM 的功能与 z/OS DFSMS™ 相似。

DFSMS/VM 提供空间管理、minidisk 管理、ISMF 和 IBM 磁带库数据服务器支持。这些在以下各节中进行了描述。

##### 空间管理

DFSMS/VM 通过自动管理 SFS 文件池中的空间来改善 DASD 使用。作为 SFS 管理员，DFSMS/VM 允许您：

- 通过为文件和目录分配管理类，将 SFS 存储转换为 DFSMS 管理的存储。每个管理类告诉 DFSMS/VM 如何在管理文件池的过程中处理其成员。

#### 2.3.14 DirMaint

利用系统架构固有的可靠性、可用性和可维护性优势。

- DirMaint 允许任何需要分配或释放 minidisk 区的事务自动处理。
- DirMaint 允许所有用户发起的事务受密码控制并记录用于审计目的。
- 命令授权通过将 DirMaint 命令分配给特权命令集来控制。用户可以被授权从多个命令集发出命令。DirMaint 提供九个预定义的命令集，但最多支持 36 个集合。
- 用户退出例程使远程系统的集中目录维护成为可能。某些退出例程还使 DirMaint 能够与其他设施（如 RACF）交互。
- 开放的命令结构允许您用自己的用户编写命令替换所有命令。
- 用于复制 CMS minidisk 文件的自动化流程最大限度地减少了人为错误的可能性。此过程在将旧（源）minidisk 归还到可用 minidisk 池之前，可选择对其进行格式化。
- 通过防止新 minidisk 空间意外分配到现有区上来确保 CMS 文件的完整性。
- DirMaint 通过最大限度地减少所需的 DIRECTXA 实用程序运行次数来提高整体系统效率。更新就地设施（DIAGNOSE 代码 X'84'）可用于立即在线放置许多更改。
- 通过提供强制定期更改密码的能力来增强系统安全性。更改密码时，用户需要输入两次新密码以防止打字错误。
- DirMaint 允许通过要求为每个用户事务输入密码来实现额外的安全级别。这是默认值。

#### 2.3.15 Performance Toolkit for VM

Performance Toolkit for VM™，源自 FCON/ESA 程序（5788-LGA），可在以下方面协助操作员和系统程序员或分析员：

- 以全屏模式操作系统操作员控制台
- 支持管理多个 VM 系统
- VM 历史文件的后处理
- 性能监控
- 通过 Web 服务器提供数据以便使用 Web 浏览器查看





- 基于个人计算机的图形
- TCP/IP 性能报告

除分析 VM 性能数据外，性能工具包还处理从资源管理设施（RMF™）Linux 模块化数据收集器 rmfpm s 获取的 Linux 性能数据。收集到的数据可以使用 RMF PM 客户端应用程序进行分析。从 RMF 获得的 Linux 性能数据可以以类似于 VM 数据呈现的方式进行查看和打印。

rmfpm s 应用程序可从以下站点获取：

```
http://www.ibm.com/servers/eserver/zseries/zos/rmf/rmfhtmls/pmweb/pmlin.html
```

> z/OS 类比：此应用程序类似于 z/OS 中的 RMF MONITOR。

#### 2.3.16 用于 z/VM 的 RACF 安全服务器

用于 z/VM 的资源访问控制设施（RACF）安全服务器是一种安全工具，它与 z/VM 基础系统中的现有功能协同工作，为安装环境提供改进的数据安全性。RACF 通过控制对信息的访问来保护信息。

RACF 还控制您在操作系统上可以执行的操作并保护您的资源。它通过识别和验证用户、授权用户访问受保护的资源以及记录和报告访问尝试来提供这种安全性。

为了帮助每个安装环境满足其独特的安全要求和目标，RACF 提供：

- 灵活控制对受保护资源的访问
- 能够为其他产品存储信息
- 选择集中式或分散式控制配置文件
- 对用户透明
- 为安装环境编写的例程提供出口

您的组织可以定义使用 RACF 保护的系统的人员和组。安全管理员使用 RACF 为每个人定义一个配置文件，该配置文件标识该用户的用户 ID、密码和其他信息。

处理 z/VM 系统与外部源之间的数据传输。数据在 RSCS 接收后存储在假脱机（spool）中，直到 RSCS 可以将其转发到目的地。RSCS 使用通信设备在本地 z/VM 系统与其他系统或远程位置之间传输数据。

RSCS 网络中的节点要么是系统节点，要么是站节点。站节点可以发出和接收信息，可以是计算机、工作站或打印机。但是，系统节点必须是计算机。除了发出和接收信息外，系统节点还可以在两个其他节点之间中继信息。

RSCS 可以与在兼容网络作业输入（NJE）的子系统控制下运行的系统节点通信，这些子系统可能需要许可，例如：

- JES2 或 JES3
- RSCS
- VSE/POWER
- AS/400® 通信实用程序
- 为 Linux 或 AIX® 提供 NJE 功能的产品

RSCS 可以与以下类型的站节点通信：

- ASCII 打印机或绘图仪
- 在提供多路传送协议的系统的控制下运行的计算机
- IBM 3270 信息显示系统打印机
- TCP/IP 网络中的行式打印机路由器（LPR）守护进程和客户端
- TCP/IP 网络中的主动文件传送（UFT）守护进程和客户端
- 在远程作业输入（RJE）控制下运行的工作站

RSCS 网络中的每个链路都与一个称为 *驱动程序* 的编程例程相关联，该例程管理链路上文件、消息和命令的传输和接收。驱动程序管理数据的方式称为 *协议*。所有网络节点之间的文件传输都使用 NJE 协议，3270 打印机使用 3270 数据流，工作站使用 RJE 协议，ASCII 打印机使用适用于该打印机的数据流。

系统网络体系结构（SNA）提供了一组管理链路上通信的协议。RSCS 用于向节点发送数据的方法因用于交换链路的连接类型而异。RSCS 可以支持 send-on-send（连续发送，如二进制同步通信或通道到通道）、SNA 和 TCP/IP 连接。

> **z/OS 类比：** RSCS 网络类似于 z/OS 中的 JES2 网络。





### 2.4 控制程序（CP）

z/VM 的两个主要组件是控制程序（CP）和对话式监控系统（CMS）。本章后面会讨论其他 z/VM 组件。在本节中，我们将解释 CP 的功能和概念。我们还将讨论执行模式。

#### 2.4.1 CP 功能和概念

CP 是支撑整个 z/VM 的操作系统。CP 负责虚拟化你的 System z 机器的真实硬件，并允许所有虚拟机同时共享真实硬件资源。

CP 还处理虚拟机的创建和管理。它可以被视为 z/VM 的操作系统组件，因为它负责管理真实设备和资源，并在需要它们的各种任务和用户之间共享它们。

> z/OS 类比：CP 类似于 z/OS 中的 NUCLEUS 或 SUPERVISOR，或 Linux 操作系统中的内核。

作为资源管理器，CP 可以为你提供一组虚拟机，这些虚拟机可以运行任何原本不会在你的 System z 硬件上运行的操作系统。没有 CP，你在任何给定时间只能在硬件上运行一个操作系统（不考虑逻辑分区），并且每个操作系统可以拥有多个虚拟机（也称为客户机），并且每个客户机允许你同时运行一个操作系统的实例。如图 2-4 第 34 页所示，CP 允许你在同一块硬件上同时运行多个 Linux 和 z/OS 镜像。

![](img/b0a4b9056f819dccd4781a5105c92d45_49_0.png)

图 2-4 CP 执行多个客户操作系统

请注意，在图中，即使我们只有 4 个 CPU 和 16 GB 的真实存储，我们的客户虚拟机总体上被定义为拥有 16 个 CPU 和 20 GB 的存储。这是因为客户操作系统中的 CPU 和存储是虚拟的。如果你愿意，可以创建一个拥有 64 个 CPU 的客户机；CP 会轮流代表所有 64 个虚拟 CPU 在所有可用真实处理器上执行任务。处理此任务的 CP 组件被称为调度程序和分派程序。

z/OS 类比：这些组件与 z/OS 的进程调度程序和分派程序，或 Microsoft® Windows 和 GNU/Linux 的调度程序非常相似，只是它们为执行调度整个虚拟机，而不是仅仅调度进程。

请注意，这种超额分配资源的能力之所以可行，是因为操作系统通常并不需要在运行的整个时间内始终需要分配给它的 100% 资源。有时该操作系统可能处于空闲状态，而在空闲时，其他操作系统可以使用硬件资源。

虚拟机在名为用户目录的文本文件中定义，如 2.2.4 “用户目录” 第 18 页所述。对于系统上的每个虚拟机，目录中都有一个部分描述该虚拟机。其中一个描述被称为目录条目。

#### 2.4.2 CP 执行模式

在任何时候，你的虚拟机都处于两种基本执行状态之一：

- 运行客户操作系统（客户模式或仿真模式）
- 未运行客户操作系统（CP 模式）

当客户操作系统运行时，它控制着你的虚拟机的设备和资源。你通过终端命令行向虚拟机发出的任何命令很可能由客户操作系统解释，而不是 CP。

然而，当你的虚拟机未运行客户操作系统时，CP 处于控制状态，你的处理器和其他虚拟设备通常处于空闲状态，不消耗真实机器资源。在此状态下，通过终端命令行向虚拟机发出的任何命令都由 CP 解释，而不是客户操作系统。

在你启动客户操作系统之前，你处于 CP 模式。当你启动客户操作系统时，你处于客户模式。如果你关闭客户操作系统，你将返回到 CP 模式。你的虚拟机在任何时刻只能处于这两种模式之一。

不过，你可以在任何时候在这些模式之间切换，即使你的客户操作系统正在运行。如果你切换到 CP 模式而客户操作系统正在运行，该操作系统将被冻结，并且在你离开 CP 模式并返回到客户模式之前不会再次运行。此时，客户操作系统将继续运行，就好像从未被中断过一样。

### 2.5 对话式监控系统（CMS）

对话式监控系统（CMS）是与 z/VM 交互最常用的点。CMS 通过丰富的命令和实用程序集展示了大型机的强大功能，这些命令和实用程序建立在 CP 提供的工具集之上。它是一个操作系统，旨在通过为用户提供比 CP 更高的功能级别的环境来促进大型机虚拟机管理。它的



CMS 在 CP 之上运行，就像任何可以在 CP 上运行的其他操作系统一样。

**z/OS 类比：** CMS 类似于 z/OS 中的 TSO 和 LINUX 中的用户空间。

CMS 可以帮助你执行各种任务，例如：为 CMS 或来宾系统编写、测试和调试应用程序；执行在 CMS 或来宾系统上开发的应用程序；创建和编辑数据文件；在 CMS 和来宾操作系统之间共享数据；以及与其他系统用户通信。

**注意：** CMS 是一个强大的操作环境，但请注意 CMS *不能* 与另一个来宾操作系统同时运行——只有 CP 才能做到这一点。

#### 2.5.1 CMS 中 HELP 命令概述

本节和以下各节解释了 CMS 中帮助系统（HELP 命令（**help**））的使用。它们描述了任务、组件和命令菜单，并讨论了格式选项，例如选择层级（级别）。这些章节列出了调用帮助系统的其他方法，如何处理消息，以及如何在 CMS 中退出帮助系统。

CMS 命令中实用的 **help** 命令提供了有关许多标准系统任务的信息。它还提供了所有 CMS 和 CP 命令的语法和功能，以及可能报告给用户的错误消息的含义。

如果您记不起命令的格式，或者正在寻找有关命令功能的的信息，请使用 **help** 命令。输出显示的信息与 IBM 文档中包含的信息相同。

易于使用的 **help** 命令类似于 Linux 系统上的 **man** 命令。如果您单独输入 **help**，将显示选项及其描述的列表。

本章接下来的几个部分解释了如何更直接地访问 **help** 命令。要从菜单中选择一个条目，将光标放在适当的单词上并按 Enter。另一个帮助窗口打开，例如任务菜单或命令菜单。

**z/OS 类比：** **help** 命令类似于 TSO HELP 或 ISPF 中的 HELP 面板。

#### 任务菜单

任务菜单是帮助系统的部分，它提供了您可以执行的任务的索引和描述，包括创建、修改或更改文件，或自定义 CMS 安装。任务菜单提供有关特定操作的详细信息，而无需您事先知道命令的名称。

当您导航到（向下钻取到）特定主题的最低级别时，您会找到命令的描述和正确格式。

要查看可用的任务和组件列表，请键入以下不区分大小写的命令：

```
help task
```

图 2-5 显示了 help task 命令的输出。

```
HELP TASK                  Task Help Information                  line 1 of 39
(c) Copyright IBM Corporation 1990, 2004

z/VM Help, main panel

This panel lists other Help panels that provide information about
various z/VM functions, topics, and tasks.
To view a Help panel, move the cursor to any character of the name
and press the ENTER key or the PF1 key.

HELPINFO  - HELP Facility topics
MENUS     - z/VM Help menus
TASKS     - Basic z/VM tasks - good choice for beginners
COMMANDS  - z/VM commands available to general users
CMS       - CMS commands
CP        - CP commands
QUERYSET  - QUERY and SET commands and subcommands
TCP/IP    - TCP/IP commands
PF1= Help   2= Top      3= Quit     4= Return    5= Locate   6= ?
PF7= Backward 8= Forward 9= PFkeys 10=           11=          12= Cursor

====> _

Macro-read 1 File
40 a                                                       23/007
```

图 2-5 help task 命令的输出

#### 组件菜单

组件菜单列出了特定 HELP 组件可用的所有命令 HELP 文件的名称。

要显示 CMS 可用的所有命令 HELP 文件，请从图 2-5 中所示的任务帮助信息窗口（HELP TASK 菜单）开始。将光标定位在 CMS 单词下的任何位置，然后按 Enter。

菜单帮助信息窗口显示如下图 2-6 所示。窗口显示了 CMS 可用的所有命令 HELP 文件。

```
CMS MENU                      Menu Help Information                     line 1 of 42
(c) Copyright IBM Corporation 1990, 2004

Help for CMS commands

To view a Help panel, move the cursor to any character of the name
and press the ENTER key or the PF1 key.
An asterisk (*) preceding the name indicates a MENU panel.
A colon (:) preceding the name indicates a TASK panel.

*BORDER   CMDCALL   DSERV    GLOBALV   NETLCNVT   RT       SYNMSGS
*CMSQUERY CMSBATCH Edit     GRAnt     NOTE       RTNDrop  SYNonym
*CMSSET   COMPARE  ERASE    HB        NUCDROP    RTNLoad  SYSWATCH
*CMSUTIL  CONWAIT  ESERV    Help      NUCXLOAD   RTNMap   TAPE
*EDIT     COPYFILE ESTATE   HELPCONV  NUCXMAP    RTNState TAPEMAC
*FILESERV CP       ESTATEW  HI        OPNNMSSG   RUN      TAPPDS
*OPENVM   CReate   ETRACE   HO        Option     SAD T    TE
*OS HELP  CSLGEN   Exec     HT        OSRUN      SAMGEN   TELL
PF1= Help   2= Top    3= Quit    4= Return    5= Locate   6= ?
PF7= Backward 8= Forward 9= PFkeys 10=          11=        12= Cursor

====> _

Macro-read 2 Files

a
23/007
```

图 2-6 CMS 组件菜单

#### 命令菜单

除了帮助系统中提供的任务菜单外，还提供了几个 VM 组件的单独命令菜单，包括 CP 和 CMS 信息的菜单。例如，如果您从初始帮助菜单中选择 CMS 的命令菜单，将显示一个面板，其中列出了可用的 CMS 命令。

菜单导航与任务菜单类似；要选择一个命令，将光标放在其上并按 Enter 或单击 PF1。





#### 2.5.2 帮助（级别）层级

帮助系统提供了多种获取命令信息的方式，具体取决于您的专业水平以及对特定任务所需详细程度。每条命令都可以显示简要、详细或相关层级的帮助。

要显示三种可用层级中的任何一种，请指定以下层级选项之一：BRIEF、DETAIL 或 RELATED。您一次只能指定一个层级选项。但是，在您对指定命令请求了一层帮助后，您可以切换（在该命令可用的其他层级之间切换）。

BRIEF 是默认选项，这意味着如果您未指定选项，则会显示简要层级的帮助（如果可用）。如果某条命令没有简要帮助，则会显示 DETAIL HELP。以下各节提供了有关三种命令帮助层级的更多信息。

#### BRIEF

BRIEF 是帮助的第一层。它适用于许多命令。简要帮助显示所请求命令的简短描述、命令的基本语法（不带选项的命令）、示例，以及如果适用，告知您是否有更多或相关信息可用的消息。

如果您处于全屏 CMS 中并请求 BRIEF HELP，您的窗口会显示您输入的帮助命令，并在其下方，在您的窗口上显示一个窗口，其中显示 BRIEF HELP 信息。如果您未处于全屏 CMS 中，则会显示 Brief Help Information 窗口。

以下示例请求 SENDFILE 命令的简要帮助：

```
help cms sendfile (brief)
```

如果您未处于全屏 CMS 中，则该命令的输出将显示在 Brief Help Information 窗口中，如第 40 页的图 2-7 所示。

图 2-7 请求 sendfile 命令简要帮助的输出

#### DETAIL

DETAIL 层提供命令的完整描述、命令格式、对参数和选项的解释、用法说明以及错误信息。有关 DETAIL 帮助的更多信息，请参阅 z/VM: CMS Commands and Utilities Reference, SC24-6073。

该帮助层有七个子集选项：DESCRIPT、FORMAT、PARMS、OPTIONS、NOTES、ERRORS 和 ALL。通过指定子集选项，您可以显示详细帮助的一个或多个特定部分。

默认选项是 ALL，这意味着会显示整个详细帮助。虽然可以更改默认选项，但要显示整个详细层，您必须显式指定 ALL 作为子集选项。有关子集选项和 DETAIL 命令的更多信息，请参阅 z/VM: CMS Commands and Utilities Reference, SC24-6073。

例如，要在 CMS 环境中显示 SENDFILE 命令的所有详细信息，请输入以下命令：

```
help cms sendfile (detail)
```

图 2-8 显示了在 All Help Information 窗口中该命令的输出。

```
SEND FILE
All Help Information
line 1 of 807

>>-- -SENDFile-...-! Choice A |-----------------><
`-SFIle-----' |!- Choice B |-
'-! Choice C |-

Choice A:
(1) -----------------
| (2) -----------------
| Options |---
'-! -----------------

Choice B:
PF1= Brief 2= Top 3= Quit 4= Return 6= ?
PF7= Backward 8= Forward 9= PFkeys 10= 11= Related 12= Cursor

=====> _

Figure 2-8 Output of the command help cms sendfile (detail)
```

#### RELATED

某些命令的帮助信息条目允许您选择类似命令的帮助条目；这称为相关帮助。

例如，假设您想从 rdrlist 中删除一个文件。在阅读 HELP ERASE 后，您意识到 ERASE 不是正确的命令。相反，使用 ERASE 命令的 RELATED 层可以让您轻松访问正确命令 DISCARD 的帮助文件。

当您请求 SET 或 QUERY 命令的相关帮助时，窗口会列出并简要描述该系统组件可用的所有 SET 和 QUERY 操作数。您可以直接从这些菜单窗口访问任何显示的操作数的帮助信息，只需将光标定位到特定操作数然后按 Enter 即可。

以下示例请求 CMS 环境中 ERASE 命令的相关帮助：

help cms erase (related)





#### 2.5.3 其他帮助选项

另外五个选项会影响帮助显示：SCREEN、NOSCREEN、TYPE、NOTYPE 和 EXTEND。这些选项控制文件和错误消息的显示以及命令的搜索顺序。有关这些选项的完整描述，请参阅 z/VM: CMS Commands and Utilities Reference，SC24-6073。

#### 2.5.4 获取帮助的其他方式

您也可以直接获取特定命令的帮助，而无需经过我们讨论的各种帮助导航形式。如果您知道想要帮助的命令，或想直接导航到该命令，请指定命令类型为：

Help CP MENU    显示可用的 CP 命令的完整菜单。
Help CP command    显示指定 CP 命令的格式。

Figure 2-9 Output of help cms erase (related

#### 2.5.7 退出帮助系统

要在 CMS 中随时退出帮助系统，请使用 PF3 或在命令行输入 quit。这两种操作都会带您返回到之前的视图。请注意，如果您已深入帮助菜单层级并希望逐级返回，可能需要多次发出 quit 命令。

作为替代方案，您可以使用 PF4 通过一次按键完全离开帮助系统。

> z/OS 类比：z/VM 中导航 HELP 菜单与 z/OS 中导航 ISPF HELP 菜单类似。

### 2.6 z/VM 中的网络选项

System z 品牌提供许多解决方案来改善您的网络连接。关于网络的一些关键方面是 System z 和 z/VM 上实现的功能，即 OSA 适配器、HiperSocket 和 VSWITCH。

#### 2.6.1 OSA 适配器

Open Systems Adapter（OSA）是一种网络控制器，可安装在大型机 I/O 机箱中。该适配器集成了多个硬件功能并支持多种网络传输协议，包括快速以太网、千兆以太网、10 千兆以太网、异步传输模式（ATM）和令牌环。

有多个版本的 OSA 可用：OSA-Express、OSA-Express2 和 OSA-Express3。每个版本的功能略有不同。较旧的 OSA-2 卡已被更新的 OSA-Express 和 OSA-Express2 卡取代且不再提供，但许多旧大型机仍在使用它们。

z/VM 系统或其任何客户操作系统可以通过直接将特定的 OSA 地址专用于该系统来提供网络连接。这可以通过用户目录中的 DEDICATE 语句完成，或通过将设备附加到客户用户 ID。

#### 2.6.2 HiperSockets

HiperSockets 技术可用于 System z 服务器。HiperSockets 是一种集成的任意到任意虚拟 TCP/IP 网络，可在多个 LPAR 或 z/VM 客户机之间提供互连。通过 HiperSockets，您可以连接在同一 System z 上运行的任何服务器，并由于低延迟而改善响应时间。

HiperSockets 是为通过内存总线提供高度可用、高速网络连接而开发的。它可用于应用程序或基础设施场景，其中网络因在同一 System z 服务器上运行的服务器之间交换大量数据而承受压力。它还提供更高的安全性，因为数据包不会离开主机，因此无法在 LAN 上被嗅探。

Figure 2-10 on page 46 显示了在应用程序服务器场景中 HiperSockets 的一种可能实现。当您使用 Linux for System z 技术来构建应用程序环境时，通常会计划采用三层架构：

- ► 前端层是 HTTP 服务器。
- ► 中间层是应用程序服务器。
- ► 后端层是数据库服务器。

采用建议的架构后，环境可以规划为：

- ► 在 Linux for System z 下的 IBM HTTP Server（由 Apache 提供支持）
- ► 在 Linux for System z 下的 IBM WebSphere Application Server
- ► 在 z/OS 下的 DB2® 服务器

如果浏览器通过网络启动会话，则三层之间会开始通信。为避免网络流量，实现 HiperSockets 解决方案可以提供帮助。借助 HiperSockets 提供的优势，层与层之间的网络流量将在 System z 服务器中以内存速度交换。





![](img/b0a4b9056f819dccd4781a5105c92d45_61_0.png)

图 2-10 使用 HiperSockets 的应用服务器场景

有关 HiperSockets 的更多信息，请参见第 301 页的 6.3 节“网络访问”。

#### 2.6.3 用于快速 LPAR 通信的 HiperSockets

HiperSockets 在 System z 服务器上的整合 Linux、z/VM、z/VSE 和 z/OS 虚拟服务器之间提供最快的 TCP/IP 通信。HiperSockets 提供内部虚拟局域网，其作用类似于 System z 服务器内的 TCP/IP 网络。此集成的授权内部代码（LIC）功能，加上支持操作系统设备驱动程序，比使用外部 TCP/IP 网络连接单个服务器或逻辑分区（LP）时，提供了更高水平的网络可用性、安全性、简单性、性能和成本效益。

HiperSockets 功能也称为内部排队直接输入/输出（IQDIO）或内部 QDIO，是 System z 服务器上的集成功能，以极小的系统和网络开销为用户提供高速逻辑 LAN 的连接。

HiperSockets 无需使用 I/O 子系统操作，也无需通过外部网络连接即可在同一 System z 服务器内的 LP 之间进行通信。HiperSockets 在整合众多虚拟服务器的服务器整合中具有重要价值，并且可以用作 Parallel Sysplex® 中某些耦合链路配置的替代方案。

HiperSockets 可定制以适应不同的流量大小。由于 HiperSockets 不使用外部网络，它可以释放系统和网络资源，消除连接成本，同时提高可用性和性能。

##### HiperSockets 连接

在 System z 内的逻辑分区（LP）或虚拟服务器的组合之间可以访问 HiperSockets。这种“*盒内网络*”概念最大限度地减少了网络延迟，并最大限度地提高了 z/VM、Linux on System z、z/VSE 和 z/OS 映像或其组合之间的带宽能力。也可以在 z/VM 下使用 HiperSockets，从而允许客户操作系统（例如许多 Linux 服务器）之间的内部网络。

每个 HiperSockets LAN 使用一个通道路径标识符（CHPID）和 IQD 通道类型。图 2-11 展示了使用四个 HiperSockets（CHPID 为 FC、FD、FE 和 FF）的 HiperSockets 连接示例。

![](img/b0a4b9056f819dccd4781a5105c92d45_62_0.png)

##### HiperSockets 优势

System z HiperSockets 是一种在 System z 服务器的不同逻辑分区（LP）中运行的虚拟服务器之间提供高速 TCP/IP 连接的技术。它消除了这些虚拟服务器之间任何物理布线或外部网络连接的需求。

虚拟服务器构成虚拟 LAN。使用 iQDIO，虚拟服务器之间的通信通过 System z 服务器系统内存中设置的 I/O 队列进行。虚拟服务器之间的流量以内存速度传输。HiperSockets 支持多个虚拟 LAN，这些虚拟 LAN 在 System z 服务器内作为 TCP/IP 网络运行。第 47 页的“HiperSockets 连接”一节讨论了每个 System z 服务器可用的 HiperSockets 数量。

HiperSockets 是 System z 服务器的 LIC 功能。它受以下操作系统的支持：

- 所有在役 z/OS 版本
- 所有在役 z/OS.e 版本
- 所有在役 z/VM 版本
- 所有在役 z/VSE 版本
- Linux on System z

利用 HiperSockets 功能可获得多项优势：

- HiperSockets 可用于在单个 System z 服务器平台上整合服务器之间的通信。可以消除所有整合的硬件服务器，以及互连它们的网络组件的成本、复杂性和维护。
- 需要访问驻留在 System z 服务器上的企业数据的整合服务器可以以内存速度访问，绕过所有网络开销和延迟。
- HiperSockets 可以定制以适应不同的流量大小。（相比之下，以太网和令牌环等 LAN 的最大帧大小由其架构预定义。）使用 HiperSockets，可以根据为每个可能的 HiperSockets 虚拟 LAN 传输的流量特征来定义最大帧大小。
- 由于在 System z 服务器外部没有服务器到服务器的流量，与跨外部 LAN 通信的服务器相比，可实现更高水平的网络可用性、安全性、简单性、性能和成本效益。例如：
  - HiperSockets 提供非常安全的连接，因为它没有外部组件，它提供非常安全的连接。出于安全目的，服务器可以连接到不同的 HiperSockets。所有安全



功能，例如防火墙过滤，对于 HiperSockets 接口来说与其它 TCP/IP 网络接口一样可用。

- HiperSockets 看起来像任何其它 TCP/IP 接口；因此，它对应用程序和受支持的操作系统是透明的。
- 当使用 DYNAMICXCF 设施时，HiperSockets 还可以改善 sysplex 环境中的 TCP/IP 通信。

有关 HiperSockets 的深入讨论，请参阅 IBM System z Connectivity Handbook，SG24-5444。

#### 2.6.4 VSWITCH

虚拟交换机，或 VSWITCH，是 z/VM 支持的最新的 LAN 类型。它在 z/VM 的 4.4 版本中引入，是一种特殊的 guest LAN，可以通过 HiperSockets 或 OSA-Express 设备提供外部 LAN 连接，而无需路由虚拟机。

z/VM 要求有且仅有一台特定机器拥有 VSWITCH 使用的 OSA-Express 设备。这些特殊的虚拟机称为 VSWITCH 控制器，本质上是额外的 TCP/IP 堆栈，代表连接到 VSWITCH 的系统管理 OSA。z/VM 的早期版本有一个预定义的 VSWITCH 控制器。从 z/VM 5.1 开始及更新版本有两个预定义的 VSWITCH 控制器：DTCVSW1 和 DTCVSW2。

VSWITCH 的另一个好处是它可以轻松配置为具有冗余 OSA 设备和额外的控制器，以便在出现问题时，交换机可以切换到备份 OSA 或控制器。

图 2-12 在第 50 页显示了虚拟交换机的逻辑视图及其所在位置。

![](img/b0a4b9056f819dccd4781a5105c92d45_65_0.png)

#### 2.6.5 关于网络的进一步信息

有关网络的更多信息，请参阅以下出版物：

- *Linux on IBM eServer zSeries and S/390: Large Scale Linux Deployment*，SG24-6824
- *Introduction to the New Mainframe: z/VM Basics*，SG24-7316
- *Networking Overview for Linux on zSeries*，REDP-3901

### 2.7 控制台

作为 z/VM 操作员，您可能会使用几种类型的控制台。控制台可以位于同一物理设备上，例如使用 3270 仿真软件的 PC 工作站，或位于物理连接的 3270 终端上。由于 z/VM 的灵活性，控制台的数量因客户安装而异。根据您的安装情况，可能有一个生产系统或多个生产系统。数百个虚拟机中每个都可能运行一个生产系统。无论控制台数量如何，以下四种类型的控制台是可用的，并在下一节中描述：

- 硬件管理控制台
- 主系统操作员控制台
- 每个虚拟机的虚拟控制台
- 当 Linux、z/OS、z/VM、z/VSE 或 z/TPF 等操作系统在虚拟机中运行时，生产系统的系统控制台。

尽管每个站点的控制台数量取决于安装情况，但每个安装至少有一个硬件管理控制台，至少一个主系统操作员控制台，以及一个或多个用于控制虚拟机的虚拟控制台。生产系统通常有自己的系统控制台。

> z/OS 类比：硬件管理控制台和主系统操作员控制台类似于 HMC，用于访问 z/OS LPAR。

有关 z/VM 控制台的更多信息以及如何与每个控制台交互，请参阅 z/VM: System Operation，SC24-6121²。

#### 2.7.1 硬件管理控制台

硬件管理控制台（HMC）与每个中央处理器群集（CPC）通信。根据您站点的安装情况，可以有一个或多个硬件管理控制台。本节仅描述 z/VM 操作员的特定任务。有关使用硬件管理控制台的更多信息，请参阅处理器群集硬件出版物。System z Hardware Management Console Operations Guide，SC28-6867 可在以下位置找到：http://www-01.ibm.com/support/docview.wss?uid=isg2bac11e0b02e3aa73852573f70056c860

从硬件管理控制台，您可以：

- 执行 z/VM 的 IPL
- 监控消息并向 z/VM 发送命令（操作系统消息面板）
- 执行基本的 z/VM 系统管理功能
- 使用集成的 3270 控制台安装、维护和操作 z/VM

> z/OS 类比：z/OS 用户应该已经熟悉这种类型的控制台，因为它也用于定义 LPAR，这是 z/OS 和 z/VM 之间的常见任务，以及访问 z/OS 控制台。

² http://publibz.boulder.ibm.com/epubs/pdf/hcsf2b30.pdf





##### 使用操作系统消息面板

从硬件管理控制台，您可以使用操作系统消息任务（面板），即 SYSC 设备，以 OPERATOR 用户 ID 登录并查看 z/VM 消息。您还可以使用操作系统消息面板在 z/VM 上发出命令。硬件管理控制台与 z/VM 之间的这种通信采用行模式。

要在 z/VM 系统的初始程序加载期间将操作系统消息面板用作系统操作员控制台，请执行以下任务之一（在下面的列表中，请参阅 z/VM: CP Planning and Administration, SC24-6083 中列出的命名章节）：

- 使用独立程序加载器（SAPL）时指定 CONS=SYSC IPL 参数。参见“传递 IPL 参数。”
- 指定加载参数 CONSSYSC 以绕过 SAPL 窗口并使 z/VM 操作员在操作系统消息面板上打开。参见“覆盖独立程序加载器默认值。”
- 在 SYSTEM CONFIG 文件的 OPERATOR_CONSOLES 语句中添加 SYSTEM_CONS。参见“系统配置文件。”

要显示紧急操作系统消息，请在 SYSTEM CONFIG 文件的 EMERGENCY_MESSAGE_CONSOLES 语句中添加 SYSTEM_CONS。

##### 设置和使用集成 3270 控制台

从硬件管理控制台，您可以使用集成 3270 控制台作为系统操作员的控制台。集成 3270 控制台由 z/VM 标识为 SYSG。此控制台使您能够在没有连接的 3270 设备的情况下安装、维护和操作 z/VM。要在 z/VM 系统的初始程序加载期间将集成 3270 控制台标识给 CP，请执行以下任务之一：

- 使用独立程序加载器（SAPL）时使用 CONS=SYSG IPL 参数。
- 指定加载参数 CONSSYSG 以绕过 SAPL 窗口并使 z/VM 操作员在集成 3270 控制台上启动。参见 z/VM: CP Planning and Administration, SC24-6083 中的“覆盖独立程序加载器默认值”。
- 将 SYSTEM_3270 添加到 OPERATOR_CONSOLES 系统配置语句。

3 http://www.vm.ibm.com/pubs/hcsg0b01.pdf
4 http://www.vm.ibm.com/pubs/hcsg0b01.pdf

#### 2.7.2 主系统操作员控制台

主系统操作员控制台是在初始程序加载（IPL）期间 CP 自动登录系统 OPERATOR 虚拟机的控制台。这可以是硬件管理控制台，或在 IPL 期间指定的设备。如果指定了 SYSC，则操作系统消息面板成为系统操作员控制台。如果指定了 SYSG，则集成 3270 控制台成为系统操作员控制台。您的安装通过使用以下语句或参数之一将设备或硬件管理控制台功能（SYSC 或 SYSG）标识为主系统操作员控制台：

- SYSTEM CONFIG 语句，OPERATOR_CONSOLES
- IPL 参数，CONS=xxxx
- 加载参数 CONSxxxx

主系统操作员控制台是您在此书中执行大多数任务的位置。例如，您从主系统控制台输入 CP 命令以执行以下任务：

- 打开 z/VM CP
- 关闭 z/VM CP
- 控制 z/VM 设备
- 与 z/VM 用户通信
- 响应 z/VM 错误
- 收集有关 z/VM 操作的信息

CP 登录到系统 OPERATOR 后，它控制主系统控制台屏幕的格式。如果您不熟悉此格式，请参阅 z/VM: Virtual Machine Operation, SC24-6128。

#### 2.7.3 z/VM 虚拟控制台

您使用的其他控制台是用于创建和初始化工作或生产系统的虚拟机的虚拟控制台。当您执行以下操作时使用此控制台：

- 登录生产系统的虚拟机。
- 设置其所需的任何特殊运行环境。
- 使用 CP IPL 命令在虚拟机中加载生产系统。
- 必须恢复生产系统。
- 控制生产系统的虚拟机。

> 5 位于 PDF 中：http://publibz.boulder.ibm.com/epubs/pdf/hcse8b11.pdf





> **注意：** 要控制生产系统本身，请使用生产系统的控制台。

当您在此控制台登录到生产系统的虚拟机时，CP 控制控制台窗口的格式。如果您不熟悉此格式，请参阅 z/VM: Virtual Machine Operation, SC24-6128。

> **注意：** 对于 z/OS 客户机，当系统控制台响应 z/VM 错误或加载（IPL）系统时，虚拟机控制台可用作 IPL 和错误记录控制台。有关更多信息，请参阅以下书籍：
> 
> ► z/VM: Virtual Machine Operation, SC24-6128
> http://publibz.boulder.ibm.com/epubs/pdf/hcse8b11.pdf
> 
> ► z/VM: Running Guest Operating Systems, SC24-6115
> http://publibz.boulder.ibm.com/epubs/pdf/hcsf8b22.pdf

有关详细信息，请参阅第 2.7.5 节“Getting to know your virtual console”第 54 页。

#### 2.7.4 The virtual machine guest systems console

当另一个操作系统在虚拟机中运行工作时，这被称为客户机系统。您使用客户机系统的系统控制台来控制工作，就好像您直接在硬件上运行客户机系统一样。某些客户机系统的系统控制台与虚拟机操作员控制台位于同一物理设备上；其他安装可能使用单独的设备。

#### 2.7.5 Getting to know your virtual console

要登录 z/VM 系统，请在 z/VM 登录窗口（见图 2-13 第 55 页）上使用以下任一方法：

- ► 在 z/VM 登录窗口的相应行中输入您的用户 ID 和密码，然后按 Enter。
- ► 将光标定位在 COMMAND 行，输入 LOGON 后跟您的用户 ID，然后按 Enter。

有关详细登录信息，请参阅第 59 页的“Logging on”。

#### z/VM ONLINE

![](img/b0a4b9056f819dccd4781a5105c92d45_70_0.png)

built on IBM Virtualization Technology

Fill in your USERID and PASSWORD and press ENTER

> （输入密码时密码不会显示）

```
USERID ===>
PASSWORD ===>
COMMAND ===>
```

RUNNING VMLINUX6

#### Figure 2-13 Logging on using the command line

系统会提示您输入密码（见示例 2-3）。

#### Example-3 Prompt for the password

```
LOGON MAINT
```

```
ENTER PASSWORD (IT WILL NOT APPEAR WHEN TYPED):
```

登录后，CP READ 提示符会出现。再次按 Enter，CP 将加载 CMS。见图 2-14 第 56 页。

然后 CMS 执行 z/VM 用户 ID 的 PROFILE EXEC 文件（如果存在）。在 PROFILE EXEC 中，您可以为您的 z/VM 用户 ID 定义设置。例如，可以定义 PF 窗口键的设置、链接到 MDISK，或加载（IPL）客户机操作系统，如 Linux 或 z/OS。

![](img/b0a4b9056f819dccd4781a5105c92d45_71_0.png)

Figure 2-14 z/VM screen after logon

此时，您已登录到您的 z/VM 虚拟机。在讨论检查虚拟机的基本命令之前，我们先介绍有关 VM 命令的入门信息。

在我们的描述中，我们通用地使用术语 command；它指 CP 命令和 CP 实用程序。z/VM 使用命令语言来对应它创建的两个环境：控制程序和虚拟机。

使用 Control Program（CP）命令语言时：

- 您是 z/VM 系统操作员，并且想要控制位于您计算机房中的真实机器的资源。
- 您是虚拟机用户，并且想要控制您的虚拟机配置和环境。

当您与加载到虚拟机中的操作系统通信时，使用虚拟机命令语言，如下所示：

- 为执行生产或测试工作，将虚拟机加载为 z/VM 系统支持的操作系统之一。您的虚拟机命令语言是您加载的操作系统的命令语言。该命令语言在记录该特定操作系统的库中描述。

为执行服务、安装和维护任务，以及编辑和文本创建、与其他人通信和解决问题，将虚拟机加载为 CMS，它是一个单用户、交互式操作系统。

您可以在以下情况下使用 CP 命令：

- 您的虚拟机处于 Control Program（CP）命令环境中。
  当您登录到 z/VM 且窗口右下角显示 CP READ 时，您的虚拟机处于 CP 环境中。
  在行模式 ASCII 设备上，没有状态区显示 CP READ，因此 CP 显示在输出区。

- 您在全屏模式下在输入命令前按下 Break 键。
  断开键可以是 PA1、VM 默认断开键，或您使用 TERMINAL BRKKEY 命令定义为断开键的另一个键。
  此外，断开键可能被某些应用程序程序或在受保护的应用程序环境中完全禁用。

- 您处于虚拟机命令环境中，未运行全屏模式，并输入 #CP 命令（并且 # 是您的逻辑行结束字符）。

- 您处于 CMS 虚拟机环境中并输入 CP 命令。

- 您处于 CMS 虚拟机环境中并且 IMPCP 功能设置为 ON。

要在 3270 设备上确定当前命令环境，请查看显示器右下角的状态区。CP READ 表示 CP 环境，VM READ 表示虚拟机环境。

如果您在虚拟机中运行 CMS，VM READ 表示 CMS 环境。当 RUNNING 出现在状态区时，输入空输入行以确定您的环境。要输入空行，请按 Enter 但不要输入任何数据。当您输入空行时，状态区将显示 CP READ 或 VM READ。

此外，如果您处于读取状态，无论是在 CP 命令环境（RUN 设置为 OFF）还是 CMS 命令环境中，并输入空行，系统将在系统输出区响应您的命令环境名称：CP 或 CMS。

您可以使用大写和小写字母的任意组合输入 CP 命令。键入命令及其操作数，然后按 Enter 处理命令。





#### 使用 3270 终端

之前，我们解释了如何登录到 z/VM 系统，并且你看到了系统的响应。现在我们讨论在使用 z/VM 系统上的 3270 终端时需要了解的内容。

图 2-15 显示了 3270 窗口的布局。

![](img/b0a4b9056f819dccd4781a5105c92d45_73_0.png)

图 2-15 3270 窗口的布局

窗口的三个区域是：输出显示区、用户输入区和屏幕状态区，如表 2-1 所描述。

表 2-1 显示区域

| Area | Description |
|------|-------------|
| Output display area | - 由第 1 行到第 22 行组成。<br>- 所有消息都显示在此处。<br>- 你输入的命令在此处显示。 |
| User input area | - 由最后两行组成，不包括最后一行的最右侧 21 个字符位置。<br>- 命令可以在此处输入。<br>- 光标控制键、Delete 键、Insert 键和逻辑文本编辑字符可用于更改此区域中的数据。<br>- 按下 Enter 后，CP 会在输出显示区重新显示此处输入的数据。 |
| Screen status area | - 由最后一行的最右侧 21 个字符位置组成。<br>- 屏幕状态指示器显示在此处。<br>- 指示当前环境是 CP 还是 VM。<br>- 此处显示的状态可以是以下值之一：<br>  - CP READ 表示 CP 向显示器发出读取请求，正在等待用户输入内容后才能继续处理。<br>  - VM READ 表示虚拟机正在等待用户的响应后才能继续处理。<br>  - RUNNING 表示 CP 或 VM 已准备好接受命令，或正在处理已执行的命令。<br>  - MORE ... 表示输出显示区已满但仍有更多数据可显示，具体如下：<br>    - CP 等待 60 秒（默认值），然后显示下一个窗口。<br>    - 使用 PA 键（3270）可在不等待 60 秒的情况下查看下一屏幕。<br>    - 使用 Enter 键（3270）可保留当前屏幕（状态更改为 HOLDING）。<br>  - HOLDING 表示用户在响应 MORE ... 时按下了 Enter（3270）。<br>  - NOT ACCEPTED 表示上一次输入未被接受（CP 将键盘锁定 3 秒）。 |

a. 如果你想使用 CMS 的回滚选项，请使用 SET FULLSCREEN ON。默认情况下此功能是禁用的。（请注意，这仅适用于 CMS。）

##### 2.7.6 会话管理

你的会话从登录系统开始，到注销时结束。本节描述了登录、注销以及在会话期间可以执行的其他几个操作。

###### 登录

阅读本节中关于登录的以下详细信息时，请参考第 55 页的图 2-13。

- 登录屏幕包含三个字段：
  - USERID
  - PASSWORD
  - COMMAND

如 2.7.5 “了解你的虚拟控制台”第 54 页所述，有两种登录方式如下：

- 在 USERID 和 PASSWORD 字段中输入你的用户名和密码。
- 使用 COMMAND 行通过发出 CP LOGON 命令，该命令有许多参数可以自定义你登录系统的方式。

要使用 COMMAND 行，请按 Tab 键直到光标定位到 COMMAND 行。（你也可以使用箭头键或鼠标手动将光标移动到 COMMAND 行。）

在 COMMAND 行上，发出 LOGON 命令。LOGON 命令的最简单用法如示例 2-4 所示。

示例 2-4 LOGON 命令的简单用法

```
LOGON TUX1
```

此命令会提示你输入密码。如果输入的密码正确，系统会将你作为用户 TUX1 登录，就像你已在 USERID 和 PASSWORD 字段中输入用户名和密码一样。

###### Notes:

- 如果你在登录屏幕上输入了错误的用户名或密码，正常的输入字段（USERID 和 PASSWORD）会消失，你将被迫从 COMMAND 行使用 LOGON 命令，如果你想再次尝试登录。因此，了解如何使用 COMMAND 行很重要，以防你在首次尝试登录时输入了拼写错误。
- CP LOGIN 命令与 CP LOGON 命令相同。两者都存在是因为有些人更喜欢使用登录一词，而另一些人更喜欢登录。

###### 断开连接

CP 提供了一个非常有用的功能，称为断开连接。你可以在不停止或以任何方式干扰虚拟机中运行的客户操作系统情况下，将终端从虚拟机断开连接。这有效地切断了你的实际终端会话与虚拟机的连接（类似于注销），但虚拟机及其客户操作系统继续运行。使用 DISC（或 disc）命令断开连接，如第 61 页的示例 2-5 所示。

> z/OS 类比：z/OS 没有类似的命令。





##### 设置清屏超时

你可能已经注意到，当你的屏幕填满时，CP 会在屏幕右下角显示文本 More... 并等待你按下键盘上清除屏幕的键，然后再显示更多输出。

> 注意：在 3270 上清屏：使用 Pause（Break）键；使用 IBM Personal Communications 3270 仿真软件时，在屏幕上右键单击鼠标并选择 Clear。

默认情况下，CP 会等待 60 秒让你清除屏幕，然后才自动清除。要自定义此行为，请使用 TERM MORE 命令并使用表 2-2 中描述的超时参数：

```
TERM MORE t1 t2
```

表 2-2 TERM MORE 命令参数

| 参数 | 描述 |
|---|---|
| t1 | CP 在响铃提醒你屏幕将自动清除之前等待的秒数。默认值为 50 秒。 |
| t2 | 响铃后到自动清除实际发生之前的秒数。默认值为 10 秒。 |

要防止 CP 保留屏幕并强制你按下清除键，将两个超时都设置为零（0）秒：

```
TERM MORE 0 0
```

请记住，通过将超时设置为零，你可能没有时间阅读终端上显示的所有消息。在某些情况下，这可能是可以接受的（例如，如果你正在运行一个命令或程序，生成大量你不关心的输出）。

要返回 60 秒的默认行为（响铃前 50 秒，清除前再额外 10 秒），请使用以下命令：

```
TERM MORE 50 10
```

> 注意：你可以为两个超时指定的最大值是 255 秒。这意味着自动清除前的最大等待时间为 8 分钟 30 秒。

##### 突出显示用户输入

CP TERM 命令有一个参数，可使所有用户输入（即你专门输入的所有文本）以与其它文本输出不同的颜色突出显示。

要启用突出显示，请使用 TERM HILIGHT ON 命令。此后你输入的任何命令都将在屏幕上以不同颜色突出显示。启用颜色更改有助于你在视觉上将输入与输出区分开来，通常使终端文本更易于阅读。

要禁用突出显示，请使用 TERM HILIGHT OFF 命令。

##### 更改屏幕颜色

你可以使用 SCREEN 命令更改 CP 在 3270 终端仿真器窗口中显示输入、输出和状态所使用的颜色，参数如表 2-3 所述：

```
SCREEN area-output color effect
```

表 2-3 SCREEN 命令参数

| 参数 | 描述 |
|-----------|-------------|
| area | 你想要更改的屏幕区域。有效区域或输出类型列于表 2-4。 |
| color | 你想要为所选区域中的文本使用的颜色。有效颜色为：
  - BLUE
  - TURQUOISE
  - RED
  - PINK
  - GREEN
  - WHITE
  - YELLOW |
| effect | 你想要应用于所选区域中文本的效果。有效效果列于表 2-5。 |

表 2-4 在第 65 页列出了 SCREEN 命令的有效区域和输出格式。

##### 表 2-4 SCREEN 命令的有效区域和输出格式

| 区域或输出 | 描述 |
|---|---|
| INAREA | 你向 CP 和客户操作系统发出命令的命令行区域。 |
| STATAREA | 屏幕底部终端状态的显示。 |
| OUTAREA | CP 和客户操作系统的消息放置供你查看的区域。屏幕的大部分是此区域。 |
| CPOUT | 这会使所有来自 CP 的消息按命令参数中指定的格式进行格式化。 |
| VMOUT | 这会使所有来自客户操作系统的消息按命令其余部分中指定的格式进行格式化。 |

表 2-5 列出了 SCREEN 命令的有效效果。

##### 表 2-5 SCREEN 命令的有效效果

| 效果 | 描述 |
|---|---|
| BLINK | 这会使屏幕上的文本闪烁。 |
| REVVIDEO | 反转视频会交换文本颜色和背景颜色。例如，绿色文本在黑色背景上应用反转视频效果后变为黑色文本在绿色背景上。 |
| UNDERLIN | 这会使文本下划线。 |
| NONE | 这不会应用任何效果。它以指定的颜色正常打印文本。 |

> 注意：要将终端重置为默认状态，请使用以下 SCREEN 命令：

```
SCREEN ALL DEFAULT
```

### 2.8 使用 z/VM 的基本命令入门

本节描述了在 z/VM 系统中导航的基本命令。有关此处讨论主题的更多详细信息，请参阅 IBM Redbooks 出版物《Introduction to the New Mainframe: z/VM Basics》，SG24-6366。





#### 2.8.1 CP

与 CP 的交互主要通过命令行界面进行。您可以在命令行中键入命令并按 Enter 键提交处理，从而向 CP 发出命令。

CP 命令的长度始终为 1 到 12 个字符，并且不区分大小写。命令通常接受参数，所有参数均以空格分隔（与大多数命令行环境一样）。

许多命令可以缩写，但缩写形式更晦涩难懂。例如，QUERY NAMES 命令可以缩写为 Q N。执行任一版本的命令都会完成相同的任务。

本章始终使用完整命令，而非缩写形式。如果您想知道某个命令的缩写，请参阅 help 命令或《CP 命令和实用程序参考》（SC24-6073）。

##### 进入 CP 模式

登录后，可能会发生各种情况，具体取决于您的虚拟机所运行的客户操作系统。由于我们在此只关心 CP，因此在我们的场景中，我们将关闭正在运行的客户操作系统并进入 CP 模式，以便直接向 CP 发出命令。

您的虚拟机很可能运行的是 CMS 操作系统。要确定是否正在运行 CMS，请查看登录时获得的输出。如果输出类似于示例 2-10，则表示您正在运行 CMS。最后一行（以 z/VM V5.3.0 开头）是 CMS 输出的第一行。

示例 2-10 登录时运行 CMS 所看到的输出

```
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0001 RDR,  NO PRT,  NO PUN
LOGON AT 09:54:43 EDT MONDAY 06/04/07
z/VM V5.3.0    2007-05-02 16:25
```

如果没有出现输出，您可能仍在运行 CMS。输入 QUERY CMSLEVEL 命令进一步检查。如果输出类似于第 67 页上的示例 2-11，则您正在运行 CMS。

##### 示例 2-11 QUERY CMSLEVEL 命令的输出

```
QUERY CMSLEVEL
CMS Level 23, Service Level 701
Ready; T=0.01/0.01 09:57:17
```

重要说明：要停止 CMS 并进入 CP 模式，请发出 #CP SYSTEM CLEAR 命令。但请注意，如果您没有运行 CMS，此命令也可能有效，但它可能会损坏您的客户操作系统。发出 SYSTEM CLEAR 命令等同于将台式个人计算机的电源线从墙上插座中拔出。它会立即停止系统，不给操作系统完成当前操作和执行清理任务的机会。如果此时操作系统正在写入文件，您可能会丢失该文件的内容，甚至可能永久损坏文件系统。

因此，如果您没有运行 CMS，请查阅客户操作系统手册以获取正确的关闭说明。

z/OS 类比：对于 z/OS 用户而言，这类似于在 HMC 上对 LPAR 执行 SYSTEM RESET。

##### 示例 2-12 #CP SYSTEM CLEAR 命令的输出

```
#CP SYSTEM CLEAR
Storage cleared - system reset.
```

此命令会清除虚拟机的内存，并停止和重置其所有虚拟处理器。

如果您确实处于 CP 模式，并且没有运行任何客户操作系统，则应该能够发出 BEGIN 命令并看到示例 2-13 中显示的输出。

##### 示例 2-13 未运行客户操作系统时 BEGIN 命令的输出

```
BEGIN
HCPGIR453W CP entered; program interrupt loop
```

如果显示的内容不同，则很可能您仍在运行客户操作系统。

##### 检查您的虚拟机

CP 有许多命令涉及获取有关您的虚拟机的信息以及定义其虚拟硬件配置。在本节中，我们将介绍用于获取有关您的虚拟机信息的命令。

首先，我们讨论 QUERY 命令，它提供有关您的虚拟机及其所运行系统的有用信息。该命令接受多个参数，其中大多数参数本身还有子参数。我们只介绍 query 命令功能的一部分。

z/OS 类比：Query 类似于 z/OS 中的各种 DISPLAY 命令。

###### CP 版本

QUERY CPLEVEL 命令指示您正在运行的 CP 版本。您可以在登录虚拟机时运行此命令。在 z/VM 术语中，版本通常称为级别（level）。请参阅示例 2-14。

z/OS 类比：对于 z/OS，在发出系统命令 D IPLINFO 时会显示类似信息。也可以通过 TSO 和 ISPF 中的变量显示。

示例 2-14 QUERY CPLEVEL 命令的输出

```
QUERY CPLEVEL
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/02/07 16:28:04 EDT
IPL at 05/03/07 13:06:26 EDT
```

###### 您的客户机名称

如果您刚刚登录，您可能知道您的客户机名称是什么（客户机名称是赋予您虚拟机的唯一标识名称）。但是，如果您同时打开了多个终端，并且忘记了哪个终端对应哪个客户机，则可以使用 CP 命令 QUERY USERID 来确定客户机名称；请参阅示例 2-15。

z/OS 类比：在 z/OS 中（登录到 ISPF 时），您的用户 ID 通常会显示在主选项面板中。

示例 2-15 QUERY USERID 命令的输出

```
QUERY USERID
TUX1 AT VMLINUX6
```




QUERY USERID 命令还会告诉你当前所在的节点。术语“节点”指的是你的客户机所运行的 z/VM 操作系统实例。在本例中，VMLINUX6 是 TUX1 客户机所运行的 z/VM 实例的名称。当你的系统管理员安装 z/VM 时，管理员会设置该节点名称。

注意：术语“虚拟机”、“客户机”和“用户”均指虚拟机。在本书中，我们互换使用这些术语。

##### 你的虚拟机资源

你的虚拟机（如同任何计算机）拥有三类资源：处理器（CPU）、内存（存储）和设备。QUERY 命令会列出关于你的虚拟机的基本信息以及这些资源的信息。

##### 查询虚拟 CPU

使用 QUERY VIRTUAL CPUS 命令来显示为你的虚拟机定义了哪些虚拟 CPU；参见示例 2-16。

###### 示例 2-16 QUERY VIRTUAL CPUS 命令的输出

```
QUERY VIRTUAL CPUS
CPU 00 ID FF02991E20948000 (BASE) CP CPUAFF ON
```

此示例表明有一个虚拟 CPU。如果你有多个 CPU，你的输出将为你拥有的每个额外 CPU 增加一行。

##### 查询虚拟存储

使用 QUERY VIRTUAL STORAGE 命令来显示你的虚拟机所拥有的存储（或 RAM）量。（z/VM 将 RAM 称为存储。除非另有说明，否则在本书中我们使用术语“存储”来指代 RAM。）

示例 2-17 中的输出显示我们的虚拟机有 32M 的存储。存储量以千字节（K）、兆字节（M）、千兆字节（G）或太字节（T）为单位给出。

###### 示例 2-17 QUERY VIRTUAL STORAGE 命令的输出

```
QUERY VIRTUAL STORAGE
STORAGE = 32M
```

##### 查询虚拟全部

使用 QUERY VIRTUAL ALL 命令来显示你的虚拟机上所有设备的列表；参见第 70 页的示例 2-18。

```
QUERY VIRTUAL ALL
STORAGE = 32M
XSTORE = none
CPU 00 ID FF02991E20948000 (BASE) CP CPUAFF ON
No AP Crypto Queues are available
CONS 0009 ON LDEV L0007 TERM STOP HOST TCPIP FROM 10.0.0.1
0009 CL T NOCOUNT NOHOLD COPY 001 READY FORM STANDARD
0009 TO TUX1 PRT DIST TUX1 FLASHC 000 DEST OFF
0009 FLASH CHAR MDFY 0 FCB LPP OFF
0009 3215 NOEOF CLOSED NOKEEP NOMSG NONAME
0009 SUBCHANNEL = 0001
RDR 000C CL * NOCOUNT NOHOLD EOF READY
000C 2540 CLOSED NOKEEP NORESCAN SUBCHANNEL = 0002
PUN 000D CL A NOCOUNT NOHOLD COPY 001 READY FORM STANDARD
000D TO TUX1 PUN DIST TUX1 DEST OFF
000D FLASH 000 CHAR MDFY 0 FCB
000D 2540 NOEOF CLOSED NOKEEP NOMSG NONAME
000D SUBCHANNEL = 0003
PRT 000E CL A NOCOUNT NOHOLD COPY 001 READY FORM STANDARD
000E TO TUX1 PRT DIST TUX1 FLASHC 000 DEST OFF
000E FLASH CHAR MDFY 0 FCB LPP OFF
000E 1403 NOEOF CLOSED NOKEEP NOMSG NONAME
000E SUBCHANNEL = 0004
DASD 0190 3390 LX6RES R/O 107 CYL ON DASD CD31 SUBCHANNEL = 0005
DASD 0191 3390 DKCD37 R/W 005 CYL ON DASD CD37 SUBCHANNEL = 0000
DASD 019D 3390 LX6N01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0006
DASD 019E 3390 LX6N01 R/O 250 CYL ON DASD CD32 SUBCHANNEL = 0007
DASD 0401 3390 LX6N01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0009
DASD 0402 3390 LX6N01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0008
DASD 0405 3390 LX6N01 R/O 156 CYL ON DASD CD32 SUBCHANNEL = 000A
```

你的虚拟机中的每个虚拟设备都有一个特定于你的虚拟机的虚拟设备号（通常称为虚拟设备地址）。在示例中，191 是标签为 DKCD37 的 DASD 卷（磁盘）上迷你磁盘的虚拟设备号。地址 0009 是你的终端会话所使用的虚拟控制台设备。

但这里的关键是要认识到有多种虚拟设备，包括一些 DASD 卷、一个穿孔卡片阅读器和一个打印机。根据你的虚拟机的定义方式，你也可能拥有其他设备。

##### 特权类

CP 使用特权类来监管虚拟机被允许执行的操作类型。

z/OS 类比：从操作系统的角度来看，z/OS 中不存在特权类或类似概念。此概念（或类似概念）必须在 RACF 或类似产品中分配。然而，z/OS 的 UNIX System Services 组件在其文件系统中设置了权限。

特权类在概念上类似于 Linux 环境中的权限。

当你的系统管理员创建你的虚拟机时，管理员会为你分配系统中可用特权类的某个子集。每个特权类由单个字母或单个数字表示，每个类都为拥有该类的用户定义了特定角色。

IBM 默认特权类为 A 到 G，除 G 类外，所有类都定义了特定的系统管理员角色。G 类定义普通用户，并且是没有管理能力的用户的默认类。它是限制性最强的类。

使用 QUERY PRIVCLASS 命令来列出你的虚拟机被授权的特权类；示例 2-19 显示了此命令的输出。

###### 示例 2-19 QUERY PRIVCLASS 命令的输出

```
QUERY PRIVCLASS
Privilege classes for user TUX1
Currently: G
Directory: G
```

这意味着你的虚拟机可以执行任何对 G 类用户有效的命令。由于任何给定特权类中的命令集都可以由系统管理员自定义，因此你能够运行的命令集可能与示例略有不同。

CP 还提供了一个命令 QUERY COMMANDS，用于列出你可用的所有命令，因此无需记住你的特权类或与之对应的命令。示例 2-20 显示了命令 QUERY COMMANDS 的输出。

###### 示例 2-20 命令 QUERY COMMANDS 的输出

```
QUERY COMMANDS
ADSTOP ATTN BEGIN CHANGE CLOSE
COMMANDS COUPLE CPFORMAT CPU DEFINE DETACH
DIAL DISCONNECT DISPLAY DUMP ECHO EXTERNAL
```





FOR INDICATE IPL LINK LOADVFCB LOCATEVM
LOGON LOGOFF MESSAGE NOTREADY ORDER PURGE
QUERY READY REDEFINE REQUEST RESET RESTART
REWIND SCREEN SEND SET SIGNAL SILENTLY
SLEEP SMSG SPOOL SPTAPE STOP STORE
SYSTEM TAG TERMINAL TRACE TRANSFER UNCOUPLE
UNDIAL VDELETE VINPUT VMDUMP XAUTOLOG XSPOOL
DIAG00 DIAG08 DIAG0C DIAG10 DIAG14 DIAG18
DIAG20 DIAG24 DIAG28 DIAG40 DIAG44 DIAG48
DIAG4C DIAG54 DIAG58 DIAG5C DIAG60 DIAG64
DIAG68 DIAG70 DIAG7C DIAG88 DIAG8C DIAG90
DIAG94 DIAG98 DIAG9C DIAGA0 DIAGA4 DIAGA8
DIAGB0 DIAGB4 DIAGB8 DIAGBC DIAGC8 DIAGD0

正如第 71 页的示例 2-20 所示，即使对于类 G 用户而言，默认情况下这是最严格的权限类，也有很多命令可用。以 DIAG 开头的条目代表诊断功能，你的虚拟机可以调用这些功能。诊断功能由程序员使用，类似于 Windows API 调用或 Linux 系统调用。你不能通过在命令行上指定名称来执行这些功能。

如果你登录到具有 B 类权限的用户 ID，可以通过使用 QUERY COMMANDS 命令并将特定命令作为附加参数来确定执行特定 CP 命令所需的权限类，如示例 2-21 所示，使用 ATTACH 命令。

示例 2-21 QUERY COMMANDS ATTACH 输出

```
q commands attach
ATTACH      IBMCLASS=B
Ready; T=0.01/0.01 15:09:46
```

#### 2.8.2 CMS

像任何操作系统环境一样，CMS 也有用于处理文件的命令。本节列出了 CMS 用户常用的文件管理命令。

命令不区分大小写。但是，当我们显示带有部分大写字符的完整命令时，我们只是表示完整命令中可以缩写的部分。例如，FILEList 命令可以完整输入为 filelist，也可以缩写为 file1。

##### The FILEList command

CMS 最有用的命令之一，FILEList 允许你列出迷你磁盘上存储的内容，并通过生成匹配结果的列表来查找文件。

z/OS 类比：类似于 z/OS ISPF 选项 3.4，除了 TSO/ISPF 用户没有真正的文件系统。用户必须知道要操作的数据集的名称。TSO 命令 ISRDDN 列出分配给你的 TSO/ISPF 会话的所有数据集，让你操作它们。ISPF 选项 11（Workplace™）也是一个非常接近的等价物。

命令语法为：

```
FILEList filename filetype fm ( options
```

filename 参数是文件的名称。只有名称与所提供文件名匹配的文件才会被列出。filetype 参数表示文件类型⁶。fm 参数表示文件模式⁷或目录 ID。关于这三个参数（triplet）的更深入讨论见第 4.2.4 节“处理磁盘”，第 129 页。

列出你已经知道名称的文件并不是很有用。你可能想确定目录 ID 上有哪些文件，或者哪些文件具有相同的名称或类型，或者可能想同时完成这些操作。为此，使用星号 (*) 作为通配符。例如，要列出文件模式 A 中的所有文件，你会输入：

```
filel * * a
```

结果如图 2-16 第 74 页所示，显示 A 文件模式只有一个文件，即 PROFILE EXEC 文件。请注意，三元组是 PROFILE EXEC A。

⁶ 在 Linux 等系统上，文件类型被称为文件扩展名。

⁷ 文件模式或目录 ID 是文件所在的磁盘。

###### Figure 2-16 File listing using the FILEList command

```
CERON  FILELIST A0 V 169 Trunc=169 Size=1 Line=1 Col=1 Alt=0
Cmd Filename Filetype Fm Format Lrecl Records Blocks  Date      Time
     PROFILE   EXEC      A1   V    66       19     1 5/09/08 14:53:47

1= Help 2= Refresh 3= Quit 4= Sort(type) 5= Sort(date) 6= Sort(size)
7= Backward 8= Forward 9= FL /n 10= XEDIT/LIST 12= Cursor

====>
                                           X E D I T  1 File
```

请注意，FILEList 命令输出的第一列写着 cmd。你实际上可以在那里输入文件管理命令，例如 erase，然后按 Enter 处理命令。这在管理文件时可以节省时间。

在发出命令时，你可能会忘记指定各种可选参数，例如当你想覆盖文件时 COPYFile 的 replace 参数，或者你可能请求 FILEList 列出你用户空间中不存在的文件模式。在这些情况下，会出现错误消息代码，后面跟着一条可能不足以帮助你确定出了什么问题的消息。但是，要获取帮助，请在 CMS 提示符下输入 help error_code，其中 error_code 是你收到的错误代码。对于



例如，如果你输入 help dmslst069e，而这是一个不存在的文件模式的错误代码，则会打开一个帮助窗口，如图 2-17 所示。

```
MSG DMSLST069E          All Help Information line 1 of 43
(c) Copyright IBM Corporation 1990, 2007

DMS069E <Output filemode|Filemode|Disk|Directory>
    <vdev|void|mode((vdev)|dirname> (is) not accessed(; 
    access_authority|access_authority)

Explanation:The specified disk, directory, or file mode has not been accessed. If "Disk" is displayed and the disk is accessed, it may not be correctly formatted for the command entered. (For example, the command is trying to write a CMS-formatted file on an OS-formatted disk.)

For the CMSDESK command, a R/W disk with file mode A is needed.

For the RECEIVE command, one of the following occurred:

o A read-only file mode was specified on the RECEIVE command and the file cannot be written onto this file mode.

o RECEIVE attempted to read in a file sent using the DISK DUMP command (or SENDFILE with the 'OLD' option), and in order to use DISK LOAD to read the file in, file mode A must be accessed in read/write mode.

PF1= 2= Top 3= Quit 4= Return 5= Locate 6= ?
PF7= Backward 8= Forward 9= PFkeys 10= 11= 12= Cursor

====>
                                          Macro-read 1 File
```

图 2-17 关于错误代码的帮助

##### COPYfile 命令

基本 COPYfile 命令（缩写为 COPY 或 copy）将文件从一个位置复制到另一个位置。指定源和目标文件名、文件扩展名和文件模式。虽然这听起来有点微不足道，但对 CMS 用户来说非常重要。

通常，CMS 用户具有只读访问权限，可以查看和列出只读磁盘上的文件。要更改这些文件，CMS 用户必须先将它们复制到可读写磁盘。允许执行此操作的命令是 COPYFILE 命令。其语法为：

```
COPYfile fileid1 (fileid2 .. fileidn) ( options
```

一个简单的示例是发出：

```
copyfile duane txt a secret data d
```

这会复制你在 A 磁盘上的文件 duane txt，并将其存储为你在 D 磁盘上的文件 secret data。

然而，你并不总是拥有 D 磁盘，或者它可能不总是允许你向其写入文件。在这种情况下，你会收到相应的错误消息。 （请注意，原文件不会被擦除。）

COPYFILE 命令是 CMS 最强大的命令之一。除了上面描述的基本复制操作外，该命令还允许你指定多个输入文件，将特定列复制到新位置，在文件中插入固定数据，选择要复制的记录范围，并执行其他操作。例如，以下命令将文件 MARK TXT 从系统（或 S）磁盘复制到你的 A 磁盘：

```
COPY MARK TXT S = = A
```

另一个命令调用示例是：

```
copyfile duck list c finch = = warbler = a birds file a (append
```

此示例将你在 C 磁盘上的文件 duck list 和 finch list，以及你在 A 磁盘上的文件 warbler list 合并，并将新的合并文件添加到已存在的 file birds file a 的末尾。这种形式的命令类似于 Linux 操作系统中使用 cat 和 >> 命令组合。

COPYFILE 命令还有其他有用的选项。以下示例将文件从你的 S 磁盘复制到你的 A 磁盘，同时确保系统文件的日期时间戳得以保留：

```
COPY ALL XEDIT S = = A (OLDDATE
FILE 'ALL XEDIT A2' ALREADY EXISTS -- SPECIFY 'REPLACE'
```

此示例说明了当输出文件 ID 已存在时（例如，在用户未保留时间戳的先前复制操作之后）发生的常见错误。在这种情况下，你必须使用另一个选项重新发出 COPY 命令，如下所示：

```
COPY ALL XEDIT S = = A (OLDDATE REPLACE
```

所有这些示例中的左括号都是 CMS 约定，改变命令默认操作的动作（即选项）放在其后。不需要右括号。

**z/OS 类比：** z/OS 中的类比是使用 ISPF 选项 3.2 分配目标文件，然后使用选项 3.3 进行复制。也可以在 ISPF EDIT 会话中创建文件的副本。

##### ERASE 命令

ERASE 命令从磁盘存储中删除文件，为其他用途释放空间。它删除一个文件，并且该文件占用的空间可以立即重复使用。ERASE 命令的语法为：

```
ERASE fn ft (fm) ( options
```

例如，以下命令删除你在 A 磁盘上的文件 frank tdata：

```
erase frank tdata a
```

**重要：** ERASE 命令提供对文件数据的即时、不可撤销的删除。它假定文件位于你的 A 磁盘上，除非另有指定。

#### 2.8.3 XEDIT

前几节讨论了如何检查你访问的磁盘以及在文件系统级别处理文件。但文件级别的编辑呢？创建和更改内容是 CMS 用户技能集的重要组成部分。本节介绍最常用于在 CMS 系统上编辑文件的实用程序。

编辑意味着在 CMS 文件中更改、添加或删除数据。你通过编辑器以交互方式进行这些更改；也就是说，你指示编辑器进行更改，编辑器执行更改，然后你请求另一次更改。

XEDIT 是 CMS 编辑器的名称，是 CMS 提供的最灵活、最强大的实用程序之一。用于使用 XEDIT 编辑文件的最短缩写命令是 X 后跟文件名，例如：

```
X PROFILE EXEC
```

同一示例的完整命令调用为：

```
XEDIT PROFILE EXEC A
```




z/OS 类比：z/OS 中对应的功能是 ISPF 编辑。

命令区域是终端底部的一行。在这里，您可以发出诸如 SAVE、FILE 和 QUIT 等命令。如果您在编辑区域（占据窗口大部分区域）输入任何内容，您就是在修改已加载的文件。这可能会让不习惯命令和数据以相同方式操作的新 CMS 用户感到困惑。

重要提示：随时按 Enter 键都会将光标直接移到命令行，但命令行上已有的任何文本都会被执行！

##### XEDIT 窗口布局

基本 XEDIT 窗口包含以下区域：文件标识行、窗口顶部的消息行（提供有关正在编辑的文件的信息）、编辑区、前缀区、当前行和命令区。

本节介绍 XEDIT 窗口的各个区域，并说明每个区域的用途。要跟随操作，请执行以下命令：

```
xedit profile exec a
```

###### 文件标识行

文件标识行是窗口中的第一行，用于标识您正在编辑的文件。显示内容包含有关当前文件的文件名、文件类型和文件模式的信息。

如果您未指定文件模式，编辑器会分配文件模式 A1。文件模式标识文件所在的已访问迷你盘或共享文件系统（SFS）目录。

输入 xedit profile exec a 后，您会在 XEDIT 窗口顶部的第一行看到文件记录格式和记录长度（V 132）。记录格式和记录长度表示行的格式和最大长度。例如，V 132 表示最大记录长度为 132 个字符，行长度可变（V）。请注意，文件行可能比窗口行更长。

###### 消息行

编辑器通过在窗口的第二行和第三行（消息行）显示消息来与您通信。这些消息提供信息，包括是否出错。

###### 编辑区

编辑区显示文件。您可以将光标移到任意行并重新键入字符来修改文件，也可以使用标准 3270 仿真键盘上的特殊键来插入或删除字符。

在按 Enter 之前，您可以在显示的行上进行任意多的更改。按 Enter 后，更改会应用到保存在虚拟存储中的文件副本上。

在编辑会话结束时，FILE 命令会将那些更改永久记录在磁盘或目录中的文件副本上。由于文件可能太长而无法在一个窗口中显示，各种子命令可以滚动窗口，以便您能在文件中前后移动。滚动窗口就像翻书页一样。

###### 前缀区

前缀区由窗口最左侧的五列组成。请注意，文件中的每一行都有一个前缀区。

该区域可能显示五个等号（=====），有时也显示行号，具体取决于所用 XEDIT 的特定配置。在某些情况下，前缀区没有任何特殊标记。

您可以通过在前缀区输入称为前缀子命令的短命令来执行各种编辑任务，例如删除一行。例如：
- ====a=  添加一行
- a====   添加一行
- 3 a==   添加三行
- 5a===   添加五行
- =q==    删除一行

z/OS 类比：XEDIT 中的前缀子命令相当于 ISPF 编辑器中的行命令。

###### 当前行

当前行是窗口中间（刻度上方）的文件行。它被高亮显示，比其他文件行更亮。当前行是一个重要概念，因为大多数子命令都从当前行开始执行其功能。

当前行会在编辑会话过程中随着您滚动窗口、上下移动等而改变。当当前行改变时，行指针（在窗口上不可见）也随之移动。许多 XEDIT 子命令从当前行开始执行其功能，完成后移动行指针。

注意：有时 XEDIT 会配置为显示刻度，该刻度出现在当前行下方，以帮助您编辑。它类似于图形文本编辑器中的边距刻度。

###### 命令区

窗口底部显示的大箭头（====>）指向命令输入区。您与编辑器通信的一种方式是在此行输入 XEDIT 子命令。您可以用大写、小写或大小写混合输入子命令，许多子命令可以缩写。例如，对于 BOTTOM 子命令，以下格式都是有效的：
- BOTTOM
- Bottom
- b

要执行子命令，请将其键入命令行，然后按 Enter。要将光标从窗口任意位置移动到命令行，可以按 Enter 或使用 PF12。

###### 状态区

窗口的右下区域是状态区，显示您编辑会话的当前状态（例如编辑模式或输入模式），以及您正在编辑的文件数量。

z/OS 类比：在 z/OS 中，ISPF 编辑器没有这种类型的状态行。

##### XEDIT 与全屏 CMS

如果您从全屏 CMS 调用 XEDIT，您看到其他用户发送消息的方式与全屏 CMS 关闭时不同。

- 当全屏 CMS 关闭时，消息会出现在已清除的屏幕上，底部显示 HOLDING 状态。您可以清除屏幕以返回 XEDIT 屏幕。
- 如果全屏 CMS 开启，您收到的任何消息都会出现在消息窗口中，该窗口会自动在您的 XEDIT 窗口上方打开。

要在消息窗口中向前滚动，请在边框角落（用加号 (+) 表示）之一键入 f（向前），然后按 Enter。



持续输入 f，直到看完消息窗口中的所有信息。当没有更多信息可显示时，窗口会自动从屏幕上移除。

##### 使用前缀子命令进行数据操作

输入 XEDIT 命令后，你便处于*编辑模式*。必须处于编辑模式才能输入 XEDIT 子命令。你可以使用*输入模式*或快速输入模式将数据输入文件，这两种模式将在后续章节中讨论。

如果正在编辑现有文件，请将光标置于文件区域并输入以替换底层文本。如前所述，XEDIT 将其*快捷方式*称为前缀子命令。前缀子命令是一或两个字符的命令，用于对特定行执行基本编辑任务。

你可以在一个或多个行的五字符前缀区域的任意位置输入前缀子命令。按下 Enter 后，窗口中已输入的所有前缀子命令都会被执行。

> **z/OS 类比：** XEDIT 前缀子命令在功能上与 ISPF 编辑器中的*行命令*类似。

##### 设置当前行

许多子命令从当前行开始执行操作。例如，INPUT 子命令提供空间让你在当前行之后输入数据。你已经看到过 INPUT 子命令在“文件顶部”行之后插入行。

你可以在屏幕上任意行的前缀区域输入正斜杠 (/) 前缀子命令。按 Enter 后，该行将成为当前行。然后，如果输入 INPUT 子命令，在输入模式下输入的新行将插入在当前行及其下一行之间。

##### 添加行

要添加一行，可在前缀区域输入单个字符 A（add，添加）或字符 I（insert，插入）以追加空行。例如，按 Enter 后，紧跟在包含 A 的行之后立即插入一个空行。A 前或后可带数字，表示添加多行。例如，A5 添加五个空行。输入 A 前缀子命令的有效方式如下：

- ===A        在该行后添加一个空行。
- a===        在该行后添加一个空行。
- 10a==       在该行后添加十个空行。
- ===A5       在该行后添加五个空行。

然后在添加的行中输入信息。如果不输入信息，这些空行将在整个编辑会话期间以及文件写入磁盘或目录后保留在文件中。

z/OS 类比：在 ISPF EDIT 中，通常使用 I(nsert，插入) 行命令。

##### 删除行

要删除一行，请在行的前缀区域输入单个字符 D。D 前或后可带数字，表示删除多行。

要删除一组连续行（即一个行块），请在要删除的第一行和最后一行的前缀区域中输入双字符 DD。使用此方法，无需计算要删除的行数；参见示例 2-22。

示例 2-22 连续行删除功能

```
==dd# This is the first line I want to remove.
==## This is the second.
==== This is the third.
==== This is the fourth.
==dd This is the fifth.
```

按 Enter 后，该行块即被删除。该块的第一行和最后一行不必位于同一窗口中；你可以在输入第二个 DD 之前滚动窗口。

输入 DD 并按 Enter 后，屏幕状态区域会显示消息：

DD pending...

使用 PF7 或 PF8 向后或向前滚动，直到找到该块的最后一行为止，然后在前缀区域输入 DD。按 Enter 后，整个行块即被删除。

z/OS 类比：两个编辑器中的功能完全相同。

##### 恢复已删除的行

如果删除了一行或多行，可以在编辑会话期间随时使用 RECOVER 子命令恢复它们。以下子命令可返回在编辑会话中删除的行：

```
RECover n
```




n 表示你想要恢复的行数。恢复的行从当前行开始插入。最后删除的行是首先恢复的行。

如果行是从文件中的不同位置删除的，你可以通过使用 M（移动）前缀子命令将它们放回它们所属的位置。有关此子命令的更多信息，请参阅第 84 页的“Moving lines”。要恢复你在一次编辑会话中删除的所有行，请输入：

```
====> recover
```

在前面 A 和 D 前缀子命令的示例中，删除了六行。要仅恢复最后两行，请使用以下命令：

```
====> recover 2
```

> z/OS 类比：这类似于在 ISPF 编辑器中使用 RECOVERY ON 命令并键入 UNDO，前提是你已在每次想要恢复的编辑步骤之间按下了 Enter。

##### Adding indented lines

要连续添加缩进文本行，在前缀区域键入字符 SI。按下 Enter 后，一行将直接添加到包含 SI 的行之后。光标定位在与上一行文本开始的同一列，从而使你更容易输入缩进文本。

如果你不想再添加行，再次按下 Enter 且在新行上不输入任何内容即可。要在使用 SI 时在文件中添加一个空行，请在前缀区域包含虚线的行上至少进行一次更改（例如按一次空格键）：

. . . . .

请注意，仅仅使用光标位置键将光标移过一行并不会更改该行。

如果你先在新行上输入一些内容，就可以在添加该行后离开该行并在文件其他地方进行修正。当光标远离新行时按下 Enter，另一条新行将添加到最后添加的行之后。只有在按下 Enter 且未在新行上键入文本时，SI 才会被取消。

##### Duplicating lines

要复制一行，在该行的前缀区域输入双引号（"）。可以在双引号前或后加上一个数字以复制该行多次；请参阅第 84 页的 Example 2-23。

###### Example 2-23 Inserting three duplicate lines

```
=3== I want three more copies of this line.
==== They will appear before this line.
```

按下 Enter 后，文件显示的输出类似于 Example 2-24。

###### Example 2-24 Output from inserting three duplicate lines

```
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== They will appear before this line.
```

要复制一段行，无论是一次还是指定次数，请在该块的第一行和最后一行输入两个双引号（"）。可以在第一个双引号前或后加上一个数字（例如 5"）以复制该块多次。

当你键入一个双引号（"）并按下 Enter 时，屏幕的状态区域会显示以下状态，允许你在完成块并按下 Enter 之前滚动窗口：

```
"" pending...
```

> z/OS 类比：在 z/OS 中，这类似于在 ISPF 编辑器中使用 R n（重复）行命令。

##### Moving lines

要移动一行，在要移动的行的前缀区域输入单个字符 M（move）。通过在另一行的前缀区域输入字符 F（following）或 P（preceding）来指示其目标。按下 Enter 后，包含 M 的行将从其原始位置移除，并插入到包含 F 的行之后或包含 P 的行之前，具体取决于情况。

可以在 M 前或后加上一个数字以指示移动多于一行（例如 5M 或 M5）在前缀区域。待移动的行和目标行可以位于不同的屏幕上。

在输入 M、F 或 P 后，屏幕的状态区域会显示一个 Pending 状态。此待处理状态允许你在输入其他前缀子命令之前滚动屏幕。





要移动一段行，请在要移动的第一行和最后一行的前缀区中输入双字符 MM。 要移动的第一行和最后一行，以及目标行，都可以位于不同的屏幕上。 在按 Enter 之前，您可以使用 PF 选择来滚动屏幕。

z/OS 类似： 在 z/OS（ISPF 编辑器）中，M(ove) 命令相同，但使用 A(fter) 而不是 F(ollowing)，以及 B(efore) 而不是 P(receeding)。

##### 复制行

复制行的过程与移动行相同，只是您输入 C 或 CC 前缀子命令而不是 M 或 MM。 复制操作会保留原始行不变，但在目标行处制作副本，目标行由 F 或 P 表示。

z/OS 类似： 在 z/OS（ISPF 编辑器）中，C(opy) 命令相同，与前面所述的 M(ove) 命令的例外情况相同

##### 取消前缀子命令

如果您输入了一个或多个创建待处理状态的前缀子命令，您可以通过在命令行中输入以下子命令来取消所有这些子命令：

```
====> reset
```

按 Enter 后，所有前缀子命令都会从显示中消失，前缀区将根据您的特定 XEDIT 配置恢复为等号、数字或空白字符。

如果您已键入任何前缀子命令（即使那些不导致待处理状态的子命令），但尚未按 Enter，您可以清除屏幕以将其删除。 如果您只键入了几个字符，简单地用空白字符覆盖它们也足够了。

##### 在文件中移动

XEDIT 允许您在文件中向后、向前、向上、向下以及到顶部和底部移动。 您已经看到 PF7 和 PF8 选择被设置为 BACKWARD 和 FORWARD 子命令，它们分别向后或向前滚动一个完整的窗口。 您也可以在命令行中输入 BACKWARD 和 FORWARD 子命令。 这些子命令的格式为：

```
BAckwardn
FOrwardn
```

这里 n 是要滚动的窗口显示次数。 这相当于按 n 次 PF7 或 PF8。 如果省略 n，编辑器将向后或向前滚动一个窗口。

如果您在当前行是文件顶行时输入 BACKWARD 子命令，编辑器会将文件环绕，使文件的最后一行成为新的当前行。 同样，如果您在当前行是文件末行时输入 FORWARD 子命令，编辑器会使文件的第一行成为新的当前行。

假设文件很长，当前屏幕显示位于文件的中间。 要返回到文件的开头，您可以输入多个 BACKWARD 子命令，或者您可以输入 TOP 子命令。

TOP 子命令使文件顶行成为新的当前行。 按如下方式输入 TOP 子命令：

```
====> top
```

BOTTOM 子命令使文件的最后一行成为新的当前行。 按如下方式输入 BOTTOM 子命令：

```
====> bottom
```

当您想在文件的开头或结尾插入新行时，这些子命令很有用。

假设您想将文件向上或向下移动几行，而不是整个窗口。 使用 DOWN 子命令使行指针向前进一个或多个行朝向文件末尾。 所指向的行成为新的当前行。 例如，以下命令会使当前行下方第五行成为新的当前行：

```
====> down 5
```

如果省略数字，则假定为 1 行。 UP 子命令将行指针朝向文件开头移动。 所指向的行成为新的当前行。 例如，以下命令会使当前行上方第五行成为新的当前行。

```
====> up 5
```

同样，如果省略数字，则假定为 1 行。

z/OS 类似： 在 z/OS（ISPF 编辑器）中，这些命令相同。

##### 在文件中搜索

在任何平台上搜索特定单词或短语是文本编辑非常重要的一部分，在使用 CMS 编辑各种配置文件时尤其重要。 使用 XEDIT 时，您可以通过在命令行中使用正斜杠（/）来搜索，如下所示：

```
====> /target_search_string
```

按 Enter 后，XEDIT 会移动到它找到的第一个匹配搜索短语的行。 XEDIT 从当前行向文件末尾方向搜索。 要移动到下一个出现位置，请重新输入命令：

```
====> /target_search_string
```

更方便的解决方案是在搜索命令前加上和号（&）字符：

```
====> &/target_search_string
```

更简单的方法是在命令行中输入等号（=）。

按 Enter 后，XEDIT 会移动到它找到的第一个匹配搜索短语的行。 每次再次按 Enter 时，XEDIT 会移动到文件中的下一个匹配项。

这可以是一种非常强大的浏览文件方式，但您也可以反向搜索。 搜索从当前行开始向文件顶部移动。 要反向搜索，请在搜索命令前加上减号（-），例如：

```
====> -/target (reverse search)
```

在某些情况下，在文件中突出显示短语的所有出现位置可能很有用。 为完成此任务，XEDIT 提供了 ALL 命令：

```
====> all /target
```

从 XEDIT 命令行，ALL 命令列出包含目标搜索短语实例的所有行。 要返回到正常编辑模式，请在不带搜索短语的情况下发出 ALL 命令，如下所示：

```
====> all
```

> z/OS 类似： 在 z/OS 中，这类似于 ISPF 编辑器的 F 'txt'（Find）主命令。




> 注意：使用 ALL 命令或搜索(/)命令时，可以将当前行设置为输出的其中一行。这样，您可以退出搜索结果，并直接在所需位置编辑文件。

##### 设置制表位

您可能希望将信息放置在特定的列中。PF4 键的功能类似于键盘上的 Tab 键。每次按 PF4 键时，光标都会定位到下一个制表列，您可以在其中输入数据。编辑器会根据文件类型定义初始制表设置；您可以使用以下子命令显示这些设置：

```
====> query tabs
```

您可以在编辑会话期间使用 SET TABS 子命令一次或多次更改这些设置：

```
====> set tabs 10 20 30
```

以上面的示例为例，第一次按 PF4 时，光标会在窗口中移动到第 10 列。第二次按时移动到第 20 列，依此类推。您可以在常规的 XEDIT 输入模式中使用 PF4 进行制表，但并非所有其他高级 XEDIT 模式都支持。要更改制表设置，请输入另一个 SET TABS 子命令。要在更改之前查看当前制表设置，请使用以下子命令：

```
====> modify tabs
```

这会在命令行中显示当前的 SET TABS 子命令；您可以覆盖这些数字并按 Enter 来定义新的制表位。

##### 插入外部文件

GET 子命令可将另一个文件的全部或部分内容插入到您正在编辑的文件中当前行的后面。被获取的文件不会被破坏；插入的是该文件的一个副本。

在输入 GET 子命令之前，请将当前行设置为要插入数据位置的前一行。这样，文件将被立即插入到当前行的下方。

要在文件的末尾插入另一个文件，请使用 BOTTOM 子命令将最后一行设为当前行。要在文件的中间某处插入另一个文件，请使用 UP 或 DOWN 子命令将所需行设为当前行。

> z/OS 类比：这类似于 z/OS 中 ISPF 编辑器的 COPY 主命令。

##### 插入另一个文件的全部内容

要将整个文件插入到您正在编辑的文件中，请使用命令：

```
====> get filename filetype
```

例如，如果您正在编辑 FILE1，并希望将 FILE2 SCRIPT A 的全部内容插入到 FILE1 的末尾，请发出以下命令将行指针移动到文件末尾：

```
====> bottom
```

将行指针置于当前文件末尾后，通过发出以下命令导入整个外部文件：

```
====> get file2 script
```

当第二个文件的全部内容插入完成后，编辑器会显示以下消息：

```
EOF reached
```

##### 插入另一个文件的一部分

有时，导入整个文件并无必要；您可能只需要外部文件的一部分。请使用带有附加可选参数的 GET 命令来插入另一个文件的一部分。

第一个附加参数指定要导入的第一行的行号。第二个附加参数表示要插入的连续行数。例如，要插入另一个文件的前 10 行：

```
====> get file2 data 1 10
```

##### 强力输入（Powertyping）

如果您需要连续输入大量文本，而不必担心行号或行长，请输入 POWERINP 命令。这将使 XEDIT 进入称为 power input（强力输入）或 powertyping mode（强力输入模式）的模式。POWERINP 的最短命令缩写是 POW。

当您处于强力输入模式时，窗口顶部会显示一条***强力输入***横幅。任何时候想要退出强力输入模式，只需按 Enter 键。在正常的 XEDIT 会话中，您的文本会被格式化以适合正确的行宽。

将 TOP 或 BOTTOM 命令与 POWERINP 结合使用，可以轻松地在文件前添加或追加内容。

z/OS 类比：POW 类似于 ISPF 的 TextEntry（TE）。

##### 自动保存

为了最大限度降低丢失数据的风险，XEDIT 提供了 SET AUTOSAVE 子命令。该子命令会在您输入或更改了一定行数后，将文件自动写入磁盘。语法如下：

```
SET AUTOSAVE n
```

n 指定输入或更改的行数。例如，每次更改 10 行就将文件写入磁盘或 SFS 目录，请输入：

```
====> set autosave 10
```

自上次自动保存（AUTOSAVE）以来您对文件所做的更改次数会以更改计数（Alt=n）的形式显示在文件标识行中。当更改计数等于 AUTOSAVE 设置值，且文件中至少包含一条记录时，文件会保存到磁盘或 SFS 目录，并将更改计数重置为零（0）。

您可以在编辑会话期间随时输入 SET AUTOSAVE 子命令，但最佳做法是在输入 XEDIT 命令创建新文件或从磁盘或 SFS 目录调用现有文件后立即输入。

当文件被自动保存时，它会写入一个新文件，该文件的文件名为一个数字，文件类型为 AUTOSAVE。如果在编辑会话期间系统发生故障，您可以恢复截至上次自动保存时所做的所有更改。

为此，请使用带有 REPLACE 选项的 CMS COPYFILE 命令，用 AUTOSAVE 文件替换原始文件。如果您在创建新文件或修订现有文件时输入了 SET AUTOSAVE 子命令，然后输入 QUIT 子命令，则新建或修订的文件不会保存，但 AUTOSAVE 文件可在磁盘上使用。

> z/OS 类比：此功能类似于 ISPF 编辑器中的 RECOVERY ON 命令，区别在于您无法设置每次保存之间的行数。按 Enter 键或 PF 键会将编辑更改保存到单独的数据集中。如果编辑会话终止，下次编辑该特定数据集时，系统会提示您进行恢复。

##### 结束编辑会话

您可以使用 FILE 或 QUIT 命令结束编辑会话。当您使用 XEDIT 命令创建新文件时，该文件会在虚拟存储中创建。当您修改现有文件时，这些修改是针对该文件的一个副本进行的，该副本会在输入 XEDIT 命令时被调入虚拟存储。




然而，虚拟存储是临时的。要将新文件或修改过的文件写入磁盘，请输入以下子命令：

```
====> file
```

当你使用 FILE 子命令时，文件会被写入磁盘或目录，并且控制权会返回给 CMS。你必须使用 FFILE 来保存一个空文件。

QUIT 子命令结束编辑会话，并使文件的永久副本保持完整地留在磁盘或目录上。你可以通过选择 PF3 或在命令行输入 quit 来执行 QUIT 子命令：

```
====> quit
```

使用 QUIT 子命令可在不保存对文件的更改的情况下退出 XEDIT。当你只是为了查看文件而不更改其内容，或在修改文件时出现错误时，这种退出 XEDIT 的方法会很有用。

如果文件是新的并且你没有输入任何数据，则文件不会被写入磁盘。如果文件是新的或已被更改，则以下警告信息会防止你无意中使用 QUIT 而不是 FILE：

```
File has been changed; type QQIT to quit anyway
```

如果你确实不想保存文件，请输入 QQUIT（缩写为 QQ）：

```
====> qquit
```

> z/OS 类比（z/OS/ISPF 编辑器类比）：主命令 CAN(cel) 与不保存退出是相同的。SAVE 命令无论数据集合或成员是否已更改都会保存它。

> ISPF 中 EDIT 配置文件值为 AUTOSAVE ON 意味着使用 PF3 退出编辑器时会保存已修改的数据集合或成员。如果 AUTOSAVE 设置为 NO，编辑器会提示你输入 SAVE 或 CANCEL（这与使用 XEDIT 命令非常相似）。

##### 自定义 XEDIT

你可以通过在你的 A 磁盘上创建 PROFILE XEDIT 文件来改进 XEDIT 界面。XEDIT 从任何数据编辑程序的基本要求开始（即，它应允许你从屏幕上交互地添加、删除或更改文件中的记录）。它还提供了一系列额外且更专业的函数。几个高级功能包括：

- 精细的数据定位命令
- 程序可控的更改
- 显示布局定制
- 选择性数据显示
- 同时处理多个文件
- 每个物理显示多个逻辑显示

认识到需要编辑器的不同用户种类，以及他们不同的期望和要求，XEDIT 允许每个用户定义文件数据应如何显示以及命令应如何生效。讨论这些高级功能，以及更多内容，已超出本书的范围。

示例 2-25 显示了一个示例 PROFILE XEDIT。

###### 示例 2-25 带有基本 XEDIT 自定义的示例 PROFILE XEDIT A

```
* * * Top of File * * *
/*********************/
/*  Sample PROFILE XEDIT  */
/*********************/

/* Set up function keys to do something useful */
'SET PF01 HELP MENU'    /* XEDIT help                */
'SET PF02 SOS LINEADD'  /* Add a line at cursor position */
'SET PF03 QUIT'         /* Quit XEDIT                */
'SET PF07 BACKWARD'     /* Scroll backward           */
'SET PF08 FORWARD'      /* Scroll forward            */
'SET PF09 ='            /* Re-execute last subcommand entered */
'SET PF10 RIGHT 10'     /* Scroll document to right 10 columns */
'SET PF11 LEFT 10'      /* Scroll document to left 10 columns */
'SET PF12 ?'            /* Retrieve last command issued. */

/* Set up colors */
'SET COLOR PREFIX BLUE'
'SET COLOR ARROW WHITE'
'SET COLOR FILEAREA GREEN'

/* Set up display of editing window */
'SET NUM ON'            /* Show line numbers         */
'SET CMDLINE BOTTOM'    /* Command line at bottom of screen */
'SET SCALE OFF'         /* No "scale" bar across window */
'SET NULLS ON'          /* Allows you to insert text in middle of a line */
'SET CASE M I'          /* Allows uppercase and lowercase characters */
'SET CURLINE ON 3'      /* Current line is always the 3rd visible line. */
'SET FULLREAD ON'       /* move cursor to any spot and char stays put */
'SET STAY ON'           /* stay at loc of last find vs bottom of file */
* * * End of File * * *
```

尝试配置文件的各种选项。例如，将文件保存到你的 CMS 系统中的 PROFILE XEDIT A 会使配置覆盖生效。先从一次添加一行开始，确定你想要什么。示例 2-25 中显示的配置可能无法满足你的



requirements, but it is presented to illustrate the customization available to XEDIT users.

> **z/OS 类比：** ISPF EDIT 配置文件的工作方式类似。
> 
> **提示：** XEDIT PROFILE 允许您自定义 XEDIT，使其行为更类似于 ISPF EDIT，如果您愿意的话。SYNONYM 命令是一个很好的起点。参见 z/VM: XEDIT 用户指南，SC24-6132 手册。

##### 使用 XEDIT 获取帮助

如果您忘记了如何使用子命令，或想查看此处未解释的子命令信息，请选择 PF1，该键设置为 HELP MENU 子命令。PF1 选项列出编辑器可用的所有子命令和宏。

如果 PF1 未显示 XEDIT 的帮助菜单，您可以手动输入命令 HELP XEDIT MENU。将光标移动到所需子命令并按 Enter。子命令说明会出现在窗口中，替换全屏文本处理 HELP 菜单。

要返回到上一个窗口，请选择 PF3。要退出 HELP 显示并在窗口中恢复您的文件，请按 PF4。

> **z/OS 类比：** 在 ISPF 编辑器中，在 ISPF 编辑器中使用 PF1 的工作方式类似，但不能直接用于编辑主命令或行命令。相反，它们以陈旧的方式组织在面板中呈现。

## 向 z/OS 系统程序员介绍 System z 上的 Linux

在本章中，我们概述了 Linux 的来源、现状以及发展趋势。我们还深入探讨了 System z 上的 Linux 及其带来的好处。

## 目标

完成本章后，您应该能够：

- 讨论 Linux 的基本概念
- 使用基本技能在 Linux 中导航
- 识别基本的 Linux 命令

![](img/b0a4b9056f819dccd4781a5105c92d45_110_0.png)

## 3.1 Linux 概述

本节概述了 Linux 以及它如何与 System z 交互。它查看了 System z 上 Linux 发行版的构成，并突出了 System z 发行版最受欢迎的企业级 Linux 版本的主要功能。

### 3.1.1 Linux 历史

从最简单的角度来说，Linux 是一个操作系统。它由赫尔辛基大学的学生林纳斯·托瓦兹于 1991 年开始开发（Linux 代表 Linus UNIX）。Linux 本身实际上只是内核；它实现了多任务和多用户功能，管理硬件，分配内存，并使应用程序能够运行。

多年来，Linux 操作系统已成为 PC 用户、企业服务器和用户的一个真实且可行的替代方案。Linux 提供了 UNIX 服务器或桌面的强大功能和灵活性。它还提供了一套实用程序、Internet 应用程序和功能齐全的桌面界面。

Linux 操作系统已成为强大的 Internet 和许多其他应用程序的服务器平台。Linux 能够从企业 Web、文件传输协议（FTP）、文件和打印机服务器，到广域信息服务器（WAIS）网站甚至企业数据库服务器运行，并具有实时集群或高性能计算集群。

Linux 是一个与 UNIX 系统类似的功能齐全的操作系统。它具有企业 UNIX 系统的许多标准功能。命令结构的<|message|> 管理通过 shell 实现。

> **z/OS 类比：** 这个 shell 与 ISPF shell（ishell）非常相似。这也类似于 z/OS TSO 环境。

增强的图形环境和桌面也可用。

Linux 的结构组织在文件系统上，这些文件系统提供了处理数据和文件所需的接口和抽象。文件与磁盘硬件一起组织在目录中。每个目录可以包含任意数量的子目录，每个子目录包含文件。这与经典的 PC 和 UNIX 操作系统文件结构类似。Linux 支持大多数现有文件系统，要么通过内核内置支持，要么通过内核模块。

### 3.1.2 Linux 组件

Linux 有三个基本组件：

- **内核**
  这提供了低级系统控制和接口、程序和硬件设备管理，以及用户级的抽象层。
- **init**
  这通常是在内核加载到内存后执行的 main 程序。从 init，您可以在用户空间执行不同的运行级别，具有不同的特性。
- **应用程序**
  Linux 应用程序涵盖许多类别。随着越来越多的公司采用这项技术，列表不断扩展。通过为 Linux 编写应用程序，开发成本通常会降低，从而催生新项目并增加整体标题数量。在 Linux 存在的众多水平和垂直市场中，我们可以列出以下类别：办公生产力、Internet 相关、网络和系统管理、软件开发、视频制作、数据管理、会计和金融，以及出版。

Linux 具有与大型 UNIX 操作系统相同的多用户和多任务处理能力。它提供了您在标准 UNIX 系统上找到的相同级别的系统管理。用户可以同时运行多个程序；它具有用户空间和内核空间的单独级别。您可以为不同用户创建用户帐户，并定义他们对文件和系统组件的访问权限。安装新设备和网络连接和控制也作为 Linux 操作系统的标准功能提供。

### 3.1.3 System z 上的 Linux 发行版

目前，System z 的受支持 Linux 发行版可从两个主要 Linux 分销商获得：Novell 的 SUSE Linux Enterprise Server（SLES）和 Red Hat Enterprise Linux（RHEL）。每个 Linux 发行版都有其优缺点。

支持 S/390® 架构的 Linux 自 2000 年初以来已普遍可用，可从 IBM developerWorks® 或 Linux 分销合作伙伴处获得。所有当前发行版（截至 2008 年 5 月）均基于 Linux 2.6 内核。每个发行版都包含额外的中间件和应用程序。发行版还包括基础设施服务，例如域名服务器（DNS）、动态主机配置协议（DHCP）和网络文件系统（NFS）文件服务器，以及 Apache Web 服务器、Squid 代理服务器、简单邮件传输协议（SMTP）邮件服务器和 Samba Windows



networking server. 这些发行版还利用 System z 服务器的 HiperSockets 技术在不同分区之间互连。

可用于 System z 的发行版有：

- Novell：SUSE Linux Enterprise Server (SLES) 10，Kernel 2.6.16 可从以下地址获取：
  http://www.novell.com/partners/ibm/mainframe/

- Red Hat：Red Hat Enterprise Linux (RHEL) 5，Kernel 2.6.18 可从以下地址获取：
  http://www.redhat.com/rhel/server/mainframe/

- Debian：Debian Etch，Kernel 2.6.18 可从以下地址获取：
  http://www.us.debian.org/ports/s390/

- 自行构建：从以下地址下载内核：
  http://www.kernel.org

有关最新内核升级可用的新硬件功能的更多信息，请参阅 developerWorks 中关于 Linux on System z 的导航：

http://oss.software.ibm.com/developerworks/opensource/linux390/index.html
http://www-03.ibm.com/systems/z/os/linux/

## 31 位和 64 位选项

Linux on System z 解决方案可用于 31 位和 64 位环境。选项的可用性取决于 System z 型号和 Linux 发行版。

> 注意：31 位和 64 位寻址环境之间的选择可能取决于您计划使用的应用程序或中间件。某些软件不支持 64 位寻址模式，可能无法正常工作。
> 
> 发行版的最新版本（SLES10 和 RHEL5）仅为 64 位。旧版本（SLES9、RHEL4）可作为 31 位或 64 位发行版提供。

Linux 2.6 内核已在 64 位模式下进行了大量测试，适用于大规模、高可用性系统。IBM 的策略侧重于在 64 位平台上运行中间件应用程序。尽可能推荐使用 64 位企业 Linux 发行版。64 位内核提供更大的内存寻址能力，并为在 System z 上运行 Linux 提供更大的灵活性。使用 64 位内核，您可以在给定的 z/VM 分区中运行许多小型 Linux 映像或较少但更大的 Linux 映像。

最能从 64 位寻址中受益的应用程序包括：

- 数据库
- 需要访问大量数据的应用程序
- Java 应用程序

尽管大多数中间件已移植或将移植到 64 位，但需要注意的是，并非所有中间件都能从更大的地址空间中受益。在这些情况下，中间件继续在 64 位 Linux 发行版上以 31 位寻址模式运行，使用 *兼容模式*。因此，如图 3-1 所示，64 位发行版上提供 31 位库。

![](img/b0a4b9056f819dccd4781a5105c92d45_114_0.png)

图 3-1 兼容模式系统调用仿真

## Linux 集成设施（IFL）

IFL 是为 Linux（或在 VM 下的 Linux）保留的处理器。其意义在于它不能用于运行其他操作系统，并且其存在不会反映在系统型号、MIPS 评级或其他容量评级中。系统型号、MIPS 或其他容量评级方法对软件成本有重大影响。添加 IFL 不会影响与系统 MIPS 相关的成本，从而允许在不影响其他软件成本的情况下使用 Linux。

## 文件系统

Linux 由文件和目录组成层次结构。Linux 文件系统分为以下主要目录：

- /home — 存储所有用户的家目录。这基本上是用户存储其拥有的任何文件的地方：媒体、源代码、桌面配置文件等。root 用户的家目录有时被称为 root 目录。
- /bin — 存储可执行文件（基本系统程序）。用于加载内核模块和访问设备的命令通常放在这里。
- /usr/bin — 存储系统命令（软件的真正仓库）
- /usr/sbin — 存储通常用于执行系统管理任务的命令。
- /usr/local — 是 Linux 文件系统层次结构标准（FHS）的二级目录。遵循 FHS 但您不希望与 FHS 第一级（/usr）上的其他软件混合的软件通常放在这里。例如，您可能正在开发的内部软件。
- /etc — 存储系统和程序的默认配置文件以及可由所有用户共享的程序默认配置文件。也存储运行级别配置文件。
- /var — 存储日志、spool 目录、数据库文件、文件服务器文件和系统锁文件。
- /lib — 存储程序和共享库。
- /dev — 存储设备文件：内存、磁盘、可移动媒体设备（存储、多媒体）和任何类型的硬件。
- /proc 和 /sys — 存储包含实时数据的系统文件系统。这些目录包含 Linux 所见的硬件配置和运行进程的实时数据：处理器、ACPI 参数、进程、每个运行进程的信息（PID、I/O 文件描述符）和内核配置。
- /opt — 存储附加软件。通常，供应商应用程序安装在此处。
- /tmp — 存储临时文件。其内容通常在启动时被删除。切勿在此处放置重要文件。

### root 用户

默认情况下，root 用户是系统管理员，这意味着 root 权限不受限制。由于 root 拥有如此大的权限，不完全了解系统的人可能会造成损害。仅建议在执行管理操作时登录 root。尽管用户 root 等同于



IBMUSER 在 z/OS 中更加强大，因为 root 默认可以访问所有内容。Root 访问权限无法被限制。

## 3.2.2 基本入门步骤

本节讨论基本命令，例如在目录中导航、查看目录或文件的内容以及创建目录。

**重要：** Linux 命令和文件名区分大小写。例如，命令 `chmod` 不能输入为 `Chmod` 或 `CHMOD`。

**提示：** 在开始输入命令或文件名后按 Tab 键可以补全剩余的命令或文件名。此外，按 Ctrl+R 可以搜索所有先前发出的命令。

## 获取 Linux 命令的帮助

Linux 没有像 z/VM 和 z/OS 那样的帮助菜单。相反，Linux 有一个名为 man 的命令，它会显示来自在线参考手册的命令页面。该页面包括：名称、使用的概要、命令功能的描述以及其他详细信息。要使用该命令，输入：

```
man commandname
```

commandname 是你想要获取帮助的命令的名称（参见示例 3-1）。

**注意：** 你必须知道要使用的命令的名称才能访问其手册页。

要滚动浏览文件，请使用上下箭头。要退出文件请按 Q。

*示例 3-1 对 man 命令本身使用 man 命令*

```
lnxken:/ # man man
NAME
    man - an interface to the on-line reference manuals

SYNOPSIS
man [-c|-w|-tZHT device] [-adhu7V] [-i|-I] [-m
system[...]] [-L
locale] [-p string] [-M path] [-P pager] [-r prompt] [-S
list] [-e
extension] [[section] page ...] ...
```

```
man -l [-7] [-tZHT device] [-p string] [-P pager] [-r prompt]
file ...
man -k [apropos options] regexp ...
man -f [whatis options] page ...
```

## DESCRIPTION

man 是系统的手册分页器。传递给 man 的每个 page 参数通常是程序、实用程序或函数的名称。然后找到并显示与每个参数关联的手册页。如果提供了 section，man 将只在手册的该部分中查找。默认操作是在所有可用部分中按预定义顺序搜索，并仅显示找到的第一个页面，即使该页面存在于多个部分中。

下表显示了手册的章节编号及其包含的页面类型。

| Section | Description |
|---|---|
| 0 | 头文件（通常位于 /usr/include） |
| 1 | 可执行程序或 shell 命令 |
| 2 | 系统调用（内核提供的函数） |
| 3 | 库调用（程序库中的函数） |
| 4 | 特殊文件（通常位于 /dev） |
| 5 | 文件格式和约定 例如 /etc/passwd |
| 6 | 游戏 |
| 7 | 杂项（包括宏包和约定），例如 man(7)、groff(7) |
| 8 | 系统管理命令（通常仅 root 可用） |
| 9 | 内核例程 [非标准] |

手册页由几个部分组成。

它们可能标记为 NAME、SYNOPSIS、DESCRIPTION、OPTIONS、FILES、SEE ALSO、BUGS 和 AUTHOR。

## 在文件系统中导航

从一个目录更改到另一个目录的命令是 cd（change directory 的缩写）。命令的正确用法是：

```
cd directoryname
```

directoryname 是要访问的目录的名称（参见第 104 页的示例 3-2）。

## 示例 3-2 cd（change directory）命令

```
lnxken:~^ # cd Desktop/
lnxken:~/Desktop #
```

使用 cd 命令时你有几个选项：

- cd ..    这会将你向上移动一级目录树（参见示例 3-3）。
- cd /    这会将你带到文件系统目录的根，无论你当前在哪个目录中（参见示例 3-4）。
- cd -    这会将你返回到之前所在的目录（参见示例 3-5）。

## 示例 3-3 更改到父目录：cd ..

```
lnxken:/etc/init.d/rc3.d # cd ..
lnxken:/etc/init.d #
```

## 示例 3-4 更改到文件系统目录的根：cd /

```
lnxken:/etc/init.d/rc3.d # cd /
lnxken:/ #
```

## 示例 3-5 更改到上一个目录：cd -

```
lnxken:/ # cd -
/etc/init.d/rc3.d
lnxken:/etc/init.d/rc3.d #
```

## 显示目录的内容

现在你可以在一个目录和另一个目录之间切换，你希望能够查看目录的内容。为此，使用 ls 命令。

- 要列出当前目录的内容，请使用不带选项的 ls 命令。
- 要列出另一个目录的内容，输入带选项的 ls 命令：
- ls directoryname

directoryname 是你想要查看内容的目录的名称。参见示例 3-6。

## 示例 3-6 列出当前目录内容

```
lnxken:/ # ls
bin  dev  home  lib64  media  opt  root  srv  tmp  var
boot  etc  lib  lost+found  mnt  proc  sbin  sys  usr
```




```
lnxken:/ # ls root/
.DCOPserver_lnxken_:3   .gconf        .local        .vnc
.DCOPserver_lnxken_3    .gconfd       .mozilla      .wapi
.ICEauthority           .gnome2       .qt           Desktop
.Xauthority             .gnome2_private .skel
.bash_history           .gnupg        .suse_register.log bin
.exrc                    .kde          .viminfo
lnxken:/ #
```

要列出带详细信息的目录内容，输入 ls -al（参见示例 3-7）。

## 示例 3-7 使用详细信息列出当前目录的所有内容

```
lnxken:/ # ls -al
total 92
drwxr-xr-x 21 root root 4096 May 19 13:58 .
drwxr-xr-x 21 root root 4096 May 19 13:58 ..
drwxr-xr-x 2 root root 4096 May 15 09:50 bin
drwxr-xr-x 4 root root 4096 May 15 09:52 boot
drwxr-xr-x 9 root root 2440 May 19 11:57 dev
drwxr-xr-x 75 root root 8192 May 19 11:58 etc
drwxr-xr-x 3 root root 4096 May 15 13:54 home
drwxr-xr-x 9 root root 4096 May 15 13:26 lib
drwxr-xr-x 5 root root 4096 May 15 13:25 lib64
drwx------ 2 root root 16384 May 15 09:43 lost+found
drwxr-xr-x 2 root root 4096 Jun 16 2006 media
drwxr-xr-x 2 root root 4096 Jun 16 2006 mnt
drwxr-xr-x 4 root root 4096 May 15 09:48 opt
dr-xr-xr-x 57 root root 0 May 19 11:57 proc
drwx------ 16 root root 4096 May 19 13:58 root
drwxr-xr-x 3 root root 8192 May 15 09:51 sbin
drwxr-xr-x 4 root root 4096 May 15 09:43 srv
drwxr-xr-x 10 root root 0 May 19 11:57 sys
drwxrwxrwt 10 root root 4096 May 15 15:15 tmp
drwxr-xr-x 13 root root 4096 May 15 09:50 usr
drwxr-xr-x 14 root root 4096 May 15 09:46 var
lnxken:/ #
```

内容颜色的默认规则如下：

- 目录 = 蓝色
- 文件 = 白色
- 可执行文件 = 绿色
- 链接 = 浅蓝色
- 设备 = 黄色
- 套接字 = 粉色

## 创建目录

要在当前目录中创建目录，使用 mkdir 命令并提供目录名称（也在示例 3-8 中显示）：

```
mkdir directoryname
```

## 示例 3-8 创建目录

```
lnxken:~/Desktop # mkdir MyMusic
lnxken:~/Desktop # ls -al
total 48
drwx------ 5 root root 4096 May 19 15:56 .
drwx------ 16 root root 4096 May 19 13:58 ..
-rw-r--r-- 1 root root 69 May 15 13:48 .directory
-rw-r--r-- 1 root root 1043 May 15 13:48 MozillaFirefox.desktop
drwxr-xr-x 2 root root 4096 May 19 15:56 MyMusic
-rw-r--r-- 1 root root 1797 May 15 13:48 Network.desktop
-rw-r--r-- 1 root root 2483 May 15 13:48 Printer.desktop
-rw-r--r-- 1 root root 887 May 15 13:48 myComputer.desktop
-rw-r--r-- 1 root root 5065 May 15 13:48 trash.desktop
lnxken:~/Desktop #
```

要为目录设置权限，输入以下命令，其中 XXX 是目录的权限代码：

```
mkdir -XXX directoryname
```

参见示例 3-9（有关权限代码的详细信息，请参阅第 3.2.3 节“文件权限”，第 110 页）。

## 示例 3-9 使用特定文件权限创建目录

```
lnxken:~/Desktop # mkdir -m777 MyPictures
lnxken:~/Desktop # ls -al
total 52
drwx------ 6 root root 4096 May 19 16:06 .
drwx------ 16 root root 4096 May 19 13:58 ..
-rw-r--r-- 1 root root 69 May 15 13:48 .directory
-rw-r--r-- 1 root root 1043 May 15 13:48 MozillaFirefox.desktop
drwxr-xr-x 2 root root 4096 May 19 15:56 MyMusic
drwxrwxrwx 2 root root 4096 May 19 16:06 MyPictures
-rw-r--r-- 1 root root 1797 May 15 13:48 Network.desktop
-rw-r--r-- 1 root root 2483 May 15 13:48 Printer.desktop
-rw-r--r-- 1 root root 887 May 15 13:48 myComputer.desktop
```

## 移动文件

要移动文件，使用命令 mv source destination，其中 source 是要移动的文件的位置和文件名，destination 是文件的新位置（参见示例 3-10）。

### 示例 3-10 从一个位置移动文件到另一个位置

```
lnxken:~/Desktop/MyDocs # ls -al
total 20
drwxr-xr-x 4 root root 4096 May 19 17:15 .
drwx------ 3 root root 4096 May 19 17:12 ..
drwxr-xr-x 2 root root 4096 May 19 16:29 MyMusic
drwxrwxrwx 2 root root 4096 May 19 17:13 MyPictures
-rw-r--r-- 1 root root 83 May 19 17:15 smilepic
lnxken:~/Desktop/MyDocs # mv smilepic MyPictures/
lnxken:~/Desktop/MyDocs # ls -al
total 16
drwxr-xr-x 4 root root 4096 May 19 17:16 .
drwx------ 3 root root 4096 May 19 17:12 ..
drwxr-xr-x 2 root root 4096 May 19 16:29 MyMusic
drwxrwxrwx 2 root root 4096 May 19 17:16 MyPictures
lnxken:~/Desktop/MyDocs # ls -al MyPictures/
total 12
drwxrwxrwx 2 root root 4096 May 19 17:16 .
drwxr-xr-x 4 root root 4096 May 19 17:16 ..
-rw-r--r-- 1 root root 83 May 19 17:15 smilepic
lnxken:~/Desktop/MyDocs #
```

> 注意：要重命名文件而不更改其位置，使用 mv 命令并将旧文件名和新文件名作为参数：
> 
> mv oldname newname
> 
> 这会将文件 oldname 重命名为 newname，而不更改其位置。

## 复制文件

要复制文件，使用命令 cp source destination，其中 source 是要复制的文件的位置和文件名，destination 是新的位置和文件名（参见第 108 页的示例 3-11 和第 108 页的示例 3-12）。





## 示例 3-11 复制文件或创建备份

```
lnxken:"~/Desktop/MyDocs/MyPictures # cp smilepic smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures # ls -al
total 16
drwxrwxrwx 2 root root 4096 May 19 17:18 .
drwxr-xr-x 4 root root 4096 May 19 17:16 ..
-rw-r--r-- 1 root root   83 May 19 17:15 smilepic
-rw-r--r-- 1 root root   83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures #
```

## 示例 3-12 从一个位置复制文件到另一个位置

```
lnxken:"~/Desktop/MyDocs/MyPictures # cp smilepic.bak /root/Desktop/MyDocs/
lnxken:"~/Desktop/MyDocs/MyPictures # ls -al ..
total 20
drwxr-xr-x 4 root root 4096 May 19 17:21 .
drwxr-x--x 3 root root 4096 May 19 17:12 ..
drwxr-xr-x 2 root root 4096 May 19 16:29 MyMusic
drwxrwxrwx 2 root root 4096 May 19 17:20 MyPictures
-rw-r--r-- 1 root root   83 May 19 17:21 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures #
```

## 删除文件或目录

要删除文件，请使用命令 rm filename，其中 filename 是要删除的文件名（参见示例 3-13）。要删除目录，请输入命令 rm -Rf filename，其中 -R 表示递归删除该目录中的所有内容，-f 表示强制执行该操作（参见示例 3-14）。

## 示例 3-13 删除文件

```
lnxken:"~/Desktop/MyDocs # rm smilepic.bak
lnxken:"~/Desktop/MyDocs # ls -al
total 16
drwxr-xr-x 4 root root 4096 May 19 17:21 .
drwx------ 3 root root 4096 May 19 17:12 ..
drwxr-xr-x 2 root root 4096 May 19 16:29 MyMusic
drwxrwxrwx 2 root root 4096 May 19 17:20 MyPictures
lnxken:"~/Desktop/MyDocs #
```

## 示例 3-14 删除目录

```
lnxken:"~/Desktop/MyDocs # rm -Rf MyMusic/
lnxken:"~/Desktop/MyDocs # ls -al
total 12
drwxr-xr-x 3 root root 4096 May 19 17:22 .
drwx------ 3 root root 4096 May 19 17:12 ..
drwxrwxrwx 2 root root 4096 May 19 17:20 MyPictures
lnxken:"~/Desktop/MyDocs #
```

## 查看文件内容

要查看文件内容，请使用以下三种命令之一：

- **less filename** 以分页方式显示文件；允许向上、向下、向右和向左滚动。
- **more filename** 以分页方式显示文件；仅允许向下滚动文件
- **cat filename** 一次显示整个文件然后返回到 shell。cat 命令也可以用于将多个文件连接成一个文件。

## 自定义命令

要自定义命令名称，请使用 alias 命令。它提供了一种帮助你记住难以记住的命令的方法。你也可以用它为命令创建快捷方式。示例 3-15 演示了如何使用 alias 命令将 rm 命令重命名为更易于记忆的名称，在此示例中为 erase 命令。

### 示例 3-15 alias 命令

```
lnxken:"~/Desktop/MyDocs/MyPictures # alias erase=rm
lnxken:"~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rw-rw-rw- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures # erase smilepic
lnxken:"~/Desktop/MyDocs/MyPictures # ls -l
total 4
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures #
```

## Linux 命令摘要

第 110 页的表 3-1 列出了帮助你入门 Linux 的基本命令。有关更多命令和 Linux 帮助，请参阅以下网站：

http://www.unixguide.net/linux/linuxshortcuts.shtml
http://blog.lxpages.com/ultimate_linux.html

### 表 3-1 基本 Linux 命令摘要

| 命令 | 描述 | 示例 |
|---|---|---|
| cd | 更改目录 | cd directoryname |
| ls | 列出目录内容 | ls directoryname |
| mv | 移动文件或目录 | mv file newlocation |
| cp | 复制文件或目录 | cp oldfile newfile |
| mkdir | 创建新目录 | mkdir newdirectory |
| rm | 删除文件或目录 | rm filename |
| more | 以有限的导航功能显示文件内容 | more filename |
| less | 以完整导航功能显示文件内容 | less filename |
| cat | 显示文件并可将文件合并在一起 | cat filename |
| man | 提供命令帮助 | man commandname |
| alias | 为命令提供别名 | alias aliasname command |
| pwd | 显示工作目录 | pwd |
| who | 列出当前登录的用户 | who |
| whoami | 显示当前登录的用户 | whoami |
| ps | 列出当前正在运行的所有进程 | ps |

### 3.2.3 文件权限

在 Linux 中，每个目录和文件都有一组权限，该权限根据授权为用户、组和其他人分配读取、写入和执行其他用户文件的权限。

在 Linux 中限制文件访问的三种方式是：

- 读取 (r)：文件或目录只能被读取。
- 写入 (w)：文件或目录可以被修改。
- 执行 (x)：文件或目录可以被执行。





为三种文件访问类型定义了三类用户：

- 用户（u）：拥有文件或目录的人
- 组（g）：属于文件或目录所分配组的一个或多个用户
- 其他用户（o）：不是文件或目录的所有者，也不属于该文件或目录的组的所有用户

文件权限列表中的第一个字符表示文件类型（参见表3-2）：

## 表3-2 文件类型

| 文件类型 | 字符 |
|---|---|
| 普通文件 | - |
| 目录 | d |
| 符号链接 | l |
| 命名管道 | p |
| 套接字 | s |
| 字符设备文件 | c |
| 块设备文件 | b |

文件权限通过使用 `ls -l` 命令列出。图3-3和图3-4展示了文件权限的布局和定位说明。

## 图3-3 文件权限布局

| 位置 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| 布局 | 文件类型 | 用户 |  |  | 组 |  |  | 其他 |  |  |
| 字符 | 类型 | 读 | 写 | 执行 | 读 | 写 | 执行 | 读 | 写 | 执行 |
| 示例 | d | r | w | x | r | w | - | r | - | - |

`ls -l` 命令的布局如图3-4所示。

## 图3-4 `ls -l` 命令的布局

| 类型与权限 | 链接数 | 文件所有者 | 文件所属组 | 大小（字节） | 最后修改日期 | 文件名 |
|---|---|---|---|---|---|---|
| -rwxrwxr- | 1 | Ken | Student | 652 | May 20 10:05 | smilepic |

在示例3-16中，文件 smilepic 显示为 `-rwxrwx-rw-`，这表明：所有者具有读、写和执行权限；组具有读和写权限；其他用户具有读和写权限。

## 示例3-16 文件权限示例

```
lnxken:~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rwxrwx-rw- 1 ken student 83 May 19 17:20 smilepic
-rw-r--r-- 1 ken student 83 May 19 17:18 smilepic.bak
lnxken:~/Desktop/MyDocs/MyPictures #
```

> 注意：尽管用户可能拥有对文件执行某个操作的权限，但根据该文件所在目录的权限，该用户可能仍无法执行该操作。

## 修改权限

用户只能修改自己的文件权限，但不能修改其他用户的权限。请注意，root 用户 ID 确实拥有修改所有文件权限的权力。

用于修改文件权限的 Linux 命令是 `chmod`，它可以通过两种方式使用：八进制法或符号法。

## 八进制法

八进制法使用数字来修改文件权限。用户理解八进制法后，使用它通常比使用符号法更快。

## 表3-3 权限组合

| 值 | 权限 |
| --- | --- |
| 1 | --- |
| 2 | --x |
| 3 | -wx |
| 4 | r-- |
| 5 | r-x |
| 6 | rw- |
| 7 | rwx |

示例3-17展示了使用 `chmod` 命令以八进制数字为文件分配权限。

## 示例3-17 使用 `chmod` 命令的八进制法

```
lnxken:~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rw-rw-r-- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:~/Desktop/MyDocs/MyPictures # chmod 750 smilepic
lnxken:~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rwxr-x--- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:~/Desktop/MyDocs/MyPictures #
```

该示例使用以下命令将文件权限从 `-rw-rw-r--` 更改为 `-rwxr-x---`：

```
chmod 750 smilepic
```

第一个位置的数字 7 表示我们想要将所有者的访问权限从读和写更改为读、写和执行。第二个位置的数字 5 表示我们想要将组的访问权限从读和写更改为读和执行（无写权限）。第三个权限位置的数字 0 表示我们想要将其他用户的访问权限从只读更改为完全无权限。

## 符号法

与 `chmod` 命令一起使用的符号可以包含四个值：

- 用户类型：
  - u 代表用户
  - g 代表组
  - o 代表其他用户

- 所做的更改类型：
  - - 代表移除权限
  - + 代表添加权限
  - = 代表设定权限

- 要应用的访问类型：
  - r 代表读
  - w 代表写
  - x 代表执行

- 更改所应用的文件或目录





示例 3-18 演示了使用符号的 chmod 命令。

## 示例 3-18 chmod 命令的符号模式

```
lnxken:"~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rw-r-x--- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures # chmod g-x smilepic
lnxken:"~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rw-r----- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures # chmod go+rw smilepic
lnxken:"~/Desktop/MyDocs/MyPictures # ls -l
total 8
-rw-rw-rw- 1 root root 83 May 19 17:20 smilepic
-rw-r--r-- 1 root root 83 May 19 17:18 smilepic.bak
lnxken:"~/Desktop/MyDocs/MyPictures #
```

## 3.2.4 作业控制

因为 Linux 是一个多任务操作系统，用户可以同时运行多个作业或进程。要查看正在运行的作业列表，请使用 `jobs` 命令。要同时查看每个正在运行的作业的进程号，请使用 `jobs -p` 命令，它会给出每个正在运行的作业的进程号。

要查看您拥有的所有正在运行的进程的列表，请使用 `ps` 命令。要查看所有正在运行的进程，请使用 `ps -e` 命令。

> 注意：词语“作业”和“进程”可以互换使用。

### 在后台运行作业

虽然大多数命令执行得很快，但如果您知道某个命令需要更多时间，您可以输入以下内容暂时将作业挂起到后台：

```
CTRL -z
```

现在您可以执行其他命令。要返回到您挂起到后台的原始作业，请输入以下命令之一：

- `fg %jobname` 将进程带到前台（执行），但保持 shell。
- `bg %jobnumber` 将进程发送到后台。

### 结束作业

如果要取消作业，请输入以下 kill 命令之一：

```
kill jobnumber
```

```
kill jobname
```

使用 `kill` 命令，您可以指定一个数字，该数字是一个级别，指示您希望如何终止进程。格式如下：

```
kill -n jobnumber/jobname
```

`n` 是级别数字。数字 9 是最高级别，立即结束作业。数字 15 允许作业在终止前进行清理。使用 `man` 命令获取有关 `kill` 命令的更多信息。

## 3.2.5 Linux vi 编辑器

Linux vi 编辑器是每个 Linux 发行版中都包含的文本编辑工具。本节通过描述 vi 的三种操作模式以及如何在模式之间切换来介绍 vi 编辑器，并介绍基本的 vi 命令。

### 操作模式

vi 编辑器在三种模式下运行：

- 命令模式：在此模式下输入命令。
- 插入模式：在光标位置插入字符。
- 替换模式：覆盖光标位置的字符。

要在模式之间切换：

- 从命令模式切换到插入模式，按以下单个键之一，但不要按 Enter：

```
i, I, a, A, o, O
```

> 注意：键入单个字符会立即将 vi 切换到插入模式。不要在此之后按 Enter 键，否则会被当作插入模式下的输入。

- 从命令模式切换到替换模式，按 R（同样，不要按 Enter）。
- 从替换或插入模式切换到命令模式，按 Esc。

图 3-5 说明了 vi 运行的三种模式以及您必须在模式之间切换时按下的键。

![](img/b0a4b9056f819dccd4781a5105c92d45_131_0.png)

图 3-5 vi 操作模式

vi 窗口的左下角指示您正在使用哪种操作模式（如果您处于命令模式，该区域为空白）：

- -- REPLACE --
- -- INSERT --

通常，vi 以命令模式启动。在您输入第一个文本之前，文件名显示在初始窗口的左下角。

各种实用程序（如 PuTTY¹，一个适用于 Windows 和 UNIX 平台的免费 Telnet 和安全外壳（SSH）客户端）使 vi 更易于使用。例如，使用 PuTTY，您可以从其他两种模式切换到插入模式。Insert 键也可以将您从插入模式切换到替换模式。

### vi 编辑器的命令

本节列出了最常用的 vi 命令。

### 在 vi 编辑器中导航

用于在编辑器中移动光标的命令列于表 3-4 中。

表 3-4 在 vi 编辑器中导航

| 命令 | 描述 |
|---|---|
| 0 | 将光标移动到当前行的开头。 |
| $ | 将光标移动到当前行的末尾。 |
| Enter | 将光标移动到下一行的开头。 |
| w | 将光标移动到下一个单词的开头。 |





| 命令 | 描述 |
|---|---|
| :i ,j d | 删除从行号 i 直到（包括）行号 j 的行。 |
| :1 , . d | 删除文件的第一行直到（包括）当前行。点号 (.) 指当前行。 |
| :. , $ d | 删除当前行直到（包括）文件的最后一行。点号 (.) 指当前行。$ 指最后一行。 |

## 移动和复制

移动和复制的命令列在表 3-7 中。

表 3-7 vi 移动和复制命令

| 命令 | 描述 |
|---|---|
| :i mj | 移动行 i，插入到行 j 之后。 |
| :i ,j mk | 移动行号 i 到 j（包含），插入到行 k 之后。 |
| :i coj | 复制行号 i，插入到行 j 之后。 |
| :i ,j cok | 复制行号 i 到 j（包含），插入到行 k 之后。 |

## 替换字符

替换字符的命令列在表 3-8 中。

表 3-8 vi 替换命令

| 命令 | 描述 |
|---|---|
| rc | 用 c 替换当前字符。 |
| :s/ppp/qqq/ | 在当前行中，将模式 ppp 的第一次出现替换为 qqq。 |
| :s/ppp/qqq/g | 在当前行中，将模式 ppp 的所有出现替换为 qqq。 |

> 重要提示：在 vi 中，单词由空格和任何不是数字也不是字母的字符分隔。

## 定位字符串模式

定位特定字符串模式的命令列在表 3-9 中。

表 3-9 vi 定位字符串模式

| 命令 | 描述 |
|---|---|
| /xxx <Enter> | 查找模式 xxx。 |
| / <Enter> | 查找上一个 /xxx 命令的模式 xxx。 |
| ?xxx <Enter> | 查找模式 xxx（搜索方向反向，向上查找） |
| ? <Enter> | 查找上一个 /xxx 或 ?xxx 命令的模式 xxx。 |

> 注意：您可以在字符串模式中使用正则表达式。例如 [0-9] 表示任意数字，[a,e,i,o,u] 表示任意元音。

## 杂项 vi 命令

杂项 vi 命令列在表 3-10 中。

表 3-10 vi 杂项命令

| 命令 | 描述 |
|---|---|
| j | 跳到行 j（光标位于该行开头）。 |
| u | 撤销当前行最近的更改。 |
| U | 将当前行恢复到首次访问时的状态。 |
| xp | 将当前字符与其下一个字符互换。 |
| ddp | 将当前行与下一行交换。 |
| ~ | 切换当前字符的大小写。 |
| n~ | 切换 n 个连续字符的大小写。 |
| :help ccc | 获取有关命令（ccc）的信息。 |

> 注意：xp（转置）命令通过交换两个连续字符的顺序来纠正大量输入错误。

> 在区分大小写的编程语言中，如 Java 和 C，许多错误与大小写错误有关。~（波浪号）命令可以纠正此问题。

## 保存和关闭文件

保存和关闭文件的命令列在表 3-11 中。

表 3-11 vi 保存和关闭命令

| 命令 | 描述 |
|:---|:---|
| :w | 写入文件（保存它）。 |
| :q | 退出 vi 会话。 |
| :!q | 不保存退出。 |
| :wq | 先保存，然后退出。 |

## 3.3 进一步探索

有关 vi 编辑器的更多信息，请学习系统上提供的教程。将 /usr/bin 目录（或根据安装情况的其他目录）中的文件 vimtutor 复制到您的主目录。然后，从主目录执行 vimtutor 命令。教程还包含练习，帮助您练习使用命令。（vi 的增强版本是 vim。）

有关通用 Linux 信息，请参阅 Linux Handbook A Guide to IBM Linux Solutions and Resources，SG24-7000。

以下 IBM 网站提供有关 Linux 的信息：

- z/VM resources for Linux on IBM System z
  http://www.vm.ibm.com/linux/
- Linux on IBM System z
  http://www.ibm.com/servers/eserver/zseries/os/linux/
- System z mainframe
  http://www.ibm.com/servers/eserver/zseries/





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





+   2. 使用可执行的 INSTDVD 执行 z/VM 的主要安装。
+   3. 从新安装的磁盘执行 IPL 并运行可执行的 INSTVM 以完成安装。

此方法提供了一个全面的对话框和稳定的安装环境。

## **z/VM 安装后剩余的活动**

通常，z/VM 的交付会附带一个推荐服务升级（RSU）磁带或 DVD。初始安装完成后应进行安装。它是从 z/VM 内部使用可执行文件 SERVICE 和 PUT2PROD 进行安装的。有关这些主题的讨论，请参阅第 9 章“应用系统维护”第 387 页。

## **磁盘注意事项**

请注意，如果您有重复的卷，z/VM 会使用位于最低设备号上的卷，而不给您选择权。这与 z/OS 相反，z/OS 会给您将设备脱机的选项。

> **重要：** 避免出现重复，并为磁盘卷标签建立合适的标准。

## **4.2 z/VM 安装概念和注意事项**

在进行 z/VM 安装之前，本节提供了在整个安装过程中使用的概念。在阅读 4.3“在 LPAR 中安装 z/VM”第 138 页之前，请先熟悉这些概念。这些概念可以帮助您将 z/VM 安装及其所需配置与典型的 z/OS 安装和配置进行比较。

### **4.2.1 与 z/VM 交互**

在与系统交互方面，z/OS 和 z/VM 之间确实存在差异。

熟悉 z/OS 的用户通常登录到系统并使用 ISPF 会话与系统交互¹。系统交互是菜单驱动的，即

> ¹ 为本书的目的，我们假设大多数 z/OS 用户是通过使用 ISPF 而不是原生 TSO 与其交互。

用户通过菜单导航到特定的系统功能或要执行的命令。

另一方面，z/VM 用户通过对话监视系统（CMS）与系统交互，CMS 是一种命令行界面²，如下节所述。

### CMS

在典型的 z/VM 安装中，CMS 是用户登录后 IPL 的代码。它旨在促进大型机虚拟机管理。在其中，您可以发出命令来编辑、创建、删除和管理文件，以及执行程序和脚本。用一个简单的类比来说，CMS 允许您执行与在 Linux 控制台上执行的基本相同的一组任务。图 4-1 说明了 3270 会话显示用户 MAINT 登录时的 CMS。CMS 的概述位于第 2.5 节“对话监视系统（CMS）”第 35 页。

图 4-1 中描绘了 CMS 界面。请注意 CMS 看起来与 Linux 控制台会话有多么相似。大多数用户熟悉使用控制台会话的概念；与 CMS 交互并没有太大不同。

```
LOGON MAINT
ENTER PASSWORD  (IT WILL NOT APPEAR WHEN TYPED):

z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsgs data
FILES: 0098 RDR,  NO PRT,  NO PUN
LOGON AT 14:35:40 EDT FRIDAY 05/09/08
z/VM V5.3.0   2008-05-06 13:40

                                      VM READ  VMLINUX6
```

![](img/b0a4b9056f819dccd4781a5105c92d45_140_0.png)

您应该熟悉如何使用 CMS 帮助菜单。请阅读第 2.5.1 节“CMS 中 HELP 命令概述”第 36 页，了解该主题的介绍。

以下列表包含您最有可能用来查找、复制和编辑文件的命令：

- FILELIST

使用此命令在 z/VM 中列出文件，从 CMS 开始。z/OS 用户通常通过菜单界面 ISPF 来执行此操作。有关此命令的详细信息，请参阅第 75 页“COPYfile 命令”。

- ► COPYFILE

使用此命令创建您将编辑的配置文件备份副本。此命令的语法在第 75 页“COPYFILE 命令”中。

- ► XEDIT

在 CMS 中编辑文件的两种方法是：

– 当您已经知道文件名及其位置时。

这是直接的场景。要编辑您在 A 磁盘上的名为 PROFILE EXEC 的文件，请在 CMS 命令行上键入以下内容：

```
xedit profile exec a
```

– 当您不知道文件名是什么，或不知道其位置，或两者都不知道时。

在这种情况下，您使用 FILELIST 命令搜索要编辑的文件以查看文件列表。然后，将光标放在要编辑的文件对应的行上，并按 F11。

尽管在整个安装过程中，您将使用这三个命令来操作文件，但请花几分钟时间查看第 2.8.2 节“CMS”第 72 页，了解其他命令。此外，请阅读书籍《Introduction to the New Mainframe: z/VM Basics, SG24-7316》的相应章节，以熟悉 z/VM 命令。

### **4.2.2 系统文件**

与每个系统一样，z/VM 也有配置文件。它们用于为用户定义迷你磁盘、定义虚拟资源（如虚拟交换机）、为 CMS 和 XEDIT 会话定义配置文件等等。本节描述以下文件：

- USER DIRECT
- SYSTEM CONFIG
- PROFILE EXEC
- PROFILE XEDIT

您将在安装过程中学习如何访问和修改这些文件。





z/OS 类比：这里讨论的配置文件是 z/VM 中 z/OS SYS1.PARMLIB 串联、用户 RACF 定义以及从登录过程 JCL 调用的初始 TSO/ISPF 例程的 z/VM 对应物

## USER DIRECT 文件

这是处理用户及其微磁盘、DASD 空间分配定义以及用户可导入其用户设置中的通用配置文件定义的 z/VM 配置文件。这些配置文件除其他用途外，还用于创建每个用户输入、输出和打印文件所需的诸如阅读器、打孔机和打印排队程序等基本设备，以及创建到其他用户磁盘的链接，特别是到 MAINT 用户某些磁盘的链接，以便在不复制到其微磁盘的情况下访问关键只读代码，例如 CMS。该文件位于 MAINT 的 2CC 磁盘上。

## SYSTEM CONFIG 文件

该文件保存系统的绝大部分配置。在此文件中设置哪些 DASD 卷将由系统拥有，例如专用于分页的卷，以及哪些卷由用户拥有，例如托管 Linux 虚拟机的卷。它还用于设置虚拟资源，例如用于为 Linux VM 提供网络服务的虚拟交换机，以及限制分配给普通用户的资源量，例如每个用户可能拥有的微磁盘数量。该文件位于 MAINT 的 CF1 磁盘上。

## PROFILE EXEC 文件

PROFILE EXEC 与其他可执行文件（也称为 execs）不同。它具有特殊的 文件名 PROFILE，并且在您进入 IPL CMS 时会自动处理（或如果您有自动 IPL 机制）。

您的 PROFILE EXEC 包含您在每次终端会话开始时输入的 CP 和 CMS 命令。它可用于为每个 CMS 用户设置特殊特性，超出该用户目录条目中定义的特性，例如：

- 使虚拟机配置中的任何非标准微磁盘或共享文件系统为 CMS 所知
- 更改在终端上显示数据的颜色（仅限彩色终端）
- 使经常使用的 execs 驻留在存储器中
- 为常用命令设置多达 24 个程序功能键
- 更改 CMS 发送的就绪消息
- 自动检查您的虚拟卡阅读器（您的收件盘）中的文件和消息
- 直接将您带到应用程序实例

每个 z/VM 用户都有自己的 PROFILE EXEC 文件。这类似于 Linux 的 .bashrc 文件，以及 z/OS 初始登录例程（REXX 或 CLIST 脚本），它们是安装自定义而不是标准 z/OS TSO 登录的一部分。每次用户登录时，此文件都会被访问，其中的任何特殊配置和命令都会被设置或运行。保持用户之间的配置文件一致是确保登录到不同用户账户时具有统一外观和感觉的良好做法。此文件位于每个 z/VM 用户的 191 磁盘上。

## PROFILE XEDIT 文件

这是 XEDIT 编辑器的配置文件，每次用户调用它时都会被访问。如您在第 91 页的“自定义 XEDIT”中所见，对此文件的良好自定义对于更好地使用 XEDIT 体验至关重要。此文件类似于 Linux 中 vi 编辑器的 .vimrc 文件。在 z/OS 中，这类似于在 ISPCFG 模块中设置的配置文件设置。此文件位于每个 z/VM 用户的 191 磁盘上。

## 4.2.3 重要的 z/VM 安装用户 ID

与每个系统一样，一些用户账户具有特殊含义。本节概述了在 z/VM 安装中使用的这些账户，并与 z/OS 和 Linux 进行了比较。用户账户为：

- MAINT 用户
- AUTOLOG1 用户
- TCPIP 用户

### MAINT 用户

这是 z/VM 的超级用户。它类似于具有通过 RACF 访问系统特权信息的 z/OS 用户。它也类似于 Linux root 用户。

该 z/VM 用户可访问 6.1.5“z/VM 特权类”第 287 页中提到的所有特权类。因此，它被授予访问系统的所有配置文件和管理命令的权限，例如授予用户访问虚拟交换机的权限。

### AUTOLOG1 用户

这是 z/VM 中的一个特殊用户，在 z/OS 或 Linux 中都没有可比较的用户。Linux 中最接近的概念是运行级别，它们负责在启动期间启动服务。

在 z/VM IPL 后立即自动运行命令或脚本是通过 AUTOLOG1 用户实现的。如 2.2.1“历史”中所述


z/VM" 第 14 页所述，z/VM 用户的概念映射到一台虚拟机。因此，AUTOLOG1 虚拟机负责在 z/VM IPL 完成后立即启动其他虚拟机（为其他用户登录）。这通常是为了启动 TCP/IP 虚拟机，例如。

> 注意：如果在加载 z/VM（IPL）时未指定 noautolog 参数，则会启动 AUTOLOG1 虚拟机。因为该虚拟机 IPL 了 CMS，所以会运行其 A 磁盘上找到的 PROFILE EXEC。这类似于 Linux 上的 /etc/profile 文件和 DOS 系统上的 autoexec.bat 文件。

> z/OS 类比：z/VM AUTOLOG1 用户执行的任务类似于在 SYS1.PARMLIB 串联中使用 START 语句在成员 IEACMDxx 和 COMMNDxx 中使用

## The TCPIP user

在 z/OS 中，TCP/IP 堆栈由 z/OS Communications Server 在单独的地址空间中管理。而在 z/VM 中，堆栈由一台虚拟机管理：TCPIP 虚拟机（定义为 TCPIP 用户）。

## 4.2.4 Dealing with disks

当 z/VM 用户登录系统时，CMS 中运行一个文件层次结构。它与 Linux 或 z/OS 使用的层次结构不同。事实上，CMS 中没有层次结构，但它确实具有文件名、文件类型和文件模式的三元组概念。每个文件名都由这三个组件构成，描述如下。您可以将此文件系统视为一个平面文件系统（或顺序文件系统），其中只有一层。

- 第一个参数，文件名，对大多数用户来说应该很熟悉，因为它只是文件的名称。在 CMS 中，文件名长度限制为八个字符，且不区分大小写。
- 第二个参数，文件类型，类似于 Linux 等系统的文件扩展名。在 CMS 中，文件类型也限制为 8 个字符长，且不区分大小写。按类比，文件名和文件类型一起形成类似于 z/OS filename.extension 文件命名约定的东西（它们之间用空格而不是点分隔）。
- 第三个参数，文件模式，指定文件的位置，即它驻留在哪个磁盘映射上。文件模式长度为一个字符，限制为字符 A-Z。文件模式使得整个文件系统成为一个平面宇宙，因为您最多只能有 26 个同时存放文件的地点。

我们在上一段中提到了映射这个词，但在谈论将磁盘映射到文件模式之前，我们应该讨论磁盘是如何组织的。磁盘只不过是存储空间。它们保存文件，文件通过其名称和类型来标识。然而，与 Linux 等系统不同，磁盘不是通过设备名称标识，而是通过设备 ID 标识。其中一些 ID 是众所周知的 ID，例如 MAINT 的 193 磁盘，其中包含有用的程序，如 CPSYNTAX。

磁盘 ID 类似于 Windows 等系统中的模板目录名。例如，两个 z/VM 用户可以拥有标有 191 的磁盘。将其视为两个不同用户在 Windows 中可以拥有的“我的文档”文件夹。两个文件夹都有相同的名称“我的文档”，但每个都属于不同的用户，并且各自表示磁盘存储中的不同区域。这里唯一的区别是，您在 CMS 中使用数字而不是名称来表示永久存储区域，即磁盘。对于 z/OS，每个 TSO/ISPF 用户在其自己的高层限定符下都有一个单独的 ISPF.PROFILE 文件。

话虽如此，我们进一步探讨磁盘的几个有趣方面。例如，如果您想访问 CPSYNTAX 命令并且未以 MAINT 登录，您可以将 MAINT 的 193 磁盘链接到您的用户空间以能够访问该命令。您通过使用 LINK 和 ACCESS 命令（或其缩写：acc）来执行此操作。

### Accessing another user’s disk (linking)

将另一个用户的磁盘链接到您的用户空间的命令序列如示例 4-1 所示。

Example 4-1 Linking and accessing disks

```
link autolog1 191 1191 rr
Ready; T=0.01/0.01 16:02:04
acc 1191 f
DMSACP723I F (1191) R/0
Ready; T=0.01/0.01 16:02:08
```

示例中显示的 LINK 命令将用户 AUTOLOG1 的磁盘 191 链接到我们的用户空间下，标签为 1191，模式为只读。这意味着我们实际上可以通过引用我们自己的已链接 1191 来访问 AUTOLOG1 的 191 磁盘上的文件。但是，要执行此操作，我们仍必须将 1191 磁盘映射到一个文件模式，以便我们可以使用三元组（文件名、文件类型、文件模式）来访问其上的文件。将磁盘映射到文件模式是我们使用 ACCESS 命令³ 执行的操作。我们将 1191 磁盘映射到我们拥有的一个未使用的文件模式

> ³ 在 z/VM 中，按我们定义的术语，映射磁盘实际上称为访问磁盘。我们在这里使用“映射”这个词是为了让不熟悉 z/VM 的人更容易理解类比。从现在开始，我们将磁盘映射称为访问磁盘。





可用，在本例中为 F。图 4-2 显示了我们刚刚执行的操作。

## 图 4-2 访问其他用户的磁盘。

![](img/b0a4b9056f819dccd4781a5105c92d45_146_0.png)

为了检查 AUTOLOG01 的 191 磁盘是否已链接并映射到我们的用户空间，我们可以运行 QUERY DISK 并检查是否存在我们新映射的 F 文件模式的条目。该命令的输出如图 4-3 第 132 页所示。请注意，F 文件模式是我们 ID 为 1191 的虚拟磁盘，其标签为 AUT191，正如我们所期望的那样。

> 注意：如果您尝试链接到另一个用户的磁盘，并且您未以 MAINT 身份登录，您可能需要为链接磁盘的访问模式（读、写）输入密码。有关访问模式的更多详细信息，请参阅第 134 页的“创建磁盘”。

4 QUERY 命令的缩写为 Q。

```
LOGON MAINT
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0113 RDR,  NO PRT,  NO PUN
LOGON AT 09:31:14 EDT TUESDAY 05/13/08
z/VM V5.3.0  2008-05-06 13:40
link autolog1 191 1191 rr
Ready; T=0.01/0.01 09:32:11
Ready; T=0.01/0.01 09:32:11
acc 1191 f
DMSACP7231 F (1191) R/O
Ready; T=0.01/0.01 09:32:20
query disk
LABEL VDEV M STAT CYL TYPE BLKSZ FILES BLKS USED-(%) BLKS LEFT BLK
TOTAL
MNT191 191  A R/W 175 3390 4096 10 28-01 31472 31500
MNT5E5 5E5  B R/W 9 3390 4096 131 1288-80 332 1620
MNT2CC 2CC  C R/W 5 3390 4096 54 434-48 466 900
MNT5ID 5ID  D R/W 26 3390 4096 273 1245-27 3435 4680
AUT191 1191 F R/O 1 3390 4096 2 9-05 171 180
MNT190 190  S R/O 100 3390 4096 687 14592-81 3408 18000
MNT19E 19E  Y/S R/O 250 3390 4096 1010 26738-59 18262 45000
Ready; T=0.01/0.01 09:32:23

RUNNING   VMLINUX6
```

图 4-3 检查磁盘是否已链接和映射

类 AIX 系统的用户可以将链接和访问视为软链接到另一个用户的目录。这自然会带来将文件模式视为映射到我们扁平 CMS 文件系统的目录的想法。对于认为在 z/VM 中没有目录会很难的读者，您会看到您可以同时管理 26 个不同的目录。只需记住，其中每一个目录实际上都是一个磁盘。

要从您的用户空间释放已链接的磁盘，请使用 RELEASE 命令（或其缩写形式：REL）。要释放我们刚刚访问的 F 磁盘，请使用 RELEASE F 命令。

## 磁盘访问约定

现在您已经了解了磁盘访问的基本概念，本节描述了与磁盘访问相关的几个约定。

A CMS 用户通常至少有两个可用磁盘（可能是稍后讨论的 minidisk）。通常，使用 CMS 的用户有一对虚拟磁盘，其地址为 191 和 190：

- 191 磁盘通常以模式 A 访问。
- 190 磁盘作为 S 访问。190 minidisk 有时被称为 CMS 系统驻留卷，因为 CMS 核就驻留在该磁盘上。

## 您的 A 磁盘

CMS 假定您在地址 190、191 和 19E 有磁盘。它还确定您是否在地址 192 有磁盘。当 CMS 加载时，这些磁盘按如下方式访问：

- 191 成为 A 磁盘
- 192 成为 D 磁盘（如果存在）
- 190 成为 S 磁盘
- 19E 成为 Y/S 磁盘

这仅在您的用户拥有虚拟地址为 191 的 DASD 时才成功。A 磁盘是用户永久文件存储的工作磁盘。一般来说，CMS 用户的 A 磁盘是他们唯一可写的磁盘。这类似于在为用户分配 DASD 空间的系统中用户的 home 目录。

A 磁盘非常重要，因为当 CMS 加载时，它会在您的 A 磁盘上查找名为 PROFILE EXEC 的文件并尝试执行该文件。

PROFILE EXEC 通常会被修改以根据用户自定义 CMS 实例，甚至加载另一个操作系统，如 Linux。

## 空间用尽

每个虚拟磁盘都分为通常大小为 4096 字节的块（尽管某些磁盘，如帮助磁盘，使用较小的块以节省因其上大量小文件而浪费的磁盘空间）。

每个文件的最小大小为一个块。最大大小受 minidisk 大小的限制。每个用户通常可以读取访问多个此类磁盘。但通常，用户在没有剩余空间写入自己的文件时会遇到问题。





USER DIRECT  C1 F 80  Trunc=72 Size=2041 Line=1967 Col=1 Alt=0

01967
****************************************************************
01968 USER CERON CERON  32M 64M G
01969 INCLUDE IBMDFLT
01970 ACCOUNT ACT4 CMSTST
01971 MACH XA
01972 IPL 190
01973 MDISK 191 3390 2040 010 LX6W02  MR READ  WRITE  MULTIPLE
01974 *
01975
****************************************************************
===>

图 4-4 通用用户的磁盘定义

文件中的第一行，第 1968 行，定义了用户 CERON 并将其密码设为同样为 CERON。虽然创建简单密码不是一个好的做法，但为了本书中的示例，我们将密码设为与用户名相同。两个参数 32M 和 64M 表示该用户虚拟机将使用的系统存储（主内存）的初始量和最大量。该行末尾的 G 表示该用户将拥有的类权限，在本例中为最低可能级别。创建用户在第 183 页的“创建 Linux MAINT 用户”中进行了讨论。

第二行，第 1969 行，将一个名为 IBMDFLT 的默认配置文件添加到用户定义中。稍后，如果你查看 USER DIRECT 文件的开头，你会注意到该配置文件将 MAINT 的一些磁盘链接到该用户的空间中。例如，它以只读模式将 MAINT 的 190 磁盘链接到其自己的 190 磁盘。这允许该用户在登录时加载（IPL）CMS。

第 1973 行显示了该用户的 minidisk 定义。它定义了该用户的 191 磁盘，在标记为 LX6W02 的 3390-3 型 DASD 上从柱面 2040 开始，大小为 10 个柱面，采用多读模式。此外，它定义了三个密码，READ、WRITE 和 MULTIPLE，供希望分别以读、写和读写模式链接到该磁盘的用户使用。

在为给定用户插入磁盘定义后，更改不会生效，直到你告诉系统执行它们。为此，使用 DIRECTXA USER 命令，但在实际提交更改之前，先检查 minidisks 的布局是否存在间隙和重叠，这是一个良好的做法。要检查更改，请运行 DISKMAP USER，它会在你的 A 文件模式中创建一个名为 USER DISKMAP 的文件。然后，查找新的用户 minidisk 定义。图 4-5 显示了该文件中与我们新创建用户相关的行。

USER  DISKMAP A1 F 80 Trunc=80 Size=382 Line=231 Col=1 Alt=0
00231
00232 VOLUME USERID CUU DEVTYPE START END SIZE
00233 LX6W02 $ALLOC$ A03 3390 00000 00000 00001
00234 40SASF40 2D2 3390 00001 00150 00150
00235 OSADMIN2 191 3390 00151 00160 00010
00236 OSADMIN3 191 3390 00161 00170 00010
<...snap...>
00318 COSTA 191 3390 01806 01815 00010
00319 HAIMO 191 3390 01816 01825 00010
00320 1826 1999 174 GAP
00321 GUILL 191 3390 02000 02009 00010
00322 OMAR 191 3390 02010 02019 00010
00323 RAY 191 3390 02020 02029 00010
00324 KEN 191 3390 02030 02039 00010
00325 CERON 191 3390 02040 02049 00010
====>

图 4-5 检查 DASD 布局是否存在间隙和重叠

请注意图 4-5 中，第 00320 行（加粗）显示了一个从柱面 1826 开始、运行到柱面 1999 的间隙，共计 174 个柱面。虽然你应尽量避免间隙以防止碎片化，但它们是无害的。第二条加粗行（00325）显示了新创建的用户；它与周围的任何 minidisks 定义之间不存在重叠。检查后，我们必须运行 DIRECTXA USER 才能使更改生效。

## 格式化 minidisk

创建新用户后，其所有者应格式化其分配的 minidisk 空间，以便为该磁盘创建文件。这是通过用户登录后运行 FORMAT 命令实现的：

```
format 191 a
```

该命令格式化用户的 191 磁盘并将其用作 A 文件模式。参见第 137 页的图 4-6

6 间隙只会在 minidisks 之间留下空磁盘空间，但重叠是指一个 minidisk 定义重叠到后续的 minidisks；z/VM 实际上允许这种重叠。





LOGON GUILL
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: NO RDR, NO PRT, NO PUN
LOGON AT 12:28:57 EDT TUESDAY 05/13/08
z/VM V5.3.0 2008-05-06 13:40

format 191 a
DMSFOR603R FORMAT will erase all files on disk A(191). Do you wish to continue?
Enter 1 (YES) or 0 (NO).
1
DMSFOR605R Enter disk label:
gui191
DMSFOR733I Formatting disk A
DMSFOR732I 10 cylinders formatted on A(191)
Ready; T=0.01/0.01 13:14:27

RUNNING VMLINUX6

Figure 4-6 Formatting a minidisk

Note: When you log on to your user account for the first time, your 191 disk (the A disk) will probably not have been formatted. You can check whether you have a suitably formatted A disk by executing the command FILELISTa. If you see a file listing after executing the FILELIST command, then it has already been formatted.

However, if you receive the following error message, you might have to format your 191 disk before continuing:
HCPCMD001E Unknown CP command: FILELIST

If this is the case, use the command FORMAT 191 A to place a VM readable file system on your A disk.

- a. The abbreviated form for the FILELIST command is FILEL.

## 4.3 Installing z/VM in an LPAR

This section discusses installation of z/VM in an LPAR. For more detailed installation instructions, see:

http://www.vm.ibm.com/install/vm53inst.pdf

### 4.3.1 Planning

Before starting the z/VM and Linux installations, plan carefully to make sure you have the following required resources:

- Hardware
- Software
- Networking

Planning also involves considerations for passwords, disks, memory, and for creating a resources worksheet.

### Hardware resources

The following hardware is required:

- A System z logical partition (LPAR); z800, z900, z890 or z990, System z9® or System z10:
  - Processors or CPUs: One IFL (or CP) minimum, two or more are strongly recommended. In Systems z9 and earlier systems you are not able to mix general CPUs and IFLs.
  - Memory: 3 GB central with 1 GB expanded minimum, 6 GB with 2 GB or more recommended. This 3:1 ratio of central to expanded storage is a good starting point for all systems except the very largest systems.
  - See the following Web site for a discussion of how to apportion memory:
    http://www.vm.ibm.com/perf/tips/storconf.html
  - DASD: twelve 3390-3 or five 3390-9 at a minimum
  - Open Systems Adapter (OSA) network cards: One card minimum with eight device numbers (technically six, but OSA triplets usually start on an even address). Two OSA Express cards with eight device numbers on one card, and four on the other is recommended for high availability.
- A network-attached computer that can act as a file server of Linux distributions with at least 3 GB of disk space plus 6 GB for each Linux distribution that you intend to serve, although more might be needed.

Setting up a server is *not* described in this book, however we reference helpful publications in the following section, “Software resources” on page 139.

- A workstation or desktop that has network access to the mainframe

### Software resources

The following software resources are required:

- z/VM 5.3 installation media with documentation (installation from DVD is described in this book).
- Linux installation media (SLES or RHEL)
- An operating system for the file server
  - You can easily set up a file server by using an existing Linux environment. The *z/VM and Linux on IBM System z: The Virtualization Cookbook for SLES9*, SG24-6695 book has instructions for setting up an NFS server.
  - Additional options to an NFS server are HTTP or FTP, served on the Apache web server or on usual FTP servers found on Linux distributions. Instructions for setting up Apache are at the following Web site:
    - http://www.apache.org
- The code associated with this book
- Tools on the workstation and desktop:
  - A 3270 Emulator such as Attachmate Extra, Hummingbird Host Explorer, or IBM Personal Communications for Windows desktops (for Linux desktops, a 3270 emulator named *x3270* is available)
  - A Linux SSH client such as PuTTY (recommended) or TeraTerm (for Linux desktops the SSH client is built in)
- A VNC viewer

### Networking resources

The following network resources are required:

- A TCP/IP address for z/VM
- One TCP/IP address for each z/OS, z/VM or Linux guest operating system
- Associated TCP/IP information:
  - DNS host name
  - DNS domain
  - DNS server TCP/IP address
  - TCP/IP gateway
  - TCP/IP subnet mask





## 磁盘规划

在规划阶段，选择和分配磁盘存储时，请考虑以下方面：

- 传统 ECKD™ DASD 与通过 SCSI/FCP 的 FBA 磁盘
- 3390-3 与 3390-9 或大磁盘支持
- 每个 Linux 映像的磁盘存储量以及如何分配文件系统

### DASD 与 SCSI/FCP

本书描述了如何使用传统 ECKD DASD，并未讨论通过 SCSI/FCP 访问的 FBA 磁盘。其原因并非任一技术更优越，而是 DASD 看起来比 SCSI/FCP 磁盘更常见。有时，会使用这两种类型的磁盘存储的组合。在这种情况下，ECKD 仿真 DASD 通常用于根文件系统，而 SCSI/FCP 磁盘用于大型数据存储区。

### 3390-3 与 3390-9

仿真 3390-3 格式约为 2.3 GB，而 3390-9 格式是其三倍大小，约为 6.8 GB。两种大小都可以使用，尽管一些性能分析师建议使用 3390-3 而非 3390-9。本书主要描述使用 3390-3，然而，在使用 3390-9 时存在差异时，我们添加了注释，尤其是在安装 z/VM 时。

### 每个 Linux 映像的磁盘存储

为了将图形环境（K 桌面环境）安装到我们的 Linux 客户机中，并且保留大量空闲空间用于通用任务（作者希望随意尝试），我们决定为客户机使用约 10 GB 的存储空间。您为 Linux on z/VM 的特定目标所需的空间量可能会有所不同，但对于任何 Linux 安装，建议根分区（/）至少为 3 GB 至 4 GB，因为有了额外空间，您可以很容易地从最小软件包集扩展到完整的软件包集安装。

在我们的示例中，为 Linux 映像分配了五个 3390-3，每个包含 3339 个柱面。经常会建议创建许多文件系统，将其挂载到根文件系统本身（/）之外的目录上，例如 /usr/、/var/、/tmp/、/home/、/opt/ 等。我们并非对所有示例都这样做，因为：

- 我们并未针对任何特定用途优化安装。有关优化 Linux 分区的更多信息，请阅读 *Linux Performance and Tuning Guidelines*，REDP-4285。
- 我们最初仅有 10 GB 可用于安装，而在如此少的空间下进行存储隔离可能会导致过多的微小分区，很快就会使系统变得无用。

拥有许多挂载文件系统的常见论点是为了防止根文件系统填满，导致系统停止。例如，在生产环境中，如果 Linux 客户机充当文件服务器，远程攻击可能导致 /var 中的日志消耗其所在分区的全部空间。如果 /var 与根分区（/）位于同一分区上，这可能会使系统停止。

> 注意：制定良好的分区计划是拥有优化且可靠的 Linux 客户机的第一步。

## 内存规划

规划内存可能是 Linux on System z 和 z/VM 上最困难的问题，但也是确保足够性能最重要的因素。最简单的解决方案似乎是让 LPAR 中拥有足够的中央内存（存储），以便 z/VM 从不分页且 Linux 从不交换。然而，这种资源通常在现实中不可用。一个好的经验法则是按每个 Linux 服务器的刚好足够原则分配内存。一个好的起点是设置虚拟机大小，通过在正常负载下更改内存分配值，使其略高于客户机在 Linux 系统级别开始交换的值。如果由于工作负载的性质而不可避免地出现一定程度的持续交换，则确保虚拟磁盘用于交换介质。

理解内存规划绝对是推荐的。以下书籍讨论了这个非常重要的话题：

- 书籍 Linux on IBM System z: Performance Measurement and Tuning，SG24-6926 在网页上：http://www.redbooks.ibm.com/redpieces/abstracts/sg246926.html?open
- 一般来说，IBM z/VM Performance Resource 页面，网页上：http://www.vm.ibm.com/perf/
- Configuring Processor Storage，网址：http://www.vm.ibm.com/perf/tips/storconf.html

一个可以推荐的规则是，只让尽可能少的虚拟机登录（或断开连接）来处理工作负载。应适当注销所有不需要的虚拟机。其结果是为其他仍在运行的虚拟服务器提供更多内存。




我们在示例中使用Linux客户机，为其分配512MB的初始存储空间，外加1.5GB的扩展存储空间（用于Linux交换空间）。对于本书而言，这已经绰绰有余。

## 规划工作表

本节提供了一个工作表，其中列出了本章所有示例中使用的资源值。请参见表4-1。在您创建自己的规划工作表时，请参考此工作表，参见附录B“规划工作表”（第403页）。

注意：在本书中，所有运行需要资源信息的命令的示例，都使用尖括号（<>）括起资源值。当您在您的系统上运行这些命令时，请务必将示例中的值替换为您自己的资源。

表4-1 z/VM资源工作表

| 名称 | 值 | 备注 |
|---|---|---|
| LPAR名称 | VMLINUX6 | 存储：4 GB + 2 GB 扩展<br>处理器：4<br>DASD：11个3390-3磁盘 |
| CPC名称 | SCZP201 | LPAR所在的CPC的名称 |
| z/VM系统名称 | VMLINUX6 | 分配给z/VM系统的名称 |
| TCP/IP主机名 | vmlinux6 | 由网络管理员分配；建议提前在DNS中设置，但不是必需的 |
| TCP/IP域名 | itso.ibm.com | 建议提前在DNS中设置 |
| TCP/IP网关 | 9.12.4.1 | 与本地子网通信的路由器 |
| DNS服务器1 | 9.12.6.7 | 由网络管理员分配 |
| DNS服务器2/3（可选） | — | 未使用 |
| OSA设备名称 | eth0 | 由IPWIZARD分配的接口名称 |
| OSA起始设备号 | 3020 | z/VM TCP/IP协议栈的OSA三元组起始编号 |
| TCP/IP地址 | 9.12.4.89 | z/VM系统的TCP/IP地址 |
| 子网掩码 | 255.255.252.0 | 由网络管理员分配 |
| OSA设备类型 | QDIO | 对于OSA/Express卡，通常为“QDIO” |
| 网络类型 | Ethernet | 通常为“Ethernet” |
| 端口名称（可选） | — | z/VM不需要 |
| 路由器类型 | None | 通常为“None” |
| VSWITCH的主OSA设备号 | 3024 | 指定第一个设备号（必须为偶数），接下来的两个设备号也将被使用 |
| VSWITCH的辅助OSA设备号 | 3028 | 应位于不同的CHPID/OSA卡上 |
| z/VM的DASD地址 | 1A20 - 1A24 | 用于承载z/VM的3390-3磁盘 |
| Linux的DASD地址 | 1A25 - 1A29 | 用于承载Linux客户机的3390-3磁盘 |
| 分页的DASD地址 | 8228 | 用于承载Linux交换空间的3390-3磁盘 |

在您使用附录B“规划工作表”（第403页）中提供的模板创建您的工作表，并规划好z/VM和Linux安装所需的全部资源后，我们就可以进行一些实际工作了。

> **注意：** 您应该熟悉z/VM的基本概念。如果不熟悉，请参阅第65页的2.8“z/VM基本命令入门”以及本章前面的各节。

## 4.3.2 从DVD安装z/VM

本节假设您已通过DVD将z/VM完成第一级安装到DASD上。请确保您：

- 完成附录B“规划工作表”（第403页）中的工作表。
- 能够访问硬件管理控制台（HMC），并使用具有进入单一对象操作模式权限的用户ID。

z/VM 5.3以磁带和DVD形式提供。由于磁带I/O速度更快，从磁带安装z/VM应该会更快，但是，从磁带安装可能需要更多次在HMC和磁带驱动器之间往返。

如果您熟悉HMC，可以使用两页的《z/VM自动安装与服务概要（DVD安装）》来替代或补充后面的说明。

如果您不熟悉HMC和z/VM，您可能需要查阅完整的安装手册《z/VM自动安装与服务指南 V5.3.0》，编号GC24-6099。在HMC中为系统设置LPAR超出了本书的范围；为z/VM创建LPAR与为z/OS创建LPAR没有区别。

如果您要在第二级安装z/VM（z/VM下的z/VM）或安装到SCSI磁盘，请使用z/VM手册，因为以下各节不介绍这些选项。

### 从DVD安装z/VM

本节说明如何从带有DVD-ROM的HMC将z/VM 5.3安装到等效于3390-3的DASD上。我们还会指出安装到更大的3390-9 DASD上的差异。对于其他配置，例如从磁带安装或安装到SCSI磁盘，请参阅z/VM文档。

要从DVD安装z/VM：

1. 在硬件管理控制台上，选择要安装z/VM的LPAR。
2. 如有必要，点击“跑道”按钮（右下角的两个环形箭头按钮）以导航到CPC恢复（有时仅命名为“恢复”）菜单。
3. 在CPC恢复菜单上，双击“集成3270控制台”，如图4-7（第146页）所示。将打开一个名为“<yourCPC>的集成3270控制台”的窗口（在较旧级别的HMC上，该窗口可能名为Personal Communications）。




> 提示：使用 Alt+Tab 键序列可在 HMC 窗口和 3270 控制台之间方便地切换。

![](img/b0a4b9056f819dccd4781a5105c92d45_161_0.png)

Figure 4-7 Integrated 3270 Console icon

- 4. 将“z/VM Product Package Version 5 Release 3.0” DVD 放入 HMC DVD 驱动器中。

- 5. 按如下方式进入单对象操作模式：

> 注意：在 z10 上，您无需进入支持元素（SE）模式即可从 DVD 加载。

- a. 在 Views 区域中双击 Groups 图标。
- b. 在 Groups Work Area 中双击 Defined CPCs。
- c. 选择您的 CPC。
- d. 如有必要，使用右下角带有圆形箭头的按钮导航到 CPC Recovery 菜单。
- e. 双击 Single Object Operations 图标。点击 yes 确认。现在应出现一个新窗口，Primary Support Element Workplace，在旧版 HMC 上它将是“窗口中的窗口”。可能会出现一个关于证书的窗口。如果出现，请点击 OK。
- f. 在此窗口顶部附近双击 Groups。
- g. 在 Groups Work Area 中双击 Images。

> 重要：如果您无法进入单对象操作模式，您可能没有足够的权限。请咨询您的系统管理员。

- 6. 选择将安装 z/VM 的 LPAR。

7. 在此窗口中绕行到 CPC Recovery 菜单，如 Figure 4-8 所示。

![](img/b0a4b9056f819dccd4781a5105c92d45_162_0.png)

Figure 4-8 CPC Recovery menu

8. 双击 Load from CD-ROM, DVD, or Server 图标。“Load from CD-ROM or Server” 面板打开（Figure 4-9 on page 148）。

## Load from CD-ROM or Server - SCZP201:A04

Use this task to load operating system software or utility programs from a CD-ROM / DVD or a server that can be accessed using FTP.
Select the source of the software:

- Hardware Management Console CD-ROM / DVD
- FTP Source

Host computer:
User ID:
Password:
Account (optional):
File location (optional): /cpdvd

OK Cancel Help

Figure 4-9 Load from CD-ROM or Server panel

- 9. 选择 Hardware Management Console CD-ROM/DVD 按钮，如果它尚未被选中。
- 10. 在 File location 字段中输入 /cpdvd。这是 DVD 上包含 z/VM 5.3 安装代码的目录。
- 11. 点击 OK。
- 12. 加载 ramdisk。“Load from CD-ROM or Server” 面板中会显示软件列表。要加载 ramdisk：

- a. 选择，如尚未选中，软件 530vm.ins，如 Figure 4-10 on page 149 所示，然后点击 OK。

![](img/b0a4b9056f819dccd4781a5105c92d45_164_0.png)

Figure 4-10 Selecting z/VM 5.3 ramdisk system

- b. 在“Confirm the action”窗口中，点击 Yes。您应该会看到“Load from CD-ROM, DVD or Server Progress”窗口。DVD 驱动器上的绿色指示灯应亮起。

- c. 当您看到消息 Completed successfully 时，点击 OK 关闭。这通常需要大约四到六分钟。

> 注意：尽管 z/VM ramdisk（IBMVMMRAM）大约在四到六分钟内加载，但已观察到较慢的加载时间（15-18 分钟）。当 DVD 驱动器上的绿色指示灯常亮时，加载时间是可以接受的。当它间歇性熄灭的时间多于亮起时，可能会导致加载时间过长。

您现在应该有一个在内存中运行的 z/VM 5.3 系统。本节中执行的任务类似于将 Linux 内核加载到内存中以进行安装。您可以将本节与第 4.4.2 节“Booting the Linux kernel for installation” on page 199 进行比较，并随后验证两个系统在安装开始前都将映像加载到主内存中。一个区别是 Linux 会自动启动安装程序，而在 z/VM 中您必须在下一节中所述调用命令。

## Copying a z/VM system image to DASD

要将 z/VM 复制到 DASD：

- 1. 通过关闭该窗口注销 primary SE 窗口退出单对象操作模式。

- 2. 使用 Alt+Tab 序列切换到 Integrated 3270 控制台窗口。ramdisk IPL 并系统启动，MAINT 用户 ID 已登录。您应该会看到 z/VM 启动，如 Figure 4-11 on page 150 所示。





# SCZHMC7：适用于 SCZP701:A04 的集成 3270 控制台

```
File Keys Font Help

09:38:21
09:38:21 ***************************************************************
09:38:21 * LICENSED MATERIALS - PROPERTY OF IBM*
09:38:21 *
09:38:21 * 5741-A05 (C) COPYRIGHT IBM CORP. 1983, 2007. ALL RIGHTS
09:38:21 * RESERVED. US GOVERNMENT USERS RESTRICTED RIGHTS - USE,
09:38:21 * DUPLICATION OR DISCLOSURE RESTRICTED BY GSA ADP SCHEDULE
09:38:21 * CONTRACT WITH IBM CORP.
09:38:21 *
09:38:21 * * TRADEMARK OF INTERNATIONAL BUSINESS MACHINES.
09:38:21 ***************************************************************
09:38:21
09:38:21 The directory on volume $RAM0 at address FFFF has been brought
09:38:21 No dump unit - Dump function is SET OFF
09:38:21 HCPAAU27001 System gateway IBMVMRAM identified.
09:38:22 z/VM Version 5 Release 3.0, Service Level 0000 (64-bit),
09:38:22 built on IBM Virtualisation Technology
09:38:22 There is no logmsg data
09:38:22 FILES: NO RDR, NO PRT, NO PUN
09:38:22 LOGON AT 09:38:22 EDT THURSDAY 06/26/08
09:38:22 SYSG LOGON AS MAINT USERS = 1
09:38:22 HCPFOP552I 4G system storage
09:38:22 FILES: 000001 RDR, 000001 PRT, NO PUN
09:38:22 HCP CRC0082I Accounting records are accumulating for userid 0
09:38:22 HCP CRC0082I EREP records are accumulating for userid OPERREB
DMS1PD2015W Unable to access the Y-disk. Filemode Y (19E) not accessed
DMSWSP327I The installation saved segment could not be loaded
z/VM V5.3.0 2007-05-04 13:22
DMSDCS1083E Saved segment CMSPIPES does not exist
DMSDCS1083E Saved segment CMSPIPES does not exist
DMSDCS1083E Saved segment CNSVMLIB does not exist
Ready; T=0.01/0.01 09:38:22

RUNNING IBMVM6
```

图 4-11 z/VM 在集成控制台上的首次引导

在以下示例中，我们的设备为 1A20-1A24（请使用您自己的值，不要输入尖括号）：

```
==> att <1a20-1a24> *
1a20-1a24 ATTACHED TO MAINT
```

**重要：** 本书示例中的尖括号（<>）表示应当用适合您环境的正确值替换我们的示例值。例如，如果要将 z/VM 安装到 DASD 1200-1204，应键入以下内容：

==> att 1a00-1a04 *

## 运行 INSTDVD

INSTDVD EXEC 将 z/VM 系统从 DVD 复制到磁盘。要运行 INSTDVD：

- 1. 执行 INSTDVD EXEC 命令：

```
==> instdvd
```

如果使用 3390-3s，将有一个面板请求五个卷（图 4-13）。

![](img/b0a4b9056f819dccd4781a5105c92d45_167_0.png)

图 4-13 instdvd DASD 窗口

- a. 输入将要安装 z/VM 的五个卷的地址。

- b. 不要选中面板右侧的 DO NOT FORMAT DASD 复选框。

- c. 请注意，除了 530RES 之外，您可以更改所有卷的标签。我们建议您将其他标签改为 530 以外的名称。第 4.3.3 节“重新标记系统卷”（第 165 页）说明了您应该更改标签的原因。我们将自己的标签改为使用前缀 LX6。

- d. 按 F5 开始安装。

- 2. 当系统提示您是否继续时，输入 Y（是）（DO YOU WANT TO CONTINUE?）。

将显示消息 NOW FORMATTING DASD <1A20>。

> **重要：** 在 z10 LPAR 上运行 INSTDVD 大约需要一个小时。
> 
> 可能会出现读取错误，导致 INSTDVD 失败。如果发生这种情况，请尝试使用以下命令，以便安装过程可以从发生读取错误的位置继续：
> 
> INSTDVD (RESTART
> 
> 读取错误可能是由 DVD 上的污垢或指纹引起的。

- 3. 系统提示您将系统 RSU 放入驱动器中。将“z/VM Stacked Recommended Service Upgrade 5301”DVD 插入 HMC DVD-ROM 驱动器，然后输入 G0。此步骤需要两到四分钟。

将显示以下消息或类似消息：

```
DVDLOAD: LOADING FILE CKD5000x IMAGE *
```

当进程完成时，将显示以下消息：

```
HCPIDV8329I INSTDVD EXEC ENDED SUCCESSFULLY.
```

## 从 DASD IPL z/VM

要从 DASD 对初始 z/VM 系统执行 IPL：

- 1. 在 HMC 中，单击选中您的 LPAR。您可能需要先双击 Groups。

将打开 CPC Recovery（有时也称为 Recovery）菜单。

- 2. 双击右侧菜单中的 Load 图标。将打开 Load 面板，如图 4-14（第 154 页）所示。





![](img/b0a4b9056f819dccd4781a5105c92d45_169_0.png)

*图 4-14 加载面板*

3. **按以下步骤操作：**
   a. 对于负载类型，选择 **Clear** 按钮。
   b. 将负载地址设置为新的系统驻留位置，即本例中为 `<1A20>` 的 530RES 卷。
   c. 将负载参数设置为 **SYSG**。这指定使用集成 3270 控制台。
   d. 单击 **OK** 开始加载。
4. 当加载任务确认窗口打开时，单击 **Yes**。
5. 大约 1-3 分钟后，当加载程序窗口中出现 **Success** 字样时，单击 **OK**。
6. 使用 **Alt+Tab** 组合键返回到集成 3270 控制台窗口。**STAND ALONE PROGRAM LOADER** 面板打开。

a. 按 Tab 键遍历到 IPL 参数部分，如图 4-15 所示，并输入值 cons=sysg。这指定使用集成 3270 控制台。

![](img/b0a4b9056f819dccd4781a5105c92d45_170_0.png)

图 4-15 IPL 参数。

b. 按 F10 键继续对 z/VM 系统进行 IPL。这大约需要 2-3 分钟。

7. 在 Start (Warm|Force|COLD|CLEAN) 提示符下，输入以下命令：
==> cold drain noautolog

8. 在 Change TOD clock 提示符下输入：
==> no
最后一条消息是：
HCPCRC8082I EREP records are accumulating for userID EREP

9. 使用 DISCONNECT 命令（或其缩写形式：DISC）断开 OPERATOR 用户 ID 的连接：
==> disc

10. 按 Enter 打开新的登录窗口。

## 完成 z/VM 安装

要完成 z/VM 安装：

1. 在 z/VM 登录窗口中，以 MAINT 身份登录。密码为 MAINT。你可能会收到关于磁盘未链接或未附加的 HCPLMN108E 或 DMSACP113S 消息。这不是问题。当你在右下角看到 VM Read 提示符时，按 Enter。

重要提示：当登录到运行 CMS 的 z/VM 用户 ID 时，在 VM READ 提示符处按 Enter。这将导致出现如下形式的提示：
Ready; T=0.01/0.01 11:14:20

2. 发出 ipl cms 命令然后按 Enter，如图所示。Ready; 提示符出现。

```
==> ipl cms
==> (Press the Enter key)
Ready;
```

3. 运行 INSTVM DVD 命令：

```
==> instvm dvd
...
HCPP LD8329I POSTLOAD EXEC ENDED SUCCESSFULLY
...
HCPIVM8392I INSTVM ENDED SUCCESSFULLY
```

EXEC 继续安装过程。此步骤大约需要 4-8 分钟。最后一条消息是：
HCPIVM8392I INSTVM ENDED SUCCESSFULLY

4. 加载推荐的服务。对于 z/VM 5.3，服务名称为 5301RSU1。运行以下命令：

```
==> ipl cms
==> Press Enter
Ready;
==> acc 500 c
DMSACC7241 500 replaces C (2CC)
==> listfile * * c
5301RSU1 SERVLINK C1
==> service all 5301rsu1
```

此步骤大约需要 3-6 分钟。最后一条消息是：
VMFSRV2760I SERVICE processing completed successfully

5. IPL CMS 并运行 PUT2PROD 命令。这会将服务投入生产：

```
==> ipl cms
==> Press Enter
Ready;
==> put2prod
```

此步骤大约需要 2-4 分钟。最后一条消息是：
VMFP2P2760I PUT2PROD processing completed successfully

返回码为 0 是理想的。你可能会收到返回码为 4 并且出现消息：

```
VMFP2P27601 PUT2PROD process completed with warnings
```

通常在 z/VM 上，返回码为 4 是可以接受的。这意味着仅发出警告。返回码为 8 或更大通常意味着遇到错误。

6. 输入以下命令以关闭并再次 IPL 你的系统：

```text
==> shutdown repl
SYSTEM SHUTDOWN STARTED
```

虽然你会丢失 3270 会话，但系统大约在 2-4 分钟后返回。之后，最后一条消息是：

```text
Press enter or clear key to continue
```

7. 按 Enter。z/VM 登录窗口打开。

恭喜！你现在已安装了一个标准的 z/VM 系统。

## 配置 PROFILE XEDIT 文件

调用时，XEDIT 命令会查找 PROFILE XEDIT 配置文件。许多 z/VM 用户 ID 都没有这样个人或共享系统文件，因此所有 XEDIT 默认值均生效。MAINT 191 (A) 磁盘上有一个 PROFILE XEDIT 文件，因此当你在 MAINT 上编辑文件时，该配置文件中的值通常生效。

为了在使用 XEDIT 时获得良好的体验，请使 MAINT 用户的配置文件与第 92 页示例 2-25 中的类似。为此，以 MAINT 登录并使用 XEDIT 本身编辑该文件：

```
==> xedit profile xedit a
```

使用 XEDIT 子命令 SAVE 保存你的更改。





> 重要提示：一个可能很危险的默认设置，尤其是在你使用 F12 来检索命令时，就是当 PF12 被设置为 FILE 子命令时。有时你可能不想通过按一个键就保存你的更改。建议将 PF12 设置为 ? 子命令，其效果等同于检索键：
> 
> ==> x profile xedit a
> 
> 修改前：SET PF12 FILE
> 
> 修改后：SET PF12 ?
> 
> 现在使用 FILE 子命令保存更改并退出。

## 配置 TCP/IP

建议你在 z/VM 环境中首次配置 TCP/IP 时，使用 IPWIZARD 命令在 z/VM 环境中初始配置 TCP/IP，然后此后手动更改配置文件。IPWIZARD 创建初始配置文件后，你需要手动维护它们。

## 登录到 MAINT

在 z/VM 登录面板中，登录到 MAINT。所有 z/VM 用户 ID 的默认密码与用户 ID 相同。输入密码 maint，密码在窗口中不会回显。

```
USERID ==> maint
PASSWORD ==>
```

输入用户 ID 和密码后，当右下角的状态区显示 VM READ 时，按 Enter。

## 使用 IPWIZARD 工具

IPWIZARD 命令位于 MAINT 193 磁盘上。要从该迷你磁盘获取 IPWIZARD，请以文件模式 G 访问它，使用 ACCESS：

- 1. 访问 MAINT 193 磁盘：
  ==> acc 193 g
- 2. 调用 IPWIZARD：
  ==> ipwizard

z/VM TCP/IP 配置向导打开；第一个字段，用户 ID，应始终为 TCP/IP：

```
*** z/VM TCP/IP Configuration Wizard ***

The items that follow describe your z/VM host

User ID of VM TCP/IP Stack Virtual Machine: TCPIP__

Host Name: <vmlinux6>________________
Domain Name: <itso.ibm.com>________________

Gateway IP Address: <9.12.4.1>________________

DNS Addresses:
1) <9.12.6.7>_
2) ________________
```

3. 从第 143 页的“规划工作表”中获取剩余值并按 F8。通用接口配置面板打开：

```
*** General Interface Configuration Panel ***

Interface Name: ETH0_________    Device Number: <3020>

IP Address: <9.12.4.89>
Subnet Mask: <255.255.252.0>_

Interface Type (Select one):

x QDIO      _ LCS      _ HiperSockets
```

请注意此面板的以下信息：

- ETH0 是接口名称。这是可以任意指定的，但建议使用。
- 设备号是 z/VM 堆栈将使用的 OSA 三元组的起始地址。
- IP 地址必须路由到 OSA 卡，将成为 z/VM 系统的 TCP/IP 地址。
- 接口类型通常是使用现代 OSA 设备时的 QDIO。

4. 完成后按 F8。QDIO 接口配置面板打开：

### *** QDIO Interface Configuration Panel ***

Network Type (Select one):

x Ethernet      _ Token Ring

Port Name (optional): ______

Router Type (Select one):

_ Primary      _ Secondary      x None

请注意此面板的以下信息：

- 通常不再需要为端口名称设置值⁷。
- 建议将路由器类型设置为无。

5. 按 F5 完成向导。显示以下消息：

```
DTCIPW25081 DTCIPWIZ EXEC is attempting to create the necessary
DTCIPW25081 configuration files
```

6. 在以下消息中，输入 1 重新启动 TCP/IP 堆栈：

```
The TCP/IP stack (TCPIP) must be restarted as part of this procedure
Would you like to restart and continue?
Enter 0 (No), 1 (Yes) 1
USER DSC LOGOFF AS TCPIP USERS = 2 FORCED BY MAINT
...
Successfully PINGed Interface (9.12.4.89)
Successfully PINGed Gateway (9.12.4.1)
Ping Level S20: Pinging host 9.12.6.7
Enter 'HX' followed by 'BEGIN' to interrupt.
```

> 重要提示：如果无法 ping 到 DNS 服务器，输入 1 重新尝试：
> PING: Ping #1 timed out
> Not all of the PINGs were successful. Would you like to try them again?
> Enter 0 (No), 1 (Yes)
> ==> 1
> ...

⁷ 如果 OSA 卡已定义了端口号，例如因为它正被需要端口号的系统共享，那么你应在此处设置相同的端口号。





==> log
一个新的登录面板打开。

+   2. 登录到 AUTOLOG1。密码与用户 ID 相同。

+   3. 在 VM READ 提示符下输入 ACCESS（NOPROF 以防止 PROFILE EXEC 运行：

```
LOGON AUTOLOG1
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: NO RDR, NO PRT, NO PUN
LOGON AT 13:30:12 EST THURSDAY 11/29/07
DMSIND2015W Unable to access the Y-disk. Filemode Y (19E) not accessed
z/VM V5.3.0 2007-11-24 12:48
acc (noprof
```

+   4. 从 MAINT 191 磁盘复制 PROFILE XEDIT，以便 XEDIT 会话在用户 ID 之间具有统一的界面。

+   a. 使用 VMLINK 命令同时链接到只读磁盘并以最高可用的文件模式访问它。默认读取密码为 read：

```
==> vmlink maint 191
ENTER READ PASSWORD:
read
DMSVML20601 MAINT 191 linked as 0120 file mode Z
```

+   b. 将 PROFILE XEDIT 复制到你的 A 磁盘：

```
==> copy profile xedit z = = a
```

+   5. 备份 PROFILE EXEC 的副本并运行编辑器来编辑它：

```
==> copy profile exec a = execorig =
==> x profile exec
```

示例 4-2 中的文本出现。

## 示例 4-2 修改前的文本

```
/**************************/
/* Autolog1 Profile Exec */
/**************************/

Address Command
'CP XAUTOLOG VMSERVS'
'CP XAUTOLOG VMSERVU'
'CP XAUTOLOG VMSERVR'
```

+   6. 按如下方式修改它，并在第 163 页的示例 4-3 中查看结果。

+   a. z/VM 共享文件系统（SFS）不需要运行 Linux，因此你可以安全地删除用于用户 ID VMSERVS、VMSERVR 和 VMSERVU 的三条 AUTOLOG 行。
+   b. 你也可以安全地删除 Address Command 行。
+   c. 添加一行使用 XAUTOLOG 命令启动 TCPIP 用户 ID，并保留启动 VSWITCH 控制器的任何语句。
+   d. 添加一行在 EXEC 完成后注销 AUTOLOG1。无需保持该虚拟机运行，因为其唯一目的是运行 PROFILE EXEC。

## 示例 4-3 修改后的文本

```
/***********************/
/* Autolog1 Profile Exec */
/***********************/

/* start up TCPIP */
/* logoff when done */

'cp autolog tcpip' /* start up TCPIP */
'cp logoff' /* logoff when done */
```

7. 使用 FILE 子命令保存你的更改并使用 LOGOFF 注销 AUTOLOG1：

=====> file

=====> log

当你的 z/VM 系统 IPL 时，TCP/IP 堆栈将自动启动（如果你在 IPL 时未指定 notautolog 参数）。

## 设置 FTP 服务器

在本节中，你将学习如何为你的 z/VM 设置 FTP 服务器，因为在第 188 页的“获取 Linux 启动所需的文件”部分，你必须将文件从工作站发送到你的 Linux 客户机虚拟机。文件必须保持其 80 字符记录长度属性。

默认情况下，z/VM 的安装中包含 FTP 服务器。要将其上线，以 TCPMAINT 登录并编辑其 198 磁盘上的 PROFILE TCPIP 文件，该磁盘作为 D 磁盘访问：

=====> x profile tcpip d

## 示例 4-4 编辑前的文件

```
; 
; 
OBEY
OPERATOR TCPMAINT MAINT MPROUTE ROUTED DHCPD REXECD SNMPD SNMPQE
ENDBEY
```

```
; -----------------------------------------------------------------
PORT
; 20 TCP FTPSERVE NOAUTOLOG ; FTP Server
; 21 TCP FTPSERVE          ; FTP Server
; 23 TCP INTCLIEN          ; TELNET Server
; 25 TCP SMTP              ; SMTP Server
...
```

在文件顶部附近添加一个 AUTOLOG 语句；FTPSERVE 应为唯一条目。在 PORT 语句中，删除分号以取消注释包含 FTPSERVE 的行（端口 20 和 21）。这些更改会导致 FTP 服务器在 TCP/IP 启动时启动。然后，使用 FILE 子命令保存你的更改。参见示例 4-5。

## 示例 4-5 编辑后的文件

```
; -----------------------------------------------------------------
OBEY
OPERATOR TCPMAINT MAINT MPROUTE ROUTED DHCPD REXECD SNMPD SNMPQE
ENDOBEY
; -----------------------------------------------------------------
AUTOLOG
    FTPSERVE 0
ENDAUTOLOG

PORT
  20 TCP FTPSERVE NOAUTOLOG ; FTP Server
  21 TCP FTPSERVE          ; FTP Server
  23 TCP INTCLIEN          ; TELNET Server
; 25 TCP SMTP              ; SMTP Server
...
====> file
```

这些更改将在你再次 IPL 系统后生效。

## 再次 IPL 系统（重新 IPL）

你可能希望在无需访问 HMC 的情况下关闭并重新 IPL z/VM。通常，HMC 已注销，因此集成 3270 控制台（SYSG）不可用。由于这些因素，使用系统控制台（SYSC）很有用，HMC 上的标题为 Operating System Messages，可以在无需使用控制台的情况下关闭 z/VM 并重新 IPL 它。此控制台无论你是否登录到 HMC 始终可访问。z/VM 在关闭和重新 IPL 过程中的消息都会写入系统控制台，但通常你可以忽略它们；你只需在几分钟内通过网络恢复系统即可。





您现在可以关闭并重新 IPL 系统。这是使之前更改生效的最快方法，因为此时还没有生产系统在运行。对 SHUTDOWN REIPL 命令传递参数 IPLPARMS CONS=SYSC：

```
==> shutdown re ipl iplparms cons=sysc
```

您将失去当前会话，但几分钟后应该会恢复。

如果网络设置正确，您现在可以通过网络访问 z/VM，而无需使用 HMC。您可以使用类似 3270 的仿真器，例如 IBM Personal Communications，通过其 IP 地址访问网络启用的 z/VM。

## 4.3.3 重新标记系统卷

此步骤是可选的，但建议执行。有时您会想要更改五个 z/VM 系统卷的卷标（如果安装在多个 3390-9 上，则为三个）。如果另一个具有相同卷标的 vanilla z/VM 系统安装在您的 z/VM 系统可访问的卷上，其中一个系统将无法正确 IPL。

在安装 z/VM 时，可以修改除一个卷标之外的所有卷标，即 530RES 卷的卷标。这缓解了接下来描述的问题，但并未缓解重复卷名的問題。要理解这种可能性，请参阅图 4-16。

![](img/b0a4b9056f819dccd4781a5105c92d45_180_0.png)

图 4-16 两个具有相同卷标的 z/VM 系统的问题

从 E340 开始的较低设备地址的 z/VM 系统应该可以正常 IPL（尽管在系统启动时您可能会看到有关重复卷标的警告）。然而，如果从设备地址 F000 开始的 z/VM 系统被 IPL，则会使用 530RES 卷，但系统中的剩余卷是按卷标而不是按设备地址搜索的。由于 z/VM 系统 1 的地址低于 z/VM 系统 2，系统 2 将使用系统 1 的卷。这对两个系统都不好！

使用标签约定访问其根分区的 Linux 系统也存在类似问题。如果您将两个 Linux 系统安装在同一磁盘上，两者都使用标签来标识其分区，第二个系统实际上会使用第一个标记为根文件系统的分区。本书的作者不建议在 Linux 中使用标签。

如果有可能在 DASD 上安装另一个 z/VM 系统，而该系统可被此系统访问，建议您执行以下各节中的步骤：

- 第 166 页的“在 SYSTEM CONFIG 文件中修改标签”
- 第 168 页的“在 USER DIRECT 文件中修改标签”
- 第 169 页的“更改五个卷的标签”
- 第 170 页的“关闭系统并重新 IPL”

您必须能够访问 HMC 才能执行这些步骤。

> 注意：此过程必须按文档所述进行。在其中一个步骤中出现错误很容易导致系统无法使用。仔细检查您的步骤，系统将毫无问题地恢复。尽量在短时间内连续完成所有步骤。关上门，不要接电话或电子邮件，关闭即时消息：））

### 在 SYSTEM CONFIG 文件中修改标签

此文件控制系统使用哪些 DASD，定义了哪些虚拟资源等等。修改各种 DASD 设置，以便系统能够使用新标签正确启动。

您必须拥有 HMC 3270 会话，因为 z/VM 必须使用 FORCE 选项重新启动。

要修改 SYSTEM CONFIG 文件中的标签：

- 1. 从 CPC Recovery（或仅 Recovery）菜单在 HMC 上启动 Integrated 3270 Console 会话。
- 2. 使用 QUERY CPOWNED 命令记录前五个由 CP 拥有的卷：

```
==> q cpowned
Slot  Vol-ID  Rdev  Type  Status
1     S30RES  A700  Own   Online and attached
2     LX6SPL  A701  Own   Online and attached
3     LX6PAG  A702  Own   Online and attached
4     LX6W01  A703  Own   Online and attached
5     LX6W02  A704  Own   Online and attached
6     MPA705  A705  Own   Online and attached
```




7  MPA706 A706 Own  Online and attached
8  MPA707 A707 Own  Online and attached
9  MPA708 A708 Own  Online and attached
10 MPA709 A709 Own  Online and attached
11 ------ ---- ----- Reserved
12 ------ ---- ----- Reserved
...

由于我们在“Running INSTDVD”第152页中更改了其他四个 DASD 的标签，因此只有 530RES DASD 需要更改其标签。

对于 3390-9： 如果 z/VM 安装在多个 3390-9 上，则应只有三个系统卷：

```
==> q cpowned
Slot  Vol-ID Rdev Type  Status
1     530RES 9300 Own   Online and attached
2     530SPL 9301 Own   Online and attached
3     530PAG 9302 Own   Online and attached
...
```

3. 使用 XEDIT 子命令有助于使此过程更可靠。它可用于 SYSTEM CONFIG 和 USER DIRECT 文件。要修改 SYSTEM CONFIG 文件中的标签，请释放 A CP 磁盘并以读写方式访问它。备份 SYSTEM CONFIG 文件：

```
==> cprelease a
CPRELEASE request for disk A scheduled.
HCPZAC67301 CPRELEASE request for disk A completed.
==> link * cfl cfl mr
==> acc cfl f
==> copy system config f = confwrks = (oldd rep
```

4. 编辑 SYSTEM CONFIG 文件并使用 ch 子命令为每个需要重新标记的标签进行重新标记（本示例中仅为 530RES）：

```
==> xedit system config f
==> ch /530RES/<LX6RES>/* *
```

注意：不要忘记将 <LX6RES> 更改为您使用的前缀。

每次更改命令后，都会显示一条消息，指示已更改的行数。

5. 清除窗口以返回 XEDIT 中的文件编辑。搜索字符串 cp_owned，您应该会看到新的标签。在使用 FILE 子命令保存文件之前，请确保它们正确：

```
====> /cp_owned
/*          CP_Owned Volume Statements                 */
```

```
/*****************************************************************/
CP_Owned  Slot  1 LX6GRES
CP_Owned  Slot  2 LX6SPL
CP_Owned  Slot  3 LX6PAG
CP_Owned  Slot  4 LX6W01
CP_Owned  Slot  5 LX6W02
...
====> file
```

- 6. 验证不存在语法错误：
- ==> acc 193 g
- ==> cpsyntax system config f
- CONFIGURATION FILE PROCESSING COMPLETE -- NO ERRORS ENCOUNTERED.

- 7. 释放并分离 F 磁盘，并使用 CPACCESS（或其缩写：CPACC）访问 A 磁盘并验证：
- ==> rel f (det
- DASD OCF1 DETACHED
- ==> cpacc * cfl a
- CPACCESS request for mode A scheduled.
- Ready; T=0.01/0.01 09:19:57
- HCPZACG732I CPACCESS request for MAINT's OCF1 in mode A completed.
- ==> q cpdisk
- Label  Userid  Vdev  Mode  Stat  Vol-ID  Rdev  Type    StartLoc    EndLoc
- MNTCF1 MAINT  OCF1  A     R/O   530RES A700 CKD    39        83
- MNTCF2 MAINT  OCF2  B     R/O   530RES A700 CKD    84        128
- MNTCF3 MAINT  OCF3  C     R/O   530RES A700 CKD   129        188

您现在已更改 SYSTEM CONFIG 文件中系统卷的标签。

> 重要：继续操作至关重要，因为您的系统现在处于一种状态，无法干净地 IPL。

## 修改 USER DIRECT 文件中的标签

USER DIRECT 文件存储有关每个 z/VM 虚拟机，即每个用户的空间使用情况的信息。必须在文件中反映对 DASD 标签所做的更改，否则您的系统最终将处于不一致状态。

再次修改 USER DIRECT 文件：

- 1. 使用 XEDIT 的 ch 子命令。您应该开始看到更多正在更改的标签出现：
- ==> copy user direct c = direwrks = (oldd rep
- ==> x user direct c

```
==> ch /530RES/<LX6RES>/* *
DMSXCG517I 84 occurrence(s) changed on 84 line(s)
```

您可以在保存更改之前选择遍历文件以验证其内容。

- 2. 使用 FILE 子命令保存文件：

```
====> file
```

您现在已更改 USER DIRECT 和 SYSTEM CONFIG 文件中系统卷的标签。同样，继续执行剩余步骤至关重要。

## 更改五个卷上的标签

要重新标记一个盘包，请使用对 DASD 卷第 0 柱面的写访问权限。已经存在 mdisk 语句为您提供该访问权限。要更改五个卷上的标签：

- 1. 查询磁盘以确保您拥有对它们的 R/W 访问权限：

```
query virtual 122-125
DASD 0122 3390 LX6SPL R/W 3339 CYL ON DASD 1A21 SUBCHANNEL = 000A
DASD 0123 3390 530RES R/W 3339 CYL ON DASD 1A20 SUBCHANNEL = 000B
DASD 0124 3390 LX6W01 R/W 3339 CYL ON DASD 1A23 SUBCHANNEL = 000C
DASD 0125 3390 LX6W02 R/W 3339 CYL ON DASD 1A24 SUBCHANNEL = 000D
```

注意：虚拟地址和卷的映射默认为：
► MAINT 122 对应 530SPL
► MAINT 123 对应 530RES
► MAINT 124 对应 530W01
► MAINT 125 对应 530w02
► $PAGE$ A03 对应 530PAG

如果您也需要重新标记它（在我们的示例安装中并非如此，因为它已正确标记），您可能需要在查询分页微磁盘之前将其链接：

```
link $page$ a03 a03 mr
Ready; T=0.01/0.01 17:24:51
query virtual a03
DASD 0A03 3390 LX6PAG R/W 3339 CYL ON DASD 1A22 SUBCHANNEL = 004A
```

- 2. 使用以下命令为每个盘包重新标记适当的标签：

```
cpfn t xa 123 <LX6RES> label
```


> **注意：** 在命令中，请确保添加最后一个参数，label。
> 
> z/VM 系统不会在下一次 IPL 之前重新读取磁包标签，因此如果要显示这些磁包，将会显示旧标签。

- 3. 将更新后的 USER DIRECT 文件加载到系统目录空间。
  - `directxa user direct c`

- 4. 在加载新目录后，关闭系统并重新 IPL 系统。

## 关闭系统并重新 IPL

你必须为此步骤运行 HMC 控制台会话，如果你尚未从那里运行。

测试更改涉及关闭并重新启动系统。在这种情况下，你不得使用 SHUTDOWN REIPL，因为你随后必须使用 FORCE 来重新启动它。要关闭系统，请单独使用 SHUTDOWN 命令：

```
==> shutdown
SYSTEM SHUTDOWN STARTED
HCPSH9060I System shutdown may be delayed for up to 210 seconds
```

要将系统恢复运行：

- 1. 从 HMC，点击 CPC Recovery（或仅 Recovery）菜单中的 LOAD 图标。
- 2. 选择 Clear 单选按钮。所有其他参数应与之前的 IPL 相同。点击 OK。
- 3. 在 Load Task Confirmation 面板上点击 Yes。
- 4. 返回到 Integrated 3270 控制台。几分钟后，Standalone Program Loader 面板应打开。使用 TAB 键遍历到 IPL Parameters 部分并输入以下值：
  - `cons=sysg`
- 5. 按 F10 键继续 IPL 你的 z/VM 系统。这大约需要三分钟。
- 6. 在 Start 提示符处，指定 FORCE 启动，因为 spool 卷标签已更改：
  - `==> force drain`
- 7. 不要更改日时钟：
  - `==> no`

8. 当 IPL 完成时，从 OPERATOR 用户 ID 断开连接：
==> disc

9. 登录到 MAINT。

你现在应该能够启动一个 3270 仿真器会话，因为 TCP/IP 服务机器应该已启动。作为 MAINT 获取一个 3270 会话并使用 QUERY CPOWNED 命令验证卷标签是否已更改：

```
==> q cpowned
Slot Vol-ID Rdev Type Status
1 LX6RES 1A20 Own Online and attached
2 LX6PSL 1A21 Own Online and attached
3 LX6PAG 1A22 Own Online and attached
4 LX6W01 1A23 Own Online and attached
5 LX6W02 1A24 Own Online and attached
...
```

如果你 IPL 了一个具有重复系统卷的系统，你可能已经破坏了你的保存段。当你无法 IPL CMS 时，你就知道这种情况发生了，因此你必须 IPL 190。

> 重要：只有在你的保存段已被破坏时才执行此操作！要重建保存段，请尝试以下命令，作为 MAINT：
> ==> vmfsetup zvm cms
> ==> sampnss cms
> ==> i 190 c1 parm savesys cms
> ==> vmfbld ppf segbld esasegs segblist ( all

## 4.4 安装 Linux

本节描述如何配置你的 z/VM 系统以安装 Linux，引导用于安装的 Linux 内核，并登录到 Linux 系统。

### 4.4.1 为安装 Linux 配置你的 z/VM 系统

要在 z/VM 上运行 Linux 虚拟机，需要一个简单但高效的环境，你必须首先配置和自定义你的环境，以便在执行 Linux 内核时，DASD、网络和易于管理和安装的 Linux 客户机等资源都可用。

涉及的配置任务包括：

- 自定义 SYSTEM CONFIG 文件
  - 更改各种参数。
  - 创建虚拟交换机。
- 为 Linux 客户机设置 DASD
  - 格式化 DASD。
  - 为系统和用户使用配置 DASD。
- 创建 Linux 维护用户
  - 创建 minidisk。
  - 设置一个用于在客户机虚拟机中引导 Linux 的通用环境。

请回顾第 4.2.2 节“系统文件”第 126 页，我们在其中提到了 z/VM 的重要配置文件。你现在即将对其进行自定义。

## 自定义 SYSTEM CONFIG 文件

z/VM IPL 时读取的第一个配置文件是 SYSTEM CONFIG 文件。

建议进行以下更改：

- 增加检索键容量。
- 允许创建虚拟磁盘（VDISK）。
- 关闭 Disconnect Timeout。这将防止空闲断开连接的用户被强制退出系统。
- 定义一个将用于 Linux 网络的虚拟交换机（VSWITCH）。

为所有 Linux 客户机系统定义虚拟交换机是良好的做法，因为如果你计划以后增加数量，你可能没有足够的物理 OSA 网络卡供你创建的每个客户机虚拟机使用。虚拟交换机使用单个真实 OSA 设备并在多个虚拟客户机之间共享网络连接。

要自定义 SYSTEM CONFIG 文件：

- 1. 释放 CF1 磁盘。

要编辑 SYSTEM CONFIG 文件，MAINT 的 CF1 minidisk 必须通过 CPRELEASE 命令（或其缩写：CPREL）作为 CP 磁盘释放。CP 磁盘可通过 QUERY CPDISK 命令查询。请注意，由于 CF1 磁盘归 CP 所有，它正以只读模式由 MAINT 作为 CP 磁盘 A 访问。因此，为了以多读模式访问该 CF1 磁盘，我们首先请求 CP 释放它，然后以多读（mr）模式访问它：

```
==> q cpdisk
Label Userid Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
```





MNTCF1 MAINT  OCF1 A  R/O MVA740 A740 CKD      39      158
MNTCF2 MAINT  OCF2 B  R/O MVA740 A740 CKD     159      278
MNTCF3 MAINT  OCF3 C  R/O MVA740 A740 CKD     279      398
==> cprel a
CPRELEASE 请求磁盘 A 已安排。
HCPZAC67301 CPRELEASE 请求磁盘 A 已完成。
==> q cpdis k
Label Userid Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
MNTCF2 MAINT  OCF2 B  R/O MVA740 A740 CKD     159      278
MNTCF3 MAINT  OCF3 C  R/O MVA740 A740 CKD     279      398

2. 释放后，以读写模式访问 MAINT CF1 磁盘。使用带多读（MR）参数的 LINK 命令，以及 ACCESS 命令以获取对迷你磁盘的读写访问权限。

```
==> link * cf1 cf1 mr
==> acc cf1 f
```

3. 现在 MAINT CF1 磁盘已作为你的 F 磁盘以读写方式访问：

+   a. 首先使用带 OLDDATE 参数的 COPYFile 命令制作 vanilla SYSTEM CONFIG 文件的备份副本以防止修改文件的时间戳，然后编辑原始副本：

```
==> copy system config f system conorig f (olddate)
==> x system config f
```

+   b. 接下来查找 Features 语句。你可以再次搜索它或使用 F8 向下翻页。建议进行以下更改和添加：

+   - 将可检索的命令数量从 20 增加到 99。
+   - 将 Disconnect_Timeout 设置为 off，以便断开连接的用户不会被强制退出。
+   - 通过将 Userlim 更改为 infinite 并添加 Syslim infinite 子句，允许用户创建无限数量的 VDISKs：

```
Features ,
Disable ,
Set_Privclass ,            /*Disallow SET PRIVCLASS command*/
Auto_Warm_IPL ,            /*Prompt at IPL always */
Clear_TDisk ,              /*Don't clear TDISks at IPL time*/
Retrieve ,                 /*Retrieve options */
Default 99 ,               /*Default.... default is 20 */
Maximum 255 ,              /*Maximum.... default is 255 */
MaxUsers noLimit ,         /*No limit on number of users */
Passwords_on_Cmds ,        /*What commands allow passwords?*/
Autolog yes ,              /*... AUTOLOG does */
Link yes ,                 /*... LINK does */
Logon yes ,                /*... and LOGON does, too */
Disconnect_Timeout off ,   /*Don't force disconnected users*/
Vdisk ,                    /*Allow VDISKs for Linux swaps */
```

```
Syslim infinite ,
Userlim infinite
```

> 注意：如果您想限制用户可以创建的 VDISKs 数量，请为其选择一个限制而不是使用 infinite。有关 VDISKS 的更多信息，请阅读第 264 页“Virtual DASD (VDISK)”中的内容。

## 4. 定义一个 VSWITCH：

使用 BOTTOM（或其缩写 BOT）子命令转到文件的底部。添加行（您可以使用 XEDIT ADD 子命令，a3，来添加三行）。定义一个 VSWITCH 并设置 MAC 地址前缀。如果您有多个 z/VM 系统，每个系统应具有唯一的前缀。将 OSA 三元组的两个起始地址（本示例中为 3024 和 3028）修改为您在第 143 页“规划工作表”中指定的地址。

```
====> bot
====> a3
/* define vswitch named vsw1 and set MAC address prefixes to
02-00-01 */
define vswitch vsw1 rdev <3024> <3028>
vm lan macprefix 020001
```

## 5. 使用 XEDIT FILE 子命令保存您的更改：

```
====> file
```

## 6. 使用位于 MAINT 193 磁盘上的 CPSYNTAX 命令测试您的更改：

```
==> acc 193 g
==> cpsyntax system config f
CONFIGURATION FILE PROCESSING COMPLETE -- NO ERRORS ENCOUNTERED.
```

注意输出。如果您有任何语法错误，请在继续之前修复它们。

## 7. 使用 RELEASE 命令（缩写为 REL）和 DETACH 参数释放并分离 MAINT CF1 磁盘。然后使用 CPACCESS 命令将其重新上线：

```
==> rel f (det
DASD OCF1 DETACHED
==> cpacc * cf1 a
CPACCESS request for mode A scheduled.
HCPZAC67321 CPACCESS request for MAINT's OCF1 in mode A completed.
==> q cp disk
```

| Label | Userid | Vdev | Mode | Stat | Vol-ID | Rdev | Type | StartLoc | EndLoc |
|-------|--------|------|------|------|--------|------|------|----------|--------|
| MNTCF1 | MAINT | OCF1 | A | R/O | MVA740 | A740 | CKD | 39 | 158 |
| MNTCF2 | MAINT | OCF2 | B | R/O | MVA740 | A740 | CKD | 159 | 278 |
| MNTCF3 | MAINT | OCF3 | C | R/O | MVA740 | A740 | CKD | 279 | 398 |





'cp set mdc stor 0m 128m' /* 限制 CSTOR 中的 minidisk 缓存 */
'cp set mdc xstore 0m 0m' /* 禁用 XSTOR 中的 minidisk 缓存 */
'cp set srm storbuf 300% 250% 200%' /* 超额分配内存 */
'cp set signal shutdown 180' /* 允许客户机有 3 分钟时间关闭 */
'cp logoff' /* 完成后注销 */

4. 使用 FILE 子命令保存更改。

> 重要提示：set mdc 和 set srm 行是 z/VM 调优值。这些对于 Linux 系统来说可能是良好的起点，但可能不是最优的。要阅读有关这些值的更多信息，请参阅以下网站：
> 
> http://www.vm.ibm.com/perf/tips/linuxperf.html
> 
> http://www.vm.ibm.com/perf/tips/prgmdcar.html

您的系统现在应已配置为启动虚拟交换机并向 Linux 虚拟机发送信号以优雅关闭。

## 验证更改

现在是让这些更改生效的时候了。您可以通过再次重新 IPL 系统或发出刚刚放入 AUTOLOG1 配置文件中的命令来做到这一点。要重新 IPL，请将参数 IPLPARMS CONS=SYS C 传递给 SHUTDOWN REIPL 命令：

```
==> shutdown reipl iplparms cons=sysc
```

虽然您会丢失会话，但它应该在几分钟内恢复。当它恢复后，请执行以下步骤：

- 1. 启动一个 3270 会话并以 MAINT 登录。
- 2. 查询新的 VSWITCH：

```
VSWITCH SYSTEM VSW1 Type: VSWITCH Connected: 0 Maxconn: INFINITE
PERSISTENT RESTRICTED NONROUTER Accounting: OFF
VLAN Unaware
State: Ready
IPTimout: 5 QueueStorage: 8
Portname: UNASSIGNED RDEV: 3024 Controller: DTCVSW1 VDEV: 3024
Portname: UNASSIGNED RDEV: 3028 Controller: DTCVSW2 VDEV: 3028 BACKUP
```

验证 VSWITCH 是否存在，并且有两个内置 VSWITCH 控制器，DTCVSW1 和 DTCVSW2。在 z/VM 5.2 版本之前，这些用户 ID 必须手动创建。

3. 使用 QUERY VDISK 和 QUERY RETRIEVE 命令查看 SYSTEM CONFIG 文件中 Features 语句所做的更改：

```
==> q retrieve
99 buffers available.  Maximum of 255 buffers may be selected.
==> q vdisk userlim
VDISK USER LIMIT IS INFINITE
==> q vdisk syslim
VDISK SYSTEM LIMIT IS INFINITE,          0 BLK IN USE
```

这表明对 SYSTEM CONFIG 文件的更改已生效。

## 设置 DASD

设置 DASD 会将为 Linux 客户机保留的 DASD 上线。涉及两个步骤：格式化 DASD 并将其注册到系统中。

仅格式化您将用于系统分页的额外 DASD。其他打算用于承载客户机操作系统（Linux）的 DASD 将稍后由客户机操作系统本身格式化。

### 格式化 DASD

我们格式化计划用作分页的 DASD。这是通过 CPFMTXA 命令完成的，这是一个用于格式化磁盘的交互式程序。

> z/OS 类比：此 z/OS 的类似命令是运行执行程序 ICKDSF 的批处理作业，并使用适当的参数。
> 
> 在 Linux 中，类似的命令是 mkfs。

要格式化磁盘：

- 1. 使用 ATTACH 命令（缩写为 ATT）将 DASD 附加到我们的用户空间，以便您可以看到它们：
+   att 8228 *
+   DASD 8228 ATTACHED TO MAINT 8228 WITH DEVCTL

- 2. 对每个磁盘使用 CPFMTXA 命令对其进行格式化。请记住将其格式化为 PAGE 卷。示例 4-6 显示了在 CPFMTXA 命令中格式化我们的 PAGE DASD 的交互。用户输入以粗体显示。

- 3. 对每个磁盘重复此过程。

示例 4-6 使用 cpfmtxa 格式化磁盘

```
cpfmtxa
ENTER FORMAT, ALLOCATE, LABEL, OR QUIT:
```

format
ENTER THE VDEV TO BE PROCESSED OR QUIT:
8228
ENTER THE CYLINDER RANGE TO BE FORMATTED ON DISK 8228 OR QUIT:
0-end
ENTER THE VOLUME LABEL FOR DISK 8228:
LX6PG2
CPFM TXA:
FORMAT WILL ERASE CYLINDERS 00000-03338 ON DISK 8228
DO YOU WANT TO CONTINUE? (YES | NO)
yes
HCPCFC6209I INVOKING ICKDSF.
ICK030E DEFINE INPUT DEVICE: FN FT FM, "CONSOLE", OR "READER"
CONSOLE
ICK031E DEFINE OUTPUT DEVICE: FN FT FM, "CONSOLE", OR "PRINTER"
CONSOLE
ICKDSF - CMS/XA/ESA DEVICE SUPPORT FACILITIES 17.0          TIME:
14:09:51
05/14/08      PAGE  1

ENTER INPUT COMMAND:
CPVOL FMT MODE(ESA) UNIT(8228) VOLID(DK8228) NOVFY -
ENTER INPUT COMMAND:
RANGE(0,3338)
ICK00700I DEVICE INFORMATION FOR 8228 IS CURRENTLY AS FOLLOWS:
PHYSICAL DEVICE = 3390
STORAGE CONTROLLER = 3990
STORAGE CONTROL DESCRIPTOR = E9
DEVICE DESCRIPTOR = 0A
ADDITIONAL DEVICE INFORMATION = 44001835
TRKS/CYL = 15, # PRIMARY CYLS = 3339
ICK04000I DEVICE IS IN SIMPLEX STATE
ICK0009II 8228 NED=002105.000.IBM.13.000000022513
ICK091I 8228 NED=002105.000.IBM.13.000000022513
ICK0302I CPVOL WILL PROCESS 8228 FOR VM/ESA MODE
ICK0309OI VOLUME SERIAL = DK8228
ICK03022I FORMATTING THE DEVICE WITHOUT FILLER RECORDS
ICK03011I CYLINDER RANGE TO BE FORMATTED IS 0 - 3338
ICK003D REPLY U TO ALTER VOLUME 8228 CONTENTS, ELSE T
U
ICK030001 CPVOL REPORT FOR 8228 FOLLOWS:

FORMATTING OF CYLINDER 0 STARTED AT: 14:09:51
FORMATTING OF CYLINDER 100 ENDED AT: 14:09:54
FORMATTING OF CYLINDER 200 ENDED AT: 14:09:56
...
FORMATTING OF CYLINDER 3100 ENDED AT: 14:12:07
FORMATTING OF CYLINDER 3200 ENDED AT: 14:12:10
FORMATTING OF CYLINDER 3300 ENDED AT: 14:12:13





FORMATTING OF CYLINDER 3338 ENDED AT: 14:12:14

VOLUME SERIAL NUMBER IS NOW = LX6PG2

CYLINDER ALLOCATION CURRENTLY IS AS FOLLOWS:
TYPE START END TOTAL
--- --- --- ----
PERM 0 3338 3339

ICK00001I FUNCTION COMPLETED, HIGHEST CONDITION CODE WAS 0
14:12:14 05/14/08

ENTER INPUT COMMAND:
END

ICK00002I ICKDSF PROCESSING COMPLETE. MAXIMUM CONDITION CODE WAS 0
ENTER ALLOCATION DATA
TYPE CYLINDERS
................
page 1-end
end
HCPCF6209I INVOKING ICKDSF.
ICK030E DEFINE INPUT DEVICE: FN FT FM, "CONSOLE", OR "READER"
CONSOLE
ICK031E DEFINE OUTPUT DEVICE: FN FT FM, "CONSOLE", OR "PRINTER"
CONSOLE
ICKDSF - CMS/XA/ESA DEVICE SUPPORT FACILITIES 17.0 TIME:
14:14:07
05/14/08 PAGE 1

ENTER INPUT COMMAND:
CPVOL ALLOC MODE(ESA) UNIT(8228) VFY(LX6PG2) -
ENTER INPUT COMMAND:
TYPE((PERM,0,3338))

ICK00700I DEVICE INFORMATION FOR 8228 IS CURRENTLY AS FOLLOWS:
PHYSICAL DEVICE = 3390
STORAGE CONTROLLER = 3990
STORAGE CONTROL DESCRIPTOR = E9
DEVICE DESCRIPTOR = 0A
ADDITIONAL DEVICE INFORMATION = 4A001835
TRKS/CYL = 15, # PRIMARY CYLS = 3339

ICK040001 DEVICE IS IN SIMPLEX STATE
ICK00911 8228 NED=002105.000.IBM.13.000000022513
ICK0911 8228 NED=002105.000.IBM.13.000000022513

ICK030201 CPVOL WILL PROCESS 8228 FOR VM/ESA MODE
ICK03090I VOLUME SERIAL = LX6PG2
ICK03024I DEVICE IS CURRENTLY FORMATTED WITHOUT FILLER RECORDS
ICK003D REPLY U TO ALTER VOLUME 8228 CONTENTS, ELSE T

U
ICK030001 CPVOL REPORT FOR 8228 FOLLOWS:

CYLINDER ALLOCATION CURRENTLY IS AS FOLLOWS:
TYPE      START      END      TOTAL
----      ----      ----      -----
PAGE         1      3338      3338

ICK00001I FUNCTION COMPLETED, HIGHEST CONDITION CODE WAS 0
14:14:42  05/14/08

ENTER INPUT COMMAND:
END

ICK00002I ICKDSF PROCESSING COMPLETE. MAXIMUM CONDITION CODE WAS 0
Ready; T=0.06/0.15 14:14:42

## Registering the disks to the system

格式化 DASD 之后，请确保系统将其识别为可用存储。此信息存储在 SYSTEM CONFIG 文件中。被识别为可用存储的做法类似于（假设设备已在 HCD IOCDS 中定义）发出 VARY xxxx ONLINE 命令，并最终将该命令放入 COMMNDxx 或 PARMLIB 串联中的 IEACMD00，如果在 z/OS 中以 OFFLINE 属性定义，则如此（还必须考虑任何挂载使用属性）。Linux 系统没有等效步骤，因为磁盘在启动时由硬件探测程序发现，并在系统完成启动后自动作为 /dev 下的设备出现。

示例 4-7 使用与您之前使用的相同步骤来访问 MAINT CF1 磁盘读写。记住示例 4-7 中显示的步骤顺序是很有益的。

### Example 4-7 Accessing the MAINT CF1 disk read-write

```
==> q cpdisk
Label Userid Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
MNTCF1 MAINT OCF1 A R/O 530RES 0200 CKD 39 83
MNTCF2 MAINT OCF2 B R/O 530RES 0200 CKD 84 128
MNTCF3 MAINT OCF3 C R/O 530RES 0200 CKD 129 188
==> cprel a
CPRELEASE request for disk A scheduled.
HCPZAC6730I CPRELEASE request for disk A completed.
==> link * cfl cf1 mr
==> acc cf1 f
```

要通过更新 SYSTEM CONFIG 文件来注册磁盘：

- 1. 编辑 SYSTEM CONFIG 文件并按名称指定每个新的页卷（PAGE）为 CP_Owned。当系统 IPL 时，它会将这些识别为分页卷。

```
==> x system config f
...
/**************************************************************/
/*
                CP_Owned Volume Statements
*/
/**************************************************************/

CP_Owned  Slot  1  LX6RES
CP_Owned  Slot  2  LX6SPL
CP_Owned  Slot  3  LX6PAG
CP_Owned  Slot  4  LX6W01
CP_Owned  Slot  5  LX6W02
CP_Owned  Slot  6  LX6PG2
CP_Owned  Slot  7  RESERVED
CP_Owned  Slot  8  RESERVED
CP_Owned  Slot  9  RESERVED
CP_Owned  Slot 10  RESERVED
CP_Owned  Slot 11  RESERVED
CP_Owned  Slot 12  RESERVED
CP_Owned  Slot 13  RESERVED
...
```

- 2. 移至 User_Volume_List 部分。用户卷（PERM）可以用 User_Volume_List 语句单独指定，或用 User_Volume_Include 语句中的通配符指定。添加将由 Linux 客户机使用的用户卷：

```
/**************************************************************/
/*
                User_Volume_List */
/*These statements are not active at the present time. They are */
/*examples, and can be activated by removing the comment delimiters */
/**************************************************************/

USER_VOLUME_LIST <WIA25>
USER_VOLUME_LIST <WIA26>
USER_VOLUME_LIST <WIA27>
USER_VOLUME_LIST <WIA28>
USER_VOLUME_LIST <WIA29>
/* User_Volume_List USRP01 */
/* User_Volume_List USRP02 */
```

- 3. 使用 FILE 子命令保存更改。

- 4. 使用 CPSYNTAX 命令验证更改的完整性，然后将 MAINT CF1 磁盘重新上线。





以下示例展示了你之前是如何执行此操作的：

```
==> acc 193 g
==> cpsyntax system config f
CONFIGURATION FILE PROCESSING COMPLETE -- NO ERRORS ENCOUNTERED.
==> rel f (det
DASD 0CF1 DETACHED
==> cpacc * cfl a
CPACCESS request for mode A scheduled.
HCPZAC67321 CPACCESS request for MAINT's 0CF1 in mode A completed.
==> q cpdis k
Label UserId Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
MNTCF1 MAINT 0CF1 A R/O 520RES 0200 CKD 39 83
MNTCF2 MAINT 0CF2 B R/O 520RES 0200 CKD 84 128
MNTCF3 MAINT 0CF3 C R/O 520RES 0200 CKD 129 188
```

## 验证更改

虽然系统在下次 IPL 时会看到这些更改，但你希望系统现在就能看到更改。你可以通过动态地将 PAGE DASD 添加到 CP 拥有的卷中来实现：

```
define cpown slot 6 LX6PG2
```

Ready; T=0.01/0.01 13:58:38

然后，通过使用 QUERY ALLOC PAGE 命令查看页面空间，如示例 4-8 所示。这类似于 z/OS 中的 DISPLAY ASM 命令和 Linux 的 free 命令。

*示例 4-8 查看新创建的 PAGE 卷。*

```
q alloc page
VOLID RDEV EXTENT START EXTENT END TOTAL PAGES HIGH %
PAGES IN USE PAGE USED
--------------------------
LX6PGAG 1A22 1 3338 600840 0 0 0%
LX6PG2 8228 1 3338 601020 13 51 0%
--------------------------
SUMMARY 1174K 13 1%
USABLE 1174K 13 1%
Ready; T=0.01/0.01 14:40:42
```

要验证 PERM 卷现在是否已联机，请使用 QUERY DASD 命令查询系统所看到的 DASD，如第 183 页的示例 4-9 所示。

```
q dasd
DASD 1A20 CP OWNED LX6RES  78
DASD 1A21 CP OWNED LX6SPL  1
DASD 1A22 CP OWNED LX6PAG  0
DASD 1A23 CP OWNED LX6W01 113
DASD 1A24 CP OWNED LX6W02  4
DASD 1A25 CP SYSTEM NW1A25 0
DASD 1A26 CP SYSTEM NW1A26 0
DASD 1A27 CP SYSTEM NW1A27 0
DASD 1A28 CP SYSTEM NW1A28 0
DASD 1A29 CP SYSTEM NW1A29 0
DASD 8228 CP OWNED LX6PG2 0
Ready; T=0.01/0.01 14:48:20
```

## 创建 Linux MAINT 用户

在启动 Linux 之前，创建一个用户到主机的公共文件，该文件将由你创建的每个 Linux 客户机系统使用。若要启动任意数量的 Linux 客户机，请为每个客户机创建一个引导参数文件（而不是每次都手动处理）。创建引导参数文件的优点是，用于引导 Linux 的文件不会在每个客户机系统用户空间中重复。

以 MAINT 身份登录以继续为安装 Linux 配置 z/VM 系统。如第 140 页“z/VM 用户和密码规划”所述，Linux 管理员 ID 为 LNXMAINT。在对 USER DIRECT 文件进行任何更改以创建其磁盘之前，先复制该文件：

```
==> copy user direct c = direorig = {old d
```

## 为 LNXMAINT 设置小磁盘空间

在虚拟地址 191 处分配一个小的 20 柱面小磁盘，并在虚拟地址 192 处定义一个更大的 300 柱面小磁盘（约 225 MB），供多个客户机共享。你可以使用工作表中指定为 PERM 空间的新 DASD 之一（第 403 页表 B-1），也可以使用 LX6W02 上的任何可用空间（如果你一直按照本书的安装步骤进行，LX6W02 很可能有部分空闲空间），因为小磁盘仅使用 320 个柱面。

> 注：柱面 0 必须始终保留用于标签，因此如果你选择使用其中一个新 DASD，应从柱面 1 开始小磁盘。

要为 LNXMAINT 设置小磁盘空间：

- 1. 编辑 USER DIRECT 文件并在文件底部添加以下用户 ID 定义：

```
==> x user direct c
====> bottom
====> a 6
...
USER LNXMAINT LNXMAINT 64M 128M BEG
INCLUDE IBMDFLT
LINK TCPMAINT 592 592 RR
MDISK 0191 3390 <2050> 0020 <LX6W02> MR READ WRITE MULTIPLE
MDISK 0192 3390 <2070> 0300 <LX6W02> MR ALL WRITE MULTIPLE
*
...
====> file
```

请注意以下关于黑色数字的要点：

- 1 用户 ID LNXMAINT 具有相同的密码；分配给该用户的存储（主内存）默认大小为 64 MB 加上 128 MB 的扩展存储，具有 B、E 和 G 类权限。
- 2 包含名为 IBMDFLT 的配置文件（该文件在 USER DIRECT 文件中更早定义）。
- 3 链接到 TCPMAINT 592 磁盘为只读，以便访问 FTP 和其他 TCP/IP 命令。
- 4 从卷 LX6W02 定义一个大小为 20 柱面的 191 小磁盘。
- 5 从卷 LX6W02 定义一个大小为 300 柱面（约 225MB）的 192 小磁盘，并具有特殊的读密码 ALL，允许任何用户 ID 在无需磁盘密码的情况下进行读访问。
- 6 一个空的注释行是为了更好的可读性。

- 2. 当在 USER DIRECT 文件中添加或修改 MDISK 语句时，始终检查是否有重叠的柱面和间隙（尽管间隙只会留下空磁盘空间，但 z/VM 允许你在同一磁盘空间上定义多个小磁盘，这不一定是有益的）。要检查，请使用 DISKMAP 命令，如“创建磁盘”第 134 页所述：

```
==> diskmap user
The minidisks with the END option specified in this directory will not be included in the following DISKMAP file.

File USER DISKMAP A has been created.
```




创建的文件 USER DISKMAP A 包含 USER DIRECT 文件中定义的所有 minidisk 卷的映射。它列出了卷上发现的任何重叠或间隙。

+   3. 编辑该文件，并用 XEDIT PREFIX OFF 子命令关闭前缀区域，以查看 80 列：

```
==> x user diskmap
===> prefix off
```

+   4. 使用 /（斜杠）子命令搜索 overlap 文本：

```
====> /overlap
```

出现以下消息，表示没有 minidisk 相互重叠：

DMSXDC546E Target not found.

查看文件的其余部分。你的 LNXMAINT 的 minidisk 定义应类似于我们的定义，如图 4-17 所示。请注意，它们定义在 LX6W02 磁盘上，除非你使用的是新 DASD 之一。

| 00236 ------------------------------- |
| 00237 |
| 00238 VOLUME USERID CUU DEVTYPE START END SIZE |
| 00239 LX6W02 $ALLOCS A03 3390 00000 00000 00001 |
| 00240 40ASF40 2D2 3390 00001 00150 00150 |
| 00241 OSAADMIN2 191 3390 00151 00160 00010 |
| <...snip...> |
| 00331 CERON 191 3390 02040 02049 00010 |
| 00332 LNXMAINT 191 3390 02050 02069 00020 |
| 00333 LNXMAINT 192 3390 02070 02369 00300 |

图 4-17 创建 LNXMAINT 后的 USER DISKMAP 文件。

+   5. 使用 QUIT 命令或按 F3 退出 USER DISKMAP 文件。

+   6. 如果你使用了新 DASD 之一，请再次编辑 USER DIRECT 文件，并为你遗漏的那个最开始的柱面添加一个新的 minidisk 定义⁸。这样可以防止系统将其报告为间隙。

以下示例是 USER DIRECT 文件：

```
==> x user direct
===> /user $alloc
USER $ALLOCS NOLOG
MDISK A01 3390 000 001 LX6RES R
```

⁸ 如果你没有遗漏它，那么你可能没有读完第 183 页“为 LNXMAINT 设置 minidisk 空间”开头的注意事项。

```
MDISK A02 3390 000 001 LX6W01 R
MDISK A03 3390 000 001 LX6W02 R
MDISK A04 3390 000 001 <W1A25> R
```

7. 当你确定 minidisk 布局正确后，可以使用 DIRECTXA 命令将 USER DIRECT 文件的更改上线：

```
==> directxa user
z/VM USER DIRECTORY CREATION PROGRAM - VERSION 5 RELEASE 3.0
EOJ DIRECTORY UPDATED AND ON LINE
HCPDIR494I User directory occupies 39 disk pages
```

8. 如果 DIRECTXA 命令失败，你必须在继续之前纠正问题。

现在你已经定义了第一个名为 LNXMAINT 的 z/VM 用户 ID。

在 Linux 中没有与此步骤等效的过程，因为在 Linux 中，用户本身并不像在 z/VM 中那样是一个完整的虚拟机。创建 Linux 用户时，其信息（用户 ID、密码）存储在系统文件中，并在 /home 目录中为其创建主文件夹。

## 登录并定制新的用户 ID

现在你应该能够登录到新的用户 ID 并格式化它的两个 minidisk：

+   1. 从 MAINT 注销，然后登录 LNXMAINT：

```
LOGON LNXMAINT
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0003 RDR,  NO PRT,  NO PUN
LOGON AT 05:41:34 EST THURSDAY 01/04/07
z/VM V5.3.0    2007-11-10 10:07
```

```
DMSACP112S A(191) device error
```

出现一条以 device error 结尾的错误消息。当 CMS 启动时，它会尝试将用户的 191 minidisk 作为文件模式 A 访问。191 minidisk 已定义给此用户 ID，但从未为 CMS 文件系统格式化⁹。

> 注意：仅用于保存 minidisk 的 DASD 不必格式化为 PERM 空间，因为其上的每个 minidisk 稍后都会被格式化。在这种情况下，格式化一个柱面并为其贴上标签就足够了。

⁹ 将 DASD 格式化为 PERM 存储与为 CMS 文件系统格式化用户 minidisk 是不同的。

## 创建 PROFILE EXEC

要创建一个简单的 PROFILE EXEC，以便每次此用户 ID 登录时运行：

+   1. 创建新文件并添加以下行。REXX EXEC 必须始终以 C 语言风格的注释开头。

```
==> x profile exec a
====> a 5
/* PROFILE EXEC */
'acc 592 e'
'cp set run on'
'cp set pf11 retrieve forward'
'cp set pf12 retrieve'
====> file
```

此 PROFILE EXEC 将 TCPMAINT 592 磁盘作为文件模式 E 访问，设置 CP run on（有关 RUN 参数的解释，请阅读第 60 页的“断开连接”部分），并按惯例设置检索键。

你可以向你的配置文件添加更多配置功能。虽然我们在这里没有提及，因为它们与安装步骤本身无关，但你可以在第 230 页的 5.2“运行系统”中看到它们。

+   2. 你可以通过注销并重新登录来测试更改。但是，键入命令 PROFILE 也能达到相同效果。默认情况下，CMS 会尝试将 191 磁盘作为 A 访问，将 192 磁盘作为 D 访问。此外，你应该已将 TCPMAINT 592 磁盘作为 E 访问。要查看你的 minidisk，请使用 QUERY DISK（q disk）命令：

```
==> profile
DMSACP7231 E (592) R/O
==> q disk
LABEL VDEV M STAT CYL TYPE BLKSZ FILES BLKS USED-(%) BLKS LEFT BLK TOTAL
LXM191 191 A R/W 120 i3390 4096 2 9-01 3591 3600
LXM192 192 D R/W 300 i3390 4096 0 11-00 53989 54000
TCM592 592 E R/O 167 i3390 4096 877 8167-68 3893 12060
MNT190 190 S R/O 100 i3390 4096 689 14325-80 3675 18000
MNT19E 19E Y/S R/O 250 i3390 4096 1010 26665-59 18335 45000
MNT191 120 Z R/O 175 i3390 4096 36 224-01 31276 31500
```

+   3. 验证你的 F11 和 F12 键已设置为 RETRIEVE 命令：

```
==> q pf11
PF11 RETRIEVE FORWARD
==> q pf12
PF12 RETRIEVE BACKWARD
```

## 获取 Linux 启动所需的文件

在第 183 页的“为 LNXMAINT 设置 minidisk 空间”一节中，你为 LNXMAINT 用户创建了两个磁盘：191 和 192 磁盘。191 磁盘将用于



用作 LNXMAINT 的主磁盘，其通用文件将存放在此。另一方面，192 磁盘将用于托管 Linux 虚拟机启动所需的所有文件。稍后，在第 193 页的“为 Linux 虚拟机设置通用配置文件”中，你将在 Linux 客户机中设置一个配置文件，该文件将以只读模式将其 191 磁盘链接到 LNXMAINT 的 192 磁盘。通过这样做，客户机的主磁盘可以通过从此链接的 LNXMAINT 磁盘读取来加载必要的 Linux 文件。

> **注意：** 要继续本节，请确保你已在 z/VM 中设置了 FTP 服务器，如第 163 页的“设置 FTP 服务器”中所述。再次强调，通过 FTP 发送文件是必需的，以确保传输保持内核和 ramdisk 文件的 80 字符记录长度。

你必须向你的 LNXMAINT 192 磁盘发送三个文件：

- Linux 内核
  - 在 SLES10 中，这是其第一张 DVD 或 CD 上的 /boot/s390x/vmrdr.ikr 文件
  - 在 RHEL5 中，这是其第一张 DVD 或 CD 上的 /images/kernel.img 文件
- Linux ramdisk
  - 在 SLES10 中，这是其第一张 DVD 或 CD 上的 /boot/s390x/initrd 文件
  - 在 RHEL5 中，这是其第一张 DVD 或 CD 上的 /images/initrd.img 文件
- 位于压缩文件中找到的 SWAPGEN 文件：
  ftp://www.redbooks.ibm.com/redbooks/SG246695/

> **注意：** 如果你的内核和 ramdisk 不是 80 字符记录长度，内核将无法加载。

作者获得了 SLES10SP2 和 RHEL5 U1 仓库的访问信息。由于我们必须选择一个作为此处示例的基础，我们决定使用 SLES。但是，当需要不同步骤或配置时，会突出显示 RHEL 系统的注释。

将这三个文件放在桌面上的同一目录中（你用于连接大型机的机器）并使用 FTP 客户端连接到服务器，如示例 4-10 所示。确保此时已注销 LNXMAINT，否则你的 FTP 客户端无法以读写模式访问磁盘。

## 示例 4-10 通过 FTP 将文件发送到 LNXMAINT 的 192 磁盘

```
# ftp <9.12.4.89> []
Connected to 9.12.4.89.
```

220-FTPSERVE IBM VM Level 530 at VMLINUX6.ITSO.IBM.COM, 16:33:09 EDT
THURSDAY 2008-05-15
220 Connection will close if idle for more than 5 minutes.
Name (9.12.4.89:root): lnxmaint 2a
331 Send password please.
Password:lnxmaint 2b
230 LNXMAINT logged in; working directory = LNXMAINT 191
Remote system type is z/VM.
ftp> cd lnxmaint.192 3
250 Working directory is LNXMAINT 192
ftp> put swapgen.exec 4
local: swapgen.exec remote: swapgen.exec
500 Unknown command, 'EPSV'
227 Data transfer will passively listen to 9,12,4,89,4,7
125 Storing file 'swapgen.exec'
100% |******************************************| 16750  14.60 MB/s
--:-- ETA
250 Transfer completed successfully.
16750 bytes sent in 00:00 (1.74 MB/s)
ftp> bin 5
200 Representation type is IMAGE.
ftp> site fix 80 6
200 Site command was accepted.
ftp> put vmrdr.ikr sles10s2.ikr 7
local: vmrdr.ikr remote: sles10s2.ikr
227 Data transfer will passively listen to 9,12,4,89,4,8
125 Storing file 'sles10s2.ikr'
100% |******************************************| 5904 KB  4.48 MB/s
00:00 ETA
250 Transfer completed successfully.
6042680 bytes sent in 00:01 (4.39 MB/s)
ftp> put initrd sles10s2.initrd 8
local: initrd remote: sles10s2.initrd
227 Data transfer will passively listen to 9,12,4,89,4,9
125 Storing file 'sles10s2.initrd'
100% |******************************************| 8067 KB  3.32 MB/s
00:00 ETA
250 Transfer completed successfully.
8261468 bytes sent in 00:02 (3.28 MB/s)
ftp> quit 9
221 Quit command received. Goodbye.

> 注意：REXX 可执行文件必须以 C 风格注释 /* */ 开头，如示例所示。

## 示例 4-11 加载 Linux 内核的脚本

```
/* EXEC punches sles10 sp2 kernel/ramdisk to reader and ipls it */

'cp spool pun *'
'cp close rdr'
'pur rdr all'
'pun sles10s2 ikr * (NOH'
'pun userid() parmfile * (NOH' 1
'pun sles10s2 initrd * (NOH'
'ch rdr all keep'
'ipl 00c clear'
```

你距离拥有 Linux 启动所需的所有文件仅一步之遥。事实上，你缺少的是示例 4-11 的加载脚本中用数字 1 表示的文件。

为了节省时间和输入，创建一个包含你将需要执行 SLES10 基于网络的安装的所有引导参数的文件。诸如 Linux 客户机将使用的 IP 地址、网络掩码、服务器仓库 URL 等信息可以放在单个文件中，并在引导时由 YaST10 读取。由于此信息特定于你创建的每个 Linux 客户机，你应该将此文件命名为：

<LINUX_GUEST> PARMFILE D

字符串 <LINUX_GUEST> 是将托管 Linux 系统的 z/VM 用户的名称。

请注意，示例 4-11 中标记为 1 的指令使用了 userid() REXX 命令来推导出完整的文件名。这意味着每个用户在从其 Linux 客户机环境中运行此脚本时都会加载不同的参数文件。

目前，你还没有 Linux 客户机的用户，因为你将在第 195 页的“创建第一个 Linux 虚拟机”部分中创建它。现在，你唯一需要做的就是将此参数文件命名为你打算赋予 Linux 客户机用户的名称。在我们的示例中，我们对 Linux 客户机使用 LNXCER。参见第 193 页的示例 4-12。

> 10 YaST 代表 Yet another Setup Tool，是 SLES 的安装程序。





### 示例 4-12 Linux 客户机 LNXCER 的引导参数文件

```
ramdisk_size=65536 root=/dev/ram0 ro init=/linuxrc TERM=dumb
hostip=<9.12.5.65> hostname=<ceron>
gateway=<9.12.4.1> netmask=<255.255.254.0>
broadcast=<9.12.7.255> layer2=0
readchannel=0.0.0600 writechannel=0.0.0601 datachannel=0.0.0602
nameserver=<9.12.6.7> portname=dontcare
install=<ftp://totibim:itso@9.12.4.69/code/sles10x>
instnetdev=osa osainterface=qdio osamedium=eth Manual=0
usessh=1 sshpassword=letmein
```

请确保将 \<value\> 条目替换为根据附录 B “规划工作表”第 403 页上的规划工作表与你的资源相对应的值。另外，请不要忘记用粗体突出显示的最后一行，因为在本书中我们指导你执行 SLES10 的 SSH 安装。

## 为 Linux 虚拟机设置通用配置文件

要使所有 Linux 客户机都能看到你为 LNXMAINT 创建的 192 磁盘，其中包含引导的全部通用文件，你有两个选择：

- 费力的方法是在 MAINT 的 USER DIRECT 文件中为每个用户描述添加一个 LINK 语句。

- 更简单的方法是基于默认配置文件创建一个配置文件并添加链接语句的正确行。然后，要使用它们，在创建 Linux 客户机用户时，只需导入此新配置文件即可。

我们的示例当然基于第二种方法。

要使用更简单的方法使所有 Linux 客户机生效：

- 1. 登录到 MAINT 并编辑 USER DIRECT 文件：

    ```
    ==> x user direct c
    ```

在 USER DIRECT 文件中，你可以将对许多用户定义通用的语句分组到一个称为配置文件的结构中。然后可以通过使用 INCLUDE 语句使该配置文件成为用户定义的一部分。你在定义 LNXMAINT 用户时使用了现有的配置文件 TCPCMSU。

- 2. 创建一个名为 LNXDFLT 的新配置文件。它将包含对所有 Linux 用户 ID 通用的用户目录语句。为了减少输入，使用 “*” 前缀命令复制应在第 37-50 行的 IBMDFLT 配置文件：

    ```
    00037 **************************************************
    00038 *
    00039 PROFILE IBMDFLT
    00040  SPOOL 000C 2540 READER *
    00041  SPOOL 000D 2540 PUNCH A
    00042  SPOOL 000E 1403 A
    00043  CONSOLE 009 3215 T
    00044  LINK MAINT 0190 0190 RR
    00045  LINK MAINT 019D 019D RR
    00046  LINK MAINT 019E 019E RR
    00047  LINK MAINT 0402 0402 RR
    00048  LINK MAINT 0401 0401 RR
    00049  LINK MAINT 0405 0405 RR
    00050 *******************************
    ```

- 3. 通过删除三个 LINK MAINT 040x 行并插入示例 4-13 中用粗体文本显示的行来编辑复制的配置文件。参见示例后的说明。

### 示例 4-13 配置文件 LNXDFLT

```
PROFILE LNXDFLT
IPL CMS
MACHINE ESA 4
CPU 00 BASE
CPU 01
NICDEF 600 TYPE QDIO LAN SYSTEM VSW1
SPOOL 000C 2540 READER *
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
LINK MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
LINK MAINT 019E 019E RR
LINK LNXMAINT 192 191 RR
LINK TCPMAINT 592 592 RR
```

示例说明：

- 1 用户 ID 登录时 IPL CMS。
- 2 将机器标识为类型 ESA，最多可定义 4 个 CPU。
- 3 定义基本 CPU。
- 4 定义第二个 CPU；如果你的 LPAR 只有一个 Real IFL/CP，则不要包含此项。
- 5 定义一个连接到从虚拟地址 600 开始的 VSWITCH 的虚拟 NIC。
- 6 提供对 LNXMAINT 192 磁盘的读取访问，作为用户的 191 磁盘。
- 7 提供对 TCPMAINT 592 磁盘的读取访问，以便用户可以访问 TCPIP 服务，例如 FTP 客户端。

- 4. 保存文件：

    ```
    ====> file
    ```

## 创建第一个 Linux VM

在第 2.2.1 节“z/VM 历史”第 14 页的虚拟化讨论中，要创建 Linux 可以运行的虚拟机，你所要做的就是创建一个 z/VM 用户。首先要做的是设置用户最小磁盘。

### 设置最小磁盘

为你的 Linux 客户机创建一个新用户，并以与“为 LNXMAINT 设置最小磁盘空间”第 183 页中为 LNXMAINT 用户所做的方式完全相同的方式设置其最小磁盘。以 MAINT 身份登录并在 USER DIRECT C 文件中添加新的用户定义。这是你要包含在“为 Linux 虚拟机设置通用配置文件”第 193 页中创建的 LNXDFLT 配置文件的第一个用户。示例 4-14 显示了你可以使用的模板。

### 示例 4-14 创建 Linux 客户机用户。

```
user <lnxcer> <lnxcer> 512M 2G BDEG
include lnxdflt
option lnknopas applmon
mdisk 100 3390 0001 3338 <nwla25> mr lnx4vm lnx4vm lnx4vm
mdisk 103 3390 0001 3338 <nwla26> mr lnx4vm lnx4vm lnx4vm
mdisk 104 3390 0001 3338 <nwla27> mr lnx4vm lnx4vm lnx4vm
mdisk 105 3390 0001 3338 <nwla28> mr lnx4vm lnx4vm lnx4vm
mdisk 106 3390 0001 3338 <nwla29> mr lnx4vm lnx4vm lnx4vm
```

该示例将此 Linux 用户 ID 定义为具有以下最小磁盘和虚拟磁盘：

- 100 用于保存 /boot 分区的最小磁盘；剩余空间分配给系统 LVM，所有其他分区都将位于其中。有关 Linux LVM 的更多信息，请参阅第 307 页的“Linux 逻辑卷管理器”。
- 101-102 这些是由 SWAPGEN EXEC 在登录时创建的虚拟磁盘（VDISK）交换空间。它们未在 USER DIRECT 中定义，而是在用户登录时在用户的 PROFILE EXEC 中动态定义。
- 103-106 这些最小磁盘将由 Linux 系统 LVM 管理。





> **重要提示：** 最小化的 Linux 客户机系统可装入单个 3390-3 DASD，且这是业界推荐的做法。此做法要求你不要使用 GNOME 或 KDE 窗口管理器，以保持安装系统的小尺寸。我们的示例并未这样做，因为我们想展示 LVM 和 KDE 的使用。

为避免在每个用户卷上报告一个柱面间隙，请使用用户 ID `$ALLOC$`。该用户被设置为 NOLOG，这意味着它永远无法登录。因此，它不是一个常规用户 ID，而是一个方便的位置，用来放置所有 PERM 卷的柱面 0 的虚拟 minidisk 定义。用户 ID `$ALLOC$` 位于 USER DIRECT C 的开头，接近第 100 行。为每个卷包含一个定义，如示例 4-15 所示。

### 示例 4-15 避免报告 1 柱面间隙

```
00104 *
00105 USER $ALLOC$ NOLOG
00106 MDISK A01 3390 000 001 LX6RES R
00107 MDISK A02 3390 000 001 LX6W01 R
00108 MDISK A03 3390 000 001 LX6W02 R
00109 MDISK A04 3390 000 001 <NW1A25> R
00110 MDISK A05 3390 000 001 <NW1A26> R
00111 MDISK A06 3390 000 001 <NW1A27> R
00112 MDISK A07 3390 000 001 <NW1A28> R
00113 MDISK A08 3390 000 001 <NW1A29> R
00114 *
```

## 更新 autolog 配置文件

你定义的新 Linux ID 必须能够访问 VSWITCH。为使其在系统 IPL 时自动生效，请将带有 GRANT 参数的 `SET VSWITCH` 命令添加到 AUTOLOG1 的 PROFILE EXEC 中。此外，还可以为你的 Linux 用户 ID 添加一个 XAUTOLOG 语句，以便在 z/VM IPL 时自动登录。

要实现这些操作，请以 MAINT 登录并确保你的 AUTOLOG1 配置文件看起来像示例 4-16 所示。

### 示例 4-16 授予用户访问虚拟交换机的权限

```
=> link autolog1 191 1191 mr
=> acc 1191 f
=> x profile exec f // add two lines
/*********************/
/* Autolog1 Profile Exec */
/*********************/
'cp xautolog tcpip'                  /* start up TCPIP */
'CP XAUTOLOG DTCVSW1'                /* start VSWITCH controller 1 */
'CP XAUTOLOG DTCVSW2'                /* start VSWITCH controller 2 */
'cp set pf12 ret'                    /* set the retrieve key */
'cp set mdc stor 0m 128m'            /* Limit minidisk cache in CSTOR */
'cp set mdc xstore 0m 0m'            /* Disable minidisk cache in XSTOR */
'cp set srm storbuf 300% 250% 200%'  /* Overcommit memory */
'cp set signal shutdown 180'        /* Allow guests 3 min to shut down */

/* Grant access to VSWITCH for each Linux user */
'cp set vswitch vsw1 grant <lnxcer>'

/* XAUTOLOG each Linux user that should be started */
'cp xautolog <lnxcer>'

'cp logoff'                          /* logoff when done */
====> file
```

这些更改要到下一次 IPL 才会生效，因此你必须为本次 z/VM 会话授予该用户 ID 访问 VSWITCH 的权限。这可以通过以下命令作为 MAINT 用户运行来完成：

```
==> set vswitch vsw1 grant <lnxcer>
Command complete
```

## 设置 Linux 客户机配置文件

这是你在客户机系统上首次运行 Linux 之前的最后一步。客户机配置文件应在你创建的客户机之间保持一致，因此最好的位置是放在 LNXMAINT 的 192 磁盘中，该磁盘由你在“设置 Linux VM 的通用配置文件”第 193 页中创建的 lnxdf1 配置文件映射为这些客户机的 A 文件模式。

以 LNXMAINT 登录并修改 PROFILE EXEC D 文件，使其看起来像示例 4-17。

### 示例 4-17 Linux 客户机配置文件

```
/* PROFILE EXEC */
'CP SET RUN ON'
'CP SET PF11 RETRIEVE FORWARD'
'CP SET PF12 RETRIEVE'
'ACC 592 C'
'SWAPGEN 101 524288'
'SWAPGEN 102 1048576'
'PIPE CP QUERY' userid() ' | var user'
parse value user with id . dsc .
ipldisk=100
if (dsc = 'DSC') then
'CP IPL' ipldisk
else
do
say 'Want to ipl Linux from DASD' ipldisk'? y/n'
parse upper pull answer .
if (answer = 'Y') then
'CP IPL' ipldisk
end
```

请回顾示例中编号语句的以下方面：

- 1, 2 这些行每次虚拟机启动时都会创建交换空间作为磁盘 101 和 102，供 Linux 使用。

> **注意：** 根据你的客户机系统的用途，定义尽可能少的交换空间。这样可以优化你的 z/VM 系统存储管理。在我们的示例中，我们使用了 512 MB 和 1 GB，因为我们不担心性能或内存限制。

- 3 该语句使用存储在 DSC 变量中的解析值来检查该用户是否正在自动登录。如果是这种情况，则脚本将 IPL 磁盘 100 中的内容，即 Linux 映像在安装后应位于的位置。

- 4 如果之前的检查得出结论用户实际上执行了普通登录，则脚本会询问你是否要从磁盘 100 IPL Linux。

我们现在将 Linux 安装到我们的客户机上。以你的 Linux 客户机用户登录并按 Enter 运行客户机的配置文件。输出将类似于第 199 页图 4-19 中的输出。





```
00: ipl cms
z/VM V5.3.0    2008-05-06 13:40

DMSACP7231 A (191) R/O
DMSACP7231 C (592) R/O
DIAG swap disk defined at virtual address 101 (64989 4K pages of swap space)
DIAG swap disk defined at virtual address 102 (129981 4K pages of swap space)
Want to ipl Linux from DASD 100? y/n
n
Ready; T=0.01/0.04 09:49:42
```

Figure 4-19 Logging in as the Linux guest user

注意交换空间是自动生成的，正如我们前面提到的。另请注意，由于这不是自动登录，系统会提示你是否从磁盘 100 IPL。回答否（n），因为 Linux 映像尚未安装到磁盘 100 上。

## 4.4.2 Booting the Linux kernel for installation

由于你之前花费时间配置了一个通用的 Linux 用户 ID（LNXMAINT），现在要开始 Linux 安装，你所要做的就是调用你在第 191 页“Linux 内核加载器脚本和引导参数文件”中创建的 SLES10S2 EXEC 脚本。图 4-20 在第 200 页显示了如何调用它以及 Linux 内核开始运行之前的输出结果。

```
Ready; T=0.01/0.04 09:49:42
sles10s2
00: 0000003 FILES PURGED
00: RDR FILE 0043 SENT FROM LNXCER PUN WAS 0043 RECS 076K CPY 001 A NOHOLD NOKEEP
00: RDR FILE 0044 SENT FROM LNXCER PUN WAS 0044 RECS 0009 CPY 001 A NOHOLD NOKEEP
00: RDR FILE 0045 SENT FROM LNXCER PUN WAS 0045 RECS 103K CPY 001 A NOHOLD NOKEEP
00: 0000003 FILES CHANGED
00: 0000003 FILES CHANGED
Linux version 2.6.16.21-0.8-default (geeko@buildhost) (gcc version 4.1.0 (SUSE Linux)) #1 SMP Mon Jul 3 18:25:39 UTC 2006
We are running under VM (64 bit mode)
Detected 2 CPU's
Boot cpu address 0
Built 1 zonelists
Kernel command line: ramdisk_size=65536 root=/dev/ram1 ro init=/linuxrc TERM=dumb hostip=9.12.5.65 hostname=ceron gateway=9.12.4.1 netmask=255.255.254.0 broadcast=9.12.7.255 layer2=0 readchannel=+0.0.0600 writechannel=+0.0.0601 datachannel=+0.0.0602 nameserver=9.12.6.7 portname=dontcare install=ftp://totibmx.itsoso9.12.4.69/code/sles10x instnetdev=osa osainterface=qdio osamedium=eth Manual=0 usessh=1 sshpassword=letmein
PID hash table entries: 4096 (order: 12, 131072 bytes)
Dentry cache hash table entries: 131072 (order: 8, 1048576 bytes)
Inode-cache hash table entries: 65536 (order: 7, 524288 bytes)
Memory: 496640K/524288k available (4298k kernel code, 0k reserved, 1401k data, 196k init)
Security Framework v1.0.0 initialized
Mount-cache hash table entries: 256
checking if image is initramfs... it is
Freeing initrd memory: 8067k freed
cpu 0 phys_idx=0 vers=FF ident=04DE50 machine=2097 unused=8000
cpu 1 phys_idx=1 vers=FF ident=04DE50 machine=2097 unused=8000
Brought up 2 CPUs
migration_cost=1000
NET: Registered protocol family 16
debug: Initialization complete
TC classifier action (bugs to netdev@vger.kernel.org cc hadi@cyberus.ca)
```

Figure 4-20 Booting the Linux kernel for installation.

此时，你的 Linux 内核已经启动并运行，ramdisk 正在负责从你的服务器存储库下载安装阶段 2 文件。该阶段 2 文件实际上包含安装程序本身，SLES10 的情况下是 YaST。由于我们选择通过 SSH 安装，引导时会显示类似于图 4-21 的消息。

```
setting root pwd to 'letmein'
Starting SSH daemon ...

eth0: <BROADCAST,MULTICAST,UP> mtu 1492 qdisc pfifo_fast qlen 1000
link/ether 02:00:01:00:00:02 brd ff:ff:ff:ff:ff:ff
inet 9.12.5.65/23 brd 9.12.5.255 scope global eth0
inet6 fe80::200:100:400:2/64 scope link
    valid_lft forever preferred_lft forever

*** sshd has been started ***

*** login using 'ssh -X root@ceron' ***
*** run 'yast' to start the installation ***
```

Figure 4-21 YaST ready for an SSH Installation

我们选择 SSH 而不是 IBM Connection 终端的原因是，SSH 连接可以在安装向导期间刷新窗口，而且是一个彩色的控制台。

> Note: Read z/VM and Linux on IBM System z: The Virtualization Cookbook for SLES9, SG24-6695 for a graphical installation of SLES10 by using a VNC client.

要继续安装，请打开到 Linux 客户机的 SSH 连接（你可以使用 Linux ssh 命令来完成此操作，如果你在 Windows 中，也可以使用 SSH 客户端，例如 PuTTY）。以 root 身份登录，并使用在安装期间保护 root 用户而定义的 letmein 密码。登录后，输入 yast 以启动安装。

> Note: You will be prompted to set the real root password of your system later during the installation. Do not be concerned about having a weak root password while installing the system.





## 开始 YaST 安装

当 YaST 在您的 SSH 连接上联机时，它将引导您完成安装向导。请执行以下步骤：

提示：Tab 键可在菜单条目中向前循环。Escape+Tab 组合键可在菜单条目中向后循环。空格键可在复选框和选择框的打开之间切换。

正在运行的安装程序是 yast2。

要开始 YaST 安装：

- 1. 选择语言，English（英语），（或您的语言），然后单击“下一步”。
- 2. 将打开 SLES10 SP2 许可协议窗口。如果您同意，请选择“是，我同意许可协议”，然后单击“下一步”。
- 3. 将打开“磁盘激活”窗口。选择“配置 DASD 磁盘”。
- 4. 将打开 YaST2 DASD 磁盘管理窗口，显示您的 Linux 客户机可用的所有 DASD，包括您的客户机用户自身使用但并非用于托管 Linux 的 z/VM 磁盘，例如其 191 磁盘。

仅使用 100-106 磁盘进行您的 Linux 安装，因为这就是您为其设置的内容。在窗口中：

a. 突出显示每个磁盘，并单击“选择”或“取消选择”以选择它；或者在突出显示某个磁盘时直接按 Enter。所选磁盘旁边会出现“是”字样。
b. 通过选择“执行操作 → 激活”，为您即将安装的 Linux 激活所选磁盘，如图 4-22（第 203 页）所示。

图 4-22 客户机系统可用的 DASD

c. 不用于交换的磁盘必须格式化，以便 Linux 可以使用它们。取消选择磁盘 101 和 102，以便为 Linux 映像保留的其他磁盘保持选中状态。

选择“执行操作 → 格式化 → 激活”，如图 4-23（第 204 页）所示。

## 图 4-23 选择用于 Linux 格式化的 PERM 卷

- 5. 在提示您选择一个并行格式化磁盘的窗口中，单击“确定”。
- 6. 对“确实要格式化以下磁盘吗？”这个问题单击“是”。

进度指示窗口将显示进度（参见第 205 页的图 4-24）。此步骤可能需要 5-15 分钟，具体取决于通道类型和磁盘速度。

![](img/b0a4b9056f819dccd4781a5105c92d45_219_0.png)

![](img/b0a4b9056f819dccd4781a5105c92d45_220_0.png)

图 4-24 DASD 格式化

- 7. 格式化完成后，单击“下一步”，然后在“磁盘激活”窗口中再次单击“下一步”。
一个窗口将提示您选择安装模式。
- 8. 选择“新安装”，然后单击“下一步”。
将打开“时钟和时区”窗口。
- 9. 选择您的时区，设置时钟，然后单击“下一步”。
将打开“安装设置”窗口。
- 10. 单击“分区”。
将打开“专家分区器”窗口，如第 206 页的图 4-25 所示。

## 专家分区器

对于 SCSI 磁盘上的根文件系统，请在 DASD 上添加一个 /boot 分区用于 IPL。

右侧的表格显示了所有硬盘上的当前分区。在最后一个安装对话框中确认整个安装之前，不会向硬盘写入任何内容。在此之前，您可以安全地中止安装。

| 设备 | ID | 大小 | F | 类型 | 挂载点 |
|---|---|---|---|---|---|
| /dev/dasda | () | 2.2 GB | | IBM-DASD | |
| /dev/dasdb | () | 256.0 MB | | IBM-DASD | |
| /dev/dasdb1 | | 253.8 MB | | Linux 原生 | swap |
| /dev/dasdc | () | 512.0 MB | | IBM-DASD | |
| /dev/dasdc1 | | 507.7 MB | | Linux 原生 | swap |
| /dev/dasdd | () | 2.2 GB | | IBM-DASD | |
| /dev/dasde | () | 2.2 GB | | IBM-DASD | |
| /dev/dasdf | () | 2.2 GB | | IBM-DASD | |
| /dev/dasdg | () | 2.2 GB | | IBM-DASD | |

[创建] [编辑] [删除] [dasdfnet]
[LVM...] [EVMS...] [RAID...v] [专家...v]
[ 返回 ] [ 中止 ] [ 完成 ]

图 4-25 创建 Linux 分区

我们使用 LVM 将五个 DASD 连接在一起，使它们在 Linux 中显示为单个 10 GB 磁盘。通过这种方式，我们可以创建 Linux 分区（如 /home），以扩展到多个磁盘并增长到我们想要的大小。但是，其中一个分区必须留在 LVM 之外，以便系统可以引导：即 /boot 分区。

> 注意：我们建议您彻底阅读以下有关 LVM 的文章，以了解磁盘性能优化和卷管理：
> ► http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_optimizedisk.html
> ► http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_volMan.html
> 
> 重要：一个精简的 Linux 客户机系统可以放在单个 3390-3 DASD 上，这是实际工作中的推荐做法。这种做法要求不使用 GNOME 或 KDE 窗口管理器，以保持安装的系统小巧。我们的示例没有这样做，因为我们要展示 LVM 和 KDE 的使用。





- 11. 单击 Create。因为 /dev/dasda 没有分区，所以会打开“在 /dev/dasda 上创建主分区”窗口，类似于图 4-26。

  ![](img/b0a4b9056f819dccd4781a5105c92d45_222_0.png)

  图 4-26 在 LVM 外创建引导分区

  在窗口中：

  - a. 选择 Format（会插入一个 x）。
  - b. 将文件系统选择为 ext3

  > 重要提示：作者建议不要使用 ReiserFS（一种替代的高级文件系统），因为文件结构树可能会损坏，这将迫使你运行 fsck --rebuild-tree 命令，这是一项耗时且危险的任务。关于文件系统类型的讨论，请参阅以下链接中的日志文件系统讨论：
  > http://www.ibm.com/developerworks/linux/linux390/perf/tuning_res_journaling.html

  - c. 将第一个柱面设为 0（零）。对于结束柱面，使用 +64M 来表示你想要一个 64 MB 大小的分区。因为 /boot 只能容纳内核、ramdisk 和引导加载程序文件，所以这对于它来说已经绰绰有余了。它也足以容纳四到五个不同的内核和 ramdisk 镜像。
  - d. 选择挂载点为 /boot。
  - e. 单击 OK。

- 12. 在 dasda 上重复相同的操作创建另一个分区。

  起始柱面显示为下一个可用的柱面。确保结束柱面为最后一个可用柱面（对于 3390-3 DASD 为 3337），并为其选择空的挂载点（挂载点选择框中的最后一个选项）。

  对其他磁盘重复此步骤，除了 dasdb 和 dasdc 因为它们是交换空间。确保你创建的分区使用这些磁盘的所有空间。你可以暂时安全地忽略要求你创建根分区（/）的警告。此步骤的目标只是使系统能够在每个其他磁盘上看到一个 Linux Native 分区，否则 LVM 将无法使用它们。

  完成此步骤后，Expert Partitioner 窗口看起来类似于图 4-27。

  ![](img/b0a4b9056f819dccd4781a5105c92d45_223_0.png)

  图 4-27 应用 LVM 之前的分区

- 13. 单击 LVM 以继续并创建 LVM。

- 14. 对于 LVM，选择一个卷组名称和物理扩展大小。我们建议你使用 YaST 为你提供的默认值。单击 OK 以继续。

  你剩余的所有分区都显示在列表中。

- 15. 通过突出显示它并按 Enter 或单击 Add Volume，将每个剩余分区添加到 LVM。你的窗口看起来类似于图 4-28 所示的状态。

  ![](img/b0a4b9056f819dccd4781a5105c92d45_224_0.png)

  图 4-28 创建 LVM

- 16. 单击 Next 以继续。

  LVM 逻辑卷管理窗口显示你创建的 /boot 分区和两个交换分区。在上一步中你创建了一个逻辑组，可以理解为创建了一个逻辑磁盘，或在 z/VM 术语中为 DASD。

  你现在必须在逻辑组内部创建逻辑卷。逻辑卷只不过是 Linux 分区，例如 /、/home、/var 等。将逻辑卷视为 z/VM minidisks。

- 17. 单击 Add。Create Logical Volume 窗口显示，类似于第 210 页的图 4-29。

Create Logical Volume

| 字段 | 值 |
| --- | --- |
| 逻辑卷名称 | root |
| 大小：（例如，4.0 GB 210.0 MB） | 8.0 GB<br>max = 11.3 GB [max] |
| 条带 | 1 |
| 条带大小 | 64 |
| Fstab 选项 | [ ] |
| 挂载点 | / |
| 按钮 | [OK] [Cancel] |

图 4-29 创建根分区

- 18. 执行以下步骤：

  - a. 将卷格式化为 ext3。
  - b. 为其指定有意义的逻辑卷名称。由于这将是我们的根分区，我们将其命名为 root。
  - c. 设置其大小。我们在这里使用 8GB，因为我们打算稍后创建一个大约 3GB 的 /home 分区。
  - d. 使用条带的默认值，除非你想根据我们提供的 LVM 参考中前面所述的内容优化系统性能。
  - e. 选择 / 作为挂载点。
  - f. 单击 OK。

- 19. 重复上一步以创建 /home 分区。将其卷命名为 home。在为其设置空间时，单击 [max] 按钮，以使用卷组中剩余的所有空间。

  完成此步骤后，窗口类似于第 211 页的图 4-30。





## Logical Volume Manager: Logical Volumes

卷组系统可用大小：84.0 MB

在此处创建用于存储数据的逻辑卷。逻辑卷几乎可以在任何普通磁盘分区可用的地方使用。您可以在逻辑卷上创建文件系统并使用它们，例如用作交换分区或作为数据库的原始分区。如果卷组中仍有未分配的物理存储并且您使用 reiserfs 作为您的

| 设备 | 挂载点 | 卷组 | 大小 |
|---|---|---|---|
| /dev/dasda1 | /boot |  | 64.6 MB Lin |
| /dev/dasdb1 | swap |  | 253.8 MB Lin |
| /dev/dasdc1 | swap |  | 507.7 MB Lin |
| /dev/system/home | /home | system | 3.3 GB |
| /dev/system/root | / | system | 8.0 GB |

[x] 查看所有挂载点，而不仅仅是当前卷 [Add] [Edit] [Remove] [Back] [Abort] [Next]

图 4-30 LVM 布局

- 20. 点击 Next 继续进入主分区菜单。
- 21. 点击 Finish 退出主分区菜单。

您现在返回到主向导。

## 继续 YaST 安装

在主向导中，选择要安装的软件包：

- 1. 选择 Change → Software
- 2. 通过点击 Filter 选择框按模式过滤软件包。
- 3. 选择您想要安装的任何模式。因为我们提供了通过 VNC 连接连接到 KDE 环境的示例，所以我们取消选择 GNOME 桌面环境并选择 KDE。完成后点击 OK。
- 4. 点击 Accept 返回到安装向导。

根据您在上一步中选择的模式（通过过滤）列出了计划安装的软件包。

根据所选模式，您可能需要接受某些依赖项。如果发生这种情况，请点击 OK 返回到安装向导。

- 5. 点击 Accept 开始安装。会显示确认窗口。
- 6. 点击 Install。安装开始，您可以观看其进行。

## 从磁盘启动您的新 Linux 系统

安装的第一部分完成后，您的 Linux 系统将关闭。返回到您的 z/VM 3270 会话。从磁盘 IPL 新安装的系统以继续安装。

### 从磁盘启动您的新 Linux 系统：

- 1. 观察系统关机时出现的以下消息：

```
Power down.
00: HCPGSP2629I The virtual machine is placed in CP mode due to a SIGP stop from CPU 01.
01: HCPGSP2630I The virtual machine is placed in CP mode due to a SIGP stop and store status from CPU 01.
```

- 2. 启动新内核：使用命令 ipl 100 IPL 磁盘（其中 100 是引导记录的磁盘地址）：

```
==> ipl 100
00: ZIPL v1.6.3 interactive boot menu
00:
00: 0. default (ipl)
00:
00: 1. ipl
00: 2. failsafe
00: 3. ipl
00: 4. failsafe
00:
00: Note: VM users please use '#cp vi vmsg <number> <kernel-parameters>'
00:
00: Please choose (default will boot in 10 seconds):
```

- 3. 在此提示下，要么等待 10 秒让默认 IPL 继续进行，要么如果您打字足够快，请尝试输入以下命令：

```
#cp vi vmsg 0
```

安装程序再次启动 SSH 服务器，如图 4-31 第 213 页所示，以便您可以开始完成安装。

```
*** sshd has been started ***

you can login now and proceed with the installation
run the command '/usr/lib/YaST2/startup/YaST2.ssh'

active interfaces:

eth0      Link encap:Ethernet  HWaddr 02:00:01:00:00:02
          inet addr:9.12.5.65  Bcast:9.12.5.255  Mask:255.255.254.0

--
lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
```

图 4-31 首次启动时的 YaST 消息。

## 完成 YaST 安装

返回在“Beginning a YaST installation”第 202 页所述的用于安装第一部分的同一 SSH 客户端。

### 完成安装：

- 1. 使用与首次启动 YaST 时相同的 SSH 密码（本例中为 letmein）登录。
  会打开设置 root 密码的窗口。
- 2. 输入您的 root 密码两次并点击 Next。不要忘记此密码！
  您看到的第一个窗口可能与上次看到的类似：软件包安装。然而，根据您的模式选择，该窗口可能已完成，而显示的是“主机名和域名”窗口。
- 3. 输入所需的值，在本例中 ceron 是主机名，itso.ibm.com 是域名。除非您环境中当然有一个 DHCP 服务器，取消选中 Change Hostname via DHCP 复选框。
- 4. 点击 Next。会显示网络配置窗口。
- 5. 在 Firewall is enabled 中，点击单词 enabled 将其更改为 disabled。
- 6. 通过点击 Change → VNC Remote Administration 启用 VNC 远程管理。所有其他值应正确，因此点击 Next。





> 警告：禁用防火墙不是一个好的做法。我们之所以这样做，是为了简化示例。之后，您应该激活防火墙并阻止您不希望系统为其提供传入连接的服务的端口。

测试 Internet 连接窗口打开。

- 7. 选择 否，跳过此测试 并点击 下一步。
- 8. 在 安装设置 窗口中，选择 跳过配置 并点击 下一步。
- 9. 在 用户身份验证方法 窗口中，接受 默认的 本地 (/etc/passwd) 并点击 下一步。
- 10. 在 “添加一个新本地用户” 窗口中，如果您不想每次都以 root 身份使用系统，您可以选择添加一个本地用户。完成后，点击 下一步。
- 11. 在 “写入系统配置” 窗口中，SUSEconfig 工具会将您的所有设置写入磁盘。
- 12. 在 版本说明 窗口中，查看发行说明，然后点击 下一步。
- 13. 在 硬件配置 窗口中选择 跳过配置，然后点击 下一步。
- 14. 在 安装完成 窗口中，如果您打算克隆系统，请选中 复选框 克隆此系统以供 Autoyast 使用，然后点击 完成。如果您不打算克隆系统，可以保持复选框未选中。

恭喜！您已完成 Linux 的安装！

## 4.4.3 登录 Linux 系统

为了以精彩的方式结束安装指南，没有什么比以一种美好的方式登录您刚刚安装的系统更好：虚拟网络计算（VNC）。为此，您必须在机器上安装 VNC 客户端。您可以使用 Linux 的 vncviewer 客户端或为 Windows 获取一个，例如 RealVNC。在我们的示例中我们使用 RealVNC。

### 使用 VNC 连接到客户机

启动 RealVNC 应用程序并输入服务器（您的 Linux 系统）的 IP 地址，后跟 VNC 服务器在其上运行的端口号。图 4-32 第 215 页 显示了我们的 VNC 客户端连接到我们的 Linux 客户机系统。

根据 IP:port 格式输入 VNC 服务器信息。参见图 4-32。

![](img/b0a4b9056f819dccd4781a5105c92d45_230_0.png)

> **注意：** 当您安装 SLES10 并启用 VNC 管理时，系统启动后 VNC 服务器将在端口 5901 上运行。

RealVNC 打开一个新窗口，显示 X Window System。此时，您可能看不到 KDM 登录管理器；相反您会看到一个空白的 X Window System。

要调出登录管理器，请通过 SSH 以 root 身份登录 Linux 客户机并输入以下文本：

```
/etc/init.d/xdm start
```

根据您的网络速度，KDM 可能需要一段时间才能在当前的 VNC 显示中显示。KDM 登录显示类似于图 4-33 第 216 页 中的显示。

![](img/b0a4b9056f819dccd4781a5105c92d45_231_0.png)

图 4-33 KDM 登录窗口

以 root 身份登录并首次查看您的图形 KDE 界面。

## 配置 KDM 在启动时自动启动

每次想要使用 VNC 登录系统时都启动 XDM 服务是不理想的。因此，您应该将其作为系统服务在运行级别中启用。

要配置 KDM 自动启动，请使用以下步骤，这些步骤对应于图 4-34 第 217 页 中的编号：

- 1. 点击 YaST 图标
- 2. 向下滚动并在左侧菜单中选择 系统。
- 3. 右侧菜单刷新后，向下滚动并选择 系统服务（运行级别）。
- 4. 向下滚动列表直到看到 xdm 的条目。

图 4-34 将 XDM 启用为系统服务。

- 5. 突出显示 xdm 行并点击 专家模式。

窗口更改为如图 4-35 第 218 页 所示的专家模式。

图 4-35 专家模式下的运行级别编辑。

6. 启用 XDM 在级别 2、3 和 5 上运行。点击 完成 以完成此过程。

这些步骤应该可以解决问题。下次以及当您使用 VNC 客户端登录时，您将看到 KDM 登录窗口。

有关我们在此书中未提及的 Linux 安装的特殊性，请阅读 Gentoo 手册¹¹：

http://www.gentoo.org/doc/en/handbook/index.xml

¹¹ 尽管这是特定 Linux 发行版的手册，但 Linux 安装背后的概念描述得非常好且通用。

## 系统服务（运行级别）：详细信息

简单模式
专家模式
设置启动后默认运行级别为：
3. 完整多用户带网络

通过选择相应服务的列表条目然后勾选或取消勾选 B-5 运行级别的复选框来为运行级别分配系统服务。

启动/停止/刷新：用于单独启动或停止服务。

设置和重置：选择要运行当前所选服务的运行级别。

- 启用服务：激活服务在标准运行级别
- 禁用服务：停用服务。
- 启用所有服务：激活所有服务在其标准运行级别

对默认运行级别的更改将在下次启动计算机时生效。

| Service | Running | B | 0 | 1 | 2 | 3 | 5 | 6 | S | Description |
|---|---|---|---|---|---|---|---|---|---|---|
| smb | No |  |  |  |  |  |  |  |  | Samba SMB |
| smbfs | No |  |  |  |  | 3 | 5 |  |  | Import remote |
| smpppd | No |  |  |  |  |  |  |  |  | Start the smpp |
| snmpd | No |  |  |  |  |  |  |  |  | start netsnmp |
| splash | No |  |  | 1 | 2 | 3 | 5 |  | S | Splash screen |
| splash_early | Yes |  |  |  | 2 | 3 | 5 |  |  | kills animatio |
| squid | No |  |  |  |  |  |  |  |  | Squid web ca |
| sshd | Yes |  |  |  |  | 3 | 5 |  |  | Start the sshd |
| svcgssd | No |  |  |  |  |  |  |  |  | Start the RPC |
| syslog | Yes |  |  |  | 2 | 3 | 5 |  |  | Start the syste |
| vmlo... | Yes |  |  |  |  |  |  |  |  | Start the Linu |
| winbind | No |  |  |  |  |  |  |  |  | NSS daemon |
| xdm | Yes |  |  |  | 1 | 3 | 5 |  |  | X Display Ma |

X Display Manager





## 4.5 将 z/OS 映像作为 z/VM 客户机运行

将 z/OS 系统作为 z/VM 的客户机运行的过程与运行任何其他客户机系统基本相同。本节讨论将 z/OS 映像从 z10 LPAR 迁移到作为 z/VM 客户机操作系统运行。这应该适用于任何 System z 处理器上的系统。这可能是许多站点的场景，因为 LPAR 限制、服务器整合或简化其测试环境。z/VM 的一个优势是它能够虚拟化硬件，例如虚拟化耦合设施、通道到通道适配器等。也可以操作设备地址，从而最大限度地减少硬件配置（IOCDS）的管理需求。后者能够在需要时快速高效地设置新的测试映像。

该过程本质上与为作为 z/VM 客户机运行而创建新的 z/OS 系统的情况相同。确定所需资源仍需规划，并且在我们将现有的 z/OS 系统作为 z/VM 客户机 IPL 的点上，将执行 z/OS 安装过程。

### 4.5.1 z/OS 候选说明

我们从 LPAR 迁移到 z/VM 客户机的 z/OS 映像为其定义了特定的资源。它具有 SYSNAME SC59，你可能想将其用作你的 z/VM 用户 ID，但不是必需的。它没有 CTC，并且未使用 CF 或其他需要考虑的硬件，除通过 OSA 适配器进行通信外。它的硬件配置与表 4-2 中简化的列表类似：

表 4-2：资源表

| 资源类型 | 描述 | 注释 |
|---|---|---|
| Sysname | SC59 | 可以是 z/VM 用户 ID |
| 内存 / CS | 2 GB | 初始存储 |
| 处理器 / CPs | 4 | — |
| DASD / 磁盘 | 53 个卷 | 3390 Mod 3 和 Mod 9 |
| OSA 网络适配器 | 2000-2005 | QDIO |
| 控制台 | 地址 F008 | 3270 控制台 |

### 4.5.2 z/VM 所需定义

表 4-2 中第 219 页列出的资源是你在打算启动 z/OS 映像的虚拟机中必须定义的资源。请注意，该表不包含所有必要的细节，例如所有 DASD 磁盘设备地址。

### 4.5.3 在 USER DIRECT 中定义 z/OS 客户机

在获得有关 z/OS 映像配置的必要数据后，我们登录到 z/VM MAINT 用户 ID 并更新了 z/VM USER DIRECT 文件（参见第 18 页的 2.2.4 节“用户目录”和第 294 页的“USER DIRECT 文件”）。

> 注：使用相应的 z/OS sysname 为客户机命名可能有意义。

图 4-36 显示了 z/OS 客户机的定义。

```
USER SC59 GUESTZOS 2G 4G G
INCLUDE IBMDFLT
ACCOUNT ITS30000
IPL CMS PARM AUTOCR
MACHINE ESA 4
OPTION MAINTCCW QUICKDSP
CONSOLE F00B 3215
NICDEF 2000 TYPE QDIO DEVICES 6 LAN SYSTEM VSW1
MDISK 0191 3390 2390 2 LX6W02 MR
MDISK 813A 3390 0 END OP1TSA MWV
MDISK 8244 3390 0 END OP1HFC MWV
....
MDISK C730 3390 0 END IODFPK RR
MDISK D42A 3390 0 END Z19RF1 RR
```

图 4-36 SC59 用户 ID 的 USER DIRECT 条目。

根据图 4-36 中的行号对语句的描述：

- 1 建立 USER SC59，密码为 GUESTZOS。它最初定义为 2 GB 存储，最大为 4 GB，并定义为特权类 G 用户（无特殊特权）。
- 2 包含 PROFILE IBMDFLT（此处未显示）。
- 3 提供记账信息。
- 4 在登录时 IPL CMS，这将自动执行 PROFILE EXEC（如果存在）。从 PROFILE EXEC，你可以执行其他 exec。
- 5 定义客户机的模式。对于此特定用户，体系结构为 ESA，最多 4 个 CPU。
- 6 为客户机用户 ID 建立选项。MAINTCCW 意味着客户机允许初始化其使用的任何 DASD。QUICKDSP 导致客户机在有工作要做时立即添加到调度列表中，而不进入合格列表。
- 7 将客户机控制台地址定义为与 z/OS 控制台相同的地址。请注意，由于 z/VM 控制台要求，此阶段必须将其定义为 3215。它将在 IPLSC59 EXEC 中重新定义为 3270 以便 IPL z/OS（参见第 225 页的示例 4-18）。
- 8 将到 z/VM vswitch 的连接定义为 OSA 设备，从地址 2000 开始的六个连续地址。
- 9 定义客户机在 CMS 中的 minidisk。用于 CMS 文件系统，例如 PROFILE EXEC（后面描述）。
- 10 11 提供 z/OS 所需的 DASD 定义。它们都定义为 minidisks，从第 0 个柱面开始到最高柱面结束（整个磁盘）。在我们的例子中，每个设备的实际地址和虚拟地址是相同的。磁盘地址可以使用除实际地址之外的地址来定义，以简化测试映像的配置管理。还请注意，磁盘定义为访问模式 MWW，即多写访问。最后的 V 定义 CP 应为此 minidisk 的 I/O 操作使用其虚拟保留/释放支持。这是为了确保如果从多个客户机访问时的完整性。如果有共享只读 DASD，则访问可以定义为只读（RR）。

> 注：并非所有磁盘都列出，只有几个示例用于说明目的。还有其他 minidisks 定义给客户机 SC59。

> 提示：你可以将 minidisks 定义为访问模式 RR 以防止它们被更新，如果这是期望的。这对于防止对某些磁盘（例如你的 SYSRES 或 IODF 磁盘）的分配或更新很有用，而无需在 RACF 或类似产品中调整任何访问规则。





更新完 USER DIRECT 文件后，保存该文件并执行以下 DIRECTXA 命令，将新的目录加载到 z/VM 存储中。
`directxa user direct c`

## 4.5.4 ZOS1 客机控制台注意事项

在此场景中，为简化操作，我们选择不使用任何通道连接控制台来操作该映像。这意味着我们可以登录到 z/VM 客机用户 ID，IPL z/OS，并将该会话用作 z/OS 操作员控制台。

**警告：** 一个问题是，如果 z/OS 操作员发出 CP LOGoff，z/OS 系统将立即终止。应使用 CP DISConnect 来保持系统运行。

**重要：** 在 z/VM 客机上运行 z/OS 时，HMC 控制台不能用于 IPL z/OS 客机

这种操作方式还意味着，我们需要在 IPL z/OS 之前将操作员控制台的模式更改为 3270，以避免控制台锁定，因为 3270 是 z/OS 中支持的终端类型。

## 4.5.5 SC59 客机 PROFILE EXEC 创建

我们为客机用户 ID SC59 创建了一个 PROFILE EXEC 文件来定义额外的 CPU。您可以根据各安装的要求添加其他定义。PROFILE EXEC 在每次执行 CMS IPL 时都会执行。该 exec 在用户 ID 自动登录到 z/VM 系统时也会执行。从断开的虚拟机重新连接不会执行 PROFILE EXEC。

图 4-37 显示了 SC59 用户 ID 的 PROFILE EXEC 文件。

```
PROFILE EXEC  F1 V 130  Trunc=130

00000 * * * Top of File * * *
00001 /* PROFILE EXEC FOR SC59 */
00002 set pf12 ret
00003 'CP DEFINE CPU 1'
00004 'CP DEFINE CPU 2'
00005 'CP DEFINE CPU 3'
```

*图 4-37 SC59 的 PROFILE EXEC*

重要：通过我们的方式定义 PROFILE EXEC，您无法 AUTOLOG 此机器并使 z/OS 系统自动 IPL。该文件不包含实际 IPL z/OS 映像的任何语句。

与其将执行 z/OS 映像 IPL 所需的语句和命令放在配置文件中，我们创建了一个 exec 来实际执行此操作。简而言之，此 exec 执行以下任务：

- 1. 将控制台模式切换为 3270
- 2. 发出命令 SET RUN ON
- 3. IPL z/OS 映像

图 4-38 显示了 IPLSC59 EXEC 的内容。

```
IPLSC59 EXEC      A1  V 130  Trunc=130 Size=14 Line=0 Col=1 Alt=2
00000 * * * Top of File * * *
00001 /* Exec to IPL the SC59 guest system */
00002 trace 'o'
00003 'vmfclear'
00004 cmd = 'TERM CONMODE 3270' || '15'X
00005 cmd = cmd || 'SET RUN ON' || '15'X
00006 say '**************************************************'
00007 say '*'
00008 say '*    This is a z/OS 1.9 system,'
00009 say '*    WAIT, the system is coming up... SC59'
00010 say '*'
00011 say '**************************************************'
00012 cmd = cmd || 'IPL D42A LOADPARM C73059M1 CLEAR'
00013 push cmd
00014 exit
00015 * * * End of File * * *
```

图 4-38 IPL 内容

IPLSC59 exec 中的重要项目在以下列表中描述：

- TERM CONMODE 3270    这会将模式（或终端类型）切换为 3270。
- '15'x    这是每个命令之后出现的换行指示符。命令本身被堆叠，并在 exec 结束之后发出（不受 exec 本身中的任何逻辑控制）。

SET RUN ON
这用于避免虚拟机进入 CP 读取模式导致 z/OS 停止

IPL D42A
这是 z/OS 的实际 IPL 命令，如果您在 LPAR 中运行 z/OS，通常在 HMC 中输入。

> 注意：IPLSC59 EXEC 中的以下重要语句或命令，都可以作为来自虚拟机本身的单独命令发出，而不是执行 IPLSC59 EXEC：
> ► TERM CONMODE 3270
> ► SET RUN ON
> ► IPL D42A LOADPARM C73059M1 CLEAR

## 4.5.6 作为 z/VM 客机 IPL 系统

创建了前面的文件后，我们关闭了在 LPAR 中运行的 z/OS 系统。然后，我们登录到 z/VM 用户 ID SC59 并运行 IPLSC59 EXEC。过了一会儿（就像正常 IPL LPAR 一样），我们看到了初始消息，我们的会话看起来与正常的 z/OS 操作员控制台完全相同。在启动所有必要的 started-task 和子系统后，我们发出 CP DISC 命令以从系统控制台断开连接，使 z/OS 系统继续运行。

> 注意：在我们定义控制台的方式中，有一个特殊之处，即在初始 IPL 时，我们必须在操作员响应前加上 #CP VINPUT VMSG 才能在 NIPCON 模式下与 z/OS 通信；例如：
> #CP VINPUT VMSG R 00,CONTINUE
> 进入正常控制台模式后，这就不再是事实了。在操作物理连接的控制台时，这不应是必要的。

## 4.5.7 z/OS 注意事项

从 z/OS 角度来看，需要注意的一点是，任何使用 symbolics HWNAME 和 LPARNAME 的情况。如果这些在 PARMLIB 成员（例如您的 IEASYMxx）或驻留在 PARMLIB 或 SYSn.IPLPARM 中的成员 LOADxx 中使用，它们就需要您关注。当 z/OS 作为 z/VM 客机运行时，LPARNAME 永远无法解析，因此对这些变量值的任何过滤都会失败。根据您包含的逻辑，IPL 可能因此问题而失败。如果您对 HWNAME 有过滤器，您应考虑将其更改为 VMUSERID。详情请参阅 z/OS: MVS Initialization and Tuning Reference，SA22-7592。




# 4.5.8 向 z/OS 客户机添加 3390 磁盘

与在 LPAR 中运行的任何 z/OS 系统一样，有时系统需要额外的 I/O 设备，例如 DASD。在 LPAR 中，在该 LPAR 的 IOCDS 中定义新的 DASD 即可使新卷可供 z/OS 系统使用。当 z/OS 系统作为 z/VM 客户机运行时，也存在类似的功能。在 z/OS 客户机系统启动后，我们进行了一系列步骤，在不中断系统或需要 IPL 的情况下，将新的 3390 磁盘卷上线到客户机系统。我们还决定将物理设备地址 8222 作为设备地址 6000 在 z/OS 上定义的那样上线到 z/OS 客户机。该磁盘的 volser 为 DK8222。我们首先将其作为客户机用户（在 USER DIRECT 文件中）的 minidisk 添加，如示例 4-18 所示。

## 示例 4-18 z/OS 客户机用户 minidisk 的 USER DIRECT 语句

```
....
MDISK 6000 3390 0 END DK8222 MWV
```

发出 DIRECTXA 命令将目录加载到 z/VM 存储中

添加卷后，在仍登录到 MAINT 的情况下，我们发出命令使新的 DASD 卷可供 z/VM 系统和客户机用户使用：

```
ATT 8222 SYSTEM
```

然后我们以 z/VM 上的客户机 z/OS 用户 ID 登录。由于这也充当操作员控制台（参见我们在 4.5.5 中“SC59 guest PROFILE EXEC creation”第 222 页的假设），我们按下了 PA1（或从我们的 3270 仿真器模拟它的键击）进入 CP 读取模式。然后我们发出以下命令使新卷可供 z/OS 系统使用：

```
LINK * 6000 6000 MWV
```

这在图 4-39 中有所说明。

![](img/b0a4b9056f819dccd4781a5105c92d45_240_0.png)

## 图 4-39 从 z/OS 客户机用户 ID 发出的 LINK 命令

清除 CP 窗口从而再次进入 z/OS 操作员控制台后，我们观察到以下消息。

```
IOS1501 DEVICE 6000 NOW AVAILABLE FOR USE
```

从 z/OS 系统控制台，我们发出以下语句以验证状态是否未发生变化（由于我们现在在 z/VM 下运行而导致）：

```
D U,,6000,1
```

然后我们从 z/OS 将设备置为在线状态，见图 4-40 中 z/OS 系统日志的快照。

```
- 12.57.20 IOS1501 DEVICE 6000 NOW AVAILABLE FOR USE
- 12.57.58 d u,,6000,1
  12.57.58 IEE4571 12.57.58 UNIT STATUS 147
  UNIT TYPE STATUS VOLSER VOLSTATE
  6000 3390 F-NRD /RSDNT
- 12.58.10 v 6000,online
  12.58.10 IEE3021 6000 ONLINE
00- 12.58.24 d u,,6000,1
  12.58.24 IEE4571 12.58.24 UNIT STATUS 153
  UNIT TYPE STATUS VOLSER VOLSTATE
  6000 3390 0 DK8222 PRIV/RSDNT
```

## 图 4-40 z/OS SYSLOG

此演示提供了使用 z/VM 虚拟化功能来操作 z/OS 所见设备地址的思路。一个可能的场景可以是为测试 z/OS 映像提供相对静态的硬件配置（考虑到 IOCDS）。通过克隆预配置的 z/OS 系统，您将能够操作每个客户机在 z/VM 中的物理设备地址及其对应的虚拟地址，从而减少配置更改的需求。

![](img/b0a4b9056f819dccd4781a5105c92d45_242_0.png)

# z/VM 系统操作

在本章中，我们介绍 z/VM 和 Linux 的几个常见系统操作任务。此外，我们将典型的 z/OS 系统操作与 z/VM 和 Linux 进行比较。我们还提供了有关克隆系统的资源指针。

## 目标

完成本章后，您应该能够：

- 与其他 z/VM 用户通信
- 理解 z/VM 的 IPL 和关闭过程
- 执行 z/VM 虚拟机的基本管理
- 执行资源管理
- 运行类似批处理作业的进程

# 5.1 使用控制台与用户通信

第 2.7 节“Consoles”第 50 页讨论了 z/VM 可用的控制台类型。使用这些控制台可以与其他 z/VM 用户通信。

您可以通过发送以下内容与 z/VM 用户通信：

- 向所有已登录用户发送一般信息消息
- 向特定用户发送一般信息消息
- 向所有已登录用户发送警告消息
- 向特定用户发送警告消息

> z/OS 类比：z/OS 用户使用 SEND 命令。

MESSAGE 和 WARNING 命令受输入命令区域长度的限制。如果消息的全部文本不适合该区域，请输入另一条命令并输入剩余文本。

如果安装了外部安全管理器（ESM），您可能无权使用 MESSAGE 或 WARNING 命令。但是，发送给系统操作员或来自系统操作员的消息以及使用 ALL 选项发送的消息不受 ESM 的授权检查限制。如需更多信息，请联系您的安全管理员。

如果 CP 没有按您输入的方式发出消息，可能是因为您在消息文本中包含了特殊的行编辑符号。例如，如果逻辑行编辑生效，# 符号是您的逻辑行结束符；如果您在消息文本中包含 #，CP 会截断您的消息。为防止 CP 将这些符号解释为逻辑行编辑功能，请输入以下命令：

```
SET LINEDIT OFF
```

然后 CP 会按您输入的方式发出消息。

## 5.1.1 向所有用户发送一般信息消息

要向所有已登录用户发送一般信息消息，例如“查询周末日程的日志”，请输入：

```
message all query log for weekend schedule
```




当跨系统扩展¹（CSE）处于活动状态，并且你希望所有登录到 CSE 复合体中所有系统的用户都能收到该消息时，请输入：

```
message all at all query log for weekend schedule
```

以下消息会显示在所有能够接收该消息的用户的显示窗口中：

```
hh:mm * MSG FROM OPERATOR: QUERY LOG FOR WEEKEND SCHEDULE
```

hh:mm 表示消息发送的时间。除非存在以下情况，否则每个用户都会立即收到该消息：

- 用户的显示设备上有待处理的操作。在这种情况下，用户会在操作完成时收到该消息。
- 用户正在运行全屏模式，或者已输入 SET MSG OFF 命令。在这些情况下，用户不会收到该消息，你会收到一条错误消息。
- 用户未登录。

### 5.1.2 向特定用户发送一般信息消息

有时，你必须仅向特定用户发送一般信息消息。例如，如果你想通知用户 VMUSER1，他未被授权使用他刚才请求你挂载的磁盘组 RC015，请输入以下命令：

```
message vmuser1 you are not authorized to use pack rc015
```

当用户 VMUSER1 的显示设备上没有待处理操作时，该消息会出现在他的显示窗口中（前提是他未运行全屏模式，并且未输入 SET MSG OFF 命令）。只有 VMUSER1 会收到此消息。

### 5.1.3 向所有用户发送警告消息

偶尔，系统问题要求你采取行动，例如必须对系统执行 IPL，这可能会中断用户的虚拟机操作。发生这种情况时，使用 warning 命令将立即用紧急消息中断用户的控制台，这与 MESSAGE ALL 不同，后者是向所有用户通报情况：

```
warning all the system will be IPLed in 5 minutes, please log off.
```

另一个示例是，当 CSE 处于活动状态，且你希望所有已登录 CSE 复合体中各系统的用户都能收到该消息时，你可能需要输入：

```
warning all at all the system will be IPLed in 5 minutes, please log off.
```

作为响应，CP 会在接下来的 60 秒内将该消息显示在所有用户的显示窗口中（前提是用户未运行全屏模式，并且未输入 SET WNG OFF 命令）。这应该能让他们有时间保存当前正在处理的工作。

> **注意：** 如果你使用 MESSAGE 命令发送警告，存在待处理操作的用户在该操作完成之前不会收到该警告，而那时可能为时已晚。

### 5.1.4 向特定用户发送警告消息

有时，你必须向特定用户发送高优先级消息。例如，用户 MVSOPR1 可能提交了一个必须在打印机 00E 上处理的高优先级文件，但该打印机专用于用户 VMUSER1。在将打印机重新分配给用户 MVSOPR1 之前，你可能需要向用户 VMUSER1 发送以下警告消息：

```
warning vmuser1 system needs printer 00e - draining in 5 minutes
```

如果该用户未运行全屏模式，并且未输入 SET WNG OFF 命令，则用户 VMUSER1 将在接下来的 60 秒内收到此消息，并应停止向此打印机发送待处理的文件。

## 5.2 运行系统

本节说明你的 z/VM 系统在启动和关闭时会发生什么。了解 IPL 和关机过程对于系统监控和问题调试非常有帮助。

### 5.2.1 z/VM IPL 工作流程

当你对 z/VM 系统执行 IPL 时，在系统完全正常运行并可使用之前，必须在 IPL 期间执行许多步骤。第 231 页上的图 5-1 显示了这些步骤的流程。

![](img/b0a4b9056f819dccd4781a5105c92d45_246_0.png)

图 5-1 z/VM IPL 流程图

在 z/VM IPL 流程图中，从上到下的步骤如下：

- 1. 从磁盘加载 z/VM 操作系统。这包括系统 CP 核心。
- 2. CP 读取 SYSTEM CONFIG 文件，以识别配置参数并实施这些参数。





3. 操作系统将 CP 所拥有的卷联机，例如用于分页、排队和 t-disk 的卷。
4. 根据启动方式（参见 5.2.2，第 234 页的“Warm start, force start, cold start, and clean start”），z/VM 在上次关机期间读取保存在检查点和热启动数据文件²中的系统属性信息并将其恢复。
5. 系统提示设置时间-日期（TOD）。
6. 用户目录，连同用户的定义，一并联机。
7. 现有的 spool 文件可供使用。
8. 所有已连接的 I/O 联机并可供使用。
9. SYSTEM CONFIG 中定义的用户卷可供使用。
10. OPERATOR 用户已登录。
11. OPERATOR 虚拟机通过登录 erep、diskacct 和 opersymp 用户来启动日志/记账/症状服务。
12. OPERATOR 用户 ID 自动登录 AUTOLOG1。
13. AUTOLOG1 根据其 PROFILE EXEC 启动其被指示启动的任何其他虚拟机。
14. 服务机器在初始化状态下向 OPERATOR 发送消息。

## Example 5-1 z/VM IPL process.

```
14:58:30 z/VM V5 R3.0 SERVICE LEVEL 0703 (64-BIT)
14:58:31 SYSTEM NUCLEUS CREATED ON 2008-05-23 AT 10:40:19, LOADED FROM LX6RES
14:58:31
14:58:31 **********************************************************************
14:58:31 * LICENSED MATERIALS - PROPERTY OF IBM*                           *
14:58:31 *                                                                   *
14:58:31 * 5741-A06 (C) COPYRIGHT IBM CORP. 1983, 2007. ALL RIGHTS          *
14:58:31 * RESERVED. US GOVERNMENT USERS RESTRICTED RIGHTS - USE,           *
14:58:31 * DUPLICATION OR DISCLOSURE RESTRICTED BY GSA ADP SCHEDULE         *
14:58:31 * CONTRACT WITH IBM CORP.                                           *
14:58:31 *                                                                   *
14:58:31 * * TRADEMARK OF INTERNATIONAL BUSINESS MACHINES.                  *
14:58:31 **********************************************************************
14:58:31
14:58:31 HCPZCO6718I Using parm disk 1 on volume LX6RES (device 1B34).
14:58:31 HCPZCO6718I Parm disk resides on cylinders 39 through 158.
14:58:31 Start ((Warm|Force|COLD|CLEAN) (Drain) (Disable) (NODirect)
14:58:31      (NOAUTOLOG) or (SHUTDOWN)
14:58:59 WARM
14:58:59 NOW 14:58:59 EDT THURSDAY 2008-06-05
14:58:59 Change TOD clock (Yes|No)
14:59:03 NO
14:59:03 The directory on volume LX6RES at address 1B34 has been brought online.
14:59:05 HCPWRS2513I
14:59:05 HCPWRS2513I Spool files available      376
14:59:07 HCPWRS2512I Spooling initialization is complete.
14:59:07 DASD 1B35 dump unit CP IPL pages 17646
14:59:07 HCPAU2U700I System gateway VMGUEST identified.
14:59:07 z/VM Version 5 Release 3.0, Service Level 0703 (64-bit),
14:59:07 built on IBM Virtualization Technology
14:59:07 There is no logmsg data
14:59:07 FILES: 0031 RDR, 0009 PRT, NO PUN
14:59:07 LOGON AT 14:59:07 EDT THURSDAY 06/05/08
14:59:07 GRAF 0020 LOGON AS OPERATOR USERS = 1
14:59:07 HCPIOP962I 2048M system storage
14:59:07 FILES: 0000314 RDR, 0000030 PRT, 0000001 PUN
14:59:07 HCPCRC0802I Accounting records are accumulating for userid DISKACNT.
14:59:07 XAUTOLOG EREP
14:59:07 Command accepted
14:59:07 XAUTOLOG DISKACNT
14:59:07 Command accepted
14:59:07 XAUTOLOG AUTOLOG1
14:59:07 Command accepted
14:59:07 XAUTOLOG OPERSYMP
14:59:07 Command accepted
14:59:07 AUTO LOGON ***     EREP      USERS = 2   BY OPERATOR
14:59:07 AUTO LOGON ***     DISKACNT  USERS = 3   BY OPERATOR
14:59:07 AUTO LOGON ***     AUTOLOG1  USERS = 4   BY OPERATOR
14:59:07 AUTO LOGON ***     OPERSYMP  USERS = 5   BY OPERATOR
14:59:07 HCPCLS6056I XAUTOLOG information for EREP: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for DISKACNT: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for AUTOLOG1: The IPL command is verified by the IPL command processor.
14:59:07 HCPCLS6056I XAUTOLOG information for OPERSYMP: The IPL command is verified by the IPL command processor.
14:59:07 AUTO LOGON ***     VMSERVS   USERS = 6   BY AUTOLOG1
14:59:07 AUTO LOGON ***     VMSERVU    USERS = 7   BY AUTOLOG1
14:59:07 AUTO LOGON ***     VMSERVR   USERS = 8   BY AUTOLOG1
14:59:07 USER DSC   LOGOFF AS AUTOLOG1 USERS = 7
14:59:07 AUTO LOGON ***     DTCVSW1   USERS = 8   BY AUTOLOG1

² 该文件存储在系统 RES 卷中



14:59:07 AUTO LOGON *** DTCVSW2 USERS = 9 BY AUTOLOGI
14:59:07 AUTO LOGON *** TCPIP USERS = 10 BY AUTOLOGI
14:59:07 * MSG FROM EREP :1 RECORDING FILE(S), 40 RECORDS, A DISK 03 % FULL
14:59:07 * MSG FROM DISKACNT:17 RECORDING FILE(S),1097 RECORDS, A DISK 27 % FULL
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *LOGREC for userid EREP.
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *ACCOUNT for userid DISKACNT.
14:59:07 * MSG FROM OPERSYMP: 26 RECORDING FILE(S), 26 RECORDS, A DISK 04 % FULL
14:59:07 HCPRC8064I Recording data retrieval has been started; recording *SYMPTOM for userid OPERSYMP.
14:59:08 3020-3022 ATTACHED TO TCPIP BY TCPIP
14:59:08 AUTO LOGON *** FTPSERVE USERS = 11 BY TCPIP

## 5.2.2 热启动、强制启动、冷启动和干净启动

z/VM 为您提供了四种基本启动类型：热启动、强制启动、冷启动和干净启动。它们之间的区别在于 CP 恢复系统环境的数量多少，其中热启动恢复最多，而干净启动保留最少。

如果热启动失败，在使用强制启动或冷启动之前，请联系您的系统支持人员，因为关键文件可能会丢失。

要恢复系统环境，您必须先保存它。当您发出 SHUTDOWN 命令并收到响应 SHUTDOWN COMPLETE 时，CP 会保存系统环境中的以下部分：

- 任何存储中的记账、EREP³ 和症状记录
- 记账、EREP 和虚拟机是症状记录记录服务，通常将这些记录从存储传输到磁盘。如果这些虚拟机未进行检索，记录将保留在存储中。SHUTDOWN 命令会将仍在存储中的任何记录写入 DASD 上的检查点区域，以便在下次 IPL 期间将记录返回到存储以供检索。

- 系统日志消息
- 系统日志消息在用户登录或重新连接时向用户传达信息。

- 搁置文件队列

> ³ EREP：环境记录编辑和打印。EREP 读取硬件和软件生成的错误和其他环境记录，编辑记录并生成打印报告。

搁置文件是磁盘上的数据集合，等待由真实或虚拟的阅读器、打印机或穿孔机处理。SHUTDOWN 命令保存有关定位这些搁置文件的队列的信息。

> 注意：热启动或强制启动后，搁置文件可能不会按相同顺序恢复。

> z/OS 类比：z/VM 的 SHUTDOWN 命令类似于 HALT（Z EOD）命令，只是 z/OS 不保留热数据。

## 系统数据文件队列

系统数据文件队列保存以下数据集合，称为系统数据文件：命名保存系统（NSS）、不连续保存段（DCSS）、映像库、用户类重构（UCR）文件、消息存储库文件和系统跟踪文件。

- 命名保存系统（NSS）是用户已命名并保留在系统数据文件中的操作系统副本。用户可以通过其名称加载操作系统，这比通过设备号加载更有效。
- 不连续保存段（DCSS）是指用户已命名并保留在系统数据文件中的一个或多个存储页。当定义为可共享的不连续保存段被加载时，一个以上的用户可以访问它。
- 映像库是一组包含在系统数据文件中的模块，它们定义打印机用于打印搁置文件的间距、字符和复制修改数据。
- 用户类重构（UCR）文件扩展命令和 DIAGNOSE 代码的特权类。这使您的安装可以自定义 z/VM 的特权类结构。
- 消息存储库文件包含翻译成国家语言的 z/VM 消息和响应。
- 系统跟踪文件包含系统内发生的事件记录。使用这些文件来确定系统问题的来源。

SHUTDOWN 命令保存有关定位这些系统数据文件的队列的信息。

## 单位记录设备、显示器和 3270 打印机的状态





当您输入 SHUTDOWN 命令时，您会保存系统环境的所有这些部分。然后，当您通过热启动重新启动系统时，CP 会恢复它们。

如果您输入 SHUTDOWN REIPL 命令，CP 会尝试自动启动指定的模块。

有关重新 IPL 另一个模块时的其他限制，请参阅 z/VM: CP Commands and Utilities Reference, SC24-6081[^4]。

除非您有理由另行操作，否则请指定热启动。请记住，如果您没有使用 SHUTDOWN 命令关闭 z/VM 系统，您可能无法通过热启动将其重新启动。SHUTDOWN 命令保存的信息正是使热启动能够工作的原因。

在强制启动期间，CP 尝试恢复热启动期间恢复的大部分内容，但可能无法完全恢复。就像在热启动中一样，CP 尝试按以下顺序恢复：

- 1. 存储中的记账、EREP 和症状记录
- 2. 系统日志消息
- 3.  spool 文件和系统数据文件队列

但是，如果 CP 在第一步中遇到错误，它会立即继续恢复 spool 文件和系统数据文件队列。除非您在系统配置文件中指定了以下语句，否则系统日志消息会丢失：

```
FEATURES ENABLE LOGMSG_FROM_FILE
```

任何剩余的记账、EREP 和症状记录都会丢失。此外，如果 CP 在恢复 spool 文件时遇到错误，它会立即继续处理队列中的下一个文件，并且发生错误的文件将被安排删除。当 spooling 初始化的初步阶段完成后，会显示一条提供 spool 文件汇总状态的消息，然后操作员可以在不丢失任何 spool 文件的情况下停止系统初始化。

此外，强制启动不会恢复任何单元记录设备特性，例如要处理的类或映像库。相反，强制启动会尝试使用系统配置文件中 RDEVICE 语句上指定的默认特性启动单元记录设备。强制启动确实会尝试恢复所有显示器和 3270 打印机的状态。

因此，在强制启动后，CP 可能无法完全恢复系统的环境。仅在热启动失败后，经系统支持人员授权后才使用强制启动。

如果强制启动失败，您必须执行冷启动。在冷启动期间，CP 仅尝试恢复系统数据文件。这意味着当您执行冷启动时，您会丢失所有 spool 文件、存储中的所有记账、EREP 和症状记录。如果您未在系统配置文件中指定以下语句，则系统日志消息会丢失：

```
FEATURES ENABLE LOGMSG_FROM_FILE
```

您的单元记录设备、显示器和 3270 打印机的状态也可能与重新启动前不同。仅在热启动和强制启动均失败时才使用冷启动。

关于热启动、强制启动、冷启动和干净启动需要掌握的基本要点是：

- 要在重新启动系统之前保存系统的环境，请使用 SHUTDOWN 命令。
- 要恢复系统的环境，请通过热启动重新启动系统。
- 如果热启动失败，
  - 检查 DASD 卷。
  - 联系系统支持人员。
  - 当重复尝试热启动失败时，尝试强制启动以尽可能多地恢复系统的环境。
- 如果您决定继续进行系统初始化，即使有文件被安排删除，也请记住这些文件无法恢复。
- 如果强制启动失败，请尝试冷启动。
- 干净启动会在不尝试恢复系统关闭前存在的 spool 文件和系统数据文件的情况下 IPL 系统。

## 5.2.3 检查系统资源

系统启动后，检查其资源。本节讨论有助于您检查系统资源和系统可用性的各种命令。

[^4]: http://publib.boulder.ibm.com/infocenter/zvm/v5r3/index.jsp?topic=/com.ibm.zvm.v53.hcpb7/hcse4b21.htm





## 检查系统级别：`query cplevel` 和 `query cmslevel`

QUERY CPLEVEL 和 QUERY CMSLEVEL 命令对于确保维护已正确应用于每个系统非常有用。可以使用这些命令检查以下项目：

- 软件版本级别、发行级别和发行修改级别
- 软件服务级别号
- CP 系统软件写入 DASD 的日期和时间（转换为当前活动时区）
- CP 最后启动的日期和时间
- CMS 的发行版和服务级别

命令的示例显示在示例 5-2 中。

*示例 5-2 检查 CP 和 CMS 级别*

```
q cplevel
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/29/07 23:21:12 EDT
IPL at 06/11/08 07:58:34 EDT
Ready; T=01/0.01 11:45:20
q cmslevel
CMS Level 23, Service Level 701
Ready; T=01/0.01 11:45:24
```

## 检查 CP 加载参数：`query cpload`

使用 QUERY CPLOAD，如示例 5-3 所示，来显示有关上次 CP IPL 的信息。显示的信息包括上次使用的 CP 模块的位置、参数磁盘的位置以及 CP 的启动方式。

*示例 5-3 查询 CPLOAD*

```
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=01/0.01 11:46:07
```

## 检查实际存储量：`query storage`

QUERY STORAGE 命令（缩写为 Q STO）用于显示 LPAR 启动后可用的实际内存量。参见第 239 页的示例 5-4。

## 检查扩展存储量：query xstorage

QUERY XSTORAGE 命令（缩写为 Q XSTO）用于显示分区中配置的实际扩展存储量。该命令的输出还显示正在使用的扩展存储量以及用于微型磁盘缓存（MDC）的量。参见示例 5-5。

```
q xstor
XSTORE= 2048M online= 2048M
XSTORE= 2048M userid= SYSTEM usage= 0% retained= 0M pending= 0M
XSTORE MDC min=0M, max=0M, usage=0%
XSTORE= 2048M userid= (none) max. attach= 2048M
Ready; T=0.01/0.01 11:47:27
```

## 检查所有处理器是否可用：query processors

QUERY PROCESSORS 命令（缩写为 Q PROC）用于显示分区的处理器当前分配情况。

MASTER 处理器是用于 IPL 的基本处理器，ALTERNATE 处理器在 IPL 时会自动上线，而 STANDBY 处理器可供分区使用，但处于离线状态。参见示例 5-6。PROCESSOR 行中的最后一个字段表示处理器的类型：CP、IFL、ICF、ZIIP 或 ZAAP。

```
q processors
PROCESSOR 00 MASTER CP
PROCESSOR 01 ALTERNATE CP
PROCESSOR 02 ALTERNATE CP
PROCESSOR 03 ALTERNATE CP
PROCESSOR 04 STANDBY CP
PROCESSOR 05 STANDBY CP
Ready; T=0.01/0.01 11:51:31
```

## 更改处理器对系统的可用性

在正常情况下，您会使用处理器群集或分区中的所有处理器启动并运行系统。但是，如果您安装的支持人员指示您这样做，您可以使用 VARY ONLINE PROCESSOR 或 VARY OFFLINE PROCESSOR 命令来控制处理器是否可供 z/VM 使用。有关这些命令的更多信息，请参阅 z/VM: CP Commands and Utilities Reference, SC24-6081⁵

## 检查系统 DASD 配置：query alloc

系统 IPL 后，检查所需的分页和排队是否可用且在线是一个良好的做法。您还可以检查临时磁盘空间。

QUERY ALLOC PAGE 检索分页空间配置。在示例 5-7 中，四个 3390-03（每个为 3339 个柱面）已配置为分页设备。在这些分页设备上总共只分配了 13 个页面。

示例 5-7 检查 LPAR 中可用的分页空间

```
q alloc page
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6PAG 1A22 1 3338 600840 0 0 0%
DK8226 8226 0 3338 601020 0 0 0%
DK8227 8227 0 3338 601020 13 26 1%
DK8228 8228 0 3338 601020 0 0 0%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 2348K 13 1%
USABLE 2348K 13 1%
Ready; T=0.01/0.01 11:54:40
```

同样，QUERY ALLOC SPOOL 命令检查排队配置。在示例 5-8 中，只有一个 3390-03 DASD 被定义为排队设备，并且正在使用 140075 个页面，约占可用于排队的总页面的 23%。

示例 5-8 检查排队空间

```
q alloc spool
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6SPL 1A21 1 3338 600840 140075 145430 23%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 600840 140075 23%
USABLE 600840 140075 23%
Ready; T=0.01/0.01 11:55:39
```

⁵ http://publibz.boulder.ibm.com/epubs/pdf/hcse4b21.pdf



最后，QUERY ALLOC TDISK 显示所有已定义和分配的临时磁盘空间，如示例 5-9 所示。

### Example 5-9 Checking the amount of TDISK allocated

```text
q alloc tdisk
VOLID RDEV EXTENT START EXTENT END TOTAL IN USE HIGH % USED
---------------- ----------------
LX6TDK 8225 1 3338 3338 20 20 1%
---------------- ----------------
SUMMARY 3338 20 1% CKD
USABLE 3338 20 1% CKD
Ready; T=0.01/0.01 11:06:01
```

## Checking system dump space configuration: query dump

QUERY DUMP 命令（缩写为 Q DUMP），在示例 5-10 中显示：

- 分配用于接收 CP 异常终止转储的设备类型和单元或单元
- DUMP 选项的当前设置

### Example 5-10 Querying the DUMP configuration

```text
q dump
DASD 1A21 dump unit CP IPL pages 31437
Ready; T=0.01/0.01 11:57:09
```

## Checking the recording status: query recording

QUERY RECORDING 命令（缩写为 Q REC）检查以下项目的状态：

- CP 对以下记录的数据收集：
    - Accounting
    - EREP（错误记录）
- CP 对症状记录的数据收集
- 对这些记录的活动检索

在第 242 页的示例 5-11 中，所有记录均处于活动状态，使用 z/VM 中定义的默认用户 ID：EREP userid 用于错误记录，ACCOUNT 用于记账信息，以及 OPERSYMP 用于症状记录收集。计数字段显示任何未处理的记录。

### Example 5-11 Status of recordings in z/VM

```text
q rec
RECORDING   STATUS   COUNT    LMT  USERID    COMMUNICATION
EREP        ON       00000000 002  EREP      ACTIVE
ACCOUNT     ON       00000000 020  DISKCNT   ACTIVE
SYMPTOM     ON       00000000 002  OPERSYMP  ACTIVE
Ready; T=0.01/0.01 11:57:36
```

## Checking real devices availability

z/VM IPL 后，系统操作员检查配置中分配和定义的所有资源是否已上线。

### Disk devices: query DASD all

QUERY DASD ALL 命令（缩写为 Q DA ALL）显示分区中所有活动真实磁盘的列表、其所有者（CP、SYSTEM，或如果未附加则为 FREE）、其标签以及在卷上定义的 MDISKS 的链接数。最后一行告知没有离线的 DASD。QUERY DASD 命令显示系统使用的所有 DASD。参见示例 5-12。

### Example 5-12 Querying all disks attached to the system

```text
q da all
DASD 1A20 CP OWNED  LX6RES  80
DASD 1A21 CP OWNED  LX6SPL  1
DASD 1A22 CP OWNED  LX6PAG  0
DASD 1A23 CP OWNED  LX6W01  127
DASD 1A24 CP OWNED  LX6W02  4
DASD 1A25 CP SYSTEM NW1A25  1
DASD 1A26 CP SYSTEM NW1A26  1
DASD 1A27 CP SYSTEM NW1A27  1
DASD 1A28 CP SYSTEM NW1A28  1
DASD 1A29 CP SYSTEM NW1A29  1
DASD 1A2A CP SYSTEM NW1A2A  1
DASD 1A2B CP SYSTEM NW1A2B  1
DASD 1A2C CP SYSTEM NW1A2C  1
DASD 1A2D CP SYSTEM NW1A2D  1
DASD 8221 CP SYSTEM DK8221  1
DASD 8226 CP OWNED  DK8226  0
DASD 8227 CP OWNED  DK8227  0
DASD 8228 CP OWNED  DK8228  0
DASD D815 CP SYSTEM LXD815  2
DASD D816 CP SYSTEM LXD816  1
DASD 1B34 LX6RES  , DASD 1B35 LX6SPL  , DASD 1B36 LX6PAG  , DASD 1B37 LX6W01
DASD 1B38 LX6W02  , DASD 8222 DK8222  , DASD 8223 LX8223  , DASD 8224 DK8224
DASD 8225 LX8225  , DASD D817 LXD817 , DASD D818 LXD818 , DASD D819 LXD819
DASD D81A LXD81A  , DASD D81B LXD81B , DASD D81C LXD81C , DASD D81D LXD81D
DASD D81E LXD81E , DASD D81F LXD81F
An offline DASD was not found.
Ready; T=0.01/0.01 11:58:00
```

### Magnetic tape drives: query tape

QUERY TAPE 命令（缩写为 Q TA）显示可供系统使用并分配使用的磁带驱动器的状态。参见示例 5-13。QUERY TAPE ALL 显示可供系统使用的所有磁带驱动器。检查真实磁带驱动器的状态。

### Example 5-13 Displaying the status of the tape drives

```text
q tape
An active tape was not found.
Ready; T=0.01/0.01 11:58:29
```

### Real channel-to-channel adapters: query ctca

QUERY CTCA 命令可以检查可供系统使用且正在使用的真实通道到通道适配器的状态。参见示例 5-14。QUERY CTC ALL 命令显示所有可用的 CTC 设备。

### Example 5-14 Querying real CTC adapters

```text
q ctc
An active CTCA was not found.
Ready; T=0.01/0.01 12:00:26
```

### Real OSA devices: query osa

QUERY OSA ALL 命令显示真实 OSA 设备的列表。参见示例 5-15。QUERY OSA 命令显示正在使用的 OSA 设备。对于每个设备，显示以下信息：

- 它们专用的虚拟机
- 在虚拟机配置中用于引用真实 OSA 设备的虚拟设备号
- 设备类型（HIPER、OSA）
- 用于访问设备的通道路径标识符（CHPID）及其类型。

### Example 5-15 Displaying the status of real OSA devices attached to the partition

```text
q osa all
OSA 3020 ATTACHED TO TCPIP 3020 DEVTYPE OSA CHPID 0C OSD
OSA 3021 ATTACHED TO TCPIP 3021 DEVTYPE OSA CHPID 0C OSD
OSA 3022 ATTACHED TO TCPIP 3022 DEVTYPE OSA CHPID 0C OSD
```




```
OSA 3024 ATTACHED TO DTCVSW2 3024 DEVTYPE OSA          CHPID 0C OSD
OSA 3025 ATTACHED TO DTCVSW2 3025 DEVTYPE OSA          CHPID 0C OSD
OSA 3026 ATTACHED TO DTCVSW2 3026 DEVTYPE OSA          CHPID 0C OSD
OSA 3028 ATTACHED TO DTCVSW1 3028 DEVTYPE OSA          CHPID 0C OSD
OSA 3029 ATTACHED TO DTCVSW1 3029 DEVTYPE OSA          CHPID 0C OSD
OSA 302A ATTACHED TO DTCVSW1 302A DEVTYPE OSA          CHPID 0C OSD
OSA 3023 FREE   , OSA 3027 FREE   , OSA 302B FREE   , OSA 302C FREE
OSA 302D FREE   , OSA 302E FREE   , OSA 302F FREE
An offline OSA was not found.
OSA 302F is an OSA Agent
Ready; T=0.01/0.01 12:00:51
```

## 显示运行中的用户：query names

为了检查所需用户是否已正确自动登录，系统操作员可以使用 QUERY NAMES 命令（缩写为 Q N）。参见示例 5-16。该命令显示系统中当前运行的虚拟机列表及其状态，如下所示：

- DSC：机器处于断开连接状态运行
- L0003：机器已登录

VSM 机器是 VTAM 服务机器的用户标识，负责管理 TCPIP 用户。

**示例 5-16 显示运行中的用户**

```
q n
LNXKEN  - DSC , LNXGUI  - DSC , LNXCER  - DSC , FTPSERVE - DSC
TCPIP   - DSC , DTCVSW2 - DSC , DTCVSW1  - DSC , VMSRVR  - DSC
VMSERVU - DSC , VMSERVS - DSC , OPERSYMP - DSC , DISKACNT - DSC
EREP    - DSC , OPERATOR - SYSC, MAINT   -L0003
VSM     - TCPIP
Ready; T=0.01/0.01 12:02:00
```

## 网络状态：ifconfig 和 netstat

IFCONFIG 和 NETSTAT 网络命令位于 TCPMAINT 的 592 磁盘上。系统操作员必须先链接到该磁盘，然后才能发出这些命令。

IFCONFIG 命令显示 TCP/IP 网络的状态，包括 IP 地址、子网掩码和传输的数据量。参见示例 5-17。

**示例 5-17 显示 TCP/IP 网络的状态**

```
ifconfig
OSA3020 inet addr: 9.12.4.89 mask: 255.255.252.0
UP BROADCAST MULTICAST MTU: 1500
vdev: 3000 type: QDIO ETHERNET portname: UNASSIGNED
ipv4 router type: NONROUTER ipv6: DISABLED
cpu: 0 forwarding: ENABLED
RX bytes: 3529660 TX bytes: 3354354
Ready; T=0.01/0.01 13:43:59
```

NETSTAT 命令显示有关系统网络的更详细信息。发出 **NETSTAT** 命令将显示所有命令选项及其简要说明。例如，NETSTAT GATE 命令显示网络网关信息，如示例 5-18 所示。

**示例 5-18 显示网络网关信息**

```
netstat gate
VM TCP/IP Netstat Level 530

Known IPv4 gateways:

Subnet Address   Subnet Mask      FirstHop Flgs PktSz Metric Link
--------------   ---------------  -------- -------- ------ --------
Default          <none>           9.12.4.1 UGS  1500   <none> OSA3020
9.12.4.0         255.255.252.0    <direct> UT   1500   <none> OSA3020

Known IPv6 gateways: None
Ready; T=0.01/0.01 13:55:46
```

## 检查系统工作负载：indicate

INDICATE LOAD 命令（缩写为 **IND LOAD**）提供系统资源使用情况的概览。当从 B 类用户发出时，输出如示例 5-19 所示。第一行显示平均处理器利用率和系统中 CPU 的总数。接下来的三行显示扩展存储、小型磁盘缓存和分页活动的使用情况。接下来的四行显示四个队列中每个队列的用户数。

最后几行显示当前处理器利用率。示例中显示的系统显然没有在运行任何任务。

**示例 5-19 系统资源利用情况概览**

```
ind load
AVGPROC-000% 04
XSTORE-000000/SEC MIGRATE-0000/SEC
MCD READS-000000/SEC WRITES-000000/SEC HIT RATIO-00%
PAGING-0/SEC STEAL-00%
```

### 5.2.4 z/VM 关机工作流程

当 z/VM 系统关闭时，会执行一些重要步骤。其中一些步骤与 IPL 步骤（见第 230 页 5.2.1 节“z/VM IPL 工作流程”）相反，但它们是互补的。例如，将系统属性保存在检查点数据文件中。图 5-2 描述了该过程。

![](img/b0a4b9056f819dccd4781a5105c92d45_261_0.png)

图 5-2 z/VM 关机流程图

在 z/VM 关机流程图中，自上而下的步骤如下：

- 1. z/VM 向来宾系统（z/OS 来宾除外）发送关机信号，请求它们关闭。这使得来宾系统能够在整个系统关闭之前自行干净地关闭。此功能必须在 SYSTEM CONFIG 文件中启用（阅读第 175 页“在系统启动时自动启动虚拟交换机”）。
- 2. 系统干净地停止系统服务，例如日志记录和记账。
- 3. z/VM 将其系统属性保存在 RES 卷上的检查点数据文件中。





+   4. 所有正在运行的进程都将被终止。
+   5. z/VM 禁用 I/O 设备。
+   6. 正在运行的系统被终止。

示例 5-20 显示了 z/VM 关机过程的输出。

## 示例 5-20 z/VM 关机过程

```
00: 14:54:42 HCPWRP963I SHUTDOWN STEP USDAC - JOURNAL USER TERMINATION
00: 14:54:43 HCPWRP963I SHUTDOWN STEP MFRSD - TERMINATE HARDWARE LOADER
00: 14:54:43 HCPWRP963I SHUTDOWN STEP APISD - TERMINATE OTHER PROCESSORS
00: 14:54:44 HCPWRP963I SHUTDOWN STEP ENASD - DISABLE TERMINAL DEVICES
00: 14:54:45 HCPWRP963I SHUTDOWN STEP ISHDN - SHUT DOWN I/O SUBSYSTEM
00: 14:54:45 HCPWRP963I SHUTDOWN STEP TTRAL - TERMINATE CONCURRENT COPY SESSIONS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP SVACV - ACTIVATE TERMINATION SAVE AREAS
00: 14:54:46 HCPWRP963I SHUTDOWN STEP CHMOF - DISABLE CHANNEL MEASUREMENT
00: 14:54:47 HCPWRP963I SHUTDOWN STEP ISHDA - DISABLE ALL DEVICES
00: 14:54:47 HCPWRP963I SHUTDOWN STEP CKPSH - TAKE A CHECKPOINT
00: 14:54:48 HCPWRP963I SHUTDOWN STEP OPRCD - SAVE OPERATOR CONSOLE LIST
00: 14:54:48 HCPWRP963I SHUTDOWN STEP MCWMD - DETERMINE MACHINE CHECK STATUS
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SOVRS - RESET IBM DASD CU CHARACTERISTICS
00: HCPWRP962I VM SHUTDOWN COMPLETED IN 10 SEC
00: 14:54:49 HCPWRP963I SHUTDOWN STEP SVADV - DEACTIVATE TERMINATION SAVE AREAS
00: 14:54:50 HCPWRP961W SYSTEM SHUTDOWN COMPLETE
00: HCPGIR450W CP entered; disabled wait PSW 00020000 00000000 00000000 00000FFF
```

## 5.2.5 z/VM 服务

z/VM 以虚拟机的形式提供多种服务。虚拟机类似于 z/OS 中的启动任务、TSO 用户或批处理作业。与某些操作系统不同，CP 没有进程的概念。相反，CP 只知道如何运行虚拟机。这意味着，任何未直接内置于 CP 的附加服务功能都必须以服务虚拟机的方式实现。

服务虚拟机与其他虚拟机相同，只是它运行某些软件（通常基于 CMS），为系统上的部分或全部其他用户提供服务。

以下示例是服务虚拟机提供的服务：

- TCP/IP 网络协议栈
- 用户目录维护（Dirmaint）
- 安全管理器（RACF）
- 性能数据收集与报告（Performance Toolkit）
- 系统管理服务（SMAPI）

z/VM 中的服务虚拟机通常具有与其提供的服务对应的用户名。表 5-1 列出了几个常见的服务虚拟机及其所提供服务的简要说明。

表 5-1 常见的服务虚拟机

| 客户机名称 | 提供的服务 |
|---|---|
| TCPIP | TCP/IP 网络协议栈及 FTP、Telnet 等工具 |
| DIRMAINT | 用户目录维护 |
| DATAMOVE | 面向 DIRMAINT 的磁盘复制和格式化服务 |
| PERSFVM | 性能记录与报告 |
| RACFVM | 客户机、设备和服务的安全管理 |
| VMSERVE | 系统管理服务 |
| RSCS | 远程假脱机设备功能 |
| PVM | 远程通信和系统访问 |
| EREP | 错误记录 |
| DISKACNT | 用户记账记录 |
| OPERSYMP | 症状记录 |
| VMSERVR<br>VMSERVS<br>VMSERVU | 共享文件系统（SFS）支持 |

## 5.3 管理客户操作系统虚拟机

z/VM 中的客户机支持允许您运行多个生产操作系统映像。您可以使用 z/VM 中的客户机支持来开发、测试、管理和迁移与生产系统一起运行在 System z 上的操作系统。以下各节将讨论所支持的客户机系统以及如何操作这些虚拟机。

### 5.3.1 客户机支持

所有受支持的大型机操作系统都可以在 z/VM 下运行，包括 z/VM 本身。有关受支持的大型机操作系统列表、z/VM 提供的支持类型以及其他有用信息，请参阅《z/VM：一般信息》GC24-6095 中的说明。如果在 IFL 上运行，则只允许 z/VM 和 Linux。

> 提示：《z/VM：一般信息》GC24-6095 还提供了可用于任何 z/VM 版本的所有受支持硬件的列表。

让每个用户都是一个虚拟机的概念对于 z/OS 用户来说是新的。因此，下一节将解释如何管理它们（启动、暂停、恢复和停止）。

### 5.3.2 启动客户操作系统

每个客户操作系统都通过独立的 z/VM 虚拟机用户 ID 运行。登录这些用户 ID 的方式与任何其他 z/VM 用户 ID 相同，并且通常在 CMS 环境中启动运行。从登录会话中，可以将客户操作系统加载到该虚拟机的存储上并运行，其方式与在 LPAR 中运行基本相同。

在 z/VM 中，以这种方式启动操作系统仍类似于使用 IPL（初始程序加载）。当您对一个操作系统执行 IPL 时，它会控制虚拟机的存储；之前运行的其他操作系统会从内存中清除，不再控制虚拟机。请记住，CP 仍将继续运行，因为 CP 不是客户操作系统。

在 CP 中，您可以使用 IPL 命令执行 IPL。CP 可以直接从设备执行 IPL，此时操作系统将从设备上的数据中读取。或者，CP 可以从存储在共享内存中的数据执行 IPL，该共享内存称为命名保存系统（NSS）。要从设备执行 IPL，请给出要 IPL 的设备的虚拟设备号；参见示例 5-21。

## 示例 5-21 对 190 磁盘执行 IPL

```
IPL 190
z/VM V5.3.0    2007-05-02 16:25
Ready; T=0.01/0.01 09:37:40
```

在示例 5-21 中，我们对 190 磁盘执行了 IPL，该磁盘默认包含 CMS 操作系统。此时，CMS 正在运行，发出的任何命令都将首先由 CMS 处理。





NSS 是操作系统内核或核心的一个副本，已保存在共享的 CP 存储中。使用 NSS 对操作系统进行 IPL 与使用磁盘相比具有以下几个优点：

- 无论有多少个客户机对其执行了 IPL，内存中都只会存在操作系统的一个副本。如果您有大量客户机，这可以极大地节省存储空间。
- 由于操作系统只存在一个副本，因此，将使用该操作系统的所有用户更新到较新版本只需替换这一个 NSS 即可。

要从 NSS 进行 IPL，请提供已保存系统的名称；请参见示例 5-22。大多数 z/VM 安装都设置了 CMS NSS。

### 示例 5-22 对 CMS 命名系统执行 IPL

```
IPL CMS
z/VM V5.3.0    2007-05-02 16:25
Ready; T=0.01/0.01 09:37:40
```

示例 5-22 显示我们使用 CMS NSS 而不是 CMS 磁盘对 CMS 执行了 IPL。请注意，CMS 的启动方式与我们 IPL 190 磁盘时的启动方式完全相同。

> **注意：** 某些客户机操作系统要求您先执行 `SYSTEM CLEAR` 命令来清除客户机的虚拟内存，然后再对该客户机执行 IPL。或者，您也可以通过指定 CLEAR 参数，让 IPL 命令为您清除内存：
>
> `IPL 190 CLEAR`

## 5.3.3 在运行客户机操作系统时发出 CP 命令

客户机操作系统启动后，在终端输入的所有命令通常由该操作系统处理，而不是由 CP 处理。但有时，您可能出于各种原因需要与 CP 交互，例如链接新磁盘、查看系统上有多少其他用户、更改虚拟网络硬件或执行任何其他与 CP 相关的任务。

CP 提供了一种方法，让您可以发出绕过客户机操作系统而直接进入 CP 的命令。为此，我们使用 `#CP` 命令。您发出 `#CP` 命令，后跟任何您想要执行的 CP 命令。

例如，假设您启动了客户机操作系统，它只检测到一个 CPU，但您认为您的虚拟机有三个 CPU。第 251 页的示例 5-23 展示了如何验证您的虚拟机确实有三个 CPU。

### 示例 5-23 从客户机操作系统内向 CP 发出命令

```
#CP QUERY VIRTUAL CPUS
CPU 00 ID FF02991E20948000 (BASE) CP CPUAFF ON
CPU 01 ID FF02991E20948000 STOPPED CP CPUAFF ON
CPU 02 ID FF02991E20948000 STOPPED CP CPUAFF ON
```

当您发出 `#CP` 命令时，CP 会暂时挂起您的客户机操作系统，时间足够完成您的命令，然后恢复它。这对您的客户机操作系统是透明的。此过程通常非常快速且无缝。

### 注意事项：

- 这种从客户机操作系统内与 CP 交互的方法在大多数客户机操作系统中都能完美运行。但是，当您在 z/VM 客户机中运行 z/VM 时，它会失败。在这种情况下，您必须先暂停作为客户机操作系统运行的 z/VM，然后才能直接向底层 CP 发出命令。有关此主题的更多信息，请参阅第 251 页的 5.3.4“暂停客户机操作系统”。
- CMS 会假设您发出的任何它无法识别的命令都是 CP 命令，并将它们直接传递给 CP 执行。这意味着当您在 CMS 中时，不必使用 `#CP` 命令来强制 CP 执行命令。您只需正常执行 CP 命令，CMS 就会将该命令传递给 CP。

## 5.3.4 暂停客户机操作系统

CP 也有一条命令用于暂时暂停您的客户机操作系统。如果您必须发出大量 CP 命令，但又不想让客户机操作系统运行或干扰您的工作，您可能需要这样做。

如果您是正在调试客户机操作系统的程序员，您可能也想这样做。要停止客户机操作系统并将控制权返回给 CP，请输入以下命令：

```
#CP STOP
```

虽然此命令不会产生任何输出，但最终结果是客户机操作系统被停止，然后您可以直接与 CP 交互，直到您明确恢复运行该客户机操作系统为止。





这种暂停来宾操作系统的办法对几乎所有来宾操作系统都完美适用。然而，当你在 z/VM 来宾中运行 z/VM 时，它会失效。当你在 z/VM 来宾中运行 z/VM 时，本质上是 CP 作为你的来宾操作系统在运行。因此，你需要处理两个 CP 实例：

- 第一个级别的 CP 是你在登录系统并创建虚拟机时启动的 CP 实例。
- 第二个级别的 CP 是你在第一个级别 CP 实例内部对其进行 IPL 时创建的。

当你运行第二个级别 CP 时，#CP 命令会向你的第二个级别 CP 发出命令——而不是像你可能期望的那样向你的第一级 CP 发出命令。

图 5-3 显示了你拥有第二级 z/VM 系统时的场景。

![](img/b0a4b9056f819dccd4781a5105c92d45_267_0.png)

图 5-3 第一级和第二级 CP。

要退出你的第二级 CP 并直接向你的第一级 CP 发出命令，请按下 3270 终端键盘上的 PA1 键。当你使用 PA1 键（称为程序注意 1 键）时，第二级 CP（包括其正在运行的任何来宾操作系统）将被暂停，你的下一个命令将由你的第一级 CP 执行。

> 注意：当你按下 PA1 键暂停来宾操作系统时，你可能会发现它只在你执行一条命令时保持暂停状态。之后，它会自动再次恢复。如果发生这种情况，是因为你的第一级虚拟机的 RUN 参数已打开。RUN 参数控制此行为。
> 
> 在你按下 PA1 键并且你的第一级 CP 处于控制状态后，要关闭 RUN 参数，请执行以下命令：
> 
> SET RUN OFF
> 
> 从此时起，你可以执行任意多个第一级 CP 命令，而第二级 CP 不会在你指示之前恢复。
> 
> 你也可以发出 SET RUN ON 命令来打开 RUN 参数，如果你愿意的话。将 RUN 设置为 ON 将确保在你断开与来宾的连接时，你的来宾操作系统保持运行。

要恢复你的来宾操作系统（无论你运行的是什么来宾操作系统）请使用 BEGIN 命令。BEGIN 命令不带参数，也不产生自身输出（示例 5-24），尽管你可能会看到来宾操作系统继续执行时产生的输出。

## 示例 5-24 重新启动已停止的来宾操作系统

```
BEGIN
```

> 注意：在某些情况下，你可能需要在来宾操作系统能够恢复操作之前清除你的 3270 终端窗口。

当你完成对来宾操作系统的使用时，使用该操作系统用于正常关闭的任何命令或程序，因为不这样做可能导致数据丢失。

CP 提供了停止正在运行的来宾操作系统、清除系统存储并直接返回到 CP 的命令；请参阅第 254 页的示例 5-25。

## 示例 5-26 QUERY VIRTUAL CPUS 命令的输出

```
QUERY VIRTUAL CPUS
CPU 00 ID FF02991E20948000 (BASE) CP CPUAFF ON
```

此输出每 CPU 包含一行，可解释如下：

- 虚拟机有一个 CPU，该 CPU 地址为 00。
- 该 CPU 地址的 ID 为 FF02991E20948000。
- 编码在 CPU ID 中的是有关硬件和你的虚拟机运行环境的的信息。细节并不至关重要，因此此处未涵盖。
- 将 CPUAFF 设置为 ON 表示此 CPU 的 CPU 亲和性已打开。CPU 亲和性指的是在你的系统上处理不同类型的处理器和 CPU 的方式；这是一个复杂主题，超出了本书的范围。
- （BASE）表示基本 CPU。这意味着此 CPU 是你在登录虚拟机时创建的第一个 CPU。你的虚拟机需要此 CPU，并且它不能被分离或重新定义。所有其他 CPU 都可以被分离和重新定义。

## 定义 CPU

如果你拥有适当的权限，你可以为你的虚拟机定义更多 CPU。可以定义更多 CPU 的能力在你的虚拟机的目录条目中定义；这是由系统管理员控制的。

如果你被允许定义多于一个 CPU，限制为 2 到 64。要定义新的 CPU，请使用 DEFINE CPU 命令；请参阅示例 5-27。

## 示例 5-27 定义单个虚拟 CPU

```
DEFINE CPU 1
CPU 01 defined
```

DEFINE CPU 命令接受一个参数，该参数是你要新 CPU 拥有的 CPU 地址，或者如果你想定义多个 CPU，则是用破折号分隔的地址范围；请参阅示例 5-28。

## 示例 5-28 定义多个虚拟 CPU

```
DEFINE CPU 1-3
CPU 01 defined
CPU 02 defined
CPU 03 defined
```



> 注意：CP 不提供用于检查你可定义的 CPU 最大数量的命令。你可以通过反复尝试来确定该值，或者查看用户目录条目中 MACHine 语句的这个值。

## 分离 CPU

如果你确定不再需要某个已定义的虚拟 CPU，则可以使用 DETACH CPU 命令（缩写为 DET CPU）将其移除。该命令采用的参数格式与 DEFINE CPU 相同，这意味着你可以用一条命令分离单个 CPU 或一个范围内的多个 CPU；参见示例 5-29。

示例 5-29 使用 DETACH 命令分离 CPU

```
DETACH CPU 1
CPU 01 detached
```

> 注意：请谨慎使用此命令。分离 CPU 会导致你的虚拟机被重置，任何正在运行的操作系统都会立即停止。

## 5.3.8 管理存储（主内存）

每个虚拟机都有内存。任何特定虚拟机允许拥有多少存储空间由系统管理员决定，并在用户目录中定义。存储并不是真正的设备，因为它不像其他设备那样具有设备号。管理存储很简单，因为你几乎不需要了解它。

你的虚拟机内存是虚拟的，就像它的所有其他资源一样。由于它是虚拟的，它可以存在于物理内存中的任何位置，甚至可以在磁盘上（使用基于磁盘的存储来支撑物理内存通常称为分页或交换）。

与 CPU 一样，CP 允许你超额分配实际存储。当客户机未登录时，它完全不会消耗任何内存。只有当客户机登录时，CP 才会为它及其虚拟 CPU 分配内存，并创建设备。

但是，即使一个具有 1 GB 存储空间的客户机登录，它也不会立即使用其全部 1 GB 内存。如果它没有运行操作系统，那么它只使用了内存中极小的一部分。只有当客户机实际使用内存时，CP 才会分配物理内存来支撑客户机的虚拟内存。

然而，如果你只是运行 CP 而不运行客户操作系统，这就不成问题。在示例 5-31 中，我们将虚拟机的内存重新定义为 4 MB。

示例 5-31 将虚拟机的存储大小设置为 4 兆字节

```
DEFINE STORAGE 4M
STORAGE = 4M
Storage cleared - system reset.
```

如示例 5-32 所示，我们恢复到原来的大小。

示例 5-32 将虚拟机的存储大小设置为 32 兆字节

```
DEFINE STORAGE 32M
STORAGE = 32M
Storage cleared - system reset.
```

注意：

- 你的存储需求可能会因你在虚拟机上执行的操作而有所不同。然而，机器实际所需的存储空间可能没有你最初想象的那么多。对于典型的台式计算机，我们往往会高估内存需求，因为内存变得越来越便宜，而且较高的估量不会对系统造成性能损失。对于 z/VM，重要的是要了解你的客户操作系统、将要在其上运行的工作负载及其内存消耗特征。
- CP 不提供检查你可定义的存储最大大小的命令。不过，你可以通过尝试定义 99 太字节的存储大小（DEFINE STORAGE 99T）来确定该值，这很可能会远远超过你可定义的上限。在这种情况下，生成的错误消息会告诉你最大存储大小。

## 5.3.9 管理 DASD

直接存取存储设备（DASD）是一种简单的磁盘，你可以像在 z/OS 中一样访问它来存储数据。z/VM 磁盘分配在 DASD 卷的部分区域上，并包含对客户操作系统重要的文件。

## 检查你的 DASD

要获取可供你使用的所有虚拟 DASD 设备的列表，请使用 QUERY VIRTUAL DASD 命令；参见示例 5-33。

示例 5-33 QUERY VIRTUAL DASD 命令的输出

```
QUERY VIRTUAL DASD
DASD 0190 3390 LX6RES R/O 107 CYL ON DASD CD31 SUBCHANNEL = 0005
DASD 0191 3390 DKCD37 R/W 005 CYL ON DASD CD37 SUBCHANNEL = 0000
DASD 019D 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0006
DASD 019E 3390 LX6W01 R/O 250 CYL ON DASD CD32 SUBCHANNEL = 0007
DASD 0401 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0009
DASD 0402 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0008
DASD 0405 3390 LX6W01 R/O 156 CYL ON DASD CD32 SUBCHANNEL = 000A
```

该示例显示了几种可供我们使用的不同 DASD 设备。输出中每行显示一个 DASD 设备。在第一个 DASD 行中，各字段的含义如下：

- 0190 此 DASD 设备的虚拟设备号。
- 3390 所使用的实际 DASD 硬件类型。
- LX6RES 此虚拟 DASD 设备所在的真实 DASD 盘组的卷标。
- R/O 你对该设备的访问级别。
- 107 CYL 此 DASD 设备的大小（107），以柱面（CYL）表示。
- ON DASD CD31 此虚拟 DASD 设备所在的真实 DASD 盘组地址。
- SUBCHANNEL = 0005 我们的虚拟设备的子通道号。有关子通道的讨论超出了本书的范围。

以下各节将更详细地介绍最重要的参数。

## 虚拟设备号

如前所述，虚拟设备号用于在虚拟机中唯一标识此设备。它可以是任何尚未在虚拟机中定义的十六进制数。

## 类型

许多年前，当真实 DASD 有多种类型时，类型参数曾经很重要。如今，除了最古老的安装之外，你可能不会看到除 3390 之外的任何 DASD 类型。类型参数保留至今是为了


保持向后兼容性。一个例外是当你处理 VDISK 时（有关此主题的更多信息，请参阅第 264 页的“虚拟 DASD（VDISK）”）。

## 卷标签和实际设备地址

卷标签和实际设备地址都适用于承载此特定虚拟 DASD 设备的实际 DASD 卷。这些参数仅供参考，除非您是系统管理员，否则不太可能需要引用它们。

## 以柱面为单位的大小

DASD 设备的大小以柱面为单位。对于 3390 型 DASD，一个柱面正好相当于 849,960 字节，约等于 850 KB。

**注意：**

- 要确定你的 x 柱面 DASD 设备可容纳多少兆字节，请将 x 乘以 0.85。
- 要确定 x MB 数据需要多少柱面，请将 x 乘以 1.2。

## 创建 DASD

有时，你可能需要更多磁盘空间。但是，新 DASD 卷的定义必须由管理员执行，因为新的虚拟 DASD 设备必须由某处的实际磁盘支持，而一般用户无权从实际磁盘分配空间。

不过，你可能有权创建 TDISK 或 VDISK；有关这些主题的详细信息，请参阅第 262 页的“临时 DASD（TDISK）”和第 264 页的“虚拟 DASD（VDISK）”。另一个选择是向管理员申请共享文件池（SFS）空间；更多详细信息请参阅第 272 页的 5.3.11 节“CMS 共享文件系统”。

## 访问其他用户的 DASD

本书介绍了访问他人磁盘的概念（见第 130 页的“访问另一个用户的磁盘（链接）”）。拥有适当的权限后，你可以读取并执行程序，甚至可以写入其他磁盘。有关该主题的详细信息，请参阅该部分。

## 移除 DASD

你可以使用 DETACH 命令移除 DASD 设备，就像移除任何其他虚拟设备一样。该命令的唯一参数是要分离的设备的虚拟设备号。请参见示例 5-34。

### 示例 5-34 DETACH 命令示例

```
DETACH 592
DASD 0592 DETACHED
```

不必担心分离你所链接的磁盘会导致丢失其他人的数据。当你分离磁盘时，你所做的只是移除虚拟机中指向实际磁盘的虚拟设备。（不过，对于 TDISK 和 VDISK 而言并非如此。）

## 临时 DASD（TDISK）

TDISK 是一种虚拟 DASD 设备，从专门为创建临时磁盘而预留的一组实际 DASD 卷中分配。TDISK 是 temporary disk（临时磁盘）的缩写。

**重要：**

- 当你注销或系统发生故障时，你创建的任何 TDISK 都会被销毁，数据也会丢失。TDISK 旨在用作临时存储空间。
- 不要将重要数据的唯一副本存储在 TDISK 上。

其他用户 ID 无法链接 TDISK。

z/OS 提示：临时 z/VM DASD 类似于 z/OS 临时数据集，例如通过指定：

```
DSN=&&DATASET,DISP=(NEW,DELETE)....
```

### 创建 TDISK

并非所有 z/VM 安装都允许创建 TDISK。如果你的系统管理员未将系统设置为允许 TDISK 分配，或者在你请求时所有 TDISK 空间都已被使用，那么你的安装环境可能就属于这种情况。

但是，你可以使用 DEFINE T3390 命令请求分配 TDISK。T3390 参数指定你要创建临时 3390 型 DASD 设备。

请注意，DEFINE T3390 命令有两个参数：你要分配给新磁盘的虚拟设备号，以及该磁盘的柱面大小。

如果你想要一个设备号为 9FF、大小为 100 柱面的 TDISK，请使用示例 5-35 中所示的命令。

### 示例 5-35 定义 TDISK

```
DEFINE T3390 9FF 100
DASD 09FF DEFINED
```

> 注意：如果你想要一个 x 兆字节的 TDISK，请将 x 乘以 1.2，以确定创建时要指定的柱面数。

你可以使用 QUERY VIRTUAL DASD 命令验证你的 9FF 磁盘是否存在，如示例 5-36 所示。

### 示例 5-36 验证 TDISK 是否已创建

```
QUERY VIRTUAL DASD
DASD 0190 3390 LX6RES R/O 107 CYL ON DASD CD31 SUBCHANNEL = 0005
DASD 0191 3390 DKCD37 R/W 005 CYL ON DASD CD37 SUBCHANNEL = 0000
DASD 019D 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0006
DASD 019E 3390 LX6W01 R/O 250 CYL ON DASD CD32 SUBCHANNEL = 0007
DASD 0401 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0009
DASD 0402 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0008
DASD 0405 3390 LX6W01 R/O 156 CYL ON DASD CD32 SUBCHANNEL = 000A
DASD 0592 3390 LX6W01 R/O 070 CYL ON DASD CD32 SUBCHANNEL = 000B
DASD 09FF 3390 (TEMP) R/W 100 CYL ON DASD 59D4 SUBCHANNEL = 000C
```

请注意，TDISK 没有卷标签，因为它驻留在 TDISK 池中，而不是位于某个特定的实际 DASD 卷上。

要使用此 TDISK 空间存储临时文件，你必须在访问该磁盘时使用 CMS 格式化该磁盘。我们将在示例 5-37 中使用磁盘文件模式 F。

### 示例 5-37 格式化 TDISK

```
format 9ff f
DMSFOR603R FORMAT will erase all files on disk F(9FF). Do you wish to continue?
Enter 1 (YES) or 0 (NO).
1
DMSFOR605R Enter disk label:
tmp9ff
DMSFOR7331 Formatting disk F
DMSFOR7321 100 cylinders formatted on F(9FF)
Ready; T=0.01/0.05 10:44:37
```





## 删除 TDISK

你可以通过使用 DETACH 命令以与删除大多数其他虚拟设备相同的方式删除 TDISK；请参阅示例 5-38。该命令的唯一参数是需要分离的设备的虚拟设备号。

### 示例 5-38 删除 TDISK

```
DETACH 9FF
DASD 09FF DETACHED
```

## 虚拟 DASD（VDISK）

VDISK 是一种虚拟 DASD 磁盘包，它驻留在 z/VM 系统的主存储器中，而不是在真实的 DASD 上。这与你可能从其他操作系统中熟悉的 RAM 磁盘概念完全相同。因为它们存在于存储中，所以 VDISK 通常比普通 DASD 设备快得多，而且也小得多，因为它占用了系统的主存储。

### 重要提示：

- VDISK 完全存在于存储中，并且不由真实磁盘支持。这意味着当你注销或系统故障时，你的 VDISK 将被销毁，数据会丢失。VDISK 旨在作为临时存储空间。
- 不要将重要数据的唯一副本存储在 VDISK 上。

z/OS 提示：VDISK 与在 z/OS 中使用 VIO 类型单元定义类似。

## 创建 VDisk

并非所有 z/VM 安装都允许创建 VDISK。如果系统管理员未为 VDISK 分配设置系统，或者可用内存太少，则你的安装可能就是这种情况。

然而，你可以通过使用 DEFINE VFB-512 命令请求 VDISK 分配。VFB-512 是 512 字节虚拟固定块的缩写。

请注意，DEFINE VFB-512 命令需要两个参数：你想分配给新磁盘的虚拟设备号，以及该磁盘以 512 字节块为单位的大小。因此，如果你想要一个设备号为 8FF 且大小为 16 MB 的 VDISK，请使用第 265 页示例 5-39 中所示的命令。

## 注释：

- 除非在用户目录中定义，否则其他用户无法链接到你的 VDISK。
- 如果在你的目录中定义了 VDISK 并且你注销，只要有其他用户链接到它，它就*不会*被销毁。

每次分配 V-DISK 空间都必须在文件可以存储在磁盘上之前进行 CMS 格式化。

## 删除 VDISK

你可以通过使用 DETACH 命令以与删除任何其他虚拟设备相同的方式删除 VDISK。其唯一参数是要分离的设备的虚拟设备号；请参阅示例 5-42。

> 示例 5-42 删除 VDISK。

```
DETACH 8FF
DASD 08FF DETACHED
```

## 5.3.10  spool 设备

*spool 设备* 处理保存在队列中的文件或数据的有序列表。CP 的 spool 设备与其他 I/O 设备不同，因为它们与诸如 DASD 之类的真实设备无关。

你可以拥有三个 spool 设备，如表 5-3 所列。每个设备主要用于处理 spool 文件。spool 设备和文件是什么以及它们如何工作，其具体细节可能相当复杂，但对于绝大多数用户来说，大多数细节并不重要。

> 注意：本书对 spool 设备的描述极其简化，因为大多数用户可能永远不需要知道所有具体细节。然而，有关此主题的更多信息，请参阅 z/VM: Virtual Machine Operation, SC24-6128。

### 表 5-3 spool 设备类型

| Spool 设备 | 描述 |
|---|---|
| Reader | 一个虚拟穿孔卡阅读器 |
| Punch | 一个虚拟穿孔卡打孔机 |
| Printer | 一个虚拟打印机 |

就我们的讨论而言，这些设备在性质上是相似的。更具体地说，我们用于管理 spool 设备队列中文件的命令可以以相同的方式用于所有这些设备。在我们的示例中，我们集中讨论 reader 设备类型。

> **z/OS 提示：** z/OS 中的 spooling 任务在作业输入子系统（JES2 或 JES3）中执行。spool 数据保存在 JES2 HASP ACE 数据集或 JES3 等效项中。

## spool 设备的使用

在 z/VM 的早期，大多数安装都包括真实的打印机、穿孔卡阅读器和打孔机。当时，这些虚拟设备用于与真实硬件接口，因此你可以实际使用真实设备。然而，今天大多数安装都没有这些真实设备。但是，spool 设备用于处理虚拟机的输入和输出。

reader 是虚拟机的输入暂存区，可以看作是邮件收件箱。从该收件箱中，我们可以将文件 CP TRANSFER 给其他用途或通过 CMS RECEIVE 将文件接收到用户的 mdisk 存储上。

你可以通过使用 CMS 命令 SENDFILE，将文件从你的磁盘之一发送给其他用户。然后这些用户可以自由地将文件从他们的 reader 保存到他们的磁盘之一。SENDFILE 命令实际上使用你的 punch 设备将文件打孔到适当用户的 reader 队列中。

虚拟卡阅读器也经常用于引导其他操作系统或独立实用程序，包括 Linux 安装程序 RAM 文件。当 reader 队列顶部的那个文件包含可加载的操作系统或独立实用程序时，IPL 000C 将开始加载过程。

> **注意：** CMS 希望在虚拟设备号 000C 找到你的 reader，在 000D 找到你的 punch，在 000E 找到你的 printer。因此，出于这个原因，这些设备通常总是使用给定的设备号创建。

## 查询 spool 设备

查询 spool 设备可以提供大量信息，并且可以通过使用 QUERY 命令以与查询其他虚拟设备类似的方式完成。





在示例 5-43 中，我们查询了阅读器，它通常使用虚拟设备号 000C 定义。（如果您的阅读器地址不是 000C，请使用 QUERY VIRTUAL ALL 命令查找您的阅读器，如第 69 页“您的虚拟机资源”中所述。）

## 示例 5-43 查询假脱机设备

```
QUERY VIRTUAL 000C
RDR  000C CL * NOCONT NOHOLD  EOF      READY
000C 2540        CLOSED  NOKEEP NORESCAN  SUBCHANNEL = 0002
```

输出中显示的大多数参数涉及假脱机设备配置或假脱机设备如何处理您的假脱机文件。

## 创建假脱机设备

您可以使用 DEFINE 命令创建假脱机设备。在大多数情况下，您的阅读器已经为您定义好了。但如果尚未定义，请为 DEFINE 命令提供一个参数，以定义您正在创建的设备类型和虚拟设备号，如示例 5-44 所示。

## 示例 5-44 定义假脱机设备

```
DEFINE READER 000C

RDR  000C DEFINED
```

您可以将 READER 替换为 PUNCH 和 PRINTER，以创建这些类型的假脱机设备。

## 移除假脱机设备

与任何其他虚拟设备一样，您可以使用 DETACH 命令移除假脱机设备。将虚拟设备号指定为参数；请参见示例 5-45。

## 示例 5-45 移除假脱机设备

```
DETACH 100
RDR  0100 DETACHED
```

这同样适用于打孔机和打印机设备。

## 了解假脱机文件

假脱机文件可以看作排队等待进一步处理的文件。它们要么 destined to a virtual machine (punch)，要么 awaiting a virtual machine

> 注意：CP 不具备编辑功能。如果您必须编辑 CP 假脱机中的文件，则必须将其传输到阅读器队列（如果它在打孔或打印队列中），然后使用 CMS RECEIVE 命令将其接收到磁盘。

设置 z/VM 系统时，系统管理员会为假脱机文件预留一些磁盘空间。位于您的某个虚拟假脱机设备队列中的任何文件实际上都存在于这块预留为系统假脱机空间的磁盘空间上。

## 显示阅读器队列中的文件

CP 允许您显示阅读器队列中文件的信息。使用 QUERY READER ALL 命令，如示例 5-46 所示。

```
QUERY READER ALL
ORIGINID FILE CLASS RECORDS CPY HOLD DATE TIME NAME TYPE
FRED 0008 A PUN 00000017 001 NONE 06/07 13:46:01 TUX1 NETLOG
FRED 0009 A PUN 00000008 001 NONE 06/07 13:49:44 PROFILE EXEC
```

此示例显示阅读器队列中的两个文件：名为 TUX1 NETLOG 的文件和名为 PROFILE EXEC 的文件。输出的要点列于表 5-4 中。

| 列 | 描述 |
|--------|-------------|
| ORIGINID | 将文件发送到您的阅读器队列的虚拟机的用户名 |
| FILE | 分配给文件的唯一编号。我们将与其他命令一起使用它。 |
| DATE & TIME | 该文件放入阅读器队列的日期和时间 |
| NAME & TYPE | 创建者赋予该文件的文件名和类型 |

您可以通过在示例 5-46 所示的 QUERY READER 命令中将 READER 替换为 PRINTER 或 PUNCH，来查询打印机和打孔队列中的文件。

## 向您的阅读器添加文件

当其他用户向您发送文件，或者程序被设置为生成发送到您的用户 ID 的输出时，文件会被添加到您的虚拟阅读器中。

如果您希望将一个 CMS 文件添加到您的阅读器中，您可以直接使用 SEND FILE 命令将该文件发送到您的用户 ID。如果您希望将打印或打孔队列中的文件添加到您的阅读器，您可以传输该文件，如示例 5-47 所示。

## 示例 5-47 将文件从打印队列传输到阅读器

```
q prt all
OWNERID FILE CLASS RECORDS CPY HOLD DATE TIME NAME TYPE DIST
LNXGUI 0029 T CON 00000017 001 NONE 06/09 11:51:06 LNXGUI
Ready; T=0.01/0.01 10:20:26
```

```
trans prt 29 * rdr
RDR FILE 0029 SENT USER1 PRT WAS 0029 RECS 0017 CPY 001 T NOHOLD NOKEEP
00000001 FILE TRANSFERRED
Ready; T=0.01/0.01 10:21:26
```

```
q rdr all
OWNERID FILE CLASS RECORDS CPY HOLD DATE TIME NAME TYPE DIST
LNXGUI 0029 T CON 00000017 001 NONE 06/09 11:51:06 LNXGUI
Ready; T=0.01/0.01 10:22:26
```

## 删除阅读器中的文件

您可以使用 PURGE 命令从阅读器队列中移除文件。使用此命令，您可以指定清除单个文件、多个文件或阅读器队列中的所有文件。要清除单个文件，请指定要从哪个队列删除以及该队列中要删除的文件编号；请参见示例 5-48。

## 示例 5-48 从阅读器删除单个文件

```
PURGE READER 8
0000001 FILE PURGED
```

CP 响应表示已删除一个文件。如果要删除多个文件，请指定所有要删除的文件编号，并用空格分隔；请参见示例 5-49。

## 示例 5-49 从阅读器删除多个文件

```
PURGE READER 8 9 10
0000003 FILES PURGED
```

CP 现在响应表示已删除所有指定的三个文件。要删除阅读器队列中的所有文件，请指定 ALL 参数，如第 271 页的示例 5-50 所示。





## 5.3.11 CMS 共享文件系统

z/OS 程序员可能熟悉 z/OS UNIX 系统服务（z/OS UNIX 或 UNIX 系统服务），它允许 z/OS 访问 UNIX 文件。z/OS UNIX 文件系统与 z/OS 数据集之间最明显的区别是，从 UNIX 系统服务内部访问时，z/OS UNIX 是一个分层文件系统。

z/VM 文件系统 CMS 共享文件系统（SFS）允许你以分层方式查看系统：z/OS 程序员可能更习惯这种类型的分层文件系统。

SFS 是随 z/VM 一起提供的额外文件系统，它相对于普通的 CMS 文件系统具有多个优势。表 5-6 列出并比较了这些文件系统。

### 表 5-6 比较和对比 SFS 与普通 CMS 文件系统

| 共享文件系统 | CMS 文件系统 |
|---|---|
| 文件级共享 | 小磁盘级共享 |
| 最小分配：零 4096 字节块 | 最小分配：1 个柱面 |
| 分层文件系统 | 平面文件系统 |
| 分配可以动态更改 | 需要更大的小磁盘 |
| 文件级恢复 | 小磁盘级恢复 |

SFS 本质上是由服务器管理的 minidisk 存储集合。图 5-4 第 273 页所示的以下三个主要区域：

- **控制数据**
  保存文件池及其用户的定义。
- **日志数据**
  保存日志，以便在中断发生时可以回滚文件。
- **用户数据**
  保存用户数据。服务器从此处分配数据以提供给用户。

![](img/b0a4b9056f819dccd4781a5105c92d45_288_0.png)

图 5-4 共享文件系统（SFS）

使用 SFS，你不再使用 minidisk，而是由管理员将你注册到文件池，并从你使用的存储组中分配一定数量的 4096 字节块，类似于 CMS minidisk 的使用方式。

虽然访问空间与访问 CMS minidisk 相似，但你使用文件池名称与用户 ID 拼接，而不是 minidisk 设备号。例如，而不是使用 191 和 ACCESS 命令，你将使用：

```
VMSYSU:USERID
```

访问 SFS 后，用户可以使用命令创建目录和子目录，方式与在工作站上类似，如果需要可以创建分层文件结构。用户然后可以在文件级 GRANT 权限，以允许其他用户读取或写入其文件空间中的数据。

如果你已在文件池中分配了空间，请查看第 274 页表 5-7 中列出的命令。

### 表 5-7 与 SMS 相关的命令

| 命令 | 描述 |
|---|---|
| SET FILEPOOL | 设置（或重置）你的默认文件池；例如：set filepool vmsysu |
| QUERY FILEPOOL | 显示你的当前文件池；例如：query filepool current |
| QUERY LIMITS | 查看你可用的 4-K 块数量；例如：query limits |
| DIRLIST | 列出你的目录。这类似于使用 FILELIST 列出 CMS 文件。 |
| ACCESS | 为你的文件空间分配一个模式字母；例如：access vmsysu:cmsuser a ACCESS 与 minidisk 的访问方式类似。 |
| CREATE | 创建目录；例如：create directory test CREATE 类似于 PC 上的 mkdir。 |
| GRANT | 授予其他用户访问文件或目录的权限。 |

整个文件系统有一个管理员，负责备份以及根据需要将 minidisk 分配给存储组。

z/VM 随附三个文件池服务器：

- VMSERVR 由 z/VM 使用
- VMSERVS 由 z/VM 使用
- VMSERVU，一个示例用户文件系统

有关这些主题的更多信息，请参阅 z/VM: CMS File Pool Planning, Administration, and Operation, SC24-6074，以及 z/VM: CMS Commands and Utility Reference, SC24-6073。

## 5.4 作业调度和运行批处理作业

z/VM 和 Linux 提供了在一天/一月/一年的特定时间调度作业运行以及使其定期运行的方法。这对于安排非中断性系统维护任务很有用；运行这些任务时，你不必停止用户在给定时间可能正在进行的工作。任务可以包括：压缩系统日志以节省空间、更新备份等。





然而，批处理作业的调度并不是 z/VM 或 Linux 中的常见概念。实际上，要运行多个 *batch* 进程，你可以为此创建一个脚本，或者一次性全部运行，知道它们最终会竞争 I/O 资源。

以下部分概述了与 z/OS 作业输入子系统（JES）类似的工具。你可以通过使用这些调度工具并创建脚本来模拟批处理队列。

## 5.4.1 作业调度

本节比较了 z/VM 和 Linux 中的作业调度。

### z/VM 中的作业调度

调度作业通常使用无需人工干预的任务来完成，例如操作日志和创建备份。在 z/VM 中调度作业并不是一项常规任务，因为管理员通常使用来宾系统中的可用工具来执行这些任务。

为了完整性，作者在网上搜索并找到了一些产品，例如 CA VM:Schedule for z/VM、IBM Operations Manager for z/VM，以及随 z/VM 提供的两个免费工具（PROP 和 WAKEUP），它们可以实现作业调度。

### Linux 中的作业调度

Linux 系统有一个名为 cron 的实用工具，用于定期调度程序运行。调度信息放在 /etc/crontab 文件中，使用以下格式：

```
minute hour day month year username command
```

你可以将每个时间组件指定为整数。例如，使用 1 到 12 的数字表示一月到十二月。或者使用星号 (*) 字符指定一个或多个组件，它们被视为通配符。例如，月份组件中的 * 表示命令将在每个月的指定日期和时间运行。username 参数应为执行命令的用户的名称，出于安全或权限原因，该名称可能不同。例如，备份进程必须由可以读取所有目录中所有文件的用户运行。每个用户还可以在主目录中放置一个 crontab 文件。有关更多信息，请参阅：

http://www.linuxdoc.org

in batch mode. The system operator generates the batch machine by either of the following methods:

- Entering the BATCH parameter in the PARM field of the IPL command
- Specifying the NOSPROF parameter of the IPL command and entering the CMSBATCH command when the VM READ status appears.

After each job is executed, the batch facility IPLs itself, thereby providing a continuously processing batch machine. The batch processor IPLs itself by using the PARM option of the CP IPL command followed by a character string that CMS recognizes as peculiar to a batch virtual machine performing its IPL. Jobs are sent to the batch machine's virtual card reader from user terminals and executed sequentially. When no jobs are waiting for execution, the CMS batch facility remains in a wait-state, ready to execute a user job. The CMS batch facility is particularly useful for compute-bound jobs such as assemblies and compilations and for execution of large user programs, because interactive users can continue working at their terminals while their time-consuming jobs are run in another virtual machine. The system programmer controls the batch facility virtual machine environment by resetting the CMS batch facility machine's system limits, by writing routines that handle special installation input to the batch facility, and by writing exec procedures that make the CMS batch facility easier to use.

> Note: For in-depth information about how to use the CMS Batch Facility, refer to the CMS Planning and Administration, SC24-6078 at:
> http://publibz.boulder.ibm.com/epubs/pdf/hcsq2b10.pdf

## 在 Linux 中模拟批处理作业

本节为你提供了如何使用脚本模拟类似批处理的处理的非常简单的概述。你还可以安排 cron 在夜间运行脚本，例如运行每日销售报告。

本节中的场景使用了 shell 脚本⁷，一种被许多 Linux shell 解释的语言，来控制进程的批处理行为。此控制脚本一次运行一个程序。我们编写了两个简单的程序来对文本文件中的单词进行排序：一个按自然顺序，另一个按逆序。

脚本显示在第 278 页的示例 5-52 中。它调用 ./batch 文件夹中找到的所有程序，我们的排序程序。每个程序在我们的 ./input 文件夹中都有对应的输入文件（我们放置了用于排序的文件），每个输出都发送到我们的 ./output 文件夹。唯一的限制是

⁷ Shell 是一个解释用户输入、调用相应系统命令并显示该命令输出的程序。它是你在 Linux 控制台登录后看到的用户界面。





让我们的控制脚本起作用的方法是将输入文件命名为与批处理程序相同的名称，加上后缀 `-input`。当然，你可以编写比这更好的脚本。

## 示例 5-52

```
#!/bin/bash

for i in `ls ./batch`; do
echo "正在启动批处理程序 $i"
./batch/$i < ./input/${i}-input > ./output/${i}-output
done
```

用于输入我们第一个程序（按自然顺序排序的程序）的输入文件如图 5-5 所示。第二个程序的输入完全相同，只是它写的是“这是第二个未排序的文件”，而不是第一个。

```
this
is
unsorted
file
one
d
g
t
e
w
a
i
o
p
```

图 5-5 用作输入的文本文件。

如示例 5-53 所示，通过调用你创建的脚本的正确名称来运行控制器脚本。

## 示例 5-53

```
ceron:"/scripts # ./controller.sh
正在启动批处理程序 101_program
正在启动批处理程序 102_program
ceron:"/scripts #
```

环境，或者在几分钟内复制多个生产环境，而不是几天。关于这个主题的文献很多。

关于克隆的两个更多信息资源是：

- z/VM 和 Linux on IBM System z: The Virtualization Cookbook for SLES 10, SG24-7493。
- z/VM: Getting Started with Linux on System z, SC24-6096

## 5.6 监控系统

系统监控是管理计算机系统最重要的活动之一。有时，你必须查看系统资源使用情况，以决定是否应该为系统提供更多存储、DASD 或 CPU。或者，如果你能识别 LPAR、虚拟机或客户机中的资源浪费，你可以充分利用硬件。

z/VM 和 Linux 世界中存在帮助你实现这些目标的工具。第 7 章“性能监控和系统分析”（第 319 页）对它们进行了详细概述。

## 5.7 备份数据

即使系统可能非常健壮，仍然有理由定期备份数据：

- 自然灾害，例如火灾
- 意外断电导致数据损坏
- 硬件故障
- 破坏数据的程序错误

诸如 z/VM 和 Linux 之类的高端系统在生产系统中不能丢失数据。因此，它们有各种工具来帮助你备份数据。第 8 章“系统事件和日志、备份和恢复”（第 351 页）列出了可用的工具和命令。

## 5.8 维护系统

系统必须维护的原因有多种：

- 安全更新
- 软件版本升级
- 安装新功能

由于这些原因，关闭生产系统进行维护是不可取的。在第 9 章“应用系统维护”（第 387 页）中，我们讨论了维护 z/VM 系统的理想方式，以及它与 z/OS 的比较。

## 5.9 调试系统

尽管系统管理员可以通过持续监控和维护来小心维护其系统，但问题仍然会出现。然而，知道从哪里查找信息来解决问题，是区分普通管理员和优秀管理员的关键。第 8 章“系统事件和日志、备份和恢复”（第 351 页）解释了 z/VM 和 Linux 中可用的工具，这些工具使你能够根据事实得出关于问题的逻辑结论。

## 6.1 管理 z/VM 安全性

在部署虚拟化技术进行服务器整合时，绝不能忽视安全问题。这些问题如果得不到适当重视，可能会使公司面临风险。不可避免的是，新技术经常成为新安全威胁的目标。

在本章中，我们解释了 z/VM 如何为你的虚拟化实例提供安全性，并概述了如何保护你的系统。

在 z/VM 中，安全性一词指的是识别用户和控制资源访问的认证和授权方案。另一方面，系统完整性允许 z/VM 控制程序（CP）在不受客户虚拟机有意或无意的干扰或损害的情况下运行，并保护客户虚拟机免受相互干扰。

### 6.1.1 用户认证

用户登录 z/VM 系统是通过启动与 z/VM（本地或 Telnet）的终端会话，然后提供 z/VM 用户 ID 及其关联密码来实现的。本地终端会话非常安全，因为数据不通过网络传输。远程终端（Telnet）或文件传输（FTP）会话通过内部或外部 IP 网络传输，可以通过配置和使用 z/VM 安全套接字层（SSL）支持来变得高度安全。SSL 所需的处理由 z/VM 附带的 SSL 服务器提供，支持 128 位加密和解密服务。z/VM SSL 服务器是一个必须单独安装的 Linux for zSeries® 应用程序。用户提供用户 ID 和密码后，控制程序会验证该信息。如果用户 ID 和密码有效，则允许登录，并将终端会话连接到虚拟机的虚拟控制台。

如果你将 z/VM 视为一个充满虚拟服务器的虚拟机房，那么可以将虚拟机用户 ID 视为服务器周围的虚拟笼子。除非拥有钥匙——虚拟机密码，否则任何人都无法进入笼子。这与离散环境非常不同，在离散环境中，进入机房自动允许访问该机房中的所有服务器。

由于服务器控制台受 z/VM 密码保护，因此你可以更安全地省去通常给予服务器控制台的保护。自动化技术也得到了极大简化，例如，自动化工具不必输入 Linux 服务器的 root 密码即可将其关闭或重新启动。虽然乍一看这似乎会降低系统安全性，但实际上



通过无需自动化软件知道 root 密码来提高安全性。

z/VM 中提供的一种特殊功能是 **Logon By**。此功能使系统管理员能够定义一个共享虚拟机。当用户输入共享用户 ID 时，用户还提供他自己的用户 ID 和密码。这样，就保留了谁实际登录到共享用户 ID 的审计跟踪，并且避免了共享密码固有的麻烦。

诸如 rexec、ftp 和 nfs 之类的远程访问协议，都要求客户端使用 z/VM 用户 ID 和密码进行身份验证。z/VM 从不信任经过身份验证的客户端的主张。一旦身份验证通过，远程客户端拥有的访问权限与用户使用终端会话登录系统时所拥有的访问权限相同。

对于网络应用程序，z/VM 提供了一个 Kerberos 服务器以及允许程序利用 Kerberos 身份验证和加密功能的编程接口。请注意，IBM 提供的网络应用程序套件和 z/VM CP 不使用 Kerberos 身份验证。虽然 z/VM 可以允许对特定资源或虚拟机的匿名访问，但此类访问必须由 z/VM 系统管理员明确启用。

## 6.1.2 用户授权

登录 z/VM 系统后，虚拟机可以访问 z/VM 系统内的各种类型资源，包括整个 DASD 卷、minidisk、磁带驱动器、网络适配器、用户文件、系统文件等。z/VM 的安全功能设计为虚拟机只能访问明确允许其访问的资源。

这些权限由系统管理员授予，以便在虚拟机启动时，它自动获得对某资源的访问权限，即使该虚拟机在其他情况下无法访问该资源。或者，权限也可以由系统管理员或资源所有者动态授予。

某些资源是基于特权类可访问的，其他资源需要额外授权。z/VM 提供的<|message|>安全设施可以根据客户环境中的任何特殊或特定要求，通过添加外部安全管理器来增强。

尽管特权命令可用于更改正在运行的 z/VM 系统，系统管理员可能会选择在系统初始化期间设置系统配置选项。这是通过对 CP 系统配置文件进行更新来实现的。因此，必须严格控制对系统配置文件的访问。

## 6.1.3 入侵检测

作为 z/VM 入侵检测功能的一部分，如果登录被拒绝，则拒绝会被延迟，并在拒绝次数超过安装定义的上限时进行安全日志记录。当达到第二个上限时，用户 ID 的登录将被禁用，会发出操作员消息，并且终端会话将被终止。

z/VM 支持日志记录。虚拟机登录和链接到其他虚拟机的 minidisk 会被检测并记录下来。利用记录的信息，您可以识别尝试使用无效密码登录虚拟机或链接到 minidisk 的行为。

z/VM 的 TCP/IP 组件检测并报告各种网络入侵，包括 SYN 泛洪、Smurf 攻击和 Ping o’ Death。

z/VM 控制程序 CP 为虚拟机定义并分配虚拟处理器。这些虚拟处理器与 CP 可用的物理或逻辑处理器相匹配（如果 z/VM 在逻辑分区中运行）。如果在虚拟机中运行的操作系统能够使用多个处理器，它将像在专用硬件环境中运行一样在其虚拟处理器上调度工作负载。此功能对于在单处理器系统上甚至以多处理器模式测试客户操作系统非常有用。

## 6.1.4 虚拟处理器安全

CP 处理在可用物理处理器上调度虚拟处理器。物理处理器可以专用于单个虚拟机，也可以由多个虚拟机共享。请记住，CP 仅处理其控制的处理器，因此如果 z/VM 在 LPAR 中运行，逻辑处理器实际上可能与其他 LPAR 共享。

因此，我们有虚拟机在其一个或多个虚拟处理器上调度工作，这些虚拟处理器映射到一个或多个逻辑处理器，而逻辑处理器又可能再次映射到一个或多个物理处理器。无需担心，因为如果虚拟、逻辑或物理处理器配置发生变化，或者工作调度在不同的物理处理器上进行，并不会带来重大的安全风险。z/VM 控制程序在为一个虚拟机保存处理器状态并为另一个虚拟机恢复处理器状态时，就像 PR/SM™ 所做的那样


LPARs。因此，无法通过处理器寄存器中的残留数据在虚拟机之间传递任何信息。

## 6.1.5 z/VM 特权类

z/VM 是一种特权系统：用户可以没有特权，也可以拥有一个或多个特权类。每个特权类代表系统允许用户运行的 CP 命令的子集。每个特权类（有时称为 CP 特权类）是为特定工作或任务集定义的，从而创建一个用户无法执行任何命令的区域。一个用户可以分配到多个 CP 特权类。用户无法输入其未被分配的特权类中的命令。本节概述了 CP 特权类、它们关联的用户、任务和安全影响。

### 特权类 A

特权类 A 是主系统操作员。系统操作员是所有 z/VM 用户中拥有最强权力和特权的用户之一。系统操作员负责系统的可用性及其资源。系统操作员还控制会计、广播消息和设置性能参数。

### 特权类 B

特权类 B 是系统资源操作员。系统资源操作员控制实际资源的分配和释放，例如内存、打印机和 DASD。请注意，系统资源操作员不控制系统操作员或假脱机操作员已控制的任何资源。

### 特权类 C

特权类 C 是系统程序员。系统程序员更新 z/VM 系统的功能，并且可以更改真实机器中的实际存储。

### 特权类 D

特权类 D 是假脱机操作员。假脱机操作员控制假脱机文件和实际单元记录设备，例如打孔机、读卡机和打印机。

### 特权类 E

特权类 E 是系统分析师。系统分析师可以访问真实存储，并检查转储以确保系统尽可能高效、正确地运行。

### 特权类 F

特权类 F 是 IBM 服务代表。IBM 代表通过检查和访问真实输入/输出设备及其处理的数据来诊断和解决问题。

### 特权类 G

特权类 G 是普通用户。这是 CP 特权类中最普遍且无害的类别。特权类 G 用户可以输入的命令仅影响其自身的虚拟机。

### 特权类 ANY

此特权类中的命令可供任何用户使用。

### 特权类示例

特权类 A、B、C、D、E 和 F 需要值得高度信任的个人，且其活动需要仔细审计。例如，拥有特权类 B 或 C 的用户可以修改系统的 CP 特权。由于这种修改违反了受控访问保护配置文件 (CAPP) 安全策略，因此必须信任系统程序员和类似特权用户不会篡改 CP 特权系统（并且审计必须确认这种信任）。

注意：Red Hat Enterprise Linux 5 是第一个原生支持满足可信操作系统通用标准 (Common Criteria) 所需功能的 Linux 操作系统。这包括在以下保护配置文件下实现 EAL 4+ 认证的所有功能：受控访问保护配置文件 (CAPP)、基于角色的访问控制 (RBAC) 和标记安全保护配置文件 (LSPP)。

有关更多信息，请参阅 IBM：Red Hat Enterprise Linux 5 在 IBM System z 上的安全优势，网址为：
http://www.redhat.com/f/pdf/rhel/security_rhel5.pdf

另一个例子是，特权类 C 用户可以输入 `CP STORE HOST` 命令，该命令允许他们更改真实存储。它还可以使用户撤销 CAPP 分类。

特权类 G 用户在其自身虚拟机之外没有任何影响力。因此，除了对存储对象的访问之外，他们的安全相关性非常低。

ANY 特权类命令不能违反系统的安全策略。这是因为 ANY 特权类中的所有命令都是可审计的，并且受自主访问控制 (DAC) 或强制访问控制 (MAC) 的约束。



强制访问控制（MAC）。因此，ANY 类用户与 G 类用户一起，无法违反安全策略。在控制程序中，每个特权级别都是独立的，不依赖于其他级别。此外，每个特权类（命令子集）与一个或多个功能类型（用户子集）相关。

## 6.1.6 涉及安全的系统用户标识

某些用户标识是在安装过程中定义的。默认系统安装的标准用户标识如下：

- **OPERATOR：** 系统操作员和高特权用户标识，类似于 Linux 系统中的 root。
- **MAINT：** 系统管理和维护，从授权角度看与 OPERATOR 类似。
- **EREP：** 环境记录编辑和打印程序（EREP）是一个硬件异常检测和预测性故障系统。
- **DISKACNT：** 记录登录和注销等事件。
- **OPERSYMP：** 系统转储分析器和问题跟踪系统。检索症状记录。

## 6.1.7 安全相关语句

可以通过编辑系统配置文件来控制系统安全。配置文件位于分配为 PARM 的卷的分区上。该迷你磁盘通常归用户 ID MAINT 所有，位于迷你磁盘地址 CF1。该文件默认名为 SYSTEM CONFIG，但其名称可以在安装过程中更改。在 IPL 时，CP 程序会读取该文件，并使用文件中包含的语句来配置系统。

配置文件中包含以下与安全相关的命令语句：

### DEFINE 命令

使用 DEFINE 命令可以：

- 更改虚拟机的配置。
- 更改操作系统的配置。
- 为系统中的现有 CP 命令添加新别名。
- 向系统添加新的 CP 命令。
- 向系统添加现有 CP 命令的新版本。
- 向系统添加新的 DIAGNOSE 代码。
- 向系统添加新的来宾 LAN。

- **USER_DEFAULTS：** 定义系统上所有用户的默认属性和权限。

## 6.1.8 资源访问控制设施（RACF）

资源访问控制设施（RACF）许可程序可以满足用户的偏好，同时不会损害安全人员提出的任何关切。RACF 的数据安全方法是提供一种访问控制机制，该机制提供有效的用户验证、资源授权和日志记录功能。RACF 支持用户问责制的概念。它很灵活，对大多数最终用户几乎没有明显影响，并且对安装的当前操作几乎没有影响或没有影响。RACF 控制对多个虚拟存储（z/OS）和虚拟机系统上资源的访问，并保护这些资源。要使软件访问控制机制有效工作，它必须能够首先识别试图访问系统的人，然后验证该用户确实是那个人。使用 RACF，您负责保护系统资源（如迷你磁盘、终端以及共享文件系统（SFS）文件和目录），并负责颁发使这些资源可供用户使用的权限。

RACF 将您的分配记录在存储于 RACF 数据库的配置文件中。然后，RACF 参考配置文件中的信息来决定是否应允许用户访问系统资源。记录信息（例如对资源的尝试访问）并生成包含该信息的报告的能力，对资源所有者来说非常有用，并且对于平稳运行的安全系统非常重要。由于 RACF 可以识别和验证用户的用户 ID，并识别用户可以访问哪些资源，因此 RACF 可以记录尝试进行用户与资源交互的事件。此功能记录实际的访问活动或与系统预期使用的偏差。

RACF 具有许多日志记录和报告功能，允许资源所有者识别尝试访问资源的用户。此外，您或您的审计员可以使用这些功能记录所有检测到的成功和不成功的访问 RACF 数据库和受 RACF 保护的资源的尝试。记录所有访问尝试使您能够检测可能的安全暴露或威胁。日志记录和报告功能包括：

- **日志记录：** RACF 会将检测到的未授权进入系统的尝试的审计记录写入文件。或者，RACF 也可以为授权尝试或检测到的未授权尝试写入记录，包括：
  - 访问受 RACF 保护的资源
  - 发出 RACF 命令
  - 修改 RACF 数据库上的配置文件




- 发送消息：RACF 会向安全控制台发送消息，用于检测到的未经授权进入系统的尝试以及检测到的未经授权访问 RACF 受保护资源或修改 RACF 数据库中配置文件的尝试。

- 保留统计信息：可选地，RACF 可以保留所选的统计信息，例如用户进入系统的日期、时间以及次数，以及单个用户访问特定资源的次数。这些信息可以帮助安装更有效地分析和控制其计算机操作。此外，为了使安装能够跟踪并保持对其用户和资源的控制，RACF 提供了命令，使安装能够列出 RACF 数据库中配置文件的內容。

随 z/VM 版本 5.3 和 RACF 功能级别 5.3 引入的多个功能包括：

- 混合大小写 8 字符密码
- 最长 100 字符的混合大小写密码短语，包括空格
- 不可能将密码重置为默认组名
- 审计跟踪可以以 XML 格式卸载
- 通过 z/VM 新的 LDAP 服务器和实用程序进行远程授权和审计

> 注：有关 RACF 的更多信息，请参阅第 2.3.16 节“z/VM 的 RACF 安全服务器”，第 30 页。

## 6.2 定义用户

本节讨论在 z/VM 中定义用户或虚拟机的过程。它将其与定义分时选项/扩展（TSO/E）用户进行比较，后者与定义 STC 用户甚至批处理用户非常相似。此外，本节在不使用额外的 z/VM 产品 DIRMAINT 和 RACF 的情况下，说明了在原生 z/VM 系统上的过程。本节不讨论有关事务系统等用户的主题。

### 6.2.1 z/OS 假设

本节概述了在 z/OS 上定义用户以及用户定义和管理活动中涉及的 z/OS 方面。在下面的章节中，我们将讨论 z/VM 上的相同活动。

有关维护 z/VM 用户目录的更多信息，请参阅：

- z/VM：CP 规划和 administration，SC24-6083
- z/VM：CP 命令和实用程序参考，SC24-6081

## 安全产品

在早期，将用户定义到 TSO 意味着使用 ACCOUNT 命令在用户属性数据集（SYS1.UADS）中定义他们。如今，大多数安装已将该数据集合并到其 RACF 数据库或 ISV 产品类似物中。当在 OS/390® 中引入 UNIX System Services 时，不使用 RACF 或类似的安全系统就几乎不可能运行 z/OS 系统。因为 z/OS 的许多基本系统功能，例如 TCP/IP，都使用或利用 UNIX System Services，因此在没有某种安全服务器的情况下运营非常困难。甚至一些安装材料也指出，负责安装 z/OS 的用户应有权访问不同的资源类等作为先决条件。在没有安全产品的情况下，执行这些检查的标准模块或服务（SAF）很可能会使这些服务失败。

UADS（或 RACF 数据库或两者）包含每个 TSO 用户的数据（RACF 库还包含 STC 和批处理标识符以及其他与安全相关的数据）。该库包含用户 ID、关联的密码、帐号或代码、默认过程名称以及每个用户的全部属性。大多数安装可能根据其业务实施某种分组或基于角色的安全性。例如，所有系统程序员通常都是 RACF 定义的同一组的成员，以便在实施了此类分组时简化访问规则的管理。

库本身以加密格式存储，因此无法直接从库中检索密码和其他数据。这也适用于独立软件供应商（ISV）替代方案。

## 在 z/OS 中定义用户的典型流程

在 z/OS 中定义 TSO、STC 或批处理用户所需的典型任务集包括为以下领域建立规则：

| 安全产品 | 用户必须定义到安全服务器或产品，例如 RACF。 |
| 存储管理 | 必须解决如何管理用户数据的规则。这可能涉及调整存储管理服务（SMS）结构、定义目录别名、预分配 ISPF 配置文件等。 |
| 其他 | 许多站点还为其 TSO 用户进行各种定制，例如调整 TSO/ISPF JCL 过程或相关服务。会计也可能 |


应包含在内。也可能出现与性能相关的任务需求，例如调整 WLM 策略。

对于大多数 z/OS 站点，这些任务由组织内不同的业务线或部门执行。

## 6.2.2 在 z/VM 中定义用户

本节讨论如何在 z/VM 中定义用户。有关如何执行此操作的更多详细信息，请参阅第 121 页上的第 4 章“安装 z/VM 并创建 Linux 或 z/OS 客户机”。

### USER DIRECT 文件

所有 z/VM 用户都必须在 USER DIRECT 文件中进行定义和维护（前提是未安装 DIRMAINT 和 RACF）。该文件有两种形式：一种或多种源文件形式，位于一个或多个 CMS 文件上；以及一种编译后的对象形式，位于 CP 格式的磁盘上。在任何给定时刻只能有一个 USER DIRECT 处于活动状态，但可以访问多个。USER DIRECT 在 IPL 时按照预定义的搜索顺序进行读取。首先，在系统驻留卷上搜索有效的对象条目。如果不存在这样的条目，则按照 CP 拥有的卷在 CP 拥有列表中出现的顺序搜索所有 CP 拥有的卷。如果 CP 找不到有效对象，z/VM 会构造一个默认用户 ID OPERATOR。通过登录该用户，您就可以建立有效的 USER DIRECT 对象。

### USER DIRECT 的源格式

USER DIRECT 的源版本可以采用两种格式：单体格式，所有语句都包含在一个物理文件中；集群格式，包含一个索引文件，该索引文件可以指向一个或多个文件，这些文件包含构建对象 USER DIRECT 文件所需的语句。

> 注意：本书中对 USER DIRECT 的所有引用均针对单体源格式。有关集群格式的更多详细信息，请参阅 z/VM: CP Planning and Administration, SC24-6083。

### 定义迷你磁盘

z/VM 中的用户数据被划分为迷你磁盘实体。这意味着将您的磁盘卷划分为具有起始柱面地址的物理范围，并从此地址开始计算柱面数量。

## 6.2.5 DISKMAP 命令

此命令用于映射 z/VM 磁盘的磁盘范围。在本节中，我们关注包含用户迷你磁盘的磁盘，因为我们将定义一个新的 CMS 用户。

> 重要：DISKMAP 命令的使用是可选的，但强烈建议使用。

DISKMAP 会报告这些磁盘上的任何间隙或重叠。间隙意味着您没有完全使用磁盘，而重叠意味着用户正在使用磁盘的同一范围。后者意味着存在覆盖数据从而损坏磁盘的潜在风险，因此应避免。

该命令通过发出以下命令来调用：

```
DISKMAP fn ft (DOENDS
```

fn 是您要检查的 USER DIRECT 源文件的文件名，ft 是其文件类型。结束文本 DOENDS 会使在映射目录中将“END”指定为结束柱面/块的 MDISK 语句包含在 DISKMAP 输出文件中。

DISKMAP 的输出存储在运行该命令的用户的 A 驱动器上的 DISKMAP 文件中（fn 是被映射文件的文件名）。

要运行 DISKMAP 命令，用户必须至少具有 B 类特权。

第 297 页上的图 6-1 显示了文件 USER DISKMAP A 的输出（由于输出很长，图中已删除了一些行）。请注意第 00329 行上的 GAP（间隙），从柱面 1886 开始，共 114 个柱面，结束于 1999。

根据 DISKMAP 的输出，要定义的用户的迷你磁盘必须从柱面 2380 开始，这样才不会产生重叠（参见第 00337 行 LYDIA 191 结束于柱面 2379）。

最好对源文件的内容执行语法检查（并运行 DISKMAP 命令以检查是否可能存在磁盘重叠；参见第 296 页上的 6.2.5“DISKMAP 命令”）。

图 6-2 说明了 DIRECTXA 命令的语法。

![](img/b0a4b9056f819dccd4781a5105c92d45_313_0.png)

图 6-2 DIRECTXA 命令的语法

请注意，文件名（fn）和文件类型（ft）的默认值分别为 USER 和 DIRECT。因此，如果您希望为文件的源版本使用不同的名称（前提是存在 MYDIR DOCUMENT 和 MYDIR DIRECT 文件），以下命令的工作方式相同：

```
DIRECTXA MYDIR DOCUMENT
```

```
DIRECTXA MYDIR
```

要检查编辑后的源文件的语法，请发出以下命令：

```
DIRECTXA fn ft * (EDIT
```

这是一个有用的功能，尤其是对于维护此类文件经验有限的人员。

例如，源文件（MYDIR DOCUMENT）包含第 299 页上图 6-3 所示的语句。管理员输入的是 LUNCH，而不是 LINK。




```
PROFILE IBMDFLT
SPOOL 000C 2540 READER **
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
USER MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
```

Figure 6-3 Sample MYDIR DOCUMENT

By issuing the following command, the response from DIRECTXA is shown in Figure 6-4.

```
DIRECTXA MYDIR DOCUMENT * (EDIT
```

```
z/VM USER DIRECTORY CREATION PROGRAM – VERSION 5 RELEASE 3.0
USER MAINT 0190 0190 RR
HCPDIR751E INVALID OPERAND – USER FOLLOWING PROFILE IBMDFLT
HCPDIR775E PROFILE DEFINITION IBMDFLT IS INVALID AND WILL NOT BE PROCESSED FOR ANY USER DEFINITIONS THAT INCLUDE IT.
EOJ DIRECTORY NOT UPDATED
```

Figure 6-4 Response from DIRECTXA

We now define the new user, with a user ID of TOSK, and define a corresponding 191 minidisk as shown in the USER DIRECT file in Figure 6-5.

```
01967 ******************************
01968 USER TOSK TOSK 32M 64M G
01969 INCLUDE IBMDFLT
01970 ACCOUNT ACT4 CMSTST
01971 MACH XA
01972 IPL 190
01973 MDISK 191 3390 2380 010 LX6W02 MR READ WRITE MULTIPLE
```

Figure 6-5 Statements to define user TOSK

The line numbers in the file (in Figure 6-5) indicate the following statements:

- Line 01968 Statement USER initiates the statements for the user. The first occurrence of TOSK is the user ID, the second is password. The 32M is the initial amount of storage defined to this user, 64M is the maximum amount of storage. The G is the privilege class (or classes) assigned to the user, in this example only a general user.
- Line 01969 Includes what is known or defined as a PROFILE in USER DIRECT, and should be seen as statements that are common for several users.
- Line 01970 Assigns an account code for the user.
- Line 01971 Sets the architecture for user TOSK.
- Line 01972 States that this user should be IPLed from 190, which corresponds to CMS.
- Line 01973 Assigns the minidisk 191 on a 3390 device; starting at cylinder 2380 for 10 cylinders on volume LX6W02 in multiple read, establishes passwords for READ (only), WRITE and MULTIPLE READ, respectively. These are used when other users access TOSK's 191.

Invoking the following command gives the response shown in Figure 6-6:

```
DIRECTXA USER DIRECT (EDIT
```

```
Ready: T=0.01/0.01 15:28:21
DIRECTXA USER DIRECT (EDIT
z/VM USER DIRECTORY CREATION PROGRAM – VERSION 5 RELEASE 3.0
EOJ DIRECTORY NOT UPDATED
Ready: T=0.01/0.01 15:28:33
```

Figure 6-6 Response from DIRECTXA without errors

To check for disk gaps or overlaps, issue the following command; the response is in Figure 6-7:

```
DISKMAP USER DIRECT (DOENDS
```

```
DISKMAP USER DIRECT (DOENDS
File USER DISKMAP A has been created.
Ready: T=0.04/0.04 15:39:12
```

Figure 6-7 DISKMAP response

Browsing the USER DISKMAP file shows no gaps or overlaps within this disk's extents, with the exception of MAINT, which is overlapping the same extent. This is because MAINT has this disk (and several others) defined as a minidisk from cylinder 0 to END. This is a normal way of defining CP-owned disks.

Issue the following command to compile the updated source to an object and bring it online to z/VM. User ID TOSK can now log on.

```
DIRECTXA USER DIRECT
```

## 6.3 Networking access

This section describes how to give network access to your guest operating systems. We discuss how you define that access for LANs and VSWITCHes.

### DEFINE LAN command

Use this command to create a guest LAN that can be shared among virtual machines on the same VM system. Each guest LAN is identified by a unique combination of owner ID and LAN name. A VM user can create a simulated network interface card (NIC) and connect it to this LAN segment.

> Note: The SET LAN command can modify attributes of the guest LAN.

You can also define a LAN during system initialization using the DEFINE LAN configuration file statement. The class B form of the command allows the invoker to create a LAN for another user (for example, OWNERID SYSTEM) and specify whether accounting is on or off for the LAN being defined.

### DEFINE VSWITCH command

Use this command to create a CP system-owned switch (a virtual switch) to which virtual machines can connect. Each switch is identified by a switch name. A z/VM user can create a simulated QDIO network interface card (NIC) and connect it to this switch with the NICDEF directory statement. Under the DEFINE VSWITCH statement, the VLAN parameter is important, but optional, if you want to isolate guest subnets based on VLAN IDs.

## 6.4 Linux on System z resource management

This section discusses the necessary steps to dynamically add new resources, such as disks, network interface cards, and CPUs, to a Linux guest.

Explaining the details of Linux on System z hardware detection and configuration is beyond the scope of this book. Nevertheless, providing a brief outline of the processes involved is necessary to help you understand the next section.

### 6.4.1 Hardware detection and configuration

This section discusses device drivers and the in-memory file system.





有关两者的更多信息，请参考 *Devices Drivers, Features, and Commands, SC33-8289*。最新版本可在 Developerworks 网站上找到，网址为：
http://www.ibm.com/developerworks/linux/linux390/october2005_documentation.html

## Devices nodes and udev

Linux 内核将它所知的字符设备和块设备表示为一对数字，<major>:<minor>。某些主设备号为特定设备驱动程序保留，其他则在 Linux 启动时动态分配给设备驱动程序。例如，主设备号 94 始终是 DASD 设备驱动程序的主设备号，但通道连接磁带设备驱动程序没有固定的主设备号。一个主设备号也可以由多个设备驱动程序共享。

设备驱动程序使用 <minor> 号来区分各个物理或逻辑设备。例如，DASD 设备驱动程序为每个 DASD 分配四个次设备号：一个用于整个 DASD，另外三个用于最多三个分区。设备驱动程序根据设备驱动程序特定的命名方案为其设备分配设备名称。每个设备名称都与一个次设备号相关联。

历史上，Linux 在 /dev 目录中提供了一大套预定义的设备节点。大多数情况下，只使用了其中一小部分。从 Linux 2.6 开始，情况发生了变化：/dev 目录中只有少数预定义的设备节点；并且有一个用户空间守护进程 udev，负责在内核通知有新设备插入时动态在 /dev 中创建所需的设备节点。Udev 还可用于调整设备节点名称以适应组织的需要，或设置节点权限等。

有关 udev 功能的信息，请参阅 udev 手册页（man 7 udev）。

## /sys filesystem

在 Linux 中将设备上线后，设备驱动程序通过一个称为 /sys 的内存文件系统向用户空间公开其参数。

> **Note:** /sys 文件系统不存在于磁盘上。每次 Linux 客户机 IPL 时都会重新创建。
> 
> /sys 是 /proc 文件系统的继任者，后者仍存在以保持向下兼容。

/sys 文件系统允许初始化脚本或用户与驱动程序参数交互以查询或修改配置。

## 6.4.2 Disk management

### Enabling a disk in Linux

在新磁盘已定义、在目录中，并且已动态附加到客户机后（请参阅第 5.3.9 节“管理 DASD”，第 258 页所述），即可在 Linux 中启用它。

使用 lscss 命令，即 List Channel Subsystem，用于显示连接到系统的所有设备。示例 6-1 显示了在将磁盘作为设备 0200 附加之前和之后的 lscss 命令输出。

### Example 6-1 The lscss command output, before and after attaching new DASD to guest

```
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9     F0 F0 FF 5054585C 00000000
lnxguill:~ #
```

此时，磁盘已被 Linux 看到，但必须启用它，操作系统才能使用它。磁盘使用 chccwdev 命令启用，如示例 6-2 所示，该命令由 IBM 提供，并在 s390-tools 软件包中提供。

### Example 6-2 Enabling a disk for Linux

```
lnxguill:~ # chccwdev -e 0.0.0200
Setting device 0.0.0200 online
Done
lnxguill:~ #
```

要启用设备，请使用 -e 开关；要禁用设备，请使用 -d 开关。当磁盘上线时，Linux 内核会为磁盘分配一个设备节点


Initrd 映像：/boot/initrd-2.6.16.21-0.8-default
共享库：lib64/ld-2.4.so lib64/libacl.so.1.1.0
lib64/libattr.so.1.1.0 lib64/libblkid.so.1.0 lib64/libc-2.4.so
lib64/libcom_err.so.2.1 lib64/libc-2.4.so lib64/libext2fs.so.2.4
lib64/libhistory.so.5.1 lib64/libncurses.so.5.5 lib64/libpthread-2.4.so
lib64/libreadline.so.5.1 lib64/librt-2.4.so lib64/libuuid.so.1.2
驱动程序模块：dasd_mod dasd_eckd_mod dasd_fba_mod
DASD：0.0.0100(ECKD) 0.0.0101(FBA) 0.0.0150(ECKD) 0.0.0200(ECKD)
文件系统模块：jbd ext3
包含：initramfs fsck.ext3
17062 个块

initrd 已更新，在 IPL 之前 zipl 需要更新 IPL 记录！

lnxquill:/etc/sysconfig/hardware # zipl
使用配置文件 '/etc/zipl.conf'
在 '/boot/zipl' 中构建启动
构建菜单 'menu'
添加 #1: IPL 部分 'ipl' (默认)
添加 #2: IPL 部分 'failsafe'
准备启动设备：dasda (0100)。
完成。
lnxquill:/etc/sysconfig/hardware #

> 注意：对于某些设备驱动程序，次设备号和名称的分配在内核启动之间可能会发生变化，在虚拟机环境中添加或移除设备时也可能变化，甚至设备被设置离线和重新上线时也会变化。因此，相同的文件名可能会导致完全不同的设备。

我们重建初始 ramdisk，以确保所有磁盘在 IPL 时按您激活它们的顺序上线。

要在 RHEL5 中使更改永久生效：

- 1. 更新 /etc/modprobe.conf 文件，在 options 行 dasd_mod= 的末尾添加新的 DASD，如示例 6-5 所示：

### 示例 6-5 更新 modprobe.conf

```
[root@mbase40 etc]# cat /etc/modprobe.conf
options dasd_mod dasd=0100,0150,0101,200
alias eth0 qeth
alias hsi0 qeth
```

- 2. 重建初始 ramdisk 并更新启动记录，如第 306 页的示例 6-6 所示。

### 示例 6-6 在 RHEL5 中重新创建初始 ramdisk 并更新启动记录

```
[root@mbase40 etc]# mkinitrd -v /boot/initrd-2.6.18-8.1.3.el5.img
2.6.18-8.1.3.el5
Creating initramfs
Looking for deps of module uhci-hcd
Looking for deps of module ohci-hcd
Looking for deps of module ehci-hcd
Looking for deps of module ext3: jbd
Looking for deps of module jbd: dasd_mod
Looking for driver for device dasd
Looking for deps of module ccw:t3990Me9dt3390dm0C: dasd_mod dasd_eckd_mod
Looking for deps of module dasd_mod
Looking for deps of module dasd_eckd_mod: dasd_mod
Looking for driver for device dasd1
Looking for deps of module ccw:t6310m80dt9336dm10: dasd_mod dasd_fba_mod
Looking for deps of module dasd_fba_mod: dasd_mod
Looking for deps of module ide-disk
Using modules: /lib/modules/2.6.18-8.1.3.el5/kernel/fs/jbd/jbd.ko
/lib/modules/2.6.18-8.1.3.el5/kernel/fs/ext3/ext3.ko
/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_mod.ko
/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_eckd_mod.ko
/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_fba_mod.ko
/sbin/nash -> /tmp/initrd.sl4762/bin/nash
/sbin/insmod_static -> /tmp/initrd.sl4762/bin/insmod
copy from '/lib/modules/2.6.18-8.1.3.el5/kernel/fs/jbd/jbd.ko' [elf64-s390]
to '/tmp/initrd.sl4762/lib/jbd.ko' [elf64-s390]
copy from '/lib/modules/2.6.18-8.1.3.el5/kernel/fs/ext3/ext3.ko'
[elf64-s390] to '/tmp/initrd.sl4762/lib/ext3.ko' [elf64-s390]
copy from
'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_mod.ko'
[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_mod.ko' [elf64-s390]
copy from
'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_eckd_mod.ko'
[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_eckd_mod.ko' [elf64-s390]
copy from
'/lib/modules/2.6.18-8.1.3.el5/kernel/drivers/s390/block/dasd_fba_mod.ko'
[elf64-s390] to '/tmp/initrd.sl4762/lib/dasd_fba_mod.ko' [elf64-s390]
Adding module jbd
Adding module ext3
Adding module dasd_mod with options dasd=0100,0150,0101,200
Adding module dasd_eckd_mod
Adding module dasd_fba_mod
```

> 注意：mkinitrd 命令的语法在 RHEL5 和 SLES10 之间有所不同。

## Linux 逻辑卷管理器

Linux 系统提供了一个功能，用于在您最初不知道分区将占用多少空间时管理磁盘：逻辑卷管理器（LVM）。LVM 允许您将多个磁盘合并在一起，形成一个更大的逻辑磁盘，然后在这个逻辑上更大的磁盘上组织您的分区。图 6-8 显示了在 LVM 下管理磁盘的示例。

![](img/b0a4b9056f819dccd4781a5105c92d45_322_0.png)

*图 6-8 Linux LVM 管理四个 DASD。*

如您所见，四个 DASD（1、2、3 和 4）被用来形成一个容纳系统分区的单一逻辑磁盘。根文件系统（/）*实际上*分配在三个不同的 DASD 上。系统并不知道也不关心这一点，因为 LVM 代码处理地址转换并访问真实磁盘上的数据。/home 分区也跨越两个 DASD，而 /var、/tmp 和 /opt 分区位于单个 DASD 上。

在第 171 页的 4.4 节“安装 Linux”中，我们选择在多个 3390-3 卷上为其根文件系统腾出空间。例如，假设我们创建的 3 GB /home 分区空间刚刚用完，我们希望给它更多空间。解决此问题的传统方法是向系统引入一个新的 DASD，该 DASD 大于承载 /home 分区的那个，并将其移动


将内容复制到新的磁盘区域。这非常笨拙、耗时且容易出错。而使用LVM，这就变成了一项简单的任务。

扩展逻辑卷（例如我们Linux安装中的/var分区）只需向逻辑组添加一块磁盘或磁盘的一个条带，以便将这个新空间分配给其任何逻辑卷。粗略打个比方，这类似于在客厅旁边新建一个房间，然后拆掉它们之间的墙壁。你得到的是完全相同的客厅和额外的空间。图6-9以磁盘为例说明了这一点。

![](img/b0a4b9056f819dccd4781a5105c92d45_323_0.png)

图6-9 通过向LVM添加更多DASD来扩展Linux分区

各种Linux发行版（如YaST）提供了用户通过界面与LVM交互的机制。在没有这种界面的系统中，命令也可以完成LVM管理。需要了解的几个命令如下：

- **pvcreate** 在磁盘上创建物理卷条目，以便LVM识别该磁盘。
- **vgscan** 扫描所有磁盘以查找卷组，并构建文件 `/etc/lvmtab` 和 `/etc/lvmtab.d/*`，这些文件是所有其他LVM命令的数据库。
- **vgcreate** 使用作为参数传入的磁盘创建卷组。这些磁盘必须先用pvcreate初始化。
- **vgextend** 将磁盘添加到卷组。该磁盘必须先用pvcreate初始化。
- **lvcreate** 在卷组内创建逻辑卷。
- **lvremove** 从卷组中移除逻辑卷。应仅对空卷或数据不再需要的卷使用此命令。
- **lvextend** 使用卷组中未分配的空间扩展逻辑卷。

要扩展我们的3 GB /home分区：

1. 以z/VM MAINT身份，将另一个3390-3 DASD连接到我们的z/VM系统。
2. 以z/VM MAINT身份，在其上定义一个迷你磁盘并将其分配给我们的Linux客户机。
3. 以Linux root身份，使用vgextend将其添加到我们的卷组。
4. 以Linux root身份，使用lvextend，利用新添加到卷组的存储空间扩展我们的/home逻辑卷。

有关Linux LVM及其使用方法的更详细讨论，请参阅《Linux for IBM eServer zSeries and S/390: Distributions》，SG24-6264。

您还可以参考以下网址的LVM HOWTO：

http://tldp.org/HOWTO/LVM-HOWTO/

有关LVM本身的性能讨论，请参阅：

- 磁盘性能优化：  
  http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_optimizedisk.html
- 卷管理：  
  http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_volMan.html

## 6.4.3 网络管理

本节详细介绍了向正在运行的Linux客户机添加额外网络接口所需的步骤；然后将此接口连接到VSWITCH、GUEST-LAN或HiperSockets网络。在客户机的网络连接建立后，配置Linux（SLES 10或RHEL 5）。

### SUSE Linux Enterprise Server 10（SLES 10）

要配置Linux使用该连接：

1. 确保Linux能看到这些设备；我们使用`lscss`命令（第310页的示例6-7）。

**示例6-7 检查新设备的可用性**

```
lnxquill:~# lscss
Device  Subchan. DevType CU Type Use  PIM PAM POM CHPID
----------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9      F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes  F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9      F0 F0 FF 5054585C 00000000
0.0.0D20 0.0.0013 1732/01 1731/01    80 80 80 21000000 00000000
0.0.0D21 0.0.0014 1732/01 1731/01    80 80 80 21000000 00000000
0.0.0D22 0.0.0015 1732/01 1731/01    80 80 80 21000000 00000000
```

2. 在`/etc/sysconfig/hardware`中创建一个新的配置文件（示例6-8）。

**示例6-8 创建新的配置文件**

```
lnxquill:/etc/sysconfig/hardware # cp -arv skel/hwcfg-qeth hwcfg-qeth-bus-ccw-0.0.0d20
'skel/hwcfg-qeth' -> 'hwcfg-qeth-bus-ccw-0.0.0d20'
```

3. 更新配置文件以反映Linux网络硬件配置，尤其是指定端口名称的CCW_CHAN_IDS和CCW_CHAN_MODE（示例6-9）。

**示例6-9 更新网络硬件配置文件**

```
#!/bin/sh
#
# hwcfg-qeth
#
# Default configuration for a qeth device
# $Id: hwcfg-qeth 1069 2004-09-02 18:23:18Z zoz $
#
STARTMODE="auto"
MODULE="qeth_mod"
MODULE_OPTIONS=""
MODULE_UNLOAD="yes"
# Scripts to be called for the various events.
SCRIPTUP="hwup-ccw"
SCRIPTUP_ccw="hwup-ccw"
SCRIPTUP_ccwgroup="hwup-qeth"
SCRIPTDOWN="hwdown-ccw"
# CCW_CHAN_IDS sets the channel IDs for this device
# The first ID will be used as the group ID
CCW_CHAN_IDS="0.0.0d20 0.0.0d21 0.0.0d22"
```




# CCW_CHAN_NUM 设置此设备的通道数
# qeth 设备始终为 3
CCW_CHAN_NUM=3

# CCW_CHAN_MODE 设置 OSA-Express 设备的端口名称
# CCW_CHAN_MODE="LZ4LAN01"

# QETH_OPTIONS 设置 OSA-Express 或
# HiperSockets 设备的额外选项。有效参数为：
# add_hhlen buffer_count broadcast_mode canonical_macaddr checksumming
# fake_broadcast fake_ll priority_queueing route4 route6
# QETH_OPTIONS="fake_ll=1"

# QETH_IPA_TAKEOVER 启用此设备的 IP 地址接管
# QETH_IPA_TAKEOVER=0

**重要：** 设备号必须为小写。

- 4. 在 `/etc/sysconfig/network` 中创建网络配置文件  
  （示例 6-10）。

_示例 6-10  创建网络配置文件_

```text
lnxgqill:/etc/sysconfig/network # cp -arv ifcfg-qeth-bus-ccw-0.0.0600 ifcfg-qeth-bus-ccw-0.0.0d20
ifcfg-qeth-bus-ccw-0.0.0d20
`ifcfg-qeth-bus-ccw-0.0.0d20' -> `ifcfg-qeth-bus-ccw-0.0.0d20'
```

- 5. 使用您的 TCP/IP 配置更新配置文件（示例 6-11）。

_示例 6-11  更新 TCP/IP 配置_

```text
lnxguill:/etc/sysconfig/network # cat ifcfg-qeth-bus-ccw-0.0.0d20
BOOTPROTO="static"
UNIQUE=""
STARTMODE="onboot"
IPADDR="172.0.0.1"
NETMASK="255.255.255.0"
NETWORK="172.0.0.0"
BROADCAST="172.0.0.255"
```

- 6. 在 Linux 中启用网络接口（示例 6-12）。

_示例 6-12  启用网络接口_

```text
lnxguill:/etc/sysconfig/hardware # echo '0.0.0d20,0.0.0d21,0.0.0d22' >
/sys/devices/qeth/0.0.0d20/portname
lnxguill:/etc/sysconfig/hardware # echo 1 >
/sys/devices/qeth/0.0.0d20/online
```

7. 确保设备已上线（示例 6-13）。

# 示例 6-13 检查设备是否已上线

```
lnxguill:/etc/sysconfig/hardware # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes  F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9     F0 F0 FF 5054585C 00000000
0.0.0020 0.0.0013 1732/01 1731/01 yes  80 80 80 21000000 00000000
0.0.0021 0.0.0014 1732/01 1731/01 yes  80 80 80 21000000 00000000
0.0.0022 0.0.0015 1732/01 1731/01 yes  80 80 80 21000000 00000000
```

8. 使用 rcnetwork 服务重启命令重新加载网络配置（示例 6-14）。

# 示例 6-14 重启网络配置服务

```
lnxguill:/etc/sysconfig/hardware # rcnetwork restart
Shutting down network interfaces:
    eth0
    eth0      configuration: qeth-bus-ccw-0.0.0600                done
    eth1
    eth1      configuration: qeth-bus-ccw-0.0.0d20                done
Shutting down service network . . . . . . . . . . . . . . . . . done
Hint: you may set mandatory devices in /etc/sysconfig/network/config
Setting up network interfaces:
    lo
    lo        IP address: 127.0.0.1/8                          done
    eth0
    eth0      configuration: qeth-bus-ccw-0.0.0600
    eth0      IP address: 9.12.5.66/23                         done
    eth1
    eth1      configuration: qeth-bus-ccw-0.0.0d20
    eth1      IP address: 172.0.0.1/24                         done
Setting up service network . . . . . . . . . . . . . . . . . . done
```

9. 检查 Linux TCP/IP 配置，以确保已创建新的接口（示例 6-15）。

# 示例 6-15 检查 Linux TCP/IP 配置

```
lnxguill:/etc/sysconfig/hardware # ifconfig -a
[...]
eth1      Link encap:Ethernet  HWaddr 02:00:01:00:00:05
          inet addr:172.0.0.1  Bcast:172.0.0.255  Mask:255.255.255.0
          inet6 addr: fe80::200:100:100:5/64 Scope:Link
```

```
NETTYPE=qeth
NETWORK=172.0.0.0
ONBOOT=yes
PORTNAME=
SUBCHANNELS=0.0.0d20,0.0.0d21,0.0.0d22
TYPE=Ethernet
```

> 重要：设备号必须为小写。

4. 在 Linux 中启用网络接口（示例 6-19）。

# 示例 6-19 启用网络接口

```
[root@mb ase40 etc]# echo '0.0.0d20,0.0.0d21,0.0.0d22' > /sys/bus/ccwgroup/drivers/qeth/group
[root@mb ase40 etc]# echo 1 > /sys/devices/qeth/0.0.0d20/online
```

5. 确保设备已上线（示例 6-20）。

# 示例 6-20 检查设备是否已上线

```
[root@mb ase40 etc]# lscss
Device  Subchan. DevType CU Type Use  PIM PAM POM CHPID s
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9    F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9    F0 F0 FF 5054585C 00000000
0.0.0D20 0.0.0013 1732/01 1731/01 yes 80 80 80 21000000 00000000
0.0.0D21 0.0.0014 1732/01 1731/01 yes 80 80 80 21000000 00000000
0.0.0D22 0.0.0015 1732/01 1731/01 yes 80 80 80 21000000 00000000
```

6. 使用 rcnetwork 服务重启命令重新加载网络配置（示例 6-21）。

# 示例 6-21 重启网络配置服务

```
[root@mb ase40 etc]# service network restart
Shutting down interface eth0: [  OK  ]
Shutting down interface eth1: [  OK  ]
Shutting down loopback interface: [  OK  ]
Bringing up loopback interface: [  OK  ]
Bringing up interface eth0: [  OK  ]
Bringing up interface eth1: [  OK  ]
```

7. 检查 Linux TCP/IP 配置以确保已创建新的接口（示例 6-22，第 315 页）。





## 示例 6-22 检查 Linux TCP/IP 配置

```
[root@mbase40 etc]# ifconfig -a
[...]
eth1 Link encap:Ethernet HWaddr 02:00:01:00:00:05
inet addr:172.0.0.1 Bcast:172.0.0.255 Mask:255.255.255.0
inet6 addr: fe80::200:100:5/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1492 Metric:1
RX packets:0 errors:0 dropped:0 overruns:0 frame:0
TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:0 (0.0 b) TX bytes:936 (936.0 b)
[...]
```

在 z/VM 下运行 Linux 时，您可以动态地向已相应准备好的客户机添加虚拟 CPU，而无需重新 IPL。

## 设置

检查 LNXGUI 目录条目并修改其初始化参数。

### LNXGUI 目录条目

LNXGUI 目录是一个运行 ESA 架构的虚拟机，支持最多四个 CPU。在 IPL 时，客户机中定义了两个 CPU。参见示例 6-23。

### 示例 6-23 LNXGUI 目录条目的摘录

```
MACHINE ESA 4
CPU 00 BASE
CPU 01
```

### LNXGUI 初始化参数

在 Linux 端，您必须告诉内核它可以使用比 IPL 时实际检测到的更多的 CPU。这是通过在 zipl.conf 参数行中添加选项 additional_cpus 来完成的，如示例 6-24 所示。

### 示例 6-24 LNXGUI zipl.conf

```
# Modified by YaST2. Last modification on Tue May 20 19:07:54 UTC 2008
[defaultboot]
defaultmenu = menu
[...]

###Don't change this comment - YaST2 identifier: Original name: ipl###
[ipl]
    target = /boot/zipl
    image = /boot/image
    ramdisk = /boot/initrd,0x1000000
    parameters = "root=/dev/dasda1  TERM=dumb additional_cpus=2"
[...]
```

更新文件 /etc/zipl.conf 后，您必须通过运行命令 zipl 来更新引导记录以反映新配置。重新启动 Linux 使更改生效。

## 向正在运行的 Linux 客户机添加虚拟 CPU

如果客户机设置正确，您可以按如下方式向正在运行的 Linux 客户机添加 CPU：

- 1. 使用类 G 命令 DEFINE CPU 在 Linux 虚拟机中定义新的 CPU（示例 6-25）。

### 示例 6-25 在 Linux 虚拟机中定义新的虚拟 CPU

```
00: CPU 00 ID FF04DE5020978000 (BASE) CP CPUAFF ON
00: CPU 01 ID FF04DE5020978000 CP CPUAFF ON
00:
00: CP DEFINE CPU 02
00: CPU 02 defined
00:
00: CP Q CPUS
00: CPU 00 ID FF04DE5020978000 (BASE) CP CPUAFF ON
00: CPU 01 ID FF04DE5020978000 CP CPUAFF ON
00: CPU 02 ID FF04DE5020978000 CP CPUAFF ON
```

虚拟机在 IPL 时有两颗 CPU 处于活动状态，现在有三颗。Linux 客户机尚未意识到此额外 CPU 资源的可用性，如示例 6-26 所示。

### 示例 6-26 初始 CPU 配置

```
lnxguill:~ # cat /proc/cpuinfo
vendor_id : IBM/S390
# processors : 2
bogomips per cpu: 3735.55
processor 0: version = FF, identification = 04DE50, machine = 2097
processor 1: version = FF, identification = 04DE50, machine = 2097
```

- 2. 通过发出以下命令在 Linux 中激活 CPU：

```
lnxguill:~# echo 1 > /sys/devices/system/cpu/cpu2/online
```

CPU 被激活时，以下消息会列在日志文件中：

```
Jun 12 15:04:00 lnxguill kernel: cpu 2 phys_idx=2 vers=FF
ident=04DE50 machine=2097 unused=8000
```

- 3. 作为管理员，使用 cat /proc/cpuinfo 命令检查 Linux 看到的 CPU 数量，如示例 6-27 所示。

### 示例 6-27 查询 CPU 数量

```
lnxguill:~# cat /proc/cpuinfo
vendor_id      : IBM/S390
# processors    : 3
bogomips per cpu: 3735.55
processor 0: version = FF,  identification = 04DE50,  machine = 2097
processor 1: version = FF,  identification = 04DE50,  machine = 2097
processor 2: version = FF,  identification = 04DE50,  machine = 2097
```

## 性能监控和系统分析

在本章中，我们介绍 z/VM 调度概念和监控命令，并将这些命令与 z/OS 等价物联系起来。我们还介绍 z/VM 监控工具和性能调优概念。本章还讨论了与在 System z 上运行 Linux 相关的监控概念和技术。

### 目标

完成本章后，您应该能够：

- 了解 z/VM 调度概念的基础知识
- 了解与性能监控相关的 CP 命令的使用
- 描述 z/OS 命令和监控概念
- 识别 z/VM 可用的监控工具
- 讨论系统监控最佳实践





## 7.1 监控 z/VM

本节介绍 z/VM 调度基础，以及 System z、z/VM 和 Linux 监控命令。

在查看 z/VM 系统性能时，可以考虑的方面很多，包括以下领域：

- 用户响应时间
- 吞吐量
- 设备利用率
- 支持的用户数量
- 可靠性
- 系统容量

如果你熟悉 z/OS，你可能听说过或使用过 z/OS 工作负载管理器（WLM）组件。它提供根据用户定义的目标及其在 z/OS 映像中的资源需求，动态分配或重新分配服务器资源（如 CPU、I/O 和内存）给一组工作负载的能力。

有关 z/OS WLM 的更多信息，请参阅：

http://www-03.ibm.com/servers/eserver/zseries/zos/wlm/pdf/zWLM.pdf

### 7.1.1 z/VM 调度

要理解 z/VM 性能参数和因素，了解其底层系统调度非常重要。

在 z/OS 中，使用作业控制语言（JCL）来告诉系统执行哪些程序，然后描述程序的输入和输出。JCL 由一系列语句组成，每个语句为批处理作业提供特定的指令或信息。它为系统提供有关诸如要执行的程序、所需数据集的位置、为 CPU 处理时间计费的部门以及作业优先级等细节的信息。系统使用作业入口子系统（JES）将作业接收到操作系统中，为 MVS 处理调度它们，并控制其输出处理。JES2 和基本控制程序（BCP）提供了将作业送入 MVS 系统并从中输出所需的必要功能。

z/VM 采用类似的调度概念，其中控制程序（CP）和调度程序协同工作以执行调度任务，这些任务涉及图 7-1 中所示的多个组件。

![](img/b0a4b9056f819dccd4781a5105c92d45_336_0.png)

图 7-1 z/VM 调度组件

### 调度组件

调度组件及其协同工作方式在本节中进行描述。

**休眠列表**

如果任何虚拟机没有进行任何处理，CP 会将其移至休眠列表。虚拟机现在处于休眠状态。

**候选列表**

处于休眠状态的虚拟机可以响应事件而唤醒，例如按下控制台上的 Enter 键。虚拟机随后会被移至候选列表，并有资格消耗系统资源。

**调度程序**

调度程序在虚拟机获得系统资源之前检查候选虚拟机列表。具体来说，调度程序会查看虚拟机定义（VMDBK）信息，了解过去消耗的资源，如处理器、存储和分页。

**分派列表**

如果调度程序确定有足够的资源可满足你的需求，而不会使其他虚拟机处于危险之中，则虚拟机将被移至分派列表。

**时间片**

分派列表中的虚拟机在队列中等待其 CPU 时间份额，通常称为时间片。需要更多工作的虚拟机可以留在分派列表中以获得另一个时间片。

**用户类别**

当你首次登录 z/VM 时，控制程序会创建一个存储区域，其中包含与你相关操作相关的信息。此存储区域称为虚拟机定义块（VMDBK）。指向此块的指针会像图 7-1 所示在列表间移动。

### 调度和用户类别

z/VM 将用户分为四个不同的类别。用户类别会影响调度程序处理用户调度方案的方式。例如，类别 1 中的用户被认为正在运行短处理事务。此类用户会被分配时间片，并预计在该时间片内完成处理。但是，如果用户多次访问分派列表仍未完成处理，分派程序可以将用户升级到类别 2。类别 2 用户允许在分派列表中停留更长时间以完成中等长度的事务。

表 7-1 描述了 z/VM 中实现的用户类别。

**表 7-1 用户类别及其描述**

| 用户类别 | 描述 |
|------------|-------------|
| 类别 0 | 用户在候选列表中无延迟即被添加到分派列表，无论其当前事务的长度如何。 |
| 类别 1 | 刚刚开始事务的用户，因此被认为当前正在处理短事务。 |





| 用户类别 | 描述 |
|---|---|
| Class 2 | 用户在首次调度列表停留期间未完成其当前事务，因此被假定正在运行中等长度的事务。 |
| Class 3 | 用户在第二次调度停留期间未完成其当前事务，因此被假定正在运行长事务。 |

如果您拥有命令权限类 E，则可以发出以下 CP 命令来查看有关这些用户类别的信息：

```
INDICATE LOAD
```

在示例 7-1 中，带数字的 Q（Qn）表示调度列表中的用户，例如 Q2；带数字的 E（En）表示资格列表中的用户，例如 E2。n 是用户 0、1、2 或 3 的类别。

> 注意：En 字段中的任何值通常都表示性能问题（可能是存储或分页限制）。

## 示例 7-1 INDicate LOAD 命令

```
ind load
AVGPROC-000% 04
XSTORE-000000/SEC MIGRATE-0000/SEC
MDC READS-000001/SEC WRITES-000000/SEC HIT RATIO-099%
PAGING-1/SEC STEAL-000%
Q0-00000(00000)                      DORMANT-00012
Q1-00000(00000)      E1-00000(00000)
Q2-00000(00000) EXPAN-001 E2-00000(00000)
Q3-00000(00000) EXPAN-001 E3-00000(00000)

PROC 0000-000% CP      PROC 0001-000% CP
PROC 0002-000% CP      PROC 0003-000% CP

LIMITED-00000
```

## 7.1.2 CP 监控命令

本节介绍基本的 z/VM 命令。如果您熟悉 z/OS，您会发现对 z/OS 的等效或类似命令的引用，以帮助您扩展对 z/OS 的现有知识。如果您不熟悉 z/OS，本节可以帮助您了解 z/VM 可用的基本功能。

## CP 命令

z/VM 系统中的性能管理需要工具来收集和分析数据，并控制虚拟机的资源使用。这些工具由控制程序（CP）通过命令和监控功能提供。

本节描述的四个 CP 命令组是：

- CP INDICATE
- CP QUERY
- CP MONITOR
- CP SET

我们介绍这些命令及其最常用的参数。

## CP INDICATE

CP INDICATE 命令提供资源利用率的快照。然而，由于它只是快照，因此必须多次发出命令并检查结果的变化。

其中一些命令具有 EXPand ed 选项，可提供更多详细信息。INDICATE 命令可由系统资源操作员、系统程序员、系统分析员和普通用户（权限类 B、C、E 和 G 用户）使用，尽管对于某些命令，不同类别的用户会看到不同的结果。

> z/OS 类比：CP INDICATE 命令类似于 SDSF 命令 DISPLAY ACTIVE（或其缩写 DA）。

## CP INDICATE ACTIVE

使用此命令显示：

- 指定时间间隔内活动的用户总数
- 在指定时间间隔内处于调度、合格和休眠列表中的用户数

该命令的示例显示在第 325 页的示例 7-2 中。

## 示例 7-2 INDicate ACTive 命令

```
ind active
0009 USERS, 0005 DISP, 0000 ELIG, 0004 DORM
Ready; T=0.01/0.01 09:54:21
```

该命令接受以下操作数：

- nnnn 标识指定时间间隔的整数。有效时间段为 0 到 9 小时，或 540 分钟，或 32400 秒。默认值为 60 秒。
- SEC 标识 nnnn 以秒为单位指定。这是默认值。
- MIN 标识 nnnn 以分钟为单位指定。
- HRS 标识 nnnn 以小时为单位指定。

## CP INDICATE I/O

使用此命令识别当前处于 I/O 等待状态的虚拟机以及它们正在等待的实际 I/O 设备号。此命令可以帮助您发现因误将 minidisk 缓存或 CU 缓存关闭而导致的问题卷。

## CP INDICATE LOAD

使用此命令显示有关系统资源的信息。请参阅示例 7-3。对于普通用户，CP 会显示该信息的子集。请注意，此命令显示的处理器使用信息实际上是一段时间内的平滑平均值。系统负载的变化可能需要几分钟才能影响该数字。此命令是分析系统性能问题的良好起点。

在 z/OS 上，您使用命令 DISPLAY ACTIVE 来显示此类信息。

> 注意：要监控瞬时处理器负载，请使用 Performance Tool Kit。

## 示例 7-3 CP INDicate LOAD

```
cp ind load
AVGPOC-000% 04
XSTORE-000000/SEC MIGRATE-0000/SEC
MDC READS-000000/SEC WRITES-000000/SEC HIT RATIO-100%
PAGING-0/SEC STEAL-00%
Q0-00001(00000) DORMANT-00010
Q1-00001(00000) E1-00000(00000)
Q2-00000(00000) EXPAN-001 E2-00000(00000)
Q3-00000(00000) EXPAN-001 E3-00000(00000)
```




## CP INDICATE SPACES

使用此命令显示用户地址空间和分页使用情况的信息，如示例 7-5 所示。

### Example 7-5 INDicate SPaces command

```
ind spaces

Spaceid=MAINT:BASE  Owned size=123M  PRIVATE
Pages: Main=1400  Xstore=0  Dasd=0  Locked=---
Private paging:
  Xstore: Reads=0        Writes=0          Migrates=0
  Dasd:   Reads=1        Writes=1
Shared paging:
  Xstore: Reads=0        Writes=0          Migrates=0
  Dasd:   Reads=0        Writes=0
Ready; T=0.01/0.01 10:12:58
```

此命令对应于 z/OS DISPLAY ACTIVE 命令。

## CP QUERY

CP QUERY 命令可以显示有关系统和用户的信息。我们介绍了一些在调查性能问题时有用的查询命令。如果您有 z/OS 背景，您可以从与 z/VM 命令相关的 z/OS 提示中受益。

### CP QUERY ALLOC

使用此命令显示分配给系统所连接的 DASD 卷的柱面数或页数，以及正在使用和可用的数量。参见第 328 页的示例 7-6。

使用 QUERY ALLOC PAGE 获取有关分页空间的详细信息。

> 注意：不要将此命令与 z/OS 命令 ALLOCATE 混淆。尽管名称相似，但两者截然不同。
> z/OS 类比：CP QUERY ALLOC 命令对应于 z/OS 命令 D ASM。

### Example 7-6 Query ALLOC command

```
q alloc
DASD 1A20 LX6RES 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000020 INUSE=0000000001 AVAIL=0000000019, ACTIVE
DASD 1A21 LX6SPL 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000338 INUSE=0000000803 AVAIL=00000002535
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A22 LX6PAG 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000338 INUSE=0000000000 AVAIL=0000000338
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A23 LX6W01 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
DASD 1A24 LX6W02 3390 CKD-ECKD (UNITS IN CYLINDERS)
      TDISK TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      PAGE  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      SPOOL TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
      DRCT  TOTAL=0000000000 INUSE=0000000000 AVAIL=0000000000
......
IPL NUCLES ACTIVE ON VOLUME LX6RES
Ready; T=01.01 01:16:51
```

### CP QUERY CHPIDS

使用此命令显示机器全部 256 个通道路径及其物理状态。 如果 CHPIDs 离线或不可用，则可能发生 I/O 性能问题。参见第 329 页的示例 7-7。

### Example 7-7 Query CHPIDS command

```
q chpids
 0 1 2 3 4 5 6 7 8 9 A B C D E F
0x + + + + + + + + + + + + + + +
1x + + + + + + + + + + + + + + +
2x . . . . . . . . . . . . . . .
3x - + . . . . . . . + + + + . .
4x + + + + + + + + + + + + + +
5x + + + + + + + + + + + + +
6x + + + + + + + + + + + + + +
7x + + + + + + + + + + + . . . +
8x . . . . . . . . . . . . . . .
9x . . . . . . . . . . . . . . .
Ax . . . + . . . + . . . . . . .
Bx . . . . . . . . . . . . . . .
Cx . . . . . . . . . . . . . . .
Dx . . . . . . . . . . . . . . .
Ex . . . . . . . . . . . . . . .
Fx + + + + + + + + + + + + + + +
```

+ 可用
- 离线
. 未配置
Ready; T=0.01/0.01 10:18:45

> z/OS 类比：此命令的作用类似于 z/OS D M=CHP 命令。两者都显示机器的通道路径及其物理状态。

### CP QUERY CPLOAD

使用此命令显示有关上次 CP IPL 的信息。显示的信息包括上次使用的 CP 模块的位置、参数磁盘的位置以及 CP 的启动方式。

### Example 7-8 Query CPLOAD command

```
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=0.01/0.01 10:21:13
```

> z/OS 类比：此命令类似于 z/OS 上的 D IPLINFO 命令。





# CP QUERY CPOWNED

使用此命令显示 CP 所拥有的 DASD 卷列表。如果出现分页或 spooling 问题，可以通过此命令检查所有必需的卷是否可用。参见示例 7-9。

### 示例 7-9 QUERY CPOWNED 命令及示例输出

```
q cpowned
Slot Vol-ID Rdev Type Status
1 LX6RES 1A20 Own Online and attached
2 LX6SPL 1A21 Own Online and attached
3 LX6PAG 1A22 Own Online and attached
4 LX6W01 1A23 Own Online and attached
5 LX6W02 1A24 Own Online and attached
6 DK8226 8226 Own Online and attached
7 DK8227 8227 Own Online and attached
8 DK8228 8228 Own Online and attached
9 ------ ---- ---- Reserved
10 ------ ---- ---- Reserved
```

# CP QUERY FRAMES

使用此命令显示主机实存的状况。你可能需要在检查存储利用率时执行此操作，而用户正处于合格列表中。

### 示例 7-10 Query FRAMES 命令

```
cp q frames
All Frames:
  Configured=1048575 Real=1048575 Usable=1048575 Offline=0
  Pageable=1026485 NotInitialized=0 GlobalClearedAvail=128
  LocalClearedAvail=128 LocalUnclearedAvail=124

Frames < 2G:
  GlobalUnclearedAvail=454261 Pageable=521003 LogicalFreeStorage=56
  RealFreeStorage=4 LockedRS=348 LockedCmd=0
  MinidiskCache=9339 Nucleus/Prefix=2430 Trace=325 Other=122

Frames > 2G:
  GlobalUnclearedAvail=436453 Pageable=505482 LogicalFreeStorage=1194
  RealFreeStorage=19 LockedRS=57 LockedCmd=0
  MinidiskCache=13138 Other=17536
```

> z/OS 类比：此命令类似于 z/OS 的 D M=STOR 命令。

# CP QUERY MAXUSERS

使用此命令显示允许的最大登录用户数。如果用户无法登录，这可能是一个很好的执行命令。

> z/OS 类比：要在 z/OS 环境中显示最大用户数，请浏览 SYS1.PARMLIB 串联中的成员 IEASYSSxx。

# CP QUERY MDC

从 B 类用户使用此命令查询整个系统的 minidisk 缓存（MDC）设置、真实设备、活动 minidisk 或目录中定义的 minidisk。参见示例 7-11。此命令对于调查 I/O 问题很有用。

### 示例 7-11 Query MDC 命令

```
q mdc
Minidisk cache ON for system
Storage MDC min=0M max=128M, usage=3%, bias=1.00
Xstore MDC min=0M max=0M, usage=0%, bias=1.00
Ready; T=0.01/0.01 10:23:24
```

# CP QUERY NAMES

使用此命令显示：
- 所有已登录用户的列表
- 每个用户所连接的显示器的真实或逻辑设备号

参见示例 7-12。

### 示例 7-12 Query Names 命令

```
q n
LNXCER - DSC , LNXGUI - DSC , LNXXEN - DSC , COSTA -L0004
FTPSERVE - DSC , TCPIP - DSC , DTCVSM2 - DSC , DTCVSW1 - DSC
VMSERVR - DSC , VMSERVU - DSC , VMSERVS - DSC , OPERSYMP - DSC
DISKACNT - DSC , EREP - DSC , OPERATOR - DSC , MAINT -L0003
VSM - DSC , TCPIP
Ready; T=0.01/0.01 10:26:04
```

> z/OS 类比：在 z/OS 系统上，你可以通过运行 SDSF 显示活动命令来显示类似信息。

# CP QUERY QIOASSIST

使用此命令确定虚拟机的队列 I/O 辅助的当前状态，如示例 7-13 所示。此命令对于调查 I/O 或网络问题很有用。

### 示例 7-13 Query QIOASSIST 命令

```
q qioassist
ALL USERS SET - ON

USER   SETTING   STATUS
MAINT  ON        INACTIVE
Ready; T=0.01/0.01 10:28:40
```

# CP QUERY QUICKDSP

使用此命令显示用户的 QUICKDSP 属性。参见示例 7-14 获取示例输出。

### 示例 7-14 QUICKDSP 命令

```
cp query quickdsp maint
USER MAINT  : QUICKDSP = OFF
```

# CP QUERY RESERVED

使用此命令显示保留的实存帧数，并为用户保留存储页。参见示例 7-15。

### 示例 7-15 Query RESERVED 命令

```
q res
MAINT    RSV=00000010 ACT=00000010
LNXGUI   RSV=00000020 ACT=00000020
REQUESTED FRAME TOTAL=00000030; ACTUAL FRAME TOTAL=00000030
Ready; T=0.01/0.01 10:57:15
```

CP QUERY RESERVED 命令在存储受限系统的用户调优时很有用。

# CP QUERY SRM

使用此命令显示调度程序用于设置系统资源访问优先级的系统范围参数。SRM 是系统资源管理器。参见第 333 页的示例 7-16。

重要提示：请谨慎使用此命令并监控其使用情况，因为如果使用不当可能会出现合格列表。





> 请注意，如果要根据用户类别来控制用户对资源的使用，CP SET SRM 命令会很有用。

### 示例 7-16 查询 SRM 命令

```text
q srm
IABIAS : INTENSITY=90%; DURATION=2
LDUBUF : Q1=100% Q2=75% Q3=60%
STORBUF : Q1=300% Q2=250% Q3=200%
DSPBUF : Q1=32767 Q2=32767 Q3=32767
DISPATCHING MINOR TIMESLICE = 5 MS
MAXWSS : LIMIT=9999
MAXWSS : PAGES=999999
XSTORE : 0%
Ready; T=0.01/0.01 12:27:28
```

> z/OS 类比：在 z/OS 中，您可以设置 SRM 参数，但无法直接查看这些参数。

## CP QUERY STOR

使用此命令显示实际存储的大小。请参见示例 7-17。

### 示例 7-17 查询 STORAGE 命令

```text
q stor
STORAGE = 4G
Ready; T=0.01/0.01 12:35:16
```

> z/OS 类比：在 z/OS 中，您可以运行 D M=STOR 命令来显示实际存储的大小。

## CP QUERY SYSTEM

使用此命令显示当前用户对系统 DASD 卷的访问。

> z/OS 类比：在 z/OS 中，在发出以下 z/OS 命令之前，您需要知道设备编号：
> D U,, ALLOC, devnum.nnnn

## CP QUERY XSTOR

使用 QUERY XSTORAGE 或 QUERY XSTORE 可显示实际扩展存储的分配情况，或调查响应时间或分页问题。请参见第 334 页的示例 7-18。

```text
q xstor
XSTORE= 2048M online= 2048M
XSTORE= 2048M userid= SYSTEM usage= 0% retained= 0M pending= 0M
XSTORE MDC min=0M, max=0M, usage=0%
XSTORE= 2048M userid= (none) max. attach= 2048M
Ready; T=0.01/0.01 12:35:19
```

## CP MONITOR

CP MONITOR 命令收集系统性能数据，这些数据可供外部数据精简程序进行分析。可以生成与系统操作或主要系统资源争用相关的统计信息。这些资源包括处理器、存储、I/O 设备和分页子系统。您可以控制所收集数据的数量与性质。

通常，监控过程具有以下流程：

1. 用户发出特权 CP MONITOR 命令来控制监控。这包括要收集的数据的类型、数量及性质。
2. 监控器收集性能数据并将监控记录存储在保存段中。
3. CMS 应用程序连接到 CP MONITOR 系统服务，以与 CP 建立数据链路。
4. 应用程序从保存段中检索并处理监控记录。

## CP SET

CP SET 命令可以更改整个系统或单个用户的性能特性。

### CP SET MAXUSERS

使用此命令控制允许登录的用户数。如果 CPU 受限，您可以使用此命令限制用户数。

> z/OS 类比：在 z/OS 中，要设置用户数，您可以在 ParmLib 中的 IEASYSxx 成员中设置参数。

### CP SET MDC

由 B 类用户使用此命令执行以下任务：

- 更改整个系统、实设备或活动微型磁盘的微型磁盘高速缓存设置。
- 清除来自实设备或活动微型磁盘的数据缓存。
- 更改用户向高速缓存插入数据的能力。

如果您没有太多微型磁盘活动，并且希望释放更多存储，此命令会很有用。

### CP SET QIOASSIST

使用此命令控制虚拟机的队列 I/O 辅助（适用于 V=V 客户机¹的 QDIO 性能辅助）。此解释执行辅助适用于使用排队直接 I/O（QDIO）架构的设备、HiperSockets 设备和 FCP 设备。

### CP SET QUICKDSP

使用此命令分配或取消分配用户对系统资源的即时访问权。

> z/OS 类比：在 z/OS 中，您可以使用 WLM 执行类似的任务。

### CP SET RESERVED

使用此命令设置可供特定虚拟机使用的实际存储帧数。

当您尝试在存储受限的环境中调优特定客户机时，此命令会很有用。

### CP SET SHARE

使用此命令更改用户的系统资源访问优先级。这是一个复杂的命令，可能对系统和用户资源使用情况产生深远影响。请谨慎使用。

### CP SET SRM

使用此命令更改系统参数。这些参数定义了调度程序所看到的时间片大小以及不同用户类别对资源的访问。这是一个复杂的命令。在使用之前，请确保您清楚了解命令的效果。

> 注意：有关 SET SRM 的更多信息，请参阅 z/VM: CP Commands and Utilities Reference, SC24-6081，该文档可在以下位置找到：http://publib.boulder.ibm.com/infocenter/zvm/v5r3/topic/com.ibm.zvm.v53.hcpb7/hcse4b21.htm

¹ 客户机类型 V=V 是 z/VM 的一种度量方式，其中 Linux 被定义为虚拟等于虚拟机。





## CP SET THROTTLE

使用此命令可控制客户操作系统可以向特定真实设备发起的 I/O 操作数量。这可以防止某个客户机干扰或独占 I/O 资源。

## 7.2 调优基础

System z 处理器经过多年的发展，已经变得非常强大和可靠。本节介绍通用的调优概念，并探讨它们在 z/VM 上的实际应用。

### 7.2.1 系统调优方法

性能分析和调优是一个多步骤的过程。无论选择哪种工具，分析系统性能的最佳方法论都是从外部开始，逐步深入，直至处理细微的调优细节。首先收集有关系统硬件和进程整体健康状况的数据。每天高峰时段处理器有多繁忙？在这些高峰期间 I/O 响应时间发生了什么变化？它们是否保持相对一致，还是被拉长？系统是否每天都会受到内存限制，导致页面等待？当前的系统资源能否提供满足服务级别协议的用户响应时间？遵循良好的性能分析流程可以帮助你回答这些问题。

了解有哪些可用的调优工具，以及它们提供的信息类型非常重要。同样重要的是，要知道何时使用这些工具，以及应该关注什么。等到电话响起、用户开始抱怨时才运行工具、收集数据，那就为时已晚。如果不定期检查系统活动与资源使用情况，你又如何知道环境中什么是正常、什么是有问题的呢？定期对系统进行健康检查，还可以为你提供对容量规划有帮助的使用情况和性能信息。

### 7.2.2 调优能起到的作用

即使不同工作负载的总和小于可用资源总量，你仍可能发现自己无法以良好的性能运行工作负载。原因可能是系统缺少某种特定资源。在这种情况下，适当的调优可以带来改变。在调优系统和负载之前，你应该弄清楚在你的配置中，哪种资源是限制因素。

调优变更通常属于以下几类：

-   减少对受限资源的使用。

    在 z/VM 下运行 Linux 系统的一个好处是能够共享和过度调配硬件资源。Linux 认为自己拥有的内存量称为虚拟内存。分配给每个 Linux 客户机的虚拟内存总量可能是处理器上可用真实内存的许多倍。z/VM 可以高效地为 Linux 客户机管理内存。对于真正内存受限的系统，一个选择可能是通过减小 Linux 客户机的虚拟机大小来减少 z/VM 的整体内存使用量。

-   获取更多受限资源份额。

    用户可以轻松增加 Linux 客户机的虚拟内存大小，因为这是在 z/VM 下对客户机定义进行快速更改。然而，不必要地增加虚拟内存分配可能导致整个系统过度分页（也称为抖动）。如果系统确实内存受限，并且 Linux 虚拟内存大小已经经过合理分配，可以考虑为某个特定的 Linux 虚拟机保留一些内存页，以牺牲其他虚拟机为代价。这可以通过 z/VM 命令（CP SET RESERVED）来完成。

-   增加总的可用资源。

    解决内存问题最直接的方法就是购买更多硬件。内存的价格多年来一直在下降，因此这可能是一个不错的选择。不过，也可以通过停止 Linux 系统中不必要的实用程序服务来释放额外资源。请注意，调优并不会增加系统资源的总量。它只是让这些资源能够被更有效地用于关键工作负载。

### 7.2.3 调优无法解决的情况

要明白这一点：你无法运行超出机器所能承载之外更多的工作。如果你的 System z 机器有两个 CPU，而你想运行的工作负载由三个运行 WebSphere 的 Linux 虚拟机组成，每个虚拟机全天都让 CPU 以 100% 的运行率工作，那么这肯定无法承载。再多的 z/VM 调优也无法使之匹配，不过应用程序本身可能存在性能问题，使得工作负载并非全天候都使用 100% 的 CPU。

当一台 System z 机器有四个 CPU，而工作负载由三个 Linux 虚拟机组成，每个虚拟机全天都以 100% 的 CPU 使用率运行时，那就几乎没有什么可调优的了。在这种情况下，z/VM 拥有足够的资源来满足每个 Linux 虚拟机的需求（不过你或许需要考虑更改配置，以便利用全部四个 CPU，让事情运行得更快）。





## 7.3 z/VM的性能与监控工具

使用各种工具来监控和提升性能是非常普遍的做法。性能监控工具可提供更多有关z/VM系统状态的功能和报告。

在本节中，我们将介绍几种性能监控工具。更详细的信息，请参阅IBM红皮书《Linux on IBM System z: Performance Measurement and Tuning》，编号SG24-6926。

### 7.3.1 用于VM的IBM Performance Toolkit

IBM Performance Toolkit for VM是一款增强的实时性能监控器和全屏操作器，允许系统程序员监控系统性能并分析瓶颈。该工具包可帮助系统程序员更高效地利用系统资源、提高系统生产率并提升用户满意度。除了分析z/VM性能数据外，Performance Toolkit for VM还能处理从IBM资源测量设施（RMF）和Linux性能收集器rmfpm获取的Linux性能数据。Performance Toolkit for z/VM还提供其他几项功能，包括：

- 以全屏模式操作系统操作员控制台
- 管理多个z/VM系统（本地或远程）
- 对MONWRITE实用程序捕获的Performance Toolkit for VM监控数据进行后处理
- 通过Web浏览器或基于PC的3270仿真器图形查看性能监控数据
- TCP/IP性能报告

第339页上的图7-2展示了一个典型的Performance Toolkit窗口。

> 注意：有关Performance Toolkit的更多信息，请参阅《Linux on IBM eServer zSeries and S/390: Performance Toolkit for VM》，SG24-6059。

*图7-2 Performance Toolkit*

### 7.3.2 用于z/VM和Linux的Tivoli OMEGAMON

OMEGAMON®是一款用于VM（虚拟机）操作系统的实时软件性能监控器。它在会话监控系统（CMS）操作系统下运行。OMEGAMON会自动向您发出异常情况警告，并实时显示VM内部操作和资源的状态。

所有OMEGAMON特性和功能都围绕逻辑调优方法的概念而设计，以改善系统性能。逻辑调优方法包括以下步骤：

1. 在您的安装环境中定义VM性能的标准。

### 7.3.3 用于z/OS的IBM Tivoli Performance Modeler

现有的信息已不足以进行容量规划。可以使用IBM Tivoli Performance Modeler for z/OS V2.3对更改以下项目的影响进行建模：

- CPU的数量和速度
- 磁盘I/O响应时间
- 分页速率（辅助存储器和扩充存储器分页）
- 逻辑分区（LPAR）定义和参数变更

Tivoli Performance Modeler从z/OS映像获取输入，包括系统和应用程序性能数据，作为建模程序的基础。然后，用户可以更改处理器类型并调整工作负载配置，以创建新模型。然后，该建模器会生成一系列图形来描述所建模的工作负载。

### 7.3.4 用于IBM System z处理器上Linux客户机的IBM z/VM Planner

面向IBM System z处理器上的Linux客户机的z/VM Planner（简称z/VM Planner）是一款基于PC的生产力工具，在Microsoft Windows下运行。（IBM员工和经授权的IBM业务合作伙伴可以与其客户一起使用该工具。）它旨在为在VM下作为客户机运行各种Linux工作负载环境的IBM大型机处理器提供容量规划洞察。输入主要包括z/VM客户机定义以及每个预期Linux客户机的容量需求。总客户机容量需求基于客户机定义进行计算；同时，由于所有客户机可能不会同时达到峰值利用率，因此使用用户指定的互补峰值百分比来计算所评估的z/VM客户机的真实综合容量需求。该工具还模拟将新客户机合并到现有VM映像时的z/VM处理器需求。由此得出的客户机容量需求与VM的容量需求相结合，以支持全部客户机集合。

z/VM Planner会生成若干图形来描述所建模的系统。这些图形说明了支持所建模工作负载所需的处理器规模、工作负载中每个应用程序使用的处理器百分比，以及工作负载所需的最小和最大处理能力估算值。第342页上的图7-4表示一个所建模工作负载的最小和最大容量需求，该工作负载包含五个运行混合Web应用程序、数据库和文件服务器的Linux客户机。





![](img/b0a4b9056f819dccd4781a5105c92d45_357_0.png)

图 7-4 面向 Linux 客户机的 IBM z/VM Planner

## 7.3.5 Tivoli Workload Scheduling Suite

Tivoli Workload Scheduling Suite 是一套最先进的生产工作负载管理器，旨在帮助您应对当前和未来的数据处理挑战。它的范围涵盖您的整个企业信息系统，包括异构环境。

Tivoli Workload Scheduling Suite 通过集成系统管理功能，简化了异构环境中的系统管理。该套件的三个主要组件是：

- Tivoli Workload Scheduler for z/OS：z/OS 环境中的调度程序
- Tivoli Workload Scheduler：分布式环境中的调度程序
- Tivoli Job Scheduling Console：面向 Tivoli Workload Scheduler for z/OS 和 Tivoli Workload Scheduler 的通用用户界面

> 注：有关 Tivoli Workload Scheduling Suite 的更多信息，请参阅：
> http://publib.boulder.ibm.com/infocenter/tivihelp/v3r1/index.jsp?toc=/com.ibm.tivoli.itws.doc/toc.xml

### Linux 客户机的容量规划注意事项

Linux 内存模型对运行在 z/VM 下的 Linux 客户机有着深远的影响：

- z/VM 内存是一种共享资源。尽管激进缓存会降低磁盘 I/O 的可能性并有利于内存访问，但必须考虑缓存成本。Linux 客户机中的缓存页面会减少可供其他 z/VM 客户机使用的 z/VM 页面数。
- 更大的虚拟内存地址空间需要更多 Linux 内核内存来进行 Linux 内存管理。在为 Linux 客户机确定内存需求时，请选择对该客户机性能影响最小的最小内存占用。为了减少较小虚拟机中可能发生的偶发交换带来的性能损失，请使用快速交换设备。

尽管 512 MB 服务器并不需要那么多内存，但最终它看起来会将其全部用完。其内存成本是 128 MB 服务器的四倍。

> 注：更多信息可在 z/VM 网站上的 Performance Report 中找到：
> http://www.ibm.com/servers/eserver/zseries/zvm/perf/docs/
>
> 其他 z/VM 性能技巧可在 z/VM 网站上获取：
> http://www.ibm.com/servers/eserver/zseries/zvm/perf/tips/

## 7.3.6 为 z/VM Linux 客户机调优内存

存储调优在虚拟化环境中非常有用，尤其是在虚拟机监控程序能够超量分配资源的情况下。z/VM 是现存功能最强大的软件虚拟机监控程序操作系统。为了获得最佳的整体系统性能，建议在所有关键资源领域（如内存）进行微调。

为了最大程度地减少系统开销并降低其占用空间，缩小实际运行的机器规模通常很有帮助。可以通过多种方式减少服务器的内存占用。一种常见且直观的方法是终止不必要的进程。您还可以通过将虚拟机大小缩减到尽可能小的尺寸来调优 z/VM 内存使用量。最佳的最小尺寸可能需要多次尝试和实验。

> 注：有关 Linux 虚拟内存容量规划的更多信息，请参阅 Linux on IBM System z: Performance Measurement and Tuning, SG24-6926。

将较大的服务器划分为多个更小、更专用的服务器，可以证明是有效的。较小的服务器可以针对特定操作进行定制。但这是有代价的，因为每台服务器都需要一定内存来运行自己的操作系统。

使用带 DIAGNOSE 访问方法的 VDISK 作为交换设备，可以减少交换带来的性能损失。此建议仅适用于您在 System z 上有大量真实内存可用的情况。使用虚拟磁盘进行交换可以减少真实设备上由交换产生的 I/O，但同时会增加使用的存储总量。当 Linux 和 z/VM 产生高换页率时，这一技巧很有用。在这种情况下，可能会遇到双分页（z/VM 将已被 Linux 换出的客户机存储再次换出）的影响，而使用 VDISK 作为交换设备有助于减少这种影响。

使用 DIAGNOSE 驱动程序进行 DASD 和 MDC 记录缓存，以降低基础设施存储成本。使用记录级小型磁盘（minidisk）缓存可减少 MDC 所需的存储量。这需要 DIAGNOSE 驱动程序。

> 注：更多信息请参阅 IBM Linux on System z: Device Drivers, Features, and Commands, SC33-8289。

如果您在 z/VM 下运行 Linux，可以利用协作内存管理 1（CMM1）功能，在客户机之间实现更好的存储分配。

另一种减少内存使用的方法是使用共享内核或就地执行（execute-in-place）技术。这些新技术可用于减少管理 Linux 实例所需的总存储量。

## 7.3.7 就地执行技术

您可以使用不连续保存段（DCSS）来最小化虚拟 Linux 的内存需求并提高其性能。在虚拟化环境中，多个 Linux 映像可能在同一时刻需要相同的数据。这意味着相同的数据可能会多次加载到内存中。其中的很大一部分



Linux 所需的内存用于二进制应用程序文件和共享库文件。这种技术可以帮助您通过 z/VM 管理的 DCSS 为某些应用程序提供共享内存的方式。

数据共享的注意事项如下：

- 只有使用相同版本应用程序的 Linux 实例才能共享应用程序文件。
- 共享数据必须是只读的。
- 众多 Linux 实例频繁使用的应用程序和库是良好的候选对象。

DCSS 可以在 Linux 客户机存储之上或存储间隙中定义。通常，对于 64 位 Linux 客户机，使用存储间隙中的 DCSS 是首选位置。Linux 可以通过就地执行文件系统（xip2）访问 DCSS。

Linux 通过 mmap() 操作加载共享库和应用程序文件，该操作将文件内容映射到应用程序的地址空间。xip2 文件系统通过将 DCSS 的内容映射到应用程序的地址空间来执行此操作，而其他文件系统使用页缓存。此功能称为就地执行，因为文件内容不会物理复制到不同的内存位置。

使用就地执行技术，Linux 可以：

- 在不进行 I/O 操作的情况下访问文件和库（从而提高整体性能）。
- 直接在共享内存段中运行应用程序（从而节省内存）。

## 7.4 监控您的 Linux 客户机

Linux 客户机的性能监控涉及检查 system z 性能以及客户机操作系统的复杂任务。在前面的章节中，我们介绍了调度概念，以及 system z/VM 上的重要 z/VM 监控命令。本节介绍 Linux 客户机监控任务。

### 7.4.1 vmstat 命令

vmstat 命令显示进程、实际内存和虚拟内存使用情况、分页、块 I/O 和 CPU 的当前统计信息。参考示例 7-19，获取以下信息：

- procs 部分显示正在运行的进程数和被阻塞的进程数。
- memory 部分显示被换出的内存、空闲内存、包含 inode 和文件元数据的缓冲区大小，以及从磁盘读取文件的缓存内存。
- swap 部分列出换入和换出。
- io（I/O）部分报告读取和写入的块数（以千字节为单位）。
- system 中的 in 和 cs 分别表示每秒中断数和上下文切换数。
- cpu 部分的标题 us、sy、id 和 wa 分别表示用户、系统、空闲、I/O 等待和窃取的 CPU 时间百分比。vmstat 命令对于识别内存不足和 I/O 等待问题非常有用，除此之外，还包括虚拟 CPU 未由物理 CPU 支持的情况。

示例 7-19 列出了使用以下命令运行 vmstat 后获得的系统信息，该命令以 5 秒间隔进行十次更新：

```
vmstat 5 10
```

### 示例 7-19 vmstat 命令

| procs | memory | swap | io | system | cpu |
| r b w | swpd free buff cache | si so | bi bo | in cs | us sy id |
| 0 0 0 | 29232 116972 4524 244900 | 0 0 | 0 0 | 0 0 | 0 0 0 |
| 0 0 0 | 29232 116972 4524 244900 | 0 0 | 0 2560 | 6 0 | 1 99 |
| 0 0 0 | 29232 116972 4524 244900 | 0 0 | 0 2574 | 10 0 | 2 98 |

### 7.4.2 pstree 命令

pstree 命令显示应用程序的依赖关系和关系。它类似于 ps -eafx 命令。示例 7-20 显示 pstree 命令。

### 示例 7-20 pstree 命令

```
user@pserver1:> pstree
|---4*[nfsd]
| -nmbd
| -nsd---nsd---5*[nscd]
| -ntpd
| -portmap
| -rpc.mountd
| -rpc.statd
| -safe_mysqld---mysqld---mysqld---mysqld
| -2*[screen---bash]
| -scsi_eh_0
| -scsi_eh_1
| -smbd
| -sshd---2*[sshd---sshd---bash---vim]
|   |-sshd---sshd---bash---su---bash
|   |-sshd---sshd---bash---pstree
| -syslogd
```

### 7.4.3 top 命令

top 命令按进程打印系统数据。它显示当前运行的系统进程的概览。top 命令本身会消耗 CPU 资源。参见示例 7-21

### 示例 7-21 top 命令

```
[user@pserver1]$ top
1:40pm up 3:17, 11 users, load average: 0.00, 0.02, 0.03
134 processes: 127 sleeping, 6 running, 1 zombie, 0 stopped
CPU states: 1.9% user, 1.7% system, 0.0% nice, 96.2% idle
Mem: 1030464K av, 675028K used, 355436K free, OK shrd, 156256K buff
Swap: 1663160K av, OK used, 1663160K free 296068K cached

PID USER PRI NI SIZE RSS SHARE STAT %CPU %MEM TIME COMMAND
1746 wolf 15 0 54772 14M 11600 R 1.1 1.4 0:00 kdeinit
6147 wolf 15 0 1080 1080 840 R 0.9 0.1 0:00 topPrint
the output
of the 'top' command to a file:
top d 4 b i > out
d refresh rate in seconds
b batch
i only active processes
```


## 7.4.4 系统状态（sysstat）工具

该软件包包含多个用于收集系统数据的 Linux 工具。sysstat 软件包是广泛使用的 Linux 标准工具。它包含在您的发行版中（RHEL 5 或 SLES 10）或可以从以下网址下载：

http://pagesperso-orange.fr/sebastien.godard/

如果您安装源代码包，则需要在 Linux on System z 上编译它才能使用。sysstat 软件包包含以下组件：

| 组件 | 描述 |
| --- | --- |
| sadc 数据收集器 | 将数据存储在二进制文件中 |
| sar 报告工具 | 读取 sadc 创建的二进制文件并将其转换为可读输出 |
| mpstat | 用于处理器利用率 |
| iostat | 用于 I/O 利用率 |

sar 报告工具打印以下信息：

- 进程创建
- 上下文切换
- 所有/单个 CPU 利用率
- 网络利用率
- 磁盘统计

有关 sysstat 的更详细描述，请参阅：

http://www.ibm.com/developerworks/linux/linux390/perf/tuning_how_tools.html#sysstat

## 7.4.5 OProfile 工具

OProfile 是 Linux 系统的开源分析器。它提供对 Linux 系统上所有运行代码的分析，包括内核、共享库、应用程序二进制文件等，并在低开销下提供各种统计信息（根据工作负载不同，开销为 1–8%）。它在 GNU GPL 下发布。OProfile 由内核驱动程序、用于收集采样数据的守护进程以及用于生成报告的工具组成。

OProfile 通常支持 Linux 内核 2.2、2.4、2.6 及更高版本。

> 注意：如果您运行：
> - SUSE Linux，内核级别必须至少为 kernel-s390(x)-2.6.5-7.191，从 SLES9 SP2 开始。
> - Red Hat Linux，内核级别必须至少为 kernel-2.6.9-22.EL，即 RHEL4 U2。
> - Linux on System z，OProfile 仅支持内核 2.6 或更高版本。

OProfile 使用 CPU 的性能计数器来统计所有运行代码的事件，并将信息汇总为每个二进制映像的分析文件。然而，System z 硬件目前不支持 OProfile 使用的这种硬件性能计数器，因此改用计时器中断。

示例 7-22 说明了在 z/VM 上运行的 Linux 客户机上 OProfile 的典型用法。要使用 OProfile 工具，请使用 sysctl 命令打开计时器。完成所有分析后，关闭计时器。要设置环境，请使用 opcontrol 命令告诉 OProfile 运行内核对应的 vmlinux 文件的位置。然后，它就可以收集分析数据了。测试和工具关闭后，可以生成分析报告。

### 示例 7-22 Oprofile 工具

```text
sysctl -w kernel.hz_timer=1 1
gunzip /boot/vmlinux-2.6.5-7.201-s390x.gz 2
opcontrol --vmlinux=/boot/vmlinux-2.6.5-7.201-s390x 3
opcontrol --start 4
<DO THE TEST>
opcontrol --shutdown 5
opreport 6
```

请注意以下几点：

- 1 打开计时器的命令（timer=1）。分析完成后，关闭计时器（timer=0）。
- 2 如果不存在，请解压 vmlinux 文件。
- 3 指定运行内核的 vmlinux 文件。
- 4 启动 OProfile 守护进程，并开始分析。
- 5 停止 OProfile 守护进程，并停止分析。
- 6 提供产品符号或二进制映像摘要。

在图 7-5 中，CPU 信息未正确显示。System z 硬件尚未支持 OProfile 所需的 CPU 性能计数器，但输出仍包含有价值的信息。

```text
CPU: CPU with timer interrupt, speed 0 MHz (estimated)
Profiling through timer interrupt
vma      samples   %     app name          symbol name
80002840 5862     34.8970 mcf_base.z_Linux  price_out_impl
800012c8 5221     31.0811 mcf_base.z_Linux  refresh_potential
800003c4 4398     26.1817 mcf_base.z_Linux  primal_bea_mpp
80003b60 408      2.4289 mcf_base.z_Linux  sort_basket
0001a67c 345      2.0538 vmlinux            default_idle
800013d8 138      0.8215 mcf_base.z_Linux  flow_cost
800003bc 98       0.5834 mcf_base.z_Linux  update_tree
800020f8 88       0.5239 mcf_base.z_Linux  dual_feasible
800036a4 72       0.4286 mcf_base.z_Linux  primal_minus
8000323c 40       0.2381 mcf_base.z_Linux  write_circulations
80002720 24       0.1429 mcf_base.z_Linux  insert_new_arc
```

图 7-5 OProfile 输出

输出包括：

- `vma`：虚拟内存区域（vma）是虚拟地址空间的连续区域。这些区域在进程生命周期中创建，当程序尝试内存映射文件、链接到共享内存段或分配堆空间时。
- `samples`：该符号的采样数
- `%`：该符号的采样数相对于可执行文件总体采样的百分比
- `app name`：符号所属的应用程序名称
- `symbol name`：执行的符号名称

从 OProfile 的报告中，我们可以分析目标模块的性能并相应地调整优化。例如，在图 7-5 中，应用程序 mcf_base.z_Linux 的模块消耗了大部分 CPU 时间。为了提高该应用程序的性能，应比其他模块更关注这些模块。

> 注意：有关 OProfile 命令的详细信息和文档，请参阅：http://oprofile.sourceforge.net/docs/





## 系统事件与日志，备份与恢复

Linux on System z 是一个可靠的应用运行环境。然而，错误情况仍可能发生。例如，您可能会遇到：

- 软件错误：程序异常终止、无效输入数据
- 操作系统错误：出现在 Linux 或 z/VM 层面
- 硬件错误：LPAR、系统或磁盘子系统故障

本章概述了 z/VM 和 Linux 中可用于收集和分析系统事件、创建备份并在发生不可恢复故障时进行恢复的多种工具。

### 目标

完成本章后，您应该能够：

- 列出可用于系统事件和错误日志记录的工具
- 列出可用于错误分析的工具
- 讨论备份和恢复数据时需考虑的各种选项

### 8.1 z/VM 与 Linux 错误处理

本节概述了 z/VM 和 Linux 中错误的处理方式，并详细介绍了若干错误代码。

#### 8.1.1 z/VM 默认错误处理

z/VM 的每个功能、模块或设施负责处理用户在执行命令时出现的相关错误。这些错误可能由以下原因引起，但不仅限于：配置错误、命令调用方式不正确、输入数据无关等。当此类错误发生时，失败的功能会通过发出错误代码和消息来通知用户。

例如，当用户尝试登录一个未在 z/VM 中定义的虚拟机时，CP 会发出如示例 8-1 所示的消息。

**示例 8-1 登录到未定义虚拟机时的错误消息**

```
L LASMAYOU LASMAYOU
HCPLGA053E LASMAYOU not in CP directory

Enter one of the following commands:

LOGON userid        (Example: LOGON VMUSER1)
DIAL userid         (Example: DIAL VMUSER2)
MSG userid message  (Example: MSG VMUSER2 GOOD MORNING)
LOGOFF
```

有关 z/VM 错误代码和消息的更多详细信息，请参阅第 353 页的 8.1.2“z/VM 错误代码”。

系统相关错误，包括间歇性和永久性机器错误以及系统 I/O 错误，由 CP 自动处理，处理方式对用户完全透明。然而，当错误发生时，CP 会记录该错误并向您的 z/VM 主系统控制台发送一条消息。该消息通知您错误的发生，并指明：

- 系统操作是否可以继续
- 系统操作是否可以继续，但可用资源减少
- 是否正在开始系统重启和恢复

如果错误发生在某个已识别的虚拟机中，且 z/VM 整体系统的完整性得到保证，则会发生软异常终止。在软异常终止期间，CP 会收集软异常转储，系统操作将继续。

如果错误更为严重，CP 将以硬异常终止方式终止。在异常终止期间：

- CP 会保存 z/VM 假脱机文件和系统数据文件队列。
- CP 会进行硬异常转储，该转储可用于以后的调试。
- CP 会尝试重新启动自身以及操作员控制台虚拟机。

> 注意：除非已设置了相应的 IPL 命令，否则所有在异常终止前运行的客户操作系统都必须手动重新启动。

如果 CP 无法重新启动，它会通知您从错误中恢复所需采取的步骤。

#### 8.1.2 z/VM 错误代码

大多数 z/VM 错误代码遵循相同的格式。该代码具有消息标识符和消息文本。

消息标识符采用以下格式之一：

```
xxxmmm###s
xxxmmm####s
```

该格式指示以下信息：

- 前 3 个字符（xxx）是标识组件的前缀。主要组件标识符列表请参见第 354 页的表 8-1。
- 接下来 3 个字符（mmm）是模块代码，用于标识给定组件中发生故障的模块或功能。
- 随后的 3 或 4 位数字（### 或 ####）是消息编号本身。
- 最后一位（s）可以是以下严重性代码之一：
  - A 需要立即操作
  - D 决策
  - E 错误
  - I 仅信息
  - R 响应
  - S 严重错误
  - T 终止性错误
  - W 系统等待（仅限 CP），警告（所有其他）

第 354 页的表 8-1 列出了消息标识符中前三个字符的组件前缀标识符。





### 表 8-1 z/VM 主要组件标识符

| 前缀 | z/VM 组件 |
| --- | --- |
| DMS | CMS（会话监控系统） |
| DTC | 适用于 z/VM 的 TCP/IP |
| DVH | 适用于 z/VM 的目录维护工具 |
| FCX | 适用于 z/VM 的性能工具包 |
| HCP | CP（控制程序） |
| RAC | RACF 安全服务器 |
| TCP | 适用于 z/VM 的 TCP/IP |

此列表并不详尽。有关更多信息，请参阅 z/VM：CP 消息和代码，GC24-6119，位于：

http://publib.boulder.ibm.com/infocenter/zvm/v5r3/topic/com.ibm.zvm.v53.hcpw0/msgfrmt.htm#msgfrmt

要查找错误消息的解释（包括解决问题提示），请使用 HELP 命令。例如，要查找第 352 页上示例 8-1 中所示错误消息的解释，请键入以下命令：

```
help HCPLGA053E
```

结果显示在示例 8-2 中。

### 示例 8-2 HCPLGA053E 错误消息帮助

```
MSG HCPLGA053E                          All Help Information                 line 1 of 12
(c) Copyright IBM Corporation 1990, 2007

HCPLGA053E  (XAUTOLOG failed for userid:) <userid|value> not in CP directory

Explanation: The user ID supplied was not found in the z/VM directory. If the command was an asynchronous XAUTOLOG, the message indicates which user ID did not get logged on.

System Action: The command is not executed; system operation continues.

User Response: Reissue the command with a valid user ID.

* * * End of File * * *
```

## 8.2 用于错误收集和分析的 z/VM 工具

作为 z/VM 系统操作员，您的职责是确保 z/VM LPAR 可用的所有资源对用户可用，以便用户完成其工作。系统操作员的职责包括收集有关以下任务的信息：

- 记账
- 系统性能
- 系统事件
- 错误记录

z/VM 中提供了一组默认用户来完成这些任务：

- DISKACNT 收集记账和计费信息。
- OPERSYMP 记录症状记录。
- OPERATOR 记录系统事件。
- EREP 记录错误记录。

要检查 z/VM 系统上各种记录的状态，可以使用 query recording 命令（缩写为 q rec），如示例 8-3 所示。

### 示例 8-3 query rec 命令的输出

```
q rec
RECORDING   COUNT   LMT USERID   COMMUNICATION
EREP        ON      00000000 002 EREP      ACTIVE
ACCOUNT     ON      00000000 020 DISKACNT  ACTIVE
SYMPTOM     ON      00000000 002 OPERSYMP  ACTIVE
Ready; T=0.01/0.01 14:58:23
```

本章重点介绍收集系统事件和错误记录。

### 8.2.1 收集有关系统事件的信息

当 z/VM 进行 IPL 时，系统操作员机器（默认为 OPERATOR）会自动登录；如果在 IPL 时指定了 NOAUTOLOG 参数，则不会启动其他机器。在 OPERATOR 控制台上，显示所有与系统相关的消息和错误消息。操作员发出的所有命令以及这些命令的应答也会显示在 OPERATOR 控制台上。

系统操作员机器在 z/VM 配置文件 SYSTEM CONFIG 中定义，如示例 8-4 所示。

### 示例 8-4 系统用户标识配置

```
/*****************************************************************/
/* System Userids */
/*****************************************************************/

System_Userids ,
Operator OPERATOR ,
Account DISKACNT ,
Dump OPERATNS ,
Erep EREP
```

此控制台日志可以保存到 spool 文件中，以便日后分析。如果发生系统异常终止，CP 也会自动将控制台日志保存到 spool 文件中。

### 控制台日志记录状态

要确定控制台活动是否记录到文件中，请发出 QUERY VIRTUAL CONSOLE 命令（缩写为 q v con），如示例 8-5 所示。输出的第一行显示 STOP，表示控制台日志记录未启用。

### 示例 8-5 控制台日志记录状态

```
q v console
00: CONS 0009 ON LDEV L0003 TERM STOP HOST TCPIP FROM
9.57.138.243
00: 0009 CL T NO CONT NOHOLD COPY 001 READY FORM STANDARD
00: 0009 TO LNXGUI PRT DIST LNXGUI FLASCH 000 DEST OFF
00: 0009 FLASH CHAR MDFY 0 FCB LPP OFF
00: 0009 3215 NOEOF 0008 NOKEP NOMS G NOMAME
00: 0009 SUBCHANNEL = 0008

Ready; T=0.01/0.01 15:28:01
```

### 启用控制台日志记录

要在虚拟机（如 LNXGUI）中启用控制台日志记录，请使用命令 CP SPOOL CONSOLE START（缩写为 cp sp con start），如示例 8-6 所示。再次使用 query console 检查状态。输出的第一行应显示 START，表示控制台日志记录已启动。





## 示例 8-6 启用控制台日志记录

```
q v console
00: CONS 0009 ON LDEV L0003 TERM STOP HOST TCPIP FROM 9.57.138.243
00: 0009 CL T NOCONT NOHOLD COPY 001 READY FORM STANDARD
00: 0009 TO LNGXGUI PRT DIST LNGXGUI FLASHC 000 DEST OFF
00: 0009 FLASH CHAR MDFY 0 FCB LPP OFF
00: 0009 3215 NOEOF CLOSED NOKEEP NOMSG NONAME
00: 0009 SUBCHANNEL = 0008
Ready; T=0.01/0.01 15:28:01
cp spool console start
Ready; T=0.01/0.01 15:31:13
q v console
00: CONS 0009 ON LDEV L0003 TERM START HOST TCPIP FROM 9.57.138.243
00: 0009 CL T NOCONT NOHOLD COPY 001 READY FORM STANDARD
00: 0009 TO LNGXGUI PRT DIST LNGXGUI FLASHC 000 DEST OFF
00: 0009 FLASH CHAR MDFY 0 FCB LPP OFF
00: 0009 3215 NOEOF OPEN 00039 NOKEEP NOMSG NONAME
00: 0009 SUBCHANNEL = 0008
Ready; T=0.01/0.01 15:31:19
```

在示例 8-7 中，我们通过在 LNGXGUI 机器的 PROFILE EXEC 中添加语句 CP SPOOL CONSOLE START 来确保虚拟机下次 IPL 时控制台日志记录被激活。

## 示例 8-7 更新 PROFILE EXEC

```
PROFILE EXEC A1 V 130 Trunc=130 Size=3 Line=0 Col=1 Alt=2

==== * * * Top of File * * *
|...+....1....+....2....+....3....+....4....+....5....+....6....+....7...
==== /* */
==== 'CP SET PF12 RETR'
==== 'CP SPOOL CONSOLE START'
==== * * * End of File * * *

===>
X E D I T 1 File
```

## 将控制台日志保存到文件

要将控制台日志保存到文件，必须停止控制台日志记录。然后会在机器的虚拟打印机中创建一个文件。该文件可以直接打印或发送到虚拟阅读器以供进一步处理。示例 8-8 在第 359 页展示了为此目的使用的命令。

## 示例 8-8 将控制台日志保存到文件

```
cp sp console close
00: PRT FILE 0041 SENT FROM LNXGUI    CON WAS 0041 RECS 0131 CPY 001 T NOHOLD
NO
KEEP
Ready; T=0.01/0.01 16:47:06
change prt all to * rdr
00: RDR FILE 0041 SENT FROM LNXGUI    PRT WAS 0041 RECS 0131 CPY 001 T NOHOLD
NO
KEEP
00: 0000001 FILE CHANGED
Ready; T=0.01/0.01 16:47:16
```

命令 CP SPOOL CONSOLE CLOSE（在示例中简写为 cp sp console close，或 cp sp con close）会关闭当前日志文件，并打开另一个日志文件。当前日志文件会被发送到虚拟机打印机。该文件 spoolid 为 0041。

命令 change printer all to * reader（在示例中简写为 change prt all to * rdr）会将机器虚拟打印机中的所有文件移动到其虚拟阅读器。星号 (*) 表示我自己，即发出命令的虚拟机。

> 注意：您可以使用单个命令关闭 spool 并将其发送到您的阅读器：
> 
> cp sp console close *
> 
> 要仅将打印机中的某个特定文件发送到虚拟机的阅读器，请指定要传输的文件的 spoolid：
> 
> ch prt 0041 to * rdr

当文件位于阅读器中时，您可以使用 RL 命令列出它们，并使用 PEEK spoolid 命令浏览它们（该命令映射到阅读器列表窗口中的 F11 键），如示例 8-9 所示。它们也可以保存到磁盘并归档。

## 示例 8-9 显示控制台日志文件

```
0041 PEEK AO V 133 Trunc=133 Size=131 Line=52 Col=1 Alt=0
File (none) (none) from LNXGUI at VMLINUX6 Format is CONSOLE.
z/VM V5.3.0  2008-05-06 13:40

Ready; T=0.01/0.01 16:45:57
q da all
00: HCPQVC022E A virtual device number was not supplied or it was invalid.
```

```
Ready(00022); T=0.01/0.01 16:46:04
q da
00: DASD 0101 9336 (VDSK) R/W      200000 BLK ON DASD  VDSK SUBCHANNEL = 0001
00: DASD 0190 3390 LX6RES R/O      107 CYL ON DASD   1A20 SUBCHANNEL = 0009
00: DASD 0191 3390 LX6W02 R/W      10 CYL ON DASD    1A24 SUBCHANNEL = 0000
00: DASD 019D 3390 LX6W01 R/O     146 CYL ON DASD   1A23 SUBCHANNEL = 000A
00: DASD 019E 3390 LX6W01 R/O     250 CYL ON DASD   1A23 SUBCHANNEL = 000B
00: DASD 0401 3390 LX6W01 R/O     146 CYL ON DASD   1A23 SUBCHANNEL = 000E
00: DASD 0402 3390 LX6W01 R/O     146 CYL ON DASD   1A23 SUBCHANNEL = 000D
00: DASD 0405 3390 LX6W01 R/O     156 CYL ON DASD   1A23 SUBCHANNEL = 000F
00: DASD 0592 3390 LX6W01 R/O      70 CYL ON DASD   1A23 SUBCHANNEL = 000C
Ready; T=0.01/0.01 16:46:06
link * 100 100 MR
Ready; T=0.01/0.01 16:46:15
link * 150 150 MR
Ready; T=0.01/0.01 16:46:20
cp console close
Unknown CP command
Ready(-0001); T=0.01/0.01 16:46:51
q v
00: STORAGE = 512M
1= Help     2= Add line  3= Quit     4= Tab      5= Clocate    6= ?/Change
7= Backward 8= Forward 9= Receive 10= Rytleft 11= Spltjoin 12= Cursor
====>
                                   X E D I T 1 File
```

此控制台日志文件显示了在虚拟机控制台中已发出的所有命令以及对这些命令的响应。如果 CP 遇到错误，它也会记录到控制台日志中。

z/OS 类比：这类似于 z/OS SYSLOG。

您还可以使用虚拟机的控制台通过使用 SET OBSERVER 命令或在用户目录 CONSOLE 语句中添加参数来显示多个用户的控制台。示例 8-10 显示了 CONSOLE 目录语句。

## 示例 8-10 LNXGUI 虚拟机目录 CONSOLE 语句

```
USER  DIRECT  C1 F 80  Trunc=72 Size=2041 Line=60 Col=1 Alt=1
00060  SPOOL 000E 1403 A
00061  CONSOLE 009 3215 T LNXMAINT OBSERVER
00062  LINK MAINT 0190 0190 RR
```



11 可恢复 0 0
12 不可恢复 0 0
13
14 通道检查
15
16 通道 0 0 0
17 通道 1 0 0
18 通道 2 0 0
19 通道 3 0 0
20 通道 4 0 0
21 通道 5 0 0
22 通道 6 0 0
23 通道 7 0 0
24 通道 8 0 0
25 通道 9 0 0
26 通道 A 0 0
27 通道 B 0 0
28 通道 C 0 0
29 通道 D 0 0
30 通道 E 0 0
31 通道 F 0 0
32
33 程序错误
34
35 ABEND 344 344
36 程序中断 21 21
37
38 当日结束 0 0
39
40 CPU 型号 序列号
41 0 2084XA 0BE34E
42
43 系统汇总报告 日期 141 08
44 (第 1 部分续) 期间从 065 08
45 子通道/通道 至 115 08
46
47 总计 CPU-0
48
49 子通道注销
50
51 通道报告字
52
53 硬件 0 0
54 软件 0 0
55
56 总记录数 419 419
57
58 CPU 型号 序列号
59 0 2084XA 0BE34E
60
61 系统汇总报告 日期 141 08
62 (第 2 部分) 期间从 065 08
63 I/O 子系统 至 115 08
64
65 ---- 总计 ---- CPU-0
66 永久 临时 路径 永久 临时
67 DASD **************************
68
69 2107-SSID 8A00 0 3 0 - -
70 2107-SSID 8C00 0 3 0 - -
71 2107-SSID 8000 0 5 0 - -
72 2107-SSID 8400 0 7 0 - -
73 2107-SSID 8600 0 14 0 - -
74 2107-SSID 8700 0 2 0 - -
75 2107-SSID 8800 0 4 0 - -
76
77 磁带 **************************
78
79 3590 FA50 0 1 0 0 1
80 3590 FA51 0 1 0 0 1
81 3590 FB00 0 1 0 0 1
82 3590 FB01 0 1 0 0 1
83 3590 FB02 0 1 0 0 1
84 3590 FB03 0 1 0 0 1
85 3590 FB10 0 1 0 0 1
86 3590 FB11 0 1 0 0 1
87 3590 FB12 0 1 0 0 1
88 3590 FB13 0 1 0 0 1
89 3590 FB30 0 2 0 0 2
90 3590 FB40 1 6 0 1 6
91 3590 FB41 0 7 0 0 7
92
93 总计 1 63 0 1 25
94 CPU 型号 序列号
95 0 2084XA 0BE34E
96 * * * 文件结束 * * *

## 8.2.3 转储和跟踪

本节概述 z/VM 中的转储和跟踪功能。

### 转储

转储是虚拟机或分区存储器的映像。如果遇到问题，很可能在该映像中的某处找到问题。转储可用于确定故障开始的时间点。

z/VM 的多个组件可以生成转储：

- CP 本身
- 运行 CMS、或另一个 z/VM 组件、或客户操作系统的虚拟机
- 通信控制器

z/VM 中提供多种类型的转储，具体取决于生成转储的组件或分析所需的信息：

- CP 转储。这是 CP 直接拥有的存储器的转储。它由 CP 在硬性异常终止期间生成，导致系统终止，并可能重新启动。

注意：查询转储命令（缩写为 q dump）显示将用于存储 CP 转储文件的设备。默认情况下，CP 转储在 SYSTEM CONFIG 中定义的系统用户 ID（默认为 OPERATNS）下的虚拟读取器中创建。参见第 357 页的示例 8-4，了解 SYSTEM CONFIG 转储语句的示例。

- 快照转储。这是 CP 直接拥有的存储器的转储，与硬性异常终止转储非常相似，但不会导致系统终止。
- CP 软异常终止转储。这是 CP 直接拥有的一小部分存储器的转储。当 CP 遇到错误且系统完整性未受损害时，或当 CP 可以将错误隔离到某个虚拟机时，会创建此转储。它不会导致系统终止。
- 独立转储。有时问题可能非常严重，以至于系统甚至无法自行生成 CP 转储。因此，每个 z/VM 系统都配备了一个特殊程序，无论问题有多严重，该程序都会生成真实存储器的转储。它被称为独立转储，因为生成它的程序独立于系统编程的其余部分。由于它独立于系统编程，因此其中的任何问题都不会阻止转储的创建。
- 仅针对在 z/VM 系统中运行的任何单个虚拟机（VMDUMP）的转储。例如，您可以请求对包含 CMS、RSCS 或驻留在虚拟机中的任何客户操作系统的虚拟机进行转储。
- 通信控制器存储器的转储。

如果您的虚拟机运行的是 Linux 或 z/OS 等客户操作系统，建议使用该操作系统可用的工具，而不是 z/VM 转储工具。有关 Linux 转储工具的讨论，请参阅第 372 页的 8.3.2“错误分析工具”。




有关 VM 转储工具的更多详细信息，请参阅位于以下位置的 z/VM V5r3.0 诊断指南，GC24-6092：http://publib.boulder.ibm.com/infocenter/zvm/v5r3/index.jsp?topic=/com.ibm.zvm.v53.hcpcl1/getdump.htm

> z/OS 类比：在 z/OS 中，使用专用的转储地址空间将转储捕获到 DASD。用户发起的转储也保存在转储地址空间中。

## Traces

虚拟机跟踪功能允许您跟踪或追踪在使用虚拟机时发生的几乎任何执行情况。例如，您可以跟踪指令、I/O 中断、分支以及存储的变化。

跟踪虚拟机内部程序的执行情况可以帮助系统操作员和支持团队识别程序中执行失败的步骤。示例 8-13 显示了在 Linux 客户机中运行 cat /root/viminfo 命令时运行的 TRACE I/O 命令的输出。

### Example 8-13 Tracing I/O in a Linux guest running cat /root/viminfo command

```
00: EXTENT 80C00000 00000000 00080000 00080000
00: EXTENT 1F209FC0 47400010 1F209FF0 0008 47400010 ........
00: LOCATE RECORD 01800001 00080000 00070000 01061000
00: CCW 1F209FC8 85001000 1DE19000 0010 85041000 ........
00: IDAL 0000000000DAAE0000
00: -> 00000000208C790E* SIGA B2740000 0000000000000000 CC 0
00: SCH 0006 DEV 0602
00: FC 00000001 MASK 80000000 00010006
00: -> 0000000000332258* SSCH MASK3300 0000000001F4844 CC 0
00: SCH 0001 DEV 0100
00: CPA 1F209FB8 PRM 010F4800 KEY 0 FPI C2 LPM F0
00: VDEV 0100 CCW 63600020 1F209FD0 000 63600020 ........
00: EXTENT 80C00000 00000000 00080000 00080000
00: CCW 1F209FC0 47400010 1F209FF0 0008 47400010 ........
00: LOCATE RECORD 01800001 00080000 00070000 01061000
00: CCW 1F209FC8 85001000 1DE19000 0010 85041000 ........
00: IDAL 0000000005CCB000
00: -> 00000000208CB852* SIGA B2740000 0000000000000000 CC 0
00: SCH 0006 DEV 0602
00: FC 00000000 MASK 20000000 20000000
00: -> 00000000208CB852* SIGA B2740000 0000000000000000 CC 0
00:          SCH 0006  DEV 0602
00:          FC 00000000  MASK  20000000  20000000
00: -> 0000000208CBB52' SIGA B2740000  0000000000000000  CC 0
00:          SCH 0006  DEV 0602
00:          FC 00000000  MASK  20000000  20000000
```

有关 z/VM trace 命令的更多信息，请参阅位于以下位置的 z/VM V5R3.0 系统操作，SC24-6121：
http://publib.boulder.ibm.com/infocenter/zvm/v5r3/topic/com.ibm.zvm.v53.hcpb2/uc9a.htm#uc9a

## 8.3 Linux activity logging and error analysis

活动日志记录内置于每个 Linux 发行版中。无论发行版如何，所有与内核相关的消息和与守护进程相关的消息都会记录到一个公共目录中。这些消息可以是：

- 信息消息：例如，有人通过 SSH 从某个 IP 地址登录到机器。
- 警告消息：例如，守护进程的一个配置选项无法应用，但并未阻止守护进程启动。
- 错误消息：例如，有人拔掉了网络接口的网线。

浏览这些日志文件的内容是进行错误识别的第一步。

### 8.3.1 Linux activity logging

负责记录内核和用户活动的两个 Linux 守护进程：klogd 和 syslog，或 syslog-ng：

- klogd 用于与内核相关的消息
  klogd 是内核记录器。它拦截并转换内核本身发出的消息，并将其格式化后传递给 syslog 以进行归档。
- syslog 及其变体用于用户空间中的所有内容
  syslog 是用户空间记录器。它从系统中运行的各种守护进程收集信息，并将消息保存到文件中以供进一步参考。

## Log files of interest

无论发行版如何，日志文件都保存在一个名为 /var/log 的公共目录中。但是，日志文件的名称可能会因发行版而异。

> 注意：/var/log 是发行版软件包提供的守护进程日志消息的标准位置。第三方软件大多数情况下会将其日志文件保存在不同的位置。

当您查找错误时，/var/log 目录中最相关的文件在 SUSE Linux Enterprise Server 10 和 Red Hat Enterprise Linux 5 上，如下一节所述。

## Files on SUSE Linux Enterprise Server 10

文件如下：

- 消息日志文件包含所有系统消息

示例 8-14 显示了 qeth 驱动程序的一份报告，说明在 5 月 21 日 16:41:21 发生了网络故障。

### Example 8-14 An extract of /var/log/messages log file on SLES10

```
May 21 15:17:15 lnxquill kernel: audit(1211397428.415:2): AppArmor (version 2.0-19.43.6320) initialized
May 21 15:17:15 lnxquill syslog-ng[1206]: Changing permissions on special file /dev/xconsole
May 21 15:17:15 lnxquill syslog-ng[1206]: Changing permissions on special file /dev/tty10
May 21 15:17:15 lnxquill kernel:
May 21 15:17:15 lnxquill kernel: Unable to find swap-space signature
May 21 15:17:23 lnxquill kernel: eth0: no IPv6 routers present
May 21 15:18:06 lnxquill sshd[1325]: Accepted keyboard-interactive/pam for root from 9.57.138.243 port 2805 ssh2
May 21 16:17:11 lnxquill syslog-ng[1206]: STATS: dropped 0
May 21 16:41:28 lnxquill kernel: qeth: Link failure on eth0 (CHPID 0x20) - there is a network problem or someone pulled the cable or disabled the port.
May 21 16:41:28 lnxquill mingetty[1319]: ttyS0: invalid character for login name found
May 21 16:42:05 lnxquill kernel: qeth: Link reestablished on eth0 (CHPID 0x20). Scheduling IP address reset.
May 21 16:42:05 lnxquill kernel: qeth: Recovery of device 0.0.0600 started
...
May 21 16:42:05 lnxquill kernel: qeth: Device 0.0.0600/0.0.0601/0.0.0602 is a Guest LAN QDIO card (level: V530)
May 21 16:42:05 lnxquill kernel: with link type GuestLAN QDIO (portname: )
```



-   `lastlog` 文件显示最近登录用户的列表。使用 `LASTLOG` 命令查询此文件。
-   `faillog` 文件显示登录失败的用户。使用 `FAILLOG` 命令查询此文件。
-   `warn` 文件包含警告信息，例如来自 SSH 的访问被拒绝等。

## 红帽企业 Linux 5 上的文件

-   `messages` 文件包含所有系统消息。
-   `lastlog` 文件显示最近登录用户的列表。
-   `faillog` 文件显示登录失败的用户。
-   `secure` 文件显示所有与安全相关的消息。

## 浏览日志文件

有许多命令可用于浏览日志文件。

浏览日志文件最标准的方式是使用文本编辑器打开它。另一种方便的显示日志文件的方式是使用 `tail` 命令，它会输出文件的最后几行。参见示例 8-15。每次文件中写入新内容时，输出都会刷新。该命令允许实时日志监控，因此在尝试重现错误时，它是查看文件写入内容的便捷方式。

### 示例 8-15 `tail -f /var/log/messages` 的输出

```
lnxquill:~ # tail -f /var/log/messages
May 29 13:54:30 lnxquill kernel: AppArmor: AppArmor (version 2.0-19.43r6320) initialized
May 29 13:54:30 lnxquill kernel: audit(1212083662.366:2): AppArmor (version 2.0-19.43r6320) initialized
May 29 13:54:30 lnxquill syslog-ng[1209]: Changing permissions on special file /dev/xconsole
May 29 13:54:30 lnxquill syslog-ng[1209]: Changing permissions on special file /dev/tty10
May 29 13:54:30 lnxquill kernel:
May 29 13:54:30 lnxquill kernel: Unable to find swap-space signature
May 29 13:54:35 lnxquill kernel: eth0: no IPv6 routers present
May 29 13:54:46 lnxquill sshd[1256]: error: PAM: Authentication failure for root from 9.57.138.243
May 29 13:54:49 lnxquill sshd[1256]: Accepted keyboard-interactive/pam
for root from 9.57.138.243 port 2063 ssh2
May 29 14:02:55 lnxquill sshd[1332]: Accepted keyboard-interactive/pam
for root from 9.57.138.243 port 2102 ssh2
```

**head** 命令的功能相同，但只显示日志文件的前几行。**dmesg** 命令显示内核日志守护进程记录的消息。

## 日志文件归档

为避免存储大量数据，日志文件会定期轮转。轮转过程由 **logrotate** 命令管理，该命令由每天启动的 **cronjob** 控制。有关 cronjob 的更多信息，请参阅第 275 页上的第 5.4.1 节“作业调度”。

根据 **logrotate** 的配置选项，日志文件会保留几天或几周，并选择是否压缩，直到达到一定的时间或大小。

如示例 8-16 所示，较旧的 messages 日志文件已轮转了四次、压缩并保存在磁盘上。这些是 SUSE Linux 9 的默认设置。

*示例 8-16 /var/log/ 目录的内容*

```text
mastervm12:/var/log # ls -al
total 3424
drwxr-xr-x   5 root root  4096 May 16 04:15 .
drwxr-xr-x  13 root root  4096 Jan 16  2007 ..
drwxr-xr-x   2 root root  4096 Feb 12 15:10 YaST2
drwxr-x---   2 root root  4096 Feb 12 10:11 apache2
-rw-r-----   1 root root  4096 Jan 16  2007 boot.log
-rw-r--r--   1 root root 13651 Apr 19 23:13 boot.msg
-rw-r--r--   1 root root 15623 Apr 19 23:12 boot.omsg
-rw-r--r--   1 root root  586 Jan 16  2007 convert_for_getconfig.log
-rw-r--r--   1 root root 32096 Apr 10 00:15 faillog
-rw-r--r--   1 root tty  29688 May 27 21:27 lastlog
-rw-r--r--   1 root root   474 Dec  6 15:37 localmessages
-rw-r-----   1 root root  5334 Apr 30 17:20 mail
-rw-r-----   1 root root  1796 Apr 30 17:20 mail.err
-rw-r-----   1 root root  5334 Apr 30 17:20 mail.info
-rw-r-----   1 root root  3974 Apr 30 17:20 mail.warn
-rw-r-----   1 root root 214109 May 27 21:27 messages
-rw-r-----   1 root root 333920 Dec 11 04:15 messages-20071211.gz
-rw-r-----   1 root root 340177 Feb  2 04:15 messages-20080202.gz
-rw-r-----   1 root root 337732 Feb 21 04:15 messages-20080221.gz
-rw-r-----   1 root root 329943 May 16 04:15 messages-20080516.gz
[...]
```





在 SUSE Linux 10 中，每当当前 /var/log/messages 文件达到 4 MB 大小时，就会创建一个新的日志文件；日志文件在被删除前会轮转 99 次。logrotate 和 syslog 配置文件可在 /etc/logrotate.* 和 /etc/syslog.conf 位置找到。

有关 logrotate 和 syslog 配置的更多信息，请参阅相应的手册页。

根据您的安全和审计策略，可能需要对 syslog 和 logrotate 进程进行微调，以保持正确的日志文件数量。

## 集中式远程日志

syslog 的最后一个值得注意的功能是其完整的远程日志记录能力；syslogd 能够向运行 syslogd 的远程主机发送消息并从远程主机接收消息。远程主机不会再次转发消息，而是将消息本地记录。

使用此功能，您可以在一台主机上控制所有 syslog 消息，如果所有其他机器都远程记录到该主机。这降低了管理需求。

请参阅 syslogd 手册页以获取更多详细信息。

## 8.3.2 错误分析工具

本节讨论用作错误分析工具的转储和跟踪。

### 转储，作为错误分析工具

有时在日志文件中找不到足够的相关信息。为了分析在 z/VM 分区中运行的 Linux 客户机之一出现异常行为的原因，请在其中一台虚拟机上运行转储工具以进行进一步分析。根据环境，可以使用多种工具：

- DASD 转储工具在 3390 或 3380 磁盘上生成转储。
- SCSI 转储工具在 FCP/SCSI 设备上生成转储。
- 磁带转储工具在磁带上生成转储。
- VMDUMP 创建来宾虚拟内存的转储。

请参阅第 373 页的表 8-2 以获取可用工具列表。

| Tool | Stand-alone tools | | | VMDUMP |
| --- | --- | --- | --- | --- |
| | DASD | SCSI | Tape | |
| Environment | VM and LPAR | LPAR only | VM and LPAR | VM only |
| Speed | Fast | Fast | Slow | Medium |
| Medium | ECKD or FBA DASD | Linux file system on a SCSI disk | tape cartridges | VM reader |
| Compression possible | no | yes | yes | no |
| Disruptive | yes | yes | yes | no |

描述如何使用所有这些工具超出了本书的范围。有关使用转储工具的详细流程，请参阅 Linux on System z: Using the Dump Tools, SC33-8412，您可以从 developerWorks 网站下载：

http://www.ibm.com/developerworks/linux/linux390/development_documentation.html#3

### 跟踪，作为错误分析工具

识别程序执行中失败步骤的另一种有用方法是跟踪程序。Linux 提供了许多用于跟踪程序执行的工具。其中一种工具称为 strace。

在最简单的情况下，strace 运行指定的命令直到其退出。它拦截并记录进程调用的系统调用以及进程收到的信号。每个系统调用的名称、其参数和返回值会打印到标准错误或使用 -o 选项指定的文件中。strace 工具可用作诊断、教学和调试工具。系统管理员、诊断人员和故障排除人员发现它对于解决源代码不易获得的程序问题非常宝贵，因为他们无需重新编译即可跟踪它们。而程序员发现，由于系统调用和信号是在用户/内核接口发生的事件，因此对该边界的仔细检查对于错误隔离、合理性检查以及尝试捕获竞争条件非常有用。

第 374 页的示例 8-17 显示了对 ls 命令进行 strace 时 strace 输出的开头。所有系统调用都详细列出，其参数和发送的返回代码。这可用于识别程序的哪个步骤失败。

### 示例 8-17 使用 stracing 与 ls 命令

```
lnxguill:/mnt/backup # strace ls
execve("/bin/ls", ["ls"], [* 55 vars *]) = 0
brk(0)                               = 0x80018000
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001f000
uname({sys="Linux", node="lnxguill", ...}) = 0
access("/etc/ld.so.preload", R_OK) = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=33471, ...}) = 0
mmap(NULL, 33471, PROT_READ, MAP_PRIVATE, 3, 0) = 0x200000020000
close(3)                             = 0
open("/lib64/librt.so.1", O_RDONLY) = 3
```

> 注意：分析 strace 程序的输出需要与应用程序的开发团队密切合作。

本节提供了 z/VM 和 Linux 工具如何处理错误的简要概述，并详细介绍了在分析应用程序导致问题的原因时可使用的几种工具。

有时，程序异常终止可能导致数据损坏，例如，如果应用程序在崩溃时正在向磁盘写入某些数据。在这种情况下，唯一的选择可能是从已存在的备份中恢复数据，以返回到数据一致的状态。备份和恢复工具在下一章部分中进行了描述。

## 8.4 备份和恢复

备份是指制作数据的副本，以便在数据丢失事件后可以使用这些副本恢复原始数据。这些额外的副本通常称为备份，主要用于两个目的：

- 在灾难后恢复状态（称为灾难恢复）
- 在文件被意外删除或损坏后恢复少量文件

备份可以根据创建方式进行分类：

- 离线备份具有破坏性，需要规划。
- 在线备份不会中断操作。

本章介绍了用于备份和恢复 z/VM 和 Linux 数据的可用工具。





## 8.4.1 z/VM 离线备份

离线备份是具有破坏性的操作，因为它们需要停止系统。使用这些操作需要适当的规划，因为生产必须停止。

### 将 z/VM 系统复制到磁盘

将 z/VM 系统备份到磁盘需要两个 z/VM 分区：一个用于备份，另一个用于发出命令。第二个分区必须能够访问正在备份的 z/VM 分区的磁盘。

该过程涉及以下步骤：

- 1. 关闭要备份的 z/VM 系统（系统 A）。
- 2. 在另一个系统（系统 B）上，将系统 A 磁盘联机。
- 3. 从系统 B，使用 DDR（z/VM DASD Dump/Restore 程序）或 Flashcopy（如果已启用）复制系统 A 磁盘。
- 4. 将系统 A 磁盘脱机。
- 5. 重新 IPL 系统 A。

这无疑是一个具有破坏性的过程，因为在备份系统之前必须停止所有操作。

> 注意：使用此方法可以同时将 z/VM 和 Linux 保存到磁盘。

### 将 z/VM 系统备份到磁带

如前一章所述，此备份也需要两个 z/VM 分区，第二个分区访问第一个分区的系统磁盘。第二个分区还必须能够访问磁带驱动器。

该过程涉及以下步骤：

- 1. 将磁带驱动器连接到 z/VM 系统 B。
- 2. 倒带。
- 3. 将系统 A 磁盘联机。
- 4. 逐个将系统 A 磁盘复制到磁带上。
- 5. 完成后，分离磁带驱动器，并将系统 A 磁盘脱机。

> 注意：使用此方法可以同时将 Linux 和 z/VM 磁盘保存到磁带。

```text
fnl ftl fml,
' | STEM VOLUMES.'
return
```

### 从磁带恢复到 DASD

要求是 z/VM 上连接有 181 设备类型的磁带驱动器，以及一个包含要恢复到的目标 DASD 列表的 RESTAPE VOLUMES A 文件（参见示例 8-20）。可以通过在输入文件中指定 skip 来跳过恢复过程中的某些 DASD。

示例 8-21 是用于从磁带恢复到 DASD 的脚本。

**示例 8-20 输入文件 RESTAPE VOLUMES A**

```text
1800
1801
1802
1803
1804
skip
1806
1807
1808
1809
```

**示例 8-21 从磁带到磁盘恢复环境的示例脚本**

```text
/* DDR volumes must be defined in file restape volumes a */
Parse upper arg fnl ftl fml
If fml = '' then fml='A'
If fnl = '' then do
FNL='RESTAPE'
ftl='VOLUMES'
fml='A'
End
call traitfic
Traitement:
do i = 1 to volumes.0 by 1
if substr(volumes.i,1) = 'skip' then
do
SAY "Skipping 1 disk"
TAPE FSF 1
end
else
do
parse var volumes.i volout .
call restore
end
end
EXIT
restore:
 'MAKEBUF'
 SAY 'RESTORING TAPE DEVICE 181 TO " VOLOUT
 QUEUE 'IN 181 3590 (LEAVE'
 QUEUE 'OUT' VOLOUT '3390'
 QUEUE 'RESTORE ALL'
 QUEUE 'YES'
 QUEUE 'YES'
 QUEUE ''
 'DDR'
 'DROPBUF'
 return
 traitfic:
 'STATE' fnl ftl fml
 IF RC <> 0 THEN EXIT 99
 'pipe c',
   fnl ftl fml,
   ' | STEM VOLUMES.'
 return
```

### 由 z/OS 控制的 z/VM 和 Linux 磁盘备份

您可以将 z/VM 和 Linux 集成到现有的 z/OS 备份和恢复流程中。

Linux 磁盘必须为使用 dasdfmt 命令做好准备，该命令允许您使用特定布局、Linux 磁盘布局或兼容磁盘布局格式化磁盘。

兼容磁盘布局是 dasdfmt 的默认布局。这意味着通过在磁盘上写入卷目录表（VTOC）来对卷的前两个磁道进行特殊处理。这使得其他 System z 操作系统能够访问该设备（例如，用于备份目的）。

此 VTOC 允许从 z/OS 访问 Linux 磁盘。此磁盘可以视为一个数据集，例如 LINUX.VOX0200.PART0001.NATIVE；可以使用标准的 z/OS DFSMSdss™ DUMP 命令保存此数据集。

> z/OS 类比：以下 JCL 是使用 DFSMSdss dump 从 z/OS 备份 Linux 磁盘的作业示例：

```text
//STEP1  EXEC PGM=ADDRSSU,REGION=0M
//IDOT   DD  DISP=(NEW,CATLG),DSN=backup.dsn........
//SYSPRINT DD  SYSOUT=* 
DUMP INDY(1nxvol) OUTDD(IDIOT)
```





DFSMSdss dump 也可以用于执行 z/VM 备份。在这种情况下，必须执行必要的物理转储，其中指定要复制的磁道范围。

## z/OS 类比：下面的 JCL 是使用 DFSMSdss dump 从 z/OS 备份 z/VM 磁盘（3390-03）的作业示例：
//STEP1  EXEC PGM=ADDRSSU,REGION=0M
//IDIOT   DD  DISP=(NEW,CATLG),DSN=backup.dsn........
//SYSPRINT DD  SYSOUT=* 

DUMP TRACKS(0,0,3338,14) -
INDY(LX6RES) OUTDD(IDIOT) ADMINISTRATOR CPVOLUME
```

## 8.4.2 z/VM 在线备份

在线备份也可以称为热备份。执行备份前不需要关闭系统。

### 使用 SPXTAPE 备份 spool 文件

您可以使用 CP 命令 SPXTAPE 将 spool 和系统数据文件（即打印机、读入器和穿孔文件）以及保存的段、NLS 文件和映像库备份到磁带。

SPXTAPE 命令允许您选择性地将 spool 和系统数据文件备份到磁带并恢复到磁盘。所有文件都可以转储，也可以应用过滤器仅保存匹配的文件。

### 复制 z/VM CPOWNED 小型磁盘

您可以通过复制 z/VM 系统磁盘来对运行中的 z/VM 系统执行热备份。这是一种非中断备份，因为在复制磁盘的同时系统仍在运行。

每个 CPOWNED 磁盘在 MAINT 用户目录中都有一个对应的 fullpack MDISK 定义，如示例 8-22 所示。

> 注意：z/VM 安装后添加的 CPOWNED 磁盘也应作为 MAINT 用户目录中的 fullpack MDISK 添加，以保持一致性。

### 示例 8-22 CP 拥有的磁盘，以及对应的 MDISKs 定义

```
Ready; T=0.01/0.01 15:35:36
q cpown
Slot  Vol-ID  Rdev  Type  Status
1  LX6RES  1A20  Own  Online and attached
2  LX6SPL  1A21  Own   Online and attached
3  LX6PAG  1A22  Own   Online and attached
4  LX6W01  1A23  Own   Online and attached
5  LX6W02  1A24  Own   Online and attached

Ready; T=01/01.01 15:35:38
q v da
DASD 0122 3390 LX6SPL R/W      3339 CYL ON DASD 1A21 SUBCHANNEL = 000A
DASD 0123 3390 LX6RES R/W      3339 CYL ON DASD 1A20 SUBCHANNEL = 000B
DASD 0124 3390 LX6W01 R/W      3339 CYL ON DASD 1A23 SUBCHANNEL = 000C
DASD 0125 3390 LX6W02 R/W      3339 CYL ON DASD 1A24 SUBCHANNEL = 000D

Ready; T=01/01.01 13:35:12
```

这些小型磁盘可以使用 DDR 或启用时使用 Flashcopy 复制到新的一组磁盘上。示例 8-23 显示了复制第一个磁盘所需的一组输入。

### 示例 8-23 使用 DDR 复制 z/VM 磁盘

```
ddr
z/VM DASD DUMP/RESTORE PROGRAM
ENTER:
IN 123 3390
ENTER:
OUT 1B34 3390
ENTER:
COPY ALL
HCPDDR711D VALID READ IS LX6RES
DO YOU WISH TO CONTINUE? RESPOND YES, NO OR REREAD:
YES
HCPDDR711D VALID READ IS DK1B34
DO YOU WISH TO CONTINUE? RESPOND YES, NO OR REREAD:
YES
COPYING  LX6RES
END OF COPY
ENTER:

END OF JOB
PRT FILE 0172 SENT FROM MAINT    PRT WAS 0172 RECS 0006 CPY 001 A NOHOLD
NOKEEP
Ready; T=09/1.13 13:41:07
```

应复制所有 z/VM CPOWNED 磁盘，除了分页磁盘，分页磁盘可以简单地格式化并分配为分页设备。但是，该分页设备必须具有与现有分页设备相同的标签，否则复制的 z/VM 系统将无法正确 IPL。

> 注意：一个良好的做法是在复制 z/VM 系统后更改系统 DASDs 标签。有关更多详细信息，请参阅第 4.3.3 节“重新标记系统卷”，第 165 页。

此复制操作会生成一个全新的 z/VM 系统，准备好进行 IPL。IPL 必须强制执行，因为没有记录暖启动数据。有关暖启动数据的更多信息，请参阅第 5.2.1 节“z/VM IPL 工作流”，第 230 页。

> 重要：虽然 spool 文件（如读入器、打印机或穿孔文件）在复制过程中可能会丢失，但这不应导致重新启动 z/VM 和环境中运行的 Linux 虚拟机出现问题。
> 
> 此方法不能应用于运行中 Linux 机器的备份。对运行中 Linux 机器的备份可能导致数据不一致。

## 8.4.3 Linux 备份工具

Linux 发行版包含用于备份和恢复数据的工具。其中一些是基本工具，如 tar 或 cpio；其他则更复杂，如 IBM Tivoli Storage Manager。

尽管本节介绍了 Linux 发行版提供的用于执行备份的多个工具，但这绝不是一个完整的列表。

> 重要：本节描述的所有工具均不执行一致性检查或数据完整性控制。

### Tar 归档实用程序

tar 实用程序是标准的 UNIX 工具，用于从一组文件或目录创建归档。然后可以将此归档压缩并保存到另一组磁盘或磁带上。参见示例 8-24。

示例 8-24 使用 tar 归档文件

```
lnxquill:"# tar cvf varlog_backup.tar /var/log
tar: Removing leading '/' from member names
/var/log/
/var/log/yaST2/
/var/log/yaST2/y2logRPM
/var/log/yaST2/y2log
/var/log/yaST2/y2logmkinitrd
/var/log/yaST2/y2log_bootloader
```




```
/var/log/YaST2/volume_info
/var/log/YaST2/disk_dasda
/var/log/YaST2/disk_dasdb
/var/log/YaST2/disk_dasdc
[...]
/var/log/scpm
/var/log/slpd.log
/var/log/boot.omsq
/var/log/dump/
lnxguill:# ls -al
total 5280
drwx------ 5 root root 4096 May 29 14:36 .
drwxr-xr-x 22 root root 4096 May 29 13:54 ..
-rw------- 1 root root 2098 May 29 13:59 .bash_history
-rw-r--r-- 1 root root 1332 Nov 23 2005 .exrc
drwx------ 2 root root 4096 May 20 15:07 .gnupg
-rw------- 1 root root 1024 May 20 15:13 .rnd
-rw------- 1 root root 4072 May 28 10:12 .viminfo
drwxr-xr-x 2 root root 4096 May 20 15:14 .wapi
-rw-r--r-- 1 root root 31732 May 20 15:14 autoinst.xml
drwxr-xr-x 2 root root 4096 Jun 16 2006 bin
-rw-r--r-- 1 root root 5324800 May 29 14:36 varlog_backup.tar
```

生成的文件 varlog_backup.tar 然后可以被压缩并保存到另一块磁盘或磁带上。

tar 的另一个用途是通过 SSH 压缩要发送到备份服务器的数据量，如示例 8-25 所示。

## Example 8-25 Backing up using tar and ssh

```
ceron:/var/log # tar cvf - /var/log | ssh 9.12.5.66 tar xvf -
tar: Removing leading '/' from member names
/var/log/
/var/log/YaST2/
/var/log/YaST2/y2logRPM
/var/log/YaST2/y2log
var/log/
var/log/YaST2/
var/log/YaST2/y2logRPM
/var/log/YaST2/y2log
/var/log/YaST2/y2logmkinitrd
/var/log/YaST2/y2log_bootloader
[...]
var/log/zmd-messages.log.2008-05-25
/var/log/zmd-messages.log.2008-05-26
/var/log/zmd-messages.log.2008-05-27
/var/log/zmd-messages.log.2008-05-28
```

```
YaST2/disk_dasda
YaST2/disk_dasda-1
YaST2/disk_dasdb
YaST2/disk_dasdc
YaST2/disk_dasdc-1
YaST2/macro_inst_cont.y cp
YaST2/macro_inst_initial.y cp
YaST2/volume_info
YaST2/volume_info-1
YaST2/y2log
YaST2/y2log-1
YaST2/y2log.SuSEconfig
YaST2/y2logRPM
YaST2/y2log_bootloader
YaST2/y2logmkinitrd
YaST2/y2start.log
apparmor/
apparmor/reports-archived/
apparmor/reports-exported/
apparmor/reports/
audit/
audit/audit.log
cups/
dump/
krb5/
news/
news/news.crit
news/news.err
news/news.notice
smpppd/

sent 5282837 bytes  received 906 bytes  3522495.33 bytes/sec
total size is 5279388  speedup is 1.00
lnxguill:~ #

lnxguill:~ # rsync -av /var/log/ /mnt
building file list ... done
lastlog
messages
wtmp

sent 112424 bytes  received 86 bytes  225020.00 bytes/sec
total size is 5279901  speedup is 46.93
```

## LVM2 snapshot

快照是 Linux 逻辑卷管理器 2 (LVM2) 的一项功能，允许管理员创建一个新的块设备，该设备在某一时间点呈现逻辑卷的精确副本，被冻结。

通常，LVM2 在需要对逻辑卷执行某些批处理，例如备份，但又不想停止正在更改数据的实时系统时使用。当备份或快照设备完成后，系统管理员可以删除该设备。此功能要求快照必须在逻辑卷上的数据处于一致状态时创建。

在示例 8-28 中，已创建了逻辑卷 `/dev/mapper/vgsystem-varloglv` 的快照。此逻辑卷保存 `/var/log` 目录，而快照 `/dev/mapper/vgsystem-varlogsnapshot` 在某一时间点以一致状态呈现该目录的内容，以便将其备份到磁带。

### Example 8-28 Creating an LVM snapshot

```
lnxguil:~# mount
/dev/dasda1 on / type ext3 (rw,acl,user_xattr)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
debugfs on /sys/kernel/debug type debugfs (rw)
udev on /dev type tmpfs (rw)
devpts on /dev/pts type devpts (rw,mode=0620,gid=5)
/dev/dasdc1 on /usr type ext3 (rw,acl,user_xattr)
/dev/mapper/vgsystem-varloglv on /var/log type ext3 (rw,acl,user_xattr)
securityfs on /sys/kernel/security type securityfs (rw)
lnxguil:~# lvcreate -s -L 3500MB -n varlogsnapshot /dev/vgsystem/varloglv
  Logical volume "varlogsnapshot" created
lnxguil:~# mount /dev/mapper/vgsystem-varlogsnapshot /mnt/backup/
lnxguil:~# cd /mnt/backup/
lnxguil:/mnt/backup # ls -al
total 48
drwxr-xr-x  4 root root 4096 May 29 15:09 .
drwxr-xr-x  3 root root 4096 May 29 15:17 ..
-rw-r--r--  1 root root 11398 May 29 15:09 boot.msg
drwxr-xr-x 10 root root 4096 May 29 15:06 log
drwx------  2 root root 16384 May 29 15:05 lost+found
-rw-r-----  1 root root 1411 May 29 15:11 messages
-rw-r-----  1 root root 347 May 29 15:09 warn
```

有关逻辑卷管理器 2 的更多详细信息，请参阅第 258 页的 5.3.9，“Managing DASD”。





## 8.4.4 其他可用工具

备份和恢复软件可由许多厂商提供，包括：

- IBM Tivoli Storage Manager

IBM Tivoli Storage Manager 的备份和恢复解决方案是一个集中式、综合性的解决方案。它采用智能数据移动和智能数据存储技术，提供快速、灵活且影响小的备份和恢复。IBM Tivoli 存储产品套件支持十多种操作系统平台、多种网络连接器以及超过 500 种离线存储设备。

有关 IBM Tivoli Storage Manager 的更多信息，请参阅 IBM Tivoli 网站：

http://www-306.ibm.com/software/tivoli/solutions/backup/

- CA VM:Backup

该工具可以备份 z/VM 中的 CMS 和非 CMS 数据，以及 Linux 系统。用户可以恢复其个人文件或小型磁盘；管理员可以恢复完整卷或整个系统。当处理器上未运行操作系统时，CA VM:Backup 的功能 Hidro 可以提供独立的备份和恢复。

有关更多信息，请参阅 CA 网站上的产品简介：

http://ca.com/files/ProductBriefs/vmbubackup_pb2.pdf

- Innovation Data Processing’s FDR/UPSTREAM

该存储管理产品用于 Open 系统的集中化、自动化和无人值守的备份和恢复以及归档。您的数据可以存储在 LAN/NAS/SAN 上。该产品为 OS/390 或 z/OS MVS 大型机服务器提供自动操作。

有关 FDR/UPSTREAM 的更多信息，请参阅：

http://www.innovationndp.fdr.com/products/upstream/zlinuxups.cfm

数据库厂商也提供自己的数据库备份工具。例如，Oracle® 提供 RMAN，Recovery Manager，用于在各种平台上处理其数据库的备份和恢复。

## 应用系统维护

本章讨论维护 z/VM 系统所涉及的流程，与在 z/OS 上执行类似流程进行比较。它仅限于这些流程的技术方面，不讨论任何管理流程或例行程序。

### 目标

完成本章后，您应该能够：

- 讨论 IBM 为 z/VM 系统提供的维护方法
- 解释维护如何投入生产
- 识别 z/VM 与 z/OS 维护之间的相似性和差异

![](img/b0a4b9056f819dccd4781a5105c92d45_402_0.png)

用于执行系统维护的指定虚拟机是 MAINT，但 z/VM 站点可以建立其他专用于此类活动的虚拟机。

维护通常是通过使用“Virtual Machine Serviceability Enhancements Staged/Extended (VMSES/E)”产品来执行的，该产品可被视为 z/OS 中“System Modification Product/Extended (SMP/E)”的 z/VM 等效产品（提供相同的一组服务）。VMSES/E 包含一组以 EXEC 形式存在的工具，用于执行维护 z/VM 系统所需的任务。由于 z/VM 的特性，维护 z/VM 系统的过程比 z/OS 更具交互性。对于 z/OS，人员通常准备并运行批处理作业来执行这些任务。

### 9.3 VMSES/E 术语

本节解释了用于 z/VM 维护的几个术语。

#### 9.3.1 交付

对 z/VM 系统的一般服务或维护通常分为以下交付分类：

- Recommended Service Upgrade (RSU)
- Corrective Service (COR)
- Expanded Service Option (ESO)

ESO 是一个以 COR 格式定义的服务集合。它可以包括在起始和结束服务级别范围内的一系列服务，也可以更具体或针对服务类型进行定制，或根据您的配置进行定制。

包含服务的下载文件通常称为信封。

#### 9.3.2 元素术语

元素术语在以下列表中描述：

- 术语 authorized program analysis report (APAR) 和 program temporary fixes (PTF) 在 VMSES/E 中使用，其含义与 SMP/E 中相同。
- 术语 small programming enhancement (SPE) 用于安装产品新版本或新发行版的服务。这对应于 SMP/E 术语 FUNCTION。





术语 *local service* 或 *local modifications* 指的是 IBM 未在 COR 或 RSU 服务磁带或其他媒体上提供的任何服务。这包括：

- 因 COR 或 RSU 周期之间的错误而被迫安装的服务，例如 PTF
- 由第三方软件安装引起的任何修改
- 您安装的任何本地修改以定制您的系统

**z/OS 类比：** 在 z/OS 的 SMP/E 中，修改（第三方或本地）类似于 USERMOD。*在 COR 和 RSU 之间* 安装的 PTF 不会附带任何特殊定义。

为了正确管理服务，*z/VM VMSES/E Introduction and Reference*，GC24-6130 出版物强烈建议使用本地跟踪号。这类似于 SMP/E 中 SOURCEID 的使用，可在 RECEIVE 期间分配并用于服务的进一步处理。

## 9.3.3 BUILD 过程

当需要更新 z/VM 控制程序（CP，也称为 NUCLEUS）或共享段时，会使用 BUILD 过程。

对于 CP，更新需要 IPL。在 z/OS 中，服务应用于 SYS1.NUCLEUS。

对于共享段，更新需要重新启动受影响的虚拟机。z/OS 类比是 TSO/ISPF 用户在 LINKLIST 重建影响其 ISPF 应用程序之一后注销并重新登录。

## 9.4 比较 VMSES/E 和 SMP/E

VMSES/E 通常通过执行 VMFINS 并使用参数来执行不同类型的任务来调用。然而，还提供了其他可执行文件来执行更复杂的活动（链接、逻辑控制执行一个以上的 VMSES/E exec）。这些可执行文件的工作方式类似于具有多个步骤和条件执行的批处理作业。

有关使用 VMSES/E 的详细信息，请参阅 *z/VM VMSES/E Introduction and Reference*，GC24-6130。

VMSES/E 与 SMP/E 一样具有软件清单，默认情况下存储在由 MAINT 拥有的最小磁盘上。

### 9.4.1 安装 COR 服务

从 COR 磁带或其他媒体安装服务与在投入生产前执行 SMP/E RECEIVE/APPLY 过程非常相似。

要安装 COR 服务：

- 1. 阅读 MEMO to Users。
- 2. 使用 VMFREC 命令接收服务。
- 3. 查看 VMFREC 的任何消息并纠正它们。
- 4. 验证安装环境。
- 5. 运行 VMFAPPLY 应用服务。
- 6. 查看 VMFAPPLY 的任何消息并纠正它们。
- 7. 执行构建或重建组件所需的任何任务。
- 8. 查看任何消息并纠正错误。
- 9. 测试已服务的组件并纠正任何错误。
- 10. 构建任何已保存的段。
- 11. 将中间应用磁盘与测试过的服务合并到生产环境。

所有这些任务，除查看和纠正项目外，都可以通过使用复合 exec SERVICE 和 PUT2PROD 来执行。图 9-1 在第 392 页显示了取自 z/VM VMSES/E Introduction and Reference，GC24-6130 的 COR 安装流程。

步骤 1-3 对应于 SMP/E RECEIVE 过程；步骤 4-6 对应于 APPLY 过程；步骤 7-11 包括您通常在 SMP/E 之外执行的任何分发或其他活动，具体取决于您的流程。对于某些 z/OS 站点，SMP/E ACCEPT 可以作为流程的一部分。

具有每个产品的固定逻辑结构，如图 9-2 所示，也取自 z/VM VMSES/E Introduction and Reference，GC24-6130。

![](img/b0a4b9056f819dccd4781a5105c92d45_408_0.png)

图 9-2 RSU 媒体的逻辑文件结构

该过程按以下顺序执行：

- 1. 接收并查看产品的文档。
- 2. 使用 exec VMFPSU 准备接收产品以帮助您进行规划。
- 3. 从 RSU 接收。
- 4. 处理 RSU 中未包含的产品额外服务，包括任何本地修改。
- 5. 重建产品。
- 6. 对每个产品重复步骤，直到全部完成。

> 注：项目 4 类似于在 SMP/E 中由服务应用而 REGRESSED 的 usermods 的重新应用。

图 9-3 在第 394 页说明了 RSU 安装任务。





![](img/b0a4b9056f819dccd4781a5105c92d45_409_0.png)

Figure 9-3 PSU installation work flow

## 9.5 z/VM 的便捷维护实践

为维护 z/VM 系统提供一种便捷做法是为此目的启动或克隆一个二级 z/VM。从该克隆或副本内部，您可以对该系统执行任何服务活动。这为在对一级系统执行相同的维护之前进行测试提供了合适的环境。许多 z/VM 站点都是以这种方式进行维护的。此维护环境可以通过在为一级 z/VM 定义的虚拟机上安装新的 z/VM 来实现。您也可以克隆初始安装，前提是存在备份副本，并且包含原始安装的磁盘已被重新标记以避免潜在的重复 volser 情况。

有关安装二级 z/VM 的详细信息，请参阅手册 z/VM: Guide for Automated Installation and Service, GC24-6099

重复标记磁盘卷的情况在以下出版物中进一步讨论：

- z/VM and Linux on IBM System z: The Virtualization Cookbook for SLES9, SG24-6695

- IBM z/VM and Linux on IBM System z: Virtualization Cookbook for Red Hat Enterprise Linux 4, SG24-7272

## 9.6 案例研究

在撰写本书期间，在主系统下启动了一个二级 z/VM。服务从 Web 下载，然后我们使用 FTP 将其放到系统上 MAINT 的 500 虚拟磁盘上。这些下载的文件被 DETERSEd（使用 DETERSE MODULE 解压缩）到 MAINT 的 500 虚拟磁盘上，这次文件类型为 SERVLINK。您还应验证这些文件具有 4005 的记录长度。

> Note: All of these activities were performed from the MAINT virtual machine.

Example 9-1 显示了为每个下载文件调用 DETERSE exec 后的终端显示。

### Example 9-1 DETERSE of the downloaded files

```
Ready; T=0.01/0.01 09:28:23
deterse S7820380 SHIPSU1 H1 530RSU03 SERVLINK H
Ready; T=2.04/2.15 09:29:42
deterse S7820381 SHIPTFSS H1 530SERVI SERVLINK H
Ready; T=0.16/0.17 09:30:12
```

准备好文件后，我们在二级 z/VM 的虚拟机 VMGUEST 中发出以下命令，在从主机的 MAINT 机器上分离 500 磁盘后：

```
VARY ONLINE 500
ATT 500
ACC 500 h
FILEL * * h
```

> Note: The FILEL * * h command displays the DETERSEd files.

然后，我们发出 SERVICE 命令来安装 RSU：

SERVICE ALL 530RSU03

Example 9-2 和 Example 9-3 显示了调用的 SERVICE exec 的终端输出。

### Example 9-2 Output from SERVICE exec

```
VMFINS2603I Processing product :PPF SERVP2P REXX :PRODID 5VMREX30%REXX
VMFREC02805I Product :PPF SERVP2P REXX :PRODID 5VMREX30%REXX has passed requisite
    checking
VMFINT2603I Installing product :PPF SERVP2P REXX :PRODID 5VMREX30%REXX
VMFREC2760I VMFREC processing started
VMFREC1852I Volume 1 of 1 of INS ENVELOPE 5303
VMFREC1851I (1 of 4) VMFRCA XL processing AXLIST
VMFRCX2159I Loading 4 part(s) to DELTA 3D2 (K)
VMFREC1851I (2 of 4) VMFRCPTF processing PARTLST
VMFRC P2159I Loading 1 part(s) to DELTA 3D2 (K)
VMFREC1851I (3 of 4) VMFRCCOM processing DELTA
VMFRC C2159I Loading 3 part(s) to DELTA 3D2 (K)
VMFREC1851I (4 of 4) VMFCALL processing APPLY
VMFRC A2159I Loading part(s) to APPLY 3A6 (G)
VMFRC A2159I Loaded 5 part(s) to APPLY 3A6 (G)
VMFREC2191I Updating Requisite table 5VMREX30 SVR REQT, Description table 5VMREX30 SRVD ESCT and Receive Status table 5VMREX30 SRVRECS with 1 new PTFs from INS 5303
```

VM READ VMGUEST

### Example 9-3 More output from SERVICE exec

```
VMFUTL2205I BUILD9  R  R/W 402  MNT402
VMFUTL2205I BASE2  T  R/W 6B2  MNT6B2
VMFUTL2205I BASE4  U  R/W 3B2  MNT3B2
VMFUTL2205I --------  A  R/W 191  MNT191
VMFUTL2205I --------  B  R/W 5E5  MNT5E5
VMFUTL2205I --------  C  R/W 2CC  MNT2CC
VMFUTL2205I --------  D  R/W 51D  MNT51D
VMFUTL2205I --------  S  R/O 190  MNT190
VMFUTL2205I --------  Y/S  R/O 19E  MNT19E
VMFSET2760I VMFSETUP processing completed successfully
AUTO LOGON ***  BLDNUC  USERS = 14
BLDNUC : CONNECT= 00:00:01 VIRTCPU= 000:00.03 TOTCPU= 000:00.06
BLDNUC : LOGOFF AT 09:50:19 EDT FRIDAY 05/23/08 BY MAINT
USER DSC  LOGOFF AS  BLDNUC  USERS = 13  FORCED BY MAINT
VMFSET2760I VMFSETUP processing started for DETACH GCS
```




```text
VMFSET2760I VMFSETUP processing completed successfully
VMFSRV2760I SERVICE processing completed successfully for GCS BUILD
VMFSUT2760I VMFSUTFB processing started
VMFSUT2760I VMFSUTFB processing completed successfully
VMFSRV2760I SERVICE processing completed successfully
Ready; T=28.63/30.61 09:50:31
CMS

                         RUNNING   VMGUEST
```

### 9.6.1  调用 PUT2PROD

在执行完之前的步骤后，我们运行了 exec PUT2PROD。在 PUT2PROD 处理期间，我们遇到了其中一个 PTF 的问题。我们发现该特定问题已被记录为已知错误，其中还包含规避该问题的必要操作。在执行了记录的操作后，我们成功运行了 PUT2PROD exec。

完成后，我们从 MAINT 发出了以下命令：

```text
SHUTDOWN REIPL
```

发出该命令后表明 CP 级别现在已达到更高的 RSU 级别：

```text
Q CPLEVEL
```

### 9.6.2  安装额外的 PTF

然后我们应用了自 RSU 发布以来提供的额外 PTF。它们本应在 PUT2PROD 之前使用 SERVICE 安装，以避免我们最初遇到的问题。这些 PTF 的安装未成功完成。我们了解到 500 虚拟设备应处于读写模式（R/W），可能是因为在 SERVICE 过程中有一个临时构建过程正在使用该磁盘。纠正此问题后，SERVICE 成功完成，PUT2PROD 也成功完成。

> **重要：** 在使用 PUT2PROD 之前应用 PTF，以避免 PUT2PROD 中的错误。
> 
> 在安装 PTF 之前，请确保 500 虚拟设备处于 R/W 模式。

## 9.7 将已维护的 z/VM 投入生产

在对 z/VM 进行维护服务后，需要进行 IPL，因为它可能是对 CP 的服务。

在方便时，根据您的服务时间或其他条件，对系统进行 IPL。与任何其他操作系统一样，所有用户，或在这种情况下，所有虚拟机，都会被关闭。z/VM 具有执行 SHUTDOWN REIPL 的能力，前提是它是由具有执行此操作适当特权类的虚拟机发出的¹。需要始终运行的虚拟机可以在 IPL 期间自动注销（AUTOLOG）。

¹ 不必像 z/OS IPL 那样从 HMC 控制台执行

## 交叉引用：z/OS、z/VM 和 Linux 命令

本附录提供了 z/OS 命令和概念与其 z/VM 和 Linux 对应的交叉引用。虽然这里没有列出所有命令和概念，但我们认为这对于 z/OS 系统程序员更熟悉 System z 上的 z/VM 和 Linux 来说是一个良好的开端。

在我们的示例中，我们在需要具体说明时引用 SLES10 命令。我们建议检查您的 Linux 发行版以验证命令是否保持不变。

本附录包含以下表格：

- Table A-1 on page 400, Commands for file editing
- Table A-2 on page 400, General commands
- Table A-3 on page 401, FTP and TCP/IP commands
- Table A-4 on page 401, General concepts

### Table A-1 Commands for file editing

| z/OS-ISPF Edit | z/VM CMS XEDIT | Linux vi | Description |
|---|---|---|---|
| r | " | yy | Repeat or copy a line |
| d | d | dd | Delete a line |
| cc..cc line command | cc ...cc | :1,3co$ | Block copy |
| mm...mm line command | mm...mm | :1,3m$ | Block move |
| dd...dd | dd...dd | :1,3d | Block delete |
| find <xxxx> | /<xxxx> | /<xxxx> | Find keyword (below) |
| find <xxxx> prev | -/<xxxx> | ?<xxxx> | Find keyword (above) |
| ex xxx | — | — | Exclude lines containing a character string (xxx) |
| del all excluded | — | — | Delete the lines that you excluded using the command "ex xxx" |
| )n line command | — | — | Indent n spaces to the right |
| (n line command | — | — | Move n spaces to the left |

### Table A-2 General commands

| z/OS command | z/VM command | Linux command | Description |
|---|---|---|---|
| d u,,b120,1 | q b120 | ls -la /dev/<device> | Display a single device named b120 (replace b120 with your device) |
| d u,,b120,8 | q b120-b127 | ls -la /dev/sd* | Display string of devices |
| v b120,online | vary on b120 | mount /dev/<device> <mnt_point> | Vary on a device |
| v b120,offline | vary off b120 | umount mnt_point | Vary off a device |
| — | q paths b120 | — | Display paths to a device |
| — | q chpid 18 | — | Display devices on a chpid |
| D M=CPU | q proc | cat /proc/cpuinfo | Display number of processors |





## 表 A-3 FTP 和 TCP/IP 命令

| z/OS 命令 | z/VM 命令 | Linux 命令 | 描述 |
|---|---|---|---|
| FTP hostname {port} | FTP hostname {port} 如需选项列表，请输入： FTP ? | ftp hostname <-P port> | 连接到远程主机以获取或放置文件。默认端口为 21。 |
| HOMETEST | HOMETEST | ping <gateway ip address> | 验证 TCP/IP 配置。 |
| NETSTAT option {TCP procname} | NETSTAT option | netstat | 显示本地主机的网络状态。如需选项列表，请输入： ? |

## 表 A-4 通用概念

| z/OS | z/VM | Linux |
|---|---|---|
| IPL(初始程序加载) | IPL(初始程序加载) | boot |
| Nucleus | Control Program (CP) | kernel |
| HELP 命令 | HELP 命令 | man 命令 |
| 数据集 SYS1.UADS | user directory | user registry |
| TSO 或 ISPF 编辑 | XEDIT | vi |
| TSO 或 ISPF | Conversational Monitor System (CMS) | shell |

## 规划工作表

填写此工作表以存储您计划用于 System z 上 z/VM 和 Linux 安装的值。

*表 B-1 读者资源工作表*

| 名称 | 值 | 注释 |
|---|---|---|
| LPAR 名称 |  |  |
| CPC 名称 |  |  |
| z/VM 系统名称 |  |  |
| TCP/IP 主机名 |  |  |
| TCP/IP 域名 |  |  |
| TCP/IP 网关 |  |  |
| DNS 服务器 1 |  |  |
| DNS 服务器 2/3（可选） |  |  |
| OSA 设备名称 |  |  |
| OSA 起始设备号 |  |  |
| TCP/IP 地址 |  |  |

## 相关出版物

本节列出的出版物被认为特别适合对本书涵盖主题进行更详细讨论。

## IBM Redbooks

有关订购这些出版物的信息，请参阅第 408 页的“如何获取 Redbooks”。请注意，此处引用的某些文档可能仅提供软拷贝。

- Introduction to the New Mainframe: z/VM Basics, SG24-7316
- Linux Handbook A Guide to IBM Linux Solutions and Resources, SG24-7000
- Linux on IBM System z: Performance Measurement and Tuning, SG24-6926-01
- Security on z/VM, SG24-7471
- z/VM and Linux on IBM System z: The Virtualization Cookbook for SLES 10, SG24-7493

## 其他出版物

这些出版物也是进一步信息来源的相关资料：

- EREP V3R5 User's Guide, GC35-0151
- Linux on IBM System z: Performance Measurement and Tuning, SG24-6926
- Linux on System z: Using the Dump Tools, SC33-8412
- System z Hardware Management Console Operations Guide, SC28-6867
- z/OS: MVS Initialization and Tuning Reference, SA22-7592
- z/OS V1R9.0 Planning for Installation, GA22-7504-17
- z/VM: CMS Commands and Utilities Reference, SC24-6073
- z/VM: CMS File Pool Planning, Administration, and Operation, SC24-6074
- z/VM: CMS Planning and Administration, SC24-6078
- z/VM: CMS User's Guide, SC24-6079
- z/VM: CP Commands and Utilities Reference, SC24-6081
- z/VM: CP Planning and Administration, SC24-6083
- z/VM: General Information, GC24-6095
- z/VM: Getting Started with Linux on System z, SC24-6096
- z/VM: Guide for Automated Installation and Service, GC24-6099
- z/VM: System Operation, SC24-6121
- z/VM: V5R3.0 CP Messages and Codes, GC24-6119
- z/VM: V5R3.0 Diagnosis Guide, GC24-6092
- z/VM: V5R3.0 System Operation, SC24-6121
- z/VM: Virtual Machine Operation, SC24-6128
- z/VM: VMSES/E Introduction and Reference, GC24-6130
- z/VM: XEDIT User's Guide, SC24-6132

## 在线资源

这些网站也是进一步信息来源的相关资料：

- z/VM library
  http://www.vm.ibm.com/library/
- VM and the VM Community: Past, Present, and Future, Melinda Varian, SHARE 89 Sessions 9059-61, 1997
  http://www.princeton.edu/~melinda/25paper.pdf
- Memory planning
  - IBM z/VM Performance Resource pages:
    http://www.vm.ibm.com/perf/
  - Configuring Processor Storage:
    http://www.vm.ibm.com/perf/tips/storconf.html
- Logical Volume Management (LVM)
  - LVM HOWTO:
    http://tldp.org/HOWTO/LVM-HOWTO/
  - Disk performance optimizing:
    http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_optimizedisk.html





- 卷管理：
  http://www.ibm.com/developerworks/linux/linux390/perf/tuning_rec_dasd_volMan.html
- 来自 IBM 的 Linux 参考资料
  - 十大理由在 z/VM 上以客户机身份运行 Linux：
    http://www.vm.ibm.com/linux/benefits.html
  - IBM Linux 技术中心 (LTC)：
    http://oss.software.ibm.com/linux
  - IBM developerWorks 在 System z 上 Linux 的导航：
    http://www-03.ibm.com/systems/z/os/linux/
    http://oss.software.ibm.com/developerworks/opensource/linux390/index.shtml
  - IBM System z 上的 Linux：
    http://www.vm.ibm.com/linux/
    http://www.ibm.com/servers/eserver/zseries/os/linux/
- 来自其他来源的 Linux 参考资料
  - IBM：IBM System z 上 Red Hat Enterprise Linux 5 的安全优势：
    http://www.redhat.com/f/pdf/rhel/security_rhel5.pdf
  - Gentoo Linux 手册：
    http://www.gentoo.org/doc/en/handbook/index.xml
  - crontab 文件：
    http://www.linuxdoc.org
  - Shell 脚本教程：
    http://en.wikipedia.org/wiki/Shell_script
- 可用于 System z 的发行版
  - Novell SUSE Linux Enterprise Server (SLES) for System z；内核 2.6.16：
    http://www.novell.com/partners/ibm/mainframe/
  - Red Hat Enterprise Linux (RHEL) 5，内核 2.6.18：
    http://www.redhat.com/rhel/server/mainframe/
  - Debian for S/390 and zSeries；Debian Etch，内核 2.6.18：
    http://www.us.debian.org/ports/s390/
  - 通过以下地址下载内核自行构建：
    http://www.kernel.org

## 索引

## 数字
- 2048M 用户 ID 334
- 2084XA 0BE34E 364
- 3270 仿真器 161
- 3390/OC 3990/E9 303
- 520RES 154
- 530RES one 153
- 530RES 卷 165

## A
- A 磁盘 76, 126, 129–130
- 命令缩写 72
- 异常结束 352
  - 严重，CP 终止 353
  - 软 352
- ACTive 命令 325
- alloc 327–328
- Alt+Tab 序列 146
- 应用程序检索 334
- 异步传输模式 (ATM) 44
- ATTACH 命令 152
- 授权程序分析报告 (APAR) 389
- AUTO LOGON 233, 396

## B
- 后台处理 114
- 向后兼容性 11, 261
- 基本控制程序 (BCP) 320
- 基本模式 13
- 批处理文件夹 277
- 批处理作业 177, 227, 257, 274, 276, 363, 389–390
- 字节文件系统 (BFS) 22
  - CMS 记录文件 22

## C
- 缓存使用，CPU 中端口利用率 255
- 计划事件容量 (CPE) 100
- 按需容量 (COD) 100
- 命令区分大小写 72
- CBPDO 交付 123
- 中央处理器复合体 (CPC) 51, 143
- 通道到通道 (CTC) 7, 243
- 通道到通道适配器 (CTCA) 243
- chmod 命令 113–114
- G 类 71
- define CPU 316
  - 用户 71–72, 288
- 清洁启动 234, 237
- 清屏 63
- CMS 批处理设施
  - 机器 276–277
  - 虚拟机 276
- CMS 命令 22, 26
  - 环境 57
  - 格式 72
  - Help 36
  - SENDFILE 40, 267
- CMS 环境 40–41, 57, 249
- CMS 文件 29, 74, 77, 270, 272, 274, 294, 297
- CMS NSS 250
- CMS 用户 26, 72, 75, 127, 133, 295–296
- 冷启动 234, 237
- 目录内容的颜色 105
- 命令格式，XEDIT 80
- 命令行 35, 44, 54, 60
  - 区域 65
  - BACKWARD 和 FORWARD 子命令 85
  - BACKWARD、FORWARD 命令 85
  - CP 模式 66
  - 当前 SET TABS 子命令 88
  - 接口 66
  - LOGON 命令 60
- 命令模式，在 vi 编辑器中 115
- 配置文件 87, 92, 101, 126–128, 157, 286, 289
- 配置 KDM 216
- 控制程序 (CP) 9, 14, 127, 138, 284, 320–321, 352, 390, 401
- 会话式监控系统 (CMS) 9, 14, 19–21, 125, 238, 339, 401
- COPYFILE 命令 75–76, 90, 126, 173
- CP 命令 42, 72, 137, 236, 240, 250, 289, 293
  - 环境 57
  - 组 324
  - 不区分大小写 57




QUERY USERID 68
SPXTAPE 379
CP 监控器 324, 334
CP 规划 52, 290, 293
CP READ 55, 57
cp set 176, 324
PF11 188, 197
关闭信号 180 176, 197
CP SET SRM 命令 333
CP SPOOL
控制台关闭 359
控制台启动 357
CPACCESS 命令 174
CPC 恢复 145
LOAD 图标 170
cpdisk 172
CPSYN TAX 181
CPSYN TAX 命令 174
CPU 01 194, 251, 255, 315-316
store status 212

D
DASD
3390 在线 134
在 SLES10 安装中激活 202-203
地址 144, 260, 404
控制台日志 360
在 SLES10 安装中格式化 203
备份列表 376
管理多个 307
盘组 70, 259
实地址 260
重建 ramdisk 305
从磁带恢复 377
虚拟地址 191 19
卷 19, 134, 169, 225, 237, 258, 327, 330
卷设置 127
DASD 盘组 259
DDR 卷 376
交付
CBPDO 123
ServerPac 122
SystemPac 123
设备驱动程序 7-8, 302, 344
设备号 243
8FF 264
9FF 263
最小卡数 138
CP 查询名称 331
加载依据 235
最低 124
OSA Express 卡 138
OSA 启动 144, 403
主 OSA 404
实 I/O 325
DFSMS/VM 21, 27
直接访问存储设备。参见 DASD
DIRECTXA 命令 186, 222, 225, 297-298
DirMaint 28
DISABLE HCD 290
断开超时 172-173
不连续保存段 (DCSS) 235, 344-345
自主访问控制 (DAC) 288
磁盘标签 137, 187, 263
DISKMAP 命令 184
DK8228 8228 240
DMSACP723I F 130, 132
DMSFOR603R Format 137, 187, 263
DNS 服务器
1 143, 160, 403
2/3 143, 403
TCP/IP 地址 139
域名服务器 (DNS) 97
重复卷
标签 165
名称 165
动态主机配置协议 (DHCP) 97

E
编辑模式，XEDIT 81
编辑会话 79-80, 82-83, 88, 90
当前更改 80
系统故障 90
EDT 星期四 06/05/08 233, 361
环境记录编辑
和打印 356
错误消息 137, 354
COPYFILE 命令 76
设备错误 186
获取帮助 36, 43, 354
Linux 错误代码 355
最大存储容量 258
无重叠迷你磁盘 185
SET MSG OFF 命令 229
现有 CP 命令
新别名 289
新版本 289
扩展服务选项 (ESO) 389
外部安全管理器 (ESM) 4, 228, 285
z/OS 客户机 121
客户机系统 21, 246
客户机用户 69
ID 221, 225
ID SC59 222
虚拟机 69

## F

特性声明 173
文件模式 22, 73, 129–130
读写磁盘 75
Z 132, 187
Z b 132, 168
文件模式 Z 162
文件名 22, 73–74, 126–127, 129, 269
文件系统 22, 96–97, 101, 127, 129, 132, 141, 272, 291, 302, 304, 345
文件传输协议 (FTP) 96
FILE2 脚本 89
FILELIST 命令 73–74, 125–126
缩写形式 137
文件模式 Y 162, 175
文件池 272–274
文件系统层次结构标准 (FHS) 101
第一张 DVD 189
第一级 17, 101
CP 252
虚拟机 253
FORCE start 170
强制启动 234, 237
FORMAT 命令 187
格式，XEDIT 命令 80
格式化选项 36, 39
全屏 CMS 39
全屏模式 57, 229, 338

## H

硬件管理 50–52, 123, 145, 148
硬件管理控制台 (HMC) 51, 121, 398
HCPVM8392I INSTVM 156
帮助
CMS 中的命令 36
HCP053E 355
在 z/OS、z/VM、Linux 中 401
XEDIT 菜单 93
HELP 命令 36
CMS 中的帮助级别 39
HiperSockets 44–46, 48
HMC 145
CD-ROM/DVD 148
级别 145–146
加载图标 153
操作系统消息 164
单一对象操作 146
SYSG 154
系统控制台 (SYSC) 164
虚拟机监控程序技术 13

## G

GCS 组件 26, 31
授予访问权限 175, 197
图形用户界面 (GUI) 25–26
组控制系统 (GCS) 20, 24
客户机操作系统 3, 19, 21, 35, 47, 139, 177, 183, 219, 248–249, 253, 286, 295, 336, 345, 366
基础产品 21
客户机配置文件 197
客户机系统定义 54
级别 17
管理 248
共享数据 22
关闭信号 246

## I

I/O 配置任务 25
I/O 设备 3, 14, 18, 225, 247, 266, 334
I/O 子系统 247, 362, 365
深入 (ID) 22
初始程序加载 (IPL) 15, 123, 227, 229, 388, 390, 401
初始 ramdisk 304–305
输入文件
格式 376
管理 74
输入模式，XEDIT 81
输入或输出 (I/O) 14–16, 325
INSTPLAN 151
INSTVM EXEC 156
整数 275, 325
集成 3270 51–52, 123, 145, 154, 166
面向 Linux 的集成设施 (IFL) 7, 99, 138, 194
239
交互式问题控制系统 (IPCS) 24
接口 eth0 314
内部排队直接输入/输出 (IODIO) 46
用户间通信工具 (IUCV) 7
INUSE 328
无效密码 286
IP 地址 139
重置 369
接管 311
IPL CMS 156, 250
在 USER DIRECT 中定义 19
IPL 部分 305
IPL 时间 161, 163, 289, 294, 356
notauto 参数 163
IPWIZARD 143, 158
ISPF 编辑器 79–81, 124
行命令 84
主命令 87–88

J
作业控制语言 (JCL) 363, 378
作业输入子系统 (JES) 267, 275–276, 320
作业调度 274–275
后台作业 114

L
语言环境 (LE) 20, 25
最后一行 59
CMS 中帮助的层（级别）39
LIC 46
许可内部代码 (LIC) 46
行式打印机路由器 (LPR) 32
Linux 23, 47, 95, 121, 283–284, 288, 319–320, 351
Linux 发行版 97, 138–139, 218, 308, 381, 399
Linux 错误
代码 355
处理 355
Linux 客户机 7, 141–142, 144, 301, 309, 337, 367
缓存页面 343
容量要求 341
环境 192
IBM z/VM 处理器 341
IPL 操作 302
LNXCER 192–193
机器 189, 191
内存要求 343
建模工作负载 341
监控任务 345
性能监控 345
配置文件 189, 197
深远影响 343
原因之一 372
大小调整注意事项 343
存储 345
系统 172, 177, 183, 192
用户 181, 192–193
虚拟机 163
虚拟机大小 337
虚拟内存大小 337
z/VM 规划器 341
Linux 映像 6–7, 98, 141, 279, 344
磁盘存储 141
其他 203
Linux 内核 8, 149, 171, 189, 191, 302–303, 355
Linux 性能
带宽能力 47
数据 30, 338
收集器 30
Linux 系统 6, 36, 166, 192, 212, 214–215, 275, 289, 307, 337, 348, 386
管理员 140
调用 72
级别 142
LVM 195
开源性能分析器 348
Linux 技术中心 (LTC) 5
Linux 工作负载
容量 8
环境 341
LNXCER Pun 200
LNXDFLT 配置文件 194
LNXMAINT 183
加载图标 153
日志文件 317, 359
正确的文件数量 372
逻辑 CPU 254
逻辑分区 (LPAR) 25, 47, 100, 121, 238–239, 286, 341
定义 13
大型机中的模式 13
逻辑卷 209–210, 307, 385
精确副本 385
逻辑卷管理器 (LVM) 195
登录屏幕 60, 155, 216
logmsg 数据 125, 132, 233, 361
LPAR


- 创建 13
- 需求 138
- LPAR 模式 13
- LPAR 名称 224
- LVM 195
- LVM2 快照 385
- LX6PAG 1A22 171, 182, 240

## M

- MACH XA 135, 299
- MAINT 用户
  - 目录 379
  - ID 149, 197
- 主编号 302
- 强制访问控制 (MAC) 288
- MCH 详细报告 (MDR) 362
- MDISK 语句 184
- 成员名称 381–382
- 消息，显示紧急 52
- 小磁盘级别 272
- 多读 (MR) 模式 135, 167, 172

## N

- 命名保存系统 (NSS) 235, 249–250
- 网络接口 301, 309, 368
  - 卡 301, 313
- 网络作业输入 (NJE) 32
- 下次 IPL 170, 197, 234, 304

## O

- 开放系统适配器 (OSA) 20, 26, 138
  - Express2 26
  - 支持设施 20, 26
- 操作系统 (OS) 2, 96, 123, 139, 231–232, 235, 248, 286, 320, 336, 366, 386
  - 基本概念 13
  - 命令语言 56
  - 新版本 2
- OSA 适配器 44, 219
- OSA 卡 140, 144, 159–160
- OSA 设备
  - 名称 143, 403
  - 类型 144, 404
- OSA/SF 26
- 超额分配内存 175
- 重叠，搜索 185

## P

- PA1 键 252–253
- 页缓存 345
- 分页设备 240, 380
- 分区
  - 基本 13
  - z/VM 客户机 13
- 密码更改 140
- 模式 xxx 119
- 性能监控 8, 29, 338
- Performance Tool Kit 325
- pf12 ret 175, 197
- 物理连接 (PC) 50, 274, 338, 340
- 电源输入模式 89
- 电源输入模式 89
- 前缀区域 78–79, 81, 185
  - 字符 SI 83
  - 双字符 DD 82
  - 双字符 MM 85
  - 前缀子命令 79
- 前缀子命令 81, 83–85
  - 数据操作 81
- 特权类 18, 70–71, 235, 285, 287, 388, 398
  - A–G 287–288
  - ANY 288
- 产品服务升级 (PSU) 392
- 生产环境 2, 5, 13, 17, 142, 280
- 生产系统 6, 50–51, 53, 165, 248, 280
- PROFILE EXEC 55, 62, 126, 188, 222, 269, 358
  - 备份副本 162
  - LNXMAINT 的 188
- PROFILE Exec 126
- PROFILE LNXDFLT 194
- PROFILE XEDIT 91–92, 126, 128, 157–158, 162
  - Copy 125, 149
  - 文件 92
- PRT 66, 70, 125, 132, 233, 357–358
- PTFs 390, 397
- PUT2PROD 命令 156

## Q

- QUERY ALLOC
  - Page 240
  - PAGE 命令 182
  - SPOOL 命令 240
  - TDISK 241
- 排队直接 I/O (QDIO) 46, 335

## R

- RAM 存储 69
- ramdisk 映像 191
- RDR 66, 70, 125, 132, 233, 359
- 读卡器队列 267, 269, 271
- 读写访问 173
- 真实 DASD 259
  - 多种类型 260
  - 盘包 259, 261–262
  - 盘包地址 265
- 真实机器 2, 16, 35, 56, 287
  - 异常终止 2
- 真实存储 3, 34, 238, 256, 287, 330, 332, 366
- 推荐服务升级 (RSU) 124, 153, 389, 392
- RECS 0006 380
- Red Hat Enterprise Linux 288
- Redbooks 网站 408
  - 联系我们 xiii
- ref f 174
- RELEASE 命令 174
- 远程作业输入 (RJE) 32
- 远程排队通信子系统 (RSCS) 21, 31, 276
  - GCS 组件 31
- 资源访问控制设施 (RACF) 21, 30, 291
- 资源管理设施 (RMF) 30, 338
- 返回码 157, 355
- REXX/VM 20, 26
- REXX/VM 解释器 26
  - 单一源代码库 26
- root 密码 213
- RSCS 网络 32
- 运行的 z/VM 系统
  - 热备份 379
- 运行 z/VM 系统热备份 379

## S

- 同时 2, 13–14, 68, 132, 344, 388
  - 不同目录 132
    - 主机计算机 13
    - 峰值利用率 341
- SAPL 屏幕 52
- 保存段
  - 重建 171
- 屏幕清除 63
- 第二级
  - CP 252
  - z/VM 系统 252, 395
- 安全套接层 (SSL) 4, 284
- SENDFILE 命令 267
- ServerPac 交付 122
- 服务虚拟机 247
- SET VSWITCH GRANT 命令 197
- SFS 目录 90
- 共享文件系统 (SFS) 22, 163, 248, 272, 291
- SHUTDOWN 命令 165, 176, 234
  - z/VM 系统 236
- SHUTDOWN REIPL 157, 165, 236, 397–398
- 简单邮件传输协议 (SMTP) 97
- 单对象操作 146
- 单个 System z 6
  - 服务器 7
- 服务器平台 48
- SLES10
  - 安装时激活 DASD 202–203
  - 安装时格式化 DASD 203
  - 安装时分区 DASD 205
- 小型编程增强 (SPE) 389
- SMTP 服务器 164
- SNA 网络 24
  - 非 VM 系统 23–24
- 快照设备 385
- 排队数据 267
- 排队设备 248, 266, 268
- 排队文件 232, 235, 266, 268
  - 保存控制台日志 357
- 排队操作员 287
- SSH 连接 201
- 独立程序加载器 (SAPL) 52, 154
- 启动
  - 清洁 234, 237
  - 冷启动 234, 237
  - 强制 234, 237
  - 热启动 237
- 状态区域 57, 158
- 存储 RAM 69
- SUSE Linux
  - 企业版服务器 97
  - 企业版服务器 10 369
  - 版本 10 372
  - 版本 9 371
- 将作业挂起到后台 114
- SYSG 154
- 系统管理员 9, 35, 69, 71, 101, 140, 255–256, 259, 261, 285, 385





SYSTEM CONFIG 文件 52, 126–127, 166–167, 174, 231–232, 246, 289, 357, 366, 388
特性语句 173
系统控制台 (SYSC) 164
系统事件 351
信息收集 356
系统维护 3, 274, 280, 387, 389
系统操作员 25, 29, 51–52, 228, 242, 244, 287, 338, 356, 362, 367
系统程序员 277, 287–288, 324, 338
系统资源 5, 31, 237, 287, 291, 321–322, 324
高效利用 338
总量 337
系统资源管理器 (SRM) 332–333
系统启动 165, 175
System z 1, 4–6, 14–15, 26, 33, 44, 95–96, 123, 138, 142, 248, 283, 320, 336, 351, 378
Linux 安装 403
虚拟服务器 46–47
SystemPac 交付 123
系统网络架构 (SNA) 23–24

## T
T3390 参数，用于 DEFINE 命令 262
目标 DASD 123
TCP FTPSERVE 164
TCP INTCLIEN 164
TCP SMTP 164
TCP/IP 地址 139–140, 144, 403
TCP/IP 通信 46
TCP/IP 网关 139, 143, 403
TCP/IP 网络 25, 32, 48–49, 161, 244
TCPCMSU 184
TCPIP 228–229, 163, 244
TDISK 241, 259, 263
分配 262
总计 328
TDISK 分配 262
TDISK 总计 328
TELNET 服务器 164
TERM 命令 63–64
术语，DASD 和微型磁盘 259
抖动 337
当日时间 (TOD) 232–233
超时 63
透明服务访问设施 (TSAF) 20, 24, 26
三元组 73, 130, 138
TSO/ISPF 用户 73, 390

## U
未分配 RDEV 176
非请求文件传输 (UFT) 32
用户类别重构 (UCR) 235
用户定义 18, 135, 193, 195, 292, 295
USER DIRECT 18–19, 126–127, 134–135, 168, 220, 265
INCLUDE 语句 193
配置文件 193
源格式 294
源版本 294
系统卷 169
z/OS 客户机 225
z/VM 客户机定义 19
用户目录 186, 232, 248, 256, 293, 295, 360, 379, 401
DEDICATE 语句 44
用户 ZOS1 18
USER DISKMAP 文件 135, 185, 296, 300
用户 ID 26, 30, 68, 145, 149, 155, 158, 271, 273, 284, 354
访问 184, 197
通用接口 162, 187
CP 类别 19
MAINT 289
用户 MVSOPR1 230
用户空间 36, 74, 97, 130, 177, 368
用户 VMUSER1 229
User_Volume_Include 181
User_Volume_List 181

## V
VDISK 172–173, 177, 259, 261, 344
分配 264
vi 编辑器 115–116, 128
虚拟设备 35, 70, 243, 254, 261, 266, 397
地址 70
编号 70, 249, 260, 262, 264, 359
编号 000C 268
编号，管理 CPU 254
虚拟磁盘。参见 VDISK
虚拟机 2, 262, 283, 285, 319, 352
几乎用之不竭的备用系统 6
命令环境 57
命令语言 56
配置 127, 243
控制程序 14
崩溃 11
定义 295
目录条目 255, 257
转储 24
环境 2, 7, 57
客户机 69
高性能通信 7
IPL 操作 358
IPL CMS 129
管理 8
操作员 53–54
密码 284
打印机 359
生产系统 53
资源使用情况 324
单独的命令 224
会话 60–61
大小 142, 337, 344
管理程序 24
SVC76 命令 362
系统 285, 291
基本原理 16
用户 14, 56, 69
用户 ID 269, 284
用户名 269
虚拟 CPU 254
虚拟读卡机 359, 366
虚拟内存区域 (VMA) 350
虚拟网卡 194
虚拟处理器 67, 286
虚拟交换机。参见 VSWITCH
虚拟电信访问方法 (VTAM) 20
虚拟化技术 10
虚拟化环境 343–344
VM READ 57, 125, 155
状态 277
VMGUEST 396
VM 系统 2–3, 7–9, 13, 24, 27, 352, 356
APPC/VM 程序 13
其他 APPC/VM 程序 27
VMSES/E 27, 390–391, 393
VNC 客户端 201, 214
VNC 查看器 139
V SOLID Read 380
卷组 209–210, 308
逻辑卷 309
剩余空间 210
卷标签 124, 165, 260–261
卷 LX6RES 232–233, 328–329
卷 LX6W02 184, 300
VSWITCH 44, 128, 144, 163, 172, 174–175, 290
控制器 49, 176
控制器 1 和 2 175, 197
语句 290, 301
VTAM SNA 控制台支持 (VSCS) 24

## W
热启动 234, 237
广域信息服务器 (WAIS) 96
工作负载管理器 (WLM) 320
工作负载使用 337

## X
XAREPMAC 记录 363
XAUTOLOG 命令 163
XEDIT
"" 前缀命令 193
ADD 子命令 174
BOTTOM 子命令 174
编辑模式 81
FILE 子命令 174
输入模式 81
强力输入模式 89
powertype 89
PREFIX OFF 子命令 185
PROFILE 157
S 磁盘 76
会话 126, 162

## Y
YaST 安装 202, 211, 213

## Z
z/OS 类比 18, 127, 254, 390
全部 87
APPC/VM VTAM 支持 (AVS) 24
AUTOLOG1 用户任务 129
自动保存 90
AVS 24
备份 Linux 378
备份 z/VM 379
CMS 36
CMS 文件 22




将文件复制到新文件  77
复制行  85
CP  21
CP INDICATE  324
CP INDICATE PAGING  326
CP QUERY ALLOC  327
CP QUERY CPLOAD  329
CP QUERY FRAMES  330
CP QUERY NAMES  331
CP QUERY STOR  333
CP QUERY SYSTEM  333
D U,,ALLOC  333
删除  82
DFSMS/VM  27
转储查看工具 (DVF)  24
转储  367
EDIT 配置文件  93
EREP  363
不保存退出  91
退出帮助  93
FILEList (FILEL)  73
文件名  74
用于 z/VM 的 HCD 和 HCM  25
HELP  36
IEASYSxx, CP SET MAXUSERS  334
使用 XEDIT 插入行  82
插入外部文件  88
语言环境 (LE)  26
移动行块  85
浏览 HELP 菜单  44
OSA/SF  26
Performance Toolkit for z/VM  30
连续键入  89
前缀子命令  79
特权类别  71
查询  68
QUERY CPLEVEL  68
QUERY SRM  333
QUERY USERID  68
用于 z/VM 的 RACF  31
恢复行  83
重复行  84
REXX/VM  26
RSCS  32
调度程序与分派程序  34
SEND 命令  228
shell  96
SHUTDOWN  235
SMP/E  390
状态行  80
SYSLOG  360
系统清除  67
TCP/IP  23
上移和下移  86
USER DIRECT  18
XEDIT  78
XEDIT 前缀子命令  81
z/OS 客户机  54, 121, 140, 220, 225, 246
z/OS 提示  259, 262
z/OS 映像  2, 16, 33, 122–123, 219, 320
z/OS 系统  9, 121, 219, 293, 331, 388
IPL  219, 223
日志  226
程序员  95
z/OS 用户  51, 67, 124, 126, 228, 249, 276
z/VM
基本命令  65
cons==sysg  155
DIRECTXA 命令  186
断开超时  172
DISKMAP 命令  184
FORMAT 命令  187
INSTPLAN EXEC  151
INSTVM EXEC  156
IPWIZARD 命令  158
PUT2PROD 命令  156
RELEASE 命令  174
关闭系统  165
独立程序加载器  154
z/VM CP  53
z/VM CPACCESS 命令  174
z/VM 客户机  13, 140, 219, 224, 251–252, 341, 343
z/VM IPL  129
进程  232
时间  196
z/VM 操作系统 (z/OS)  13, 17, 69, 121, 319
z/VM 站点  122, 389, 394
z/VM 系统  4, 9, 15–17, 122, 140, 143, 230, 236, 246, 269, 284–285, 320, 324, 356, 366, 387
网络连接  44
性能管理  324
TCP/IP 地址  144, 159
各种记录  356
z/VM 用户  53, 55, 125, 128, 130, 227–228, 276
z/VM 5.3 版
检查磁盘链接和映射  132
CMS  125
控制台日志文件  359
CP 模式  66
安装介质  139, 145
IPL 190 249
IPL CMS 250
IPL 进程  233
LNXMAINT 控制台输出  361
LOGON MAINT 125, 132
