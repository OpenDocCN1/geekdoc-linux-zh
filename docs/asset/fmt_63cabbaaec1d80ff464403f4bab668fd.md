
## 病毒扫描器

尽管普遍认为 Linux 能够免疫针对 Microsoft Outlook 用户的邮件病毒，但让 UNIX 邮件服务器允许通过感染邮件是有意义的。尽管 Ubuntu 默认不提供病毒扫描器，但一些流行的扫描器在 Ubuntu 仓库中可用。以 ClavAV 作为最典型的例子。

## 自动回复

自动回复会对收到的消息自动生成回复；它们通常用于通知收件人不在办公室。幸运的是，Ubuntu 默认不包含此类功能，但你可以从 Ubuntu 仓库中找到并安装类似 gnarly 的自动回复。如果你订阅了邮件列表，请注意来自账户的自动回复可能会给列表中的其他人带来极大困扰。在激活自动回复并离开办公室之前，请退出邮件列表。

## Microsoft Exchange Server 的替代方案

在微软产品尚未被开源软件取代的最后一个领域中，就是作为 Microsoft Exchange Server 的替代品。许多企业使用 Microsoft Outlook 和 Microsoft Exchange Server 用于访问电子邮件并提供日历、备忘录、文件共享和其他协作功能。行业内对 Exchange Server 的通用投诉集中在可扩展性、管理（特别是备份和恢复）以及许可费用上。

“即插用”（drop-in）替代方案需要与 Microsoft Outlook 兼容，因为它的目标是在使用 Outlook 的 Microsoft 桌面环境环境中替换 Exchange Server。“相似型”（work-alike）替代方案提供与 Exchange Server 类似的功能，但不提供对 Outlook 客户端本身的兼容性；后者是许多开源替代方案的典型特征。

存在多种“即插用”替代方案，但没有完全开源的，因为需要某种专有连接器为 Microsoft Outlook 客户端提供服务（或为 Linux Evolution 客户端提供 Exchange 服务）。对于 Outlook 兼容性，关键似乎在于实现 MAPI（微软消息应用程序接口）的完整、开放实现。这一目标很难实现，因为 MAPI 是一个文档记录较少的微软协议。对于仅限 Linux 的解决方案，许多替代方案缺失的要素是与 Exchange Server 提供的功能类似的可用组日历/调度系统。

当然，开源世界中这类功能的独立应用随处可见，但“群软件”的一个特点是其集中管理；另一个特点是所有组件可以共享信息。

以下章节将介绍几个可用服务器，从 Microsoft Exchange Server 本身开始，转向兼容性越来越低的应用程序。这些服务器均未由 Ubuntu 提供。

### Microsoft Exchange Server/Outlook 客户端

由于部署广泛，Exchange Server 和 Outlook 似乎是该行业的基准。它们提供了一个专有服务器，用于提供电子邮件、联系人、调度、公共文件夹、任务列表、日志记录和备忘录，并使用 Microsoft Outlook 作为客户端，MAPI 作为 API。如果你考虑 Microsoft Exchange 提供的“全套”功能，没有任何替代方案能提供 100% 与 Microsoft Exchange Server 完全相同的功能——即使是那些被视为即插用替代方案的方案。Microsoft Exchange Server 的主页为 www.microsoft.com/exchange/

### Communigate Pro

Communigate Pro 是 Microsoft Exchange Server 的专有“即插用”替代方案，提供电子邮件、网页邮件、轻级目录访问协议（LDAP）目录、Web 服务器、文件服务器、联系人、日历（第三方）、IP 电话（VoIP）和列表服务器。Communigate Pro MAPI 连接器允许从 Microsoft Outlook 和其他启用 MAPI 的客户端访问服务器。该服务器的主页为 www.stalker.com/

### Oracle Beehive

Oracle Beehive 可能是你能找到的最接近 Exchange 的替代品。它允许你通过即时消息、电子邮件、文件共享（工作空间）、日历和其他工具进行协作。Beehive 支持 Linux 平台，其主页为 www.oracle.com/products/middleware/beehive/index.html。

