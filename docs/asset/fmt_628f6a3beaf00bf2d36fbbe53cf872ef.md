
3. 考虑使用自动伸缩自动调整 AWS 实例群的大小。通过设计多可用区（Multi-AZ）架构，您可以进一步增加多站点解决方案的可用性。

# 从灾难回滚

一旦主站点恢复到工作状态，您将需要恢复正常服务，这通常被称为“回滚”（fail back）。根据您的 DR 策略，这通常意味着反转数据复制流，主站点宕机期间接收到的任何数据更新都能同步回，且不会丢失数据。让我们从各种故障转移方法来讨论回滚。

# 备份与恢复方法的回滚

要从灾难恢复站点回滚到现已工作的生产站点，您需要遵循以下步骤：

### 灾难恢复备份与恢复方法的关键步骤

- 1. 冻结 DR 站点的数据更改。
- 2. 制作备份。
- 3. 将备份恢复到主站点。
- 4. 将用户重新指向主站点。
- 5. 解冻更改。

# 光源模型、热备用和多站点方法的回滚

使用光源模型（Pilot Light）、热备用（Warm-Standby）和多站点方法从灾难恢复站点进行回滚，使用的是相同的方法来向原生产站点恢复服务。

### 灾难恢复光源模型、热备用和多站点方法的回滚

- 1. 在主站点同步更改后，建立从 DR 站点到主站点的反向镜像/复制。
- 2. 冻结 DR 站点的数据更改。
- 3. 将用户重新指向主站点。
- 4. 解冻更改。

## 总结

在本章中，我们讨论了如何解耦应用程序以实现扩展性和高可用性。讨论的技术包括使用 `Amazon SQS` 和 `Amazon SNS` 将应用程序的前端与后端解耦，从而减少它们之间的相互依赖关系（例如，它们可以独立扩展）。如 `Amazon S3` 和 `Amazon DynamoDB` 等区域级应用程序可以将其数据复制到其他区域，以提供区域高可用解决方案。在构建系统时，使用固有的容错 `AWS` 托管服务是最佳实践。对于无法利用托管服务的负载，则取决于您如何使其具有高可用。`AWS` 提供了组件——您只需将它们组合在一起即可交付高可用或容错的系统。最后，针对使用各种 `DR` 故障转移场景和每种故障转移方法的回滚方法的灾难和恢复计划。

# 复习资源

- `Amazon Simple Queue Service`: <https://aws.amazon.com/sqs/>
- `Amazon Simple Notification Service`: <https://aws.amazon.com/sns/>
- `Amazon DynamoDB` 跨区域复制: <http://docs.aws.amazon.com/amazynamodb/latest/developerguide/Streams.CrossRegion.html>
- `AWS` 上的灾难恢复: <https://d3c629buwruutt.cloudfront.net/AWS_Disaster_Recovery.pdf>
- `AWS` 上的容错与高可用: <https://media.amazon.webservices.com/architecturecenter/AWS_ac_ra_fha_04.pdf>

## 考试要点

理解 `Amazon SQS` 轮询。`Amazon SQS` 默认使用短轮询，仅查询部分服务器（根据加权随机分布）以确定是否有消息包含在响应中。长轮询通过查询所有（而非有限数量的）服务器来消除空响应。

理解可见性超时（`visibility timeout`）及其应用场景。在接收到消息后，它留在队列中。为了防止其他消费者再次处理该消息，`Amazon SQS` 设置了可见性超时，在此期间内，`SQS` 防止其他消费者接收和处理该消息。

理解 `Amazon SQS` 标准队列的消息顺序。标准队列提供松散的 `FIFO`（先入先出）能力。

