
图 14.15：使用 `ReAR` 恢复系统的示例。

## 结论

良好的备份定义了策略、执行的恢复测试以及使用的存储介质，并指定恢复时间目标 (RTO) 和恢复点目标 (RPO)。通常在企业中备份被低估，只有在灾难发生时才会成为首要任务。随着云和新技术（如容器）的采用，备份仍然相关，但方法有所不同。新系统可以通过自动化从头创建，应用程序以镜像形式存储。因此只需要存储所需的数据。

有不同的商业备份解决方案，例如 `EMC Networker`、`HP Data Protector` 或 `Symantec NetBackup`。此外，还有成熟的提供了可使用的开源解决方案。本章涵盖了 `Bacula` 作为主要的开源解决方案，以及 `Relax-and-Recover` (`ReAR`) 作为一种完美的裸机灾难恢复解决方案。

## 关键事实

-   需要良好的备份规划以避免灾难性情况。
-   需要频繁进行恢复测试以确保副本的完整性和恢复协议的有效性。
-   现代系统需要重新思考什么应该存储在备份中。
-   对于关键环境，灾难恢复计划是有用的且必须的。
-   `Bacula` 是一个成熟且适用于企业级的开源备份解决方案。
-   在裸机环境中，`Relax-and-Recover` (`ReAR`) 解决方案是一个完美的选择。

## 问题

- 1. 差分备份所需的空间比增量备份少。
    a. 正确
    b. 错误
2. 3-2-1 原则包含三个副本、两种不同的存储介质和一份异地备份。
    a. 正确
    b. 错误
3. 备份解决方案中避免数据重复的功能名称是什么？
    a. 减少复用 (reduplication)
    b. 去重 (deduplication)
    c. 多路复 (multiplexing)

- 4. `Bacula` 中用于获取信息和运行作业的主要命令是什么？
    a. `bacula`
    b. `bacula-cli`
    c. `bconsole`

- 5. 命令 `rear` 的哪个参数用于执行备份？
    a. `backup`
    b. `mkbackup`
    c. `run`

## 答案

- 1. b
2. a
3. b
4. c
5. b

# 第 15 章

# 多云管理

## 引言

正如本书中所描述的样，许多公司通过转向虚拟化（不仅是计算，还有网络和存储）以及容器化环境实现了其 IT 基础设施的现代化。另一个大转型是从本地基础设施向公云的迁移。这种迁移带来了许多优势，但也存在一些需要考虑的因素。

在多个云环境（如 `Amazon Web Services`、`Microsoft Azure`、`Google Cloud` 或 `阿里云`）中工作为环境的自动化和管理带来了新的挑战。将私有云（如 `OpenStack`）与公共提供商结合被称为混合云。

本章将重点介绍不同的云服务提供商、它们提供的不同服务以及它们之间的比较。它将描述使用公云的优点和缺点。它还将描述管理多云的不同策略以及如何使用自动化工具 `Terraform` 实现。

## 结构

在本章中，我们将讨论以下主题：

- 云服务提供商简介
- 云服务
- 多云管理
- 代码即基础设施
- `Terraform`

# 云服务提供商简介

云服务提供商负责提供供使用的各种服务。在过去的十年里，云服务提供商已经从简单提供计算和服务存储服务演变为提供数百种服务。云服务提供商负责所有基础设施，包括存储、网络、计算和安全。
目前提供的分类服务包括以下（由 `Amazon Web Services` 提供的分类）：

- 基础设施软件：此类服务别的服务提供与基础设施相关的解决方案。
    - 备份与恢复：用于存储和备份的服务。
    - 数据分析：用于数据分析的服务。
    - 高性能计算：高性能计算服务。
    - 迁移：用于迁移项目的服务。
    - 网络基础设施：用于创建网络解决方案的服务。
    - 操作系统：`Linux` 和 `Windows` 操作系统的镜像。
    - 安全：用于基础设施的安全服务。
    - 存储：与存储相关的服务。
