
`10.10.10.10:allow,RELAYCLIENT="`

然后运行

```
tcprules /etc/tcp.smtp.cdb /etc/tcp.smtp.tmp < /etc/tcp.smtp
```

添加 `-x /etc/tcp.smtp.cdb`

Postfix 一直默认拒绝中继。事实上，在首次运行它之前，必须配置你允许接收邮件和发送邮件的网络，这对应于 `main.cf` 中的 `hostname`、`mydomain`、`myorigin`、`mydestination` 和 `mynetworks` 变量。对于许多系统来说，这些是你唯一需要处理的变量，以获得有效的 Postfix 配置。

不幸的是，由于 SMTP 服务器并不了解实际的邮件投递情况，早期的版本（1999 年之前的版本）在假设进行中继时不会响应 SMTP 错误。因此，像 ORBS 或 RBL 这样的中继检查器可能会认为它是开放中继。请升级到较新版本的 Postfix 以避免此问题。

## 第 11 章：邮件与 FTP 安全

### 垃圾邮件 (Spam)

| 流行度 | 10 |
| :--- | :--- |
| 简单性 | 10 |
| 影响 | 4 |
| 风险评分 | 8 |

垃圾邮件浪费了你的磁盘空间，消耗了带宽，并无故占用了你的 CPU。许多资深系统管理员被迫编写复杂的 `Procmail` 规则，以防止系统因过度使用而陷入崩溃。（任何使用鼠标删除邮件的人都不是资深管理员，可能连 `Procmail` 碰都不会碰。）垃圾邮件通常包含 HTML 代码，旨在将你自动重定向到违规者的网站、收集关于你的数据、使用 Web 虫验证有效地址，或者仅仅渲染你的浏览器功能栏，让你无法逃避它们。单条垃圾邮件本身可能包含攻击，也可能不，但我们认为它们没有理由使用你的系统资源。

### 拦截垃圾邮件

