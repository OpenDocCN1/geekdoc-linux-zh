
当数据必须快速访问并需要长期持久化时，建议使用`Amazon EBS`。`Amazon EBS`卷特别适用于作为文件系统、数据库的主存储，或任何需要精细粒度更新以及访问原始、所有者级或块级存储的应用。`Amazon EBS`既适用于执行随机读写的数据库类型应用程序，也适用于吞吐量密集型应用程序。

实例存储型实例和`EBS`型实例的另一个区别是可停止的能力。（注：原文此处存在大量重复的错误短句，翻译时已根据逻辑进行了处理）。`图 4.1` 实例存储型`Amazon EC2`实例与`EBS`型`Amazon EC2`实例的差异

`Amazon EFS`为`Amazon EC2`提供可扩展的文件存储。您可以同时挂载该文件系统。（注：原文此处存在大量重复的错误短句，翻译时已根据逻辑进行了处理）。

## 第 4 章 • 计算

`Amazon EC2`实例使用实例存储进行启动的时间比`Amazon EC2`实例使用`Amazon EBS`更长。影响启动时间的另一个因素是在初始启动实例时使用用户数据（`user data`）。使用用户数据会减慢启动过程。使用完全配置的`AMI`（你可以自行创建）可以加快启动过程。请注意，由于完全配置的`AMI`是硬编码的，因此在修改方面的灵活性较低（你必须创建一个全新的`AMI`），因此在启动速度和配置的灵活性之间需要进行权衡。

实例元数据（`Instance metadata`）是关于你的实例的数据，你可以用它来配置或管理实例。可以通过`http://169.254.169.254/`访问元数据。`Amazon EC2`实例还可以包含动态数据，例如在实例启动时生成的实例身份文档，实例通过元数据可以访问该文档。它会验证实例的属性，例如订阅的软件、实例大小、实例类型、操作系统和`AMI`。可以通过`http://169.254.169.254/latest/dynamic/instance-identity/document`访问。你还可以访问在启动实例时提供的用户数据。例如，你可以使用特定参数来配置实例、下载补丁、安装软件或挂载简单脚本。你还可以使用这些数据构建通用`AMI`，这些`AMI`可以通过启动时提供的配置文件进行修改。例如，如果你为极小企业运行`Web`服务器，它们可以使用相同的`AMI`，并从你在启动时用户数据中指定的`Amazon S3`桶中检索其内容。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_153_0.png)

> 虽然你只能从实例本身访问实例元数据和用户数据，但数据并没有受到加密方法的保护。任何可以访问实例的人都可以查看其元数据。因此，你应该采取适当措施来保护敏感数据（例如长加密密钥）。你不应该将密码等敏感数据作为用户数据存储。

## 快照 (Snapshots)

你可以通过创建时间点快照将`Amazon EBS`卷上的数据备份到`Amazon S3`。快照是增量备份，这意味着只有自你最近快照之后设备上发生变化的块会被保存。这最大限地减少了创建快照所需的时间并节省了存储成本。当你删除快照时，只有该快照特有的数据会被移除。活动快照包含了将你的数据（从快快照开始）还原到新的`Amazon EBS`卷所需的所有信息。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_153_1.png)

作为`AWS`系统运营`way`，了解`Amazon EC2`提供的不同类型块存储的性能和运行特性至关重要。

## 监控 AWS 云服务的状态

`AWS`提供了两个显示`AWS`云服务状态的仪表板。第一个是`AWS 服务健康仪表板`（`AWS Service Health Dashboard`）。该仪表板显示整个`AWS`基础设施的服务健康状况，你可以对其进行个性化以跟踪你的`AWS`云服务。通过`AWS 服务健康仪表板`，你可以查看跨区域服务的健康状况（`AWS GovCloud [US]`区域和中国`[北京]`区域除外）。你还可以订阅跨区域选择服务的`RSS`馈。此外，你还可以查看所有区域所有服务的系统状态（同样排除`AWS GovCloud [US]`区域和中国`[北京]`区域）。

第二个仪表板是`AWS 个人健康仪表板`（`AWS Personal Health Dashboard`）。`AWS 个人健康仪表板`提供了可能影响你账户的`AWS`健康事件信息。这些信息以两种方式呈现：一个按分类组织近期和即将发生的事件的仪表板，和一个显示过去 90 天内所有事件的完整日志。`AWS 个人健康仪表板`使用`AWS API`，你可以用它创建自己的健康仪表板或将其输入到你可能拥有的任何现有系统中。

