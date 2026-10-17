
`ReadIOPS`: 此指标是每秒平均磁盘 I/O 操作次数。

`WriteIOPS`: 此指标是每秒平均磁盘 I/O 操作次数。

`ReadLatency`: 此指标以秒为单位，是每次磁盘读取 I/O 操作所需的平均时间。

`WriteLatency`: 此指标以秒为单位，是每次磁盘写入 I/O 操作所需的平均时间。

# AWS 弹性负载均衡器 (ELB)

只有当有请求通过负载均衡器时，AWS ELB 才会向 Amazon CloudWatch 报告指标。当有请求通过负载均衡器时，弹性负载均衡每隔 60 秒测量并发送一次指标。负载均衡器中报告给 Amazon CloudWatch 的指标包含以下内容：

- `BackendErrors`

- `HealthyHostCount`

- `UnhealthyHostCount`

- `RequestCount`

- `Latency`

- `HTTPCode_2XX`

- `HTTPCode_3XX`

- `HTTPCode_4XX`

- `HTTPCode_5XX`

- `HTTPCode_ELB_4XX`

- `HTTPCode_ELB_5XX`

- `SpillOver`

- `SurgeQueueLength`

`BackendErrors`: 此指标是负载均衡器与注册实例之间未成功建立的连接数。

`HealthyHostCount`: 此指标是注册负载均衡器的健康实例数。如果启用了跨区域负载均衡，则 `LoadBalancer` 维度在所有可用区计算。否则，按可用区计算。

`UnhealthyHostCount`: 此指标是注册负载均衡器的不健康实例数。实例在超过健康检查阈值后被视为不健康；满足健康检查阈值后被视为健康。

`RequestCount`: 此指标是在特定间隔内（一分钟或五分钟）完成或建立的请求数。

- HTTP listener: 来自注册实例的 HTTP 错误响应

- TCP listener: 到注册实例的连接数

- `Latency`: 此指标代表从向实例发送请求到收到回复之间持续的时间（秒）

  - HTTP listener: 从负载均衡器向注册实例发送请求到响应头开始的总秒数

  - TCP listener: 负载均衡器向注册实例建立连接所需的总秒数

`HTTPCode_Backend_2XX`: 此指标是注册实例生成的 HTTP 2XX 响应代码数。2XX 状态表示操作已完全接收、理解并接受。此计数不包括负载均衡器生成的任何响应代码。

`HTTPCode_Backend_3XX`: 此指标是注册实例生成的 HTTP 3XX 响应代码数。3XX 状态表示重定向，需要后续操作来完成请求。

`HTTPCode_Backend_4XX`: 此指标是注册实例生成的 HTTP 4XX 响应代码数。4XX 状态表示客户端错误。请求包含语法错误或无法执行。

`HTTPCode_Backend_5XX`: 此指标是注册实例生成的 HTTP 5XX 响应代码数。5XX 状态表示服务器错误。服务器未能处理看似有效的请求。

`HTTPCode_ELB_4XX`: 此指标是负载均衡器生成的 HTTP 4XX 客户端错误代码数。当请求格式错误或不完整时产生此类错误。这由 ELB 生成。

`HTTPCode_ELB_5XX`: 此指标是负载均衡器生成的 HTTP 5XX 服务器错误代码数。此计数不包括注册实例生成的任何响应代码。

# Amazon CloudWatch Events

如果负载均衡器上没有注册健康的实例，或者请求速率超过了实例（溢出）或负载均衡器的容量，则会报告该指标。此错误由 ELB 生成。

`SpilloverCount` 该指标是由于激增队列满拒绝的请求总数。

- **HTTP 监听器** 负载均衡器返回 HTTP 503 错误代码。

- **TCP 监听器** 负载均衡器关闭连接。

`SurgeQueueLength` 该指标是等待路由的请求总数。如果负载均衡器无法与健康实例建立连接以路由请求，则会将请求置于队列。

