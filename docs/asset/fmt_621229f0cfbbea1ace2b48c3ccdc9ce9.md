
例如，如果用户的邮箱地址是 `jan@example.net`，而 `Jan` 告诉你 `Fred` (`fred.smith@gmail.com`) 在今天早上 8:00 左右给她发了邮件，但她还没有收到，这些信息就足够你着手了。你要的第一件事是打开当前的 `/var/log/mail.log`，并使用像 `less` 这样的程序，跳到大约 8:00 左右的日志。你在这里并不一定是在寻找 `Jan` 的邮件，只是进行一次完整性检查，看看那个时间段内是否有其他邮件投递。事实是，即使邮件系统在那个时间宕机，邮件也会在次级邮件服务器中队列，或者一旦邮件服务器恢复在线，邮件应该在不久之后被投递。

## 接收邮件的问题

在你确认邮件服务器在那个时间点运行正常后，接下来你应该尝试将今天邮件日志中 `Jan` 的所有入站邮件过滤到一个不同的文件中，以便更容易地查阅：

```
$ grep 'to=@example.net' /var/log/mail.log > /tmp/jans_incoming_emails
```

如果 `Jan` 告诉你是几天前发送的邮件而不是今天，你需要将 `/var/log/mail.log` 替换为包含该日期条目的存档邮件日志。无论哪种情况，你都可以用文本编辑器打开 `/tmp/jans_incoming_emails`，首先查看 `Jan` 是否收到了任何其他消息，其次查看她在早上 8:00 左右收到了什么种的消息。如果你想更专业一点，可以运行另一个 `grep` 来过滤出时间范围内的消息，但为了安全起见，至少查看早上 8:00 前后各一小时的消息。在查阅此文件的过程中，如果你发现任何符合该时段的消息，你需要提取完整的邮件事务记录。例如，你感兴趣的日志条目可能看起来像：

```
Apr 19 08:05:06 incoming postfix/local[13089]: to=62337254a2=jan@example.net,
- relay=local, delay=4.7, delays=0.4/0.3/0/4.3, dsn=2.0.0, status=sent (delivered to
- command=/usr/bin/postfix -t)
```

你可以从那行代码中提取邮件 ID `62337254a2`，然后回到主日志 (`/var/log/mail.log`) 并 `grep` 整个事务：

```
$ grep 62337254a2 /var/log/mail.log
Apr 19 08:05:02 incoming postfix/smtpd[13058]: 62337254a2: client=unknown[23.19.244.191]
Apr 19 08:05:02 incoming postfix/cleanup[13081]: 62337254a2: message-id=<Z3j1ZwSmhI23ZIIZjw
- SmhKububen0882queuequickclickdeals.info
Apr 19 08:05:02 incoming postfix/qmgr[10784]: 62337254a2: from=contest@quickclickdeals.
- info, size=11382, rcpt=(queue)
Apr 19 08:05:06 incoming postfix/local[13089]: 62337254a2: to=jan@example.net,
- relay=local, delay=4.7, delays=0.4/0.3/0/4.3, dsn=2.0.0, status=sent (delivered to
- command=/usr/bin/postfix -t)
Apr 19 08:05:06 incoming postfix/qmgr[10784]: 62337254a2: removed
```

在这种情况下，这是错误的邮件（很可能是垃圾邮件），因为 `FROM` 头部并不是来自 `fred.smith@gmail.com`。

在查看邮件时的另一种方法是，由于 `FROM` 头部不是来自 `fred.smith@gmail.com`，如果你在查看 `Jan` 的邮件时发现它不是来自那里，你可以过滤出所有入站邮件：

```
$ grep 'from=fred.smith@gmail.com' /var/log/mail.log > /tmp/fred_incoming_emails
```

在你确认邮件服务器在那个时间点运行正常后，接下来你应该尝试将今天邮件日志中 `Jan` 的所有入站邮件过滤到一个不同的文件中，以便更容易地查阅：

```
$ grep 'to=@example.net' /var/log/mail.log > /tmp/jans_incoming_emails
```

如果 `Jan` 告诉你是几天前发送的邮件而不是今天，你需要将 `/var/log/mail.log` 替换为包含该日期条目的存档邮件日志。无论哪种情况，你都可以用文本编辑器打开 `/tmp/jans_incoming_emails`，首先查看 `Jan` 是否收到了任何其他消息，其次查看她在早上 8:00 左右收到了什么种的消息。如果你想更专业一点，可以运行另一个 `grep` 来过滤出时间范围内的消息，但为了安全起见，至少查看早上 8:00 前后各一小时的消息。在查阅此文件的过程中，如果你发现任何符合该时段的消息，你需要提取完整的邮件事务记录。例如，你感兴趣的日志条目可能看起来像：

```
Apr 19 08:05:06 incoming postfix/local[13089]: to=62337254a2=jan@example.net,
- relay=local, delay=4.7, delays=0.4/0.3/0/4.3, dsn=2.0.0, status=sent (delivered to
- command=/usr/bin/postfix -t)
```