## 使用 Amazon CloudWatch 进行监控

`Amazon EC2`实例默认开启`Amazon CloudWatch`监控。默认提供基础监控，它每五分钟收集一次指标。你可以启用详细指标，这些指标会每分钟收集一次数据。`Amazon CloudWatch`监控`Amazon EC2`的以下指标：

- `CPU`利用率

- 磁盘读取

- 磁盘写入

- 网络入站

- 网络出站

- 实例状态检查

- 系统状态

- `CPU`额度使用情况（仅限`T2`实例）

- `CPU`额度余额（仅限`T2`实例）

你可以根据特定实例、特定镜像、`Auto Scaling`组或作为聚合值查看`Amazon CloudWatch`指标。`Amazon CloudWatch`可用于触发警报，以停止、终止、重启或恢复`Amazon EC2`实例。

## 使用 AWS CloudTrail

你可以使用`AWS CloudTrail`获取你的账户的`AWS API`调用历史和相关事件。这包括使用`AWS`管理控制台、`AWS`软件开发包(`SDK`)、命令行工具以及更高级`AWS`云服务进行的调用。当启用`AWS CloudTrail`日志时，对`Amazon EC2`的调用将记录在日志文件中，以及任何其他`AWS CloudTrail`服务记录中。`AWS CloudTrail`决定如何在指定的时间和文件大小创建并写入新文件。所有的`Amazon EC2`操作被记录。每条日志记录都包含有关谁生成请求的信息。日志中的用户身份信息可以帮助你判断请求是使用`root`权限或`IAM`凭据、联合用户的临时安全凭据，还是通过另一个`AWS`云服务生成的。

理解为何以及何时使用`Amazon CloudWatch`和`AWS CloudTrail`不仅有助于你监控和管理`Amazon EC2`以及`AWS Systems Manager`

`Systems Manager`是一项管理服务，可帮助你自动收集清单、应用补丁、创建镜像。

## IP 地址

当`AMI`启动时，它拥有元数据和用户数据。元数据包含关于实例的信息，例如订阅的软件、实例大小、实例类型、操作系统和`AMI`。可以通过`169.254.169.254/latest/dynamic/instance-identity/document`访问。你还可以访问在启动实例时提供的用户数据。例如，你可以使用特定参数来配置实例、下载补丁、安装软件或挂载简单脚本。你还可以使用这些数据构建通用`AMI`，这些`AMI`可以通过启动时提供的配置文件进行修改。例如，如果你为极小企业运行`Web`服务器，它们可以使用相同的`AMI`，并从你在启动时用户数据中指定的`Amazon S3`桶中检索其内容。

`IP`地址在实例启动时分配。如果实例停止并启动，`IP`地址可能会发生变化。对于静态`IP`地址，你可以使用弹性`IP` (`EIP`)。

## 购买选项

购买`EC2`有多种选项：

- 按需付费 (`On-Demand`)：非常简单——你为所使用的实例付费。

- 预留 (`Reserved`)：预留实例与按需付费相比提供了折扣。你需要对特定的家族或区域做出承诺。

- 竞价 (`Spot`)：竞价实例允许你竞标空闲容量，这可以显著降低成本。每小时价格根据供需波动。

## 成本估算

`AWS`提供了估算成本的工具：`AWS 每月计算器`和`AWS 总拥有成本 (TCO)`计算器。`AWS`每月计算器有一种机制，可以选择特定区域的服务并将其加入总成本中。`TCO`计算器允许你估算使用`AWS`时的节省成本。

## 成本跟踪

`AWS`提供了`Trusted Advisor`和个人健康仪表板来管理和跟踪成本。这些工具可以在`AWS`管理控制台中找到。`AWS Trusted Advisor`提供有关如何可能减少`AWS`支出的建议。个人健康仪表板专门负责你的费用和账单。通过个人健康仪表板，你可以查看并下载账单、探索账单（图形化和分析）、创建预算并根据这些预算接收通知。你还可以创建成本分配标签，允许你将成本与创建的资源关联。

## 创建你自己的 AMI

正如在实施部分所述，在选择`AMI`时可以使用你自己的`AMI`。创建`AMI`的过程取决于你创建的是实例存储型`AMI`还是`EBS`型`AMI`。

要创建实例存储型`AMI`，首先从与你想创建的`AMI`类似的`AMI`启动实例。你可以连接到实例并进行自定义。当实例设置成你想要的样子，你可以对其进行打包。打包过程需要几分钟。过程完成后，你就获得了一个包。

