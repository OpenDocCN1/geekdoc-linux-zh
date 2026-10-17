
传统的 `mbox` 格式将所有分配到文件夹的邮件合并到一个文件中，并对单个文件进行索引（不，是单文件作为索引）。在 `maildir` 中，每个邮件文件夹有三个子目录：`/cur`、`/new` 和 `/tmp`。每封邮件保持在一个独立的文件。如果你为大量用户运行邮件服务器，你应该选择一个能够处理大量小文件的文件系统。

`mbox` 确实有一个主要缺点。当你访问包含所有邮件的单体 `mbox` 文件时，假设发生了某种类型的损坏，无论是文件本身还是索引，从这种问题中恢复可能会非常困难。如果 `mbox` 文件通过网络访问，它们特别容易出现问题并导致文件损坏；应该避免通过 `NFS`（网络文件系统）访问挂载的 `mbox` 邮件，因为可能会发生文件损坏。

取决于你如何访问邮件，`maildir` 允许多个应用程序同时访问 `maildir` 文件；`mbox` 则不允许。

对邮件用户代理（MUA）或电子邮件客户端的选择也会影响你对邮件目录的选择。例如，`pine` 程序不缓存任何目录信息，并且每次访问它时都必须重新读取邮件目录。更高级的电子邮件客户端执行缓存，因此 `maildir` 可能是一个不错的选择。似乎并不存在完美的方案。

## 选择 MTA

Ubuntu 还有其他 MTA 可用，但前面几节讨论的是最流行的。你应该选择哪一个？这取决于你需要做什么。`Postfix` 的邮件优势在于……

## 邮件投递代理 (The Mail Delivery Agent)

`SMTP` 是一种服务器到服务器协议，设计用于投递到始终连接到用户命令的系统；用户在特定操作而连接，并经常断开。为了适应这种差异，许多系统使用邮件投递代理，或 `MDA`。`MDA` 类似于

`MTA`（见下文），但它不处理系统之间的传输，且不向用户提供接口。

> 注意

`Program` 或 `Spamassassin` 都是 `MTA` 的示例；这两个过滤服务都对 `MTA` 进行过滤，而 `MTA` 则在本地存储消息，然后将其提供给 `MUA` 或邮件客户端供用户阅读。

`MTA` 使用 `POP3` 或 `IMAP` 协议进行此过程。类似于邮局的邮政箱，`POP3` 和 `IMAP` 实现了一种“存储并转发”的过程，如果你只是想读读邮件，这种方式可以减轻对维护本地邮件服务器的需求。例如，拨号上网的用户可以间性地连接到其 `ISP` 的邮件服务器，使用 `Fetchmail` 获取邮件（请参见本章后文的“使用 Fetchmail 获取邮件”章节）。

## 邮件用户代理 (Mail User Agent)

邮件用户代理，简称 `MUA`，是电子邮件系统的另一个必要部分。`MUA` 是一个邮件客户端或阅读器，允许用户读取和编写电子邮件，并提供用户界面。大多数用户所熟悉的“电子邮件”其实就是邮件应用程序本身。一些流行的 UNIX 命令行 `MUA` 有 `eim`、`pine` 和 `mut`。Ubuntu 还提供了现代的 GUI：`Evolution`、`Thunderbird`、`Mozilla Mail`、`Balsa`、`Sylpheed` 和 `KMail`。相比之下，常见的非 UNIX `MUA` 有 `Microsoft Outlook`、`Outlook Pegasus`、`Eudora` 和 `Necklace Messenger`。

`Microsoft Windows` 和 `Macintosh` 的 `MUA` 通常包含某些 `MTA` 功能；而 Unix 则不包含。例如，`Microsoft Outlook` 可以连接到你的互联网服务提供商的邮件服务器来发送消息。另一方面，UNIX `MUA` 通常依赖于如 `Sendmail` 等外部 `MTA`。这看起来似乎是一个没必要的复杂的方法，如果是为了连接单个用户到其 `ISP`，确实如此。对于任何情况，使用外部 `MTA` 都能允许你拥有更大的活性，因为你可以使用任何数量的外部程序处理处理处理你的电子邮件功能并定制服务。让不同的应用程序处理过程可以让你对如何向网络用户以及个人和小型办公室/家庭办公室（SOHO）用户提供电子邮件产生极大控制。

