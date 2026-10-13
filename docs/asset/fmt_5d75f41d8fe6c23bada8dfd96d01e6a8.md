
如果你有一台 `majordomo` 流量非常大的机器，你可以考虑对传入邮件使用 `sendmail`，对传出邮件使用 `qmail`。只要在安装 `qmail` 时注意不要创建 `sendmail` 包装器即可。

### Qmail 用户 ID 和配置文件

`Qmail` 为其进程使用多个 Linux 用户 ID。这些 ID 在从 `rpm` 安装 `qmail` 时创建，同时也会创建所有必要的目录。

配置文件位于 `/var/qmail/control/`。与仅有一个或很少几个控制文件的其他 MTA 不同，`qmail` 将每个参数或参数组保存在单独的文件中。唯一必不可少的文件是 `me`，其中包含完全限定的本地主机名。如果你想将所有传出邮件通过邮件集线器或你的 ISP 路由，你还需要一个 `smtp` 路由文件。它应包含一行

```
:mailhub.myISP.net
```

这将导致所有非本地邮件通过指定的邮件集线器中继。对于更复杂的路由，你可以在控制文件中放入多行。这可能很有用，特别是对于邮件集线器，如果你有某些域名希望通过专用网络路由。

你可以在 `qmail` 网站 `http://www.qmail.org` 上获取大量补充工具和文档。

## Exim

`Exim`是我将要考虑的最后一个 MTA，也是最现代的 MTA，它是基于对 MTA 应做什么的清晰认识而设计的。相比之下，`sendmail` 的原始作者在很大程度上是在摸索前进。

`Exim` 受 `smail` 启发，风格非常相似，但仅处理 SMTP。它简化了 `smail` 的许多概念，并具有良好的清晰文档，可能是我见过的任何 MTA 中最好的。同时，`exim` 在没有 `sendmail` 复杂性的情况下提供了 `sendmail` 的许多虚拟域和中继功能。

`Exim` 还提供了其他 MTA 中没有的一些队列控制。

队列中的邮件可以在操作员控制下被“冻结”和“解冻”。

本地邮件可以立即投递，而远程邮件可以批量处理以便稍后传输。

有一个队列监控实用程序，以便操作员可以了解情况如何。

与 `smail` 一样，`exim` 使用传输、主管和路由器的概念。它还实现了许多 `sendmail` 命令行选项，因此在大多数用途上它是一个即插即用的替代品。

### Exim 配置

`Exim` 在工作站上基本可以直接使用。你可能想要调整一些次要配置参数。只有一个配置文件位于 `/usr/exim/configure`。它有几个部分，并且在安装时注释很多，因此编辑起来应该没有问题。

在 `local_delivery:` 驱动程序中，你可能想将

```
file = /var/mail/${local_part}
```

改为

```
file = /var/spool/mail/${local_part}
```

取决于你的 MUA 期望用户邮箱位于何处。

### Exim 工作站

要将所有邮件通过你的邮件集线器或 ISP 路由，请使用 `smart_route` 路由器：

```
smart_route:
 driver = domainlist
 transport = remote_smtp
 route_list = "* mailhub.myISP.com bydns_a"
```

这应位于默认配置中 `lookuphost:` 路由器之前。

### 邮件集线器

`Exim` 默认关闭所有中继。你需要为自己的域内的主机启用它。为此设置

```
local_domains = mydomain.com:foobar.com
 relay_domains = *.mydomain.com:*.foobar.com
```

`local_domains` 变量将把这些域视为本地；即不涉及中继。`relay_domains` 将导致接受发往这些子域的邮件。

从自己的工作站发出的中继通过以下方式启用

```
host_accept_relay = localhost:*.mydomain.com
```

### 反垃圾邮件保护

`Exim` 为传入消息提供用户和系统过滤器。用户过滤器位于 `~/.forward`。一个过滤器 `.forward` 与普通 `.forward` 的区别在于其第一行为

```
# Exim filter
```

大小写和空白不重要。

最简单的垃圾邮件过滤器类型是

```
if $(reply_address) contains "@spamsite.com" and
  $(reply_address) does not contain "postmaster@"
then
  seen finish
endif
```

这将简单地丢弃该邮件。

使用形式为 `$header_headername` 的名称——例如 `$header_bcc` 或 `$header_reply_to`。