队列的最大大小为 1,024。当队列满时，额外的请求将被拒绝。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_430_0.png)

- 当后端实例处理应用程序请求的速度赶不上其进入的速度时，激增队列将开始增加。这是由于许多问题导致的，其中主要是后端实例面临的容量限制。

- 通过扩展实例来提高计算能力，以确保 `SurgeQueueLength` 永远不超过最大队列容量。

- 溢出是激增队列长度增加的直接结果。当 ELB 达到最大队列容量时，它将开始丢弃新请求。当请求被丢弃时，终端用户不会收到通知。

- 监控 `SurgeQueueLength` 和 `SpilloverCount`，以便发生可能的高溢出计数时获得报警，这会导致请求丢失和客户体验不良。

# Amazon CloudWatch Events

Amazon CloudWatch Events 提供近实时的系统事件流，描述 AWS 资源的更改。使用相对简单的规则，可以将事件路由到一个或多个目标进行处理。

将 Amazon CloudWatch Events 视为 AWS 环境的中枢神经系统。它连接到支持的 AWS 云服务，并在操作变化发生时感知这些变化。然后，在规则的驱动下，它响应变化发送消息并激活函数。

## 事件

事件是 AWS 环境中的变化，可以通过四种不同的方式生成：

- 它们产生于 AWS 内部，当资源状态变化时，例如 Amazon EC2 实例状态从等待中（pending）变为运行（running）。

- API 调用和控制台登录可以生成事件并通过 AWS CloudTrail 将其传递给 Amazon CloudWatch Events。

- 可以运行代码来生成应用程序级事件并将其发布到 Amazon CloudWatch Events 进行处理。

- 它们可以按计划发布，提供周期性或 Cron 风格的调度选项。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_431_0.png)

这是一个处于等待（pending）状态的 Amazon EC2 实例状态变更通知事件。

```json
{
  "id":"7bf73129-1428-4cd3-a780-95db273d16002",
  "detail-type":"EC2 Instance State-change Notification",
  "source":"aws.ec2",
  "account":"8675309719",
  "time":"2015-11-11T21:29:54Z",
  "region":"us-east-1",
  "resources":[
    "arn:aws:ec2:us-east-1:8675309719:instance/i-dec12221"
  ],
  "detail":{
    "instance-id":"i-dec12221",
    "state":"pending"
  }
}
```

记住，事件表示 AWS 环境发生了变化。当 AWS 资源的状态发生变化时，可以生成事件。AWS CloudTrail 发布 API 用的事件。可以创建自定义的应用程序级事件并将其发布到 Amazon CloudWatch Events。计划事件按周期性生成。

# Amazon CloudWatch Events

当 Amazon EC2 实例的状态从等待（pending）变为运行（running）时，Amazon EC2 会生成一个事件。在启动或终止实例时会触发 Auto Scaling 事件。

- 当进行 API 调用时，AWS CloudTrail 会发布事件。

- 生成自定义的应用程序级事件并将其发布到 Amazon CloudWatch Events。

- 可以按周期性生成计划事件。

Amazon CloudWatch Events 可用于使用 cron 或速率表达式调度在特定时间触发的操作。所有计划事件都使用协调标准时间 (UTC) 时区，最小周期为一分钟。

## 规则

规则匹配传入的事件并将其路由到目标进行处理。单个规则可以路由到多个目标并被并行处理。这允许组织的不同部分查找并处理它们感兴趣的事件。

规则可以通过仅传递某些部分或通过常量覆盖，来定制化发送到目标的 JSON。

> 由于发送到多个目标的规则是并行处理的，因此它们的顺序会丢失。

## 目标

目标处理从 Amazon CloudWatch Events 发送给它的 JSON 格式数据。Amazon CloudWatch Events 将系统事件实时流传递给一个或多个目标函数或流。这些目标包括：

- Amazon EC2 实例

- AWS Lambda 函数

- Amazon Kinesis 传输

- Amazon ECS 任务

- Amazon Step Functions 状态机