- `DevOps`：此类服务提供关注开发者和开发者团队的工具。
    - 敏捷生命周期管理：用于敏捷开发的服务。
    - 应用开发：用于应用程序开发的服务。
    - 应用服务器：用于应用程序开发的服务器。
    - 应用堆栈：用于应用程序开发的堆栈。
    - 持续集成与持续交付：用于 `CI/CD` 的服务。
    - 代码即基础设施：用于基础设施的服务。
- 问题与 Bug 跟踪：开发团队用于跟踪和管理软件 Bug的服务。
- 监控：用于监控操作软件的服务。
- 日志分析：用于日志记录和日志分析的服务。
- 源码控制：用于管理和维护源码控制工具。
- 测试：用于软件自动化测试的服务。
- 业务应用：此类服务帮助运行业务。
- 区块链：用于区块链的服务。
- 协作与生产力：用于实现协作的服务。
- 联系中心：用于在组织内启用联系中心的服务。
- 内容管理：侧重于内容管理。
- `CRM`：侧重于客户关系管理的工具。
- 电子商务：提供电子商务解决方案的服务。
- 在线学习：提供在线学习解决方案的服务。
- 人力资源：用于启用组织内人力资源的服务。
- IT 业务管理：用于启用组织内业务管理的服务。
- 商业智能：用于启用组织内商业智能的服务。
- 项目管理：用于项目管理的工具。
- 机器学习：此类服务提供机器学习算法和模型包。
- 物联网 (`IoT`)：用于创建物联网相关解决方案的服务。
- 桌面端应用：此类服务提供与基础设施相关的解决方案。
- 数据产品：此类服务是一组基于文件的数据。

目前市场上最受欢迎的云服务提供商是：

- `Amazon Web Services` (`AWS`)：服务的先驱，主导着市场。
- `Microsoft Azure`：市场上第二大云平台，与 `Microsoft` 产品有良好的集成。
- `Google Cloud Platform` (`GCP`)：第三大平台。
- 阿里云 (`Alibaba Cloud`)：这是第四大中国集团。

在私有云，最流行的开源解决方案是 `OpenStack`。`OpenStack` 是一个成熟的解决方案，拥有 `Red Hat`、`Mirantis` 和 `Canonical` 等支持。选择云提供商需要考虑几个因素：

- 成本节省：尽管使用公云的主要原因之一是降低成本，但错误的规划和工作流的实施会导致运行服务的成本增加，从而进一步增加公云的成本。
- 可用性：大多数云提供商提供不同的区域和可用区。
- 服务：在云竞争中，大多数提供相似的服务。但特定的服务可以产生差异。
- 易用性：某些云提供商比其他更容易使用，包括文档支持。
- 迁移：根据本地提供的服务，云提供商是合适的。

## 优点

与本地运行服务相比，使用云提供商具有许多优势。迁移到云的主要原因是：

- 服务协议 (`SLA`)：大多数云提供商保证服务可用率为 99.99%。
- 服务目录：在云提供商中，可以运行虚拟机、容器，他们还有负载均衡器或备份解决方案等数百种选项，整合在同一个门户中。云还可以立即启用更多服务。
- 基础设施：用户不再需要维护基础设施，包括物理组件（服务器、路由器、电缆等）和虚拟组件（路由、网络、存储等）。
- 灵活性：可以根据需求动态更改分配的资源。
- 可扩展性：可以手动或按需增加计算能力、存储或更多服务。
- 可访问性：云提供商通过互联网提供各种服务，这使他们能够直接向终端用户提供服务。
- 安全性：云提供商提供的解决方案是安全的，并且提供了增加安全性的方案，例如存储加密、私有网络和防火墙。

对于任何解决方案，使用云提供商（尤其是公云）存在一些问题。这些包括：

- 成本：尽管使用公云的主要原因之一是降低成本，但错误的规划和工作流的实施会导致运行服务的成本增加，从而进一步增加公云的成本。在迁移过程中，定义需求、规划可能的成本并监控服务的使用是非常重要的。
- 供应商锁定：迁移到公云意味着适应并使用提供商提供的服务。这可能会减少未来可能需要转向更适合公司的其他解决方案。
- 控制力较弱：虽然由提供商管理基础设施是一个优势，但如果你无法控制所提供服务涉及的不同元素，这可能是一个劣势。
- 支持：云提供商提供的支持可能无法满足某些公司的需求，特别是在服务的新实现方面，因为它所需的时间比预期的要长。

