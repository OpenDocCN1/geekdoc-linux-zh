
![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_636_0.png)

# Linux 系统管理手册

5: Date: Fri, 5 Nov 1999 06:31:10 -0100 (Etc/GMT)
6: Received from: login.011556.wgukas.com (mail.wgukas.com) [233.214.241.87] nby (8.5/8.7) with SMTP XAA01510 for faklin321@thaxghlo.um.de;
Thu, 4 November 1999 02:21:59 -0700 (EDT)

7: To: mrktnet77@kayak.msk.ru
8: Subject: Just Released! Millions CD Vol. 6A
9: Comments: Authenticated Sender is <user11556@wgukas.com>
10:Message-ID: 020210872648597456-sa_ghklou.um.

请勿回复此邮件 -
如需从未来的邮件列表中移除：
mail.greg1148@usa.net?Subject=Remove

第 1 行是在本地交付期间由 `/bin/mail` 添加的。域名 `msk.ru` 存在，但主机 `kayak.msk.ru` 不存在；如果该站点在使用分拆 DNS，那么这将是合法的。第 2 行是一个有效的 `Received` 行——它是唯一准确性有保证的 `Received` 行，因为它是由我们自己的主机（在此为 `xor`）添加的。第 3 行是 `sendmail` 添加的 `From` 头部，因为邮件最初没有该头部。第 4 行是来自毫无防备的主机（`gaia.es`）的有效 `Received` 行，该主机运行 `sendmail 8.8`，在该版本默认允许中继（以及以何种方式）。第 4 行中的“default”是下一个 `Received` 行是伪造的线索。第 6 行是一个伪造的 `Received` 行。它位于 `Date` 之下，当 `sendmail` 接收邮件时它要么缺失，要么已经就位。格式是错误的，这通常是一种篡改。IP 地址 `233.214.241.87` 没有反向 DNS。在过去研究和学术互联网的时代，这本是一个出问题的线索。今天，许多主机没有反向 DNS 目。第 7 行中，收件者地址仅在信封上。第 9 行识别了经过验证的发送者，这有时是邮件来源的线索。这暗示 `wgukas.com` 是发送者，除非在发送者处的伪装改变了情况。第 10 行是伪造的。`msk.ru` 域名存在，但主机 `kayak.msk.ru` 不存在；如果该站点在使用分拆 DNS，那么这将是合法的。`xor.com` 是真实的原始。`gaia.es` 可能是发送者。`saturn.global.com` 可能是开放中继。第19 章 电子邮箱

# 第 19 章 电子邮件

它将其重命名到垃圾邮件文件夹中，你可以在设置和调整参数时检查它。请访问 spamassassin.tain.org 查看。

## 19.11 SENDMAIL SENDMAIL 安全性

随着互联网的爆炸式增长，诸如 `sendmail` 这样带有用户提供的输入并投递到本地用户、文件或 shell 的程序，经常为黑客提供攻击途径。`sendmail` 与 DNS 甚至 IP 一样，正在尝试将身份验证和加密作为解决这些基础安全问题的内置解决方案。

最近美国对加密出口法律的放宽允许 `sendmail` 在出厂时附带了内置的加密钩子。版本 8.11 及更高版本支持 SMTP 身份验证和 TLS 加密（传输层安全协议，以前被称为 SSL，即安全套接层）。`sendmail` 在此语境下使用 TLS 术，并作为扩展实现了它。对于 SMTP 协议，STARTTLS 带来了其针对证书文件和密钥的新配置选项。访问数据库匹配的新操作可能要求认证必须成功。

在本节中，我们将描述 `sendmail` 权限、所有权和隐私保护的演变。然后我们将讨论 TLS 和 SASL（简单身份验证和安全层）及其在 `sendmail` 中的使用。

`sendmail` 随着时间的推移逐渐收紧了安全性，现在它在相信转发（forward）或别名（aliases）内容之前对文件权限非常挑剔。尽管这种安全收紧已成为常态，但有时有必要放宽这些严格的新策略。为此，`sendmail` 引入了 `DefaultAlias` 选项，希望该名称能提示管理员他们正在考虑的内容是不安全的。

此选项有许多可能的值——最后计数有 35 个。默认值是安全的。关于值的列表……请使用 `sendmail` 发行版中的 `doc/op/ps`。O'Reilly 的 `sendmail` 书第二版中没有列出这些值，但第三版中一定会有，或者直接将该选项设置为安全。

## 所有权

在 `sendmail` 世界中，三个用户账户非常重要：`DefaultUser`（默认用户）、`TrustedUser`（信任用户）和 `RunAsUser`（运行用户）。

