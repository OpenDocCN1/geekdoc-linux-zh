
当`AWS CloudTrail`将新日志文件发布到`Amazon S3`存储桶时，可以通知。您可以使用`Amazon SNS`管理通知。

通知是可选的。要启用通知，请配置`AWS CloudTrail`在每次发送新日志文件时将信息发送到`Amazon SNS`主题。要接收这些通知，请订阅该主题。要通过程序处理通知，请将`Amazon SQS`队列订阅到该主题。

## 控制`AWS CloudTrail`的用户权限

`AWS CloudTrail`与`IAM`集成，`IAM`控制对`AWS CloudTrail`以及`AWS CloudTrail`需要的其他`AWS`资源的访问，包括`Amazon S3`存储桶和`Amazon SNS`主题。使用`IAM`控制哪些`AWS`用户可以创建、配置或删除`CloudTrail`跟踪、启动和停止记录，以及访问包含日志信息的存储桶。

## 授予`AWS CloudTrail`管理权限

要管理`AWS CloudTrail`跟踪，请授予`IAM`用户显式权限以执行与`AWS CloudTrail`任务的操作。在许多场景下，可以使用包含预定义权限的`AWS`托管组来实现这一点。典型方法是创建一个具有相应权限的`IAM`组，并将单个`IAM`用户添加到该组中。例如，您可以为对`AWS CloudTrail`操作具有完全访问权限的用户创建一个`IAM`组，并为应该能够查看跟踪信息但不能创建或更改跟踪的用户创建另一个组。

以下是适用于`AWS CloudTrail`的`AWS`托管策略：

- `AWSCloudTrailFullAccess`: 此策略赋予用户对`AWS CloudTrail`操作的完全访问权限，以及管理`Amazon S3`存储桶、`Amazon CloudWatch Logs`日志组和用于跟踪的`Amazon SNS`主题的权限。
- `AWSCloudTrailReadOnlyAccess`: 此策略允许组中的用户查看跟踪和存储桶。

## 日志管理和数据事件

在创建跟踪时，该跟踪会记录您的账户的只读和只写管理事件。如果需要，可以使用该跟踪来指定该跟踪是否应该记录数据事件。数据事件是访问`Amazon S3`对象资源的对象级`API`操作，例如`getObject`、`DeleteObject`和`PutObject`。只有符合跟踪设置的事件才会投递到`Amazon S3`存储桶和`Amazon CloudWatch Logs`日志组。如果事件不符合跟踪设置，则跟踪不会记录该事件。

## 用于`AWS CloudTrail`的`Amazon SNS`主题策略

要向`Amazon SNS`主题发送通知，当发生以下情况时，`AWS CloudTrail`必须对主题拥有所需的权限：

- 在`AWS CloudTrail`控制台中创建或更新跟踪时创建`Amazon SNS`主题。
- 使用`AWS CLI` `create-subscription`和`update-subscription`命令创建`Amazon SNS`主题。
- `AWS CloudTrail`自动在策略中添加以下字段：
    - 允许的`SID`
    - `AWS CloudTrail`的服务主体名称
    - `Amazon SNS`主题，包括区域、账户`ID`和主题名称

以下策略允许`AWS CloudTrail`从支持的区域发送有关日志文件交付的通知：

