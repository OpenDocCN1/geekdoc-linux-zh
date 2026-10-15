
`server_advertise_condition = $[if def.tis_cipher]`

`server_prompts = User Name : Password`

`server_condition = $[if and({eq(${auth[1]):username}),{eq(${auth[2]):mypassword})]`

`server_set_id = $auth`

身份验证数据可以来自许多来源：LDAP、PAM、`/etc/passwd`。`server_advertise_condition`子句通过要求连接使用 TLS 安全（通过 STARTTLS 或 SSL）来防止邮件客户端明文发送密码。如果你希望 Exim 在充当客户端时具有相同的行为，请在 `client`子句中使用 `client_condition`选项，同样使用 `tis_cipher`。

参考文档以获取所有可能的 Exim 身份验证选项的详情和示例。

## 路由器 Routers

路由器根据收件人邮件地址工作，要么通过重写地址，要么将它们分配给传输 `transport`并发送。特定的路由器可以有多个实例，每个实例都有不同的选项。

你指定了一系列路由器。邮件从第一个路由器开始，并通过列表，直到邮件被接受或拒绝。接受的路由器通常将邮件处理到传输驱动程序。路由器处理传入和传出的邮件。它们感觉有点像编程语言中的子程序。

路由器可以为邮件返回以下任何处置：

- `accept` - 路由器接受该地址并将其交给传输驱动程序
- `pass` - 此路由器无法处理该地址；继续下一个路由器
- `decline` - 路由器选择不处理该地址；请使用下一个路由器！
- `fail` - 地址无效；路由器将其放入队列以生成退信邮件
- `defer` - 将邮件留在队列中等待
- `error` - 路由器规范中存在错误；邮件被推迟

## 接受路由器 The accept router

`accept`路由器将地址标记为 OK 并将其传递给传输驱动程序。以下是名为 `localusers`的接受路由器用于投递邮件的示例。

```
local The::
driver accept router

an address as OK and passes the message to a transport driver.

are

of are examples of accept router called localusers for delivering mail.
```

如果满足条件，路由器将邮件传递给传输驱动程序。

## DNS 查询路由器 The dnslookup router

`dnslookup`路由器通常用于传出的邮件。它查找收件人域名的 MX 记录并将邮件传递给 SMTP 传输进行投递。这是一个名为 `remoteusers`的实例：

```
remoteusers:
driver = dnslookup
domains = !example.com
transport = remote_delivery
```

## 手动路由器 The manual router

灵活的 `manualroute`驱动可以以你想要的任何方式获取邮件。路由信息可以是根据收件人域名匹配的规则表 `route_list`，也可以适用于所有域的单一路由 `route_data`。以下是 `manualroute`的两个示例。第一个示例实现了“智能主机”`smart host`概念，所有非本地邮件都发送到中央（智能）主机进行处理。此实例名为 `smarthost`，并适用于所有不在 `local_domains`列表中 `!`字符的收件人域名。

```
smarthost:
driver = manualroute
domain = !local_domains
transport = remote_snmp
route_data = smarthost.example.com
```

## 第 20 章 电子邮件 Electronic Mail

```
save_to_file:
driver = accept
domain = example.com
```

`localusers`路由器实例检查地址的域名部分为 `example.com`且地址的本地部分为本地用户的用户名。如果两个条件都满足，路由器将邮件传递给名为 `my_local_delivery`的传输驱动程序，其在 `transports`部分定义。`save_to_file`实例为拨号用户设计；它将邮件附加到指定的 `batch_appendfile`中。

## 通过 .forward 文件进行用户级过滤

```
firewall:
driver = manualroute
transport = remotedb-smtp
route_data = $(lookup[$domain] cdb ($internal/host/routes/))
```

### 重定向路由器 redirect router

重定向驱动 `redirect driver`地址允许进行重写，例如系统级别名文件或用户的 `~/forward`文件所要求的重写。它通常不会将重写后的地址分配给留给链链中其他路由器的传输层 `transport`。

在下方显示的第一个实例 `system_aliases`通过对 `/etc/aliases`文件进行线性搜索 `search`来查找别名。这对于较小的别名文件是可以接受的，但如果你的文件非常大，请将该行替换为数据库查找。第二个实例 `forwardfile`首先验证邮件是否投递给本地用户，然后检查该用户的：`.forward`文件。

```
system_aliases:
driver = redirect
data = $(lookup[$local_part] lsearch (/etc/aliases))
```

```
user_forward:
driver = redirect
check_local_user
file = $home/forward
no_verify
```

`check_local_user`选项确保收件者是有效的本地用户。`no_verify`表示不验证 `.forward`文件重定向邮件的地址是否有效；直接发送即可。

## 通过 .forward 文件进行用户级过滤

Exim 不仅允许通过 `.forward`文件进行转发，还根据用户 `.forward`文件的内容进行过滤。它支持自身的过滤机制，以及由 cdb IETF 标准化的 `sieve`过滤。如果用户 `.forward`文件的第一行是：

```
#Exim filter
```

或者

