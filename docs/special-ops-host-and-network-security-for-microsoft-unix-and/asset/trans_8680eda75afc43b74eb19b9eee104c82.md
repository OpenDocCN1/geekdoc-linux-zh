
这需要巨大的精力，因此请明智选择。一旦创建了每个区域，你就应该为每个区域设计安全策略。每个区域都应该根据其业务重要性和你可用的资源，接受适当程度的评估和修复。

最后，这个过程必须包含你的项目团队的投入，并需要管理层的批准。如果你单兵匹马地选择了四个网络区域，并根据资源选择对其中两个进行评估，那么在发生事件时，你可能会发现在那些指责你的人眼中你你是一个“单点故障”。听我的，你不会希望这个决定由你独自承担的。记住要让其他部门参与，记录下你的计划，并在开始之前获得批准。如果你意识到自己人手短缺或预算不足，请将此文档提供给你的主管审阅。谁知道呢，你可能会证明你的合理性并获得更多资源。

## 评估主机和网络漏洞

安全评估可以被看作是事故预防。事故是通过在漏洞被利用之前对其进行识别和修复来预防的。通过防止即使只是一次事故，你也有效地降低了企业资产在机密性、完整性和可用性方面遭受中断或损失的风险。根据你的业务，这些资产可能不仅影响底线，它们可能就是底线本身。

内部安全评估的目标是评估企业主机和网络的安全性。这种评估不仅会识别出症状性的安全问题（漏洞），还将确定导致这些漏洞的系统性原因（例如补丁管理不当）。有效处理这两个问题的组织可以有效减少你网络环境中的当前和未来风险。

内部安全（也称为 INS）关于识别和处理对你关键企业资产影响最大的漏洞。修复应该侧重于高投资回报率。在大多数环境中，INS 评估-修复的生命周期必须是快速且廉价的。我们已经讨论了这些步骤，如资产清单和对关键企业资产进行排序，那么下一步是什么呢？

你需要仔细审视你用于保护内部网络的可用资金，并对适合你的评估类型做出书面记录的决策。我猜你将决定将你的网络分成若干部分，并以不同的方式评估每个部分。这将允许你在对某些部分进行评估时做到全面，而只从其他网络中收集高严重的漏洞。这些解决方案中的每一个可以使用每章中详细说明的工具和技术、使用第 3 章描述的技术，或使用自动化漏洞评估产品来执行。

## 使用自动化漏洞评估 (VA)

漏洞评估 (VA) 是对自动化漏洞评估过程应用程序的术语。它们允许你在手动询问几台机器的时间内检查许多机器。所有的 VA 工具都将执行主机发现并检测网络上可进行扫描的活动系统。它们都具有某些服务发现（端口扫描）或低级枚举功能，用以确定每个主机上哪些服务是活跃的并需要检查的。最后，执行漏洞检查以确定活跃的服务是否有任何安全问题。然而，VA 是 INS 生命周期中的一个关键部分，但它并不能完全消除人为因素。你应该进行手动系统检查以验证报告中的虚假阳性，并主机主机以识别虚假阴性。

## 执行主机诊断审查

一旦你涵盖了基础知识（如发现常见的网络漏洞），评估单个主机的安全性将变得非常有价值。主机评估将揭示在标准主机和网络评估期间永远无法发现的漏洞。需要审查的关键领域包括以下：

- OS 补丁管理
- 文件系统安全（包括 Windows 的注册表）
- 用户账户
- 密码
- 文件共享（网络文件系统 [NFS] 或 Windows 共享）
- 活跃服务
- TCP/IP 主机过滤
- 日志和审计
- 特定于系统的安全设置
- 存储数据的加密
- 防病毒保护
- 通用控制（备份、物理安全、空调、UPS）
- 软件/应用程序版本和补丁
- 软件/应用程序访问控制
- 软件/应用程序配置

根据此列表创建特定于系统的清单；还要使用此书每一章的特定信息，以及来自 www.sans.org/score 等替代来源的数据。此外，你应该跟踪监听的 TCP 和 UDP 端口。图 1.2 显示了一个部分 Windows 清单的基本示例。电子表格的其他选项页可以包含 IIS 日志示例、Fport.exe 的输出或外部 TCP/IP 端口。

## 图 1.2 跟踪主机审查的清单示例

| ID | 主机名 | IP | OS | 描述 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | | | 10.1.1.199 | Windows | | |
| 2 | | | 10.1.1.7 | SQL Legacy | 10.1.1.5 | | |
| 3 | | | | Domain | | |
| 4 | Operating System | | | Windows 2000 | Windows 2000 | |
| 5 | Registered Applications | | | Domain Controllers | Production DB | 8.0.25 |
| 6 | Descriptions | | | SMB | Legacy System | | |
| 7 | Admin user | | | Address | Admin | Yes |
| 8 | | | | | | |
| 9 | Domain | | | Domain Admin with black password | | |
| 10 | | | | Domain Admin with cracked password | | |
| 11 | | | | | | |
| 12 | Domain | | | Domain Admin with cracked password | | |
| 13 | Local | | | Administration with black password | | |
| 14 | | | | | | |
| 15 | Local | | | Administration with cracked password | David P. | David, Tom. |
| 16 | | | | | | |
| 17 | | | | | | |
| 18 | Windows | | | Auditing disabled | | |
| 19 | Windows | | | Security policy not enabled | | |
| 20 | Windows | | | Windows Service Pack (SP2) | SP2 | X |
| 21 | Windows | | | Service account locked in Domain Admin | SMS | SMS, Antivirus |
| 22 | | | | | | |
| 23 | | | | | | |
| 24 | Windows | | | Shares not implemented | SP2 | X |
| 25 | Windows | | | Service Pack applied | SP1 | |
| 26 | | | | | | |
| 27 | | | | Antivirus not installed | | |
| 28 | | | | | | |
| 29 | SQL | | | Service Pack not applied (SP) | SP3 | X |
| 30 | SQL | | | Guest account has no password | | |
| 31 | | | | Guest account enabled | | |
| 32 | | | | | | |
| 33 | SQL | | | System level account has username | Mikhail, Thomas |
| 34 | SQL | | | Dangerous procedure not set (defense) | | |
| 35 | SQL | | | System level account has password | web | |
| 36 | | | | | | |
| 37 | General | | | Generic password for accounts | BI 44, H33 | X |
| 38 | General | | | Vulnerabilities | | |

## 内部安全

本书的每一章都包含了工具、技术和清单，将协助你对特定技术的审查。选择方法（抽样还是全面）应基于关键性和分配的时间。

## 修复漏洞

发现漏洞只是降低风险的一半。你仍然需要快速有效地修复漏洞、暴露面和配置错误。
