
```
mynetworks=192.168.0.0
relay_domains=$mydestination
```

连接到 Internet 的本地网络中的主机需要知道中继主机，即邮件服务器的身份。您使用 `relayhost` 参数设置此项。此外，`myorigin` 应仅设置为 `mydomain`。如果有 DNS 服务器将网关标识为邮件服务器，您只需将 `relayhost` 设置为 `mydomain` 的值。如果没有，则 `relayhost` 应设置为网关/邮件服务器的特定主机名。如果您的本地网络未运行 DNS 服务器，请确保将 `disable_dns_lookups` 设置为 `yes`。

```
relay_host=$mydomain
```

## 直接连接

如果您的系统直接连接到 Internet，并且您使用 ISP 接收邮件，您可以将 Postfix 配置为 null 客户端仅发送邮件。将 `relay_host` 参数设置为仅您的域名。此外，在 `master.cf` 文件中，注释掉 SMTP 服务器和本地投递代理条目。

```
relayhost = $mydomain
```

## 伪装

如果您的邮件服务器在本地网络的网关上运行，并且您希望隐藏该网络中的主机，您可以选择伪装本地主机，让它看起来所有邮件都来自域本身，而不是特定主机。要设置此选项，您使用 `masquerade_domains` 参数。在以下示例中，所有由本地主机如 `rabbit.mytrek.com` 发送的邮件都将被标记为仅来自 `mytrek.com`。因此，由用户 `chris@rabbit.mytrek.com` 发送的消息将被发送为来自 `chris@mytrek.com`。

```
masquerade_domains = $mydomain
```

默认情况下，收到的邮件不会被伪装。这允许 Postfix 仍然将收到的邮件投递到特定主机。如果您希望收到的邮件也被伪装，您必须将 `envelope_recipients` 参数添加到分配给 `masquerade_class` 参数的值列表中。在这种情况下，Postfix 将不再能够投递收到的邮件。

## 虚拟域

如果您的网络已实现虚拟域，您将需要设置一个虚拟域表，然后使用 `virtual_maps` 选项指定该表。设置表很简单，只需在文本文件如 `/etc/postfix/virtual` 中列出虚拟名称及其真实地址。然后使用 `postmap` 命令创建 Postfix 表：

```
postmap /etc/postfix/virtual
```

> NOTE 请参阅 www.postfix.org 上的 Postfix FAQ，了解如何为网关、本地工作站或直接连接到互联网的主机（null server）设置 Postfix 的详细说明。

## Security: UCM

Postfix 参数允许您配置控制其礼貌地称为未经请求的商业邮件（UCM）的方法。

## Controlling User and Host Access

使用访问文件，您可以控制特定用户、主机和域的访问权限。访问文件的工作方式与 Sendmail 使用的类似。条目在文本文件中创建，以用户、主机或域名或地址开头，后跟要采取的操作。可以接受、拒绝或带消息拒绝用户、主机或域。一旦条目创建完成，就可以使用 `postmap` 命令将其安装到 Postfix 数据库文件中：

```
postmap /etc/postfix/access
```

然后您可以在各种 Postfix 操作中使用访问文件来控制客户端、收件人和发件人。

## Blocking Access

访问也可以通过使用邮件滥用预防系统（MAPS）来控制，该系统提供 RBL+ 服务，这是一组基于邮件地址 DNS 的数据库（mail-abuse.org）。这些数据库，如实时黑洞列表（RBL），列出了已知被邮件滥用者使用的邮件地址。域或主机与服务维护的列表进行匹配。该服务可以访问本地服务器或直接从在线站点访问。各种 Postfix 操作允许您使用 MAPS 数据库来控制客户端、收件人、发件人的访问。

## Header and Body Checks

使用 `header_checks` 参数，您可以指定一个 Postfix 表，在其中列出拒绝消息的标准。标准是可以匹配消息头的模式。可以使匹配的消息被拒绝、带回复被拒绝、直接删除或记录警告。您可以选择执行多个操作，包括 `REJECT`、`DISCARD`、`WARN`、`HOLD` 和 `IGNORE`。

