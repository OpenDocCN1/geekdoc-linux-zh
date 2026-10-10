
我该如何解决这个问题？

你通过 MX 记录向邮件服务器发送给该域（例如 `domain.net`）的邮件，并要求其被转发到特定主机（在此例中为 `relay.domain.net`），但中继机器没有将自己识别为 `domain.net`。在 `/etc/mail/local/host-names`（在 8.10 版本之前名为 `/etc/sendmail.cw`）中添加 `domain`（如果你在使用 `FEATURE(use_cw_file)`），或者在 `/etc/mail/sendmail.cf` 中添加 `"Cw domain.net"`。

`sendmail` FAQ 位于 http://www.sendmail.org/faq/，如果你想对你的邮件设置进行任何“调优”，建议阅读。

### 3. 我如何在拨号号 PPP 主机上运行邮件服务器？

你可以将位于局域网的 FreeBSD 设备连接到互联网。该 FreeBSD 机器将成为局域网的邮件网关。PPP 连接是非专用的。

这样做至少有两种方法。一种是使用 UUCP。

另一种方法是获取一个全时的互联网服务器为你的域提供辅助 MX 服务。例如，如果你的公司域是 `example.com`，而你的互联网服务提供商有 `example.net` 为你的域提供辅助 MX 服务：

| example.com. | MX 10 |
| example.net. | MX 20 |

对于最终接收者应只指定一个主机（在 `example.com` 的 `/etc/mail/sendmail.cf` 中添加 `C example.com`）。

当 `sendmail` 尝试投递邮件时，它将尝试通过现代链路连接到（你的）`example.com`。它很可能会超时，因为你没有在线。`sendmail` 程序将自动将其投递到辅助 MX 站点，即你的互联网提供商（`example.net`）。辅助 MX 站点随后将定期连接到你的主机并将邮件投递到主 MX 主机（`example.com`）。

你可能想使用类似下面的脚本：

```bash
#!/bin/sh

# 将我放在 /usr/local/bin/bppymisp

( sleep 60 ; /usr/sbin/sendmail -q ) &

/usr/sbin/ -direct bppymisp
```

如果你要为用户创建一个单独的登录脚本，可以使用 `sendmail -qReExample.com` 代替上面的脚本。这将强制立即处理队列中所有针对 `example.com` 的邮件。

该情况的改进如下：

消息摘自 FreeBSD 服务提供商的邮件列表（http://lists.FreeBSD.org/maillist/getinfo/freebsd-org）。

- > 我们为客户提供辅助 MX。客户每天自动连接到我们的服务几次，以获取邮件投递到他的主 MX（当他的域有邮件到达时，我们不会打电话通知他。我们的 `sendmail` 每 30 分钟发送一次邮件队列。目前，他必须在线 30 分钟以确保所有邮件都已送达主 MX）。
- > 是否有命令可以启动 `sendmail` 立即发送所有邮件？当然，该用户在我们的机器上没有 root 权限。

在 `sendmail.cf` 的“隐私标志”（privacy flags）部分中，有一个定义 `Opgoaway,restrictqrun`。移除 `restrictqrun` 以允许非 root 用户启动队列处理。你可能还喜欢调整：

### 4. 为什么我一直收到 Relaying denied（拒绝中继）？

在 `sendmail.cf` 的“隐私标志”部分中，有一个定义 `Opgoaway,restrictqrun`。移除 `restrictqrun` 以允许非 root 用户启动队列处理。你可能还喜欢调整：

## 第 24 章 电子邮件

为了发挥最大的效用，备用 MX 站点应该具有与你不同的 Internet 网络连接。你的 ISP 或另一个友好的站点应该能够轻松地为你提供这项服务。

### 24.6.2 您的域名的邮件

为了设置一个“邮件主机”（mailhost，即邮件服务器），你需要将任何发送到你工作站的邮件都指向该主机。基本上，你希望“接管”域域内任何主机名（在本例中为 `*.BSD.org`）的邮件，并将其重定向到你的邮件服务器，以便你的用户可以在邮件服务器上接收邮件。