你可以采取的其他操作包括将邮件转发到其他位置、写入日志文件、将邮件保存到文件等等。文档 `./exim.*/doc/filter.txt` 中的说明非常清晰全面。

使用系统过滤器可以在邮件进入系统时立即应用规则。要启用它，请添加以下内容：

```
central_filter:
  driver = forwardfile
  file = /usr/exim/filters/${local_part}
  no_check_local_user
  no_verify
  filter
  allow_system_actions
```

设置 `allow_system_actions` 允许在过滤器文件中使用 `freeze` 和 `fail`。这些命令在用户过滤器中完全不可用。

文件规范中使用 `$local_part` 允许系统管理员为每个本地用户设置单独的过滤器集。当然，你也可以通过将文件规范设为固定字符串来为所有人设置一个全局过滤器集。

## 邮件处理的辅助程序

本章的其余部分介绍了一些辅助程序。`Fetchmail` 是一个支持程序，有助于通过拨号链路收集邮件。相比之下，`Majordomo` 提供了全新的功能，使用电子邮件作为传输媒介的讨论组。

### Fetchmail

`Fetchmail` 更像是一个半 MTA 而不是完整的 MTA。正如其名称所示，它从服务器读取邮件，但不写入邮件。这可能看起来很奇怪，但有时这样的程序是必要的。

如果你拥有完整的 Internet 连接，你不需要 `fetchmail`。在这种情况下，你在 `25` 端口上的正常邮件监听器就能满足你的所有需求。如果你 ISP 通过 SMTP 发送邮件并识别新连接以启动邮件，你也不需要 `fetchmail`

以下。你如果你的 MUA 支持 POP，则也不需要 `fetchmail`，尽管在这种情况下你可能仍想运行 `fetchmail` 以利用其多用户分发功能。

你需要 `fetchmail` 如果你的 ISP 仅通过 POP 或 IMAP 发送邮件，或不自动检测新连接以启动 SMTP 发送。我所知的所有情况下，从工作站到 ISP 的外发邮件都通过 SMTP 进行。

`Fetchmail` 从指定的服务器读取邮件并将其转发到其他目的地。它本身并不真正投递邮件。在正常使用中，你会要求 `fetchmail` 将邮件转发到本地机器上的 `25` 端口，或运行 `procmail` 来执行实际的投递到用户邮箱。

`Fetchmail` 可以由单个用户运行，也可以作为守护进程运行。

为了完成工作，`Fetchmail` 需要提供几条信息：

- 要轮询哪些服务器

- 何时轮询它们

- 使用哪种协议

- 要使用的用户 ID 和密码，或其他身份验证方式

- 它读取的邮件应丢弃到何处

- 是否从服务器删除邮件

## 运行 Fetchmail

最简单的方法是以 root 守护进程的方式运行 `fetchmail`，从 `/etc/rc.d` 启动。为此你必须满足两个要求：

- 你的 ISP 或邮件中继可以经由 SMTP 向你发送邮件。

- 你在 `25` 端口运行着 SMTP 监听器。

要启动 `fetchmail`，在 `/etc/rc.d/` 的适当位置添加以下内容：

```
/usr/bin/fetchmail -d 3600 -f /etc/fetchmailrc
```

这将以守护进程方式运行 `fetchmail`，轮询间隔为一小时，并从 `/etc/fetchmailrc` 读取其命令。你仍需告诉程序该做什么。

通常，你只会轮询一个邮件服务器，但规范可以重复任意多次。

示例配置将以

```
poll mail.myISP.com protocol ETRN
```

开头

这将从服务器下载所有人的邮件到此工作站。

如果另一方面你只能使用 POP 或 IMAP 进行邮件下载，以 root 守护进程运行是不安全的。由于邮件列表邮件的处理方式，存在邮件永远无法投递的危险。因此，每个用户必须运行自己的 `fetchmail` 守护进程。在这种情况下，配置存储在每个用户的 `~/.fetchmailrc` 中：

```
poll mail.myISP.net protocol POP3 username myname password mypassword
```

这告诉 `fetchmail` 要登录哪个邮件服务器，使用哪种协议，以及在服务器上使用什么用户 ID 和密码。这些用户 ID 和密码与本地机器上的完全没有任何关联。
