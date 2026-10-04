
另一方面，另一种选择要隐蔽得多，但它假设 IT 部门与基础设施的其他部分之间存在我们可以利用的某些联系，例如 Lambda 函数、IAM 角色、S3 存储桶或某个用户——基本上是散落在草堆中的根针……或者真的如此吗？

仔细一想，实际上有一些东西在 IT 部门和基础设施团队之间有很概率被共享：GitHub 账户。他们总不会为了讨好这两个技术团队就注册两个账户吧？

让我们加载从 Jenkins 获取的 GitHub 令牌，并寻找对 Google Workspace、Gmail、Google Drive 等的引用。我们写了一个简短的 Python 脚本来加载仓库名称：

```python
# list_repos.py
from github import Github
g = Github("8e24ffcc0eeddee673ffa0ce5433ffcee7ace561")
for repo in g.get_user().get_repos():
    print(repo.name, repo.clone_url)
```

```bash
root@Point1:~/# python3 list_repos.py > list_repos_gp.txt
root@Point1:~/# egrep -i "it[_-]|gapps|gsuite|users?" list_repos_gp.txt

it-service      https://github.com/gretschp/it-service.git
it-gsuite-apps  https://github.com/gretschp/it-gsuite-apps.git
users-sync      https://github.com/gretschp/users-sync
--snip--
```

这是一个明显的交叉渗透 ① 迹象。我们克隆 `it-gsuite-apps` 的源代码并……你猜怎么着？！它是一个用于自动化许多 Google Workspace 管理操作的应用程序和服务列表，例如用户置备、组织单元 (OU) 分配、终止账户等：

```bash
root@Point1:~/# ls -lh it-gsuite-apps

total 98M
drwxrwxrwx 1 root root  7.9M provisionner
drwxrwxrwx 1 root root 13.4M cron-tasks
drwxrwxrwx 1 root root  6.3M assign-ou
--snip--
```

这些正是我们用来实现对 Google Workspace 控制的操作类型！当然，这个敏感的仓库对普通用户是不可见的，但我猜冒充 Jenkins 有其特殊之处。

我们开始梦想提取 CEO 的电子邮件并揭露这种欺诈性业务，但很快意识到这个仓库中没有包含任何明文密码。

虽然 AWS 依赖于访问密钥（access keys）来身份验证用户和角色，但 Google 选择了 OAuth2 协议，这需要显式的用户交互。本质上，将打开一个浏览器，验证用户，并生成一个验证代码，该代码必须粘贴回命令行以生成临时私密钥来调用 Google Workspace API。

机器无法遵循这种身份验证流程，因此 Google 还提供了可以使用私密钥进行身份验证的服务账户。然而，查看源代码时，我们没有发现任何私密钥的丝倪：

```bash
root@Point1:~/it-gsuite-apps/# grep -Ri "BEGIN PRIVATE KEY" *
root@Point1:~/it-gsuite-apps/#
```

> 注意
> * {是服务账户只能在 Google Cloud Platform (GCP) 上定义。因此，实际上，为了正确使用 Google Workspace，还需要订阅 GCP。当然，文档中完全没有提到这一点，所以你就像神奇地从 Google Workspace 窗口进入了 GCP 平台。*

所以，我们深入 `it-gsuite-apps` 的代码以了解该程序是如何获取 Google Workspace 权限的，并意外发现了列表 13-2 所示的行。

```java
--snip--
getSecret(SERVICE_TOKEN);
--snip--
public static void getSecret(String token) {
    String secretName = token;
    String endpoint = "secretsmanager.eu-west-1.amazonaws.com";
    String region = "eu-west-1";

    AwsClientBuilder.EndpointConfiguration config = new AwsClientBuilder.
--snip--
```

列表 13-2：从 AWS Secrets Manager 加载服务令牌的代码片段*

现在很合理了。密钥并不是硬编码在应用程序中的，而是通过 Secrets Manager 动态获取的，用于集中存储密钥。我们没有密钥，但幸运的是我们拥有管理员权限，所以可以轻松搜索：

```bash
root@Point1:~/# aws secretsmanager list-secrets \
--region eu-west-1 \
--profile rundeck

"Name": "inf/instance-api/api-token",
"Name": "inf/rundeck/mysql/test",
"Name": "inf/rundeck/log/apikey",
"Name": "inf/rundeck/vpn-employees",
--snip--
```

遗憾的是，无论如何 grep，都没有发现任何与 Google Workspace 相关的。。手动检查每个条目后，真相大白：IT 部门必须使用另一个 AWS 账户。这是唯一的解释。

不必恐慌，跳转到 AWS 账户将从 MX 到 GP。

这两个公司是不同的（尽管交织在一起）。它们拥有独立的 AWS 账户。然而，IT 部门与技术团队一样，是支付账单的实体。

最可能的配置是 GP 创建了一个组织，该组织包含多个 AWS 账户：一个用于技术团队，另一个用于 IT 部门，另一个用于测试等。在这种配置中，一个 AWS 账户被提升为“主”状态。这个特殊账户可以用于将新账户添加到组织，并限制每个账户的可用服务。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设：

```bash
root@point1:~/# aws organizations list-accounts
"Accounts": [
  Id: 983457354409, Name: Infra, Email: infra-admin...
  Id: 354899546107, Name: GP, Email: ...
  Id: 123456789012, Name: IT, Email: ...
]
```

列表 13-3：列出账户

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

看起来不错。正如预料的那样，我们看到了管理员。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 rundeck 角色调用 `list-accounts` API 来轻松证实我们的假设。