## 云服务

让我们讨论一些云服务。

## `Amazon Web Services` (`AWS`)

`AWS` 于 2006 年开始提供其首次服务。在编写本书时，全球基础设施包含 29 个区域，每个区域有多个可用区（`AZ`），总共 93 个可用区。最新估计显示，`AWS` 在云服务市场中的份额为 34%。`Amazon Web Services` 提供的一些主要服务如下：

- **`Amazon Elastic Compute Cloud` (`EC2`)**：运行虚拟机的服务，以及在云端运行裸机（`Bare Metal`）节点的能力。
    - `EC2` 提供了市场上的大多数 `Linux` 发行版选项，包括 `Red Enterprise Linux`、`Ubuntu` 或 `Debian`。
    - `Amazon Machine Image` (`AMI`) 包含了用于运行 `EC2` 实例的操作系统。
    - 运行 `EC2` 实例需要指定安全组（`Security Group`），它是防火墙规则的定义。
    - 可以根据虚拟机的需要指定不同的存储选项。
    - **密钥对 (`Key Pair`)** 定义了一个用于远程访问实例的 `SSH` 公钥。
- **`Amazon Virtual Private Cloud` (`VPC`)**：允许运行虚拟网络并在运行实例。这创建了一个私有且隔离的网络。像普通网络一样，它包含了子网、路由和 `IP` 地址等元素。
    - `Elastic IP` 地址是用于从互联网访问 `EC2` 实例的公共地址。此 `IP` 可以从运行中的实例上绑定和解绑。
- **`Amazon Simple Storage Service` (`S3`)**：一种对象存储服务，提供扩展性、数据可用性、安全性和性能。
- **`Amazon Elastic Beanstalk`**：用于部署和扩展 Web 应用程序的服务。
- **`Amazon Relation Database Service` (`RDS`)**：在云端中设置、运行和扩展数据库的服务。可用的选项如下：
    - 兼容 `MySQL` 的 `Amazon Aurora`。
    - 兼容 `PostgreSQL` 的 `Amazon Aurora`。
    - `MySQL`、`MariaDB`、`PostgreSQL`、`Oracle` 和 `SQL Server`。
- **`Amazon DynamoDB`**：快速、灵活的 `NoSQL` 数据库服务，适用于任何规模的性能。
- **`Amazon Elastic Container Service` (`ECS`)**：全托管的容器编排服务，可以轻松地部署、管理和扩展容器化应用程序。
- **`Amazon Elastic Kubernetes Service` (`EKS`)**：在 `AWS` 云端和本地数据中心运行 `Kubernetes` 的服务。
- **`Amazon Elastic Load Balancing` (`ELB`)**：将入站流量分发到多个目标的服务。
- **`Amazon CloudFront`**：为高性能和安全性构建的内容交付网络（`CDN`）服务。
- **`Amazon Route 53`**：高可用且可扩展的域名系统（`DNS`）网络服务。
- **`Amazon Lambda`**：无服务器、事件驱动的计算服务，允许代码在几乎任何类型的应用程序或后端服务中运行，无需配置或管理服务器。
- **`AWS Identity and Access Management` (`IAM`)**：安全地管理身份以及 `AWS` 服务和资源的访问。

## `Microsoft Azure`

`Microsoft Azure` 起于 2008 年，并于 2010 年正式发布。该名称于 2014 年被采用，尽管之前名为 `Windows Azure`。在编写本书时，有 60 个可用区域。最新估计认为 `Microsoft Azure` 拥有 21% 的市场份额。提供的主要服务如下：

- **`Azure Virtual Machines`**：运行虚拟机的服务。它可以运行 `Linux` 发行版或 `Windows Server`。
    - `Azure Marketplace` 包含用于运行的经过认证的操作系统和应用程序。
    - 通过创建虚拟机，可以在许多选项中指定
        - 尺寸（`CPU` 和内存）
        - 存储类型和大小
        - 身份验证（例如 `SSH` 公钥）
        - 配置防火墙规则
        - 要连接的虚拟网络（`Vnet`）