```
#Sieve filter
```

那么后续的过滤命令（约 15 个）可以用于确定邮件应该投递到何处。过滤本身并不会投递邮件——它只是干预目标地址。例如：

```
#Exim filter
if $header_subject: contains SAGE or $header_subject: contains sysadmin
then
    save $home/mail/sage-sysadmin
endif
```

有许多可用选项可以控制用户在相应的 `.forward`文件中可以做什么和不能做什么。选项名称以 `forbid_`或 `allow_`开头。这些选项对于防止用户在不应该的情况下运行 shell、将库加载到二进制文件中或使用嵌入的 Perl 解释器至关重要。升级时请检查新的 `.forward_`选项，以确保你的用户无法在 `.forward`文件中玩得太花。

## 传输层 Transports

路由器决定邮件应该去哪里，而传输层实际上将它们送往那里。本地传输层通常是追加到文件、管道到本地程序，或通过 LMTP 协议与 IMAP 服务器通信。远程传输层通过 SMTP 与跨互联网的对端通信。

Exim 有五种传输层：`appendfile`、`lmtp`、`smtp`、`autoreply`和 `pipe`；我们将详细介绍 `appendfile`和 `smtp`。`autoreply`传输层通常用于发送休假回复邮件，`pipe`传输层将邮件作为通过 UNIX 管道的命令的输入。根据规则，你必须定义传输层的实例，并且拥有多个相同类型的传输层实例是可以的。对于路由器来说，顺序很重要，但对于传输层则不然。

### appendfile 传输层

`appendfile`驱动将邮件存储在指定文件或目录的 mbox、mbx、Maildir 或 mailstore 中。在编译 Exim 时，必须包含相应的邮件邮箱格式；默认情况下它们在 `EDITIME`文件中被注释掉了。以下示例定义了 `my_local_delivery`传输层 `appendfile`传输层的一个实例，在第821页的 `localusers`路由器实例定义中被引用。

```
my_local_delivery:
driver = appendfile
file = /var/mail/$local_part
delivery_date_add
envelope_to_add
return_path_add
group = mail
mode = 0660
```

各种 `*_add`行向邮件添加头。`group`和 `mode`子句确保传输代理可以写入文件。

### smtp 传输层

`smtp`传输层是任何邮件系统的核心。在这里我们定义了两个实例，一个用于标准 SMTP 端口 `25`，另一个用于邮件提交端口 `587`。

### 本地扫描函数

```
my_remote_delivery:
driver = smtp
my_remote_delivery_port587:
driver = smtp
port = 587
headers_add = X-processed-by: MACRO_HEADER port 587
```

第二个实例 `my_remote_delivery_port587`指定了端口，并向邮件中添加一个头，其中包含对输出端口的指示。`MACRO_HEADER`会在配置文件的其他定义。

## 重试配置 Retry configuration

配置文件中的 `retry`部分必须存在，否则 Exim 将永远不会尝试重递第一次尝试未投递的邮件。你可以指定三个时间间隔，每个间隔的频率比前一个低。在最后一个间隔过期后，邮件将作为不可投递退回给发送者。`retry`语句理解后缀 `m`、`h`、`d`和 `w`，分别表示分钟、小时、天和周。你可以为不同的主机或域名指定不同的间隔。

重试部分如下所示：

```
begin retry
  F, 2h, 15m; F, 24h, 1h; F, 4d, 6h
```

此示例意味着：“对于任何域名，临时失败的地址应每隔 15 分钟重试一次，持续 2 小时，然后在接下来的 24 小时内每小时重试一次，然后在 4 天内每 6 小时重试一次，最后作为不可投递退回。”

## 重写配置 Rewriting configuration

配置文件的重写部分以 `begin rewrite`开始。它用于修复地址，而不是重路由。例如，你可以在输出地址上使用它

* 让邮件看起来来自你的域名
* 将用户名映射到标准格式

## 本地扫描函数 Local scan function

如果你想进一步自定义 Exim，例如为了过滤病毒，你可以编写函数包含配置文件的 `local_scan`部分。参考 Exim 文档以了解如何

## amavisd 与 Exim 连接

要配置 Exim 将所有发往你域名的邮件发送到 `amavis`，配置文件中的第一个路由器类似于：

```
amavis:
  no_verify
driver = manualroute
condition = ${if [$interface_port]} [1025] \
    {eq [$received_protocol]} (scanned-ok) }}
domain = local_domains
transport = amavis
route_list = * localhost
self = send
```

该行表示将来自端口 1025 的邮件转发到 `amavis`。这是 `amavis`返回的端口，因此此类邮件无法返回 `amavis`而会产生循环。`amavis`传输层配置如下：

```
amavis:
  driver = smtp
port = 1024
allow_localhost
```

你还必须在设置全局选项的配置文件开头添加行

```
local_interfaces = 0.0.0.0:25 127.0.0.1:1025
```

告诉 Exim 接受来自任何地址 25 以及来自 `localhost`10025 的邮件，使用 `amavis`返回端口。

