

# 分析服务并获取支持

工具提供了相关工具的链接，帮助您成功使用 Red Hat 产品。解决方案引擎（Solution Engine）为您提供了一种高效的方法来快速搜索解决方案，如果您没有找到满意的解决方案，可以提交工单。客户门户实验室（Customer Portal Labs）提供基于 Web 的应用程序和工具，帮助您提高性能、诊断问题、安全问题并优化配置。例如，产品周期检查器（Product Cycle Checker）可以帮助您查看特定产品及其支持生命周期计划。另一个工具救援模式助手（Rescue Mode Assistant）可以帮助您识别系统的根本原因、生成报告或修复系统的启动时问题。在别处还有许多其他可用工具：

| Tools | Customer Portal Labs |
| --- | --- |
| Solution Engine | Configuration |
| Package | Deployment |
| Errata | Security |
| | Troubleshooting |

图 16.33：工具

安全（Security）提供了访问 https://access.redhat.com/security/ 的 Red Hat 产品安全中心的权限。它还提供了有关高关注安全问题的信息、访问 Red Hat CVE 数据库、Red Hat 博客的安全中心，以及关于 Red Hat 安全响应流程以及我们如何评估和解决这些问题的资源。

最后，社区（Community）菜单是 Red Hat 专家、客户和合作伙伴进行通信与协作的地方。这里提供了讨论论坛、博客以及您所在地区即将举行的活动信息。