- **`Azure Virtual Network` (`VNet`)**：管理私有网络的服务。虽然与数据中心的传统网络类似，但它带来了 `Azure` 基础设施的额外优势，如扩展、可用性和隔离性。
    - `Azure` 使用 `Public IP` 指外部地址，这些地址可以连接到虚拟机。
- **`Azure Blob Storage`**：用于云的对象存储解决方案。它针对存储大量的非结构化数据进行了优化。非结构化数据是不符合特定数据模型或定义的数据，例如文本或二进制数据。
- **`Azure Web Apps`**：一种用于托管 Web 应用程序、`REST API` 和移动后端的 `HTTP` 服务。
- **`Azure Cloud Services`**：使用 `Azure Service Manager` 创建高可用、无限扩展的云应用程序和 `API`。
- **`Azure Resource Manager`** 是 `Azure` 的部署和管理服务。它提供了一个管理层，允许您在 `Azure` 账户中创建、更新和删除资源。
- **`Azure SQL`**：在现代 `SQL` 系列云数据库上进行迁移、现代化和创新。
- **`SQL Server Stretch Database`**：动态地将 `Microsoft SQL Server 2016` 的热数据和冷事务数据扩展到。
- **`Azure Database for MySQL`**：基于 `MySQL` 的关系数据库服务。
- **`Azure Database for PostgreSQL`**：基于 `PostgreSQL` 的关系数据库服务。
- **`Azure SQL Database`**：面向 `IoT` 的全托管关系型数据库。
- **`Azure Cosmos DB`**：具有 `SLA` 保证的速度和可用性的快速 `NoSQL` 数据库。
- **`Azure Kubernetes Service` (`AKS`)**：提供了开始开发 `Kubernetes` 的快方式。
- **`Azure Container Instances`**：按需运行 `Docker` 容器。
- **`Azure Load Balancer`**：负载均衡互联网和私有网络流量。
- **`Azure Content Delivery Network` (`CDN`)**：提供快速交付内容的全球解决方案。
- **`Azure DNS`**：提供名称解析的域名托管服务。
- **`Azure Functions`**：提供无服务器计算。
- **`Azure Active Directory` (`AD`)**：企业级身份服务，提供单登录和多因素身份验证。

## `Google Cloud Platform`

`Google Cloud Platform` 于 2009 年开始以预览形式提供某些服务。它于 2011 年正式正式可用（`GA`）。在编写本书时，它有 35 个区域和 106 个可用区。最新估计 `Google Cloud Platform` 拥有 11% 的市场份额。提供的主要服务如下：

- **`Compute Engine`**：安全且可定制的计算服务，可在 `Google` 上创建并运行虚拟机。
    - `Compute Engine` 提供了许多预配置的公共镜像。
    - 通过创建实例，可以指定其他项：
        - 分配的资源（`CPU` 和内存）
        - 存储类型和大小
        - 配置防火墙规则
        - 身份验证（例如 `SSH` 公钥）
        - 要连接的网络（`VPC`）