在本章中，我们讨论了如何解耦应用程序以实现扩展性和高可用性。讨论的技术包括使用 `Amazon SQS` 和 `Amazon SNS` 将应用程序的前端与后端解耦，从而减少它们之间的相互依赖关系（例如，它们可以独立扩展）。如 `Amazon S3` 和 `Amazon DynamoDB` 等区域级应用程序可以将其数据复制到其他区域，以提供区域高可用解决方案。在构建系统时，使用固有的 `AWS` 托管服务是最佳实践。对于无法利用托管服务的负载，则取决于您如何使其高可用。`AWS` 提供了组件——您只需将它们组合在一起即可交付高可用或容错的系统。最后，针对使用各种 `DR` 故障转移场景和每种故障转移方法的回滚方法的灾难和恢复计划。

# 第10 章 高可用性

理解 `Route 53` 健康检查的工作原理。了解检查类型以及如何针对指标设置告警。

了解如何设置高可用 `VPN`。虚拟私网网关（`VPG`）支持双隧道。大多数路由器可以在主备模式下工作。

理解如何使 `AWS Direct Connect` 高可用。要使 `AWS Direct Connect` 高可用，请部署 `Direct Connect`。

理解如何将 `VPN` 作为 `Direct Connect` 的备份。如果您无法部署 `Direct Connect` 或对可用性有额外要求，请保留现有的 `VPN` 作为备份。

了解 `AWS` 提供的各种灾难恢复方法。故障故障转移类型包括备份/恢复、光源模型、热备用和多站点。了解如何故障转移以及回滚。

# 技巧

准备好测试中心！带上两种政府颁发的身份证（包含照片）。带上确认函。将所有电脑、可穿戴设备等留在家里。您不想因为物理问题错过考试。

# 练习

到目前您应该已经建立了 `AWS` 账户。如果还没有，现在是设置的时候。请注意，这些练习是在您的 账户中进行的，因此不是免费的。

启动资源时使用免费层。`Amazon` 免费层适用于参与的 `AWS` 区域：美国东部（弗吉尼亚北部）、美国西部（俄勒冈）、美国西部（加州）、加拿大（中部）、欧洲（伦敦）、欧洲（爱尔兰）、欧洲（法兰克福）、亚洲（新加坡）、亚洲（东京）、悉尼和南方（圣保罗）。更多信息请见 <https://aws.amazon.com/dn/optaton/server-side-test/free-tier/>

尚未安装 `AWS` 命令行工具，请参考第 2 章练习 2.1（`Linux`）或练习 2.2（`Windows`）。

`AWS CLI` 的参考可以在此处找到：`docs.aws.amazon.com/cli/latest/reference/`

这些练习将引导您完成一些高可用场景，并让您研究“如何操作”以完成练习。通过查找如何执行

通过完成特定任务，你将走上掌握该任务之路。本指南的目标不仅仅是帮助你准备 `AWS` 认证 `SysOps` 管理员 – 助理考试，它旨在成为你作为 `AWS` 认证 `SysOps` 管理员日常工作中的参考伙伴。

## 练习 10.1

### 创建 `Amazon SNS` 主题。

在此练习中，你将创建一个 `Amazon SNS` 消息。

- 1. 登录 `AWS` 管理控制台。
- 2. 导航到 `Messaging`（消息），然后到 `Amazon SNS`，加载 `Amazon SNS` 仪表板。
- 3. 创建一个新主题。主题名称和显示名称都使用 `MyTopic`。
- 4. 注意到 `ARN` 是自动分配的。

你刚刚创建了第一个 `Amazon SNS` 主题。

## 练习 10.2

### 为你的主题创建订阅。

在此练习中，你将使用你的电子邮件地址为主题创建订阅，然后你将确认你的电子邮件地址。

- 1. 在 `AWS` 管理控制台的 `Amazon SNS` 仪表板中，导航到 `Topics`（主题）。
- 2. 选择你刚刚创建的主题。将订阅协议更改为 `Email`（电子邮件），并输入你的电子邮件地址。
- 3. 创建订阅。
- 4. 你将收到一封来自 `Amazon Simple Notification Service (Amazon SNS)` 的邮件。在继续之前，你必须打开它并确认你的电子邮件地址。

