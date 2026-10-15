
```
Type the number of the solution to view or 'e' to return to the previous menu.
1 [ 253273:VER] How to register and subscribe a system to the Red Hat Customer Portal using Red Hat Subscription-Manager
2 [ 265523:VER] Enabling or disabling a repository using Red Hat Subscription Management.
3 [ 108423:VER] Why does subscription-manager list return: "No Installed products found"
output omitted...
Select Solution: 1
```

如上所示选择文章 1 号，您将将被提示选择阅读的文档章节。最后，使用 `Q` 退出当前章节，或反复使用以退出 `redhat-support-tool` 命令。

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

## Title

===============================================================================

使用 Red Hat Subscription-Manager 将系统注册并订阅到 Red Hat 客户门户

URL: https://access.redhat.com/solutions/253273

Created On: None

Modified On: 2017-05-29

## Title

===============================================================================

使用 Red Hat Subscription-Manager 将系统注册并订阅到 Red Hat 客户门户

URL: https://access.redhat.com/solutions/253273

Created On: None

Modified On: 2017-05-29

## Issue

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

当服务器拔掉电源时，操作系统无法继续运行。

+ 1 紧急 (Urgent)

2 高 (High)

3 普通 (Normal)

4 低 (Low)

请选择严重程度（或输入 'q' 退出）：`4`

是否要为此案例分配一个案例组 (y/N)? N

在打开支持案例之前，您是否想查看此问题的解决方案？

(y/N) N

支持案例 01034421 已成功打开。

如果没有指定 `--product` 和 `--version` 选项，`redhat-support-tool` 将为这些选项提供列表。

```
[user@host ~]$ redhat-support-tool
Welcome to the Red Hat Support Tool.
Command (? for help): opcase
Do you want to use the default product - "Red Hat Enterprise Linux" (y/N)?: y
output omitted...
29 7.5
31 7.6
32 8.0 Beta
```

请选择版本（或输入 'q' 退出）：`yum fails to install apache`

请输入描述（完成后在空行上按 Ctrl-D）：

yum cannot find correct repo

+ 1 紧急 (Urgent)

2 高 (High)

3 普通 (Normal)

4 低 (Low)

请选择严重程度（或输入 'q' 退出）：`4`

是否要使用默认的（未分组）案例组 (y/N)?: y

在打开支持案例之前，您是否想查看此问题的解决方案？ (y/N) N

支持案例 018355678 已成功打开。

## 为支持案例附加诊断信息

包含诊断信息可以更快解决问题。在打开案例时附加 `sosreport`。`sosreport` 命令会生成一个从运行的系统中收集的诊断信息的压缩包。如果已创建了存档，`redhat-support-tool` 会提示包含它：

> 请为支持案例 01034421 附加 SOS 报告。以 root 用户身份创建 SOS 报告并执行以下命令 -c sosreport 直接发送到案例：

`redhat-support-tool attachment -c 01034421 path to sosreport`

您现在要为 01034421 附加文件吗？(y/N) N

Command (? for help):

## 第 1 章 | 管理服务与支持

如果不存在当前的 SoS 报告，管理员可以稍后生成并附加一个。使用 `redhat-support-tool addattachment` 命令附加报告。

订阅者可以查看、修改和关闭支持案例：

+ Command (? for help): `listcases`
