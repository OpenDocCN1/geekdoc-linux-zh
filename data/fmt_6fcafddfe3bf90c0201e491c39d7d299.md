
10. Amazon CloudWatch 不区分指标的来源。如果您从不同的来源推送具有相同命名空间（`namespace`）和维度（`dimensions`）的指标，CloudWatch 将其视为单个指标。这对于分布式扩展系统中的指标非常有用。例如，`Web` 服务器中的所有主机都可以发布相同的指标，代表它们正在处理的请求的延迟。CloudWatch 将这些视为单个指标，允许您获取跨应用程序所有请求的最小值、最大值、平均值和总和的统计数据。

```
http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html
```

11. A. 每个指标数据点必须标记时间戳。时间戳可以追溯到过去两周，或提前最多两小时。如果您不提供时间戳，Amazon CloudWatch 将根据数据接收的时间为您创建一个时间戳。

`http://docs.aws.com/AmazonCloudWatch/latest/monitoring/cloudwatch-concepts.html`

12. `Put-metric-data` 将指标数据点发布到 Amazon CloudWatch。Amazon CloudWatch 将数据点与指定的指标关联。如果该指标不存在，Amazon CloudWatch 将创建该指标。当 Amazon CloudWatch 创建指标时，该指标可能需要 15 分钟才会出现。

`http://docs.aws.com/AmazonCloudWatch/latest/Reference/API-PutMetricData.html`

13. 通过 CloudWatch，您可以记录、持续监控并保留与跨 AWS 基础设施的 `API` 调用相关的事件。CloudWatch Events 提供描述 AWS 资源变化的实时事件流，发送到 Amazon EC2 实例、AWS Lambda 函数、Amazon Kinesis Streams、Amazon ECS 任务、Step Functions 状态机、Amazon SQS 队列、主题或内置目标。

`https://aws.amazon.com/cloudtrail/`

`http://docs.aws.com/AmazonCloudWatch/latest/events/WhatIsCloudEvents.html`

# 复习题答案

# 第 10 章：高可用

1. A, C. Amazon Simple Notification Service（Amazon SNS）支持这些协议：`HTTP`/`HTTPS`、Email/JSON、Amazon SQS 和 SMS。

2. 要开始使用 Amazon SNS，首先创建主题（`topic`），选择您的协议，订阅主题并向您的主题发布。

3. 一些 AWS 客户利用一个或多个 AWS Direct Connect 连接的优势作为连接 AWS 的主连接，并结合成本成本备份连接。为了实现这一目标，他们建立了带有 `VPN` 备份的 AWS Direct Connect 连接。

4. 如果您建立了 AWS Direct Connect 连接，流量将自动转移到第二条链路。前提是您在配置连接时启用了双向转发检测（`BFD`），以确保快速检测和故障转移。

5. 跨区域复制是存储桶级的功能，允许在不同 AWS 区域的存储桶之间自动、异步复制对象。要激活此功能，请向您的源桶添加复制配置。在配置中，您需要提供信息，例如要复制对象的目标桶。您可以请求 S3 复制所有对象或具有特定键名前缀的对象的子集。例如，您可以配置跨区域复制，仅复制键名前缀为 `Tax/` 的对象。这将导致 Amazon S3 复制键名如 `Tax/doc1` 或 `Tax/doc2` 的对象，而不是键名为 `Legal/doc3` 的对象。

# 第 10 章：高可用

6. 可见性超时（Visibility timeout）是消息对其他应用程序不可见的时间段。在可见性超时期间，组件从队列中删除。

7. Amazon RDS 多 AZ 部署提供了增强的可用性和可靠性，因为 RDS 将数据同步复制到另一个可用区的备用实例。

8. A, B, E. 您可以使用 Route 53 别名、权重、延迟路由设置各种故障转移配置。您可以选择主活动、主备式或其他混合配置。

9. B, C. Route 53 健康检查监控应用程序、`Web` 服务器和其他资源的健康状况。您创建的每个健康检查监控以下内容：指定资源（如 `Web` 服务器）的健康状况；CloudWatch 告警的状态；健康检查的状态。

10. B. 虽然硬件 `VPN` 如何冗余，软件 `VPN` 支持两个隧道。只需从 AWS 管理控制下载路由器配置并配置两个网关。

11. D. Amazon S3 是可能需要快速恢复的备份数据的理想目的地。在 S3 之间传输数据通常通过网络进行，因此可以在任何地方访问。有很多与 Amazon S3 和 Amazon Glacier 集成的商业和开源备份解决方案。

