
# 10.0.0.51 是 LAN 中的 IP

```text
inet_interfaces = 10.0.0.51, 127.0.0.1
mynetworks = 10.0.0.0/24, 127.0.0.0/8
smtpd_recipient_restrictions = permit_mynetworks, reject
```

有必要重写以确保发送者不会以这种形式出现：

```text
geeko@da51.digitalairlines.com
```

而是以常见的格式：

```text
geeko@digitalairlines.com
```

另一方面，主机对于发送给 `root` 的邮件非常重要。因此，发送给 `root` 的邮件不应被重写。

在 `/etc/postfix/main.cf` 文件中的两个条目就足够这种简单的场景：

```text
masquerade_exceptions = root
masquerade_domains = digitalairlines.com
```

此外，必须告知 Postfix 它应该向哪个邮件服务器投递邮件。`relayhost` 条目还确保 Postfix 不尝试与收件者的相应邮件服务器建立直接联系。

```text
relayhost = dal.digitalairlines.com
```

## 练习 4-2 在本地网络发送邮件

在本次练习中，你将在本地网络发送邮件。你配置 Postfix 并测试你的配置。你可以在练习集中找到此练习。

（练习结束）

## 通过互联网接收邮件

如果邮件服务器不仅用于发送本地网络用户的电子邮件消息，还用于接收发往该域名的互联网邮件，那么配置起来会困难一些。防止邮件服务器被垃圾邮件发送者滥用为中继（open relay）非常重要。

无论 Postfix 的具体配置如何，都必须通过 MX 记录将服务器引入 DNS 作为负责的邮件服务器。

除了上一节的要求外，邮件服务器还必须：

- 接受来自互联网并发往你域名的邮件
- 拒绝来自互联网但不是发往你域名的邮件
- 拒绝来自已知垃圾邮件源的邮件

因此，需要许多额外的条目。

由于理论上邮件可以在所有接口上接收，因此 `inet_interfaces` 需要一个不同的值。`mynetworks_style` 可以保持不变。

```text
inet_interfaces = all
mynetworks_style = subnet
```

Postfix 必须知道它能接受哪些域的邮件：

```text
hostname = da51.digitalairairlines.com
mydomain = digitalairairlines.com
mydestination = $hostname, local.$mydomain
```

如果 Postfix 不仅负责你域名的邮件，还负责其他域的邮件（Web 托管主机通常如此），则这些域名不会输入 `mydestination` 下，而是在 `virtual` 查找表中，这将在下一节中介绍。

接受或不接受邮件的决定由以下变量控制，这些变量包含了各种标准：

- `smtpd_helo_restrictions`
- `smtpd_sender_restrictions`
- `smtpd_recipient_restrictions`
- `smtpd_client_restrictions`

只有当消息通过所有标准且未被拒绝时，才会被投递。

例如，可以使用 `smtpd_sender_restrictions` 防止已知的垃圾邮件发送者投递邮件。如果发送者在 RBL（实时黑列表）列表中，可以在检查是否是发往本地用户之前拒绝该消息：

```text
maps_rbl_domains = rbl-domains.digitalairlines.com
smtpd_sender_restrictions = reject_maps_rbl
```

以下条目确保接受来自 `$mynetworks` 指定范围的邮件，以及根据 `$mydomain` 规范由 Postfix 负责的邮件——所有其他邮件将由于 `reject_unauth_destination` 被拒绝：

```text
smtpd_recipient_restrictions = permit_mynetworks,
reject_unauth_destination
```

所有限制可能性的解释将超出本课程的范围。

## 练习 4-3

### 在互联网上使用 Postfix

在本次练习中，你配置 Postfix 向互联网发送电子邮件。你可以在练习集中找到此练习。

（练习结束）

## 配置查找表

查找表包含在整个 Postfix 系统中处理电子邮件的规则。这些表通过文件中的变量进行激活：

```text
/etc/postfix/main.cf
```

表通过文件中的变量激活：

```text
/etc/postfix/main.cf
```

然后表定义为：

```text
/etc/postfix/main.cf
```

查找表的结构如下：

- 空行或以 `#` 开头的行不被解释。
- 以空格开头的行被视为上一行的延续。
- 它也可以使用正则表达式。

每个查找表都有一个 man 手页：`man lookup-table`。

以下是查找表：

- `access` 查找表
- `canonical` 查找表
- `recipient_canonical` 查找表
- `sender_canonical` 查找表
- `relocated` 查找表
- `transport` 查找表
- `virtual` 查找表
- `aliases` 查找表

## access 查找表

你可以使用 `/etc/postfix/access` 查找表来拒绝或允许来自发送者的邮件。`smtpd` 守护进程在邮件到达时评估此表。

以下描述了：

- 激活查找表
- access 表格式

### 激活查找表