你可以从那行代码中提取邮件 ID `62337254a2`，然后回到主日志 (`/var/log/mail.log`) 并 `grep` 整个事务：

```
$ grep 62337254a2 /var/log/mail.log
Apr 19 08:05:02 incoming postfix/smtpd[13058]: 62337254a2: client=unknown[23.19.244.191]
Apr 19 08:05:02 incoming postfix/cleanup[13081]: 62337254a2: message-id=<Z3j1ZwSmhI23ZIIZjw
- SmhKububen0882queuequickclickdeals.info
Apr 19 08:05:02 incoming postfix/qmgr[10784]: 62337254a2: from=contest@quickclickdeals.
- info, size=11382, rcpt=(queue)
Apr 19 08:05:06 incoming postfix/local[13089]: 62337254a2: to=jan@example.net,
- relay=local, delay=4.7, delays=0.4/0.3/0/4.3, dsn=2.0.0, status=sent (delivered to
- command=/usr/bin/postfix -t)
Apr 19 08:05:06 incoming postfix/qmgr[10784]: 62337254a2: removed
```

在这种情况下，这是错误的邮件（很可能是垃圾邮件），因为 `FROM` 头部并不是来自 `fred.smith@gmail.com`。

在查看邮件时的另一种方法是，由于 `FROM` 头部并不是来自 `fred.smith@gmail.com`，如果你在查看 `Jan` 的邮件时发现它不是来自那里，你可以过滤出所有入站邮件：

```
$ grep 'from=fred.smith@gmail.com' /var/log/mail.log > /tmp/fred_incoming_emails
```

# 第 8 章：网站宕机了吗？追踪 Web 服务器问题

## 服务器正在运行吗？

Web 服务器最先要排查的问题之一是 Web 服务器完全无法访问。这是一组非常常见的排查步骤，因此在第 5 章中已经将其用作诊断网络问题的主要示例。毕竟，当你无法访问 Web 服务器时，想要回答的首要问题之一就是问题出在你的本地端还是远程端。对于一套完整的排查步骤，我强烈建议你先过过一遍第 5 章；但是，本章假设问题不在网络上，因此它会重复第 5 章中某些针对 Web 服务器的排查步骤。在示例中，服务器名称为 `web1`，IP 地址为 `10.1.2.5`，因此请确保修改你的更改以匹配你 Web 服务器的主机名和 IP。

## 远程端口开放了吗？

现在你路由到了该机器，但无法访问端口 `80` 的 Web 服务器。下一次测试是查看端口是否开放。有许多不同的方法可以实现这一点。例如，你可以尝试 `telnet`：

```
$ telnet 10.1.2.5 80
Trying 10.1.2.5...
telnet: Unable to connect to remote host: Connection refused
```

如果你看到 `Connection refused`（拒绝连接），要么是端口关闭（可能是 `Apache` 没有在远程主机上运行，或者没有在该端口上监听），要么是防火墙阻止了你的访问。如果 `telnet` 可以连接，那么，嗯，你根本没有网络问题。如果 Web 服务已启动但工作方式不符合你的预期，你需要调查 Web 服务器上的 `Apache` 配置。

与 `telnet` 相比，我更倾向于使用 `nmap` 来测试端口，因为它通常可以检测到防火墙。如果没有安装 `nmap`，请使用你的包管理器安装 `nmap` 软件包。要测试 `web1`，你需要输入以下内容：

```
$ nmap -p 80 10.1.2.5
Starting Nmap 4.62 ( http://nmap.org ) at 2009-02-05 18:49 PST
```

`web1` (`10.1.2.5`) 上有趣的端口：

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 80/tcp | filtered | |

啊！`nmap` 足够智能，它通常能区分真正关闭的端口和位于防火墙后的关闭端口。通常情况下，当一个端口实际上已关闭时，`nmap` 会报告其为 `closed`（关闭）。但在这里它报告为 `filtered`（过滤）。这告诉我们，某个防火墙在中间丢弃了到达地板的数据包。这意味着你需要调查网关 (`10.1.1.1`) 和 `web1` 自身的任何防火墙规则，以查看端口 `80` 是否被拦截。

## 在本地测试远程主机

到此时，我们要么已经将问题缩小到网络问题，要么我们认为问题出在主机本身。如果我们认为问题出在主机本身，我们可以进行几项操作来测试端口 `80` 是否可用。

### 测试监听端口

一旦你确定问题不在你的网络上，你就应该登录 Web 服务器并测试端口 `80` 是否正在监听。`netstat -inp` 命令将列出所有正在监听的端口以及打开该端口的进程。你可以直接运行它并解析输出内容，查找任何在端口 `80` 上监听的内容，或者你可以使用 `grep` 只查看在端口 `80` 上监听的项：