12. A. 虽然 S3 网关会让数据恢复更快，但需要恢复的是数据库。如果您使用数据中心生产数据库同步的小型数据库，光纤方案（`Pilot light`）将是更好的选择。在灾难发生，您将调整数据库大小以处理生产负载。

13. D. 如果您将虚拟私有网关连接到 Amazon VPC 并在路由表中启用传播，您的 `VPN` 连接将作为传播路由自动出现在您的路由表中。

14. A. 多站点运行在 AWS 或您的现有基础设施上，并采用主活动式配置。您将采用的数据复制方法取决于您选择的恢复点。对于零恢复目标，您可能会找到一个与生产工作负载同步运行的全规模容灾备备站点。当灾难发生时，所有流量将路由到能够处理您的应用程序 100% 预期负载的站点。

15. 热备（`warm-standby`）术语用于描述一种容灾备备场景，其中全功能环境的缩小版本在云中始终运行。热备解决方案扩展了光纤方案元素和准备工作。由于服务始终运行，它进一步缩短了恢复时间。通过识别您的业务关键系统，您可以在 AWS 上完全复制这些系统并实现始终在线。

## 索引

## A

- 访问控制，484。另请参见 AWS Identity and Access Management

- Amazon CloudWatch, 379–381

- Amazon RDS, 81

- Amazon Redshift 集群, 293–294

    - 细粒度，81
    - 用于负载均衡器，178
    - 网络隔离的，82
    - 对于 Route 53, 185

- 访问控制列表 (ACLs), 3, 8

- Amazon S3, 75

- Amazon VPC, 157, 158

    - 网络，71, 72, 157, 158, 485, 487
    - 网络安全，48, 71

- 访问密钥，25, 55, 484

- 访问日志，486

- Amazon CloudFront, 192

- Amazon S3, 137

- 弹性负载均衡 (Elastic Load Balancing), 63, 177

    - ENs，63

- ACID, 252–254

- ACLs。另请参见 访问控制列表

- ACM。另请参见 AWS Certificate Manager

- 活动目录 (Active Directory), 94, 482

- Active Directory Connector (AD), 13, 182

    - 主主式故障转移，458
    - 主备式故障转移，459
    - 主备式故障转移，458

- AD Connector。另请参见 Active Directory Connector

- 地址解析协议 (ARP), 71

- 管理访问，控制，123

- Adobe Flash Media Server, 186

- Adobe Media, 186

- Adobe RTMP。另请参见 实时消息传输协议 (Real-Time Messaging Protocol)

- 代理，400, 401–483, 484

- Amazon CloudWatch 的聚合

    - 统计数据，375–376

- 报警，192, 365。另请参见 Amazon CloudWatch Alarms

- 别名记录，183

- Amazon API Gateway, 17

- Amazon Aurora, 81, 255, 490

    - PostgreSQL 版本，259
    - 主实例，256
    - 读副本，267
    - 可靠性，257
    - 复制，257
    - 向上扩展，273
    - 安全，258
    - 卷，256–257

- Amazon CloudFront, 3, 9, 11, 17, 15, 185, 234, 488, 492

    - 与 AWS WAF 的，64
    - 控制台报告，194
    - 实施，186–194
    - 密钥对，59
    - 管理，194
    - 监控，192
    - 安全，74–75, 194
    - 用于 TLS 的，197

- Amazon CloudWatch, 10, 13, 119, 177, 184, 192, 365, 367, 482, 492, 495

    - Amazon EBS 监控，3368–391
    - Amazon EC2 监控，378–388, 421
    - Amazon ElasticCache 监控，391–392
    - Amazon RDS 标，280, 292–393
    - 身份验证与访问，控制，379–381
    - AWS 费用监控，406–410
    - AWS Cloud 服务集成，382
    - 与 AWS CloudTrail 的，414, 421
    - 仪表板，376
    - 数据报告，390, 403
    - 维度，372–373, 405–406
    - 弹性负载均衡器指标，393–395
    - ev，396
    - 限制，382–383
    - 指标，404
    - 通用，366–385
    - 自定义，369–370
    - 免费，369
    - 留存，370
    - 缺失数据点，386
    - 命名空间，371
    - RDS 指标，280
    - RDS 监控，278, 279

# Amazon CloudWatch Alarms – Amazon Elastic Compute Cloud (Amazon EC2)

- 服务，368–369
- 统计数据，373
- 聚合，375–376
- 分位数，376–377
- 周期，374–375
- 单位，374
- 服务，328
- 任务，327–328

- Amazon EC2 专用主机，74

- Amazon EC2 Systems Manager，120

- Amazon ECR。另请参见 Amazon EC2 Container Registry

- Amazon EFS。另请参见 Amazon Elastic File System

