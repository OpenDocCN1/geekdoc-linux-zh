
从 x86 迁移到 Linux 的复杂性随平台架构和上下文而变化。Linux 操作系统更加直观，使得迁移更加容易。但是，当你考虑应用程序、数据库管理系统或中间件迁移时，需要考虑复杂性、成本和风险。

此附录提供了额外的用例场景，其中电信公司、医疗公司和能源公用公司都想从 x86 迁移到 LinuxONE。它描述了每个行业特定的挑战。

此附录包括以下章节：

- 电信行业整合与云
- 医疗行业：移动解决方案
- 能源公用行业：System z 云自动化解决方案

## 电信行业整合与云

在此场景中，电信公司 T1 选择 LinuxONE 平台用于 Linux 操作系统的整合和虚拟化。电信公司 T1 希望构建云平台，但他们希望减少运营成本和整体数据中心占用。该公司的策略是提高满足用户请求的业务系统 BSS 和支持系统 OSS。在此示例中，可以使用以下技术：

电信公司 T1 整合了以下基础设施：

- IBM LinuxONE Rockhopper
- IBM zVM 6.3
- 平台上的 Red Hat Enterprise Linux 或 SUSE Linux Enterprise
- IBM ProTIER Gateway TS7680：去重和虚拟带库

电信公司 T1 使用以下云应用：

- IBM SmartCloud®
- 使用 IBM Tivoli System Automation 进行自动化
- 自动配置：Tivoli Provisioning Manager
- 生命周期管理：IBM SmartCloud Control Center

电信公司 T1 使用这些构建监控和系统管理工具：

- zVM 和 Linux 上的 IBM Tivoli OverWatch：作为 zVM 虚拟机运行的实例及其负载性能如何以及如何相互影响：
- 通过详细的性能指标对比 Linux 操作。
- 来自性能工具（PTK 是先决条件）的数据收集补充了 IBM Tivoli Monitoring for Linux 代理的数据收集。
- 通过动态工作空间链接，您可以轻松地在 Tivoli 企业门户之间进行导航。
- 查看并监控虚拟机、组、响应时间和 LPAR 报告的负载，以及有关 zVM 和 Linux 使用资源（如 CPU 利用率、存储、小型磁盘和 TCP/IP）的视图。
- 高级帮助有助于了解系统性能如何影响业务和利润。
- 通过细粒视图，IT人员可以轻松跟踪跨多个系统和平台的复杂问题，并共享相关信息。
- IBM Wave for zVM v1.1：IBM 是一种 zVM 和 Linux 服务器的新型虚拟化管理产品，利用可视化极大地自动化并简化了管理和维护任务：
- 在单一仪表板中自动化、简化并监控虚拟服务器及资源。
- 与手动执行相比，可以在更短的时间内完成复杂的虚拟化任务。
- 配置虚拟资源（服务器、网络、存储）以加速云基础设施的转型。
- 使用高级的 z/VM 管理能力，例如通过几次点击即可实现虚拟机实时迁移（Live Guest Relocation）。
- 将责任下放到适当的团队，并提供更多的自助能力。

图 A-1 显示了使用 LinuxONE 的云解决方案的架构概述。

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_198_0.png)

图 A-1 使用 LinuxONE 的云解决方案

## 医疗健康行业：移动与互联网解决方案

在此场景中，虚构的 H1 医院选择了 LinuxONE 作为其移动应用平台。H1 医院希望构建一个安全的平台，提高响应速度和价值感知，并降低多平台开发成本。

使用以下工具来构建安全平台：

- IBM Worklife 作为其功能的一部分提供了可扩展的身份验证模型。为了符合联邦信息处理标准（FIPS），H1 医院结合 WebSphere Application Server 使用 Worklife 以获得额外保护。医院保护了后端服务器和数据的应用程序及适配器。
- 通过 Worklife，H1 医院可以根据角色、时间和位置授予数据访问权限。医生可以在移动设备上访问患者记录。然而，如果他们在家里或值班期间查看患者最新的观察结果，则需要额外的身份验证。此外，尽管医生可以访问其患者的信息，但医疗供应商也有权访问以检查并更新库存。

该解决方案旨在提高响应速度和感知价值：