此功能在 `/etc/postfix/main.cf` 文件中被激活：

```text
smtpd_sender_restrictions = hash:/etc/postfix/access
```

### access 表格式

每行都定义了一个由 `smtpd` 在邮件到达时评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。每行由第一列的电子邮件地址定义和第二列的定义的动作组成。

电子邮件地址模式的可能值包括：

- `user@domain`：为指定的电子邮件地址定义一个过滤器。
- `domain.name`：为指定域的所有电子邮件地址定义过滤器。
- `user@`：为具有相同用户部分的所有电子邮件地址定义过滤器。

动作的可能值包括：

- `4x Text, 5x Text`：拒绝带有特定数值代码（参见 RFC211）和定义的文本消息的邮件。
- `REJECT`：用通用错误消息拒绝邮件。
- `OK`：接受邮件。
- `DISCARD` 可选文本：确保邮件被丢弃且不向发送者发送错误消息。

*可选文本*会显示在日志中。如果没有指定文本，日志中将显示一条通用消息。

示例：

| postmaster@digital airlines.com | OK |
| :--- | :--- |
| spam@hahaha.net | 550 We're fighting against spam! |
| 194.95.93.10 | REJECT |

## canonical 查找表

你可以使用 `/etc/postfix/canonical` 查找表来重写输入和输出邮件的发送者和收件者地址。头部和信封都会被重写。`cleanup` 守护进程在邮件到达时读取此表。

以下描述了：

- 激活查找表
- canonical 表格式

### 激活查找表

此功能在 `/etc/postfix/main.cf` 文件中被激活：

```text
canonical_maps = hash:/etc/postfix/canonical
```

### canonical 表格式

每行定义了一个由 `smtpd` 在邮件到达时评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。每行由第一列的电子邮件地址定义和第二列的定义动作组成。

电子邮件地址模式的可能值：

- `user@domain`：为指定的电子邮件地址定义过滤器。
- `user`：为所有具有相同用户部分的电子邮件地址定义过滤器，前提是电子邮件的域名部分列在 `/etc/postfix/main.cf` 文件的变量 `$myorigin`、`$mydestination`、`$inet_interfaces` 或 `$proxy_interfaces` 之一。
- `@domain`：为指定域名的的所有电子邮件地址定义过滤器。

动作的可能值：

- `user@domain`：将电子邮件地址重写为此处定义的值。

示例：

| training@digital airlines.com | geeko@digitalairlines.com |
| :--- | :--- |
| @slc.digitalairlines.com | slc@digitalairlines.com |

如果你想以不同的方式转换发送者地址和收件人地址，请使用：

- `recipient_canonical` 转换收件人地址
- `sender_canonical` 转换发送者地址

## recipient_canonical 查找表

你可以使用 `/etc/postfix/recipient_canonical` 查找表来转换入站和出站邮件的收件人地址。清理进程（`cleanup daemon`）在邮件到达时，会在评估通用查找表 `/etc/postfix/canonical` 之前评估此表。

描述了以下主题：

- 激活查找表
- recipient_canonical 查找表格式

### 激活查找表

此功能通过 `/etc/postfix/main.cf` 文件中的条目进行激活：

```text
recipient_canonical_maps = hash:/etc/postfix/recipient_canonical
```

### recipient_canonical 查找表格式

每行定义了一个由 `smtpd` 在邮件到达时评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。每行由第一列的电子邮件地址定义和第二列的定义动作组成。

电子邮件地址模式的可能值：

- `user@domain`：为指定的电子邮件地址定义过滤器。
- `user`：为所有具有相同用户部分的电子邮件地址定义过滤器，前提是电子邮件的域名部分列在文件 `/etc/postfix/main.cf` 的变量 `$myorigin`、`$mydestination`、`$inet_interfaces`、`$proxy_interfaces` 之一。
- `@domain`：为指定域名的所有电子邮件地址定义过滤器。

动作的可能值：

- `user@domain`：将电子邮件地址重写为此处定义的值。

示例：

| geek@digitalairlines.com | training@digital airlines.com |
| :--- | :--- |
| @slc.digitalairlines.com | slc@digitalairlines.com |

## sender_canonical 查找表

你可以使用 `/etc/postfix/sender_canonical` 查找表来重写入站和出站邮件的发送者地址（对于出站邮件：将 `login@host_internal.com` 转换为 `firstname.surname@mycompany.com`）。清理进程在邮件到达时，会在读取通用查找表 `/etc/postfix/canonical` 之前读取此表。

描述了以下主题：

- 激活查找表
- sender_canonical 查找表格式

### 激活查找表

此功能通过 `/etc/postfix/main.cf` 文件中的条目进行激活：

```text
sender_canonical_maps = hash:/etc/postfix/sender_canonical
```

### sender_canonical 查找表格式