你刚刚为你的主题创建了订阅。

## 练习 10.3

### 向你的主题发布消息。

在此练习中，你将向你的主题发布消息。

- 1. 在 `AWS` 管理控制台的 `Amazon SNS` 仪表板中，导航到 `Topics`（主题）。
- 2. 导航到你的主题（选择 `Publish to Topic`，发布到主题）。

### 练习 10.3（继续）

- 3. 使用 `Test Message` 更新主题。将消息格式保留为 `Raw`（原始），并将生存时间 (`TTL`) 固定为 300。在消息中，输入 `This is a test, only a test.`
- 4. 发布消息。

检查你的电子邮件，你应该已经收到了 `Amazon Simple Notification (Amazon SNS)` 消息。在完成练习 10.4 和 10.5 之前，不要删除此主题。

## 练习 10.4

### 创建 `Amazon Simple Queue Service (Amazon SQS)`。

在此练习中，你将创建一个 `Amazon Simple Queue Service (Amazon SQS)`。

- 1. 登录 `AWS` 管理控制台。
- 2. 导航到 `Messaging`，然后到 `Amazon Simple Queue Service`，加载 `Amazon SQS` 仪表板。
- 3. 创建一个新队列，默认可见性超时设置为 30 秒，消息保留期设置为 1 天。将最小消息大小保持为 256 KB，其余设置保持默认值。然后创建队列。

你现在应该有一个名为 `Input` 的队列。

## 练习 10.5

### 将队列订阅到你的 `Amazon SNS` 主题。

现在你将订阅练习 10.1 中的 `MyTopic`。

- 1. 在 `AWS` 管理控制台中，导航到 `Messaging` 然后到 `Amazon Simple Queue Service`。
- 2. 选择你的输入队列（`input`），并订阅到你的 `MyTopic` `Amazon SNS` 主题。
- 3. 返回 `Amazon SNS` 仪表板，选择 `Topics`（主题）。
- 4. 发布到 `Topic`（主题），并选择默认设置。
- 5. 导航到 `Amazon SQS` 仪表板。
- 6. 你会在输入队列中注意到一条消息（如果你开启了电子邮件通知，屏幕上应该弹出一个邮件）。
- 7. 选择输入队列，选择 `Actions`（操作）并 `poll the queue`（轮询队列）。
- 8. 选择 `more details`（更多详细）查看消息。滚动查看正文并注意不同的字段。
- 9. 删除消息、删除队列，然后删除你的 `Amazon SNS` 主题。

## 练习 10.6

### 在多可用区（Multi-AZ）配置中部署 `Amazon RDS`。

在此练习中，你将在多可用区配置创建一个 `Amazon Relational Database Service (Amazon RDS)` `MySQL` 数据库并模拟故障转移。

- 1. 登录 `AWS` 管理控制台，导航到 `Amazon RDS` 控制台。
- 2. 启动一个新的 `RDS` 实例，选择 `MySQL` 作为数据库类型并选择 `Production MySQL Multi-AZ Deployment`（生产环境 `MySQL` 多可用区部署）。
- 3. 在 `Instances Specifications`（实例规格）仪表板中，将存储类型更改为 `General Purpose SSD`（通用 `SSD`）。将分配的存储更改为 100 GB。
- 4. 在 `Settings`（设置）中，`DB Instance Identifier`（数据库实例标识符）= `certbook`，`master username`（主用户名）= `admin`，`password` = `password`。在生产环境中使用复杂的名称和密码。
- 5. 创建名为 `certbookdb` 的新安全组，`database name`（数据库名称）= `certbookdb`。所有设置保持默认。
- 6. 启动 `DB` 实例。（此步骤需要几分钟才能完成，请休息一下。）
- 7. 要模拟故障转移，选择你的 `certbook` `Amazon RDS` 实例并重启它。
- 8. 确认重启。
- 9. 导航到 `Details`（详细信息）选项卡（带有放大镜的小图标）。
- 10. 记下你的 `Availability Zone`（可用区），再次重启，然后注意你的 `Availability Zone`。
- 11. 现在让我们为 `certbookdb` 创建一个读取副本（`Read Replica`）。
- 12. 选择 `Actions`（操作），然后选择 `Create Read Replica Instance`（创建读取副本实例）。
- 13. 输入 `certbookdb-rr` 作为 `DN` 标识符，设置保持默认值。
- 14. 回到 `Details`（详细信息）页面，你将看到你的读取副本。

