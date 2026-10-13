
- Linux WWW HOWTO（http://www.linuxdoc.org/HOWTO/WWW-HOWTO.html）
- Apache 网站（http://www.apache.org/）
- Linux.com Web 服务器列表（http://www.linux.com/links/Software/Web_servers/）
- 万维网联盟（http://www.w3.org/）

## Linux 作为数据库服务器

直到不久以前，Linux 尚未获得广泛认可的领域之一是数据库服务。Linux 长期以来拥有全套免费的关系数据库软件包，包括著名的 PostgreSQL（简称 Postgres）、mSQL 和 MySQL。

然而，自 1998 年以来，这种情况已逐渐改变。大多数主要的商业数据库厂商现在都提供其产品的 Linux 版本，包括 Oracle、Sybase 和 Informix。这使 Linux 进入了可扩展、全面支持的数据库平台领域，并使其成为那些希望将部分或全部后端处理迁移到基于 Linux 的系统的组织的一个可行选择。

以下是 Linux 上一些领先的商业和免费数据库平台：

- **IBM：** IBM 的 DB2 数据库服务器可用于 Linux。它提供 Java 支持，并且据称具有很高的可扩展性。该软件的免费开发与测试版本可从 http://www.software.ibm.com/data/db2/linux 获取。
- **Informix：** Informix 在 Linux 商业数据库平台中排名前五。该公司提供两款 Linux 服务器：Informix SE——一款免费提供的小规模数据库系统；以及 Informix Dynamic Server Linux Edition Suite——一个更强大的数据库环境。完整细节请访问 http://www.informix.com/。
- **Mini SQL：** Mini SQL，简称 mSQL，是 Linux 上最知名、使用最广泛的关系数据库之一。mSQL 最初是共享软件，可免费用于非商业和教育用途；如今已发展为一款价格适中、高效的商业产品，并仍在 http://www.hughes.com.au/ 免费提供非商业和教育用途。
- **MySQL：** MySQL 是一款来自瑞典的关系数据库服务器，可免费用于非 Microsoft 系统。只要服务器不被出售、安装不收费，且软件不包含在商业发行版中，就无需付费。MySQL 以卓越性能著称，可从 http://www.mysql.com/ 下载。
- **PostgreSQL：** PostgreSQL 被认为是 Linux 上以开源许可证提供的最稳健的服务器。PostgreSQL 可从 http://looking-glass.usask.ca/ 下载。
- **Oracle：** Oracle 是顶级数据库厂商，按某些统计口径，它是企业数据库市场的领导者。Oracle 传统上只在商业 Unix 和 Windows NT 系统上提供，现在则提供其旗舰产品 Oracle 8 数据库系统的 Linux 版本。可从 http://platforms.oracle.com/linux/index_lx.htm 获取免费的 30 天试用版。
- **Sybase：** 作为排名前五的数据库厂商之一，Sybase 在 Linux 上免费提供其 Adaptive Server Enterprise（ASE）产品。ASE 几乎不受限制，可用于 Linux 系统上的任何用途。更多信息请访问 http://www.sybase.com/。

有关将 Linux 部署为数据库服务器的详细讨论，请参阅第 24 章“Linux 数据库服务器”。

## Linux 作为新闻服务器

许多企业内联网的一个常见功能是某种形式的讨论论坛，例如 Microsoft Exchange 或 Lotus Notes 所提供的论坛。互联网标准的 NNTP 协议是互联网上著名的 Usenet 新闻组网络的基础。

新闻组提供非实时讨论。也就是说，用户可以随时发布帖子，然后随时阅读其他帖子，因为帖子会保留在组内供以后阅读和参考。这与聊天系统形成对比，聊天系统要求参与者之间进行实时互动。

在 Linux 系统上，NNTP 服务通过 INN 软件包提供。有关 INN 新闻服务器的安装和管理，请参阅第 26 章“新闻服务”。

## Linux 作为邮件服务器

邮件服务通常分为两个部分：

- **邮件用户代理（MUA）：** MUA 通常是用户看到的邮件客户端软件，如 Eudora、Pegasus、Pine、Netscape Messenger 或 Outlook Express。
- **邮件传输代理（MTA）：** MTA 是后端服务器系统，为 MUA 提供邮件投递和存储功能。

在互联网术语中，MTA 使用简单邮件传输协议（SMTP）来路由和投递电子邮件。互联网电子邮件系统中的大部分邮件都通过基于 SMTP 的 MTA 进行路由。

在 UNIX 世界（包括 Linux）中，领先的 MTA 是 sendmail。作为占主导地位的 MTA，sendmail 不仅被广泛部署，而且其复杂性和功能也在不断增长，以满足这一庞大用户群的多样化需求。这种复杂程度体现在：大多数邮件管理员从不试图精通 sendmail，而是依赖印刷参考资料。事实上，有整本书专门介绍 sendmail 系统的安装、配置和维护。

许多 Linux 发行版都带有 sendmail 系统。第 16 章“使用 sendmail 的 Linux 邮件服务”更深入地介绍了基于 sendmail 的邮件服务器的安装和实现。除 sendmail 外，Linux 还有其他几种 MTA 可用，它们提供更好的安全性、性能或简化的配置和管理。这些包括：

- **smail：** smail 在 Linux 世界中广泛用作 MTA。对于大多数安装场景，它提供比 sendmail 更简单的配置。
- **qmail：** qmail 专注于安全性，试图解决 sendmail 中众所周知的安全漏洞。qmail 尽量避免隐藏漏洞，并力求提供卓越的投递可靠性，同时将收件箱损坏的可能性降至最低。

## 硬件需求

要评估内联网的硬件需求，没有简单的方法。这在很大程度上取决于你计划提供的内联网服务数量、用户数量以及他们的使用程度。

尽管如此，以下几点准则仍然适用：

1. 除非你在运行一个极小的内联网，否则你不希望在同一台 Linux 系统上运行多个内联网服务。也就是说，为 Web、数据库、新闻和邮件服务器提供独立的硬件是明智之举。这不仅提供了更好的性能和扩展空间，还消除了单点故障。如果你在没有冗余系统的情况下将所有服务运行在单个系统上，并且系统硬件发生故障，那么所有服务都会失败，而不是只有一个服务失败。
2. 如果你的硬件预算允许，可以通过运行至少两台 Web、数据库、新闻和邮件服务器来实现冗余。对于数据库和新闻服务器，所有服务都可以进行自动数据镜像。多台服务器可以分担负载，当一台服务器发生故障时，另一台可以在你修复或更换故障服务器的同时接管工作。这可以帮助你实现接近 100% 的正常运行时间。
3. 新闻服务器往往有较高的硬件需求。如果你计划建立本地新闻组，并部分订阅互联网新闻组，那么一台单处理器 Pentium 300、配备 256MB 内存和 16GB Ultra Wide SCSI-2 硬盘空间应该就能满足需求。如果你想为内联网用户提供完整的互联网新闻订阅，可能需要高达 4 个 CPU、2GB 内存和 1 TB 磁盘空间。将新闻服务器与其他内联网服务共用是极不明智的。第 26 章将详细讨论新闻服务器。
4. Web 服务器的性能主要取决于可用 RAM，尤其是在 Web 服务器上部署了交互式或数据驱动应用程序的情况下。目标是防止 Web 服务器上发生任何内存交换，因为这会显著影响最终用户的性能体验。快速的 CPU 和网卡很重要，但如果它们的成本意味着可用 RAM 将不够充足，就不应使用。第 23 章将详细讨论 Web 服务器。
