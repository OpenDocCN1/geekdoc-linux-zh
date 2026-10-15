
你通过上传源码包在 AWS Elastic Beanstalk 上部署新应用程序。该源码包可以是 `ZIP` 或 `WAR` 文件（你可以在 `ZIP` 文件中包含多个 `WAR` 文件）。该源码包的大小不能超过 512 MB。

### 管理

AWS Elastic Beanstalk 根据定义是高可用的。它会创建多个计算实例，将这些计算实例位于两个可用区，并创建一个负载均衡器（经典弹性负载均衡器）以将计算负载分散到多个实例上。

你可以配置自动扩展（`Auto Scaling`）来建立最小实例数、最大实例数以及触发实例数量增加或减少的参数。这些触发器可以是基于时间的，也可以基于事件的。

当你进入 AWS Elastic Beanstalk 控制台时，它会显示该区域运行的所有环境，并按应用程序排序。你可以通过名称进一步钻取以查看环境、应用程序版本和保存的配置。对于应用程序、应用程序版本和环境的数量存在限制。

在使用 `Amazon EC2` 时，你负责通过 AWS Elastic Beanstalk 对客户端操作系统和应用程序进行补丁和更新。

# 你的 AWS Elastic Beanstalk 环境更改

建议在更改 AWS Elastic Beanstalk 环境和配置时，使用 AWS Elastic Beanstalk 控制台和 `CLI`。虽然可以使用其他服务控制台、`CLI` 命令或 `SDK` 修改你的 AWS Elastic Beanstalk 环境，但这些更改不会反映在 AWS Elastic Beanstalk 控制台中，且你将无法监控、更改或保存你的环境。当你尝试在不使用 AWS Elastic Beanstalk 控制台的情况下终止环境时，也会导致问题。

# 监控你的 AWS Elastic Beanstalk 环境

你可以使用基础健康报告或增强健康报告和监控系统来监控环境的健康状况。基础健康报告提供整体状态（通过环境的颜色键）。它不会向 `Amazon CloudWatch` 发布任何指标。增强健康报告和监控不仅通过颜色键提供状态，还提供了一个有助于识别问题严重程度和原因的描述符。你还可以配置增强健康报告和监控将指标作为自定义指标发布到 `Amazon CloudWatch`。

你可以从单个实例检索日志文件，或将这些日志文件上传到 `Amazon S3` 桶进行永久存储。

# 安全

当你使用 AWS Elastic Beanstalk 创建环境时，会提示创建两个 `IAM` 角色：

`Service role`：用于 AWS Elastic Beanstalk 访问其他 AWS 服务。

`Instance profile`：应用于你环境中的实例，允许它们将日志上传到 `Amazon S3` 并执行其他任务。

除了这两个角色外，你还可以在 `IAM` 中创建策略并将其附加到用户、组和角色上。与 `Amazon EC2` 一样，在 AWS Elastic Beanstalk 中，你需要创建一个 `Amazon EC2` 密钥对来访问计算实例内部的客户端操作系统。访问将通过端口 22（用于 `SSH`）或端口 3389（用于 `RDP`）进行。

AWS Elastic Beanstalk 允许开发者部署高扩展性和高可用的 Web 基础设施，而无需了解或理解弹性负载均衡（`Elastic Load Balancing`）、自动扩展组或可用区等服务。

# AWS Lambda

AWS Lambda 是一种无服务器计算服务。它响应事件运行你的代码。AWS Lambda 会自动管理底层计算资源，无需你配置服务器。无需置备或管理服务器。

代码的执行（称为 AWS Lambda 函数）可以由你基础设施内部或外部的事件触发。AWS Lambda 是一个运行在多个可用区的区域性服务。这使得它具有高可用性和高可扩展性。由于代码是无状态的，它几乎是自动执行的，没有部署或配置延迟。

# 实现

AWS Lambda 的实现涉及以下步骤：

1. 配置 AWS Lambda 函数。
2. 创建部署包。
3. 上传部署包。
4. 创建调用类型。

允许编写代码的语言有 `Node.js`、`Java`、`Python` 和 `C#`。你选择的语言还决定了可以使用哪些工具编写代码。这些工具包括 AWS Lambda 控制台、`Visual Studio`、`.NET Core`、`Eclipse` 或你自己的环境。使用这些语言创建部署包。

一旦创建了部署包，你就将其上传以创建 AWS Lambda 函数。你可以使用的工具是 AWS Lambda 控制台、`CLI` 和 `AWS SDK`。