- Amazon SNS 主题

- Amazon SQS 队列

- 内置目标

# 指标和维度

Amazon CloudWatch Events 每分钟向 Amazon CloudWatch 发送指标。`AWS/CloudWatch` 命名空间包含表 9 所示的指标。

## 9.5 Amazon CloudWatch Metrics

| 指标 | 描述 |
| --- | --- |
| `Invocations` | 测量响应规则时被调用的次数。Amazon CloudWatch Events 仅在指标具有非零值时发送此指标。这包括重试或失败。<br>- 有效维度: `RuleName`<br>- 单位：计数 |
| `FailedInvocations` | 测量失败的调用次数。这不包括重试或成功的调用。<br>- 有效维度: `RuleName`<br>- 单位：计数 |
| `TriggeredRules` | 测量匹配任何事件而触发的规则数量。<br>- 有效维度: `RuleName`<br>- 单位：计数 |
| `MatchedEvents` | 测量匹配任何规则的事件数量。<br>- 有效维度：无<br>- 单位：计数 |
| `ThrottledRules` | 测量被限流的触发规则数量。<br>- 有效维度: `RuleName`<br>- 单位：计数 |

Amazon CloudWatch Events 指标使用单一维度：`RuleName`。正如名称所示，它通过规则名称过滤。

# Amazon CloudWatch Logs

Amazon CloudWatch Logs 可用于监控、存储和访问来自 Amazon EC2 实例、CloudTrail 以及本地数据中心服务器的日志文件。然后可以检索并报告相关日志。Amazon CloudWatch Logs 可以监控应用程序日志、系统日志、服务器日志和自定义日志。通过对这些指标设置报警可以生成通知。

Amazon CloudWatch Logs 由几个部分组成：

- 日志代理

- 日志事件

- 日志流

- 日志组

- 指标过滤器

- 留存策略

**日志代理** 日志代理将日志导向 Amazon CloudWatch。由于共享责任模型，AWS 对虚拟机没有有效的可见性，因此必须由代理发送数据到 Amazon CloudWatch。

**日志事件** 日志事件是操作系统或应用程序报告到日志文件的活动，并带有时间戳。事件仅支持文本格式。

日志事件包含两个属性：事件发生的时间戳和原始日志消息。

默认情况下，任何非空白字符开始的行都会关闭上一个日志消息并开始一个新的日志消息。

**日志流** 日志流是由单个源（例如 Web 服务器）报告的日志事件组。

**日志组** 是多个资源的日志流组，例如管理相同内容的 Web 服务器组。

**留存策略** 和 **指标过滤器** 设置在日志组上，而不是日志流上。

**指标过滤器** 指标过滤器告诉 Amazon CloudWatch 如何从摄取的日志事件中提取指标观测值并转换为 Amazon CloudWatch 指标。

例如，通过一个名为 `404_Error` 的指标过滤器，可以过滤日志以查找 `404` 访问错误。可以为这些 `404` 错误创建报警。

**留存策略** 留存策略决定了事件在 Amazon CloudWatch Logs 中保留多长时间。策略分配给日志组并应用于组中的所有日志流。

留存时间可以从 1 天到 10 年不等。你也可以选择日志永不过期。

# 归档数据

所有上传到 Amazon CloudWatch 的日志事件都会保留。可以指定保留时长。数据会被压缩、放入存档并存储。存储归档数据会产生费用。

> Amazon CloudWatch Logs 可以摄来自 AWS 外部源的日志。这意味着来自本地数据中心的日志数据可以发送到 Amazon CloudWatch Logs 进行报告。

# 日志监控

使用 Amazon CloudWatch Logs 通过日志数据监控应用程序和系统。Amazon CloudWatch Logs 可以跟踪应用程序日志中发生的错误，并在错误率超过阈值时发送通知。由于 Amazon CloudWatch 使用日志数据进行监控，因此不需要更改代码。如果未提供 `datetime_format`，则对每个日志事件都使用当前时间。如果提供的 `datetime_format` 对于日志消息无效，则使用上一个成功解析时间戳的事件的时间戳。如果没有之前的日志，则使用当前时间。当日志事件回退到当前时间或上一个日志事件的时间时，系统会记录一条警告消息。

