
在提供 FTP 访问时，管理系统资源（网络带宽或内存）可能重要的其他设置还包括：

- `dirlist_enable`—切换开启或关闭目录列表。
- `dirmessage_enable`—切换用户进入目录时显示消息。一个相关的设置是 `is_recurse_enable`，你可以用它来禁止递归目录列表。
- `download_enable`—切换开启或关闭下载。
- `max_clients`—设置最大连接数限制。
- `max_per_ip`—设置来自同一 IP 地址的连接数限制。

## 使用 ftphosts 文件允许或拒绝 FTP 服务器连接

你可以在 `/etc/ftphosts` 中创建一个文件，以允许或拒绝特定用户或地址连接 FTP 服务器。该文件的格式为单词 `allow` 或 `deny`，可选跟随一个用户名，然后跟一个 IP 或 DNS 地址：

```
allow username address
deny username address
```

列表 26.2 显示了此文件的示例配置。

```
LISTING 26.2 用于允许或拒绝用户的 ftphosts 配置文件

# 示例主机访问文件
#
# '#' 之后的所有内容都被视为注释
# 空行会被忽略
allow user1
deny 192.168.1.100
allow user2 example.com
```

# 第 27 章 处理电子邮件

以下是一个关于电子邮件如何成功处理并发送到目的地的简化示例：

- `matthew@semourcray.net` 编写并发送了一封邮件消息给 `heather@gracehopper.net`。
- `semourcray.net` 上的 MTA 接收了 Matthew 的邮件消息，并将其队列，以便在其他等待发送的邮件之前投递。
- `semourcray.net` 上的 MTA 通过端口 24 连接 `gracehopper.net` 上的 MTA。在 `gracehopper.net` 确认连接后，`semourcray.net` 上的 MTA 发送邮件消息。在 `gracehopper.net` 接受并确认接收消息后，连接关闭。
- `gracehopper.net` 上的 MTA 将邮件消息放入 Heather 的收件箱中；当 Heather 登录时，她会收到新邮件的通知。

然而，在这个过程中可能会出现许多问题。以下是几个例子：

- 如果 `gracehopper.net` 上不存在 Heather 怎么办？在这种情况下，`gracehopper.net` 上的 MTA 会拒绝发送者，并通知 `semourcray.net` 上的 MTA 问题所在。`semourcray.net` 上的 MTA 生成一封邮件消息并发送给 `matthew@semourcray.net`，告知他 `gracehopper.net` 上不存在 Heather（或者根据邮件服务器的配置，默默地丢弃消息而不向发送者提供任何问题指示）。
- 如果 `gracehopper.net` 不响应 `semourcray.net` 的连接尝试怎么办？（也许服务器正在进行维护而关机了）。`semourcray.net` 上的 MTA 会通知发送者初始投递尝试失败。系统将根据服务器管理员决定的间隔进行进一步尝试，直到达到截止日期，并通知发送者该消息无法投递。

## 邮件传输代理 (Mail Transport Agent)

Ubuntu 提供了多种 MTA 可供选择，每种都有其优缺点。通常，它们隐藏在 Ubuntu 的底层，在世界各地的服务器之间静默移动，几乎或完全不需要维护。某些 MTA 极其强大，每天能够处理数百封邮件，而另一些则是为较小规模的安装环境设计的。其他 MTA 可能没有那么强大，但功能非常完备。在下一节中，我们将查看 Ubuntu 上可用的一些较流行的 MTA。

### Sendmail

`Sendmail` 处理了当今互联网传输的绝大多数电子邮件。它在 Linux/UNIX/BSD 世界中非常流行，并得到了良好的支持。它还有一个商业版本，带有 GUI 界面，易于配置。

#### 电子邮件是如何发送和接收的

`Sendmail` 不仅流行，与某些其他 MTA 相比，它还特别强大。然而，它并非没有缺点，你会发现在较大的环境中，其他 MTA 每秒可以处理更多的邮件。`Sendmail` 的另一个问题是，要完全精确地按照你的意图进行配置可能会非常复杂。虽然有几本书专门针对 `Sendmail` 编写，但最流行的一本超过了一千页，这反映了 `Sendmail` 配置的复杂性。

然而，我们应该感谢，`Sendmail` 的默认配置对于大多数基础安装来说都是开箱即用的，使得进一步配置变得没有必要。即使你想将其作为基础电子邮件服务器使用，也只需要进行微小的调整。与 `Sendmail` 相关的复杂性通常会导致系统管理员将其替换为其他更容易配置的替代方案之一。