例如，你可以执行以下操作：

- 使用 `Evolution` 读取和编写邮件
- 使用 `Sendmail` 发送你的邮件
- 使用 `biff` 在有新邮件时通知你
- 使用 `Fetchmail` 从远程邮件服务器获取你的邮件

![](img/757e95bd85c59465935194247625328c_624_0.png)

- 使用 `Postmail` 根据发件者、主题或许多变量自动对你的入站邮件进行排序
- 使用 `Spamassin` 在你阅读之前消除不需要的消息

## 基础 Postfix 配置与操作

由于 `Postfix` 是 Ubuntu 推荐的客户端（也是使用最广泛的客户端），以下章节提供了配置和运行你的电子邮件系统的简要说明和示例。然而如前提到的，`Postfix` 是一个极其复杂的程序，具有许多配置选项。因此，本章仅涵盖了部分基础知识。关于 `Postfix` 以及其他 `MTA` 的更多信息，请参见本章末尾的“参考”部分。

`Postfix` 配置由 `/etc/postfix` 目录中的文件处理，大部分配置由 `main.cf` 文件处理。配置文件 `main.cf` 的实际语法非常易读（见下文示例）：

```
# 查看 /usr/share/postfix/main.cf.dist 获取带注释的更完整的版本
# Debian 特有：指定文件名将导致该文件的
# 第一行用作名称。Debian 默认
# 是 /etc/mailname。
#myorigin = /etc/mailname.
```

```
smtpd_banner = $hostname SMTPD $mail_name (Ubuntu)
biff = no
```

```
# 附加 .domain 是 MUA 的工作。
append_dot_mydomain = no
```

```
# 取消下行的注释以生成“延迟邮件”警告
#delay_warning_time = 4h
```

```
# TLS 参数
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.pem
smtpd_use_tls=yes
smtpd_tls_session_cache_database = btree:${queue_directory}/smtpd_sccache
smtpd_tls_session_cache_database = btree:${queue_directory}/smtp_sccache
```

```
# 查看 postfix 软件包中的 /usr/share/doc/postfix/TLS_README.gz 获取
# 关于在 smtp 客户端中启用 SSL 的信息。
```

```
myhostname = optimus
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
```

```
mydestination = optimus, localhost.localdomain, , localhost
relayhost =\mynetworks = 127.0.0.0/8
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
```

复杂的电子邮件服务器设置超出了本书的范围，我们将引导你参考 Dent 编写的《Postfix: The Definitive Guide》。这是一个非常棒的参考，而且相当少见，因为它只运行到版本 3.0 左右。这看起来似乎是一个没必要的复杂的方法，如果是为了连接单个用户到其 `ISP`，确实如此。对于任何情况，使用外部 `MTA` 都能允许你拥有更大的活性，因为你可以使用任何数量的外部程序处理你的电子邮件功能并定制服务。让不同的应用程序处理过程可以让你对如何向网络用户以及个人和小型办公室/家庭办公室（SOHO）用户提供电子邮件产生极大控制。

例如，你可以执行以下操作：

- 使用 `Evolution` 读取和编写邮件
- 使用 `Sendmail` 发送你的邮件
- 使用 `biff` 在有新邮件时通知你
- 使用 `Fetchmail` 从远程邮件服务器获取你的邮件

![](img/757e95bd85c59465935194247625328c_624_0.png)

- 使用 `Postmail` 根据发件者、主题或许多变量自动对你的入站邮件进行排序
- 使用 `Spamassin` 在你阅读之前消除不需要的消息

由于 `Postfix` 是 Ubuntu 推荐的客户端（也是使用最广泛的客户端），以下章节提供了配置和运行你的电子邮件系统的简要说明和示例。如前提到的，`Postfix` 是一个极其复杂的程序，具有许多配置选项。因此，本章仅涵盖了部分基础知识。关于 `Postfix` 以及其他 `MTA` 的更多信息，请参见本章末尾的“参考”部分。

`Postfix` 配置由 `/etc/postfix` 目录中的文件处理，大部分配置由 `main.cf` 文件处理。配置文件 `main.cf` 的实际语法非常易读（见下文）：
