
第一条命令备份当前的生产环境 `sendmail.cf` 文件，而下一条命令构建一个新的生产环境 `sendmail.cf` 文件。启动 `sendmail` 后，通过上一节定义的命令，`sendmail` 将带有新配置运行。

在检查 `sendmail.mc` 文件之前，请仔细查看可用于配置 `sendmail` 的宏和参数。

## 宏

以下是为 `sendmail.mc` 定义的宏：
- `DOMAIN`：用于定义相同域名的邮件服务器的通用元素。
- `EXPOSED_USER`：防止特定用户的域名伪装。
- `FEATURE`：启用特定的 `sendmail` 功能。
- `MAILER`：指定服务器上使用的邮件投递程序（`local`, `smtp`, 或 `procmail`）。
- `MASQUERADE_AS`：在所有发出的邮件中插入有效域名，而不是原始域名。
- `OSTYPE`：定义主机操作系统的类型。

## 功能

一旦生成了基础的域名和操作系统参数，下一步是使用 `FEATURE` 宏启用 `sendmail` 功能。每个要启用的功能都需要一个 `FEATURE` 实例。常用的功能包括：

- `accept_unqualified_senders`：接受来自邮件地址不具有完全限定域名（FQDN）的电子邮件用户的邮件投递。
- `accept_unresolvable_domains`：接受来自 FQDN 无法解析的用户邮件投递。
- `access_db`：启用一个发送者和域名数据库，用于维护哪些邮件会被自动退回或拒绝。
- `always_add_domain`：在所有通过 `sendmail` 发送的邮件中插入 FQDN，即使是投递给本地用户的邮件。
- `blacklist_recipients`：定义不允许接收电子邮件的接收者列表。
- `domaintable`：用新域名名替换旧域名名。
- `mailtable`：允许每个支持的虚拟域关联不同的邮件服务器。
- `nullclient`：允许本地 `sendmail` 实例将所有消息转发到单个出站 `sendmail` 服务器进行投递。
- `promiscuous_relay`：允许从任何站点通过本地服务器中继邮件。不应使用此功能，因为存在垃圾邮件商可能会发现你的服务器并利用它中继垃圾邮件，以掩盖其真实来源。
- `redirect`：将目标为系统中不存在的用户的消息重定向。这需要在 `/etc/aliases` 中有一个相应的条目，包含原用户的名称和其新电子邮件地址。
- `relay_based_on_mx`：使用 DNS 中的 MX 记录来确定本地 `sendmail` 服务器是否为中继其他服务器消息的正确服务器。
- `relay_entire_domain`：允许本地域内的所有主机通过本地 `sendmail` 服务器路由电子邮件。
- `smrsh`：功能受限的 shell，可用于通过 `sendmail` 守护进程限制系统访问。
- `use_ct_file`：防止用户在发送邮件时更改其电子邮件地址的用户名。
- `use_cv_file`：包含邮件服务器的所有 DNS 别名列表。
- `vertertunable`：支持对相同用户名但实际属于不同虚拟域的用户账户路由电子邮件。因此，`joe@domainone.com` 不会被 `joe@domaintwo.com` 混淆，尽管这两个域使用同一个 `sendmail` 实例。

## 参数

可以使用 `m4 define` 命令为 `sendmail` 的操作设置特定参数。`sendmail` 默认大多数值对于正常使用都是满意的，你可能需要更改某些值。`sendmail` 定义了大量的参数，但此处仅检查了一些最常过的参数：

- `confDOMAIN_NAME`：如果你的 DNS 服务器不可靠，你可能想在这里设置默认域名。
- `confLOG_LEVEL`：指定 `sendmail` 的日志级别，范围从 0（极小）到 13（所有）。
- `confMAILER_NAME`：返回消息以及系统其他自动生成的邮件的别名。这通常设置为 `MAILER-DAEMON`，它通常别名为 `root`。因此，可以将该值设置为 `root`。
- `confMAX_MESSAGE_SIZE`：接受投递的任何消息的最大大小（单位为字节）。虽然现在大附件很常见，但应该设置一个几兆字节的上限，以防止拒绝服务攻击。
- `confSMTP_LOGIN_MSG`：用标准的 `sendmail` 版本横幅替换为本地（通常是无描述的）消息。这对于防止黑客尝试利用你特定版本 `sendmail` 的特定漏洞很有用。

