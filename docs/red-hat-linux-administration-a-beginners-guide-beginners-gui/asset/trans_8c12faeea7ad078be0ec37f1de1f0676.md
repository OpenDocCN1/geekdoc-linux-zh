

```
FEATURE(`nullclient')
define(`MAIL_HUB', `mail.example.com')
```

其中 **mail.example.com** 是邮件枢纽。

**local_procmail** 此功能指示 Sendmail 使用 Procmail 作为本地邮件器。它最多可以接受三个参数：Procmail 的路径（默认为 */usr/local/bin/procmail*）、传递给 Procmail 的参数（默认为 *-X -a hostname -d username*），以及邮件器的标志。现实地说，你通常只需要指定 Procmail 的位置即可。除非你有特殊需求并且已经阅读了相应的 Procmail 参数文档，否则无需担心传递给 Procmail 的参数。例如：

```
FEATURE(`local_procmail', `/usr/bin/procmail')
```

**smrsh** Sendmail 的一个安全问题在于，配置它的人员（我们）会犯错误。最普通的错误之一是以不安全的方式设置可以通过别名扩展运行的程序，这些程序可以被远程用户利用。这无异于用锤子打自己的脚。
Sendmail 试图通过 Sendmail 受限 Shell（**smrsh**）拿走这把“锤子”。它是一个功能非常简化的 shell，功能有限，因此由于配置不当而可被利用的漏洞更少。
此功能接受一个参数，用于指定 **smrsh** 的位置。如果 **smrsh** 位于 */usr/sbin* 目录中，我们应指定：

```
FEATURE(`smrsh', `/usr/sbin/smrsh')
```

**promiscuous_relay** 默认情况下，Sendmail 不允许任何站点通过你的站点中继邮件。这是为了保护你免受垃圾邮件发送者将你的系统作为跳板（hopping point）的侵害。如果由于某些极其奇怪的原因，你必须允许随机人员通过你的邮件服务器中继，你可以使用此功能。

![](img/ec2066d370d3af1a767664d36aa7ddfe_420_0.png)

*允许随机人员通过你的服务器中继是一个极坏的主意。这会使你的站点面临拒绝服务（DoS）攻击、带宽被盗用，以及收到来自愤怒的未经许可电子邮件接收者的大量电子邮件的梦魇。在像这样开放你的系统之前，请理解其后果！*

**relay_entire_domain** Sendmail 的默认行为是仅中继来自 **access** 数据库（在本模块稍后“垃圾邮件控制：access 数据库”中讨论）中列出的主机的邮件。使用此功能，你允许你域内的任何主机通过你中继。

**relay_based_on_MX** 此功能指示 Sendmail 查找请求通过你中继的主机的 DNS MX 记录。如果 Sendmail 发现该主机的 MX 记录就是 Sendmail 正在运行的同一台主机，则消息将被接受进行中继。

**accept_unqualified_senders** 通常，Sendmail 拒绝来自不合格电子邮件地址的邮件。例如，来自 alicee@example.com 的邮件是可接受的，但仅来自 alicee 的邮件则不可接受。使用此功能指示 Sendmail *不*要求发件人电子邮件地址必须合格。

**accept_unresolvable_domains** Sendmail 默认会验证发件人的域名是否可以通过 DNS 解析。这防止人们伪造来自不存在域名的电子邮件。如果你的站点由于某种原因（例如你位于防火墙之后）对互联网 DNS 命名空间的视野有限，你将希望使用此功能告诉 Sendmail 接受来自无法解析域名的消息。

**access_db** 此功能启用 **access** 数据库，允许你根据源域名或电子邮件地址指定是否接受、拒绝、丢弃或以特殊代码拒绝所有传入的电子邮件。我们将在本模块稍后讨论垃圾邮件控制时的“垃圾邮件控制：access 数据库”中更详细地探讨此功能的配置文件。

**blacklist_recipients** 有些用户不应该收到任何电子邮件，例如 **nobody**、**bin** 或 **lp**。你可以使用此功能结合 **access_db** 功能将这些用户列入黑名单，使他们无法接收电子邮件。

黑名单配置如何与 **access_db** 配合使用将在“垃圾邮件控制：access 数据库”中稍后讨论。

## 可配置参数

Sendmail 为其功能提供了许多可配置参数。在本节中，我们将回顾这些参数，并解释它们的用途及其默认值。你会发现，在大多数情况下，默认值都完美无缺，你不需要更改任何内容。

你可以在 **README.cf** 文件中看到非常长的可配置选项列表。然而，其中许多选项使用频率极低，以至于当你完成本模块时，你可能会忘记它们的存在。因此，表 13-2 仅涵盖最常见的选项。

| 选项名称 | 描述 | 默认值 |
|---|---|---|
| confMAILER_NAME | 内部生成邮件（通常用于退回邮件的错误消息）所使用的名称。 | MAILER-DAEMON |
| confDOMAIN_NAME | 你的域名。只有当 Sendmail 无法自行确定你的域名时，你才应设置此选项。 | 无默认值 |
| confCW_FILE | 包含服务器可能所使用的 hostname 列表的文件的完整路径（参见 use_cw 文件功能）。 | /etc/sendmail.cw |
| confCT_FILE | 包含受信任用户列表的文件的完整路径（参见 use_ct 文件功能）。 | /etc/sendmail.ct |
| confCR_FILE | 中继域文件的完整路径。这是 Sendmail 将进行中继的域名列表。（你应该使用 access_db 功能替代。） | /etc/mail/relay-domains |
| confALIAS_WAIT | 当邮件别名文件更新时，必须使用 newaliases 命令将其转换为内部数据库格式。此参数告诉 Sendmail 在自行重建数据库之前等待 newaliases 运行多长时间。 | 10 分钟 (10m) |
| confMIN_FREE_BLOCKS | Sendmail 接受新消息时邮件存储分区必须具备的空闲块数量。此选项允许 Sendmail 保护系统免受电子邮件突发流量的影响。 | 100 块，其中 1 块（在 Linux 下）等于 1K |
| confMAX_MESSAGE_SIZE | Sendmail 将接受的最大消息大小（以字节为单位）。 | 无限 |
| confAUTO_REBUILD | 指定 Sendmail 是否应在需要时自动重建别名数据库。 | False |
| confLOG_LEVEL | 指定 Sendmail 的日志记录级别。级别数字越高，执行的日志记录越多。级别代码如下：0 最小日志记录 1 严重系统故障和潜在安全问题 2 通信丢失（网络问题） 3 临时错误、格式错误的地址、转发/包含错误 4 次要故障、过时的别名数据库、通过 check_rule 集合的连接拒绝 5 消息收集统计信息 6 错误消息创建、VRFY 和 EXPN 命令 7 投递失败（未知主机或用户等） 8 成功投递和别名数据库重建 9 消息延迟 10 数据库扩展（别名、转发和用户数据库查找） 11 NIS 错误和工作结束处理 12 所有 SMTP 连接 13 不良用户 shell 和权限不适当的文件 | 日志级别 9 |

表 13-2 Sendmail 最常见的可配置参数

| 选项名称 | 描述 | 默认值 |
| --- | --- | --- |
| **confME_TOO** | 当消息发送给一个发件人是其成员之一的别名列表时（例如用户 *hdrs* 向 *management* 发送消息，该别名扩展为用户 *hd*、*julia* 和 *cael*），此选项确定是否也应将消息发送给发件人。 | False（不将消息发回给发件人） |
| **confTO_INITIAL** | Sendmail 在连接远程站点发送邮件时应等待的超时期间。 | 5 分钟 (5*m) |
| **confTO_IDENT** | Sendmail 在尝试通过 IDENT 协议识别试图向其发送邮件的人的用户名时应等待的超时期间。 | 30 秒 (30*s) |
| **confTO_QUEUEWARN** | 在告知用户其通过 Sendmail 中继的消息因无法联系远程站点而被延迟之前，等待的超时期间。 | 4 小时 (4*h) |
| **confSMTP_LOGIN_MSG** | 发送给试图连接 Sendmail 的人的问候消息。有些站点开始自定义此字符串，以便远程站点不知道实际运行的是哪种邮件服务器；本质上，这是通过模糊性实现的安全，其底层哲学是，“为什么告诉它们你不必告诉它们的事情？”只要明白，模糊邮件服务器的类型并不意味着如果攻击者足够坚定，他们就无法突破。 | 服务器主机名、Sendmail 版本以及 Sendmail 配置文件版本 |
| **confDOUBLE_BOUNCE_ADDRESS** | 如果发生错误，Sendmail 会将电子邮件通知发送给站点管理员。站点管理员由此选项定义。大多数站点保持默认设置不变，并使用别名将消息路由到系统管理员。 | Postmaster |

表 13-2 Sendmail 最常见的可配置参数（续）

![](img/ec2066d370d3af1a767664d36aa7ddfe_423_0.png)

配置文件中的某些参数代表时间值。这些值的格式是数字后跟一个字母，其中字母是 s（秒）、m（分钟）、h（小时）或 d（天）。例如，**10m** 表示 10 分钟，**3d** 表示 3 天，等等。

例如，要将 Procmail 程序的路径设置为 `/usr/bin/procmail`，我们将使用：

```
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')
```

## 完整的示例配置

以下是用于构建 Red Hat & 配置文件的完整 **.mc** 文件：

```
VERSIONID(`linux_setup_for_Red_Hat_Linux')dnl
OSTYPE('linux')
define(`confDEF_USER_ID', `8:12')dnl
undefine(`UUCP_RELAY')dnl
undefine(`BITNET_RELAY')dnl
define(`confAUTO_REBUILD')dnl
define(`confTO_CONNECT', `1m')dnl
define(`confTRY_NULL_MX_LIST',true)dnl
```

