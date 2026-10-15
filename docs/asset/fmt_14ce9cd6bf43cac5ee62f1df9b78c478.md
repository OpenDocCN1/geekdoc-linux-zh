
DKIM（DomainKeys Identified Mail）是电子邮件消息的加密签名系统。它让接收方不仅可以验证发送者的身份，还可以验证消息在传输过程中未被篡改。该系统使用 DNS 记录来发布域的加密密钥和消息签名策略。

原始的 DomainKeys 系统是 DKIM 的前身，提供类似功能并由 Yahoo! 主导。它仍在使用中。DKIM 和 DomainKeys 不会冲突，站点可以验证两种类型的签名。对于签署新消息，最好使用 DKIM。

ADSP（Author Domain Signing Practice）DNS 记录让发送方为每个子域声明其签名策略。例如，一家银行可能会声明它签署来自 `transactions.mybank.com` 的所有邮件。任何接收到声称来自该域但未签名或无法验证签名的邮件的人都应拒绝或隔离它。然而，`marketing.mybank.com` 可能根本不签署其消息。

一段时间以来，ADSP 被称为 SSP（sender signing policy），因此你可能仍会看到任一类型的 DNS TXT 记录。DKIM 由本章描述的所有 MTA 支持，但实际部署一直缓慢。我们不确定原因。

即使你不想基于 DKIM 或 SPF 验证失败而拒绝消息，你仍然可以使用这些信息来提高消息的垃圾邮件分数或根据发送者的声誉改变你的行为。

### MTA-specific antispam features

每个 MTA 都有配置选项可以帮助缓解垃圾邮件问题。例如，一些 MTA 可以确定它们被要求执行数以亿计的

RCPTs 并可以在滥用它们的连接之间引入例如 15 秒的延迟。

我们将在 MTA 配置的其他细节中与垃圾邮件相关的配置选项一起介绍。对于 sendmail，请参阅第 789 页；对于 Exim，请参阅第 818 页；对于 Postfix，请参阅第 840 页。DKIM 和 ADSP 在本章第 845 页以及第 590 页开始的第 17 章中有更详细的讨论。

### MailScanner

Julian Field 的 MailScanner（`mailscanner.info`）是一个积极维护的、灵活的、开源的邮件枢纽扫描器；它可以识别垃圾邮件、病毒和钓鱼尝试。它用 Perl 编写，使用外部的防病毒（ClamAV 和其他 25 种工具）和反垃圾邮件（SpamAssassin）软件。其反钓鱼组件名为 ScamNailer（`scamnailer.info`），是独立的，不依赖于 MailScanner。你可以以用户、域或 IP 地址的粒度调整 MailScanner 的配置规则集。

MailScanner 不是 milter，而是一个独立的程序，运行在 MTA 的邮件队列上。例如，你可以配置 DMZ 中的 MTA 接受消息（在与 milters、黑名单等进行内联检查后）并将它们放入入站队列。你让 MailScanner 从该队列读取消息，进行反垃圾邮件、反病毒和反钓鱼处理，然后将通过检查的消息转移到单独的出站队列。另一个 MTA 实例可以随后处理出站队列并投递消息。

这种系统的一个缺点是，被 MailScanner 拒绝的邮件会产生退信消息，因此可能导致回弹垃圾邮件的产生。

尽管 MailScanner 是免费的，但提供商业支持。它还拥有活跃的用户邮件列表和一个全天候 24/7 监控的专用 IRC 频道。它在网上以及 Julian Field 所著的书籍 *MailScanner: A User Guide and Training Manual* 中都有完善的文档。MailScanner 的配置文件附带了大量注释，以至于配置原语几乎被淹没；一旦你成为专家，你可能想要删除一些样板内容。

你可以通过名为 Mail-Watch 的 Web 前端从 MailScanner 捕获统计数据。MRTG 可以绘制数据图表，如下页的展品 C 所示。请注意 9 月 19 日发生的巨大峰值，可能是一种攻击。

### amavisd-new