你编写的代码是所谓的 AWS Lambda 函数的一部分。AWS Lambda 函数的其他元素是：

- 内存
- 最大执行时间
- `IAM` 角色
- `Handler name`

你指定的内存量控制 `CPU` 性能。每个 AWS Lambda 函数的默认内存为 512 MB，但范围可以从 128 MB 到 1536 MB，每 64 MB 递增。

# AWS Lambda

由于你需要为运行 AWS Lambda 函数的资源付费，超时是为了防止 AWS Lambda 函数无限期运行。你可以选择 1 到 300 秒（5 分钟）之间的值。当达到超时时，AWS Lambda 函数将被终止。

`IAM` 角色控制特定 AWS Lambda 函数对资源的访问级别。当使用 AWS Lambda 访问其他资源时，这一点很重要。

`Handler` 指的是代码中 AWS Lambda 开始执行的方法。AWS Lambda 将触发调用的任何事件信息（调用类型的详细信息）作为参数传递给处理器。

当 Lambda 函数被调用时，AWS Lambda 根据你的配置启动容器。由于正在启动容器，第一次调用可能会有延迟。AWS Lambda 会在调用后维持一段时间容器以加快后续调用的响应速度。

# 如何调用 Lambda 函数

AWS Lambda 函数可以同步或异步调用。如果你使用 AWS 云服务调用 AWS Lambda，这些云服务将控制是同步还是异步调用。例如，如果 `Amazon S3` 调用 AWS Lambda 函数，`Amazon Cognito` 同步调用 Lambda 函数。AWS Lambda 通过以下方式调用：

- `Push event model`：某些事件源可以将事件发布到 AWS Lambda 并直接调用你的 AWS Lambda 函数。推送模型适用于 `Amazon S3`、`Amazon SNS`、`Amazon Cognito`、`Amazon Echo` 和用户应用程序，每个事件都会触发 Lambda 函数。
- `Pull event model`：某些事件源发布事件，但 AWS Lambda 必须轮询事件源并在事件发生时调用你的 AWS Lambda 函数。该模型适用于 AWS Lambda 使用流式事件源，例如 `Amazon Kinesis` 和 `Amazon DynamoDB Streams`。例如，AWS Lambda 轮询你的 `Kinesis` 流或 `Amazon DynamoDB` 流，并在检测到流中有新记录时调用你的 AWS Lambda。
- `Direct invocation model`：这种调用类型导致 AWS Lambda 同步执行函数并立即向调用应用程序返回响应。该调用类型适用于自定义应用程序。

> 编写 Lambda 代码的建议之一是确保代码是无状态的（即它不引用任何底层基础设施）。

### 管理

你可以通过 AWS Lambda 控制台或使用 `CLI` 测试你的 AWS Lambda 函数。`Amazon CloudWatch` 为 AWS Lambda 提供指标。这些指标包括但不限于以下内容：

- 调用次数
- 调用持续时间
- 请求数
- 每个请求的延迟
- 代码执行持续时间

`AWS CloudTrail` 会记录用于 AWS Lambda 函数的 `API` 调用。这为故障排除提供了另一个信息来源。AWS Lambda 函数在被调用时会执行。如果执行失败，将会进行额外的两次尝试。作为可选方案，你可以配置 AWS Lambda 将失败的负载发送到死信队列 (`DLQ`)。该 `DLQ` 可以以 `Amazon Simple Notification Service` (`AWS SNS`) 或 `Amazon Simple Queue Service` (`SQS`) 队列的形式存在。

# 安全

AWS Lambda 的底层基础设施是 `Amazon Linux AMI`。由于 AWS 负责维护这些基础设施（包括打补丁和升级），你无法登录这些计算实例，也无法自定义操作系统或语言运行时。

每个 AWS Lambda 函数都关联有一个角色（`role`）。该角色控制了你的特定的 AWS Lambda 函数可以访问哪些资源。因此，你需要向该角色授予必要的权限级别。

你使用 AWS Lambda 函数策略来管理权限。AWS Lambda 函数策略允许你通过事件（例如 `Amazon S3` 存储桶上的事件通知）来调用 AWS Lambda 函数。AWS Lambda 函数策略还用于在源事件位于包含 AWS Lambda 函数的 AWS 账户之外时调用 AWS Lambda 函数。

> 将 AWS Lambda 视为一种服务，它可以让你获取 `CPU` 周期，而无需亲自获取 `CPU`。

# Amazon Lightsail

