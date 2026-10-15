

# Linux我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。和 UNIX 的 Oracle Real Application Clusters 安装指南

## 1 预安装清单

### 1.1 开始之前：规划您的安装

- 1.1.1 检查 My Oracle Support
- 1.1.2 考虑使用软件更新选项
- 1.1.3 检查 Oracle 技术网络
- 1.1.4 查看 Oracle RAC 的安装步骤
- 1.1.5 查看如何使用集群验证实用程序 (CVU)
- 1.1.6 查看并备份现有的 Oracle 安装
- 1.1.7 查看全球化要求
- 1.1.8 查看文档

### 1.2 服务器硬件、网络和操作系统概述

- 1.2.1 查看服务器硬件和软件要求
- 1.2.2 服务器环境配置概述
- 1.2.3 Oracle 基目录概述
- 1.2.4 网络连接要求概述
- 1.2.5 安全外壳 (SSH) 配置概述
- 1.2.6 浏览器要求概述
- 1.2.7 特定于平台的服务器配置概述

### 1.3 Oracle RAC 存储概述

- 1.3.1 在何处查看存储系统要求
- 1.3.2 Oracle 自动存储管理集群文件系统概述

*《适用于 Linux 和 UNIX 的 Oracle Real Application Clusters 安装指南》*介绍了如何安装和配置 Oracle Real Application Clusters（Oracle RAC）。在使用本指南之前，您必须首先完成 Oracle Clusterware 的安装，如适用于您平台的 *《Oracle Grid Infrastructure 安装指南》* 中所述。

### 目标受众

*《适用于 Linux 和 UNIX 的 Oracle Real Application Clusters 安装指南》*为安装和配置 Oracle RAC 的数据库管理员（DBA）提供数据库安装信息。

### 文档可访问性

有关 Oracle 对可访问性的承诺的信息，请访问 Oracle 可访问性计划网站：`http://www.oracle.com/pls/topic/lookup?ctx=acc&id=docacc`。

### 访问 Oracle 支持

Oracle 客户可以通过 My Oracle Support 获得电子支持。有关信息，请访问 `http://www.oracle.com/pls/topic/lookup?ctx=acc&id=info`，如果您有听力障碍，请访问 `http://www.oracle.com/pls/topic/lookup?ctx=acc&id=trs`。

### 相关文档

有关更多信息，请参阅以下 Oracle 资源：

#### Oracle Real Application Clusters 文档

大多数 Oracle 错误消息文档仅以 HTML 格式提供。如果您只能访问 Oracle 文档介质，请按范围浏览错误消息。找到范围后，使用浏览器的"在页面中查找"功能来定位特定消息。连接到 Internet 时，您可以使用 Oracle 在线文档的错误消息搜索功能搜索特定错误消息。

##### 安装指南

- Oracle Diagnostics Pack 安装指南
- 适用于您平台的 Oracle Grid Infrastructure 安装指南

##### 特定于操作系统的管理指南

- Oracle Clusterware 管理与部署指南
- Oracle 数据库管理员参考，适用于 UNIX 系统的 11g 第 2 版 (11.2)
- 适用于 Microsoft Windows 的 Oracle 数据库平台指南

##### Oracle 数据库 11g 第 2 版 (11.2) 真实应用集群管理

- Oracle 真实应用集群管理与部署指南
- Oracle 数据库 2 天 DBA 在线帮助
- Oracle 企业管理器真实应用集群指南在线帮助
- Oracle 诊断包入门指南

#### 通用文档

- Oracle 数据库新增功能指南
- Oracle 数据库网络服务管理员指南
- Oracle 数据库概念
- Oracle 数据库参考

印刷版文档可在 Oracle Store 通过以下网站购买：

`https://shop.oracle.com`

要下载免费的发行说明、安装文档、白皮书或其他资料，请访问 Oracle 技术网络 (OTN)。使用 OTN 前必须在线注册；注册是免费的，可以在以下网站进行：

`http://www.oracle.com/technetwork/index.html`

如果您已有 OTN 的用户名和密码，则可以直接访问 OTN 网站的文档部分：

`http://www.oracle.com/technetwork/indexes/documentation/index.html`

Oracle 错误消息文档仅提供 HTML 格式。您可以在安装介质的文档目录中按范围浏览错误消息。找到范围后，请使用浏览器的搜索功能定位特定消息。连接到互联网时，您可以使用 Oracle 在线文档的错误消息搜索功能搜索特定的错误消息。

### 约定

本文档中使用了以下文本约定：

| 约定 | 含义 |
|---|---|
| **粗体** | 粗体表示与操作相关的图形用户界面元素，或在文本或术语表中定义的术语。 |
| *斜体* | 斜体表示书名、强调或需要您提供特定值的占位符变量。 |
| `等宽` | 等宽表示段落中的命令、URL、示例中的代码、屏幕上出现的文本或您输入的文本。 |

## Oracle 真实应用集群安装中的新增功能

本节描述了与 Oracle 真实应用集群 (Oracle RAC) 安装和配置相关的新功能。本节中的主题包括：

- [第 2 版 (11.2.0.4) 的新增功能](#)
- [第 2 版 (11.2.0.4) 中不再支持的选项](#)
- [第 2 版 (11.2.0.3) 的新增功能](#)
- [第 2 版 (11.2.0.2) 的新增功能](#)
- [第 2 版 (11.2) 的新增功能](#)
- [第 1 版 (11.1) 的新增功能](#)

### 第 2 版 (11.2.0.4) 的新增功能

以下是第 2 版 (11.2.0.4) 的新功能列表：

#### 集群和 Oracle RAC 诊断工具增强

从 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.4) 开始，跟踪文件分析器和收集器会随 Oracle Grid Infrastructure 安装自动安装。跟踪文件分析器和收集器是一个诊断收集工具，用于简化 Oracle Clusterware、Oracle Grid Infrastructure 和 Oracle RAC 系统上的诊断数据收集。

> **注意：** 跟踪文件分析器和收集器从 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.4) 开始可用。

**另请参阅：** *Oracle Clusterware 管理与部署指南*，了解有关使用跟踪文件分析器和收集器的信息

#### Oracle 数据库健康检查和最佳实践建议

Oracle RAC 配置审计工具 (RACcheck) 随 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.4) 提供，用于评估单实例和 Oracle RAC 数据库安装中的已知配置问题、最佳实践、定期健康检查以及升级前后的最佳实践。

> **注意：** Oracle RAC 配置审计工具从 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.4) 开始可用。

> **另请参阅：** *Oracle 真实应用集群管理与部署指南*

### 第 2 版 (11.2.0.4) 中不再支持的选项

以下功能在 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.4) 中不再受支持：

**OUI 不再支持块和原始设备**

从此版本开始，OUI 不再支持在块或原始设备上安装 Oracle Clusterware 文件。请将 Oracle Clusterware 文件安装在 Oracle 自动存储管理磁盘组上，或在受支持的共享文件系统上。

**弃用 `-cleanupOBase`**

在此版本中，卸载工具的 `-cleanupOBase` 标志已弃用。此标志没有替代项。

### 第 2 版 (11.2.0.3) 的新增功能

从 Oracle 数据库 11g 第 2 版 (11.2.0.3) 开始，您可以在提供软件更新下载详细信息时输入代理域信息。代理域标识用于身份验证的安全数据库。如果您没有代理域，则无需为代理用户名、代理密码和代理域字段提供条目。此信息区分大小写。

此代理域仅用于软件更新下载。

### 第 2 版 (11.2.0.2) 的新增功能

以下是第 2 版 (11.2.0.2) 的新功能列表：

**增强的补丁集安装**

从 Oracle 数据库 11g 第 2 版的 11.2.0.2 补丁集发布开始，Oracle 数据库补丁集是 Oracle 数据库软件的完整安装。请注意新补丁集打包带来的以下变化：

- 支持从以前的版本 (11.x, 10.x) 直接升级到最新的补丁集。
- 建议的最佳实践是进行异地补丁集升级，即在新的、单独的 Oracle 主目录中安装补丁集。支持就地升级，但不推荐。
- 新安装包括安装最新的补丁集，而不是先安装基础版本然后再升级到补丁版本。

> **另请参阅：** My Oracle Support 说明 1189783.1，"从 11.2.0.2 开始的 Oracle 数据库补丁集重要更改"，可从以下 URL 获取：

`https://support.oracle.com`

#### 新增软件更新选项

使用软件更新功能，在 Oracle 数据库安装过程中动态下载并应用软件更新。您也可以使用 `downloadUpdates` 选项单独下载更新，然后在安装过程中通过提供更新所在的位置来应用它们。

#### Oracle 真实应用集群单节点 (Oracle RAC One Node)

Oracle RAC One Node 是在集群的一个节点上运行的 Oracle RAC 的单个实例。您可以使用 Oracle RAC One Node 将许多数据库整合到单个集群上，开销极小，同时仍提供故障转移保护、在线滚动补丁应用以及操作系统和 Oracle Clusterware 的滚动升级等高可用性优势。使用 Oracle RAC One Node，您可以标准化整个企业中的所有 Oracle 数据库部署。

您可以使用 Oracle 数据库和 Oracle Grid Infrastructure 配置助手，例如 Oracle 数据库配置助手 (DBCA) 和 RCONFIG 来配置 Oracle RAC One Node 数据库。

Oracle RAC One Node 是一个 Oracle RAC 数据库实例。您可以使用计划内的在线迁移在新目标节点上临时启动第二个 Oracle RAC One Node 实例，以便将当前 Oracle RAC One Node 实例迁移到这个新的目标节点。迁移后，源节点实例将被关闭。如果当前节点发生故障，Oracle RAC One Node 数据库也可以故障转移到其托管服务器池中的另一个集群节点。

如果您使用第三方集群软件，例如 Veritas、SFRAC、IBMPowerHA 或 HP Serviceguard，则不支持 Oracle RAC One Node。目前不支持 Sun Solaris 集群。

从 Oracle 数据库第 2 版 (11.2.0.2) 开始，Oracle RAC One Node 在所有经过 Oracle 真实应用集群 (Oracle RAC) 认证的平台上均受支持。

#### 冗余互连使用

在以前的版本中，要利用冗余网络进行互连，需要使用绑定、中继、组合或类似技术。Oracle Grid Infrastructure 和 Oracle RAC 现在可以利用冗余网络互连，而无需使用其他网络技术，从而增强集群中的最佳通信。此功能从 Oracle 数据库 11g 第 2 版 (11.2.0.2) 开始提供。

冗余互连使用支持跨多个（最多四个）专用网络（也称为互连）的负载平衡和高可用性。

### 第 2 版 (11.2) 的新增功能

以下是第 2 版 (11.2) 的新功能列表：

#### Oracle 自动存储管理和 Oracle Clusterware 安装

从 Oracle Clusterware 11g 第 2 版 (11.2) 开始，Oracle 自动存储管理 (Oracle ASM) 是 Oracle Grid Infrastructure 安装的一部分。在 Oracle Clusterware 和 Oracle RAC 安装中，Oracle ASM 安装在 Oracle Clusterware 主目录中。此外，可以将 Oracle ASM 配置为需要单独的管理权限，因此 OSDBA 组的成员可能不再提供对数据库和存储层的管理员访问权限。

#### Oracle 自动存储管理集群文件系统 (ACFS)

Oracle 自动存储管理集群文件系统（Oracle ACFS）是一种全新的跨平台、可扩展的文件系统与存储管理设计，它将 Oracle 自动存储管理（Oracle ASM）技术扩展到支持所有应用数据。Oracle ACFS 提供动态的文件系统大小调整功能，并利用跨所有可用存储的分发、平衡和条带化技术来提升性能，同时通过 Oracle ASM 的镜像和奇偶校验保护机制确保存储可靠性。

Oracle ACFS 适用于 Linux。在本版本发布时，尚不支持 UNIX 平台。

#### 集群验证实用程序修复脚本与网格基础架构检查

集群验证实用程序（CVU）具有以下新功能：

- CVU 可以生成 shell 脚本（修复脚本），这些脚本执行成功安装所需的系统配置，此外还能识别可能导致安装失败的系统问题。
- CVU 提供了额外的检查，以解决安装、配置和操作方面的问题。
- CVU 由 OUI 自动调用以验证先决条件，并会提示您创建修复脚本，以纠正许多阻碍安装的系统配置问题。

#### 数据库代理与监听程序

DBCA 不再为 `LOCAL_LISTENER` 设置值。当 Oracle Clusterware 启动数据库资源时，它会更新实例参数。`LOCAL_LISTENER` 被设置为本地节点监听程序地址的虚拟 IP 端点。您不应修改 `LOCAL_LISTENER` 的设置。新安装的实例仅将自身注册为使用单一客户端访问名称（SCAN）监听程序作为远程监听程序。SCAN 是分配给集群而非单个节点的虚拟 IP 地址，因此可以在不要求更新由集群服务的客户端的情况下添加或删除集群成员。升级后的数据库将继续注册到所有节点监听程序，并另外注册到 SCAN 监听程序。

#### 带时区数据类型的时间戳的夏令时升级

当由于夏令时变更而更新时区版本文件时，带时区的时间戳（TIMESTAMP WITH TIMEZONE，TSTZ）数据可能会变得过时。在之前的版本中，数据库管理员需要运行 SQL 脚本 `utltzuv2.sql` 来检测受时区版本变更影响的 TSTZ 数据，然后必须执行大量手动过程来更新 TSTZ 数据。

使用新提供的 `DBMS_DST` PL/SQL 包，TSTZ 数据的更新是透明的，只需极少的手动操作。此外，客户端不再需要修补其时区数据文件。

> **另请参阅：** *Oracle Database Upgrade Guide* 以获取有关准备升级带时区时间戳数据的信息，*Oracle Database Globalization Support Guide* 以获取有关如何升级时区文件和带时区时间戳数据的信息，以及 *Oracle Call Interface Programmer's Guide* 以获取有关客户端和服务器使用不同版本时区文件操作的性能影响的信息。

#### 企业管理器数据库控制配置

Database Control 11g 提供了在新节点上自动配置 Oracle Clusterware 和 Oracle RAC 安装，然后将现有的 Oracle Clusterware 和 Oracle RAC 数据库扩展到这些已配置节点的功能。此配置过程要求先成功安装 Oracle RAC，然后才能使用此功能。

> **另请参阅：** *Oracle Real Application Clusters Administration and Deployment Guide* 以获取有关此功能的信息。

#### 企业管理器集群件资源管理

您可以使用 Enterprise Manager Cluster 主页对高可用应用程序和 Oracle Clusterware 资源管理执行全面的管理和监控支持。这些管理任务包括创建和修改服务器池。

#### 网格即插即用

过去，在集群中添加或移除服务器需要大量的手动准备工作。网格即插即用通过使用集群内的网格命名服务，使每个节点能够动态执行以下任务，从而降低了安装、配置和管理服务器节点的成本：

- 为自己协商合适的网络标识
- 从配置文件获取其运行所需的附加信息
- 使用配置文件数据配置或重新配置自己，使主机名和地址在网络上可解析

由于服务器动态执行这些任务，添加和移除节点只需管理员将服务器连接到集群，并启用集群来配置节点。使用网格即插即用和最佳实践建议，将节点添加到数据库集群是正常服务器重启的一部分，而当服务器关闭时，从集群中移除节点会自动发生。

#### 改进的部署、反配置和卸载

Oracle 配置助手提供了额外的指导，以确保推荐的部署并防止配置问题。此外，配置助手会验证配置，并提供修复问题的脚本，您可以选择使用或拒绝。如果您接受修复脚本，则配置问题将自动得到修复。

Oracle 配置助手提供了反配置和卸载 Oracle Real Application Clusters 的功能，而无需额外的步骤。

#### 用于简化客户端访问的 SCAN 地址




单一客户端访问名称（SCAN）我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。提供给所有连接到集群的客户端的地址。SCAN 是在域名服务（DNS）或网格命名服务（GNS）中注册到三个 IP 地址的域名。当向集群添加或从中移除节点时，SCAN 无需更改客户端。使用 SCAN 的客户端也可以使用轻松连接来访问集群。

## Oracle RAC 零停机补丁

Opatch 现在可以以多节点、多补丁的方式应用补丁，并且如果数据库的其他实例未应用该补丁，则不会启动已应用非滚动补丁的实例。Opatch 还会检测数据库架构的补丁级别是否低于新补丁，并运行 SQL 命令将架构升级到新的补丁级别。

> **另请参阅：** *Oracle Universal Installer and OPatch User's Guide for Windows and UNIX*。

## Oracle RAC 11g 第 2 版 (11.2) 中已弃用的选项

请注意本版本的以下变更：

- 在安装过程中，将文件安装在原始设备上不再是可选项。您必须使用共享文件系统，或使用 Oracle 自动存储管理。如果您从早期版本升级且当前使用原始设备，则您现有的原始设备可以继续使用。升级完成后，如果您选择，可以迁移到 Oracle ASM 或共享文件系统。

- 除非数据库的操作系统 OSDBA 组与指定为 Oracle 自动存储管理的 OSASM 组是同一个组，否则本版本将移除充当 Oracle ASM 实例管理员的 SYSDBA 权限。

- 如果启用了单独的 Oracle ASM 访问权限，且数据库管理员不是 OSASM 组的成员，则数据库管理员必须是 Oracle ASM 的 OSDBA 组成员才能访问 Oracle ASM 文件。您可以将 Oracle RAC 数据库的 OSDBA 组指定为 Oracle ASM 实例的 OSDBA 组。

## 第 1 版 (11.1) 的新功能

以下是 Oracle RAC 11g 第 1 版 (11.1) 的新功能列表：

> **注意：** 此列表中的一些功能已被 11.2 版本中的更改所取代，特别是为 Oracle ASM 列出的那些功能。

### 安装文档中的变更

通过 Oracle Database 11g 第 1 版，Oracle Clusterware 可以作为独立产品进行安装或配置，并且提供了有关存储管理的额外文档。有关安装规划，请注意以下文档：

#### Oracle Database 2 Day + Real Application Clusters Guide

本书概述了安装和配置双节点 Oracle Clusterware 和 Oracle RAC 环境的过程，并提供了示例。

#### Oracle Grid Infrastructure Installation Guide

这本特定于平台的书籍提供了将 Oracle Clusterware 作为独立产品安装，或与 Oracle Database 或 Oracle RAC 一起安装 Oracle Clusterware 的过程。它包含需要系统管理员权限的系统配置说明。

#### Oracle 真应用集群安装指南

本书（即您正在阅读的指南）提供在成功完成 Oracle Clusterware 安装后安装 Oracle RAC 的操作流程。其中包含面向数据库管理员的数据库配置说明。

#### Oracle 数据库存储管理员指南

本书为负责管理和维护存储或配置和管理 Oracle 自动存储管理（Oracle ASM）的数据库与存储管理员提供相关信息。

#### Oracle Clusterware 管理和部署指南

这是 Oracle Clusterware 的管理员参考手册。其中包含有关管理任务的信息，包括涉及操作系统配置变更以及克隆 Oracle Clusterware 的任务。

#### Oracle 真应用集群管理和部署指南

这是 Oracle RAC 的管理员参考手册。其中包含有关管理任务的信息。这些任务包括数据库克隆、节点的添加和删除、Oracle Cluster Registry（OCR）管理、使用 SRVCTL 及其他数据库管理实用程序，以及操作系统配置的调优变更。

### 安装选项的变更

以下是 Oracle Database 11g 的安装选项变更：

- **Oracle Application Express：** 此功能随 Oracle Database 11g 一起安装。它之前名为 HTML DB，作为单独的 Companion CD 组件提供。

- **Oracle Configuration Manager：** Oracle Configuration Manager（OCM）已集成到 Oracle Universal Installer 中。但它对于数据库和客户端安装而言是一个可选组件。Oracle Configuration Manager 在之前的版本中称为 Customer Configuration Repository（CCR），是一款用于收集和存储与存储在 Oracle ASM 和数据库 Oracle 主目录中的软件配置相关详细信息的工具。

- **Oracle Data Mining：** 企业版安装类型默认选择 Oracle Database Mining 选项。在 Oracle Database 11g 中，当您选择 Create Database 选项时，数据挖掘元数据将与 SYS 元数据一起创建。

- **Oracle Database：** 此功能已集成到 Oracle Universal Installer 中。但它对于数据库安装而言是一个可选组件。

- **Oracle SQL Developer：** 此功能随基于模板的数据库安装（如通用用途、事务处理和数据仓库）默认安装。它也会随数据库客户端的管理员、运行时和高级安装一起安装。

- **Oracle Warehouse Builder：** 此信息集成工具现在随 Oracle Database 的标准版和企业版一起安装。使用企业版时，您可以购买额外的扩展流程。安装 Oracle Database 还会安装一个预置种子仓库 OWBSYS，这是使用 Oracle Warehouse Builder 所必需的。

- **Oracle Ultra Search：** 从 Oracle Database 11g 开始，Oracle Ultra Search 已集成到 Oracle Database 中。在之前的版本中，此产品作为 Companion CD 组件提供。

- **Oracle XML DB：** 从 Oracle Database 11g 开始，Oracle XML DB 不再是一个可选功能。它使用 Database Configuration Assistant 为所有数据库安装进行安装和配置。

#### 可安装的新组件

以下是安装 Oracle Database 11g 时可用的新组件：

- **Oracle Application Express：** 从 Oracle Database 11g 开始，HTML DB 不再作为 Companion CD 组件提供。该组件已更名为 Oracle Application Express，随 Oracle Database 11g 一起安装。

  在 Oracle Database 11g 中，Oracle Application Express 取代了 iSQL*Plus。

  另请参阅：*Oracle Application Express 用户指南*以获取有关 Oracle Application Express 的更多信息。

- **Oracle Configuration Manager：** 此功能在高级安装期间提供。它之前名为 Customer Configuration Repository（CCR）。它对于数据库和客户端安装而言是一个可选组件。Oracle Configuration Manager 收集和存储与存储在数据库 Oracle 主目录中的软件配置相关的详细信息。

- **Oracle Database Vault：** 此功能对于数据库安装而言是一个可选组件。

  另请参阅：*Oracle Database Vault 管理员指南*以获取有关 Oracle Database Vault 的更多信息。

- **Oracle Real Application Testing：** 此功能随 Oracle Database 11g 企业版安装类型默认安装。

  另请参阅：*Oracle Database Real Application Testing 用户指南*以获取有关 Oracle Real Application Testing 的更多信息。

- **Oracle SQL Developer：** 此功能随基于模板的数据库安装（如通用用途、事务处理和数据仓库）默认安装。它也会随数据库客户端的管理员、运行时和高级安装一起安装。

  另请参阅：*Oracle SQL Developer 用户指南*以获取有关 Oracle SQL Developer 的更多信息。

- **Oracle Warehouse Builder：** 此功能现在作为数据库安装中的一个选项包含在内。

  > **注意：** 使用 Oracle Database 11g 第 2 版（11.2）的标准版和企业版时，会安装具有基本功能的 Oracle Warehouse Builder。但是，使用企业版时，您可以购买扩展 Oracle Warehouse Builder 的选项。

  另请参阅：*Oracle Warehouse Builder 源和目标指南*以获取有关 Oracle Warehouse Builder 的更多信息。

#### 安装的增强功能和新特性

以下是 Oracle Database 11g 第 2 版（11.2）的增强功能和新特性列表：

#### 自动诊断存储库

自动诊断存储库是 Oracle Database 11g 中新增的一项功能。此功能的主要目标是减少解决缺陷所需的时间。自动诊断存储库是在 Oracle Database 11g 中实现的诊断框架层，用于存储诊断数据，同时还提供服务 API 以访问数据。存储诊断数据的默认目录为 `ORACLE_BASE/diag`。

自动诊断存储库实现以下功能：

- 所有 Oracle 产品的诊断数据都写入磁盘上的存储库。

- 提供便于浏览存储库以及读写数据的接口。

对于 Oracle RAC 安装，如果您使用共享的 Oracle Database 主目录，则自动诊断存储库必须位于所有节点均可访问的共享存储位置。

Oracle Clusterware 继续将诊断数据存储在 `Grid_home/log` 目录中，其中 `Grid_home` 为 Oracle Clusterware 主目录。

#### Oracle 自动存储管理快速镜像重新同步

Oracle ASM 快速镜像重新同步可在磁盘路径发生临时故障后，只要磁盘驱动器介质未损坏，就能快速重新同步磁盘组中的 Oracle ASM 磁盘。任何导致故障组暂时不可用的故障都被视为临时故障。磁盘路径故障（如电缆断开、主机总线适配器或控制器故障，或磁盘电源中断）都可能导致临时故障。快速镜像重新同步的持续时间取决于中断的持续时间。重新同步所需的时间通常远少于完全重建整个 Oracle ASM 磁盘组所需的时间。

另请参阅：*Oracle 自动存储管理管理员指南*。

#### Oracle ASM、卸载及其他配置助手增强功能

ASM 配置助手（ASMCA）是一种新的配置工具，可从 Oracle Grid Infrastructure 集群主目录运行。ASMCA 用于配置 ASM 实例、磁盘组、卷和文件系统。ASMCA 在安装过程中运行，也可以像 DBCA 一样用作管理配置工具。

数据库配置助手（DBCA）、数据库升级助手（DBUA）和 Oracle Net 配置助手（NETCA）已得到改进。这些改进包括以下内容：

#### 用于 Oracle ASM 管理的新 SYSASM 权限和 OSASM 组

此功能引入了一个新的 `SYSASM` 权限，专门用于执行 Oracle ASM 管理任务。使用 `SYSASM` 权限代替 `SYSDBA` 权限，可以更清晰地区分 Oracle ASM 管理和数据库管理之间的职责。

OSASM 是一个专门用于 Oracle ASM 的新操作系统组。OSASM 组的成员可以使用操作系统认证以 SYSASM 身份连接，并拥有对 Oracle ASM 的完全访问权限。

#### Oracle ASM 首选读取磁盘组

在以前的版本中，Oracle ASM 使用镜像区段的主副本所在的磁盘作为数据读取的首选磁盘。在此版本中，使用新的初始化文件参数 `asm_preferred_read_failure_groups`，您可以指定位于特定集群节点附近的磁盘作为该节点获取镜像数据的首选磁盘。此选项在数据库配置助手（DBCA）中提供，可以在安装后配置。这一更改有助于更快地处理具有广泛分布的共享存储系统或扩展集群（节点地理分散的集群）的数据，并提高灾难恢复准备能力。

#### Oracle 自动存储管理滚动迁移

Oracle ASM 的滚动迁移使您能够在不影响数据库可用性的情况下，升级或修补集群 Oracle ASM 节点上的 Oracle ASM 实例。滚动迁移提供了更高的可用性，以及更优雅的 Oracle ASM 软件从一个版本到下一个版本的迁移。此功能适用于运行在 Oracle Database 11g 第 1 版（11.1）及更高版本上的 Oracle ASM 配置。换句话说，您必须先安装 Oracle Database 11g 第 1 版（11.1），然后才能执行滚动迁移。

> **注意：** 在升级期间，您不能更改 Oracle ASM 或 Oracle Database 主目录的所有者。您必须使用与现有 Oracle ASM 或 Oracle Database 主目录相同的 Oracle 软件所有者。

**另请参阅：** *Oracle 自动存储管理管理员指南*

- 包含改进的升级前脚本，以提供空间估算、初始化参数、统计信息收集和新的警告。DBUA 还提供从 Oracle Database 9.0、9.2、10.1 和 10.2 版本的升级。

- Oracle Database 11g 第 11.2 版更新：还提供从 11.1 的升级。仅支持就地升级。

- 启动升级前运行的任何服务

**卸载工具** 包含一个卸载工具（`deinstall`），该工具在安装前可在安装介质中使用，安装后可在 Oracle 主目录中使用。它位于路径 `$ORACLE_HOME/deinstall` 中。该脚本停止 Oracle 软件，并删除操作系统上的 Oracle 软件和配置文件。

#### 数据挖掘模式创建选项

在 Oracle Database 11g 中，当您以 SYS 用户身份运行 SQL 脚本 `catproc.sql` 时，将创建数据挖掘模式。因此，数据挖掘选项已从数据库配置助手的数据库功能屏幕中移除。

#### Oracle 磁盘管理器网络文件系统管理

Oracle 磁盘管理器（ODM）可以自行管理网络文件系统（NFS），而无需使用操作系统内核 NFS 驱动程序。这称为 Direct NFS。Direct NFS 在 Oracle 数据库内核中实现 NFS 版本 3 协议。这一更改使得可以使用 ODM 接口监控 NFS 状态。Oracle 数据库内核驱动程序会自动调整以获得可用资源的最佳使用。

此功能提供以下优势：

- 通过提供 Oracle 内核对网络文件服务器输入输出路径的控制，简化调优和诊断，避免在操作系统级别调优网络性能的需要。

- 一个高度稳定、高度优化的数据库操作 NFS 客户端。

- 将 Oracle 网络文件系统层用于用户任务，将操作系统内核网络文件系统层保留用于网络通信。

- 使用 Oracle 缓冲区缓存而不是文件系统缓存，以简化调优。

- 一个通用的、一致的 NFS 接口，可在 Linux、UNIX 和 Windows 平台上使用。

- Oracle RAC 感知 NFS 性能。使用操作系统 NFS 驱动程序时，即使 NFS 是共享文件系统，也必须使用选项 `noac`（NO Attribute Caching，无属性缓存）挂载 NFS 驱动器，以防止操作系统 NFS 驱动程序通过本地存储文件属性来优化文件系统缓存。ODM NFS 自动识别 Oracle RAC 实例，并对数据文件执行适当的操作，无需用户、系统管理员或 DBA 进行额外的重新配置。如果您将 Oracle Clusterware 投票磁盘或 Oracle 集群注册表（OCR）文件存储在 NFS 上，则必须继续使用 `noac` 选项挂载投票磁盘。

#### 最优灵活架构（OFA）简化

随着 Stripe and Mirror Everything 架构（SAME）的发展，以及存储设备存储和吞吐能力的提高，原始 OFA 增强性能的使命已转变为其提供组织良好的 Oracle 安装的角色，将软件、配置文件和数据分离。这种分离增强了安全性，并简化了升级、克隆和其他管理任务。

Oracle Database 11g 第 2 版（11.2）对 OFA 进行了多项更改，以解决这一变化的目的。

作为此更改的一部分：

- 在 Oracle RAC 安装期间，系统会提示您接受默认值，或选择 Oracle 基目录的位置，而不是 Oracle 主目录的位置。此更改有助于在公共位置安装多个 Oracle 主目录，并分离软件单元以简化管理。

- 在此版本中，作为自动诊断资料库（ADR）实现的一部分，以下 `admin` 目录发生了更改：

- `bdump`（位置由 `background_dump_dest` 初始化参数设置；存储 Oracle 后台进程跟踪文件）

- `cdump`（位置由 `core_dump_dest` 初始化参数设置；存储 Oracle 核心转储文件）

- `udump`（位置由 `user_dump_dest` 初始化参数设置；存储 Oracle 用户 SQL 跟踪文件）

默认情况下，这些跟踪文件和核心文件的位置位于 `/diag` 目录中，该目录在路径 `$ORACLE_BASE/diag` 中。



# Oracle Database 11g Release 2 安装变更与预安装检查清单

## 安装变更概述

- 初始化参数`BACKGROUND_DUMP_DEST`和`USER_DUMP_DEST`已弃用。它们继续被设置，但您不应手动设置这些参数。

- 引入了一个新的初始化参数`DIAGNOSTIC_DEST`。它包含“ADR 基”的位置，即一个或多个自动数据库资料库主目录所在的基目录。Oracle 文档通常将这些主目录称为 ADR 主目录。每个数据库实例都有一个 ADR 主目录，它是许多其他目录的根目录，这些目录包含跟踪文件、警报日志、健康监视器报告和严重错误的转储。您还可以使用 SQL 语句`select name, value from v$diag_info`查看警报和跟踪文件。

- 默认快速恢复区（以前称为闪回恢复区）从`$ORACLE_HOME/.../recovery_area`移动到`$ORACLE_BASE/recovery_area`。

- 默认数据文件位置从`$ORACLE_HOME/.../oradata`移动到`$ORACLE_BASE/oradata`。

- 引入了一个新实用程序，即 ADR 命令解释器（`ADRCI`）。`ADRCI`便于查看警报日志和跟踪文件。

对于 Oracle RAC 安装，Oracle 要求快速恢复区和数据文件位置位于所有节点共享的位置。Oracle 通用安装程序在安装期间会确认这一点。

此更改不会影响 Oracle Clusterware 跟踪文件的位置。

> **另请参阅：** *Oracle 数据库管理员指南* 了解有关这些更改的详细信息，以及 *Oracle 数据库实用程序* 了解使用`ADRCI`查看警报日志和列出跟踪文件的信息

### Oracle 配置管理器以改进支持

在安装期间，系统会询问您是否要安装 Oracle 配置管理器（OCM）。OCM 是一个可选工具，使您能够将您的配置信息与您的 My Oracle Support 账户（以前的 OracleMetalink）关联。这可以通过确保服务器系统信息随时可用来促进服务请求的处理。

配置 OCM 工具需要您从服务协议中获取以下信息：

- My Oracle Support 电子邮件地址/用户名

- 密码

此外，如果主机系统没有直接连接到 Internet，系统会提示您输入服务器代理信息。

### 大数据文件支持

大数据文件支持是一项自动化功能，它使 Oracle 能够更高效地在 Oracle ASM 上支持更大的文件，并提高最大文件大小。

> **另请参见：** *《Oracle 自动存储管理管理员指南》*

### 将数据库从数据库控制切换到网格控制配置

在之前的发行版中，数据库配置助理包含在创建数据库时使用数据库控制或网格控制进行配置的功能，或者在创建后重新配置数据库的功能。但是，如果您想将配置从数据库控制更改为网格控制，这需要大量工作。使用 Oracle Database 11g，数据库配置助理允许您通过运行 Oracle 企业管理器配置插件，将数据库的配置从数据库控制切换到网格控制。

## Oracle Database 11g Release 1 (11.1) 中已弃用的组件

以下组件曾是 Oracle Database 10g release 2 (10.2) 的一部分，但在 Oracle Database 11g 中不可用于安装：

- `iSQL*Plus`

- Oracle Workflow

- Data Mining Scoring Engine

- Oracle Enterprise Manager Java console

## 预安装检查清单

大多数 Oracle Real Application Clusters (Oracle RAC) 安装错误是由于在启动 Oracle Universal Installer 之前未完成所有必需步骤造成的。本章旨在供数据库管理员在系统管理员和存储管理员的协助下使用，以协调安装工作并规划 Oracle Clusterware 的任务，为完成 Oracle RAC 的安装做好准备。本章包含以下主题：

- 开始之前：规划您的安装

- 服务器硬件、网络和操作系统概述

- Oracle RAC 存储概述

- 准备安装所需的附加信息

- 使用 CVU 确认集群已为 Oracle RAC 安装做好准备

- 为升级或共存数据库停止现有 Oracle 进程

### 1.1 开始之前：规划您的安装

本节提供了一个任务列表，Oracle 建议您在启动 Oracle Clusterware 和 Oracle RAC 安装之前完成这些任务。无论您的位置是拥有由系统管理员、存储管理员、网络管理员、数据库管理员以及第三方硬件和软件供应商组成的庞大项目团队的 Tier IV 数据中心，还是您是一个人的项目团队，规划对于确保安装顺利进行都很重要。本文档集不涉及如何确定安装的硬件规模或容量规划的建议。请注意，使用 Oracle Clusterware 和 Oracle RAC，您可以根据需要添加节点和实例，以应对测试或工作负载增加的情况。请查看并完成以下步骤作为安装计划的一部分：

- 检查 My Oracle Support

- 考虑使用软件更新选项

- 检查 Oracle 技术网络

- 查看 Oracle RAC 的安装步骤

- 查看如何使用集群验证实用程序 (CVU)

- 查看并备份现有 Oracle 安装

- [查看全球化要求](https://support.oracle.com)

- [查看文档](https://support.oracle.com)

#### 1.1.1 检查 My Oracle Support

在决定是在现有硬件上安装 Oracle Database 11g release 2 (11.2)，还是决定为安装购买哪些服务器和存储硬件之前，请登录 My Oracle Support：

`https://support.oracle.com`

点击 **Certify** 选项卡。检查您打算安装的操作系统平台的 Oracle RAC 认证矩阵，以确保您的硬件配置得到 Oracle Clusterware 和 Oracle RAC 的支持。您可以获得有关受支持硬件选项的指导，以帮助您做出购买决策。

要访问认证矩阵：

1. 登录 My Oracle Support。

2. 点击 **Certifications** 选项卡。

3. 提供有关您平台的信息以获取认证信息。

除了特定的认证硬件配置外，Certify 页面还提供支持和补丁信息，以及关于如何进行 Oracle Clusterware 或带有 Oracle RAC 11g release 2 (11.2) 的 Oracle Clusterware 安装的一般建议，包括有关供应商集群件和其他配置问题的重要信息。

如果您没有 My Oracle Support 帐户，请联系您的 Oracle 销售代表。

此外，您可能希望参考 Oracle.com (`http://www.oracle.com`) 获取有关特定实施场景规划、最佳实践以及可帮助您制定安装计划的其他信息的更多资源。特别要参考 Oracle 技术网络上的 Oracle Real Application Clusters 页面：

`http://www.oracle.com/technology/products/database/clustering/index.html`

Oracle RAC 技术认证矩阵提供了有关可用于部署 Oracle RAC 的受支持技术的详细信息。

#### 1.1.2 考虑使用软件更新选项

OUI 可以安装关键补丁更新、受支持操作系统的系统要求更新以及其他重要更新，这些更新可以确保您的安装成功。Oracle 建议您在安装期间启用软件更新选项。

如果您选择启用软件更新选项，则必须提供有效的 My Oracle Support 用户名和密码，以便 OUI 可以下载最新的更新，或者您必须提供先前下载的软件更新选项包的位置路径。

此外，如果您有代理域，则需要准备好提供目标代理域以及通过该域访问 Internet 所需的用户身份验证（用户名和密码），以便 OUI 可以获取软件更新。如果您没有此信息，请在安装前咨询您的网络管理员。

如果您计划在安全的数据中心运行安装，则可以通过在具有 Internet 访问权限的系统上启动 OUI 来下载更新，然后再开始安装。要启动 OUI 仅下载更新，请输入以下命令：

```
$ ./runInstaller -downloadUpdates
```

提供 My Oracle Support 用户名和密码，并在需要时提供代理设置。下载更新后，将更新文件传输到您计划运行安装的服务器上的目录。

#### 1.1.3 检查 Oracle 技术网络

Oracle 技术网络 (OTN) 包含有关部署选项、容量规划、各种 NFS 平台上的最佳实践以及扩展集群部署的白皮书，这些内容不在本指南中涉及。您可以在以下网站查看可用的论文：

[http://www.oracle.com/technology/products/database/clustering/index.html](http://www.oracle.com/technology/products/database/clustering/index.html)

#### 1.1.4 查看 Oracle RAC 的安装步骤

安装 Oracle RAC 包括以下步骤：

1. 准备服务器（系统、存储和网络管理）：

   - 安装操作系统，并将操作系统包和补丁安装到所需版本。

   - 创建所需的组、用户和软件主目录。

   - 如果您计划部署网格命名服务 (GNS)，请设置 GNS 的域名转发，并根据需要在 DNS 和服务器上设置网络地址。

   - 设置所需的存储。

   - （可选）将所有软件暂存到一个节点上进行安装（“本地节点”）。

> **注意：** 在 Oracle Grid Infrastructure 安装过程中，您可以选择多个互连用于专用网络。此功能称为冗余互连使用。

此功能从 Oracle Database 11g Release 2 (11.2.0.2) 开始可用。

使用冗余互连使用，Oracle Clusterware 可以定义多个接口用于集群互连网络，而无需使用 bonding 或其他技术。

当您定义多个互连时，无论是在安装访谈期间还是之后使用 Oracle 接口配置 (`OIFCFG`) 命令行实用程序，Oracle Clusterware 都会创建一到四个高可用性 IP (HAIP) 地址。Oracle RAC 和 Oracle ASM 实例使用这些互连地址来确保节点之间高可用、负载均衡的互连通信。

**另请参见：** *《Oracle Clusterware 管理和部署指南》* 以获取有关使用`OIFCFG`修改互连的更多信息

2. 安装 Oracle Grid Infrastructure for a cluster，包括 Oracle Clusterware 和 Oracle Automatic Storage Management（系统和存储管理）：

   - 安装 Oracle Grid Infrastructure for a cluster。安装期间，Fixup 脚本会对操作系统参数、用于安装和用户环境变量的安全外壳（SSH）执行额外的配置。

   - 将 Oracle Clusterware 和 Oracle Automatic Storage Management 打补丁至最新的补丁集。

3. 安装 Oracle RAC（数据库管理）：

   - 安装 Oracle Real Application Clusters。

   - 将 Oracle RAC 打补丁至最新的补丁集。

   - 完成 Oracle RAC 数据库的安装后配置。

#### 1.1.5 审查如何使用集群验证实用程序（CVU）

在安装 Oracle Clusterware 或 Oracle RAC 之前，使用 CVU 来确保您的集群已为安装做好准备。CVU 包含在 Oracle Universal Installer 中，因此当您启动 Oracle RAC 安装时，CVU 会运行。但是，您可以在开始 Oracle RAC 安装之前使用 CVU 来确保 Oracle RAC 所需的任何软件包或配置信息都已就位。

Oracle 提供 CVU 以在安装、补丁更新或其他系统更改之前执行系统检查。此外，CVU 可以生成 fixup 脚本，这些脚本由 root 用户运行，可以将许多内核参数更改为成功安装所需的最低设置。

使用 CVU 可以帮助系统管理员、存储管理员和数据库管理员确保每个人都已完成系统配置和预安装步骤，以便安装、更新或补丁成功完成。您可以在以下 URL 获取最新版本的 CVU：

`http://www.oracle.com/technology/products/database/clustering/cvu/cvu_download_homepage.html`

如果您有一个负责执行硬件或操作系统配置步骤的供应商，那么请供应商在完成其工作后完成集群的相关 CVU 检查，以确保您的系统配置正确。数据库管理员在启动 Oracle RAC 安装之前，应参考第 1-18 页的“使用 CVU 确认集群已为 Oracle RAC 安装做好准备”部分，以确认他们的系统已为安装做好准备。

#### 1.1.6 审查并备份现有的 Oracle 安装

如果您有现有的 Oracle 安装，请记录版本号、补丁和其他配置信息，并审查现有安装的升级过程。在继续安装之前，请先审查 Oracle 升级文档，以决定您希望如何进行。

Oracle RAC 11g 第 2 版 (11.2)，您的集群上必须已安装 Oracle Clusterware 和 Oracle ASM 11g 第 2 版 (11.2)。Oracle Clusterware 发行版版本必须等于或大于您要安装的 Oracle RAC 版本。

> 另请参阅：Oracle Grid Infrastructure 安装指南

有关升级前、升级后、兼容性和互操作性的最新更新和最佳实践，请参阅“Oracle Upgrade Companion”。

“Oracle Upgrade Companion”可通过 My Oracle Support 上的注释 785351.1 获取：

`https://support.oracle.com/`

关于升级，请注意以下几点：

- 您的集群上一次只能运行一个版本的 Oracle Clusterware。Oracle Clusterware 版本必须是集群上运行的任何软件（Oracle Clusterware、Oracle 数据库、Oracle RAC 和 Oracle Automatic Storage Management）中最新的发行版。

- 您可以在集群上拥有多个 Oracle 数据库的 Oracle 主目录。但是，这些主目录中的 Oracle RAC 数据库软件必须来自等于或早于所安装的 Oracle Clusterware 版本的版本；您不能在您正在运行的 Oracle Clusterware 版本之后发行的 Oracle 数据库版本上运行 Oracle Clusterware。

  例如：

  如果您将 Oracle Clusterware 11g 第 2 版作为集群件安装，那么您可以在一个节点上运行 Oracle Database 10g 第 1 版单实例数据库，并且在集群上也可以运行单独的 Oracle RAC 10g 第 1 版、第 2 版和 Oracle RAC 11g 第 1 版或第 2 版数据库。

  但是，您不能在集群上安装 Oracle Clusterware 10g 第 2 版，然后安装 Oracle RAC 11g。

- 从版本 10.1.0.6 和 10.2.0.3 开始，您可以使用数据库升级助手（DBUA）对 Oracle RAC 进行补丁集升级。您也可以使用 DBUA 在 Oracle RAC 的主要点版本之间进行升级（例如，从 10.1 到 10.2，或从 10.2 到 11g）。

- 在升级过程中，您无法更改 Oracle 数据库主目录的所有者。您必须使用与现有 Oracle 数据库主目录所有者相同的 Oracle 软件所有者。

- 与任何系统更改一样，在安装新软件之前，请备份您的现有数据库。

**另请参阅：** *《Oracle 数据库升级指南》*

#### 1.1.7 审查全球化要求

在您开始安装希望支持英语以外语言的安装之前，请审查 *《Oracle 数据库全球化支持指南》*。

请注意以下事项：

- Oracle 建议您使用 Unicode `AL32UTF8`作为数据库字符集。Unicode 是支持当前大多数口语的通用字符集。Unicode 还支持许多历史脚本（字母）。Unicode 是许多技术的本机编码，包括 Java、XML、XHTML、ECMAScript 和 LDAP。Unicode 非常适合支持互联网和全球经济的数据库。

- 操作系统会话的区域设置决定了用户界面的语言以及 Oracle Universal Installer、Oracle Net Configuration Assistant 和 Database Configuration Assistant 等组件的全球化行为。区域设置还决定了用户应用程序通过 Oracle JDBC 驱动程序创建的 Oracle 数据库会话的全球化行为，除非应用程序覆盖了该设置。

- `NLS_LANG`环境变量决定了 SQL\*Plus、exp 和 imp 等组件的用户界面语言和全球化行为。此变量还设置了客户端应用程序和数据库使用的语言和区域。该变量还声明了客户端应用程序输入和显示数据的字符集。

> **注意：** 您平台的《Oracle 数据库安装指南》更全面地讨论了与不同语言一起使用的数据库字符集，并提供了有关安装和配置 Oracle 数据库全球化支持的更多信息。

#### 1.1.8 审查文档

在安装 Oracle Clusterware 之前，请审查适用于您的操作系统平台的《Oracle Grid Infrastructure 安装指南》，特别是“安装前”和“存储”章节，以完成安装所需的所有必要步骤。

《Oracle Grid Infrastructure 安装指南》还包含大多数需要 root 权限或存储管理员权限的任务，这些任务需要在开始 Oracle RAC 安装之前完成。



此外，请审查发行版说明和 My Oracle Support (`https://support.oracle.com`)，以确保您拥有关于系统要求和其他可能影响您的安装的信息的最新信息。此次审查所花费的少量时间可以节省以后追踪安装错误原因所需的更大量时间。同时，请确保您拥有本文档的最新版本；Oracle 文档在发行后会进行更新。

Oracle 建议您在集群节点上安装 Web 浏览器，以便在安装 Oracle RAC 时启用 Oracle Enterprise Manager 和 Oracle Application Express，并根据需要访问在线文档。在线文档提供 PDF 和 HTML 格式。

> **注意：** 有关 Oracle 数据库的概述，请参阅《Oracle 数据库概念》，有关 Oracle Clusterware 或 Oracle RAC 配置和部署的更多信息，请参阅《Oracle Real Application Clusters 管理和部署指南》。您平台的《Oracle Grid Infrastructure 安装指南》包含有关 Oracle RAC 的服务器和存储配置信息。

## 1.2 服务器硬件、网络和操作系统概述

在尝试安装 Oracle RAC 之前，必须成功安装 Oracle Clusterware。为了成功完成安装，请确保 Oracle 软件所需的硬件、网络和操作系统预安装步骤已完成。未能完成所需的预安装步骤是安装失败最常见的原因。

在作为 Oracle Grid Infrastructure for a Cluster 安装的一部分安装 Oracle Clusterware 之前，您应该已经完成安装和配置 CPU、内存、共享存储、网卡、主机总线适配器、互联以及任何其他网络或服务器硬件。您还应该已经安装了操作系统及任何厂商集群软件。请查阅您的厂商文档以完成这些任务。若相关，请与您的厂商合作完成本文档中列出的 Oracle 预安装步骤，以确认厂商硬件和软件配置正确。

在 Oracle Grid Infrastructure for a Cluster 安装过程中，完成安装的人员需确定每个全局接口的计划用途，将每个接口标识为 **Public** 接口类型（用于公共 IP 地址和虚拟 IP 地址）、**Private** 接口类型（用于集群成员节点间的互连），或 **Do not use** 接口类型（Oracle Clusterware 和 Oracle RAC 应忽略）。例如，用作网络文件系统专用接口的接口应标记为 **Do not use** 接口类型。

Oracle RAC 配置过程中无需额外的网络配置。

安装的服务器和网络准备包括以下内容：

- 查看服务器硬件和软件要求
- 服务器环境配置概述
- Oracle Base 概述
- 网络连接要求概述
- 安全 Shell (SSH) 配置概述
- 浏览器要求概述
- 特定于平台的服务器配置概述

### 1.2.1 查看服务器硬件和软件要求

以下是服务器硬件和软件配置的摘要。

#### Oracle 要求

集群中的每个节点需要以下条件：

- 受支持的服务器硬件，包括处理器和系统配置。

  在现有硬件上开始安装之前以及购买新硬件之前，请查看 My Oracle Support，以确保该硬件受 Oracle Clusterware with Oracle RAC 11g release 2 (11.2) 支持。

  > **注意：** 集群中的每个节点必须使用相同的操作系统。此外，Oracle 强烈建议您在集群的每个节点上使用相同的软件配置。

- 系统要求中列出的操作系统软件包。

  不支持自定义操作系统软件包安装，因为它们可能不包含必需的软件包。您可以根据需要添加额外的软件包，但如果从默认软件包集中减少软件包，则可能会遇到所需的软件包出现 *failed dependencies*（依赖失败）错误。

- 每个节点上受支持的互连软件协议，以支持 Oracle Clusterware 表决磁盘轮询，并支持 Oracle RAC 的 Cache Fusion。

  您的互连 *必须* 经 Oracle 针对您的平台认证。

#### Oracle 建议：系统管理员任务

Oracle 建议采取以下措施以简化服务器安装和维护，并防止服务问题：

- 使用时间协议，确保集群中的所有节点使用相同的时间参考。使用 Oracle Clusterware 11g release 2 (11.2) 时，如果在安装时未启用网络时间协议，则 Oracle Clusterware 安装将启用集群时间同步服务。
- 为所有集群规模配置冗余交换机。
- 在每个节点上使用相同的服务器硬件，以简化服务器维护。

#### 附加选项：系统管理员和厂商

- 虽然您不需要将厂商集群软件与 Oracle Clusterware 一起使用，但 Oracle 支持使用许多厂商集群软件选项。但是，您必须安装 Oracle Clusterware 才能使用 Oracle RAC。请注意，当您使用厂商集群软件时，Oracle Clusterware 会将某些任务（例如节点成员资格决策）委派给厂商集群软件。
- 如果您使用非以太网互连，可能需要第三方厂商集群软件。

设置服务器硬件后，请查看预安装章节中的“检查硬件要求”，以确保您的系统有足够的 RAM，`TMP` 和 `TEMP_DIR` 位置有足够的可用空间用于安装，并且您的系统满足其他硬件要求。

### 1.2.2 服务器环境配置概述

配置 Oracle 软件组和用户，并配置用户环境，如您平台的 *Oracle Grid Infrastructure 安装指南* 预安装章节中所述。这些包括以下内容：

- 创建和配置 Oracle RAC 安装所有者（通常为 `oracle`）；这是您应使用的安装用户账户。
- 创建一个 OSDBA 操作系统组，其成员通过操作系统认证被授予 SYSDBA 权限（通常为 `dba`）。
- 创建二进制文件和存储安装路径。

> **另请参阅：** 您平台的 *Oracle Grid Infrastructure 安装指南*

### 1.2.3 Oracle Base 概述

Oracle Base 位置是存储 Oracle Database 二进制文件的位置。安装过程中，系统会提示您输入 Oracle Base 路径。通常，在 Oracle Grid Infrastructure 安装期间会创建数据库的 Oracle Base 路径。

每个 Oracle Home 都可以有自己的 Oracle Base。通常，Oracle Base 路径基于安装所有者名称。如果您为 Oracle Grid Infrastructure 安装和 Oracle RAC 安装设置了不同的安装所有者，那么您将拥有两个符合最佳灵活架构 (OFA) 准则的 Oracle Base 路径。例如，如果用户 `grid` 是 Oracle Grid Infrastructure 安装的所有者，用户 `oracle` 是 Oracle Database 安装的所有者，那么您将有两个 Oracle Base 目录：

- `/u01/app/grid` — 用户 `grid` 的 Oracle Base，该用户拥有 Oracle Grid Infrastructure 二进制文件
- `/u01/app/oracle` — 用户 `oracle` 的 Oracle Base，该用户拥有 Oracle Database 二进制文件

为准备安装，Oracle 建议您仅设置 `ORACLE_BASE` 环境变量来定义 Oracle 二进制文件和配置文件的路径。Oracle Universal Installer (OUI) 会根据结构良好的 Oracle 软件环境的最佳灵活架构 (OFA) 规则，在必要时创建其他路径和环境变量。

例如，对于 Oracle Database 11g，Oracle 建议您不要设置 Oracle Home 环境变量，而是让 OUI 创建它。如果 Oracle Base 路径是 `/u01/app/oracle`，那么默认情况下，OUI 将创建以下 Oracle Home 路径：

```
/u01/app/oracle/product/11.2.0/dbhome_1
```

确保您为 Oracle 软件选择的路径（例如 Oracle Home 路径和 Oracle Base 路径）仅使用 ASCII 字符。由于默认情况下某些路径使用安装所有者名称，因此此 ASCII 字符限制适用于用户名、文件名和目录名。

> **注意：** 如果您从现有的 Oracle RAC 安装进行升级，则必须使用与现有安装相同类型的 Oracle Home。例如，如果您的现有安装中有共享 Oracle Home，则必须升级到 Oracle RAC 11g release 2 (11.2) 的共享 Oracle Home。类似地，如果在集群节点上有本地 Oracle Home，则必须升级到集群节点上的本地 Oracle Home。

### 1.2.4 网络连接要求概述

以下是 Grid Plug and Play 配置中 Grid Naming Service (GNS) 以及手动网络配置的网络配置要求概述。网络管理员和系统管理员可以参考您平台的 *Oracle Grid Infrastructure 安装指南* 中的预安装章节以获取详细的配置信息。

Oracle Clusterware 和 Oracle RAC 的网络配置需要多个地址。以下是这些地址的列表：

- **GNS 虚拟 IP 地址（仅限 GNS 安装）：** 在 GNS 中配置的静态 IP 地址。GNS 虚拟 IP 监听器将查询转发到集群中由 GNS 管理的子域中的节点。

  在子域内，GNS 使用多播域名服务 (mDNS) 使集群能够在节点添加到集群和从集群中删除时动态映射主机名和 IP 地址，而无需在 DNS 中进行额外的主机配置。

  要启用 GNS，您必须让网络管理员提供一组分配给集群的子域 IP 地址（例如 `grid.example.com`），并将该子域的 DNS 请求转发到集群的 GNS 虚拟 IP 地址，GNS 将为其提供服务。

- **单客户端访问名称 (SCAN)：** 一个域名，解析为为 SCAN 分配的所有地址。Oracle 建议您分配三个指向 SCAN 的地址。在 Oracle Grid Infrastructure 安装期间，会为每个 SCAN 地址创建监听器，并由 Oracle Clusterware 控制哪个服务器响应 SCAN 地址请求。

  为了实现高可用性，您应在 DNS 中提供至少三个 IP 地址用于 SCAN 映射。SCAN 域名在您的企业网络中必须是唯一的。

- **虚拟 IP 地址：** 为每个节点分配一个公共互联网协议（IP）地址，用作客户端连接的虚拟 IP 地址（VIP）。如果节点发生故障，Oracle Clusterware 会将 VIP 地址故障转移到可用节点。

  在安装过程中，如果您不使用网格命名服务（该服务会自动提供 VIP），则需要您提供 VIP 地址。每个节点的 VIP 都与集群中每个节点上相同接口名称相关联。如果您有域名服务器（DNS），则您的网络管理员应将 VIP 的主机名注册到 DNS 中，以便任何客户端以及集群节点都能解析 DNS。VIP 在安装时不应被使用，因为这是由 Oracle Clusterware 管理的 IP 地址。

- **公共 IP 地址：** 为每个节点分配的公共主机名地址，由 GNS 分配，或在初始系统配置时由系统管理员为手动配置分配。公共 IP 地址名称必须能解析为主机名。请将公共 IP 和 VIP 地址都注册到 DNS 中。如果您没有 DNS，则必须确保两个公共 IP 地址都在节点 `/etc/hosts` 文件中（适用于所有集群节点）。

- **私有 IP 地址：** 为每个节点分配的私有 IP 地址，用作专用互连地址，仅用于节点间集群通信。GNS 会自动配置该地址。如果您选择手动配置，则必须确保每个私有 IP 地址满足以下条件。私有 IP 地址必须：

  - 与公共网络分开
  - 在每个节点的相同网络接口上可访问
  - 连接到节点之间的网络交换机以用于私有网络；不支持交叉线缆互连

  私有互连由 Oracle Clusterware 和 Oracle RAC 用于节点间通信。如果您使用手动配置，则私有 IP 地址必须在每个节点的 `/etc/hosts` 文件中可用。Oracle 建议将私有网络互连配置在专用交换机上，这些交换机除了同一集群中的节点外，不连接任何其他设备。

> **注意：** 所有主机名必须符合 RFC 952 标准，该标准允许使用字母数字字符。使用下划线（"_"）的主机名不受支持。

表 1-1 及其后续内容概述了手动网络连接的 IP 地址要求。

如果您选择不使用 GNS，则在安装之前，您的网络管理员必须配置 SCAN、公共、虚拟和私有 IP 地址。当集群中添加或移除节点时，您的网络管理员还必须重新配置网络。

例如，对于一个两节点集群，每个节点有一个公共接口和一个私有接口，并且您已定义了一个 SCAN 域名地址以在 DNS 上解析为三个 IP 地址之一，那么您的网络接口配置可能如下表所示：

**表 1–1 手动网络配置示例**

| 标识 | 主节点 | 主机节点 | 给定名称 | 类型 | 地址 | 地址分配者 | 解析者 |
|---|---|---|---|---|---|---|---|
| 节点 1 公共 | 节点 1 | node1 | node1¹ | 公共 | 192.0.2.101 | 固定 | DNS |
| 节点 1 VIP | 节点 1 | 由 Oracle Clusterware 选择 | node1-vip | 虚拟 | 192.0.2.104 | 固定 | DNS 和 hosts 文件 |
| 节点 1 私有 | 节点 1 | node1 | node1-priv | 私有 | 192.168.0.1 | 固定 | DNS 和 hosts 文件，或无 |
| 节点 2 公共 | 节点 2 | node2 | node2¹ | 公共 | 192.0.2.102 | 固定 | DNS |
| 节点 2 VIP | 节点 2 | 由 Oracle Clusterware 选择 | node2-vip | 虚拟 | 192.0.2.105 | 固定 | DNS 和 hosts 文件 |
| 节点 2 私有 | 节点 2 | node2 | node2-priv | 私有 | 192.168.0.2 | 固定 | DNS 和 hosts 文件，或无 |
| SCAN VIP 1 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.201 | 固定 | DNS |
| SCAN VIP 2 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.202 | 固定 | DNS |
| SCAN VIP 3 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.203 | 固定 | DNS |

¹ 节点主机名可能解析为多个地址。

### 1.2.5 安全外壳（SSH）配置概述

Oracle Clusterware 和 Oracle RAC 需要配置安全外壳（SSH）。系统管理员可以按照 *Oracle Grid Infrastructure 安装指南* 预安装章节中“在所有集群节点上配置 SSH”部分描述的过程，为集群中的每个节点配置到集群所有其他节点的 SSH 访问。

Oracle 建议您要求系统管理员为将拥有 Oracle RAC 安装的用户账户，在所有集群成员节点上允许 SSH 连接。启用此功能后，您可以使用 Oracle Universal Installer 中的脚本为安装设置 SSH 配置。如果由于您用于安装的用户账户的环境限制导致此脚本无法运行，则您或您的系统管理员需要手动设置 SSH 以进行安装。

此外，请注意，显示到终端的任何消息（例如“每日消息”）都可能禁用 SSH 配置。请要求您的系统管理员查阅适用于您平台的 *Oracle Grid Infrastructure 安装指南* 中的 SSH 部分。

### 1.2.6 浏览器要求概述

您需要 Web 浏览器来访问文档，以及使用 Oracle Enterprise Manager 和 Oracle Application Express。Web 浏览器必须支持 JavaScript 以及 HTML 4.0 和 CSS 1.0 标准。

Oracle Enterprise Manager 支持以下浏览器：

- Microsoft Internet Explorer 10（支持 Oracle Enterprise Manager Database Control 11.2.0.3 或更高版本）
- Microsoft Internet Explorer 9.0
- Microsoft Internet Explorer 8.0
- Microsoft Internet Explorer 7.0 SP1
- Microsoft Internet Explorer 6.0 SP2
- Firefox 21.0（支持 Oracle Enterprise Manager Database Control 11.2.0.4）
- Firefox 17.0.6 ESR（支持 Oracle Enterprise Manager Database Control 11.2.0.4）
- Firefox 3.6
- Firefox 3.5
- Firefox 3.0.7
- Firefox 2.0
- Safari 4.0.x
- Safari 3.2
- Safari 3.1
- Google Chrome 27.0（支持 Oracle Enterprise Manager Database Control 11.2.0.4）
- Google Chrome 4.0
- Google Chrome 3.0
- Netscape Navigator 9.0
- Netscape Navigator 8.1

有关 Oracle Application Express 支持的浏览器列表，请参阅 *Oracle Application Express 安装指南*。

> **注意：** 安装 Oracle RAC 不需要浏览器。

### 1.2.7 特定平台服务器配置概述



Oracle Clusterware和Oracle RAC已在特定操作系统内核和特定操作系统组件上进行了测试。Oracle要求您使用为此版本认证的操作系统内核和组件。

Oracle建议您或您的系统管理员在开始安装之前仔细查阅*Oracle Grid Infrastructure安装指南*中的系统要求，以确保您的系统满足这些要求。如果您的系统未达到最低操作系统内核和组件要求，则您的安装可能无法完成，或者在Oracle Clusterware或Oracle Database运行时可能出现其他错误。

除了标准系统要求配置外，在特定服务器硬件上的部署可能包括额外的操作系统配置步骤。请查阅预安装章节，并检查My Oracle Support Certify页面，以确保您了解针对特定硬件平台配置的任何额外要求或建议。

### 1.3 Oracle RAC存储概述

要安装Oracle RAC，您需要为数据库文件配置共享存储。请查阅以下部分进行存储规划：

- [在哪里查看存储系统要求](https://docs.oracle.com/en/database/oracle/oracle-database/19/racad/overview-oracle-rac-storage.html#GUID-5B88276E-0E67-4B30-BB5C-62415E32E447)

- [Oracle自动存储管理集群文件系统概述](https://docs.oracle.com/en/database/oracle/oracle-database/19/racad/overview-oracle-rac-storage.html#GUID-AC79374D-E09B-4A5D-A9B4-C662754F89F8)

- [Oracle数据库和恢复文件选项概述](https://docs.oracle.com/en/database/oracle/oracle-database/19/racad/overview-oracle-rac-storage.html#GUID-F560652B-832F-438F-909A-72B00E992263)

- [Oracle RAC的一般存储注意事项](https://docs.oracle.com/en/database/oracle/oracle-database/19/racad/overview-oracle-rac-storage.html#GUID-B0B9424D-84F1-4C5C-9058-9BE8B1544D49)

- [在Oracle Grid Infrastructure和Oracle RAC中使用逻辑卷管理器](https://docs.oracle.com/en/database/oracle/oracle-database/19/racad/overview-oracle-rac-storage.html#GUID-9AC89729-E9C4-46FC-9C56-1758E2F6F54B)

#### 1.3.1 在哪里查看存储系统要求

请参阅适用于您操作系统的*Oracle Grid Infrastructure安装指南*中“为集群的Grid Infrastructure和Oracle Real Application Clusters（Oracle RAC）配置存储”章节，以查看安装规划的存储选项。存储和系统管理员可以参考此章节，为Oracle RAC上的Oracle Database文件配置存储。请注意，当数据库配置助手（`DBCA`）配置自动磁盘备份时，`DBCA`使用一个必须共享的数据库恢复区域。

#### 1.3.2 Oracle自动存储管理集群文件系统概述

从Oracle Database和Oracle Grid Infrastructure 11.2及更高版本开始，Oracle自动存储管理（Oracle ASM）已扩展，包含一个通用文件系统（Oracle自动存储管理文件系统，或ACFS），可用于您无法直接放置在Oracle ASM上的任何文件，例如数据库主目录或应用程序文件。在本版本发布时，此功能在Linux上可用，但在UNIX平台上不可用。

**另请参阅：** My Oracle Support上的Certify页面，获取有关存储选项的最新信息：[https://support.oracle.com](https://support.oracle.com)

*Oracle自动存储管理管理员指南*，了解存储配置管理的概述

#### 1.3.3 Oracle数据库和恢复文件选项概述

存储Oracle数据库和恢复文件有两种方式：

> **注意：** 不支持在原始设备或块设备上安装文件。请在共享文件系统或Oracle ASM上安装文件。支持升级现有的原始设备或块设备。

#### 1.3.4 Oracle RAC 的通用存储注意事项

对于所有安装，您必须选择要用于 Oracle 数据库文件或用于 Oracle RAC 与 Oracle 集群就绪件（Oracle RAC）的存储选项。如果您希望在安装过程中启用自动备份，那么您还必须选择要用于恢复文件（快速恢复区）的存储选项。对于每种文件类型，您不必使用相同的存储选项。

表 1–2 显示了支持用于存储 Oracle 数据库文件和 Oracle 数据库恢复文件的存储选项。Oracle 数据库文件包括数据文件、控制文件、重做日志文件、服务器参数文件和密码文件。

> **注意：**有关 Oracle RAC 安装支持的存储选项的最新信息，请参阅 My Oracle Support 网站上的认证页面：https://support.oracle.com

- **Oracle 自动存储管理：**Oracle 自动存储管理（Oracle ASM）是一个集成的、高性能的 Oracle 数据库文件系统和磁盘管理器。它自动执行数据库文件的条带化和镜像。

> **注意：**对于使用 Oracle RAC 的标准版 Oracle 数据库安装，Oracle ASM 是唯一支持的存储选项。

- **受支持的共享文件系统：**受支持的文件系统包括以下内容：

  - 受支持的集群文件系统：请注意，如果您打算将集群文件系统用于数据文件，则应在为 Oracle 集群就绪件创建分区时创建足够大的分区以容纳数据库文件。

    **另请参阅：**My Oracle Support 上的认证页面，了解受支持的集群文件系统

  - **NAS 网络文件系统 (NFS)**，列在 Oracle 认证中：请注意，如果您打算将 NFS 用于数据文件，则应在为 Oracle 集群就绪件创建分区时创建足够大的分区以容纳数据库文件。

    **另请参阅：**My Oracle Support 上的认证页面，了解受支持的网络附加存储 (NAS) 设备和受支持的集群文件系统

> **注意：**Oracle RAC 软件可以安装在 OCFS2 上。但是，它不能安装在 Oracle 集群文件系统 (OCFS) 上。Oracle RAC 和 Oracle Grid Infrastructure 软件可以安装在网络附加存储 (NAS) 上。

有关 OCFS2 认证状态，请参阅 My Oracle Support 上的认证页面。

#### 表 1–2 Oracle 数据库和恢复文件支持的存储选项

| 存储选项 | 数据库 | 恢复 |

|---|---|---|

| Oracle 自动存储管理 | 是 | 是 |

| OCFS2 | 是 | 是 |

| 本地存储 | 否 | 否 |

| NFS 文件系统 | 是 | 是 |

| 注意：需要经过认证的 NAS 设备 | | |

| 现有安装中使用的共享原始设备 | 仅适用于升级，或作为手动配置 | 否 |

| 现有安装中使用的共享块设备 | 仅适用于升级，或作为手动配置 | 否 |

在为每种文件类型选择要使用的存储选项时，请遵循以下准则：

- 如果您满足所选存储选项列出的所有要求，则可以为每种文件类型选择任何受支持的存储选项组合。

- Oracle 建议您选择 Oracle 自动存储管理（Oracle ASM）作为数据库和恢复文件的存储选项。

- 对于标准版 Oracle RAC 安装，Oracle ASM 是数据库或恢复文件唯一支持的存储选项。

- 如果您打算升级现有的 Oracle RAC 数据库，或具有 Oracle ASM 实例的 Oracle RAC 数据库，则必须确保您的系统满足以下条件：

    - 在 Oracle RAC 数据库或具有 Oracle ASM 实例的 Oracle RAC 数据库所在的节点上运行 Oracle Universal Installer (OUI) 和数据库配置助手 (DBCA)。

    - Oracle RAC 数据库或具有 Oracle ASM 实例的 Oracle RAC 数据库正在您打算作为新集群安装成员的相同节点上运行。例如，如果您有一个在三节点集群上运行的现有 Oracle RAC 数据库，则必须在所有三个节点上安装升级。您不能仅升级集群的两个节点，而在升级过程中移除第三个节点。

    - 另请参阅：《Oracle 数据库升级指南》了解有关如何准备升级现有数据库的信息

- 如果您没有提供外部文件冗余的存储选项，则必须配置至少三个表决磁盘区域以提供表决磁盘冗余。

#### 1.3.5 在 Oracle Grid Infrastructure 和 Oracle RAC 中使用逻辑卷管理器

Oracle Grid Infrastructure 和 Oracle RAC 仅支持集群感知的卷管理器。要确认您要使用的卷管理器是否受支持，请查看 My Oracle Support 上的认证选项卡，该选项卡可通过以下 URL 访问：https://support.oracle.com

### 1.4 准备安装的补充信息

本节包含有关 Oracle 集群就绪件、Oracle 自动存储管理（Oracle ASM）和 Oracle RAC 的补充信息，这些信息可能对您的安装计划团队阅读以决定如何配置安装有所帮助。它包含以下主题：

- Oracle ASM 随 Oracle Grid Infrastructure 安装

- 获取用于 Oracle Enterprise Manager 的 Oracle ASM ASMSNMP 密码

- Oracle 集群就绪件和供应商集群件

- Oracle RAC 安装的共享组件

- 简化带时区时间戳数据的升级

- 确保为 HP-UX 创建外部作业用户

- Oracle Database 11g Real Application Clusters 版本兼容性

#### 1.4.1 Oracle ASM 随 Oracle Grid Infrastructure 安装

在过去的版本中，Oracle ASM 是作为 Oracle 数据库安装的一部分安装的。从 Oracle Database 11g 第 2 版 (11.2) 开始，Oracle ASM 是 Oracle Grid Infrastructure 安装的一部分。如果您想升级现有的 Oracle ASM 安装，则必须通过运行 Oracle Grid Infrastructure 升级来升级 Oracle ASM。

如果您未选择 Oracle ASM 作为 Oracle 集群就绪件文件的存储选项，则必须首先使用 Oracle ASM 配置助手 (ASMCA) 配置 Oracle ASM，创建 Oracle ASM 实例，并创建用于 Oracle 数据库存储的磁盘组。

#### 1.4.2 获取用于 Oracle Enterprise Manager 的 Oracle ASM ASMSNMP 密码

从 Oracle Grid Infrastructure 管理员处获取 ASMSNMP。

在集群的 Oracle Grid Infrastructure 安装期间，会创建 ASMSNMP 帐户并将其状态设置为 OPEN。它被授予 ASM 的 SYSDBA 权限。Oracle Enterprise Manager 需要访问 ASMSNMP 帐户来监视 Oracle ASM 实例并从 ASM 相关的数据字典视图中检索数据。

> **另请参阅：***《Oracle 自动存储管理管理员指南》* 了解有关 ASMSNMP 帐户的其他信息

#### 1.4.3 Oracle 集群就绪件和供应商集群件

Oracle 集群就绪件提供集群服务。当您使用 Oracle 集群就绪件时，不需要供应商集群件。如果您打算安装 Oracle RAC，则必须安装 Oracle 集群就绪件。

#### 1.4.4 Oracle RAC 安装的共享组件

对于 Oracle RAC，您和您的系统管理员应注意，Oracle RAC 环境中的所有实例共享控制文件、服务器参数文件、重做日志文件和所有数据文件。这些文件必须放置在共享文件系统上，并且所有集群数据库实例必须能够访问它们。每个实例还有一组自己的重做日志文件。在故障期间，共享访问重做日志文件使幸存实例能够执行恢复。

#### 1.4.5 简化带时区时间戳数据的升级

作为 Oracle Database 11g 第 2 版 (11.2) 安装的一部分，时区版本文件从 1 到 11 安装在路径`$ORACLE_HOME/oracore/zoneinfo/`中。您可以继续使用当前时区版本，也可以升级到最新版本。Oracle 建议您将服务器升级到最新的时区版本。升级到新的时区版本可能会导致现有的带时区时间戳 (TSTZ) 数据变得过时。使用新提供的`DBMS_DST` PL/SQL 包，您可以透明地更新 TSTZ 数据，只需最少的手动步骤和系统停机时间。

Oracle RAC 数据库的所有实例必须使用相同的时区。Oracle RAC 数据库时区默认为 Oracle Grid Infrastructure Grid 用户的时区设置，除非实例是使用 SQL*Plus 启动的。当您使用 SQL*Plus 时，必须确保为数据库实例使用的时区设置与 Oracle 集群就绪件使用的时区设置相同。您可以使用以下命令更改 Oracle 集群就绪件用于数据库的时区，其中`time zone`是您要更改到的时区：

```
srvctl setenv database -T 'TZ=time zone'
```

时区版本文件也安装在客户端上。从 Oracle Database 11g 第 2 版开始，您不再需要立即升级客户端时区文件。升级可以在系统管理员最方便的时候进行。但是，当客户端和服务器使用不同的时区版本时，可能会有轻微的性能损失。

> **另请参阅：***《Oracle 数据库升级指南》* 了解有关准备升级带时区时间戳数据的信息，*《Oracle 数据库全球化支持指南》* 了解有关如何升级时区文件和带时区时间戳数据的信息，以及 *《Oracle 调用接口程序员指南》* 了解有关客户端和服务器使用不同版本时区文件运行的性能影响的信息

#### 1.4.6 确保为 HP-UX 创建外部作业用户

如果您正在 HP-UX 上安装 Oracle Real Application Clusters，请确保创建了一个具有低权限的用户来拥有外部作业，并注意您必须以 root 用户身份登录并在安装后修改`$ORACLE_HOME/rdbms/admin/externaljob.ora`将此用户设置为外部作业用户。只有 root 用户可以修改此文件。

#### 1.4.7 Oracle Database 11g Real Application Clusters 版本兼容性

您可以在同一台计算机上安装和运行不同版本的 Oracle 数据库软件：

### 使用 CVU 确认 Oracle RAC 安装的集群就绪状态

- 当你安装了包含不同发行版 Oracle 软件的 Oracle Clusterware 时，Oracle Clusterware 的版本必须大于或等于 Oracle 数据库软件的版本。Oracle Clusterware 和 Oracle 自动存储管理将随 Oracle Grid Infrastructure 11g 第 2 版 (11.2) 安装一同升级。

- 如果你有一个现有的 Oracle 主目录，那么你可以创建一个新的 Oracle 主目录，并将 Oracle 数据库 11g 第 2 版 (11.2) 安装到这个新的 Oracle 主目录中。你应该确保 Oracle Clusterware 位于一个单独的 Oracle Grid Infrastructure 主目录中。Oracle Grid Infrastructure for a Cluster 的安装不能安装在 Oracle 数据库的 Oracle 基础目录中。

- 如果你正在运行 Oracle RAC 的 Oracle9i 发行版，并且希望继续使用该发行版，那么你必须运行与该发行版兼容的集群软件，例如 Oracle Cluster Manager 或第三方集群软件。Oracle Clusterware 11g 发行版可以与 Oracle9i 数据库软件安装在同一系统上，但 Oracle9i 软件不能由 Oracle Clusterware 11g 支持。

> **注意：** 如果你想在将数据库升级到 Oracle 数据库 10g 或 Oracle 数据库 11g 后移除第三方集群软件，那么你必须先移除第三方集群软件，然后重新安装 Oracle Clusterware。

如果 OUI 检测到之前的数据库发行版，那么 OUI 会询问你的升级偏好。你可以选择使用 DBUA 升级其中一个之前的发行版数据库，或者使用 DBCA 创建一个新数据库。在此对话框中收集的信息将在软件安装后传递给 DBUA 或 DBCA。

如果 OUI 检测到之前的 Oracle Clusterware 发行版，那么会提示你升级现有的 Oracle Clusterware 安装。一个服务器上只能存在一个 Oracle Clusterware 版本，并且服务器必须仅是一个集群的成员。

你不能先为独立服务器安装 Oracle Grid Infrastructure，然后再为集群安装 Oracle Grid Infrastructure。如果你已经为独立服务器安装了 Oracle Grid Infrastructure，那么你必须先移除该安装，然后才能为集群安装 Oracle Grid Infrastructure。



> **注意：** 不要将 Oracle 二进制文件从 Oracle 主目录移动到另一个位置。这样做可能导致动态链接失败。

### 1.5 使用 CVU 确认 Oracle RAC 安装的集群就绪状态

在开始安装之前，请使用 CVU 来确保你的系统已为 Oracle RAC 安装做好准备。如果有任何检查失败，请修复报告的错误，可以手动修复或使用生成的修复脚本，或者联系你的系统或存储管理员来解决错误的原因。

CVU 位于 Grid 主目录的 `bin` 目录中。例如，如果 Oracle Grid Infrastructure for a cluster 的主目录是 `/u01/crs`，那么路径就是 `/u01/crs/bin`。要启动 CVU，请导航到 Grid 主目录的 `bin` 目录，并使用类似以下的命令：

`cluvfy stage -pre dbinst -fixup -n nodelist -r release -osdba OSDBA -verbose`

在上面的命令中，`-fixup` 和 `-osdba` 是可选标志。

例如，对于一个包含 nodeA 和 nodeB 两个节点的集群，你正在测试集群以准备使用 Oracle RAC 安装 Oracle 数据库 11g，并且你的 OSDBA 组是 dba，以下命令会检查系统就绪状态：

```
$ ./cluvfy stage -pre dbinst -fixup -n nodea,nodeb -osdba dba -verbose
```

有关 CVU 命令的更多信息，请输入 `./cluvfy -help`。

**另请参阅：** *《Oracle Clusterware 管理和部署指南》* 以获取有关 CVU 的详细信息

### 1.6 为升级或共存数据库停止现有 Oracle 进程

如果你计划在具有现有 Oracle RAC 或 Oracle 数据库安装的系统上进行安装，那么你必须执行额外的任务来为安装准备你的系统。

[表 1-3](#) 概述了如果你有现有 Oracle 数据库安装时需要做的事情。请查看该表，并根据需要执行任务。

**另请参阅：** *《Oracle 数据库升级指南》* 以获取有关准备和执行升级的更多信息

| 安装场景 | 你需要做的事情 |
|:---|:---|
| 从 Oracle 数据库 10g 第 1 版 (10.1) 升级到 11g 第 2 版 (11.2) | 无需额外任务。请参阅第 1-20 页的[在具有 Oracle 数据库 10g 的系统上安装 Oracle 数据库 11g](#) |
| 在系统上安装 Oracle 数据库 11g 第 2 版 (11.2) 与 Oracle 数据库 10g 第 1 版 (10.1) 共存 | 无需额外任务。请参阅第 1-20 页的[在具有 Oracle 数据库 10g 的系统上安装 Oracle 数据库 11g](#) |
| 从 Oracle9i 第 9.2 版升级到 Oracle 数据库 11g 第 2 版 (11.2) | 关闭全局服务守护进程，并关闭端口 1521 上的默认监听器（如果存在）。请参阅第 1-20 页的[在具有 Oracle9i 数据库第 2 版的系统上安装 Oracle 11g 数据库](#) |
| 在系统上安装 Oracle 数据库 11g 第 2 版 (11.2) 与 Oracle9i 第 9.2 版共存 | 关闭端口 1521 上的默认监听器（如果存在），并关闭全局服务守护进程。请参阅第 1-20 页的[在具有 Oracle9i 数据库第 2 版的系统上安装 Oracle 11g 数据库](#) |

#### 在具有 Oracle 数据库 10g 的系统上安装 Oracle 数据库 11g

如果你的系统已经安装了 Oracle 数据库 10g，并且你安装 Oracle 数据库 11g 第 2 版 (11.2) 以与 Oracle 数据库 10g 安装共存或对其进行升级，那么大多数安装类型会使用 TCP/IP 端口 1521 和 IPC 键值 `EXTPROC` 配置并启动一个默认的 Oracle Net 监听器。以下情况之一会发生：

- 在共存安装期间，数据库配置助手 (DBCA) 会自动将监听器及相关文件从 Oracle 数据库 10g 的 Oracle 主目录迁移到 Oracle 数据库 11g 的 Oracle 主目录。

- 在升级期间，Oracle 数据库升级助手 (DBUA) 会自动定位 Oracle 数据库 10g 的监听器，并将该监听器迁移到 Oracle 数据库 11g。

> **注意：** 对于 Oracle 数据库 11g 第 2 版 (11.2) 与使用 Oracle ASM 的 Oracle 数据库 10g 第 1 版 (10.1) 数据库共存，10.1 数据库必须是 10.1.0.3 或更高版本。

#### 在具有 Oracle9i 数据库第 2 版的系统上安装 Oracle 11g 数据库

**任务说明** 如果你正在一个具有现有 Oracle9i 数据库第 2 版 (9.2) 的系统上安装 Oracle 数据库 11g 第 2 版 (11.2)，并且 Oracle Net 监听器进程正在使用与 Oracle 数据库 11g 第 2 版 (11.2) 安装默认使用的*相同*端口或键值（端口 1521），那么 OUI 只能配置新的监听器；它无法启动它。为了确保新的监听器进程在安装过程中启动，你必须在启动 OUI 之前关闭任何现有的监听器。要执行此操作，请参阅第 1-20 页的“关闭监听器”。

你必须关闭全局服务守护进程 (GSD)，因为否则在 Oracle 数据库 11g 安装期间，Oracle 数据库 9i 第 9.2 版的 SRVM 共享数据将被升级到一个 9.2 版 GSD 无法使用的 Oracle 集群注册表中。Oracle Grid Infrastructure 安装会启动一个 11g 第 2 版 (11.2) 的 GSD 来为 Oracle9i 9.2 客户端提供服务。要执行此操作，请参阅第 1-21 页的“关闭全局服务守护进程”。

**关闭监听器** 要确定现有的 Oracle 数据库 9i 监听器进程是否正在运行并在必要时将其关闭，请按照以下步骤操作：

1. 切换到软件所有者用户。例如：

   `# su - oracle`

2. 输入以下命令以确定 Oracle 数据库 9i 监听器进程是否正在运行，并识别其名称和安装它的 Oracle 主目录：

   `$ ps -ef | grep tnslsnr`

   此命令显示有关系统上运行的 Oracle Net 监听器的信息：

   `... oracle_home1/bin/tnslsnr LISTENER -inherit`

   在此示例中，*oracle_home1* 是安装监听器的 Oracle 主目录，*LISTENER* 是监听器名称。

3. 设置 ORACLE_HOME 环境变量以指定监听器的相应 Oracle 主目录：

   - Bourne、Bash 或 Korn shell：

     `$ ORACLE_HOME=oracle_home1`

     `$ export ORACLE_HOME`

   - C 或 tcsh shell：

     `% setenv ORACLE_HOME oracle_home1`

1-20 Oracle Real Application Clusters 安装指南

4. 输入以下命令以识别监听器使用的 TCP/IP 端口号和 IPC 键值：

```
$ $ORACLE_HOME/bin/lsnrctl status *listenername*
```

> **注意：** 如果监听器使用默认名称 LISTENER，则无需在此命令中指定监听器名称。

5. 输入类似于以下命令以停止监听器进程：

```
$ $ORACLE_HOME/bin/lsnrctl stop *listenername*
```

6. 重复此过程，以停止在此系统及集群中所有其他节点上运行的所有监听器。

#### 关闭全局服务守护进程

作为数据库安装软件所有者（例如 *oracle*），在集群的每个节点上，使用以下语法关闭 GSD：

```
$ cd *92_Oracle_home*
$ bin/gsdctl stop
```

在上述语法示例中，变量 *92_Oracle_home* 是 Oracle Database 9i 第 2 版 (9.2) 的主目录。

#### 停止用于升级或共存数据库的现有 Oracle 进程

## 2 使用 Oracle Real Application Clusters 安装 Oracle Database 11*g*

本章描述使用 Oracle Real Application Clusters (Oracle RAC) 安装 Oracle Database 11g 第 2 版 (11.2) 的安装过程的第二阶段。第一阶段是完成 Oracle Clusterware 的安装，如您平台对应的 *Oracle Grid Infrastructure 安装指南* 中所述。

> **另请参阅：** 您平台对应的 *Oracle Database 安装指南* 以获取更多信息，例如如何打开压缩文件以及有关设置安装文件的其他信息。此外，在安装过程中，单击 **帮助** 可查看每个安装屏幕的选项和提示说明，单击 **详细信息** 可查看日志文件。

本章包含以下主题：

- 审查 Oracle Application Express 要求
- 选择配置选项
- Oracle Database Vault 安装和配置
- Oracle Database 配置类型描述
- Oracle Configuration Manager 选项
- 数据库安全选项
- 更改管理账户数据库密码
- OUI 和 DBCA 在安装期间的操作
- 使用其他语言安装 Oracle Database
- 选择数据库名称
- 使用 Oracle Universal Installer 安装 Oracle RAC
- 使用 Oracle Universal Installer 安装 Oracle RAC One Node
- 使用 DBCA 配置 Oracle RAC One Node

### 2.1 审查 Oracle Application Express 要求

在 Oracle Database 11g 版本中，Oracle Application Express 作为 Oracle Database 选项提供，而非 Oracle Application 选项。如果您打算在安装 Oracle Clusterware 之后安装 Oracle Database，并且您有要升级的现有 Oracle Database 安装，请审查以下 Oracle Application Express 要求：

- [Oracle Application Express 的浏览器要求](Browser Requirements for Oracle Application Express)
- [使用现有 Oracle HTML Server 安装进行安装](Installing with Existing Oracle HTML Server Installations)
- [Oracle Application Express 的 Oracle Text 要求](Oracle Text Requirement for Oracle Application Express)
- [Oracle Application Express 的 Oracle XML DB 要求](Oracle XML DB Requirement for Oracle Application Express)

#### 2.1.1 Oracle Application Express 的浏览器要求

要查看或开发 Oracle Application Express 应用程序，Web 浏览器必须支持 Java Script 以及 HTML 4.0 和 CSS 1.0 标准。以下浏览器满足此要求：

- Mozilla 1.7 或更高版本
- Firefox 1.0.4 或更高版本

#### 2.1.2 使用现有 Oracle HTML Server 安装进行安装

Oracle Application Express 必须能够访问 Oracle HTTP Server 和 `mod_plsql` 才能运行。以下产品包含满足此要求的 HTTP Server 和 `mod_plsql` 版本：

- Oracle 9i Database 第 2 版 (9.2) 或更高版本
- Oracle 9i Application Server 第 1 版 (1.0.2.2) 或更高版本

#### 2.1.3 Oracle Application Express 的 Oracle Text 要求

必须安装 Oracle Text，以便您可以在 Oracle Application Express 中使用可搜索的联机帮助。默认情况下，Oracle Text 作为 Oracle Database 的一部分安装。

> 另请参阅：*Oracle Text 应用程序开发人员指南* 以获取有关 Oracle Text 的更多信息。

#### 2.1.4 Oracle Application Express 的 Oracle XML DB 要求

要升级到 Oracle Database 11g 第 2 版 (11.2)，必须在要升级的 Oracle 数据库中安装 Oracle XML DB。如果您使用的是在安装期间或通过数据库配置助手 (DBCA) 创建的预配置数据库，则 Oracle XML DB 已安装并配置。

> 另请参阅：*Oracle XML DB 开发人员指南* 以获取有关手动将 Oracle XML DB 添加到现有数据库的更多信息。

### 2.2 选择配置选项

本节描述您在开始 Oracle RAC 安装过程之前应了解的 OUI 功能。

> 另请参阅：[附录 C，“从单实例 Oracle 数据库转换为 Oracle RAC 和 Oracle RAC One Node”](Appendix C, "Converting to Oracle RAC and Oracle RAC One Node from Single-Instance Oracle Databases") 以获取有关如何将单实例数据库转换为 Oracle RAC 的信息。

在“选择安装选项”页面上，您将看到以下选项：

- **创建并配置数据库**：为您提供使用为特定系统负载需求（例如在线事务处理 (OLTP) 数据库或决策支持或数据仓库数据库）设计的预配置数据库模板创建数据库的选项。

- **仅安装数据库软件**：安装 Oracle Database 软件；您必须稍后完成数据库配置。

- **升级现有数据库**：升级现有数据库。

如果您要安装 Oracle Database 软件，Oracle 建议您使用预配置数据库选项之一，或在“选择配置”页面上选择 **高级** 选项，并配置自定义的入门数据库。

> **另请参阅：** 如果您有现有的 Oracle 安装，请记录您的环境版本号、补丁程序和其他配置信息，并审查您现有安装的升级过程。在继续安装之前，请审查 Oracle 升级文档以决定如何继续。

有关升级前、升级后、兼容性和互操作性讨论的最新更新和最佳实践，请参阅“Oracle 升级伴侣”。“Oracle 升级伴侣”可通过 My Oracle Support 上的注释 785351.1 获取：https://support.oracle.com/

### 2.3 Oracle Database Vault 安装和配置

如果您要安装 Oracle Database Vault，请审查以下信息：

- Oracle Database Vault 要求
- Oracle Database Vault 帐户
- 多个 Oracle Database Vault 主目录
- 使用 Oracle Database Vault 安装启动监听器
- 安装 Oracle Database Vault

#### 2.3.1 Oracle Database Vault 要求

Oracle Database Vault 要求如下：

- Oracle Database Enterprise Edition 安装（单实例或 Oracle RAC）
- 将初始化参数 `db_block_size` 设置为 4096 或更高
- Oracle Enterprise Manager Console
- Oracle Clusterware 正在运行（用于在 Oracle RAC 环境中安装）

> **注意：** 您必须具有 `root` 访问权限才能启动 Oracle Clusterware。命令 `crsctl start crs` 也会启动数据库。在启动 OUI 安装 Oracle Database Vault 之前，请关闭数据库。

> **另请参阅：** [E.3.1 节，“在添加产品或升级前停止 Oracle 数据库进程”](#)

- 为您要安装 Oracle Database Vault 的数据库配置的监听器。为确保在安装期间启动新的监听器进程，您必须在启动 Oracle Universal Installer 之前关闭现有监听器。

- Oracle Database Vault 安装所有者对 Oratab 文件（AIX：`/etc/oratab`；Solaris、HP-UX：`/var/opt/oracle/oratab`）和 `oraInst.loc` 文件（AIX：`/etc/oraInst.loc`；Solaris、HP-UX：`/var/opt/oracle/oraInst.loc`）的写入权限。此访问权限通过使用与 Oracle Database 安装相同的安装所有者或具有 `oinstall` 组成员资格的其他用户提供。

- Oracle Database 的现有密码文件。此外，密码文件认证参数 `REMOTE_LOGIN_PASSWORDFILE` 必须已设置为 EXCLUSIVE 或 SHARED。



您可以在 Oracle Database 初始化文件中设置`REMOTE_LOGIN_PASSWORDFILE`参数。使用`orapwd`实用程序创建和管理密码文件。

> **另请参阅：** *Oracle Database 管理员指南* 以获取有关创建和维护密码文件的更多信息。

## 2.3.2 Oracle Database Vault 帐户

Oracle Database Vault 会提示您输入两个可在安装期间创建的帐户。它们是 Oracle Database Vault Owner 和 Oracle Database Vault Account Manager 帐户。您必须在安装期间为 Database Vault Owner 提供帐户名和密码。创建 Oracle Database Vault Account Manager 是可选的。

### 2.3.2.1 Oracle Database Vault Owner

Oracle Database Vault Owner 帐户被授予`DV_OWNER`角色。此帐户可以管理 Oracle Database Vault 角色和配置。

Oracle Database Vault Owner 用户名长度至少为 2 个字符，最多为 30 个字符。帐户密码长度至少为 8 个字符，最多为 30 个字符。

您为 Oracle Database Vault Owner 帐户选择的密码必须安全。强制执行以下密码限制：

- 密码必须包含至少一个字母、一个数字和一个非字母数字字符（符号）。
- 密码不能与帐户名相同。
- 密码不能包含任何连续重复的字符。

### 2.3.2.2 Oracle Database Vault Account Manager

Oracle Database Vault Account Manager 被授予`DV_ACCTMGR`角色。此帐户用于管理数据库用户帐户。创建 Oracle Database Vault Account Manager 是为了促进职责分离。如果您选择不创建 Oracle Database Vault Account Manager 帐户，则默认将`DV_ACCTMGR`角色授予 Oracle Database Vault Owner 帐户。

Oracle Database Vault Account Manager 用户名长度至少为 2 个字符，最多为 30 个字符。帐户密码长度至少为 8 个字符，最多为 30 个字符。

## 2.3.3 多个 Oracle Database Vault 主目录

适用于 Oracle Database Vault 所有者的相同密码限制，同样适用于 Oracle Database Vault 账户管理员。

你可以在同一系统上安装多个 Oracle Database Vault，但需位于不同的 Oracle 主目录中。

## 2.3.4 使用 Oracle Database Vault 安装启动监听器

你需要在执行安装的节点以外的所有 Oracle RAC 节点上启动监听器和数据库。必须使用服务器控制（`srvctl`）工具来启动和停止 Oracle Database Vault Oracle RAC 实例。请勿使用 SQL*Plus 来启动和停止 Oracle RAC 实例。

例如：

```
$ORACLE_HOME/bin/lsnrctl start listener_name
$ORACLE_HOME/bin/srvctl start instance -d database_name -i instance_name
```

## 2.3.5 安装 Oracle Database Vault

Oracle Database Vault 通过“高级安装”选项进行安装。你可以在安装后使用 DBCA 配置 Oracle Database Vault，也可以选择不配置。

### 2.3.5.1 在 Oracle RAC 安装期间配置 Oracle Database Vault

要在安装 Oracle RAC 的同时安装 Oracle Database Vault：

1. 启动 Oracle Universal Installer，并选择高级安装。
2. 选择企业版，然后选择“选择选项”。
3. 除默认安装组件外，还需选择 Oracle Label Security (OLS) 和 Oracle Database Vault。
4. 安装完成后，继续创建数据库。
5. 创建数据库后，启动 DBCA。
6. 选择配置数据库的选项。
7. 在组件列表中，选择 Oracle Label Security 和 Oracle Database Vault 以配置到数据库。
8. 提供所需的 Oracle Database Vault 用户 ID 和密码以继续配置。如果你想启用独立的 Oracle Database Vault 管理员，则可以选择配置`DV_ACCTMGR`用户。

### 2.3.5.2 在 Oracle RAC 安装后配置 Oracle Database Vault

要在安装 Oracle RAC 后配置 Oracle Database Vault：

1. 安装 Oracle RAC 企业版数据库。
2. 停止所有数据库进程。
3. 输入以下命令：

```
$ make -f $ORACLE_HOME/rdbms/lib/ins_rdbms.mk dv_on
$ make -f $ORACLE_HOME/rdbms/lib/ins_rdbms.mk ioracle
```

4. 启动所有 Oracle RAC 进程。
5. 启动 DBCA，并选择“配置数据库”选项。
6. 在组件列表中，选择 Oracle Label Security 和 Oracle Database Vault。
7. 提供所需的管理用户账户和密码，并继续配置。

## 2.4 Oracle 配置类型描述

运行 OUI 时，你可以选择“典型”或“高级”安装类型。

“典型”安装类型安装具有基本配置选项的 Oracle Database 默认配置。Oracle 建议大多数用户选择“典型”作为其安装类型。

“高级”安装类型用于自定义安装，仅应在你有特定需求时使用，例如需要为`SYS`、`SYSMAN`、`SYSTEM`和`DBSNMP`账户设置不同的密码，或使用与服务器上不同的数据库字符集，更改产品语言或其他非标准配置。

你可以在集群中的两个或多个节点上安装 Oracle RAC One Node。Oracle RAC One Node 安装会在你选择作为 Oracle RAC One Node 池成员的某个节点上启动一个实例。如果该实例发生故障，则 Oracle RAC One Node 实例将使用“在线数据库重定位”在另一个池成员上启动。此功能会将数据库实例和连接迁移到其他集群节点以实现高可用性。

> **另请参阅：** *Oracle Database 高可用性概述*，了解有关 Oracle RAC One Node 的信息

### 2.4.1 通用事务处理和数据仓库配置类型

“通用事务处理”类型和“数据仓库”配置类型使用针对每种数据库类型优化的预配置数据库模板。

在安装过程中，OUI 会启动 Oracle 网络配置助手 (NETCA) 和 DBCA，并无需额外输入即可安装预配置的数据库。在数据库安装过程中，OUI 会显示进度指示器。

这两种配置类型的 DBCA 处理会创建一个初始数据库，并配置 Oracle 网络服务。

如果你选择“高级”配置，则必须输入下一节中描述的特定信息。

### 2.4.2 使用高级安装类型

使用“高级”安装类型来满足特定要求，例如选择要添加或删除的特定组件、使用非默认字符集创建数据库，或添加除英语以外的产品用户界面语言翻译。默认情况下，安装会根据操作系统的语言配置新数据库的字符集。

> **另请参阅：** *Oracle Database 全球化支持指南*，了解有关字符集和语言配置的详细信息

以下部分提供了有关创建 Oracle RAC 数据库时 OUI 和 DBCA 处理的更多详细信息。

> **另请参阅：** *适用于你平台的 Oracle Database 安装指南*，了解有关配置全球化的信息

## 2.5 Oracle Configuration Manager 选项

在安装过程中，系统会提示你提供启用 Oracle Configuration Manager 所需的信息。此选项允许你将有关 Oracle RAC 配置的信息与你的 My Oracle Support（原 *OracleMetalink*）账户相关联。如果你需要向 Oracle Support 提交服务请求，该配置信息可以帮助更快速地解决服务问题。

配置 OCM 工具需要你从服务协议中获取以下信息：

- My Oracle Support 电子邮件地址/用户名
- 密码

此外，如果主机系统没有直接连接到互联网，系统会提示你输入服务器代理信息。

如果遇到注册失败并不确定是否指定了正确的国家/地区代码，请参阅 My Oracle Support (https://support.oracle.com)。你可以通过选择菜单选项 **更多**，然后选择 **设置** 来查找与你的 My Oracle Support 账户关联的国家/地区。在“设置”菜单中，选择 **账户和权限**。

> **另请参阅：** *Oracle Configuration Manager 安装和管理指南* 以获取更多信息

## 2.6 数据库安全选项

在安装过程中，系统会提示你选择数据库安全配置。**安全配置** 选项使用数据库审计选项以及密码策略和过期设置来配置数据库。

对于新的数据库安装，Oracle Database 11g 第 2 版 (11.2) 的默认配置包含 **安全配置** 选项。如果你想禁用这些增强的安全控制，则可以选中 **禁用安全设置** 框。然后，Oracle Database 将使用 Oracle Database 10g 第 2 版的默认选项进行安装。安装后，你可以通过启动 DBCA 并修改安全设置来更改安全设置。你可以启用或禁用审计或密码安全设置，或恢复到以前的安全设置。

对于数据库升级，升级后的数据库会保留你现有的数据库安全配置，以确保与现有应用程序的兼容性。安装后，你可以使用 DBCA 为测试启用或禁用 **安全配置** 审计或密码安全设置。

要在安装后启用或禁用安全配置，必须使用命令行 DBCA 选项。根据设计，DBCA 11g 第 2 版及更高版本的图形用户界面没有启用或禁用安全配置的选项。

> **注意：** Oracle 强烈建议在安装期间使用 **安全配置** 选项配置你的数据库，或者在安装后使用命令行 DBCA 进行配置。

## 2.7 更改管理账户数据库密码

所有数据库都包含管理账户`SYS`、`SYSTEM`和`SYSMAN`。管理账户是高权限账户，仅需由授权执行管理任务的人员使用，例如启动和停止数据库、管理数据库内存和存储、创建和管理数据库用户等。

除`SYS`、`SYSTEM`、`SYSMAN`和`DBSNMP`外，所有 Oracle 系统管理账户的密码在安装后都会被吊销。你应该在安装后更改管理账户和`DBSNMP`的密码。你必须将管理账户密码更改为与默认密码不同的密码。

> **另请参阅：** *Oracle Database 2 天 DBA 在线帮助* 和 *Oracle Database 管理员指南*，了解有关管理账户的更多信息

指定密码时请遵循以下准则：

- 密码长度必须在 8 到 30 个字符之间。
- 密码不得以数字开头。
- 密码不得与用户名相同。
- 密码不得是 Oracle 保留字。
- `SYS`账户密码不得为`change_on_install`。
- `SYSTEM`账户密码不得为`manager`。
- `SYSMAN`账户密码不得为`sysman`。
- `DBSNMP`账户密码不得为`dbsnmp`。
- 若要为所有账户使用相同的密码，该密码不得为`change_on_install`、`manager`、`sysman`或`dbsnmp`。
- 密码应至少包含 1 个字母字符、1 个数字字符和 1 个标点字符。
- 密码不应是简单或明显的单词，例如 welcome、account、database 和 user。

## 2.8 OUI 和 DBCA 在安装期间的操作

安装 Oracle Database 后，OUI 会运行 DBCA 来创建你的数据库，遵循最优灵活架构 (OFA) 准则。遵循 OFA 准则创建的安装意味着 DBCA 使用标准文件命名和文件放置实践来创建你的数据库文件，包括默认的服务器参数文件 (SPFILE)。

DBCA 处理的主要阶段如下：

- 创建数据库。
- 如有必要，配置 Oracle 网络服务。
- 启动监听器和数据库实例。

您也可以使用 DBCA 的独立模式来创建或删除数据库，或将数据库管理从 Oracle Enterprise Manager Database Control 切换到 Oracle Enterprise Manager Grid Control。

请注意，对于 Oracle Database 11.1 及更高版本，DBCA 不再用于管理 Oracle RAC 数据库的服务。对于所有服务的管理和监控，请使用`srvctl`、Oracle Enterprise Manager DB Control 或 Grid Control。Oracle Net Configuration Assistant (NetCA) 作为 Oracle Grid Infrastructure 安装的一部分运行。

**另请参阅：** 以下文档获取更多信息：

- *Oracle Database Net Services Administrator's Guide*，如果您遇到问题（例如，监听器配置问题），以及有关轻量级目录访问协议 (LDAP) 支持的更多信息
- *Oracle Enterprise Manager Real Application Clusters Guide Online Help*，有关使用 Oracle Enterprise Manager 进行服务管理

在 Oracle Database 10g 及更高版本中，一些数据库语言和区域定义文件已更新，以更好地反映相关区域中使用的区域设置约定。

如果由此产生的默认 NLS 参数值变化对您的现有应用程序产生不利影响，那么您可以通过安装 Oracle9i 兼容性定义文件来恢复更改。要将 Oracle11g 文件替换为 Oracle9i 文件，您必须按照 ["Using Oracle Universal Installer to Install Oracle RAC"](https://example.com)（第 2-10 页）中描述的方式，从命令行运行 OUI，并使用以下语句将`b_cr9idata`变量设置为`true`：

```
./runInstaller oracle.rsf.nlsrtl_rsf:b_cr9idata=true
```

**另请参阅：** *Oracle Database Globalization Support Guide*，获取有关 Oracle Database 语言和区域定义文件更新的更多信息

## 2.9 使用其他语言安装 Oracle Database

要使用默认语言（英语）以外的其他语言（无论是数据库还是在数据库上运行的应用程序），您必须使用高级安装类型。

**另请参阅：** *Oracle Database Globalization Support Guide*

## 2.10 选择数据库名称

数据库名称输入字段用于设置以下 Oracle 初始化参数值：

- `DB_NAME`
- `DB_UNIQUE_NAME`
- `DB_DOMAIN`

在 Oracle RAC 环境中，数据库名称 (`DB_UNIQUE_NAME`) 部分是一个不超过 30 个字符的字符串，可以包含字母数字、下划线 (`_`)、美元符号 (`$`) 和井号 (`#`) 字符，但必须以字母字符开头。数据库名称中不允许使用其他特殊字符。数据库的`DB_NAME`参数设置为数据库名称的前 8 个字符。

全局数据库名称 (`DB_DOMAIN`) 的域名部分不得超过 128 个字符。不允许使用带下划线 (`_`) 的域名。`DB_UNIQUE_NAME.DB_DOMAIN`的整个值在企业中必须是唯一的。

例如，如果您的数据库全局数据库名称为`or1$racprod2551.example.com`（您在安装期间提供），则以下值用于初始化参数：

| 参数 | 值 |
| :--- | :--- |
| `DB_UNIQUE_NAME` | `or1$racprod2551` |
| `DB_DOMAIN` | `example.com` |
| `DB_NAME` | `or1$racp` |

SID 前缀是数据库名称的前 8 个字符。SID 前缀只能包含字符 a-z、A-Z 和 0-9。SID 前缀不能包含操作系统特殊字符，因此如果您在数据库名称的前 8 个字符中使用了特殊字符，则这些特殊字符在 SID 前缀中将被省略。每个数据库都有一个唯一的 SID 前缀。数据库的 SID 前缀在集群中必须是唯一的。

对于 Oracle RAC 数据库，每个实例都有一个唯一的标识符`ORACLE_SID`，它由 SID 前缀和实例编号组成。Oracle RAC 数据库实例的`ORACLE_SID`生成方式取决于您选择如何管理数据库。如果您选择策略管理的数据库，则 Oracle 以`name_#`格式生成 SID，其中`name`是`DB_UNIQUE_NAME`的前八个字母数字字符，`#`是实例编号。如果您选择管理员管理的数据库，则 DBCA 会预先生成实例名称的 SID，SID 格式为`name#`。

例如，如果数据库的`DB_UNIQUE_NAME`为`or1$racprod2551`，则使用以下 SID 值：

| 数据库或实例类型 | 用于`ORACLE_SID`的值 |
| :--- | :--- |
| 单实例 Oracle 数据库 | `orlracpr` |



| 策略管理的 Oracle RAC 实例 | `orlracpr_1` |
| 管理员管理的 Oracle RAC 实例 | `orlracpr1` |

### 2.11 使用 Oracle Universal Installer 安装 Oracle RAC

要安装带有 Oracle RAC 的 Oracle Database 软件：

1. 确保您可以通过 SSH 访问其他节点。OUI 要求运行 Oracle RAC 安装的用户帐户允许设置无密码 SSH。OUI 可以自动为您设置，或者您的系统管理员可以在安装开始前为您设置。

2. 打开您打算运行 OUI 的终端，并以您希望拥有 Oracle Database 安装的用户帐户登录（例如，`oracle`）。

   如果您无法关闭 `stty` 命令，或者有其他限制会阻止从 OUI 内部自动配置 SSH，那么您必须在继续启动安装程序之前确保 SSH 已配置并启用。

3. 确保您拥有 `su` 或 `sudo` 凭据，因为安装过程中会提示您以 `root` 用户身份运行脚本。

   要使用“软件更新”选项获取最新的系统要求更新、关键补丁更新和其他建议的安装更新，请使用有效的 My Oracle Support 用户名和密码，或在提示时提供已下载的“软件更新”选项包的路径。

4. 从 Oracle Database 11g release 2 (11.2) 安装介质或安装二进制下载区域的 Disk1 启动 `runInstaller` 命令。例如，如果软件二进制下载区域是 `/home/oracle/oraclesw`，请输入以下命令：

   ```
   $ cd /home/oracle/oraclesw/Disk1
   $ ./runInstaller
   ```

5. 当 OUI 提示时，提供信息或以 `root` 身份运行脚本。如果在安装过程中需要帮助，请点击**帮助**。点击**详细信息**查看日志文件。

> **注意：** 对于 Oracle RAC 安装或升级，您可以同时在集群中的所有节点上运行 `root.sh` 脚本。

如果您在安装过程中遇到问题，请检查安装日志文件中记录的 OUI 操作。日志文件位于 Oracle 清单目录中的以下位置：

`OraInventory/logs/installActionsdate_time.log`

> **注意：** 您在数据库安装期间提供的 Oracle 主目录名称和路径*必须与*您在第一阶段 Oracle Grid Infrastructure 安装期间使用的主目录*不同*。您*不得*将 Oracle Database 11g 与 Oracle RAC 软件安装到您已为集群安装 Oracle Grid Infrastructure 的同一主目录中。

请注意，由于 Oracle ASM 是 Oracle Grid Infrastructure 主目录的一部分，因此在 Oracle RAC 安装期间无法对其进行升级。

当您完成安装的第二阶段（也是最后阶段）后，请继续执行[第 4 章，"Oracle Real Application Clusters 安装后过程"]以执行安装后任务。

> **注意：** 安装完成并创建数据库后，如果您决定要在数据库中安装其他 Oracle Database 11g release 2 (11.2) 产品，那么在尝试安装其他产品之前，您必须停止*所有*在 Oracle 主目录中运行的进程。为了使 Oracle Universal Installer 能够重新链接某些可执行文件和库，必须停止所有数据库进程。有关更多信息，请参阅[附录 E，"如何在现有的 Oracle Real Application Clusters 数据库中停止进程"](附录 E，"如何在现有的 Oracle Real Application Clusters 数据库中停止进程")。

以下是关于安装需要注意的附加信息列表：

- 在“选择数据库管理选项”页面上，如果您已完成 Grid Control Management Agent 安装，则可以选择 Grid 或 Local Database control。否则，对于 Oracle RAC 仅支持使用 Local Database control 进行数据库管理。当您使用本地 Database Control 时，可以选择电子邮件选项并输入出站 SMTP 服务器名称和电子邮件地址。

  如果您执行的安装不包括 Oracle Enterprise Manager（例如，不带 Oracle Enterprise Manager 的高级安装软件安装、未配置 Oracle Enterprise Manager 的安装，或使用您自己的脚本创建数据库），那么您可以稍后使用 OUI、DBCA 或 Oracle Enterprise Manager Configuration Assistant (EMCA) 实用程序配置 Oracle Enterprise Manager。

### 2.12 使用 Oracle Universal Installer 安装 Oracle RAC One Node

要安装 Oracle RAC One Node：

1. 打开您打算运行 OUI 的终端，并以您希望拥有 Oracle Database 安装的用户帐户登录（例如，`oracle`）。

   如果您无法关闭 `stty` 命令，或者有其他限制会阻止从 OUI 内部自动配置 SSH，那么您必须在继续启动安装程序之前确保 SSH 已配置并启用。

2. 确保您拥有 `su` 或 `sudo` 凭据，因为安装过程中会提示您以 `root` 用户身份运行脚本。

3. 从 Oracle Database 11g release 2 (11.2) 安装介质或安装二进制下载区域的 Disk1 启动 `runInstaller` 命令。例如，如果软件二进制下载区域是 `/home/oracle/oraclesw`，请输入以下命令：

   ```
   $ cd /home/oracle/oraclesw/Disk1
   $ ./runInstaller
   ```

4. 选择配置 Oracle RAC One Node 数据库，并选择在所有将运行 Oracle RAC One Node 的节点上安装 Oracle RAC。

5. 当 OUI 提示时，提供信息或以 `root` 身份运行脚本。如果在安装过程中需要帮助，请点击**帮助**。点击**详细信息**查看日志文件。

### 2.13 使用 DBCA 配置 Oracle RAC One Node

如果你已选择仅在集群节点上安装 Oracle RAC 软件，可以使用 Oracle 数据库配置助手（DBCA）来配置 Oracle RAC One Node。

> **注意：** 对于 Oracle RAC 安装或升级，你可以同时在集群的所有节点上运行 `root.sh` 脚本。

如果在安装过程中遇到问题，请检查安装日志文件中记录的 OUI 操作。日志文件位于 Oracle 清单目录中的以下位置：

```
OraInventory/logs/installActionsdate_time.log
```

> **警告：** 你在数据库安装过程中提供的 Oracle 主目录名称和路径*必须不同于*你在第一阶段 Oracle Grid Infrastructure 安装时使用的主目录。你*不得*将 Oracle Database 11g 与 Oracle RAC 软件安装到安装 Oracle Grid Infrastructure for a cluster 软件时使用的同一主目录中。

如果你正在升级数据库，则必须使用相同类型的 Oracle 主目录。例如，你不应该从本地 Oracle 主目录更改为共享 Oracle 主目录。

请注意，由于 Oracle ASM 是 Oracle Grid Infrastructure 主目录的一部分，因此它无法在 Oracle RAC 安装过程中进行升级。

安装完成后，启动 DBCA，在欢迎页面上选择**Oracle RAC One Node 数据库**。DBCA 仅在你选择的节点集中的一个节点上启动。你可以稍后向集群添加其他节点。

选择一个节点会将 Oracle RAC One Node 部署在单个节点上。Oracle 建议你选择希望 Oracle RAC One Node 能够故障转移至的所有集群节点。

如果你选择的节点少于两个，或者创建了基数为 2 或更大的服务器池，则 DBCA 会发布一条警告消息，指出你选择的配置将不支持 Oracle RAC One Node 实例的故障转移。

当你创建管理型 Oracle RAC One Node 数据库时，请注意，虽然数据库仅在你安装了二进制文件的节点池中的一个节点上启动，但所有候选服务器都会被放入 Generic 服务器池中。如果这些服务器尚未处于 Generic 或 Free 池中，则这可能会导致停止在候选服务器上运行的资源。

> **另请参阅：** Oracle 技术网络获取有关 Oracle RAC One Node 的更多信息：

> [http://www.oracle.com/technology/products/database/clustering/index.html](http://www.oracle.com/technology/products/database/clustering/index.html)

## 3 使用数据库配置助手创建 Oracle Real Application Clusters 数据库

本章介绍如何在独立模式下使用数据库配置助手（DBCA）来创建和删除 Oracle Real Application Clusters（Oracle RAC）数据库。本章包含以下主题：

- 在 Oracle RAC 中使用数据库配置助手
- 使用数据库配置助手的优势
- 从早期版本自动迁移监听程序
- 为 Enterprise Manager DB Control 设置环境变量
- 验证 DBCA 的要求
- 使用 DBCA 创建 Oracle RAC 数据库
- 使用 DBCA 删除 Oracle RAC 数据库

### 3.1 在 Oracle RAC 中使用数据库配置助手

DBCA 具有以下主要数据库功能：

- 创建和删除数据库
- 添加和删除数据库实例
- 为数据库及其实例设置网络配置
- 在 Oracle Enterprise Manager Grid Control 中注册数据库或配置 Database Control
- 配置数据库选项，例如 Oracle Database Vault
- 启动数据库及其实例

> **注意：** 集群托管服务不再通过 DBCA 管理。请改用 Oracle Enterprise Manager DB Control 中的集群托管服务页面（可从集群数据库可用性页面访问）。有关更多信息，请参阅 *Oracle Real Application Clusters 管理和部署指南*。

#### 另请参阅：

- 第 3-4 页的"使用 DBCA 创建 Oracle RAC 数据库"，了解有关在独立模式下使用 DBCA 的更多信息
- *Oracle Database Net Services 管理员指南* 以解决问题——例如监听程序配置问题——以及获取有关轻量级目录访问协议（LDAP）兼容目录支持的更多信息
- *Oracle Enterprise Manager Real Application Clusters 指南联机帮助*，了解有关使用 Oracle Enterprise Manager 的更多信息

### 3.2 使用数据库配置助手的优势

Oracle 建议你使用 DBCA 来创建 Oracle RAC 数据库，因为预配置数据库会针对服务器参数文件（SPFILE）和自动撤销管理等功能优化你的环境。如果你使用 Oracle ASM 或集群文件系统存储，DBCA 还会配置自动备份，该备份使用快速恢复区。

DBCA 使你能够创建策略管理型和管理型数据库。使用 DBCA，你还可以在数据库创建过程中创建特定于站点的表空间。如果你的数据文件需求与 DBCA 模板提供的不同，请先使用 DBCA 创建数据库，然后再修改数据文件。你还可以在数据库创建过程中运行用户指定的脚本。

DBCA 还会为各种 Oracle 高可用性功能（如集群管理工具）配置你的 Oracle RAC 环境。DBCA 还会启动支持你所定义配置所需的任何数据库实例。

### 3.3 从早期版本自动迁移监听程序

如果你的系统安装了 Oracle Database 10g 或 11g，并且你安装 Oracle Database 11g 第 2 版（11.2）以与 Oracle Database 10.1、10.2 或 11.1 安装共存或对其进行升级，则大多数安装类型会自动将现有 Oracle Database 监听程序迁移到 11g 第 2 版（11.2）Oracle 主目录中。在迁移过程中，它们会使用与现有监听程序相同的 TCP/IP 端口和 IPC 密钥值来配置和启动默认的 Oracle Net 监听程序。

在 Oracle Clusterware 升级期间，默认监听程序（*LISTENER_NODENAME*）已迁移到 Oracle Grid Infrastructure 主目录（Grid 主目录）。DBCA 始终使用默认监听程序。

监听程序迁移过程会停止现有 Oracle 主目录中的监听程序，并在新的 Oracle 主目录中重新启动它。如果数据库使用的是默认监听程序（`LISTENER_NODENAME`），则它会在 Oracle Clusterware 升级过程中由 NETCA 自动迁移到 Oracle Clusterware 主目录。如果数据库使用的是非默认监听程序，则 DBUA 会将非默认监听程序迁移到 Oracle Database 主目录中。

在迁移过程中，客户端应用程序可能无法连接到注册到正在迁移的监听程序的任何数据库。

### 3.4 为 Enterprise Manager DB Control 设置环境变量

在 Oracle Database 的早期版本中，你需要设置 `ORACLE_HOME` 和 `ORACLE_SID` 环境变量来启动、停止和检查 Enterprise Manager 的状态。从 Oracle Database 11g 第 2 版（11.2）及更高版本开始，你需要设置 `ORACLE_HOME` 和 `ORACLE_UNQNAME` 环境变量来使用 Enterprise Manager。例如，在每个节点上，使用以下类似命令为 `oracle` 用户设置这些值，默认 shell 为 Bourne shell，其中 Oracle 主目录为 `/u01/app/oracle`，数据库唯一名称为 `sales`：

```
$ export ORACLE_HOME=/u01/app/oracle/product/11.2/dbhome1
$ export ORACLE_UNQNAME=sales
```

将这些环境变量放在每个集群成员节点的 `oracle` 用户配置文件中，以确保在系统重启后环境变量设置仍然可用。

### 3.5 验证 DBCA 的要求

要使用 DBCA 更改数据库配置，请使用集群验证实用程序（CVU）验证你的系统是否已为配置更改做好准备，使用以下命令语法：

```
/Grid_home/bin/cluvfy stage -pre dbcfg -fixup -n node_list -d Oracle_home [-verbose]
```

在上述语法示例中，变量 `Grid_home` 是 Oracle Grid Infrastructure 主目录，变量 `node_list` 是集群中的节点列表（以逗号分隔），变量 `Oracle_home` 是 OUI 创建或修改数据库的 Oracle 主目录路径。`-fixup` 标志会生成一个修复脚本，可以以 `root` 身份运行该脚本来解决许多操作系统配置任务（如果在运行检查之前这些任务尚未完成）。

例如，要执行检查以确定你的系统是否已为在包含 `node1` 和 `node2` 两个节点的集群上安装带有 Oracle RAC 的 Oracle Database 做好准备，Oracle Grid Infrastructure 主目录路径为 `/u01/app/grid/11.2.0`，Oracle 主目录路径为 `/u01/app/oracle/product/11/db1`，请输入以下命令：

```
$ /u01/app/grid/11.2.0/bin/cluvfy stage -pre dbcfg -fixup -n node1,node2 -d\
/u01/app/oracle/product/11/db1
```

你可以选择 `-verbose` 选项，以便在 CVU 执行系统检查时接收进度更新，以及测试结果的详细报告。

如果 CVU 摘要显示集群验证检查失败，并且你无法通过运行修复脚本解决这些问题，请检查并更正相关的系统配置步骤，然后重新运行测试。

命令 `cluvfy.sh stage -pre dbcfg` 验证以下内容：

- 节点可达性：所有指定节点都可从本地节点访问。
- 用户等价性：所有指定节点上都存在用户等价性。
- 节点连通性：所有指定节点之间通过可用的公共和专用网络接口存在连通性。
- 管理权限：`oracle` 用户在指定节点上具有适当的管理权限，可以创建 Oracle RAC 数据库。

### 3.6 使用 DBCA 创建 Oracle RAC 数据库

要在没有 Oracle ASM 或集群文件系统的单机模式下使用 DBCA 创建数据库，必须已配置共享存储设备。此外，必须已运行 Oracle Net 配置助手 (NETCA) 来配置 Oracle Net `listener.ora` 文件。运行 DBCA 时，不再需要将操作系统环境变量 `ORACLE_HOME` 设置为 Oracle RAC 数据库主目录，或将 `ORACLE_UNQNAME` 设置为数据库唯一名称。

您可以使用 DBCA 从 Oracle 提供的模板或自己创建的模板创建数据库。这些模板包含针对特定类型工作负载优化的设置。

Oracle 为以下两种工作负载类型提供了模板：

- 通用或事务处理



# 数据仓库

对于更复杂的环境，您可以选择**自定义数据库**选项。此选项不使用模板，并会导致更详尽的配置过程，这意味着创建数据库需要更长时间。

单击**显示详细信息**以查看每种数据库类型的配置。选择适合您的数据库将支持的工作负载类型的模板。如果不确定选择哪个，则选择默认的**通用或事务处理**模板。

要启动 DBCA，请以安装所有者帐户（例如，`oracle`）连接到已安装 Oracle RAC 的其中一个节点，将 SSH 密钥加载到内存中，然后从`$ORACLE_HOME/bin`目录输入`dbca`命令。

> **注意：** 在 Oracle RAC 环境中，必须为启动 DBCA 的终端会话将 SSH 密钥加载到内存中。如果执行此操作，则在尝试启动 DBCA 时会收到用户等效性错误。如果系统对 SSH 使用密码短语，则必须提供密码短语才能加载 SSH 密钥。

使用以下命令加载 SSH 密钥：

```
$ exec /usr/bin/ssh-agent $SHELL
$ /usr/bin/ssh-add
```

如果需要，在出现提示时提供密码短语。然后即可启动 DBCA。

启动 DBCA 时，它显示的第一页是 Oracle RAC 的欢迎页面，其中包含选择 Oracle RAC 数据库的选项。仅当启动 DBCA 的 Oracle 主目录是在集群上安装时，DBCA 才会显示此 Oracle RAC 欢迎页面。

如果 Oracle RAC 欢迎页面打开，则按照 DBCA 的提示提供信息。如果需要帮助，请单击**帮助**。

Oracle Clusterware 完整性：Oracle Clusterware 堆栈的所有组件完全运行正常。

`inventory`正确位于目录`/etc/oraInst.loc`中，且`oraInventory`文件未损坏。此外，使用以下 CVU 命令语法执行集群件诊断：`/Grid_home/bin/cluvfy/cluvfy.sh stage -post crsinst -n nodelist`。

例如，挂载点为`/u01/app/grid/11.2.0`，节点为`node1`和`node2`，运行以下命令：

```
$ /u01/app/grid/11.2.0/bin/cluvfy stage -post crsinst -n node1,node2
```

使用 DBCA 时请注意以下重要信息：

- 如果属于集群安装的节点未出现在**节点选择**页面上，请运行`opatch lsinventory`执行库存诊断，并运行 CVU 执行集群件诊断。

- 全局数据库名称长度最多为 30 个字符，且必须以字母字符开头。全局数据库名称的域部分最多为 128 个字符，只能包含字母字符、数字字符以及句点 (.) 字符。

- SID 前缀必须以字母字符开头。

- 您可以使用的 SID 前缀的最大字符数为 8 个字符。DBCA 使用 SID 前缀为每个实例生成唯一的`ORACLE_SID`变量值。

- 在**管理选项**页面上，您可以选择 Oracle Enterprise Manager 监控和管理界面。

- 请注意，对于 Oracle RAC 11g 第 2 版及更高版本，存储管理角色`SYSASM`需要是 OSASM 组的成员。此组可能与 OSDBA 不同，后者成员被授予`SYSDBA`权限。此列表中需要`SYSASM`权限的任务标记为 **SYSASM 权限**。

- **SYSASM 权限：** 要使用快速恢复区，Oracle 建议您创建至少两个独立的 Oracle ASM 磁盘组：一个用于数据库区，一个用于恢复区。Oracle 建议您将数据库区和恢复区放在不同的故障组中。如果已划分管理权限，请让存储管理员设置快速恢复区。

数据库控制始终是一个选项。如果 DBCA 在集群上发现 Grid Control 代理，它还会为您提供使用 Grid Control 的 Enterprise Manager 选项。在数据库控制和 Grid Control 界面之间进行选择。

您可以启用每日备份操作。对于每日备份，您需要输入备份时间以及执行备份操作的操作系统的用户凭据。

从 Oracle RAC 11g 第 11.2.0.2 版及更高版本开始，您无法再通过 DBCA 或 OUI 设置电子邮件通知。

故障组由共享硬件定义，例如两个存储设备之间共享的控制器，或位于同一主轴上的两个磁盘。如果两个存储设备共享可能失效的硬件，导致两个存储设备都不可用，则称这些存储设备处于同一故障组中。

如果不使用 Oracle Oracle，Oracle 建议数据文件和快速恢复区位于 Oracle 主目录之外，在单独的位置，就像独立的 Oracle ASM 故障组一样，这样硬件故障不会影响可用性。

**另请参阅：** *Oracle Database Concepts* 获取有关使用快速恢复区的更多信息，*Oracle Automatic Storage Management Administrator's Guide* 获取有关故障组和高可用性与恢复最佳实践的信息。

- **SYSASM 权限：** 在 **Oracle ASM 磁盘组**页面上，如果看不到要添加的存储设备，请单击**更改磁盘发现路径**以更改 DBCA 用于查找可用存储设备的搜索路径。您可以选择状态为`Candidate`或`Former`（从未在 Oracle ASM 磁盘组中使用过或已不在组中）的存储设备，方法是选中该框。如果您要添加仍具有 Oracle ASM 磁盘头但磁盘组不再使用的存储设备（如果在中止安装后选择存储设备、尝试在不删除磁盘组的情况下进行卸载或其他配置问题，可能会发生这种情况），请使用`Force`命令。

- 在**恢复配置**页面上，如果您使用的是 Oracle ASM 或集群文件系统存储，则还可以在恢复配置页面上选择快速恢复区及其大小。如果您使用的是 Oracle ASM，则快速恢复区默认为 Oracle ASM 磁盘组。如果您使用的是 OCFS2，则快速恢复区默认为`$ORACLE_BASE/flash_recovery_area`。

- 在**初始化参数**页面上，如果您在 Linux 系统上安装，请注意 **内存大小 (SGA 和 PGA)**（设置初始化参数`MEMORY_TARGET`或`MEMORY_MAX_TARGET`）不能大于操作系统上的共享内存文件系统。

例如，如果系统上的共享内存文件系统分配为 1 GB，但您将内存大小 (`MEMORY_TARGET`) 设置为 2 GB，则在数据库启动期间会收到以下错误：

```
ORA-00845: MEMORY_TARGET not supported on this system
ORA-01078: Failure in processing system parameters
```

此问题与其他平台无关。

对于所有平台，如果您打算在集群中添加的节点数量多于当前 DBCA 会话期间拥有的数量，请单击**所有初始化参数**，并将参数`CLUSTER_DATABASE_INSTANCES`更改为计划添加到集群的节点总数。

此外，如果您单击**所有初始化参数**，请注意，如果全局数据库名称长于 8 个字符，则数据库名称值（在`DB_NAME`参数中）将被截断为前 8 个字符，`DB_UNIQUE_NAME`参数值将设置为全局名称。

**另请参阅：** *Oracle Database Administrator's Reference for Linux and UNIX-Based Operating Systems* 获取有关初始化参数的信息。

响应 DBCA 提示后，查看摘要对话框信息并单击 **确定**，DBCA 将执行以下操作：

- 创建可运行的 Oracle RAC 数据库及其实例

- 创建 Oracle RAC 数据字典视图

- 为集群数据库配置网络

- 将以前版本的 Oracle Database 监听器及相关文件迁移到 Oracle Database 11g Oracle 主目录

## 3.7 使用 DBCA 删除 Oracle RAC 数据库

本节介绍如何使用 DBCA 删除 Oracle RAC 数据库。此过程会删除数据库并移除数据库的初始化参数文件、实例、OFA 结构以及 Oracle 网络配置。但是，如果数据文件位于原始设备或原始分区上，则此过程不会删除这些数据文件。

使用 DBCA 删除数据库：

1. 在其中一个节点上启动 DBCA。

   - 从`$ORACLE_HOME/bin`目录运行`dbca`命令。

   - DBCA 欢迎页面将显示。

2. 选择**Oracle Real Application Clusters**，然后点击**下一步**。

   - 点击**下一步**后，DBCA 将显示操作页面。

3. 选择**删除数据库**，然后点击**下一步**。DBCA 将显示集群数据库列表页面。

4. 如果您的用户 ID 和密码未经操作系统身份验证，则集群数据库列表页面将显示用户名和密码字段。如果出现这些字段，请输入具有`SYSDBA`权限的用户帐户的用户 ID 和密码。

5. 选择要删除的数据库，然后点击**完成**。

   - 点击**完成**后，DBCA 将显示一个对话框，确认 DBCA 将要删除的数据库和实例。

6. 点击**确定**开始删除数据库及其关联的文件、服务和环境设置，或点击**取消**停止操作。

点击**确定**后，DBCA 将继续操作并删除该数据库的所有关联实例。DBCA 还会移除参数文件、密码文件和`oratab`条目。

至此，您已完成以下操作：

- 从集群中删除了所选数据库

- 删除了分配给该数据库的高可用性服务

- 删除了该数据库的 Oracle Net 配置

- 取消配置了该数据库的 Database Control

- 从集群中删除了该数据库的 OFA 目录结构

- 如果数据文件不在原始设备上，则删除了这些数据文件

# Oracle Real Application Clusters 安装后操作流程

本章介绍在安装带有 Oracle Real Application Clusters（Oracle RAC）软件的 Oracle Database 11g 第 2 版（11.2）后，如何完成安装后任务。本章包含以下主题：

- 必需的安装后任务

- 推荐的安装后任务

- Oracle RAC 的 Oracle Configuration Manager 安装后配置

- 安装后启用和禁用数据库选项

> **注意：** 本章仅介绍基本配置。有关更详细的配置和调优信息，请参阅 *Oracle Database Administrator's Guide* 以及产品管理和调优指南。另请参阅适用于您平台的 *Oracle Database Installation Guide*，了解其他安装后配置信息。

## 4.1 必需的安装后任务

完成安装后，请执行以下任务：

- 下载并安装补丁更新

- 在 HP-UX 上为安装设置外部作业所有权

- 配置 Oracle 产品

- 使用符号链接从 OCFS2 重新定位实例相关的内存映射文件

### 4.1.1 下载并安装补丁更新

请参阅 My Oracle Support 网站，获取适用于您安装的必需补丁更新。

> **注意：** 浏览器需要 Adobe Flash 插件 9.0.115 或更高版本才能使用 My Oracle Support。请访问 Adobe Flash 检查页面，检查您的浏览器是否安装了正确版本的 Flash 插件，并安装最新版本的 Adobe Flash。

如果您尚未安装 Flash，请从 Adobe 网站下载最新版本的 Flash Player：

```
http://www.adobe.com/go/getflashplayer
```

下载必需的补丁更新：

1. 使用 Web 浏览器访问 My Oracle Support 网站：

   ```
   https://support.oracle.com
   ```

2. 登录 My Oracle Support。

> **注意：** 如果您不是 My Oracle Support 注册用户，请点击**注册 My Oracle Support**进行注册。

3. 在 My Oracle Support 主页面上，点击**补丁程序和更新**。

4. 在补丁程序部分，点击**简单搜索**。

5. 指定以下信息，然后点击**执行**：

   - 在**搜索依据**字段中，选择**产品或系列**，然后指定 RDBMS Server。

   - 在**版本**字段中，指定当前版本号。

   - 在**补丁程序类型**字段中，指定 Patchset/Minipack。

   - 在**平台或语言**字段中，选择您的平台。

6. 在结果列表中，找到 Oracle Database 的最新补丁集。

   - Oracle 数据库的补丁集在描述列中标识为 Product:Patchset x.x.x.x PATCH SET FOR ORACLE DATABASE SERVER。

7. 在补丁程序列中，点击您要下载的补丁程序编号。

8. 在补丁集页面上，点击**查看 README**并阅读显示的页面。README 页面包含有关补丁集的信息以及如何将补丁程序应用到您的安装。

9. 返回补丁集页面，点击**下载**，并将文件保存在您的系统上。

10. 使用 Oracle Database 11g 第 2 版（11.2）提供的 unzip 实用程序，解压缩从 My Oracle Support 下载的 Oracle 补丁更新。unzip 实用程序位于`$ORACLE_HOME/bin`目录中。

### 4.1.2 在 HP-UX 上为安装设置外部作业所有权

仅在 HP-UX 平台上，请完成以下过程，将外部作业所有权设置为低权限用户`extjob`：

1. 以 root 身份登录。

2. 切换到 Oracle Database Oracle 主目录：

```
# cd $ORACLE_HOME/rdbms/admin/
```

3. 停止 Oracle Database 实例。

4. 将`$ORACLE_HOME/dbs/*.dat`文件移动到本地文件系统上的目录。

5. 从`$ORACLE_HOME/dbs`目录创建指向本地文件系统上`*.dat`文件的符号链接。

6. 重新启动 Oracle Database 实例。

## 4.2 推荐的安装后任务

Oracle 建议您在安装 Oracle RAC 后完成以下任务：

- 备份 root.sh 脚本

- 设置 Oracle 用户环境变量

- 重新编译所有 PL/SQL 模块

- 设置其他用户帐户

- 运行 Oracle RAC 配置审计工具

### 4.2.1 备份 root.sh 脚本

Oracle 建议您在完成安装后备份`root.sh`脚本。如果您在同一 Oracle 主目录中安装其他产品，Oracle Universal Installer（OUI）会在安装过程中更新现有`root.sh`脚本的内容。如果您需要原始`root.sh`脚本中包含的信息，可以从`root.sh`文件副本中恢复。

### 4.2.2 设置 Oracle 用户环境变量

在每个节点上，在安装所有者用户配置文件中（在本示例中为`oracle`），设置环境变量`ORACLE_BASE`和`ORACLE_HOME`以及`ORACLE_SID`；同时将`ORACLE_HOME/bin`添加到 path 环境变量中。

例如：

```
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=/u01/app/oracle/11.2.0/dbhome_1
export PATH=$PATH:$ORACLE_HOME/bin
export ORACLE_SID=sales1
```

如果未设置环境变量`ORACLE_HOME`和`ORACLE_SID`，并且您尝试使用 SQL*Plus 或其他工具，则会收到一条错误消息，要求您设置这些变量。

### 4.2.3 重新编译所有 PL/SQL 模块

Oracle 建议您在创建或升级数据库后运行`utlrp.sql`脚本。此脚本会重新编译所有可能处于无效状态的 PL/SQL 模块，包括包、过程和类型。这是一个可选步骤，但 Oracle 建议您在安装后立即执行，而不是在以后执行。

1. 完成 Oracle 软件所有者用户帐户环境的设置（例如`oracle`），如前一节中的"[设置 Oracle 用户环境变量](#)"所述。

2. 启动 SQL*Plus，如下所示：

   ```
   $ sqlplus "/ AS SYSDBA"
   ```

3. 运行`utlrp.sql`脚本，其中`Oracle_home`是 Oracle 主目录路径：

   ```
   SQL> @Oracle_home/rdbms/admin/utlrp.sql
   ```

### 4.2.4 设置其他用户帐户

有关设置其他可选用户帐户的信息，请参阅 *Oracle Database 11g Administrator's Guide for UNIX Systems*。

完成这些操作后，您就可以执行[第 5 章"在 Oracle Real Application Clusters 环境中配置服务器参数文件"](#)中描述的初始配置任务。

### 4.2.5 运行 Oracle RAC 配置审计工具

Oracle 建议您运行 Oracle RAC 配置审计工具（RACcheck）来检查您的 Oracle RAC 安装。RACcheck 是一个 Oracle RAC

## 4.3 Oracle Configuration Manager 在 Oracle RAC 上的安装后配置

如果您已安装 Oracle Configuration Manager，则必须运行一个脚本来创建数据库账户，以收集数据库配置信息集合。您必须在**连接**和**断开**两种模式下都创建此账户。该数据库账户存储用于收集配置信息的 PL/SQL 过程，并拥有执行收集操作的数据库管理系统作业。账户设置完成后，该账户将被锁定，因为不再需要登录权限。

要为配置收集配置数据库，请运行以下脚本：



`$ORACLE_HOME/CCR/admin/scripts/installCCRSQL.sh collectconfig -s SID -r SYSDBA-USER -p SYSDBA-PASSWORD`

脚本`installCCRSQL.sh`会创建一个 Oracle Configuration Manager 用户，并将 PL/SQL 过程加载到由`ORACLE_SID`定义的数据库中。您也可以在命令行中使用`-s`选项指定数据库 SID，如下例所示，其中 SID 为`orcl`：

`$ORACLE_HOME/CCR/admin/scripts/installCCRSQL.sh collectconfig -s orcl`

对于 Oracle RAC，您只需针对一个实例运行数据库脚本，例如执行安装的本地实例。但是，Oracle Configuration Manager 必须安装在所有实例主目录中。

**另请参阅：**

- *Oracle Configuration Manager 安装和管理指南* 了解更多信息

- *Oracle Database Vault 管理员指南* 了解其他配置任务

### 4.4 安装后启用和禁用数据库选项

安装 Oracle Database 时，某些选项会被启用，而其他选项则被禁用。要为某个 Oracle 主目录启用或禁用特定的数据库功能，请关闭数据库并使用`chopt`工具。

`chopt`工具是一个位于`ORACLE_HOME/bin`目录中的命令行实用程序。它使用以下语法，其中`db_option`是您要修改其状态的选项：

`chopt [enable | disable] db_option`

`db_option`的可能值如表 4–1 所述：

#### 表 4–1 数据库选项的 Chopt 工具命令选项

| 值 | 描述 |

| :--- | :--- |

| `dm` | Oracle Data Mining 数据库文件 |

| `dv` | Oracle Database Vault |

| `lbac` | Oracle Label Security |

| `olap` | Oracle OLAP |

| `partitioning` | Oracle 分区 |

| `rat` | Oracle Real Application Testing |

| `ode_net` | Oracle Database Extensions for .NET 1.x |

| `ode_net_2` | Oracle Database Extensions for .NET 2.0 |

#### 示例 4–1 如何使用 Chopt 启用数据库选项

在此示例中，`chopt`工具用于在数据库`oradb1`中启用 Oracle Label Security：

```
$ cd $ORACLE_HOME/bin
$ srvctl stop database -d oradb1
$ chopt enable lbac
$ srvctl start database -d oradb1
```

## 5 在 Oracle Real Application Clusters 环境中配置服务器参数文件

本章描述在 Oracle Real Application Clusters 环境中服务器参数文件的位置和配置。本章包含以下主题：

- 参数文件与 Oracle RAC

- 在 Oracle RAC 中使用服务器参数文件

- Oracle RAC 中的参数文件搜索顺序

- 在 Oracle RAC 环境中迁移到 SPFILE

- Oracle RAC 中的服务器参数文件错误

**另请参阅：** *The Oracle Real Application Clusters Administration and Deployment Guide* 了解关于参数的更多信息，以及对 Oracle RAC 数据仓库环境中并行执行相关参数的讨论

### 5.1 参数文件与 Oracle RAC

Oracle 数据库使用参数文件中的参数设置来确定如何控制各种数据库资源。您可以使用两种类型的文件进行参数管理：服务器参数文件或一个或多个传统的客户端参数文件。

Oracle 建议您使用 SPFILE 管理参数。如果您使用客户端参数文件，那么在关闭数据库后，Oracle 不会保留为自调优所做的参数更改。

### 5.2 在 Oracle RAC 中使用服务器参数文件

默认情况下，Oracle 数据库为每个节点基于一个 SPFILE 创建`init`参数文件。您可以仅使用 Oracle 企业管理员或`ALTER SYSTEM SET` SQL 语句更改 SPFILE 文件中的参数设置，因为服务器参数文件是一个二进制文件。请勿尝试手动编辑此文件。

> **注意：** Oracle 建议您避免修改自调优参数的值；覆盖这些设置可能会对性能产生不利影响。

如果您是从早期的 Oracle 数据库版本升级，请查看以下关于 Oracle RAC 服务器参数文件的部分。

#### 5.2.1 关于服务器参数文件

对于 Oracle Database 11g 第 2 版及更高版本，数据库代理会自动维护 SPFILE，其值基于您在`srvctl`命令`srvctl add/modify -p spfile`中指定的值，其中`spfile`是 SPFILE 的名称。您无需创建或维护`initORACLE_SID.ora`文件。

服务器参数文件的默认位置位于以下路径：

`$ORACLE_HOME/dbs/spfile$ORACLE_SID.ora`

如果您在节点上使用存储，则服务器参数文件的默认位置对于 Oracle RAC 数据库和 Oracle ASM 实例是不合适的，因为所有实例必须使用相同的服务器参数文件。

相反，Oracle 建议您在此目录中使用 PFILE：

`$ORACLE_HOME/dbs/init$ORACLE_SID.ora`

此路径对每个实例都有效，它指向一个共享的初始化参数文件。例如，如果您使用 NFS 存储，那么在 Linux 或 UNIX 系统上，该文件应包含类似于以下内容的条目：

`SPFILE='/nfs/db/oracle_dg/dbspfile'`

但是，如果您使用集群文件系统，则使用以下文件位置：

在基于 Linux 和 UNIX 的系统上：

`SPFILE='/shared_mount/dbname/spfiledbname.ora'`

在此语法示例中，变量`shared_mount`是共享挂载点，变量`dbname`是数据库名称。

要使用 DBCA 创建数据库并使用服务器参数文件，请启动 DBCA。当出现初始化参数页时，在“文件位置”选项卡下选择 **创建服务器参数文件**。做出此选择后，在 **服务器参数文件名** 字段中输入共享文件系统文件名或存储路径。

> **注意：** 使用 DBCA 创建服务器参数文件时，默认的`SPFILE`文件名为`$ORACLE_HOME/dbs/init$ORACLE_SID.ora`。

### 5.3 Oracle RAC 中的参数文件搜索顺序

Oracle 数据库按以下顺序搜索您的参数文件：

1. `$ORACLE_HOME/dbs/spfilesid.ora`

2. `$ORACLE_HOME/dbs/spfile.ora`

3. `$ORACLE_HOME/dbs/initsid.ora`

### 5.4 在 Oracle RAC 环境中迁移到 SPFILE

通过使用本节中描述的过程创建和编辑服务器参数文件来迁移到 SPFILE。本节包含以下主题：

- Oracle RAC 中的服务器参数文件位置

- 迁移到服务器参数文件的过程

#### 5.4.1 Oracle RAC 中的服务器参数文件位置

对于单节点群集配置，或者如果您使用 Oracle ASM 磁盘组或集群文件系统，请将服务器参数文件放在 Oracle ASM 磁盘组或文件系统上。否则，请将服务器参数文件放在大小至少为 5 MB 的共享原始设备上。

#### 5.4.2 迁移到服务器参数文件的过程

通过完成以下过程迁移到 SPFILE 文件：

1. 通过按原样复制所有共享的`IFILE`内容，将所有实例的初始化参数文件合并到一个`initdbname.ora`文件中，其中`dbname`是数据库名称。您在`IFILE`参数文件中定义的所有参数都是全局的。因此，以`parameter=value`的格式创建它们，不要使用`SID`前缀。

2. 使用以下语法从`initsid.ora`文件复制所有特定于实例的参数定义，其中变量`sid`是实例的`SID`：

   `sid.parameter=value`

3. 如果您使用集群文件系统，Oracle 建议您使用以下命令定义新 SPFILE 的位置，其中`spfile`是 SPFILE 的名称：

   `srvctl modify database -p spfile`

   您也可以使用`CREATE SPFILE`语句创建服务器参数文件，如下例所示：

   `CREATE SPFILE='?/dbs/spfile_dbname.ora'`

   `FROM PFILE='?/dbs/initdbname.ora'`

   如果您使用 Oracle ASM，则可以使用以下语法创建服务器参数文件，其中`disk_group_name`是磁盘组名称，`db_uniquename`是数据库名称，`dbname`是数据库名称，`Oracle_home`是 Oracle 主目录路径：

   `CREATE SPFILE='+disk_group_name/db_uniquename/spfiledbname.ora'`

   `FROM PFILE='Oracle_home/dbs/initdbname.ora'`

   这些语句读取您通过合并 IFILE 创建的合并后的`initdbname.ora`文件，然后将合并文件中的参数设置传输到您的服务器参数文件中。

4. Oracle 建议您使用`SPFILE`，并使用`PFILE`作为指向`SPFILE`的指针。通过运行`STARTUP`命令来完成此操作，如下例所示，其中文件`initsid.ora`中的`SID`变量`sid`是您在步骤 3 的`SPFILE`条目中使用的`SID`。例如：

   `STARTUP PFILE=$ORACLE_HOME/dbs/initsid.ora`

如果使用此`STARTUP`命令语法，Oracle 数据库将使用`initsid.ora`文件中指定的服务器参数文件条目。

> **注意：** 从 Oracle ASM 11g 第 2 版及更高版本开始，Oracle ASM 实例的`SPFILE`可以存储在 Oracle ASM 中。你也可以将 Oracle ASM 实例的`SPFILE`放置在文件系统上，或者为每个 Oracle ASM 实例使用传统的客户端参数文件。

> **另请参阅：** 《*Oracle 自动存储管理管理员指南*》以获取有关管理 Oracle ASM 实例的更多信息。

### 5.5 Oracle RAC 中的服务器参数文件错误

Oracle 数据库会报告在创建服务器参数文件期间或启动时读取文件期间发生的错误。如果在参数更新期间发生错误，Oracle 会将错误记录在`ALERT.LOG`文件中，并忽略后续对该文件的参数更新。如果发生这种情况，请执行以下任一操作：

- 关闭实例，恢复服务器参数文件，然后重新启动实例。

- 允许实例继续运行，无需理会后续的参数更新。

当你错误地使用`ALTER SYSTEM SET`语句尝试进行参数更改时，Oracle 数据库会显示错误。当从服务器参数文件读取或写入时发生错误时，Oracle 数据库会执行此操作。

> **另请参阅：** 《*Oracle Real Application Clusters 管理和部署指南*》以获取有关备份`SPFILE`的更多信息。

## 6 配置服务器池和 Oracle Enterprise Manager Database Control

本章介绍 Oracle Real Application Clusters（Oracle RAC）环境中的服务器池和 Oracle Enterprise Manager Database Control 配置。本章包含以下主题：

- 了解服务器池

- 在安装期间和之后配置 Database Control

### 6.1 了解服务器池

服务器池是将集群逻辑划分为服务器池，用于托管数据库或其他应用程序。服务器池使用`crsctl`和`srvctl`命令进行管理。

> **注意：** 默认情况下，任何命名用户都可以创建服务器池。为了限制拥有此权限的操作系统用户，Oracle 强烈建议你将特定用户添加到 CRS 管理员列表中。

> **另请参阅：** 《*Oracle Clusterware 管理和部署指南*》以获取有关将用户添加到 CRS 管理员列表的更多信息。

每个服务器池名称在集群中必须是唯一的。两个服务器池不能使用相同的名称。

服务器池管理有两种类型：

- **管理员管理**：数据库管理员定义运行数据库资源的服务器，并根据需要手动放置资源。这是以前版本中使用的管理策略。

- **策略管理**：数据库管理员指定数据库资源将在哪个服务器池（不包括 generic 或 free）中运行。Oracle Clusterware 负责将数据库资源放置在服务器上。

服务器池名称是必需属性。你还可以为以下属性提供值；如果未指定，则将设置为默认值：

- **MIN_SIZE**：你希望资源运行在其上的最少服务器数量。默认值为 0。

- **MAX_SIZE**：你希望资源运行在其上的最大服务器数量。默认值为 -1，表示资源可以在集群中的所有可用节点上运行。

- **IMPORTANCE**：资源池的相对重要性，用于确定在节点加入或离开集群时如何重新配置服务器。默认值为 0。

> **注意：** 建议使用 Oracle Database 11g 第 2 版及更高版本数据库的策略管理服务器池的客户端通过单客户端访问名（SCAN）访问数据库。强烈建议使用 SCAN，因为策略管理数据库的实例可以在不同时间运行在不同的服务器上；使用虚拟 IP（VIP）地址连接到策略管理数据库的特定节点或实例是不可能的。

#### 6.1.1 Oracle RAC One Node 和服务器池

关于 Oracle RAC One Node 和服务器池，请注意以下几点：

- Oracle RAC One Node 仅在一个服务器池中运行。此服务器池的处理方式与其他任何服务器池相同。

- Oracle RAC One Node 数据库实例的在线重定位允许将 Oracle RAC One Node 数据库从一个节点计划迁移到另一个节点。重定位必须始终在服务器池内进行。

- 通过 WLM 集成，Oracle RAC One Node 数据库实例的在线重定位操作不会从重要性设置为较低值的服务器池中移除服务器，因为目标服务器必须已经位于该服务器池中，或位于 Free 中。

- Oracle RAC One Node 数据库可以是 Data Guard 物理备用数据库。

#### 6.1.2 基于策略的集群和容量管理

使用基于策略的服务器池管理，数据库管理员定义工作负载的资源需求，包括以下内容：

- 定义应用程序首选的服务器或实例数量。Oracle Clusterware 会自动分配资源，直到达到指定的数量（只要它们在物理上可用），并在必要时将资源重定位到另一个节点。

- 定义支持应用程序所需的实例数量。

资源不再定义为属于特定实例或节点。取而代之的是定义资源需求的优先级。

**另请参阅：** 《*Oracle Real Application Clusters 管理和部署指南*》

### 6.2 在安装期间和之后配置 Database Control

以下各节介绍如何在 Oracle RAC 安装期间配置 Oracle Enterprise Manager Database Control，以及如何在安装后配置 Database Control：

- 了解在 Oracle RAC 中使用 EMCA

- 在安装期间配置 Database Control

- 使用 DBCA 配置 Database Control

- 使用 EMCA 在安装后配置 Database Control

- 使用输入文件设置 EMCA 参数

- 指定 Database Control 使用的端口

- EMCA 故障排除提示

#### 6.2.1 了解在 Oracle RAC 中使用 EMCA

每个 EMCA 命令都可在 Oracle RAC 环境中使用，某些命令仅适用于集群配置。要执行 EMCA 集群命令，请使用几乎在所有 EMCA 操作模式中都可用的`-cluster`标志。

当你使用 EMCA 为 Oracle RAC 配置 Database Control 时，你为集群中的每个实例配置 Database Control。但是，默认情况下，Database Control 控制台仅在本地节点上启动。在集群的每个其他节点上，仅启动 Enterprise Manager 代理。这是因为 Database Control 控制台会打开大量到数据库的连接。如果集群中每台主机上都运行一个控制台实例，那么在 32 节点或 64 节点环境中，你很容易超过允许的最大打开连接数。

当 Database Control 控制台在本地节点上启动时，在每个其他节点上，`emctl start dbconsole`和`emctl stop dbconsole`命令仅启动和停止代理。每个远程代理将其各自的数据上传到在本地节点上运行的控制台，在那里你可以监视和管理集群中的所有目标。在 Oracle RAC 数据库的每个实例上，将创建以下子目录，其中`nodename`是集群中节点的名称，`DBUniqueName`是数据库唯一名称。



`$ORACLE_HOME/nodename_DBUniqueName`

但是，请注意，如果你将配置了 Database Control 的现有 Oracle RAC 10g 第 1 版数据库升级到当前版本，则会保留现有的 Database Control 配置。现有的 Database Control 在每个集群节点上都有一个 Database Console 运行。该控制台仍将在每个单独的节点上启动。

如果你想修改现有配置，请使用以下命令：

```
emca -reconfig dbcontrol -cluster -EM_NODE nodename -EM_NODE_LIST NODE_list
```

其中`nodename`是节点的公共名称，`NODE_list`是以逗号分隔的节点列表。此命令重新配置当前的 Database Control 设置，并按顺序执行以下操作：

1. 如果尚未启动，则在`nodename`上启动 Database Control 控制台。
2. 重定向监视`NODE_list`中数据库实例的代理，使其将数据上传到在`nodename`上运行的控制台。同样，监视`nodename`上数据库实例的代理也将数据上传到本地控制台。请注意，如果未在命令行输入命令选项`-EM_NODE`或`-EM_NODE_LIST`，系统将提示你输入。

`-EM_NODE`在提示时如果未指定，则默认为本地节点。如果未指定，`-EM_NODE_LIST`默认为配置了数据库的所有节点。

使用此命令可在多个节点上启动控制台。例如，在一个包含`node1`、`node2`、`node3`、`node4`、`node5`、`node6`、`node7`和`node8`节点的八节点集群上，您可以依次运行以下命令：

```
$ emca -reconfig dbcontrol -cluster -EM_NODE node1 -EM_NODE_LIST node2,node3,node4
$ emca -reconfig dbcontrol -cluster -EM_NODE node5 -EM_NODE_LIST node6,node7,node8
```

在此场景中，有两个 Database Control 控制台在运行，一个在`node1`上，另一个在`node5`上。从任一控制台中，您都可以管理和监控集群中的所有目标。

要获取有关当前集群配置的信息，您可以运行以下命令：

```
$ emca -displayConfig dbcontrol -cluster
```

> **注意：** 如果您使用`emca -cluster`命令为 Oracle RAC 配置 Database Control，请检查所有集群节点上的`TNS_ADMIN`环境变量。如果每个节点设置了不同的`TNS_ADMIN`，则无法正确配置目标的监听程序。在这种情况下，请在运行`emca -cluster`命令之前，在所有集群节点上设置相同的`TNS_ADMIN`。

要为集群新添加的节点配置 Enterprise Manager，请使用以下命令：

```
$ emca -addNode db
```

在策略管理的数据库上，另一个常见操作是添加和删除集群节点。添加新节点后，您可以运行 EMCA 来使用`emca -addNode db`命令为该节点配置 Database Control 或中央代理管理。运行 EMCA 仅配置 Enterprise Manager，使您能够以与集群中其他数据库实例一致的方式管理该实例。

为新节点配置 Enterprise Manager 时，请仅在添加节点之后运行 EMCA 命令。此外，请从集群中已配置了 Enterprise Manager 的节点运行该命令，因为在运行命令时，现有节点上的 Enterprise Manager 配置设置会传播到新节点。由于`-addNode`选项只能在 Oracle RAC 环境中使用，因此您无需在命令行上使用`-cluster`选项。

运行`emca -addNode db`命令后，输入该节点和数据库的节点名称和数据库唯一名称。例如：

```
Node name: node2
Database Unique Name: EM102
```

要从集群中删除某个特定节点并取消其 Enterprise Manager 配置，请登录到与您计划删除的节点不同的节点，并使用`emca -deleteNode db`命令。运行此命令将移除 Enterprise Manager 配置，这样您将无法再在该节点上通过 Enterprise Manager 管理实例。确保在删除集群节点之前运行 EMCA 命令。由于此选项只能在 Oracle RAC 环境中使用，因此您无需在命令行上使用`-cluster`选项。

### 6.2.2 在安装过程中配置 Database Control

如果您在安装 Oracle RAC 11g 第 2 版 (11.2) 时创建数据库，您可以选择配置数据库，使其可通过 Oracle Enterprise Manager 10g Grid Control 控制台或 Oracle Enterprise Manager 11g Database Control 控制台进行管理。

要选择 Grid Control 控制台作为管理选项，必须在网络主机上安装 Oracle Management Service。此外，必须在安装数据库的主机上安装 Oracle Management Agent。否则，Grid Control 控制台选项将不可用，您必须改用 Database Control 来管理数据库。

对于大多数 Oracle RAC 11g 第 2 版 (11.2) 安装类型，在安装过程中创建数据库时，您必须选择 Database Control 或 Grid Control 作为管理选项。

但是，如果您使用以下方法之一创建数据库，则可以选择不配置 Database Control：

- 在企业版或标准版安装过程中选择高级数据库配置选项
- 在安装后运行数据库配置助手 (DBCA)

如果您在 Oracle RAC 11g 第 2 版 (11.2) 安装过程中未配置 Database Control，则生成的 Oracle 主目录中不会创建`hostname_dbuniquename`目录。

### 6.2.3 使用 DBCA 配置 Database Control

配置现有 Oracle Database 11g 第 2 版 (11.2) 数据库以使用 Database Control 进行管理的主要方法是使用 DBCA。您可以使用 DBCA 创建新数据库或重新配置现有数据库。

> 另请参阅：*Oracle Database 2 Day DBA 联机帮助*中的"安装 Oracle 软件并构建数据库"，了解有关使用 DBCA 创建新数据库实例的更多信息，以及 *Oracle Enterprise Manager Real Application Clusters 指南联机帮助* 中有关使用 DBCA 的 Oracle RAC 示例。

要使用 DBCA 重新配置数据库以使用 Database Control 进行管理：

1. 以有权安装 Oracle 软件并创建和运行数据库的管理组成员身份登录数据库主机。
2. 启动 DBCA 并切换到`ORACLE_HOME/bin`目录，然后输入以下命令：

   ```
   $ ./dbca
   ```

   DBCA 欢迎页面出现。

3. 转到操作页面并选择**配置数据库选项**。
4. 转到数据库页面并选择要配置的数据库。
5. 转到管理选项页面并选择以下选项：

   - **使用 Enterprise Manager 配置数据库**
   - **使用 Database Control 进行数据库管理**

6. 可选地，选择启用电子邮件通知和启用每日备份的选项。

   有关 Enterprise Manager 通知和每日备份的更多信息，请在管理选项页面上单击**帮助**。

7. 继续前进，直到**完成**按钮可用。
8. 单击**完成**以重新配置数据库，使其使用 Database Control。

   DBCA 重新配置数据库后，Oracle 主目录中会出现一个新的子目录。该目录使用以下格式命名，并包含刚配置的数据库特定的 Database Control 配置和状态文件：

   `hostname_dbuniqueName`

   请注意，对于集群数据库，目录命名为`nodename_dbuniqueName`。

   例如：

   `mycluster1.example.com_myNewDB`

### 6.2.4 安装后使用 EMCA 配置 Database Control

当您使用 DBCA 配置 Oracle RAC 11g 第 2 版 (11.2) 时，DBCA 提供图形用户界面来帮助您选择 Database Control 选项并配置数据库的其他方面。但是，如果您想使用操作系统命令行配置 Database Control，则可以使用 Enterprise Manager Configuration Assistant (EMCA)。

> **注意：** 在使用 EMCA 配置 Database Control 的过程中，数据库可能会变得不可用，用户可能无法连接到数据库或对数据库执行操作。

要使用 EMCA 配置 Database Control：

1. 设置`ORACLE_HOME`环境变量以指定要管理的数据库的 Oracle 主目录。
2. 切换到`ORACLE_HOME/bin`目录。
3. 输入以下命令并附带表 6-1 中所示的任何可选命令行参数来启动 EMCA：

   ```
   $ ./emca
   ```

根据您在 EMCA 命令行中包含的参数，EMCA 会提示您输入配置 Database Control 所需的信息。

例如，输入以下命令来配置 Database Control，使其自动执行数据库的每日备份：

```
$ ./emca -config dbcontrol db -backup
```

EMCA 命令的格式为：

```
emca [operation] [mode] [flags] [parameters]
```

**注意：** 要为使用 Oracle ASM 的单实例数据库配置 Database Console，您无需使用 EMCA 命令提供额外参数。运行以下命令来配置 Database Console，它将自动检测 Oracle ASM 实例：

```
emca -config dbcontrol db -repos create
```

表 6-1 描述了有效的执行操作和模式，并列出了方括号中的可选参数。表 6-2 介绍了标志及其行为，表 6-3 则详细定义了可选参数。EMCA 参数的格式为`[-parameterName parameterValue]`。多个参数可以在命令行上组合使用。

#### 表 6-1 EMCA 命令行操作

| 命令 | 说明 |
|---------|-------------|
| `emca -h \| --h \| -help \| --help` | 使用此选项显示 EMCA 实用程序的帮助消息。列出了表 6-1、表 6-2 和表 6-3 中描述的选项以及您可以包含的有效参数。 |
| `emca -version` | 打印与 EMCA 关联的版本信息。 |
| `emca -config dbcontrol db [-repos (create \| recreate)] [-cluster] [-silent] [-backup] [parameters]` | 为数据库配置 Database Control。选项包括创建（或重新创建）Database Control 存储库、配置自动备份，以及在集群数据库上执行这些操作。 |
| `emca -config centralAgent (db \| asm) [-cluster] [-silent] [parameters]` | 为数据库或 Oracle Automatic Storage Management (ASM) 实例配置中央代理管理。选项包括在集群环境中执行此操作。此操作将配置数据库，使其可以通过 Oracle Enterprise Manager 10g Grid Control 控制台进行集中管理。要使用此选项，您必须事先在网络主机上安装 Enterprise Manager 的 Oracle Management Service 组件。此外，必须在运行数据库的主机上安装 Oracle Management Agent。 |
| `emca -config all db [-repos (create \| recreate)] [-cluster] [-silent] [-backup] [parameters]` | 为数据库同时配置 Database Control 和中央代理管理。可能的配置选项与上述类似。 |
| `emca -deconfig dbcontrol db [-repos drop] [-cluster] [-silent] [parameters]` | 取消数据库的 Database Control 配置。选项包括删除 Database Control 存储库以及在集群数据库上执行这些操作。例如，您可能需要使用此命令从计划删除的数据库中移除 Database Control 配置。在此类场景中，请在物理删除数据库之前移除 Database Control 配置。此操作不会删除实际的数据库或其数据文件。 |
| `emca -deconfig centralAgent (db \| asm) [-cluster] [-silent] [parameters]` | 取消数据库或 Oracle ASM 实例的中央代理管理配置。选项包括在集群环境中执行此操作。例如，您可能需要使用此命令从计划删除的数据库中移除中央代理管理配置。在此类场景中，请在物理删除数据库之前移除中央代理管理配置。此操作不会删除实际的数据库或其数据文件。 |

### 6.2.5 使用输入文件设置 EMCA 参数

您无需在运行 EMCA 时逐一回答提示，而是可以使用`-respFile`参数来指定一个输入文件。您创建的输入文件必须采用与以下示例类似的格式：

```
PORT=1521
```

#### 表 6–1 EMCA 命令行操作

| 命令 | 描述 |
|---|---|
| `emca -deconfig all db [-repos drop] [-cluster] [-silent] [参数]` | 为数据库取消配置数据库控制和中心代理管理。可用的取消配置选项与上述描述的选项类似。 |
| `emca -addNode (db \| asm) [-silent] [参数]` | 为数据库或 ASM 存储的新集群实例配置 Enterprise Manager。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -deleteNode (db \| asm) [-silent] [参数]` | 为正在删除的节点取消配置 Enterprise Manager。下文将在"了解如何将 EMCA 与 Oracle RAC 配合使用"中进一步讨论。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -addInst (db \| asm) [-silent] [参数]` | 为数据库或 Oracle ASM 存储的新集群实例配置 Enterprise Manager。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -deleteInst (db \| asm) [-silent] [参数]` | 为集群数据库或 Oracle ASM 存储的特定实例取消配置 Enterprise Manager。下文将在第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"中进一步讨论。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -reconfig ports [-cluster] [参数]` | 显式重新分配数据库控制端口。选项包括在集群环境中执行此操作。更多信息，请参阅第 6-11 页的"指定数据库控制使用的端口"。 |
| `emca -reconfig dbcontrol -cluster [-silent] [参数]` | 重新配置集群数据库的数据库控制部署。请注意，此命令必须与`-cluster`选项一起使用。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -displayConfig dbcontrol -cluster [-silent] [参数]` | 显示集群环境中数据库控制当前部署配置的信息。请注意，此命令必须与`-cluster`选项一起使用。更多信息，请参阅第 6-3 页的"了解如何将 EMCA 与 Oracle RAC 配合使用"。 |
| `emca -upgrade (db \| asm \| db_asm) [-cluster] [-silent] [参数]` | 将早期版本的 Enterprise Manager 配置升级到当前版本。可以同时为数据库、Oracle ASM 或数据库和 Oracle ASM 实例执行此操作。此操作不会升级实际的数据库或 Oracle ASM 实例，也不会升级 Enterprise Manager 软件。相反，它会升级指定实例的配置文件，使其与当前版本的 Enterprise Manager 软件兼容。EMCA 将尝试升级主机上指定数据库和/或 Oracle ASM 目标的所有实例，涵盖所有 Oracle 主目录（因为某些目标属性，如监听程序端口或 Oracle 主目录，可能已更改）。 |



| `emca -restore (db \| asm \| db_asm) [-cluster] [-silent] [参数]` | 将当前版本的 Enterprise Manager 配置恢复到早期版本。这是 `-upgrade` 选项的反向操作（将逆转任何由 `-upgrade` 操作导致的更改），因此选项类似。 |

表 6–2 EMCA 命令行标志

| 标志 | 描述 |
| :--- | :--- |
| `db` | 为数据库（包括集群数据库）执行操作。对于使用 Oracle 自动存储管理 (ASM) 存储数据文件的数据库，请使用此选项。如果数据库使用 Oracle ASM，此处描述的所有配置操作和模式（`-upgrade` 和 `-restore` 除外）都会自动检测到这一点，并将更改同时应用于数据库和 Oracle ASM 实例。 |
| `asm` | 仅为 Oracle ASM 实例（包括集群 Oracle ASM 实例）执行操作。 |
| `db_asm` | 此标志只能在 `-upgrade` 和 `-restore` 模式下使用。为数据库和 Oracle ASM 实例一起执行升级/恢复操作。数据库和 Oracle ASM 实例可以单独升级或恢复（即，升级 Oracle ASM 实例不需要升级其服务的数据库实例）。因此，可以为数据库及其相应的 Oracle ASM 实例分别升级或恢复 Enterprise Manager 配置。 |
| `-repos create` | 创建一个新的数据库控制管理存储库。 |
| `-repos drop` | 删除当前的数据库控制管理存储库。 |
| `-repos recreate` | 删除当前的数据库控制管理存储库，然后重新创建一个新的。 |
| `-cluster` | 为集群数据库或 Oracle ASM 实例执行操作。 |
| `-silent` | 在不提示输入其他信息的情况下执行操作。如果指定了此模式，则必须在命令行上输入所有必需参数，或使用 `-respFile` 参数在输入文件中指定这些参数。您可以通过在命令行输入 `emca -help` 来查看可用参数列表。 |
| `-backup` | 为数据库配置自动备份。EMCA 将提示设置每日自动备份选项。将使用默认的 Enterprise Manager 设置来备份数据库文件。注意：如果您使用此选项，EMCA 将使用 `db_recovery_file_dest` 初始化参数的值来标识自动备份的恢复区域。如果未设置该参数，EMCA 将生成错误。您稍后可以使用数据库控制中的“维护”页面修改这些设置。更多信息，请参阅数据库控制联机帮助。 |

表 6–3 EMCA 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| `-respFile` | 指定一个输入文件的路径，该文件列出了 EMCA 在执行配置操作时要使用的参数。 |
| `-SID` | 数据库系统标识符 |
| `-PORT` | 为数据库提供服务的监听程序的端口号 |
| `-ORACLE_HOME` | 数据库 Oracle 主目录，作为绝对路径 |
| `-LISTENER_OH` | 运行监听程序的 Oracle 主目录。如果监听程序运行的 Oracle 主目录与数据库运行的 Oracle 主目录不同，则必须指定 `LISTENER_OH` 参数。 |
| `-HOST_USER` | 主机用户名（用于自动备份） |
| `-HOST_USER_PWD` | 主机用户密码（用于自动备份） |
| `-BACKUP_SCHEDULE` | 格式为“HH:MM”的计划（用于每日自动备份） |
| `-EMAIL_ADDRESS` | 用于通知的电子邮件地址 |
| `-MAIL_SERVER_NAME` | 用于通知的传出邮件 (SMTP) 服务器 |
| `-ASM_OH` | Oracle 自动存储管理 Oracle 主目录 |
| `-ASM_SID` | Oracle ASM 实例的系统标识符 |
| `-ASM_PORT` | 为 Oracle ASM 实例提供服务的监听程序的端口号 |
| `-ASM_USER_ROLE` | 连接到 Oracle ASM 实例的用户角色 |
| `-ASM_USER_NAME` | 连接到 Oracle ASM 实例的用户名 |
| `-ASM_USER_PWD` | 连接到 Oracle ASM 实例的密码 |
| `-DBSNMP_PWD` | DBSNMP 用户的密码 |
| `-SYSMAN_PWD` | SYSMAN 用户的密码 |
| `-SYS_PWD` | SYS 用户的密码 |
| `-SRC_OH` | 要升级/恢复其 Enterprise Manager 配置的数据库的 Oracle 主目录 |
| `-DBCONTROL_HTTP_PORT` | 使用此参数指定您在 Web 浏览器中显示数据库控制台所使用的端口。更多信息，请参阅第 6-11 页的“指定数据库控制使用的端口”。 |
| `-AGENT_PORT` | 使用此参数指定数据库控制的 Management Agent 端口。更多信息，请参阅第 6-11 页的“指定数据库控制使用的端口”。 |
| `-RMI_PORT` | 使用此参数指定数据库控制的 RMI 端口。更多信息，请参阅第 6-11 页的“指定数据库控制使用的端口”。 |
| `-JMS_PORT` | 使用此参数指定数据库控制的 JMS 端口。更多信息，请参阅第 6-11 页的“指定数据库控制使用的端口”。 |
| `-CLUSTER_NAME` | 集群名称（用于集群数据库） |
| `-DB_UNIQUE_NAME` | 数据库唯一名称（用于集群数据库） |
| `-SERVICE_NAME` | 数据库服务名（用于集群数据库） |
| `-EM_NODE` | 运行数据库控制台的节点（用于集群数据库）。更多信息，请参阅第 6-3 页的“了解如何将 EMCA 与 Oracle RAC 配合使用”。 |
| `-EM_NODE_LIST` | 以逗号分隔的节点列表，用于仅代理配置，将数据上传到 `-EM_NODE`。更多信息，请参阅第 6-3 页的“了解如何将 EMCA 与 Oracle RAC 配合使用”。 |

```
SID=DB
DBSNMP_PWD=xpE234D
SYSMAN_PWD=KDOdk432
```

创建 EMCA 输入文件后，您可以在命令行中按如下方式使用它：

```
$ ./emca -config dbcontrol db -respFile input_file_path
```

例如，要配置数据库控制以执行每日备份并创建数据库控制管理储存库，请创建一个与以下示例类似的输入文件：

```
PORT=1521
SID=DB
DBSNMP_PWD=dow31224
SYSMAN_PWD=squN3243
HOST_USER=johnson
HOST_USER_PWD=diTf32of
SYS_PWD=qlKj4352
BACKUP_SCHEDULE=06:30
```

创建输入文件后，在操作系统提示符处输入以下命令：

```
$ ./emca -config dbcontrol db -repos create -backup -respFile input_file_path
```

#### 6.2.6 指定数据库控制使用的端口

初次安装 Oracle RAC 11g 第 2 版 (11.2) 或使用 EMCA 配置数据库控制时，数据库控制使用一组默认系统端口。例如，默认情况下，在 11g 第 2 版中，您使用端口 1158 访问数据库控制，如下所示：

```
http://host.domain:1158/em
```

这是互联网号码分配机构 (IANA) 分配给数据库控制的默认端口。同样，由 IANA 分配的默认数据库控制代理端口是 3938。

要使用非默认端口，请在初次使用 EMCA 配置数据库控制时使用以下 EMCA 命令行参数。或者，您可以在使用以下命令配置数据库控制后显式分配端口：

```
emca -reconfig ports [-cluster]
```

> **注意：**您也可以在安装并配置 Oracle RAC 11g 第 2 版 (11.2) 后，使用以下 EMCA 命令行参数来配置数据库控制。

以下列表总结了控制标准数据库控制端口分配的 EMCA 命令行参数：

- `-DBCONTROL_HTTP_PORT` *port_number*

  此端口号用于数据库控制台 URL。例如，如果您将此端口设置为 5570，则可以使用以下 URL 显示数据库控制台：

  `http://host.domain:5570/em`

- `-RMI_PORT` *port_number*

  此端口号由远程方法调用 (RMI) 系统使用，该系统是数据库控制所需的 J2EE 软件的一部分。如果您想为数据库控制台配置特定端口，可以更改默认端口。当使用非默认端口 (1521) 时，请结合 `emca reconfig` 命令使用 `-RMI_PORT` 或 `-JMS_PORT` 选项。

- `-JMS_PORT` *port_number*

  此端口由 OC4J Java 消息服务 (JMS) 使用，它是数据库控制所需的 J2EE 软件的一部分。如果您想为数据库控制台配置特定端口，可以更改默认端口。当使用非默认端口 (1521) 时，请结合 `emca reconfig` 命令使用 `-RMI_PORT` 或 `-JMS_PORT` 选项。

- `-AGENT_PORT` *port_number*

  此端口由数据库控制管理代理使用，该代理负责为数据库控制监控和管理数据库。

#### 6.2.7 EMCA 故障排除提示

以下部分描述了在使用 EMCA 配置数据库控制时需要考虑的一些故障排除提示：

- [更改数据库监听程序端口后使用 EMCA](更改数据库监听程序端口后使用 EMCA)
- [升级 11g 第 2 版网格控制代理](升级 11g 第 2 版网格控制代理)
- [数据库主机名或 IP 地址更改时使用 EMCA](数据库主机名或 IP 地址更改时使用 EMCA)
- [TNS 配置更改时使用 EMCA](TNS 配置更改时使用 EMCA)

##### 6.2.7.1 更改数据库监听程序端口后使用 EMCA

如果您在配置数据库控制后更改了数据库的监听程序端口，则数据库状态将显示为关闭。要重新配置数据库控制以使用新的监听程序端口，请使用 `-config dbcontrol db [-cluster]` 命令行参数运行 EMCA 命令。

##### 6.2.7.2 升级 11g 第 2 版网格控制代理

将配置了 Oracle Enterprise Manager（无论是数据库控制还是网格控制中心代理）的 Oracle Database 10g 第 1 版数据库和 Oracle ASM 实例升级到 Oracle Database 11g 第 2 版 (11.2) 数据库时，相关主机上引用已升级实例的所有 Enterprise Manager 目标都会自动更新。这是因为升级涉及更改实例的 Oracle Home、端口或其他目标关联属性。但是，如果主机上的某些目标由 Oracle Database 11g 第 2 版 (11.2) 网格控制代理管理，则这些目标在升级期间可能无法成功更新。要更新这些目标，请在已升级的数据库（或 Oracle ASM）目标的主页上，单击**监视配置**。在监视配置页面上，您可以将 Oracle Home、监听程序端口等属性更新为正确的值。

##### 6.2.7.3 数据库主机名或 IP 地址更改时使用 EMCA

当数据库主机名（包括域名）或 IP 地址更改时，请使用 `-repos create` 标志的 `emca` 命令取消配置，然后重新配置数据库控制台。例如：

```
emca -deconfig dbcontrol db -repos drop
```

```
emca -config dbcontrol db -repos create
```

或

```
emca -deconfig dbcontrol db
emca -config dbcontrol db -repos recreate
```

##### 6.2.7.4 TNS 配置更改时使用 EMCA

当 TNS 配置更改时，请设置环境变量，然后运行以下命令：

```
emca -config dbcontrol db
```

## 理解 Oracle Real Application Clusters 已安装配置

本章描述 Oracle Real Application Clusters (Oracle RAC) 的已安装配置。本章包含以下主题：

- 理解 Oracle RAC 中的配置环境
- 理解集群节点上的时区设置
- Oracle RAC 的 Oratab 配置
- 使用数据库配置助理创建的数据库组件
- 在 Oracle RAC 中管理撤消表空间
- 初始化参数文件
- Oracle 数据库默认审计策略和初始化参数
- 理解服务注册相关参数
- 配置监听程序文件 (`listener.ora`)
- 网络服务名称 (`tnsnames.ora` 文件)
- 网络服务配置文件 (`sqlnet.ora` 文件)

### 7.1 理解 Oracle RAC 中的配置环境

Oracle Net Configuration Assistant (NETCA) 和 Database Configuration Assistant (DBCA) 会配置您的环境以满足创建数据库和 Oracle Enterprise Manager 发现 Oracle RAC 数据库的要求。

> **注意：**配置文件在集群数据库的每个节点上创建。

完成 Oracle RAC 安装后，请避免更改主机名，包括添加或删除域名限定符。主机名是在 Oracle Clusterware 安装期间创建的，并且在数据库进程中被广泛使用。更改了主机名的节点必须从集群中删除，并使用新名称重新添加。

### 7.2 理解集群节点上的时区设置

Oracle RAC 要求所有集群节点具有相同的时区设置。在 Oracle Clusterware 安装期间，安装过程会确定运行 Oracle Universal Installer (OUI) 的节点上 Grid 安装所有者的时区设置，并将该时区值用作所有节点上 Oracle Clusterware 管理的所有进程的默认时区设置。此默认设置用于数据库、Oracle ASM 和任何其他受管进程。但是，如果您使用 SQL*Plus 启动实例，则必须确保 Oracle RAC 使用的时区值与 Oracle Clusterware 的时区相同。您可以通过运行命令 `srvctl setenv database -T 'TZ=time zone'` 来更改 Oracle Clusterware 用于数据库的时区。

### 7.3 Oracle RAC 的 Oratab 配置

Oracle 在 `oratab` 配置文件中为每个 Oracle RAC 数据库创建一个条目。`oratab` 文件由安装期间的 `root.sh` 脚本创建，并由 Database Configuration Assistant 在创建或删除数据库时更新。当数据库首次在之前未运行过的节点上启动时，Database Agent 也会自动创建 `oratab` 文件条目。Oracle ASM Agent 会创建 Oracle ASM `oratab` 条目。

Oracle Enterprise Manager 在服务发现期间使用 `oratab` 文件来确定 Oracle RAC 数据库的名称，并确定系统重新启动时数据库是否应自动启动。

数据库条目具有以下语法：

`$DB_UNIQUE_NAME:$ORACLE_HOME:N`

冒号 (:) 用作字段分隔符。新行终止条目。以井号 (#) 开头的行是注释。由于 Oracle RAC 数据库的所有实例都具有相同的 `DB_UNIQUE_NAME`，但每个实例都有自己的 `ORACLE_SID`，因此在 `oratab` 文件中使用 `$DB_UNIQUE_NAME` 环境变量作为数据库条目。

您的 Oracle RAC 数据库的 `$DB_UNIQUE_NAME` 标识符在企业中必须是唯一的。`$ORACLE_HOME` 是数据库的目录路径，`N` 表示在重新启动时不应启动数据库。以下是名为 `sales` 的数据库的条目示例：

`sales:/u01/app/oracle/sales:N`

### 7.4 使用数据库配置助理创建的数据库组件

本节描述 DBCA 创建的数据库组件，包括：

- 表空间和数据文件
- 控制文件
- 重做日志文件

#### 7.4.1 表空间和数据文件

对于单实例和集群数据库环境，Oracle 数据库被划分为称为表空间的更小的逻辑空间区域。每个表空间

#### 7.4.2 控制文件

数据库配置有两个控制文件，存储在共享存储上。

#### 7.4.3 重做日志文件

每个实例至少配置有两个重做日志文件，存储在共享存储中。如果使用文件系统，则这些文件为共享文件系统文件。如果使用 Oracle ASM，则这些文件存储在 Oracle ASM 磁盘组中。

使用预配置数据库配置选项创建的重做日志文件名因存储类型而异。除非使用集群文件系统，否则必须输入块设备或原始设备名称。

### 7.5 在 Oracle RAC 中管理撤销表空间

Oracle 数据库将回滚或撤销信息存储在撤销表空间中。为了管理撤销表空间，Oracle 建议使用自动撤销管理。自动撤销管理是一种自动化的撤销表空间管理模式，比手动撤销管理更易于管理。

当 Oracle ASM 和 Oracle 托管文件与自动撤销管理一起使用时，首次启动的实例（因此没有撤销表空间）将自动由另一个实例为其创建撤销表空间。重做日志也是如此。

**另请参阅：** *Oracle Real Application Clusters Administration and Deployment Guide*，了解有关管理撤销表空间的更多信息

### 7.6 初始化参数文件



Oracle 建议使用服务器参数文件（SPFILE）来存储 Oracle 数据库初始化参数。Oracle 建议将所有 SPFILE 存储在 Oracle ASM 上，包括 Oracle ASM SPFILE。SPFILE 必须位于共享存储上；集群数据库中的所有实例都可以访问此参数文件。

**另请参阅：** [第 5 章 "在 Oracle Real Application Clusters 环境中配置服务器参数文件"](Chapter 5, "Configuring the Server Parameter File in Oracle Real Application Clusters Environments")，了解有关参数文件创建和使用的更多信息

### 7.7 Oracle 数据库默认审计策略和初始化参数

Oracle 数据库安装了一个基线数据库审计策略。该策略涵盖存储在 Oracle 数据库表中的访问控制配置信息、存储在 Oracle 目录中的信息（回滚段、表空间等）、系统权限的使用以及 Oracle 标签安全配置。

**另请参阅：** *Oracle Database Vault Administrator's Guide*，了解有关数据库审计策略的更多信息

### 7.8 了解服务注册相关参数

Oracle RAC 数据库提供了连接负载均衡和故障转移的重要优势。独立 Oracle 数据库通过在本地调度程序之间分配连接来执行负载均衡。

Oracle RAC 数据库通过使用 Oracle Clusterware SCAN（单客户端访问名）来平衡集群数据库中所有实例之间的连接，从而增强负载均衡。

查看以下部分以了解 Oracle RAC 负载均衡功能：

- [了解单客户端访问名（SCAN）和负载均衡](Understanding%20Single%20Client%20Access%20Name%20(SCAN)%20and%20Load-balancing)

- [了解负载均衡、故障转移和高可用性](Understanding%20Load-Balancing,%20Failover,%20and%20High%20Availability)

#### 7.8.1 了解单客户端访问名（SCAN）和负载均衡

单客户端访问名（SCAN）是一个完全限定名（主机名+域），配置为解析为分配给 SCAN 的所有地址。这些地址使用 DNS 服务器上的轮询 DNS 或 GNS 配置中的集群内解析。SCAN 监听器可以在集群中的任何节点上运行。

Oracle Database 11g 第 2 版及更高版本的实例仅向 SCAN 监听器注册为远程监听器。升级后的数据库向 SCAN 监听器注册为远程监听器，同时也继续向所有节点监听器注册。

SCAN 在集群上运行，而不是在集群节点上运行。SCAN 为数据库提供位置独立性，因此客户端配置不必依赖于哪些节点正在运行特定数据库。例如，如果在集群中配置策略管理的服务器池，则 SCAN 允许连接到这些服务器池中的数据库，而不管哪些节点被分配给该服务器池。

SCAN 的功能类似于节点虚拟 IP（VIP）地址。但是，SCAN 解析为在集群中任何节点上运行的 SCAN VIP，因此与节点的虚拟 IP 地址不同，连接到 SCAN 的客户端在节点添加到集群或从集群中移除时不再需要更新的虚拟 IP 地址。由于 SCAN 地址解析到集群，而不是集群中的节点地址，因此可以添加或移除节点而不影响 SCAN 地址配置。

在 Oracle Grid Infrastructure 安装期间，SCAN 监听器为解析 SCAN 的地址数量创建相应数量的 IP 地址。Oracle 建议 SCAN 解析为三个地址，以提供高可用性和可扩展性。如果 SCAN 解析为三个地址，则创建三个 SCAN 监听器。

Oracle RAC 通过配置多个节点上的多个监听器来管理同一数据库服务的客户端连接请求，从而提供节点 VIP 地址的故障转移。如果节点发生故障，则连接到 VIP 的服务将透明地重新定位到存活节点，使通过 VIP 连接的客户端能够快速收到故障通知。如果应用程序和客户端配置了透明应用程序故障转移选项，则客户端将重新连接到存活节点。Oracle Clusterware 将客户端应用程序请求从 SCAN 路由到提供服务的最轻负载实例的 VIP。

配置为使用 Oracle Database 11g 第 2 版之前版本的 IP 地址的客户端可以继续使用其现有连接地址；使用 SCAN 不是必需的。当早期版本的 Oracle Database 升级时，它会向 SCAN 监听器注册，客户端可以开始使用 SCAN 连接到该数据库。数据库通过 `init.ora` 文件中的远程监听器参数向 SCAN 监听器注册。`REMOTE_LISTENER` 参数必须设置为 `SCAN:PORT`。不要将其设置为使用 SCAN 作为 `HOST=SCAN` 的单个地址的 TNSNAMES 别名。

> **另请参阅：** *Oracle Grid Infrastructure Installation Guide*，了解有关 SCAN 及其配置的详细信息

#### 7.8.2 了解负载均衡、故障转移和高可用性

连接负载均衡和故障转移通过利用集群数据库中的冗余资源来提高可用性。

数据库代理（以前称为 `racgimon`）自动配置 `LOCAL_LISTENER` 初始化参数。您无需更改此设置。使用 SQL 命令 `ALTER SYSTEM SET REMOTE_LISTENER` 将 `REMOTE_LISTENER` 设置为 SCAN 端口和 SCAN。如果更改 SCAN 端口，则需要更改 `REMOTE_LISTENER` 配置。

`LOCAL_LISTENER` 参数标识本地监听器，`REMOTE_LISTENER` 参数标识全局监听器列表。`REMOTE_LISTENER` 参数始终设置为 SCAN 地址。例如，如果集群名称为 `mycluster`，域为 `example.com`，则 SCAN 地址将类似于 `myscan.mycluster.example.com:1521`。

默认情况下，DBCA 使用专用服务器配置您的环境。但是，如果在使用 DBCA 时选择共享服务器选项，则 Oracle 将配置共享服务器。在这种情况下，Oracle 数据库同时使用专用服务器和共享服务器处理。当配置共享服务器时，`DISPATCHERS` 参数指定方式如下例所示：

```
DISPATCHERS="(protocol=tcp)"
```

如果 `DISPATCHERS` 初始化参数未指定 `LISTENER` 属性（如前例所示），则 PMON 进程会向 `LOCAL_LISTENER` 和 `REMOTE_LISTENER` 参数指定的所有监听器注册所有分发进程的信息。

但是，当指定了 `LISTENER` 属性时，PMON 进程会向 `LISTENER` 属性指定的监听器注册分发进程信息。在这种情况下，为指定分发进程设置 `LISTENER` 属性会覆盖 `REMOTE_LISTENER` 设置，如下例所示：

```
DISPATCHERS="(protocol=tcp)(listener=listeners_db_name)"
```

> **注意：** 在前例及本章各处出现的符号 `db_name`，指的是您在 DBCA 提示下输入的数据库名称（或 Oracle SID），或者指的是您为 `CREATE DATABASE` 语句的 `DATABASE` 关键字输入的条目。

**另请参阅：** *Oracle 数据库网络服务管理员指南*，了解有关跨实例注册、共享和专用服务器配置以及连接负载均衡的更多信息。

### 7.9 配置监听器文件（listener.ora）

您可以在 `listener.ora` 文件中配置两种类型的监听器，如下文各节所述：

- 网格命名服务（GNS）与监听器

- 关于本地监听器

- 关于多个监听器

- Oracle 数据库如何使用监听器文件（`listener.ora`）

#### 7.9.1 网格命名服务（GNS）与监听器

如果您启用了网格命名服务（GNS），则无需手动配置监听器。在 GNS 配置中，集群有一个 GNS 守护进程。发往 GNS 管理的集群域的服务请求会被路由到 GNS 虚拟 IP 地址，该地址再将这些请求路由到 GNS 守护进程。

GNS 守护进程监听注册信息。当 SCAN 虚拟 IP 启动时，它会向 GNS 注册其地址。当 GNS 收到 DNS 发来的 SCAN 请求时，它会将注册的地址返回给 DNS。

#### 7.9.2 关于本地监听器

在 Oracle 数据库创建过程中，`LOCAL_LISTENER` 参数会自动配置为指向数据库的本地监听器。数据库代理将 `LOCAL_LISTENER` 参数设置为一个不需要 TNS 别名的连接描述符。

您可以手动为 `LOCAL_LISTENER` 设置值。但是，Oracle 建议您不要设置该参数，以便数据库代理可以自动维护它。

例如，在创建数据库后，如果您需要添加第二个监听器，该监听器监听端口 2012，请使用以下命令使数据库在启动时向两个监听器注册：

```
> alter system set local_listener='(DESCRIPTION=
(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.0.61)(PORT=1521))
(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.0.61)(PORT=2012))))'
scope=BOTH SID='OCRL1';
```

> **另请参阅：** *Oracle 数据库网络服务管理员指南*，了解有关理解和配置监听器的信息。

`tnsnames.ora` 文件位于路径 `$ORACLE_HOME/network/admin` 中。默认情况下，`tnsnames.ora` 文件从 Oracle Grid Infrastructure 主目录中读取，路径为 `Grid_home/network/admin`。

监听器关联不再需要 `tnsnames.ora` 文件条目。`REMOTE_LISTENER` 由 DBCA 配置为引用 SCAN 名称和端口，无需 `tnsnames.ora` 条目。

以下是 Oracle RAC 11g 第 2 版（11.2）`tnsnames.ora` 文件的示例：

```
# tnsnames.ora Network Configuration file:
# /u01/app/oracle/product/11.2.0/dbhome_1/network/admin/tnsnames.ora
# Generated by Oracle Configuration tools
RACDB =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = myscan.mycluster.example.com)(PORT = 1521))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = RACDB)
    )
  )
```

#### 7.9.3 关于多个监听器

如果 DBCA 检测到节点上有多个监听器，则会显示一个监听器列表。您可以选择一个或所有这些监听器来注册您的数据库。

> **注意：** 要使用 `lsnrctl` 命令管理 11g 第 2 版（11.2）本地和 SCAN 监听器，请将您的 `ORACLE_HOME` 环境变量设置为 Oracle Grid Infrastructure 主目录（Grid 主目录）的路径。请勿尝试使用来自以前版本 Oracle 主目录位置的 `lsnrctl` 命令，因为它们无法用于新版本。

#### 7.9.4 Oracle 数据库如何使用监听器文件（listener.ora）

服务通过向本地监听器和 SCAN 监听器注册其负载来协调其会话。SCAN 监听器将客户端重定向到运行特定服务实例的负载最低节点上的本地监听器。该监听器要么将客户端重定向到分发进程（如果数据库配置为共享服务器），要么将客户端重定向到专用服务器进程。本地监听器配置为响应数据库连接请求以及非数据库连接请求，例如外部过程或 XDB 请求。

监听器代理动态更新监听器的端点。随着 Oracle 数据库 11g 第 2 版的安装，`listener.ora` 文件现在只包含一个 IPC 密钥和以下信息：

```
(ADDRESS = (PROTOCOL=TCP)(HOST=)(PORT=1521))
```

此信息隐式指向本地节点的 HOST 端点。`listener.ora` 文件在每个节点上都是相同的。

在安装 Oracle RAC 之前，在 Oracle Grid Infrastructure 安装过程中，Oracle Net Configuration Assistant 会在 Grid 主目录中创建并启动一个名为 `LISTENER` 的默认监听器。该监听器配置了默认的协议监听地址。监听器配置为响应在安装期间指定的一个协议地址定向的连接请求。

在 Oracle RAC 安装过程中，Oracle RAC 数据库使用 Oracle Clusterware 监听器，并配置有关 Oracle RAC 数据库的服务信息。Oracle 数据库 11g 第 2 版（11.2）数据库服务会自动向监听器注册其信息，例如其服务名称、实例名称和负载信息。此功能称为服务注册，不需要在 `listener.ora` 文件中进行配置。创建监听器后，Oracle Net Configuration Assistant 会启动该监听器。

安装后，您可以使用 `srvctl` 命令或使用 NetCA 修改监听器。无需手动编辑 `listener.ora` 文件。

以下是包含名为 `node1` 的节点条目的 `listener.ora` 文件示例：

```
LISTENER_SCAN1=(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=IPC)(KEY=LISTENER_SCAN1)))) # line added by Agent
LISTENER_NODE1=(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=IPC)(KEY=LISTENER)))) # line added by Agent
# listener.ora.mycluster Network Configuration File:
# /u01/app/oracle/11.2.0/dbhome_1/network/admin/listener.ora.mycluster
# Generated by Oracle configuration tools.

LISTENER_NODE1 =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ENABLE_GLOBAL_DYNAMIC_ENDPOINT_LISTENER_NODE1=ON # line added by Agent
ENABLE_GLOBAL_DYNAMIC_ENDPOINT_LISTENER_SCAN2=ON # line added by Agent
ENABLE_GLOBAL_DYNAMIC_ENDPOINT_LISTENER_SCAN1=ON # line added by Agent
```

##### 7.9.4.1 监听器注册与 PMON 发现

当监听器在 Oracle 实例启动后启动，并且该监听器被列为服务注册目标时，注册不会发生，直到下一次 Oracle 数据库进程监视器（PMON）发现例程启动。默认情况下，PMON 发现每 60 秒发生一次。

要覆盖 60 秒延迟，请使用 `SQL ALTER SYSTEM REGISTER` 语句。此语句强制 PMON 进程立即注册服务。

Oracle 建议您创建一个脚本，在启动监听器后立即运行此语句。如果在监听器运行且实例已注册时运行此语句，或在监听器关闭时运行此语句，则该语句将无效。

**另请参阅：** *《Oracle 数据库网络服务管理员指南》* 以获取有关监听器和 `listener.ora` 文件的更多信息。

### 7.10 网络服务名称（tnsnames.ora 文件）

`tnsnames.ora` 文件在每个节点上创建，包含网络服务名称。连接标识符是一个映射到连接描述符的标识符。连接描述符包含以下信息：

- 指向服务的网络路由，包括通过协议地址定位的监听器位置

- Oracle 数据库的 `SERVICE_NAME`

> **注意：** 您在 `tnsnames.ora` 文件中使用的 `SERVICE_NAME` 参数是单数形式，因为您只能指定一个服务名称。数据库初始化文件中还有 `SERVICE_NAMES` 参数。`SERVICE_NAMES` 参数默认为全局数据库名，该名称由初始化参数文件中的 `DB_NAME` 和 `DB_DOMAIN` 参数组成。

从 Oracle Clusterware 11g 第 2 版及更高版本开始，数据库配置代理（DBCA）不再设置 `LOCAL_LISTENER` 参数。启动数据库的 Oracle Clusterware 代理会动态设置 `LOCAL_LISTENER` 参数，除非您显式设置 `LOCAL_LISTENER` 参数，即使用命令 `ALTER SYSTEM SET LOCAL_LISTENER` 手动设置该参数。`tnsnames.ora` 文件中不再需要 `Listener_alias` 条目。

例如，创建数据库后，如果需要添加第二个监听器（监听端口 2012），则使用以下命令使数据库在启动时向两个监听器注册：

```
> alter system set local_listener=' (DESCRIPTION=
 (ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=192.168.0.61)(PORT=1521))
 (ADDRESS=(PROTOCOL=TCP)(HOST=192.168.0.61)(PORT=2012))))'
 scope=BOTH SID='OCRL1' ;
```

**另请参阅：** *《Oracle 数据库管理员指南》*

对于 `REMOTE_LISTENER` 参数，Oracle Clusterware 使用 EZ 连接语法 `scanname:scanport`，因此 `tnsnames.ora` 文件中不需要为 `REMOTE_LISTENER` 参数设置任何条目。

DBCA 创建用于连接的网络服务名称，如下文各节所述。



请查阅以下各节以获取有关网络服务名称的信息：

- [数据库连接的网络服务名称](Net Service Names for Database Connections)
- [网络服务名称实例连接](Net Service Name Instance Connections)
- [tnsnames.ora 示例文件](tnsnames.ora Example File)

#### 7.10.1 数据库连接的网络服务名称

连接到数据库任意实例的客户端使用数据库的 SCAN 名称。此条目还使 Oracle Enterprise Manager 能够发现 Oracle RAC 数据库。

为集群配置了三个 SCAN 地址，并分配给服务器。如果所选地址失败，则到 SCAN 名称的连接请求将故障转移到下一个地址。因此，如果某个实例失败，客户端仍可使用另一个实例进行连接。

在以下示例中，客户端使用 `myscan.mycluster.example.com` 连接到目标数据库 `mycluster.example.com`。

```
mycluster.example.com =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = host=myscan.mycluster.example.com)(PORT = 1522))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = myApp)
    )
  )
```

该数据库的 Easy Connect 地址应类似于以下内容：

`myscan.mycluster.example.com/mycluster.example.com`

#### 7.10.2 网络服务名称实例连接

连接到数据库特定实例的客户端使用该实例的 SCAN 名称。此条目（例如）使 Oracle Enterprise Manager 能够发现集群中的实例。这些条目也用于启动和停止实例。

在以下示例中，Oracle Enterprise Manager 使用 `myscan.mycluster.example.com` 连接到节点 `node1` 上名为 `mycluster1` 的实例：

```
mycluster1.example.com=
  (description=
    (address=(protocol=tcp)(host=myscan.mycluster.example.com)(port=1521))
    (connect_data=
      (service_name=mycluster.example.com)
      (instance_name=mycluster1)))
```

#### 7.10.3 tnsnames.ora 示例文件

此示例是预配置数据库配置安装过程中创建的 `tnsnames.ora` 文件示例。

```
# tnsnames.ora Network Configuration File: /u01/app/oracle/11.2.0/dbhome_1/network/admin/tnsnames.ora
# Generated by Oracle configuration tools.

sales =
  (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = myscan.mycluster.example.com)(PORT = 1522))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = myApp)
    )
  )
```

> **另请参阅：** *《Oracle 数据库网络服务管理员指南》* 以获取有关 `tnsnames.ora` 文件的更多信息。

### 7.11 网络服务配置文件（sqlnet.ora 文件）

Oracle Universal Installer 在数据库安装后启动 Oracle Net Configuration Assistant，并创建网络服务配置文件，即 `sqlnet.ora` 文件。

默认情况下，`sqlnet.ora` 文件位于以下目录中：

```
$ORACLE_HOME/network/admin
```

在此目录中，除了安装期间生成的默认 `sqlnet.ora` 文件外，您还可以在 `sample` 目录中找到示例 `sqlnet.ora` 文件。

在安装过程中，Oracle Net Configuration Assistant 在 `sqlnet.ora` 文件中创建以下条目，其中 *Oracle_base* 是 Oracle RAC 安装所有者的 Oracle 基础目录路径：

```
NAMES.DIRECTORY_PATH=(TNSNAMES, EZCONNECT)
ADR_BASE =Oracle_base
```

参数 `NAMES.DIRECTORY_PATH` 指定了用于将连接标识符解析为连接描述符的命名方法的优先顺序。

Easy Connect 命名方法消除了在 TCP/IP 环境中对 `tnsnames.ora` 文件中的服务名称进行查找的需要。使用 Easy Connect，客户端使用一个简单的 TCP/IP 地址的连接字符串，该字符串由主机名以及可选的端口和服务名组成。如果您使用此方法，则无需命名或目录系统。

> **另请参阅：** *《Oracle 数据库网络服务管理员指南》* 以获取有关 `sqlnet.ora` 文件的更多信息。

## 8 删除 Oracle Real Application Clusters 软件

本章介绍如何从 Oracle Real Application Clusters（Oracle RAC）Oracle 主目录中完全删除所有 Oracle 数据库、实例和软件。

本章包含以下主题：

- 卸载过程概述
- 识别集群上的所有实例
- 卸载 Oracle RAC 软件

> **另请参阅：** 有关特定产品的文档（如果您想删除单个产品），以确保您了解适用于该产品的要求和限制。

### 8.1 卸载过程概述

要从 Oracle 主目录中完全删除所有 Oracle 数据库、实例和软件：

- 识别与 Oracle 主目录关联的所有实例
- 关闭进程
- 删除 Oracle 数据库主目录中安装的监听器
- 删除数据库实例
- 删除 Oracle 自动存储管理（11.1 或更早版本）
- 删除 Oracle Clusterware 和 Oracle 自动存储管理（Oracle Grid Infrastructure）

> **注意：** 您无法删除或卸载 Oracle Database Vault 选项。但是，您可以禁用它。有关更多详细信息，请参阅 *《Oracle Database Vault 管理员指南》*。

您可以删除 Oracle Configuration Manager。有关更多详细信息，请参阅 *《Oracle Configuration Manager 安装和管理指南》*。

从 11.2 及更高版本开始，Oracle 自动存储管理和 Oracle Clusterware 构成了 Oracle Grid Infrastructure 安装。这些组件将一起安装和删除。

### 8.2 识别集群上的所有实例

要识别与要删除的 Oracle 主目录关联的所有实例，请输入以下命令：

AIX、HP-UX 或 Linux：

```
$ more /etc/oratab
```

Solaris：

```
$ more /var/opt/oracle/oratab
```

此命令的输出包含类似以下内容的条目：

```
+ASM1:/u01/app/grid/11.2.0:N
CUST:/u01/app/oracle/product/11.2.0/dbhome_1:N
```

这些条目表明，Oracle Grid Infrastructure 集群主目录（`/u01/app/grid/11.2.0`）中的 `+ASM` Oracle 自动存储管理实例和 `CUST` Oracle 数据库实例与 Oracle 主目录 `/u01/app/oracle/product/11.2.0/dbhome_1` 相关联。

### 8.3 卸载 Oracle RAC 软件

卸载工具可从服务器中移除 Oracle Clusterware 和 Oracle 自动存储管理（Oracle ASM），以及 Oracle Real Application Clusters（Oracle RAC）或独立 Oracle 数据库安装。以下各节介绍该脚本，并提供有关使用该工具的其他选项的信息：

- 关于卸载工具
- 运行 Oracle RAC 卸载命令的示例
- Oracle RAC 卸载参数文件示例

#### 8.3.1 关于卸载工具

卸载工具（`deinstall`）会停止 Oracle 软件，并移除操作系统上的 Oracle 软件和配置文件。它在安装前位于安装介质中，安装后位于 Oracle 主目录中。它位于路径 `$ORACLE_HOME/deinstall` 中。

> **注意：** 运行 `deinstall` 命令时，如果中央库存（`oraInventory`）中除了要重新配置和移除的主目录之外没有其他已注册的主目录，则 `deinstall` 命令会移除 Oracle RAC 安装所有者的 Oracle 基目录中的以下文件和目录内容：

- `admin`
- `cfgtoollogs`
- `checkpoints`
- `diag`
- `oradata`
- `flash_recovery_area`

Oracle 强烈建议您使用最优灵活架构（OFA）配置来配置安装，并且为 Oracle 软件保留专用的 Oracle 基路径和 Oracle 主路径。如果您在 Oracle 基目录中拥有由拥有 Oracle 软件的用户帐户拥有的用户数据，则 `deinstall` 命令会删除这些数据。

`deinstall` 命令会停止 Oracle 软件，并移除操作系统上的 Oracle 软件和配置文件。该命令使用以下语法，其中变量内容以斜体表示：

```
deinstall -home complete path of Oracle home [-silent] [-checkonly] [-local]
[-paramfile complete path of input parameter property file] [-params name1=value
name2=value . . .] [-o complete path of directory for saving files] [-help]
```

运行 `deinstall` 工具的默认方法是从 Oracle 主目录中的 `deinstall` 目录运行。例如：

```
$ cd $ORACLE_HOME/deinstall
$ ./deinstall
```

此外，您可以从其他位置运行 `deinstall` 工具，或使用参数文件，或选择其他选项来运行该工具。

选项如下：

- **-home**

  使用此标志指定要检查或卸载的 Oracle 主目录的主路径。如果您要使用同一 Oracle 主目录中的 `deinstall` 命令来卸载 Oracle 软件，请在另一个位置提供参数文件，而不要使用 `-home` 标志。

- **-silent**

  使用此标志以非交互模式运行命令。如果使用 `-silent` 选项，则必须使用 `-paramFile` 标志，并提供包含要卸载或重新配置的 Oracle 主目录配置值的参数文件。

  要创建属性文件并提供所需参数，请参阅模板文件 `deinstall.rsp.tmpl`，该文件位于卸载工具主目录或 Oracle 主目录的 `response` 文件夹中。

如果您有一个正在运行的系统，则可以不使用模板文件，而是通过使用 `-checkonly` 标志运行 `deinstall` 命令来生成属性文件。`deinstall` 命令将发现要卸载和重新配置的 Oracle 主目录的信息。它会生成属性文件，然后您可以将该文件与 `-silent` 选项一起使用。

- **-checkonly**

  使用此标志检查 Oracle 软件主目录配置的状态。使用 `checkonly` 标志运行命令不会移除 Oracle 配置。`checkonly` 标志会生成一个参数文件，您可以将其与 `deinstall` 命令一起使用。

  运行 `checkonly` 生成参数文件时，系统会提示您提供有关系统的信息。您可以接受工具从您的 Oracle 安装中获取的默认值（显示在方括号 `[]` 内），也可以提供不同的值。要接受默认值，请按 **Enter** 键。

- **-local**

  在多节点环境中使用此标志来重新配置集群中的 Oracle 软件。

  使用此标志运行 `deinstall` 时，它会在本地节点（运行 `deinstall` 的节点）上重新配置并卸载 Oracle 软件。在远程节点上，它会重新配置 Oracle 软件，但不会卸载 Oracle 软件。

- **-paramfile** *输入参数属性文件的完整路径*

  使用此标志以默认位置以外的位置的参数文件运行 `deinstall`。使用此标志时，请提供参数文件所在的完整路径。如果您要从计划卸载的 Oracle 主目录运行 `deinstall` 命令，则无需使用 `-paramfile` 选项。

  参数文件的默认位置取决于 `deinstall` 的位置：

  - 从安装介质或暂存位置运行时：`$ORACLE_HOME/inventory/response`。
  - 从 OTN 下载的解压存档文件运行时：`/ziplocation/response`。
  - 安装后从已安装的 Oracle 主目录运行时：`$ORACLE_HOME/deinstall/response`。

- **-params** *[name1=value name2=value name3=value ...]*

  将此标志与参数文件一起使用，以覆盖您在已创建的参数文件中要更改的一个或多个值。

- **-o** *保存响应文件的目录的完整路径*

  使用此标志提供属性文件（`deinstall.rsp.tmpl`）保存位置以外的其他路径。

  参数文件的默认位置取决于 `deinstall` 的位置：

  - 安装前从安装介质或暂存位置运行时：`$ORACLE_HOME/`
  - 从 OTN 下载的解压存档文件运行时：`/ziplocation/response/`。
  - 安装后从已安装的 Oracle 主目录运行时：`$ORACLE_HOME/deinstall/response`。

- **-help**

  使用帮助选项（`-help`）获取有关命令选项标志的其他信息。

#### 8.3.2 运行 Oracle RAC 卸载命令的示例

`deinstall` 命令运行时，系统会提示您提供要从系统中移除的 Oracle 软件的主目录。请根据提示提供其他信息。

如果您在 `$ORACLE_HOME/deinstall` 文件夹之外输入 `deinstall` 命令，则会显示帮助信息，除非您输入了 `-home` 标志并提供了路径。如果您从 `$ORACLE_HOME/deinstall` 文件夹运行 `deinstall` 命令，则卸载将开始，而不会提示您输入主目录地址。

使用可选标志 `-paramfile` 提供参数文件的路径。

在以下示例中，`deinstall` 命令位于路径 `/u01/app/oracle/product/11.2.0/dbhome_1/deinstall` 中：

```
$ cd /u01/app/oracle/product/11.2.0/dbhome_1/deinstall
$ ./deinstall
```

#### 8.3.3 Oracle RAC 卸载参数文件示例

您可以使用 `-paramfile` 选项运行 `deinstall` 命令，以使用您在参数文件中指定的值。以下是参数文件的示例，其中 Oracle Database 二进制文件所有者为 `oracle`，Oracle Database 主目录（Oracle 主目录）位于路径 `/u01/app/oracle/product/11.2.0/dbhome_1/`，Oracle 基目录（其他 Oracle 软件的安装位置）为 `/u01/app/oracle/`，中央 Oracle 清单主目录（`oraInventory`）为 `/u01/app/oraInventory`，虚拟 IP 地址（VIP）为 `192.0.2.1`，本地节点（运行卸载会话的节点）为 `node1`，远程节点为 `node2`，OSDBA 组为 `dba`：



```
#Copyright (c) 2005, 2006 Oracle Corporation. All rights reserved.
#Wed Feb 11 16:30:21 PST 2009
DISK_GROUPS.typi=
REMOTE_NODES=node2
ORACLE_BASE.typi=/u01/app/oracle
STORAGE_TYPE.typi=FS
ASM_HOME=
ASM_LOCAL_SID=
FLASH_RECOVERY_LOC.typi=
LOGDIR=/u01/app/oraInventory/logs/
DB_TYPE.typi=RAC_DB
ORACLE_BASE=/u01/app/oracle
INVENTORY_LOCATION=/u01/app/oraInventory
NODE_LIST.typi=node1,node2
ARCHIVE_LOG_DESTINATION_LOC.typi=
ASM_FILES.typi=
LOCAL_SID.typi=typi1
CLUSTER_NODES=node1,node2
DB_UNIQUE_NAME_LIST=typi
RAW_MAPPING_FILE.typi=
ORA_CRS_HOME=/u01/app/grid/11.2.0/
HOME_TYPE=RACDB
CRS_HOME=false
SID_LIST.typi=typi1,typi2
DATAFILE_LOC.typi=/oradbocfs/storage/database/oradata/typi
ORACLE_BINARY_OK=true
local=false
```

## 卸载 Oracle RAC 软件

```
LOCAL_NODE=node1
CREATION_MODE.typi=y
CONFIGFILE_LOC.typi=/oradbocfs/storage/database/oradata/typi/control01.ctl, /oradbocfs/storage/database/oradata/typi/control02.ctl, /oradbocfs/storage/database/oradata/typi/control03.ctl, /u01/app/oracle/product/11.2.0/dbhome_1/dbs/drltypi.dat, /u01/app/oracle/product/11.2.0/dbhome_1/dbs/dr2typi.dat
DIAG_DEST.typi=/u01/app/oracle/diag/rdbms/typi
SPFILE_LOC.typi=/oradbocfs/storage/database/oradata/typi/spfiletypi.ora
silent=true
ORACLE_HOME=/u01/app/oracle/product/11.2.0/dbhome_1
```

# A 排查 Oracle Real Application Clusters 安装故障

本附录提供有关安装 Oracle Real Application Clusters（Oracle RAC）的故障排查信息。包含以下章节：

- 排查 Oracle Real Application Clusters 安装故障
- 关于安装后使用 CVU 集群健康检查

> **另请参阅：** 安装介质中 Documentation 目录下的 Oracle Database 11g 第 2 版（11.2）Oracle Real Application Clusters 文档集：
> - *Oracle Real Application Clusters 管理与部署指南*
> - *Oracle Clusterware 管理与部署指南*

## A.1 排查 Oracle Real Application Clusters 安装故障

本节包含以下主题：

- 一般安装问题
- Oracle RAC 安装错误消息
- 在 Oracle Clusterware 安装期间执行集群诊断
- 查看安装会话日志
- 配置助手错误

### A.1.1 一般安装问题

以下列出了安装期间可能出现的错误类型示例。包含以下问题：

- 尝试获取磁盘时发生错误
- 无法连接到服务器、服务器拒绝连接或无法打开显示
- 无法从 OUI 节点选择屏幕中选择节点
- 节点 `nodename` 不可达
- PROT-8：无法将指定文件中的数据导入集群注册表
- PRKP-1001：启动实例时出错
- 时间戳在未来
- YPBINDPROC_DOMAIN：域未绑定

#### 尝试获取磁盘时发生错误

**原因：** `/etc/oratab` 中存在一条指向不存在的 Oracle 主目录的条目。OUI 错误文件应显示以下错误："java.io.IOException: /home/oracle/OraHome//bin/kfod: not found"

**操作：** 删除 `/etc/oratab` 中指向不存在的 Oracle 主目录的条目。

#### 无法连接到服务器、服务器拒绝连接或无法打开显示

**原因：** 这些是 Windows 或 UNIX 系统上典型的 X Window 显示错误，通常是因为 `xhost` 未正确配置。

**操作：** 在本地终端窗口中，以启动 X Window 会话的用户身份登录，然后输入以下命令：

`$ xhost fully_qualified_remote_host_name`

例如：

`$ xhost somehost.example.com`

然后输入以下命令，其中 `workstation_name` 是工作站的主机名或 IP 地址。

Bourne、Bash 或 Korn shell：

`$ DISPLAY=workstation_name:0.0`

`$ export DISPLAY`

要确定 X Window 应用程序是否在本地系统上正确显示，请输入以下命令：

`$ xclock`

X 时钟应出现在您的显示器上。如果失败，则服务器上可能限制了 `xhost` 命令的使用。

如果您使用 VNC 客户端访问服务器，请确保您访问的是分配给您用于安装的用户的可视界面。例如，如果您使用 `su` 命令在另一个用户可视界面上切换为安装所有者，且 `xhost` 命令的使用受到限制，则您无法使用 `xhost` 命令来更改显示。如果您使用分配给安装所有者的可视界面，则正确的显示将可用，输入 `xclock` 命令将显示 X 时钟。

#### 无法从 OUI 节点选择屏幕中选择节点

**原因：** Oracle Clusterware 未安装，或 Oracle Clusterware 服务未启动运行。

**操作：** 安装 Oracle Clusterware，或检查您的 Oracle Clusterware 状态。考虑重新启动节点，因为这样做可能会解决问题。

#### 节点 *nodename* 不可达

**原因：** IP 主机不可用

**操作：** 请尝试以下操作：

1. 运行命令 `ifconfig -a`。将此命令的输出与 `/etc/hosts` 文件的内容进行比较，确保节点 IP 已列出。
2. 运行命令 `nslookup` 查看主机是否可达。
3. 以 `oracle` 用户身份，尝试使用 `ssh` 或 `rsh` 连接到该节点。如果提示输入密码，则说明用户等价性未正确设置。请联系您的系统管理员，或查阅您平台的 *Oracle Grid Infrastructure 安装指南* 以完成 SSH 配置。

#### PROT-8：无法将指定文件中的数据导入集群注册表

**原因：** 现有 Oracle Cluster Registry 原始设备分区中的空间不足，导致运行 `rootupgrade.sh` 时迁移失败。要确认此问题，请在日志文件 `$ORA_CRS_HOME/log/hostname/client/ocrconfig_pid.log` 中查找错误 "utopen:12:Not enough space in the backing store"。

**操作：** 找出具有 280 MB 或更多可用空间的原始设备。从 `/etc/oracle/srvConfig.loc`（AIX、HP-UX、Linux）或 `/var/opt/oracle/srvConfig.loc`（Solaris）中定位现有原始设备名称，并使用 `dd` 命令将此原始设备的内容复制到新设备。

#### PRKP-1001：启动实例时出错

**原因：** 缺少 ODBC 驱动程序管理器。关联消息为 **CRS-0215: Could not start resource**。

**操作：** 清理安装，从 http://www.unixodbc.org 下载并安装 ODBC 驱动程序，然后重新启动安装。这是 Oracle RAC 数据库的要求，在您平台的 *Oracle Grid Infrastructure 安装指南* 的系统需求中有记录。

#### 时间戳在未来

**原因：** 一个或多个节点的时钟时间与本地节点不同。如果是这种情况，您可能会看到类似以下的输出：

`time stamp 2005-04-04 14:49:49 is 106 s in the future`

**操作：** 确保集群的所有成员节点具有相同的时钟时间。

#### YPBINDPROC_DOMAIN：域未绑定

**原因：** 当节点公共网络互连被拔出且 VIP 未进行故障切换时，可能会在安装后测试期间发生此错误。节点会挂起，用户无法登录系统。当 Oracle 主目录、`listener.ora`、Oracle 日志文件或任何操作脚本位于 NAS 设备或 NFS 挂载上，且名称服务缓存守护进程 `nscd` 未被激活时，会发生此错误。

**操作：** 在集群的所有节点上输入以下命令以启动 `nscd` 服务：

```
/sbin/service nscd start
```

### A.1.2 Oracle RAC 安装错误消息

请注意，执行 Oracle RAC 安装的用户必须同时属于 `oinstall` 组和 OSDBA 组（通常是 `oinstall` 和 `dba`）。如果不是这种情况，安装将会失败。

有关解决错误消息的更多帮助，请参阅 My Oracle Support。例如，文档 ID 1372375.1 包含了一些 Oracle Real Application Clusters 最常见的安装问题。

### A.1.3 在 Oracle Clusterware 安装期间执行集群诊断

如果 Oracle Universal Installer（OUI）未显示节点选择页面，请从 Oracle Clusterware 主目录中的二进制目录（Linux 和基于 UNIX 的系统上为 `Grid_home/bin`）运行 `olsnodes -v` 命令，并分析其输出来执行集群软件诊断。如果详细输出表明集群软件未运行，请参阅您的集群软件文档。

此外，使用以下命令语法检查集群管理器的完整性：

```
cluvfy comp clumgr -n node_list -verbose
```

在上述语法示例中，变量 `node_list` 是集群中的节点列表，以逗号分隔。

### A.1.4 查看安装会话日志

在安装过程中，Oracle Universal Installer 将其执行的所有操作记录在日志文件中。如果在安装过程中遇到问题，请查看日志文件以获取有关问题可能原因的信息。

要查看日志文件，请按以下步骤操作：

1. 如有必要，输入以下命令以确定 `oraInventory` 目录的位置：

```
$ cat /opt/oracle/oraInst.loc
$ cat /var/opt/oracle/oraInst.loc
```

2. 输入以下命令以确定日志文件的名称：

```
$ ls -ltr
```

此命令按创建顺序列出文件，最近的文件显示在最后。安装程序日志文件的名称类似于以下格式，其中 `date_time` 表示安装开始的日期和时间：

```
installActionsdate_time.log
```

要查看日志文件中的最新条目（问题信息最可能出现的位置），请输入类似于以下的命令：

```
$ tail -50 installActions2007-07-20_09-53-22AM.log | more
```

此命令显示日志文件的最后 50 行，并允许您逐页浏览。

如果 Oracle Universal Installer 显示的错误或日志文件中列出的错误表明存在重新链接问题，请参阅以下文件获取更多信息：

```
$ORACLE_HOME/install/make.log
```

### A.1.5 配置助手错误

要排查在配置助手运行期间发生的安装错误：

查看"查看安装会话日志"（第 A-4 页）一节中列出的安装日志文件。

查阅位于 Oracle RAC 安装所有者 Oracle 基目录中，路径为 `$ORACLE_BASE/cfgtoollogs` 的特定配置助手日志文件。尝试修复导致该错误的问题。

如果您看到“致命错误。请重新安装”消息，请通过查阅日志文件来寻找问题原因。有关进一步说明，请参考第 A-5 页的“致命错误”部分。

本节包含以下主题：

- 配置助手失败
- 致命错误

#### A.1.5.1 配置助手失败

Oracle 配置助手失败会在安装屏幕底部注明。配置助手界面会显示附加信息（如果可用）。配置助手执行状态存储在以下文件中：

```
oraInventory_location/logs/installActionsdate_time.log
```

有关配置助手相关错误的更多详细信息，请在以下目录中查找：

```
$ORACLE_BASE/cfgtoollogs
```

Oracle 基目录是 Oracle RAC 安装所有者的 Oracle 基目录。完成状态代码列于下表：

| 状态 | 结果代码 |
| :--- | :--- |
| 配置助手成功 | 0 |
| 配置助手失败 | 1 |
| 配置助手取消 | -1 |

#### A.1.5.2 致命错误

如果您在配置助手运行期间收到致命错误，则必须完成以下任务：

1. 卸载 Oracle 软件。
2. 纠正导致致命错误的原因。
3. 重新安装 Oracle 软件。

## A.2 关于在安装后使用 CVU 集群健康检查

从 Oracle Grid Infrastructure 11g 第 2 版 (11.2.0.3) 及更高版本开始，您可以使用 CVU healthcheck 命令选项来检查您的 Oracle Clusterware 和 Oracle Database 安装是否符合强制性要求和最佳实践指南，并检查其是否正常运行。

使用以下语法运行 healthcheck 命令选项：

```
cluvfy comp healthcheck [-collect {cluster | database}] [-db db_unique_name] [-bestpractice | -mandatory] [-deviations] [-html] [-save [-savedir directory_path]]
```

例如：

```
$ cd /home/grid/cvu_home/bin
$ ./cluvfy comp healthcheck -collect cluster -bestpractice -deviations -html
```

各选项含义如下：

- `-collect [cluster|database]`

  使用此标志指定要执行 Oracle Clusterware (cluster) 或 Oracle Database (database) 的检查。如果在使用 healthcheck 选项时不使用 `collect` 标志，则 `cluvfy comp healthcheck` 会同时检查 Oracle Clusterware 和 Oracle Database。

- `-db db_unique_name`

  使用此标志指定对 `db` 标志后输入的数据库唯一名称进行检查。

  CVU 使用 JDBC 以 `cvusys` 用户身份连接到数据库以验证各种数据库参数。因此，如果您想对使用 `-db` 标志指定的数据库执行检查，则必须首先在该数据库上创建 `cvusys` 用户，并向该用户授予 CVU 特定角色 `cvusapp`。您还必须授予 `cvusapp` 角色成员对系统表的 `select` 权限。

  `CVU_home/cv/admin/cvusys.sql` 中包含一个 SQL 脚本，用于创建此用户。使用此 SQL 脚本在所有要使用 CVU 验证的数据库上创建 `cvusys` 用户。

  如果使用 `db` 标志但未提供数据库唯一名称，则 CVU 会发现集群上的所有 Oracle Database。如果您想对这些数据库执行最佳实践检查，则必须在每个数据库上创建 `cvusys` 用户，并向该用户授予 `cvusapp` 角色以及执行最佳实践检查所需的 `select` 权限。

- `[-bestpractice | -mandatory] [-deviations]`

  使用 `bestpractice` 标志指定最佳实践检查，使用 `mandatory` 标志指定强制性检查。添加 `deviations` 标志指定您只想查看与最佳实践建议或强制性要求的偏差。您可以指定 `-bestpractice` 或 `-mandatory` 标志，但不能同时指定两者。如果既未指定 `-bestpractice` 也未指定 `-mandatory`，则会同时显示最佳实践和强制性要求。

- `-html`

  使用 `html` 标志以 HTML 格式生成详细报告。

  如果指定了 `html` 标志，并且系统上有 CVU 识别的浏览器，则在检查完成后浏览器会启动并显示报告。

  如果未指定 `html` 标志，则详细报告将以文本文件形式生成。

- `-save [-savedir dir_path]`



使用`save`或`-save -savedir`标志保存验证报告（`cvucheckreport_timestamp.txt`和`cvucheckreport_timestamp.htm`），其中`timestamp`是验证报告的时间和日期。

如果单独使用`save`标志，则报告保存在路径`CVU_home/cv/report`中，其中`CVU_home`是CVU二进制文件的位置。

如果使用`-save -savedir`标志并输入要保存CVU报告的路径，则CVU报告将保存在您指定的路径中。

## B 使用脚本或响应文件创建 Oracle Real Application Clusters 数据库

本附录描述了非交互式安装的步骤，在此过程中，您可以使用脚本创建 Oracle Real Application Clusters (Oracle RAC) 数据库。

> **注意：** 由数据库配置助手 (DBCA) 生成的脚本仅供参考。Oracle 强烈建议您使用 DBCA 创建数据库。

**另请参阅：** *Oracle Universal Installer and OPatch User's Guide for Windows and UNIX* 以获取有关生成脚本的详细信息

本附录包含以下主题：

- 使用 DBCA 生成 Oracle RAC 的安装脚本
- 关于 Oracle RAC 的 DBCA 非交互式（静默）配置
- 使用 Oracle RAC 的 DBCA 非交互式（静默）配置
- 响应文件如何工作
- 准备响应文件
- 使用响应文件运行 Oracle Universal Installer
- 使用响应文件运行 Net Configuration Assistant
- 使用响应文件运行配置助手
- 使用响应文件进行安装后配置

### B.1 使用 DBCA 生成 Oracle RAC 的安装脚本

要生成创建 Oracle RAC 数据库的脚本，使用脚本创建数据库并准备好数据库供使用，请完成以下步骤：

1. 启动 DBCA 并选择您喜欢的选项来构建 Oracle RAC 数据库。

   在 DBCA 会话的“创建选项”页面上，取消选中“创建数据库”，并在单击“完成”之前选择**生成数据库创建脚本**。您可以接受脚本的默认目标目录，也可以浏览其他位置。无论哪种情况，您都应记下路径名称以供下一步使用。

   > **另请参阅：** [第 3 章，“使用数据库配置助手创建 Oracle Real Application Clusters 数据库”](第 3 章，“使用数据库配置助手创建 Oracle Real Application Clusters 数据库”) 以获取有关运行 DBCA 会话的更多信息

2. 导航到 DBCA 创建脚本的目录，并查阅 SQL 脚本以确保它们包含构建具有所需特性的数据库的语句。如果不包含，Oracle 建议您重新运行 DBCA 以使用所需配置创建脚本，而不是自己编辑脚本。

3. 在您在 DBCA 会话中标识的每个集群节点上，运行脚本`sid.sh`，其中`sid`是您在 DBCA“数据库名”页面上输入的 SID 前缀。

4. 通过运行`ALTER SYSTEM`命令或在每个实例的 PFILE 中取消注释，将初始化参数`cluster_database`在 SPFILE 中设置为值`TRUE`。

5. 按照 [第 7 章，“了解 Oracle Real Application Clusters 已安装的配置”](第 7 章，“了解 Oracle Real Application Clusters 已安装的配置”) 中的说明配置 Oracle Net Services 以支持您的新数据库和实例。

6. 通过发出`ALTER SYSTEM`命令或在每个实例的 PFILE 中取消注释，在 SPFILE 中设置`local_listener`和`remote_listener`参数。

7. 按照 *Oracle Real Application Clusters Administration and Deployment Guide* 中的说明运行`SRVCTL`以配置和启动数据库及实例应用程序。

> **另请参阅：** *Oracle Universal Installer and OPatch User’s Guide for Windows and UNIX* 以获取有关使用 Oracle Universal Installer (OUI) 创建和使用脚本安装 Oracle 软件的更多信息

### B.2 关于 Oracle RAC 的 DBCA 非交互式（静默）配置

您可以使用 DBCA 执行 Oracle RAC 的非交互式或 *静默* 配置。要执行静默配置，您必须已完成 Oracle Grid Infrastructure (Oracle Clusterware and Oracle ASM) 安装，从 Oracle Database 主目录运行`root.sh`脚本，并定义 Oracle 主目录环境变量。

您可以使用 DBCA 从 Oracle 提供的模板或从您创建的模板创建数据库。模板包含针对特定类型工作负载优化的设置。

Oracle 提供以下两种工作负载类型的模板：

- 通用或事务处理
- 数据仓库

对于更复杂的环境，您可以选择“自定义数据库”选项。此选项不使用模板，会导致更广泛的安装访谈，这意味着创建数据库需要更长时间。

### B.3 使用 Oracle RAC 的 DBCA 非交互式（静默）配置

以下命令语法在现有的 Oracle ASM 磁盘组中创建 Oracle RAC 数据库，其中集群节点为`node1`和`node2`，磁盘组

### B.4 响应文件的工作原理

当你启动 OUI 时，可以使用响应文件来自动化 Oracle 软件的安装和配置过程，可以是完全自动化，也可以是部分自动化。OUI 使用响应文件中包含的值来回答部分或全部安装提示。

通常，安装程序以交互模式运行，这意味着它会在图形用户界面（GUI）屏幕上提示你提供信息。当你使用响应文件提供这些信息时，你需要通过命令提示符以以下任一模式运行安装程序：

- **静默模式**

  如果你在响应文件中包含了所有提示的答案，并在启动安装程序时指定了`-silent`选项，那么安装程序将以静默模式运行。在静默模式安装过程中，安装程序不会显示任何屏幕。相反，它会在你用于启动它的终端中显示进度信息。

- **响应文件模式**

  如果你在响应文件中包含了部分或全部提示的答案，但省略了`-silent`选项，那么安装程序将以响应文件模式运行。在响应文件模式安装过程中，安装程序会显示所有屏幕，包括你在响应文件中指定信息的屏幕，以及你未在响应文件中提供所需信息的屏幕。

你通过为响应文件中列出的变量输入值来定义静默或响应文件安装的设置。例如，要指定 Oracle 主目录名，请为`ORACLE_HOME`变量提供适当的值：

```
ORACLE_HOME="OraDBHome1"
```

另一种指定响应文件变量设置的方法是在运行安装程序时将其作为命令行参数传递。例如：

```
-silent "ORACLE_HOME=OraDBHome1" ...
```

在此命令中，*directory_path* 是 DVD 上`database`目录的路径，或硬盘上`Disk1`目录的路径。

> **另请参阅：** *Oracle Universal Installer and OPatch User's Guide for Windows and UNIX* 获取更多关于响应文件的信息。

#### B.4.1 使用静默模式或响应文件模式的原因

下表提供了以静默模式或响应文件模式运行安装程序的用例。

| 模式 | 用途 |
| :--- | :--- |
| 静默 | 在以下安装中使用静默模式：• 完成无人值守安装，你可以使用操作系统工具（如`at`）进行调度。• 在多个系统上完成多次类似安装，无需用户交互。• 在未安装 X Window System 软件的系统上安装软件。安装程序在你用于启动它的终端上显示进度信息，但不显示任何安装程序屏幕。 |
| 响应文件 | 如果你想在多个系统上完成类似的 Oracle 软件安装，并为部分但不是全部安装程序提示提供默认答案，则使用响应文件模式。如果你未在响应文件中指定特定安装程序屏幕所需的信息，那么安装程序将显示该屏幕。对于你已提供所有必需信息的屏幕，它会进行抑制。 |

#### B.4.2 使用 Oracle ASM 创建数据库文件

在创建使用 Oracle 自动存储管理（Oracle ASM）的数据库之前，你必须运行`root.sh`脚本。因此，在静默模式安装期间，你无法使用 Oracle ASM 作为数据库文件的存储选项来创建数据库。相反，你可以使用静默模式完成仅软件安装，然后在完成仅软件安装并运行`root.sh`脚本后，以静默模式运行 Oracle Net Configuration Assistant 和 DBCA。

> **注意：** 此限制仅适用于使用 Oracle 自动存储管理作为数据库文件存储选项的数据库。你可以在静默模式安装期间创建使用文件系统选项的数据库。

#### B.4.3 使用响应文件的一般步骤

以下是使用安装程序以静默或响应文件模式安装和配置 Oracle 产品的通用步骤：

> **注意：** 你必须在以静默或响应文件模式运行安装程序之前，在系统上完成所有必需的预安装任务。

1. 如果服务器上不存在`oraInst.loc`文件，则创建它。
2. 准备响应文件。
3. 以静默或响应文件模式运行安装程序。
4. 如果你完成了仅软件安装，则以静默或响应文件模式运行 Net Configuration Assistant 和 DBCA。

这些步骤将在以下部分中描述。

### B.5 准备响应文件

本节介绍了准备响应文件以供静默模式或响应文件模式安装期间使用的方法：

- 编辑响应文件模板
- 录制响应文件

#### B.5.1 编辑响应文件模板

Oracle 为每个产品、安装类型以及每个配置工具提供了响应文件模板。这些文件位于安装介质上的`database/response`目录中。

> **注意：** 如果你已将软件复制到硬盘，则响应文件位于`/Disk1/response`目录中。

表 B–1 列出了此软件提供的响应文件：

**表 B–1 Oracle Database 的响应文件**

| 响应文件 | 描述 |
|---|---|
| `db_install.rsp` | Oracle Database 11g 的静默安装 |
| `dbca.rsp` | DBCA 的静默安装 |
| `netca.rsp` | Oracle Net Configuration Assistant 的静默安装 |

> **警告：** 当你修改响应文件模板并保存文件以供使用时，响应文件可能包含明文密码。响应文件的所有权应仅授予 Oracle 软件安装所有者，并且应将响应文件的权限更改为 600。Oracle 强烈建议数据库管理员或其他管理员在不使用响应文件时删除或保护它们。

要复制和修改响应文件：

1. 将响应文件从响应文件目录复制到系统上的目录：

   ```
   $ cp /directory_path/response/response_file.rsp local_directory
   ```

   在此示例中，`directory_path`是安装介质上`database`目录的路径。如果你已将软件复制到硬盘，也可以选择在`response`目录中编辑该文件。

2. 在文本编辑器中打开响应文件：

   ```
   $ vi /local_dir/response_file.rsp
   ```

   **另请参阅：** *Oracle Universal Installer and OPatch User's Guide for Windows and UNIX* 获取有关创建响应文件的详细信息。

3. 按照文件中的说明进行编辑。

> **注意：** 如果你未正确配置响应文件，安装程序或配置助手将会失败。

4. 将文件的权限更改为 600：

   ```
   $ chmod 600 /local_dir/response_file.rsp
   ```

> **注意：** Oracle Database 安装的完全指定的响应文件包含数据库管理账户和 OSDBA 组成员用户（自动备份所需）的密码。确保只有 Oracle 软件所有者用户才能查看或修改响应文件，或考虑在安装成功后删除它们。

#### B.5.2 录制响应文件

你可以使用交互模式下的 OUI 录制响应文件，然后对其进行编辑，用于完成静默模式或响应文件模式安装。此方法对于高级安装或仅软件安装很有用。

从 Oracle Database 11g Release 2 (11.2) 开始，你可以在安装过程中通过单击摘要页面上的**保存响应文件**将所有安装步骤保存到响应文件中。你可以使用生成的响应文件进行后续的静默安装。

在录制响应文件时，你可以完成安装，也可以在摘要页面退出安装程序，然后再开始将软件复制到系统之前。

如果在响应文件模式安装期间使用录制模式，那么安装程序会将原始源响应文件中指定的变量值记录到新的响应文件中。

> **注意：** 录制响应文件时无法保存密码。

要录制响应文件：

1. 完成与正常安装相同的预安装任务。当你运行安装程序录制响应文件时，它会检查系统以验证其是否满足安装软件的要求。因此，Oracle 建议你完成所有必需的预安装任务，并在完成安装时录制响应文件。

2. 确保 Oracle 软件所有者用户（通常是`oracle`）具有创建或写入 Oracle 主目录路径的权限，该路径将在运行安装程序时指定。

3. 在每个安装屏幕上，指定所需信息。

4. 当安装程序显示摘要屏幕时，执行以下操作：

   a. 单击**保存响应文件**并指定文件名和位置以保存响应文件的值。

   b. 单击**完成**以创建响应文件并继续安装。如果不想继续安装，请单击**取消**。安装将停止，但录制的响应文件将被保留。

## B.4 使用 Oracle ASM 创建数据库文件

在创建使用 Oracle 自动存储管理（Oracle ASM）的数据库之前，你必须运行`root.sh`脚本。因此，在静默模式安装期间，你无法使用 Oracle ASM 作为数据库文件的存储选项来创建数据库。相反，你可以使用静默模式完成仅软件安装，然后在完成仅软件安装并运行`root.sh`脚本后，以静默模式运行 Oracle Net Configuration Assistant 和 DBCA。

> **注意：** 此限制仅适用于使用 Oracle 自动存储管理作为数据库文件存储选项的数据库。你可以在静默模式安装期间创建使用文件系统选项的数据库。

## B.5 使用响应文件的一般步骤

以下是使用安装程序以静默或响应文件模式安装和配置 Oracle 产品的通用步骤：

> **注意：** 你必须在以静默或响应文件模式运行安装程序之前，在系统上完成所有必需的预安装任务。

1. 如果服务器上不存在`oraInst.loc`文件，则创建它。
2. 准备响应文件。
3. 以静默或响应文件模式运行安装程序。
4. 如果你完成了仅软件安装，则以静默或响应文件模式运行 Net Configuration Assistant 和 DBCA。

这些步骤将在以下部分中描述。

## B.6 准备响应文件

本节介绍了准备响应文件以供静默模式或响应文件模式安装期间使用的方法：

- 编辑响应文件模板
- 录制响应文件

### B.6.1 编辑响应文件模板

Oracle 为每个产品、安装类型以及每个配置工具提供了响应文件模板。这些文件位于安装介质上的`database/response`目录中。

> **注意：** 如果你已将软件复制到硬盘，则响应文件位于`/Disk1/response`目录中。

**表 B–1 Oracle Database 的响应文件**

| 响应文件 | 描述 |
|---|---|
| `db_install.rsp` | Oracle Database 11g 的静默安装 |
| `dbca.rsp` | DBCA 的静默安装 |
| `netca.rsp` | Oracle Net Configuration Assistant 的静默安装 |

> **警告：** 当你修改响应文件模板并保存文件以供使用时，响应文件可能包含明文密码。响应文件的所有权应仅授予 Oracle 软件安装所有者，并且应将响应文件的权限更改为 600。Oracle 强烈建议数据库管理员或其他管理员在不使用响应文件时删除或保护它们。

要复制和修改响应文件：

1. 将响应文件从响应文件目录复制到系统上的目录：

   ```
   $ cp /directory_path/response/response_file.rsp local_directory
   ```

   在此示例中，`directory_path`是安装介质上`database`目录的路径。如果你已将软件复制到硬盘，也可以选择在`response`目录中编辑该文件。

2. 在文本编辑器中打开响应文件：

   ```
   $ vi /local_dir/response_file.rsp
   ```

   **另请参阅：** *Oracle Universal Installer and OPatch User's Guide for Windows and UNIX* 获取有关创建响应文件的详细信息。

3. 按照文件中的说明进行编辑。

> **注意：** 如果你未正确配置响应文件，安装程序或配置助手将会失败。

4. 将文件的权限更改为 600：

   ```
   $ chmod 600 /local_dir/response_file.rsp
   ```



> **注意：** Oracle Database 安装的完全指定的响应文件包含数据库管理账户和 OSDBA 组成员用户（自动备份所需）的密码。确保只有 Oracle 软件所有者用户才能查看或修改响应文件，或考虑在安装成功后删除它们。

### B.6.2 录制响应文件

你可以使用交互模式下的 OUI 录制响应文件，然后对其进行编辑，用于完成静默模式或响应文件模式安装。此方法对于高级安装或仅软件安装很有用。

从 Oracle Database 11g Release 2 (11.2) 开始，你可以在安装过程中通过单击摘要页面上的**保存响应文件**将所有安装步骤保存到响应文件中。你可以使用生成的响应文件进行后续的静默安装。

在录制响应文件时，你可以完成安装，也可以在摘要页面退出安装程序，然后再开始将软件复制到系统之前。

如果在响应文件模式安装期间使用录制模式，那么安装程序会将原始源响应文件中指定的变量值记录到新的响应文件中。

> **注意：** 录制响应文件时无法保存密码。

要录制响应文件：

1. 完成与正常安装相同的预安装任务。当你运行安装程序录制响应文件时，它会检查系统以验证其是否满足安装软件的要求。因此，Oracle 建议你完成所有必需的预安装任务，并在完成安装时录制响应文件。

2. 确保 Oracle 软件所有者用户（通常是`oracle`）具有创建或写入 Oracle 主目录路径的权限，该路径将在运行安装程序时指定。

3. 在每个安装屏幕上，指定所需信息。

4. 当安装程序显示摘要屏幕时，执行以下操作：

   a. 单击**保存响应文件**并指定文件名和位置以保存响应文件的值。

   b. 单击**完成**以创建响应文件并继续安装。如果不想继续安装，请单击**取消**。安装将停止，但录制的响应文件将被保留。

组名称为`ASMgrp1`，密码为`my_password`，ASM SYS 密码为`My_ASM_Password`：

```
# su oracle -c "$ORACLE_HOME/bin/dbca -silent -createDatabase -templateName General_Purpose.dbc -gdbName $DBNAME -sid $SID -sysPassword my_password -systemPassword my_password -sysmanPassword my_password -dbsnmpPassword my_password -emConfiguration LOCAL -storageType ASM -diskGroupName ASMgrp1 -datafileJarLocation $ORACLE_HOME/assistants/dbca/templates -nodeinfo node1,node2 -characterset WE8ISO8859P1 -obfuscatedPasswords false -sampleSchema false -asmSysPassword My_ASM_password"
```

### B.6 使用响应文件运行 Oracle Universal Installer

现在，你已经准备好在命令行运行 OUI，指定你创建的响应文件来执行安装。OUI 可执行文件`runInstaller`提供了多个选项。要获取所有这些选项的完整帮助信息，请使用`-help`选项运行`runInstaller`命令，例如：

`$ directory_path/runInstaller -help`

帮助信息会在一段时间后显示在一个窗口中。

要使用响应文件运行安装程序：

1. 完成与正常安装相同的预安装任务。

2. 以软件安装所有者用户身份登录。

3. 如果你要完成响应文件模式安装，请设置`DISPLAY`环境变量。

   > **注意：** 如果你要完成静默模式安装，则无需设置`DISPLAY`环境变量。

4. 要以静默或响应文件模式启动安装程序，请输入类似以下的命令：

   `$ /directory_path/runInstaller [-silent] [-noconfig] \`

   `  -responseFile responsefilename`

   > **注意：** 不要为响应文件指定相对路径。如果指定相对路径，安装程序将失败。

   在此示例中：

   - `directory_path`是 DVD 上`database`目录的路径，或硬盘上`Disk1`目录的路径。

   - `-silent`表示你要以静默模式运行安装程序。

   - `-noconfig`会抑制在安装过程中运行配置助手，改为仅执行软件安装。

   - `responsefilename`是你配置的安装响应文件的完整路径和文件名。

5. 安装完成后，以`root`用户身份登录并运行`root.sh`脚本：

   `$ sudo sh`

   `password:`

   `# /oracle_home_path/root.sh`

### B.7 使用响应文件运行 Net Configuration Assistant

你可以以静默模式运行 Net Configuration Assistant，以在系统上配置和启动 Oracle Net 监听器、配置命名方法以及配置 Oracle Net 服务名称。要以静默模式运行 Net Configuration Assistant，你必须复制并编辑响应文件模板。Oracle 在 DVD 上`database/response`目录中的`response`目录下提供了名为`netca.resp`的响应文件模板。

> **注意：** 如果你已将软件复制到硬盘，则响应文件模板位于`database/response`目录中。

要使用响应文件运行 Net Configuration Assistant：

1. 将`netca.rsp`响应文件模板从响应文件目录复制到系统上的某个目录：

   `$ cp /directory_path/response/netca.rsp local_directory`

   在此示例中，`directory_path`是 DVD 上`database`目录的路径。如果你已将软件复制到硬盘，你也可以在`response`目录中编辑该文件。

2. 在文本编辑器中打开响应文件：

   `$ vi /local_dir/netca.rsp`

3. 按照文件中的说明进行编辑。

   > **注意：** 如果未正确配置响应文件，Net Configuration Assistant 将失败。

4. 以 Oracle 软件所有者用户身份登录，并设置`ORACLE_HOME`环境变量以指定正确的 Oracle 主目录。

5. 输入类似以下的命令以静默模式运行 Net Configuration Assistant：

   `$ $ORACLE_HOME/bin/netca /silent /responsefile /local_dir/netca.rsp`

   在此命令中：

   - `/silent`选项表示以静默模式运行 Net Configuration Assistant。

   - `local_dir`是你复制`netca.rsp`响应文件模板的目录的完整路径。

### B.8 使用响应文件运行配置助手

你可以在响应文件或静默模式下运行配置助手，以在 Oracle 软件安装到系统后进行配置和启动。要在响应文件或静默模式下运行配置助手，你必须复制并编辑响应文件模板。

> **注意：** 如果你已将软件复制到硬盘，则响应文件模板位于`Disk1/response`目录中。

本节包含以下主题：

- 关于响应文件模式下的 Database Configuration Assistant

- 在响应文件或静默模式下运行 Database Configuration Assistant

- 关于安装后配置文件

- 使用响应文件运行安装后配置

#### B.8.1 关于响应文件模式下的 Database Configuration Assistant

在响应文件模式下，DBCA 使用你在响应文件中指定的值或作为命令行选项指定的值来创建数据库。当它配置和启动数据库时，会显示一个包含状态消息和进度条的窗口。它显示的窗口与在企业版或标准版安装过程中创建预配置数据库时显示的窗口相同。

要在响应文件模式下运行 DBCA，请使用图形显示并设置`DISPLAY`环境变量。使用`-progressOnly`标志将运行模式设置为响应文件模式。

Oracle 在 DVD 上的`/Disk1/response`目录中提供了名为`dbca.rsp`的响应文件模板。

#### B.8.2 在响应文件或静默模式下运行 Database Configuration Assistant

要在响应文件或静默模式下运行 DBCA：

1. 将`dbca.rsp`响应文件模板从响应文件目录复制到系统上的某个目录：

   `$ cp /directory_path/response/dbca.rsp local_directory`

   在此示例中，`directory_path`是 DVD 上`database`目录的路径。如果你已将软件复制到硬盘，你也可以在`response`目录中编辑该文件。

   > **注意：** 作为编辑响应文件模板的替代方法，你也可以在运行 DBCA 时通过命令行选项指定所有必需信息来创建数据库。要了解支持的选项列表，请输入以下命令：

   `$ $ORACLE_HOME/bin/dbca -help`

2. 在文本编辑器中打开响应文件：

   `$ vi /local_dir/dbca.rsp`

3. 按照文件中的说明编辑文件。

   > **注意：** 如果未正确配置响应文件，DBCA 将失败。

4. 以 Oracle 软件所有者用户身份登录，并设置`ORACLE_HOME`环境变量以指定正确的 Oracle 主目录。

5. 要在响应文件模式下运行 DBCA，请设置`DISPLAY`环境变量。

6. 使用以下命令语法以静默或响应文件模式运行 DBCA：

   `$ORACLE_HOME/bin/dbca {-progressOnly | -silent} -responseFile \`

   `/local_dir/dbca.rsp`

   在此示例中：

   - `-silent`选项表示你要以静默模式运行 DBCA。

   - `-progressOnly`选项表示你要以响应文件模式运行 DBCA。

   - `local_dir`是你复制`dbca.rsp`响应文件模板的目录的完整路径。

### B.9 使用响应文件进行安装后配置

以下各节介绍如何在安装 Oracle 软件后创建和运行响应文件配置。本节中的主题包括：

- 关于安装后配置文件

- 使用响应文件运行安装后配置

#### B.9.1 关于安装后配置文件

当你运行静默或响应文件安装时，你在响应文件中提供有关服务器的信息，这些信息在图形用户界面安装中通常需要手动提供。但是，响应文件不包含配置助手在软件安装完成后所需的用户账户密码。配置助手通过名为`configToolAllCommands`的脚本启动。你可以通过使用密码响应文件在响应文件模式下运行此脚本。该脚本使用密码依次运行配置工具以完成配置。

如果你保留密码文件用于克隆安装，Oracle 强烈建议你将密码文件存储在安全位置。此外，如果你需要停止安装以修复错误，你可以使用`configToolAllCommands`和密码响应文件来运行配置助手。

`configToolAllCommands`密码响应文件具有以下语法选项：

- `internal_component_name`是配置助手配置的组件名称。

- `variable_name`是配置文件变量的名称。

- `value`是要用于配置的所需值。

命令语法如下：

`internal_component_name|variable_name=value`

例如：

`oracle.assistants.asm|S_ASMPASSWORD=myPassWord`

Oracle 强烈建议您使用密码响应文件来维护安全性：

- 响应文件的权限应设置为 600。

- 响应文件的所有者应为安装所有者用户，其所属组应设置为中央清单（`oraInventory`）组。

#### B.9.2 使用响应文件运行安装后配置

要使用`configToolAllCommands`脚本运行配置助手，请执行以下操作：

1. 使用语法`filename.properties`创建响应文件。例如：

   `$ touch cfgrsp.properties`

2. 使用文本编辑器打开该文件，剪切并粘贴密码模板，并根据需要进行修改。

**示例 B-1 用于 Oracle Real Application Clusters 的密码响应文件**

Oracle 数据库配置需要为 DBCA 提供 SYS、SYSTEM、SYSMAN 和 DBSNMP 密码。仅当数据库使用 Oracle ASM 进行存储时，才需要提供`S_ASMSNMPPASSWORD`响应。此外，如果选择了配置 Oracle Enterprise Manager，则必须提供 Oracle 软件安装所有者用户的密码作为`S_HOSTUSERPASSWORD`响应。

```
oracle.assistants.server|S_SYSPASSWORD=password
oracle.assistants.server|S_SYSTEMPASSWORD=password
oracle.assistants.server|S_SYSMANPASSWORD=password
oracle.assistants.server|S_DBSNMPPASSWORD=password
oracle.assistants.server|S_HOSTUSERPASSWORD=password
oracle.assistants.server|S_ASMSNMPPASSWORD=password
```

如果不想启用 Oracle Enterprise Manager 或 Oracle ASM，请将这些密码字段留空。

3. 更改文件权限以确保文件安全。例如：

   `$ ls -al cfgrsp.properties`

   `-rw------- 1 oracle oinstall 0 Apr 30 17:30 cfgrsp.properties`

4. 切换到`$ORACLE_BASE/cfgtoollogs`目录

   使用以下语法运行配置脚本：

   `configToolAllCommands RESPONSE_FILE=/path/name.properties`

   例如：

   `$ ./configToolAllCommands RESPONSE_FILE=/home/oracle/cfgrsp.properties`

#### 使用响应文件进行安装后配置

B-12 Oracle Real Application Clusters 安装指南

## 从单实例 Oracle 数据库转换为 Oracle RAC 和 Oracle RAC One Node

本附录介绍将 Oracle Database 11g 第 2 版 (11.2) 单实例数据库转换为 Oracle Real Application Clusters (Oracle RAC) 和 Oracle RAC One Node 数据库的过程。本附录包含以下主题：

- 将数据库转换为 Oracle RAC 的管理问题

- 使用 DBCA 转换为 Oracle RAC 和 Oracle RAC One Node

- 使用 rconfig 和 Oracle Enterprise Manager 准备转换

- 使用 RCONFIG 将数据库转换为 Oracle RAC

- ConvertToRAC 的 Rconfig XML 输入文件示例

- 转换后步骤

如果您从 Oracle Parallel Server 升级到 Oracle RAC，或者从 Oracle RAC 的早期版本升级，请使用 Oracle Database Upgrade Assistant (DBUA)。

本章中的过程假定原始单实例数据库和目标 Oracle RAC 数据库使用相同的版本，并运行在同一平台上。

> **注意：** 对于 Oracle RAC 数据库，必须使用集群化的 Oracle ASM 实例。

**另请参见：** *Oracle Database Licensing Information*，了解适用于您所购买许可证的合规要求

### C.1 将数据库转换为 Oracle RAC 的管理问题

在将单实例数据库转换为 Oracle RAC 之前，请注意以下管理事项：

- 从单实例 Oracle 数据库转换为 Oracle RAC 之前，应提供备份过程。

- 对于 Oracle RAC 环境中的归档，归档文件格式需要一个线程号。

- Oracle RAC 数据库所有实例的归档日志都是介质恢复所必需的。因此，如果归档到文件且不使用集群文件系统，或采用其他方式提供共享文件系统，则必须能够从集群数据库拥有实例的所有节点访问归档日志。

- 默认情况下，所有数据库文件都会迁移到 Oracle 托管文件 (OMF)。该功能简化了表空间创建，确保数据文件位置一致并符合 OFA 规则，并减少了数据文件管理中的人为错误。

### C.2 使用 DBCA 转换为 Oracle RAC 和 Oracle RAC One Node



可以使用数据库配置助手（`DBCA`）将单实例 Oracle我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。数据库转换为 Oracle RAC 或 Oracle RAC One Node。`DBCA` 自动配置控制文件属性、创建还原表空间和重做日志，并为集群环境生成初始化参数文件条目。`DBCA` 还配置 Oracle Net Services、Oracle Clusterware 资源，以及 Oracle Enterprise Manager 或 SRVCTL 实用程序（`SRVCTL`）用于 Oracle RAC 数据库管理的配置。

在使用 `DBCA` 将单实例数据库转换为 Oracle RAC 或 Oracle RAC One Node 数据库之前，请确保系统满足以下条件：

- 硬件和操作系统软件配置必须受支持。
- 它具有共享存储：Oracle Cluster File System 或 Oracle ASM 必须在所有节点上可用且可访问。在 POWER 系统上的 Linux 中，请确保 GPFS 在所有节点上均可用且可访问。
- 您的应用程序没有任何设计特性妨碍其与集群数据库处理一起使用。

如果您的平台支持集群文件系统，则可以将其用于 Oracle RAC。您也可以转换为 Oracle RAC 并使用非共享文件系统。无论哪种情况，Oracle 强烈建议您使用 Oracle Universal Installer（`OUI`）执行 Oracle Database 11g 第 2 版（11.2）安装，以便在集群中每个选定节点的相同位置设置 Oracle 主目录和清单。

本节介绍以下方案：

- 使用 `DBCA` 将 Oracle Database 11g 安装转换为 Oracle RAC
- 使用 `DBCA` 将集群上的单实例转换为 Oracle RAC

## C.2.1 使用 DBCA 将 Oracle Database 11g 安装转换为 Oracle RAC

要将位于非集群计算机上的单实例 Oracle 数据库转换为 Oracle RAC，请按以下顺序执行以下各节中介绍的过程：

- 备份原始单实例数据库
- 完成 Oracle Clusterware 安装
- 验证集群
- 复制预配置数据库映像
- 安装 Oracle Database 11g 软件（含 Oracle RAC）

### C.2.1.1 备份原始单实例数据库

使用 `DBCA` 通过以下过程创建单实例数据库的预配置映像：

1. 导航至 `$ORACLE_HOME` 中的 `bin` 目录，并启动 `DBCA`。
2. 在欢迎页面中，单击**下一步**。
3. 在操作页面中，选择**管理模板**，然后单击**下一步**。
4. 在模板管理页面中，选择**创建数据库模板**和**从现有数据库（结构及数据）**，然后单击**下一步**。
5. 在源数据库页面中，在**数据库实例**列表中选择数据库名称，然后单击**下一步**。
6. 在模板属性页面中，在**名称**字段中输入模板名称。Oracle 建议使用数据库名称。

   默认情况下，模板文件生成在`ORACLE_HOME/assistants/dbca/templates`目录中。如果愿意，可以在**描述**字段中输入文件说明，并在**模板数据文件**字段中更改模板文件位置。

   完成输入后，单击**下一步**。

7. 在数据库相关文件位置页面中，选择**保持文件位置**，以便将数据库恢复到当前目录结构，然后单击**完成**。

   `DBCA` 会生成两个文件：数据库结构文件（*template_name*.dbc）和数据库预配置映像文件（*template_name*.dfb）。

### C.2.1.2 完成 Oracle Clusterware 安装

按照适用于您平台的 *Oracle Grid Infrastructure 安装指南*完成 Oracle Clusterware 安装。

### C.2.1.3 验证集群

使用集群验证工具（`CVU`）验证集群配置。

### C.2.1.4 复制预配置数据库映像

复制预配置数据库映像。这包括将 `DBCA` 在上一个过程“备份原始单实例数据库”（第 C-2 页）中创建的数据库结构 *.dbc 文件和数据库预配置映像 *.dfb 文件复制到集群中您计划运行 `DBCA` 的节点上的临时位置。

### C.2.1.5 安装 Oracle Database 11g 软件（含 Oracle RAC）

1. 运行 `OUI` 执行包含 Oracle RAC 的 Oracle 数据库安装。
2. 在 `OUI` 的“指定硬件集群安装”页面中，选择**集群安装模式**，然后选择要包含在 Oracle RAC 数据库中的节点。
3. 在 `OUI` 数据库配置类型页面中，选择**高级**安装类型。

   安装 Oracle 数据库软件后，`OUI` 会运行安装后配置工具，例如网络配置助手（`NETCA`）、`DBCA` 等。

4. 在 `DBCA` 模板选择页面中，使用在“复制预配置数据库映像”过程中复制到临时位置的模板。使用浏览选项选择模板位置。

## C.2.2 使用 DBCA 将集群上的单实例转换为 Oracle RAC One Node

选择您要部署的选项。您的选择包括：Oracle RAC 数据库；Oracle RAC One Node 数据库；或 Oracle 单实例数据库。

5. 如果您在 `OUI` 存储选项页面上选择了原始存储，并且尚未设置 `DBCA_RAW_CONFIG` 环境变量，那么请在初始化参数页面的 `DBCA` 文件位置选项卡上，用相应的原始设备文件替换数据文件、控制文件和日志文件等。您还必须在存储页面上用原始设备替换默认的数据库文件。

> **另请参阅：** [第 3 章，“使用数据库配置助手创建 Oracle Real Application Clusters 数据库”](http://example.com) 了解更多关于 `DBCA` 的详细信息

6. 创建 Oracle RAC 数据库后，`DBCA` 将显示密码管理页面，您必须在该页面上更改具有 `SYSDBA` 和 `SYSOPER` 角色的数据库特权用户的密码。当 `DBCA` 退出时，转换过程即完成。

请使用 `DBCA` 按照以下过程将单实例 Oracle 数据库转换为 Oracle RAC One Node：

1. 切换目录到 `$ORACLE_HOME/bin`。
2. 启动 `DBCA`：`$ dbca`。
3. 从欢迎窗口中，选择 **Oracle Real Application Clusters** 数据库。
4. 使用您在 [C.2.1.5 节，“安装带 Oracle RAC 的 Oracle Database 11g 软件”](#) 中选择的模板进行部署。

## C.2.3 使用 DBCA 将集群上的单实例转换为 Oracle RAC

单实例数据库可以存在于集群计算机上，有三种场景：

- 场景 1：运行单实例数据库的 Oracle 主目录是集群安装的。执行到 Oracle RAC 的转换的步骤在第 C-4 页的 [“从集群启用的 Oracle 主目录运行的集群上的单实例”](#page C-4) 中描述。
- 场景 2：运行单实例数据库的 Oracle 主目录是集群安装的，但 Oracle RAC 功能已禁用。有关如何在该环境中将数据库转换为 Oracle RAC 的说明，请参阅第 C-7 页的 [“从禁用 Oracle RAC 的 Oracle 主目录运行的集群上的单实例”](#page C-7)。
- 场景 3：运行单实例数据库的 Oracle 主目录不是集群安装的。将单实例数据库转换为 Oracle RAC 的过程在第 C-7 页的 [“从单实例安装的 Oracle 主目录运行的集群上的单实例”](#page C-7) 中描述。

### C.2.3.1 从集群启用的 Oracle 主目录运行的集群上的单实例

执行以下过程，将运行在集群上、从集群安装的（带 Oracle RAC 的 Oracle Database 11g）Oracle 主目录运行的单实例数据库进行转换。

1. 使用 `DBCA` 创建单实例数据库的预配置映像，如第 C-2 页 [“备份原始单实例数据库”](Back Up the Original Single-Instance Database) 一节所述。要手动执行转换，请关闭单实例数据库。
2. 要向集群添加节点，请按照适用于您平台的 *Oracle Grid Infrastructure 安装指南* 中的描述，将这些节点添加并连接到集群。确保所有这些节点都能访问共享存储。此外，按照 *Oracle Clusterware 管理和部署指南* 中“将 Clusterware 和 Oracle 软件扩展到新节点”的过程，将 Oracle Clusterware 主目录扩展到新节点。
3. 从现有的 Oracle 主目录，按照 *Oracle Clusterware 管理和部署指南* 中“在 Oracle RAC 数据库层添加节点”的过程，将此主目录扩展到新节点。
4. 从新添加的节点之一，使用 `NETCA` 配置附加节点上的监听器。选择与现有节点上使用的相同端口号和协议。如果 `NETCA` 在节点列表页面上显示了现有节点，则不要选择该节点，因为该节点上的监听器已经配置好了。
5. 使用以下任一过程转换数据库：

   - [使用 DBCA 的自动转换过程](Automated Conversion Procedure Using DBCA)
   - [手动转换过程](Manual Conversion Procedure)

#### C.2.3.1.1 使用 DBCA 的自动转换过程

1. 如果您按照第 C-2 页 [“备份原始单实例数据库”](Back Up the Original Single-Instance Database) 一节所述创建了单实例数据库的预配置映像，那么使用 `DBCA` 完成转换为 Oracle RAC 数据库。
2. 从初始节点启动 `DBCA`。选择要作为集群数据库一部分包含的节点名称。在模板选择页面上，选择您在第 C-5 页步骤 1 中创建的预配置模板。输入数据库名称并响应其余的 `DBCA` 提示。
3. 要为集群数据库文件使用原始设备：当初始化参数页面出现时，在文件位置选项卡上为 `SPFILE` 输入原始设备名称。在存储页面上，用控制文件、重做日志和数据文件的原始设备替换默认的数据库文件名，以创建集群数据库。单击 **完成**，然后创建数据库。

创建 Oracle RAC 数据库后，`DBCA` 将显示密码管理页面，您必须在该页面上更改具有 `SYSDBA` 和 `SYSOPER` 角色的数据库特权用户的密码。当 `DBCA` 退出时，转换过程即完成。

#### C.2.3.1.2 手动转换过程

由于您在第 C-5 页的步骤 1 中未使用 `DBCA` 创建单实例数据库的预配置映像，请执行以下步骤完成转换：

1. 在您已添加的每个节点上创建最优灵活体系结构（`OFA`）目录结构。

   **另请参阅：** 第 D-1 页的 [“Oracle RAC 的目录结构”](Directory Structures for Oracle RAC) 以获取有关 `OFA` 的更多信息

2. 如果要将文件系统上的单实例数据库文件转换为原始设备，请使用 `dd` 命令将数据库数据文件、控制文件、重做日志和服务器参数文件复制到其对应的原始设备。否则，请继续下一步。
3. 通过运行带有 `REUSE` 关键字的 `CREATE CONTROLFILE` SQL 语句重新创建控制文件，并根据 Oracle RAC 配置的需要指定 `MAXINSTANCES` 和 `MAXLOGFILES` 等。`MAXINSTANCES` 的建议默认值为 32。
4. 关闭数据库实例。
5. 如果您的单实例数据库使用的是 `SPFILE`，则使用以下 SQL 语句从 `SPFILE` 创建一个临时 `PFILE`：

   ```sql
   CREATE PFILE='pfile_name' from spfile='spfile_name'
   ```

6. 将 `CLUSTER_DATABASE` 参数设置为 `TRUE`，使用 `sid.parameter=value` 语法将 `INSTANCE_NUMBER` 参数设置为每个实例的唯一值。

   如果您在单实例数据库上优化了内存使用，那么在转换为 Oracle RAC 时，请调整系统全局区（`SGA`）的大小以避免交换和分页。您应该进行此调整，因为 Oracle RAC 需要大约 350 字节用于每个缓冲区以容纳全局缓存服务（`GCS`）。例如，如果您有 10,000 个缓冲区，那么 Oracle RAC 需要大约 350 乘以 10,000 字节的额外内存。因此，请通过相应更改 `DB_CACHE_SIZE` 和 `DB_nK_CACHE_SIZE` 参数来调整 `SGA` 的大小。

7. 使用第 5 步创建的 `PFILE` 启动数据库实例。
8. 如果您的单实例数据库使用的是自动撤销管理，则使用 `CREATE UNDO TABLESPACE` SQL 语句为每个附加实例创建一个撤销表空间。如果您使用的是原始设备，请确保撤销表空间的数据文件位于原始设备上。
9. 为每个附加实例创建至少包含两个重做日志的重做线程。如果您使用的是原始设备，请确保重做日志文件位于原始设备上。使用 `ALTER DATABASE` SQL 语句启用新的重做线程。然后，关闭数据库实例。
10. 将 Oracle 密码文件从初始节点或您正在工作的节点复制到集群数据库将有实例的附加节点的相应位置。为每个附加实例适当替换每个密码文件中的 `ORACLE_SID` 名称。
11. 将 `REMOTE_LISTENER=LISTENER_DB_NAME` 和 `sid.LOCAL_LISTENER=LISTENER_SID` 参数添加到 `PFILE` 中。
12. 在 `tnsnames.ora` 文件中配置数据库和实例的网络服务条目，以及每个实例的 `LOCAL_LISTENER` 和 `REMOTE_LISTENER` 的地址条目。完成此操作后，将这些文件复制到所有节点。
13. 按照第 5-3 页“迁移到服务器参数文件的过程”一节中的过程，从 `PFILE` 创建 `SPFILE`。如果您未使用集群文件系统，请确保 `SPFILE` 位于原始设备上。
14. 创建包含以下条目的 `$ORACLE_HOME/dbs/initsid.ora` 文件：

    ```
    spfile='spfile_path_name'
    ```

    变量 `spfile_path_name` 是 `SPFILE` 的完整路径名。

15. 在本地节点上，运行 `catclust.sql`。此命令创建 Oracle RAC 数据库所需的字典视图。例如：

    ```sql
    SQL> start ?/rdbms/admin/catclust.sql
    ```

### C.2.3.2 在已禁用 Oracle RAC 功能的 Oracle 主目录中运行集群上的单实例

如果您执行了单节点集群（包含 Oracle RAC）安装，但后来通过取消与 `oracle` 二进制文件的链接禁用了 Oracle RAC 功能，则可以在集群上从已禁用 Oracle RAC 的 Oracle 主目录中安装单实例。（但是，您也可以在节点选择页面上选择 **本地** 和 **非集群** 选项，在已禁用 Oracle RAC 的集群上创建单实例主目录。）执行以下步骤将这种类型的单实例数据库转换为 Oracle RAC 数据库：

1. 使用 `DBCA` 按照 C-2 页“备份原始单实例数据库”一节中的描述，为您的单实例数据库创建预配置映像。要手动执行转换，请关闭单实例数据库。
2. 切换到 Oracle 主目录下 `rdbms` 目录中的 `lib` 子目录。
3. 通过运行以下命令重新链接 `oracle` 二进制文件：

   ```
   make -f ins_rdbms.mk rac_on
   make -f ins_rdbms.mk ioracle
   ```

4. 继续执行 C-5 页的步骤 2。

### C.2.3.3 在已执行单实例安装的 Oracle 主目录中运行集群上的单实例

仅当在单实例 Oracle Database 11g 第 2 版（11.2）安装期间，您在 `OUI`“指定硬件集群安装”页面上选择了本地安装选项时，才能在集群上从已执行单实例安装的 Oracle 主目录中运行单实例。

要将此类型的数据库转换为 Oracle RAC 数据库，请执行以下各节中描述的步骤：

1. C-2 页的“备份原始单实例数据库”。
2. C-3 页的“完成 Oracle Clusterware 安装”。
3. C-3 页的“验证集群”。
4. C-3 页的“安装包含 Oracle RAC 的 Oracle Database 11g 软件”。在此步骤中，请确保选择一个不同于单实例数据库运行所在的新的 Oracle 主目录。

## C.2.4 将 Oracle RAC One Node 转换为 Oracle RAC

您可以通过以 Oracle RAC One Node 数据库所有者身份登录并输入以下 `SRVCTL` 命令，将 Oracle RAC One Node 数据库转换为 Oracle RAC 数据库：

```
$ srvctl convert database -c RAC
```

运行此命令后，除了数据库服务器池外，您还必须为数据库拥有的每个服务创建服务器池。服务服务器池的 `SERVER_NAMES` 值必须设置为您从 Oracle RAC One Node 转换为 Oracle RAC 节点的节点。

将管理员管理的 Oracle RAC One Node 数据库转换为 Oracle RAC 数据库会设置所有数据库服务，使单实例成为首选。转换数据库后，您可以通过运行 `SRVCTL` `add instance` 命令来添加实例。



将策略管理的 Oracle RAC One Node我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。数据库转换为 Oracle RAC 数据库会将所有数据库服务设置为 UNIFORM 基数。这还会导致重用数据库当前运行所在的服务器池。转换会重新配置数据库以在服务器池中的所有节点上运行。该命令不会启动任何其他实例，但运行 SRVCTL `start database` 命令会在服务器池中的所有节点上启动数据库。

> **另请参阅：** *《Oracle Real Application Clusters 管理和部署指南》* 以获取更多信息。

### C.3 使用 rconfig 和 Oracle Enterprise Manager 准备转换

您可以使用 `rconfig` 或 Oracle Enterprise Manager 来协助将单实例数据库安装转换为 Oracle RAC 数据库。前者 `rconfig` 是一个命令行实用程序。Oracle Enterprise Manager Grid Control 数据库管理选项“转换为集群数据库”提供了一个图形界面转换工具。以下各节介绍了如何使用这些转换工具：

- 转换为 Oracle RAC 数据库的先决条件
- 使用 RCONFIG 进行 Oracle RAC 转换期间的配置更改
- 使用 RCONFIG 或 Oracle Enterprise Manager 将数据库转换为 Oracle RAC
- 使用 Oracle Enterprise Manager 将数据库转换为 Oracle RAC

> **注意：** 在开始转换之前，就像在对数据库进行任何重大更改之前一样，请始终备份您的现有数据库。

#### C.3.1 转换为 Oracle RAC 数据库的先决条件

在将单实例数据库转换为 Oracle RAC 数据库之前，请确保为您打算将其作为 Oracle RAC 数据库节点的每个集群节点满足以下条件：

- 已安装、配置并运行 Oracle Clusterware 11g 第 2 版 (11.2)。
- 已安装 Oracle RAC 11g 第 2 版 (11.2) 软件。
- Oracle 二进制文件已启用 Oracle RAC。
- 共享存储（Oracle Cluster File System 或 Oracle ASM）可用且可从所有节点访问。
- `oracle` 帐户存在用户等效性。
- 如果您打算使用 Oracle Enterprise Manager，则所有 Oracle Enterprise Manager 代理都已配置并正在运行，并且配置了集群和主机信息。
- 您已备份现有数据库。

> **注意：** Oracle RAC 数据库必须使用集群 Oracle ASM 实例。

#### C.3.2 使用 RCONFIG 进行 Oracle RAC 转换期间的配置更改

请注意使用 `rconfig` 将单实例数据库转换为 Oracle RAC 时发生的以下更改：

- 在转换过程中，`rconfig` 将目标 Oracle RAC 数据库置于归档日志模式，并为数据库启用归档。如果您不打算使用归档日志空间，则可以在转换完成后禁用归档日志。
- 对于 **共享存储类型** 值，如果您输入 **CFS**，并且您使用集群文件系统作为单实例数据库的存储，则 `rconfig` 会将环境转换为使用 Oracle 托管文件 (OMF) 进行数据库存储，并将数据文件放在共享存储位置下的子目录中。
- 在转换过程中，`rconfig` 将数据库文件移动到指定的共享位置，并使用 OMF 配置它们。

如果您想避免在转换后的数据库中使用 OMF，则单实例数据库文件必须已位于共享文件系统中，并且您必须指明 `rconfig` 不应移动文件。

#### C.3.3 使用 RCONFIG 或 Oracle Enterprise Manager 将数据库转换为 Oracle RAC

以下是将单实例 Oracle 数据库转换为 Oracle RAC 数据库的场景列表：

- 将单实例 Oracle Database 11g 第 2 版 (11.2) 转换为 Oracle 11g 第 2 版 (11.2) Oracle RAC 数据库，从*同一个* Oracle 主目录运行，并使用与单实例数据库相同的数据文件。

在此场景中，从 Oracle RAC 数据库主目录运行 `rconfig` 实用程序，或使用 Oracle Enterprise Manager Grid Control 单实例数据库目标上的 **转换为 RAC** 选项。

- 将早于 Oracle Database 11g 第 2 版 (11.2) 的单实例 Oracle Database 版本转换为 Oracle 11g 第 2 版 (11.2) Oracle RAC 数据库，从同一个 Oracle 主目录运行，并使用与单实例数据库相同的数据文件。

在此场景中，使用 OUI 和数据库升级助手 (DBUA) 将单实例数据库更新到 Oracle Database 11g 第 2 版 (11.2)。然后使用 `rconfig` 或 Oracle Enterprise Manager **转换为 RAC** 选项，如上一场景所述。

- 将单实例 Oracle Database 11g 第 2 版 (11.2) 转换为 Oracle 11g 第 2 版 (11.2) Oracle RAC 数据库，从不同的 Oracle 主目录运行，并使用与单实例数据库相同的数据文件。

在此场景中，在目标数据库主目录中运行 `rconfig` 实用程序，或使用 Oracle Enterprise Manager Grid Control 单实例数据库目标上的 **转换为 RAC** 选项。在出现提示时提供文件存储位置。

- 将单实例 Oracle Database 11g 第 2 版 (11.2) 转换为 11g 第 2 版 (11.2) Oracle RAC 数据库，从不同的 Oracle 主目录运行，并且运行单实例数据库的主机*不是* Oracle RAC 数据库的节点之一。

在此场景中，创建单实例数据库的克隆映像，并将克隆映像移动到集群的一个节点所在的主机。然后使用 `rconfig` 或 Oracle Enterprise Manager **转换为 RAC** 选项，如上一场景所述。

#### C.3.4 使用 Oracle Enterprise Manager 将数据库转换为 Oracle RAC

您可以使用 Oracle Enterprise Manager Grid Control 将单实例数据库转换为 Oracle RAC。要使用此功能，请完成以下步骤：

> **另请参阅：** *《Oracle Database 升级指南》* 以获取有关升级现有 Oracle Database 安装的信息。

1. 登录到 Grid Control。从 Grid Control 主页，单击 **目标** 选项卡。
2. 在“目标”页面上，单击 **数据库** 二级选项卡，然后单击您要转换为 Oracle RAC 的数据库的名称列中的链接。
3. 在“数据库实例主页”上，单击 **更改数据库** 二级选项卡。
4. 在“管理”页面上的“数据库管理 更改数据库”部分中，单击 **转换为集群数据库**。
5. 以具有 `SYSDBA` 权限的数据库用户 `SYS` 登录到您要转换的数据库，然后单击 **下一步**。
6. 在“转换为集群数据库：集群凭据”页面上，提供您要转换的目标数据库的 `oracle` 用户名和密码。如果目标数据库正在使用 Oracle ASM，则还需提供 ASM `SYS` 用户和密码，然后单击 **下一步**。
7. 在“主机”屏幕上，选择您希望成为已安装 Oracle RAC 数据库集群成员的集群中的主机节点。完成选择后，单击 **下一步**。
8. 在“转换为数据库：选项”页面上，选择您是希望使用现有的监听程序和端口号，还是为集群指定新的监听程序和端口号。同时提供集群上集群数据库实例的前缀。

   输入信息完成后，单击 **下一步**，或如果您在决定如何输入信息时需要帮助，请单击 **帮助**。

9. 在“转换为集群数据库：共享存储”页面上，选择使用现有共享存储区域的选项，或者选择将数据库文件复制到新的共享存储位置的选项。同时，决定您是希望使用现有的快速恢复区，还是希望使用 Oracle Database 管理的文件将恢复文件复制到新的快速恢复区。

如果您使用 Oracle ASM，则 Oracle 建议将数据库区和恢复区放置在独立的故障组中。故障组由共享硬件定义，例如两个磁盘共享一个控制器，或两个磁盘位于同一转轴上。如果两个磁盘共享可能故障的硬件，导致两个磁盘均不可用，则这些磁盘被视为位于同一故障组中。如果您不使用 Oracle ASM，则 Oracle 建议将数据文件和快速恢复区放置在不同的位置，如同独立的 Oracle ASM 故障组一样，以便硬件故障不会影响可用性。

当您完成信息输入后，请单击 **“下一步”**，如果您在决定如何输入信息时需要帮助，请单击 **“帮助”**。

10. 在“转换为集群数据库：审查”页面上，审查您选择的选项。如果您想继续转换，请单击 **“提交作业”**。如果您想更改已选择的选项，请单击 **“返回”**。要取消转换，请单击 **“取消”**。
11. 在“确认”页面上，单击 **“查看作业”** 以检查转换的状态。

### C.4 使用 RCONFIG 将数据库转换为 Oracle RAC

您可以使用命令行实用程序 `rconfig` 将单实例数据库转换为 Oracle RAC，或将其转换为 Oracle RAC One Node，具体取决于您在 `ConvertToRAC.xml` 文件中提供的值。要使用此功能，请完成以下步骤：

> **另请参阅：** 有关升级现有 Oracle 数据库安装的信息，请参阅 *《Oracle 数据库升级指南》*

1. 以 `oracle` 用户身份，导航到目录 `$ORACLE_HOME/assistants/rconfig/sampleXMLs`，并使用文本编辑器（如 `vi`）打开文件 `ConvertToRAC.xml`。
2. 查看 `ConvertToRAC.xml` 文件，并根据系统要求修改参数。XML 示例文件包含注释行，提供有关如何配置文件的说明。

> **注意：** 将转换选项 `Convert verify="ONLY"` 设置为执行测试转换，以确保转换可以成功完成。

完成更改后，请使用语法 `filename.xml` 保存文件。记下您选择的文件名。

3. 导航到目录 `$ORACLE_HOME/bin`，并使用以下语法运行命令 `rconfig`：

`rconfig input.xml`

其中 `input.xml` 是您在步骤 2 中配置的 XML 输入文件的名称。

例如，如果您创建名为 `convert.xml` 的输入 XML 文件，则输入以下命令

`$ ./rconfig convert.xml`

**注意：** `ConvertToRAC.xml` 文件中的 `Convert verify` 选项有三个可选值：

- `Convert verify="YES"`：`rconfig` 执行检查以确保在开始转换之前，已满足单实例到 Oracle RAC 转换的先决条件。
- `Convert verify="NO"`：`rconfig` 不执行先决条件检查，并直接开始转换。
- `Convert verify="ONLY"`：`rconfig` 仅执行先决条件检查；完成先决条件检查后不开始转换。

如果转换失败，请使用以下过程进行恢复并重新尝试转换：

1. 尝试使用 DBCA 删除数据库选项删除数据库。
2. 恢复源数据库。
3. 查看转换日志，并修复其报告的任何可能导致转换失败的问题。`rconfig` 日志文件位于 `$ORACLE_BASE/cfgtoollogs` 下的 `rconfig` 目录中。
4. 重新尝试转换。

### C.5 用于 ConvertToRAC 的 Rconfig XML 输入文件示例

以下是 `rconfig` 实用程序的 XML `ConvertToRAC` 输入文件的两个示例。[示例 C-1](Example_C-1) 是一个 XML 输入文件，用于将带有 Oracle ASM 的单实例数据库转换为使用 Oracle ASM 存储上策略托管服务器池的 Oracle RAC 数据库。[示例 C-2](Example_C-2) 是一个 XML 输入文件，用于将带有 Oracle ASM 的单实例数据库转换为使用管理员托管服务器池的 Oracle RAC 数据库。

#### 示例 C–1 用于策略托管数据库的 RConfig ConvertToRAC

```xml
<?xml version="1.0" encoding="UTF-8"?>
<n:RConfig xmlns:n="http://www.oracle.com/rconfig"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.oracle.com/rconfig">
    <n:ConvertToRAC>
    <!-- Verify 在尝试转换前执行预检查，以确保满足所有先决条件。允许的值为：YES|NO|ONLY -->
    <n:Convert verify="YES">
    <!--指定非 RAC 数据库的当前 OracleHome 作为 SourceDBHome -->
            <n:SourceDBHome>/oracle/product/11.2.0/db_1</n:SourceDBHome>
    <!--指定应配置 RAC 数据库的 OracleHome。它可以与 SourceDBHome 相同 -->
            <n:TargetDBHome>/oracle/product/11.2.0/db_1</n:TargetDBHome>
    <!--指定非 RAC 数据库的 SID 和凭据。需要具有 sysdba 角色的用户来执行转换 -->
                    <n:SourceDBInfo SID="sales">
                    <n:Credentials>
                       <n:User>sys</n:User>
                       <n:Password>oracle</n:Password>
                       <n:Role>sysdba</n:Role>
                    </n:Credentials>
                    </n:SourceDBInfo>
    <!--指定策略托管集群数据库将使用的现有或新服务器池列表。 -->
    <n:ServerPoolList>
        <n:ExistingServerPool name="custom"/>
        <n:NewServerPool name="newpool" cardinality="2"/>
    </n:ServerPoolList>
    <!--指定 RacOneNode 及服务名称，以将数据库转换为 RACOne Node -->
    <!--n:RacOneNode servicename="salesrac1service"/-->
    <!--对于策略托管数据库，不需要 InstancePrefix。如果指定了，它将被忽略。实例名称根据 db_unique_name 为策略托管数据库自动生成。-->
    <!-- 从 11.2 开始，不再需要监听器详细信息。数据库会使用运行在 Oracle Grid Infrastructure 主目录中的默认监听器和 SCAN 监听器进行注册。 -->
    <!--指定 RAC 数据库将使用的存储类型。允许的值为 CFS|ASM。非 RAC 数据库应具有相同的存储类型。转换不需要 ASM 凭据。 -->
    <n:SharedStorage type="ASM">
    <!--指定要为 RAC 数据库配置的数据库区位置。如果此字段为空，当前存储将用于 RAC 数据库。对于 CFS，此字段将包含目录路径。 -->
    <n:TargetDatabaseArea>+ASMDG</n:TargetDatabaseArea>
    <!--指定要为 RAC 数据库配置的快速恢复区。如果此字段为空，非 RAC 数据库的当前恢复区将被配置为 RAC 数据库的恢复区。如果当前数据库未使用恢复区，则生成的 RAC 数据库将没有恢复区。 -->
    <n:TargetFlashRecoveryArea>+ASMDG</n:TargetFlashRecoveryArea>
    </n:SharedStorage>
    </n:Convert>
    </n:ConvertToRAC>
</n:RConfig>
```

#### 示例 C-2 用于管理员托管数据库的 Rconfig ConvertToRAC



```xml我是由深度求索（DeepSeek）研发的 deepseek-v4-flash-0731 智能大模型。<?xml version="1.0" encoding="UTF-8"?>
<n:RConfig xmlns:n="http://www.oracle.com/rconfig"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.oracle.com/rconfig rconfig.xsd">
    <n:ConvertToRAC>
    <!-- Verify 在尝试转换前执行预检查，以确保满足所有先决条件。允许的值为：YES|NO|ONLY -->
    <n:Convert verify="YES">
    <!--指定非 RAC 数据库的当前 OracleHome 作为 SourceDBHome -->
    <n:SourceDBHome>/oracle/product/11.2.0/db_1</n:SourceDBHome>
    <!--指定应配置 RAC 数据库的 OracleHome。它可以与 SourceDBHome 相同 -->
    <n:TargetDBHome>/oracle/product/11.2.0/db_1</n:TargetDBHome>
    <!--指定非 RAC 数据库的 SID 和凭据。需要具有 sysdba 角色的用户来执行转换 -->
    <n:SourceDBInfo SID="sales">
        <n:Credentials>
            <n:User>sys</n:User>
            <n:Password>oracle</n:Password>
            <n:Role>sysdba</n:Role>
        </n:Credentials>
    </n:SourceDBInfo>
    <!--指定应运行 RAC 实例的节点列表，用于管理员托管集群数据库。LocalNode 应是此节点列表中的第一个节点。 -->
```

### C.6 转换后的步骤

完成转换后，请注意以下针对 Oracle RAC 环境的建议，详见 Oracle RAC 文档：

- 遵循使用负载均衡和透明应用故障转移的建议，详见 *Oracle Real Application Clusters 管理与部署指南*
- 使用本地管理表空间替代字典管理表空间，以减少争用并管理 Oracle RAC 中的序列，详见 *Oracle Real Application Clusters 管理与部署指南*
- 遵循使用自动段空间管理的指导方针，详见 *Oracle Real Application Clusters 管理与部署指南*

Oracle RAC 中的缓冲区缓存和共享池容量需求略高于单实例 Oracle 数据库的需求。因此，您应将缓冲区缓存大小增加约 10%，共享池大小增加约 15%。

## Oracle Real Application Clusters 环境的目录结构

本附录描述 Oracle Real Application Clusters（Oracle RAC）软件环境的目录结构。本附录包含以下主题：

- [了解 Oracle RAC 目录结构](https://docs.oracle.com/en/)
- [Oracle RAC 的目录结构](https://docs.oracle.com/en/)

### D.1 了解 Oracle RAC 目录结构

当您安装带有 Oracle RAC 的 Oracle Database 11g 第 2 版（11.2）时，除 `oraInventory`、Oracle Automatic Storage Management 主目录（如适用）和 Oracle Clusterware 主目录外，所有子目录都位于顶级 `ORACLE_BASE` 目录下。`ORACLE_HOME` 和 `ADMIN` 目录也位于 `ORACLE_BASE` 下。

> **参见：** *Oracle Real Application Clusters 管理与部署指南*，获取有关 `$ORACLE_HOME` 和 `/ADMIN` 目录的更多信息

### D.2 Oracle RAC 的目录结构

[表 D-1](#Table_D-1) 显示了一个符合 OFA（最优灵活架构）的 Oracle RAC 示例数据库的分层目录树：

表 D-1 符合 OFA 的示例环境的目录结构

| 根目录 | 二级 | 三级 | 四级 | 描述 |
| :--- | :--- | :--- | :--- | :--- |
| `$ORACLE_BASE` | | | | `/u01/app/oracle`<br>默认的 `ORACLE_BASE` 目录，其中软件所有者为 `oracle` 用户。 |
| | `ORACLE_HOME` | | | `/u01/app/oracle/11.2.0/`<br>Oracle 主目录的默认名称。请注意，Oracle 数据库主目录位于 Oracle 基目录路径下。Oracle Clusterware 目录*不得*位于数据库二进制文件所在的 Oracle 基目录路径下。 |
| | | `installation_type` | | Oracle 基目录下的安装类型。如果您打算安装多个软件实例，也可以选择添加计数器。例如，对于 Oracle 数据库安装，当数据库是第二个数据库时，路径如下：<br>`/u01/app/oracle/11.2.0/dbhome_2` |
| | `/ADMIN` | | | 管理目录。请注意，在 Oracle Database 11g 中，`bdump`、`cdump` 和 `udump` 文件已重新定位到 `$ADR_BASE` 目录。 |
| | | `/db_unique_name` | | 数据库唯一名称；当数据库名称为 8 个或更少字符时，与 `dbname` 相同。 |
| | | | `/hdump` `/pfile` | 数据库服务器的转储目标。 |
| `$ADR_BASE` | | | `/bdump` `/cdump` `/udump` | 自动诊断仓库转储目标跟踪文件。请注意，此目录路径由初始化参数 `DIAGNOSTIC_DEST` 设置，并且自动诊断仓库的路径必须位于所有节点均可访问的共享存储位置上。<br><br>默认情况下，此路径是 Oracle 基目录的子集，位于以下路径：<br>`$ORACLE_BASE/diag/` |
| Oracle Grid Infrastructure for a cluster 主目录（Grid 主目录） | | | `/u01/app/grid/11.2.0/` | 符合 OFA 的 Oracle Clusterware 主目录路径。<br><br>在 Oracle Grid Infrastructure for a cluster 安装过程中，会安装 Oracle Clusterware 和 Oracle Automatic Storage Management（Oracle ASM）软件。`root.sh` 脚本会更改 Oracle Clusterware 主目录所有父目录的权限，仅授予 `root` 用户写入权限。因此，Oracle Clusterware 主目录不得是 Oracle 基目录的子目录。 |
| | | `/bin` | | Oracle 二进制文件子目录。 |
| | | `/network` | | Oracle Net 子目录。 |

**参见：** *Oracle Database Linux 和 UNIX 操作系统管理员参考*，获取有关 `$ORACLE_HOME` 和 `/admin` 目录的更多信息

## 如何停止现有 Oracle Real Application Clusters 数据库中的进程

本附录描述如何停止 Oracle Real Application Clusters（Oracle RAC）数据库中的所有进程，以便向现有数据库添加其他产品，或为补丁更新做准备。本附录包含以下主题：

- 备份 Oracle RAC 数据库
- 关闭 Oracle RAC 数据库
- 停止所有 Oracle 进程
- 使用 CVU 验证 Oracle RAC 升级的就绪状态

### E.1 备份 Oracle RAC 数据库

在对 Oracle 软件进行任何更改之前，Oracle 建议您创建 Oracle Database 安装的备份。

### E.2 关闭 Oracle RAC 数据库

在每个节点上以 `NORMAL` 或 `IMMEDIATE` 优先级关闭所有现有的 Oracle Database 实例。您可以使用 Oracle Enterprise Manager 或 `SRVCTL` 来关闭 Oracle RAC 数据库及其实例。

> **注意：** 如果您使用 Oracle Clusterware 或 Cluster Ready Services，则在修改 Oracle 软件之前，必须先关闭所有集群节点上的所有 Oracle Database 实例。如果您正在执行补丁更新，请查阅补丁集说明中的详细说明。

### E.3 停止所有 Oracle 进程

停止在要修改数据库软件的 Oracle 主目录中运行的所有监听器和其他进程。

> **注意：** 在关闭 Oracle ASM 实例、Oracle Clusterware 或 Oracle Restart 之前，必须先关闭使用它们的所有数据库实例。

本节包含以下主题：

- 在添加产品或升级前停止 Oracle 数据库进程
- 停止 Oracle Clusterware 和 Oracle ASM 实例

#### E.3.1 在添加产品或升级前停止 Oracle 数据库进程

本节概述了在向 Oracle 数据库 11g 第 2 版 (11.2) 添加其他产品之前需要完成的工作。如果您正在执行补丁升级，请参阅相应补丁的数据库补丁集说明以获取额外指示。

> **注意：** 您必须按列出的顺序执行这些步骤。

1. 关闭每个节点上 Oracle 主目录中可以访问数据库的任何进程。

   > **注意：** 在关闭任何由 Enterprise Manager Grid Control 监控的进程之前，请在 Grid Control 中为您打算关闭的进程设置一个停机时间段。这是必要的，以便这些进程的可用性记录表明此次关闭是计划内停机，而不是计划外系统中断。

   例如：

   ```
   $ORACLE_HOME/bin/emctl stop dbconsole
   ```

2. 关闭所有节点上的所有 Oracle RAC 实例。要关闭某个数据库的所有 Oracle RAC 实例，请输入以下命令，其中 `db_name` 是数据库名称：

   ```
   $ORACLE_HOME/bin/srvctl stop database -d db_name
   ```

#### E.3.2 停止 Oracle Clusterware 和 Oracle ASM 实例

如果您正在修改 Oracle Clusterware 或 Oracle 集群就绪服务 (CRS) 的安装，请关闭以下 Oracle 数据库服务。

> **注意：** 您必须按列出的顺序执行这些步骤。

1. 关闭每个节点上可能正在访问数据库的 Oracle 主目录中的任何进程；例如，Oracle Enterprise Manager Database Control。

   > **注意：** 在关闭任何由 Oracle Enterprise Manager Grid Control 监控的进程之前，请在 Grid Control 中为您打算关闭的进程设置一个停机时间段。这是必要的，以便这些进程的可用性记录表明此次关闭是计划内停机，而不是计划外系统中断。

2. 关闭所有节点上的所有 Oracle RAC 实例。要关闭某个数据库的所有 Oracle RAC 实例，请输入以下命令，其中 `db_name` 是数据库名称：

   ```
   $ORACLE_HOME/bin/srvctl stop database -d db_name
   ```

3. 停止所有节点上的所有节点应用程序。要停止在某个节点上运行的节点应用程序，请输入以下命令，其中 `$GRID_HOME` 是 Oracle Grid Infrastructure 主目录，`node` 是应用程序正在运行的节点名称：

   ```
   $ $GRID_HOME/bin/srvctl stop nodeapps -n node
   ```

4. 以 `root` 用户身份在所有节点上输入以下命令，以停止 Oracle Clusterware 或 CRS 进程：

   ```
   # crsctl stop cluster
   ```

   要停止集群中所有节点上的 Oracle Clusterware 和 Oracle ASM 实例，您可以输入单个命令：`crsctl stop cluster -all`。

> **注意：** `crsctl stop crs` 命令用于停止用于单实例数据库的 Oracle Restart 服务。

### E.4 使用 CVU 验证 Oracle RAC 升级就绪性

请查看本节内容，以验证您的 Oracle RAC 集群是否已准备好进行升级。

#### E.4.1 关于 CVU 数据库升级验证命令选项

使用命令 `cluvfy stage -pre dbinst -upgrade` 检查您的 Oracle RAC 安装是否已准备好进行升级。使用 `-pre dbinst -upgrade` 标志运行 `cluvfy` 将执行系统检查，以确认集群是否处于从现有 Oracle RAC 安装进行升级的正确状态。

该命令使用以下语法，其中变量内容用斜体表示：

```
cluvfy stage -pre dbinst -upgrade -src_dbhome src_RACHome -dest_dbhome dest_RACHome -dest_version dest_version [-fixup [-fixupdirpath fixupdirpath]] [-verbose]
```

选项如下：

- **-src_dbhome *src_RACHome***

  使用此标志指定您正在升级的源 Oracle RAC 主目录位置，其中 `src_RACHome` 是您想要升级的主目录路径。

- **-dest_dbhome *dest_RACHome***

  使用此标志指定升级后的 Oracle RAC 主目录位置，其中 `dest_RACHome` 是 Oracle RAC 主目录的路径。

- **-dest_version *dest_version***

  使用 `dest_version` 标志指定升级的发行版号，包括任何补丁集。发行版号必须包含表示发行版到平台特定补丁级别的五位数字。例如：`11.2.0.2.0`。

> **另请参阅：** *Oracle 数据库管理员指南*，了解有关发行版号格式的信息

- **`-fixup [-fixupdirpath fixupdirpath]`**

  使用 `-fixup` 标志表示您希望生成有关为确保集群准备好升级而需要完成的任何必要步骤的说明。默认位置是 CVU 工作目录。如果您想将修复说明放置在其他目录中，请添加 `-fixupdirpath` 标志，并提供修复目录的路径。

- **`-verbose`**

  使用 `-verbose` 标志产生各个检查的详细输出。

#### E.4.2 验证 Oracle RAC 基础架构系统升级就绪性的示例

您可以通过运行以下命令来验证节点 `node1` 和 `node2` 上是否已配置安装 Oracle RAC 所需的权限：

```
$ ./cluvfy stage -pre dbinst -upgrade -src_dbhome /u01/app/oracle/product/11.1.0/dbhome_1 -dest_dbhome /u01/app/oracle/product/11.2.0/dbhome_1 -dest_version 11.2.0.3.0 -fixup -fixupdirpath /home/oracle/fixup -verbose
```

#### E.4.3 验证 Oracle 数据库升级的系统就绪性

使用集群验证实用程序 (Cluster Verification Utility) 来帮助您进行系统检查，为开始数据库升级做准备。安装程序会自动运行适当的 CVU 检查，要么提示您解决问题，要么提供一个修复脚本，供您在继续升级之前在集群的所有节点上运行。

> **另请参阅：** *Oracle 数据库升级指南*

## 管理 Oracle 数据库端口号

本附录列出了默认端口号，并描述了如何在安装后更改分配的端口。本附录包含以下主题：

- 关于管理端口
- 查看端口号和访问 URL
- Oracle 组件的端口号和协议
- 更改 Oracle Management Agent 端口
- 更改 Oracle Enterprise Manager Database Console 端口
- 更改 Oracle XML DB 端口

### F.1 关于管理端口

在安装过程中，Oracle Universal Installer (OUI) 从一组默认端口号中为组件分配端口号。许多 Oracle RAC 组件和服务使用端口。作为管理员，了解这些服务使用的端口号并确保服务器上没有两个服务使用相同的端口号非常重要。

大多数端口号在安装期间分配。每个组件和服务都有一个分配的端口范围，这是 Oracle RAC 在分配端口时尝试使用的一组端口号。Oracle RAC 从范围中的最低编号开始，并执行以下检查：

- 该端口是否被主机上的另一个 Oracle 数据库安装使用？
  - 该安装在当时可以是活动的也可以是不活动的；Oracle 数据库仍然可以检测到该端口是否被使用。
- 该端口是否被当前正在运行的进程使用？
  - 这可以是主机上的任何进程，包括 Oracle 数据库进程以外的进程。



如果上述任何问题的答案是肯定的，那么 Oracle RAC 将移动到分配端口范围中的下一个最高端口，并继续检查，直到找到空闲端口。

## F.2 查看端口号和访问 URL

在大多数情况下，Oracle 数据库组件的端口号列在用于配置该端口的工具中。此外，某些 Oracle 数据库应用程序的端口列在`portlist.ini`文件中。此文件位于目录`$ORACLE_HOME/install`中。

如果您在安装后更改了端口号，则不会在`portlist.ini`文件中更新，因此您只能在安装后立即依赖此文件。要查找或更改端口号，请使用本附录中描述的方法。

## F.3 Oracle 组件的端口号和协议

表 F–1 列出了在安装期间配置的组件使用的端口号和协议。默认情况下，如果可用，则范围内的第一个端口被分配给该组件。

**表 F–1 Oracle 组件中使用的端口**

| 组件和描述 | 默认端口号 | 端口范围 | 协议 | 仅在互连上使用 |
| --- | --- | --- | --- | --- |
| 集群管理器<br>端口号在安装期间自动分配。之后无法查看或修改此端口。<br>此端口专门用于集群互连，这是一个在物理上与公共网络分离的专用网络，并使用专用硬件进行互连。 | 动态 | 动态 | UDP | 是 |
| 集群同步服务 (CSSD)<br>节点重启建议消息固定端口。<br>此端口用于所有具有广播功能的接口。广播仅在即将发生节点驱逐重启时发生。 | 42424 | 动态 | UDP | 是 |
| 事件管理器 (EVM)<br>端口号在安装期间自动分配。之后无法查看或修改此端口。<br>此端口专门用于集群互连，这是一个在物理上与公共网络分离的专用网络，并使用专用硬件进行互连。 | 动态 | 动态 | UDP | 是 |
| 网格即插即用 (GPNPD)<br>GPNPD 提供对网格即插即用配置文件的访问，并协调集群节点之间的配置文件更新，以确保所有节点都具有最新的配置文件。 | 动态 | 动态 | TCP | 否 |
| 多播域名服务 (MDNSD)<br>网格即插即用使用 mDNS 进程在集群中定位配置文件，GNS 也使用它来执行名称解析。mDNS 进程在 Linux 和 UNIX 上是后台进程，在 Windows 上是服务。 | 5353 | 动态 | UDP / TCP | 否 |

### 表 F–1（续）Oracle 组件中使用的端口

| 组件及描述 | 默认端口号 | 端口范围 | 协议 | 仅用于互联网络 |
| --- | --- | --- | --- | --- |
| **Oracle Data Guard** — 共享 Oracle Net 端口，并在安装过程中配置。要重新配置此端口，请使用 Net Configuration Assistant 重新配置 Oracle Net 监听器。参见：*Oracle Database Net Services Reference* | 默认 1521，（与监听器值相同） | 可手动修改为任何可用端口 | TCP | 否 |
| **Oracle Connection Manager** — Oracle 客户端连接到 Oracle Connection Manager 的监听端口。安装后可使用 Net Configuration Assistant 配置 Oracle Connection Manager。 | 1630 | 1630 | TCP | 否 |
| **Oracle Clusterware Daemon (CRSD)** — CRS 守护进程（Oracle Cluster Ready Services Daemon）节点间连接。端口号在安装过程中自动分配，之后无法查看或修改。此端口专用于集群互联网络。 | 动态 | 动态 | UDP | 是 |
| **Oracle Cluster Registry** — 端口号在安装过程中自动分配，之后无法查看或修改。此端口专用于集群互联网络。 | 动态 | 动态 | UDP | 是 |
| **Oracle Containers for J2EE (OC4J)** — CRS Agent 在本地使用端口 8888 来管理容器的生命周期。 | 8888，23944（11.2.0.3 及更早版本；在 11.2.0.4 中已移除） | 8888 | TCP | 否 |
| **Oracle Enterprise Manager Database Console** — Oracle Enterprise Manager Database Control 的 HTTP 端口。在安装过程中配置。第 F-5 页的“更改 Oracle Enterprise Manager Database Console 端口”说明了如何修改其端口号。 | 1158 | 5500–5519 | TCP/HTTP | 否 |
| **Oracle Enterprise Manager Database Console** — Oracle Enterprise Manager Database Control 的 RMI 端口。在安装过程中配置。第 F-5 页的“更改 Oracle Enterprise Manager Database Console 端口”说明了如何修改其端口号。 | 5520 | 5520–5539 | TCP | 否 |
| **Oracle Enterprise Manager Database Console** — Oracle Enterprise Manager Database Control 的 JMS 端口。在安装过程中配置。第 F-5 页的“更改 Oracle Enterprise Manager Database Console 端口”说明了如何修改其端口号。 | 5540 | 5540–5559 | TCP | 否 |
| **Oracle Enterprise Manager** — Oracle Enterprise Manager 通过公共互联网络与 QoS 交互的 RMI 端口。 | 23792 | 手动配置 | RMI | 否 |
| **Oracle Grid Interprocess Communication (GIPCD)** — 支持冗余互联网络使用的辅助守护进程。 | 42424 | 动态 | UDP | 是 |
| **Oracle Grid Naming Service (GNSD)** — Oracle Grid Naming Service 守护进程提供集群 mDNS 和外部 DNS 服务器之间的网关。`gnsd` 进程在集群内执行名称解析。 | 53（公共），动态（互联网络） | 53（公共），动态（互联网络） | UDP/TCP（公共），TCP 互联网络 | 否 |
| **Oracle High Availability Services (OHASD)** — Oracle High Availability Services (OHAS) 守护进程启动 Oracle Clusterware 堆栈。此端口专用于集群互联网络。 | 42424 | 动态 | UDP | 是 |
| **Oracle Management Agent** — Oracle Management Agent 的 HTTP 端口，是 Oracle Enterprise Manager 的一部分。在安装过程中配置。第 F-5 页的“更改 Oracle Management Agent 端口”说明了如何修改其端口号。 | 3938 | 1830–1849 | HTTP | 否 |
| **Oracle Notification Services (ONS)** — ONS 的端口，用于发布和订阅服务，以通信所有快速应用程序通知 (FAN) 事件的信息。FAN 通知进程使用当集群服务器不可达或网络接口故障时 Oracle 发布的系统事件。使用`srvctl`修改 ONS 端口。如果未指定 ONS 端口值，则 ONS 守护进程监听本地端口默认为 6100，ONS 守护进程远程端口默认为 6200。 | 6100（本地），6200（远程） | 手动配置 | TCP | 否 |
| **Oracle Real Application Clusters** — 端口号在安装过程中自动分配，之后无法查看或修改。此端口专用于集群互联网络。 | 动态 | 动态 | UDP | 是 |
| **Oracle Net Listener** — 允许 Oracle 客户端通过 Oracle Net 协议连接到数据库。可在安装过程中配置。要重新配置此端口，请使用 Net Configuration Assistant。 | 1521 | 端口号更改为下一个可用端口。可手动修改为任何可用端口。 | TCP | 否 |
| **Oracle XML DB** — 如果基于 Web 的应用程序需要从 HTTP 监听器访问 Oracle 数据库，则使用 Oracle XML DB HTTP 端口。在安装过程中配置，但之后无法查看。“更改 Oracle XML DB 端口”说明了如何更改其端口号。 | 0 | 手动配置 | HTTP | 否 |
| **Oracle XML DB** — 当应用程序需要从 FTP 监听器访问 Oracle 数据库时，使用 Oracle XML DB FTP。在安装过程中配置，但之后无法查看。“更改 Oracle XML DB 端口”说明了如何更改其端口号。 | 0 | 手动配置 | FTP | 否 |

## F.4 更改 Oracle Management Agent 端口

要查找 Oracle Management Agent 端口的当前设置，请在`ORACLE_HOME/host_sid/sysman/config/emd.properties`文件中搜索`EMD_URL`，其中`host_sid`是包含本地主机名和 Oracle RAC 数据库 SID 的字符串。

要更改 Oracle Management Agent HTTP 端口，请使用`emca -reconfig ports`命令：

```
emca -reconfig ports -AGENT_PORT 1831
```

## F.5 更改 Oracle Enterprise Manager Database Console 端口

要查找当前的 HTTP、RMI 和 JMS 端口设置，请在以下文件中搜索，其中`host_sid`是包含本地主机名和 Oracle RAC 数据库 SID 的字符串：

- HTTP 端口：在`ORACLE_HOME/host_sid/sysman/config/emd.properties`文件中搜索`REPOSITORY_URL`。
- RMI 端口：在`ORACLE_HOME/oc4j/j2ee/OC4J_DBConsole_host_sid/config/rmi.xml`文件中的`rmi-server`标签中搜索`port`属性。
- JMS 端口：在`ORACLE_HOME/oc4j/j2ee/OC4J_DBConsole_host_sid/config/jms.xml`文件中的`jms-server`标签中搜索`port`属性。

要更改 Oracle Enterprise Manager Database Control 端口，请使用`emca -reconfig ports`命令：

```
ORACLE_HOME/bin> emca -reconfig ports option setting
```

在上例中，*option* 指定以下一个或多个端口，*setting* 是新的端口值：

| 选项 | 描述 | 示例 |
| --- | --- | --- |
| `DBCONTROL_HTTP_PORT` | 设置 HTTP 端口 | `emca -reconfig ports -DBCONTROL_HTTP_PORT 1820` |
| `RMI_PORT` | 设置 RMI 端口 | `emca -reconfig ports -RMI_PORT 5520` |
| `JMS_PORT` | 设置 JMS 端口 | `emca -reconfig ports -JMS_PORT 5521` |

您可以在一行中指定多个`-reconfig port`设置，例如：

```
emca -reconfig ports -DBCONTROL_HTTP_PORT 1820 -AGENT_PORT 1821 -RMI_PORT 5520
```

## F.6 更改 Oracle XML DB 端口

默认情况下，Oracle XML DB 的 FTP 和 HTTP（包括 HTTPS）端口设置为 0，这会禁用对 Oracle XML DB 的 FTP 或 HTTP 访问。

要更改 Oracle XML DB 端口，必须运行`catxdbdbca.sql`脚本，该脚本在默认安装中位于`$ORACLE_HOME/rdbms/admin`。

更改 Oracle XML DB 端口：

1. 检查 Oracle 监听器是否正在运行。

   如果无法启动监听器，请参阅 *Oracle Database Net Services Administrator's Guide*。

2. 以`SYS`或 XDB 用户身份使用`SYSDBA`权限登录 SQL*Plus。

   例如，要以`SYS`用户身份登录 SQL*Plus：

   ```
   SQL> sqlplus sys/ as sysdba
   ```

3. 运行`catxdbdbca.sql`脚本。

   例如，要使用 2200 作为 FTP 端口，8200 作为 HTTP 端口，并假设您的 Oracle 主目录位于`/u01/app/oracle/product/11.2.0/dbhome_1/`，请输入以下命令：

   ```
   SQL> /u01/app/oracle/product/11.2.0/dbhome_1/rdbms/admin/catxdbdbca.sql 2200 8200
   ```

4. 退出 SQL*Plus。

> **另请参阅：** *Oracle Database Administrator's Guide*，了解有关使用 SQL*Plus 连接到数据库的信息。

# 索引

## A

- 高级安装类型, 2-6
- 架构
  - 最优灵活架构 (OFA), 2-8
- 归档日志
  - 目标位置，转换为集群数据库, C-1
- ASM
  - 与快速恢复区, 3-5
- ASMSNMP, 1-16
- 自动诊断信息库, xxi
  - 诊断数据的默认目录, xxi
- 自动存储管理。*参见* Oracle ASM
- 自动撤消管理, 7-3

## B

- 备份
  - 与转换为集群数据库, C-1
- 块设备, 1-15
  - 仅升级支持, 1-14

## C

- 候选磁盘, 3-6
- 更改主机名, 7-1
- 集群数据库
  - 已安装配置, 7-2
- 集群文件系统
  - 数据文件的存储选项, 1-14
- 集群管理器
  - 端口、范围和协议, F-2
- 集群同步服务 (CSS)
  - 端口、范围和协议, F-2
- 集群验证工具
  - 检查集群管理器的完整性, A-4
  - DBCA 数据库创建阶段就绪性检查, 3-3
  - 验证数据库安装的就绪性, 1-18
- CLUSTER_DATABASE_INSTANCES, 3-6
- 集群件诊断, A-4
- 命令
  - crsctl start crs, 2-3
  - lsnrctl start instance, 2-5
  - ps, 1-20
- 组件
  - 使用 DBCA 时创建, 7-2
- 配置助手
  - 故障排除, A-4
- 连接负载均衡, 7-4
- 连接管理器。*参见* Oracle 连接管理器
- 控制文件
  - 已安装配置, 7-3
- 控制文件, 1-17
  - 说明, 7-3
- 转换为集群数据库
  - 管理注意事项, C-1
  - 从非集群系统, C-2
  - 从单实例, C-4
  - 从单实例转换为 Oracle 真正应用集群, C-1
  - 转换后, C-14
  - 不建议转换的原因, C-2
  - 从单实例 Oracle 数据库转换为 Oracle 真正应用集群, C-1
- 转换
  - 从单实例转换为 Oracle 真正应用集群, C-8
  - 从单实例转换为 Oracle 真正应用集群, C-10
  - 从单实例 Oracle 数据库转换为 Oracle 真正应用集群, B-1
  - 使用 rconfig, C-8
- 创建数据库
  - 使用脚本, B-1
- 创建
  - Oracle 真正应用集群数据库
    - 使用数据库配置助手, 2-8, 3-1, 3-4
- 客户配置信息库。*参见* Oracle 配置管理器

## D

- 数据文件
  - 存储选项, 1-14
- 数据文件, 1-17
  - 与 DBCA, 7-3
  - 说明, 7-2
- 数据库
  - 组件，使用 DBCA 时创建, 7-2
- 数据库代理, 7-5
  - 与监听器, 7-7
  - 与服务器参数文件, 5-2
- 数据库配置助手
  - 创建的组件, 7-2
  - 控制文件, 7-3
  - 创建 Oracle 真正应用集群数据库
    - 安装后, 3-4
    - 安装期间, 2-8, 3-1
  - 数据文件, 7-2
  - 使用其删除数据库, 3-7
  - 删除 Oracle 真正应用集群数据库, 3-7
  - 初始化参数文件, 7-4
  - 初始化参数页面, 3-6
  - 集群数据库列表页面, 3-7
  - 操作页面, 3-7
  - Oracle ASM 磁盘组页面, 3-6
  - 恢复配置页面, 3-6
  - 重做日志文件, 7-3
  - 回退段, 7-3
  - 以静默模式运行, B-9
  - *参见* DBCA
  - 摘要对话框, 3-7
  - 表空间, 7-2
  - 使用, 3-1
  - 欢迎页面, 3-4



# 数据库配置类型

- 选择, 2-6

# 数据库控制

- 安装后配置, 6-2, 6-6
- 安装期间配置, 6-2
- 使用`DBCA`配置, 6-5
- 使用`EMCA`配置, 6-6

# 使用脚本创建数据库, B-1

# 数据库文件

- 支持的存储选项, 1-15

# 夏令时

- 与`TIMESTAMP WITH TIME ZONE`数据, 1-17

# DB_NAME, 3-6

# DB_UNIQUE_NAME, 3-6

- 初始化参数, 3-6

# DBCA

- 使用其配置数据库控制, 6-5
- 删除数据库, 3-7
- 将`SSH`密钥加载到内存以启动, 3-4
- 管理选项页面, 6-5
- 不再设置`local_listener`和`remote_listener`, 7-9
- 在`UNIX`上启动, 6-5
- 在`Windows`上启动, 6-5

# dbca.rsp 文件, B-5

# DBSNMP

- 密码要求, 2-8

# 专用服务器, 7-5

# 使用 DBCA 删除数据库, 3-7

# 已弃用特性

- 服务管理, 2-9

# 诊断, A-4

# 目录结构, D-1

# 磁盘组

- 与首选读取磁盘组, xxii

# DNS

- 在其中注册服务器地址, 1-9

# 从安全数据中心安装前下载安装程序更新, 1-3

# DV_ACCTMGR, 2-4

# DV_OWNER, 2-4

## E

# 简易连接, 7-11

# EMCA

- 命令行参数, 6-7
- 为`Oracle`真正应用集群配置数据库控制, 6-3
- 使用其配置数据库控制, 6-6
- 更改监听器端口后重新配置数据库控制, 6-12
- 指定端口分配, 6-11
- 数据库控制问题故障排除, 6-12
- 故障排除提示, 6-12
- 使用输入文件指定`EMCA`参数, 6-10

# 企业管理器配置助手

- *参见* `EMCA`

# enterprise.rsp 文件, B-5

# 环境变量

- `ORACLE_HOME`, 1-20

# 错误消息

- 安装期间, A-1
- `ORA-00845`, 3-6
- `ORA-01078`, 3-6

# /etc/hosts

- 其中的服务器地址, 1-9

## F

# 故障转移

- 与服务注册, 7-5

# 故障组, 3-5

# 快速镜像重新同步, xxi

# 快速恢复

- 与`Oracle`管理的文件, C-10

# 快速恢复区, 3-5

# 新特性, xiii

# 文件系统

- 数据文件的存储选项, 1-14

# 文件系统

- `Oracle`数据库支持的选项, 1-14

# 文件

- `dbca.rsp`, B-5
- `enterprise.rsp`, B-5
- 响应文件, B-5

## G

# gid

- 选择, 2-9

# 全局数据库名

- 选择, 2-9

## H

# 高可用性

- 互连, 1-3
- 停止服务, E-3

# 高可用性 IP 地址, 1-3

# 主机名

- 更改, 7-1

## I

# 初始化参数文件, 7-4

- 实例的, 5-1
- 监听器参数, 7-6

# 初始化参数

- `CLUSTER_DATABASE_INSTANCES`, 3-6
- `DB_NAME`, 3-6
- `DISPATCHERS`, 7-6
- `LOCAL_LISTENER`, 7-5
- `MEMORY_TARGET`, 3-6
- `REMOTE_LISTENER`, 7-5

# 安装

- 与全球化, 1-5, 2-6
- 目录结构, D-1
- `listener.ora`文件, 7-7
- 非交互式, B-1
- 安装完成后安装其他产品, 3-7
- `Oracle`配置管理器, 2-7
- `Oracle`数据库 Vault, 2-3
- 响应文件, B-5
  - 准备, B-5, B-6
  - 模板, B-5
- 静默模式, B-7
- `tnsnames.ora`文件, 7-9

# 实例

- 初始化参数文件, 5-1

## J

# Java 消息服务 (JMS), 6-12

## L

# 语言

- *参见* 全球化, 1-5

# 语言支持与安装, 2-6

# 集群数据库列表页面, 3-7

# 监听器

- 从 10.1 自动迁移到 10.2, 3-2
- 标识其`Oracle`主目录, 1-20
- `lsnrctl`命令, 1-21
- 注册, 7-8
- 服务注册, 7-8
- 停止, 1-20, 1-21
- 停止现有监听器进程, 1-19

# listener.ora 文件, 7-7

- 配置, 7-6
- 默认配置, 7-7

# 监听器

- `listener.ora`文件, 7-7

# 负载均衡

- 与服务注册, 7-4

# 本地监听器

- 配置, 7-5

# local_listener

- `DBCA`不再在`tnsnames.ora`中设置, 7-9

# 日志文件

- 如何在安装期间查看日志文件, 2-1
- 使用其进行故障排除, A-4

# lsnrctl 命令, 1-21

## M

# 管理选项页面

- `DBCA`中的, 6-5

# 内存大小 (SGA 和 PGA), 3-6

# MEMORY_TARGET, 3-6

# MetaLink。*参见* My Oracle Support

# 迁移

- 从单实例, C-2

# 多个 Oracle 主目录

- 与`Oracle`集群件, 1-5

# 多个 Oracle RAC 数据库

- 对集群件的要求, 1-5

# My Oracle Support, 4-1

- 与存储要求, 1-13
- 安装前检查, 1-2

## N

# 网络配置助手 (NetCA)

- 响应文件, B-8
- 在命令提示符下运行, B-8

# 网络命名方法, 7-11

# 网络服务名, 7-9

# netca.rsp 文件, B-5

# 网络

- 计划接口使用, 1-7
- 服务器地址, 1-9

# 网络附加存储 (NAS), 1-14

# 网络配置文件

- `listener.ora`, 7-7
- `sqlnet.ora`, 7-11
- `tnsnames.ora`, 7-9

# 网络目录, D-2

# 新特性, xiii

# 非交互模式。*参见* 响应文件模式

## O

# olsnodes 命令, A-4

# 操作系统

- `Oracle RAC`的预安装要求, 1-12

# 最优灵活架构 (OFA), 2-8

# Oracle Application Express

- 联机帮助, 2-2
- 与`Oracle Text`, 2-2
- 安装要求, 2-1
- 支持的 Web 浏览器, 1-12

# Oracle ASM

- 与候选磁盘, 3-6
- 与故障组, 3-5
- 更改磁盘发现路径, 3-6
- 磁盘组, xxi
- 快速镜像重新同步, xxi
- 与此版本兼容的`Oracle`数据库版本, 1-20
- `OSASM`组, xxii
- 首选读取磁盘组, xxii
- 响应文件, B-4
- 滚动升级, xxii
- 数据文件的存储选项, 1-14
- `SYSASM`权限, xxii

# Oracle 集群注册表端口, F-3

# Oracle 集群件

- 与多个数据库版本, 1-5
- 端口、范围和协议, F-3

# Oracle 配置管理器

- 启用所需信息, 2-7
- 配置所需提供信息, xxiv
- 安装后, 4-5

# Oracle 连接管理器

- 端口、范围和协议, F-3

# Oracle Data Guard

- 端口、范围和协议, F-3

# Oracle Data Mining, xix

# Oracle 数据库

- 数据文件存储选项, 1-14
- 支持的存储选项, 1-13
- 升级, 1-4, 2-3
- 可使用`Oracle ASM`共存的版本, 1-20

# Oracle 数据库配置助手

- 响应文件, B-5

# Oracle 数据库升级助手, 3-2, C-1

# Oracle 数据库 Vault, xix, xx

- 配置, 2-3
  - `Oracle`数据库 Vault 账户管理员 (`DV_ACCTMGR`), 2-4
  - `Oracle`数据库 Vault 所有者 (`DV_OWNER`), 2-4
- 使用其启动和停止`Oracle RAC`实例, 2-5

# Oracle Enterprise Manager

- `ASMSNMP`, 1-16
- 用于将单实例数据库转换为`Oracle`真正应用集群, C-10

# Oracle Enterprise Manager 代理

- 端口
  - 更改, F-5
  - 范围和协议, F-4

# Oracle Enterprise Manager 数据库控制台

- 端口
  - 更改, F-5
  - 范围和协议, F-3

# Oracle 事件管理器

- 端口、范围和协议, F-2

# Oracle 主目录

- `ASCII`路径, 1-9

# Oracle 主目录

- 标识监听器的, 1-20

# Oracle Net

- 标识监听器的`Oracle`主目录, 1-20
- `lsnrctl`命令, 1-21
- 停止现有监听器, 1-19
- 停止监听器, 1-20
- 停止监听器, 1-21

# Oracle Net 配置助手

- 响应文件, B-5

# Oracle Net 监听器

- 端口
  - 范围和协议, F-5

# Oracle RAC One Node, 2-6

# Oracle RAC 技术认证矩阵, 1-2

# Oracle 真正应用集群

- 数据库，删除, 3-7
- 已安装组件, 1-17
- 操作系统要求, 1-12
- 概述, 3-1, 7-1
- 端口
  - 范围和协议, F-5
- 存储要求, 1-13

# Oracle 真正应用测试, xx

# Oracle SQL Developer, xix, xx

# Oracle Text

- `Oracle Application Express`的要求, 2-2

# Oracle Ultra Search, xx

# Oracle Universal Installer

- 响应文件
  - 列表, B-5

# Oracle 升级伙伴, 1-4, 2-3

# Oracle Warehouse Builder, xix, xx

# Oracle XML DB, xx

- 端口
  - 更改, F-6
  - 范围和协议, F-5

# ORACLE_BASE 环境变量

- 设置, 4-4

# ORACLE_HOME 环境变量

- 设置, 1-20, 4-4

# ORACLE_SID 环境变量

- 设置, 4-4

# Oracle9i

- 检查监听器, 1-20

# OracleMetaLink。*参见* My Oracle Support

# oratab 文件, 7-2

# OSASM

- 与`SYSASM`, xxii

# OWBSYS 信息库, xix

## P

# 参数文件搜索顺序, 5-2

# 参数

- 初始化, 5-1

# 密码短语, 3-4

- `SSH`的, 3-4

# 密码

- `Oracle`数据库 Vault 账户管理员, 2-5
- `Oracle Database Vault`所有者，2-4
- 密码，2-8

# 补丁更新

- 下载，4-1
- 安装，4-1
- `My Oracle Support`，4-1

# 补丁升级，E-2

# 补丁

- `Oracle RAC`的操作系统补丁，1-12

# 策略管理型数据库

- 和`SCAN`，6-2

# portlist.ini 文件，F-1

# 端口

- 访问 URL，F-1
- 集群管理器，范围与协议，F-2
- 集群同步服务，范围与协议，F-2
- 已为应用程序配置，F-1
- 默认范围，F-1
- `Oracle`集群注册表，F-3
- `Oracle Clusterware`，范围与协议，F-3
- `Oracle`连接管理器，范围与协议，F-3
- `Oracle Data Guard`，范围与协议，F-3
- `Oracle Enterprise Management Agent`
  - 更改，F-5
  - 范围与协议，F-4
- `Oracle Enterprise Manager Database Console`
  - 更改，F-5
  - 范围与协议，F-3
- `Oracle`事件管理器，范围与协议，F-2
- `Oracle Net Listener`
  - 范围与协议，F-5
- `Oracle Real Application Clusters`
  - 范围与协议，F-5
- `Oracle XML DB`
  - 更改，F-6
  - 范围与协议，F-5
- 更改监听器端口后重新配置`Database Control`，6-12
- 指定`Database Control`端口，6-11

# 安装后

- 补丁下载与安装，4-1
- 产品配置，4-3
- `root.sh`备份，4-4
- 用户账户设置，4-4

# 预配置数据库安装类型，2-6

# 安装前要求

- 操作系统，1-12

# 专用 IP 地址，1-9

# 进程

- 停止现有，1-19
- 停止现有监听器进程，1-19
- 停止监听器进程，1-20

# ps 命令，1-20

# 公用 IP 地址，1-9

## R

# RAC。*参见* Oracle Real Application Clusters。

# racgimon，7-5

# 原始设备

- 仅支持用于升级，1-14

# RBS 表空间

- 描述，7-3

# rconfig，C-8

# readme.txt 文件，F-1

# 恢复文件

- 支持的存储选项，1-15

# 重做日志文件

- 安装配置，7-3

# 重做日志文件，1-17

- 描述，7-3

# 冗余互连使用，1-3

# 远程监听器

- 配置，7-5

# 远程方法调用 (RMI)，6-12

# remote_listener

- 不再由`DBCA`在`tnsnames.ora`中设置，7-9

# 响应文件安装

- 准备，B-5
- 响应文件
  - 模板，B-5
- 静默模式，B-7

# 响应文件模式

- 关于，B-3
- 使用原因，B-4
- *另请参见* 响应文件、静默模式，B-3

# 响应文件

- 关于，B-3
- 使用模板创建，B-5
- `dbca.rsp`，B-5
- `enterprise.rsp`，B-5
- 用于`Oracle ASM`，B-4
- 通用过程，B-4
- `Net Configuration Assistant`，B-8
- `netca.rsp`，B-5
- 在命令行传递值，B-3
- *另请参见* 静默模式，B-3
- 通过`Oracle Universal Installer`指定，B-7

# 回滚段

- 描述，7-3

# root.sh

- 备份，4-4

## S

# SCAN

- 策略管理型数据库的客户端需要使用`SCAN`，6-2

# 创建 Oracle Real Application Clusters 的脚本

- 数据库，B-1

# 安全配置数据库安装

- 选项，2-7

# 安全数据中心

- 下载安装程序更新，1-3

# 安全 Shell 配置，1-11

# 安全性

- 启用或禁用所需命令行`DBCA`，2-7
- `Oracle Database Vault Account Manager`密码，2-5
- `Oracle Database Vault`所有者密码，2-4
- 安全配置选项，2-7
- 选择密码，2-8

# 服务器参数文件，1-17, 5-1, 7-4

- 错误，5-4

# 服务器池

- 配置，6-1
- 策略管理型需要`SCAN`，6-2
- `XML`转换文件，C-12

# 服务注册

- 关于，7-8
- 配置，7-4

# 共享服务器，7-5

# SID，2-9

# 静默模式

- 关于，B-3
- 使用原因，B-4
- *另请参见* 响应文件，B-3

# 静默模式安装，B-7

# 单实例数据库

- 转换，C-10

# SPFILE

- 默认创建，5-1
- 默认位置，5-2
- 在原始设备上管理，5-2
- 迁移至，5-3

# sqlnet.ora 文件，7-11

# SSH，3-4

# SSH 配置，1-11

# Standard Edition Oracle Database

- 支持的存储选项，1-14

# 存储

- 用于`Oracle RAC`，1-13
- 支持的选项，1-14

# 存储选项



- 快速镜像重同步，xxi
- 企业版安装，1-13
- 标准版安装，1-13
- 摘要对话框，3-7
- 支持的存储选项，1-15
  - 和块设备，1-15
- 支持的技术，1-2
- `SYS`
  - 密码要求，2-8
- `SYSASM`，xxii
  - 和 `OSASM`，xxii
- `SYSASM` 权限
  - 所需存储任务，3-5, 3-6
- `SYSMAN`
  - 密码要求，2-8
- `SYSTEM`
  - 密码要求，2-8
- 系统标识符，2-9
- `SYSTEM` 表空间
  - 描述，7-3

## T

- 表空间
  - 和 `DBCA`，7-2
  - 为大型排序扩展，7-3
  - `RBS`，7-3
  - `SYSTEM`，7-3
  - `TEMP`，7-3
  - 用于自动撤销管理的撤销表空间，7-3
  - `USERS`，7-3
- `TEMP` 表空间
  - 描述，7-3
- 时区版本文件，1-17
- `tnsnames.ora` 文件，7-9
  - 默认配置，7-9
- 故障排除
  - 节点不可用于选择，A-2
  - 使用 `EMCA` 时，6-12
  - 尝试获取磁盘时出错，A-2
  - 无法打开显示，A-2
  - 配置助手错误，A-4
  - 服务器拒绝连接，A-2
  - 磁盘空间错误，1-9
  - 启动实例错误，A-3
  - 连接服务器失败，A-2
  - 日志文件，2-1, A-4
  - 节点不可达，A-2
  - `Oracle Application Express` 的在线帮助，2-2
  - `PRKP-1001`
    - 启动实例错误，A-3
  - 启动或配置 `Database Control` 时的问题，6-12
  - `PROT-8`
    - 无法从指定文件向集群注册表导入数据，A-3
  - 查看日志文件，A-4
  - 时间戳在未来，A-3
  - 使用 `EMCA`，6-12
  - `X` 服务器，A-2
  - `YPBINDPROC_DOMAIN`
    - 域未绑定，A-3
- 典型安装类型，2-6

## U

- 撤销管理，7-3
- 升级，1-4, 2-3
  - 和使用相同的 `Oracle` 主目录，1-9
  - 和使用相同的 `Oracle` 主目录类型，2-13
  - 现有 `Oracle` 数据库，3-2
  - 监听器，3-2
  - 带补丁的 `Oracle` 数据库，E-2
  - `Oracle Clusterware` 版本要求，1-4
  - `TIMESTAMP WITH TIME ZONE` 数据，1-17
- 升级
  - 和 `SCAN`，7-5
  - 停止进程，1-19
- 用户账户
  - 安装后设置，4-4
- `USERS` 表空间
  - 描述，7-3

## V

- `VIP`，1-10
  - `VIP` 地址，1-9
  - 虚拟 IP 地址，1-9
- 虚拟 IP。*参见* `VIP`

## W

- Web 浏览器
  - `Oracle Application Express` 支持，1-12
  - `Oracle Enterprise Manager` 支持，1-12