- Amazon Elastic Block Store (Amazon EBS), 7, 9, 12, 210, 212, 486, 488

    - Amazon EBS.，222–223
    - VPC 日志的，165

- Amazon CloudWatch Alerts，279, 365, 384–388

- Amazon CloudWatch Events，365, 395

    - 事件，396–397
    - 指标和维度，398
    - 规则，397
    - 目标，397

- Amazon CloudWatch Logs，13, 62, 279, 318, 365, 399

    - 代理，400–401, 484
    - 归档数据，400
    - 部署，317
    - 维度，405–406
    - 监控，400–401
    - 指标，404–405
    - 搜索和过滤，403–404
    - VPC 日志，165

- EC2 容量，217–218

- 停用，220

- EC2 配置，115

- EC2 实例类型，113

- 由 EBS 支撑的 EC2 实例，116–118, 117, 394

- EC2.，221

- IOPS 和吞吐量，216

- 最大 IOPS，215

- 最大吞吐量，215–216

- 监控，220, 389–390

- 挂载卷，218

- 定价，214

- 预留 IOPS，217

- 预留，216–218

- Amazon Cognito，93–94

- Amazon DynamoDB，9, 12, 251, 283, 472, 485, 490, 491, 492

    - Amazon VPC 端点，292
    - 核心组件，284–285
    - 数据类型，288
    - 元数据标签，291
    - 多路复制，457
    - 读写一致性，290–391
    - 预留容量，290
    - 安全，80–81, 68–220
    - 快照，218–219
    - 状态检查，390–391
    - 吞吐量，215–216, 220
    - 卷，68, 116
    - 类型，213–216

- Amazon Elastic Compute Cloud (Amazon EC2)，8, 12, 16, 109, 174, 398, 390, 494

- Amazon EBS 供应和容量，217–218

- Amazon EBS。另请参见 Elastic Block Store

- Amazon EC2。另请参见 Amazon Cloud

- Amazon EC2 Container Registry (Amazon ECR)，327

- Amazon EC2 Container Service (Amazon ECS)，109, 123–125, 174

    - 集群，325–326
    - 容器，326–327
    - 镜像，327
    - 存储库，327

- Amazon EMR 和，89–90

- 自动恢复，455–456

- 使用 AWS CLI，27, 116

    - 块存储，210
    - 配置，114–117
    - 客户责任，44
    - 挂载的 EBS 卷，212–213, 213
    - EBS 支撑的实例，116–118, 117
    - 特性，111
    - 健性检查，175
    - 实施，111–117

# Amazon Elastic File System – Amazon Relational Database Service

- 实例购买选项，120–121

- 实例类型选择，112–123

- 密钥，59

- 负载均衡，和 153, 171

- 位置，482

- 公共 IP 地址，114

- 安全，65–69

- 安全组，271

- 快照，118

- 竞价定价 (Spot Pricing)，114

- 状态检查，378–399

- 存储配置，115–116

- 存储库支撑的实例，116–118

- Amazon Elastic File System (Amazon EFS)，12, 218–222, 289

- Amazon Elasticache，12, 77–88, 296–297

    - 监控，391–392

- Amazon EMR，89–90

- Amazon Glacier，12, 230, 488

    - 备份存储与，468
    - 生命周期周期策略，223
    - 日志归档至，62
    - MFA 破解，231
    - 复制，210
    - 取回时间，211
    - 安全，77–79
    - Vault Lock，231

- Amazon Infrastructure Group，47

- Amazon Inspector，13, 64, 123, 485

- Amazon Kinesis，17–90

- Amazon Lightsight，109, 130–133, 468

- Amazon Machine Image (AMI)，8, 11

    - 创建，121–122, 316
    - ID，338
    - 实例存储，222
    - 密钥，59
    - 选择，112
    - 证书生成，49
    - 存储格式化，210
    - 更新，67

- Amazon RDS。另请参见 Relational Database Service

- Amazon RDS tag，277

- Amazon Redshift，44, 292

    - Amazon EC2-Classic，294
    - Amazon EC2-VPC，294
    - 备份，85
    - 账单，295–296
    - 集群访问和安全，293–294
    - 集群，293
    - 数据库，294
    - 事件和通知，295
    - 高可用性，293
    - 监控，295
    - 性能，295
    - 安全，84–87

- Amazon Redshift Spectrum,292

- Amazon Relational Database Service (Amazon RDS)，9, 12, 44, 251, 492

    - Amazon CloudWatch 指标，280, 392–393
    - Amazon Redshift.，278–280
    - 自动补丁，84
    - 块，63–268
    - DB 实例，255–256
    - 加密，82–272
