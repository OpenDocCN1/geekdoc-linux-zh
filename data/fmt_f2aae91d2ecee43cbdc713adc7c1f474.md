
- C. Amazon RDS 独立运行两个数据库实例，每个实例都有自己的连接字符串。你必须更新应用程序服务器上的代码，因为 AWS 对虚拟机管理器层没有可见性。
- D. Amazon RDS 使用 `Route 53` 创建连接字符串并自动更新 IP 地址以指向备用实例。

- 12. 将 Amazon Elastic Block Store (Amazon EBS) 卷挂载到 Amazon Elastic Compute Cloud (Amazon EC2) 实例时，必须满足哪些条件？
    - A. Amazon EBS 卷必须与实例位于同一个可用区（Availability Zone）。
    - B. Amazon EBS 卷必须与实例位于同一个账户中。
    - C. Amazon EBS 卷必须被分配给一个 `AMI ID`。
    - D. Amazon EBS 卷必须与实例具有相同的安全组。

- 13. 你被要求将繁忙的 `MySQL` `Amazon Relational Database Service` (Amazon RDS) 数据库迁移到 `Amazon Aurora`。你需要尽可能减少停机时间且不丢失任何数据。满足这些要求的最佳方法是什么？
    - A. 为 Amazon RDS 实例创建快照。使用该快照为 `Amazon RDS for MySQL` 数据库创建一个 `Amazon Aurora` 副本。一旦同步完成，将 `Aurora` 读入实例转换为独立的 `Amazon Aurora` DB 集群，并将应用程序指向新的 `Amazon Aurora` DB 集群。
    - B. 创建 `Amazon Simple Storage Service` (Amazon S3) 桶，并将 Amazon RDS 数据库作为平面文件转储上传到桶中。从转储恢复到新的 Amazon Aurora 数据库。
    - C. 将最近的 Amazon RDS 自动备份恢复到新的 Amazon Aurora 实例。启动应用程序，将应用程序指向新的 `Amazon Aurora` DB 实例，并启动应用程序。
    - D. 创建快照。将快照恢复到新的 Amazon Aurora 实例。将应用程序指向新的 `Amazon Aurora` DB 实例，并启动应用程序。