```
$ netstat -inp | grep :80
ctcp 0 0 0.0.0.0:80 0.0.0.0:* LISTEN 919/apache
```

第一列告诉你是端口所使用的协议。第二列和第三列是接收和发送队列（都被设置为 0）。你需要关注的列是第四列，因为它列出了主机监听的本地地址。`0.0.0.0:80` 告诉我们主机正在其所有的 IP 地址上监听端口 `80` 的流量。如果 `Apache` 仅在服务器的以太网地址上监听，你将在这里看到一个像 `10.1.2.5:80` 的特定 IP。

## 服务器正在运行吗？

最后一列告诉你是哪个进程打开了该端口。在这里你可以看到 `Apache` 正在运行并监听。如果你在 `netstat` 输出中没有看到这些，那么你需要启动你的 `Apache` 服务器。

如果进程正在运行并监听端口 `80`，那么可能是服务器设置了某种防火墙。使用 `iptables` 命令列出你所有的防火墙规则。如果你的防火墙已禁用，你的输出看起来像这样：

```
$ sudo /sbin/iptables -L
Chain INPUT (policy ACCEPT)
  target      prot opt destination
Chain FORWARD (policy ACCEPT)
  target      prot opt destination
Chain OUTPUT (policy ACCEPT)
  target      prot opt destination
```

注意，在此输出中，默认策略被设置为 `ACCEPT`（接受）。但是，你的防火墙可能设置为默认丢弃所有包，即使它没有列出任何规则。如果是这种情况，你将看到类似下面的输出：

```
$ sudo /sbin/iptables -L
Chain INPUT (policy DROP)
  target      prot opt destination
Chain FORWARD (policy DROP)
  target      prot opt destination
Chain OUTPUT (policy DROP)
  target      prot opt destination
```

另一方面，如果你的防火墙规则拦截了端口 `80`，输出可能更像这样：

```
$ sudo /sbin/iptables -L
Chain INPUT (policy ACCEPT)
```

| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| REJECT | tcp | -- | 0.0.0.0/0 |
| REJECT | icmp | unreachable | |

| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| DROP | tcp | -- | source |
| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| DROP | tcp | -- | destination |
| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| DROP | tcp | -- | source |
| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| DROP | tcp | -- | destination |
| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| 80 | tcp | -- | |
| 目标 | 协议 | 选项 | 目的 |
| :--- | :--- | :--- | :--- |
| 80 | tcp | -- | traffic

显然，在后一种的情况下，你需要修改防火墙规则来允许 `80` 流量。

## 从命令行测试 Web 服务器

一旦你确认 Web 服务器在正确的端口上监听，下一步排查步骤是确认 Web 服务器是否有响应。虽然你可以使用浏览器来测试，但如果你知道如何使用 `curl` 或 `telnet` 这样的命令行工具来测试 Web 服务器。

### 使用 Curl 测试 Web 服务器

`Curl` 是一个相对简单的工具，它可以处理 `HTTP` 和 `HTTPS` 等。如果你查看它的帮助页（输入 `man curl`），你会发现它支持各种选项。事实上，`Curl` 相比 `telnet` 的优势在于它可以为你处理 `HTTP` 协议。

## 从命令行测试 Web 服务器

由于我们只是想测试 Web 服务器的功能，我们不需要使用 `curl` 的任何高级选项。事实上，从命令行测试 Web 服务器只需输入 `curl` 然后是想要加载的 URL：

```
$ curl http://www.example.net
<html><body><h1>Welcome to Example.net!</h1><p>This is an example page for Example.Net.</p><p>If you're interested in <a href="mailto:click.here">click here</a>.</p></body></html>
```

在这个示例中，你可以看到由 `Apache` Web 服务器创建的默认网页。如果由于某些原因 Web 服务器无法访问，你会看到类似这样的：

```
$ curl http://www.example.net
curl: (7) couldn't connect to host
```

默认情况下，`curl` 只输出你请求的网页内容，但通常当你排查 Web 服务器时，你需要获取额外数据，例如 `HTTP` 状态码（稍后介绍）、请求所需的时间、传输了多少数据等。`Curl` 提供了一个 `-w` 选项，允许你提取请求的附加数据并显示在屏幕上。例如，如果你想查看请求的 `HTTP` 状态码，你可以输入：

```
$ curl -w "%{http_code}" http://www.example.net
<html><body><h1>Welcome to Example.net!</h1><p>This is an example page for Example.Net.</p><p>If you're interested in <a href="mailto:click.here">click here</a>.</p></body></html>
200
```

额外信息会出现在请求的最后。在这种情况下，`HTTP` 状态码是 `200`，这是我们想要的。`curl` 的帮助页列出了 `-w` 参数的许多额外选项，你可以在输出中将它们组合在一起。

# 第8章 - 网站宕机了吗？追踪 Web 服务器问题

使用该命令可以获取状态码、请求耗时、下载数据大小以及内容类型：