### Postfix

`Postfix` 起源于 IBM Secure Mailer，但发布到社区时具有许多速度上的优势。与 `Sendmail` 相比，它更容易管理，并且拥有更多优势。`Postfix` 为 `Sendmail` 提供了一个无痛的替代方案，你完全可以在不让系统崩溃的情况下将 `Sendmail` 替换为 `Postfix`。事实上，依赖 `Sendmail` 的应用程序会自动使用 `Postfix` 并继续正常工作（因为 `Postfix` 使用了 `Sendmail` 包装器，欺骗其他程序使其认为 `Postfix` 就是 `Sendmail`）。这种包装器（或者更准确地说是）使得如果你已经在运行 `Sendmail`，切换到 `Postfix` 将变得极其简单。`Postfix` 恰好也是 Ubuntu 的首选 MTA，因此我们在本章后部分将花更多时间研究它。

为了增强安全性，许多 `Postfix` 进程使用 `chroot` set（限制仅访问文件系统的特定部分）来提高安全性，并且 `Postfix` 中没有 `setuid` 组件。在 Ubuntu 中，`chroot` 配置不再被使用，事实上，`Postfix` 的作者也建议不要使用。你可以手动将 `Postfix` 配置为 `chroot` 配置，但 Ubuntu 不再支持这一点。

如果你是从零开始，`Postfix` 被认为是比 `Sendmail` 更好的选择。

### Qmail 和 Exim

`Qmail` 是 `Postfix` 的直接竞争对手，但 Ubuntu 并没有提供。`Qmail` 设计得比 `Sendmail` 更容易使用，同时也更快、更安全。然而，`Qmail` 并不是 `Sendmail` 的无缝替换，因此将现有的 `Sendmail` 安装迁移到 `Qmail` 并不像从 `Sendmail` 迁移到 `Postfix` 那样简单。`Qmail` 相对容易管理，并与许多软件插件集成，包括网页邮件系统和 POP3 服务器。可以通过 `www.qmail.org/` 获取 `Qmail`。

`Exim` 是另一个 MTA，可以在 `www.exim.org/` 获取。`Exim` 被认为比 `Sendmail` 或 `Postfix` 更快、更安全，但配置起来与两者都大不同。`Exim` 和 `Qmail` 使用 `maildir` 格式而不是 `mbox`，因此两者都被认为是 NFS 安全的（见下侧边栏）。

![](img/2a083394994f21b0)

#### MDIR 对比 MAILBOX（邮箱箱）

`mbox` 格式将所有邮件保存在单个文件中。虽然这很简单，但有一个巨大的缺点：如果你在网络上访问收件箱，可能会出现某种损坏。从这种问题可能会变得困难。如果在 NFS 上访问文件，`mailbox` 特别容易出现问题。

`Maildir` 引入了三个子目录：`cur`、`new` 和 `tmp`。每封邮件都保存在独立的唯一文件中。取决于你访问邮件的方式，`maildir` 允许多个应用程序同时访问邮件；而 `mbox` 不行。

邮件代理（MUA）或邮件客户端的选择也会影响你对目录格式的选择。例如，`pine` 程序不缓存任何信息，每次访问时必须重新读取目录。如果你使用 `pine`，`maildir` 是一个糟糕的选择。高级邮件客户端会执行缓存，因此 `maildir` 可能是一个不错的选择，尽管客户端缓存可能会不同步。

似乎不存在完美的选择。Ubuntu 提供了邮件替代方案，它们各有优劣。注意这些替代方案之间的差异，并重新评估你的选择，以确保它是最适合现状的。

## 选择 MTA

Ubuntu 上还有其他 MTA 可用，但本节讨论的是最流行的。你应该选择哪一个？这取决于你的需求。`Postfix` 的主要优势是它可以扩展并以高速度处理大量邮件，而且它比复杂的 `Sendmail` 容易配置得多。然而，你可能会发现某些特定需求只有 `Sendmail` 能提供。当你需要时，在 MTA 之间切换是很容易的。

## 投递代理 (Mail Delivery Agent)

`SMTP` 是一种服务器之间的协议，旨在向连接到系统的系统的递。拨号系统仅在用户命令时连接；它们为了特定操作而连接，并且经常断开。为了适应这种差异，许多邮件系统还包含一个邮件投递代理（MDA）。MDA 将邮件传输到没有永久互联网连接的系统。MDA 类似于

## 电子邮件是如何发送和接收的

一个 MTA（参见下文），但它不处理系统之间的投递，也不为用户提供界面。

### 注意
