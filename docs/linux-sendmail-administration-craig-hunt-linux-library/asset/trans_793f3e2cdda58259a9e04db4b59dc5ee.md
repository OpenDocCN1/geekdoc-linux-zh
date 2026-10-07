
EXPOSED_USER (username) 此宏在发送者地址的用户部分与 `username` 匹配时，禁用伪装（masquerading）。某些用户名（如 root）在许多系统中出现，因此在整个域内内是不唯一的。对于这些用户，转换地址的主机部分将无法判断邮件的真实来源，并导致无法回复。此命令防止 `MASQUERADE_AS` 命令对特定用户的发送者地址产生作用。这与在 `sendmail.cf` 文件的类中设置值相同。

还有若干项影响中继（relaying）和伪装的特征。我们已经讨论过 `FEATURE(stickyhost)`。其他与伪装相关的特征包括：

- FEATURE(masquerade_envelope) 此特征使信封地址（envelope addresses）以与发送者地址相同的方式进行伪装。该命令的示例请参见第 9 章。

- FEATURE(allmasquerade) 此特征以与发送者地址相同的方式伪装接收者地址。因此，如果发送者地址的主机部分符合 `MASQUERADE_AS` 命令的要求，它就会被转换。除非你确定本地系统已知的每一个别名都被处理该伪装域的邮件服务器所知，否则请使用此特征。

- FEATURE(limited_masquerade) 此特征将伪装限制在类 `M` 中定义的主机。在类 `w` 中定义的主机不进行伪装。

- FEATURE(masquerade_entire_domain) 此特征对整个 `MASQUERADE_DOMAIN` 内的所有主机进行伪装。如果不使用此特征，则只有与 `MASQUERADE_DOMAIN` 定义的值完全匹配的地址会被转换。如果使用此特征，则所有以 `MASQUERADE_DOMAIN` 定义的值结尾的地址都会被转换。例如，假设定义了 `MASQUERADE_AS(foobirds.org)` 和 `MASQUERADE_DOMAIN(foobirds.org)`。如果设置了 `FEATURE(masquerade_entire_domain)`，则发出的邮件中 `swans.foobirds.org` 的每个主机名都会被转换为 `foobirds.org`。否则，只有名为 `swans.foobirds.org` 的特定主机会被转换。

某些特征定义了邮件服务器作为中继服务器时如何处理邮件。这些特征在第 11 章中描述：

- FEATURE(access_db) 将用户、域名或 IP 地址映射到关键字，该关键字告诉 `sendmail` 如何处理针对该主机、域或网络的中继。此数据库在第 11 章中使用。

- FEATURE(blacklist_recipient) 使用访问数据库根据接收者地址控制邮件投递。`access_db` 特征根据邮件来源控制中继和投递。此特征增加了了根据目的地控制邮件中继和投递的能力。

- FEATURE(dnsbl1) 根据 DNS 黑名单（DNS blacklist）控制邮件投递。DNS 数据库中列出的源地址和目的地址可能会被拒绝邮件投递或中继服务。

- FEATURE(promiscuous_relay) 从任何站点向任何站点中继邮件。通常情况下，Sendmail 不中继邮件。使用此特征是一个坏主意，因为它让你成为垃圾邮件发送者的可能中继服务。

- FEATURE(relay_entire_domain) 从类 `M` 中定义的任何域向任何站点中继邮件。

- FEATURE(relay_hosts_only) 从访问数据库或类 `R` 中定义的任何主机中继邮件。

- FEATURE(relay_based_on_MX) 从你的系统作为 MX 服务器的任何站点中继邮件。

- FEATURE(relay_local_from) 中继发送者地址包含你的本地域名的邮件。

警告 邮件中继可能被垃圾邮件发送者和伪造者滥用。请谨慎使用。

入站邮件也可以进行过滤以减少垃圾邮件发送者的影响。为此目的有两个宏可用：

MAIL_FILTER(`name`, `equates`) 此宏使用 Sendmail Mail Filter API 语法定义邮件过滤器。

INPUT_MAIL_FILTER(`name`, `equates`) 此宏定义邮件过滤器并设置该邮件过滤器的调用。

源文件还用于与 DNS 密切相关的特征和宏。这些特征包括：

- FEATURE(unqualified_senders) 此特征即使发送者地址不包含主机名，也接收来自该网络的邮件。通常，不带主机名的登录邮件是不接受的。这是一个危险的特征，应只在隔离的网络上使用。

- FEATURE(unresolvable_domains) 此特征接收无法 DNS 解析的主机名。这是一个危险的特征，仅在缺乏完整 DNS 服务的系统上。

- FEATURE(always_add_domain) 此特征将主机添加到所有本地邮件。在名为 `ibis.foobirds.org` 的服务器上启用此特征后，从 `craig@ibis` 到 `kathy@ibis.foobirds.org` 的邮件会被投递。

- FEATURE(bestmx_is_local) 使用此特征，任何作为其 MX 服务器的站点都会被 Sendmail 服务器接受为本地邮件。

DNS 宏：

- CANONIFY(domain) 此宏定义一个域名，在启用 `canonify` 特征时，通过 DNS 将其转换为规范形式（canonical form）。在 DNS 中存储的主机名通过此宏转换为规范名。

- CANONIFY_DOMAIN_FILE(filename) 此宏标识一个包含列表的文件。

# MAILER

Mailer 指向一个 m4 源文件。此宏标识一个包含列表的文件。

Mailer 指向一个列表。

本节描述的宏和特征不仅限于：

- pop | 邮局协议 (POP) 支持。
- procmail | procmail 的接口。
- mail11 | DECnet mail11 。
- phquery | 用于电话簿的 phquery 程序。
- qpage | 用于向传真机发送邮件的 QuickPage 。
- cyrus | cyrus 和 cyyrusbb 。

你的宏配置文件应包含 `MAILER(local)` 和 `MAILER(smtp)` 条目。选择 local 和 smtp 提供了标准 TCP/IP 安装的所有内容。其他特征有：

- uucp 为直接连接到 UUCP 网络的系统提供 UUCP 邮件支持。uucp-old 支持标准的 UUCP 邮件，而 uucp-new 适用于一次传输处理多个接收者的远程站点。如果你的系统同时拥有 TCP/IP 和 UUCP 连接，请在 `MAILER(smtp)` 之后指定 `MAILER(uucp)`。