Amazon Lightsail 设计旨在让你能够轻松地通过 AWS 启动和管理虚拟专用服务器 (`VPS`)。当你启动 Amazon Lightsail 实例时，你可以选择操作系统、开发者堆栈或应用程序，以及你想要运行的实例大小。Amazon Lightsail 实例带有 `SSD` 备份存储、公可的 `IP` 地址、`DNS` 管理和数据传输能力。

Amazon Lightsail 的设计旨在便于启动单机服务器。Amazon Lightsail 对开发者（包括专业人士和爱好者）特别有帮助，因为它让他们专注于开发，而不是花费在安装软件或框架上。

# 实现

你可以通过控制台或 `CLI` 访问 Amazon Lightsail。通过控制台访问可以通过 AWS 管理控制台进行，也可以通过独立的 Amazon Lightsail 控制台进行。

实现 Amazon Lightsail 涉及通过选择操作系统、应用程序或开发者堆栈来创建你的实例。

# 操作系统选择

Amazon Lightsail 的操作系统选择是 `Amazon Linux` 或 `Ubuntu`。

# 应用程序和开发者堆栈选择

以下是 Amazon Lightsail 的应用程序选择：

- `Drupal`
- `Joomla`
- `Redmine`
- `GitLab`
- `WordPress`
- `Magento`
- `Nginx`

以下是 Amazon Lightsail 的开发者堆栈选择：

- `LAMP`
- `LEMP`
- `MEAN`
- `Node.js`

在选择应用程序或开发者堆栈后，选择你的实例计划，该计划决定了虚拟 `CPU` (`vCPUs`) 的数量、内存大小、磁盘空间大小以及预期的数据传输量。分配一个唯一的名称（该名称需要在你的账户内唯一），决定你想要启动的实例数量（最多为 20 个），并创建你的实例。

你的 Amazon Lightsail 实例将在自己的 `Amazon VPC` 中启动。

### 管理

一旦实例运行，你就可以停止实例、重启它或删除它。实例被删除后计费将停止。

# 第 4 章 ■ 计算

管理 Amazon Lightsail 涉及管理实例本身以及管理客体操作系统、应用程序或开发者 `CLI`。管理实例可以通过 Amazon Lightsail 控制台或 `CLI` 完成。管理其他方面可以通过 Amazon Lightsail 控制台提供的 `SSH` 连接或通过你自己的 `SSH` 客户端访问实例来完成。通过你自己的 `SSH` 客户端访问涉及从你的 AWS 账户下载私钥。

Amazon Lightsail 控制台为你提供了五项管理功能的访问：连接 (`Connect`)、指标 (`Metrics`)、网络 (`Networking`)、快照 (`Snapshots`) 和历史 (`History`)。连接让你能够通过 Amazon Lightsail 控制台登录客体操作系统（而不是独立的 `SSH` 客户端）。

# 可用指标

指标提供以下信息：

- `CPU` 利用率
- 网络入
- 状态检查失败实例（指示特定实例出现故障）
- 状态检查失败系统（指示底层 AWS 硬件出现故障）

所有这些指标都以小时、六天、一周和两周为增量提供。

### 网络

网络提供有关你的 `IP` 地址的信息，包括公网 `IP` 地址（从互联网访问）和私有 `IP` 地址（内部访问的地址）。你可以将公 `IP` 变为静态 `IP` 地址。网络还列出了防火墙上的端口，并提供了根据需要打开或关闭端口的能力，从而控制谁可以访问你的实例。

快照是你创建和存储快照的地方。你也可以在这里根据快照创建新实例。拍摄和存储快照的数量没有限制。请注意，存储快照是收费的。

历史列出了实例何时创建、停止和重启；提供了有关已拍摄快照的信息；并提供了有关已附加或解绑静态 `IP` 地址的信息。

通过 Amazon Lightsail，你可以保留分配给实例的 `IP` 地址、分配静态 `IP` 地址或创建 `DNS` 区域。Amazon Lightsail 中的公 `IP` 地址的行为与 `Amazon EC2` 中的公 `IP` 地址非常相似；当你停止一个 Amazon Lightsail 实例时，公 `IP` 地址会被移除；当重启该实例时，将分配一个新的 `IP` 地址。如果你需要 `IP` 持久，应该分配静态 `IP` 地址。`DNS` 区域支持 `A`、`CNAME`、`MX` 和 `TXT` 记录。你可以使用 `Route 53` 注册域名。

# 费用

Amazon Lightsail 的费用按小时计算，最小计费时间为一小时。虽然每个实例都有每月费用上限，但可能会产生额外的费用，基于：

1. 快照的存储费用
2. 超过额的数据传输费用
3. 未分配给实例的公 `IP` 地址