默认情况下，除非邮件传输器另有指定，否则所有 `sendmail` 都会以 `DefaultUser` 身份运行。如果 `/etc/passwd` 文件中存在 `mail`、`sendmail` 或 `daemon` 用户，则 `DefaultUser` 将为此。否则，默认为 UID 1 和 GID 1。我们建议使用 `mailaccount` 和 `mailgroup`。使用星号 `*` 作为密码添加它：没有有效的 shell，没有主目录，且默认组为 `mailnull`。你必须将 `mailaccount` 条目添加到 `/etc/group` 文件中。`mailaccount` 不拥有任何文件。如果 `sendmail` 不以 root 身份运行，则 `mailuser` 将设置为 setuid。

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_640_0.png)

# Linux 系统管理手册

如果设置了 `RunAsUser`，`sendmail` 会忽略 `DefaultUser` 的值，并以 `RunAsUser` 身份执行所有操作。如果你正在运行 setgid 的 `sendmail`（到 `smsp`），那么提交过程将通过 SMTP 将消息传递给真实的 `sendmail`。真实的 `sendmail` 没有设置 set 位，但它从启动文件中以 root 身份运行。

`sendmail` 的 `TrustedUser` 可以拥有映射文件和别名文件。`TrustedUser` 被允许启动守护进程或重建 `aliases` 文件。此机制的存在是为了支持 `sendmail` 的 GUI 界面，这些界面需要为某些用户提供有限的权限控制。如果你设置了 `TrustedUser`，请确保保护它指向的账户，因为该账户可能被利用以获取 root 权限 `TrustedUser` 不同于 `TRUSTED_USERS` 类，后者决定谁可以重写消息中的行。

`RunAsUser` 是 `sendmail` 在打开到 25 端口的套接连接时运行的 UID。小于 1,024 的端口只能由超级用户打开；因此，`sendmail` 从启动文件中以 root 身份运行。

`sendmail` 的 `TrustedUser` 可以拥有映射文件和别名文件。`TrustedUser` 被允许启动守护进程或重建 `aliases` 文件。此机制的存在是为了支持 `sendmail` 的 GUI 界面，这些界面需要为某些用户提供有限的权限控制。如果你设置了 `TrustedUser`，请确保保护它指向的账户，因为该账户可能被利用以获取 root 权限 `TrustedUser` 不同于 `TRUSTED_USERS` 类，后者决定谁可以重写消息中的行。

`RunAsUser` 是 `sendmail` 在打开到 25 端口的套接连接时运行的 UID。小于 1,024 的端口只能由超级用户打开；因此，`sendmail` 从启动文件中以 root 身份运行。

### 权限

文件和目录权限对于 `sendmail` 至关重要。

表 19.16 权限

| 路径 | 所有者 | 模式 |
|---|---|---|
| /var/spool/client | smmsp | 770 |
| /var/spool/mailqueue | RunAsUser | 700 |
| /var/spool/ | root | 755 |
| /etc/mail | TrustedUser | 644 |
| /etc/mail | TrustedUser | 755 |

# 第 19 章 电子邮件

### 表 19.17 PrivacyOption 变量的值

| 值 | 含义 |
|---|---|
| public | 不进行任何隐私/安全检查 |
| needmailhelo | 要求进行 SMTP HELO（识别远程主机） |
| noexpn | 不允许 SMTP EXPN 命令 |
| novry | 不允许 SMTP VRFY 命令 |
| needexpnhelo | 在没有 HELO 的情况下不扩展地址 (EXPN) |
| needvrfyhelo | 在没有 HELO 的情况下不验证地址 (VRFY) |
| noverb | EXPN 不允许使用详细模式 |
| restrictmailq | 仅允许 mqueue 目录的组查看队列 |
| restrictqur | 仅允许 mqueue 目录的所有者运行队列 |
| restrictexp | 限制通过 -bv 和 -v 标志显示的文件 |
| noernm | 添加身份验证警告（Authentication-Warning）标头（这是默认值） |
| noreceipt | 关闭成功返回回执的状态通知 |
| nobodyreturn | 在 DSN（投递状态报告）中不返回正文 |
| goaway | 禁用 SMTP 状态查询（EXPN, VRFY 等） |

- a. 当给出 EXPN 命令时，详细模式跟随转发，并提供有关用户邮件位置的更多信息。在任何暴露在外部的机器上，应使用 Noverb 或更好的是 noexpn。
- b. 除非是 root 或 TrustedUser，否则不允许。
- c. ETRN 是一种专为拨号主机设计的 SMTP 命令。它请求队列仅保留发送该主机的消息。

Hat 默认设置为警告，SuSE 设置为警告、needmailhelo、novry、noexpn 和 noverb。

# 运行 chrooted 监狱（针对极度偏执的者）

如果你担心 sendmail 对你文件系统的访问权限，你可以在 chrooted 监狱中启动它。在监狱中准备一个最小的文件系统，包括类似 /dev/null、/etc 基础文件（passwd、group、resolv.conf、sendmail.cf、任何映射文件、*）、sendmail 需要的共享库、sendmail 二进制文件、邮件目录以及任何日志文件。你可能需要反复调整该列表以达到完美状态。使用 chroot 命令启动受监狱限制的 sendmail。例如：

```