## 示例 sendmail.mc 文件

这是一个示例的 `sendmail.mc` 文件，包含了在前节中讨论的一些参数、功能和宏：

```
OSTYPE('solaris2')

define('CONFDOMAIN_NAME', 'cassowary.net')

define('CONFLOG_LEVEL', '13')

define('CONFMAILER_NAME', 'root')

define('CONFMAX_MESSAGE_SIZE', '1048576')

define('CONF_LOGIN_MSG', 'No Mail Server')

FEATURE('smsh','/usr/bin/smsh')

FEATURE(redirect)

FEATURE(always_add_domain)

FEATURE(blacklist_recipients)

FEATURE('access_db')
```

这是一个包含了在前节中讨论的一些参数、功能和宏的示例 `sendmail.mc` 文件。提供了许多示例，特别是 Eric Allman 的自读文件应该认真考虑的 `sendmail` 配置文件。

### 步骤

### 配置 sendmail (sendmail.cf)

`sendmail.cf` 文件由单行命令组成，范围从规则和宏到选项和头部。某些命令必须出现一次以影响规则的解释。`sendmail.cf` 文件中的主要命令类型：

- `C`：指定一个包含多个项的类。例如，`C(MAILCLIENTS)` 指定了邮件客户端（`mars`, `venus`）。
- `D`：指定宏。例如，`Dmail.company.com` 指定了一个名为 `$` 的宏。
- `E`：指定环境变量。作为安全措施，`sendmail` 不使用传递的环境信息，而是使用在 `sendmail.cf` 中指定的值。设置虚拟机（JVM）的位置，使用 `JVM=/usr/local/java/bin`。
- `H`：指定头部，例如 `Received:`。由于包含多部分消息，这些定义现在变得复杂。
- `M`：指定投递程序。例如，`MLocal, P=/bin/mail` 指定 `/bin/mail` 是投递程序，这在 Solaris 下通常如此。
- `O`：指定选项。例如，设置 `O SendMime=True` 可启用发送 MIME 封装的消息。
- `P`：设置消息优先级。例如，优先邮件的优先级设置为零（`Pfirst-class=0`），而垃圾邮件的优先级设置为 -100（`Pjunk=-100`）。
- `R`：指定规则。例如，规则 `R$- $(Mdomain) Rewrite` 将宏定义的 FQDN 添加用户名。
- `S`：指示规则的开始，既可以用数字指定（例如 `S2` 代表规则 2），也可以用标签指定（例如 `SDomainRules` 代表 DomainRules 规则集）。

`sendmail.cf` 文件包含了六种定义的规则：

- `S0`：处理基础地址解析。例如，如果指定了用户地址，则错误信息为“需要用户地址”。
- `S1`：处理电子邮件发送者地址。
- `S2`：处理电子邮件接收者地址。
- `S3`：执行规范化并启动重写规则。例如，会检查无效地址（例如使用冒号），并从地址中删除任何括号 `<>`。
- `S4`：执行最终的路由，包括将扩展后的地址如 `pwatters%mail@companyA.com` 转换为 `pwatters@companyA.com`。
- `S5`：在 `/etc/aliases` 中定义的所有别名扩展后发生的最终重写规则集。

# 第六部分：服务、目录与应用程序

用户定义的规则集可以占用 `S6` 及以上。例如，Solaris 中定义了规则集 33 以支持 Sun 的 RemoteMode。一个典型的 `sendmail` 规则格式如下：

```
Rhs rhs description
```