为了方便起，在两台机器上都应该存在一个具有相同用户名的用户。使用 `adduser(8)` 来完成此操作。

邮件主机将是你在网络上每个连接的指定交换器。在你的 DNS 配置中如下所示：

```
example.FreeBSD.org A 204.216.27.XX ; Workstation MX 10 hub.FreeBSD.org ; Mailhost
```

这将把发往邮件主机的邮件重定向到 A 记录指向的任何地方。邮件会被发送到 MX 主机。

除非你运行 DNS 服务器，否则你无法执行此操作。如果你没有或无法运行自己的 DNS 服务器，请联系你的 ISP 或任何提供 DNS 服务的机构。

如果你正在进行虚拟邮件托管，以下信息将非常有用。在此示例中，我们假设你有一个拥有自己领域的客户（在本例中为 `customer.org`），你希望所有发送给 `customer.org` 的邮件都到达你的邮件主机 `mail.myhost.com`。你的 DNS 条目应该如下：

```
customer.org MX 10 mail.myhost.com
```

如果你只想处理该域的电子邮件，则不需要为 `customer.org` 创建 A 记录。

> 注意：请注意，除非为 `customer.org` 存在 A 记录，否则对等将无法工作。

你必须做的最后一件事是告诉邮件主机上的 `sendmail` 哪些域名和/或主机名应该接收邮件。有几种不同的方法。以下任一方法均可行：

- 如果你使用 `FEATURE(use_cw_file)`，请将主机添加到 `/etc/mail/local-host-names` 文件。如果你使用的是早于 8.10 版本的 `sendmail`，该文件是 `/etc/sendmail.cf`。
- 如果使用的是 `sendmail` 8.10 或更高版本，请向 `/etc/sendmail.cf` 或 `/etc/mail/sendmail.cf` 添加一行 `Cyour.host.com`。

### 24.7 使用 UUCP 的 SMTP 邮件

FreeBSD 自带的 `sendmail` 配置适用于直接连接到 Internet 的站点。希望通过 UUCP 交换邮件的站点必须安装另一个 `sendmail` 配置。

手动调整 `/etc/mail/sendmail.cf` 是一个高级主题。`sendmail` 版本 8 通过 `m4(1)` 预处理生成配置文件，实际配置发生在更高层次的抽象上。`m4(1)` 配置可以在 `/usr/src/usr.sbin/sendmail.cf` 下找到。

如果你在安装系统时没有使用箔片（foils），则 `sendmail` 配置集已被拆分到独立的发行 tar 包中。假设你已经挂载了 BSD 源码 CD-ROM，

```
# cd /cdrom/src
# cat sendmail.cf?? | tar xf -C /usr/src/contrib/sendmail
```

这仅提取出几百 KB。`cf` 目录下的 `README` 可以作为 `m4(1)` 配置的基础入门介绍。

支持 UUCP 投递的最佳方法是通过 `mailtable` 文件。这是 `sendmail` 可用于做出路由决策的数据库。

首先，你创建了你的 `.mc` 文件吗？目录 `/usr/src/usr.sbin/sendmail/cf/cf` 包含了一些示例。假设你将文件命名为 `foo.mc`，你只需要执行以下操作将其转换为有效的 `sendmail.cf` 并：

```
# cd /usr/src/usr.sbin/sendmail/cf/cf
# make foo.cf
# cp foo.cf /etc/mail/sendmail.cf
```

一个典型的 `.mc` 文件可能如下：

```
VERSIONID('Your version number') OSTYPE(bsd4.4)

FEATURE(accept_unresolvable_domains)

FEATURE(nocanonify)

FEATURE(mailtable, 'hash -o /etc/mail/mailtable')
```

```
define('UUCP_RELAY', your.uucp.relay)

define('UUCP_MAX_SIZE', 200000)

define('CONFDONT_PROBE_INTERFACES')
```

MAILER (local)
MAILER (smtp)
MAILER (uucp)

Cw your.alias.host.name
Cw youruucpnodomain.UUCP