> 时间戳用于检索日志事件和生成指标。如果指定了错误的格式，日志事件可能无法检索并生成不准确的指标。

# 代理

由于 AWS 对虚拟化程序（Hypervisor）没有可见性，因此需要代理将日志数据发布到 Amazon CloudWatch Logs。Linux 和 Windows 都有代理。代理包含以下组件：

- 用于 AWS CLI 的插件，将日志数据推送到 Amazon CloudWatch Logs

- 运行 Amazon CloudWatch Logs `aws log push` 命令的脚本，将数据发送到 Amazon CloudWatch Logs

- 确保守护始终运行的 cron 作业

# Linux 版 Amazon CloudWatch Logs Agent

Amazon CloudWatch Logs 代理需要 Python 2.6、2.7、3.0 或 3.3 以及任意版本的 Linux：

- Amazon Linux 版本 2014.03.02 或更高

- Ubuntu Server 版本 12.04、14.04 或 16.04

- CentOS 版本 6、6.3、6.4、6.5 或 7.0

- Red Hat Enterprise Linux (RHEL) 版本 6.5 或 7.0

- Debian 8.0

# Amazon CloudWatch Logs：代理与 IAM

Amazon CloudWatch Logs 代理需要 `CreateLogGroup`、`CreateLogStream`、`DescribeLogStreams` 和 `PutLogEvents` 操作。

> 在最新版本的代理中，不再需要 `DescribeLogStreams`。

以下是用于代理的示例 IAM 策略：

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents",
        "logs:DescribeLogStreams"
      ],
      "Resource": [
        "arn:aws:logs:*:*:*"
      ]
    }
  ]
}
```

从 Amazon Linux 机器镜像 (AMI) 2014.09 开始，Amazon CloudWatch Logs 代理可以作为 Red Hat 包管理器 (RPM) 安装，通过 `awslogs` 包提供。较早版本的 Amazon Linux 可以通过 `sudo yum update -y` 命令更新实例来访问 `awslogs` 包。通过 RPM 安装 `awslogs` 包而不是使用 Amazon CloudWatch Logs 安装程序，实例可以接收来自 AWS 的定期包更新和补丁，而无需手动重新安装 Amazon CloudWatch Logs 代理。

如果使用 Python 脚本安装代理，请勿使用 RPM 安装方法更新 Amazon CloudWatch Logs 代理。这样做可能会导致配置问题，阻止 Amazon CloudWatch Logs 代理将日志发送到 Amazon CloudWatch。

# Windows 版 Amazon CloudWatch Logs Agents

从 EC2Config 版本 2.2.5 开始，可以将系统中的所有 Windows Server 日志导出到安全日志、应用程序日志和 Internet 信息服务 (IIS) 日志并发送到 Amazon CloudWatch Logs。EC2Config 版本 2.2.10 或更高版本增加了将任何事件日志数据、Windows 事件跟踪 (ETW) 数据或文本日志文件导出到 Amazon CloudWatch Logs 的能力。Windows 性能计数器数据也可以导出到 Amazon CloudWatch。EC2 实例使用代理将日志数据发送到 Amazon CloudWatch。对于 Microsoft Windows，代理是 EC2Config 服务或系统管理器 (SSM) 代理。默认情况下，EC2Config 服务包含在 AWS Server 2003-2012 中。EC2Config 在实例启动时启动并在执行任务后停止。EC2Config 还可以按需要执行任务。这些任务中某些是自动启用的，另一些必须手动启用。Windows Server 2016 AMI 不使用 EC2Config。相反，这些 AMI 使用 EC2Launch PowerShell 脚本。表 9.6 显示了不同 Windows 上的可用代理类型。