防止垃圾邮件最广泛的方法是 MAPS（邮件滥用防御系统——为了记忆，“spam”反过来写就是 maps）实时黑洞列表，或 RBL (<http://mail-abuse.org/rbl/>)，它最初由 Paul Vice 创建。这是一个通过 DNS 可访问的服务，列出了已知的垃圾邮件发送者或被垃圾邮件发送者使用的开放中继机器。采用 DNS 垃圾邮件防护的邮件服务器会对所有连接到它的机器 IP 地址进行 DNS 查询。如果该 IP 已注册，将不接受来自它的邮件。位于 <http://www.orbs.org/> 的 Orbs 行为修改系统是另一个流行的数据库，仅列出开放中继。

在下面的示例中，我们将展示如何使用域名 `rbl.maps.vix.com` 启用 RBL 保护。对于其他 MAPS 和 ORBS 域名，请查看各自的网页。

#### Sendmail 垃圾邮件防护

你可以通过向 `sendmail.mc` 添加行来增加垃圾邮件防护。每个版本的 Sendmail 语法均不同。

| 版本 | 配置 |
| :--- | :--- |
| 8.9 | `FEATURE(rbl, rbl.maps.vix.com)` |
| 8.10 | `FEATURE(dnsbl, rbl.maps.vix.com, error message)` |
| 8.11 | `HACK(check_dnsbl, rbl.maps.vix.com, general, reason)` |

#### Linux 攻防解析：Linux 安全密钥与解决方案

**小型垃圾邮件防护**

`Rblmsmtpd` (<http://cr.py.to/ucspi-tcp/rblmsmtpd.html>) 与 `qmtpd` 配合工作，拦截 RBL 样式数据库中列出的站点。`Rblmsmtpd` 由 `tcpserver` (`inetd`) 启动并对连接的机器进行 DNS 查询。如果该机器不在数据库中，则启动实际 `smpd` 程序。你必须重写你的 `tcpserver` 连接以允许 `rblmsmtpd`，如下：

```
tcpserver <options> smtp /usr/bin/rblmsmtpd -b \- r "relays.mail-abuse.org Open relay problem" //var/bin/qmail-smtpd <options>
```

#### Postfix 垃圾邮件防护

要启用基于 DNS 的垃圾邮件防护，首先将 `maps_rbl_domains` 变量设置为你想要查询的域名，例如：

`maps_rbl_domains = rbl.maps.vis.com, dul.maps.vis.com`

然后简单地在 `smtp_client_restrictions` 后面追加 `"reject_maps_rbl"`，例如：

`smtp_client_restrictions = permit_mynetworks, reject_maps_rbl`

其他其他限制请参考 Postfix 文档。

### 邮件炸弹 (Mail Bombs) 与拒绝服务攻击

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 8 |
| 风险评分 | 7 |

如果黑客决定对你不利，他可以通过泛洪 SMTP 端口或用大量邮件填充队列（即邮件炸弹）来实施拒绝服务（DoS）攻击，迅速消耗你的磁盘空间。由于这些通常位于 `/var`，如果满了会产生灾难性影响。系统日志将无处可去，最终你的机器可能会死机。

### Sendmail 的资源限制

有多种 Sendmail 选项可以限制守护进程使用的资源：

| 选项 | 描述 |
| :--- | :--- |
| `MaxDaemonChildren` | 限制运行的 Sendmail 进程数量。有助于保护 CPU 利用率。 |

### 邮件与 FTP 安全

| 选项 | 描述 |
| :--- | :--- |
| `ConnectionRateThrottle` | 限制每秒允许的入站连接数。 |
| `MaxRcptsMessage` | 限制单封邮件接收者的数量。对防止构造垃圾邮件很有用。 |
| `MaxMessageSize` | 拒绝过大的邮件。如果你经常交换大文件，可能会有问题；但服务通常通过 HTTP 完成。 |

将这些变量设置得太低会导致邮件延迟或被拒绝，因此在设置之前请检查邮件日志以确定使用情况。

### Qmail 的资源限制

Qmail 默认允许同时处理 20 封发送邮件。如果你有大量的发送邮件（例如你在支持邮件列表），你可能需要以此释放磁盘空间。只需将希望支持的并发发送数放入 `/var/qmail/control/conrenclimit` 文件并重启 Qmail。编译时限制为 120，但你可以在运行时通过 `config.conf` 进行更改。

Qmail 不强制执行额外的限制。Bernstein 认为你应该直接通过 `/etc/limits.conf` 实施限制，并使用 `edquota` 对 `/var` 定义配额。

# 破解 Linnx 暴露：Linux 安全秘密与解决方案

`smtp - inet n - - - 10 smtpd`

我们限制了机器，使其在任何时候都不允许超过十个并发 SMTP 消息。其他 `cf` 变量包括：

| 变量 | 描述 |
| :--- | :--- |
| `local_destination_concurrency_limit` | 同时投送给同一接收者的消息数量。 |
| `default_destination_concurrency_limit` | 可能同时发送给同一接收者的消息总数。 |
| `message_size_limit` | 任何大于此大小的消息都将被拒绝。 |
| `bounce_size_limit` | 在发生退信时，回传给发送者的消息部分大小。发送整个消息可以被认为是昂贵且不必要的。 |
| `queue_minfree` | 队列文件系统应留出多少空间；用于在文件系统填满之前停止 Postfix 接收新消息。 |

还有许多其他变量可以根据喜好进行调整。请查看文档以及访问 <http://www.postfix.org/resource.html> 和 <http://www.postfix.org/rate> 了解资源和速率限制选项。

# Postfix 全局可写邮件投递目录 (Maildrop Directory)

| 流行度: 5 |
| :--- |
| 简单性: 5 |
| :--- |
| 影响: 4 |
| :--- |
| 风险评分: 5 |

在最初发布时，Postfix 吹嘘其套件中没有任何程序被设置了 `setuid` 或 `setgroup`。所有投递的邮件都由其中一个 Postfix 程序写入邮件投递目录，然后由一个独立的 Postfix 守护进程拾取并进行适当的投递。

# 第 11 章：邮件与 FTP 安全

然而，为了让所有用户都能发送邮件，他们需要能够写入此目录，这意味着它需要具有全局可写权限。`/tmp` 设置了粘滞位（sticky bit），是为了确保用户在邮件被设置之前无法删除他人的邮件。遗憾的是，该系统仍然可能受到其他邮件相关的攻击。

Postfix 会丢弃邮件目录中任何具有多个硬链接的文件。由于该目录是全局可写的，任何人都可以为队列中的文件添加额外的链接。这些文件（电子邮件）将被删除且永远不会发送，并且不会向用户发送任何警告。