每行定义了一个由 `smtpd` 在邮件到达时评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。每行由第一列的电子邮件地址定义和第二列的定义动作组成。

电子邮件地址模式的可能值为：

- `user@domain`：为指定的电子邮件地址定义过滤器。
- `user`：为所有具有相同部分的电子邮件地址定义过滤器，前提是电子邮件的域名部分列在文件 `/etc/postfix/main.cf` 的变量 `$myorigin`、`$mydestination`、`$inet_interfaces` 或 `$proxy_interfaces` 之一。
- `@domain`：为指定域名的所有电子邮件地址定义过滤器。

动作的可能值为：

- `user@domain`：将电子邮件地址重写为此处定义的值。

示例：

| training@digital airlines.com | geeko@digital airlines.com |
| :--- | :--- |
| @slc.digitalairlines.com | slc@digitalairlines.com |

## relocated 查找表

你可以使用 `/etc/postfix/relocated` 查找表，向发送给在该系统中不存在的用户的邮件发送者返回相应的退信邮件，并附带关于目标收件人新地址的说明。

描述了以下主题：

- 激活查找表
- relocated 查找表格式

### 激活查找表

此功能通过 `/etc/postfix/main.cf` 文件中的条目进行激活：

```text
relocated_maps = hash:/etc/postfix/relocated
```

### relocated 查找表格式

每行定义了一个由 `smtpd` 在邮件到达时评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。每行由第一列的电子邮件地址定义和第二列的定义动作组成。

电子邮件地址模式的可能值为：

- `user@domain`：为指定的电子邮件地址定义过滤器。
- `user`：为所有具有相同部分的电子邮件地址定义过滤器，前提是电子邮件的域名部分列在文件 `/etc/postfix/main.cf` 的变量 `$myorigin`、`$mydestination`、`$inet_interfaces` 或 `$proxy_interfaces` 之一。
- `@domain`：为指定域名的所有电子邮件地址定义过滤器。

动作的可能值为：

- `user@domain`：将电子邮件地址重写为此处定义的值。

示例：

| training@digital airlines.com | geeko@digital airlines.com |
| :--- | :--- |
| @slc.digitalairlines.com | slc@digitalairlines.com |

## transport 查找表

你可以使用 `/etc/postfix/transport` 查找表来为特殊地址范围定义邮件路由。

描述了以下主题：

- 激活查找表
- transport 查找表格式

### 激活查找表

此功能通过 `/etc/postfix/main.cf` 文件中的条目进行激活：

```text
transport_maps = hash:/etc/postfix/transport
```

### transport 查找表格式

每行定义了一个在邮件发送前由 `qmgr` 或 `trivial-rewrite` 进程评估的规则。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。

`uucp` 定义了通过 Postfix 管道传递电子邮件，该管道通过 `/etc/postfix/master.cf` 文件配置，用于通过 UUCP 传递电子邮件。接收者主机指定为 `nexthop`。

示例：

| digitalirlines.com | smtp:da51.digitalirlines.com:10025 |
| :--- | :--- |
| suse.com | uucp:da150 |

## 虚拟查找表

你可以使用 `/etc/postfix/virtual` 虚拟查找表为多个具有不同用户名的域名设置电子邮件。

描述了以下主题：

- 激活查找表
- 虚拟查找表格式

### 激活查找表

该功能通过在 `/etc/postfix/main.cf` 文件中的以下条目激活：

```text
virtual_maps = hash:/etc/postfix/virtual
```

### 虚拟查找表格式

每一行定义了一个规则，当邮件到达时由 `smtpd` 对其进行评估。规则从上到下处理，并在出现第一个匹配项时结束规则匹配。

使用虚拟域名需要先定义虚拟域名。这是通过将虚拟域名名放在第一列，并将任意文本放在第二列来实现的。文本仅用于保持文件的结构，没有意义。

其他所有描述该域名接收者地址的行包含：

- 第一列：接收者地址。
- 第二列：
  - 应该投传入邮件的本地电子邮件用户的用户名。
  - 或者
  - 逗号分隔的所有应投传入邮件的本地电子邮件用户列表。

当你指定虚拟域名时，只有包含该虚拟域名的电子邮件地址会被修改。带有子域或主机名的地址不会被修改。你需要先将它们指定为虚拟域名。

示例：

| virtual.domain | geeko, tux |
| :--- | :--- |
| postmaster@virtual.domain | postmaster |
| user1@virtual.domain | geeko |
| user2@virtual.domain | tux |

## 别名查找表

`/etc/aliases` 查找表用于定义别名。你无法将电子邮件重定向到其他主机或域名上的邮箱箱。

描述了以下主题：

- 激活查找表
- 别名查找表格式

### 激活查找表

该功能通过在 `/etc/postfix/main.cf` 文件中的以下条目激活：

```text
alias_maps = hash:/etc/aliases
```