- 14. 如果 RDS 多可用区（Multi-AZ）部署的 `Amazon Relational Database Service` (Amazon RDS）实例的主节点发生故障，你必须执行以下操作进行恢复：
    - A. 什么都不用做。节点将自动故障转移到备用区域的三个只读副本之一。
    - B. 什么都不会自动故障转移到备用实例；可能会发生短暂的停机。
    - C. 通过从最近的自动备份恢复手动建立一个新实例。
    - D. 使用 AWS CLI 的 `initialize-rds-failover` 命令手动启动跟随者。

- 15. 作为你收到的应用程序要求的一部分，你必须部署一个新的 `Amazon DynamoDB` 数据库。你必须以高可用的方式部署。你如何部署此数据库？
    - A. 在单个可用区（AZ）中部署 `Amazon DynamoDB` 数据库。设置到 `Amazon S3` 的自动备份任务，以及从 `S3` 到第二个可用区 `DynamoDB` 数据库的自动恢复任务。
    - B. 为两个可用区使用 `Amazon DynamoDB` 本 版本。
    - C. 你无法使用 `Amazon DynamoDB` 高可用（HA）需求。
    - D. 在目标区域部署 `Amazon DynamoDB` 数据库。

- 16. 你的应用程序数据库被用户报告运行缓慢。经过调查，你发现它面临着大量的读取操作。克服这一问题的一种方法是什么？
    - A. 使用 `Amazon CloudFront` 分发。
    - B. 为数据库使用 `ElastiCache`。
    - C. 为应用层使用 `AWS Shield`。
    - D. 使用 `Route 53` 基于延迟的路由。

- 17. 你有一个分配了弹性 IP 的 `Elastic Compute Cloud` (Amazon EC2) 实例。当你终止（terminate）它时会发生什么？
    - A. 弹性 IP 保留在账户中。
    - B. 弹性 IP 保留在实例上。
    - C. 弹性 IP 被删除。
    - D. 你无法执行该操作。

- 18. 你正在使用 `CloudFront` 提供内容。保护这些内容的最佳方法是什么？
    - A. 使用源访问标识（`OAI`）。
    - B. 使用身份和访问管理（`IAM`）。
    - C. 使用签名 URL 或 `Cookie`。
    - D. 使用 `Amazon Simple Storage Service` (S3)。

- 19. 你正寻求加密 `DynamoDB`。你该如何做？
    - A. 在 `DynamoDB` 控制台中开启服务器端加密。
    - B. 通过 `AWS CLI` 开启服务器端加密。
    - C. `DynamoDB` 不支持服务器端加密。
    - D. 使用透明数据加密（`TDE`）。

- 20. 你正在重构你的应用程序。目标之一是使用 `Auto Scaling` 来添加和删除实例。哪种 AWS 服务提供此功能？
    - A. `Relational Database` (`RDS`)
    - B. `Amazon EC2`
    - C. `DynamoDB`
    - D. `Simple Storage Service` (`S3`)

- 21. 你的公司维护着一个集群的应用程序。你想迁移到一个提供此功能的服务。你需要设置什么？
    - A. `Simple Queue Service` (`SQS`)
    - B. `Amazon CloudFront`
    - C. `Amazon Elasticsearch`
    - D. `AWS X-Ray`

- 22. 你需要创建一个允许 `Direct Connect` 的虚拟有云（`VPC`）。以下组合允许 `Direct Connect` 但阻止访问互联网？
    - A. 如果你有 `Direct Connect` 连接，默认你可以访问互联网。
    - B. 创建具有 `Internet` 网关（`IGW`）和 `VPN` 网关的 `VPC`。
    - C. 创建 `Direct Connect` 网关（`Direct Connect Gateway`）。

- 23. 你在经典负载均衡器（classic balancer）后有 10 个 `Amazon Elastic Compute Cloud` (Amazon EC2) 实例。你需要执行什么来确保流量只路由到健康实例？
    - A. 终止健康实例。
    - B. 在负载均衡器上启用跨可用负载。
    - C. 开启健康检查，负载均衡器会将流量发送到健康实例。
    - D. 什么都不用做。负载均衡器会终止健康实例。

- 24. 你注意到 `Auto Scaling` 组已经扩展到最大尺寸。当 `Auto Scaling` 组扩容（`scales out`）和收缩（`scales in`）时，如何收到通知？
    - A. 让你的 `Auto Scaling` 组向 `Simple Queue Service`（`SQS`）发送消息。定期检查队列中的 `Auto Scaling` 消息。
    - B. 为你的手机号码配置 `Simple Notification Service`（`SNS`）主题的短信订阅。
    - C. 为 `Amazon SNS` 主题配置一个发送电子邮件的 `Amazon Lambda` 函数。
    - D. 定期查询 `Auto Scaling` 组以检查期望容量。

- 25. 你被分配为一个研发部门实施高性能计算（HPC）工作负载。该负载逐个处理任务，并且能够容忍集群中的节点故障。每个任务运行大约一小时。从成本效益的角度来看，哪种 AWS 云服务最适合你的工作负载？
    - A. `Amazon Elastic Compute Cloud` (Amazon EC2) `Spot` 实例
    - B. `Amazon EC2` 需需实例
    - C. `Amazon Elastic Compute Cloud` (Amazon EC2) 预留实例
    - D. `AWS Lambda`

## 评估测试答案

- 1. C. 实例状态（Instance Status）监控你单个实例的软件和硬件。列出的其他项目是影响底层 AWS 硬件的故障。
- 2. B. 公有子网（Public Subnet）中的路由表有一条指向 `IGW` 的路由。`IGW` 与 `VPC` 关联，而不是与子网。弹性负载均衡（Elastic Load Balancers）可以同时位于公共子网和私有子网中。
- 3. A. 默认情况下，负载均衡器将流量均匀分布在你为负载均衡器启可用区（Availability Zones）。要在所有启用的可用区内的所有注册实例之间分配流量，请为负载均衡器启用跨区域负载均衡（cross-zone load balancing）。但是，仍然建议在每个可用区维持数量相当的实例，以获得更好的容错性。
- 4. C. 如果你在创建 DB 实例或集群时未指定首选维护窗口，则 Amazon RDS 将每周随机选择的一天分配一个 30 分钟的维护窗口。
- 5. A. 你负责云端安全，这包括对运行在客户账户内的资源配置并应用安全组（Security Groups）。
- 6. C. `Amazon Simple Storage Service`（Amazon S3）提供了一种低成本的方法，以高可用且持久性的方式存储对象。
- 7. D. 每个 `Amazon EBS` 卷最多可选择 16 TB，因此你必须创建多个卷的 RAID 数组以达到所需的 `IOPS`。
- 8. A. 用户数据（User data）在启动时运行并可用于安装软件。列出的其他答案是元数据（`metadata`）的示例，它们与 `Amazon EC2` 实例关联，并通过 `Amazon EC2` 元数据服务访问。
- 9. C. `VPC` 的子网必须与 `VPC` 本身位于相同的范围内。
- 10. C. 你可以使用伸缩策略（scaling policies）自动增加或减少组中运行的 `EC2` 实例数量，以适应变化的情况。当伸缩策略生效时，自动扩展组（Auto Scaling group）会调整组的所需容量并根据需要启动或终止实例。如果你手动进行扩展或按比例扩展，必须调整组的所需容量以使更改生效。
- 11. Amazon RDS 连接字符串基于 `Amazon Route 53` `DNS`。在 Amazon RDS 内部，它们被称为端点（`endpoints`）。端点包括数据库实例的 `DNS` 名称和端口号。
- 12. `Amazon EBS` 卷必须与你附加的实例位于同一个可用区（`AZ`）。
- 13. A. 你可以创建一个 `Amazon Aurora` 读副本（Read Replica）来从 `Amazon RDS` `MySQL` 源同步数据。通过切换到副本，你可以高效地在数据库之间迁移。使用手动快照来预填充读副本。
- 14. B. 多可用区部署中的 `Amazon RDS` 实例将自动从故障的主节点故障转移到备用节点。
- 15. `Amazon DynamoDB` 数据库会自动在 AWS 区域内的三个设施之间复制。
- 16. `Amazon ElastiCache` 提供内存缓存，可以缓存频繁读取的数据，并缓解常见的读取查询命中你的数据库层。
- 17. A. 弹性 IP（Elastic IPs）与账户关联，而不是 `Amazon EC2` 实例关联。然而，未分配的弹性 IP 会产生费用。这样做是为了防止囤积 IP 地址。
- 18. 不应使用 `IAM`，因为内容将由没有 `IAM` 账户的个人访问。`List Distribution` `API` 仅列出分发；它不控制访问。源身份（`OAI`）是你控制 `Amazon S3` 对象中内容访问的方法，而不是 `Amazon CloudFront` 分发。
- 19. `Amazon DynamoDB` 不支持 AWS 密钥管理服务（AWS KMS）服务端加密。你可以使用客户端加密在 `Amazon DynamoDB` 中存储加密数据。
- 20. `Amazon DynamoDB` 是一种快速且灵活的 NoSQL 数据库服务，适用于所有需要一致性和单位毫秒延迟的应用。
- 21. `Amazon SQS` 提供一种消息队列服务，它是全托管的。
- 22. `AWS Direct Connect` 将 `VPN` 网关连接到 `VPC`，它是 `VPC`。
- 23. 你可以使用健康检查来监控注册实例的健康状况。
- 24. 当你使用 `Auto Scaling` 扩展你的应用程序时，`Amazon SNS` 会通过 `Lambda` 发送。
- 25. A. 竞价实例（Spot instances）为你提供相对于按需价格的空闲容量折扣。

# 第 1 章

## AWS 上的系统运维简介

AWS CERTIFIED SYSOPS ADMINISTRATOR - ASSOCIATE 考试本章涵盖的主题可能包括但不限于以下：

### 领域 4.0：部署与配置

- 4.1 展示如何构建环境并管理实施

内容可能包括：

- 如何部署云服务
- 对三层架构的熟悉
- 部署无服务器架构

### 领域 6.0：安全

- 6.1 展示在使用 AWS 平台时确保数据完整性和访问控制

内容可能包括：

- AWS 责任共担模型
- AWS CloudTrail
- Amazon EC2 安全组
- 网络访问列表 (ACL)

### 领域 7.0：网络

- 7.1 展示如何在 AWS 上实现网络功能

内容可能包括：

- Amazon 虚拟私有云 (Amazon VPC)

![](img/5a8c28d2e214d3abf9ba8ffcdf58f47_36_0.png)

![](img/5a8c28d2e214d3abf9ba8ffcdf58f47_37_0.png)

## 优化系统

作为系统运维人员，你是公司实现性能最大化的最佳代理，因为你的分析能够帮助你选择正确的基础设施配置、最优的存储方法以及尽可能好的客户结果。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_38_0.png)

