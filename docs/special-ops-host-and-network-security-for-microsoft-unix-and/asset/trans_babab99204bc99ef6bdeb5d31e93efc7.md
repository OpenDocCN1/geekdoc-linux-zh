

## 可用安全工具链接

- www.quare.net/tools.jsp?id=07 Oracle 审计工具
- www.jammed.com/-jwa/hacks/security/tnscmd Tnscmd
- www.ngsoftware.com 用于 Oracle 的 Squirrel
- www.appsecinc.com 用于 Oracle 的 AppDetective
- www.ngsoftware.com OraScan
- www.appsecinc.com 用于 Oracle 的 DbEncrypt
- www.iss.net 数据库扫描器
- www.symantec.com 用于 Oracle 的 ESM
- www.pentafasa.com 用于 Oracle 的 VigilEnt

## 邮件列表

- http://otn.oracle.com/deploy/security/alerts.htm 点击订阅安全告以加入 Oracle 公司的邮件列表。当针对 Oracle 安全漏洞的补丁可用时，将发送通知。
- bugtraq@securityfocus.com 此邮件列表跟踪并讨论已发现的漏洞。任何关注计算机安全的人应该订阅此列表。
- www.appsecinc.com/resources/mailinglist.html 此邮件列表专门针对 Oracle 产品的新型漏洞。
- vulnwatch@vulnwatch.org 一个由志愿者版主社区支持并运行的非讨论、非补丁、全漏洞公告列表。

## 其他感兴趣的书籍

- Theriault, Marlene and William Heney. Oracle 安全. O’Reilly and Associates, 1998.

## 攻击与防御 Oracle • 第 13 章

- Newman, Aaron C. and Marlene Theriault. Oracle 安全手册. Osborne/McGraw-Hill, 2001.
- Feuerstein, Steven, Charles Dye, and John Beresniewicz. Oracle 内置程序包. O'Reilly & Associates, 1998.
- Brown, Bradley D. Oracle 9i Web 开发. Osborne/McGraw-Hill, 2001.
- Loney, Kevin and Marlene Theriault. Oracle 9i DBA 手册. Osborne/McGraw-Hill, 2001。（之前的版本 Oracle DBA 手册也很好。）
- Finnigan, Peter. 步步为 Oracle 安全. SANS 学院 (http://store.sans.org)。

## 解决方案快速通道

### 攻击监听器 (Listener)

- 监听器会向询问者泄露信息。
- 监听器可以通过多种方式被远程破解。
- 针对缓冲区溢出漏洞的利用。
- 加载操作系统库并执行函数。
- 监听器默认是不安全的。
- 它可以很容易地被安全。

### 攻击数据库

- 数据库服务器有大量的默认用户 ID 和密码。
- 数据库服务器存在多种缓冲区溢出漏洞。
- 左外连接查询可以绕过表权限。
- PL/SQL 会引发安全漏洞。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_749_0.png)

拥有 `CREATE PROCEDURE` 权限的用户可以执行任意 Java。

### 攻击 Oracle 应用服务器

- 最新版本的 Oracle 应用服务器存在一系列安全漏洞。
- WebDAV 默认启用。
- DAV 模块中存在格式字符串漏洞。
- iSQL*Plus 中存在缓冲区溢出漏洞。

### 防御 Oracle

- 新漏洞将不断被发现。
- 使用最佳实践来降低带来的风险。
- 加固监听器是第一步。
- 开启 TCP 节点有效检查。
- 设置服务账户；使用低权限的操作系统账户。
- 密切关注新警和补丁，并尽快安装。

## 常见问题

以下由本书作者回答的常见问题旨在衡量你对本章所介绍概念的理解程度，并帮助你在现实生活中实施这些概念。如果您对本章有任何问题想让作者回答，请访问 **www.syngress.com/solutions** 并点击“询问作者”表单。

- Q：Microsoft SQL Server 和 Oracle 哪个更安全？
A：都不能。它们各有优劣。我经常听到人们因为微软的安全失败从 SQL Server 迁移到 Oracle，但 Oracle 也有类似的记录。

- Q：Oracle 的“不可摧毁”营销活动如何？
A：根据 Oracle 内部消息人士，该活动讨论的不是安全性，而是指在使用集群时业务是不可摧毁的。100% 的可用时间意味着“业务”是不可摧毁的。此外，该活动体现了 Oracle 对安全的承诺。多个 Oracle 版本已经通过了 14 次独立安全评估。当前版本尚未通过该评估。

- Q：为什么我不能再以 "internal" 身份连接了？
A：此功能在 Oracle 9i 中已禁用。

- Q：Oracle 密码是如何加密的？
A：Oracle 密码使用数据加密标准 (DES) 算法加密，生成八字节哈希值并存储在 SYS.USER 表中。为了创建哈希，将用户名和密码拼接并分成八字节的小节。密码的前八字节被用作密钥通过 DES 加密魔数 0x123456789ABCDEF，生成的字节再用用户名/密码的后续字节进行加密，生成一个新的八字节值。重复此过程，直到整个用户名/密码都被使用完毕。

一个值得注意的有趣特征是创建哈希值时使用的“盐”（salt）。盐就是用户名。这增加了额外的安全性，因为具有相同密码的不同用户具有不同的哈希值。然而，它还没有达到真正的盐的效果，因为同一个密码在被同一用户使用时，哈希值始终是相同的值。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_751_0.png)

## 第 14 章

## 攻击与防御 Unix
作者 Hal Flynn

本章解决方案：

- 攻击 Unix
- 工程化一个安全的 Unix 系统
- 针对特定平台的配置
- 加固继承的系统

相关章节：

- 第 18 章：创建有效的安全策略
- 总结
- 解决方案快速通道
- 常见问题

729

## 引言

在企业环境中，典型的异构网络上存在许多多样化的系统。通常，Unix 系统是其中的很大一部分。在企业环境中，有多个服务于特定、个人用途的 Unix 系统并不罕见。这些系统虽然在平台和操作系统类型上有所不同，但面临着类似的默认配置问题和新发现的漏洞，并且需要工作来维护它们的完整性。

本章将从对攻击 Unix 的简要讨论开始。在第一节中，我们检查使用信息收集攻击。随后，描述了针对 Unix 系统的常用攻击，例如利用编程错误和输入验证错误。

接下来，我们研究如何安全地安装 Unix，包括获取有效介质、安装主机以及配置系统以维护完整性的必要步骤。我们还研究了可以用于使主机更安全的特性，并介绍了对继承系统的完整性验证和加固。

## 攻击 Unix

正如作战部队在发起攻击前需要目标的情报报告一样，明明的攻击者在尝试破解主机之前需要关于站点的信息。操作员在被投送到某地完成任务之前，会想要地图、兵力、武器和目标信息，一个