# 实例大小

更改 Amazon Lightsail 大小涉及对现有实例进行快照并启动一个更大的实例。无法修改单个实例的 `vCPU` 数量、内存或 `SSD` 大小。

# 安全

Amazon Lightsail 的安全性遵循 AWS 共享责任模型。对计算实例的访问通过 AWS 工具（特别是 `IAM`）控制，而对客体操作系统、应用程序或开发者堆栈的访问由你控制。保持客体操作系统、应用程序或开发者堆栈更新并打补丁是你的责任。AWS 通过仅打开特定操作系统、应用程序或开发者堆栈的相关端口来协助控制访问。你可以打开额外的端口或修改现有端口。

# AWS Batch

AWS Batch 允许你在 AWS 上运行批处理计算负载。这些工作负载可以是任何规模。AWS Batch 允许终端用户计划、调度和执行批处理作业，同时能够控制成本。

# 实现

AWS Batch 使用本地批处理系统用户熟悉的术语：

- 作业 (`Job`)
- 作业定义 (`Job definition`)

## 第 4 章 • 计算

- 任务队列
- 调度器
- 计算环境

作业是 AWS Batch 执行的工作单元。作业可以作为 AWS Lambda 函数或运行在 `Amazon EC2` 上的容器化应用程序的形式执行。

作业定义（`Job definitions`）与 `Amazon ECS` 任务定义的概念相似——它们指定了作业如何运行。作业定义中指定的某些属性包括 `vCPU` 需求、内存需求、挂载点和环境变量等项。

任务队列是作业存放的地方，直到它们被调度到计算资源为止。例如，你可以拥有多个任务并使用任务队列设置优先级。你可以指定让特定队列中的作业在尝试执行另一个队列中的作业之前完成。

调度器评估任务队列中的作业，并对在何时、在何处以及如何运行这些作业做出决定。只要满足对其他资源的所有依赖关系，该算法采用先入先出（`FIFO`）。

计算环境有两种类型：托管和非托管。在托管环境中，你只需指定所需的配置（例如实例类型、最小/最大/所需的 `vCPUs`、竞价实例 `Spot` 实例的使用），由 AWS 负责启动和扩展你的资源。你可以指定在哪个 `Amazon VPC` 和子网中启动计算实例。在非托管计算环境中，由你启动并管理计算资源，并需要包含 `Amazon ECS` 代理以及运行支持的 `Linux` 和 `Docker` 版本。

## 实现 AWS Batch 作业

实现批处理作业的步骤如下：

1. 定义作业。
2. 配置计算环境。
3. 配置任务队列。
4. 提交作业。

作业一旦提交，它将通过以下状态：

- `Submitted`：已提交到队列但尚未被调度器评估。
- `Pending`：已提交到队列并已评估，但由于依赖另一个作业或资源尚未运行。
- `Runnable`：在队列中无未决依赖项，已准备好被调度。
- `Starting`：已调度到主机并正在容器初始化操作。
- `Running`：作业正在运行。
- `Succeeded`：作业已完成。
- `Failed`：作业所有可用尝试均失败。

如果作业失败，你可以自动化重试最多 10 次。

## 总结

### 管理

AWS Batch 有服务配额限制。你最多可以拥有 10 个计算环境、5 个任务队列以及每个任务队列 3 个计算环境。这些限制可以通过 AWS 管理控制台或 `AWS CLI` 修改。你还可以拥有最多 20 个作业依赖和 1,000,000 个提交状态的作业。最大作业大小为 20 `KB`。这三个限制无法更改。

## 监控

你可以通过 `CLI` 或 AWS Batch 板监控你的 AWS Batch 环境。作业的日志（例如 `STDERR` 和 `STDOUT`）可在 AWS 管理控制台中查看，并可以写入 `Amazon CloudWatch Logs`。你可以使用 `SSH` 访问启动的 `Amazon EC2` 实例以处理你的 AWS Batch 作业。

## 费用

AWS Batch 没有额外费用。唯一的费用是 `Amazon EC2` 资源或 AWS Lambda 资源。你可以对所有计算实例使用竞价定价（`Spot pricing`）以降低成本。

## 安全

AWS Batch 使用 `IAM` 控制对所用 AWS 资源的访问。通过 `IAM`，你可以为组织中的不同用户定义策略，以获得不同级别的访问权限。由于你控制创建计算资源的 `Amazon VPC`，你可以使用私有子网、网络 `ACL` 和安全组实施额外的安全分层。

## 总结
