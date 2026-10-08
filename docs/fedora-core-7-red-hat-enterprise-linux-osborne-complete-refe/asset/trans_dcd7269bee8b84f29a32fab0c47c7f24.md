

Postfix 并非实现为单个大型程序，而是由一系列较小的程序组成，每个程序都旨在执行特定的与邮件相关的任务。Postfix 主守护进程持续运行，并管理其他 Postfix 守护进程的使用，仅在需要时运行它们。**退信（bounce）**守护进程处理无法投递的邮件，**简单重写（trivial-rewrite）**守护进程重定向消息，而**showq**守护进程则提供关于打印队列的信息。

## Postfix 命令

多个 Postfix 命令允许你管理服务器任务。**sendmail** 命令用于发送消息。你使用 **mailq** 来显示邮件队列的状态。**newaliases** 命令获取别名文件中列出的邮件别名，并将其存储在一个可被 Postfix 使用的数据库文件中。**postmap** 命令用于维护 Postfix 使用的各种数据库文件，例如用于邮件别名的别名文件以及限制服务器接收消息的访问文件。此外，Postfix 提供了较低级别的工具，所有这些工具的名称都以 **post** 开头，例如维护别名数据库的 **postalias** 命令，以及显示打印队列文件的 **postcat**。

## Postfix 配置：main.cf

Postfix 的配置是通过在其配置文件 **main.cf** 中设置参数来处理的。Fedora 安装 Postfix 时附带一个默认的 /etc/postfix/main.cf 文件，其中已设置了大多数基本配置值。参数名称通常对用户比较友好。例如，目录位置由以 _directory 结尾的参数指定，例如 **queue_directory** 指定 Postfix 队列的位置，**daemon_directory** 指定 Postfix 守护进程的位置。大多数参数都已实现默认值。例如，为特定的资源控制（如消息大小、时间限制和每个队列允许的消息数量）设置了默认值。你可以编辑 **main.cf** 文件以更改参数值，从而满足自己的需求。进行任何更改后，你只需使用 **postfix reload** 命令重新加载配置即可：

```
postfix reload
```

### 网络参数

你很可能需要设置几个网络参数。为了简化这一过程，Postfix 定义了一些持有关键网络信息的参数，例如 **myhostname**（保存你的系统的主机名）和 **mydomain**（保存你的网络域名）。例如，**myhostname** 将被设置为主机 **turtle.mytrek.com**，而 **mydomain** 则仅为 **mytrek.com**。像 **myhostname** 和 **mydomain** 这样的参数本身也被用作分配给其他参数的值。在下例中，**myhostname** 和 **mydomain** 被设置为邮件服务器运行所在的主机及其网络域名：

```
myhostname=turtle.mytrek.com
mydomain=mytrek.com
```

**myorigin** 参数指定服务器发送电子邮件的来源地址。默认情况下，这被设置为参数 **myhostname** 的值，如下所示。请注意，**myhostname** 变量前有一个 $ 符号以对其进行求值。

```
myorigin=$myhostname
```

如果你使用的是直接连接到互联网的单台系统，你可能希望保留此配置，将邮件标记为由你的主机发送。然而，如果你的系统作为网络的网关运行，你的邮件服务器正在从该网络上的不同主机发送邮件。你可能希望将源地址更改为域名，以便邮件被视为来自该域名。

```
myorigin=$mydomain
```

### 本地网络

**mydestination** 参数保存你的邮件服务器将接收邮件的域名列表。默认情况下，这些包括 **localhost** 和你系统的主机名。

```
mydestination = $myhostname localhost.$mydomain
```

如果希望邮件服务器接收整个本地网络的邮件，还需要指定其域名。这样，服务器就可以接收仅发送到该域名的邮件，而不仅仅是发送到特定主机的邮件。

```
mydestination = $myhostname localhost.$mydomain $mydomain
```

此外，如果你的主机有其他主机名，并且有 DNS 记录通过那些名称识别你的主机，则需要指定这些名称。例如，你的主机也可以是一个可以接收邮件的 Web 服务器。主机 **turtle.mytrek.com** 也可以被标识为网站 **www.mytrek.com**。这两个名称都必须列在 **mydestination** 参数中。

```
mydestination = $myhostname localhost.$mydomain $mydomain www.$mydomain
```

如果你的系统是本地网络的一个或多个网络的网关，你可以使用 **mynetworks** 参数指定它们。这允许你的邮件服务器中继发送给这些网络的邮件。网络使用其 IP 地址进行指定。**relay_domains** 参数允许你指定可以中继消息的网络的域名地址。默认情况下，这被设置为 **mydestination**：

```
mynetworks=192.168.0.0
relay_domains=$mydestination
```

通过网关连接到互联网的本机网络中的主机需要知道中继主机（邮件服务器）的身份。你使用 **relayhost** 参数设置这一点。此外，**myorigin** 应仅设置为 **mydomain**。如果有 DNS 服务器将网关标识为邮件服务器，你可以直接将 **relayhost** 设置为 **mydomain** 的值。如果没有，则 **relayhost** 应设置为网关/邮件服务器的特定主机名。如果你的本地网络未运行 DNS 服务器，请确保将 **disable_dns_lookups** 设置为 **yes**。