这将拒绝任何地址未解析的客户端；`permit_mynetworks`，允许由 `mynetworks` 定义的任何客户端访问；以及 `check_client_access`，它将检查访问数据库以查看是否应接受或拒绝客户端。`reject_rbl_client` 和 `reject_rhsbl_client` 将拒绝来自指定域的客户端。

```
smtpd_client_restrictions = permit_mynetworks, \
    reject_unknown_client, check_client_access, reject_maps_rbl
```

`reject_rbl_client` 限制基于指定的 MAPS 服务拒绝域地址。该站点可以是在线站点或设置提供该服务的本地站点。`reject_rhsbl_client` 限制拒绝主机地址。

```
smtpd_client_restrictions = reject_rbl_client relays.mail-abuse.org
```

要从访问文件实现限制，您可以使用 `hash` 指令和文件名。

```
smtpd_client_restrictions = hash:/etc/postfix/access
```

相应的 `smtpd_sender_restrictions` 参数的工作方式与客户端对应参数类似，但控制来自特定发件人的访问。它具有许多相同的限制，并增加了 `reject_non_fqdn_sender`，它将拒绝任何没有完全限定域名邮件头的邮件，以及 `reject_sender_login_mismatch`，它将要求发件人验证。`reject_rhsbl_sender` 限制基于指定的 MAPS 服务拒绝域地址。

`smtpd_recipient_restrictions` 参数将限制服务器将接受邮件的收件人。限制包括 `permit_auth_destination`，它允许授权消息，以及 `reject_unauth_destination`，它拒绝未授权消息。`check_recipient_address` 限制将检查本地网络的收件人地址，而 `check_recipient_maps` 将拒绝在列出本地、 relay 和虚拟收件人以及别名的收件人表中未验证的地址。`reject_unknown_recipient_domain` 限制拒绝没有 DNS 条目的收件人地址。`reject_rhsbl_recipient` 限制基于指定的 MAPS 服务拒绝域地址。

您可以使用诸如 `smtpd_helo_restrictions` 等参数进一步细化限制，它要求客户端发出 HELO 命令。限制参数包括 `reject_invalid_hostname`，它检查语法错误，`reject_unknown_hostname` 用于没有 DNS 条目的主机，以及 `reject_non_fqdn_hostname` 用于名称未完全限定的主机。`strict_rfc821_envelopes` 参数将实施严格的信封协议合规性。

## Sendmail

Sendmail 作为服务器同时接收和发送邮件消息运行。Sendmail 监听从其他主机接收并发送到其服务的网络主机上的用户的任何邮件消息。同时，Sendmail 处理用户发往远程用户的消息，确定将它们发送到哪些主机。您可以了解更多关于 Sendmail 的信息

在 www.sendmail.org 上，包括在线文档和当前软件包。Sendmail 新闻组是 comp.mail.sendmail。你也可以从 www.sendmail.com 获得商业版本。

你的网络设计中的域名服务器指定了运行 Sendmail 服务器的主机。这是你的邮件主机。消息发送到该主机，其 Sendmail 服务器然后将消息发送给适当的用户及其主机。在你的域名服务器配置文件中，邮件主机条目使用 MX 条目指定。要打印待将来投递的消息邮件队列，你可以使用 `mailq`（或 `sendmail -v -q`）。这会使用打印邮件队列的指令运行 Sendmail。

Sendmail 软件包包含用于管理你的 Sendmail 服务器的多个实用程序。其中包括 `mailq`，用于显示传出消息的队列；`mailstats`，显示邮件服务器使用统计；`hoststat`，提供与邮件服务器连接的远程主机的统计；以及 `praliases`，打印 `/etc/aliases` 文件中列出的邮件别名。其中一些，如 `mailq` 和 `hoststat`，只是以某些选项调用 Sendmail。其他，如 `mailstats` 和 `praliases`，是独立的程序。
