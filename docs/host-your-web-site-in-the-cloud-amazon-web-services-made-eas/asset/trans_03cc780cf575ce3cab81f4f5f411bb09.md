

## 可用区

AWS **可用区**（Availability Zone）代表 AWS 地域（Region）内一组独立的地理位置。每个可用区都有独立的电网和网络连接，从而受到保护，免受其他可用区故障的影响。同一地域内的可用区之间通过低成本、低延迟的连接相互连接。地域名称是可用区名称的一部分。例如，`us-east-1a` 是 `us-east-1` 地域中四个可用区之一。

可用区名称到特定物理位置的映射对于每个 AWS 账户而言是不同但保持一致的。例如，我的 `us-east-1a` 可能与你的 `us-east-1a` 不同，但我的 `us-east-1a` 始终位于相同的物理位置。这种按用户进行的映射是有意为之的，旨在简化扩展和负载管理。

`DescribeAvailabilityZones` 函数和 `ec2-describe-availability-zones` 命令返回特定地域的可用区列表。

## 地域

AWS **地域**（Region）代表位于同一地理区域内的一组 AWS 可用区。每个 AWS 地域都有一个大致指示其覆盖区域的名字，但出于安全考虑，具体位置是保密的。当前的地域包括 `us-east-1`（弗吉尼亚北部）、`us-west-1`（加利福尼亚北部）、`eu-west-1`（爱尔兰）和 `ap-southeast-1`（新加坡）。随着时间的推移，将有更多地域可用。`DescribeRegions` 函数和 `ec2-describe-regions` 命令返回当前地域列表。您可能出于业务、法律或性能原因选择使用多个地域。

## 访问标识符

AWS 使用多种不同的**访问标识符**（access identifiers）来识别账户。这些标识符使用不同形式的公钥加密，并且始终以配对形式存在。配对的第一个元素是公开的，可以根据需要公开，用于识别单个 AWS 账户。第二个元素是私密的，绝不应共享，并用于为每个向 AWS 发出的请求创建签名。当签名作为请求的一部分传输时，它确保请求的完整性，并允许 AWS 验证该请求是否由正确的用户发出。AWS 可以使用两种不同的访问标识符集合。第一种由访问密钥 ID（Access Key ID）和秘密访问密钥（Secret Access Key）组成。第二种是包含公钥和私钥的 X.509 证书。您可以从 AWS 门户查看您的访问标识符。⁶

## Amazon 机器镜像

**Amazon 机器镜像（AMI）** 非常类似于计算机的根驱动器。它包含操作系统，还可以包括额外的软件以及应用程序的各个层，如数据库服务器、中间件、Web 服务器等。您从启动一个预构建的 AMI 开始，不久后就会学会如何为自己创建、分享甚至出售自定义 AMI。每个 AMI 都有一个唯一的 ID；例如，由 `ami-bf5eb9d6` 标识的 AMI 包含 Ubuntu 9.04 jaunty 服务器。DescribeImages 函数和 `ec2-describe-images` 命令返回已注册实例的列表。AWS AMI 目录⁷ 包含公共已注册 AMI 的完整列表。

## 实例

一个**实例**（instance）代表一个正在运行的 AMI 副本。您可以启动相同 AMI 的任意数量副本。使用 `RunInstances` 和 `ec2-run-instances` 命令启动实例。使用 `DescribeInstances` 和 `ec2-describe-instances` 列出正在运行的实例，使用 `TerminateInstances` 函数或 `ec2-terminate-instances` 命令终止实例。不久后，您还将了解 AWS 管理控制台（Management Console），这是一个用于管理 EC2 实例的可视化工具。

## 弹性 IP 地址

AWS 允许您分配固定的（静态的）IP 地址，然后将它们（或路由它们）附加到您的实例；这些被称为**弹性 IP 地址**（Elastic IP Addresses）。每个实例最多可以附加一个此类地址。名称中的“弹性”部分表示您可以根据需求变化轻松地分配、附加、分离和释放这些地址。使用 `AllocateAddress` 函数或 `ec2-allocate-address` 命令分配地址，并使用 `AssociateAddress` 函数或 `ec2-associate-address` 命令将地址附加到实例。

