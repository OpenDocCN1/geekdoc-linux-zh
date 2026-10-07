
如果您进入 **Tasks**（前述截图中的标签页），在前述输出中标记为敏感的 `webhook_secret` 将用于在 GitHub 存储库端设置 webhook。要查看它，您需要运行以下命令：

```
admin@myhome:~$ terraform output webhook_secret
"bf3b20b285c9c741eff34621215ca41cb62594298a4cec44a19ac3c70ad3333c-c979e8b24c0699003e5a879683e4d0729efa750c47cdbeef3779b3eaef*"
```

Terraform 已成功初始化！

Terraform 创建了一个名为 `.terraform.lock.hcl` 的锁文件，用于记录它所做的 provider 选择。请将此文件包含在您的版本控制存储库中，这样在将来您运行 `terraform init` 时，Terraform 默认会做出相同的选择。

现在，我们可以运行以下 `terraform plan` 命令：

```
admin@myhome~~$ terraform plan
```

Terraform 使用所选 provider 生成了以下执行计划。资源操作通过以下符号表示：

+ * create（创建）
* read（（数据资源）

Terraform 将执行以下操作：

# 为了可读性，输出已截断

```
# aws_cloudwatch_log_group.atlantis will be created

+ resource "aws_cloudwatch_log_group" "atlantis" {

  + arn = (known after apply)

  + id = (known after apply)

  + name = "atlantis"

  + name_prefix = (known after apply)

  + retention_days = 7

  + skip_destroy = false

  + tags = {

    + "Name" = "atlantis"

  }

  + tags_all = {

    + "Name" = "atlantis"

  }

}
```

# 为了可读性，删除了部分输出
Plan: 添加 49 个，更改 0 个，删除 0 个。

如果您看到类似的输出，可以对其进行应用（apply）。模块还将恢复许多关于已资源的信息。这些信息值得关注。

运行 `terraform apply` 后（需要几分钟时间），您将看到类似下方的输出：

```
Apply complete! Resources: 49 added, 0 changed, 0 destroyed.
```

# 输出 (Outputs):

```
alb arn = "arn:aws:elasticloadbalancing:eu-central-1:673522208003-loadbalancer/atlantis/8e6a5c314c2936bb"

# 为了可读性，输出已截断

atlantis_url = "https://atlantis.devopsfury.com"

atlantis_url_events = "https://atlantis.atlantis.devopsfury.com/events"

public_subnet_ids = [

  "subnet-08a96bf6a1a565a20",

  "subnet-08b98459f42567dbd"

]
```

如果您正确完成了所有操作，应该能够访问我们之前创建的 `atlantis.automation.yourorganisation.tld` 域下的 Atlantis 网站。该模块已为我们在 Route53 区域添加了所有必要的记录。

如果到目前为止一切顺利，当您访问 https://atlantis.automation.yourorganisation.tld 时，您将看到下面的 Atlantis 面板：

![](img/ee6546d87ccdb3a825326ec9b7ed6bdd_379_0.png)

Apply 命令已启用

+ - 禁用 APPLY 命令

# 锁 (Locks)

未找到锁。

图 13.1 – 使用 Terraform 模块成功部署后的 Atlantis 网站

## 使用 Terraform、GitHub 和 Atlantis 进行 CI/CD

我们还可以使用与 Atlantis 位于同一存储库中的模块通过 Terraform 实现其自动化。

这是该模块的完整 URL：`https://github.com/terraform-aws-modules/terraform-aws-lantis/tree/master/github-repository-webhook`。

或者，您也可以通过 GitHub 网站并遵循文档手动创建 webhook 进行测试：`https://docs.github.com/en/webhooks-and-events/webhooks/creating-webhooks`。

记住使用 Terraform 输出变量中自动生成的密钥 —— `webhook_secret`。

创建 webhook 的文档在 Atlantis 文档中也有详细说明：`https://www.runatlantis.io/docs/configuring-webhooks.html#github-enterprise-`。

您可能会遇到 Atlantis 未按预期运行，且在访问网络门户时遇到 HTTP 500 错误。为了跟踪此服务的任何问题（如果 Atlantis 仍然不可用或对 GitHub webhook 响应错误），您可以前往 AWS 控制台并找到 ECS 服务。从那里，您应该选择集群 `lantis`。如果您点击它，将会在下图中看到集群的配置和状态：

Amazon Elastic Container Service（亚马逊弹性容器服务） > Clusters（集群） > atlantis > Services（服务）

![](img/ee6546d87ccdb3a825326ec9b7ed6bdd_380_0.png)

图 13.2 – Amazon Elastic Container Service (ECS) Atlantis 集群信息

## 使用 Atlantis 进行 CI/CD

如果您进入 `Tasks`（前述截图中的标签页），在前述输出中标记为敏感的 `webhook_secret` 将用于在 GitHub 存储库端设置 webhook。要查看它，您需要运行以下命令：