此配置会导致所有扫描离线进行，因为响应病毒和垃圾邮件生成的退回邮件可能会变成回弹。将 `amavis`放在路由器顺序列表的后期，让 Exim 的 ACL 语言处理简单轻量级的邮件检查可能是更好的解决方案。更好的方法是使用 Exim 的 `${run...}`来强制 `amavis`进行在线检查。Exim 内置的能力使得 `amavisd`不再那么必要。

## 日志 Logging

Exim 写入三种不同的日志文件：主日志 `main`、拒绝日志 `reject`和恐慌日志 `panic`。每条日志记录都包含写入时间。你在 `EDITME`文件 `构建 Exim 之前`或运行时配置文件的 `log_file_path`选项值中指定日志文件的位置。默认情况下，日志保留在 `/var/spool/exim/log`目录。

`log_file_path`选项最多接受两个冒号分隔的值。每个值必须是 `syslog`关键字或嵌入了 `%s`的绝对路径，其中可以替换为 `main`、`reject`和 `panic`的名称。例如，

## 调试

```
log_file_path = syslog /var/log/exim.log
```

将同时发送到 `syslog` `使用设施 "mail"`以及 `/var/log`目录下的 `exim_main`、`exim_reject`、`exim_panic`文件。Exim 以 `info`优先级提交主条目到 `syslog`，以 `notice`优先级提交拒绝条目，以 `alert`优先级提交恐慌条目。

主日志包含每条消息到达和投递的一行记录。它可以通过包含在 Exim 发行包中的 Perl 脚本 `eximstats`进行总结。

拒绝日志 `reject log`记录了因策略原因被拒绝的消息信息：例如恶意软件、垃圾邮件等。它包含了来自主日志的邮件摘要行，以及被拒绝消息的原始头信息。如果你更改了策略，请检查拒绝日志以确保其运行正常。

恐慌日志 `panic log`用于记录软件中的严重错误：`exim`在放弃运行前写入该日志。如果没有出现问题，恐慌日志不应该存在。如果存在，请让 `cron`检查它，修复导致恐慌的问题然后删除该文件。当下次发生足以恐慌的情况时，`exim`会重新创建它。

调试时，你可以通过 `log_selector = +smtp_connection -snmp_incomplete_transaction +...`等选项增加日志的数据量和类型：

`log_selector`机制可以包含或排除的日志类别列在 Exim 规范末尾的“Log files”部分。大约有 35 种可能，包括 `+all`，这会真的填满你的磁盘！

`exim`还为其处理的每条消息保留一个临时日志。它以消息 ID 命名并位于 `/var/spool/exim/mslog`。如果你在特定目标上遇到问题，应该检查那里。

## 调试

Exim 拥有强大的调试辅助工具。你可以配置想要关于每个潜在调试主题查看的信息量。`exim -d`告诉 `exim`进入调试模式，在该模式下，它将在前台运行且不与终端分离。你可以在特定的调试类别前加上 `+`或 `-`来增加详细程度或消除某个类别。例如，`-expand+acl`请求输出调试信息，提供关于字符串扩展和 ACL 解析的额外细节。`这两个类别是常见问题点`。你可以调整 30 多个调试页面的类别：列表请参见主页。

调试邮件系统的一种常用技术是在非标准端口上启动 MTA 并通过 `telnet`与其通信。例如，要以守护进程模式启动 `exim`，监听端口 26，并开启调试信息，请使用：

```
$ sudo exim -d -oX 26 -bd
```

然后你可以 `telnet`到 26 端口并输入 SMTP 命令，以尝试重现你正在调试的问题。

或者，你可以让 `swaks`为你处理 SMTP 通信。它是一个 Perl 脚本，让 SMTP 调试更快更简单。`swaks#help`可以为你提供一些文档，而 `jetmore.org/john/code/#swaks`提供了完整的细节。

如果你的日志文件显示大约 30 秒的超时，这表明可能是 DNS 超时。5 秒的超时更有可能是 `identd`查询超时。`identd`是一个旨在识别邮件消息实际发送者的守护进程，但由于它太容易被欺骗，现在没有人使用它。

## 20.15 POSTFIX

Postfix 是另一个流行的 `sendmail`替代方案。Wietse Verma 在 1996 年于 IBM 的 T. J. Watson 研究中心进行休年工作时启动了 Postfix 项目，他至今仍在活跃开发它。Postfix 的设计目标不仅包括安全性 `首要任务！`，还包括开源发布策略、快速性能、健壮性和灵活性。所有主流发行版都包含了 Postfix，而且从 10.3 版本开始，Mac OS X 已经转向 Postfix 而非 `sendmail`作为默认邮件系统。

关于 Postfix 最重要的知识点是：首先，它是开箱即用的 `简单的配置文件只有一两行`，其次，它利用正则表达式来有效地过滤邮件，特别是结合 `PCRE` `Perl 兼容正则表达式`库时。Postfix 与 `sendmail`兼容，体现在 Postfix 的别名和文件格式及语义与 `sendmail`相同。
