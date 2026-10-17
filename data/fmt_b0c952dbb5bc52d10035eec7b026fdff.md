
## 访问控制列表 (ACL)

访问控制列表过滤地址和消息。它们可用于阻止垃圾邮件、限制连接速率并根据发送者、接收者或内容执行策略。

## 第 18 章 电子邮箱

下面定义了一个名为 `my_acl_check_rcpt` 的示例 ACL。我们通过将它的名称赋值给配置文件中的 `acl_rcpt` 选项来调用它。

## Exim

此 `accept` 语句保证了发送到本地域名的发 postmaster 的邮件总能被送达，这有助于调试。

```
require verify = sender
```

`require` 行检查是否可以返回退信邮件；然而，它只检查发送者的域名。1 18 如果发送者的用户名被伪造，退信邮件仍可能失败；即，退信邮件本身可能会被退回。你可以通过调用另一个程序添加更广泛的检查，但某些站点认为主机存在滥用行为，可能会将你的邮件服务器加入黑名单或不良声誉列表。

```
accept hosts = +relay_from_hosts
control = submission
control = dkim_disabled_verify
```

上述 `accept` 语句检查允许通过此主机进行中继的主机，以及向系统提交邮件的本地主机。`control` 行指定 Exim 应该充当邮件提交代理，并在消息从用户代理到达时修复任何标头缺陷。由于不检查收件人地址，因为许多用户对错误返回感到困惑。（这部分配置仅适用于中继到智能主机的本地机器，而不适用于你可能愿意为其中继的任何外部域。）禁用 DKIM 验证是因为这些邮件是由你的用户或中继伙伴发出的邮件。

```
accept authenticated = *
control = submission
control = dkim_disabled_verify
```

最后一个 `accept` 语句处理通过 SMTP `AUTH` 进行身份验证的本地主机。再次，这些邮件被视为来自用户代理的提交内容。

```
require message = Relay not permitted

domains = +local_domains : +relay_to_domains
```

```
require verify = recipient
```

在这里，我们检查消息发往的目标域名，并要求它要么在我们的本地域名列表中，要么在我们的允许中继的域名列表 `relay_to_domains` 中。（这些域名列表是在 ACL 上文之外定义的。）任何不在这些列表中的目标地都将通过自定义错误消息被拒绝。

```
accept
```

最后，在满足所有之前的先决条件但没有触发更具体的 `accept` 或 `deny` 规则的情况下，我们验证收件人并接受该消息。某些发给本地用户的 Internet 消息属于此类。

> 18. `require` 意味着“如果如果未匹配则拒绝”。

我们在上面的示例中没有包含任何黑名单扫描。要访问黑名单，请使用默认配置文件中的示例之一或类似的内容：

```
deny condition = ${if ip4($sender_host_address)}

  authenticated = *

  !hosts = +my_whitelist_ips

  dnslists = list.dnswl

domains = +local_domain

  verify = recipient

  message = You are on RBL $dnslist_domain: $dnslist_text

dnslists = zen.spamhaus.org

logfile = Blacklisted sender [$sender_host_address] \

  $dnslist_domain: $dnslist_text
```

翻译成英文，该代码指定如果消息符合所有以下标准，将用自定义错误消息将其拒绝并记录（同时也带有自定义消息）：

- 它来自一个 IPv4 地址（某些列表无法正确处理 IPv6）。
- 它未与身份验证的 SMTP 会话关联。
- 它来自不在本地白名单中的发送者。
- 它来自不在全局（Internet）白名单中的发送者。
- 它的地址是一个有效的收件人。
- 发送主机在 zen.spamhaus.org 黑名单上。

变量 `dnslist_text` 和 `dnslist_domain` 通过赋值给 `dnslists` 设置，这会触发黑名单查找。此 `deny` 子句可以放在你对地址中异常字符的检查之后。

这是另一个 ACL，如果远端没有正确说 `HELO`，则会拒绝邮件：

```
acl_check_mail:
  deny message = 503 Bad command - must send HELO/EHLO first
  condition = ${if def!sender_hello_name}
  accept
```

Exim 通过 `smtp_enforce_sync` 选项解决了前面提到的问题（“未正确说 `HELO`”的更具体情况），该选项默认开启。

## 在 ACL 期间进行内容扫描

Exim 在邮件遍历邮件系统的过程中的几点支持强大的内容扫描：在 ACL 期间（SMTP `DATA` 命令之后）；通过 `transport_filter` 选项，或在完成所有 ACL 检查后使用 `local_scan` 函数进行交付。你必须通过设置 Exim 中的 `WITH_CONTENT_SCAN` 变量来为 Exim 编译内容扫描支持；它默认是被注释掉的。此选项赋予了 ACL 额外的力量和灵活性，并增加了两个新的配置选项：`spamd_address` 和 `av_scanner`。

在 ACL 期间扫描允许消息在 MTA 与发送主机的会话中直接被拒绝。消息永远不会被接受交付，因此不需要退回。这种拒绝消息的方法很好，因为它避免了由于向伪造发送者地址发送退信邮件引起的反射垃圾邮件（backscatter spam）。

## 身份验证器 (Authenticators)

身份验证器是与 SMTP `AUTH` 命令的挑战响应序列交互的驱动程序，并识别客户端和服务器都能接受的身份验证机制。Exim 支持以下机制：

- `AUTH_CRAM_MD5` (RFC2195)
- `AUTH_PLAINTEXT`
- `AUTH_PLAIN`

（注：原文此处存在大量重复错误，已进行清理以反映逻辑内容。）

## `accept` 路由器 (`accept` router)

`accept` 路由器将地址标记为 OK 并将关联的消息传递给传输驱动（transport driver）。以下是 `accept` 路由器的实例示例：`localcallers` 用于投送本地邮件，`save_to_file` 用于追加到归档。

```
localcallers:
driver = accept
domains = example.com
check_local_user
transport = my_local_delivery
```

```
save_to_file:
driver = accept
domains = dialup.example.com
transport = batchsmtp_appendfile
```

`localusers` 路由器实例检查目标地址的域名部分是否为 example.com，以及地址的本地部分是否为本地用户的登录名。如果同时满足这两个条件，路由器会将消息传递给名为 `my_local_delivery` 的传输驱动，该驱动程序定义在 `transports` 部分。`save_to_file` 实例专为拨号用户设计；它会将消息追加到 `batchsmtp_appendfile` 指定的文件。

## `dnslookup` 路由器 (`dnslookup` router)

`dnslookup` 路由器通常处理发送的消息。它查找收件者域名的 MX 记录，并将消息传递给 SMTP 传输驱动进行投递。这是一个名为 `remoteusers` 的实例：

```
remoteusers:
driver = dnslookup
domains = !example.com
transport = my_remote_delivery
```