### Bynari

Bynari 提供了一组专有服务器，作为 Microsoft Exchange Server 的即插用替代方案，用于电子邮件、日历、公共文件夹、调度、地址簿、网页邮件和联系人。尽管它运行在 Linux 上，但除非配合 Evolution 和 Thunderbird 使用，否则不提供 Linux 客户端，且连接器为 Microsoft Outlook Online 提供服务。主页为 www.bynari.net/

### Open-Xchange

Open-Xchange 拥有良好的背景，曾由 Novell/SUSE 拥有并开发，直到后来独立成立了自己的公司。它基于开放标准工作，提供了多种协作选项，并根于 Linux。它可以与各种协议配合，使其可用连接性最好的套件之一。你可以在 www.open-xchange.com 获取开源版本。

### phpgroupware

`phpgroupware` 是用 PHP 编写的开源应用（配合 MySQL 或 postgresql 加上 Web 服务器以及 IMAP 邮件服务器使用）。`phpgroupware` 提供基于 Web 的日历、列表、地址簿、电子邮件、新闻头条和文件管理器。其模块化特性允许你根据需要插入各种组件。主页为 www.phpgroupware.org

### PHProjekt

`PHProjekt` 是用 PHP 编写的开源软件（配合 MySQL、PostgreSQL、Oracle 和 Microsoft SQL）。`PHProjekt` 提供日历、联系人管理器、时间卡系统、项目管理、在线聊天、讨论论坛、工单系统、电子邮件、文件、书签、投票系统、任务列表、提醒、搜索以及集成。主页为 www.PHProjekt.com/

### Horde

`Horde` 是一个基于 PHP 的框架。配合 HTTP 服务器（Apache、Microsoft IIS、Netscape）和 MySQL 数据库，`Horde` 提供了网页邮件、联系人管理器、日历、CVS 查看器、文件管理器、时间跟踪、邮件规则管理器、备忘录、任务、冲突、新闻组、论坛、错误跟踪、仓库和演示。主页为 www.horde.org/

## 参考文献

- www.sendmail.org/——Sendmail 主页。在这里你可以找到关于 Sendmail MTA 的配置信息。
- www.postfix.org/——Postfix 主页。在使用 Postfix MTA 时可以在该站点找到文档和示例配置。
- help.ubuntu.com/community/Postfix——Postfix 的社区文档。
- www.qmail.org/——Qmail MTA 主页。包含文档以及指向 Qmail 其他资源的链接。
- https://help.ubuntu.com/community/ClamAV——ClamAV 的社区文档。
- www.rfc-editor.org/——RFC（意见请求稿）库，定义了现代计算机使用的“规则”。
- www.procmail.com/——Procmail 主页。
- Sendmail (O'Reilly Publishing) 由 Brian Costales, Claus Assmann, George Jansen 和 Gregory Neel 著，ISBN: 0-596-51029-2——Sendmail 的事实标准指南。书中内容超过 1000 页，这让你了解 Sendmail 到底有多复杂。
- Postfix (Sams Publishing) 由 Richard Blum 著，ISBN: 0-672-32114-9——Sams 出版的关于 Postfix MTA 的优秀书籍。
- Postfix: The Definitive Guide (O'Reilly Publishing) 由 Kyle D. Dent 著，ISBN: 0-596-00212-2——Postfix 的另一份优质资源。
- Running (Sams Publishing) 由 Richard Blum 著，ISBN: 0-672-31945-4——这本书与 Sams 出版的 Postfix 书相似，不同之处它涵盖的是 Qmail MTA。

## 第28 章 代理、反向代理与虚拟专用网络 (VPN)

- 速度——你希望缓存常用网站以充分利用你的带宽。
- 安全——你希望监控人们的操作。

`Squid` 可以实现这些以及更多功能。

## 安装 Squid