## 弹性块存储卷

**弹性块存储**（Elastic Block Store，EBS）卷是可寻址的磁盘卷。您（或代表您工作的应用程序）可以创建卷并将其附加到同一可用区中的任何正在运行的实例。然后，卷可以被格式化、挂载，并像本地磁盘驱动器一样使用。卷的生命周期独立于任何特定的实例；您可以拥有即使没有实例运行时也能持久的磁盘存储。使用 CreateVolume 函数或 ec2-create-volume 命令创建卷，然后使用 AttachVolume 函数或 ec2-attach-volume 命令将卷附加到正在运行的实例。

## 安全组

**安全组**（Security Group）定义了实例允许的入站网络连接集合。每个组都有名称，由协议、端口和 IP 地址范围列表组成。一个组可以应用于多个实例，而单个实例也可以受多个组的约束。使用 CreateSecurityGroup 函数和 ec2-add-group 命令创建组。AuthorizeSecurityGroupIngress 函数和 ec2-authorize 命令为现有安全组添加新的权限。

## 访问控制列表

**访问控制列表**（Access Control List，ACL）指定对象的权限。ACL 是身份/权限对的列表。GetObjectAccessControlPolicy 函数检索对象现有的 ACL，SetObjectAccessControlPolicy 函数在对象上设置新的 ACL。

## AWS 基础设施 Web 服务

现在您已经了解了关键概念，让我们来看看每个 AWS 基础设施 Web 服务。

## Amazon 简单存储服务

**Amazon 简单存储服务**（Amazon Simple Storage Service，S3）用于存储二进制数据对象，供私人或公共使用。S3 实现具有容错性，并假设硬件故障是常见现象。

有多个独立的 S3 位置：美国标准区域、加利福尼亚北部区域、⁸ 欧洲和亚洲。

S3 自动对每个对象进行多次副本，以实现高可用性以及持久性。这些对象的大小可以从一字节到五吉字节不等。所有对象都位于存储桶（buckets）中，您可以在其中包含任意数量的对象。您的 S3 账户最多可容纳 100 个存储桶或命名对象容器。存储桶名称取自全局命名空间，因此您需要小心并确保拥有健全的存储桶命名策略。当您存储对象时，您需要提供一个必须对存储桶唯一的键。S3 域名、全局唯一的存储桶名称和对象键的组合形成一个全局唯一标识符。可以使用 HTTP 请求访问 S3 对象，使 S3 成为存储静态网页、样式表、JavaScript 文件、图像和媒体文件的理想场所。例如，这是我的金毛猎犬 Maggie 的照片的 S3 URL：http://sitepoint-aws-cloud-book.s3.amazonaws.com/maggie.jpg。

存储桶名称是 **sitepoint-aws-cloud-book**，唯一的键是 **maggie.jpg**。S3 域名是 s3.amazonaws.com。

每个 S3 对象都有自己的 ACL。默认情况下，每个新创建的 S3 对象都是私有的。您可以使用 S3 API 使其对所有人或指定用户可访问，并授予他们读和/或写权限。我将 Maggie 的照片设置为公共可读，以便您可以看到它。

其他 AWS 服务使用 S3 作为 AMI、访问日志和临时文件的存储系统。

Amazon S3 的费用基于存储的数据量、进出 S3 的数据传输量以及向 S3 发出的请求数量产生。

## Amazon CloudFront

Amazon **CloudFront** 是一项内容分发服务，设计用于与 Amazon S3 协同工作。由于所有 Amazon S3 数据都来自位于美国、欧洲和亚洲的中心位置，从世界某些地区访问可能需要几百毫秒。CloudFront 通过以下方式解决这种“光速”限制