# 第 4 章 ● 计算

它由一个镜像清单（`image.manifest.xml`）和包含根卷模板的文件（`image.part.xx`）组成。将程序包上传到你的`S3`存储桶，然后注册`AMI`。

要创建一个基于`Amazon EBS`的`AMI`，请先从从与你想要创建的`AMI`相似的`AMI`启动实例。你可以连接到实例并对其进行自定义。在实例配置正确后，停止实例（停止实例可确保实例的数据完整性；系统将对其进行快照）。

接下来创建镜像。当你创建一个基于`Amazon EBS`的`AMI`时，`AWS`会自动为你注册它。一旦你创建了`AMI`，就可以控制谁可以访问它。你可以在其他`AWS`区域之间共享`AMI`。请注意，如果`AMI`是加密的，你将无法共享它。

# 置放组 (Placement Groups)

置组是单个可用区内实例的逻辑分组。

对于受益于低网络延迟、高吞吐量或两者兼有的应用程序，建议使用置组。高性能计算(`HPC`)是一个可能从置组中受益的应用程序示例。由于所有实例都在同一个可用区内，根据定义，位于同一置组的`Amazon EC2`实例不能位于不同的可用区或不同的区域。同一置组中的`Amazon EC2`实例之间通过私有`IPv4`地址或`IPv6`地址相互通信。

# 安全

`Amazon EC2`环境中的安全是终端用户和`AWS`共同承担的责任。这是因为在该环境中，某些部分是由终端用户控制的。物理安全和虚拟机管理器（`Hypervisor`）的安全是`AWS`的责任。另一方面，终端用户负责保护运行在其实例上的操作系统以及运行在该操作系统上的应用程序。你保留了选择何种安全措施来保护你的内容、平台、应用程序、系统和网络的控制权，这与在本地数据中心对应用程序的操作不同。

关于`Amazon EC2`，你负责控制谁可以访问机器（包括网络访问和管理访问），并保持客主机操作系统为最新且已过补丁。如果你需要，可以在无需`AWS`授权的情况下应用额外的安全层（例如，在客主机操作系统上运行`IP Tables`或`Windows Defender`）。`AWS`对你的实例或客主机操作系统没有任何访问权限。

# 控制网络访问

`AWS`提供了许多关于网络访问的工具：将`Amazon EC2`实例放置在`Amazon VPC`中（在第 3 章讨论过`Amazon VPC`安全）以及使用安全组控制特定接口的访问。通过管理访问，你再次可以通过将`Amazon EC2`实例放置在`Amazon VPC`中、使用安全组以及使用公/私钥对对进行加密并控制访问来控制访问。

# 控制管理访问

`AWS`提供了许多工具来管理实例的安全性。这些工具包括：

- `IAM`

- `AWS Trusted Advisor`

- `AWS Service Catalog`

- `Amazon Inspector`

`IAM`允许你创建策略来控制对`API`的访问，并将这些策略应用于用户、组和角色。

`AWS Trusted Advisor`作为`AWS Support`的一部分，会检查开放的安全组和允许`Amazon EC2`实例的访问权限级别等内容，并提供建议以提高你的`AWS`基础设施的安全性。

`Service Catalog`允许`IT`管理员为用户创建、管理和分发产品组合，用户随后可以在个性化门户中访问他们需要的产品。`AWS Service Catalog`允许组织集中管理常用的`IT`服务，并帮助组织实现一致的治理并满足合规性要求，同时允许用户在组织设置的限制内仅部署所需的批准的`IT`服务。

`Amazon Inspector`是一项安全漏洞评估服务，有助于提高你的`AWS`资源的安全合规性。`Amazon Inspector`会自动评估资源是否存在漏洞或偏离最佳实践的情况，并生成一个按严重程度排序的详细安全发现列表。

> `AWS`还提供了许多开发者文档、白皮书、文章和教程，帮助你保护环境。这些内容可以在`AWS`网站的云安全资源页面上找到。

![](img/5a8c28d2e214d3abf9ba8ffcdf583f47_158_0.png)

# Amazon EC2 容器服务 (Amazon ECS)

`Amazon ECS`是一种高度可扩展的容器管理服务。`Amazon ECS`使在`Amazon EC2`实例上运行、停止和管理`Docker`容器变得简单。

通过`Amazon ECS`，你可以使用`API`调用跨你的集群启动并放置容器。你根据资源需求、隔离策略和可用性要求调度容器的放置。你可以同时将`Amazon ECS`用于集群管理和用于调度将部署项调度到主机上。