```
relay_host=$mydomain
```

### 直接连接

如果你的系统直接连接到互联网，并且你使用 ISP 接收邮件，你可以将 Postfix 配置为 null 客户端，仅用于发送邮件。将 **relay_host** 参数设置为仅你自己的域名。此外，在 **master.cf** 文件中，注释掉 SMTP 服务器和本地投递代理条目。

```
relayhost = $mydomain
```

## 伪装

如果你的邮件服务器在本地网络的网关上运行，并且你想隐藏该网络中的主机，可以选择对本地主机进行伪装，使其看起来所有邮件都来自该域名，而不是来自特定主机。要设置此选项，请使用 `masquerade_domains` 参数。在以下示例中，由本地主机（如 *rabbit.mytrek.com*）发送的所有邮件都将仅显示为来自 *mytrek.com*。因此，由用户 *chris@rabbit.mytrek.com* 发送的消息将以 *chris@mytrek.com* 的身份发出：

```
masquerade_domains = $mydomain
```

默认情况下，接收到的邮件不会被伪装。这允许 Postfix 仍将接收到的邮件投递到特定主机。如果你希望接收到的邮件也被伪装，你需要将 `envelope_recipients` 参数添加到分配给 `masquerade_class` 参数的值列表中。在这种情况下，Postfix 将不再能够投递接收到的邮件。

## 虚拟域名

如果你的网络已实施虚拟域名，你需要设置一个虚拟域名表，然后使用 `virtual_maps` 选项指定该表。设置表很简单，只需在诸如 /etc/postfix/virtual 之类的文本文件中列出虚拟名称及其真实地址即可。然后使用 `postmap` 命令创建 Postfix 表：

```
postmap /etc/postfix/virtual
```

在 main.cf 文件中，使用 `virtual_maps` 参数指定该表。Postfix 然后使用此表来查找虚拟域名。

```
virtual_maps = hash:/etc/postfix/virtual
```

> **注意** 有关如何为网关、本地工作站或直接连接到互联网的主机（null server）设置 Postfix 的详细信息，请参阅 www.postfix.org 上的 Postfix FAQ。

## 访问控制

域可以被接受、拒绝或拒绝并附带消息。一旦创建条目，就可以使用 postmap 命令将它们安装到 Postfix 数据库文件中：

```
postmap /etc/postfix/access
```

然后，你可以在各种 Postfix 操作中使用访问文件来控制客户端、收件人和发件人。

也可以通过使用邮件滥用防御系统（MAPS）来控制访问，该系统提供 RBL+ 服务，这是一个基于 DNS 的邮件地址数据库集合（mail-abuse.com）。这些数据库（如实时黑洞列表（RBL））列出了已知被邮件滥用者使用的邮件地址。域名或主机将与由该服务维护的列表进行匹配，该服务可以在本地服务器上访问，也可以直接从在线网站访问。各种 Postfix 操作允许你使用 MAPS 数据库来控制客户端、收件人或发件人的访问。

## 头部和正文检查

使用 header_checks 参数，你可以指定一个 Postfix 表，在其中列出拒绝消息的标准。有关详细信息，请检查 /etc/postfix/header_checks 文件。标准是可以匹配消息头部的模式。你可以选择拒绝匹配的消息、拒绝并回复、直接删除或记录警告。你有选择采取多种操作的选项，包括 REJECT（拒绝）、DISCARD（丢弃）、WARN（警告）、HOLD（保留）和 IGNORE（忽略）。

```
header_checks = regexp:/etc/postfix/header_checks
```

数据库（在此情况下为 /etc/postfix/header_checks）将包含行，每行包含一个正则表达式和相应的操作。正则表达式可以是 header_checks 参数中指定的标准正则表达式（见第 8 章）（由 regexp 表示），或者符合 Perl 兼容正则表达式（prece）。

body_checks 参数允许你使用正则表达式和类似 header_checks 的操作，逐行检查文本消息的正文，使用 /etc/postfix/body_checks 文件。

## 控制客户端、发件人和收件人

使用 smtpd_client_restrictions 参数，你可以限制特定客户端对邮件服务器的访问。你可以应用的限制包括 reject_unknown_client_hostname（拒绝地址未解析的任何客户端）、permit_mynetworks（允许由 mynetworks 定义的任何客户端访问）以及 check_client_access（检查访问数据库以确定是否应接受或拒绝客户端）。reject_rbl_client 和 reject_rhsl_client 参数将拒绝来自指定域的客户端。

```
smtpd_client_restrictions = permit_mynetworks, \
reject_unknown_client, check_client_access, reject_maps_rbl
```

reject_rbl_client 限制根据指定的 MAPS 服务拒绝域名地址。该站点可以是提供此服务的在线站点或本地站点。reject_rhsl_client 限制拒绝主机地址。

```
smtpd_client_restrictions = reject_rbl_client relays.mail-abuse.org
```

