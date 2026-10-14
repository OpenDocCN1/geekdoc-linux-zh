
```
client% -v user@companyB.com
Subject: Hello
Hi user@companyB.com. This is a test.
^D
```

```
220 mail.serverB.com Sendmail 8.9.1a/8.9.1; Sat, 19 Feb 2000 12:33 +0100 (EST)
>>> HELLO mail.companyA.com
250 mail.serverB.com Hello mail.companyA.com (snippet.companyA.com), pleased to meet you
>>> MAIL FROM:<user@companyA.com>
250 <user@companyA.com> Sender ok
>>> RCP TO:<user@companyB.com>
250 <user@companyB.com>... Recipient ok
>>> DATA
354 Enter mail end, with ".* on a line by itself
>>> Hi user@companyB.com. This is a test.
250
250 OK
>>> QUIT
221 mail.serverB.com closing connection
user@companyB.com... Sent (Ok)
```

在之前的示例中，本地邮件服务器（`mail.companyA.com`）连接远程服务器（`mail.companyB.com`）并将邮件递交给用户。通过这种方式，`mail`可以为用户和管理员识别特定用户或网络问题提供有用提示。由于电子邮件是一项关键服务，且 `sendmail` 是最广泛部署的 MTA，它也与安全警告和问题相关。这导致一些开发者开发了如 `qmail` 等 MTA 系统，虽然全球范围内许多组织部署了不当响应，但关注 Sendmail Consortium（`http://www.sendmail.org/`）等网站的标题是有用的。允许用户在运行 `sendmail` 的服务器上执行任意命令。对于用 C 语言编写的 UNIX 应用程序这是一个常见问题，但前提是未实现数组大小的边界检查。在 `sendmail` 的情况下，当使用松散的 MIME 头发起攻击时——有一个补丁允许 `sendmail` 检测并拒绝可能与攻击相关的邮件。如果你需要应用该补丁，可以在 `ftp://ftp.sendmail.org/pub/sendmail/sendmail.8.9.1a.patch` 获取。

# m4 配置

可以使用 `m4` 语言通过使用一组为 `sendmail` 开发的预定义宏来创建 `sendmail.cf` 文件。为了使用 `m4` 宏创建 `sendmail.cf` 文件，需要创建一个包含要运行宏列表（以及适用于你站的适当参数值）的文本文件，通常命名为 `sendmail.mc`。一旦此文件安装在主 `sendmail` 目录下的 `cf/cf` 子目录中，就可以从该目录使用以下命令构建新的 `sendmail.cf` 文件：

```
# cp /etc/sendmail.cf /etc/sendmail.orig
# m4 ../m4/cf.m4 sendmail.mc > /etc/sendmail.cf
```

第一个命令备份当前的 `sendmail.cf` 文件，而下一个命令构建新的 `sendmail.cf` 文件。一旦使用上一节定义的命令启动 `sendmail`，`sendmail` 将使用新运行。

在检查示例 `sendmail.mc` 文件之前，让我们详细查看用于配置 `sendmail` 的宏和参数。

# 宏

以下宏用于 `sendmail.mc`：

- `DOMAIN` 用于定义具有相同域名的邮件服务器的共同元素。
- `EXPOSED_USER` 防止特定用户的域名伪装。
- `FEATURE` 启用特定的 `sendmail` 特性。
- `MAILER` 指定在服务器上使用的邮件传递程序（`local`, `smtp` 或 `procmail`）。
- `MASQUERADE_AS` 在所有出发邮件上插入有效域名，而不是操作系统类型。
- `OTYPE` 定义主机操作系统类型。

# 特性

一旦生成了基本的域名和操作系统参数，下一步是使用 `FEATURE` 宏启用特定的 `sendmail` 特性。每个启用的特性都需要一个 `FEATURE` 实例。常用的特性包括