- **`Virtual Public Cloud` (`VPC`)**：跨所有区域的全局虚拟网络。整个组织使用单个 `VPC`，在项目内部隔离。
- **`Cloud Storage`**：用于存储非结构化数据的托管服务。存储任何量的数据并在需要时检索。
- **`Cloud App Engine`**：构建单体服务器端渲染的网站。`App Engine` 支持流行的开发语言以及一系列开发工具。
- **`Cloud SQL`**：针对 `MySQL`、`PostgreSQL` 和 `SQL Server` 的全托管关系数据库服务。
- **`Cloud Spanner`**：具有无限扩展性、强一致性和高可用性的全托管关系型数据库。
- **`Datastore`**：适用于您的 Web 和移动应用程序的高扩展性 `NoSQL` 数据库。
- **`Kubernetes Engine` (`GKE`)**: 一种自动部署、扩展和管理 `Kubernetes` 的简单方法。
- **`Cloud Load Balancing`** (`云负载均衡`): `Google Cloud` 上高性能、可扩展的负载均衡。
- **`Cloud CDN`**: 具有规模和触达能力的快速、可靠的 Web 和视频内容交付。
- **`Cloud DNS`**: 可靠、有弹性且低延迟的 `DNS`，为 `Google` 全球网络提供服务，涵盖注册、管理和提供域名所需的一切。
- **`Cloud Functions`** (`云函数`): 通过我们的可扩展、按需付费函数服务 (`FaaS`) 产品，在云端运行代码，无需管理服务器或容器。
- **`Identity and Access Management`** (`IAM`, `身份和访问管理`）：允许管理员授权谁可以对特定资源执行操作。

## 阿里云

阿里云从 2009 年开始提供不同的服务。在编写此书时，它已有 24 个区域和 74 个可用区。最新的估计显示阿里云占有 5% 的市场份额。提供的主要服务如下：

- `Elastic Compute Service` (`弹性计算服务`): 在云端运行虚拟机的服务。
- `Alibaba Cloud Marketplace` (`阿里云市场`)：包含多个准备好在云上运行的操作系统、发行版和应用程序。
- `Virtual Private Cloud` (`专有云`): 一种虚拟私有云服务，提供隔离的云网络以便在安全环境中运行资源。
- `Object Storage Service` (`OSS`, `对象存储服务`): 全托管对象存储服务，可从任何地方存储和访问任意数据。
- `Enterprise Distributed Application Service` (`企业分布式应用服务`): 用于多种应用部署选项和微服务解决方案的 `PaaS` 平台。
- `ApsaraDB RDS`: 构建在 `Apsara` 分布式文件系统上的稳定、可靠且可扩展的在线关系型数据库服务。
- `ApsaraDB RDS for MySQL`: 全托管在线服务，支持 `MySQL 5.5`、`5.6`、`5.7` 和 `8.0`。
- `ApsaraDB RDS for PostgreSQL`: 针对 `PostgreSQL` 的按需数据库托管服务，具有自动监控、备份和灾备能力。
- `ApsaraDB RDS for SQL Server`: 针对 `SQL Server` 的按需数据库托管服务，具有自动监控、备份和灾备能力。
- `PolarDB-X`: 为解决超高并发、海量数据存储和大表性能瓶颈等数据库挑战而设计。
- `ApsaraDB for MongoDB`: 安全、可靠且弹性扩展的云数据库服务，支持自动监控、备份和时间点恢复。
- `Elastic Container Instance` (`弹性容器实例`): 一种灵活且安全的无服务器容器实例服务。
- `Alibaba Cloud Container Service for Kubernetes` (`ACK`, `阿里云 Kubernetes 服务`): 一种基于 `Kubernetes`的服务，通过在云端运行容器化应用来确保企业的高效率。
- `Server Load Balancer` (`SLB`, `负载均衡`): 将网络流量分发到后端服务器组，以提高服务能力和应用可用性。
- `Alibaba Cloud CDN`: 快速、稳定、安全的自定义交付服务，面向全球用户加速内容分发。
- `Alibaba Cloud DNS`: 快速、稳定可靠的权威 `DNS` 服务。
- `Function Compute` (`函数计算`): 安全稳定的无服务器计算平台。
- `Resource Access Management` (`RAM`, `访问访问管理`）：允许您集中管理对阿里云及资源的访问。

网站 `https://comparecloud.in/` 包含了服务列表以及每个热门公共云提供商的对应服务（包括 `IBM Cloud`、`Oracle Cloud` 和 `华为云`）。图 15.1 显示了之前描述的一些服务的对比表格：

| `Amazon EC2` | `Azure Virtual Machine` | `Compute Engine` | `Alibaba Cloud` |
|---|---|---|---|
| `Amazon Elastic Container Service` (`ECS`) | `Azure Kubernetes Service` (`AKS`) | `Container Service` | `Alibaba ECS` |
| `Amazon Kubernetes Service` (`EKS`) | `Azure Container Instances` | `Kubernetes Engine` | `Container Service for Kubernetes` |
| `Amazon Redshift on AWS` | `Azure Red OpenShift` | | |
| `AWS Lambda` | `Azure Service Fabric` | `Google Cloud Functions` | `Function Compute` |
| | `Azure Functions` | `EventArc` | |
| | `Event Grid` | | |
| `AWS Elastic Beanstalk` | `Azure Web Apps` | `Google App engine` | `Enterprise Distributed Application Service` |
| | `Azure Cloud Services` | | |
| `Amazon Simple Storage Service` (`S3`) | `Azure Blob Storage` | `Cloud Storage` | `Object Service` |
| `Amazon S3 Glacier` | `Azure Archive Storage` | | `Object Archive` |
| | `Azure Cloud Storage` | | |
| `Amazon Aurora` | `SQL Database` | `Cloud SQL` | `AuroraDB for MySQL` |
| `Amazon RDS` | `SQL Database for MySQL` | | `AuroraDB for SQL Server` |
| | `SQL Database for PostgreSQL` | `Cloud Spanner` | `AuroraDB for PostgreSQL` |
| | `SQL Database Enterprise` | | `Distributed Relational Database Service` (`RDS`) |
| `Amazon DynamoDB` | `Azure Cosmos DB` | `Cloud Datastore` | `ApsaraDB MongoDB` |
| `Amazon DynamoDB Accelerator` (`DAX`) | `Stable Storage` | `Table Store` | |
| | `Azure Time Series Insights` | | |
| `Amazon VPC` | `Azure VNet` | `Virtual Private Cloud` | `Virtual Private Cloud` |
| `Amazon CloudFront` | `Azure CDN` | `Cloud CDN` | `Alibaba Content Delivery Network` |
| | `Azure Front Door` | | |
| `Amazon Route 53` | `Azure DNS` | `Cloud DNS` | `Alibaba Cloud` |
| `Elastic Load Balancing` | `Azure Load Balancer` | `Cloud Load Balancing` | `Server Load Balancer` |
| `AWS Identity and Access Management` | `Azure Active Directory` | `Cloud IAM` | `Resource Access Management` |
| | | `Cloud Identity-Aware Proxy` | |

图 15.1：云服务对比

## `OpenStack`

云解决方案 `OpenStack` 是一个开源平台，通常部署用于在本地环境中构建私有云。这一成熟的解决方案始于 2010 年，被数千家公司使用。`OpenStack` 提供的服务描述如下：

- `Nova`: 提供了一种配置计算实例（而非虚拟）的方法。
- `Neutron`: 处理网络基础设施的创建和管理，包括交换机、子网。
- `Keystone`: 提供 `API` 认证和多租户授权。
- `Horizon`: 提供 `OpenStack` 服务的 Web 用户界面。
- `Cinder`: 为虚拟机提供卷块存储服务。
- `Glance`: 镜像服务，用户可以在此上传并发现供 使用 使用镜像。
- `Swift`: 高可用、分布式且最终一致的对象存储。
- `Ironic`: 配置裸机服务器的服务。
- `Heat`: 使用声明式模板编排应用的服务。

参考图 15.2 查看 `OpenStack` 组件：

- `Octavia`: 为 `OpenStack` 带来网络负载均衡。
- `Barbican` (`密钥管理服务`): 提供秘密数据的存储、配置和管理。
- `Manila`: 提供共享文件系统的服务。
- `Designate`: 一种开源的 `DNS` 服务实现。

有不同的公司为 `OpenStack` 提供商业支持。示例包括：

- `Red Hat OpenStack Platform`: 与 `Red Hat Enterprise Linux` 共同工程，确保稳定且适用于生产环境的云。
- `Canonical` 的 `Charmed OpenStack`: 针对价格性能优化的企业云平台，为运行关键任务工作负载设计。与 `Ubuntu` 结合，符合行业最高的安全、稳定性和质量标准。
- `Mirantis OpenStack for Kubernetes`: 提供高性能且可扩展的 `IaaS`，让您能够利用 `Kubernetes` 的能力部署、运行和扩展裸机云，提供极其可靠且高度可扩展的私有云。
- `VMware Integrated OpenStack` (`VIO`): `VMware` 支持的 `OpenStack` 发行。通过 `VIO`，客户可以在 `VMware` 技术之上快速部署生产级的 `OpenStack` 云，利用其现有的 `VMware` 投资和专业知识。

## 多云管理

使用单一云供应商最大的缺点之一是被锁定在一个供应商的服务和成本中。多云管理的概念是一套工具和程序，允许我们使用多个云供应商，并根据需求（如成本或可用性）部署服务。要分的服务可以是简单的，如运行在虚拟机中的应用程序，也可以是复杂的，如 `Kubernetes` 集群。

现如今，越来越多的公司开始使用多个云供应商，原因如下：

- 降低成本：在云上运行服务的价格在不同之间可能差异巨大。如果公司决定选择作为其主服务的提供商，它可以降低使用不同提供商的其他某些服务的成本。
- 可用服务：大多数提供商都提供相同的服务，但特定的服务可能成为选择不同于主服务的另一个提供商的原因。
- 可用性：大多数提供商在许多区域都可用，为某个国家或地区的用户提供服务的特定区域可能成为在不同提供商中部署服务的原因。

`多云管理` (`Multi Cloud Management`) 工具可以分为三类不同的类别：

- `基础设施自动化工具`：这些工具可用于在多个`云提供商` (`Cloud Providers`) 中部署服务或应用程序。示例如下：
    - `Terraform`：在本章后面将描述，`Terraform` 用于在多个提供商中连接和部署服务。
    - `Ansible`：允许以简单的方式在不同的提供商中执行不同的操作。
- `管理工具`：该类别的工具负责仅从一个应用程序或门户管理多个云。某些示例如下：
    - `Embotics`：一种帮助现代基础设施和运营团队减少混合和多云管理挑战的解决方案。
    - `Kyryl` `多云管理平台`：通过全面的功能和集成，简化多云 IT 架构的管理。
    - `Red Hat` `高级集群管理` (`Red Hat Advanced Cluster Management`)：帮助从一个仪表板管理不同云中的不同 `Kubernetes` 安装。
- `云提供商解决方案`：某些提供商提供与其他提供商互操作的服务。
    - `Google Anthos`：为混合和多云环境提供一致的开发和运营体验。
    - `Azure Arc`：一个扩展 `Azure` 平台的桥梁，帮助您构建应用程序和服务，并灵活地跨数据中心、边缘和多云环境运行。

## 基础设施即代码 (`Infrastructure as code`)

随着云的采用，在以快速灵活的方式部署新基础设施方面出现了新需求。部署方法主要有两种：

- `声明式` (`Declarative`)：这种方法描述要做什么，没有特定的控制流，以获得预期的基础设施。在特定的基础设施部署工具出现之前，这种方法是最常用的。它包括使用针对平台的特定工具进行管理，例如：
    - `AWS 命令行界面` (`AWS`)： 用于从命令行与 `AWS` 服务交互的工具。通过使用 `aws` 命令，可以创建不同的服务，例如 `VPC`、`EC2` 实例或负载均衡器等。
    - `Google Cloud CLI` (`gcloud`)：一组用于在 `Google Cloud` 平台上创建和管理资源的工具。
    - `Azure 命令行界面` (`CLI`)：一组用于创建和管理 `Azure` 资源的命令。
    - `阿里云 CLI`：包括 `aliyun` 命令，用于与您的阿里云资源进行交互和管理。
    - `Openstack CLI`：`OpenStackClient` 项目提供了一个统一的命令行界面，允许通过易用的命令 `openstack` 访问项目 `API`。
- `命令式` (`Imperative`)：在这种方法中，它描述了基础设施应该什么样。所使用的工具将读取所需的定义，并确保最终状态是正确的。与声明式方法相比，这种方法有几个几个优势，如下：
    - `幂等性` (`Idempotent`)：该过程可以执行多次；如果仅当资源状态与定义不符时，则会对其进行修改。
    - `灵活性` (`Flexibility`)：可以根据新需求更新定义，目标环境也将随之更新。
    - `删除` (`Removal`)：删除定义的基础设施是一个直接的操作，由该工具负责正确移除。

大多数流行的自动化工具都提供了使用命令式方法操作云提供商的可能性。`Ansible` 可以使用模块查找合适的 `AMI` 镜像、定义 `SSH` 密钥并创建 `EC2` 实例。`Ansible` 将使用与 `AWS API` 通信的特定库，`boto3`。以下示例显示了一个在 `AWS` 上创建不同资源的 Playbook：

```yaml