由 123net - 自有工作，CC BY-SA 3.0，https://commons.wikimedia.org/w/index.php?curid=17384917

然而，你做的不仅仅是优化速度；你还在为了成本优化。通过使用弹性环境，你的环境不仅在需求高峰期间进行向外扩展以最小化延迟，还能在稍后进行收缩以减少支出。你管理的是一个每天每小时都处于高利用率的环境。

## 加固系统

事物会损坏，系统会离线，但你不会让这些让你彻夜难眠。你维护的是高可用架构：系统能够检测到故障组件并自动切换，根据需要进行更换和恢复，而不会中断对消费者的服务。

但你的可用性方法涵盖的不仅是单一区域和多个可用区（Availability Zones）。AWS 上的系统运营在需要时跨区域和混合方法，以确保无论大自然带来什么影响，业务都能持续运行。

## 保护系统

安全组、访问控制列表和私有网络的结合，辅以 `Amazon CloudFront` 和 `AWS Shield` 等原生工具，可以帮助你的环境抵御最阴险的攻击。

# 第 4 章 第 1 节 AWS 系统运维简介

然而，威胁并不总是来自外部。你知道最危险的向量是内部攻击。这就是为什么你严密地执行了分区域、限制性权限集策略，以便无人能进入未经授权的区域，并结合详细的应用程序编程接口（`API`）日志，报告所有操作，以对你的资产提供全面的控制。