### `Amazon SNS`主题策略

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AWSCloudTrailSNSPolicy201311101",
      "Effect": "Allow",
      "Principal": {"Service": "cloudtrail.amazonaws.com"},
      "Action": "SNS:Publish",
      "Resource": "arn:aws:sns:Region:STopicOwnerAccountID:STopicName"
    }
  ]
}
```

## `AWS Config`

`AWS Config`是一种托管服务，提供`AWS`资源清单、配置历史和配置更改通知，以实现安全和治理。`AWS Config`可以发现现有的`AWS`资源，导出带有所有配置详细的`AWS`资源完整清单，并确定资源在任何时间点的配置情况。这些功能实现了合规审计、安全分析、资源更改跟踪和故障排除。

`AWS Config`能够轻松跟踪资源配置，无需预先投资或维护数据收集代理，或维护大型数据库。启用`AWS Config`后，可以查看与`AWS`资源相关的所有配置属性的持续更新详情。可以配置`Amazon SNS`提供每次配置更改的通知。

`AWS Config`提供`AWS`账户中`AWS`资源的配置详细视图。这包括资源之间如何关联以及它们是如何配置的。资源是`AWS`中的实体，例如`EC2`实例、`EBS`卷、安全组或`Amazon VPC`。通过`AWS Config`，您可以执行以下操作：

- 评估资源配置是否符合预期设置。
- 获取`AWS`资源当前配置的快照。
- 检索一个或多个资源的历史配置。
- 每当资源被创建、修改或删除时接收通知。
- 查看资源之间的关系，例如使用特定安全组的资源。

## 使用`AWS Config`的方法

在`AWS`上运行应用程序时，必须集体创建和管理资源。随着应用程序需求的增长，跟踪资源添加的需求也随之增长。`AWS Config`设计用于在以下场景下监督应用程序资源。

### 资源管理

为了对资源配置进行更好的治理并检测资源配置错误，需要对存在哪些资源以及这些资源在任何时间是如何配置的进行细粒度的可见化。使用`AWS Config`在资源被创建、修改或删除时自动发送通知。无需通过对每个单独资源进行轮询来监控这些内容。

使用`AWS Config`规则评估`AWS`资源的配置设置。当`AWS Config`检测到资源违反了已建立规则之一的条件时，`AWS Config`将该资源标记为非合规并发送通知。`AWS Config`在资源创建、更改或删除时进行持续评估。

### 审计与合规性

某些数据需要频繁审计以确保符合内部策略和最佳实践。为了证明合规性，需要访问资源的历史配置。这些信息由`AWS Config`提供。

### 配置更改的管理与故障排除

当使用相互依赖的多个资源时，一个资源的配置更改可能会对相关资源产生意外后果。通过`AWS Config`，可以查看一个资源与其他资源的关系，并评估提议更改的影响。

`AWS Config`提供的资源历史配置可以通过提供问题资源的最后良好配置的访问来协助故障排除。

### 安全分析

要分析潜在的安全脆弱性，需要有关`AWS`资源配置的详细信息。这些信息可能包括授予用户的`IAM`权限，或控制资源访问的`Amazon EC2`安全组规则。

使用`AWS Config`查看在`AWS Config`记录的任何时间分配给`IAM`用户或角色的`IAM`策略。这些信息可以帮助确定用户在特定时间所拥有的权限。

使用`AWS Config`查看`Amazon EC2`安全组的配置以及在特定时间开放的端口规则。这些信息可以帮助确定安全组是否阻止了进入特定端口的`TCP`流量。

## `AWS Config`规则

`AWS Config`规则代表了资源的预期配置，并根据`AWS Config`记录的相关资源的配置更改进行评估。针对资源配置的规则评估结果将显示在仪表板上。通过`AWS Config`，客户可以从配置的角度评估其整体合规性和风险状态，查看随时间演变化的合规性趋势，并确定是哪种配置更改导致资源偏离了规则限制。

规则代表资源的配置项（`CI`）属性值，通过将这些属性值与`AWS Config`记录的`CI`进行比较来进行评估。规则分为两种类型：`AWS`托管规则和客户托管的规则。

## `AWS`托管规则

`AWS`托管规则由`AWS`预构建并管理。选择要启用的规则，然后提供一些配置参数即可开始。

## 客户托管的规则

可以开发自定义规则并将其添加到`AWS Config`中。将每个自定义规则与`Lambda`函数关联。此`Lambda`函数包含评估资源是否符合规则的逻辑。

将此函数与规则关联，规则将调用该函数，然后评估资源是否符合规则，并将评估结果发送到`AWS Config`。

> 使用`AWS Config`
>
> 通过使用`AWS Config`规则，客户可以从配置的角度评估其整体合规性和风险状态，查看随时间演变化的合规性趋势，并确定是哪种配置更改导致资源偏离了规则限制。

默认情况下，客户可以在`AWS`账户中最多创建`50`条`AWS Config`规则。这是一个软限制，可以通过联系`AWS`支持来进行增加。

## 规则是如何评估的

任何规则都可以更改触发型规则或周期性规则。

更改触发型规则在`AWS Config`记录任何指定资源的配置更改时执行。此外，必须指定以下内容之一：

- `Tag Key`：键:值 意味着为具有指定标签键:值的资源记录的任何配置更改将触发规则的评估。
- `Resource Type(s)`：为指定资源类型内的任何资源记录的任何配置更改将触发规则的评估。
- `Resource ID`：为资源类型和资源`ID`指定的资源记录的任何更改将触发规则的评估。

# 第 9 章 ■ 监控指标

周期性规则按指定的频率触发。可选频率为`1`小时、`3`小时、`6`小时、`12`小时或`24`小时。周期性规则拥有适用于该规则的所有资源当前`CI`的完整快照。

## 配置项（`Configuration Items`）

`CI`是资源在特定时间点的配置。一个`CI`由五个部分组成：

- 跨越不同类型资源的基本信息（例如`ARN`、标签）
- 资源特有的配置数据（例如`Amazon EC2`实例类型）
- 与其他资源的关系映射（例如，`Amazon EC2::volume-6886ff28` “挂载到实例” `Amazon EC2 instance-i-2460abc`）
- 与此状态相关的`AWS CloudTrail`事件`ID`
- 标识`CI`信息的元数据，例如`CI`的版本及其捕获时间

## 规则评估

规则评估决定了规则在特定时间点是否符合资源。它是针对资源配置进行规则评估的结果。`AWS Config`规则将捕获并存储每次评估的结果。结果将包含资源、规则、评估时间以及指向导致不合规的`CI`的链接。

## 规则合规性

如果资源符合所有适用于它的规则，则为合规。否则，则为不合规。同样，如果规则可用的所有资源都符合该规则，则资源为合规。否则，则为不合规。

在某些情况下（例如规则拥有的权限不足），评估可能产生“数据不足”状态。该状态被排除在资源或规则的合规状态判断之外。

## `AWS Config`和`AWS CloudTrail`

`AWS CloudTrail`记录账户上的`API`活动以及对这些活动信息的访问。你可以使用`AWS CloudTrail`获取`API`操作的完整详细信息，例如调用者身份、`API`调用时间、请求参数以及`AWS`云服务返回的响应元素。

`AWS Config`将`AWS`资源的特定时间点配置细节记录为`CI`。你可以使用`AWS Config`在任何时间点回答“我的`AWS`资源在某时候长什么样？”。你可以使用`AWS CloudTrail`回答“谁调用了`API`修改了此资源？”。

在实践中，你可以使用`AWS Config`控制台检测过去是否错误配置了安全组。结合集成的`AWS CloudTrail`信息，你可以找到错误配置安全组的用户并了解其发生的时间。

每个自定义规则都是一个`AWS Lambda`函数。当调用该函数来评估资源时，它将获得资源的`CI`。函数可以检查该项目并根据需要调用其他`AWS API`函数。在`AWS Lambda`函数对合规性做出裁决后，它会调用`PutEvaluations`函数来记录该决策。

## 价格

使用`AWS Config`的客户根据`AWS`账户中支持的资源记录的`CI`数量收费，且仅在记录`CI`时收取一次费用。保留`CI`不需要额外费用或任何预付。用户可以随时停止记录`CI`并继续访问之前记录的`CI`。每个`CI`的费用汇总到每月账单中。

如果你使用`AWS Config`规则，费用基于该月内活跃的`AWS Config`规则。当使用`AWS`资源调用规则时，结果将记录为一次评估。如果规则在当月内有一个或多次评估，则该规则为激活状态。

## 总结

`AWS Config`是一项允许客户评估、审计和评价其`AWS`资源配置的服务。通过`AWS Config`，可以查看`AWS`资源内部及其之间的更改，深入研究资源历史，并确定与预期配置的整体合规性。

`CloudWatch`提供应用程序性能和运行状况的系统级可视化。`CloudWatch`告警根据自定义阈值发送通知。使用`CloudWatch`监控`AWS`资源并确定利用率低的实例。

## 考试要点

熟悉`Amazon CloudWatch`。`Amazon CloudWatch`是一种针对`AWS`云资源以及你在`AWS`上运行的应用程序的监控服务。你可以使用`Amazon CloudWatch`来收集和跟踪指标、收集和监控日志文件，并设置告警。

`Amazon CloudWatch`可以监控`AWS`资源，例如`Amazon EC2`实例、`Amazon DynamoDB`表和`Amazon RDS`实例，以及由应用程序生成的自定义指标和应用程序生成的任何日志文件。

你可以使用`Amazon CloudWatch`获取资源利用率、应用程序性能和运行健康状况的全局可见性。你可以利用这些见解做出反应，并保持你的应用程序顺利运行。

`Amazon CloudWatch Events`有三个组件：事件（`Events`）、规则（`Rules`）和目标（`Targets`）。事件表示`AWS`环境的变化。目标处理事件。规则匹配传入的事件将其路由到目标进行处理。

了解`Amazon CloudWatch Alarms`的功能。`Amazon CloudWatch Logs`允许你使用现有的系统、应用程序和自定义日志文件对系统进行监控和故障。

通过`Amazon CloudWatch Logs`，近实时监控特定短语、值或模式的日志。日志数据可以在极高持久性、低成本的存储中无限期存储和访问，而不会填满硬盘。

学会创建监控计划。创建监控计划涉及回答基本问题：你的监控目标是什么？你将监控哪些资源？多久监控一次这些资源？你将使用哪些监控工具？谁来执行监控任务？出现问题时应该通知谁？

了解并理解自定义指标。你现在可以将业务和应用程序指标存储在`Amazon CloudWatch`中。你可以根据这些指标查看图表、指标并启动自动化操作，就像你对`Amazon CloudWatch`为你的`AWS`资源存储的指标一样。

虚拟机监控程序（`Hypervisor`）以上指标的可见性需要代理程序（`agent`）。`Amazon CloudWatch`可以告诉你虚拟机程序层面的`CPU`和`RAM`利用率，但它不知道哪些特定任务或进程影响了性能。`CloudWatch`可以看到`I/O`，但看不到磁盘使用情况。这需要代理程序。

熟悉`Amazon CloudWatch Alarm`的工作原理。你可以创建一个监控单个指标的`CloudWatch`告警。告警根据指标在多个周期内相对于阈值的值执行一个或多个操作。该操作可以是`Amazon EC2`实例、自动伸缩操作，或发送到`Amazon SNS`主题的通知。

了解`Amazon CloudWatch Alarm`的三种状态。这些是`OK`、`ALARM`和`INSUFFICIENT_DATA`。如果告警处于`OK`状态，说明受监控的指标在你定义的接受范围内。如果告警处于`ALARM`状态，说明指标已超过阈值。如果数据缺失或不完整，则处于`INSUFFICIENT_DATA`状态。

监控有两个级别：基础和详细。`Amazon EC2`的基础监控默认每五分钟将`CPU`负载、`I/O`和网络`I/O`指标发送到`Amazon CloudWatch`。默认每分钟将详细指标数据发送到`CloudWatch`。某些服务（如`Amazon RDS`）默认开启详细监控。

`Amazon CloudWatch`执行两种类型的`Amazon EC2`状态检查：系统（`System`）和实例（`Instance`）。系统状态检查监控你使用的`AWS`系统以确保它们运行正常。这些检查会检测你的实例中需要`AWS`参与才能修复的问题。实例状态检查监控你单个实例的软件和配置。这些检查会检测需要你参与修复的问题。

熟悉一些用于监控的常用指标。有很多可用指标，但并非所有指标都会考试中测试。然而，某些会被测试，了解常用的指标是一个好主意：`QueueLength`（队列长度）、`DatabaseConnections`（数据库连接）、`DiskQueueDepth`（磁盘队列深度）、`FreeStorageSpace`（可用存储空间）、`ReplicaLag`（复制延迟）、`ReadIOPS`（读取`IOPS`）、`WriteIOPS`（写入`IOPS`）、`Latency`（延迟）、`SurgeQueueLength`（激增队列长度）和`SpilloverCount`（溢出计数）。

如何知道为`Amazon RDS`设置`Amazon CloudWatch`事件订阅。`Amazon RDS`使用`Amazon`通知服务（`Amazon SNS`）在`Amazon RDS`事件发生时提供通知。这些可以是`Amazon SNS`支持的`AWS`区域的任何通知，电子邮件、短信或发送到`HTTP`端点的调用。详情可以在此处找到：`http://docs.aws.amazon.com/AmazonRDS/Latest/UserGuide/Events.html`

`Amazon ElasticCache`有两个引擎：`Redis`和`Memcached`。`Memcached`是多线程的，`Redis`是单线程的。

了解`EBS`卷状态检查。`Degraded`（降级）和`Severely Degraded`（严重下降）意味着`EBS`卷状态检查处于警告状态且存在`I/O`。`Stalled`（阻塞）或`Not Available`（不可用）意味着`EBS`卷处于受损状态且没有`I/O`。

学习指标`SurgeQueueLength`和`SpilloverCount`。当超过`SurgeQueueLength`限制时，会发生溢出。请求被丢弃且不通知用户。客户体验受到负面影响。

# 学习技巧
