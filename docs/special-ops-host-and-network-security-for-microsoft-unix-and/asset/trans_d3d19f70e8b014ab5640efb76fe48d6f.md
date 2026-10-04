

# 保护 Exchange 和 Outlook 网页访问的安全 • 第 7 章 365

smtpgate.soromita.com 使用 Microsoft SMTPSVC (5.0.2195.4905); Wed, 7 Aug 2002 05:59:31-0700

接收自 hnlex01.pacific.soromita.com ([192.168.1.42]) 通过 sfe0x4.numerica.soromita.com (InterScan E-Mail Woost NT); Wed, 07 Aug 2002 05:59:48-0700

接收自 hnlex03.pacific.soromita.com ([192.168.23.8]) 通过 hnlex01.pacific.soromita.com 使用 Microsoft SMTPSVC (5.0.2195.5329); Wed, 7 Aug 2002 05:59:29-0700

```
x-mimeole: Produced By Microsoft Exchange V6.0.6249.0
content-class: urn:content-classes:message
MIME-Version: 1.0
Content-Type: multipart/mixed;
boundary="----_NextPart_001_01C23E12.42DD6818"
```

主题: 新长板的订单
日期: 7 Aug 2002 07:59:27-0000
Message-ID: <90FDFC1EC02B2147B94B8A1IP77C182F05308260@hnlex03.pacific.soromita.com>
X-MS-Has-Attachment: yes
X-MS-Correlator:\Thread-Order: 新长板的状态
Thread-Index: AC1SqFykv6mTMpRO6+vvSVTufMeq==
From: <Suriya Supanasakul <<SSuriya@soromita.com>
To: <Bessara, Robert* <<Bessara@BobsBoogleBoards.com>

注意，您可以通过查看最早的主机和 IP 地址来追踪消息的来源路径。在这种情况下，消息源于名为 HNLEX03 的服务器，IP 地址为 192.168.23.8。随后它被传输到另一个名为 HNLEX01 的内部服务器，然后传输到 SFOEX04 的服务器，最后传输到组织的 SMTP 网关 (SMTPGATE)。

Exchange 2000 目前没有可以允许您重写或清除 SMTP 头的解决方案（这可以通过 SMTP 接收器（sink）来实现）。我不建议清理内部传输消息的 SMTP 头部，因为这可能会使邮件传输问题变得更加复杂。然而，我建议找到在消息离开您的组织之前清除其头部的方法。目前支持此功能的两个产品包括思科防火墙 (www.cisco.com)、Check Point 的 Firewall-1 (www.checkpoint.com) 以及 Clearswift Mail Sweeper (www.mimeseeper.com)。其他供应商已计划在未来的防火墙和 SMTP 扫描器中提供支持。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_389_0.png)

# 针对可能的安全泄密的审计

审计 Exchange 2000 是至关重要的。如果您目前没有审计您的 E2K 系统，您可能甚至没有意识到正面临安全问题。更糟糕的是，您可能发现自己存在安全问题，但可能甚至无法追踪到源头。审计可分为几类：Windows 2000 事件审计、Exchange 2000 事件审计以及对 Internet协议使用的审计。

# Windows 2000 事件审计

您需要利用的必备安全审计工具之一是内置的 Windows 2000 事件审计，您可以通过本地安全策略进行配置，或者通过 Active Directory 组对象（Group Object）对整个 OU（组织单元）的计算机进行批量配置。图 7.24 显示了我倾向于配置的典型审计策略事件。

图 7.24 Exchange 服务器的审计策略

![](img/729efc56f204a2ebffb8295c3a2dfdfb_390_0.png)

我选择审计的事件通常会告诉我何时有人访问了服务器、对服务器进行了安全或账户相关的更改，以及何时可能重启了服务器。表 7.12 显示了我倾向于记录的事件及其解释。

# 保护 Exchange 和 Outlook 网页访问的安全 • 第 7 章 367

### 表 7.12 推荐审计策略事件

| 策略 | 解释 |
|---|---|
| 审计账户登录事件 | 审计使用域账户的登录。审计账户更改，例如重重置或组成员更改。审计事件并不总是能生成我所需的详细信息（例如账户是启用还是禁用），仅显示账户发生了更改。 |
| 审计登录事件 | 审计使用成员服务器本地账户的登录 |
| 审计策略更改 | 审计策略的更改，例如更改审计策略 |
| 审计系统事件 | 审计如系统关机或重启等事件 |

> Windows 2000 事件日志可能会迅速增长到相当大的体积。这些日志的默认大小为 512KB，并且会覆盖旧于七天的数据。管理员经常忽略审计日志已满的警告，随后又疑惑为什么审计日志中的信息不完整。请将您的审计日志大小增加到有用且合理的范围。对于一个托管 1,000 个邮箱箱的典型 Exchange 2000 服务器，我认为将日志文件设为 20,480KB (20MB) 甚至更大是不合理的。我强烈建议将所有服务器的最大事件日志大小增加到至少 20MB。

尽管我不喜欢配置一个涵盖服务器上发生的每项活动的审计策略，但我也避开极简审计以及仅检查失败情况的审计。您在服务器上设置的每项额外审计策略都会在某种程度上增加服务器负载，并增大安全日志文件的大小。如果您真正担心记录可能影响系统安全的事件，您将不会记录人们尝试完成某事但失败的事件，这直是我的哲学。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_391_0.png)

# 保护 Exchange 和 Outlook 网页访问的安全 • 第 7 章 367

有关 Windows 2000 事件审计的更多信息，请参阅第 5 章。

# Exchange 2000 事件审计

还有一些您应该为 Exchange 启用的事件。图 7.25 显示了 Exchange 服务器的诊断日志页面。在 Exchange 5 中，您可以在几个位置找到诊断日志页面，但在 Exchange 2000 中，这些事件集中在单个页面上。要启用 Exchange 的任何类型的诊断日志，您必须为每个服务器配置诊断日志页面。图 7.25 显示了诊断日志页面。

# 图 7.25 Exchange 诊断日志

![](img/729efc56f204a2ebffb8295c3a2dfdfb_392_0.png)