好了。你创建了一个带有读取副本的高可用 `Amazon RDS` `MySQL` 数据库。你还模拟了故障转移。

## 复习题

1. 你正寻求使用 `Amazon Notification Service (SNS)` 来发送通知。`SNS` 支持哪些协议？（多选）

   - A. `HTTP`
   - B. `SQL`
   - C. 电子邮件
   - D. `SQS`

2. 设置 `SNS` 的第一步是什么？

   - A. 创建主题
   - B. 订阅到
   - C. 发布到主题
   - D. 定义资源名称 (`ARN`)

3. 你担心连接性。你可以向管理层建议什么？

   - A. 部署到
   - B. 只要使用两个 `SNS` 是冗余的
   - C. 创建 `VPC`
   - D. 创建 `Amazon VPC`

4. 为了确保发生故障时流量将路由到，你必须做什么？

   - A. 主备模式
   - B. 手动配置你的流量到
   - C. 打开工单
   - D. 打开工单

5. 所有者担心存储 的可用性。你可以做什么来确保更高水平的可用性？

   - A. 无需。`S3` 设计时考虑了持久性。
   - B. 启用存储的版本控制
   - C. 在另一个区域创建 `Amazon S3` 桶并启用跨区域复制到
   - D. 在另一个区域创建桶

6. 你与应用程序开发团队合作创建了一个 `Simple Queue Service (SQS)` 标准队列。你的开发者抱怨消息被处理了多次。你可以做什么来限制这种行为？

   - A. 让开发者使应用程序幂等
   - B. 使用先入先出（`FIFO`）队列并让开发者指向
   - C. 增加队列的可见性超时
   - D. 调整 `Amazon` 实例的大小

7. 你在 `VPC` 中有一个应用程序测试版本。测试应用程序使用 `Relational Database Service (RDS)` 作为数据库。如何让 `Amazon RDS` 高可用？

   - A. 在一个可用区（`AZ`）部署 `Amazon RDS`，并在另一个可用区部署读取副本。
   - B. 以多可用区模型部署 `Amazon RDS`
   - C. 使用 `DynamoDB`，因为它是一个区域服务
   - D. 在另一个区域部署读取副本

8. 你正在管理一个部署在 `AWS` 上的多区域应用程序。你目前使用自己的 `DNS`。`Amazon Route 53` 支持哪些类型的故障转移？（三选）

   - A. 主主故障转移
   - B. 主主备故障转移
   - C. 基于延迟的故障转移
   - D. 权重轮询 (`WRR`) 故障转移
   - E. 主备故障转移

9. `Amazon Route 53` 支持以下类型的健康检查。（多选）

   - A. 特定 `Amazon` 虚拟有云 (`VPC`) 的健康状况
   - B. 指定资源（例如 `Web` 服务器）的健康状况
   - C. `Amazon CloudWatch` 告器的状态
   - D. 其他健康检查的状态

10. 如何让你的硬件 `VPN` 冗余？

    - A. 在 `AWS` 上部署你自己的软件 `VPN` 解决方案，确保软件版 `VPN` 部署在两个独立的可用区。关掉硬件 `VPN`。
    - B. 部署两个客户网关。配置客户网关以利用硬件 `VPN` 提供的两个隧道。