- H1 医院正在寻找一种通信解决方案，以便在医院的任何地方找到员工。使用 Worklight，医院可以构建允许即时安全通信的应用程序。医生和护士可以快速找到同事，而无需停止手头的工作。
- 当 H1 医院医生的移动设备未连接网络时，必须输入处方。JSONStore 是 Worklight 中面向文档的存储系统，使用加密容器并确保运行应用程序的设备离线时，应用程序中的文档对医生可用。
- 通过该应用程序，患者可以使用移动设备预注册挂号，并输入他们的过敏史和健康状况。Worklight 使用带有服务器身份验证的安全套接层（SSL）并通过 HTTPS 进行通信以保护信息。

该解决方案还降低了多平台开发成本：

- Worklight 提供了一个基于标准的平台，允许 H1 医院使用第三方库和框架。
- 使用 Worklight，H1 医院还可以通过任何 HTML5、原生和混合开发方法的组合快速创建移动应用程序。

图 A-2 显示了通过全局安全策略和端到端安全事务，从移动设备到 LinuxONE 平台后端事务核心系统的安全访问。

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_200_0.png)

图 A-2 从移动设备到后端事务核心系统的访问

## 能源与公用事业行业：System z 上的 SAP 云自动化解决方案

在此场景中，场景 E1 选择 System z 平台作为运行在 Linux 上的 SAP 应用以及运行在 IBM z/OS 上的数据库。能源 E1 希望通过云解决方案和 SAP 系统自动化，将复制和刷新完整 SAP 系统的时间从几天缩短到几小时。这种组合可以实现 SAP 系统日常操作的自动化、标准化并提高速度，减少因人为错误导致的风险。

该公司还希望减少在复杂、重复性任务上花费的时间，释放熟练人员从事更高价值的工作，并提供更高的运营效率。这种减少有助于削减成本并加速新工作负载的价值实现。

公司构建了一个包含以下项目的虚拟平台：

- IBM zEC12 或 zBC12。
- IBM zVM 6.3。
- z 平台上的 Red Hat Enterprise Linux 或 SUSE Linux Enterprise Server。
- IBM DB2 for z/OS。
- IBM Database Provisioning System (DPS):
  - Web 应用 JCL 引擎。
  - 数据库管理。
  - 与 DB2 Cloning Tool 集成。

z/OS IBM DB2 Cloning Tool：DB2 Cloning Tool 在几分钟内提供可用的 DB2 克隆，提高了效率并释放了 DBA 时间：

- 快速克隆 DB2 子系统、DB2 表空间或索引空间以创建环境。
- 自动化克隆过程，在几分钟内提供可用的 DB2 克隆。
- 通过重命名和目录数据集、修复卷内部结构以及更新 DB2 内部控制信息来克隆 DB2 子系统。
- 快速复制技术可以在子系统内或跨子系统复制 DB2 数据集。
- 使用卷级技术（如 IBM Flashcopy）自动化克隆过程，克隆 DB2 子系统以及任何数据复制技术（如 Flashcopy），克隆表和索引空间，并自动转换对象 ID 以简化和自动化数据刷新。

SAP NetWeaver Landscape Management (LVM)：通过精简和自动化业务流程，SAP NetWeaver LVM 软件使您的 IT 部门能够专注于新倡议、控制 IT 成本并实现业务差异化：

- 管理物理和虚拟化环境中针对您的 SAP 布局的管理点。
- 集中化管理、日常管理和生命周期管理任务。
- 通过自动化复制、克隆和刷新来实现自动化，节省时间、精力和资金。

构建具有自动化生命周期管理操作的用于 SAP 的 IBM Entry 云解决方案：

IBM Entry Cloud 配置简化了数据库、操作系统、存储系统和 SAP Basis 管理员所执行的复杂任务。当与 SAP NetWeaver LVM 结合时，它将复制和刷新 SAP 系统的时间从几天缩短到几小时。自动化程度也提高了质量。

要构建用于 SAP 的 IBM Entry Cloud 解决方案，请选择：

- SAP System Copy：刷新新系统。
- SAP System Copy：刷新现有系统。
- SAP System Refresh：从 PRD（生产环境）复制到非 PRD。
- 使用 z/VM v6.2 单系统映像 (SSI) 和虚拟机实时迁移 (LGR)。

System z Linux，IBM Entry Cloud 解决方案非常适用于希望在本地环境中通过 IBM DB2 for z/OS 运行 SAP 的任何 IT 组织。图3 显示了该解决方案与传统方案相比的额外价值。

图 A-3 使用 Entry Cloud Solution 自动化系统复制