`amavisd-new` 是 MTA 与各种病毒和垃圾邮件扫描器（如 ClamAV 和 SpamAssassin）之间的接口。它最初基于 AmaViS（A Mail Virus Scanner），但与原版已几乎没有共同之处。它用 Perl 编写，由 Mark Martinec 开发；网站为 `jjs.si/software/amavisd`。我们遵循维护者的惯例，将整个软件包称为加粗的 `amavisd-new`；然而，守护进程本身称为 `amavisd`。

### Exhibit C MRTG graph of mail traffic

![](img/14d78e3cecac4581d37024baf1e94cca_818_0.png)

`amavisd-new` 通过本地域或 TCP 套接字与 MTA 通信。它可以在内联过滤（用作 milters，在 MTA 接受消息之前）或在消息已被接受但在投递给收件人之前进行过滤。

当你的 MTA 可以使用 milters 等自行扫描时，为什么还要使用另一块软件？一个答案是，将所有过滤器的配置集中在一个地方很方便。如果所有过滤都通过一个接口协调，也更有可能更容易应对新攻击或包含新工具。另一个好处是扫描器可以运行在单独的机器上，从而分担繁忙服务器接收和处理消息的负载。一个不错的折中方案是在 MTA 中进行简单、快速的检查，然后将更昂贵的检查交给 `amavisd` 这样的工具。

`amavisd` 可以与许多反垃圾邮件和反病毒扫描包接口。它功能强大但也有几个缺点：

- 文档有点分散，不清楚什么内容是当前的，什么内容是旧的且不再正确。

- 配置很复杂。有很多参数以及那些参数的细微不同的变体。

#### How amavisd works

`amavisd` 介于持有待审核消息的 MTA 和实际执行检查的软件之间。`amavisd` 在 TCP 端口 10,024 上监听来自 MTA 的连接，使用 SMTP 或 LMTP 接收消息，并在端口 10,025 上向 MTA 返回其答案。它也可以使用本地域套接字，如果它与 MTA 运行在同一台机器上。

如果 amavisd 将扫描后的邮件和结果交还给最初接收该邮件的 MTA，则可以在线路上进行过滤，并在 MTA 的初始 SMTP 会话期间拒绝邮件。如果 amavisd 反而将邮件排队到内部邮件枢纽，则过滤为离线处理，违规邮件可以被丢弃或退回。

有关 SNMP 的更多信息，请参阅第 21 章。

amavisd 非常注重不丢失邮件，不让邮件未经检查就溜走，尊重各个收件人的意愿，并遵循各种电子邮件相关 RFC 中规定的标准。尽管是用 Perl 编写的，amavisd 的性能相当不错。它只扫描每封邮件一次，无论与之关联的收件人有多少。日志可以非常详细，发行版中的工具可以通过 SNMP 监控过滤。amavisd 不需要以 root 身份运行，并且拥有良好的安全记录。

### amavisd 安装

从 `jims.is/software/amavisd` 下载最新版本的软件，或获取 Linux 软件包并跳过分发层级顶部的 INSTALL 文件中详细说明的步骤。项目主页提供了指向预编译软件包的链接。amavisd 预计以用户和组 vscan 或 amavis 运行，因此最简单的方法可能是创建该用户和组，然后以 vscan 身份登录以获取软件并安装它。在你正确安装并运行 amavisd 后，将该账户的登录 shell 更改为 `/bin/false` 或其他受限 shell。

文件 `amavisd.conf-default` 包含每个可能的配置参数及其默认值。`amavisd.conf-sample` 是一个更典型的带注释的示例配置文件。最后，`amavisd.conf` 是一个最小的起点（但仍超过 750 行！），其中包含一些必须更改的变量的注释。配置语言是 Perl。

### 基本 amavisd 配置

以下是主机名为 `mail.example.com` 的基本 amavisd 配置，其中 MTA 和 amavisd 在同一台机器上运行，并使用 TCP 和 SMTP 协议相互通信。

```
use strict;

$myhostname = 'mail.example.com';
@local_domains_maps = ({'example.com'});
@mynetworks = qw[127.0.0.0/8 192.168.0.0/16];

$forward_method = 'smtp:[127.0.0.1]:10025';
$enable_db = 1;
$enable_global_cache = 1;
$max_servers = 5;
$DO_SYSLOG = 1;
$SYSLOG_LEVEL = 'mail.info';
$bypass_decode_parts = 1;
```