> 注意
> 您应该在[开始使用 Red Hat](https://access.redhat.com/start/) 中完成整个导览，包括关于如何个性化您的客户门户体验以及探索您的 Red Hat 订阅优势的章节，以获取有关客户门户的完整信息。您需要在客户门户账户中至少有一个激活的订阅才能访问此页面。

# 使用 RED HAT 支持工具搜索知识库

Red Hat 支持工具 `redhat-support-tool` 提供了一个基于文本的界面，允许您从系统的命令行在客户门户上搜索知识库文章并提交案例。该工具没有图形界面，由于它需要与 Red Hat 客户门户交互，因此需要访问 Internet。使用任何终端或 SSH 连接运行 `redhat-support-tool` 命令。

`redhat-support-tool` 命令可以在交互模式下使用，也可以带有选项和参数作为命令使用。该工具的语法适用于这两种方法。默认情况下，程序在交互模式下启动。使用 `help` 命令查看所有可用命令。交互模式支持制表补全以及调用父 shell 中程序的能力。

```
[user@host ~]$ redhat-support-tool
Welcome to the Red Hat Support Tool.
Command (? for help):
```

# 分析服务并提供支持

当调用时，**redhat-support-tool** 会提示输入 Red Hat 客户订阅者的登录信息。为了避免重复提供这些信息，工具会请求将账户信息存储在用户的家目录（`./redhat-support-tool/redhat-support-tool.conf`）。如果通过特定的 Red Hat 客户门户账户提交问题，可以使用 **global** 选项将账户信息保存到 `/etc/redhat-support-tool.conf` 以及其他系统级配置中。工具的 `config` 命令可以修改配置设置。

**redhat-support-tool** 命令允许订阅者从 Red Hat 客户门户搜索并显示知识库内容。知识库执行关键字搜索，类似于 `man` 命令。用户可以输入错误代码、日志文件中的语法或任何关键词组合来生成相关解决方案文档列表。

这里有一个初始配置和搜索描述：

```
[user@host]$ redhat-support-tool
Welcome to Red Hat Support Tool.
Command (? for help): search How to manage system entitlements with subscription-manager
Please enter your RNH user ID: subscriber
Save the user ID /home/student/.redhat-support-tool/redhat-support-tool.conf(y/n): y
Please enter the password for subscriber: password
Save the password for subscriber in /home/student/.redhat-support-tool/redhat-support-tool.conf(y/n): y
```

在提示用户输入所需的用户配置后，工具继续执行原始搜索请求：

```
Type the number of the solution to view or 'e' to return to the previous menu.
1 [ 253273:VER] How to register and subscribe a system to the Red Hat Customer Portal using Red Hat Subscription-Manager
2 [ 265523:VER] Enabling or disabling a repository using Red Hat Subscription Management.
3 [ 108423:VER] Why does subscription-manager list return: "No Installed products found"
output omitted...
Select Solution: 1
```

如上所示选择文章 1 号，您将将被提示选择阅读的文档章节。最后，使用 `Q` 退出当前章节，或反复使用以退出 **redhat-support-tool** 命令。

```
Select Solution: 1
Type the number of the section to view or 'e' to return to the previous menu.
1 Title
2 Issue
3 Environment
4 Resolution
5 Display all sections
End of options.
Section: 1
```

RH124-RHEL8.0-en-1-20190507

579

# 分析服务并获取支持

Title
===============================================================================
使用 Red Hat Subscription-Manager 将系统注册并订阅到 Red Hat 客户门户
URL: https://access.redhat.com/solutions/253273
Created On: None
Modified On: 2017-05-29

Title
===============================================================================
使用 Red Hat Subscription-Manager 将系统注册并订阅到 Red Hat 客户门户
URL: https://access.redhat.com/solutions/253273
Created On: None
Modified On: 2017-05-29

Issue
===============================================================================
使用 Red Hat Subscription-Manager 将系统注册并订阅到 Red Hat 客户门户
URL: https://access.redhat.com/solutions/253273
Created On: None
Modified On: 2017-05-29

# 使用 RED HAT 工具管理支持案例

订阅的一个益处是通过客户门户访问技术支持。根据支持级别，可以通过在线或电话联系 Red Hat。请访问 https://access.redhat.com/support/policy

# 准备 Bug 报告

在联系 Red Hat 支持部门之前，收集信息至关重要。

定义问题。能够清晰地陈述问题及其症状。尽可能具体。详细列出重现问题的步骤。

收集背景信息。哪个产品和版本受影响？准备好提供信息。这可能包括 `sosreport` 或崩溃转储（crash dump）。

确定严重级别。Red Hat 使用四个严重级别来划分问题。紧急和高级的问题应通过电话处理。

| SEVERITY | DESCRIPTION |
| --- | --- |
| Urgent (Severity 1) | 严重影响您在生产环境中对软件的使用。包括生产数据丢失或系统故障。该问题会导致业务中断且没有替代方案。 |
| High (Severity 2) | 软件可以运行但在生产环境的功能严重降低。该情况对您的业务产生高影响且没有替代方案。 |
| Medium (Severity 3) | 在生产环境或开发环境中涉及软件的部分非关键使用。对于生产环境，对业务产生中等或低的影响。可以通过替代方案继续运行。对于开发环境，该情况会导致项目迁移到生产环境出现问题。 |
| Low (Severity 4) | 一般使用问题、文档错误报告或对未来产品增强或修改的建议。对于生产环境，对业务或系统性能/功能的影响低或没有。对于开发环境，对业务产生中等或低的影响，但可以通过替代方案继续运行。 |

# 使用 redhat-support-tool 管理 Bug 报告

订阅者可以使用 `redhat-support-tool` 创建、查看、修改和关闭 Red Hat 支持案例。当案例处于打开或维护状态时，用户可以附加文件或文档，例如诊断报告（sosreport）。该工具会将文件上传并附加到案例中。

包括产品、版本、摘要、描述、严重性和案例组在内的案例细节可以通过命令行选项分配，也可以让工具提示所需信息。在以下示例中，打开了一个新案例。指定了 `--product` 和 `--version` 选项。

```
[user@]$ redhat-support-tool.
Welcome to Red Hat Support Tool.
Command (? for help): opencase --product="Red Hat Enterprise Linux" --nversion="7.0"
Please enter a summary (or 'q' to exit): System fails to run without power
nPlease enter a description (Ctrl-D on an empty line when complete):
```