`Amazon ECS`消除了对集群管理的需要。`Amazon ECS`可用于构建,,,,,,`can to to to to the the and the..`。`Amazon ECS`是一项跨多个可用区运行的高可用服务。它可以用于监控在`in of ECS the and the the Console`。

# 实现

要实现`Amazon ECS`，你需要在实例上安装代理。如果你使用`Amazon ECS`优化的实例，则代理已经安装。此外，`Amazon be can to to to to your ECS`。

- 集群是容器实例的逻辑分组，只能是单个集群的成员。

- `Amazon ECS`是你的一个仓库。

-- `is is is where you define the repository.`

# 部署容器

要部署容器，你需要执行以下操作：

1. 定义任务（`Task`）。在此处你分配名称并决定内存大小。

2. 定义服务（`Service`）。在此处你决定想要运行多少个实例并注册负载均衡器。

3. 创建`Amazon ECS`集群。在此处根据配置创建集群。

4. 创建栈（`Stack`）。在此处通过控制台创建栈。

### 管理

`Amazon ECS`可以使用`AWS`管理控制、`AWS CLI`配置。

# 监控 Amazon ECS

监控你的`Amazon ECS`集群的主要工具是`CloudWatch`。`AmazonWatch`按分钟收集`Amazon ECS`指标并将其发送到`CloudWatch`。`AmazonWatch`保存这些指标两周。你可以监控整个集群的`CPU`和内存利用率。你可以使用`CloudWatch`触发告警、发送通知并创建仪表板来监控服务。

一旦启动，你可以在`Amazon ECS`控制台和`CloudWatch`控制台中查看`CloudWatch`指标。`Amazon ECS`控制台提供最多 24 小时的视图，而`CloudWatch`控制台提供精细且可自定义的服务视图。

另一个工具是`AWS CloudTrail`，它将记录所有的`Amazon ECS API`调用。`AWS Trusted Advisor`是监控你所有`AWS`资源（包括`Amazon ECS`）以提高性能、可靠性的另一个来源。

使用`Amazon ECS`无额外费用。仅对`Amazon EC2`实例或`AWS Lambda`请求时间收费。

# 安全

对于`Amazon ECS`，你需要执行：

1. 控制谁可以创建任务定义。

2. 控制谁可以部署集群。

3. 控制谁可以访问`Amazon EC2`实例。

`IAM`是用于前两个必要的工具。对于控制`Amazon EC2`实例，适用于`Amazon EC2`部分描述的工具。你可以使用`IAM`角色、安全组以及（由于这些`Amazon EC2`实例位于`Amazon VPC`中）网络访问控制列表(`ACL`)和路由表来控制对`Amazon EC2`实例的访问。

# AWS Elastic Beanstalk

`AWS Elastic Beanstalk`允许你在`AWS`云中部署和管理应用程序，而无需担心运行这些应用程序的基础设施。`AWS Elastic Beanstalk`在不限制选择或控制的情况下降低了管理的复杂性。你只需上传应用程序，`AWS Elastic Beanstalk`就会自动处理容量配置、负载均衡、伸缩和应用程序健康监控的细节。

# AWS Elastic Beanstalk 支持的语言

`AWS Elastic Beanstalk`支持使用以下开发的应用程序：

- `Java`

- `PHP`

- `.NET`

- `Node.js`

- `Python`

- `Ruby`

# AWS Elastic Beanstalk 部署的服务

`AWS Elastic Beanstalk`会自动部署`Amazon VPC`、计算实例（跨越多个可用区）、安全组（用于实例和负载均衡器）、自动扩展（`Auto Scaling`）、`Amazon S3`桶、`Amazon CloudWatch`告警以及域名。尽管`AWS Elastic Beanstalk`会自动完成你的环境部署，但你仍然可以根据需要进行修改。

# 实现

你可以使用多种工具来创建和管理`AWS Elastic Beanstalk`环境。这些工具如下：

- `AWS Management Console`

- `AWS Elastic Beanstalk CLI`

- `AWS SDK for Java`

- `AWS Toolkit for Eclipse`

- `AWS SDK for .NET`

- `AWS Toolkit for Visual Studio`

- `AWS SDK for Node.js`

- `AWS SDK for PHP`（需要`PHP 5.2`或更高版本）

- `Boto`（`Python`的`AWS SDK`）

- `AWS SDK for Ruby`