## AWS 认证系统运维管理员 - 助理级 (AWS Certified SysOps Administrator - Associate)

正如本章引言介绍，AWS 系统运维人员关注广泛的职责。AWS 认证系统运维管理员 - 助理级认证旨在测试你对系统运维领域的知识。这本书不仅解释了考试中的领域，还将引导你熟悉作为 AWS 系统运维人员要获得成功必须掌握的 AWS 的不同方面。测试分为七个权重相当的领域组成：

- 1. 监控与指标
- 2. 高可用性
- 3. 分析
- 4. 部署与配置
- 5. 数据管理
- 6. 安全
- 7. 网络

在你探索各个 AWS 架构和服务时，请注意，许多 AWS 产品具有适用于大多数（如果不是全部）七个领域的运维考量。

## 你应该学习哪些 AWS 服务？

简单的答案是，“所有服务”。

AWS 正在不断演进并增加新产品。截至本书时，AWS 拥有超过 90 种独特的服务。每种服务都有自己的安全、数据、监控和可用性考量。作为 AWS 系统运维人员，你的任务是理解这些考量，以及如何为了性能和成本优化这些服务。本书接接几章将引导你了解服务类别，解释如何从运维角度处理这些服务，并讨论你应该学习的内容。

## 参考架构：三层设计

由于有 90 多个服务和大约 55 道题，从数学上讲，并不是每个服务都能在认证考试中涵盖。常用的服务出现在许多不同的问题中，而具有特定用例的服务出现概率要低。

例如，在学习存储产品时，你必须理解 `Amazon Simple Storage Service` (`Amazon S3`)、`Amazon Elastic Block Store` (`Amazon EBS`) 和 `Amazon Glacier` 提供的选项。你可以预期这些服务会出现在所有领域的问题中。相比之下，`AWS Snowmobile` 可能会出现在测试中，但因为它仅用于少数特定场景，从统计学讲，它不太可能出现一次，或者根本不出现。

最佳准则是查看常见的参考架构。在这些参考架构中，你可以看到特定的架构，这些服务是通用的。

## 参考架构：三层设计

由于 90 多个服务和大约 55 道题，从数学上讲，并不是每个服务都能在认证考试中涵盖。常用的服务出现在许多不同的问题中。

以下部分提供了：

- 前端层（Web）
- 应用层（Application）
- 数据库层（Database）

### 三层设计引言

三层模型演进自 90 年代。在云原生演进中，三层模型是：

在 AWS 架构中是可扩展的。

### Web 层 (Web Tier)

Web 层是前端，它接收请求并传递给 AWS。
