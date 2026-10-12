
# Linux Oracle Grid Infrastructure 安装指南

![](img/bcef005f52e2f1502f2321ec621dac26_0_0.png)

主要作者：Aparama Kamath

贡献作者：Douglas Williams, David Brewer, Jonathan Creighton, Barb Lundlund, Saar Maoz, Marcus Michalew, Hanlin Qian, James Steinner

贡献者：Aman Kushwaha, Tony Antony, Ravi Avidaiyan, Mario Brient, Mark Bauer, Yuki Feng, Mark Fuller, Bob Glover, Paul Hunter, Yengvei Hu, Masaku Ito, Mayumi Hayasaka, Prashak Joshi, Sameer Joshi, Rohan Karn, Krapp, Eric Kaiser, Jai Kraisani, Shanka Lanka, Okamura, Stefan Freeman, Jain Sharma, John Lee, John Sharp, Scott Lu, Dave Macrath, Meng Ge, Manoj Aminani, Anil Nagar, Vanir, Saxena, James Simmons, Akshay Shah, Arsh Shakan, Vivian Schman, Miles Paler, Stalai Dalip, Deepak Saggi, Bob Thom, Matt T Taylor, Federico Valle, Rickman, Jim Woack, Warren Xu, Sivakumar Yarlagada, Mino, Watanabe, Zheng

## 前言

## 3 为集群和 RAC 上的 Oracle Grid Infrastructure 配置存储

## 4 使用 OUI 安装集群 Oracle Grid Infrastructure

+ 4.1 准备使用 OUI 安装 Oracle Grid Infrastructure ................................ 4-1
4.3 安装 Oracle Grid Infrastructure ................................... 4-7
4.4 使用仅软件安装安装 Oracle Grid Infrastructure ............... 4-9
4.4.1 安装软件二进制文件 ........................................ 4-9
4.4.2 配置软件二进制文件 ................................. 4-10
4.4.3 使用响应文件配置软件二进制文件 ................................. 4-10
4.8 Oracle Grid Infrastructure 的离线过程 .................................4-12

## 5 Oracle Grid Infrastructure 安装后过程

## 6 如何修改或安装 Oracle Grid Infrastructure

## A Grid Infrastructure 安装过程排错

+ A.10 存储配置问题..................................A-12
+ A.10.1 从丢失节点文件系统或 Grid Home 中恢复.......A-12

### A.10.2 Oracle ASM 库驱动程序问题 ............................................................ A-13

### A.11 在脚本运行结束前完成安装.............................. A-14

## B 使用响应文件安装和配置 Oracle

### B.1 响应文件的工作原理.................................................................................. B-1

### B.1.1 使用静默模式或响应文件的原因 ........................................ B-2

### B.1.2 使用响应文件的通用步骤 ........................................................ B-2

### B.2 准备响应文件............................................................................................... B-2

### B.2.1 编辑响应文件模板.................................................................................. B-3

### B.2.2 记录响应文件....................................................................................... B-4

### B.3 使用响应文件运行安装程序..................................................................... B-5

### B.4 使用响应文件运行网络配置助手.................................................. B-5

### B.5 使用响应文件进行安装后配置.................................................... B-6

### B.5.1 关于安装后配置文件.................................................................. B-6

### B.5.2 使用响应文件运行安装后配置....................................... B-7

## C 配置大内存优化

### C.1 HugePages（巨页）概述.......................................................................... C-1

### C.1.1 HugePages 提供了什么...................................................................... C-1

### C.2 HugePage 配置的限制............................................................... C-2

### C.3 禁用透明巨页（Transparent HugePages）........................................... C-2

## D 集群基础结构的 Oracle Grid Infrastructure 概念

### D.1 理解安装前配置....................................................... D-1

### D.1.1 理解 Oracle 组和用户.................................. D-1

### D.1.2 理解 Oracle Base 目录路径........................................................ D-3

### D.1.3 理解网络地址....................................................................... D-3

### D.1.4 理解网络时间要求........................................................... D-5

### D.2 理解存储配置.................................................................... D-6

### D.2.1 理解 Oracle 自动存储管理集群文件系统.................. D-6

### D.2.2 迁移现有的 Oracle ASM 实例.................................................................. D-6

### D.2.3 关于将独立 Oracle ASM 实例转换为集群实例......................... D-7



### D.3 理解服务器池
### D.3.1 服务器池和基于策略的概述
### D.3.2 服务器池如何工作
### D.3.3 空闲服务器池（Free Server Pool）
### D.3.4 通用服务器池（Generic Server Pool）
### D.4 理解原地升级（Out-of-Place Upgrade）

## E 如何手动完成安装前提任务

### E.1 在所有集群节点上手动配置 SSH
### E.1.1 检查系统上的 SSH 配置
### E.1.2 在集群节点上配置 SSH
### E.1.3 在集群节点上启用 SSH 用户等效性
### E.2 配置内核参数
### E.2.1 安装的最小参数设置
### E.2.2 SUSE Linux 的额外参数和内核设置
### E.3 手动检查 OCFS2 版本

## F 如何升级到 Grid Infrastructure 11g Release 2

### F.1 升级前备份 Oracle 软件
### F.2 取消 Oracle 环境变量
### F.3 ASM 和 Oracle Grid Infrastructure
### F.4 集群软件的限制
### F.5 准备升级现有的集群软件
### F.5.1 完成现有集群软件升级的检查
### F.5.2 使用 CVU 检查就绪状态
### F.6 使用 CVU 验证集群软件
### F.6.1 关于 CVU 升级选项
### F.6.2 验证数据库就绪状态
### F.6.3 验证数据库就绪状态
### F.7 从早期版本进行滚动升级
### F.7.1 节点不可用时的集群软件升级
### F.7.2 节点不可用时完成集群软件升级
### F.7.3 Oracle 自动存储管理的滚动升级
### F.8 更新数据库控制和网格控制
### F.9 解锁现有的集群软件
### F.10 升级后集群软件降级
### F.11 升级后集群健康检查大小

## 索引

## 表格列表

- 1–1 64 位 Linux 和 Linux 交换空间
- 2–1 64 位 Linux 和 Linux 交换空间
- 2–2 Linux 交换空间
- 2–3 命名服务示例
- 2–4 网络配置示例
- 2–5 x86 操作系统内核要求
- 2–6 x86 Grid Infrastructure 和 Oracle RAC 要求
- 2–7 x86 数据库功能要求
- 2–8 x86-64 操作系统内核要求
- 2–9 x86-64 Grid Infrastructure 和 Oracle RAC 要求
- 2–10 x86-64 数据库功能要求
- 2–11 IBM：安装所有者资源建议范围
- 3–1 支持 Oracle ACIS 和 Oracle ADVM 的平台
- 3–2 集群软件和 Oracle RAC 支持的存储空间
- 3–3 集群软件共享文件系统卷要求



- 3–4 Oracle RAC 共享文件系统卷要求................................................ 3-8

- 3–5 按冗余类型所需的 Oracle 集群软件总存储空间...............................               3-20

- 3–6 按冗余类型所需的 Oracle 数据库总存储空间............................... 3-20

## 前言

《Linux 版 Oracle Grid Infrastructure 安装指南》介绍了如何配置服务器，以便为安装和配置 Oracle Grid Infrastructure（Oracle Clusterware 和 Oracle Automatic Storage Management）做好准备。它还解释了如何配置服务器和存储，为安装 Oracle Real Application Clusters（Oracle RAC）做好准备。

# 目标读者

《Linux 版 Oracle Grid Infrastructure 安装指南》为网络和系统管理员提供配置信息，并为在集群安装的 Oracle Grid Infrastructure 环境中安装和配置 Oracle Clusterware 和 Oracle Automatic Storage Management 的数据库管理员（DBA）提供数据库安装信息。

对于打算安装 Oracle RAC 的具有特殊系统角色的客户，本书旨在供系统管理员、网络管理员或存储管理员使用，用于配置系统以为集群版 Oracle Grid Infrastructure 安装做好准备，并完成所有需要系统 root 权限的配置任务。当 Oracle Grid Infrastructure 安装和配置成功完成后，系统管理员只需提供配置信息，并授予数据库管理员在 Oracle RAC 安装期间运行脚本的权限。

本指南假设您熟悉 Oracle Database 概念。更多信息，请参阅“相关文档”列表中的书籍。

# 文档可访问性

有关 Oracle 对无障碍访问承诺的信息，请访问 Oracle 无障碍访问计划网站：http://www.oracle.com/pls/topic/lookup?ctx=acc&id=docacc。

# 获取 Oracle 支持

购买了支持服务的 Oracle 客户可以通过 My Oracle Support 访问电子支持。更多信息，请访问 http://www.oracle.com/pls/topic/lookup?ctx=acc&id=info；如果您有听力障碍，请访问 http://www.oracle.com/pls/topic/lookup?ctx=acc&id=trs。

# 相关文档

如需更多信息，请参考以下 Oracle 资源：

# Oracle Clusterware 和 Real Application Clusters 文档

本安装指南概述了完成 Oracle Clusterware 和 Oracle Automatic Storage Management 安装所需的步骤，以及执行 RAC 预安装步骤。

如果您需要安装 Oracle Database 或 Oracle RAC，请按照本安装指南所述完成预安装任务，完成 Oracle Grid Infrastructure 安装，并查看相应的安装指南以获取更多信息。您可以在 Oracle Grid Infrastructure 安装上为单机服务器安装 Oracle 数据库，也可以安装 Oracle RAC 数据库。如果您想安装 Oracle Restart 部署的 Grid Infrastructure，请参考《Linux 版 Oracle Database 安装指南》。

大多数 Oracle 错误消息文档仅以 HTML 格式提供。如果您只能访问 Oracle 文档介质，请按范围浏览错误消息。使用浏览器的“页面查找”功能定位特定消息。在连接 Internet 时，您可以使用 Oracle 在线文档的错误消息搜索功能搜索特定的错误消息。

# 安装指南

- *Linux 版 Oracle Database 安装指南*

- *Linux 和 UNIX 版 Real Application Clusters 安装指南*

# 特定于操作系统的管理指南

- *UNIX 版 Oracle 管理参考, 11g Release 2 (11.2)*

# Oracle Clusterware 和 Oracle Automatic Storage Management 管理指南

- *Oracle Clusterware 管理与部署指南*

- *Oracle Automatic Storage Management 管理员指南*

# Real Application Clusters 管理指南

- *Real Application Clusters 管理与部署指南*

- *Oracle Database 2 Day + Real Application Clusters 指南*

# 通用文档

- *Oracle Database 2 Day DBA*

- *Oracle Database 管理指南*

- *Oracle Database 概念*

- *Oracle Database Net Services 管理员指南*

- *Oracle Database 参考*

打印文档可在 Oracle Store 购买：

```
https://shop.oracle.com
```

要下载发布说明、安装文档、白皮书或其他资料，请访问 Oracle Technology Network (OTN)。在使用 OTN 之前您必须在线注册；注册是免费的，可以在以下网站进行：

http://www.oracle.com/technetwork/index.html

如果您已拥有 OTN 的用户名和密码，可以直接进入 OTN 网站的文档部分：

http://www.oracle.com/technetwork/indexes/documentation/index.html

Oracle 错误文档仅以 HTML 格式提供。您可以在安装介质的 Documentation 目录中按范围浏览错误消息。当您找到某个范围时，使用浏览器的搜索功能定位特定的错误消息。在连接 Internet 时，您可以使用 Oracle 在线文档的错误消息搜索功能搜索特定的错误消息。

# 惯例

本文使用了以下文本约定：

| 惯例 | 含义 |
|---|---|
| **粗体** | 粗体表示与操作相关的图形用户界面元素，或正文或表表中定义的术语。 |
| *斜体* | 斜体表示书名、强调或由您提供特定值的占位符变量。 |
| 等宽字体 | 等宽字体表示段落中的命令、URL、示例中的代码、屏幕上显示的文本或您输入的文本。 |

## Oracle Grid Infrastructure 安装和配置有哪些新功能？

本节描述了与 Oracle Grid Infrastructure（Oracle Clusterware 和 Oracle Automatic Storage Management）以及 Oracle Real Application Clusters（Oracle RAC）安装和配置相关的新功能。本指南取代了《Clusterware 安装指南》。本节主题为：

- Release 2 (11.2.0.4) 的新功能

- Release 2 (11.2.0.4) 不支持的选项

- Release 2 (11.2.0.3) 的新功能

- Release 2 (11.2.0.2) 的新功能

- Release 2 (11.2) 的新功能

- Release 1 的新功能

## Release 2 (11.2.0.4) 的新功能

以下是 Release 2 (11.2.0.4) 的新功能列表：

### Cluster 和 Oracle 诊断工具增强

从 Oracle Infrastructure 开始，Trace Analyzer 和 Collector 会随 Oracle Infrastructure 自动安装。Trace Analyzer 和 Collector 是一种诊断工具，用于简化 Oracle Clusterware、Oracle Infrastructure 和 Oracle RAC 的诊断收集。

注意：从 Release 2 的 Oracle Infrastructure 开始提供 Trace Analyzer 和 Collector。

另请：Clusterware 管理与部署指南

### Oracle Database 健康检查和最佳实践建议

Oracle RAC 配置审计工具 (RACcheck) 随 Oracle Infrastructure 提供，用于评估单实例和 Oracle RAC 的已知配置问题、最佳实践、定期健康检查以及升级前和后的最佳实践。

注意：RAC 配置审计工具从 Oracle Infrastructure 11g Release 2 开始提供。



另请：*Real Application Clusters 管理与部署指南*

## Release 2 (11.2.0.4) 不支持的选项

以下功能不再受 Oracle Infrastructure 11g Release 2 支持：

### OUI 不支持块设备和行设备

此此，OUI 不支持在块设备或行设备上安装 Oracle Cluster 文件。请在 Oracle Storage Management 磁盘组或支持的文件系统上安装 Oracle Cluster 文件。

### `-cleanupBase` 的弃用

卸载工具的 `-cleanupBase` 标志在此版本中已弃用。该标志暂无替代方案。

## Release 2 (11.2.0.3) 的新功能

以下是 Release 2 (11.2.0.3) 的新功能列表：

### 对 Oracle Linux (UEK) 的 Oracle ACFS 和 ADVM 支持

适用于 x86-64 位的 Linux Oracle ASM 11g (11.2.0.3) 支持 Oracle Linux 内核 UEKs-2.6.32-100.34.1 以及后续 2.6.32-100 内核的 Oracle Storage Management 集群文件系统 (ACFS) 和 Oracle ASM 卷管理器 (ADVM)。

### 对 SUSE Enterprise Linux 11 的 Oracle ACFS 和 ADVM 支持

适用于 x86-64 位的 Linux Oracle ASM 11g (11.2.0.3) 支持 SUSE Enterprise Linux 11 Service Pack 1 (SLES11 SP1)，64 位的 Oracle Storage Management 集群文件系统 (ACFS) 和 Oracle ASM 卷管理器 (ADVM)。

### Oracle Clusterware 升级配置功能

如果节点在升级过程中无法访问，从 11.2.0.3 版本开始，您可以带有 `-force` 标志运行 `rootupgrade.sh` 脚本以完成升级。

## Release 2 (11.2.0.2) 的新功能

### Oracle Grid Infrastructure 软件配置向导

Oracle Grid Infrastructure 配置向导允许您在执行纯软件安装后配置 Oracle Grid Infrastructure 软件。不再需要手动编辑 `config_params` 配置文件，此向导将引导您逐步完成整个过程。

另参阅《Oracle Clusterware Administration and Deployment Guide》以获取有关配置向导的更多信息。

## 增强补丁集安装

从 Oracle Grid Infrastructure 11g Release 2（Oracle Clusterware 和 Oracle Automatic Storage Management）的 11.2.0.2 补丁集开始，Oracle Grid Infrastructure 补丁集是该软件的完整安装。新的补丁集封装带来了以下变化：

- 支持从之前的版本（11.x，10.x）直接升级到最新的补丁集。
- 仅支持离置（Out-of-place）补丁集。离置升级是将补丁集安装到新的、独立的目录（home）中。
- 新安装由安装最新的补丁集组成，而不是先安装基础版本再升级到补丁版本。

另参阅 My Oracle Support 备注 1189783.1，“Starting With 11.2.0.2 Important Changes to Oracle Database Patch Sets”，可用 URL 为：

```
https://support.oracle.com
```

## Oracle ACFS 和 ADVM 对 SUSE Linux 的支持

Oracle ASM 11 release 2 (11.2.0.2) 以及针对 x86-64 位 Linux 系统支持在 SUSE Linux 10 Service Pack 3 (SLES10 SP3) 及后续 SLES10 服务包上的 Oracle ASM Dynamic Volume Manager (ADVM)（仅限 64 位）。

## Oracle Clusterware 包含 Cluster Health Monitor

Cluster Health Monitor 实时收集系统指标并在存储库中收集其他指标以便后续分析，从而能够在 Oracle Support 的帮助下确定许多 Clusterware 和 Oracle RAC 问题的根源。

Cluster Health Monitor 还结合 Oracle Database Quality of Service Management (QoS) 工作，通过提供指标检测节点上的内存过度提交。QoS 管理可以关闭过载节点的服务以减轻压力并保护现有的工作负载。

为了支持 QoS 管理，Oracle Database Resource Manager 和指标已增强，以支持细粒度的性能指标，并且还可以使用用户定义的性能类管理工作负载。

> 注意：Cluster Health Monitor 不适用于 IBM: Linux on System z。

## Grid 安装所有者和 ASMOPER

在安装期间，在特权操作系统组中，可以选择指定一个组作为 ASM 组的 OSOPER。如果您选择为 ASM 组创建 OSOPER，则可以输入在所有集群节点上配置的 ASM 组 OSOPER 组名。此外，Grid Infrastructure 安装所有者不再需要是该组的成员。

## 新软件更新选项

使用 Software Updates 功能在 Oracle Database 安装过程中动态下载并应用更新。您还可以使用 `downloadupdates` 选项单独下载更新，并在后的安装过程中提供更新所在的位置来应用它们。

## 冗余互连的使用

在之前的版本中，需要利用冗余网络进行互连、绑定（bonding）、汇聚（trunking）或类似技术。Oracle Grid Infrastructure 和 Oracle RAC 现在可以使用冗余网络互连无需其他技术来增强集群的光纤通信。此功能从 Oracle Database 11g Release 2 (11.2.0.2) 开始可用。

冗余互连的使用允许多个（最多四个）专用网络（也称为互连）之间实现负载均衡和高可用性。

## Oracle Database Quality of Service Management

Quality of Service (QoS) Management 服务器允许管理员通过关联运行性能和资源指标，并使用专家系统进行分析，产生建议的资源调整以满足策略目标，从而管理托管在 Oracle 集群中的应用程序服务级别。

Oracle Database Quality of Service Management 不适用于 Linux on System

> **另参阅：**Oracle Database Quality of Service Management User's Guide

## Release 2 (11.2) 的新功能

以下是 Oracle Clusterware 和 Oracle ASM 11g release 2 (11.2) 安装的新功能列表：

### Oracle Automatic Storage Management 和 Oracle Clusterware

通过 Oracle Grid Infrastructure 11g release 2 (11.2)，Oracle Automatic Storage Management (ASM) 和 Oracle Clusterware 被安装在单个目录中，称为 Grid Infrastructure 目录。配置向导在配置 Oracle ASM 和 Clusterware 的安装程序交互过程后启动。

组合产品的安装被称为 Oracle Grid Infrastructure。然而，Oracle Clusterware 和 Oracle Automatic Storage Management 仍然是独立的产品。

> **另参阅：**《Oracle Database Guide for Linux》获取有关如何安装 Oracle Grid Infrastructure 的信息

### Oracle Automatic Storage Management 和 Oracle Cluster Files

通过 Oracle Grid Infrastructure 11g release 2 (11.2)，Oracle Automatic Storage Management (ASM) 和 Oracle Clusterware 被安装在单个目录中，称为 Grid Infrastructure 目录。配置向导在配置 Oracle ASM 和 Clusterware 的安装程序交互过程后启动。



组合产品的安装被称为 Oracle Grid Infrastructure。然而，Oracle Clusterware 和 Oracle Automatic Storage Management 仍然是独立的产品。

> **另参阅：**《Oracle Database Guide for Linux》获取有关如何安装 Oracle Grid Infrastructure 的信息

### Oracle Automatic Storage Management 和 Oracle Cluster Files

通过 Oracle Grid Infrastructure 11g release 2 (11.2)，Oracle Automatic Storage Management (ASM) 和 Oracle Clusterware 被安装在单个目录中，称为 Grid Infrastructure 目录。配置向导在配置 Oracle ASM 和 Clusterware 的安装程序交互过程后启动。

### Oracle Automatic Storage Management Cluster File System (ACFS)

Oracle Automatic Storage Management Cluster File System (ACFS) 是一种新的多平台、可扩展的文件系统和存储管理设计，扩展了 Automatic Storage Management (ASM) 技术以支持所有应用程序数据。ACFS 提供动态文件系统大小调整，并通过在所有可用磁盘上的分布、平衡和条带技术提高性能，并通过镜像和校验保护提供存储可靠性。

### Oracle ASM Role Separation with SYSASM

在 Oracle ASM 11g release 1 (11.1) 中引入的 `SYSASM` 权限与 `SYSDBA` 权限完全分离。如果您选择包含此可选功能，指定不同的操作系统作为 `OSASM` 和 `OSDBA` 组，则 `SYSASM` 管理权限仅对 `OSASM` 组的成员可用。`SYSASM` 权限还可以在 Oracle ASM 实例上通过密码身份验证授予。

您可以将 `OPERATOR` 权限（`SYSASM` 权限的子集，包括启动和停止 Oracle ASM）指定给 ASM 组 `OSOPER` 的成员。

使用 `SYSASM` 而非 `SYSDBA` 权限为存储层提供系统可以在 Oracle ASM 管理和数据库管理之间提供了更清晰的职责划分，防止使用相同存储的不同数据库意外覆盖彼此的文件。

> **另参阅：**《Oracle Automatic Storage Management Administrator's Guide》

### Cluster Time Synchronization Service

集群节点应保持同步。在此版本中，Oracle Cluster 提供了 Cluster Time Synchronization Service (`CTSS`)，确保集群中存在同步服务。如果在配置期间未找到网络时间协议 (`NTP`)，则配置 `CTSS` 以确保时间同步。

### Enterprise Manager Database Cluster Provisioning

Enterprise Manager Database Control 11 提供了在新节点上自动配置 Oracle Grid Infrastructure 和 Oracle RAC 安装的能力，然后将现有的 Oracle Grid Infrastructure 和 Oracle RAC 数据库扩展到这些配置的节点。此配置程序在可以使用此功能之前需要成功安装 Oracle RAC。

### Fixup Scripts and Grid Infrastructure Checks

在 Oracle 11g release 2 (11.2) 中，Oracle Universal Installer (`OUI`) 会检测安装最低要求是否未完成，并创建名为修复脚本（fixed scripts）的脚本程序来解决许多不完整的系统配置要求。如果 `OUI` 检测到标记为“可修复”的任务未完成，则您可以

点击修复并再次检查（Fix & Check Again）按钮生成修复脚本，轻松修复问题。

修复脚本在安装期间生成。系统提示您在单独的终端会话中以 root 身份运行脚本。运行脚本时，它会在必要将内核值提高到所需的最低值，并完成其他系统配置任务。

您也可以在安装前让集群验证实用（`CVU`）生成修复脚本。

## 网格即插用 (Grid Plug and Play)

在过去，在集群中添加或删除服务器需要大量的准备准备工作。在此版本中，您可以继续手动配置服务器节点，或使用网格即插用在节点添加到或从集群时动态对其进行配置。

网格即插用通过在集群内启动网格命名服务，允许每个节点动态执行以下任务，从而降低安装、配置和管理服务器节点的成本：

- 为自身协商适当的网络标识

- 获取运行配置方案所需的额外信息

- 使用配置文件数据对自身进行配置或重新配置，使主机名和地址在网络上解析

由于服务器动态执行这些任务，因此添加或删除节点所需的步骤减少到了最。

## 改进的输入/输出隔离进程

Oracle Clusterware 11g release 2 (11.2) 用集群同步服务守护进程 Agent 和 Monitor 替换了 `oprod` 和 `Hangcheck` 进程，以提供对挂起的更准确识别并避免虚假终止。

## 智能平台管理接口 (IPMI) 集成

智能平台管理接口 (`IPMI`) 是一种行业标准管理协议，包含在许多服务器中。`IPMI` 独立于操作系统运行，即使系统未通电也可以运行。带有 `IPMI` 的服务器包含主板管理控制器 (`BMC`)，用于与服务器通信。

如果配置了 `IPMI`，当需要节点隔离且服务器无响应时，Oracle Clusterware 将使用 `IPMI`。

## Oracle Clusterware 离线升级 (Out-of-place Upgrade)

在此版本中，您可以将新版本的 Oracle Clusterware 安装到现有 Oracle Cluster 安装的单独家 中。此功能减少了升级集群中节点的停机时间。执行离线升级时，软件的新旧版本同时存在于节点上，位于不同的位置，但只有一个软件版本处于激活状态。

## 使用 Oracle Enterprise Manager 进行 Oracle Clusterware 管理

在此版本中，您可以使用 Oracle Enterprise Manager 集群主页对独立数据库和 Oracle RAC 环境执行全面的管理和监控支持，使用高可用应用程序和 Oracle 集群资源管理。

当 Oracle Enterprise Manager 与 Oracle Clusterware 安装时，它可以提供一组在 Oracle Enterprise Manager 中拥有 Oracle Clusterware 管理员角色的用户，并为高可用应用程序和 Oracle Clusterware 资源管理提供全面的管理和监控支持。在配置并部署 Oracle Enterprise Manager 后，您可以使用 Oracle Enterprise Manager 配置添加到集群的额外节点。

## 用于简化客户端访问的 SCAN

在此版本中，单客户端访问名称 (`SCAN`) 是为所有连接到集群的客户端提供的主机名。`SCAN` 注册到至少一个多多三个 IP 地址，位于域名服务 (`DNS`) 或网格命名服务 (`GNS`) 中。`SCAN` 消除了在集群添加或删除节点时更改客户端的需要。客户端还可以使用 `EZCONNECT` 访问集群。

## 用于补丁的 SRVCTL 命令增强

在此版本中，您可以使用服务器控制工具 `SRVCTL` 关闭运行在 Oracle home 内的所有 Oracle 软件，或用于补丁。Oracle 基础设施补丁在所有节点上自动执行，并以多节点、多补丁的方式应用补丁。

## 典型安装选项

为了简化集群安装，特别是对于那些初次接触集群的客户，Oracle 引入了典型安装路径。典型安装尽可能将许多选项设置为默认值以遵循这些推荐的最佳实践。

## 投票磁盘备份程序更改

在先前的版本中，使用 `dd` 命令备份投票磁盘是一项强制的安装后任务。从 Oracle Clusterware release 11.2 及更高版本开始，不支持使用 `dd` 命令备份和恢复投票磁盘。

不再需要手动备份投票磁盘，因为投票磁盘会在 OCR 中或在发生任何配置更改时自动备份。投票磁盘数据会自动恢复到任何添加的投票磁盘中。

**另请参阅：** Oracle Clusterware 管理与部署指南

## Release 1 (11.1) 新功能



这是 `release 1 (11.1)` 的新功能列表。

## 安装文档中的更改

随着 Oracle Database `1g release 1` 的发布，Oracle Cluster 可以作为独立产品安装或配置，并提供有关存储管理的额外文档。对于安装规划，请注意以下文档：

## Oracle Database 2 天 + 实时应用集群

此书提供了安装和配置双节点 Oracle Clusterware 和 RAC 环境程序的概述和示例。

## Oracle Clusterware 安装指南

本书（您正在阅读的指南）提供了将 Clusterware 作为独立产品安装，或与 Oracle Database 或 Oracle RAC 一起安装 Clusterware 的程序。它包含了需要管理员权限的系统配置说明。

## Oracle Application Clusters 安装指南

这本特定平台的书籍提供了位于安装 Oracle Clusterware 后安装 Oracle RAC 的程序。它包含了供数据库管理员使用的数据库配置说明。

## Oracle Database 存储管理员指南

本书为管理和维护存储或配置 Oracle 存储管理 (`ASM`) 的数据库和存储管理员提供信息。

## Oracle Clusterware 管理与部署指南

这是 Oracle Clusterware 的管理员参考。它包含了有关管理任务的信息，包括涉及操作系统配置更改和复制 Clusterware 的。

## Oracle Real Application Clusters 管理与部署指南

这是 Oracle RAC 的管理员参考。它包含了有关管理任务的信息。这些任务包括数据库集群、节点添加和删除、Oracle 集群注册表 (`OCR`) 管理、使用 SRL 和其他数据库管理工具以及对操作系统配置的调整。

## Release 1 (11.1) 安装增强和新功能

以下是 Oracle Database `11g release (11.1)` 的增强和新功能：

### 用于 Oracle ASM 管理的 SYSASM 权限和 OSASM 操作系统组

此功能引入了一个新的 `SYSASM` 权限，专门用于执行 Oracle ASM 管理任务。使用 `SYSASM` 权限代替 `SYDSBA` 在 Oracle ASM 和数据库管理之间提供了更清晰的职责划分。

`OSASM` 是专门用于 Oracle ASM 的操作系统组。`OSASM` 组成员可以使用操作系统身份验证以 `SYSASM` 身份连接并访问 Oracle ASM。

### Oracle 预安装 RPM（之前的 Oracle Valid RPM）

预安装 RPM 可以安装在使用 Red Hat Enterprise Linux 或 Oracle Linux 操作系统的服务器上。它可以从不可破坏 Linux 网络 (`ULN`) 获取。此 RPM 完成安装 Clusterware 所需的预配置任务，包括设置内核参数和添加所需的内核 RPM。它还为安装 Oracle RAC 做好准备。要在不可破坏 Linux 网络上注册您的服务器或获取更多信息，请参阅以下 URL：

```
https://linux.oracle.com
```

# 1 集群 Oracle Grid Infrastructure 的典型安装

本章描述了集群 Oracle Grid Infrastructure 的“典型（Typical）”安装与“高级（Advanced）”安装的区别，并描述了完成典型安装所需的步骤。

本章包含以下章节：

- 典型安装和高级安装
- 使用典型安装完成的预安装步骤
- 需要手动执行的预安装步骤

## 1.1 典型安装和高级安装

Oracle Grid Infrastructure 安装有两种安装选项：

- **典型安装（Typical Installation）：** 典型安装选项是一种简化的安装方式，具有最少的人动配置选择。Oracle 建议您在大多数集群实现中选择此类安装。
- **高级安装（Advanced Installation）：** 高级安装选项是一个高级操作程序，需要较高程度的系统知识。它允许您选择特定的配置选项，包括额外的存储和网络选择、使用操作系统组身份验证进行基于角色的管理权限、与 IPMI 集成，或在指定 Oracle 自动存储管理（ASM）角色时具有更细粒度的控制。

## 1.2 使用典型安装完成的预安装步骤

在 Oracle Clusterware `11g Release 2 (11.2)` 中，安装期间 Oracle Universal 安装程序 (`OUI`) 会生成脚本（`runifup.sh`），您可以运行这些脚本来完成预安装步骤。

安装期间会生成修复脚本（Fixup scripts）。系统会在会在单独的终端会话中以 root 身份运行脚本。运行脚本时，它们将完成配置任务：

- 如果必要，将安装和运行所需的内核参数设置为至少最小值。
- 如果必要，为安装所有者的 Oracle Inventory 目录和操作系统权限组重新配置主组和次组成员关系。

## 需要手动执行的预安装步骤

- 如果必要，将 shell 限制设置为所需值。

## 1.3 需要手动执行的预安装步骤

完成以下手动配置任务：

- 验证系统需求
- 检查网络需求
- 检查操作系统软件包
- 创建组和用户
- 检查存储
- 为 Oracle 自动存储管理准备存储
- 安装 Oracle Grid Infrastructure 软件

如果您需要任何关于完成这些任务的信息，请参见第 2 章“集群 Oracle Grid Infrastructure 预安装任务”和第 3 章“为集群 Oracle Grid Infrastructure 和 Oracle RAC 配置存储”。

### 1.3.1 验证系统需求

输入以下命令检查可用内存：

```
grep MemTotal /proc/meminfo
grep SwapTotal /proc/meminfo
```

确保交换空间（swap space）大于或等于下表所示安装所需的最小尺寸：

| 表 1-1 64 位 Linux 和 System z 上的 Linux 所需交换空间 |

| 可用 RAM | 所需交换空间 |

| :--- | :--- |

| 2 GB 到 32 GB 之间 | 等于 RAM 大 |

| 大于 32 GB | 32 GB RAM |

如果交换空间和 Grid home 位于同一个文件系统，请将各自的需求相加所需的最小空间。

```
df -h
```

此命令检查文件系统上的可用空间。如果您对 Oracle Cluster 文件使用普通冗余（即三个 OCR 位置和三个投票磁盘位置），则保留用于 Oracle Grid Infrastructure 文件的共享存储卷应至少有 2 GB 的可用文件空间。

> 注意：您无法在原始分区（raw partitions）上安装 OCR 或投票磁盘文件（Oracle Cluster 文件）。您只能安装在 Oracle ASM 或支持的存储选项上。原始设备的唯一用途是作为 Oracle ASM 磁盘。

如果您计划安装在 Oracle ASM，为了确保 Oracle ASM 上 OCR 或投票磁盘文件的高可用性，您需要在三个单独的故障组中为 Oracle Cluster 提供至少 2 GB，并至少有三个物理磁盘。每个磁盘的容量至少为 1 GB，以确保有足够的空间创建集群文件。

确保为集群 Oracle Grid Infrastructure （Grid home）留出至少 6.5 GB 的空间。这包括 Oracle Clusterware 和 Oracle 自动存储管理 (Oracle ASM) 的文件和日志文件。

```
df -h
```

确保每个节点 至少有 2 GB 的可用空间。

> 注意：对于无法在子网的情况，请参见 2.6 节“检查硬件需求”以获取更多信息。

### 1.3.2 检查网络需求

确保您拥有以下内容：

- 集群的单一访问名称 (`SCAN`)
- IP 地址需求
- 网络使用

#### 1.3.2.1 集群的单一访问名称 (SCAN)

在安装期间，系统会提示您用于集群的单一访问名称 (`SCAN`)，它是连接到集群内节点的。默认情况下，`SCAN` 的名称如下，例如：

```
NE-Sa9
```

如果您需要超过 15 个字符的 `SCAN`，请注意集群名称默认为前 15 个字符。

#### 1.3.2.2 IP 地址需求

在启动安装之前，每个节点必须至少配置两个接口：一个私有 IP 地址，一个公有 IP 地址。

##### 1.3.2.2.1 手动配置的 IP 地址需求

如果您未启用 `GNS`，则每个节点的公有和虚拟 IP 地址必须是静态 IP 地址，在安装前配置但未使用。公有和虚拟 IP 地址必须位于同一子网。

Oracle Cluster 管理您在安装期间识别为私有的子网上的 IP。

集群必须配置以下地址：

- 每个节点的地址，具有以下特征：
  - 静态 IP 地址
  - 在安装前配置，并在安装前可解析到该节点
  - 与所有 IP 地址、`VIP` 和 `SCAN` 地址位于同一子网



- 每个节点的虚拟 IP 地址，具有以下特征：

  - 静态 IP 地址
  - 在安装前配置但未使用
  - 与所有公有 IP 地址、VIP 和 SCAN 地址位于同一子网

- 集群的单一访问名称 (`SCAN`)，具有以下特征：

  - 安装前已在域名服务器 (`DNS`) 上配置了三个静态 IP 地址，这三个地址与提供的 `SCAN` 名称关联，且 `DNS` 向请求者随机返回这三个地址
  - 安装前在 `DNS` 中配置以解析到未使用的地址
  - 给出的名称不以数字开头
  - 与所有 IP 地址、VIP 和 `SCAN` 地址位于同一子网
  - 符合 `RFC 952` 标准，该标准允许字母和连字符（`-`），但不允许下划线（`_`）。

- 每个节点的私有 IP 地址，具有以下特征：

  - 静态 IP 地址
  - 安装前配置，但在独立的私有网络上，具有自己的子网，且除集群成员节点外无法解析

## 1.3.2.3 冗余互连的使用

在之前的版本中，为了利用冗余网络进行互连，需要使用绑定（bonding）、汇聚（trunking）或类似的技术。`Oracle Grid Infrastructure` 和 `Oracle RAC` 可以在不使用其他网络技术的情况下，利用冗余互连网络，以增强集群的优化通信。此功能从 `Oracle Database 11g Release 2 (11.2.0.2)` 开始可用。

冗余互连的使用（`Redundant Interconnect Usage`）实现了多个（最多4个）私有网络（也称为互连）之间的负载均衡和高可用性。

## 1.3.2.4 网络接口的预期用途

在安装期间，系统会要求您识别 `OUI` 检测到的每个网络接口的用途，即公共接口、私有接口或“不使用”（`do not use`）。对于您计划用于其他用途的接口——例如专用网络文件系统的接口——您必须将这些实例标识为“不使用”，以便 `Oracle Clusterware` 忽略它们。

冗余互连的使用无法保护用于公共通信的接口。如果您需要为公共接口提供高可用或负载均衡，请使用第三方解决方案。通常可以使用绑定、汇聚或类似技术来实现此目的。

您可以通过选择多个接口作为私有接口来为私网络启用冗余互连的使用。当您识别出多个接口作为私有接口时，冗余互连将创建一个冗余互连。此功能从 `Oracle Grid Infrastructure 11g Release 2 (11.2.0.2)` 开始可用。

## 1.3.3 检查操作系统软件包

请参考第 2.8 节“识别软件需求”中列出的表格获取您的操作系统所需的包列表，或参考第 2.1 节“关于安装 Linux 操作系统”描述的系统配置脚本（如 `Oracle Preinstallation RPM`）。

## 1.3.4 创建组和用户

输入以下命令创建默认组和用户：

一个用于所有系统验证管理权限的系统权限组，包括 `Oracle RAC`（如果已安装）：

```bash
# groupadd -g 1000 oinstall
# groupadd -g 1031 dba
# useradd -u 1101 -g oracle -G dba oracle
# mkdir -p /u01/app/11.2.0/grid
# mkdir -p /u01/app/oracle
# chown -r oracle:oracle:/u01
# chmod 775 /u01/
```

此命令集创建一个单一安装所有者，具有所需的系统权限以授予 `Oracle` 库存目录权限（仅限安装），并授予 `OSASM/SYSASM` 和 `OSDBA/SYSDB` 权限。它为 `Oracle Grid Infrastructure` 和 `Oracle RAC` 创建了 `Oracle` 基础 `/u01/app/oracle`。它创建了 `Grid` 家（`Oracle Grid Infrastructure` 二进制文件存储的位置）`/u01/app/11.2.0/grid`。

## 1.3.5 检查存储

您必须在 `Oracle ASM` 上留出空间用于 `Oracle` 集群文件（投票磁盘和集群注册表），以及 `Oracle` 数据库文件（如果您安装了独立实例或 `Oracle Real Application Clusters Databases`）。新安装不再支持在块或原始设备上创建 `Oracle Clusterware`。

> 注意：当使用 `Oracle ASM` 管理 `Oracle` 集群文件或 `Oracle` 数据库文件时，无论数据库数量多少，`Oracle` 在每个节点上创建一个 `Oracle ASM` 实例。

## 1.3.6 为 Oracle Automatic Management 准备存储

安装 `Linux ASMLIB RPM` 以简化存储管理。`ASMLIB` 提供了供 `Oracle ASM` 使用的持久权限和存储设备，消除了更新 `udev` 或 `devlabel` 文件以包含存储路径和权限的需求。

如果您无法安装 `ASMLIB RPM`，或选择手动配置存储设备，请复阅第 3 章中的相关章节。

> 另：如果您需要详细的存储配置信息，或需要更多关于 `ASMLIB` 的信息，请查看第 3 章“为集群和 `Oracle RAC` 的 `Oracle Grid Infrastructure` 配置存储”。

`ASMLIB 2.0` 以一组三个 `Linux` 软件包的形式提供：

- `oracleasmlib-2.0` - `Oracle ASM` 库
- `oracleasm-support-2.0` - 管理 `ASMLIB` 所需的实用程序
- `oracleasm` - 用于 `Oracle ASMLIB` 库的内核模块

每个发行版都有自己的一套 `ASMLIB 2.0` 软件包，且在每个发行版中，每个内核都有一个包含 `oracleasm` 软件包的版本。

### 1.3.6.1 使用 ULN 自动安装 ASMLIB

如果您已注册 `Oracle Linux Network (ULN)`，可以自动下载并安装 `ASMLIB`。

1. 以 `root` 身份登录。
2. 运行以下命令：

```bash
# oracleasm install oracleasmlib-$(uname -r)
```

### 1.3.6.2 手动安装 ASMLIB

如果您不是 `ULN` 成员，或选择手动配置存储设备，请复阅第 3 章中的相关章节。

1. 以 `root` 身份登录并运行以下命令确定您正在使用的内核：

```bash
# uname -r
```

2. 使用 `URL` 打开浏览器：`http://www.oracle.com/technet/server/linux/index.html`
3. 下载 `oracleasm` 和 `oracleasm-support` 软件包。
4. 下载与您的内核对应的 `oracleasm` 软件包。
5. 以 `root` 身份登录并安装以下。

### 1.3.6.3 配置 ASMLIB

安装内核后，以 `root` 身份登录并输入以下命令：

```bash
# oracleasm configure -i
```

按照系统提示提供信息。如果不带 `-i` 标志输入 `oracleasm` 命令，将显示当前配置。

### 1.3.6.4 标记 ASM 候选分区

为了让 `OUI` 识别候选分区，您必须以 `root` 身份登录并标记磁盘。要标记供 `ASM` 使用，输入以下语法，`ASM_DISK_NAME` 是 `ASM` 组名称，`candidate_disk` 是您要分配给该组的磁盘名称：

```bash
# oracleasm createdisk ASM_DISK_NAME candidate_disk
```

例如：

```bash
# oracleasm createdisk datal /dev/sdf
```

## 1.3.7 安装 Grid Infrastructure 软件

1. 从安装媒体根目录启动 `OUI`：`./runInstaller`
2. 选择安装并配置集群 `Grid Infrastructure`，然后选择典型安装。在随后的安装屏幕中，根据提示输入配置信息。

如果收到无法通过脚本修复的安装验证错误，请查看第 2 章“集群预安装任务”以找到配置节点的章节。修复后，继续安装直到完成。

# 关于安装 Linux 操作系统

本节提供了有关安装支持的 `Linux` 发行版的信息。它包含以下主题：

- 完成最小化 `Linux` 安装
- 完成默认 `Linux` 安装
- 关于 `Oracle Linux` 和不可破坏的企业级内核 (`Unbreakable Enterprise Kernel`)
- 关于 `Oracle` 预安装 `RPM` 和 `Oracle` 验证 `RPM`
- 在 `ULN` 支持下安装 `Oracle` 预安装 `RPM` 或 `Oracle` 验证 `RPM`
- 从 `DVD` 或镜像安装 `Oracle` 预安装 `RPM`
- 使用 `Ksplice` 进行零停机更新

## 2.1.1 完成最小化 Linux 安装



要完成最小化安装，请选择其中一个最小化安装选项（在自定义安装中从“软件包组选择”中选择“最小化（Minimal）”选项，或者取消选择除基础包（Base pack）以外的所有包）。此项安装会标记用于数据库安装的 RPM，因此您必须使用适用于您的 Oracle Linux 版本的 RPM 程序包来安装所需的包。您使用的包取决于您的 Linux 版本以及您在不可破坏 Linux 网络 (`ULN`) 的支持状态。

> 注意：Oracle 预安装 RPM 安装了 `X11` 客户端库，但不安装 Windows 系统服务器包。要使用如 `OUI`、配置助手和 Oracle Enterprise Manager 等图形界面，请将显示设置为带有 X Window 服务器包的系统。

参考以下 URL 获取有关安装精简包集的文档：

`https://support.oracle.com/CSP/main/article?cmd=show&type=NOT&id=728346.1`

> 注意：如果您不是不可破坏 Linux 网络或 Red Hat 支持网络的成员，且您是 Oracle 支持客户，则可以下载指令来配置一个脚本，该脚本记录了安装精简包的说明：

`https://support.oracle.com/CSP/main/article?cmd=show&type=NOTid=579101.1`

您也可以搜索“Linux reduced set of packages”来查找相关指令。

安装 Oracle Grid Infrastructure 需要 `SSH`。`OpenSSH` 应该包含在 Linux 发行版的最小化安装中。要确认是否安装了 SSH 包，请输入以下命令：

```
# rpm -qa | grep ssh
```

如果您没有看到 SSH 包列表，请为您的 Linux 发行版安装这些包。

注意：Oracle 预安装 RPM 安装了 `X11` 客户端库，但不安装 X Window 系统服务器包。要使用如 `OUI`、配置助手和 Oracle Enterprise Manager 等图形界面，请将显示设置为带有 X Window 系统服务器包的系统。

## 2.1.2 完成默认 Linux 安装

如果您没有安装 Oracle 预安装 RPM，Oracle 建议您使用默认软件包（RPMs）安装 Linux 操作系统。此安装包含了大多数必需的包，并有助于限制对包依赖关系的手动验证。Oracle 建议在安装期间不要对 RPM 进行自定义。

要获取有关默认安装的信息，请登录 Oracle Support：

```
https://support.oracle.com
```

搜索“default rpms linux installation”，并查找您的 Linux 发行版。例如：

```
https://support.oracle.com/CSP/main/article?cmd=show&type=NOT&id=401167.1
```

安装完成后，请检查您的发行版的系统要求，以确保您已安装了所有所需的包，并完成您的发行版和系统配置所需的所有其他任务。

## 2.1.3 关于 Oracle Linux 和不可破坏的企业级内核 (Unbreakable Enterprise Kernel)

Oracle 的不可破坏内核 (Unbreakable Kernel) 为在数据中心运行 Red Enterprise Linux (RHEL) 5 或 Oracle Linux 5 的客户提供来自上游开发的最新创新。从 Oracle Linux 5 Update 6 开始，默认包含并启用不可破坏的企业级内核。

不可破坏的企业级内核基于最近的稳定主线 Linux 内，并包含了与 Oracle Database、Oracle 中间件和 Oracle 工程团队合作开发的优化，以确保最严苛的企业工作负载的稳定性和性能。

Oracle 高度建议在您的 Linux 环境部署不可破坏的企业级内核，特别是如果您运行企业级应用程序。但是，使用 Oracle 不可破坏的企业级内核是可选。如果您需要严格的 RHEL 内核兼容性，Oracle Linux 也包含与 RHEL 内核兼容的内核，内核直接从 RHEL 源代码编译。

您可以在以下处获取更多关于 Linux 不可破坏的企业级内核的信息：

```
http://www.oracle.com/us/technologies/linux
```

Linux 不可破坏的企业级内核是 Oracle 产品使用的标准内核。Oracle Database 以及其他 Oracle 产品的构建和 QA 系统专门使用 Linux 不可破坏的企业级内核。Linux 不可破坏的企业级内核也是 Oracle Exadata 和 Oracle Exagic 系统使用的内核。在 Oracle 参与的所有 Linux 基准测试中，以及用于 x86-64 的 Oracle 预安装 RPM 中，都使用了 Linux 不可破坏内核。

# 关于安装 Linux 操作系统

`Ksplice` 是 Oracle Linux 的一部分，可以在 Linux 操作系统 (OS) 运行时更新内核，无需重启或任何中断。`Ksplice` 仅适用于 Oracle Linux。

## 2.1.4 关于 Oracle 预安装 RPM 和 Oracle 验证 RPM

如果您的 Linux 发行版是 Oracle Linux 且您是 Oracle Linux 客户，可以使用适用于您版本的 Oracle 预安装 RPM 或 Oracle 验证 RPM 完成大多数预安装配置任务，这些包可以通过 Oracle Linux 网络获取，或在 Oracle Linux DVD 上提供。使用 Oracle 预安装 RPM 并非强制要求，但 Oracle 建议您使用它来节省设置集群服务器的时间。

安装后，Oracle 预安装 RPM 或 Oracle 验证 RPM 会执行以下操作：

- 下载并安装安装 Oracle Grid Infrastructure 需要的所有额外包
- 创建 `oracle` 用户以及 `oinstall` 和 `dba` 组
- 设置 `sysctl.conf` 设置
- 设置硬限制
- 设置内核参数

要成为 Oracle Linux 客户，请联系您的销售代表，或从 Oracle 商店购买许可：

`https://shop.oracle.com/product/linux`

要在不可破坏 Linux 上注册您的服务器，或查找更多信息，请参考：

`https://linux.oracle.com`

如果您使用的是 Oracle Linux 4.7 及更高版本，或 Oracle Linux 5.2 及更高版本，媒体中包含了预安装 RPM。

注意：Oracle 预安装 RPM 安装了 `X11` 客户端库，但不安装 X Window 系统服务器包。要使用如 `OUI`、配置助手和 Oracle Enterprise Manager 等图形界面，请将显示设置为带有 X Window 系统服务器包的系统。

> 注意：Oracle 预安装 RPM 安装了 `X11` 客户端库，但不安装 Windows 系统服务器包。要使用如 `OUI`、配置助手和 Oracle Enterprise Manager 等图形界面，请将显示设置为带有 X Window 服务器包的系统。

此外，用户和组将使用可用 ID 创建。如果在运行预安装 RPM 的集群节点上 ID 不相同，可能会不同的组和用户 ID 会安装失败。

为了避免此问题，请以软件所有者的身份运行命令。如果所有节点的组或用户 ID 不一致，请根据需要进行更改以确保它们一致。

## 2.1.5 在 ULN 支持下安装 Oracle 预安装 RPM 或 Oracle 验证 RPM

使用以下步骤订阅不可破坏 Linux 网络 (`ULN`) Linux 通道，并添加分发适用于您的版本的 Oracle 预安装 RPM 或 Oracle 验证 RPM 的 Oracle 通道：

1. 在不可破坏网络 (`ULN`) 注册您的服务器。默认情况下，您已注册适用于您的操作系统和硬件的 Oracle Linux 最新 通道。
2. 登录不可破坏 Linux 网络：

`https://linux.oracle.com`
3. 点击 Systems 标签，并在 Systems Profiles 列表中选择已注册的服务器。System Details 窗口显示服务器的订阅。
4. Manage Subscriptions。打开 System Summary。
5. 从 Available Channels 列表中根据您的 Linux 发行版选择 Oracle 安装媒体副本和更新补丁通道。例如，如果您的发行版是 x86-64 的 Oracle Linux 5 Update 6，请选择以下：

- Oracle Linux 5 Update 6 media copy (x86_64)
- Oracle Linux 5 Update 6 Patch (x86_64)
6. 点击 Subscribe。
7. 启动终端并根据您的平台以 root 身份输入以下命令。

Oracle Linux 6:



# `yum install oracle-rdms-server-11gR2-preinstall`

Oracle Linux 5 或 Oracle Linux 4:

# `yum install oracle-rdms-server-11gR2-preinstall`

## `yum install oracle-validated`

你应该能看到输出指示你已经订阅了 Oracle Linux 频道，并且软件包已安装。例如：

```
elin5_u6_i386_base
elin5_u6_x86_64_patch
```

Oracle Linux 会自动创建标准的（非角色分配的）Oracle 安装所有者和组，并为 Oracle 安装设置其他内核配置设置。

- 8. 在集群中的所有其他服务器上重复步骤 1 到 8。

> 注意：检查 RPM 日志文件以查看系统配置更改。例如：

Oracle Linux 6:

`/var/log/oracle-rdms-server-11g82-preinstall/results/orakernel.log`

Oracle Linux 5 和 Oracle Linux 4:

`/var/log/oracle-validated/results/orakernel.log`

## 2.1.6 从 DVD 或镜像安装 Oracle 预安装 RPM

使用此程序从 Oracle Linux 发行版安装 Oracle 预安装 RPM：

- 1. 通过 Oracle Store 订购 Oracle Linux 介质包，或从 Oracle Software Delivery Cloud 网站下载 Oracle Linux 和 Oracle VM 的磁盘镜像。

Oracle Store：

```
https://shop.oracle.com
```

Oracle Software Delivery Cloud 网站：

```
http://edelivery.oracle.com/linux
```

- 2. 启动 Oracle Linux 安装。

- 3. 检查第一个软件选择，该列表列出了特定任务的软件选项。在屏幕顶部，有一个“现在自定义”或“以后自定义”的选项。选择 `Customize now`，并点击 `Next`。

- 4. 在配置页左侧选择 `Base System`，然后在屏幕右侧选择 `System Tools`。点击 `Optional Packages`。

打开 System Tools 窗口。

- 5. 从软件包列表中选择 Oracle Preinstallation RPM 软件包复框，并点击 `Next`。

- 6. 完成其他屏幕以完成 Oracle Linux。

Oracle Linux 会自动创建标准的（非角色分配的）Oracle 安装所有者和组，并为 Oracle 安装设置其他内核配置设置。

在所有集群成员节点上重复步骤 2 到 6。

## 2.1.7 使用 Ksplice 执行零停机更新

Ksplice Uptract 提供 Linux 安全和错误修复更新，其重新封装的格式允许这些更新在不重启内核的情况下应用。

要使用 Ksplice Uptract：

- 从 Unbreakable Linux Network 获取或验证你的 Oracle Linux 高级订阅：

```
https://linux.oracle.com
```

- 以 root 身份登录。

- 确保你想要使用 Ksplice 的服务器可以访问互联网。如果你正在使用代理服务器，请在 shell 中设置代理服务器和端口值，使用类似于以下命令：

```
# export http_proxy=http://proxy.example.com:port
# export https_proxy=http://proxy.example.com:port
```

- 下载 Ksplice Uptract 仓库 RPM 软件包：

```
https://www.kspline.com/yum/uptract/ol/ksplice-uptract-release.noarch.rpm
```

- 运行以下命令：

```
rpm -i ksplice-uptract-release.noarch.rpm
yum install uptract
```

- 使用文本编辑器打开 `/etc/uptract/uptract.conf`，编辑你的高级访问密钥并保存文件。你必须对所有系统使用相同的访问密钥。

- 运行以下命令对内核执行零停机更新：

```
uptract-upgrade -y
```

另请：

- Ksplice Uptract 网站获取更多信息：

```
http://www.kspline.com
```

- 用于 Oracle Linux 的 Oracle Ksplice：

```
http://oss.oracle.com/ksplice/docs/ksplice-quickstart.pdf
```

## 2.2 查看升级最佳实践

> 注意：在启动任何配置更改之前，务必为现有数据库创建备份。

如果你有现有 Oracle 安装，请检查版本号、补丁和其他配置信息，并查看你现有安装的 Oracle 升级程序。在继续安装之前查看 Oracle 文档，以决定你想如何进行。

高级安装 集群 Oracle Grid Infrastructure 预安装任务 2-7

你可以通过对单个节点或集群中的节点进行滚动升级，在不关闭 RAC 数据库的情况下升级 Oracle Automatic Storage Management (Oracle ASM) 11g release 1 (11.1)。然而，如果你在使用 Oracle ASM 的集群上有单机数据库，则必须在升级之前关闭单机数据库。如果你是从 Oracle ASM 10g 升级，则必须关闭整个 ASM 集群以执行升级。

如果你有现有 ASM 安装，请查看 Oracle 升级文档。ASM home 的位置在此版本中发生了变化，你可能希望考虑其他配置更改，以简化或自定义存储管理。如果你有上一个版本的现有 ASM home，则它应该由你计划用于升级 Oracle Clusterware 的相同用户使用。

在操作系统的滚动升级期间，当两个版本的操作系统都通过你正在使用的 Oracle 数据库认证时，可以使用不同的操作系统二进制文件，

> 注意：使用混合操作系统版本仅在升级期间（持续几小时）获得支持。Oracle Clusterware 不支持在同一集群中拥有具有不同指令集架构 (ISA) 处理器的节点。

## 2.3 安装修复脚本

OUI 在检测到未满足要求时会创建名为 `fix.sh` 的修复脚本。如果 OUI 检测到任务未完成，它会生成修复脚本。

修复脚本执行以下操作：

- 设置成功安装所需的内核参数。

- 共享内存参数。

- 文件描述符和 UDP 接收参数。

- 设置 Oracle 目录的权限。

- 重新配置主要和辅助组成关系。

- 必要时设置 shell 限制。

如果你在集群节点之间配置了用户的 SSH，你可以在安装之前检查配置。要执行此操作，以执行安装的用户身份登录，导航到 fix 命令所在的区域，并使用以下命令语法，其中 `node` 是你想作为集群成员节点逗号分隔列表：

```
$ fix.sh stage -preinst -n node
```

例如，如果你打算配置一个具有 `node1` 和 `node2` 的双节点集群，输入以下命令：

```
$ fix.sh stage -preinst -n node1,node2
```

## 2.4 使用 X 登录到远程系统

在安装期间，你需要以 root 或或其他用户的身份在远程终端执行任务。为想要启用远程显示的用户账户完成以下程序。

> 注意：如果你以其他用户（例如 `oracle`）登录，请对该用户重复此程序。

要启用远程显示，请完成以下程序之一：

- 如果你从 X 工作站或 X 终端安装软件，

- 1. 启动本地终端会话，例如 X 终端 (`xterm`)。

- 2. 如果你在另一个系统上安装软件且该系统作为 X 显示器，使用以下语法输入命令，以允许远程主机在本地服务器上显示 X ：

```
# ssh + RemoteHost
```

- 3. 如果你不在本地系统上安装软件，使用 `ssh` 命令连接到要安装软件的系统：

## 为 Oracle Grid Infrastructure 创建组、用户和路径

```
# ssh -Y RemoteHost
其中 RemoteHost 是完全限定远程主机名。-Y 标志 ("yes") 允许远程 X11 客户端对原始 X11 显示器具有完全访问权限。
```

例如：

```
# ssh -Y somehost.example.com
```

- 4. 如果你不是以 root 用户登录的，请输入以下命令将用户切换为 root：

```bash
$ su - root
password:
#
```

- * 如果你正从安装了 X server 软件的 PC 或或其他系统安装软件，那么：



> 注意：必要时，请参阅你的 X Window System 文档以获取有关完成此过程的更多信息。根据你所使用的 X 软件，你可能需要以不同的顺序完成任务。

1. 启动 X Window System 软件。
2. 配置 X Window System 软件的安全设置，以允许远程主机在本地系统上显示 X 应用程序。
3. 连接到你想要安装软件的远程系统，以 Oracle Grid Infrastructure 客户端软件所有者（`grid`, `oracle`）的身份登录，并在系统中启动终端会话；例如，一个终端（`xterm`）。
4. 在远程系统上打开另一个终端，并以 `root` 用户身份登录远程系统，以便你可以在提示时以 `root` 身份运行脚本。

## 2.5 为 Oracle Grid Infrastructure 创建组、用户和路径

以 `root` 登录，并使用以下指令查找或创建 Oracle Grid Infrastructure 的 Oracle Inventory 组和软件所有者。

- 确定 Oracle Inventory 和 Oracle Inventory 组是否存在
- 如果不存在 Oracle Inventory，则创建 Oracle Inventory 组
- 创建 Oracle Infrastructure 用户
- 创建 Oracle Base 目录路径
- 创建作业角色分离的操作系统权限组和用户
- 创建标准组、用户和路径的示例
- 创建角色分配组、用户和路径的示例

> 注意：在安装 Oracle Grid Infrastructure 期间，会安装 Oracle Clusterware 和 Oracle 自动存储管理（Oracle ASM）。你不再可以拥有单独的 Oracle Cluster 安装所有者和 Oracle ASM 安装所有者。

### 2.5.1 确定 Oracle Inventory 和 组是否存在

当你首次在系统上安装 Oracle 软件时，OUI 会创建 `orainst.loc` 文件。该文件标识了 Inventory 组的名称（默认是 `oinstall`）以及 Oracle 中央清单（Central Inventory）的路径。`orainst.loc` 文件的内容类似于：

```
inventory_loc=central_inventory_location
inst_group=oinstall
```

在前面的示例中，`central_inventory_location` 是 Oracle 中央清单的位置，而 `group` 是具有向中央清单写入权限的组名（OINSTALL 权限）。

如果你已有一个现有的 Oracle 中央清单，请确保在所有 Oracle 软件安装中都使用相同的 Oracle Inventory，并确保你打算用于安装的所有 Oracle 用户都具有写入该目录的权限。

要确定你的系统上是否存在 Oracle 中央清单目录 (`oraInventory`)：

输入以下命令：

```bash
# more /etc/orainst.loc
```

如果 `orainst.loc` 文件存在，该命令的输出与以下类似：

```
inventory_loc=/u01/app/oracle/oraInventory
inst_group=oinstall
```

在之前的输出示例中：

- `inventory_loc` 组显示了 Oracle Inventory 的位置。
- `inst_group` 参数显示了 Oracle Inventory 组的名称（在此示例中为 `oinstall`）。

使用命令 `grep groupname /etc/group` 来确认指定的组是否存在于系统上。例如：

```bash
$ grep oinstall /etc/group
oinstall:x:1000:grid,oracle
```

### 2.5.2 如果不存在 Oracle Inventory，则创建 Oracle Inventory 组

如果 `orainst.loc` 文件不存在，通过输入类似的命令来创建 Oracle Inventory 组：

```bash
# /usr/bin/groupadd -g 1000 oinstall
```

上述命令创建了清单组 `oinstall`，其组 ID 为 `1000`。Inventory 组的成员被授予向 Oracle 中央清单 (`oraInventory`) 的权限。

默认情况下，如果不存在 Inventory 组，安装程序会将 Oracle Grid Infrastructure for Cluster 软件安装所有者的主组列为 oraInventory 组。确保该组可以作为所有用户的主组。

> 注意：组 ID 和用户 ID 在集群中的所有节点上必须一致。检查并确保你要使用的组 ID 和用户 ID 在每个集群成员节点上可用，并确认每个 Oracle Grid Infrastructure for a Cluster 安装所有者的主组具有相同的名称和组 ID。

### 2.5.3 创建 Oracle Grid Infrastructure 用户

在以下情况下，你必须为 Oracle Grid Infrastructure 创建软件所有者：

- 如果 Oracle 软件所有者用户不存在；例如，如果这是首次安装；
- 如果 Oracle 软件所有者用户存在，但你想使用不同的操作系统、不同的组设置。



- 如果 Oracle 软件所有者用户不存在；例如，如果这是首次安装；

- 如果 Oracle 软件所有者用户存在，但你想使用不同的操作系统、不同的组设置。

- `-u` 选项指定用户 ID。使用此命令标记是可选的，因为你可以允许系统为你提供自动生成的用户 ID。但是，你必须记住为 Oracle Grid Infrastructure 创建的用户 ID，因为你在预安装期间需要使用它，并且你必须在集群的所有节点上为该用户拥有相同的用户 ID。

- `-g` 选项指定主组，该主组必须是 Oracle Inventory 组。例如：`oinstall`

- `-g` 选项指定辅助组，辅助组必须包含 OSASM 组，该组成员被授予 SYSASM 权限以管理 Oracle ASM 系统，这与数据库管理员组分开；或者你可以指定一个组同时用于 OSASM 和 OSDBA 组，以便该组成员被授予 SYSASM 和 SYSDBA 权限，从而授予管理 ASM 实例和 Oracle 数据库实例的系统权限。在代码示例中，此组为 `asmadmin`

如果你同时创建 Oracle Grid Infrastructure 和 Oracle 数据库，则此用户必须拥有 OSDBA 作为辅助组。在此示例中，组名为 `asmdba`。它是被授予访问 Oracle ASM 存储权限的成员。如果你计划让多个数据库访问 Oracle ASM 存储，则你必须创建一个 OSDBA ASM 组，或者为所有数据库和 ASM 的 OSDBA 组使用同一个组。

使用 `usermod` 命令更改现有的用户 ID 和组。

例如：

```
# id oracle
uid=501(oracle) gid=501(oracle) groups=501(oracle)
# /usr/sbin/usermod -u 1001 -g 1000 -G 1000,1001 oracle
# id oracle
uid=1001(oracle) gid=1000(oinstall) groups=1000(oinstall),1001(oracle)
```

- 2. 为将拥有 Oracle Grid Infrastructure 的用户设置密码。例如：

```
# passwd grid
```

- 3. 在集群的所有节点上重复此过程。

> 注意：如有必要，在使用或修改现有用户之前，请联系你的系统管理员。Oracle 建议不要在每个节点上使用默认的 UID 和 GID，因为组和用户 ID 在每个节点上可能不同。相反，请提供通用的分配组和用户 ID，并在创建或修改组之前确认它们已用于任何节点上。

## 2.5.4 创建 Oracle Base 路径

Grid 安装所有者的基目录是存储诊断日志、管理日志以及与 Oracle ASM 和 Oracle Clusterware 相关其他日志的位置。

### 为 Oracle Grid Infrastructure 创建组、用户和路径

如果你已经创建了符合 Oracle 最佳灵活架构 (OFA) 指南的 Oracle Clusterhome 路径，则你不需要创建 Oracle base 目录。OUI 会找到一个符合 OFA 的路径，并在该路径下创建 Oracle base 目录。

为了让 OUI 识别该路径为 Oracle 软件路径，它必须采用 `[u0-99]/app` 的形式，并且对库存库所有者 (`oinstall`) 的任何成员可写。Oracle base 的 OFA 路径为 `/u01/app/user`，其中 `user` 是软件安装所有者的名称。

如果你为集群和数据库软件所有者准备了独立的 Grid Infrastructure，Oracle 建议你手动创建 Oracle Grid Infrastructure home 和 Oracle base homes，以便你保存日志文件。

```
# mkdir -p /u01/app/11.2.0/grid
# mkdir -p /u01/app/grid
# mkdir -p /u01/app/oracle
# chown grid:install /u01/app/11.2.0/grid
# chown grid:install /u01/app/grid
# chown oracle:install /u01/app/oracle
# chmod -R 775 /u01/
# chown -R oinstall /u01
```

> 注意：不支持将集群的 Oracle Grid Infrastructure 二进制文件放在共享的 OCF2 集群系统上。

> 如果你计划在共享的 OCF2 位置安装 Oracle RAC home，则你必须将 OCF2 升级到 1.4.1 版本，该版本支持可写 mmaps。

## 2.5.5 创建角色分离的操作系统

### 2.5.5 创建角色分离的操作系统组

Oracle 建议你至少使用两个组：一个成员被授予管理权限的系统权限组，以及一个用于限制用户访问的安装所有者组（即 orinventory）。

### 为 Oracle Grid Infrastructure 创建组、用户和路径

Oracle 建议你至少使用两个组：一个成员被授予管理权限的系统权限组，以及一个用于限制用户访问的安装所有者组（即 orinventory）。在 Oracle 工具（如集群验证实用程序）中，如果你选择一个组来写入 orinventory，那么该组名应该是 `oinstall`。

### 创建角色分离的组和用户的概述

- 创建具有角色分离的数据库组和用户

> 注意：如需使用目录服务（如网络信息服务 NIS），请参阅你的操作系统文档以获取更多信息。

## 2.5.5.1 创建角色分离的组和用户的概述

本节提供了如何创建用于角色分离的用户和组的概述。以 `root` 身份登录以创建这些组。

- 用于具有角色分离的 Oracle 安装的用户

- 用于角色分离安装的数据库组

- 用于角色分离安装的 Oracle ASM 组

### 2.5.5.1 用于具有角色分离的 Oracle 安装的用户

Oracle 建议在创建独立软件安装的情况下，创建以下操作系统组和用户。

为每个 Oracle 软件产品创建一个软件所有者（通常情况下，数据库软件所有者使用 `oracle`，Oracle Grid Infrastructure 使用 `grid`）。

当你首次在系统上安装 Oracle 软件时，必须创建一个至少软件所有者。该用户拥有 Oracle Grid Infrastructure 的二进制文件，你也可以让该用户成为 Oracle 数据库或 Oracle RAC 二进制文件的所有者。

Oracle 软件所有者必须将 Oracle Inventory 组作为主组，以便 Oracle 软件安装所有者可以写入库存 (`orinventory`)，并确保 OCR 和 Oracle 资源权限正确。数据库软件所有者还必须 OSDBA 和（如果你创建了）OSOPER 组作为辅助组。在 Oracle 文档中，当 Oracle 所有者用户互相指代时，被称为 `oracle` 用户。

在 Oracle 文档中，创建 Oracle Grid Infrastructure 二进制文件的用户称为 `grid` 用户。该用户同时拥有 Oracle Clusterware 和 Oracle 自动存储的二进制文件。

有关 OSDBA、OSASM 和 OSOPER 组以及 SYDBA、SYASASM 和 SYOSOPER 权限的更多信息，请参阅《Oracle Clusterware 管理和部署指南》和《Oracle 管理员指南》。

# 为 Oracle Grid Infrastructure 创建组、用户和路径

## 2.5.5.1.2 用于任务角色分离安装的数据库组

如果您正在安装 Oracle Database，则需要以下操作系统组和用户：

- OSDB 组（通常为 `dba`）

在您首次在系统上安装 Oracle Database 软件时，必须创建此组。此组用于标识具有数据库管理权限（SYSDBA 权限）的操作系统帐户。如果您没有为 Oracle ASM 实例分离 OSDB、OSOPER 和 OSAM 组，则具有 SYSOPER 和 SYSASM 权限的操作系统帐户必须是此组的成员。代码示例中使用的名称为 `dba`。如果您没有指定单独的组作为 OSAM 组，则您定义的 OSDB 组默认也是 OSAM 组。

要指定一个除默认 `dba` 组以外的组名，您必须选择“高级”安装类型来安装软件，或者作为该组的成员的用户启动 Oracle Universal 安装程序 (`OUI`)。在这种情况下，OUI 会提示您指定组的名称。

OSDB 组的成员曾被授予 Oracle ASM 实例 SYSASM 权限，包括挂载和卸载磁盘。在 Oracle Grid Infrastructure 12 版本中，如果指定了不同的操作系统组作为 OSDB 和 OSAM 组，则该权限将被移除。如果同时使用同一个组作为 OSDB 和 OSASM，则该权限将被保留。

- 用于 Oracle Database 的 OSOPER 组（通常为 `oper`）



这是一个可选组。如果您想创建一个独立的操作系统用户组，并赋予一组有限的数据库管理权限（`SYSOPER` 权限），请创建此组。默认情况下，`OSDB` 组的成员也拥有由 `SYSOPER` 权限授予的权限。

要使用 `OSOPER` 创建一个权限比默认 `dba` 组更少的数据库组，您必须选择“高级”安装类型来安装软件，或者作为非 `dba` 组成员的用户启动 `OUI`。在这种情况下，`OUI` 会提示您指定组的名称。该组的常用名称为 `oper`。

## 2.5.5.1.3 用于任务角色分离的 ASM 组

`SYSASM` 是一个新的系统组，允许将 Oracle 存储管理与 `SYSDBA` 分离。在 Oracle 自动存储管理 12 版本 (`11.2`) 中，除非指定的 `OSAM` 组与指定的 `OSDB` 组是同一个组，否则 `OSDB` 组的成员不会被授予 `SYSASM` 权限。

选择操作系统组作为 Oracle ASM 的操作系统身份验证组。在启动 `OUI` 之前，为 Oracle ASM 创建以下组和用户：

- 自动存储管理组（通常为 `asmadmin`）

这是一个必需的组。如果您希望为 Oracle ASM 和 Oracle Database 员拥有独立的管理权限组，请将此组作为一个独立的组创建。在 Oracle 文档中，授予权限的成员所在的操作系统组被称为 `OS` 组；在代码示例中，如果专门创建了一个组来授予此权限，则将其称为 `asmadmin`。

如果您的系统上有有多个数据库，并使用多个 `OSDB` 组，以便为每个数据库提供单独的 `SYSDBA` 权限，那么您应该单独创建一个 `OSASM` 组，并使用一个与数据库用户不同的用户来拥有 Oracle Grid Infrastructure 安装程序（Oracle Clusterware 和 Oracle ASM）。Oracle ASM 可以支持多个数据库。

`OSASM` 组的成员可以使用 SQL 通过操作系统身份验证以 `SYSASM` 身份连接到 Oracle ASM 实例。`SYSASM` 权限允许挂载和卸载组以及其他管理任务。`SYSASM` 权限对 RDBMS 数据库没有访问权限。

- 数据库管理员组（ASM 的 `OSDBA`，通常为 `asdba`）

`ASM` 数据库管理员组 (`OSDBA` for `ASM`) 的成员被授予对 `ASM` 管理的文件读写权限。Oracle Grid Infrastructure 所有者所有 Oracle Database 软件所有者必须能够访问 Oracle `ASM` 管理的文件，且所有在数据库具有 `OSDBA` 身份的用户必须是 `ASM OSDBA` 组的成员。

- `ASM` 操作员组成员（`ASM` 的 `OSOPER`，通常为 `asoper`）

这是一个可选组。如果您想创建一个独立的系统用户组，以拥有有限的 Oracle `ASM` 存储管理权限（`ASM` 的 `SYOPER` 权限），启动和停止 Oracle `ASM`，请创建此组。默认情况下，`OSASM` 组的成员也拥有由 `ASM SYOPER` 权限授予的所有权限。

要使用 Oracle `ASM` 操作员组创建一个权限比默认管理员更少的 Oracle `ASM` 管理员组，您必须选择“高级”安装类型来安装软件。在这种情况下，`OUI` 会提示您指定组的名称。例如，此组为 `asoper`。

## 2.5.5.2 创建具有角色分离的数据库组和用户

以下章节描述了如何创建所需的操作系统用户和组：

- 创建 `OSDBA` 组以准备数据库安装
- 创建用于数据库安装的 `OSOPER` 组
- 创建 `OSASM` 组
- 创建 `ASM` 的 `OSOPER` 组
- 创建用于数据库访问 Oracle `ASM` 的 `ASM OSDBA` 组
- 创建 Oracle 软件所有者用户
- Determine是否存在 Oracle 软件所有者用户
- 创建 Oracle 软件所有者用户
- 修改现有 Oracle 软件所有者用户
- 在其他集群节点上创建相同的数据库用户和组

## 2.5.5.1 创建 OSDBA 组以准备数据库安装

如果您打算安装 Oracle Database 并配合 Oracle Grid Infrastructure 安装使用，则在以下情况下必须创建 `OSDBA` 组：

- 不存在 `OSDBA` 组；例如，如果这是首次安装 Oracle Database
- 存在 `OSDBA` 组，但您想为新安装授予不同的操作系统用户组管理权限

如果不存在 `OSDBA` 组或您需要一个新的 `OSDBA` 组，请按以下方式创建。除非已存在同名的组，否则使用组名 `daba`：

```bash
groupadd -g 1031 dba
```

## 2.5.5.2 创建用于数据库安装的 OSOPER 组

只有当您想标识一组具有操作员权限的系统用户时，才创建 `OSOPER` 组。对于大多数安装，仅创建 `OSDBA` 组即可。要使用 `OSOPER` 组，必须在以下情况下创建它：

- 不存在 `OSOPER` 组；例如，如果这是首次安装 Oracle Database
- 存在 `OSOPER` 组，但您想为新安装授予不同的操作系统用户组操作权限

如果您需要一个新的 `OSOPER` 组，请按以下方式创建。除非已存在同名的组，否则使用组名 `oper`：

```bash
groupadd -g 1032 oper
```

## 2.5.5.3 创建 OSAM 组

如果不存在 `OSAM` 组或您需要一个新的 `OSAM` 组，请按以下方式创建。除非已存在同名的组，否则使用组名 `asmdmin`：

```bash
groupadd -g 1020 asmdmin
```

## 2.5.5.4 创建 ASM 的 OSOPER 组

如果您想标识一组操作系统用户（例如数据库管理员），他们希望获得有限的 Oracle `ASM` 存储管理权限（包括启动和关闭 `ASM` 存储的能力），请创建 `ASM` 的 `OSOPER` 组。对于大多数安装，仅创建 `OSAM` 组即可，并在安装期间将该组作为 `ASM` 的 `OSOPER` 组提供。

如果您需要新的 `ASM OSOPER` 组，请按以下方式创建。除非已存在同名的组，否则使用组名 `asmoper`：

```bash
groupadd -g 1022 asmoper
```

## 2.5.5.5 创建用于数据库访问 Oracle ASM 的 ASM OSDBA 组

您必须创建 `ASM OSDBA` 组以提供对 Oracle `ASM` 实例的访问。如果 `OSDBA` 和 `OSASM` 是不同的组，则这是必要的。

如果不存在 `ASM OSDBA` 组或您需要新的 `ASM OSDBA` 组，请按以下方式创建。除非已存在同名的组，否则使用组名 `asmdba`：

```bash
groupadd -g 1021 asmdba
```

# 为 Oracle Grid Infrastructure 创建组、用户和路径

- 如果存在 Oracle 软件所有者用户，但您希望使用不同的操作系统以及具有不同的组成员关系，以便在新的 Oracle Database 安装中为这些组提供数据库管理权限。
- 如果您已经为 Oracle Grid Infrastructure 创建了 Oracle 软件所有者（例如 `grid`），并且您想为 Oracle Database 创建一个独立的 Oracle 软件所有者（例如 `*oracle*`）。

## 2.5.5.2.7 确定 Oracle 软件所有者用户是否存在

要确定是否存在名为 `*oracle*` 或 `*grid*` 的 Oracle 软件所有者用户，请输入与下例类似的命令（在本例中，确定 `*oracle 是否存在*`）：

```bash
# id oracle
```

如果用户存在，此命令的输出将类似于：

`uid=501(oracle) gid=501(install) groups=502(dba),503(oper)`

确定您是想使用现有用户还是创建另一个用户。要使用现有用户，请确保该用户的主组是 Oracle Inventory 组和 `OSOPER` 组。请参阅以下章节以获取更多信息：

- 若要修改现有用户，请参阅第 2.5.5.2.9 节“修改现有软件所有者用户”。
- 若要创建用户，请参阅第 2.5.5.2.8 节“创建 Oracle 软件所有者”。

> 注意：必要时，在使用或修改现有用户之前，请联系您的系统管理员。Oracle 建议不要在每个节点上使用默认的 UID 和 GID，因为每个节点上的组和用户 ID 可能不同。相反，请提供通用的分配组和用户 ID，并在创建或修改组和用户之前确认它们已用于任何节点。

## 2.5.5.2.8 创建 Oracle 软件所有者

如果 Oracle 软件所有者用户不存在，或者您需要一个新的 Oracle 软件所有者用户，请按照以下步骤创建。使用用户名 `*oracle*` 创建符合您需求的用户：

- 1. 创建 `oracle` 用户，请输入与下例类似的命令：

```bash
# /usr/bin/useradd -u 1101 -g install -G dba,asmdba oracle
```

在先述命令中：

- `-u` 选项指定您提供的 ID。使用此标志位是可选的，您可以允许系统为您提供自动生成的用户 ID 号。但是，您必须记录 `oracle` 用户 ID 号，因为在稍后的预安装期间需要它。



- `-g` 选项指定主组，该主组必须是 Oracle Inventory 组——例如 `install`

- `-G` 选项指定辅助组，这些组必须包含 OSDBA 组、ASM 的 OSDBA 组，如果需要，还包括 ASM 的 OSOPER 组。例如：`dba`, `asmdba` 或 `dba`, `asmdba`, `asmoper`

### 2. 设置 oracle 用户的密码：

```bash
# passwd oracle
```

## 2.5.5.2.9 修改现有 Oracle 软件所有者用户

如果 `oracle` 用户存在，但其主组不是 `install`，或者它不是相应的 OSDBA 或 ASM OSDBA 组的成员，请输入与下例类似的命令进行修改。使用 `-g` 选项指定主组，并使用 `-G` 选项指定任何辅助组：

```bash
# /usr/sbin/usermod -g install -G dba,asmdb oracle
```

在集群中的所有其他节点上重复此过程。

## 2.5.5.2.10 在其他集群节点上创建数据库用户和组

Oracle 软件用户以及 Oracle Inventory、OSDBA 和 OPER 必须在所有集群节点上存在且一致。要创建这些相同的用户和组，您必须识别在创建它们的节点上分配的用户 ID 和组 ID，然后在其他节点上创建具有相同名称和 ID 的用户和组。

> 注意：只有在使用本地用户和组时，必须执行以下过程。如果您使用 NIS 定义的用户和组，则它们在每个节点上已经是一致的。

### 识别现有用户组 ID

要确定 `grid` 或 `oracle` 用户的用户 ID (`uid`) 以及现有 Oracle 组的组 ID (`gid`)，请遵循以下步骤：

- 1. 输入与下例类似的命令（在本例中，确定 `oracle` 用户的用户 ID）：

```bash
# id oracle
```

此命令的输出类似于：

`uid=502(oracle) gid=501(install) groups=502(dba),503(oper),506(asmdb)`

- 2. 从输出中识别该用户所属组的用户 ID (`uid`) 和组 ID (`gids`)。确保这些 ID 在集群的每个节点上都是一致的。用户的主组位于 `gid` 之后。辅助组位于 `groups` 之后。

### 在其他集群节点上创建用户和组

要在其他集群节点上创建用户和组，请在每个节点上重复过程：

- 1. 以 `root` 身份登录集群节点。

- 2. 输入下例类似的命令创建 `installall`、`asadmin` 和 `asmdb` 组，如果需要，创建 `asoper`、`dba` 和 `oper` 组。使用 `-g` 选项为每个组指定正确的组 ID。

```bash
# /usr/sbin/groupadd -g 1000 installall
# /usr/sbin/groupadd -g 1020 asadmin
# /usr/sbin/groupadd -g 1021 asmdb
# /usr/sbin/groupadd -g 1022 asmoper
# /usr/sbin/groupadd -g 1031 dba
# /usr/sbin/groupadd -g 1032 oper
```

**注意：** 如果组已存在，必要时请使用 `groupmod` 命令进行修改。如果无法在此节点上使用相同的组 ID，请查看所有节点上的 `/etc/group` 文件以识别每个节点上可用的组 ID。您必须将所有节点的组 ID 更改为相同。

- 要创建 `oracle` 或 Grid Infrastructure (`grid`) 用户，输入与下例类似的命令（在本例中，创建 `oracle` 用户）：

```bash
# /usr/sbin/useradd -u 1011 -G oinstall asmdba oracle
```

在上述命令中：

- `-u` 选项指定用户 ID，该 ID 必须是之前节识别的。

- `-g` 选项指定主组，必须是 Oracle Inventory 组，例如 `oinstall`。

- `-G` 选项指定辅助组，可以包括 OSDBA、ASM OSDBA 和 ASM OSOPER 组。例如：

- `grid` 安装者：`asmadmin`，其成员被授予 SYSASM 权限。

- 不具备 SYSASM 权限的 Oracle Database Owner：OSDBA (`dba`)、ASM OSDBA (`asmoper`)。

> 注意：如果用户已存在，必要时请使用 `usermod` 命令进行修改。如果无法为每个节点使用相同的用户 ID，请查看所有节点上的 `/etc/passwd` 文件以识别每个节点上可用的用户 ID。您必须为所有节点指定该 ID。

- 设置用户密码。例如：

```bash
# passwd oracle
```

- 按照“配置 Grid Infrastructure 软件用户”节所述完成每个用户的用户环境任务。

## 2.5.6 创建标准组、用户和路径示例

以下是创建 Oracle Inventory 组 (`oinstall`) 以及单组 (`dba`) 作为 OSDBA、ASM OSDBA 组的示例。此外，它展示了如何创建 Grid Infrastructure 软件所有者 (`grid`) 以及具有正确组关系的 Oracle Database 所有者 (`oracle`)。此示例还展示了如何配置符合 OFA 标准且权限正确的 Oracle 路径：

```bash
# groupadd -g 1000 install
# groupadd -g 1031 dba
# useradd -u 1100 -g install -G dba grid
# useradd -u 1101 -g install -G dba oracle
# mkdir -p /u01/app/11.2.0/grid
# mkdir -p /u01/app/grid
# chown grid:installall /u01
# mkdir /u01/app/oracle
# chown oracle:installall /u01/app/oracle
# chmod 775 /u01
```

运行这些命令后，您可能拥有以下组：

- Oracle 中央库存组，或 orainventory 组 (`installall`)。以中央库存组为主组的成员被授予 INSTALLALL 权限写入 oraInventory 目录。

- 单个系统权限组，用作 OSASM、OSDBA、ASM OSDB 和 OPER（对应组 `dba`），被授予 SYSASM 和 SYSOPER 权限以管理 Oracle Clusterware、Oracle ASM 和 Oracle Database 的成员被授予 SYSASM 和 SYSOPER 权限访问 Oracle ASM 存储。

- 集群所有者 (`grid`) 的 Oracle grid 安装，以 orainventory 组为主组，OSASM 组为辅助组，其 Oracle 目录为 `/u01/app/grid`。

- Oracle Database (`oracle`) 以 orainventory 组为主组，OSDBA 组为辅助组，其 Oracle 目录为 `/u01/app/oracle`。

- `/u01` 属于 `grid:install`，在安装前由 `root` 运行 `root.sh` 脚本。此权限允许 OI 创建 Oracle Inventory 目录，路径为 `/u01/app/oraInventory`。

- `/u01` 属于 `grid:install`，在安装前由 `root` 运行 `root.sh` 脚本。

- `/u01/11.2.0/grid` 属于 `grid:install`，权限为 775。这些权限是安装所需的，并在安装过程中会更改。

- `/u01` 属于 `grid:install`，在安装前权限为 775，安装后权限更改为 755。

- `/u01/app/oracle` 属于 `oracle:installall`，权限为 775。

## 2.5.7 创建角色分配组、用户和路径示例

以下是创建兼容最优灵活架构（OFA）部署的角色分配组和用户的示例：

```bash
# groupadd -g 1000 installall
# groupadd -g 1020 asmadmin
# groupadd -g 1021 asdba
# groupadd -g 1031 dba
# groupadd -g 1042 dba2
# groupadd -g 1022 asommer
# useradd -u 1100 -g install -G asmadmin, asmdba grid
# useradd -u 1101 -g install -G dba oracle
# useradd -u 1102 -g install -G dba2, asmdba oracle
```



```bash
# mkdir -p /u01/app/11.2.0/grid
# mkdir -p /u01/app/grid
# chown -R grid:install /u01
# mkdir -p /u01/app/oracle
# chown oracle:install /u01/app/oracle
# mkdir -p /u01/app/oracle
# chown oracle:install /u01/app/oracle2
# chmod -R 775 /u01
```

运行这些命令后，你将拥有以下组和用户：

- 一个 Oracle 集中库存组，或称为 oracleinventory 组 (`oracleinstall`)，该主组的成员被授予了写入 `oracleInventory` 目录的权限。
- 一个独立的 ASM 组 (`asmadmin`)，其成员被授予 `SYSASM` 权限以管理 Oracle Clusterware 和 Oracle ASM。
- 一个独立的 ASM OSDBA 组 (`asmdba`)，其成员包括 `grid`、`oracle1` 和 `oracle2`并被授予访问 Oracle ASM 的权限。
- 一个独立的 ASM OSOPER 组 (`asmoper`)，其成员拥有有限的 Oracle ASM 管理员权限，包括启动和停止 Oracle ASM 的权限。
- 一个用于集群所有者的 Oracle Grid 安装组 (`grid`)，作为其主组，并将 OSASM (`asmadmin`) 和 ASM OSDBA (`asmdba`) 作为次要组。
- 两个不同数据库的两个独立 OSDB 组 (`dbal` 和 `dba2`)，为每个数据库建立 `SYDBA` 权限。
- 两个 Oracle 数据库所有者 (`oracle1` 和 `oracle2`)，用于划分 Oracle 数据库二进制文件的所有权，并以 `OracleInventory` 组为其主组，以其对应的数据库 OSDB 组 (`dbal` 和 `dba2`) 以及 ASM OSDBA 组 (`asmadmin`) 为次要组。
- 安装前，一个符合 OFA 标准的挂载点 `/u01` 属于 `grid:install`。
- 一个属于 Grid 安装所有者的 Oracle base `/u01/app/oracle` 属于 `grid:install`，初始权限为 775，在安装过程中会更改为 755。
- 一个 Oracle base `/u01/app/oracle2` 属于 `oracle2:install`，权限为 775。
- 一个 Grid home `/u01/app/11.2.0/grid` 属于 `grid:install`，权限为 775 (`drwxrxr-x`)。这些权限是安装必需的，在安装过程中会更改为 `root:install` 权限的 755 (`drwx-xr-x`)。
- `/u01/app/Inventory`。此路径仍然属于 `grid:install`，以便允许其他 Oracle 软件写入程序写入集中库存。

## 2.6 检查硬件要求

检查以下要求：

- 通用服务器要求
- 服务器硬件要求
- 服务器内存要求
- 检查服务器硬件和内存配置

### 2.6.1 通用服务器要求

- 确保服务器以运行级别（run level）3 或运行级别 5 启动。
- 确保服务器运行相同的操作系统二进制文件。Oracle Grid Infrastructure 安装和 Oracle Real Application Clusters (Oracle RAC) 支持在同一集群中使用具有不同硬件的服务器。

### 2.6.2 服务器硬件要求

每个系统必须满足以下最小硬件要求：

- 至少 1024 x 768 的显示分辨率，以便 OUI 正确显示。
- `/tmp` 目录至少有 1 GB 空间。
- Oracle Grid Infrastructure for a Cluster home (Grid home) 需要 6.6 GB 空间，这包括 ClusterClusterware 和 Oracle ASM 文件和日志文件、ACFS 日志文件，以及如果你的平台支持 Cluster Health Monitor 库。
- Grid Infrastructure 所有者的 Oracle base 目录中需要额外的高达 10 GB 空间，用于存储 Trace File Analyst 和 Collector 生成的诊断收集数据。
- 在 Linux x86 平台上，如果你打算安装 Oracle Database，请为 Oracle base 分配 4 GB 空间。
- 对于 Linux x86_64 平台，如果你打算安装 Oracle Database，请为 Oracle base 分配 4.6 GB 的磁盘空间。

> 注意：如果你打算在集群上安装 Oracle Databases 或 Oracle RAC，请注意每个服务器上的 `/dev/shm` 挂载区域的大小必须大于服务器数据库的系统全局区域 (SGA) 和程序全局区域 (PGA)。请数据库管理员审核预期的 SGA 和 PGA 大小，以确保在集群上安装数据库后无需增加 `/dev/shm`。

如果你正在安装 Oracle Database，那么由于你选择配置自动数据库备份，你需要在文件系统或 Oracle Automatic Storage Management 磁盘组中准备额外的空间作为快速恢复区 (Fast Recovery Area)。

另参：Oracle Automatic Storage Management Administrator's Guide

### 2.6.3 服务器内存要求

确保你的系统满足以下要求，取决于你的系统架构：

- 64 位系统和 Linux on System z 内存要求
- 内存要求

高级安装 Oracle Grid Infrastructure for a Cluster 预安装任务 2-25

## 检查硬件要求

**注意：** 在 Linux 上，Hugepages（大页）功能使用内存映射文件通过大页页表分配不可交换的内存。如果你启用了 Hugepages，则在计算交换空间之前，应从 RAM 中减去分配给 HugePages 的内存。

如果你遇到指示交换空间大小不足的 OUI 错误，但你的交换空间符合此处列出的要求，则可以忽略该错误。

#### 2.6.3.1 64 位系统和 Linux on System 内存要求

每个系统必须满足以下条件：

- 安装 Oracle Grid Infrastructure for a Cluster（包括计划安装 RAC 的安装）至少需要 2.5 GB 的 RAM。
- 交换空间等于可用 RAM 的倍数，如下表所示：

表 2-1

| 可用 RAM | 需要的 Swap |
| --- | --- |
| 2.5 GB 到 32 GB 之间 | 等于 RAM 的大小 |
| 大于 16 GB | 16 GB |

#### 2.6.3.2 内存要求

每个系统必须满足以下条件：

- 安装 Oracle Grid Infrastructure for a Cluster（包括计划安装 Oracle 的安装）至少需要 2.5 GB 的 RAM。
- 交换空间等于可用 RAM 的倍数，如下表所示：

表 2-2

| 可用 RAM | 需要的 Swap |
| --- | --- |
| 2.5 GB 到 16 GB 之间 | 等于 RAM 的大小 |
| 大于 16 GB | 16 GB |

### 2.6.4 检查服务器硬件和内存配置

要确保每个系统满足这些要求，请遵循步骤操作：

1. 确定物理 RAM，输入以下命令：

```bash
grep MemTotal /proc/meminfo
```

如果物理 RAM 的大小小于所需大小，则必须在继续之前安装更多内存。

2. 确定已配置交换空间的大小，输入以下命令：

```bash
grep SwapTotal /proc/meminfo
```

如有必要，请参考你的操作系统文档了解如何配置额外的交换空间。

3. 确定 `/tmp` 目录中的可用空间，输入以下命令：

```bash
df -k /tmp
```

此命令以 1 KB 块为单位显示磁盘空间。在大多数系统上，你可以使用带有 -h 标志的命令 (`df -h`) 以“人类可读”格式显示输出，例如 "2G" 和 "10M"。如果 `/tmp` 目录可用磁盘空间小于 1 GB（小于 1048576 个 1-块），请完成以下操作之一：

 删除 `/tmp` 目录中的不必要文件以释放空间。

 扩展包含 `/tmp` 的文件。如有必要，请联系系统管理员获取扩展文件的信息。

4. 确定系统的空闲 RAM 和磁盘空间量，输入以下命令：

```bash
free
```

> 注意：
> - Oracle 建议在确定最终值之前多次获取可用 RAM 和交换空间的值。因为可用 RAM 和交换空间会根据与计算机的交互而变化。
> - 联系你的操作系统供应商获取交换空间分配指南。供应商指南优于本指南中的交换空间要求。



### 5. 确定系统架构是否可以运行该软件，输入以下命令：

```bash
uname -m
```

> 注意：此命令显示处理器类型。如果你打算在 64 位架构上安装，输出应为 `x86_64`。

## 2.7 检查网络要求

检查以下章节以确保你拥有安装 Oracle Grid Infrastructure 集群所需的网络和互联网协议 (`IP`) 地址：

- 网络硬件要求
- `IP` 地址要求
- Oracle Grid Infrastructure 使用网络广播要求
- Oracle Grid Infrastructure 使用网络的多组播要求
- 将域名权限委托给 Grid Naming Service 的 `DNS` 配置
- `IP` 地址配置示例

### 2.7.1 硬件要求

- 命名服务配置选项
- 网络接口配置选项
- 多路互连与企业级 Linux
- 启用命名守护进程（Name Service Daemon）

> 注意：有关 Oracle RAC 支持的互连协议和硬件的最新信息，请参考 Oracle Support 网站上的 `URL`：
> 
> `https://support.oracle.com`

以下是网络配置的节点列表：

- 每个节点必须至少有两个网络适配器或网卡（`NIC`）：一个用于公网接口，一个用于私网接口（互连）。
- 使用冗余互连（Redundant Interconnect Usage）时，集群应识别多个接口，无需使用绑定（bonding）或其他技术。此功能适用于 Oracle Database 11g Release2 (`11.2.0`)。

当定义了多个接口时，Oracle Cluster 会创建高可用 `IP`（`HAIP`）地址。Oracle RAC 和 `ASM` 实例使用这些接口来确保高可用性。

默认情况下，Oracle Grid Infrastructure 软件使用所有私网接口的 `HAIP` 地址进行跨接口的通信负载均衡。如果某个私网接口故障或不可用，Oracle Cluster 将透明地将相应的 `HAIP` 地址移动到剩余的接口之一。

> 注意：如果定义了多个接口作为私网接口，Oracle Cluster 同时仅激活四个接口。然而，如果其中一个活动接口故障，Oracle Cluster 将 `HAIP` 地址切换到定义的私网接口集中的另一个。

当节点升级到 Oracle Grid Infrastructure 11g release2 (`11.2.0`) 或更高版本时，系统使用了现有的网络分类。

若要配置多个公网接口，在安装之前应使用第三方技术来聚合多个公网接口，然后选择单个接口作为公网接口。Oracle Grid Infrastructure 建议在未使用聚合技术的情况下，如果您在集群中配置两个公网接口，节点上的公网接口故障不会导致 `VIP` 自动转移到另一个公网接口。

### 网络要求检查

Oracle 建议使用冗余互连（Redundant Interconnect Usage）来利用多个私网接口。然而，您也可以使用第三方技术来实现私网的冗余。

- 如果 Oracle Cluster 使用 `OUL`，所有节点网络适配器相关的公网接口名称必须相同，网络适配器相关的私网接口名称也应相同。如果您使用复制（cloning）创建新集群或向现有集群添加节点，则不受此限制。

例如：对于双节点集群，您不能将 `node1` 的 `eth0` 配置为公网接口而将 `node2` 的 `eth1` 配置为公网接口。接口名称必须相同，但您必须在相同的网络适配器上配置私网接口。如果 `eth` 是 `node1` 的私网接口，则 `eth0` 应该是 `node2` 的私网接口。

**另参：** 参考《Oracle Clusterware 管理与部署指南》，了解如何使用复制添加节点。

- 对于公网，每个网络适配器必须支持 `TCP/IP`。
- 对于私网，接口必须支持数据传输协议（`UDP`），使用支持 `TCP/IP` 的高速网络适配器和交换机（最低要求千兆网）。

> `UDP` 是 Oracle RAC 的默认互连协议，`TCP` 是 Oracle Clusterware 的互连协议。您必须使用交换机进行互连。Oracle 建议使用专用交换机。

Oracle 不支持互连令牌环或交叉线。

- 每个节点的私网互连必须位于同一子网，这些子网必须连接到集群的每个节点。例如，如果私网接口的子网掩码为 `255.255.255.0`，则您的私网范围是 `192.168.0.0--192.168.0.255`；如果您的私网地址子网掩码为 `255.255.255.0`，则您的私网地址范围可以是 `192.168.0.[0-255)`。
- 对于使用冗余互连的集群，每个私网接口应位于不同的子网。然而，每个集群成员节点必须在每个私网互连子网上都有接口，这些子网必须连接到集群的每个节点。例如，您可以在 `192.168.0` 和 `10.0.0` 子网上拥有私网，但每个集群成员节点都必须拥有连接到这两个子网的接口。
- 对于私网，所有指定的互连接口（interconnect interfaces）的终端点在网络上必须是完全可达的。不应有一个节点连接到所有私网接口。可以使用 `ping` 测试互连是否连通。

## 2.7.2 IP 地址要求

在开始安装之前，您必须在每个节点上至少配置两个接口：一个用于私网 `IP` 地址，一个用于公网 `IP` 地址。

高级安装 集群 Oracle Grid Infrastructure 预安装任务 2-29

您可以使用以下选项之一配置 `IP` 地址：

- 使用 Oracle 命名服务（`GNS`）分配 `IP` 地址。如果选择此选项，将为物理主机分配 `IP` 地址，并动态分配 Oracle Clusterware 管理的 `VIP`。在这种情况下，`VIP` 地址通过 `DHCP` 分配，并使用配置为集群一部分的域名服务器解析。如果您计划使用 `GNS`，则您需要：
  - 在公网上运行 `DHCP` 服务
  - `DHCP` 提供足够的地址以供每个节点提供 1 个 `VIP`，并为集群扫描地址（`SCAN`）提供 3 个 `IP` 地址
- `IP` 地址分配。如果选择此选项，将为集群中的每个物理主机分配固定 `IP` 地址，以及 Oracle Clusterware 管理的 `VIP`。此外，使用基于域名服务器（`DNS`）的静态解析。选择此选项要求您在修改集群时请求网络管理更新。

> 注意：Oracle 建议为服务器主机使用静态名称。

公网地址和虚拟 `IP` 地址必须位于同一子网。

Oracle 仅支持默认网络使用 `DHCP` 分配，不支持后续网络。

### 2.7.2 使用命名服务的 IP 地址要求

如果启用命名服务（`GNS`），则到集群的名称解析将委托给 `GNS`，`GNS` 监听在 `GNS` 虚拟 `IP` 地址上。您需要在安装前的域名服务器（`DNS`）中定义此地址。`DNS` 必须配置为将集群名称请求（委托子域中的任何名称）委托给 `GNS`。当请求到达 `DNS` 时，`GNS` 处理请求并响应请求的地址。

要使用 `GNS`，管理员在安装之前必须建立 `DNS` 查询，将子域的 `DNS` 解析定向到集群。如果您启用了 `GNS`，则在公网上必须有一个 `DHCP` 服务，允许集群根据需要动态分配 `VIP` 地址。

> 注意：以下限制适用于厂商配置：
> - 如果已安装厂商集群，则无法选择使用 `GNS`，因为厂商集群不支持它。
> - `GNS` 不能与另一种多播 `DNS` 同时使用。如果您想使用 `GNS`，请禁用系统上的任何第三方 `mDNS` 守护进程。

### 2.7.2.2 手动配置的 IP 地址要求

如果你没有启用 `GNS`，则每个节点的公共 `IP` 和虚拟 `IP` 地址必须是静态 `IP` 地址，且在安装前为每个节点配置好，但当前未被使用。公共 `IP` 和虚拟 `IP` 地址必须位于相同的子网内。

Oracle Clusterware 会在你在安装向导中识别为私有的接口上管理私有子网中的私有 `IP` 地址。

集群必须配置以下地址：

- 每个节点的公共 `IP` 地址，具有以下特征：
  - 静态 `IP` 地址
  - 在安装前为每个节点配置，且在安装前可解析到该节点
  - 与所有其他公共 `IP` 地址、`VIP` 地址和 `SCAN` 地址位于同一子网内
- 每个节点的虚拟 `IP` 地址（`VIP`），具有以下特征：
  - 静态 `IP` 地址
  - 在安装前为每个节点配置，但当前未被使用
  - 与所有其他公共 `IP` 地址、`VIP` 地址和 `SCAN` 地址位于同一子网内
- 集群的单一客户端访问名称 (`SCAN`)，具有以下特征：
  - 在安装前在域名服务器 (`DNS`) 上配置三个静态 `IP` 地址，以便这三个 `IP` 地址与提供的 `SCAN` 名称关联，并且 `DNS` 以随机顺序向请求者返回所有三个地址
  - 在安装前在 `DNS` 中配置，以解析当前未使用的地址
  - 给出的名称不以数字开头
  - 与所有其他公共 `IP` 地址、`VIP` 地址和 `SCAN` 地址位于同一子网内
  - 符合 `RFC 952` 标准，该标准允许字母、数字和连字符（“–”），但不允许下划线（“_”）
- 每个节点的私有 `IP` 地址，具有以下特征：
  - 静态 `IP` 地址
  - 在安装前配置，但在独立的私有网络上，拥有自己的子网，且该子网无法被其他集群成员节点解析



SCAN 是用于为集群提供服务访问的名称。由于 SCAN 与整个集群关联而非特定节点，因此 SCAN 可以在无需重新配置客户端的情况下从集群中添加或删除节点。它还为数据库增加了位置无关性，使得客户端配置不必依赖于运行特定数据库的节点。客户端可以继续以以前版本相同的方式访问集群，但 Oracle 建议访问集群的客户端使用 SCAN。

注意：在典型（Typical）安装中，SCAN 提供的名称也是集群名称，因此 SCAN 名称必须满足集群名称的要求。在高级（Advanced）安装中，SCAN 和集群名称在安装期间在单独字段中输入，因此集群名称的要求适用于 SCAN 名称。

你可以使用 `nlookup` 命令来确认 DNS 是否正确与地址关联。例如：

```
root@node$ nlookup mycluster-scan
Server: dns.example.com
Address: 192.0.2.101
Name: mycluster-scan.example.com
Address: 192.0.2.202
Name: mycluster-scan.example.com
Address: 192.0.2.203
```

安装后，当客户端向集群发送请求时，Oracle Clusterware 监听器会将客户端请求重定向到集群中的服务器。

注意：Oracle 强烈建议你不要在 hosts 文件中配置 VIP 地址。请对 SCAN 使用 DNS 解析。如果你使用 hosts 文件解析 SCAN，你将只能解析到一个 IP 地址，并且只有一个 SCAN 地址。在 DNS 或 hosts 文件中配置 SCAN 是唯一支持的配置。不支持在网络信息服务 (NIS) 中配置 SCAN。另参阅：附录 D，“理解网络地址”

## 2.7.3 Oracle Grid Infrastructure 使用网络的广播要求

广播通信（ARP 和 UDP）必须在 Oracle Grid Infrastructure release 2 patchset 1 (2.1.0.2) 及更高版本使用的所有公共和私有接口上正常工作。广播必须跨越公共或私有接口使用的任何配置 VLAN 正常工作。

## 2.7.4 Oracle Grid Infrastructure 使用网络的多播要求

在 Oracle Grid Infrastructure release 2 (2.1) 中，每个集群成员节点守护进程在所有接口上均使用多播与集群中的其他节点通信。在 Oracle Grid Infrastructure release 2 patchset 1 (2.1.0.2) 及更高版本中，私有互连需要多播。出于这一原因，你至少必须为集群启用多播：

- 跨越为私有互连定义的广播域
- 在 IP 地址子网范围 `224.0.0.0/24` 和 `239.0.0.1/24` 上

你不需要跨越路由器进行多播通信。

## 2.7.5 用于向 Grid 命名服务进行委托的 DNS 配置

如果你计划使用 DNS 安装 Oracle Grid Infrastructure，你必须配置你的域名服务器 (DNS)，向集群成员节点子域发送 GNS 请求。以下是执行区域委托需要完成的操作概述。你的实际操作可能与此示例有所不同。

配置 DNS 使用委托发送 GNS 请求：

- 在 DNS 中为 GNS 虚拟 IP 地址创建一个条目，其中地址使用 `CLUSTERNAME.DOMAINNAME`。例如，如果集群名称为 `mycluster`，域名为 `example.com`，IP 地址为 `192.0.2.1`，则创建一个类似下面的条目：

```
mycluster-gns.example.com A 192.0.2.1
```

你提供的地址必须是路由的。

- 设置 GNS 子域到 GNS 虚拟 IP 地址的转发，以便 GNS 指向该虚拟 IP。为此，请在 DNS 中创建如下配置（假设使用 NS1）：

```
mycluster-gns.example.com NS ns1.example.com
```

- 在 DNS 中配置的 NS 记录解析当前未使用的地址：

```
ns1.example.com A 192.0.2.1
```

- 当使用 GNS 时，必须在 `/etc/resolv.conf` 中配置如下内容：

```
search example.com
nameserver mycluster-gns.example.com
```

注意：在使用 GNS 时，请注意使用 NIS 可能会产生问题。

## 2.7.6 Grid 命名服务配置示例

如果你使用 GNS，则需要将 GNS 虚拟 IP 委托到该静态 IP 地址。

当节点添加到集群时，GNS 服务器可以动态提供这些地址。由于 GNS 自动分配和配置地址，无需进一步配置。以下示例提供了关于 GNS 的信息，集群名称为 `mycluster`，域名为 `example.com`，子域为 `example.com`，`192.0.2` 代表公共 IP 地址，`192.168.0` 代表私有 IP 子网：

### 表 2-3 Grid 命名服务示例

| 身份 | 主机名 | 给定名称 | 类型 | 地址 | 地址分配方式 | 解析 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| GNS VIP | 无 | 由集群选择 | mycluster-gns.example.com | 虚拟 | 192.0.2.1 | 网络管理员固定 | DNS |

| 节点 1 公共 | 节点 1 | node1 | 公共 | 192.0.2.101 | 固定 | GNS |

| 节点 1 VIP | 节点 1 | 由集群选择 | node-vip | 虚拟 | 192.0.2.104 | DHCP | GNS |

| 节点 1 私有 | 节点 1 | node1-priv | 私有 | 192.168.0.1 | 固定或 DHCP | GNS |

| 节点 2 公共 | 节点 2 | node2 | 公共 | 192.0.2.102 | 固定 | GNS |

| 节点 2 VIP | 节点 2 | 由集群选择 | node2-vip | 虚拟 | 192.0.2.105 | DHCP | GNS |

| 节点 2 私有 | 节点 2 | node2-priv | 私有 | 192.168.0.2 | 固定或 DHCP | GNS |

| SCAN VIP 1 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.201 | DHCP | GNS |

| SCAN VIP 2 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.202 | DHCP | GNS |

| SCAN VIP 3 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.203 | DHCP | GNS |

## 2.7.7 手动 IP 地址配置示例

如果您选择不使用 GNS，在安装之前必须配置公有、虚拟和私有 IP 地址。此外，请检查可以通过 `ping` 命令访问默认网关。要找到默认网关，请使用操作系统实用程序中描述 `route` 命令。

例如，在一个双节点集群中，每个节点都有一个公网接口和一个私有接口，并且您定义了一个 SCAN 域地址以供您的 DNS 解析到三个地址之一，您的接口配置可能如下表所示：

| 表格 2-4 手动网络配置示例 |

| 节点身份 | 宿主机节点 | 别名 | 类型 | 地址 | 分配方式 | 解析方式 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 节点 1 公网 | node1 | node1¹ | 公网 | 192.0.201 | 固定 | DNS |

| 节点 1 VIP | 由 Oracle Clusterware 选择 | node1-vip | 虚拟 | 192.0.204 | 固定 | DNS 和 hosts 文件 |

| 节点 1 私有 | node1 | node1-priv | 私有 | 192.168.0.1 | 固定 | DNS 和 hosts 文件，或无 |

| 节点 2 公网 | node2 | node2¹ | 公网 | 192.0.202 | 固定 | DNS |

| 节点 2 VIP | 由 Oracle Clusterware 选择 | node2-vip | 虚拟 | 192.0.2.105 | 固定 | DNS 和 hosts 文件 |

| 节点 2 私有 | node2 | node2-priv | 私有 | 192.168.0.2 | 固定 | DNS 和 hosts 文件，或无 |

| SCAN VIP 1 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.201 | 固定 | DNS |



| SCAN VIP 2 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.202 | 固定 | DNS |
| SCAN VIP 3 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.203 | 固定 | DNS |

- ¹ 节点主机名可能会解析到多个地址。

您不需要担心互连网络（interconnect），如果您对互连网络需要名称解析，可以在主机文件或 DNS 中配置私有 IP 名称。然而，Oracle Cluster 会在安装期间定义为私有接口（`eth1`）的接口上分配地址，并用于私有子网的子网。

SCAN 解析的地址由 Oracle Clusterware 分配，它们没有固定到特定的节点。为了启用 VIP 故障转移，上表所示配置将 SCAN 地址和两个节点的 VIP 地址定义在同一个子网 192.0.2 上。

高级安装 Oracle Cluster 集群版 Oracle Grid Infrastructure 预安装任务 2-35

## 检查网络需求

> **注意：** 所有主机名必须符合 RFC 952 标准

### 2.7.8 网络接口配置选项

您为网络选择的精确配置取决于您想要配置的集群的规模和用途，以及您所需的可用性级别。

如果 Oracle RAC 使用了经过认证的网络附属存储 (NAS)，且该存储通过基于以太网的网络连接，那么您必须有一个第三网络接口用于 I/O。在这种情况下，未提供三个独立的接口可能会导致负载下出现性能和稳定性问题。

### 2.7.9 多条私有互连和 Linux

在内核 2.6.31 及以上版本中（也包括 Oracle Unbreakable Kernel 2.6.32），反向路径过滤（Reverse Path Filtering）修复了一个错误。由于此项修正，使用多个网卡 (NIC) 用于私有互连的 RAC 系统现在需要对 `rp_filter` 参数进行特定设置。此要求也适用于所有运行 Linux 2.6.32 及以上版本的 Exadata 系统。如果没有这些 `rp_filter` 参数设置，互连数据包可能会被阻塞或丢。

`rp_filter` 值将反向路径过滤器设置为 0、严格过滤 (1) 或宽松过滤 (2)。将私有互连的 `rp_filter` 值设置为 0 或 2。将私有互连 NIC 设置为其他值可能会导致私有互连出现连接问题。禁用或放过滤被认为是不安全的，因为私有互连应该处于私有且隔离的网络中。

例如，当 `eth1` 和 `eth2` 是私有互连，而 `eth0` 是公网时，使用 `/etc/sysctl.conf` 中的以下条目将 `rp_filter` 值设置为 2（宽松过滤），公网地址设置为 1（严格过滤）：

```
net4.conf.eth2.rp_filter = 2
net4.conf.eth1.rp_filter = 2
net4.conf.eth0.rp_filter = 1
```

Enterprise Linux 5.6 (Update 1) 在 `inits-scripts-8.45.33-1.0.4.eli386.rpm` 中包含一个修复，该修复将内核参数 `net4.conf.default.rp_filter` 设置为 2（宽松模式）。因此，在 Enterprise Linux 5.6 上应用 Unbreakable Kernel 后，您可能不需要进行手动更改，因为所有 NIC 的 `rp_filter` 值都设置为 2。如果您在公网上需要更严格的路径过滤，请将公网 `rp_filter` 设置为 1。

**另请：** 我的支持备注 1286796.1 针对多个私有互连和 Linux 内核 2.6.32+ 的 rp_filter，可通过以下地址获取：

```
https://support.oracle.com
```

### 2.7.10 启用名称服务缓存守护进程 (nscd)

为了让 Oracle Cluster 更好地容 NAS 设备或 NFS 挂载的网络故障，请启用名称服务缓存守护进程 (nscd)。

检查 nscd 是否设置为系统重启时加载，输入命令 `chkconfig --list nscd`。例如：

```
# chkconfig --list nscd
nscd 0:off 1:off 2:off 3:on 4:off 5:off 6:off
```

在前面的示例中，nscd 在运行级别 3 开启，在运行级别 5 中关闭。nscd 应在运行级别 3 和运行级别 5 中都开启。

要更改配置以确保 nscd 在运行级别 3 和运行级别 5 中都开启，请输入以下之一：

# 在 Red Hat 上：

```
# chkconfig --level3 nscd on
```

# 在 SUSE 上：

```
# chkconfig --level3 nscd on
```

要在当前会话启动 nscd，输入：

```
# service nscd start
```

使用新设置重启 nscd，输入：

```
# service nscd restart
```

## 2.8 识别需求

根据您打算安装的产品，检查表 2-7 以确定是否需要为软件包安装额外功能。

> **注意：** 对于 Asian Server、Oracle Linux 和 Red Hat Enterprise Linux，系统需求通过内核版本识别。具体而言：

Oracle Linux 4 和 Red Hat Enterprise Linux 4 的需求相同。

Asian Server 3、Oracle Linux 5 和 Red Hat Enterprise Linux 5 的需求相同。

Asian Server 4、Red Hat Enterprise Linux 6 的需求相同。

从 Oracle Database 11 Release 2 (11.2) 开始，安全增强 Linux (SELinux) 功能支持 Oracle Linux 4、Red Hat Enterprise Linux 5。

以下是发布时的支持 Linux 版本列表：

- x86 平台软件需求列表
- x86-64 平台软件需求列表
- IBM 系统 Linux 软件需求列表

### 表 2–5（续）Linux x86 操作系统内核要求

| Linux 发行版 | 要求 |
| :--- | :--- |
| Red Hat Enterprise Linux 发行版 | - Red Hat Enterprise Linux 4, Update 7, 内核 2.6.9 或更高<br>- Red Hat Enterprise Linux 5, Update 2, 内核 2.6.18 及更高<br>- Red Hat Enterprise Linux 6, 内核 2.6.32-71 或更高 |
| SUSE Linux Enterprise 发行版 | - SUSE Linux Enterprise Server 10, 内核 2.6.16.21 或更高<br>- SUSE Linux Enterprise Server 11, 内核 2.6.27.19 或更高 |

### 表 2–6 Linux x86 网格基础架构和 Oracle RAC 软件包要求

| 项目 | 要求 |
| :--- | :--- |
| Oracle Linux 4 和 Red Hat Enterprise 4 | 必须安装以下软件包（或更高版本）：<br>-`binutils-2.15.92.0.2`<br>-`compat-libstdc++-33-3.2.3`<br>-`efutils-libelf-0.97`<br>-`efutils-libelf-devel-0.97`<br>-`gcc-3.4.6`<br>-`gcc-c++-3.4.6`<br>-`glibc-2.3.4-2.41`<br>-`glibc-common-2.3.4`<br>-`glibc-devel-2.3.4`<br>-`glibc-headers-2.3.4`<br>-`libaio-devel-0.3.105`<br>-`libaio-0.3.105`<br>-`libgcc-3.4.6`<br>-`libstdc++-3.4.6`<br>-`libstdc++-devel-3.4.6`<br>-`make-3.80`<br>-`numactl-0.6.4.1386`<br>-`pdksh-5.2.14`<br>-`sysstat-5.0.5`<br>-`unixODBC-2.2.11`<br>-`unixODBC-devel-2.2.11` |

### 表 2-6（续）Linux x86 网格基础架构和 Oracle RAC 软件包要求

| 项目 | 要求 |
| :--- | :--- |



## 表 2–6（续）Linux x86 网格基础架构和 Oracle 软件包要求

| 项目 | 要求 |
| :--- | :--- |
| Server 3, Oracle Linux 5 和 Red Hat Enterprise Linux 5 | 必须安装以下软件包（或更高版本）：<br>binutils-2.17.50.0.6<br>compat-libstdc++-33-3.2.3<br>elfutils-libelf-0.125<br>elfutils-libelf-devel-0.125<br>elfutils-libelf-devel-static-0.125<br>gcc-4.1.2<br>gcc-4.4.2-5.24<br>glibc-2.5<br>glibc-devel-2.5<br>glibc-headers-2.5<br>kernel-headers-2.6.18<br>ksh-9026014<br>libaio-0.3.106<br>libaio-devel-0.3.106<br>libgcc-4.1.2<br>libgomp-4.1.2<br>libstdc++-4.1.2<br>libstdc++-devel-4.1.2<br>make-3.81<br>sysstat-7.0.2<br>unixODBC-2.2.11<br>unixODBC-devel-2.2.11 |
| Oracle Linux 6, Red Hat Enterprise Linux Server 4 | 必须安装以下软件包（或更高版本）：<br>binutils-2.20.51.02-5.el6.i686<br>compat-libstdc++-1.10-el6.i686<br>compat-libstdc++-33-3.2.3-69.el6.i686<br>gcc-4.4.13-el6.i686<br>g++-4.4.4-13.el6.i686<br>glibc-2.12-1.7.el6.i686<br>glibc-devel-2.12-1.7.el6.i686<br>libgcc-4.4.13-el6.i686<br>libstdc++-4.4.13-el6.i686<br>libstdc++-devel-4.4.13-el6.i686<br>libaio-0.3.107-2.el6.i686<br>libaio-devel-0.3.107-2.el6.i686<br>make-3.81-19.el6.i686<br>sysstat-9.0.4-11.el6.i686 |

| 项目 | 要求 |
| :--- | :--- |
| SUSE Linux Enterprise Server 10 | 必须安装以下软件包（或更高版本）：binutils-2.16.9.0.5,compat-libstdc++-5.0.7,gcc-4.1.2,gcc-c++-4.1.2,gcc-2.4.31.63,glibc,glibc-dev-2.4.31.63,ksh-93-12.9,libaio-0.3.104,libio-dev-0.3.104,libelf-0.8.5,libgcc-4.1.2,libstdc++-4.1.2,libstdc++-devel-4.1.2,make-3.80,sysstat-8.0.4 |
| SUSE Linux Enterprise Server 11 | 必须安装以下软件包（或更高版本）：binutils-2.19,gcc-4.3,gcc-c++-4.3,glibc-2.9,glibc-dev-2.9,ksh-93,libcap-1.10-6,libstdc++-3.3.2008.02,libstdc++-4.3.2008.02,libaio-0.3.104,libio-dev-0.3.104,libgcc-4.3.2008.02,libstdc++-dev-4.3.2008.02,make-3.81,sysstat-8.1.5 |

注：Linux x86 的 `numa` 包链接为 `/usr/lib`。

## 表 2–7 Linux x86 Oracle 数据库功能要求

| 项目 | 要求 |
| :--- | :--- |
| LDAP 软件包 | 如果您没有执行默认安装、打算使用 LDAP 并想要使用 `osirreg`、`oircad` 或 `schemasync` 脚本，请为您的 Linux 发行版安装内核 RPM |
| Linux 插件模块 (Linux PAM) | 为您的 Linux 发行版安装最新的 PAM（插件模块）库。PAM 为系统管理员提供了更大的灵活性来选择应用程序验证用户的方式。在 Linux 上，调度作业需要 PAM。 |

## 表 2–7（续）Linux x86 Oracle 数据库功能要求

| 项目 | 要求 |
| :--- | :--- |
| ProC/C++, Oracle Call Interface, Oracle C++ Developer's Kit (XDK) | 支持 Intel C/C++ Compiler v10.1 或之前列出的发行版 GNU C 和 C++ 编译器用于这些产品。<br>注：Intel C/C++ Compiler v10.1 仅用于软件包要求中提到的 `gcc` 版本标准模板库构建 `OCCI`。<br>Oracle XML Developer's Kit 支持与 `OCCI` 相同的编译器。 |
| Oracle ODBC 驱动 | 如果您打算使用数据库连接 (ODBC)，则应该安装 Linux 最新的 ODBC 驱动管理器。<br>您应该从您的操作系统供应商处获取最新的 ODBC 驱动。您可以在以下 URL 了解 ODBC：`http://www.unixodbc.org`<br>只有在您计划使用 ODBC 时才需要 ODBC RPM。如果您不计划使用 ODBC，则不需要为 Oracle Clusterware、Oracle ASM 或 Oracle RAC 安装 ODBC RPM。<br>要使用 ODBC，您必须根据您的操作系统安装额外的 32 位 RPM：<br>Oracle Linux 4 和 Red Hat Enterprise Linux 4：<br>unixODBC-2.2.11 (32 bit) 或更高<br>unixODBC-devel-2.2.11 (32 bit) 或更高<br>CentOS 5, Oracle Linux 5 和 Red Hat Enterprise Linux 5：<br>unixODBC-2.2.11 (32 bit) 或更高<br>unixODBC-devel-2.2.11 (32 bit) 或更高<br>Oracle Linux 6, Red Hat Enterprise Linux 6 和 Anonymous Server 4：<br>unixODBC-2.2.14-11.el16.i686 或更高<br>unixODBC-devel-2.2.14-11.el16.i686 或更高<br>SUSE Linux Enterprise 10：<br>unixODBC-2.2.11 (32 bit) 或更高<br>unixODBC-devel-2.2.11 (32 bit) 或更高<br>SUSE Linux Enterprise 11：<br>unixODBC-2.2.11 (32 bit) 或更高<br>unixODBC-devel-2.2.11 (32 bit) 或更高 |
| Oracle JDBC/OCI | 如果您打算使用 Java 连接 (JDBC)，则应该安装 Linux 最新的 JDBC 驱动。<br>您应该从您的操作系统供应商处获取当前的 JDBC 驱动。 |

## x86-64 要求

对于 Oracle Linux 4 和 Red Hat Enterprise 4，必须安装以下软件包（或更高版本）：

- binutils-2.15.92.0.2
- compat-libstdc++-33-3.2.3
- efutils-libelf-0.97
- efutils-libelf-devel-0.97
- gcc-3.4.6
- gcc-c++-3.4.6
- glibc-2.3.4-2.41
- glibc-common-2.3.4
- glibc-devel-2.3.4
- glibc-headers-2.3.4
- libaio-devel-0.3.105
- libaio-0.3.105
- libgcc-3.4.6
- libstdc++-3.4.6
- libstdc++-devel-3.4.6
- make-3.80
- numactl-0.6.4.1386
- pdksh-5.2.14
- sysstat-5.0.5
- unixODBC-2.2.11
- unixODBC-devel-2.2.11

对于 Server 3, Oracle Linux 5 和 Red Hat Enterprise Linux 5，必须安装以下软件包（或更高版本）：

binutils-2.17.50.0.6
compat-libstdc++-33-3.2.3
elfutils-libelf-0.125
elfutils-libelf-devel-0.125



# 软件包列表

`elfutils-libelf-devel-static-0.125`

`gcc-4.1.2`

`gcc-4.4.2-5.24`

`glibc-2.5`

`glibc-devel-2.5`

`glibc-headers-2.5`

`kernel-headers-2.6.18`

`ksh-9026014`

`libaio-0.3.106`

`libaio-devel-0.3.106`

`libgcc-4.1.2`

`libgomp-4.1.2`

`libstdc++-4.1.2`

`libstdc++-devel-4.1.2`

`make-3.81`

`sysstat-7.0.2`

`unixODBC-2.2.11`

`unixODBC-devel-2.2.11`

## Oracle Linux 6, Red Hat Enterprise Linux Server 4

对于 Oracle Linux 6, Red Hat Enterprise Linux Server 4，必须安装以下软件包（或更高版本）：

`binutils-2.20.51.02-5.el6.i686`

`compat-libstdc++-1.10-el6.i686`

`compat-libstdc++-33-3.2.3-69.el6.i686`

`gcc-4.4.13-el6.i686`

`g++-4.4.4-13.el6.i686`

`glibc-2.12-1.7.el6.i686`

`glibc-devel-2.12-1.7.el6.i686`

`libgcc-4.4.13-el6.i686`

`libstdc++-4.4.13-el6.i686`

`libstdc++-devel-4.4.13-el6.i686`

`libaio-0.3.107-2.el6.i686`

`libaio-devel-0.3.107-2.el6.i686`

`make-3.81-19.el6.i686`

`sysstat-9.0.4-11.el6.i686`

## SUSE Linux Enterprise Server 10

对于 SUSE Linux Enterprise Server 10，必须安装以下软件包（或更高版本）：

`binutils-2.16.9.0.5`

`compat-libstdc++-5.0.7`

`gcc-4.1.2`

`gcc-c++-4.1.2`

`gcc-2.4.31.63`

`glibc`

`glibc-dev-2.4.31.63`

`ksh-93-12.9`

`libaio-0.3.104`

`libio-dev-0.3.104`

`libelf-0.8.5`

`libgcc-4.1.2`

`libstdc++-4.1.2`

`libstdc++-devel-4.1.2`

`make-3.80`

`sysstat-8.0.4`

## SUSE Linux Enterprise Server 11

对于 SUSE Linux Enterprise Server 11，必须安装以下软件包（或更高版本）：

`binutils-2.19`

`gcc-4.3`

`gcc-c++-4.3`

`glibc-2.9`

`glibc-dev-2.9`

`ksh-93`

`libcap-1.10-6`

`libstdc++-3.3.2008.02`

`libstdc++-4.3.2008.02`

`libaio-0.3.104`

`libio-dev-0.3.104`

`libgcc-4.3.2008.02`

`libstdc++-dev-4.3.2008.02`

`make-3.81`

`sysstat-8.1.5`

## 表 2–8（续）Linux x86-64 操作系统内核要求

| Linux 发行版 | 要求 |
|---|---|
| Red Hat Enterprise Linux 发行版 | - Red Hat Enterprise Linux 4, Update 7, 内核 2.6.9 或更高版本<br>- Red Hat Enterprise Linux 5, Update, 2.6.18 或更高版本<br>- 带有 Oracle Unbreakable Enterprise Kernel for Linux 的 Red Hat Enterprise Linux 5,内核 2.6.32 或更高版本<br>- Red Hat Enterprise Linux 6, 2.6.32-71.el6.x86_64 或更高版本<br>- 带有 Oracle Unbreakable Enterprise Kernel for Linux 的 Red Hat Enterprise Linux 6,内核 2.6.32-103.28.5.el6.x86_64 或更高版本<br>- Red Hat Enterprise Linux 7,内核 3.10.0-54.0.el17.x86_64 或更高版本<br>- 带有 Oracle Unbreakable Enterprise Kernel 的 Red Hat Enterprise Linux 7, 3.8.13-el7.uek.x86 或更高版本 |
| SUSE Enterprise Linux 发行版 | - SUSE Linux Enterprise Server 10, Service Pack 2 (SP2), 内核 2.6.16 或更高版本<br>- SUSE Linux Enterprise Server 11,内核 2.26.19 或更高版本<br>- SUSE Linux Enterprise Server 12,内核 3.12.49-11 或更高版本 |
| 麒麟高级服务器 (NeoKylin Advanced Server) | - 麒麟6, 2.6.32-431.el6.x86_64 或更高版本<br>- 麒麟7, 3.10.0-327.el17.x86_64 或更高版本 |

## 表 2–9 Linux x86-64 Oracle Grid Infrastructure 和 RAC 软件包要求

| 项目 | 要求 |
|---|---|
| Oracle 7 和 Red Hat Enterprise 7 | 必须安装以下软件包（或版本）：<br>-`linux-2.23.25.0.1-12.el17.x86_64`<br>-`compat-libcap-1.10.el17.x86_64`<br>-`gcc-4.8.2-3.el17.x86_64`<br>-`gcc-c++-4.8.2-3.el17.i6886`<br>-`glibc-2.17-36.el17.i6886`<br>-`glibc-2.17-36.el17.x86_64`<br>-`glibc-devel-2.17-36.el17.i6886`<br>-`glibc-devel-2.17-36.el17.x86_64`<br>-`ksh libaio-0.3.109-9.el17.i6886`<br>-`libaio-0.3.109-9.el17.x86_64`<br>-`libaio-devel-0.3.109-9.el17.i6886`<br>-`libaio-devel-0.3.109-9.el17.x86_64`<br>-`libgcc-4.8.2-3.el17.x86_64`<br>-`libgcc-4.8.2-3.el17.i6886`<br>-`libstdc++-4.8.2-3.el17.x86_64`<br>-`libstdc++-4.8.2-3.el17.i6886`<br>-`libstdc++-devel-4.8.2-3.el17.x86_64`<br>-`libstdc++-devel-4.8.2-3.el17.i6886`<br>-`libxi-1.7.2-1.el17.i6886`<br>-`libxi-1.7.2-1.el17.x86_64`<br>-`libhtst-1.2.2-1.el17.i6886`<br>-`libhtst-1.2.2-1.el17.x86_64`<br>-`make-3.82-19.el17.x86_64`<br>-`sysstat-10.1.5-1.el17.x86_64` |

集群预安装任务：高级安装 Grid Infrastructure 2–45

## 表 2-9（续）Linux x86-64 Oracle Grid Infrastructure 和 Oracle RAC 软件包要求

| 项目 | 要求 |
| --- | --- |
| Oracle 6 (2.62-30.100.25.el6.x86_64 或更高版本) | 订阅 Unbreakable Linux 上的 Oracle 6 频道，然后安装 Oracle Preinstallation RPM。这会安装 Oracle Unbreakable Enterprise Kernel 以及 Grid Infrastructure 和 Oracle Databases 所需的所有内核。 |



## 表 2–9（续）Linux x86-64 Oracle Grid Infrastructure 和 RAC 要求

| Oracle 6, Red Hat Enterprise Linux 6 和 Asian Server 4 | 必须安装以下软件包（或更高版本）：<br> `binutils-20.51.02-p5.2-11.el16` (x86_64)<br> `compat-libibc-33.2.69.el16` (x86_64)<br> `compat-libstdc++-33.2.69.el16` (i6886)<br> `gcc-4.4.4-13.el16` (x86_64)<br> `gcc-c++-4.4.4-13.el16` (x86_64)<br> `glibc-2.12-1.7.el16` (i6886)<br> `glibc-2.12-1.7.el16` (x86_64)<br> `glibc-devel-2.12-1.7.el16` (i6886)<br> `glibc-devel-2.12-1.7.el16` (x86_64)<br> `ksh`<br> `libgcc-4.4.4-13.el16` (i6886)<br> `libgcc-4.4.4-13.el16` (x86_64)<br> `libstdc++-4.4.4-13.el16` (i6886)<br> `libstdc++-4.4.4-13.el16` (x86_64)<br> `libstdc++-devel-4.4.4-13.el16` (i6886)<br> `libstdc++-devel-4.4.4-13.el16` (x86_64)<br> `libaio-0.3.107-10.el16` (i6886)<br> `libaio-0.3.107-10.el16` (x86_64)<br> `libaio-devel-0.3.107-10.el16` (i6886)<br> `libaio-devel-0.3.107-10.el16` (x86_64)<br> `make-3.82-19.el16`<br> `cmake-3.4.21.el16` (x86_64) |

| Oracle Linux 5 Update 5 (2.62-30.100.9 或更高版本) | 订阅 Unbreakable Linux 上的 Oracle Linux 5 频道，然后安装 Oracle Preinstallation RPM。这会安装 Oracle Unbreakable Enterprise Kernel 以及 Grid Infrastructure 和 Oracle Databases 所需的所有内核。 |

| 项目 | 要求 |
| --- | --- |
| Asian Server 3, Oracle Linux 5 和 Red Hat 5 | 必须安装以下软件包（或更高版本）：`binutils-2.17.50.4`, `compat-libstdc++-33.2.3`, `compat-libstdc++-33.2.3` (32位), `elfutils-libelf-0.125`, `elfutils-libelf-devel-0.125`, `gcc-4.1.2`, `gcc-4.1.2`, `glibc-2.5-24`, `glibc-2.5-24` (32位), `glibc-common-2.5`, `glibc-devel-2.5`, `glibc-devel-2.5` (32位), `glibc-headers-2.5`, `ksh`, `libaio-0.3.106`, `libaio-0.3.106` (32位), `libaio-devel-0.3.106`, `libaio-devel-0.3.106` (32位), `libgcc-4.1.2`, `libgcc-4.1.2` (32位), `libstdc++-4.1.2`, `libstdc++-4.1.2` (32位), `libstdc++-devel-4.1.2`, `make-3.81`, `sysstat-7.0.2`, `unixODBC-2.2.11`, `unixODBC-2.2.11` (32位), `unixODBC-devel-2.2.11`, `unixODBC-devel-2.2.11` (32位), `coreutils-5.97.23.el5_4.1` 或更高版本 |

## 表 2–9（续）Linux x86-64 Oracle Grid Infrastructure 和 Oracle RAC 要求

| 项目 | 要求 |
| --- | --- |
| Oracle Linux 4 和 Red Hat Enterprise 4 | 必须安装以下软件包（或更高版本）：`binutils-2.15.92.0`, `compat-libdso++-33-3.2.3`, `compat-libdso++-33-3.2.3` (32位), `elfutils-libelf-0.97`, `elfutils-libelf-devel-0.97`, `expat-1.95.7`, `gcc-c++-3.4.6`, `gcc-c++-3.4.6`, `glibc-2.3.4-2.41`, `glibc-2.3.4-2.41` (32位), `glibc-common-2.3.4`, `glibc-devel-2.3.4`, `glibc-headers-2.3.4`, `libaio-0.3.105`, `libaio-0.3.105` (32位), `libaio-devel-0.3.105`, `libaio-devel-0.3.105` (32位), `libgcc-3.6`, `libgcc-3.6` (32位), `libstdc++-3.4.6`, `libstdc++-3.4.6` (32位), `libstdc++-devel-3.4.6`, `make-3.80`, `numactl-0.6.4.x86_64`, `pdksh-5.2.14`, `sysstat-5.0.5`, `unixODBC-2.2.11`, `unixODBC-2.2.11` (32位), `unixODBC-devel-2.2.11`, `unixODBC-devel-2.2.11` (32位) |

| SUSE Linux Enterprise 12 | 必须安装以下软件包（或更高版本）：`binutils-2.25.0-13`, `gcc-4.6-189`, `gcc-4.8-5-24.1`, `glibc-2.19-39`, `glibc-2.19-39` (32位), `glibc-devel-2.19-39`, `glibc-devel-2.19-39` (32位), `libaio-0.3.109-17`, `libcap-10-59.61`, `libstdc++-48-devel-5-24.1` (x86_64), `libstdc++-48-devel-32bit-4.8-5` (x86_64), `libstdc++-5.2+r22605-4.1` (x86_64), `libstdc++-32bit-4.6-189` (x86_64), `libgcc-5.2+r22605-4.1` (x86_64), `libgcc-32bit-4.6-189` (x86_64), `libgcc-devel-32bit-4.8-189` (x86_64), `mksh-50-13`, `make-4.0-1.x86_64`, `sysstat-10.2-1.x86_64`, `org-x11-driver-video-7.6-15-36.21` (x86_64), `org-x11-server-7.6-15-36.21` (x86_64), `org-x11-essentials-7.6-14` (noarch), `org-x11-nm-4.3-7.2` (x86_64), `org-x11-fonts-7.6-29.45` (noarch), `org-x11-7.6-13` (noarch), `org-x11-server-extra-7.6-15-36.21` (x86_64), `org-x11-libs-7.6-45.14` (noarch), `org-x11-fonts-7.6-29.45` (noarch)。注意：你必须下载并安装补丁 `18370031`。有关如何下载和安装该补丁，请参见：`https://support.oracle.com` |

## 表 2–9（续）Linux x86-64 Oracle Grid Infrastructure 和 RAC 要求

| 项目 | 要求 |
| --- | --- |



## SUSE Linux Enterprise Server 11
| 必须安装以下软件包（或更高版本）：`binutils-2.19`, `gcc-4.3`, `gcc-32bit-4.3`, `gcc-c++-4.3`, `glibc-2.9`, `glibc-32bit-2.9`, `glibc-devel-2.9`, `glibc-devel-32bit-2.9`, `sh-93`, `libaio-0.3.104`, `libaio-32bit-0.104`, `libaio-devel-0.3.104`, `libaio-devel-32bit-0.104`, `libstdc++-33.3`, `libstdc++-32bit-3.3_2008122`, `libstdc++-43-32bit-4.3_2008122`, `libstdc++-43-devel-4.3_2008122`, `libstdc++-43-devel-32bit-4.3_2008122`, `libgcc-4.3.3_2008122`, `libgcc-c++-devel-4.3`, `make-2.1`, `sysstat-8.1.5` |

## SUSE Linux Enterprise Server 10
| 必须安装以下软件包（或更高版本）：`binutils-2.16.91.0.5`, `compat-libstdc++-5.0.7` (IBM:Linux 上不需要), `gcc-c++-4.1.2`, `gcc-2.4-31.63`, `glibc-2.4`, `glibc-devel-2.4`, `glibc-32bit-2.4`, `sh-93r-12.9`, `libaio-0.3.104`, `libaio-32bit-0.104`, `libaio-devel-0.3.104`, `libaio-devel-32bit-0.104`, `libelf-0.8.5`, `libgcc-4.1.2`, `libstdc++-4.1.2`, `make-3.80`, `numactl-0.9.6.x86_64`, `sysstat-8.0.4` |

## 表 2–9（续）Linux x86-64 Oracle Grid Infrastructure 和 Oracle RAC 软件包要求

| 项目 | 要求 |
| --- | --- |
| NeoKotlin Linux Advanced Server 7 | 必须安装以下软件包（或更高版本）：`binutils-2.23.52.0-15.el7.x86_64`, `compat-libcap-1.10-7.el7.x86_64`, `gcc-4.8.5-4.el7.01.x86_64`, `gcc-c++-4.8.5-4.el7.01.x86_64`, `glibc-2.17-105.el7.01.x86_64`, `glibc-2.17-105.el7.ns01.i6886`, `glibc-devel-2.17-105.el7.ns01.x86_64`, `glibc-devel-2.17-105-el7.ns01.i6886`, `make-20180218.el7.x86_64`, `libaio-0.3.105.el7.ns01.i6886`, `libaio-0.3.105.el7.x86_64`, `libaio-devel-0.3.105.el7.ns01.i6886`, `libaio-devel-0.3.105.el7.x86_64`, `libgcc-4.8.5-4.el7.01.x86_64`, `libgcc-c++-4.8.5-4.el7.01.x86_64`, `libstdc++-4.8.5-4.el7.x86_64`, `libstdc++-4.8.5-4.el7.ns01.i6886`, `libstdc++-devel-4.8.5-4.el7.ns01.x86_64`, `libstdc++-devel-4.8.5-4.el7.ns01.i6886`, `sysstat-10.1.5.el7.x86_64` |
| NeoKotlin Linux Advanced Server 6 | 必须安装以下软件包（或更高版本）：`binutils-20.51.02-p5.2-11.el16` (x86_64), `compat-libcap-1.10-7` (x86_64), `compat-libstdc++-33.2.69.el16` (i6886), `gcc-4.4.4-13.el16` (x86_64), `gcc-c++-4.4.4-13.el16` (x86_64), `glibc-2.12-1.7.el16` (i6886), `glibc-2.12-1.7.el16` (x86_64), `glibc-devel-2.12-1.7.el16` (i6886), `glibc-devel-2.12-1.7.el16` (x86_64), `ksh`, `libgcc-4.4.4-13.el16` (i6886), `libgcc-4.4.4-13.el16` (x86_64), `libstdc++-4.4.4-13.el16` (i6886), `libstdc++-4.4.4-13.el16` (x86_64), `libstdc++-devel-4.4.4-13.el16` (i6886), `libstdc++-devel-4.4.4-13.el16` (x86_64), `libaio-0.3.107-10.el16` (i6886), `libaio-0.3.107-10.el16` (x86_64), `libaio-devel-0.3.107-10.el16` (i6886), `libaio-devel-0.3.107-10.el16` (x86_64), `make-3.82-19.el16`, `cmake-3.4.21.el16` (x86_64) |

## 表 2–10 Linux x86-64 Oracle Database 功能包要求

| 项目 | 要求 |
| --- | --- |
| LDAP 软件包 | 如果您没有执行默认的 Linux 安装，但打算使用 LDAP，并且想要使用脚本 `isrvrq`、`oidca`, 或 `schemysync`，则请为您的 Linux 发行版安装内核 RPM |
| ProC/C++, Oracle Call Interface, Oracle C++ Call Interface, Oracle XML Developer's Kit (XDK) | 安装 C++ 编译器 10.1 或更高版本，并且之前列出的适用于该发行版的 GNU C 和 C++ 编译器支持与这些产品配合。<br>注意：Intel C/C++ Compiler v10.1 仅可配合供应商 gcc 版本中的标准模板库来构建 Oracle C++ Call Interface (OCCI) 应用。<br>Oracle XML Developers's Kit 支持与 OCCI 相同的编译器 |
| Linux 可插身份认证模块 (PAM) | 为您的 Linux 发行版安装最新的 PAM（Linux 可插身份认证模块）库。PAM 为系统管理员提供了更大的灵活性来选择应用程序如何验证用户。在 Linux 上，外部调度器需要 PAM |
| Oracle ODBC 驱动 | 如果您打算使用数据库连接 (ODBC)，则应为 Linux 安装的最新的 ODBC 驱动管理器。<br>您应该从您的操作系统供应商处获取最新的 ODBC 驱动。您可以在以下 URL 了解 ODBC：`http://www.unixodbc.org` |

## 表 2–10 (续) Linux x86-64 Oracle Database 功能包要求

Oracle Linux 4 和 Red Hat Enterprise Linux 4:
- `unixODBC-2.2.11` (32 位) 或更高版本
- `unixODBC-devel-2.2.11` (64 位) 或更高版本
- `unixODBC-2.2.11` (64 位) 或更高版本

Asianian Server 3, Oracle Linux 5 和 Red Hat Enterprise Linux 5:
- `unixODBC-devel-2.2.11` (32 位) 或更高版本
- `unixODBC-devel-2.2.11` (64 位) 或更高版本
- `unixODBC-2.2.11` (64 位) 或更高版本

Oracle Linux 6 和 Red Hat Enterprise Linux 6:
- `unixODBC-2.2.14-11.el6` (x86_64) 或更高版本
- `unixODBC-2.2.14-11.el6.1686` 或更高版本
- `unixODBC-devel-2.2.14-11.el16` (x86_64) 或更高版本
- `unixODBC-devel-2.2.14-11.el16.1686` 或更高版本

Oracle Linux 7 和 Red Hat Enterprise Linux 7:
- `unixODBC-2.3.1-6.el7,x86_64` 或更高版本
- `unixODBC-2.3.1-6.el7.x86_64` 或更高版本
- `unixODBC-devel-2.3.1-6.el7,x86_64` 或更高版本
- `unixODBC-devel-2.3.1-6.el7.1686` 或更高版本



### SUSE Linux Enterprise Server 10:

- unixODBC-32bit-2.2.11 (32 位) 或更高版本
- unixODBC-2.2.11 (64 位) 或更高版本
- unixODBC-devel-2.2.11 (64 位) 或更高版本

### SUSE Linux Enterprise Server 11:

- unixODBC-2.12 或更高版本
- unixODBC-devel-2.12 或更高版本
- unixODBC-32bit-2.12 (32 位) 或更高版本

### 在 Oracle Linux Advanced Server 7 上:

- unixODBC-2.3.1-11.el17.1686 或更高版本
- unixODBC-2.3.1-11.el17.x86_64 或更高版本
- unixODBC-devel-2.3.1-11.el17.1686 或更高版本
- unixODBC-devel-2.3.1-11.el17.x86_64 或更高版本

### 在 Oracle Linux Server 6 上:

- unixODBC-2.2.14-el12.1686 或更高版本
- unixODBC-2.2.14-el12.x86_64 或更高版本
- unixODBC-devel-2.2.14-el12.1686 或更高版本
- unixODBC-devel-2.2.14-el12.x86_64 或更高版本

可以使用以下可选 JDK 版本，但安装并非强制：

- JDK 6 (Java SE 1.6.0_21)
- JDK 5 (1.5.0_24)

注意：默认安装了 JDK 5。

## 表 2–10 (续) Linux x86-64 Oracle Database 功能包要求

| 项目 | 要求 |
| --- | --- |
| Oracle Application Clusters | 对于集群，使用版本 1.2 或更高。检查 ocfs2 版本执行命令：`modinfo ocfs2`<br>检查 ocfs2 工具执行命令：`rpm -qa | grep ocfs2`<br>确保 ocfs2 和 ocfs2-tools 版本至少为 1.2.7<br>有关 ocfs2 的信息请参考网站：http://oss.oracle.com/projects/ocfs2/<br>ocfs2 状态请参考：http://oss.oracle.com/projects/ocfs2/ |

## 2.8.3 IBM: Linux 系统软件要求

确保服务器上安装了 OpenSSH。OpenSSH 是所需的软件。

## 表 2–11 IBM: Linux 系统包要求

| 项目 | 要求 |
| --- | --- |
| 操作系统 | Red Hat Enterprise Linux 7<br>Red Hat Enterprise Linux 6<br>Red Hat Enterprise Linux 5<br>Red Hat Enterprise Linux 4<br>SUSE Linux Enterprise Server 11<br>SUSE Linux Enterprise Server 10 |

## 表 2–11 (续) IBM: Linux 系统包要求

| 项目 | 要求 |
| --- | --- |
| 内核版本 | 系统必须运行适用于每个 Linux 发行版的内核版本：<br>Red Hat Enterprise Linux 7: 3.10.0-229.el7 或更高版本<br>Red Hat Enterprise Linux 6: 2.6.32-200 或更高版本<br>Red Hat Enterprise Linux 5: 2.6.18 或更高版本<br>Red Hat Enterprise Linux 4: 2.6.9 或更高版本<br>SUSE Linux Enterprise Server 11: 3.10.32.12 或更高版本<br>SUSE Linux Enterprise Server 10: 2.6.16.0 或更高版本 |

Red Hat Enterprise Linux 7 必须安装以下包（或更高版本）：

- binutils-2.23.52.0.1-30.el7.s390x
- compat-libstdc++-1.10-7.el7.s390x
- cpp-4.8.2-16.el7.s390x
- gcc-4.6.3-9.el7.s390x
- gcc-c++-4.8.3-9.el7.s390x
- glibc-2.17-78.el7.s390x
- glibc-2.17-78.el7.s390x
- glibc-devel-2.17-78.el7.s390x
- glibc-headers-2.17-75.el5.s390x
- s390-201.22.el7.s390x
- ksh-20120801-22.el7.s390x
- libaio-0.3-109-12.el7.s390x
- libaio-0.3-109-12.el7.s390x
- libaio-devel-0.3-109-12.el7.s390x
- libaio-devel-0.3-109-12.el7.s390x
- libgcc-4.8.3-9.el7.s390x
- libgcc-4.8.3-9.el7.s390x
- libstdc++-4.8.3-9.el7.s390x
- libstdc++-4.8.3-9.el7.s390x
- libstdc++-devel-4.8.3-9.el7.s390x
- libstdc++-devel-4.8.3-9.el7.s390x
- libacl-1.2.2-el7.s390x
- libacl-1.2.2-el7.s390x
- libXtst-1.2.2-21.el7.s390x
- libXtst-1.2.2-21.el7.s390x
- make-3.82-21.el7.s390x
- mpfr-3.1.1-4.el7.s390x
- sysstat-10.1.5-7.el7.s390x

## 表 2–11 (续) IBM: Linux 系统包要求

| 项目 | 要求 |
| --- | --- |
| Red Hat Enterprise Linux 6 | 必须安装以下包（或更高版本）：<br><br>- binutils-2.20.51.0.2-58.s390x<br>- compat-libstdc++-33.2.3-16.s390<br>- gcc-4.4.6-el6.s390<br>- gcc-c++-4.4.6-el6.s390<br>- glibc-2.12-47.el6.s390<br>- glibc-2.12-47.el6.s390<br>- glibc-devel-2.12-47.el6.s390<br>- glibc-devel-2.12-47.el6.s390<br>- libaio-0.3-107-el6.s390<br>- libaio-0.3-107-el6.s390<br>- libaio-devel-0.3-107-el6.s390<br>- libgcc-4.4.6-el6.s390<br>- libgcc-4.4.6-el6.s390<br>- libstdc++-4.4.19-el6.s390<br>- libstdc++-4.4.19-el6.s390<br>- make-3.119.el6.s390<br>- 2.4.18.el6.s390<br>- unixODBC-2.2.14-11.el6.s390 (使用 ODBC 时需要)<br>- unixODBC-devel-2.2.14-11.el6.s390 (使用 ODBC 时需要) |

| Red Hat Enterprise Linux 5 | 必须安装以下包（或更高版本）：<br><br>- binutils-2.17.50.0.6.el15.s390<br>- compat-libstdc++-33.2.3-6.s390<br>- compat-libstdc++-33.2.3-61.s390<br>- gcc-4.1.2-46.el5.s390x<br>- gcc-c++-4.1.2-46.el5.s390x<br>- glibc-2.5-42.s390<br>- glibc-2.5-42.s390x<br>- glibc-devel-2.5-42.s390<br>- glibc-devel-2.5-42.s390x<br>- libaio-0.3-106-3.2.s390<br>- libaio-0.3-106-3.2.s390x<br>- libaio-devel-0.3-106-3.2.s390x<br>- glibc-devel-2.1.106-3.2.s390x<br>- libgcc-4.1.2-46.el5.s390<br>- libgcc-4.1.2-46.el5.s390x<br>- libstdc++-4.1.2-46.el5.s390x<br>- libstdc++-4.1.2-465<br>- libstdc++-4.1.2-46.el5.s390x<br>- make-3.81<br>- sysstat-7.0.2-3.el5.s390x |



- `unixODBC-2.2.11` (使用 ODBC 时需要)
- `unixODBC-devel-2.2.11` (使用 ODBC 时需要) |

## 表 2–11 (续) IBM: Linux 系统带包要求

| 项目 | 要求 |
| --- | --- |
| Red Enterprise Linux 4 | binutils-2.15.92.0.25 (s390) <br> - compat-libstdc++-33.2.3-6 (s390) <br> - compat-libstdc++-33.2.3-61 (s390) <br> - gcc-4.1.2 (s390) <br> - gcc-c++-4.1.2 (s390) <br> - glibc-2.3.4.s390 <br> - glibc-2.3.4.s390x <br> - glibc-devel-2.3.4.s390 <br> - glibc-devel-2.3.4.s390 <br> - libaio-0.3-106-3.2.s390 <br> - libaio-0.3-106-3.2.s390 <br> - libaio-devel-0.3-106-3.2.s390 <br> - libgcc-4.1.2 (s390) <br> - libgcc-4.1.2 (s390) <br> - libstdc++-4.1.2 (s390) <br> - libstdc++-4.1.2 (32 位) <br> - libstdc++-devel-4.1.2 (32 位) <br> - libstdc++-devel-4.1.2 (x86_64) <br> - make-3.80 <br> - sysstat-5.0.25 (s390) <br> - unixODBC-2.2.11 (使用 ODBC 时需要) <br> - unixODBC-devel-2.2.11 (使用 ODBC 时需要) |
| SUSE Linux Enterprise Server 11 | binutils-2.20.0-7.9 (s390) <br> - gcc-4.3.62.19 (s390) <br> - gcc-c++-4.3.62.19 (s390) <br> - glibc-2.11-0.17 (s390) <br> - glibc-2.11-0.17 (32 位) <br> - glibc-devel-2.11-0.17 (s390) <br> - glibc-devel-2.11-0.17 (32 位) <br> - ksh <br> - libaio-0.3-107 (s390) <br> - libaio-0.3-107 (32 位) <br> - libaio-devel-0.3-107 (s390) <br> - libaio-devel-0.3-107 (32 位) <br> - libgcc43-4.3.20091019-0.7.35 (s390) <br> - libstdc++43-4.3.20091019-0.7.35 (s390) <br> - libstdc++-devel-4.3.20091019-0.7.35 (s390) <br> - libstdc++-devel-4.3.20091019-0.7.35 (32 位) <br> - libstdc++-devel-4.1.2 (x86_64) |

## 识别软件需求

| 表 2–11（续）IBM: Linux on System z 软件包需求 |
| 项目 | 要求 |
| SUSE Linux Enterprise Server 10 | 必须安装以下软件包（或更高版本）：<br>binutils-32bit-2.16.91.0.5-23.34.33 (s390x)<br>gcc-4.1.2.20070115-0.296 (s390x)<br>g++-4.1.2.20070115-0.296 (s390x)<br>glibc-2.4-31.74.1 (s390x)<br>glibc-32bit-2.4-31.74.1 (s390x)<br>glibc-devel-2.4-31.74.1 (s390x)<br>glibc-devel-32bit-2.4-31.74.1 (s390x)<br>ksh<br>libio-0.3.104-14.2 (s390x)<br>libio-32bit-0.3.104-14.2 (s390x)<br>libio-devel-0.3.104-14.2 (s390x)<br>libio-devel-32bit-0.3.104-14.2 (s390x)<br>libgcc-4.1.2.20070115-0.296 (s390x)<br>libstdc++-4.1.2.20070115-0.296 (s390x)<br>libstdc++-4.1.2.20070115-0.296 (s390x)<br>make-3.8-202.2 (s390x)<br>sysstat-8.0.4.1.27 (s390x)<br>unixODBC-2.2.11（仅在使用 ODBC 时需要）<br>unixODBC-devel-2.2.11（仅在使用 ODBC 时需要） |
| IBM WebSphere MQ for Linux | MQ Series 7.0 (Red Hat 5, Red Hat 6, Red Hat 7, SUSE 10, SUSE |
| Micro Focus Server Express | Micro Focus Server Express 5.1 |

## 表 2–11（续）IBM: Linux on z 软件包需求

| 项目 | 要求 |
| Oracle ODBC 驱动 | 如果你打算使用 ODBC，请安装 OCF2 L4 或更高版本。你可以从以下 URL 下载并安装驱动管理器：http://www.unixodbc.org <br><br>该网站提供 Linux RPM 软件包。安装 Oracle Clusterware、Oracle Database 或 Oracle RAC 不需要 ODBC 驱动管理器。<br><br>运行需要以下额外的 ODBC RPM 软件包（或更高版本）：<br><br>- Red Hat Enterprise Linux 4: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 <br>- Red Hat Enterprise Linux 5: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 <br>- Red Hat Enterprise Linux 6: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 <br>- Red Hat Enterprise Linux 7: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 <br>- SUSE Linux Enterprise Server 10: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 <br>- SUSE Linux Enterprise Server 11: <br>  - unixODBC-2.2.11 (32 bit) 或更高 <br>  - unixODBC-devel-2.2.11 (64 bit) 或更高 <br>  - unixODBC-2.2.11 (64 bit ) 或更高 |

## 2.9 检查软件需求

要确保系统满足这些需求，请执行以下步骤：

### 验证 UDP 和内核参数

要确保系统满足这些需求，请执行以下步骤：

- 1. 确定发行版和版本，执行以下命令：

  ```bash
  cat /proc/version
  ```

  示例输出为 Red Hat Enterprise Linux 7 (3.10.0-11.el7.x86_64)。

- 2. 确定内核版本，执行以下命令：

  ```bash
  uname -r
  ```

  示例输出为 3.10.0-1062.el7.x86_64。

- 3. 检查是否安装了所需的软件包，执行以下命令：

  ```bash
  rpm -qa | grep glibc
  ```

  或者，使用以下命令检查特定版本：

  ```bash
  rpm -q --format '%{NAME}-%{VERSION}' glibc
  ```

- 4. 检查是否安装了 OCF2，执行以下命令：

  ```bash
  modinfo ocfs2
  ```

  如果没有安装该包，请从你的发行版下载。

- 5. 确定 TCP 临时端口范围，执行以下命令：

  ```bash
  cat /proc/sys/ipv4/ip_port_range
  ```



示例输出范围为 32768 61000。如果你需要更新范围，请使用以下命令：

```bash
echo 65500 > /proc/sys/ipv4/ip_port_range
```

Oracle 建议你进行这些设置。例如，以 root 身份使用文本编辑器编辑 `/etc/sysctl.conf`，并添加以下内容：

`net.ipv4.ip_port_range = 65500`

然后运行：

```bash
sysctl -p
```

Oracle JDBC/OCI 驱动可以使用以下 JDK 版本，但对于安装程序来说它们不是是必需的：

- JDK 6 SR1 或更高
- JDK 5 SR3 或更高

# 在 Linux 上安装 cvuqdisk 软件包

```bash
# /sbin/service ntpd stop
# chkonfig ntpd off
# rm /etc/ntp.conf
```

或者，将 `/etc/ntp.conf` 移动到 `/etc/ntp.org`。

同时删除以下文件：

```
/var/run/ntpd.pid
```

当安装程序发现 NTP 服务未激活时，集群时间同步服务将在节点之间同步时间。如果未配置 NTP，集群时间同步服务将在激活模式下启动，Oracle 集群将不会集群内执行任何活跃的时间同步。

要确认安装后 `ctssd` 是否处于激活状态，请以 Grid 安装所有者的身份输入以下命令：

```bash
$ crctl check ctss
```

如果您正在使用 NTP 并希望继续使用它而不是集群时间同步服务，则需要修改 NTP 配置以设置 `-x` 标志，这将防止时间向回调整。完成此任务后重启网络时间守护进程。

要执行此操作，对于 Oracle Linux、Red Hat Linux 和亚洲系统，请编辑 `/etc/sysconfig/ntpd` 文件以添加 `-x` 标志，如示例所示：

```bash
# 默认切换到 id 为 'ntp:ntp'。
OPTIONS="-x -u ntp -p /var/run/ntpd.pid"

# 在 ntpdate 成功同步后设置为 'yes' 以同步硬件时钟
SYNC_HWCLOCK=no

# ntpdate 的额外选项
NTPDATE_OPTIONS="**"
```

然后，重启 NTP 服务。

```bash
# /sbin/service ntp restart
```

在 SUSE 上，使用以下设置修改配置文件 `/etc/sysconfig/ntp`：

```bash
NTP_OPTIONS="-x -u ntp*
```

使用以下命令重启守护进程：

```bash
# service ntp restart
```

## 2.12 在 Linux 上安装 cvuqdisk 软件包

安装操作系统软件包 `cvuqdisk`。如果没有 `cvuqdisk`，集群验证工具（Cluster Verification Utility）将无法发现共享磁盘，且当您运行集群验证工具时，您会收到错误消息“Package cvuqdisk not installed”。请根据您的硬件（例如 x86_64 或 i386）使用 `cvuqdisk` rpm。

要安装 `cvuqdisk` RPM，请完成以下步骤：

- 1. 找到 `cvuqdisk` RPM 软件包，它位于安装介质的 `rpm` 目录下。如果您已经安装了 Oracle Grid Infrastructure，则它位于 `grid_home/rpm` 目录。
- 2. 将 `cvuqdisk` 软件包复制到集群中的每个节点。您应该确保每个节点都运行相同版本的 Linux。
- 4. 使用以下命令查找您是否有已版本的 `cvuqdisk` 软件包：

```bash
# rpm -qi cvuqdisk
```

如果您已有现有版本，请输入以下命令卸载 `cvuqdisk`：

```bash
# rpm -e cvuqdisk
```

- 5. 设置环境变量 `CVUQDISK_GRP` 指向将拥有 `cvuqdisk` 的组，通常为 `oinstall`。例如：

```bash
# CVUQDISK_GRP=oinstall; export CVUQDISK_GRP
```

- 6. 在保存 `cvuqdisk` rpm 的目录下，使用以下命令安装 `cvuqdisk` 软件包：

```bash
rpm -iv package
```

例如：

```bash
# rpm -iv cvuqdisk-1.0.9-1.rpm
```

## 2.13 启用智能平台管理接口 (IPMI)

智能平台管理接口 `IPMI` 提供了一套用于计算机硬件和固件的通用接口，系统管理员可以使用这些接口监控系统健康状况并管理系统。在 Oracle 11 Release 2 中，Oracle 集群可以集成 IPMI 以提供故障隔离支持并确保集群完整性。

您可以在安装期间通过选择 IPMI 作为节点终止协议来配置节点。您也可以在安装后使用 `crctl` 命令配置 IPMI。

> 参见《集群管理与部署指南》，了解如何在安装后配置 IPMI

### 2.13.1 启用 IPMI 的要求

要能够使用 IPMI 管理集群节点，必须配置以下硬件和软件：

- 每个集群节点都需要一个运行兼容 IPMI 1.5 或更高版本的固件的基板控制器 `BMC`，支持 LAN IPMI 并配置为 LAN 远程控制。
- 每个集群节点都需要安装 IPMI 驱动程序。
- 集群需要一个用于 IPMI 的管理网络。这可以是共享网络，但 Oracle 建议配置专用网络。

## 智能平台管理接口 IPMI

- 每个集群成员用于 BMC 的以太网必须连接到 IPMI 管理网络。
- 每个集群成员必须连接到管理网络。
- 某些服务器平台在关机时会将网络接口进入节能模式。在这种情况下，它们可能以较低的速度运行（例如 100 MB 而不是 1 GB）。对于这些平台，连接到 BMC 的网络交换端口必须自动协商为较低速度，否则 IPMI 将无法正常工作。

### 2.13.2 配置 IPMI 管理网络

您可以为 BMC 配置 DHCP 或静态 IP 地址。Oracle 建议您使用 DHCP 为 BMC 配置动态 IP 地址分配。要使用此选项，您必须配置一个可以分配 BMC IP 地址的 DHCP 服务器。

> 注意：如果为 IPMI 配置静态 IP 地址，则必须确保这些地址在网络上是唯一的。

请参考您所选择的配置工具文档，了解有关使用该工具配置 BMC 的详情。

当你在每个节点上配置 BMC 时，你必须完成以下操作：

- 启用局域网 IPMI，以便通过管理网络控制 BMC。
- 使用 DHCP 或 GNS 启用动态 IP 地址，或为 BMC 配置静态 IP 地址。
- 为 BMC 建立管理员用户账户和密码。
- 如果您在标记的 VLAN 上使用 BMC，请为 BMC 配置 VLAN 标签。

您使用的配置工具并不重要，但为了确保 BMC 正常运行，必须满足这些条件。

### 2.13.3.2 使用 IPMitool 配置 BMC 示例

以下是使用 `ipmitool`（版本 1.8.6）配置 BMC 的示例。

- 1. 以 root 身份登录。
- 2. 使用 `bmc info` 命令通过 IPMI 驱动验证 `ipmitool` 是否能与 BMC 通信，并在输出中查找设备 ID。例如：

```
# ipmitool bmc info             : 32
Device ID
```

如果 `ipmitool` 未与 BMC 通信，请查看第 2-64 页的“配置 Open IPMI 驱动”部分，并确保 IPMI 驱动正在运行。
- 3. 使用以下步骤启用局域网 IPMI：
  - 确定用于局域网 IPMI 通道的通道号。从通道 1 开始，运行以下命令，直到找到显示 LAN 属性（例如 IP 地址）的通道：

```
# ipmitool lan print 1

IP Address Source      : 0x01
IP Address            : 140.87.155.59
```

  - 为找到的通道开启 LAN 访问。例如，当通道为 1 时：

`# ipmitool lan set 1 access on`

- 4. 使用以下步骤之一为 IPMI 配置 IP 地址设置：
  - 动态 IP 地址 `DHCP`

动态 IP 地址是 Oracle 通用安装程序（Universal Installer）的默认假设。Oracle 建议选择此选项，以便更容易地从集群中添加或删除节点，因为地址设置可以自动分配。

**注意：** 使用 DHCP 需要子网上有一个 DHCP 服务器。

设置通道。例如，如果通道为 1，则输入以下命令启用 DHCP：

```
# ipmitool lan set 1 ipsrc dhcp
```

- 使用静态 IP 地址



如果 BMC 与操作系统共享网络连接，则 IP 地址也必须在相同的子网上。你不仅需要设置 IP 地址，还需要设置网络掩码和默认网关的正确值。例如，假设通道为 1：

```
# ipmitool lan set 1 ipaddr 192.168.0.55
# ipmitool lan set 1 netmask 255.255.255.0
# ipmitool lan set 1 defgw ipaddr 192.168.0.1
```

注意，指定的地址 `192.168.0.55` 将仅与 BMC 相关，且不会响应正常的 ping。

### 5. 使用以下步骤建立带有用户名和密码的管理员账户（假设通道为 1）：

- a. 设置 BMC 在通过局域网访问 ADMIN 时需要密码认证。例如：

`# ipmitool lan set 1 auth MD5, PASSWORD`

- b. 列出 BMC 上的插槽，并识别一个未使用的插槽（名称字段为空的用户 ID）。

```
# ipmitool getchannel 1
```

User ID : 4

User Name : 

Fixed Name : 

Access Available : call-in / callback

Link Authentication : disabled

IPMI Messaging : disabled

Privilege Level : NO ACCESS

- c. 为识别出的插槽分配管理员用户名和密码并启用消息（注意 v1.5 的用户名和密码最多为 16 个字符）。此外，将局域网（通道 1）的权限级别设置为 ADMIN（4）。例如，用户名为 admin，密码为 password：

```
# ipmitool user set 1 username
# ipmitool user set 1 password
# ipmitool user set 1 enable on
# ipmitool user set 1 access on
# ipmitool user set 1 privilege 4
```

- d. 使用命令验证设置。输出应类似于：

## 2.14 安装期间自动 SSH 配置

为了安装 Oracle 软件，应在集群节点之间建立安全 Shell `SSH` 连接。OUI 使用 `ssh` 和 `scp` 命令在远程节点上运行命令并将文件复制到其他节点。

**注意：** Oracle Grid Infrastructure 安装需要 SSH。Oracle Enterprise Manager 也使用 SSH。

在某些情况下，当远程节点关闭 SSH 连接时，Oracle 集群安装在“Attach-Home”操作可能会失败。为了避免此问题，请在所有集群节点的 SSH 守护进程配置文件 `/etc/ssh/sshd_config` 中设置以下参数以实现无限超时：

```
LoginGraceTime 0
```

另参见：如何在配置文件中使用 `stty` 命令以防止终端引起的错误

## 2.15 配置 Grid Infrastructure 所有者用户环境

你使用 Oracle Grid Infrastructure 安装所有者账户（`oracle` 或 `grid`）运行安装程序。但在启动安装程序之前，你必须配置安装所有者账户的环境。如果需要，还要创建其他软件所有者。

本节包含以下主题：

- Grid Infrastructure 软件所有者环境
- 配置 Oracle 软件所有者环境的步骤
- 检查 Oracle 软件安装用户的资源限制
- 显示和 X11 设置
- 防止终端引起的错误

### 2.15.1 Grid Infrastructure 软件所有者环境

你必须进行以下更改以配置 Oracle Grid Infrastructure 软件所有者环境：

- 在 shell 启动文件中设置安装软件所有者（`grid`, `oracle`）的默认文件创建掩码（`umask`）。将掩码设置为 `022` 可以确保执行软件安装的用户创建的文件具有 `644` 权限。

## 21.5.2 配置 Oracle 软件所有者环境的

要选择 Oracle 软件所有者的环境，请针对每个软件所有者（`grid`, `oracle`）执行以下步骤：

- 1. 启动一个新的终端会话；例如，启动 X 终端 (`xterms`)。

- 2. 输入以下命令以确保 X Window 应用程序可以在系统上显示：

```bash
$ host + hostname
```

*hostname* 是本地主机的名称。

- 3. 如果您尚未登录到要安装软件的系统，请以软件所有者用户身份登录该系统。

- 4. 如果您未以该用户身份登录，请切换到您正在配置的软件所有者用户。例如，使用 `grid` 用户：

```bash
$ grid
```

- 5. 要确定用户的默认 shell，输入以下命令：

```bash
$ echo SHELL
```

- 6. 使用任何文本编辑器打开用户的启动文件：

  * Bash shell (`bash`):

```bash
$ vi .bash_profile
```

  * Bourne shell (`sh`) 或 Korn shell (`ksh`):

```bash
$ vi .profile
```

  * C shell (`csh` 或 `tsh`):

```bash
% vi .login
```

- 7. 输入或编辑以下行，指定默认文件模式创建掩码值为 `022`：

```bash
umask 022
```

- 8. 如果文件中设置了 `ORACLE_SID`、`ORACLE_HOME` 或 `ORACLE_BASE` 环境变量，请从文件中删除这些行。

- 9. 保存文件并退出文本编辑器。

- 10. 欲要运行 shell 启动脚本，请输入以下命令之一：

  * Bash shell:

```bash
$ ./.bash_profile
```

  * Bourne, Bash 或 Korn shell:

```bash
$ ./.profile
```

- 为安装软件所有者（`grid`, `oracle`）设置文件描述符的未设置限制限制

- 在准备安装 Oracle Grid Infrastructure 之前，设置软件所有者的环境变量 `DISPLAY` 变量

- C shell:

  % source ./.login

- 11. 如果您不是在本地系统上安装软件，请输入类似下面的命令，将 X 应用程序显示在本地系统上：

  - Bourne 或 Korn shell:

  $ DISPLAY=local_host:0.0 : export DISPLAY

  - C shell:

  % setenv DISPLAY local_host:0.0

在此示例中，`local_host` 是您想要显示安装程序的主机名或 IP 地址（您的工作站或其他客户端）。

- 12. 如果您确定 `/tmp` 目录的可用空间小于 1 GB，请识别一个至少有 1 GB 可用空间的文件系统，并设置 `TMP` 和 `TMPDIR` 环境变量指定此系统上的临时目录：

> **注意：** 安装 Oracle RAC 时，不能使用共享文件系统作为临时目录（通常为 `/tmp`）的位置。如果您将 `/tmp` 放在共享文件系统上，则安装将失败。

- a. 使用 `-h` 命令识别具有足够空间的文件系统。

- b. 如必要，输入类似下面的的命令在您识别的文件系统上创建临时目录，并对该目录设置适当权限：

```
$ su root
# mkdir /mount_point/tmp
# chmod 775 /mount_point/tmp
# exit
```

- c. 输入类似下面的的命令设置 TEMP 和 TMPDIR 环境变量：

  - Bourne, Bash 或 Korn shell:

  $ TMP=/mount_point/tmp

  $ TMPDIR=/mount_point/tmp

  $ export TMPDIR

  - C shell:

  % setenv TEMP /mount_point/tmp

  % setenv TMPDIR /mount_point/tmp

- 13. 要验证环境设置正确，输入以下命令：

```
$ umask
$ env | more
```

验证 `umask` 命令显示值为 `22`、`022` 或 `0022`，并且在本节中设置的环境变量值正确。

### 2.15.3 Oracle 软件安装用户的资源限制

对于每个安装软件所有者，使用以下推荐范围检查资源限制：

表 2-12 安装者资源限制范围

| 资源 | Shell 限制 | 软限制 | 硬限制 |
| --- | --- | --- | --- |
| 文件描述符 | `nofile` | 至少 1024 | 至少 65536 |
| 用户可用进程数 | `nproc` | 至少 2047 | 至少 16384 |
| 进程栈大小 | `stack` | 至少 10240 KB | 至少 32768 KB |

要检查资源限制：

- 1. 以安装者身份登录。



- 2. 检查文件描述符的软硬限制。确保结果在推荐范围内。例如：

```
$ uimit -Sn
1024
$ uimit -Hn
65536
```

- 3. 检查可用进程数的软硬限制。确保结果在推荐范围内。例如：

```
$ uimit -Su
2047
$ uimit -Hu
16384
```

- 4. 检查栈设置的软限制。确保结果在推荐范围内。例如：

```
$ uimit -Ss
10240
$ uimit -Hs
32768
```

- 5. 为每个 Oracle 软件安装者重复此过程。

### 2.15.4 显示和转发配置

如果您位于远程终端，本地节点只有一个显示界面（这是典型的），请使用以下语法设置 `DISPLAY` 环境变量：Bourne, Korn 和 Bash shell

```
$ export DISPLAY=hostname:
```

C shell:

```
$ setenv DISPLAY hostname:0
```

例如，如果您使用 Bash shell 且您的主机名为 `node`，请输入以下命令：

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

在安装 Oracle Grid Infrastructure 时，OUI 使用 `SSH` 执行命令并复制文件到其他节点。安装期间，系统上的隐藏文件（例如 `.bashrc` 或 `.cshrc`）。

安装期间，如果您的主机名为 `node`，请执行以下命令：

当您的主机名为 `node` 时，请执行以下命令：

## 2.17 集群名称要求

集群名称长度至少为 1 个字符，最多 15 个字符，必须包含字母和数字，不能以数字开头，并可以包含连字符 (`-`)。

在典型安装中，你提供的 SCAN 也是集群名称，因此 SCAN 必须满足集群名称的要求。在高级安装中，SCAN 和集群名称在安装期间分别在不同的字段中输入，因此集群名称的要求不适用于 SCAN 名称。

## 3 为集群和 Oracle RAC 配置 Oracle Grid Infrastructure 存储

本章描述了你在启动安装程序安装 Oracle Clusterware 和 Oracle 自动存储管理 (`Oracle ASM`) 之前必须完成的存储配置任务，同时也描述了在向集群中添加 Oracle 实时应用集群 (`Oracle RAC`) 安装之前必须完成的任务。

本章包含以下主题：

- 审核 Oracle Grid Infrastructure 存储选项
- 共享文件系统存储配置
- Oracle 自动存储管理存储配置
- 对块设备（Block Devices）和原始设备（Raw Devices）的支持
- 在 IBM: Linux on System z 上配置原始逻辑卷

## 3.1 审核 Oracle Grid Infrastructure 存储选项

本节描述了用于集群 Oracle Grid Infrastructure 存储的支持选项。它包含以下章节：

- Oracle Clusterware 和 Oracle RAC 存储选项概述
- Oracle ACFS 和 Oracle ADVM 支持
- 关于 Oracle ACFS 的通用信息
- Oracle Grid Infrastructure 和 Oracle RAC 的通用存储考虑
- 使用 Oracle ASM 组进行存储的指南
- 在 Oracle Grid Infrastructure 和 Oracle RAC 中使用逻辑卷管理器
- 支持的存储选项



- 在选择磁盘存储选项后

> 另：请访问 My Oracle Support 上的 Oracle 认证网站获取有关认证存储选项的最新信息：

```
https://support.oracle.com
```

### 3.1.1 Oracle Clusterware 和 Oracle RAC 存储选项概述

存储 Oracle Clusterware 文件有两种方式：

- Oracle 自动存储管理 (Oracle ASM)：你可以在 Oracle ASM 磁盘组中安装 Oracle Clusterware 文件（集群注册和投票磁盘文件）。

`Oracle ASM` 是典型安装以及标准版（Standard Edition）`Oracle RAC` 安装所需的数据库存储选项。它是一个用于 Oracle Clusterware 和 Oracle 数据库文件的集成式、高性能的数据库文件系统和磁盘管理器。它会自动对数据库文件进行条带（striping）和镜像（mirroring）处理。

- 支持的共享文件系统：支持的文件系统包括以下：

  - 网络文件系统 (`NFS`)：注意：如果你需要为数据文件使用 `NFS`，那么在创建 Oracle Grid Infrastructure 分区时，应创建足够大的容纳数据库文件的分区。`NFS` 对于软件二进制文件、Oracle Clusterware 和数据库文件的挂载方式有所不同。

注意：不支持在集群文件系统上放置集群 Oracle Grid Infrastructure 二进制文件。

你不再可以使用 UI 在块设备或原始设备上安装 Oracle Clusterware 或 Oracle 数据库文件。

另见：访问 My Oracle Support 支持的文件系统以及 `NFS` 或 `NAS` 光纤。

### 3.1.2 Oracle ACFS 和 Oracle ADVM 支持

自动存储管理集群文件系统 (`Oracle ACFS`) 将 Oracle ASM 技术扩展到支持单机和集群配置下的所有应用程序数据。Oracle 自动存储管理动态卷管理器 (`Oracle ADVM`) 提供卷管理服务和标准的磁盘驱动接口，通过 Oracle 自动存储管理动态卷管理器接口为支持 Oracle ASM 的客户端 Oracle 存储管理集群文件提供提供。

`Oracle ACFS` 和 `Oracle ADVM` 支持 `Oracle Linux 5` 和 `Red Hat Enterprise Linux 5`（适用于 Linux x86 和 x86-64）。表 3-1 列出了支持 `Oracle ACFS` 和 `Oracle ADVM` 的版本、平台和内核版本。

| 版本 | 平台/操作系统 |

| :--- | :--- |

| 11.2.x | Linux x86: Oracle Linux 5 和 Red Hat Enterprise Linux 5 | 2.6.18 及对 2.6.18 的后续更新 |

| 11.2.0.1 | Linux x86-64: Oracle Linux 5 和 Red Hat Enterprise Linux 5 | 2.6.18 |

### 3.1.3 关于 Oracle ACFS 的通用信息

自动存储管理集群文件系统 (`Oracle ACFS`) 将 Oracle ASM 技术扩展到支持单机和集群配置下的所有应用程序数据。Oracle 自动存储管理动态卷管理器 (`Oracle ADVM`) 提供卷管理服务和标准的磁盘驱动接口，通过 Oracle 自动存储管理动态卷管理器接口为支持 Oracle ASM 的客户端 Oracle 存储管理集群文件系统提供。

`Oracle ACFS` 和 `Oracle ADVM` 支持 `Oracle Linux 5` 和 `Red Hat Enterprise Linux 5`（适用于 Linux x86 和 x86-64）。表 3-1 列出了支持 `Oracle ACFS` 和 `Oracle ADVM` 的版本、平台和内核版本。

*(注：此处表格内容与前文重复或存在乱码，已根据翻译要求保持格式对齐)*

# 审核 Oracle Grid Infrastructure 存储选项

在安装 Oracle Grid Infrastructure 期间，您可以创建一个磁盘组。在 Oracle Grid Infrastructure 安装完成后，您可以使用 `ASMCA`、`SQL*Plus` 或 `ASMCMD` 创建额外的磁盘组。请注意，对于 Oracle Database 11g Release版 2 (11.2) 及更高版本，Oracle 数据库配置助手 (`DBCA`) 并不具备为 ASM 创建磁盘组的功能。

如果您在安装完 Oracle Grid Infrastructure 之后安装 Oracle Database 或 Oracle RAC，您可以使用同一个磁盘组用于数据库文件、OCR 和投票文件（voting files），也可以使用不同的磁盘组。如果在安装 Oracle RAC 之前或创建数据库之前创建了多个磁盘组，您可以决定采取以下操作之一：

如果您仅为存储创建一个磁盘组，则 OCR 和投票磁盘文件、数据库文件和恢复文件都包含在这一个磁盘组中。如果您为存储创建了多个磁盘组，则可以选择将文件放置在不同的磁盘组中。

Oracle Grid Infrastructure 和 Oracle RAC 仅支持集群感知的卷管理器。这意味着，您需要使用与特定厂商集群解决方案兼容的卷管理器。要确认您想要使用的卷管理器是否受支持，请查看 My Oracle Support 上的 Certifications 标签页，确认相关的集群解决方案是否通过 Oracle RAC 认证。My Oracle Support 的地址如下：

下表显示了用于存储 Oracle Clusterware 和 Oracle RAC 文件的存储选项。

为集群和 Oracle RAC 的 Oracle Grid Infrastructure 配置存储 3-5 页

# 审核 Oracle Grid Infrastructure 存储选项

**注意：** 有关 `OCFS2` 的信息，请参考以下网站：

```
http://oss.oracle.com/projects/ocfs2/
```

如果您计划在共享的 `OCFS2` 位置上安装 Oracle RAC 环境，则必须将 `OCFS2` 升级到至少 1.4.1 版本，该版本支持共享可写 smaps。

有关 `OCFS2` 集群认证以及其他集群文件系统支持，请参考 My Oracle Support 上的 Certify 页面。

## 表 3–2 Oracle Cluster 和 Oracle RAC 支持的存储选项

| 存储选项 | OCR 和投票磁盘文件 | Oracle Cluster 二进制文件 | Oracle RAC 二进制文件 | Oracle 数据库文件 | Oracle 恢复文件 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| Oracle 自动存储管理 (Oracle ASM) |  |  | 否 | 是 | 是 |

| Oracle 自动管理集群文件系统 (Oracle ACFS) |  |  | 是 | 否 | 否 |

| 本地文件系统 | 是 | 是 | 是 | 是 | 是 |

| 认证 NAS 文件服务器上的 NFS 文件系统 | | | | | |

| 共享磁盘分区（设备或原始设备） | OUI 或 ASMCA 不支持，但软件支持。它们可以在安装后添加或删除。 | No | OUI 或 ASMCA 不支持，但软件支持。它们可以在安装后添加或删除。 | No | |

选择存储选项时请遵循以下指南：

- 您可以为每种文件类型选择任何存储选项的组合，只要满足所选存储选项的所有要求。

- 您可以使用 ASM 11g Release 2 (11.2) 及更高版本存储 Oracle Cluster 文件。您无法使用先前的 Oracle ASM 版本来实现此功能。

- 如果您没有提供外部文件冗余的存储选项，则必须配置至少三个投票磁盘位置和至少三个 Oracle 集群注册（OCR）位置以提供冗余。

### 3.1.8 在您选择磁盘存储选项后

当您确定了磁盘存储选项后，请配置共享存储：

- 要使用文件系统，请参考第 3-7 页的共享文件系统存储配置。

- 要使用 Oracle 自动存储管理，请参考第 3-34 页的“在 Oracle ASM 上使用数据库磁盘组”。

3-6 Oracle Grid Infrastructure 安装指南

### 3.2 共享文件系统存储配置

安装程序未为 Oracle 集群注册 (`OCR`) 或 Oracle Clusterware 投票磁盘建议默认位置。如果您选择在文件系统中创建这些文件，请查看以下章节以完成 Oracle Clusterware 的存储需求：

- 使用共享文件系统的要求

- 决定为 Oracle Clusterware 使用集群文件系统

- 决定为数据文件使用 Direct NFS

- 决定为数据文件使用 NFS

- 配置 NFS 挂载和缓冲区大小参数

- 检查 Oracle Clusterware 的 NFS 挂载和缓冲区大小参数



- 检查 Oracle RAC 的 NFS 挂载和缓冲区大小参数
- 启用 Direct NFS 磁盘管理器控制 NFS
- 在 Direct NFS 上启用混合列式压缩
- 在共享文件系统上为 Oracle Clusterware 文件创建目录
- 在共享文件系统上为 Oracle 数据库文件创建目录
- 禁用 Direct NFS 磁盘管理器控制 NFS

> 注意：OCR 是一个包含集群配置信息和状态的文件。安装程序在安装 Oracle Clusterware 期间会自动初始化 OCR。数据库配置助手使用 OCR 来存储其创建的集群数据库的配置。

### 3.2.1 使用共享文件系统的要求

要为 Oracle Clusterware、Oracle ASM 和 Oracle RAC 使用共享文件系统，文件系统必须符合以下要求：

- 要使用 NFS 文件系统，它必须是支持的 NAS 设备。通过以下 URL 登录 Oracle Support，点击 Certification 标签页查找有关支持的 NAS 设备的最新信息：

`https://support.oracle.com`

- 如果您选择将 Oracle 集群注册 (OCR) 文件放置在共享文件系统中，则 Oracle 建议至少满足以下一点：

  - 用于文件系统的磁盘位于高可用存储设备上（例如 RAID 设备）。
  - 至少挂载了两个文件系统，并使用 Cluster1g Release 2 为 OCR 提供冗余。
  - 用于文件系统的磁盘位于高可用存储设备上（例如 RAID 设备）。
  - 挂载了至少两个文件系统，数据库文件位于其中一个文件系统，恢复文件位于另一个文件系统。

- 执行安装的用户帐户必须对您指定的路径具有写入权限。

> 注意：不支持从 Oracle9 release 2 使用原始设备或共享文件升级 OCR。如果您正在升级 Clusterware，且现有集群使用 100 MB OCR 和 20 MB 投票分区，则必须将这些分区扩展到 300 MB。Oracle 建议不要使用分区，而是将 OCR 和投票磁盘放在磁盘组。所有存储产品必须由您的服务器和存储厂商支持。

使用表 3-3 和表 3-4 确定文件系统的最小大小：

| 表 3-3 Oracle Cluster 共享文件系统卷要求 |  | 卷数量 | 卷大小 |
| :--- | :--- | :--- | :--- |
| 具有外部冗余的投票磁盘 | 3 | 每个投票磁盘卷至少 300 MB |
| 具有外部冗余的集群注册 (OCR) | 1 | 每个 OCR 卷至少 300 MB |
| 提供的 Clusterware 文件（OCR 和投票磁盘） | 1 | 每个 OCR 卷至少 300 MB，每个投票磁盘卷至少 300 MB |

| 表 3-4 Oracle RAC 共享文件系统卷要求 | | | |
| 存储的文件类型 | 卷数量 | 卷大小 |
| :--- | :--- | :--- | :--- |
| Oracle 数据库文件 | 1 | 每个卷至少 1.5 GB |
| 恢复文件 | 1 | 每个卷至少 2 GB |

在表 3-3 和表 3-4 中，所需的卷大小是累积的。例如，为了在共享文件系统中存储所有 Oracle Cluster 文件并提供常规冗余，您至少需要 2 GB 的可用存储，分布在三个位置（OCR 的三个独立卷位置及两个 OCR 镜像，每个卷一个投票磁盘）。您应该至少有三个物理磁盘，每个至少 500 MB，以确保投票磁盘和 OCR 文件位于不同的物理磁盘。如果您使用一个卷用于数据库文件和另一个卷用于添加 RAC，

3-8 Oracle Grid Infrastructure 安装指南

恢复文件，那么您在两个卷上至少应该有 3.5 GB 的可用存储，并且所有卷上至少有 5.5 GB 的可用空间。

> 注意：如果您使用 `fdisk` 通过指定设备大小（例如 +30%）在共享分区上创建分区，根据磁盘的圆柱几何结构，实际创建的设备可能比请求的尺寸小。这是由于目前的磁盘限制。Oracle 建议您对分配给 Oracle ASM 的整个磁盘进行分区。

## 3.2.2 解码以使用集群文件系统用于 Oracle 集群文件

对于新安装，Oracle 建议您使用 Oracle 自动存储管理 (Oracle ASM) 来存储投票磁盘和 OCR 文件。对于 Linux x86 (32位) 和 x86-64 (64位) 平台，Oracle 提供了一个集群文件系统 OCFS2。然而，Oracle 不建议对集群文件文件使用 OCFS2。

## 3.2.3 决定对数据文件使用 Direct NFS

Direct NFS 客户端是使用内核管理 NFS 的替代方案。本节包含有关 Direct NFS 客户端的信息：

- 关于 Direct NFS 客户端存储
- 使用 `oranstab` 文件配合 Direct NFS Client
- 使用 Direct NFS 客户端挂载 NFS 存储设备
- 使用 `oranstab` 指定网络路径

### 3.2.3.1 关于 Direct NFS 客户端存储

在 Oracle Database 11g Release 2 中，您无需使用操作系统内核 FS 客户端，而是配置 Oracle Database 使用 Oracle 内部 Direct NFS 客户端直接访问 NFS V3 服务器。

要启用 Oracle Database 使用 Direct NFS 客户端，在开始安装之前，NFS 文件必须通过常规 NFS 挂载进行挂载并可用。Direct NFS 在安装后管理设置。您应该将内核挂载选项作为备份，但对于正常操作，Direct NFS 客户端将管理 NFS 挂载。

请参考您的供应商文档完成 NFS 配置和挂载。某些 NFS 服务器要求 NFS 客户端使用保留端口连接。如果您的 NFS 服务器在开启了保留端口检查的情况下运行，则您必须禁用它以便 Direct NFS 客户端运行。禁用保留端口检查，以确保您的 NFS 服务器文档正常工作。

对于限制 root 端口的服务器，您可以使用 `insecure` 选项允许 root 以外的客户端连接到 NFS 服务器。或者，您可以按照第 3.2.12 节“禁用 Direct NFS 客户端 Oracle 磁盘管理 NFS 集群”所述禁用 Direct NFS 客户端。

> 注意：使用支持 Oracle RAC 的 NFS 服务器。请参考以下 URL 获取支持信息：`https://support.oracle.com`

为集群和 Oracle RAC 的 Oracle Grid Infrastructure 配置存储

### 3.2.3.2 使用 oranstab 文件配合 Direct NFS Client

如果您使用 Direct NFS 客户端，则可以选择使用一个新文件 `oranstab` 进行 Oracle 数据文件管理，以指定针对 Oracle Database 到 Direct NFS 客户端的特定选项。例如，您可以使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

> 另参见第 3.2.3.5 节“配置存储 NFS 挂载和缓冲区参数”，获取有关配置 `/etc/fstab` 的信息

在所有情况下，挂载点必须由内核 NFS 系统挂载，即使它们在使用 Direct NFS 客户端提供服务。

> 警告：Direct NFS 客户端不会为写入大小 (`wtmax`) 小于 32768 的 NFS 服务器服务。

### 3.2.3.3 使用 Direct NFS 客户端挂载 NFS 存储设备

Direct NFS 客户端根据 `/etc/mtab` 中的配置确定 NFS 存储设备的挂载点设置，这些配置是随着配置 `/etc/fstab` 文件更改的。

Direct NFS 客户端按以下顺序搜索挂载条目：

1. `$ORACLE_HOME/dbms/oranstab`
2. `/etc/oranstab`
3. `/etc/mtab`

Direct NFS 客户端使用第一个匹配的条目。Oracle Database 默认不启用 Direct NFS。要启用 Direct NFS 客户端，请执行以下步骤：

1. 切换目录到 `$ORACLE_HOME/dbms/lib`。



## 2. 输入以下命令：

```
make -f ins_rdms.mk dnfs_on
```

> 注意：每个实例只能有一个活动的 Direct NFS 客户端实现。在另一个实例上使用 Direct NFS 客户端将阻止另一个实现。

## 共享文件系统存储配置

如果 Oracle Database 使用通过 `oranstab` 配置的挂载点，则可以使用新文件 `oranstab` 来指定针对 Oracle Database 到 Direct NFS 客户端的额外选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则您必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

## 3.2.4 决定对数据文件使用 Direct NFS

Direct NFS 客户端是使用内核管理 NFS 的替代方案。本节包含有关 Direct NFS 客户端的信息：

- 关于 Direct NFS 客户端存储
- 使用 `oranstab` 文件配合 Direct NFS Client
- 使用 Direct NFS 客户端挂载 NFS 存储设备
- 使用 `oranstab` 指定网络路径

### 3.2.3.1 关于 Direct NFS 客户端存储

在 Oracle Database 11g Release 2 中，您无需使用操作系统内核 FS 客户端，而是配置 Oracle Database 使用 Oracle 内部 Direct NFS 客户端直接访问 NFS V3 服务器。

要启用 Oracle Database 使用 Direct NFS 客户端，在开始安装之前，NFS 文件必须通过常规 NFS 挂载进行挂载并可用。Direct NFS 在安装后管理设置。您应该将内核挂载选项作为备份，但对于正常操作，Direct NFS 客户端将管理 NFS 挂载。

请参考您的供应商文档完成 NFS 配置和挂载。某些 NFS 服务器要求 NFS 客户端使用保留端口连接。如果您的 NFS 服务器在开启了保留端口检查的情况下运行，则您必须禁用它以便 Direct NFS 客户端运行。禁用保留端口检查，以确保您的 NFS 服务器文档正常工作。

对于限制 root 端口的服务器，您可以使用 `insecure` 选项允许 root 以外的客户端连接到 NFS 服务器。或者，您可以按照第 3.2.12 节“禁用 Direct NFS 客户端 Oracle 磁盘管理 NFS 集群”所述禁用 Direct NFS 客户端。

> 注意：使用支持 Oracle RAC 的 NFS 服务器。请参考以下 URL 获取支持信息：`https://support.oracle.com`

为集群和 Oracle RAC 配置 Oracle Grid Infrastructure 3-9

### 使用 `oranstab` 文件配合 Direct NFS Client

如果您使用 Direct NFS 客户端，则可以选择使用一个新文件 `oranstab` 进行 Oracle 数据文件管理，以指定针对 Oracle Database 到 Direct NFS 客户端的特定选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。



在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则您必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

> 另参见第 3.2.3.5 节“配置存储 NFS 挂载和缓冲区参数”，获取有关配置 `/etc/fstab` 的信息

在所有情况下，挂载点必须由内核 NFS 系统挂载，即使它们在使用 Direct NFS 客户端提供服务。

> 警告：Direct NFS 客户端不会为写入大小 (`wtmax`) 小于 32768 的 NFS 服务器服务。

### 使用 Direct NFS 客户端挂载 NFS 存储设备

Direct NFS 客户端根据 `/etc/mtab` 中的配置确定 NFS 存储设备的挂载点设置，这些配置是随着配置 `/etc/fstab` 文件更改的。

Direct NFS 客户端按以下顺序搜索挂载条目：

1. `$ORACLE_HOME/dbms/oranstab`
2. `/etc/oranstab`
3. `/etc/mtab`

Direct NFS 客户端使用第一个匹配的条目。Oracle Database 默认不启用 Direct NFS。要启用 Direct NFS 客户端，请执行以下步骤：

1. 切换目录到 `$ORACLE_HOME/dbms/lib`。
2. 输入以下命令：

```
make -f ins_rdms.mk dnfs_on
```

> 注意：每个实例只能有一个活动的 Direct NFS 客户端实现。在另一个实例上使用 Direct NFS 客户端将阻止另一个实现。

### 共享文件系统存储配置

如果 Oracle Database 使用通过 `oranstab` 配置的挂载点，则可以使用新文件 `oranstab` 来指定针对 Oracle Database 到 Direct NFS 客户端的额外选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则您必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

要启用 Oracle Database 使用 Direct NFS 客户端，要启用 Oracle Database 使用 Direct NFS 客户端，在开始安装之前，NFS 文件必须通过常规 NFS 挂载进行挂载并可用。Direct NFS 在安装后管理设置。您应该将内核挂载选项作为备份，但对于正常操作，Direct NFS 客户端将管理 NFS 挂载。

请参考您的供应商文档完成 NFS 配置和挂载。某些 NFS 服务器要求 NFS 客户端使用保留端口连接。如果您的 NFS 服务器在开启了保留端口检查的情况下运行，则您必须禁用它以便 Direct NFS 客户端运行。禁用保留端口检查，以确保您的 NFS 服务器文档正常工作。

对于限制 root 端口的服务器，您可以使用 `insecure` 选项允许 root 以外的客户端连接到 NFS 服务器。或者，您可以按照第 3.2.12 节“禁用 Direct NFS 客户端 Oracle 磁盘管理 NFS 集群”所述禁用 Direct NFS 客户端。

> 注意：使用支持 Oracle RAC 的 NFS 服务器。请参考以下 URL 获取支持信息：https://support.oracle.com

为集群和 Oracle RAC 配置 Oracle Grid Infrastructure 3-9

### 使用 oranstab 文件配合 Direct NFS Client

如果您使用 Direct NFS 客户端，则可以选择使用一个新文件 `oranstab` 进行 Oracle 数据文件管理，以指定针对 Oracle Database 到 Direct NFS 客户端的特定选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

在使用 Oracle RAC 时，当 `oranstab` 文件放置在 `$ORACLE_HOME/dbms` 时，文件中的条目特定于共享数据库。在这种情况下，所有运行 Oracle RAC 的节点使用相同的 `$ORACLE_HOME/dbms/oranstab` 文件。在非共享 Oracle RAC 安装中，`oranstab` 必须在所有节点上进行复制。

当 `oranstab` 文件放置在 `/etc` 时，它可以包含集群节点上运行的所有 Oracle 数据库使用的挂载点，包括独立数据库。然而，在 Oracle RAC 系统上，如果 `oranstab` 文件放置在 `/etc`，则您必须在所有节点上同步每个 `/etc/oranstab` 文件，就像您必须处理 `/etc/fstab` 一样。

### 使用 Direct NFS 客户端挂载 NFS 存储设备

Direct NFS 客户端根据 `/etc/mtab` 中的配置确定 NFS 存储设备的挂载点设置，这些配置是随着配置 `/etc/fstab` 文件更改的。

Direct NFS 客户端按以下顺序搜索挂载条目：

1. `$ORACLE_HOME/dbms/oranstab`
2. `/etc/oranstab`
3. `/etc/mtab`

Direct NFS 客户端使用第一个匹配的条目。Oracle Database 默认不启用 Direct NFS。要启用 Direct NFS 客户端，请执行以下步骤：

1. 切换目录到 `$ORACLE_HOME/dbms/lib`。
2. 输入以下命令：

```
make -f ins_rdms.mk dnfs_on
```

> 注意：每个实例只能有一个活动的 Direct NFS 客户端实现。在其他实例上使用 Direct NFS 客户端将阻止另一个实现。

## 3.2.4 决定对数据文件使用 Direct NFS

Direct NFS 客户端是使用内核管理 NFS 的替代方案。本节包含有关 Direct NFS 客户端的信息：

- 关于 Direct NFS 客户端存储
- 使用 oranstab 文件配合 Direct NFS Client
- 使用 Direct NFS 客户端挂载 NFS 存储设备
- 使用 oranstab 指定网络路径

### 共享文件系统存储配置

> 另参见第 3.2.3.5 节“配置存储 NFS 挂载和缓冲区参数”，获取有关配置 `/etc/fstab` 的信息

在所有情况下，挂载点必须由内核 NFS 系统挂载，即使它们在使用 Direct NFS 客户端提供服务。

> 警告：Direct NFS 客户端不会为写入大小 (`wtmax`) 小于 32768 的 NFS 服务器服务。

## 3.2.5 配置存储 NFS 挂载和缓冲区参数

如果 Oracle Database 使用通过 `oranstab` 配置的挂载点，则可以使用新文件 `oranstab` 来指定针对 Oracle Database 到 Direct NFS 客户端的额外选项。例如，您使用 `oranstab` 为挂载点指定额外的路径。您可以添加 `/etc` 或到 `$ORACLE_HOME/dbms`。

### 共享文件系统存储配置

**注意：** 在 Oracle Unbreakable Enterprise Linux 和 Oracle Linux 内核 2.6.32 及更高版本中，`intr` 和 `nointr` 挂载选项已弃用。

如果您在 NFS 挂上有 Grid Infrastructure 二进制文件，必须包含 `suid` 选项。

Oracle Clusterware 文件（OCR 和投票磁盘文件）的 NFS 客户端挂载选项为：



```
rw,bg,hard,nintr,size=32768,wsize=32768,tcp,noacs,vers=3,time=600,acime=0
```

更新每个节点上的 `/etc/fstab` 文件，添加包含适用于平台 NFS 挂载选项的目。如果您的平台是 x86-64，且正在为 Oracle Clusterware 创建挂载点，请按照以下格式更新 `/etc/fstab`：

```
nfs_server:/vol /u2/oracle/cwfiles nfs \
rw,bg,hard,nintr,size=32768,wsize=32768,time=600,acime=0,suid
```

注意，挂载选项适用于 Oracle 软件二进制文件、Clusterware 文件（OCR 和投票磁盘）以及数据文件。

要为二进制文件创建挂载点，请提供类似于以下二进制位点的条目：

```
nfs_server:/vol /u2/oracle/grid nfs \
rw,bg,hard,nintr,size=32768,wsize=32768,vers=3,time=600,acime=0,suid
```

> **另请：** 请参阅 My Oracle Support 通知 39515.1，“用于 NAS 设备的 Oracle 文件挂载选项”，获取最新的挂载选项信息，访问以下 URL：

https://support.oracle.com

> **注意：** 请参考您的服务提供商文档获取有关挂载选项的其他信息。

## 3.2.7 检查 Oracle RAC 的 NFS 挂载和缓冲区大小参数

如果您有 NFS 挂载，必须在每个具有 Oracle RAC 实例的节点上使用特殊的挂载选项挂载 NFS 卷以存储数据库文件。在挂载 NFS 文件系统时，Oracle 建议使用与设备认证时 NAS 使用的相同的挂载选项。请参阅您的设备文档或联系您的供应商获取推荐的挂载选项。

更新每个节点上的 `/etc/fstab` 文件，添加类似于以下格式的条目：

```
nfs_server:/vol /u2/cradata /u2/cradata nfs \
rw,bg,hard,nintr,vers=3,time=600,acime=0,size=32768,wsize=32768 0 0
```

强制挂载选项必须包含在挂载 NFS 卷时必须使用的最小挂载选项集。这些选项对于保护数据完整性和防止任何数据库损坏至关重要。未使用这些挂载选项可能会导致生成文件访问错误。请参阅《为 Cluster 和 Oracle RAC 配置 Oracle Grid Infrastructure 存储》3-13 操作系统或 NAS 设备文档，以获取有关您平台支持的特定选项的更多信息。

另请：参阅 My Oracle Support 通知 359515.1 获取更新的 NAS 挂载信息，访问以下 URL：

https://support.oracle.com

## 3.2.8 启用 NFS 的 Direct NFS 客户端磁盘管理器

完成以下步骤以启用 Direct NFS 客户端：

- 1. 为每个要使用 Direct NFS 客户端的 NFS 服务器创建一个具有以下属性的 `orstab` 文件：

- `Server` (服务器): NFS 服务器名称。

- `Local` (本地): 数据库主机上的至多四个路径，通过 IP 地址或名称指定，如在数据库主机上运行 `ifconfig` 命令所示。

- `Path` (路径): 指向 NFS 服务器的最多四个网络路径，通过 IP 地址或名称指定，如在 NFS 服务器上使用 `ifconfig` 命令显示所示。

- `Export` (导出): 从 NFS 服务器导出的路径。

- `Mount` (挂载): Direct NFS 客户端在超时前应等待成功挂载的时间（秒为单位）。此参数为可选。默认超时时间为 10 分钟（600）。

- `Droute`: 指定传出的消息不应由操作系统路由，而应使用它们所绑定的 IP 地址。注意，此 POSIX 选项在路径位于相同子网的 Linux 系统上有时不起作用。

- `management` (管理): 启用 Direct NFS 客户端使用管理接口进行 SNMP 查询。如果 SNMP 运行在 NFS 服务器的独立接口上，则可以使用此参数。默认值为 1。

- `community` (团体): 指定用于 SNMP 查询的团体字符串。默认值为 `public`。

接下来的示例显示了 `orstab` 中可能的 NFS 服务器条目。单个 `orstab` 可以有多个服务器条目。

示例 3-1 使用 Local 和 Path 的 NFS 服务器

以下示例同时使用了 `local` 和 `path`。由于它们位于不同的子网，因此不需要指定 `droute`。

```
server: MyDatabaseServer
local: 192.0.2.0
path: 192.0.100.0
local: 192.0.100.0
path: 192.0.100.1
export: /vol/oradata mount: /mnt/oradata
community: private
```

示例 3-2 在同一子网中使用 Local 和 Path，并带有 droute

以下示例显示了在同一子网内的 `local` 和 `path`。在此情况下下指定了 `droute`：

```
server: MyDataServer
local: 192.0.2.0
path: 192.0.2.128
local: 192.0.2.1
path: 192.0.2.1
droute
export: /vol/oradata mount: /mnt/oradata
management: 192.0.2.128
```

示例 3-3 使用名称代替 IP 地址，并有多个导出

```
server: MyDataServer
local: LocalPath1
path: NFPath1
local: LocalPath2
path: NFPath2
local: LocalPath3
path: NFPath3
local: LocalPath4
path: NFPath4
droute
export: /vol/oradata3 mount: /mnt/oradata
export: /vol/oradata4 mount: /mnt/oradata
export: /vol/oradata5 mount: /mnt/oradata
export: /vol/oradata6 mount: /mnt/oradata
```

- 2. 默认情况下，Direct NFS 客户端以禁用状态安装。要启用 NFS 客户端，请在每个节点上完成以下步骤。如果您为集群使用了共享的 Grid home，则在共享的 Grid home 中完成以下步骤：

- a. 以 Grid 身份登录。

- b. 进入 `Grid_home/rdbms/lib`。

- c. 执行以下命令：

```
$ make -f ins_rdbms.on
```

## 3.2.11 在共享文件系统上为 Oracle 数据库创建目录

使用以下指令为 Oracle 数据库和恢复文件的共享文件系统创建目录（例如用于 Oracle RAC 数据库）。

- 1. 如必要，配置共享文件系统并将其挂载到每个节点上。

> 注意：你用于文件系统的挂载点在每个节点上必须完全相同。确保文件系统配置为在节点重启时自动挂载。

- 2. 使用 `df -h` 命令确定每个挂载文件系统的空闲磁盘空间。

3. 从显示内容中识别文件系统：

| 文件类型 | 文件系统要求 |
| --- | --- |
| 数据库文件 | 选择以下任一：

- 具有至少 1.5 GB 空闲空间的的单个文件系统。

- 两个或多个文件系统，总计至少有 1.5 GB 的空闲磁盘空间。 |
| 恢复文件 | 选择一个至少有 2 GB 空闲磁盘空间的文件系统。 |

如果你对多个文件类型使用同一个文件系统，请将每个类型的磁盘空间需求相加，以确定总空间需求。

4. 记录你识别出的文件系统的挂载点目录名称。

5. 如果执行安装的用户（通常为 `oracle`）具有在安装 Oracle 数据库的磁盘上创建目录的权限，则 `DBCA` 将自动创建 Oracle 数据库目录和恢复目录。

如果执行安装的用户没有写入权限，你必须使用类似下面的命令手动创建这些子目录，在每个挂载点目录中创建推荐的子目录，并设置适当的所有者、用户组和权限：

- 数据库目录：

```
# mkdir /mount_point/oradata
# chown oracle:install /mount_point/oradata
# chmod 775 /mount_point/oradata
```

- 恢复目录（快速恢复区域）：

```
# mkdir /mount_point/recovery_area
# chown oracle:install /mount_point/recovery_area
# chmod 775 /mount_point/recovery_area
```



通过使这些目录成为 `install` 组的成员，允许多个 `oracle` 实例（包括带有 `OSDBA` 组的实例）读取。

当你完成在每个挂载点目录中创建子目录并设置了适当的所有者、组和权限后，即已完成 Oracle 数据库共享存储的 `OCFS2` 或 `NFS` 配置。

## 3.12 禁用 Direct NFS 客户端 Oracle 磁盘管理

完成以下步骤禁用 Direct NFS 客户端：

- 以 Oracle Grid Infrastructure 所有者的身份登录，并使用以下命令禁用 Direct NFS 客户端，`Grid_home` 为 Oracle Grid Infrastructure 家目录路径：

```bash
$ cd Grid_home/rdms/lib
$ make -f ins_rdms.mk dnfs_off
```

在集群中的每个节点上执行这些命令，或者如果你为 Oracle Grid Infrastructure 安装使用共享家目录，则在共享 Grid 目录上执行。

- 移除 `oranfstab` 文件。

> 注意：如果你删除了 Oracle 数据库正在使用的 NFS 路径，必须重启数据库才能使更改生效。

## 3.3 Oracle 自动存储管理存储配置

查看以下章节以为 Oracle 自动存储管理配置存储：

- 为 Oracle 自动存储管理配置存储

- 在 Oracle ASM 上使用磁盘组配合 Oracle数据库文件

- 配置 Oracle 自动存储管理集群文件系统

- 升级现有的 Oracle ASM 实例

### 3.3.1 为 Oracle 自动存储管理配置存储

本节描述了如何为 Oracle 自动存储管理配置存储

- 识别 Oracle 自动存储管理的存储需求

- 在 NAS 设备上创建供 Oracle ASM 使用的文件

- 使用现有的 Oracle ASM 磁盘组

- 使用 ASMLIB 为 Oracle ASM 配置磁盘

- 为多路径磁盘配置 ASMLIB

- 手动为 Oracle ASM 配置磁盘

### 3.3.1 识别 Oracle 自动存储管理的存储需求

要识别使用 Oracle ASM 的存储需求，你必须确定需要多少设备以及多少空闲磁盘空间。要完成此任务，请遵循以下步骤：

- 确定你希望将 Oracle ASM 用于 Clusterware 文件（`OCR` 和投票磁盘）、Oracle 数据库文件、恢复文件，还是除 Oracle Clusterware 或 Oracle Database 二进制文件以外的所有文件。Oracle 数据库文件包括数据文件、控制文件、重做日志文件、服务器参数文件密码文件。

注意：你不需要为 Oracle Clusterware、Oracle 数据库文件和恢复文件使用相同的存储机制。你可以对一种文件类型使用共享文件系统，对另一种类型使用 ASM。

如果你选择启用自动备份且没有可用的共享文件系统，则你必须选择 ASM 进行恢复文件存储。

如果你在安装期间启用了自动备份，则可以通过为快速恢复区域指定 Oracle 自动存储管理磁盘组，来选择 Oracle ASM 作为恢复文件的存储机制。如果你选择了非交互式安装模式，默认情况下它会创建一个磁盘组并存储 OCR 和投票磁盘文件。如果你想在随后的数据库安装中拥有任何其他磁盘组，可以选择交互模式，或者在启动数据库安装之前运行 `ASMCA`（或命令行工具）创建适当的磁盘组。

- 2. 选择用于 Oracle ASM 磁盘组的 Oracle ASM 冗余级别。

你为 Oracle ASM 磁盘组选择的冗余级别取决于 Oracle ASM 如何镜像磁盘组中的文件，并决定了所需的设备数量和空闲空间，如下：

- 外部冗余

外部冗余磁盘组至少需要一个磁盘设备。外部冗余磁盘组中的有效磁盘空间是其所有设备磁盘空间之和。

对于 Clusterware 文件，外部冗余磁盘组提供外部冗余磁盘组提供 1 个投票磁盘文件。

对于大多数数据，Oracle 建议使用外部冗余技术。

- 正常冗余

正常冗余磁盘组至少需要两个磁盘设备。正常冗余磁盘组中的有效磁盘空间是其所有设备磁盘空间之和。

对于 Clusterware 文件，正常冗余磁盘组提供 2 个副本文件。

对于大多数安装，Oracle 建议使用正常冗余。

- 高冗余

高冗余磁盘组至少需要三个磁盘设备。高冗余磁盘组中的有效磁盘空间是其所有设备磁盘空间的三分之一。

### 3.3.2 Oracle 自动存储管理存储配置

对于 Clusterware 文件，高冗余磁盘组提供 5 个副本文件。在内冗余的情况下，集群可以容忍两个磁盘组的丢失。

虽然高冗余磁盘组提供了高级别的数据保护，但在选择高冗余之前，你应该考虑额外存储的成本。

- 3. 确定 Oracle Cluster 文件和恢复文件所需的总空间。

使用表 3-5 和表 3-6 确定 Oracle Cluster 文件在投票磁盘位于独立组时所需的最小磁盘数量和空间：

表 3-5 Oracle Cluster 存储需求表

| 冗余级别 | 最小磁盘数量 | Oracle 集群注册 (OCR) | 投票磁盘文件 | 所有文件类型 |
|---|---|---|---|---|
| 外部 | 1 | 300 MB | 300 MB | 600 MB |
| 正常 | 3 | 300 MB | 900 MB | 1.5 GB |
| 高 | 5 | 900 MB | 1.5 GB | 2.4 GB |

如果你在安装期间创建磁盘组，则它必须为 2 GB。

> 注意：如果投票磁盘位于磁盘组中，请注意带有 Oracle Cluster 文件（OCR 和投票文件）的组比其他磁盘组具有更高的最小故障组数量。

仲故障组是一种特殊的故障组，这些故障组中的磁盘不包含用户数据。在确定存储用户数据的冗余需求时，不考虑仲故障组。但在挂载磁盘组时，仲故障组会计数。

表 3-6 Oracle 数据库存储需求表

| 冗余级别 | 最小磁盘数量 | 数据库文件 | 恢复文件 | 所有文件类型 |
|---|---|---|---|---|
| 外部 | 1 | 1.5 GB | 3 GB | 4.5 GB |
| 正常 | 2 | 3 GB | 6 GB | 9 GB |
| 高 | 3 | 4.5 GB | 9 GB | 13.5 GB |

- 4. 确定分配单元大小。每个 Oracle ASM 磁盘都划分为分配单元（`AU`）。分配单元是磁盘组内分配的基本单位。你可以从 1, 2, 4, 8, 16, 32 或 64 中选择 AU 值。

3-20 Oracle Grid Infrastructure 安装指南

# Oracle 自动存储管理存储配置

MB，取决于特定的磁盘组兼容性级别。默认值设置为 1 MB。

5. 对于集群软件（Clusterware）安装，你还必须为 Oracle ASM 元数据添加额外的磁盘空间。你可以使用以下公式计算 OCR、投票文件以及 Oracle ASM 元数据的磁盘空间需求（MB）：

```
total = [2 * ausize disks] + [redundancy * (ausize * nodes (clients + 1) + 30) + (64 * nodes) + 533)]
```

其中：

- `redundancy` = 镜像数量：external（外部）= 1，normal（普通）= 2，high（高）= 3。

- `ausize` = 元数据 AU 大，单位为 MB（默认为 1 MB）。

- `nodes` = 集群中的节点数。

- `clients` = 每个节点的数据库实例数。

- `disks` = 磁盘组中的磁盘数。

例如，对于一个四节点的 Oracle RAC 安装，在普通冗余磁盘组中使用三块磁盘，你需要额外的 1684 MB 空间：

[2 * 1 * 3] + [2 * (4 * (4 + 1) + 30)+(64 * 4) + 533]] = 1684 MB

为了确保 Oracle ASM 上 Oracle Cluster 文件的高可用性，对于普通磁盘组，根据大多数实例的通用规则，你必须在三个故障组中至少拥有 2 GB 的磁盘空间用于 Oracle Cluster 文件，并至少包含三块物理磁盘。为了确保创建 Oracle Cluster 文件的有效空间为 2 GB，最佳实践建议确保每个磁盘的容量至少为 2.1 GB，三块磁盘的总容量为 6.3 GB。

6. 可选为 Oracle ASM 磁盘组标识故障组（failure groups）。

如果你打算使用普通或高冗余磁盘组，可以通过关联自定义故障组中的一组设备来进一步保护数据库免受硬件故障的影响。默认情况下，每个设备包含自己的故障组。然而，如果两个磁盘连接到同一个 SCSI 控制器的普通冗余磁盘组中，那么当控制器故障时，磁盘组将不可用。此示例中的控制器是一个单点故障。

为了防止此类故障，可以使用两个 SCSI 控制器，每个控制器连接两个磁盘，并为连接到每个控制器的磁盘定义故障组。这种配置将允许磁盘组容忍一个 SCSI 控制器的故障。

为集群和 Oracle RAC 配置 Oracle Grid Infrastructure 存储（3-21 版本）



# Oracle 自动存储管理存储配置

**注意：** 安装完成后，请使用 GUI 工具 `ASMCA`、命令行工具 `asmcmd` 或 SQL 命令定义自定义故障组。

如果你定义了自定义故障组，那么对于仅包含数据库文件的故障组，普通冗余磁盘组必须至少指定两个故障组，高冗余磁盘组必须至少指定三个故障组。

对于包含数据库文件和集群软件文件（包括投票磁盘）的故障组，普通冗余磁盘组必须至少指定三个故障组，高冗余磁盘组必须至少指定五个故障组。

包含投票文件的磁盘组对于普通冗余至少有 3 个故障组，对于高冗余至少有 5 个故障组。否则，最小值分别为 2 和 3。故障组的最小数量适用于是否为自定义。

- 如果你确定系统上不存在合适的磁盘组，请安装或识别适当的磁盘设备添加到新的磁盘组。在识别磁盘设备时遵循以下指南：
  - `Oracle ASM` 磁盘组中的所有设备大小应相同且具有相同的性能特性。
  - 不要将单个物理磁盘上的多个分区指定为磁盘组设备。每个磁盘组设备应位于单独的物理磁盘。
  - 虽然你在 `Oracle ASM` 磁盘组中选择逻辑值作为设备，但 Oracle 不建议这样做，因为这增加了 `Oracle ASM` 不需要的复杂性。此外，如果你决定在 `Oracle ASM` 和 `Oracle RAC` 中使用逻辑卷，`Oracle RAC` 需要逻辑卷管理器。

Oracle 建议如果选择逻辑卷管理器，请使用逻辑卷管理器表示未分拆或镜像的单个 LUN，以便减少额外存储层的影响。

## 3.3.1.2 在 NAS 设备上创建文件供 Oracle ASM 使用

如果你拥有认证的 NAS 存储设备，可以在 `NFS` 挂载目录中创建零填充文件，并将这些文件作为 `Oracle ASM` 中的磁盘设备。

要创建这些文件：
- 如果你有认证的 NAS 存储设备，可以在 `NFS` 挂载目录中创建零填充文件，并将这些文件作为 `Oracle ASM` 中的磁盘设备。



如果你有认证的 NAS 存储设备，可以在 NFS 挂载目录中创建零填充文件，并将这些文件作为 Oracle ASM 中的磁盘设备。

## 3.3.1.3 使用 ASM 磁盘组

要确定是否存在现有的存储磁盘组，或确定磁盘组中是否有足够的空间，可以使用 Oracle 命令行工具 `asmcmd`、Oracle Enterprise Manager Grid Control 或 Database Control。或者，你可以使用以下步骤：

- 1. 查看 `oratab` 文件的内容以确定系统是否配置了 Oracle ASM 实例：

```
$ /etc/oratab
```

如果 Oracle ASM 实例在系统上配置，`oratab` 文件应包含如下行：

```
+ASM2:oracle_home_path
```

在此示例中，`ASM2` 是 Oracle ASM 实例的系统标识符 `SID`，带有节点号，`oracle_home_path` 是其所在的 Oracle home 目录。按照习惯，Oracle ASM 实例的 `SID` 以加号开头。

- 2. 设置 `ORACLE_SID` 和 `ORACLE_HOME` 环境变量以为 Oracle ASM 实例指定适当的值。

- 3. 连接到 Oracle ASM 实例并启动实例，如果：

```
$ORACLE_HOME/bin/asmcmd
ASMCMD> startup
```

- 4. 输入以下命令之一查看现有磁盘组、它们的冗余级别以及每个磁盘组的可用空间：

```
ASMCMD> lsdg
```

或：

```
$ORACLE_HOME/bin/asmcmd -p lsdg
```

- 5. 从输出中，识别具有适当冗余级别的磁盘组，并记录其包含的可用空间。

- 6. 如果必要，安装或识别满足上一节列出的存储要求的额外磁盘设备。



## Oracle 自动存储管理存储配置

**注意：** 如果您正在向现有磁盘组添加设备，Oracle 建议使用与该磁盘组中现有设备大小和性能相同的设备。

### 3.3.1.4 使用 ASMLIB 为 Oracle ASM 配置磁盘

Oracle 自动存储管理（Oracle ASM）库驱动程序简化了设备的配置和管理，因为它消除了每次系统重启时都需要重新绑定 Oracle ASM 使用的磁盘设备的需求。

如果没有 ASMLIB，Linux 2.6 内核和加载程序，除非在每个集群成员节点上创建权限或规则文件，否则设备路径不会保持权限和路径持久性；例如 `/dev/sda` 在重启后可能会显示为 `/dev/sdb`。添加新设备需要您使用 udev 文件为新磁盘提供权限和路径持久性。

使用 ASMLIB，可以定义希望作为 Oracle ASM 磁盘使用的磁盘范围。ASMLIB 维护持久化在存储设备上的权限和磁盘标签，因此即使在操作系统升级后，该标签仍然可用。您可以通过在每个节点上运行一个 `oracleasm` 命令来更新所有集群成员节点上的存储路径。

如果您打算在 Linux 上使用块设备进行数据库存储的 Oracle ASM，Oracle 建议您安装 ASMLIB 驱动程序相关工具，并使用它们为 Oracle ASM 配置磁盘。

> **警告：** 在 IBM: Linux on System 服务器上，由于块兼容性问题，对于 Oracle Grid Infrastructure 11.2.0.1 及更高版本，无法配合 SCSI 存储设备和光纤通道（FCP）使用 ASMLIB。

> **解决方法：** 直接使用块设备（例如使用类似于 `/dev/mapper/mpath_part1` 的路径），或使用 DASD 磁盘。

**参见：** Oracle 支持文档说明了如何在 SLES 下的 IBM: Linux on System 上为 Oracle ASM 11.2 配置磁盘存储设备（Doc ID 1350088.1）以及如何在 Red Hat 5 下的 IBM: Linux on System 上为 Oracle ASM 11.2 配置磁盘存储设备（Doc ID 1351746.1），地址：
`https://support.oracle.com`

要使用 Oracle 自动存储管理库驱动程序（ASMLIB）配置 Oracle ASM 设备，请完成以下任务：
- 安装和配置 Oracle ASM 库驱动程序软件
- 在 x86 系统上配置使用 Oracle ASM 库驱动器的磁盘
- 在 IBM: Linux on System z 上配置使用 ASM 库驱动器的磁盘
- 管理 Oracle ASMLIB 库驱动和磁盘

> **注意：** 在安装期间使用 Oracle ASM 驱动程序创建数据库，必须选择以交互模式运行 `ASMCA` 的安装方法。您还必须将默认磁盘发现更改为 `ORCL:\`

### 3.3.1.4 安装和配置 Oracle ASM 库驱动程序软件

ASMLIB 已包含在 Unbreakable Enterprise Kernel（企业级内核）软件包和 SU 11 中。如果您是 Unbreakable Linux Network（UEL）的成员，可以通过订阅 Oracle Software for Enterprise Linux 频道来安装 ASMLIB，并使用 `up2date` 获取适用于您的系统和内核的最新包。有关更多信息，请参考以下 URL：
`http://www.oracle.com/technetwork/topics/linux/lib/index-10839.html`

要手动安装和配置 ASMLIB 驱动软件，请按照以下步骤操作：
- 1. 输入以下命令确定系统的内核版本和架构：
  `# uname -rm`
- 2. 从 Oracle Technology Network (OTN) 网站下载所需的 ASMLIB 包：
  `http://www.oracle.com/technetwork/server-storage/linux/downloads/index-088143.html`

> **注意：** 在 Red Hat Linux 5 Advanced Server 上使用 ASMLIB 必须安装版本 2.0.1 或更高版本的 `oracleasm-support` 包。ASMLIB 已包含在 SUSE 发行版中。

> **提示：** 我的 Oracle 支持文档 1089399.1 关于 Red Hat 发行版支持 ASMLIB 信息：
  `https://support.oracle.com/CSP/main/article?cmd=show&type=NOTid=1089399.1`

您必须安装软件包，其中 `version` 为 ASMLIB 驱动版本，`arch` 为系统架构，`kernel` 为您使用的内核版本：
```
oracleasm-support-version.arch.rpm
oracleasm-kernel-version.arch.rpm
oracleasmlib-version.arch.rpm
```
- 3. 切换用户到 root 用户：
  `$ su -`
- 4. 输入类似下面的命令来安装软件包：
  `# rpm -ivh oracleasm-support-version.arch.rpm \
  oracleasm-kernel-version.arch.rpm \
  oracleasmlib-version.arch.rpm`

例如，如果您在 AMD64 系统上使用 Red Hat Enterprise Linux 5 内核，则输入类似下面的的命令：
```
# rpm -ivh oracleasm-support-2.1.3-1.el15.x86_64.rpm \
oracleasm-kernel-2.6.18-194.26.1.el15xsnm-2.0.5-1.el15.x86_64.rpm \
oracleasmlib-2.0.5-1.el15.x86_64.rpm
```
- 5. 输入以下命令运行 `oracleasm` 配置脚本：
  `# /usr/sbin/oracleasm configure`

> **注意：** `/usr/sbin/oracleasm configure` 命令用于配置 ASMLIB 驱动程序。

| Prompt | 建议响应 |
|---|---|
| 拥有接口的默认用户： | 指定用户（例如 `grid`） |
| 拥有接口的默认组： | 指定组（例如 `asm`） |
| 启动时启动 ASM 库驱动程序 (y/n) | 按回车在系统启动时启动库。 |
| 启动时扫描 ASM 磁盘 (y/n) | 按回车在系统启动时扫描 ASM 磁盘。 |

脚本完成以下任务：
- 创建 `/etc/sysconfig/oracleasm` 配置
- 创建 `/dev/oracleasm` 挂载点
- 挂载 ASMLIB 驱动程序

### 为集群的 Grid Infrastructure 配置存储

输入以下命令加载 `oracleasm` 内核模块：
`# /usr/sbin/oracleasm init`

在所有想要安装 RAC 的节点上重复此过程。

- 1. 如果您想在磁盘组中使用 IDE、SCSI 或 RAID 设备，请按照以下步骤操作：
  - a. 如必要，安装或配置您打算使用的共享磁盘设备。
  - b. 要识别要使用的磁盘设备名称，输入以下命令：
    `# /sbin/lsblk -l`

根据磁盘类型，设备名称可能有所不同：

| 磁盘类型 | 设备名称格式 | 说明 |
|---|---|---|
| IDE 磁盘 | `/dev/hdx` | 在此示例中，x 是标识 IDE 磁盘的字母，n 是分区号。例如，`/dev/hda` 是第一个 IDE 总线上的第一个磁盘。 |
| SCSI 磁盘 | `/dev/sdxxn` | x 是标识 SCSI 磁盘的字母，n 是分区号。例如，`/dev/sda` 是第一个 SCSI 总线上的第一个磁盘。 |
| RAID 磁盘 | `/dev/rdxydpz` `/dev/ida/cxydpz` | 根据 RAID 控制器，RAID 设备可能有不同的设备名称。在所示示例中，x 是标识控制器的数字，y 是标识磁盘的数字，z 是标识分区的数字。例如，`/dev/ida/cd0` 是第一个控制器上的第二个逻辑驱动器。 |

要将设备包含磁盘组，可以指定整设备名称或分区名称。

> **注意：** Oracle 建议您在每个磁盘上创建一个单个整盘分区。

- c. 使用 `fdisk` 或 `parted` 在设备上创建一个单个整盘分区。
- 2. 输入类似下面的命令将磁盘标记为 Oracle ASM 磁盘：
  `# /usr/sbin/oracleasm createdisk DISK1 /dev/sdb1`

在此示例中，`DISK1` 是您分配给磁盘的名称。

- 5. 从输出中，识别具有适当冗余级别的磁盘组，并记录其包含的可用空间。
- 6. 如果必要，安装或识别满足上一节列出的存储要求的额外磁盘设备。



# Oracle 自动存储管理 (ASM) 存储配置

**注意：** 您指定的磁盘名称可以包含大写字母、数字和下划字符。它们必须以大写字母开头。

如果您在 Oracle ASM 中使用多路径（multi-path）磁盘驱动程序，请确保为磁盘指定正确的逻辑设备名称。

- 3. 要使磁盘在集群中的其他节点上可用，请在每个节点上以 root 身份执行以下命令：

```
# /usr/bin/oracleasm scandisks
```

此命令会识别连接到节点并标记为 Oracle ASM 磁盘的共享磁盘。

### 3.3.1.4.3 为 IBM: Linux on System z 配置磁盘设备使用 ASM 库驱动程序

1. 如果您使用兼容的磁盘布局进行格式化，请输入类似下所示的命令在设备上创建一个单整盘分区：

```
# /sbin/fdisk -a /dev/sdxxxx
```

- 2. 输入类似下所示命令将磁盘标记为 ASM 磁盘：

```
# /etc/init.d/oracleasm createdisk DISKI /dev/sdxxxx
```

在此示例中，`DISKI` 是您想要分配给磁盘的名称。

> **注意：** 您指定的磁盘名称可以包含大写字母、数字和下划字符。它们必须以大写字母开头。

如果您在 ASM 中使用多路径磁盘驱动程序，请确保为磁盘指定正确的逻辑设备名称。

- 3. 要使磁盘在集群其他节点上可用，请在每个节点上以 root 身份执行以下命令：

```
# /etc/init.d/oracleasm scandisks
```

此命令会识别连接到节点并标记为 Oracle ASM 磁盘的共享磁盘。

### 3.3.1.4.4 管理 Oracle ASM 库驱动程序和磁盘

要管理 Oracle 自动存储管理库驱动程序 (`ASMLIB`) 和磁盘，请根据表 3–7 所示的不同选项使用 `oracleasm` 初始化脚本。

表 3–7 ORACLEASM 脚本选项

| 选项 | 描述 |
| --- | --- |
| configure | 如果必要，使用 configure 选项重新配置 Oracle 自动存储管理库驱动程序：\n# /usr/sbin/oracleasm configure -i\n要查看命令选项，请输入不带 -i 标志的 oracleasm configure。 |
| enable disable | 使用 disable 和 enable 选项更改系统启动时 Oracle 自动存储管理库驱动程序的操作。enable 选项会导致自动存储管理库驱动程序在系统启动时加载。\n# /usr/bin/oracleasm enable |
| start stop restart | 使用 start、stop 和 restart 选项在不重启系统的情况下加载或卸载 Oracle 自动存储管理库驱动程序。\n# /usr/bin/oracleasm restart |
| createdisk | 使用 createdisk 选项为自动存储管理库驱动程序标记磁盘设备并为其重命名：\n# /usr/bin/oracleasm createdisk DISKNAME devicename |
| deletedisk | 使用 deletedisk 选项取消标记磁盘设备：\n# /usr/bin/oracleasm deletedisk DISKNAME\n> **警告：** 不要使用此命令取消标记被 Oracle 自动存储管理磁盘组使用的磁盘。在取消标记之前，您必须先从 Oracle 自动存储管理组中删除磁盘。 |
| querydisk | 使用 querydisk 选项确定磁盘或磁盘名称是否被 Oracle 自动存储管理库驱动程序使用：\n# /usr/bin/oracleasm querydisk (DISKNAME \| devicename) |
| listdisks | 使用 listdisks 选项列出标记的 Oracle 自动存储管理库驱动程序的磁盘名称：\n# /usr/bin/oracleasm listdisks |
| scandisks | 使用 scandisks 选项允许集群节点识别哪些共享磁盘在另一个节点上已被标记为 Oracle 自动存储管理驱动驱动：\n# /usr/bin/oracleasm scandisks |

### 3.3.1.5 使用多路径配置 ASMLIB

使用多路径配置 ASMLIB（自动存储管理驱动程序）需要额外的配置。

参阅 Oracle Support 网站获取更新：

```
https://support.oracle.com
```

### 3.3.1.51 使用多路径的 Oracle ASM

Oracle ASM 要求每个磁盘具有唯一标识。如果磁盘以多个路径出现，则会导致错误。在多路径配置下：

1. 磁盘的初始路径

2. 磁盘的第二个路径

3. 外部存储访问

例如：如果您有一个本地磁盘 `/dev/sda`，以及一个连接到外部存储的磁盘，则显示两个路径。Oracle ASM 显示为 `/dev/sdb` 和 `/dev/sdc`。

在多路径配置下，系统可以使用 `/dev/sdb` 或 `/dev/sdc`。如果系统使用 `/dev/sdb` 路径且电缆被拔掉，则会发生错误。多路径将从 `/dev/sdb` 切换到 `/dev/sdc`。

大多数系统软件无法感知多路径。默认情况下，2.6 内核命名方案 `udev` 在系统启动时创建设备文件名，并将所有权分配给 root。重启服务器后，`udev` 会为 Oracle 集群分区（投票磁盘）更改设备文件名和所有者。

### 3.3.1.52 配置扫描顺序以选择多路径

要配置 ASM 选择多路径磁盘，请执行以下步骤：

1. 使用编辑器打开 `/etc/sysconfig/oracleasm`。

2. 编辑 `ORACLE_SCANORDER` 变量以提供前缀。例如，如果您想选择多路径磁盘，请提供类似的前缀：

```
ORACLE_SCANORDER="multipath*"
```

3. 保存文件。

完成此操作后，ASMLIB 将扫描所有 `multipath` 前缀的磁盘，将其标记为 Oracle。在步骤 2 的示例中，`multipath` 实际上位于 `/etc/multipath.conf`。

### 3.3.1.5.4 配置扫描顺序以排除单路径

要配置 ASMLIB 排除特定的单路径磁盘，请执行以下步骤：

1. 使用编辑器打开 `/etc/sysconfig/oracleasm`。

2. 编辑 `ORACLEASM_SCANNEXCLUDE` 变量以提供前缀。例如，如果您想排除 `/dev/sdb` 和 `/dev/sdc` 单路径磁盘，请提供类似的前缀：

```
ORACLEASM_SCANNEXCLUDE="sdb sdc"
```

3. 保存文件。

完成此操作后，ASMLIB 将扫描除 `sdb` 和 `sdc` 外的所有磁盘，因此忽略 `/dev/sdb` 和 `/dev/sdc`。

### 3.3.1.6 为 Oracle ASM 手动配置设备

如果您使用 ASMLIB，则不需要在 `udev` 中确保权限和设备路径的持久性。

# Oracle 自动存储管理存储配置

如果您没有使用 ASMLIB，则必须自定义规则文件。当 `udev` 启动时，它会按顺序执行规则文件中的规则（配置指令）。这些文件位于 `/etc/udev/rules/` 路径下。规则文件按词法顺序读取。例如，`90-wacom.rules` 文件中的规则将在将在 `90-ib.rules` 文件中的规则之前解析并执行。

在 UDEV 规则文件中指定设备时，请确保按照所示顺序在任何其他属性之前指定 `OWNER`（所有者）、`GROUP`（组）和 `MODE`（模式）。例如，如果您想在 UDEV 行中包含 `ACTION` 属性，请在 `OWNER`、`GROUP` 和 `MODE` 之后指定 `ACTION`。

当规则描述同一设备时，在支持的 Linux 内核版本上，将应用最后一个文件。

若要为磁盘设备配置权限，请运行以下命令：

- 1. 要获取现有块的信息，请在一个集群节点的设备上运行 `scsi_id` (`/sbin/scsi_id`) 命令以获取它们的唯一设备标识符。在使用 `-s` 参数运行 `scsi_id` 命令时，设备路径和名称应相对于 sysfs 目录 `/sys`（例如，在引用 `/sys/block/device` 时使用 `/block/device`）。例如：

```bash
# scsi_id -g -s /block/sdb
3609a000886fe66956988a45333524174
```

```bash
# scsi_id -g -s /block/ade/sdel
3609a000886fe66956988a45333524179
```

记录集群感知设备的 `scsi_id` 标识符，以便在需要时提供。

> 注意：`scsi_id` 命令对于给定的设备应返回相同的设备标识符，无论从哪个节点运行该命令。

- 2. 通过编辑 `/etc/scsi_id.config` 文件并向文件中添加 `options=-g` 将 SCSI 设备配置为信任设备（白名单）。例如：



```bash
# cat /etc/scsi_id.config
vendor="ATA",options=-p 0x0
options=-g
```

## 3. 使用文本编辑器为 Oracle ASM 设备创建 UDEV 规则文件，为安装所有者和 Oracle Grid Infrastructure 管理员的组成员设置权限为 `0660`。例如，使用安装 `grid` 和基于角色的组配置，对应 OS 组 `asmadmin`：

```bash
# /etc/udev/rules.99-oracle-asmdevs.rules
KERNEL="sd*", BUS="scsi_id", PROGRAM="/sbin/scsi_id"
RESULT="14f705e666695669c000000000", OWNER="grid", GROUP="asmadmin", MODE="0660"
KERNEL="sd*", BUS="scsi_id", PROGRAM="/sbin/scsi_id"
RESULT="14f705e666695669c000000001", OWNER="grid", GROUP="asmadmin", MODE="0660"
KERNEL="sd*", BUS="scsi_id", PROGRAM="/sbin/scsi_id"
RESULT="14f705e666695669c0000000002", OWNER="grid", GROUP="asmadmin", MODE="0660"
```

## 4. 将规则拷贝到集群中的所有其他节点。运行：

```bash
# scp 99-oracle-asmdevices.rules root@node2:/etc/udev/rules.d/99-oracle-asmdevices.rules
```

## 5. 使用 `/sbin/partprobe devicename` 在集群的所有成员节点上加载更新的块设备分区。您必须以 root 身份执行此操作。

## 6. 运行 `udevtest` (`/sbin/udevtest`) 命令来测试您创建的 UDEV 配置。输出应指示块设备可用且规则已应用。例如：

```bash
udevtest /block/sdb1
main: looking device at /block/sdb1 from subsystem 'block'
udev_rules:name= add symlink
udev_dev_name= add symlink
/disk/by-path/ip-192.168.1.1:3260-scsi-ign.1992-08.com.netapp:sn.887085-part1
udev_moknd: preserve file "/dev/" because it has correct dev_t
run_run: /sbin/udev/dev1 --export /dev/t.tmp-8-17
run_run: /sbin/udev/dev1 returned with status 4
run_run: /sbin/scsi_id
run_run: /sbin/scsi_id returned with status 0
run_run: /sbin/scsi_id returned with status 0
udev_rules:name= applied, so 'sdb1' becomes 'ocri'
udev_add: creating node /dev/ocri1 currently present symlinks
udev_add: creating node /dev/ocri, mode = '0640', uid = '0', gid = '50'
udev_add: creating node /dev/ocri currently present symlinks
udev_add: creating node /dev/ocri
/disk/by-id/scsi-360-36a9800068ef6f5968a4453335251417-part1' to '.../ocri'
/disk/by-path/ip-192.168.1.1:3260-scsi-ign.1992-08.com.netapp:sn.84187085-part1
main: /socket/ocr/kernel/monitor
main: /lib/udev/udev_run_devd
main: /socket/freesdesktop/hal/udev_event
main: /sbin/pam_console_apply /dev/ocri
/disk/by-id/scsi-360-36a9800068ef6f5968a4453335251417-part1
```

## 7. 运行命令...

`home/bin)` 将现有的 Oracle ASM 升级到 11g Release 2 (11.2)，并配置故障组、Oracle ASM 卷和 Oracle 自动存储集群文件系统 (Oracle ACFS)。

> 注意：在升级之前，您必须首先关闭现有 Oracle ASM 实例的节点上的所有数据库实例和应用程序。

在安装过程中，如果您是从 Oracle ASM 版本升级到 11.2，并选择使用 Oracle ASM，且 ASMCA 检测到在另一个 Oracle ASM home 中安装了合适的 Oracle ASM 版本，那么在安装 Oracle ASM 11g Release 2 (11.2) 二进制文件后，可以启动 ASMCA 来升级现有的 Oracle ASM 实例。然后您可以选择通过创建 Oracle ASM 卷并创建 Oracle ACFS 来配置 Oracle ACFS 部署。

如果您是从 Oracle ASM 11g release 2 (11.2.0.1) 或更高版本升级，则 Oracle ASM 将作为滚动升级的一部分随 Oracle Grid Infrastructure 一起升级，ASMCA 在升级期间由 root 脚本启动。ASMCA 无法将 Oracle ASM 从版本 11.2.0.1 独立升级到 11.2.0.2。

在现有的 Clusterbase 或 Oracle RAC 安装中，如果所有节点上的 Oracle ASM 实例版本为 11g release 1，则提供执行 Oracle ASM 实例滚动升级的选项。如果 Oracle RAC 安装中的第一个 Oracle ASM 实例版本是 11g release 1 之前的版本，则无法进行滚动升级。所有节点上的 Oracle ASM 将被升级到 11g Release 2 (11.2)。

### 3.4 对块和原始设备的支持

随着 Oracle Database 和 Oracle RAC 11g Release 2 (11.2) 的发布，不再支持使用数据库配置助手或安装程序在块或原始设备上存储 Oracle Clusterware 或 Oracle Database 文件。

如果您打算升级现有的 Oracle RAC 数据库或带有 Oracle ASM 实例的 Oracle RAC 数据库，可以使用现有的原始或块分区，并对现有的安装进行滚动升级。不允许使用块或原始设备创建新安装。

此外，对于 IBM: Linux on System z 设备，您可以使用 `-d 1` 选项使用 Linux 磁盘布局格式化 DASD（例如，如果您想为 ASM 文件管理创建一个分区）。如果您使用此磁盘布局，DASD 的分区设备名称为 `/dev/dasdxxxx`。

### 3.5 在 IBM: Linux on z 上配置原始逻辑卷

在 IBM: Linux on z 上，您可以使用原始逻辑卷 (LVM) 卷用于 Oracle Cluster 和自动存储管理文件。您可以在直接访问存储设备 (DASD) 或 SCSI 设备上的卷组中创建原始逻辑卷。要配置所需的逻辑卷，请遵循以下步骤：

> 注意：您不需要在 Linux 中格式化 FBA 类型的 DASD。FBA 类型 DASD 的单个整盘分区设备名称为 `/dev/dasdxxxx`。

为集群和 Oracle RAC 的 Oracle Grid Infrastructure 配置存储 3-37

# 在 IBM: Linux on z 上配置原始逻辑卷

1. 如必要，安装或配置您打算用于磁盘组的共享 DASD 并重启系统。

2. 输入命令识别系统上配置的 DASD：

   # `/proc/dasd/devices`

此命令的输出包含类似下行的内容：

`0302(ECKD) at ( 94: 48) is dasdm : active at blocksize: 4096, 540000 blocks, 2109 MB`

这些行显示了每个 DASD 的信息：

* 设备号 (`0302`)
* 设备类型 (`ECKD` 或 `FBA`)
* Linux 设备主号和次要号 (`94: 48`)
* Linux 文件名 (`dasdm`)

通常情况下，DASD 的设备名称格式为 `dasdxxxx`，其中 `x` 是识别设备的一个到四个字母。

* 设备的块大小和设备大小



### 3. 从显示内容中识别您想要使用的设备。

如果显示的设备是 FBA 类型的 DASD，则您无需对其进行配置。您可以继续将它们绑定到 Oracle 数据库文件。

如果您使用 ECKD 类型的 DASD，如果该 DASD 尚未格式化，请输入类似下方的命令来格式化 DASD：

```
# /sbin/dasdfint -b 4096 -f /dev/dasdxxxx
```

> 警告：格式化 DASD 会破坏设备上的所有现有数据。请确保：
> 
> * 您指定了正确的 DASD 设备名称
> * DASD 不包含您想要保留的现有数据

此命令使用 4 KB 的块大小和兼容的磁盘布局（默认）格式化 DASD，允许您在 DASD 上创建多多三个分区。

### 4. 如果您打算在 SCSI 设备上创建原始逻辑卷，请执行第 5 步。

如果您打算在 DASD 上创建原始逻辑卷，且您已使用兼容的磁盘布局格式化了 DASD，请确定您如何创建分区。

要在设备上创建单磁盘分区（例如，如果您想为数据库文件在整个原始逻辑卷创建一个分区），请输入类似下方的命令：

```
# /sbin/fdasd -a /dev/dasdxxxx
```

Oracle Grid Infrastructure 安装指南

# 在 IBM: Linux on z 上配置原始逻辑卷

此命令在设备上创建一个分区。现在可以准备将设备标记为物理卷。请继续第 6 步。

### 5. 如果您打算在 SCSI 设备上创建原始逻辑卷，请遵循以下步骤：

a. 如必要，安装或配置您打算用于磁盘组的共享 DASD 并重启系统。

b. 输入以下命令识别您要使用的磁盘名称：

```
# fdisk -l
```

SCSI 设备的设备名称类似于：

`/dev/sdxn`

在此示例中，`x` 是标识磁盘的字母，`n` 是分区号。例如，`/dev/sda` 是第一个磁盘。

c. 如必要，使用 `t` 命令更改分区。

d. 输入类似下方的命令将您要使用的每个设备标记为物理卷：

对于 SCSI 设备：

```
# pvcreate /dev/sda1 /dev/sdb1
```

要在设备上创建以下：

### 7. 使用您标记的设备创建一个名为 `oracle_vg` 的卷组，输入类似下方的命令：

对于 SCSI 设备：

```
# vgcreate oracle_vg /dev/sda1 /dev/sdb1
```

为集群和 Oracle RAC 的 Oracle Grid Infrastructure 配置存储 3-39

# 在 IBM: Linux on z 上配置原始逻辑卷

对于 DASD 设备：

```
# vgcreate oracle_vg /dev/dasdal /dev/dasdb
```

### 8. 在您创建的卷组中创建所需的逻辑卷，输入类似下方的命令：

```
# lvcreate -L size -n lv_name vg_name
```

在此示例中：

- `size` 是逻辑卷的大小，例如 `500M`
- `lv_name` 是逻辑卷的名称，例如 `orcl_system_raw_500m`
- `vg_name` 是卷组的名称，例如 `oracle_vg`

例如，要在 `oracle_vg` 卷组中名为 `rac` 的数据库的 SYSTEM 表空间创建一个 500 MB 的逻辑卷，输入以下命令：

```
# lvcreate -L 500M -n rac_system_raw_500m oracle_vg
```

> 注意：这些命令为每个逻辑卷创建一个类似于下方的设备名称：
> 
> `/dev/vg_name/lv_name`

### 9. 在其他集群节点上，输入以下命令扫描所有卷组并激活它们：

```
# vgscan
# vgchange -a y
```

# 为集群安装 Oracle Grid Infrastructure

本章描述了为集群安装 Oracle Grid Infrastructure 的步骤。Oracle Grid Infrastructure 由 Oracle Clusterware 和 Oracle 自动存储管理 (Oracle ASM)组成。如果您之后计划安装带有实时应用集群 (Oracle RAC) 的 Oracle Database，这就是两阶段安装中的第一阶段。

本章包含以下主题：

- 使用 OUI 准备安装 Oracle Grid Infrastructure
- 安装 Oracle Grid Infrastructure
- 使用仅软件安装方式安装 Oracle Grid Infrastructure
- Oracle Berkeley DB 的限制
- 确认 Oracle Clusterware 功能
- 确认 Oracle Clusterware 文件的 Oracle ASM 功能
- 理解 Oracle Grid Infrastructure 中的离线过程

## 4.1 准备使用 OUI 安装 Oracle Grid Infrastructure

在用安装程序安装 Oracle Grid Infrastructure 之前，请使用以下检查清单，确保您已拥有安装期间所需的所有信息，并确保您已完成开始安装之前必须完成的所有任务。在完成下列表中的每个任务时请进行勾选，并记录所需的信息，以便您在安装期间提供它们。

- 停止正在运行的 Oracle 进程

您可能需要停止正在运行的 Oracle 进程：

**在未使用 Oracle ASM 的独立数据库节点上安装：** 在安装 Oracle Grid Infrastructure 软件时，不需要停止数据库。

**在已经在 Oracle ASM 上运行独立 Oracle Database 11g release 2 (11.2) 的节点上安装：** 停止 Oracle ASM 实例。Oracle ASM 实例将在安装期间重启。

**在 Oracle RAC 节点上安装：** 此安装需要升级 Oracle Clusterware，因为运行 Oracle RAC 需要 Oracle Clusterware。作为升级的一部分，当滚动升级从节点到节点进行时，您必须停止数据库节点。

### 准备使用 OUI 安装 Oracle Grid Infrastructure

> 注意：如果您正在将 Oracle RAC 9i Release 2 (9.2) 节点升级到 Oracle Grid Infrastructure 11g Release 2（版本 11.2.0.1 和 11.2.0.2），且 TNLSNR 正在监听 SCAN 监听的端口（默认 1521），则应关闭 TNLSNR。

如果您正在升级到 Oracle Grid Infrastructure 11g Release 2 (11.2.0) 或更高版本，则可以忽略此问题。

如果正在运行来自 Oracle9i Release 9.2 或更早版本的全局服务守护 (GSD)，则在安装 Oracle Grid Infrastructure 之前运行以下命令：

```
$ Oracle_home/bin/gsdctl stop
```

其中 `Oracle_home` 是运行 GSD 的 Oracle Database home。

> 警告：如果您有 Oracle9i release 2 (9.2) Oracle Cluster Manager (Oracle CM) 安装，请停止 Oracle CM 服务，这将阻止 Oracle Grid Infrastructure 11g Release 2 (11.2) 软件检测 Oracle9i 2 节点列表并导致 Oracle Grid Infrastructure 安装失败。

> 注意：如果您在启动 Oracle 通用安装程序 (OUI) 后收到停止所有 Oracle 服务的警告，请运行命令

```
Oracle_home/bin/localconfig delete
```

其中 `Oracle_home` 是现有的 Clusterware home。

- 如果已有现有安装，为 Oracle 自动存储管理和集群升级做准备

在 Oracle Grid Infrastructure 安装期间，现有的 Oracle Clusterware 和集群 ASM 安装都将进行升级。

当集群成员运行 Oracle Grid Infrastructure 11g Release 2 (11.2) 时，新的集群软件将成为活动集群。

如果您打算安装 Oracle RAC，必须在安装 Oracle Database 11g Release 2 (11.2) 版本 Oracle RAC 之前，首先在所有集群节点上升级到 Oracle Grid Infrastructure 11g Release 2 (11.2)。

> 注意：所有 Oracle Grid Infrastructure 升级（现有 Oracle Clusterware 和 Oracle ASM 安装的升级）均为原地升级。

- 确定 Oracle 目录 (`oralInventory`) 位置



如果您已经在系统中安装了 Oracle 软件，`OUI` 会从 `/etc/oraInst.loc` 文件中检测现有的 Oracle 目录 (`oralInventory`) 目录并使用该位置。这是安装在您的系统上的 Oracle 软件的中心目录。拥有 Oracle Inventory 组作为主组的用户被授予 `OINSTALL` 权限以写入中心目录。

如果您在系统中首次安装 Oracle 软件，`OUI` 会从 `/etc/oraInst.loc` 文件中检测现有的 Oracle 目录 (`oralInventory`) 目录并使用该位置。这是安装在您的系统上的 Oracle 软件的中心目录。拥有 Oracle Inventory 组作为主组的用户被授予 `OINSTALL` 权限以写入中心目录。

### 4-2 Oracle Grid Infrastructure 安装指南

（注：原文后续存在大量重复文本，已根据要求处理，未重复输出内容）

如果您的网络中存在代理网域（`proxy realm`），`OUI` 将尝试下载更新。系统会提示您提供代理网域以及用户身份验证信息以便通过代理服务访问 Internet。如果您已配置了代理网域，请准备好提供这些信息。如果您没有配置代理网域，可以留代理认证字段为空。

## 识别 Oracle Cluster 文件的共享存储并在必要时准备存储空间

在安装期间，系统会要求您提供以下 Oracle Cluster 文件的路径。这些文件必须在集群的所有节点之间共享，既可以存储在 Oracle ASM 上，也可以存储在支持的文件系统上：

- 投票盘（Voting disks）是 Oracle Cluster 用于验证集群节点成员关系和状态的文件。
- 投票盘的所有者必须是执行安装的用户（`grid` 或 `oracle`），并且权限必须设置为 `640`。
- Oracle Cluster 注册表文件（`OCR`）包含用于 Oracle Cluster 的集群和数据库配置信息。

在安装之前，`OCR` 文件的所有者必须是执行安装的用户（`grid` 或 `oracle`）。该用户必须使用 `grid` 作为其主组（`group`）。在安装期间，`OUI` 会将 `OCR` 文件的所有者更改为 `root`。

如果您的系统没有外部存储冗余，则建议您为 `OCR` 磁盘提供两个额外位置，为投票盘提供两个额外位置，总共六个分区（三个用于 `OCR`，三个用于投票盘）。创建冗余存储位置可以在发生故障时保护 `OCR` 和投票盘。为了保护您的集群，`OCR` 和投票盘副本的存储位置应位于完全不同的路径、控制器上，以确保没有存储位置存在共享的单点故障。

当您选择将 `OCR` 存储在 Oracle ASM 上时，默认配置是在一个 Oracle ASM 磁盘组上创建 `OCR`。在具有普通冗余或高冗余的磁盘组中，`OCR` 将受到免于磁盘故障的保护。

为了防止 `OCR` 受到逻辑磁盘故障的影响，请在安装后创建另一个 Oracle ASM 磁盘组，并使用 `orconfig` 命令将 `OCR` 添加到第二个磁盘组。

> 另见：参考第 2 章“Advanced Installation Oracle Grid Infrastructure for a Cluster Preinstallation Tasks”以及《Oracle Automatic Storage Management Administrator’s Guide》，获取有关向组添加磁盘的信息。

## 确保 cron任务在集群安装期间不运行

如果在启动每日 `cron` 任务时安装程序正在运行，且您的 `cron` 任务正在执行清理操作，导致临时文件在安装完成之前被删除，可能会遇到无法解释的安装问题。Oracle 建议在每日 `cron` 任务运行之前完成安装，或安装完成后禁用执行清理的每日 `cron` 任务。

## 准备在 IBM: Linux on System z 上安装 Oracle Clusterware

- 已完成 IPMI 配置并准备好 IPMI 管理员账户信息

如果您打算使用 IPMI，请确保 BMC 接口已配置，并在安装期间提示时提供管理账户的用户名和密码。

对于非标准安装，如果您在安装后更改了一个或多个节点上的配置（例如，如果集群节点上的 BMC 接口具有不同的管理员用户名和密码），请决定是想在安装时识别 BMC 接口，还是在安装后修改 IPMI 管理员账户。

- 确保您为 Oracle Grid Infrastructure 选择的 Oracle home 路径仅使用 ASCII 字符

此限制包括所有者用户名（它是某些 home 路径的默认值），以及您可能选择作为路径的其他目录。

- 取消环境变量。如果您将 `ORA_CRS_HOME` 设置为环境变量，请在启动安装或升级之前取消设置。您永远不应该将 `ORA_CRS_HOME` 作为用户环境变量。

如果您的系统上存在现有安装，且您使用相同的用户账户进行此类安装，请取消设置以下环境变量：`ORA_CRS_HOME`；`ORA_NLSID`；`TNS_ADMIN`

- 决定是否要使用软件更新选项。`OUI` 可以为支持的操作系统安装关键补丁更新、系统要求更新、操作系统和内核包，以及其他有助于确保安装顺利进行的其他重大更新。Oracle 建议您在安装期间启用更新。

如果您选择启用更新，则在安装期间必须提供 My Oracle Support 用户名和密码。如果您在可以访问 Internet 的系统上启动 `OUI` 来下载更新，提供 My Oracle Support 用户名和密码。输入以下命令启动更新：

```
./runinstaller -downloadUpdates
```

## 准备在 IBM: Linux on System z 上安装 Oracle Clusterware

- 已完成 IPMI 配置并准备好 IPMI 管理员账户信息

如果您打算使用 IPMI，请确保 BMC 接口已配置，并在安装期间提示时提供管理账户的用户名和密码。

对于非标准安装，如果您在安装后更改了一个或多个节点上的配置（例如，集群节点上的 BMC 接口具有不同的管理员用户名和密码），请决定是想在安装时识别 BMC 接口，还是在安装后修改 IPMI 管理员账户。

- 确保您为 Oracle Grid Infrastructure 选择的 Oracle home 路径仅使用 ASCII 字符

此限制包括所有者用户名（它是某些 home 路径的默认值），以及您可能选择作为路径的其他目录。

- 取消环境变量。如果您将 `ORA_CRS_HOME` 设置为环境变量，请在启动安装或升级之前取消设置。您永远不应该将 `ORA_CRS_HOME` 作为用户环境变量。

如果您的系统上存在现有安装，且您使用相同的用户账户进行此类安装，请取消设置以下环境变量：`ORA_CRS_HOME`；`ORA_NLSID`；`TNS_ADMIN`

- 决定是否要使用软件更新选项。`OUI` 可以为支持的操作系统安装关键补丁更新、系统要求更新、操作系统和内核包，以及其他有助于确保安装顺利进行的其他重大更新。Oracle 建议您在安装期间启用更新。

如果您选择启用更新，则在安装期间必须提供 My Oracle Support 用户名和密码。如果您在可以访问 Internet 的系统上启动 `OUI` 来下载更新，提供 My Oracle Support 用户名和密码。输入以下命令：

```
./runinstaller -downloadUpdates
```

## 在 IBM: Linux on System z 上准备安装 Oracle Clusterware

由于 IBM: Linux on System z 不支持连接 DVD-ROM 驱动器，您必须从光盘将安装文件拷贝到硬盘。访问 Oracle 技术网络站点：

```
http://www.oracle.com/technology/software
```

对于每个光盘，创建一个名为 `Diskn` 的目录（其中 `n` 是光盘编号），并将文件拷贝到该目录。在您拷贝了安装文件后，可以使用以下方法在 IBM: Linux on System z 上访问它们：

- 使用 FTP 将文件拷贝到 IBM: Linux on System z。
- 使用 NFS 或 Samba 方法让 IBM: Linux on System z 可访问文件系统。

> 注意：由于 IBM: Linux on System z 的块大小问题，11.2.0.1 及更高版本无法使用 ASMLIB 光纤通道 (`FCP`)。

## 安装 Oracle Grid Infrastructure

本节提供了有关使用安装程序安装 Oracle Grid Infrastructure 的信息。它包含以下章节：

- 使用 `OUI` 安装 Oracle Grid Infrastructure
- 使用集群配置文件安装 Oracle Grid Infrastructure

### 4.3.1 使用 OUI 安装 Oracle Grid Infrastructure

按照以下步骤在您的集群上安装 Oracle Grid Infrastructure（Oracle Clusterware 和自动存储管理）。安装期间的任何时候，如果您对要求的操作有疑问，请点击 `OUI` 页面上的帮助按钮。



## 切换到安装媒体目录并运行安装程序

1. 切换到安装媒体上的 `/Disk1` 目录（或您下载安装二进制文件的目录），并运行 `runinstaller` 命令。例如：

```
$ cd /home/grid/oracle_sw/Disk1
$ ./runinstaller
```

2. 选择 Type（类型）或 Advanced（高级）

3. 在安装期间需要帮助时，提供信息或以 root 身份运行脚本。点击 Details 查看日志文件。如果在任何节点上运行 `root.sh` 时，您可以解决问题并按照第 6.5 章“在不删除二进制文件的情况下配置 Oracle Clusterware”的步骤重新运行 `root.sh`。

> 注意：您必须在第一个节点上运行 `root.sh` 并等待其完成。如果您的集群有四个或更多节点，`root.sh` 可以在第一个节点以外的所有节点上并发运行。与第一个节点一样，最后一个节点的 `root.sh` 必须单独运行。

4. 在在所有节点上运行 `root.sh` 后，OUI 将运行网络配置助手 `netca` 和集群验证实用 `Cluster Verification Utility`。这些程序无需用户干预即可运行。

5. 自动存储管理配置助手 `asmca` 在安装期间配置 Oracle ASM。

当您确认网格基础架构（Grid Infrastructure）安装成功后，可以使用它来维护其他应用程序的高可用性，或者您可以安装 Oracle 数据库。

以下是关于安装需要注意的额外信息列表：

- 如果您在 Linux 系统上进行安装，并在安装期间使用了 ASM 库驱动程序 `ASMLIB`，那么 Oracle 自动存储管理 `ASM` 默认发现将找到所有被 `ASMLIB` 标记为 ASM 磁盘的磁盘。

- 如果您打算安装带有 Oracle RAC 的 Oracle Database 11g Release 2 `11.2`，请参阅《Linux 版 Oracle 集群指南》`Real Application Clusters Guide for Linux`。

> 此外：参考《Oracle Cluster Administration and Deployment Guide》来克隆 Oracle Grid Infrastructure，并参考《Oracle Real Application Clusters Administration and Deployment Guide》获取有关添加 Oracle RAC 节点的克隆和节点添加程序的信息。

- 在安装 Oracle Grid Infrastructure 期间运行 `root.sh` 时，跟踪文件（TF）分析器和收集器 `Trace File Analyzer and Collector` 也会安装在目录 `grid_home/tfa` 中。

> 此外：参考《Oracle Cluster Administration and Deployment Guide》获取有关使用跟踪文件分析器和收集器的信息

### 4.3.2 使用集群配置文件安装 Oracle Grid Infrastructure

在安装 Oracle Grid Infrastructure 期间，您可以有两种选择：手动提供集群配置信息，或使用集群配置文件。集群配置文件是您可以在启动 OUI 之前创建的文本文件，它为 OUI 提供配置集群所需的集群节点地址。

Oracle 建议，如果您打算在测试集群上执行重复安装，或者打算在许多节点上执行安装，请考虑使用集群配置文件。

要手动创建集群配置文件，请启动文本编辑器，并创建一个文件，提供每个集群节点节点的公共 IP 地址和虚拟 IP 地址，格式如下：

```
node1 node1-vip
node2 node2-vip
```

例如：

```
mynodel1 mynodel1-vip
mynode2 mynode2-vip
```

### 4.4 使用仅软件安装安装 Oracle Grid Infrastructure

本节包含以下任务：

- 安装软件二进制文件
- 配置软件二进制文件
- 使用响应文件配置软件二进制文件

> 注意：Oracle 建议仅由高级用户执行仅软件安装，因为此安装需要手动后安装步骤来启用 Oracle Grid Infrastructure

如果您在安装期间使用“网格基础架构仅软件”`Infrastructure Software Only` 选项，将在本地节点上安装软件二进制文件。要完成您的集群安装，您必须执行配置 Clusterware 和 Oracle ASM 的额外步骤、创建本地安装集群、将其部署到其他节点，并将其他节点添加到集群。

另请：参考《Oracle Cluster Administration and Deployment Guide》获取如何将 Oracle Grid Infrastructure 克隆到其他节点并将其添加到集群的信息。

#### 4.4.1 安装软件二进制文件

执行仅软件安装：

1. 在本地节点上，使用命令 `runcluvfy.sh stage -pre csint` 验证集群节点是否满足安装要求。确保您已完成所有存储和服务器预安装要求。

2. 从 Oracle Database 11g Release 2 `11.2` 安装介质或下载目录中的相关目录运行 `runInstaller`。例如：

3. 在第一个节点上完成 Oracle Grid Infrastructure 的仅软件安装。

4. 软件安装完成后，运行 `oracleRoot.sh` 脚本并继续第 6 步。对于 Oracle RAC 版本 11.2.0.2 及以上的安装，对于 Oracle RAC 版本 11.2.0.1 的安装，在启用 Oracle RAC 选项的情况下重新链接 Oracle Clusterware，运行类似下方的命令（在此示例中，Grid home 为 `/u01/app/11.2.0/grid`）：

```
$ /home/grid/oracle_sw/Disk1
$ ./Installer
```

```
$ /u01/app/11.2.0/grid
```



## 4.4 仅软件安装 Oracle Grid Infrastructure

### 仅软件安装（安装 Oracle Grid Infrastructure）

本节包含以下任务：

- 安装软件二进制文件
- 配置软件二进制文件
- 使用响应文件配置软件二进制文件

> 注意：Oracle 建议仅由高级用户执行仅软件安装，因为此安装需要手动后安装步骤来启用 Oracle Grid Infrastructure

如果您在安装期间使用仅软件选项将在本地节点上安装软件二进制文件。要完成您的集群安装，您必须执行配置 Clusterware 和 Oracle ASM 的额外步骤、创建本地安装集群、将其部署到其他节点，并将其他节点添加到集群。

另请：参考《Oracle Cluster Administration and Deployment Guide》获取如何将 Oracle Grid Infrastructure 克隆到其他节点并将其添加到集群的信息。

### 4.4.1 安装软件二进制文件

执行仅软件安装：

1. 在本地节点上，使用命令 `runcluvfy.sh stage -pre csint` 验证集群节点是否满足安装要求。确保您已完成所有存储和服务器预安装要求。
2. 从 Oracle Database 11g Release 2 (11.2) 安装介质或下载目录中的相关目录运行 `runInstaller`。例如：
3. 在第一个节点上完成 Oracle Grid Infrastructure 的仅软件安装。
4. 软件安装完成后，运行 `oracleRoot.sh` 脚本并继续第 6 步。对于 Oracle RAC 版本 11.2.0.2 及以上的安装，对于 Oracle RAC 版本 11.2.0.1 的安装，在启用 Oracle RAC 选项的情况下重新链接 Oracle Clusterware，运行类似下方的命令（在此示例中，Grid home 为 `/u01/app/11.2.0/grid`）：

```
$ /home/grid/oracle_sw/Disk1
$ ./Installer
```

```
/u01/app/11.2.0/grid
```

## 4.3.2 使用集群配置文件安装 Oracle Grid Infrastructure

在安装 Oracle Grid Infrastructure 期间，您可以有两种选择：手动提供集群配置信息，或使用集群配置文件。集群配置文件是您可以在启动 OUI 之前创建的文本文件，它为 OUI 提供配置集群所需的集群节点地址。

Oracle 建议，如果您打算在测试集群上执行重复安装，或者打算在许多节点上执行安装，请考虑使用集群配置文件。

要手动创建集群配置文件，请启动文本编辑器，并创建一个文件，提供每个集群节点节点的公共 IP 地址和虚拟 IP 地址，格式如下：

```
node1 node1-vip
node2 node2-vip
```

例如：

```
mynodel1 mynodel1-vip
mynode2 mynode2-vip
```

## 4.7 确认 Oracle Clusterware 文件的 Oracle ASM 功能

> **注意：** 安装完成后，在 Oracle Clusterware 运行时不要手动删除或运行删除 `/tmp/.oracle` 或 `/var/tmp/.oracle` 或其文件的 cron 任务。如果您删除了这些文件，Oracle Clusterware 可能会出现间性挂起，并且您将遇到错误 `CRS-0184`：无法与 CRS 进程通信。

如果您在 Oracle ASM 上安装了 OCR 和投票磁盘（voting disk），则可以使用 Oracle Grid Infrastructure 安装所有者的身份使用以下命令语法来确认您的 ASM 安装正在运行：

```
srvctl status asm
```

例如：

```
$ srvctl status asm
ASM is running on node1,node2
```

5. 自动存储管理配置助手 `asmca` 在安装期间配置 Oracle ASM。

当您确认网格基础架构（Grid Infrastructure）安装成功后，可以使用它来维护其他应用程序的高可用性，或者您可以安装 Oracle 数据库。

以下是关于安装需要注意的额外信息列表：

- 如果您在 Linux 系统上进行安装，并在安装期间使用了 ASM 库驱动程序 `ASMLIB`，那么 Oracle 自动存储管理 `ASM` 默认发现将找到所有被 `ASMLIB` 标记为 ASM 磁盘的磁盘。
- 如果您打算安装带有 Oracle RAC 的 Oracle Database 11g Release 2 (11.2)，请参阅《Linux 版 Oracle集群指南》（Real Application Clusters Guide for Linux）。

> 此外：参考《Oracle Cluster Administration and Deployment Guide》来克隆 Oracle Grid Infrastructure，并参考《Oracle Real Application Clusters Administration and Deployment Guide》获取有关添加 Oracle RAC 节点的克隆和节点添加程序的信息。

- 在安装 Oracle Grid Infrastructure 期间运行 `root.sh` 时，跟踪文件（TF）分析器和收集器（Trace File Analyzer and Collector）也会安装在目录 `grid_home/tfa` 中。

> 此外：参考《Oracle Cluster Administration and Deployment Guide》获取有关使用跟踪文件分析器和收集器的信息



只有在 Oracle Cluster 文件需要时，Oracle ASM 才会运行。如果您没有在 Oracle ASM 上安装 OCR 和投票磁盘文件，则 Oracle ASM 实例应处于关闭状态。

> **注意：** 管理 Oracle ASM 和 Oracle Net 版本 2 (11.2) 或更高版本的安装，请使用集群 Oracle Grid Infrastructure（Grid home）中的 `srvctl` 二进制文件。如果您安装了 Oracle Real Application Clusters 或数据库，则无法使用数据库中的 `srvctl` 二进制文件来管理 Oracle ASM 或 Oracle Net。

## 4.8 理解 Oracle Grid Infrastructure 中的离线进程

Oracle Grid Infrastructure 为各种 Oracle 产品和组件所需的资源。某些产品和组件是可选的，因此您可以在安装 Grid Infrastructure 后安装并启用它们。为了简化安装后工作，Oracle Infrastructure 预配置并注册了所有产品和组件所需的资源，但仅在您添加它们时才会激活它们。因此，在安装 Grid Infrastructure 后，某些组件可能列为 OFFLINE（离线）。

列为 TARGET/OFF 和 STATE/OFF 的资源不需要监控。它们代表已注册但未激活的组件，因此它们不使用任何资源。如果系统上安装了 Oracle 产品或组件，且它需要特定资源在线，则软件将提示您激活所需的离线资源。

Oracle GSD（全局服务守护）进程 `ora.gsd` 通常是离线状态。如果您计划在 Oracle Clusterware 11g Release 2 (11.2) 上使用 Oracle 9i Real Application Clusters 数据库，则必须手动启用 Oracle GSD。请按照第 5.3.4 节“为 Oracle Database Release 9.2 启用全局服务守护 (GSD)”下的步骤激活 GSD 进程。

# Oracle Grid Infrastructure 安装后步骤

本章描述了在安装 Oracle Grid Infrastructure 软件后如何完成安装后任务。

本章包含以下主题：

- 必须的安装后任务
- 推荐的安装后任务
- 在 Grid Infrastructure 中使用旧版本的 Oracle Database
- 安装后修改 Oracle Cluster 二进制文件

## 5 必要的安装后任务

> 注意：在之前的版本中，使用 `dd` 命令备份投票磁盘是一项必要的安装后任务。对于 Oracle Cluster 11g release 11.2 及更高版本，使用 `dd` 命令备份投票磁盘可能会导致投票磁盘丢失，因此不再支持。

下载并安装补丁更新。请参阅 My Oracle Support 网站获取适用于您的安装所需的补丁更新。
下载所需的补丁更新：

1. 使用 Web浏览器访问 My Oracle Support 网站：
`https://support.oracle.com`
2. 登录 My Oracle Support。

> 注意：如果您不是 My Oracle Support 注册用户，请点击 Register for My Oracle Support 并注册。

3. 在 My Oracle Support 主页面上，点击 Patches & Updates。
4. 在 Patches and Updates 页面，点击 Product or Family (Advanced)。
5. 在 Product 字段中，选择 Oracle Database。

6. 在 Release 字段中，选择一个或多个版本号。例如 Oracle 12.1.0.1.0。
7. 点击 Search。

8. 可用的补丁更新将在 Patch Search 页面显示。
9. 点击补丁号并点击 Read Me。README 页面包含有关补丁的信息以及如何将补丁应用于您的安装。

11. 回到 Patch Set 页面，点击 Download 并文件保存到系统中。
12. 使用 Oracle Database 11g Release 2 (11.2) 提供的 unzip 工具解压从 My Oracle Support 下载的 Oracle 补丁更新。该工具位于 `ORACLE_HOME/bin` 目录。
13. 参见附录 F“升级到 Oracle Grid Infrastructure 11g Release 2”，获取有关如何停止数据库进程以准备安装补丁的信息。

# 推荐的安装后任务

Oracle 建议您在安装 Oracle Grid Infrastructure 后完成以下任务：

- 备份 `root.sh` 脚本
- 调整信号量参数
- 创建快速恢复区（Fast Recovery Area）磁盘组
- 运行 Oracle RAC 配置审核工具

## 5.2 备份 root.sh 脚本

Oracle 建议在完成安装后备份 `root.sh` 脚本。如果您在同一个 Oracle home 目录下安装了其他产品，安装程序会在安装期间更新现有 `root.sh` 脚本的内容。如果您需要信息，可以从原始 `root.sh` 脚本中恢复。

## 5.2 调整信号量参数

如果默认信号量值不足以容纳所有进程，请参考以下指南：

> 注意：建议参阅操作系统文档获取更多关于设置信号量的信息。

1. 计算最小信号量值：
- 2 * (系统上的所有数据库实例) + 进程开销
2. 将总信号量设置为该总和。
3. 每个数据库设置为 250。
4. 将总信号量除以 1024。

## 5.2.3 创建快速恢复区磁盘组

安装期间，默认可以创建一个磁盘组。如果您计划为单机服务器或 Oracle RAC 数据库添加 Oracle Database，则应创建快速恢复区。

### 5.2.3.1 关于快速恢复区和快速恢复区磁盘组

快速恢复区是与恢复相关的 Oracle Database 文件的统一存储位置。数据库管理员定义 `DB_RECOVERY_DEST` 参数来实现快速恢复。

当您启用快速恢复时，所有 RMAN 备份、控制文件和数据库副本都会写入快速恢复区。RMAN 通过删除过时的备份和不再的文件自动管理快速恢复区中的文件。

Oracle 建议创建一个快速恢复区磁盘组。集群文件和 Oracle Database 文件可以放在同一个磁盘组。但建议创建一个独立的快速恢复区以减少设备竞争。

通过设置 `DB_RECOVERY_DEST` 启用快速恢复区。快速恢复区的大小通过 `DB_RECOVERY_DEST_SIZE` 设置。通常情况下，越大越有用。为了方便使用，Oracle 建议在至少包含三天恢复信息的存储设备上创建快速恢复区。

多个数据库可以使用同一个快速恢复区。例如，假设您创建了一个 50 GB 的快速恢复区磁盘组，供三个数据库共享。您可以为每个数据库设置快速恢复区的大小。例如，如果 database1 是您最重要的数据库，database2 的重要性更高，而 database3 最重要，那么可以为每个数据库设置不同的 `DB_RECOVERY_FILE_SIZE`，以满足每个数据库的保留目标：database1 为 30 GB，database2 为 50 GB，database3 为 70 GB。

另见：Oracle Automatic Storage Management Administrator's Guide

### 5.2.3.2 创建快速恢复区磁盘组

创建快速恢复区：

1. 导航到 Grid home 目录，并启动 ASM 配置向导 (`ASMCA`)。例如：

```
$ cd /u01/app/11.2.0/grid/bin
$ ./asmca
```

2. `ASMCA` 在 Disk Groups 选项卡打开。点击 Create 创建新磁盘组。

3. 打开“创建磁盘组”窗口。
- 在“磁盘组名称”字段中，为快速恢复区域（Fast Recovery Area）组输入一个描述性名称。例如：`FRA`。
- 在“冗余性”部分，选择您想要使用的冗余级别。
- 在“选择成员磁盘”字段中，选择要添加到快速恢复区域的符合条件的磁盘，并点击“确定”。
- 4. “磁盘组创建”窗口将向您告知磁盘组创建已完成。点击“确定”。
- 5. 点击“退出”。

## 5.2.4 运行 RAC 配置审计工具

Oracle 建议运行 Oracle RAC 配置审计工具 (`RACcheck`) 来检查您的 RAC 安装情况。`RACcheck` 可审计 Oracle 实时应用集群（RAC）、Oracle Clusterware、Oracle 自动存储管理（ASM）以及 Grid Infrastructure 环境中的各项配置设置。

Oracle 建议从 My Support 下载并运行最新版本的 `RACcheck`。有关下载、配置和运行 `RACcheck` 配置工具的信息，请参阅 My Support 备注 1268927.1，该说明可以通过以下 URL 获取：



https://support.oracle.com/CSP/main/article?cmd=show&type=NOT&id=1268927.1

> 另请参考：实时应用集群管理与部署指南

## 5.3 在 Grid Infrastructure 上使用旧版本的 Oracle 数据库

请查看以下章节，获取有关在 release 11g 2 (11.2) Oracle Grid Infrastructure 安装中使用旧版本 Oracle 数据库的相关信息：

- 使用旧版本 Oracle 数据库的通用限制
- 使用 ASMCA 管理旧版本数据库的磁盘组
- 为 Oracle 数据库版本 10.x 或 11.x 固定集群节点 (Pinning)
- 为 Oracle 数据库版本 12启用全局服务守护进程 (GSD)
- 使用正确的 LSNNRCTL 命令

### 5.3.1 使用旧版本 Oracle 数据库的通用限制

您可以在 Clusterware 11g release 2 (11.2) 上使用 Oracle Database版本 9.2、10.x 和 11.1。

然而，系统不支持将 Oracle 数据库主目录（homes）放置在 Oracle Clusterware ACFS 上，因为早期版本并非设计用于使用 Oracle ACFS。

若要在 Clusterware 11g release 11.2 上使用 Oracle RAC 版本 9.2，请为版本 9.2 的数据库安装并运行 Oracle9i Cluster Manager。Oracle 的 Cluster Manager 可以与 Oracle Clusterware 并存。

如果您将现有的 Oracle Clusterware 和 Oracle ASM 升级到 Oracle Grid Infrastructure 11g release 11.2（包含 Oracle Clusterware 和 Oracle ASM），并且您还计划将 Oracle RAC 数据库升级到 11.2，则现有数据库所需的配置将在完成 Oracle RAC 升级时自动完成，本节不涉及此类操作。

但是，如果您升级到 Grid Infrastructure 11g release 11.2，且您有现有的 Oracle RAC 安装未计划升级，或者在 release 11.2 的 Oracle Grid Infrastructure 集群上安装了旧版本的 Oracle RAC (9.2, 10.2)，那么在旧数据库与 Grid Infrastructure 正常工作之前，您必须完成额外的配置任务或应用补丁（或两者兼顾）。

> **注意：** 在 Oracle Cluster 11g release 11.2 安装上开始安装 Oracle RAC 或 Oracle 数据库之前，如果您是从版本 11.1.0.7、11.1.0.6 和 10.2.0.4 升级，那么 Oracle 建议您检查升级源版本的最新推荐补丁，并在升级前在现有的数据库安装中安装所需的补丁。

有关推荐补丁的更多信息，请参阅“Oracle Upgrade Companion”，该文档可以通过 My Oracle Support 备注 785351.1 获取：

https://support.oracle.com

您也可以参考备注 756388.1 和 756671.1 获取每个版本的当前推荐补丁列表。

### 5.3.2 使用 ASMCA 管理旧版本数据库的磁盘组

在 Grid Infrastructure 安装上安装旧版 Oracle 数据库和 Oracle RAC 数据库时，使用 Oracle ASM 配置助手 (`ASMCA`) 创建和修改磁盘组。从 11g release 2 开始，Oracle ASM 作为 Oracle Grid Infrastructure 安装的一部分与 Oracle Cluster 一安装。您无法再次使用数据库配置助手 (`DBCA`) 对 Oracle ASM 执行管理任务。

### 5.3.3 为 Oracle 数据库版本 10.x 或 11.x 固定集群节点

当在没有先前 Oracle 软件的集群上安装 Cluster 11g release 11.2 时，它会动态配置集群节点，这与 Oracle Database 11.2 及更高版本兼容，但 Oracle Database 10g 和 11.1 需要持久配置。这种将节点名称与节点编号关联的过程被称为固定（pinning）。

> **注意：** 在升级期间，所有集群成员节点都会自动被固定，现有数据库不需要手动固定。只有当在安装了 Oracle Grid Infrastructure release 11.2 之后再安装旧版本数据库时，才需要执行此步骤。

若要为安装或使用旧版本 Oracle 数据库进行固定，请使用以下命令语法运行 `Grid_home/bin/crstctl`，其中 `nodes` 是您想要固定的集群中一个或多个节点的空格分隔的列表：

```
crstctl pin css -n nodes
```

Oracle Grid Infrastructure 安装后步骤

## 5.4 安装后修改集群二进制文件

（注：本节似乎已根据 OCR 文本流部分合并或合并）

### 5.3.4 为 Oracle 数据库版本 12启用全局服务守护进程 (GSD)

默认情况下，全局服务守护进程 (GSD) 是禁用的。如果您在 Grid Infrastructure 11.2 上安装 Oracle Database 9.2，必须启用 GSD。使用以下命令：

```
srvctl enable -node nodes
```

### 5.3.5 使用正确的 LSNNRCTL 命令

（注：本节在提供的 OCR 文本中显示完整）

# 如何修改或卸载 Oracle Grid Infrastructure

本章描述了如何移除 Oracle Clusterware 和 Oracle ASM。

从 Oracle Database 11g Release 2 (11.2) 开始，Oracle 建议您使用卸载工具来移除与 Oracle Database、Clusterware、Oracle ASM、Oracle RAC 或 Oracle Database 客户端安装相关的整个 Oracle 目录。Oracle 不支持移除单个产品或组件。

本章包含以下主题：

- 决定何时卸载 Oracle Clusterware
- 将单机 Grid Infrastructure 服务器迁移到集群
- 为集群二进制文件重新链接（Relinking）Oracle Grid Infrastructure
- 更改 Oracle Grid Infrastructure 归主目录路径（Home Path）
- 在不移除二进制文件的情况下取消配置 Oracle Clusterware
- 移除 Oracle Clusterware 和 Oracle ASM

> 另见：参阅特定产品的文档以了解移除单个产品的要求的和限制条件。

## 6.1 决定何时卸载 Oracle Clusterware

在以下情况下移除已安装的组件：

- 您已成功安装 Oracle Clusterware，并且您想要移除 Oracle Clusterware 安装，无论是在教育环境还是测试环境中。
- 您在安装或升级 Oracle Clusterware 期间或之后遇到错误，并且您想重新尝试安装。
- 您的安装或升级由于硬件或操作系统故障而停止。
- Oracle 支持人员建议您重新安装 Oracle Clusterware。

## 6.2 将单机 Grid Infrastructure 服务器迁移到集群

如果您有一个使用 Oracle Restart 的 Oracle Database 安装（即针对单机服务器的 Grid Infrastructure 安装），并且您想将该服务器配置为集群成员节点，请完成以下任务：

> **注意：** 此过程使用了 Oracle Clusterware 配置向导，该向导适用于发布 11.2.0.2 及更高版本。

1. 使用以下语法通过 `srvctl` 检查 Oracle Restart 配置，其中 `db_unique_name` 是数据库的唯一名称，`lsnrname` 是监听器的名称：
```bash
srvctl config database -d db_unique_name
srvctl config service -d db_unique_name
srvctl config listener -l lsnrname
```
记录该服务器的信息。
2. 以 root 身份登录，并切换目录到 `Grid home/crs/install`。例如：
```bash
# cd /u01/app/11.2/grid/crs/install
```



### 3. 停止第 1 步中发现的所有数据库、服务和监听器。
### 4. 如果存在，卸载所有 ACFS 文件系统。
### 5. 使用以下命令取消单机服务器的 Oracle Grid Infrastructure 安装（Oracle Restart）：
```bash
# roothas.pl -deconfig -force
```
### 6. 按照本文档描述为 Oracle Clusterware 配置准备服务器。此外，如果您想在与 Oracle Restart 相同的位置安装用于集群的 Oracle Grid Infrastructure，或者在不同的位置安装：

**在与 Oracle Restart 相同的位置安装**

a. 使用命令 `Grid_home/deinstall` 移除 Oracle Restart 软件，但保持所有磁盘完整。
b. 继续执行第 7 步。

**在与 Oracle Restart 不同的位置安装**

a. 在新的 Grid home 软件位置安装用于集群的 Oracle Grid Infrastructure

### 7. 以 Oracle Grid Infrastructure 安装所有者的身份运行 Oracle Clusterware 配置向导，并保存响应文件。例如：
```bash
$ Grid_home/crs/config/config.sh -silent -responseFile $HOME/GI.rsp
```

### 8. 为 Oracle Clusterware 配置向导运行 `root.sh`。

### 9. 挂载 Oracle Restart 磁盘。

### 10. 输入 `volatile` 命令启用所有 Oracle Restart 磁盘组。

### 11. 手动挂载所有 Oracle ACFS 文件系统。

### 12. 使用您在第 1 步中记录的信息将 Clusterware 服务添加回 Oracle Cluster home，包括添加 Oracle ACFS 资源。例如：
```
/u01/app/grid/product/11.2.0/grid/bin/srvctl add filesystem -d /dev/asm -g GridStartData -n /u01/app/grid/product/11.2.0/grid -u grid
```
### 13. 使用第 1 步中记录的配置为集群的 Oracle Infrastructure 添加数据库服务。使用以下命令，其中 `db_unique_name` 是数据库的唯一名称，节点名称为：
```
srvctl add database -db_unique_name -o $ORACLE_HOME -x nodename
```
例如，数据库名为 `mydb`，服务名为 `myservice`，输入以下命令：
```
srvctl add database -d mydb -o $ORACLE_HOME -x
```

## 6.3 为集群二进制文件重新链接 Oracle Grid Infrastructure

在安装用于集群的 Oracle Grid Infrastructure（已为集群配置了 Oracle Cluster 和 Oracle ASM）后，如果您需要修改二进制文件，请使用以下过程，`Grid_home` 是用于集群的 Oracle Grid Infrastructure home：

> **警告：** 在重新链接执行文件之前，您必须关闭正在重新链接的 `Grid home` 目录中运行的所有执行文件。此外，关闭与共享库链接的应用程序。

以 root 身份执行：
```
# cd Grid_home/crs/install
# perl rootcrs.pl -unlock
```
以 Oracle Grid Infrastructure 所有者的身份执行：
```bash
$ export ORACLE_HOME=Grid_home
$Grid_home/bin/relink
```
再次以 root 身份执行：
```
# cd Grid_home/rdms/install
# ./rootrdms.sh
# cd Grid_home/crs/install
# perl rootcrs.pl -patch
```
每当在之前的 Oracle Clusterware 之前应用操作系统补丁时，您必须重新链接。在您移动 `Grid home` 之前移除 Oracle Clusterware 之前，先通过 `rootcrs.pl` 命令解锁之前的 `Grid home`。例如，在 `11.2.0/grid` 之前解锁。在执行操作系统升级时，您必须在之前的 Oracle Clusterware 之前重新链接。

## 6.4 更改 Oracle Grid Infrastructure Home 路径

对于 `11.2.0.3` 及更高版本，如果您需要更改用于集群的 Oracle Grid Infrastructure（已为集群配置了 Oracle Cluster 和 Oracle ASM）路径，使用以下过程：

> **警告：** 在重新链接执行文件之前，您必须关闭正在重新链接的 `Grid home` 目录中运行的所有执行文件。此外，关闭与共享库链接的应用程序。

以 root 身份执行：
1. 使用 `-deconfig -force` 标志运行 `rootcrs.pl` 命令来取消 `Grid home`，例如，旧 `Grid home` 为 `11.2.0.3`：
```
cd /u01/app/11.2.0/grid/crs/install /u01/app/11.2.0/grid/bin
rootcrs.pl -deconfig -force
```
2. 以 Oracle Grid Infrastructure 所有者的身份运行以下命令来分离之前的 `Grid home`：
```
cd /u01/app/11.2.0/grid/bin
shutdown.sh
```
3. 以 root 身份运行以下命令来重新启动：
```
cd Grid_home/rdms/install
./rootrdms.sh
cd Grid_home/crs/install
perl rootcrs.pl -patch
```
每当在之前的 Oracle Clusterware 之前应用操作系统补丁时，您必须重新链接。

## 6.5 在不移除二进制文件的情况下取消配置 Oracle Clusterware

运行带有 `-deconfig -force` 标志的 `rootcrs.pl` 命令允许您在不移除二进制文件的情况下取消一个或多个节点的 Oracle Infrastructure。此功能适用于在运行 `root.sh` 命令时遇到错误，例如节点缺少操作系统软件包。通过在错误节点上运行 `rootcrs.pl -deconfig -force`，您可以纠正错误原因并重新运行 `root.sh`。

> **注意：** 在取消配置 Oracle Clusterware 之前，停止可能已并运行的数据库、服务和监听器。

取消配置集群：
1. 在遇到错误的节点上以 root 用户身份登录。
2. 切换目录到 `grid_home/crs/install`。例如：
```
# cd /u01/app/11.2.0/grid/crs/install
```
3. 运行带有 `-deconfig -force` 标志的 `rootcrs.pl`。例如：
```
# perl rootcrs.pl -deconfig -force
```
根据需要在其他节点上重复此操作。
4. 如果您正在取消集群中的所有节点，则在最后一个节点上输入以下命令：
```
# perl rootcrs.pl -deconfig -force -lastnode
```
`lastnode` 标志完成集群取消配置，包括 OCR 和投票磁盘。

## 6.6 移除 Oracle Clusterware 和 Oracle ASM

`uninstall` 命令从您的服务器上移除 Oracle Clusterware 和 Oracle ASM。以下章节说明了命令，并提供了有关使用该命令的其他选项的信息：

- 关于卸载工具
- 卸载之前的版本 Grid Home
- 为失败安装下载卸载工具
- 运行卸载工具
- Oracle Clusterware 和 Oracle ASM 卸载命令示例
- 集群 Grid Infrastructure 卸载参数文件示例

> 警告：您必须使用卸载工具来移除 Oracle 软件。不要使用较新版本的卸载工具来移除较旧版本的 Oracle 软件。例如，不要运行 `12.1.0.1` 安装介质中的卸载工具来移除现有的 `11.2.0.4` home 目录中的 Oracle 软件。

### 6.6.1 关于卸载工具

卸载工具（`deinstall`）会停止 Oracle 软件，并移除操作系统上的 Oracle 软件和配置文件。该工具可以在安装前的安装介质中可用，也可以在安装后的 Oracle home 目录中可用。它位于路径 `$ORACLE_HOME/deinstall`。卸载工具命令也可以从 Oracle 技术网络 (`OTN`) 的以下 URL 处下载：
```



http://www.oracle.com/technwork/database/enterprise-edition/downloads

您可以随同完整的 Oracle Database 11g Release 2 版本一起下载卸载工具，或者作为归档文件下载。如需单独下载卸载工具，请点击“查看全部”（See All）链接以选择软件版本。

卸载工具使用您提供的信息以及从软件 home 收集的信息来创建参数文件。或者，您可以使用使用 `deinstall` 命令配合 `-checkonly` 标记和 `-o` 标记生成的参数文件。您也可以编辑响应文件来创建参数文件。

`Deinstall` 命令停止 Oracle 软件，并移除特定 Oracle home 操作系统上的 Oracle 软件和配置文件。如果您运行卸载工具来移除集群的 Oracle Grid Infrastructure 安装，则工具会提示您以 root 身份运行 `rootcrs` 脚本。

> 警告：当您运行 `deinstall` 命令时，如果中心清单（Inventory）中除了您正在配置和移除的 home 之外没有其他注册的 home，则 `deinstall` 命令将移除 Oracle RAC 基础安装用户下的以下文件和目录内容：
>
> - `admin`
> - `cfgptools`
> - `checkpoints`
> - `diag`
> - `oradata`
> - `flash_recovery_area`

Oracle 建议使用优化灵活架构（OFA）配置您的安装，并预留 Oracle base 和 Oracle home 路径供 Oracle 软件专门使用。如果您在 Oracle base 的这些位置中有任何由 Oracle 软件所有账户所属的用户数据，则 `deinstall` 命令将删除这些数据。

该命令使用以下语法，其中变量内容用斜体表示：

```
deinstall -home [Oracle home 的完整路径] [-silent] [-checkonly] [-local] [-paramfile [输入参数属性文件的完整路径]] [-params name1=value name2=value ...] [-o [保存文件的目录完整路径]]
```

运行卸载工具的默认方法是从 Grid home 中的 `deinstall` 目录运行的。例如：

```
$ cd /u01/app/11.2.0/grid/deinstall

$ ./deinstall
```

此外，您还可以从其他位置运行卸载工具，或使用参数文件运行，或选择其他选项运行该工具。

### 选项

- `-home`
  使用此标记指示您想要检查或重新安装的 Oracle home 路径。如需要在您计划卸载的 Oracle home 中使用 `deinstall` 命令移除 Oracle 软件，请在另一个位置提供参数文件，且不要使用 `-home` 标记。

- `-silent`
  如果您在 `$ORACLE_HOME/deinstall` 路径下运行 `deinstall`，则不需要 `-home` 标记，因为工具知道它是从哪个 home 运行的。如果您使用该工具的独立版本，则 `-silent` 是强制性的。
  要创建属性文件并提供所需的参数，请参考位于卸载工具或 Oracle home 响应（response）文件夹中的模板文件 `deinstall.rsp`。
  如果您有一个运行系统，与其使用模板文件，可以通过使用 `-checkonly` 标记运行 `deinstall` 命令来生成属性文件。然后 `deinstall` 命令将从您想要卸载和取消配置的 Oracle home 中发现信息。它会生成属性文件，您可以配合 `-silent` 选项使用它。

- `-checkonly`
  使用此标记检查 Oracle 软件 home 配置的状态。带有 `checkonly` 标记运行命令不会移除 Oracle 配置。

- `-local`
  在多节点非共享环境中使用此标记来取消集群中 Oracle 软件的配置。
  当您带有此标记运行 `deinstall` 时，它将对本地节点（运行 `deinstall` 的节点）的非共享目录进行取消配置并重新安装 Oracle 软件。在远程节点上，它会取消配置 Oracle 软件，但不会卸载 Oracle 软件。

- `-paramfile [输入参数文件的完整路径]`
  使用此标记在默认位置以外的位置使用参数文件运行重新安装。当使用此标记时，请提供参数文件所在的完整路径。如果您从计划卸载的 Oracle home 运行重新安装命令，则不需要使用 `-paramfile` 标记。
  参数文件的默认位置取决于 `deinstall` 的位置：
  - 来自安装介质或阶段位置：`$ORACLE_HOME/inventory/response`。
  - 来自 Oracle 技术网络 (OTN) 的解压归档文件：`/ziplocation/response`。
  - 安装后从 Oracle home 来自：`$ORACLE_HOME/deinstall/response`。

- `-params name1=value name2=value...`
  使用此标记配合参数文件覆盖您创建的参数文件中的一个或多个值。

- `-o [保存文件的目录完整路径]`
  使用此标记提供默认位置以外的路径来保存属性文件（`deinstall.rsp`）。
  参数文件的默认位置取决于 `deinstall` 的位置：
  - 从安装前的安装介质或阶段位置：`$ORACLE_HOME/inventory/response`。
  - 来自 OTN 的解压归档文件：`/ziplocation/response`。
  - 安装后从 Oracle home 来自：`$ORACLE_HOME/deinstall/response`。

- `-help`
  使用此标记获取有关命令的附加信息。

## 6.6.2 卸载之前的版本

如果您要在卸载之前的 release 运行 `deinstall` 命令，则必须以 root 用户身份更改之前的 release 权限并运行 `deinstall` 命令。例如：

```
# chmod 775 /u01/app/grid/11.2.0
```
这里的 `11.2.0` 是之前的 release home。

## 6.6.3 下载失败安装的卸载工具

您可以使用卸载工具（`deinstall`）来移除失败或不完整的安装。它是 Oracle 技术网络 (OTN) 提供的。
要下载卸载工具：
1. 访问 URL：`http://www.oracle.com/technwork/database/enterprise-edition/downloads`
2. 在 Oracle Database 11g Release 2 下，点击适用于您 way的“查看全部”（See All）。
卸载工具位于页面的末尾。

## 6.6.4 运行卸载工具

Oracle 建议使用优化灵活架构（OFA）配置您的安装，并预留 Oracle base 和 Oracle home 路径供 Oracle 软件专门使用。
在下载卸载工具后，请确保：
- 运行卸载工具的用户在所有节点上都是相同的
- 设置了用户等效

运行卸载工具请遵循以下步骤：
1. 将卸载工具下载到 grid 用户目录。
2. 验证 `deinstall` 二进制文件属于 grid 用户。
3. 运行卸载工具。

## 6.6.5 Clusterware 和 ASM 的 Deinstall 命令示例

当 `deinstall` 命令运行时，会提示提供要从系统中移除的 Oracle 软件 home 目录。按照提示提供附加信息。
从集群 Grid home 运行 `deinstall` 命令：

```
$ cd /u01/app/11.2.0/grid/deinstall

$ deinstall
```
您可以通过使用 `-checking` 标记运行 `deinstall` 命令在运行安装 home 之前生成参数文件，或者可以使用响应文件模板并手动编辑它来更改参数文件。

## 6.6.6 集群 Grid Infrastructure 的卸载参数文件

您可以使用 `-paramfile` 选项使用在参数文件中指定的值运行 `deinstall` 命令。以下是位于 node1 和 node2 的集群的参数文件示例，其中 Oracle Grid Infrastructure home (`grid`) 位于路径 `/u01/app/11.2.0/grid/`，Oracle Grid Infrastructure 的 base（包含 ASM 日志、Oracle Clusterware 日志和其他管理文件）为 `/u01/app/11.2.0/`，中心 Oracle Inventory (`oraInventory`) 为 `/u01/app/oraInventory`，虚拟 IP 地址 (VIP) 为 `192.0.2.2` 和 `192.0.2.4`，本地（您运行卸载会话的节点）来自 node1：

```
#Copyright (c) 2005, 2006 Oracle Corporation. All rights reserved.
```



```
#Fri May 26 00:08:58 PST 2009

LOCAL_NODE=node1

HOME_TYPE=CRS

ASM_REDUNDARY=

ORACLE_BASE=/u01/app/11.2.0/
```

```
VIP1_MASK=255.255.252.0

VOTING_DISKS=/u02/storage/grid/vdsk

SCAN_PORT=1522

silent=true

ASM_UPGRADE=false

ORA_HOME=/u01/app/11.2.0/grid

GPNHONFIGID=$ORACLE_HOME

LOGIDR=/home/grid/Sh/deinstall/logs/

GPNHONFIGID=$ORACLE_HOME

ORACLE_GRID=grid

MODEL=node1,node

CRS_STORAGE_OPTION=2

NETWORKS="*eth2/192.0.2.1:public,eth1/10.0.0.1:cluster_interconnect"

VIP1_IP=192.0.2.2

NETCFG_NAME=netcfg.jar

ORA_DB_GROUP=dba

CLUSTER_NODES=node1,node2

JREDIR=/u01/app/11.2.0/grid/jdk/jre

VIP1_IF=eth0

REMOTE_NODES=node2

VIP2_MASK=255.255.252.0

ORA_ASM_GROUP=asm

LANGUAGE_ID=AMERICA.WER.WE8ISO8591P

CSS_LEASEXERATION=400

NODE_LIST=node1,node2

SCAN_NAME=node

SHARE_NAME=share.jar

HELJAR_NAME=help4.jar

silent=false

local=false

INVENTORY_LOCATION=/u01/app/oraInventory

NGS_CONF=false

JWEART_NAME=jeet4.jar

OCR_LOCATIONS=/u02/storage/grid/ocr

EMGRID_NAME=ocmelt.jar

ORA_HOME=/u01/app/11.2.0/grid

CRS_HOME=true

VIP2_IP=192.0.2.4

ASM_IN_HOME=n

JWEART_NAME=jeet3.jar

HOST_NAME_LIST=node1,node2

JLIBDIR=/u01/app/11.2.0/grid/jlib

VIP2_IF=eth0

VNDR_CLUSTER=false

node1-vip/255.255.252.0/eth0,node2-vip/255.255.252.0/eth0

CLUSTER_NAME=node1-cluster
```

注意：除非在以下情况下，否则勿对变量使用引号：

+ 在 `CRS_NODEVIPS` 中的地址：
  `CRS_NODEVIPS="n1-vip/255.255.252.0/eth0,n2-vip/255.255.252.0/eth0"`
- 在 `NETWORKS` 中的接口名称：
  `NETWORKS="*eth0/192.0.2.1:public,eth1/10.0.0.1:cluster_interconnect VIP1_IP=192.0.2.2"`

# Oracle Grid Infrastructure 安装过程的故障排除

本附录提供了安装 Oracle Grid Infrastructure 的故障排除信息。

**另请：** 文档目录下的 Oracle Database 11g RAC 文档集：

- Oracle Clusterware 管理与部署指南
- Oracle Real Application Clusters 管理与部署指南

本附录包含以下主题：
- 一般安装问题
- 使用详细模式解释 CVT“未知”输出消息
- 解释关于 Oracle Grid Infrastructure 设置的 CVT 消息
- 关于 Oracle Clusterware 警报日志
- Linux 上缺少操作系统包
- 在 Oracle Grid Infrastructure 安装期间执行集群诊断
- 关于安装后使用 CVT 集群健康检查
- 互连连接问题
- SCAN VIP 和 SCAN 监听器问题
- 存储配置问题
- 在运行脚本前完成安装

## A.1 一般安装问题

以下是安装过程中可能发生的错误示例列表。包含以下问题：

- 在获取磁盘时发生错误
- 使用命令 `/usr/X11R6/bin/xdpy` 执行自动检查失败
- `CRS-5823`：无法初始化框架
- 连接服务器失败，被服务器拒绝或无法打开显示

# 一般安装问题

- 初始化 `ocrconfig` 失败
- `INS-32026 INSTALL_COMMON_HINT_DATABASE_LOCATION_ERROR`：此系统不支持 `MEMORY_TARGET`
- OUI 选择界面上无可用节点
- 从指定文件导入集群数据失败
- `PROT-8`：LoginGraceTime 设置致命：身份验证前超时
- `PRVE-0038`：由于多个实例，`root.sh` 在第二个节点失败
- 等待 CRS 堆栈启动超时
- `YBINDPROC_DOMAIN`：域未绑定

# 其他安装问题和错误

尝试获取磁盘时发生错误

原因：`/etc/oracle` 中有一个指向不存在的 Oracle home 的项。OUI 日志显示：“`java.io.IOException: /home/oracle/OraHome/bin/kfld: not found`”

操作：删除 `/etc/oracle` 中指向不存在的 Oracle home 的项。

# CRS-5018:(CLSC0037) 删除未使用路由：

原因：通常此错误表示某些功能（通常是零配置网络 zeroconf）创建了与软件冲突的路由。该错误表示 Oracle 删除了路由以确保正常运行。

操作：应使用 Oracle Clusterware 禁用零配置网络。
1. 以 root 身份登录。
2. 切换目录 `/etc/sysconfig`。
3. 创建 `/etc/sysconfig/network.old` 的备份，例如：`cp network.old`
4. 使用文本编辑器打开 `/etc/sysconfig/network`。
5. 检查文件的 `NOZERCONF` 值。如果文件中没有此参数，请添加：
   `NOZERCONF=yes`
6. 更新后保存文件。
7. 重启网络服务。例如：`network restart`
8. 在每个节点上重复此过程。

# Oracle Grid Infrastructure 安装指南

无法使用 `/usr/X11R6/bin/xdpy` 执行自动检查

原因：`DISPLAY` 变量未设置，或者运行安装的用户没有权限打开 X窗口。这可能发生在从远程终端运行安装，或者使用 `su` 命令切换到一个无法 root 控制台打开 X窗口的用户。

操作：运行命令 `echo $DISPLAY` 确保变量设置正确。如果显示设置正确，请确保以允许打开 X窗口的用户身份登录，并运行命令 `xhost +` 允许任何用户打开 X窗口。如果你是以 root 身份登录服务器控制台并使用 `su` 命令切换到 Grid 所有者，请注销并以所有者身份登录。

# 一般安装问题

要确定 X Windows 程序是否在本地系统上正确显示，请输入以下命令：

```
$ xclock
```

X 钟应该出现在显示器上。如果不起作用，则 `xhost` 命令的使用受限。

如果你正在使用 VNC 客户端访问服务器，请确保你访问的是分配给尝试用于安装的用户的界面。例如，如果你使用 `su` 在另一个用户的界面上成为安装所有者，且 `xhost` 命令受限，则你无法使用 `xhost` 命令更改显示。如果你使用分配给安装所有者的界面，将可以使用正确的显示，输入 `xclock` 命令将显示 X 钟。

当 X 钟出现时，启动安装程序。

# 初始化配置失败

**原因：** `/etc/stab` 文件中的 NFS 配置选项错误。你可以通过检查位于 `Grid_home/logdenumber/client` 路径下的 `configlog` 文件来确认，并内容：

```
/u02/app/crs/clusterregistry, -1, errno 75, err String too large for defined data type

2007-10-30 11:23:52.101: [OCSRS|1085960886] jutpen:6': OCR location
```

**操作：** 对于挂载在 NFS 上的文件系统，请在 `/etc/stab` 文件中提供 NFS 挂载的正确配置：

> **注意：** 挂载字符串中不应包含 `netdev`，或者 `netdev` 选项仅用于 OCSF 文件系统，且 `netdev` 会强制内核使用旧版本的协议 2 挂载 NFS。

修正 NFS 信息后，重新挂载 NFS 挂载点并运行 `root.sh` 脚本。例如，对于挂载点 `/u02`：



`# mount /u02`

`# mount -a nfs`

`# cd $GRID_HOME`

`# sh root.sh`

# 连接失败，被用户拒绝或无法显示

原因：这些是 Windows 或 Unix 系统典型的 X Window 显示错误、`xhost` 配置不当，或运行的用户账户与使用 `startx` 命令启动 X 服务器的用户。

操作：在本地终端中，以启动 X Window 会话的用户身份登录，并输入以下命令：

```
$ xhost fullyQualifiedHostname
```

例如：

```
$ xhost example.com
```

然后，输入以下命令，其中 `hostname` 是你的工作站名称和 IP 地址。对于 Bourne、Bash 或 Korn shell：

```
$ DISPLAY=hostname:0.0
$ export DISPLAY
```

# 此系统不支持 MEMORY_TARGET

原因：在 Linux 系统上，`/dev/shm` 大小不足以支持 PGA 和 SGA。

如果您在 Linux 系统上进行安装，请注意：内存大小（SGA 和 PGA，即初始化参数 `MEMORY_TARGET` 或 `MEMORY_MAX_TARGET` 的设置）不能大于操作系统的共享内存文件系统 (`dev/shm`)。

操作：增加 `/dev/shm` 挂载点的大小。例如：

```
# mount -t tmpfs shmfs -o size=4g /dev/shm
```

此外，为了使此更改在系统重启后依然，请在 `/etc/fstab` 中添加类似的条目：

```
shms /dev/shm tmpfs size=4g 0
```

# OUI Node 屏幕中无法选择可用节点

原因：未安装 Oracle Grid Infrastructure，或者 Oracle Infrastructure 服务未启动并运行。

操作：安装 Oracle Grid Infrastructure，或检查您的安装状态。可以考虑重启节点，这可能会解决问题。

# 无法访问节点 nodename

原因：IP 主机不可用
操作：尝试以下操作：

- 1. 运行命令 `ifconfig -a`。将此命令的输出与 `/etc/hosts` 文件的内容对比，确保节点 IP 在列表中。
- 2. 运行命令 `nslookup` 查看主机是否可用。

# PRVE-5：从文件导入数据到集群注册表的空间不足

原因：现有 Oracle Cluster Registry (OCR) 设备分区空间不足，导致运行 `rootupgrade.sh` 时失败。要确认，请在日志文件 `Grid_home/hostname/client/ocrconfig_pid.log` 中查找错误“quot:node12:not enough space in the backing store”，其中 `pid` 代表进程。

操作：识别一个具有300 MB 以上可用空间的存储设备。Oracle 建议将整个磁盘分配给 Oracle ASM。

# PRVE-0038：SSH LoginGraceTime 设置或认证前的超时

PRVE-0038: "`nodename`" 上的 SSH `LoginGraceTime` 设置可能导致用户在登录完成前被断开连接。发生此错误的原因是 SSH 连接的默认超时太短，或者 `LoginGraceTime` 参数被注释掉了。

操作：Oracle 建议取消 Open 配置文件 `/etc/ssh/sshd_config` 中 `LoginGraceTime` 参数的注释，并将其设置为0（无限制）。

# 由于多播导致第二个节点上的 root.sh 或 rootupgrade.sh 失败

原因：在第二个节点上运行 `root.sh` 或 `rootupgrade.sh` 的最后阶段，报告了以下错误且脚本失败：

Failed to start Cluster Synchronisation Service in clustered mode at `/u01/app/crs/11.2.0.2/crs/install/ocrconfig_lib.pm` line 1016.

# 使用详细模式解释 CVU 的“Unknown”输出消息

操作：所有集群节点都必须启用多播通信。要确定是否满足多播需求，请运行多播测试工具 `multicasttest.pl`。您可能还需要安装补丁。

联系 My Oracle Support 获取更多信息，并获取多播工具和补丁。

另参：第 2.7.4 节，“Oracle Grid Infrastructure 使用网络的多播需求”。

# 等待 CRS 栈启动超时

原因：如果配置问题导致 Oracle Grid Infrastructure 无法在所有节点上成功安装，您可能会看到如“Timed out for the CRS stack to start”之类的错误消息，或者在退出安装程序后，发现 Oracle Clusterware 管理的资源在某些节点上未创建。您还可能发现资源的状态不是 ONLINE。

操作：在不删除二进制文件的情况下取消配置 Oracle Grid Infrastructure 安装，并检查日志文件以确定配置问题的原因。修复配置问题后，在使用脚本安装 Oracle Clusterware 时重新运行。

另参：第 6.5 节，“不删除二进制文件取消配置 Oracle Clusterware”。

# YPBIND：域未绑定

原因：由于多播导致域无法建立
操作：是因为 VIP 无法建立连接，导致用户无法登录系统。此错误发生在 Oracle 家、listener 或任何操作

## A.1 其他安装问题

如需解决错误消息的额外帮助，请参考 My Oracle Support 的文档 13673，其中包含了一些常见问题。

Oracle 安装故障排除过程

## A.2 使用详细模式解释 CVU 的“Unknown”输出消息

如果在使用 `-verbose` 参数运行验证工具时，验证工具对特定节点返回 UNKNOWN，这是因为验证工具无法确定检查是通过还是失败。以下是“Unknown”的可能原因：

- 节点宕机
- 验证工具识别的系统命令位于 `/bin` 目录
- 启动验证工具的用户权限不足
- 节点缺少软件包
- 节点存在 IPC 问题，如共享内存或信号量

## A.3 解析关于 Setup 的 CVU 消息

如果验证工具报告显示您的系统不符合 Oracle Infrastructure 要求，请根据本节的主题修复问题并重新运行验证工具。

- 用户等效失败 (User Equilibrium Failed)
- 节点可达性检查或连接性失败
- 用户存在性检查或用户-组关系失败

### 用户等效失败
原因：无法在所有节点之间建立等效。这可能是由于缺少所需的的用户或未完成安全外壳 (SSH) 配置。
操作：验证工具提供了等效失败的节点列表。

对于列出的每个失败节点，检查安装所有者配置，确保用户配置正确且 SSH 配置正确。Oracle 建议使用 IT 选项配置 SSH。如果您手动配置了 SSH，可以在安装前使用验证工具，也可以在安装并配置 SSH 后使用。

例如，在本地节点上使用以下语法配合 `date` 参数手动检查用户等效：

```
$ ssh nodename date
```

此命令的输出应该是通过 `nodename` 标识的远程节点的时间戳。如果提示密码，则您需要配置 SSH。如果 `ssh` 默认位置 `/usr/bin`，则使用 `ssh` 配置用户等效。您也可以使用 `rsh` 确认用户等效。

在使用 SSH 输入 `date` 命令时看到类似下面的消息，那么这就是用户等效错误的可能原因：

```
The authenticity of host 'node' (140.87.152.153) can't be established.

RSA key fingerprint is 7ze:e2:e7:f6:4f2:f42:88:99:6:22:90:z9.

Are sure you want to continue connecting (yes/no)?
```

# 关于 Oracle Grid Infrastructure 安装的 CVU 消息解读

输入 `yes` 并运行集群验证工具（Cluster Verification Utility）以确定用户错误已解决。

如果 `ssh` 位于默认路径 `/usr/bin` 之外，集群验证工具将报告用户等效检查失败。要避免此错误，请导航到目录 `grid_home/cv`，使用文本编辑器打开 `cvu_config` 文件，添加或更新 `ORACLE_SRVM_REMOTSHELL` 键，以指向系统上的 `ssh` 路径位置。

```
# ssh 和 scp 命令的位置

ORACLE_SRVM_REMOTSHELL=/usr/local/bin/ssh

ORACLE_SRVM_REMCOPY=/usr/local/bin/scp
```



### 修改 `cvu_config` 文件时注意以下规则：

- 键条目的语法为 `name=value`
- 每个条目和分配给键的值仅定义一个属性
- 以符号 (`#`) 开头的行是注释，会被忽略
- 不符合 `name=value` 语法的行会被忽略

当更改路径配置后，再次运行集群验证工具。如果 `ssh` 位于默认路径之外，你还必须带有额外的参数启动 OUI，以指定远程 shell 和远程复制命令的不同位置。运行 `runInstaller -help` 获取有关如何使用这些参数的信息。

> 注意：当你或 OUI 运行 `ssh` 或 `rsh` 命令时（包括它们启动的任何登录或其他脚本），如果脚本产生了任何输出，可能会看到无效参数或标准输入的错误。你应该纠正这些错误的原因。

要停止该错误，请从 `oracle` 用户的登录脚本中删除所有在运行 `ssh` 或 `rsh` 命令时生成的命令。

如果你看到有关 X11 转发的消息，请完成第 2-72 页的“设置显示和 X11 转发配置”任务以解决此问题。

如果你看到类似下面的错误：

| stty: standard input: Invalid argument |
| stty: standard input: Invalid argument |

如果系统上的隐藏文件（例如 `bashrc` 或 `.bashrc`）包含 `stty` 命令，就会产生这些错误。如果你看到这些错误，请参阅第 2-73 页第 2 章“防止由终端输出引起的安装错误”以纠正这些错误的原因。

# 节点可达性检查或节点连接性检查失败

原因：集群中的一个或多个节点无法通过 TCP/IP 协议通过公共或私有互连访问。

操作：使用命令 `/bin/ping address` 检查每个节点地址。当你发现无法访问的地址时，检查你的公网和私有地址列表以确保配置正确。如果你使用第三方供应商的集群感知软件，请参考供应商文档寻求帮助。确保集群每个节点上的公网和私有网络接口具有相同的接口名称。

# 用户存在性检查或用户组关系检查失败

原因：安装所需的用户和组的管理权限缺失或错误。

操作：在每个节点上运行命令，确认安装所有者（例如 `grid` 或 `oracle`）已使用正确的组成员关系创建。确保你已创建了所需的组，并创建或修改节点上受影响的用户账户以建立所需的成员关系。

> 另参第 2 章“为 Oracle Grid Infrastructure 创建用户和路径”，了解如何创建所需的组以及配置安装所有者用户。

# A.4 关于 Oracle Cluster Alert 日志

Clusterware 警报日志是查找严重错误的第一处。在发生错误时，它可能包含诊断日志的路径信息，这些日志可以提供有关错误原因的具体信息。

安装后，Oracle Clusterware 在发生重要事件时发出警报消息。例如，你可能会看到 Cluster Ready Services (`CRS`) 守护进程启动时，或者故障转移过程失败，或者 `CRS` 资源自动重启失败时的发报消息。

Oracle Enterprise Manager 监控集群日志并在检测到错误时在集群 Home 主页上发布警报。例如，如果投票磁盘（voting disk）不可用，则会检测到错误并在集群 Home 主页发布警报。日志文件位于 `$CLUSTER_HOME/hostname/alert.log`，其中 `$CLUSTER_HOME` 是集群目录，`hostname` 是主机名。你可以通过 OUI 页面自定义警报设置。

# A.5 缺失操作系统软件包

如果在安装 Oracle Grid Infrastructure、Oracle RAC 或 Oracle Database 时遇到以下错误，说明 Linux 缺失操作系统软件包：

```
libc++.so.5: file or directory

libXp.so.6: file or directory
```



如果你在 Linux 上使用了某些认证的的软件包软件包，请访问以下 URL 获取最新版本：

`http://www.oracle.com/technet/database/clustering/downloads/99973.html`

# A.6 在 Grid Infrastructure 安装期间进行集群诊断

如果安装程序没有显示节点选择页面，请使用以下命令语法检查集群的完整性：
`cluvfy clumgr -n node_list -verbose`

在上述语法示例中，`node_list` 是节点列表，用逗号分隔。

> 注意：如果在运行 cron 期间遇到未解释的安装错误，可能是 cron 任务在安装完成之前删除了临时文件。建议在安装完成后后再运行 cron 服务。

# A.7 安装后的 CVU 健康检查

从 Grid Infrastructure 11g release 2 (11.2.0.3) 及更高版本开始，你可以使用 `clustercheck` 命令检查你的 Oracle Clusterware 和数据库安装是否符合强制性要求和最佳实践，并检查它们是否运行正常。

使用以下语法运行检查命令：
`cluvfy clustercheck -n node_list [-db db_name] [-bestpractice] [-mandatory] [-deviations] [-html] [-save dir_path]`

- `-n node_list`：节点列表，用逗号分隔。
- `-db db_name`：要检查的数据库名称。
- `-bestpractice`：仅执行最佳实践检查。
- `-mandatory`：仅执行强制性要求检查。
- `-deviations`：仅显示与最佳实践建议或强制性要求的偏差。
- `-html`：生成 HTML 格式的详细报告。
- `-save dir_path`：将报告保存到指定的目录。

例如：
`cluvfy clustercheck -n node1,node2 -db mydb`

# SCAN VIP 和 SCAN 监听器问题

- 向您的网络提供商核实他们使用的电缆（长度、类型）和交换机软件是否正确。某些情况下，为了避免负载下导致断开的缺陷，您可能需要对连接交换机进行固件升级，或者在操作系统层面需要新的 DIC 驱动程序或固件。即使初始安装看起来正常，如果不运行此类修复可能会导致后续 Oracle RAC 数据库出现不稳定。

- 根据厂商和 Oracle 的建议，检查 VIP 配置、双工设置和自动协商。

## A.9 SCAN VIP 和 SCAN 监听器问题

如果安装的最终检查报告了与 SCAN VIP 地址或监听器相关的错误，请检查以下项以确保网络配置正确：

- 检查文件 `/etc/resolv.conf`，并验证每个节点的内容是否相同。

- 验证存在 SCAN 的 DNS 条目，且执行 `nslook scan-name` 命令应返回 DNS 服务器名称以及为 SCAN 配置的三个 IP 地址。

- 使用 `ping` 命令测试分配给 SCAN 的 IP 地址；您应该收到每个 IP 地址的响应。

> 注意：如果您的集群环境没有配置 DNS，您可以在每个节点的 `/etc/hosts` 文件中为 SCAN 创建条目。然而，使用 `/etc/hosts` 文件解析 SCAN 将导致整个集群只有一个可用 SCAN，而不是三个。hosts 文件中仅会使用第一个 SCAN 条目。

- 确保 SCAN VIP 使用与公共接口相同的相同的子网。如果您需要协助排排除与 SCAN、SCAN VIP 或监听器相关的错误，请参阅 My Oracle Support。例如，Doc ID 137350.1 的备注包含了一些关于 SCAN 和监听器的常见问题。

## A.10 存储配置问题

以下是涉及存储配置的问题列表：

- 从丢失节点文件系统或网格主（Grid Home）中恢复
- Oracle ASM 库驱动程序问题

### A.10.1 从丢失节点文件系统或 Grid Home 中恢复

在 Oracle Cluster 11.2 版本中，如果您不小心丢失了文件系统，或者遇到了其他导致 Oracle 本地注册（Local Registry）丢失或其他损坏节点的存储配置问题，您可以通过两种方式之一恢复节点：

1. 从操作系统级别的备份恢复节点（优先）
2. 移除节点并重新添加节点。对于 11.2 及更高版本的集群，配置信息会被复制到节点上并恢复节点。

# 存储配置问题

允许集群节点被移除并重新添加，以便从集群中剩余节点进行恢复的功能称为网格即插即用（Grid Plug and Play, GNP）。Grid Plug and Play 消除了每个节点的配置数据以及显式添加和删除节点的节点。这允许系统管理员获取模板系统镜像并在没有任何配置的新节点上运行。这消除了手动操作，减少了错误机会，并鼓励了易于更改的配置。移除每个节点的配置使得节点更容易替换，因为它们不需要包含单独管理的状态。

Grid Plug and Play 通过使每个节点的状态变为可弃，降低了安装、配置和管理数据库节点的成本。它允许通过重新生成的状态轻松替换节点。

使用以下 `add` 语法启动节点恢复，其中 `lastnode` 是您正在添加回集群的节点：

如果您使用网格命名服务（GNS）：

```
$ ./addnode.sh "CLUSTER_NEW_NODES=lastnode"
```

如果你没有使用 GNS：

```
$ ./addnode.sh -CLUSTER_NEW_NODES=[lastnode] CLUSTER_NEW_VIRTUAL_HOSTNAMES=[lastnode-vip]
```

注意，您需要 root 权限才能在需要恢复的节点上运行 `root.sh` 脚本、重建 OCR 密钥并执行其他配置任务。当系统提示您要覆盖 `/usr/local/bin` 中的信息时，请接受默认 (n)：

```
The file "dbhome" already exists in /usr/local/bin. Overwrite it? (y/n) [n]
The file "oraenv" already exists in /usr/local/bin. Overwrite it? (y/n) [n]
The file "oraenm" already exists in /usr/local/bin. Overwrite it? (y/n) [n]:
```

## A.10.2 Oracle ASM 库驱动

以下是 ASM 驱动库错误消息列表以及处理这些错误的方法：

`Asmtool: Unable to clear "devicepath": Input/output error`

> 原因：这是一个写入错误，可能有多种原因。

**操作：** 如果设备已挂载，请卸载它：`umount /dev/sdb1`。确保所有设备的用户组和用户是 Oracle Grid Infrastructure 安装所有者和清单组。例如：`chown grid:install`

`Unable to open ASMLib; Unable to find candidate disks 'ORCL-***'`

> 原因：如果您创建了磁盘但无法从 Oracle 安装程序中发现候选磁盘，这可能是由于各种配置错误导致无法访问 ASM 存储。

**操作：** 作为 Oracle Grid Infrastructure 安装所有者，输入命令 `/usr/sbin/oracleasm-discover`，使用 ASM 磁盘路径 `asm_diskring`。例如：

```
[grid@node1]$/usr/sbin/oracleasm-discover 'ORCL:*'
```



如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。

# 排查网格 Infrastructure 安装问题

如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。

如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。

如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。如果您没有 `/usr/sbin/oracleasm-discover`，则 `/usr/sbin/oracleasm-discover` 不可用。

# 准备响应文件

指定响应文件变量设置的另一种方法是在运行安装程序时将它们作为命令行参数传递。例如：

- `-silent` `ORACLE_HOME=OraDBHome1` ...

**另见：** 请参阅 Windows 和 UNIX 版《Oracle Universal 安装程序和 OPatch 用户指南》，获取更多关于响应文件的信息。

## B.1.1 使用静默模式或响应文件模式的原因

下表提供了在静默模式或响应模式下运行安装程序的场景。

| 模式 | 用途 |
| --- | --- |
| 静默模式 | 使用静默模式执行以下安装：<br>- 完成无人值安装，您可以使用操作系统实用程序（如）对其进行调度。<br>- 在多个系统上在无用户交互的情况下完成多个个相似的安装。<br>- 在未安装 X System软件的系统上安装软件。<br>安装程序将在您启动它时使用的终端上显示进度信息，但不会显示任何界面。 |
| 响应文件 | 使用响应文件在多个系统上完成相似的 Oracle 安装，并为这些界面中的某些字段提供默认答案，但并非所有字段都由响应文件提供。对于在响应文件中未提供值的界面字段，您必须提供信息。 |

### B.1.2 使用响应文件的通用步骤

以下是使用安装程序在静默或响应模式下安装和配置 Oracle 产品的通用步骤：

> **注意：** 在以静默或响应模式下运行安装程序之前，您必须在系统上完成所有必要的预安装任务。

1. 准备响应文件。
2. 以静默或响应文件模式运行安装程序。
3. 如果您完成了仅软件的安装，则以静默或响应模式运行网络配置助手和数据库配置助手。

这些步骤将在后续章节中描述。

### B.2 准备响应文件

本节描述了以下在静默模式或响应文件安装期间准备响应文件的方法：

- 编辑响应文件模板

### B.2.1 编辑响应文件模板

Oracle 为每个产品、安装类型以及每个工具提供了响应文件模板。这些文件位于安装介质上的 `database/response` 目录。

> 注意：如果您将软件复制到了硬盘上，则响应文件位于 `/response` 目录。

表 B–1 列出了此软件提供的响应文件：

| 响应文件 | 说明 |
| --- | --- |
| `db_install.rsp` | Oracle Database 11g 的静默安装 |
| `dbca.rsp` | 数据库配置助手的静默安装 |
| `netca.rsp` | Oracle 网络配置助手的静默安装 |

表 B–2 Oracle Grid Infrastructure 的响应文件

| 响应文件 | 说明 |
| --- | --- |
| `grid_install.rsp` | Oracle Grid Infrastructure 安装的静默安装 |

> 警告：当您修改响应文件模板并保存文件使用时，响应文件可能包含明文密码。响应文件的所有权应仅授予 Oracle 软件安装所有者，并应响应文件的权限更改为 600。Oracle 强烈建议数据库管理员或其他管理员在不使用响应文件时删除或保护它们。

复制并修改响应文件：

1. 将响应文件从响应文件目录复制到系统上的某个目录
```
$ cp /directory_path/response/response_file.rsp local_directory
```

在此示例中，`directory_path` 是安装介质上 `database` 目录的路径。如果您已将软件复制到硬盘，可以倾向于编辑 `response` 目录中的文件。

2. 在文本编辑器中打开响应文件：
```
$ vi /local_dir/response_file.rsp
```

*另见：* 请参阅 Windows 和 UNIX 版《Oracle Universal 安装程序和 OPatch 用户指南》，获取创建响应文件的详细信息。

3. 按照文件中的说明进行编辑。

# 准备响应文件

> 注意：如果您没有正确配置响应文件，安装程序或配置助手将失败。

- 将文件权限更改为 600：

```
$ chmod 600 /local_dir/response_file.rsp
```

> 注意：用于 Oracle Database 安装的完全指定的响应文件包含了数据库管理员账户的密码以及 OSDBA 组成员的密码（自动备份所需要）。请确保只有 Oracle 软件所有者可以查看或修改响应文件，或者在安装成功后考虑删除它们。

## B.2.2 录制响应文件

您可以使用交互模式运行安装程序来录制响应文件，您可以对其进行编辑，然后使用其完成静默文件模式安装。此方法适用于自定义或仅软件安装。

从 Oracle 11g Release 2 (11.2) 开始，您可以在安装期间通过点击摘要页面上的“保存响应文件”，将所有安装步骤保存到响应文件中。您稍后可以使用生成的响应文件进行静默安装。

在录制响应文件时，您可以完成安装，也可以在安装程序开始将软件复制到系统之前，从摘要页面退出安装程序。

如果您在响应文件安装期间使用录制模式，安装程序会将原始响应文件中指定的变量值记录到新的响应文件中。

> 注意：Oracle Universal 安装程序不录制响应文件的密码。

录制响应文件：

1. 像正常安装一样完成安装任务。
2. 确保 Oracle Grid Infrastructure 软件所有者用户（通常为 `grid`）具有权限在运行安装程序时指定的 Grid home 路径上创建或写入。
3. 在每个安装界面上指定所需信息。
4. 当安装程序显示摘要界面时，执行以下步骤：
   a. 点击“保存响应文件”，指定保存响应文件的文件名和位置，然后点击“保存”。
   b. 点击“完成”创建响应文件并继续安装。如果您只想创建响应文件，请点击“保存”。安装将停止，但您输入的设置将记录在响应文件中。
5. 在另一个系统上使用保存的响应文件之前，编辑文件并进行任何更改。

### B.3 使用响应文件运行安装程序

在命令行运行 Oracle Universal 安装程序并指定您创建的响应文件。Oracle Universal 安装程序执行文件 `runInstaller` 提供了多个选项。有关完整选项集的帮助信息，请运行带有 `-help` 的 `runInstaller` 命令。例如：

```
$ directory_path/runInstaller -help
```

帮助信息将出现在窗口中。
使用响应文件运行安装程序：

1. 像正常安装一样完成预安装任务。
2. 以软件安装所有者的身份登录。
3. 如果您正在完成响应文件安装，请设置 `DISPLAY` 环境变量。

> 注意：如果您正在完成静默安装，则不需要设置 `DISPLAY` 环境变量。

4. 以静默或响应文件模式启动安装程序，输入类似下面的命令：

```
$ /directory_path/runInstaller [-silent] [-noconfig] -responsefile filename
```

> 注意：不要指定响应文件的相对路径。如果指定了相对路径，安装程序将失败。

在此示例中：

- `directory_path` 是 DVD 的路径或您已复制安装二进制文件的硬盘上的目录路径。
- `-silent` 以静默模式运行安装程序。
- `-noconfig` 在安装期间静默配置助手，转而执行仅软件安装。
- `responsefilefilename` 是您配置的安装文件的完整路径和名称。

5. 安装完成后，以 `root` 用户身份登录并运行 `root.sh` 脚本。例如

```
$ root
password:
# /oracle_home_path/root.sh
```

### B.4 使用响应文件运行网络配置助手

您可以使用静默模式运行网络配置助手，在系统上配置并启动 Oracle Net 监听器，配置命名方法并配置 Oracle

网络服务。要以静默模式运行 Net 网络配置助手，您必须复制并编辑响应文件模板。Oracle 在 DVD 上的 `database/response` 目录下提供了一个名为 `netca.rsp` 的响应文件。

> 注意：如果您已将软件复制到硬盘，则响应文件模板位于 `database/response` 目录。

使用响应文件运行网络配置助手：

- 1. 从响应文件将 `netca.rsp` 响应文件模板复制到系统上的某个目录：
```



$ cp `/directory_path/response/netca.rsp` `local_directory`

在此示例中，`directory_path` 是 DVD 中数据库目录的路径。如果您已将软件复制到硬盘，您可以在您偏好的响应文件位置编辑该文件。

- 2. 使用文本编辑器打开响应文件：

```
$ /local_dir/netca.rsp
```

- 3. 按照文件中的说明进行编辑。

> 注意：如果您没有正确配置响应文件，网络配置助手将失败。

- 4. 以 Oracle 软件所有者的身份登录，并设置 `ORACLE_HOME` 环境变量以指定正确的 Oracle 目录。静默模式：

- 5. 输入类似下面的命令以静默模式运行网络配置助手：

```
$ ORACLE_HOME/bin/netca -silent -responsefile /local_dir/netca.rsp
```

在此命令中：

- `-silent` 选项表示网络配置助手在静默模式下运行。
- `local_dir` 是您复制 `netca.rsp` 响应模板的目录的完整路径。

### B.5 使用响应文件进行安装后配置

使用以下章节在安装 Oracle 软件后创建并运行响应文件。

#### B.5.1 关于安装后配置文件

当您运行静默安装或响应文件安装时，您会在响应文件中提供有关服务器的信息，而这些信息通常是在图形用户界面中手动提供的。然而，响应文件不包含配置助手在软件安装完成后所需的用户账户密码。配置助手是通过名为 `configGetAllCommands` 的脚本启动的。您可以使用响应文件在响应模式下运行此脚本。该脚本使用密码连续运行配置工具以完成配置。

如果您保留了用于克隆安装的密码文件，Oracle 建议将其存储在安全位置。此外，如果您想停止安装以修复错误，可以使用 `configToolAllCommands` 和密码响应文件运行配置助手。

`configToolAllCommands` 响应文件包含以下语法选项：

- `internal_component_name` 是配置助手配置的组件名称
- `variable_name` 是配置文件变量的名称
- `value` 是配置时所需的预期值。

命令语法如下：
`internal_component_name|variable_name=value`

例如：
`oracle.assistants.asm|S_ASMPASSWORD=welcome`

Oracle 强烈建议通过密码响应文件维护安全性：

- 响应文件的权限应设置为 `600`。
- 响应文件的所有者应为安装所有者用户，组设置为中心清单（`oralInventory`）组。

#### B.5.2 使用响应文件运行安装后配置

使用 `configToolAllCommands` 脚本运行配置助手：

- 1. 使用 `filename.properties` 语法创建响应文件。例如：
  `$ touch cfgprop.properties`
- 2. 使用文本编辑器打开文件，并编辑密码模板，根据需要进行修改。

> 示例 B–1 用于群集 Oracle Grid Infrastructure 安装的密码响应文件

Oracle Grid Infrastructure 需要 Oracle 自动存储管理配置助手 (`ASMCA`) 的密码，如果您有 BMC 卡并想启用此功能，还需要智能管理接口配置助手 (`IPICA`) 的密码。提供以下响应文件：

```
oracle.assistants.asm|S_ASMPASSWORD=password

oracle.assistants.asm|S_ASMMITORPASSWORD=password

oracle.crs|S_BMCPASSWORD=password
```

如果您没有 BMC 卡或不想启用 IPMI，请留空 `S_BMCPASSWORD` 字段。

示例 B–2 用于 Oracle Real Application Clusters 的密码响应文件

数据库配置需要 `SYS`、`SYSTEM`、`SYSMAN` 和 `DBSNMP` 密码用于数据库配置助手 (`DBCA`)。此外，如果使用 Oracle 存储，则配置 `ASMNMP` 密码。如果如果选择了 Oracle Enterprise Manager，则为 Oracle 软件所有者提供 `S_HOSTUSERPASSWORD` 响应。

```
oracle.assistants.server|S_ASMPPASSWORD=password

oracle.assistants.server|S_SYSTEMPASSWORD=password

oracle.assistants.server|S_SYSMANPASSWORD=password

oracle.assistants.server|S_DBSNMPPASSWORD=password

oracle.assistants.server|S_HOSTUSERPASSWORD=password

oracle.assistants.server|S_ASMNOPPASSWORD=password
```

如果您不想启用 Oracle Enterprise Manager 或 Oracle ASM，请留空这些字段。

- 3. 修改文件权限。例如：

```
$ ls -al cfgprop.properties

-rw------- 1 oracle 0
```

- 4. 切换到 `$ORACLE_HOME/cfgtool`，并使用以下语法运行配置脚本：`RESPONSE_FILE=/path/name.properties`，例如：

```
$ ./configToolAllCommands
```

## C 配置大内存优化

本附录提供了在 Linux 系统上使用 Hugepages 配置大内存优化的信息。它包含以下主题：

- HugePages 概述
- HugePage 配置限制
- 禁用透明 HugePages

### C.1 HugePages 概述

您可以选择配置 HugePages。对于某些用途，HugePages 可以提供增强性能。然而，这是一个高级配置选项，并不是 Oracle RAC 的要求。以下是 HugePages 的概述。您必须执行的配置任务取决于内核发行和硬件。如果您决定配置集群节点使用 HugePages，请参考您的发行文档以及 Oracle 技术网络 (`OTN`) 和 Oracle Support 获取更多信息。

#### HugePages 提供什么

HugePages 是集成到 2.6 版本 Linux 内核中的功能，是一种处理大内存的大页方法。它适用于 32 位和 64 位配置。HugePage 的大小从 2MB 到 256MB 不等，取决于内核版本和架构。数据库减少了操作系统对页状态的维护并增强了 TLB（转换缓冲区）命中。如果没有 HugePages，操作系统将每个 4 KB 的内存作为一个页，当分配给 SGA 时，操作系统必须更新该页的生命周期（脏、空闲、映射到进程等）。使用 HugePages 后，页表（虚拟内存映射）更小，因为每个页表项指向 2MB 到 256MB 的页。此外，内核需要监控的页更少。例如，如果您在 64 位硬件上使用 HugePages 并映射 256 MB 内存，您可能需要一个页表项 (`PTE`)。如果不使用 HugePages 且要映射 256 MB，则需要 256 MB * 1024 KB / 4 KB = 65536 个 PTE。

### C2 HugePage 配置限制

要使用 HugePages，必须配置 Grub 在启动期间为 HugePages 分配内存。预留空间后，可以根据需要使用 HugePages。然而，如果系统启动时未预留空间，则 HugePages 分配可能会失败。

除非系统管理员通过修改可用页数或池大小来更改 hugepages 配置，否则 HugePages 在系统启动后不会分配或释放。

### C3 禁用透明 HugePages

Red Hat Enterprise Linux 6、SUSE Enterprise Server 11 以及早期版本的 Oracle Linux 6 UEK 内核默认禁用透明 HugePages 内存。在较版本的 Oracle Linux UEK 内核中禁用了透明 HugePages。

透明 HugePages 会导致运行时内存分配延迟。为了避免性能问题，Oracle 建议在所有 Oracle 数据库服务器上禁用透明 HugePages。Oracle 建议使用标准的 HugePages 来增强性能。透明 HugePages 内存与标准 HugePages 的区别在于内核在运行时动态分配内存。标准 HugePages 在启动时预分配，且在运行时不会改变。

> **另参：**《Linux 和 UNIX 系统的 Oracle 数据库管理员参考》中的 HugePages 信息

以 `root` 用户身份运行以下命令之一检查是否启用了透明 HugePages 内存：

Red Hat Enterprise Linux 内核：



```
# cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
```

其他内核：

```
# cat /sys/kernel/mm/transparent_hugepage/enabled
```

以下是显示启用 `[always]` 标志时使用透明 HugePages 内存的示例输出。

```
[always] never
```

> 注意：如果内核中移除了透明 HugePages，则 `/sys/kernel/mm/transparent_hugepage` 或 `/sys/kernel/mm/redhat_transparent_hugepage` 文件不存在。

要禁用透明 HugePages，请执行以下步骤：

- 1. 在 `/etc/grub.conf` 文件的内核启动命令行添加以下条目：`transparent_hugepage=never`

例如：

```
title Oracle Linux Server (2.6.32-300.25.1.el6uek.x86_64)
root (hdb0,0)
kernel /vmlinux-2.6.32-300.25.1.el6uek.x86_64 ro=LABEL=/
transparent_hugepage=never
initrd/initramfs-2.6.32-300.25.1.el6uek.x86_64.img
```

- 2. 重启系统以更改永久生效。

# 集群安装 Oracle Grid Infrastructure 概念

本附录解释了要求执行的预安装任务的原因以及其他安装概念。

本附录包含以下章节：

- 理解预安装配置
- 理解存储配置
- 理解服务器池
- 理解离地升级

## D.1 理解预安装配置

本节回顾了关于集群 Oracle Grid Infrastructure 预安装任务的相关概念。它包含以下子节：

- 理解 Oracle 组和用户
- 理解 Oracle Base 目录路径
- 理解网络地址
- 理解网络时间要求

### D.1.1 理解 Oracle 组和用户

本节包含以下主题：

- 理解 Oracle Inventory 组
- 理解 Oracle Inventory 目录

#### D.1.1.1 理解 Oracle Inventory 组

你必须拥有一个组，其成员被授予访问 Oracle Inventory (`oraInventory`) 目录的权限，该目录是服务器上所有 Oracle 软件安装的中央清单目录。该组成员具有 Oracle 中央清单 (`oraInventory`) 目录的写入权限，并被授予 Oracle Cluster 资源、OCR 密钥、Oracle Cluster home 中允许 DW 访问的目录或其他权限。默认情况下，此组名为 `oinstall`。Oracle Inventory 组必须是 Oracle 软件安装的主主组。

`oraInventory` 目录包含以下内容：

- 系统上 Oracle home 目录（Oracle Grid Infrastructure 和 Oracle Database）的注册表
- Oracle 软件安装的安装日志和跟踪文件。这些文件也会复制到相应的 Oracle home 中以供以后参考。
- 关于 Oracle 安装的其他元数据信息存储在各个 Oracle home 清单目录中，与中央清单分开。

你可以配置一个组作为 Oracle Inventory 的访问控制组、数据库管理员 (OSDBA) 以及所有 Oracle 软件用于操作系统身份验证的其他控制组。然而，如果你使用一个组为所有系统权限提供操作系统身份验证，则该组必须是你希望授予管理系统权限的所有用户的主主组。

> 注意：如果软件已安装在系统上，则现有的 Oracle Inventory 组必须是你用于安装 Oracle Grid Infrastructure 的操作系统 (`oracle` 或 `grid`) 的主主组。参考“确定 Oracle Inventory 是否以及 Oracle Inventory 是否存在”来识别 Oracle Inventory 组。

#### D.1.1.2 理解 Oracle Inventory 目录

Oracle 目录 (`oraInventory`) 是服务器上所有安装 Oracle 软件的中央清单位置。

当你首次在系统上安装 Oracle 软件时，系统会提示你提供 `orainventory` 目录路径。

当你为执行 Oracle Grid Infrastructure 安装的用户提供非环境变量 `ORACLE_BASE` 的 Oracle base 路径时，OUI 会 `ORACLE_BASE../oraInventory` 路径下创建 Oracle inventory。例如，如果 `ORACLE_BASE` 设置为 `/opt/oracle/11`，则 Oracle inventory 在路径 `/opt/oracle/oraInventory` 创建，这样所有安装的中央清单都在该特定 Oracle 安装用户的 Oracle base 之外。

如果你输入的路径未设置 `ORACLE_BASE`，则 Oracle Inventory 目录将放置在执行安装的用户的家目录下。例如：

```
/home/oracle/oraInventory
```

由于这可能导致后续多个 Oracle 软件所有者进行安装时出现权限错误，Oracle 建议不要接受此选项，并使用符合 OFA 标准的路径。

对于新安装，Oracle 建议创建一个符合 OFA 结构的 Oracle 路径（例如 `/u01/app/oraInventory`），该路径由 Oracle 软件所有者拥有，或者将 Oracle base 变量设置为符合 OFA 标准的路径。

如果你将 Oracle base 变量设置为如 `/u01/app/grid` 或 `/u01/app/oraInventory` 等路径，则 Oracle Inventory 将默认设置到该路径，并具有正确的权限，允许所有 Oracle 安装所有者写入此中央清单目录。

## D-2 Oracle Grid Infrastructure 安装指南

默认情况下，Oracle Inventory 目录不会安装在安装所有者的 Oracle base 目录下。这是因为 Oracle 软件安装共享一个公共的 Oracle Inventory，因此所有用户只有一个 Oracle Inventory，而每个用户都有独立的 Oracle base。

### D.1.2 理解 Oracle Base 目录路径

本节包含关于准备 Oracle base 目录的信息。

#### D.1.2.1 Oracle base 目录概述

在安装期间，系统会提示指定一个 Oracle base 位置，该位置由安装用户拥有。你可以选择一个具有现有 Oracle home 的位置，或者选择另一个不具备 Oracle base 目录结构的目录位置。

使用 Oracle base 目录路径有助于组织 Oracle 安装，并确保多个数据库的安装维持最优的可灵活架构 (OFA) 配置。

#### D.1.2.2 理解 Oracle Base 和 Grid Infrastructure 目录

即使你没有使用相同的软件安装 Grid Infrastructure (Oracle Clusterware 和 ASM) 或 Oracle Database，也请注意，Grid Infrastructure 安装期间的 `root.sh` 脚本会将放置集群二进制文件的 home 目录的所有权更改为 `root`，并将所有祖目录也更改为 `root`。由于此原因，Grid Infrastructure for cluster 无法与 Oracle software 位于一起。

> 参见 Oracle Database 安装指南获取更多关于 Oracle Restart 信息

## D1.3 理解网络地址

在安装期间，系统要求你指定每个网络接口的计划用途，将每个接口识别为公共或私有接口，或者你希望 Clusterware 使用的接口。公共和虚拟 IP 地址配置在公共接口上。参考以下详细信息获取有关每种类型的类型：

- 关于公共 IP 地址
- 关于私有 IP 地址
- 关于虚拟 IP 地址
- 关于网格命名服务 (GNS) IP 地址
- 关于 SCAN

### D1.3.1 关于公共 IP 地址

公共 IP 地址通过 DHCP 动态分配，或在主机文件中静态定义。它使用公共接口（客户端可用接口）。

### D1.3.2 关于私有 IP 地址

私有地址配置在私有接口上。Oracle Cluster 使用标记为私有的接口。每个节点都需要配置地址，但不需要额外配置。由于 Cache Fusion 和节点间的流量，Oracle 强烈建议使用物理隔离的私有网络。该网络仅供集群节点访问。你不应在具有私有地址的网络设置防火墙，因为可能会拦截流量。

### D1.3.3 关于虚拟 IP 地址

虚拟 IP (`VIP`) 地址注册在 GNS 或 DNS 中。为你的 VIP 选择符合以下要求的地址：



- 该 IP 地址和主机名当前未使用（可以通过 `ping` 命令访问）
- VIP 与你的公共接口位于同一子网

### D1.3.4 关于网格命名服务 (GNS) IP 地址

GNS 虚拟 IP 地址是配置在 DNS 中的静态 IP 地址。DNS 将查询委托给 GNS 虚拟 IP 地址，GNS 守护在该地址响应传入的解析请求。

在子网内，GNS 使用多播域命名服务 (`mDNS`) 配合 Oracle Cluster 来动态添加和删除主机名及地址，而无需在 DNS 中进行额外配置。要启用 GNS，你需要让网络管理员为分配给集群的子域一组 IP 地址（例如 `grid.example.com`），并将域的 DNS 请求委托给集群的 GNS 虚拟 IP 地址。地址集通过 DHCP 提供给集群，公共网络必须可用。

> 参见 Oracle Cluster 管理和部署指南获取更多关于网格命名服务的信息

### D1.3.5 关于 SCAN

Oracle Database 11g release 2 使用 SCAN 连接到数据库。SCAN 及其关联 IP 地址为客户端连接提供了稳定的名称，独立于组成集群的节点。SCAN 地址、虚拟 IP 地址必须全部位于同一子网中。

SCAN 是一个虚拟 IP 名称，类似于用于虚拟 IP 地址的名称（例如 `node-vip`）。然而，与虚拟 IP 不同，SCAN 与整个集群关联，而不是单个节点关联，并且与多个 IP 地址关联，而不仅仅是一个。

SCAN 的工作原理是能够解析到处理公共客户端连接的集群中的 IP 地址。当客户端请求时，监听在 SCAN IP 地址和 SCAN 端口的 SCAN 监听器将提供服务。由于集群上的所有服务都已注册到 SCAN 监听器上，SCAN 会返回当前提供该服务的负载最低节点上的本地监听器地址。最后，客户端通过提供服务的节点建立与服务的连接。所有这些操作对客户端来说都是透明的，无需在集群中进行任何显式配置。

在安装期间会创建监听器。它们监听在节点上提供的用于 SCAN 地址的 SCAN IP 上。Oracle Net Services 将请求路由到提供服务的最少实例。由于 SCAN 解析到集群地址而不是集群中的节点地址，因此可以向集群中添加或删除节点而不会影响 SCAN 配置。

应配置 SCAN，使其能够通过集群内的网格名称服务 (`GNS`) 或域名服务 (`DNS`) 进行解析。为了高可用性和可扩展性，Oracle 建议您配置 SCAN 解析到三个 IP 地址。至少，SCAN 必须解析到至少一个地址。

如果您指定了 DNS 名称，则 SCAN 默认为 `clustername-scan.GNS_domain`。否则，它默认为 `clustername-scan.current_domain`。例如，如果您从服务器节点启动 Grid Infrastructure 安装，集群名称为 `mycluster`，DNS 为 `grid.example.com`，那么 SCAN 即为 `mycluster-scan.grid.example.com`。

对于 Oracle Database 11g release 2 之前的版本，配置使用 IP 地址的 Oracle 客户端可以继续使用现有的连接：不需要 SCAN。当您升级到 Oracle Cluster 11g release 2 (11.2) 时，SCAN 将变得可用。您应该使用 SCAN 连接到 Oracle Database 11g 2 或更高版本的数据库。当较早版本的 Oracle Database 升级时，它会注册到 SCAN 监听器，客户端可以开始使用 SCAN 连接到数据库。数据库通过 `initora` 文件中的 `remote_listener` 参数向 SCAN 监听器注册。`REMOTE_LISTENER` 参数必须设置为 `SCAN:PORT`。不要对 SCAN 使用带有单个地址的 `HOST+SCAN` 的 TNSNAMES 别名。

SCAN 适用于大多数部署。然而，使用 Oracle Database 11g release 2 以及使用服务器池的策略管理数据库应该使用 SCAN 访问数据库。这是因为策略管理数据库可以在不同时间运行不同的服务器上，因此为策略管理数据库连接到特定的虚拟 IP 地址是不可能的。

## D.1.4 理解网络时间需求

Oracle Cluster 11g release 2 (11.2) 自动配置了集群时间同步服务 (`CTSS`)。该服务使用针对此类集群部署的最优同步策略对所有集群节点进行自动同步。

## 理解存储配置

如果您有现有的集群同步服务（例如 NTP），它将在观察模式下启动。否则，它将在活动模式下启动，以确保集群节点之间的时间同步。CTSS 不会引起兼容性问题。

CTSS 模块作为 Oracle Grid Infrastructure 安装的一部分进行。CTSS 守护进程由 OHAS 守护进程 (`ohasd`) 启动，不需要命令行界面。

### D.2 理解存储配置

- 了解 Oracle 自动存储管理集群文件系统
- 关于缓解现有 ASM 实例的影响
- 关于将独立 Oracle ASM 安装转换为集群安装

### D.2.1 了解 Oracle 自动存储管理集群文件系统

Oracle 自动存储管理已扩展，包含一个通用型文件系统，称为 Oracle 自动存储管理集群文件系统 (`ACFS`)。ACFS 是一种全新的多平台、可扩展的文件系统和存储管理技术，扩展了 Oracle 自动存储管理 (`ASM`) 功能，以支持维护在 Oracle 数据库之外的客户文件。ACFS 支持的文件包括应用程序二进制文件和应用程序报告。其他支持的文件包括视频、音频、文本、图像、图画和其他通用文件数据。

### D.2.2 关于缓解现有 ASM 实例的影响

如果您在集群上安装了来自先版本的 ASM 安装，可以使用 Oracle 存储管理配置助手 (`ASMCA`) 将实例升级到 11g release 2 (11.2)。如果版本是 Oracle ASM release 1，则无法执行滚动升级。

### D.2.3 关于将独立 Oracle ASM 安装转换为集群安装

如果您在作为集群成员节点的一个或多个节点上有现有的独立 ASM 安装，OUI 将继续安装用于集群的 Oracle Grid Infrastructure。

## D.3 理解服务器池

本节提供了服务器池的要概述。它包含以下主题：

- 服务器池和基于策略管理的概述
- 服务器池如何工作
- 免费服务器池
- 通用服务器池

### D.3.1 服务器池和基于策略管理的概述

使用 Clusterware 11g release 2 (11.2) 及更高版本，由 Oracle Cluster 管理的资源包含在称为服务器池的逻辑资源组中。资源托管在共享基础设施上并包含在服务器池中。根据策略对硬件资源（如 CPU 和内存）的消耗进行限制，其行为就像部署在单系统环境中一样。

注意：为了限制此权限，Oracle 强烈建议您将特定用户添加到 CRS 管理员列表中。

# 理解服务器池

Oracle Grid Infrastructure 安装所有有权限使用 `SRVCTL`、`Oracle Enterprise Manager Database Control` 或 Oracle Database Configuration Assistant (`DBCA`) 创建和配置服务器池。

基于策略的管理：

- 允许在需要时启用动态容量分配，以根据您在策略中使用的优先级提供服务器容量。
- 允许按重要性分配资源，以便应用程序在任何可能的情况下获得最低需求，并确保低优先级的应用程序不会占用更重要应用程序的资源。
- 在必要时确保隔离性，以便您为集群中的应用程序和数据库提供专用服务器。

运行在服务器池中的应用程序和数据库不共享资源。正因如此，服务器池在必要时隔离资源，但会根据需要启用动态容量分配。与角色分离的管理相结合，此功能满足了具有标准化集群环境但允许多个管理员组共享公共集群基础设施组织的需求。

### D.3.2 服务器池如何工作

服务器池将集群划分为若干组托管相同或相似资源的服务器。它们将均匀的负载（一组 Oracle Cluster 集群资源）分发到集群中的几台服务器上。例如，您可以限制 Oracle 数据库仅运行在特定的服务器池中。当您启用角色分离的管理时，可以显式授予操作系统用户更改服务器池属性的权限。

顶层服务器池：

- 逻辑上划分集群
- 始终是排他的，这意味着在特定时间点，一台服务器只能存在于一个特定的服务器池中

服务器池在分配时会被分配以下三个属性：

- `MIN_SIZE`：服务器池应包含的服务器最小数量。如果服务器池中的服务器数量低于此属性的值，则 Oracle Cluster 将自动从其他地方将服务器移动到该服务器池中，直到服务器数量达到该属性值，或者从不那么重要的的池中有空闲服务器为止。
- `MAX_SIZE`：服务器池可能包含的最大服务器数量。
- `IMPORTANCE`：一个从 0 到 1000 的数字（0 为最低），用于对服务器池在集群中所有其他服务器池进行排名。



当安装 Oracle Cluster 时，会自动创建两个服务器池：`Generic`（通用）和 `Free`（空）。在新的安装中，所有服务器最初都被分配到 `Free` 服务器池。服务器会自动从 `Free` 移动到新定义的服务器池中。当您升级 Oracle Cluster 时，所有节点都被分配到 `Generic` 服务器池，以确保与 Oracle Database 11g Release 2 (11.2) 之前的数据库版本的兼容性。

## D.3.3 Free 服务器池

`Free` 服务器池包含未分配到任何其他服务器池的服务器。`Free` 服务器池的属性限制如下：

- `SERVER_NAMES`、`MIN_SIZE`、`MAX_SIZE` 不能由用户编辑
- `IMPORTANCE` 和 `ACL` 可以由用户编辑

**另参：** Oracle Clusterera Administration and Deployment Guide

## D.3.4 Generic 服务器池

`Generic` 服务器池存储 11g Release 2 (11.2) 之前的数据库以及具有固定配置的管理员管理的数据库。此外，`Generic` 服务器池包含符合以下任一条件的服务器：

- 您在应用程序资源类型所有资源的 `HOSTING_MEMBERS` 属性中指定的服务器
- 在列出 `Generic` 服务器池为服务器池的服务器池的 `SERVER_NAMES` 属性中指定的名称的服务器
- `Generic` 服务器池的属性限制如下：
- 任何人无法修改 `Generic` 服务器池的属性（所有属性均为只读）
- 当您在 `HOSTING_MEMBERS` 属性中指定服务器名称时，Oracle Clusterware 仅在服务器满足以下条件时允许：
    - 在线且存在于 `Generic` 服务器池中
    - 在线且存在于 `Free` 服务器池中，在这种情况下 Oracle Clusterware 将服务器移动到 `Generic` 服务器池
    - 在线且存在于任何其他服务器池中，且客户端是 `CRS` 管理员（控制服务器池资源管理的用户角色）或被允许使用该服务器池的服务器，在这种情况下服务器将被移动到 `Generic` 服务器池
    - 离线且客户端是 `CRS` 管理员
- 当您向 `Generic` 服务器池注册服务器池时，Oracle Clusterware 仅当服务器名称通过之前为资源指定的相同要求时才允许。

服务器在集群启动时或向集群添加服务器时最初被考虑分配到 `Generic` 服务器池，在此之后才分配到其他服务器池。

## D.4 理解离地升级

在离地升级中，安装程序在单独的 Oracle Cluster home 中安装新版本。Oracle Clusterware 的两个版本都位于每个集群成员节点上，但只有一个版本是激活的。

滚动升级在软件升级到新版本时避免了停机并确保连续可用性。

如果您在每个节点上都有 Oracle Cluster homes，则你可以在所有节点上执行离地升级，或者执行部分滚动升级，使得某些节点运行来自早期版本 Oracle Cluster home 的 Oracle Clusterware，而其他节点运行来自新 Oracle Cluster home 的 Oracle Clusterware。

不支持 Oracle Clusterware 11g release 2 的就地升级。

另参：附录 F，“如何升级到 Oracle Grid Infrastructure”，有关完成滚动升级的说明

## E 手动完成安装前提任务

本附录提供了手动完成集群验证工具 (`CVU`) 和安装程序 (`OUI`) 通常在安装期间完成的配置任务的说明。如果您无法使用修复脚本，请参考此附录。

本附录包含：

- 在节点上配置 SSH
- 配置内核
- 在节点上启用 SSH

### E.1 手动配置 SSH

强制要求无密码 SSH。在后续示例中，使用了 `grid` 用户。您必须为打算使用的每个 Oracle 软件所有者单独配置 SSH。

#### E.1.1 检查系统的现有 SSH 配置

要确定 `ssh` 是否正在运行，请输入命令：

```
$ pgrep
```

#### E.1.2 在节点上配置 SSH

要配置 SSH，首先需要在每个节点上创建 RSA 或 DSA 密钥，然后将所有节点生成的密钥复制到每个节点上都相同的文件中。SSH 文件必须允许 `root` 和软件用户读取。

##### E.1.2.1 在每个节点创建 SSH 目录并创建

在每个节点上完成以下步骤：

1. 以软件所有者身份登录（在本示例中为 `grid` 用户）。
2. 为了确保您是以 `grid` 用户身份登录，并验证用户 ID 与分配给 `grid` 用户的预期 ID 匹配，请输入 `id` 和 `grid` user。例如：

```
$ id
uid=502(grid) gid=501(install) groups=501(install), 502(grid, asmdmin, asmdba)
gid=grid
uid=502(grid) gid=501(install) groups=501(install), 502(grid, asmdmin, asmdba)
```

3. 如必要，在 `grid` 用户的目录下创建 `.ssh` 目录，并对其设置权限以确保只有 `oracle` 用户具有读写权限：

```
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
```

> 注意：如果权限未设置为 700，SSH 配置将失败。

4. 输入以下命令：

```
$ /usr/bin/ssh-keygen -t dsa
```

# 在所有集群节点上手动配置 SSH

在出现提示时，接受密钥文件的默认位置（按 **Enter**）。

> **注意：** Oracle Clusterware 11g release 2 及更高版本不支持带有密码短码的 SSH。

此命令将 DSA 公钥写入 `~/.ssh/id_dsa.pub` 文件，将私钥写入 `~/.ssh/id_dsa` 文件。

切勿将 DSA 密钥分发给任何未授权执行安装 Oracle 软件的人员。

- 5. 对您打算成为集群成员的每个节点，使用 DSA 密钥重复步骤 1 到 4。

## E.1.2.2 将所有密钥添加到公用的 authorized_keys 文件

完成以下步骤：

- 1. 在本地节点上，切换目录到 Oracle Infrastructure 所有者家目录下的 `.ssh` 目录（通常，是 `grid` 或 `oracle`）。

然后，使用以下命令将 DSA 密钥添加到 `authorized_keys` 文件：

```bash
$ id_dsa.pub >> authorized_keys
$ ls
```

在目录中，您应该看到您创建的 `id_dsa.pub` 文件和 `authorized_keys` 文件。

2. 在本地节点上，使用 `SCP`（安全复制）或 `SFTP`（FTP）将 `authorized_keys` 文件复制到远程节点上的 `oracle` 用户 `.ssh` 目录。以下示例使用 `SCP`，针对名为 `node2` 的节点，使用 Oracle Infrastructure 所有者 `grid`，其中 `grid` 用户路径为 `/home/grid`：

```bash
[grid@node2] $ scp authorized_keys /home/grid/.
```

系统会提示接受一个 DSA 密钥。输入 `Yes`，您将看到您正在复制到 `known_hosts` 文件的节点。

在出现提示时，提供 `grid` 用户的密码，该密码在集群的所有节点上应是相同的。`authorized_keys` 文件被复制到远程节点。

您的输出应该如下所示，其中 `xxx` 代表有效 IP 地址的部分：

```bash
[grid@.ssh] $ scp authorized_keys node2:/home/grid/.
The authenticity of host 'node2' (xxx.173.152) can't be established.
DSA key fingerprint is 7e:60:60:a4:40:d4:ae:f6:74:ae:78:fe:7e
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'node2,xxx.173.152' to the list of known hosts
grid@node2's password:
authorized_keys   100   828   7.5KB/s   00
```

3. 使用 `SSH` 登录到您复制 `authorized_keys` 文件的节点。然后切换到 `.ssh` 目录，并将第二个节点的 DSA 密钥添加到 `authorized_keys` 文件中，在提示输入密码时点击 **Enter**，以便设置免密 SSH：

如何完成安装先决任务 手册 E-3



```bash
[grid#node1] $ ssh node2
[grid#node2] $cd .ssh
[grid#node2] $ssh cat id_dsa.pub >> authorized_keys
```

从每个节点到每个其他节点成员重复步骤 2 和 3。当您已将每个集群节点成员的密钥都添加到最后一个希望作为集群节点成员的节点的 `authorized_keys` 文件中时，请使用 `scp` 将 `authorized_keys` 文件从该节点复制回到所有集群节点，覆盖其他节点上的现有版本。

要确认 `authorized_keys` 文件中包含所有节点，输入命令 `more authorized_keys`，并确定每个节点成员是否有 DSA 密钥。遵循列表密钥类型 (`ssh-dsa`)，后面跟上密钥，然后是用户和服务器。例如：

```
ssh-dsa AAAAAAAAAA ... * grid@node1
```

> 注意：每个节点的 `grid` 用户 `~/.ssh/authorized_keys` 文件必须包含所有集群节点生成的 `~/.ssh/id_dsa.pub` 文件的内容。

## E.1.3 启用节点间的 SSH 等效

在将包含所有密钥的 `authorized_keys` 文件复制到集群每个节点后，按照下列顺序完成操作。在本示例中，Oracle Grid Infrastructure 软件名为 `grid`：

- 1. 在要运行的系统中以 `grid` 用户登录。

2. 使用以下命令语法 `hostname1`、`hostname2` 等集群节点的公主机名（别名和完全域名）从本地节点到每个节点，包括从本地节点到自身，以及从每个节点到每个其他节点：

```bash
[grid@nodename]$ $ ssh hostname
[grid@nodename]$ $ ssh hostname
```

例如：

```bash
[grid@grid]$ $ ssh node
The authenticity of host 'node' (xxx.xxx.101)' can't be established.
DSA key fingerprint is 7e:60:zz:zc:48:z1:a0:f7:4e.
Are you want to continue connecting (yes/no)? yes
Warning: Permanently added 'node,xxx.xxx.101' (DSA) to the list of known hosts.
Mon Dec 4 11:08:13 PST 2006
[grid@grid]$ $ ssh node.example.com
The authenticity of host 'node.example.com' (xxx.xxx.101)' can't be established.
DSA key fingerprint is 7e:60:zz:zc:48:z1:a0:f7:4e.
Are you want to continue connecting (yes/no)? yes
Warning: Permanently added 'node.example.com,xxx.xxx.101' (DSA) to the list of known hosts.
Mon Dec 4 11:08:13 PST 2006
[grid@grid]$ $ ssh node2
Mon Dec 4 11:08:35 PST 2006
```

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

（注：原文此处存在重复段落，翻译了多次关于 `known_hosts` 的描述）

- 3. 在每个节点重复步骤 2。

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

- 4. 在每个节点重复步骤 3。

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

（此处重复了原文的描述逻辑）

## 在所有集群节点上手动配置 SSH

在出现提示时，接受密钥文件的默认位置（按 `Enter`）。

> **注意：** Oracle Clusterware 11g release 2 及更高版本不支持带有密码短码的 SSH。

此命令将 DSA 公钥写入 `~/.ssh/id_dsa.pub` 文件，将私钥写入 `~/.ssh/id_dsa` 文件。

切勿将 DSA 密钥分发给任何未授权执行 Oracle 软件的人员。

- 5. 对您打算成为集群成员的每个节点，使用 DSA 密钥重复步骤 1 到 4。

## E.1.2.2 将所有密钥添加到公用的 authorized_keys 文件

完成以下步骤：

- 1. 在本地节点上，切换目录到 Oracle Infrastructure 所有者家目录下的 `.ssh` 目录（通常，是 `grid` 或 `oracle`）。

然后，使用以下命令将 DSA 密钥添加到 `authorized_keys` 文件：

```bash
$ id_dsa.pub >> authorized_keys
$ ls
```

在目录中，您应该看到您创建的 `id_dsa.pub` 文件和 `authorized_keys` 文件。

2. 在本地节点上，使用 `SCP`（安全复制）或 `SFTP`（FTP）将 `authorized_keys` 文件复制到远程节点上的 `oracle` 用户 `.ssh` 目录。以下示例使用 `SCP`，针对名为 `node2` 的节点，使用 Oracle Infrastructure 所有者 `grid`，其中 `grid` 用户路径为 `/home/grid`：

```bash
[grid@node2] $ scp authorized_keys /home/grid/.
```

系统会提示接受一个 DSA 密钥。输入 `Yes`，您将看到您正在复制到 `known_hosts` 文件的节点。

在出现提示时，提供 `grid` 用户的密码，该密码在集群的所有节点上应是相同的。`authorized_keys` 文件被复制到远程节点。

您的输出应该如下所示，其中 `xxx` 代表有效 IP 地址的部分：

```bash
[grid@.ssh] $ scp authorized_keys node2:/home/grid/.
The authenticity of host 'node2' (xxx.173.152) can't be established.
DSA key fingerprint is 7e:60:60:a4:40:d4:ae:f6:74:ae:78:fe:7e
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'node2,xxx.173.152' to the list of known hosts
grid@node2's password:
authorized_keys   100   828   7.5KB/s   00
```

3. 使用 `SSH` 登录到您复制 `authorized_keys` 文件的节点。然后切换到 `.ssh` 目录，并将第二个节点的 DSA 密钥添加到 `authorized_keys` 文件中，在提示输入密码时点击 `Enter`，以便设置免密 SSH：

```bash
[grid#node1] $ ssh node2
[grid#node2] $cd .ssh
[grid#node2] $ssh cat id_dsa.pub >> authorized_keys
```

从每个节点到每个其他节点成员重复步骤 2 和 3。当您已将每个集群节点成员的密钥都添加到最后一个希望作为集群节点成员的节点的 `authorized_keys` 文件中时，请使用 `scp` 将 `authorized_keys` 文件从该节点复制回到所有集群节点，覆盖其他节点上的现有版本。

要确认 `authorized_keys` 文件中包含所有节点，输入命令 `more authorized_keys`，并确定每个节点成员是否有 DSA 密钥。遵循列表密钥类型 (`ssh-dsa`)，后面跟上密钥，然后是用户和服务器。例如：

```
ssh-dsa AAAAAAAAAA ... * grid@node1
```

> 注意：每个节点的 `grid` 用户 `~/.ssh/authorized_keys` 文件必须包含所有集群节点生成的 `~/.ssh/id_dsa.pub` 文件的内容。

## E.1.3 启用节点间的 SSH 等效

在将包含所有密钥的 `authorized_keys` 文件复制到集群每个节点后，按照下列顺序完成操作。在本示例中，Oracle Grid Infrastructure 软件名为 `grid`：

- 1. 在要运行的系统中以 `grid` 用户登录。

2. 使用以下命令语法 `hostname1`、`hostname2` 等集群节点的公主机名（别名和完全域名）从本地节点到每个节点，包括从本地节点到自身，以及从每个节点到每个其他节点：



```bash
[grid@nodename]$ $ ssh hostname
[grid@nodename]$ $ ssh hostname2
```

例如：

```bash
[grid@grid]$ $ ssh node
The authenticity of host 'node' (xxx.xxx.101)' can't be established.
DSA key fingerprint is 7e:60:zz:zc:48:z1:a0:f7:4e.
Are you want to continue connecting (yes/no)? yes
Warning: Permanently added 'node,xxx.xxx.101' (DSA) to the list of known hosts.
Mon Dec 4 11:08:13 PST 2006
[grid@grid]$ $ ssh node.example.com
The authenticity of host 'node.example.com' (xxx.xxx.101)' can't be established.
DSA key fingerprint is 7e:60:zz:zc:48:z1:a0:f7:4e.
Are you want to continue connecting (yes/no)? yes
Warning: Permanently added 'node.example.com,xxx.xxx.101' (DSA) to the list of known hosts.
Mon Dec 4 11:08:13 PST 2006
[grid@grid]$ $ ssh node2
Mon Dec 4 11:08:35 PST 2006
```

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

- 3. 在每个节点重复步骤 2。

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

- 4. 在每个节点重复步骤 3。

在此过程结束时，每个成员节点的公主机名都应注册在所有其他节点的 `known_hosts` 文件中。

## E.2.1 最小参数设置

在安装期间，或当运行带有 `-fixup` 标志的集群验证实用程序 (`cluvfy`) 时，会生成修复脚本。如果无法使用修复，请查看下表以手动设置值：

| 参数 | 值 | 文件 |
|---|---|---|
| `semmsl` | 250 | `/proc/sys/sem` |
| `semmns` | 32000 | |
| `semop` | 100 | |
| `semni` | 128 | |
| `shmax` | 536870912 (512 MB) | `/proc/sys/shm` |

最大分配：

- Linux x86: 至少小于 4 GB，或 429496795。

建议：内存的一半。

- Linux x86-64: 至少小于物理内存

建议：内存的一半。

参见 Oracle-Support Note 567361 获取更多关于 `shmax` 的信息。

| 参数 | 值 | 文件 |
|---|---|---|
| `shmnmi` | 4096 | `/proc/sys/kernel/shmnmi` |
| `shmall` | 2097152 | `/proc/sys/kernel/shmall` |
| `file-max` | 6815744 | `/proc/sys/fs/file-max` |
| `ip_local_port_range` | 最小: 9000 最大: 65500 | `/proc/sys/net/ipv4/ip_local_port_range` |
| `rmem_default` | 262144 | `/proc/sys/net/core/rmem_default` |
| `rmem_max` | 4194304 | `/proc/sys/net/core/rmem_max` |
| `wmem_default` | 262144 | `/proc/sys/net/core/wmem_default` |
| `wmem_max` | 1048576 | `/proc/sys/net/core/wmem_max` |
| `aio-max-nr` | 1048576 | `/proc/sys/fs/aio-max-nr` |

> 注意：如果任何参数的当前值大于表中的值，脚本不会更改该参数的值。

## E.2.2 SUSE Linux 额外参数和内核设置

仅限 SUSE 系统，根据需要完成以下步骤：

- 1. 输入以下命令，使系统在启动时读取 `/etc/sysctl.conf`：

```
# /sbin/chkconfig boot.sysctl on
```

2. 仅在 SUSE 系统上，使用文本编辑器更改 `/etc/sysconfig/boot.sysctl` 参数中的 `RUN_PARALLEL` 标志从 `yes` 改为 `no`。

3. 将 `oinstall` 组的 GID 作为参数 `/proc/sys/vm/hugetlb_shm_group` 的值。这样做允许 `oinstall` 组拥有共享内存段的组权限。

例如，`oinstall` 组的 GID 为 501：

```
# echo 501 > /proc/sys/vm/hugetlb_shm_group
```

运行此命令后，使用 `vi` 将以下文本添加到 `/etc/sysctl.conf`，并启用 `boot.sysctl` 脚本在系统重启运行时：

`.hugetlb_shm_group=501`

> 注意：只能定义一个组为 `vm.hugetlb_shm_group`。

4. 在集群中的所有其他节点上重复步骤 1 到 3。

## E.3 手动检查 OFS2 版本

要手动检查您的 OCFS 版本，请输入以下命令：

```
modinfo ocfs2
rpm -qa | grep ocfs2
```

确保 `ocfs2console` 和 `ocfs2-tools` 至少为 1.2.7，且其他 OCFS 组件符合 `ocfs2-kernel_version-1.2.7` 或更高的模式。如果您想在共享主目录下安装 Oracle RAC，则 OCFS 版本必须为 1.4.1 或更高。

有关 OCF2 的信息，请参考网站：

`http://oss.oracle.com/projects/ocfs2/`

## 如何升级到 Oracle Grid Infrastructure 11g Release 2

本附录描述了如何执行 Oracle Clusterware 和 Oracle Automatic Storage Management (ASM) 的升级。

Oracle Clusterware 升级可以是滚动升级，其中部分节点会被关闭，而其他节点保持活动状态。Oracle Automatic Storage Management Release 2 (11.2) 升级是滚动升级。如果您升级了部分节点，则对您未选择升级的现有集群节点将执行仅限软件的安装。

本附录包含以下主题：

- 升级前备份 Oracle 软件
- 取消 Oracle 环境变量
- 关于 Oracle ASM 和 Oracle Grid Infrastructure 安装与升级
- Clusterware 和 Oracle ASM 升级的限制
- 准备升级现有的 Oracle Clusterware 安装
- 使用 CVU 验证 Oracle Clusterware 升级的就绪情况
- 从早期版本执行滚动升级
- 更新 DB Control 和 Grid Control 目标参数
- 解锁现有的 Oracle Clusterware 安装
- 升级后降级 Oracle Clusterware
- 升级后检查 Cluster Health Monitor 存储大小

### F.1 升级前备份 Oracle 软件

在对 Oracle 软件进行任何更改之前，Oracle 建议您为 Oracle 软件和数据库创建备份。

### F.2 取消 Oracle 环境变量

取消 Oracle 环境变量。

如果您已将 `ORA_CRS_HOME` 设置环境变量，请遵循 Oracle Support 的说明，在开始安装或升级之前取消它。除非有 Oracle Support 的明确指示，否则您永远不要将 `ORA_CRS_HOME` 作为环境变量。

## 关于 Oracle ASM 和 Oracle Grid Infrastructure 安装与升级

检查并确保安装用户的登录 shell 配置文件（例如 `.profile` 或 `.bashrc`）没有设置 `ORA_CRS_HOME`。

如果您在系统中已有现有的安装，并且使用相同的用户账户进行此安装，请取消以下环境变量：`ORA_CRS_HOME`；`ORACLE_HOME`；`ORA_NLS10`；`TNS_ADMIN` 以及任何与 Oracle 软件目录连接的 Oracle Infrastructure 安装的其他环境变量。



## F.3 关于 Oracle ASM 和 Oracle Grid Infrastructure 安装与升级

在过去，Oracle Automatic Storage Management (Oracle ASM) 是作为 Oracle Database 安装的一部分的。在 Oracle 11g release 2 (11.2) 中，在安装 Grid Infrastructure 组件时会安装 Oracle ASM，并在安装到集群（如 Oracle RAC 或独立服务器上的 Oracle Restart）时，它与 Oracle Cluster 共享一个 ASM。

如果您有现有的 ASM 实例，您可以在安装 Oracle Infrastructure 的同时对其进行升级，也可以在安装后使用 ASM Configuration Assistant (`ASMCA`) 进行升级。然而，请注意，在升级 Oracle ASM 之前，许多 ASM 功能被禁用，且在 Oracle ASM 在 Grid Infrastructure 目录中运行之前，Clusterware 将无法正常工作。因此，Oracle 建议如果您没有在升级 Oracle Cluster 的同时升级 ASM，则应立即升级 Oracle ASM。

可以使用 Oracle ASM Configuration Assistant (`ASMCA`) 对 ASM 实例执行离线升级。除了使用图形用户界面运行 `ASMCA` 外，您还非交互（静默）模式下运行 `ASMCA`。

在之前的版本中，您可以使用 Database Upgrade Assistant (`DBUA`) 升级 Oracle Database 或 Oracle ASM。现在不再如此。您只能使用 `DBUA` 升级 Oracle 数据库实例。使用 ASM Configuration Assistant (`ASMCA`) 升级 Oracle ASM。

> 参见 Oracle Database Upgrade Guide 和 Oracle Automatic Storage Management Administrator's Guide，以获取有关升级 Oracle ASM 安装的更多信息

## F.4 Clusterware 和 Oracle ASM 升级的限制

Oracle 建议您使用 `CVU` 检查升级 Oracle Grid Infrastructure 11g release 2 或 Oracle RAC database 11g Release 2 安装是否需要任何补丁。

> 参见 F6 节，“使用 CVU 验证 Oracle Clusterware 升级的就绪情况”

请注意 Oracle Infrastructure 升级的以下限制和变化：

- Oracle 建议您使用 `CVU` 检查升级 Oracle Grid Infrastructure 11g release 2 或 Oracle RAC database 11g Release 2 安装是否需要任何补丁。
- 要将 Oracle Grid Infrastructure 从 11.2.0.2 升级到 11.2.3 或更高版本，必须应用补丁 11.2.1 (11.2.2 PSU) 1 或更高版本。
- Oracle Cluster 和 ASM 升级始终是离线升级。在 Release 2 (11.2) 中，您无法对现有家 Oracle Cluster 和 ASM 进行原地升级。
- 如果 Oracle Cluster home 是共享家，请注意对于 Oracle Cluster 和 ASM 11 Release 2 的 Cluster home，可以使用非共享家作为 Grid Infrastructure。
- 在 Oracle Cluster 11 release 1 及后续版本中，Oracle Cluster 11g 软件的所有必须执行 Oracle Cluster 11g 升级。在 Oracle Database 11g 之前，所有 Oracle 软件安装都由用户（通常是 *oracle*）拥有，或者 Oracle Database 软件由单独用户拥有，而 Oracle Cluster 软件由 *crs* 所有。
- Oracle ASM 和 Oracle Cluster 都运行在 Oracle Grid Infrastructure home 中。
- 在向 Release 2 (11.2) 进行大版本升级期间，在升级完成之前，11g Release 2 (11.2) Oracle Grid Infrastructure 中的软件尚未完全可用。在运行 `rootupgrade.sh` 脚本并在所有节点完成升级之前，不支持从 11g Release 2 (11.2) home 运行 `srvctl`、`crsctl` 和其他命令。
- 在 Oracle Grid Infrastructure 升级期间，使用 `srvctl` 查找早期版本（10.x 或 11.1 版本）home 中的现有数据库。
- 在安装 Oracle Cluster 期间，如果本地节点上有单实例 Oracle ASM 版本，则将其转换为集群 Oracle ASM 11g。

## 准备升级现有 Oracle 集群安装

适用于 Release 2 (11.2) 安装，且 Oracle ASM 在所有节点上的 Oracle Grid Infrastructure 上运行。

- 带有 Oracle Cluster 11g Release 2 (11.2) 及更高版本，你可以对共享的集群 home 环境进行升级。
- 如果单实例（非集群式）Oracle ASM 安装在远程节点上（该节点是本地节点以外的节点，即正在执行 Oracle Grid Infrastructure 安装的节点），则它将保持为单实例 Oracle ASM 安装状态。然而，在安装过程中，如果你选择将 Oracle 集群注册表 (`OCR`) 投票磁盘文件放置在 Oracle ASM 上，则会在集群中的所有节点上创建集群的 ASM 安装，导致远程节点上的单实例 ASM 安装变得无法工作。
- 随着 Oracle Database 和 Oracle RAC 11g Release 2 (11.2) 的发布，不再支持使用数据库配置助手 (`DBCA`) 或安装程序将 Oracle 集群或 Oracle 数据库文件存储在块设备或原始设备上。

如果你打算升级现有的 RAC 数据库或带有 ASM 实例的 Oracle RAC 数据库，可以使用现有的原始或块设备，并对现有安装进行滚动升级。不允许使用块设备或原始设备进行新安装。

**另参阅：** Oracle Database 升级指南

## F.5 准备升级现有 Oracle 集群安装

如果你有现有的 Oracle 集群安装，则通过执行离地升级（out-of-place upgrade）来升级现有集群。你无法执行原地升级（in-place upgrade）。

本节包含以下主题：

- 升级现有 Oracle 集群安装前完成的检查
- 运行 Oracle RACcheck 升级就绪评估

### F.5.1 升级现有 Oracle 集群安装前完成的检查

在开始升级之前完成以下任务：

- 1. 针对每个节点，使用集群验证工具 (Cluster Verification Utility) 确保你已完成安装前的准备步骤。它可以生成修复脚本 (Fixup scripts) 来帮助你准备服务器。此外，安装程序将帮助你确保满足所有必要的先决条件。

确保你拥有安装期间所需的各种，包括以下：

- Oracle Cluster 的 Oracle 基础位置 (base location)
- 与你现有 Oracle Cluster 路径不同的 Grid Infrastructure home 路径
- 一个 `SCAN` 扫描地址
- 用于授予 Oracle ASM 数据文件访问权限的特权用户组（ASM 的 `OSDBA` 组）、用于授予 Oracle ASM 实例管理权限的组（`OSASM` 实例），以及用于授予 Oracle ASM 实例一组管理权限的组（ASM 的 `OSOPER`）
- `root` 用户权限，以便在安装期间以 root 身份运行脚本
- 2. 对于运行安装的安装所有者，如果你为现有安装设置了环境变量，请取消环境变量 `$ORACLE_HOME` 和 `$ORACLE_SID`，因为这些环境变量在升级期间会持续使用。例如：

```
$ORACLE_BASE
$ORACLE_HOME
$ORACLE_SID
```

**另参阅：** 章节 F2，“取消 Oracle 环境变量”

### F.5.2 运行 RACCheck 升级就绪评估

可以使用 `RACCheck`（Oracle RAC 配置审计工具）升级就绪评估来为升级到 Oracle Infrastructure 11.2.0.3、11.2.0.4 和 12.1.0.1 获取自动化的针对升级的健康检查。你可以运行 `RACCheck` 升级就绪评估工具，并自动化许多手动的升级前和升级后检查。



Oracle 建议从 My Oracle Support 下载并运行最新版本的 RACcheck。有关下载、配置和运行 RACcheck 配置审计工具的信息，请参阅 My Oracle Support 备注 1457357.1，该 URL 如下：

https://support.oracle.com/csp/main/article?cmd=showtype=NOTID&id=1457357.1

## F.6 使用 CVU 验证 Oracle Clusterware 更新的就绪性

查看本节内容以验证你的集群是否已准备好升级。

### F.6.1 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项如下：

- `-nodelist`

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- `-rolling`

使用此标志验证滚动升级的就绪性。

## 从早期版本执行滚动升级

- `src_crshome src_Gridhome`

使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。

- `-dest_crsshome dest_Gridhome`

使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。

- `-dest_version dest_version`

使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。

- `[-fixup (fixupdir path)]`

使用此标志指示修复目录的路径。

- `[-verbose]`

使用此标志产生详细输出。

### F.6.2 验证 Oracle 集群更新的就绪性

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- `-nodelist`

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- `-rolling`

使用此标志验证滚动升级的就绪性。

### F.6.3 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- `-nodelist`

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- `-rolling`

使用此标志验证滚动升级的就绪性。

## F.5 准备现有 Oracle 集群安装

如果你有现有的 Oracle 集群安装，则通过执行离地升级（out-of-place upgrade）来升级现有集群。你无法执行原地升级（in-place upgrade）。

本节包含以下主题：

- 升级现有 Oracle 集群安装前完成的检查
- 运行 Oracle RACcheck 升级就绪评估

### F.5.1 升级现有 Oracle 集群安装前完成的检查

在开始升级之前完成以下任务：

1. 针对每个节点，使用集群验证工具（Cluster Verification Utility）确保你已完成安装前的准备步骤。它可以生成修复脚本（Fixup scripts）来帮助你准备服务器。此外，安装程序将帮助你确保满足必要的先决条件。

确保你拥有安装期间所需的各种，包括：

- Oracle Cluster 的 Oracle 基础位置（base location）
- 与你现有 Oracle Cluster 路径不同的 Grid Infrastructure home 路径
- 一个 SCAN 扫描地址
- 用于授予 Oracle ASM 数据文件访问权限的特权用户组（ASM 的 OSDBA 组）、用于授予 Oracle ASM 实例管理权限的组（OSASM 实例），以及用于授予 Oracle ASM 实例一组管理权限的组（ASM 的 OSOPER）
- root 用户权限，以便在安装期间以 root 身份运行脚本

2. 对于运行安装的安装所有者，如果你为现有安装设置了环境变量，请取消环境变量 `$ORACLE_HOME` 和 `$ORACLE_SID`，因为这些环境变量在升级期间会持续使用。例如：

```
$ORACLE_BASE
$ORACLE_HOME
$ORACLE_SID
```

**另参阅：** 章节 F2，“取消 Oracle 环境变量”

### F.5.2 运行 RACCheck 升级就绪评估

RACCheck（Oracle RAC 配置审计工具）升级就绪评估可以为升级到 Oracle Infrastructure 11.2.0.3、11.2.0.4 和 12.1.0.1 获取自动化的针对升级的健康检查。你可以运行 RACCheck 升级就绪评估工具，并自动化许多手动的升级前和升级后检查。

Oracle 建议从 My Oracle Support 下载并运行最新版本的 RACcheck。有关下载、配置和运行 RACcheck 配置审计工具的信息，请参阅 My Oracle Support 备注 1457357.1，该 URL 如下：



https://support.oracle.com/csp/main/article?cmd=showtype=NOTID&id=1457357.1

## F.6 使用 CVU 验证 Oracle Clusterware 更新的就绪性

查看本节内容以验证你的集群是否已准备好升级。

### F.6.1 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项如下：

- - nodelist

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- - rolling

使用此标志验证滚动升级的就绪性。

## 从早期版本执行滚动升级

- src_crshome src_Gridhome

使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。

- -dest_crsshome dest_Gridhome

使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。

- -dest_version dest_version

使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。

- [-fixup (fixupdir path)]

使用此标志指示修复目录的路径。

- -verbose

使用此标志产生详细输出。

### 从早期版本执行滚动升级

- src_crshome src_Gridhome

使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。

- -dest_crsshome dest_Gridhome

使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。

- -dest_version dest_version

使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。

- [-fixup (fixupdir path)]

使用此标志指示修复目录的路径。

- -verbose

使用此标志产生详细输出。

### F.6.2 验证 Oracle 集群更新的就绪性

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- - nodelist

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- - rolling

使用此标志验证滚动升级的就绪性。

### F.6.3 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- - nodelist

`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- - rolling

使用此标志验证滚动升级的就绪性。

## F.5 准备现有 Oracle 集群安装

如果你有现有的 Oracle 集群安装，则通过执行离地升级（out-of-place upgrade）来升级现有集群。你无法执行原地升级（in-place upgrade）。

本节包含以下主题：

- 升级现有 Oracle 集群安装前完成的检查

- 运行 Oracle RACcheck 升级就绪评估

### F.5.1 升级现有 Oracle 集群安装前完成的检查

在开始升级之前完成以下任务：

- 1. 针对每个节点，使用集群验证工具 (Cluster Verification Utility) 确保你已完成安装前的准备步骤。它可以生成修复脚本 (Fixup scripts) 来帮助你准备服务器。此外，安装程序将帮助你确保满足必要的先决条件。

确保你拥有安装期间所需的各种，包括：

- Oracle Cluster 的 Oracle 基础位置 (base location)

- 与你现有 Oracle Cluster 路径不同的 Grid Infrastructure home 路径

- 一个 SCAN 扫描地址

- 用于授予 Oracle ASM 数据文件访问权限的特权用户组（ASM 的 OSDBA 组）、用于授予 Oracle ASM 实例管理权限的组（OSASM 实例），以及用于授予 Oracle ASM 实例一组管理权限的组（ASM 的 OSOPER）

- root 用户权限，以便在安装期间以 root 身份运行脚本

- 2. 对于运行安装的安装所有者，如果你为现有安装设置了环境变量，请取消环境变量 `$ORACLE_HOME` 和 `$ORACLE_SID`，因为这些环境变量在升级期间会持续使用。例如：

```
$ORACLE_BASE
$ORACLE_HOME
$ORACLE_SID
```

**另参阅：** 章节 F2，“取消 Oracle 环境变量”

### F.5.2 运行 RACCheck 升级就绪评估

RACCheck（Oracle RAC 配置审计工具）升级就绪评估可以为升级到 Oracle Infrastructure 11.2.0.3、11.2.0.4 和 12.1.0.1 获取自动化的针对升级的健康检查。你可以运行 RACCheck 升级就绪评估工具，并自动化许多手动的升级前和升级后检查。

Oracle 建议从 My Oracle Support 下载并运行最新版本的 RACcheck。有关下载、配置和运行 RACcheck 配置审计工具的信息，请参阅 My Oracle Support 备注 1457357.1，该 URL 如下：

https://support.oracle.com/csp/main/article?cmd=showtype=NOTID&id=1457357.1

## F.6 使用 CVU 验证 Oracle Clusterware 更新的就绪性

查看本节内容以验证你的集群是否已准备好升级。



### F.6.1 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项如下：

- `-nodelist`
`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。
- `-rolling`
使用此标志验证滚动升级的就绪性。

## 从早期版本执行滚动升级

- `src_crshome src_Gridhome`
使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。
- `-dest_crsshome dest_Gridhome`
使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。
- `-dest_version dest_version`
使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。
- `[-fixup (fixupdir path)]`
使用此标志指示修复目录的路径。
- `-verbose`
使用此标志产生详细输出。

### F.6.2 验证 Oracle 集群更新的就绪性

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- `-nodelist`
`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。
- `-rolling`
使用此标志验证滚动升级的就绪性。

### F.6.3 关于 CVU 网格验证命令选项

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项：

- `-nodelist`
`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。
- `-rolling`
使用此标志验证滚动升级的就绪性。

## F.5 准备现有 Oracle 集群安装

如果你有现有的 Oracle 集群安装，则通过执行离地升级（out-of-place upgrade）来升级现有集群。你无法执行原地升级（in-place upgrade）。

本节包含以下主题：

- 升级现有 Oracle 集群安装前完成的检查
- 运行 Oracle RACcheck 升级就绪评估

### F.5.1 升级现有 Oracle 集群安装前完成的检查

在开始升级之前完成以下任务：

- 1. 针对每个节点，使用集群验证工具（Cluster Verification Utility）确保你已完成安装前的准备步骤。它可以生成修复脚本（Fixup scripts）来帮助你准备服务器。此外，安装程序将帮助你确保满足必要的先决条件。

确保你拥有安装期间所需的各种，包括：

- Oracle Cluster 的 Oracle 基础位置（base location）
- 与你现有 Oracle Cluster 路径不同的 Grid Infrastructure home 路径
- 一个 SCAN 扫描地址
- 用于授予 Oracle ASM 数据文件访问权限的特权用户组（ASM 的 OSDBA 组）、用于授予 Oracle ASM 实例管理权限的组（OSASM 实例），以及用于授予 Oracle ASM 实例一组管理权限的组（ASM 的 OSOPER）
- root 用户权限，以便在安装期间以 root 身份运行脚本
- 2. 对于运行安装的安装所有者，如果你为现有安装设置了环境变量，请取消环境变量 `$ORACLE_HOME` 和 `$ORACLE_SID`，因为这些环境变量在升级期间会持续使用。例如：

```
$ORACLE_BASE
$ORACLE_HOME
$ORACLE_SID
```

另参阅：章节 F2，“取消 Oracle 环境变量”

### F.5.2 运行 RACCheck 升级就绪评估

RACCheck（Oracle RAC 配置审计工具）升级就绪评估可以为升级到 Oracle Infrastructure 11.2.0.3、11.2.0.4 和 12.1.0.1 获取自动化的针对升级的健康检查。你可以运行 RACCheck 升级就绪评估工具，并自动化许多手动的升级前和升级后检查。

Oracle 建议从 My Oracle Support 下载并运行最新版本的 RACcheck。有关下载、配置和运行 RACcheck 配置审计工具的信息，请参阅 My Oracle Support 备注 1457357.1，该 URL 如下：

`https://support.oracle.com/csp/main/article?cmd=showtype=NOTID&id=1457357.1`

## F.6 使用 CVU 验证 Oracle Clusterware 更新的就绪性

查看本节内容以验证你的集群是否已准备好升级。

### F.6.1 关于 CVU 网格验证命令选项



导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

该命令使用以下语法，变量内容用斜体表示：

```
runcluvfy.sh -pre crsinint -upgrade [-n nodelist list] [-rolling] -src_crshome src_Gridhome -dest_crsshome dest_Gridhome -dest_version dest_version [-fixup (fixupdir path)] [-verbose]
```

选项如下：

- `-n` `nodelist`
`-n` 标志指示集群成员节点，即你想要运行升级前验证的非域限定节点名称的逗号分隔列表。如果你不在验证命令中没有添加 `-n` 标志，则将对集群中的所有节点进行验证。如果在运行 `runcluvfy.sh` 的节点上集群软件处于关闭状态，则必须添加 `-n` 标志。

- `-rolling`
使用此标志验证滚动升级的就绪性。

## 从早期版本执行滚动升级

- `src_crshome` `src_Gridhome`
使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。

- `-dest_crsshome` `dest_Gridhome`
使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。

- `-dest_version` `dest_version`
使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。

- `[-fixup (fixupdir path)]`
使用此标志指示修复目录的路径。

- `-verbose`
使用此标志产生详细输出。

### 从早期版本执行滚动升级

- `src_crshome` `src_Gridhome`
使用此标志指示你想要升级的现有 Oracle Cluster 或 Grid home 的位置，其中 `src_Gridhome` 是 home 的路径。

- `-dest_crsshome` `dest_Gridhome`
使用此标志指示升级的位置，其中 `dest_Gridhome` 是 home 的路径。

- `-dest_version` `dest_version`
使用此标志指示升级的发行版本号，其中 `dest_version` 是版本号。

- `[-fixup (fixupdir path)]`
使用此标志指示修复目录的路径。

- `-verbose`
使用此标志产生详细输出。

### F.6.2 验证 Oracle 集群更新的就绪性

导航到升级阶段（即 `runcluvfy.sh` 命令所在阶段），运行命令 `runcluvfy.sh stage -pre crsinint -upgrade` 以检查你的 Oracle Clusterware 安装升级的就绪性。带有 `-pre crsinint -upgrade` 标志运行 `runcluvfy.sh` 会执行系统检查，以确认集群是否处于从现有集群升级的正确状态。

（此处省略重复部分，翻译逻辑保持一致）

...直到 Oracle ASM 升级，

直到 Oracle ASM 升级，

如果如果安装了更早版本的 Oracle Automatic Storage Management，那么安装程序将启动 ASM Configuration Assistant 来升级 Oracle ASM 到 11g (11.2)。

> 注意：Oracle 建议保持 RAC 实例运行。当你在启动 root 脚本时，实例会被关闭并重新启动。

1. 启动安装程序，并选择升级现有 Clusterware 和 ASM 安装。
2. 在节点选择界面，选择所有节点。
3. 当提示时，在集群中的每个节点上运行 `rootupgrade.sh` 脚本。

首先在本地节点上运行脚本。脚本将关闭早期版本安装，将其替换为新的 Clusterware 版本，并启动新的 Clusterware 安装。

当脚本在最后一个节点之外的所有节点上成功运行后，你可以在所有节点上并行运行，但其中一个作为最后一个节点。

4. 在最后一个节点上运行 `rootupgrade.sh` 脚本后，如果你是从早于 11.2.0.1 的版本升级，并且勾选了带有 ASMCA 标记框，那么 ASM Configuration Assistant 将自动运行，Oracle Clusterware 升级即完成。如果你在升级的面试阶段取消勾选了该框，则不运行 ASMCA。

Grid home 中的 11g Release (11.2) Oracle ASM 管理工具（例如 `svctl`）将无法工作。

2. 因为 Oracle Grid Infrastructure home 的位置与之前的 Oracle Cluster 和 Oracle ASM home 不同，请更新任何使用了位于 Oracle Cluster 和 Oracle ASM home 中的实用程序、库文件或其他文件的脚本或应用程序。

> 注意：在升级结束时，如果您手动将 OCR 备份位置设置为旧版本的 Oracle Cluster (CRS home)，则你必须将 OCR 备份位置重新设为 Oracle Grid Infrastructure home (Grid home)。如果您没有手动设置 OCR 备份位置，则此问题与您无关。

由于 Oracle Clusterware 的升级是离线升级（out-of-place upgrades），因此之前的 Oracle Cluster home 不能作为 OCR 备份的位置。必须删除旧 Oracle Cluster home 中的备份。

## F.7.2 在节点变得不可访问时完成 Oracle Cluster 升级

如果在升级过程中某些节点变得不可访问，您将无法完成升级，因为升级脚本 (`rootupgrade.sh`) 未在不可访问的节点上运行。由于升级未完成，Oracle Clusterware 将保持在之前的版本。您可以通过执行命令 `crctl activeversion` 来确认升级未完成。

要解决此问题，请使用以下语法带有 `-force` 标志运行 `rootupgrade.sh` 命令：

```
Grid_Home/rootupgrade -force
```

例如：

```bash
# /u01/app/11.2.0/grid/rootupgrade -force
```

此命令强制完成升级。通过命令 `crctl query activeversion` 验证升级已完成。活动版本应为升级版本。

## F.7.3 对 Oracle 自动存储管理进行滚动升级

在完成 Oracle Cluster 11g Release 2 (11.2) 之后，如果您在升级 Oracle Clusterware 时没有选择升级 ASM，那么您可以使用 Oracle Automatic Storage Management Configuration Assistant (`asmca`) 将其分离出来并执行滚动升级。

您可以使用 `asmca` 独立完成升级，但您应该在升级 Oracle Cluster 后尽快进行，因为在 Oracle ASM 升级之前，诸如 `svctl` 等 Oracle ASM 管理工具将无法工作。

> 注意：仅当旧版本的 Oracle ASM 为 11.1.0.6 或 11.1.0.7 时，ASMCA 才会执行滚动升级。否则，ASMCA 将执行普通升级，此时 ASMCA 会关闭所有节点上的所有 Oracle ASM 实例，并在新的 Grid home 中重新启动所有实例。

### F.7.3.1 准备升级 Oracle ASM

如果您打算对 Oracle ASM 执行滚动升级，请注意以下几点：

- Oracle Clusterware 的活动版本必须是 11g Release 2 (11.2)。通过输入以下命令确定活动版本：

```
$ csctl crs activeversion
```

- 您可以将单实例 Oracle ASM 安装升级为集群式 Oracle ASM 安装。但是，只有当您在安装 Oracle ASM 的节点上运行安装时，才能升级现有的单实例 Oracle ASM 安装。您无法在远程节点上升级单实例 ASM 安装。

- 您必须确保在开始升级过程之前，现有 ASM 安装上的任何重平衡（rebalance）操作都已完成。

在在升级过程中，您会将 Oracle ASM 实例更改为升级状态。由于此升级状态会限制 ASM 操作，您应该在开始后尽快完成升级过程。以下是 Oracle ASM 实例处于升级状态时允许的操作：

- 磁盘组的挂载和卸载
- 打开、调整大小或删除数据库文件
- 恢复实例



对固定视图和包的查询：允许用户查询固定视图并使用固定包（如 `dbms_diskgroup`）运行任何 PL/SQL

### F.7.3.2 升级 Oracle ASM

完成以下步骤以升级 Oracle ASM：

1. 在您计划启动升级的节点上，将环境变量 `ASMCA_ROLLING_UPGRADE` 设置为 `true`。例如：

```
$ export ASMCA_ROLLING_UPGRADE=true
```

2. 从 Oracle Grid Infrastructure 11g Release 2 (11.2) home 启动 `asmca`。例如：

```
$ cd /u01/11.2/grid/bin
$ ./.asmca
```

3. 选择升级。

ASM Configuration Assistant 为集群中的所有节点顺序升级 ASM。

4. 完成升级后，运行命令取消 `ASMCA_ROLLING_UPGRADE` 环境变量。

另参：《Oracle Database Upgrade Guide》和《Oracle Automatic Storage Management Administrator's Guide》，获取有关准备 Oracle ASM 升级计划的更多信息，以及启动、完成和停止 Oracle ASM 升级的方法。

## F.8 更新 DB Control 和 Grid Control 目标参数

由于 Oracle Cluster release 2 (11.2) 是将 Oracle Cluster 离线升级到新位置（即 Oracle Grid Infrastructure for Cluster，或 Grid home），必须更改系统文件中 CRS HOME 的路径。如果您不更改该参数，将在 DB Control 或 Grid Control 中遇到“cluster target broken”等错误。

使用以下步骤解决此问题：

1. 登录 dbconsole 或 gridconsole。
2. 导航到 Cluster 标签页。
3. 点击 Monitoring Configuration
4. 使用新的 Grid home 更新 Oracle Home 的值。

## F.9 解锁现有的 Oracle Clusterware 安装

从之前的版本升级后，如果您想重新安装旧版本的 Oracle Grid Infrastructure home，则必须先更改 home 的权限和所有者。

此脚本将降级 OCR。如果您想停止部分或失败的 11g Release 2 (11.2) 安装并恢复之前的版本 Oracle Clusterware，请在此命令中使用 `-force` 标志。

3. 以 Grid 安装所有者的身份登录，并运行以下命令，其中 `/u01/app/grid` 是新（更新的）Grid home (11.2) 的位置：

```
$Grid_home=/u01/bin/runInstaller -now -waitforcompletion -ignoreSysPrereqs -updateNodeList -silent CRS=false ORACLE_HOME=/u01/app/grid
```

4. 以 Grid 基础设施所有者的身份运行命令 `./runInstaller -now -waitcompletion -ignoreSysPrereqs -updateNodeList -silent CRS=true ORACLE_HOME=home12_crs_home`，其中 `home12_crs_home` 代表早期 Oracle Cluster 安装的目录。

例如：

```
$Grid_home=/u01/bin/runInstaller -waitforcompletion -ignoreSysPrereqs -updateNodeList -silent CRS=true ORACLE_HOME=/u01/app/crs
```

## 5. 降级到 11.2 及更高版本

1. 如果您正将 Oracle Infrastructure release 2 (11.2.0.4) 降级到早期的 11.2 版本，在所有集群节点上执行 `rootupgrade.sh` 后，请从 11.2.0.4 Grid home 运行以下命令：

`acsroot uninstall`

2. 从早期的 Grid home 以特权用户 (root) 运行以下命令：

`acsroot install`

3. 在每个节点上，使用命令 `crctl start cr` 从早期 Oracle Cluster home 启动 Oracle Clusterware。例如，如果早期版本 home 为 `crshome11202`，请在每个节点上使用以下命令：

`cshome11202/bin/crsctl start cr`

降级到 11.1 及更高版本

您将被提示在集群的每个节点上顺序从早期 Oracle Cluster 安装 home 运行 `root.sh`。完成此任务后，降级即告完成。

从早期 Oracle Cluster 安装 home 运行 `root.sh` 会启动 Oracle Cluster 堆栈，启动之前在旧版本 Oracle Cluster 中注册的所有资源，并配置初始化脚本以运行早期版本的 Oracle Cluster 堆栈。

6. 修改环境变量以指向您要降级到的目录：

- `ORACLE_HOME`
- `PATH`

确保您的 `oratab` 文件以及任何设置 `ORACLE_HOME` 值的客户端脚本指向降级后的 Oracle home。

## F.11 升级后检查集群健康监控（Cluster Health Monitor）仓库的大小

如果您是从早期版本的 IPD/OS 升级到 Oracle Grid Infrastructure release 2 (11.2.0.2 及更高版本)，则应检查集群健康监控仓库（CHM 仓库）的大小。Oracle 建议您查看自己的 CHM 仓库需求，如果您希望维持较大的 CHM 仓库，请增大仓库大小。

> 注意：当您安装 Oracle Grid Infrastructure 并在每个节点上运行 `root.sh` 脚本时，您之前的 之前的 IPD/OS 仓库将被删除。

IBM: Linux on System z 配置不支持集群健康监控。

默认情况下，release 11.2.0.2 及更高版本的 CHM 仓库大小至少为 1GB 或 3600 秒（1小时）。对于 release 11.2.0.2 和 11.2.0.3，无论集群大小如何，CHM 仓库均为1GB (1 GB)。

要增大 CHM 仓库，请使用以下命令语法，其中 `RETENTION_TIME` 是秒为单位的 CHM 仓库大小：

```
oclumon manage -repos resize RETENTION_TIME
```

`RETENTION_TIME` 的值必须大于 3600（一小时）且小于 259200（三天）。如果增大了 CHM 仓库大小，则必须确保集群每个节点都有足够的本地空间供仓库使用。如果空间不足，可以将仓库移动到共享存储。

例如，将仓库大小设置为四小时：

```
$ oclumon manage -repos resize 14400
```

## 索引

## A

accounts 配置, 2-5

ACFS. 参见 Oracle ACFS.

aio-max-nr, E-6

AMD-34

software requirements, 2-43

and asm errors, 2-12

architecture

checking system architecture, 2-27

Asianux

operating system requirements, 2-31, 2-44

ASM

and multiple databases, 2-18

and rolling upgrade, 7-22

ASM library driver (ASMLIB), 4-8

block devices, 2-28

candidate disks, 1-7, 3-25

characteristics of failure groups, 2-31, 3-35

checking availability, 2-28, 3-39

configuring disks for ASM, 2-25

creating the OSDBA for ASM group, 2-19

disks, 3-19

display attacks, 2-28

on Linux, 3-39

failure groups, 3-19

examples, 2-21, 3-35

identifying, 2-31, 3-35

identifying available disks, 3-28

number of instances on each node, 1-6

OSAM administrator, 2-27

OSDBA for ASM group, 2-18



## recommendations for disk groups, 3-19

required for Standard Edition, 3-2

required for Typical instance, 3-2

rolling upgrade of, 4-2

space for Cluster files, 3-20

space for preconfigured data, 3-20

storage option for data files, 4-4

storing Oracle Cluster files, 3-6

## ASM disks, 4-8

### ASM group
creating, 2-19

### ASM library driver (`oracleasm`)
installing, 3-26

Used to create disk groups for older releases, 5-5

## ASMLIB, 4-8
configuring system options for, 3-31

how to configure, 3-27

## ASM, 4-3, B-7
Automatic Management Cluster File System. 参见 Oracle ACFS.

Automatic Storage Management. 参见 ASM.

## B

### Bash shell
default startup file, 2-70

setting shell limits, 2-72

`bash_profile`, 2-70

### binaries
relinking, 5-6

### block devices and upgrades, 3-4
creating permissions for Oracle Cluster files, 3-32

creating permissions for Oracle Database files, 3-37

support of, 3-37

support, 3-4

device name, 2-28

for upgrades, 3-37

### block devices deployed, BMC
configuring, 2-65

### BMC interface
preinstallation tasks, 63

## C shell
default startup file, 2-70

setting shell limits, 2-72

candidate disks marking, 1-7, 3-25

### Bourne shell
default startup file, 2-70

setting shell limits on Linux, 2-72

## D

central inventory, 2-16

about, 2-1

central inventory. 参见 Oracle Inventory group

changing host names, 4-4

checkdisk error, E-5

checking disk availability for ASM, 3-39

checking Linux distribution, 2-60

`chmod` command, 3-17

`chown` command, 3-17

### clients
connecting to SCANs, 3-4

### cloning
cloning a Grid to other nodes, 4-9

cluster configuration file, 4-8

cluster file system storage option for data files, 3-4

cluster file systems Grid home supported on, 3-2

cluster name, 4-4

cluster nodes private node names, 4-4

public node names, 4-4

specifying ids and gids, 2-21

virtual node names, 4-4

Cluster Time Synchronization, 6-11

### Cluster Verification
`cuvadisk`, 2-62

`trou`, A-7

### commands, 2-71
`asmca`, 3-6

`asmcmcd`, 2-12

`cat`, 2-60

`chmod`, 3-17

`chown`, 3-17

`crctl`, 4-11, 5-3, F-9

`dd`, xx

`df`, 1-3-27, 2-71

`env`, 2-71

`fdisk`, 3-28, 3-32, 3-39

`free`, 2-37

`groupadd`, 2-21

`id`, 2-21

`ipmitool`, 2-66

`lsdev`, 3-28, 3-39

`lsmod`, 2-64

`mkdir`, 3-17

`modinline`, 2-60

`modprobe`, 2-64

`nscd`, 3-36

`partpt`, 3-34, 3-37

`passwd.`, 2-22

`ping`, 2-29

`rootopts.pl`, 5-6

andconfigure, 6-4

`rootupgrade.sh`, F-3

`rpm`, 2-60, 63

`sqlplus`, 2-12

`srvctl`, F-3

`swap`, 2-26

`swapon`, 2-26

`umask`, 2-27, 60, 3-26

`unf`, F-5

`useradd`, 2-13, 2-20, 22-22

`usermod`, 2-21

`xhost`, 2-5

`xm`, 2-10

`yum`, 2-5

- 对于数据文件，3-9

- 最小写入大小值，3-10, 目录

- 创建单独的数据目录，3-16, 3-17

- 数据文件目录的权限，3-17

- 磁盘组

- ASM, 3-19

- Oracle ASM 磁盘组建议

- 磁盘空间

- 建议，3-19

- 检查，2-27

- ASM 中预配置数据库的节点，3-20

- 磁盘

- 检查 ASM 情况，2-28, 3-39

- 显示已连接磁盘，3-28

- 在 Linux 上，3-29

- 磁盘，亦参阅 ASM 磁盘

- DISPLAY 环境变量设置，2-71

- DNS, A-12

# E

- 模拟器

- 从 X 模拟器安装，2-10

- enterprise.file, B-3

- env 命令，2-71

- 环境

- 检查设置，2-71

- 为 oracle 用户配置，2-69

- 环境变量

- DISPLAY, 2-71

- ORACLE_BASE, 2-70, D-2

- ORACLE_HOME, 2-12, 2-70, F-5

- ORACLE_SID, 2-20, F-5

- 从 shell 启动项中移除，2-70

- SHELL, 2-79

- TEMP 和 TMPDIR，2-27, 2-71

- 勘误

- Linux 内核错误，2-70

- X11 转发，2-72, E-5

- 使用 ODPatch 的错误，3-6

- Exadata

- 以及 rp_, 过滤器，3-26

- 重新链接二进制文件文件，5-6

- 示例

- ASM 故障组，3-21, 3-35

# F

- 故障组

- ASM, 3-19

- ASM 故障组的特性，2-21, 3-35

- ASM 故障组示例，3-21, 3-35

- idisk 命令，2-28, 3-39

- 特性，新的，xv

- 隔离，xx

- 以及 cssd 代理和监控，xx

- 以及 IPMI，xx, 2-63, 4-6

- 文件创建掩码设置，2-69

- 文件系统

- 数据文件的存储选项，3-4

- 文件系统，3-6

- file-max, E-6

- 文件

```bash
bash_profile, 2-70
- dbca.re, B-3
- 编辑 shell 脚本，2-70
- enterprise., B-3
- .login, 2-70
- radmf.loc, 2-11
- /proc/sys/fs/mem, E-6
- /proc/sys/kernel, E-6
- /proc/sys/shm, E-6
- /proc/sys/kernel/shmmax, E-6
- /proc/sys/net/ipv4/local_port_range, E-6
- /proc/sys/net/ipv4/local_port_range
```

- 响应，2-8

- 卷集，3-27

- 修复脚本，2-8

- 关于，1-1

# G

- GFS, 3-6

- gid

- 识别，2-21

- 指定，2-21

- 在其他节点上指定，2-21

- 全球化

- 支持，4-3

- GNS

- 关于，2-30

- GFS 虚拟接口，4-3

- GFS, 3-6

- Grid home

- 以及 Oracle ，2-13

- 默认路径，2-74

- 磁盘空间，2-25

- 解锁，5-6



# 命名服务，GNS

- grid 用户，2-16
- `grid_install.sp`，B-3
- 组
- 识别，2-21
- 指定，2-21
- 在其他节点上指定，2-21
- OSASM (`asmd`)，2-17
- OSDBA (`dba`)，2-17
- OSDBA for ASM (`asdba`)，2-18
- OSDBA group (`dba`)，2-17
- OSOPER (`oper`)，2-17
- OSOPER group (`oper`)，2-17
- 安装所需的，2-26
- 创建用户时指定，2-21
- 使用 NIS，2-16, 22

# K

- 内核
- Linux 勘误，2-60
- 内核参数-配置，E-5
- Korn shell
- 以及 LDAP，2-41, 2-52
- 默认启动文件，2-70
- 设置 shell 限制，2-72
- `ksh`
- 计时器
- 被 csd 代理替换，xx
- 硬件要求，2-24
- 高可用 IP 地址，2-28
- 主机名
- 更改，4-4
- 合法主机名，4-4

# L

- LDAP
- `odisreg` 系统要求，2-41, 2-52
- `oidca` 系统要求，2-41, 2-52
- 合法主机名，4-4
- `libpam`，2-41
- 协议-参见 LDAP
- Linux
- 检查版本，2-60
- `cvudskij` 包，2-62
- 确定，2-60
- 显示已连接磁盘，3-39
- `ner` 勘误，2-60
- 多路互连文件设置，2-36
- Linux (32位) 系统要求，3-38
- Linux on System z-IBM-86/64 系统要求，43
- Linux-pam，2-41, 2-52
- 日志文件
- 安装期间访问，4-7
- `logan` 文件，2-70
- `leader` 命令，3-38, 3-39

# IBM

- Linux on System z-集群健康监控可用，1-3
- IBM: System z-软件要求，2-54
- `id` 命令，2-21
- IDE 磁盘
- 设备名称，3-28
- INS-3026 错误，2-13
- 安装
- 以及 cron 任务，4-5
- 全球化，4-3
- 将 Grid 基础设施复制到其他，A-14
- 节点，4-9
- 完成后，B-2
- 响应文件，B-2
- 准备，B-2, B-4
- `amples`，B-2
- 静默模式，B-5
- 使用集群配置文件，4-8
- 安装类型
- 以及 ASM，3-20
- 接口，4-3
- 私有实例所需的，D-4
- `intermunt` 处理-以及套接字文件，4-12
- `ip_local_port_Range`，E-6
- IPMI
- 未由 GNS 配置的地址，2-64
- 配置驱动程序，2-64
- 安装前任务，2-63
- 安装准备，4-6

# M

- 掩码
- 设置默认文件创建，2-69
- 内存资源，2-29
- 最小 Linux 安装
- 建议，2-2
- 混合二进制文件，3-38
- `mkdir` 命令，3-17
- 模式
- 设置默认文件模式创建，2-69
- 多个数据库
- 以及 ASM，2-18
- 多路互连
- `rap_filter` 设置，2-36

# J

- JDK 要求，2-37
- 任务角色分离用户，2-16

# Index-4

- 多个 oracle home，2-12, 3-17
- 配置 Oracle ASM 驱动程序，3-27
- My Oracle Support，5-1

# N

- 配置 Oracle ASM 驱动程序，3-27
- My Oracle Support,5-1
- Oracle ASM 驱动程序
- 如何配置，3-27
- Oracle base
- 网络配置助手 (NetCA)
- 不允许在 grid homes 下，2-74
- 响应文件，B-5
- Oracle base 目录
- 在命令行提示符运行，B-5
- 关于，D-3
- `netca.rsp` 文件，B-3
- Oracle base，2-13
- 最小磁盘空间，2-25
- 网络信息服务
- Oracle Berkeley DB
- 限制，4-11
- NIS
- Oracle 集群注册
- 新功能，xv
- 配置，4-5
- NFS，3-12
- 镜像，3-8
- 以及数据，3-11
- 分区，3-8
- 以及 Oracle 集群文件，3-7
- 块大小参数，3-12, 3-13
- `parties`，3-32
- 直接 NFS，3-9
- 支持的存储选项，3-6
- 对于数据文件，3-11
- Oracle 集群
- `rsize`，3-12
- 以及系统，3-6
- 升级 Oracle ASM 实例，1-6
- 滚动升级，4
- 替代本地用户和组，2-16
- 支持的存储选项，3-6
- 非交互模式
- 查找命令，A-12
- 升级，3-8
- NTP 协议
- ASM 磁盘空间要求，3-20
- 以及 sweeping，2-62
- Oracle 集群安装指南
- 由 Oracle Grid Installation-Guide，4
- 在 Linux 上检查，2-60
- Oracle 数据库
- 检查版本，2-43, 2-54
- 创建数据文件，3-16, 3-17
- 对于 Linux，2-60
- 操作系统要求，3-39, 4
- 特权用户组，2-17
- 状态，2-60
- 与 ASM 的要求，3-20
- 数据库配置助手
- 关于，D-1
- 响应文件，B-5
- 以及 Oracle.loc，2-21
- 检查，2-21
- Oracle 磁盘管理器
- 检查，2-21
- 以及直接 NFS，3-14
- Oracle 企业级管理器
- 补丁，B-7
- Oracle Grid Infrastructure 响应，B-3
- 操作系统主，2-12
- 检查发行版和版本，2-60
- ASCII 路径，4
- 不同的集群成员，2-38, 3-17
- ACFS 限制，D-6
- Oracle 存储库，A-9
- 要求，2-37
- 检查，2-11
- 补丁更新，5-1
- Oracle 重装 RPM，xx
- 包含 Linux，2-4, 2-5
- 安装，2-5
- 故障排除，2-5
- 实时应用程序集群
- 配置系统要求，3-39, 4
- Oracle 用户
- 配置，2-69
- `ORACLE_BASE` 环境变量：从启动项，2-70
- `ORACLE_HOME` 环境变量：从启动项，2-70
- `ORACLE_SID` 环境变量：从启动项，2-70
- `oracleasm` RPM-安装，3-26
- `oracle-dbms-server` rpm，2-4
- `oracle-validated.rpm`,2-4
- `oracl.loc` 和中央库存，2-11
- 内容，2-11
- `oracl.loc` 文件位置，2-11
- 之，2-16
- `oralinventory.` 参见 Oracle 存储组
- OSAM 组，2-17
- 关于，2-17
- 以及多个数据库，2-18
- 以及 SYSASM，2-18
- 创建，2-19
- OSDB for ASM 组，2-18
- 关于，2-17
- OSDB 组和 SYSASM 权限，2-17
- 创建，2-18
- 在其他节点上，2-21
- 描述，2-17
- OSDB 组用于 ASM-创建，2-19
- OSOPER 组用于 ASM-关于，2-17
- 创建，2-19
- OSOPER 组和 SYSOPER 权限，2-17
- 创建，2-19
- 在其他节点上，2-21
- 描述，2-17

# P

- 包 `cvudsk` 未安装，2-62
- 包
- 检查，2-60
- 默认 Linux 安装，以及2-38
- 包。参见 RPMs
- PAM, 2-41
- 分区
- 与 ASM 使用，3-19
- 传递命令，2-22
- 补丁更新
- 下载，5-1
- 安装，5-1
- My Oracle Support，5-1
- 数据目录权限，3-17
- 物理 RAM 要求，2-24
- `ping` 命令，A-12
- 策略管理数据库和 SCANS，D-5
- 安装后
- 补丁下载并安装，5-1
- `root.sh` 回滚，5-2
- 预配置数据库
- ASM 磁盘空间要求，3-20
- 使用 ASM 的要求，3-20
- 特权组
- 对于 Oracle Database，2-17
- 处理器
- 检查系统架构，2-27
- `/proc/sys/fs/aio-max`，E-6
- `/proc/sys/fs/file-max` file，E-6



- `/proc/sys/fs/kernel/sem` file, E-6

- `/proc/sys/fs/kernel/shm`, E-6

- `/proc/sys/fs/kernel/shm` file, E-6

`/proc/sys/kernel/shmaxx`, E-6

`/proc/sys/kernel/shmn`, E-6

`/proc/sys/net/core/rmem_default`, E-6

`/proc/sys/net/core/rmem_max`, E-6

`/proc/sys/net/core/wmem_max`, E-6

`/proc/sys/net/ipv4/ip_local_port_range`, E-6

`profile.file`, 2-70

- 在命令行中传递值, B-1

- 使用 Oracle 安装程序指定, B-5

- 响应文件。另见静默模式

- `rmem_default`, E-6

- `rmem_max`, E-6

- 滚动升级

- ASM, 4-2

- ASM 的, 4-8

- Oracle Clusterware, 4-2

- root 用户

- 以 root 登录, 2-9

- `root.sh`, 4-7

- 备份, 5-2

- 运行, 4-3, A-14

- RPMs

- 检查, 2-60

- 默认 Linux 实例和, 2-38

- `sizeize` 参数, 3-12

- 运行级别, 2-25

`PRVF-5436` 错误, 2-62

# R

RAC

- 为 Linux 上的 ASM 配置磁盘, 3-39

- RAID

- 以及镜像 Oracle 集群注册表投票盘, 3-8

- 推荐的 ASM 冗余级别, 3-19

- RAID 磁盘设备名称, 3-28

- RAM 需求, 2-24

- 值和升级, 3-4, 3-37

- 支持, 3-37

- 升级现有分区, 3-8

- 原始设备存放

- 恢复文件

- 支持的存储, 3-6

- - Red Hat

- 操作系统, 2-38, 2-44

- - Red Hat 包管理器 (RPM)

SRP

- 预配置数据库的冗余级别和空间空间需求, 3-20

- 冗余交互式用法, 2-28

- 链接 Oracle Grid Infrastructure 目录二进制文件, 5, 63-4

- 需求, 3-20

- 硬件, 2-24

- `resolv.conf`, A-12

- 响应安装准备, B-2

- 响应, B-2

- 模板, B-2

- 静默模式, B-5

- 响应文件

- 关于, B-1

- 使用原因, B-2

- 另见静默响应文件, B-1

- 响应文件

- 关于, B-1

- 使用模板创建, B-3

- `dbca.rsp`, B-3

- 企业级, B-2

- 一般步骤, B-2

- `grid_install.rsp`, B-3

- 网络配置助手 (NetCA), B-5

- `netca.rsp`, B-3

# S

- SCAN 分析, 4-3, A-12

- SCAN 监听器, A-12, D-5

- SCANS, 2-31

- 理解, D-4

- 策略管理数据库需要使用 SCAN, D-5

- 脚本

- `root.sh`, 4-3

- SCSI 磁盘设备名称, 3-28

- 安装程序配置的安全 shell (SSH), 2-68

- 安全

- 分配 Oracle 软件的所有权, 2-15

- 用户身份验证, 4-21, 5-22

- `sem` 文件, E-6

- `sem` 参数

- Linux 上的推荐值, E-6

- `semms` 参数

- Linux 上的推荐值, E-6

- `semctl` 参数

- `semop` 参数

- Linux 上的推荐值, E-6

- 设置 shell 限制, 7-72

- shell

- 确定 用户的默认 shell, 2-70

- `SHELL` 环境变量

- 检查值, 2-70

- 限制

- 在 Linux 上设置, 2-72

- shell 启动文件编辑, 2-70

- 移除环境变量, 2-70

- 小的, E-6

- `shmaxx`, E-6

- `shmmn`, E-6

- 静默模式

Index-7

- 关于, B-1

- 使用原因, B-2

- 另见响应文件, E-1

- 静默模式安装, B-1

- 客户端访问名称, 查看 Scan

- 软件需求, 2-27

- 检查软件需求, 2-59

- 转发, 2-72

- OUI 自动配置, 2-68

- 配置, E-1

- 支持的版本, E-1

- 使用时, 2-68

- shell 启动文件, 2-70

- 存储

- 标记 ASM 候选, 4-8

- Oracle Clusterware, 3-6

- 防止安装选项, 2-73

- 使用原因, B-2

- SUSE

- 操作系统, 2-38, 2-44

- 需求, 2-24

- SYSASM, 以及 OASAM, 2-17

- 弃弃, 2-18

- 在 ASM 上使用

- SYSDBA 权限

- 关联组, 2-17

- SYSOP 权限

- 关联组, 2-17

- 系统架构

- 禁用, C-2

- 故障排除, 6-1

- `asmd` 命令和 `oracle` 目录, 2-12

- OUI 自动配置, 2-69

- DBFS 不识别 ASM 大小

- 无法创建磁盘组, 5-55

- 配置 Oracle Clusterware 的原因

- 不同组和用户 ID, 2-55

- 磁盘错误, 4-4

- DISPLAY 错误, 2-72

- 环境路径, 2-26

- 错误消息, A-1

- 身份验证之前的超时, A-5

- 日志中的字符串, 2-73

- 间性挂起, 4-12

- 日志文件, 4-7

- 缺失操作系统包, A-9

- m, 2-36

- 安装期间权限, D-2

- 公共网络过滤器, 2-36

- `root.sh` 错误, 6-4

- 运行级别, 2-25

- `sqlplus` 错误和 `oracle` 目录, 2-12

- `sh`, E-2

- `ssh` 配置失败, E-2

- `ssh` 错误, 73

- SSH 超时, A-5

- `stty` 错误, 2-73

- 无法清除设备, A-13

- 无法找到磁盘, A-13

- 无法打开 ASMLib, L-13

- 未解释的安装错误, 4-5, A-10

- 用户权限, A-7, E-2

- 用户 ID 不同导致权限错误, 2-14, 20

- 用户权限错误, 12

- 使用 `dd` 命令备份投票盘, xi

- X 转发错误, 2-73

# T

- `tcs` shell 限制, 2-72

- `TEMP` 环境变量, 2-27

- 临时目录, 2-26

- 查看 `/tmp` 目录

- 临时磁盘空间检查, 2-26

- 释放空间, 2-24

- 释放, 226

- 需求, 2-24

- 终端输出命令

- Oracle 安装帐户的抑制, 2-73

- `/tmp` 目录空间检查, 2-26

- 释放空间, 2-26

- `TMPDIR` 环境变量, 2-27

- 设置, 71

- Transparent HugePages

# U

- 识别现有 `uid`, 2-21

- 指定, 2-21

- 在其他节点上指定, 2-21

- `umask` 命令, 2-69, 71

- Linux 扩展内核 (UEK)

- 关于, 2-3

- 以及 `rp` 过滤器设置, 2-36

- 支持的发行版, 2-44

- 不可能的 Linux 内核。查看 Linux 扩展内核。

- 卸载, 6-1

- 卸载, 6-1

`upgrade`

Index-8

- Oracle Clusterware, 4-2

- 限制, F-2

- 取消环境变量, F-5

- 升级, 2-7

- 以及 SCANs, D-5

- Oracle ASM, F-8

- 使用原始或块设备, 3-4

- 升级现有 Oracle ASM 实例, 1-6

- 以及 OCR 分区, 3-8

- 以及投票盘分区, 3-8

- 将共享 Oracle Clusterware 到本地 `grid` 目录, 2-74

- 用户等效, A-7

- 用户等效错误组和用户, 2-14, 20

- 用户 ID 识别, 2-21

- 指定, 2-21

- 在其他节点上指定, 2-21

- `useradd` 命令, 2-13, 20, 2-22

- 在其他节点上创建相同的用户, 2-21

- 创建 `grid` 用户, 2-12

- 创建 `oracle` 用户, 2-13, 2-19, 2-20

- `oracle` 软件所有者 (`oracle`), 2-16

- 设置 shell 限制, 2-72

- 在 Linux 上设置用户的 shell 限制, 2-72

- 创建时指定组, 2-21

- 使用 NIS, 2-16, 3-21

- X 系统启用远程主机, 2-9

- X11 转发错误, 2-72

- X11 转发错误, E-5



# V

- `xhost` host 命令, 2-10
- 防止安装错误的标题抑制, 2-73
- SCAN 的 VIP, A-12
- 使用 `dd` 命令备份投票盘已弃用, xi
- 配置, 4-5
- 镜像, 3-8
- 分区大小, 3-8
- 支持的存储选项, 3-6

# W

- `wmem_default`, E-6
- `wmem_max`, E-6
- 工作站安装, 2-9
- `wsize` 参数, 3-12
- `wtmax`, 3-10
- Direct NFS 的最小值, 3-10

# X

- X 模拟器安装, 2-10
- X 终端安装, 2-10
- X Window 系统启用远程主机, 2-10