- `accept_unqualified_senders` 接受来自没有完全限定域名的用户的邮件递送。
- `accept_unresolvable_domains` 接受来自完全限定域名无法解析的用户邮件递送。
- `access_db` 启用维护的发送者和域名数据库，自动退回或拒绝。
- `always_add_domain` 在所有通过 `sendmail` 发送的邮件上插入域名，即使是递交给本地用户的邮件。
- `blacklist_recipients` 定义不允许接收邮件的接收者列表。
- `domaintable` 用新域名替换旧域名。
- `mailertable` 允许为每个每个虚拟域名关联不同的邮件服务器。

## 第 37 章：传输层

673

- `nullclient` 允许本地 `sendmail` 实例将所有消息转发到单个导出的 `sendmail` 服务器进行递送。
- `promiscuous_relay` 允许任何站点的邮件通过本地服务器中继。应始终避免使用此选项，因为垃圾邮件商人可能会发现你的服务器并利用它中继垃圾邮件，从而掩盖其真实来源。
- `redirect` 为系统中已不存在的用户重定向消息。这需要在 `/etc/aliases` 中有一个相应的条目，名称为原用户或其新电子邮件地址。
- `relay_based_on_mx` 使用 DNS 中定义的 MX 记录来确定本地 `sendmail` 服务器中继来自其他人的消息是否正确。
- `relay_entire_domain` 允许域范围内的所有主机通过本地 `sendmail` 服务器路由电子邮件。
- `smrsh` 一个功能受限的 shell，可用于限制 `sendmail` 守护进程对系统的访问。
- `use_ct_file` 防止用户在发出的邮件组中更改其电子邮件的用户名部分。
- `use_cw_file` 包含邮件服务器所有 DNS 别名的列表。
- `virtirable` 支持对属于虚拟域的同名用户账户路由电子邮件。因此，`joe@domainone.com` 不会与 `joe@domainintwo.com` 混，尽管这两个域可以使用同一个 `sendmail` 实例。

## 参数

可以使用 `m4 define` 命令为 `sendmail` 的操作设置特定参数。虽然 `sendmail` 默认设置的大多数值对于正常使用已经足够，但你可能需要更改某些值。`sendmail` 定义了大量的参数，但我们在这里只检查一些常用的修改参数：

- `confDOMAIN_NAME` 如果你的 DNS 服务器不可靠，你可能想在这里设置默认名称。
- `confLOG_LEVEL` 指定 `sendmail` 的日志记录，范围从 0（最小）到 13（所有）。
- `confMAILER_NAME` 用于系统返回消息和其他自动生成的邮件的别名。这通常被设置为 `MAILER-DAEMON`，它通常被别名为 `root`。（因此，直接将该值设置为 `root` 也是可能的。）
- `confMAX_MESSAGE_SIZE` 接受递送的任何消息的最大 own（字节）。虽然现在大附件很常见，但应设置几兆字节的上限以防止拒绝服务攻击。放置标准的 `sendmail` 版本横幅，并带有本地（通常是不具特征的）消息。这对于防止破解者尝试利用你特定版本的 `sendmail` 漏洞很有用。

## Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南

674

## 示例 sendmail.mc 文件

在这里，我们定义了一个示例的 `sendmail.mc` 文件，其中包含了我们之前讨论的一些参数和宏：

```
OSTYPE('solaris2')
define('CONFDOMAIN_NAME', 'cassowary.net')
define('CONFLOG_LEVEL', '13')
define('CONFMAILER_NAME', 'root')
define('CONFMAX_MESSAGE_SIZE', '1048576')
define('confSMTP_LOGIN_MSG', 'No Name Mail Server')
FEATURE('smsh', '/usr/sbin/smsh')
FEATURE('redirect')
FEATURE('always_add_domain')
FEATURE('blacklist_recipients')
FEATURE('access_db_')
```

`sendmail` 源码中提供了许多配置文件的更详细示例。特别是 Eric Allman 编写的优秀 README 文件，任何认真考虑进行扩展 `sendmail` 配置的人都应该阅读。

## 示例 SMTP 事务
