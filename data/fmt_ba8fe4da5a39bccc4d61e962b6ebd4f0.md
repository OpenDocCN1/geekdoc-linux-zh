
```
Mon Sep 3 07:13:05 2001 1 localhost.localdomain 100
/var/ftp/pub/b o a testing@test.com ftp 0 * c
Mon Sep 3 02:35:05 2001 11 helios /var/ftp/pub/configuration a
_ o a testing@test.com ftp 0 * c
Mon Sep 3 02:35:05 2001 11 helios /var/ftp/pub/configuration a
_ o a testing@test.com ftp 0 * c
```

以下是电子邮件如何成功处理并发送到目的地的简化示例：

- 1. `andrew@hudson.org`撰写并发送了一封邮件给`paul@hudzilla.org`。
- 2. `hudson.org`上的 MTA 接收了 andrew 的邮件，并将其放入发送队列，排在其他正在等待发送的邮件之后。
- 3. `hudson.org`上的 MTA 通过端口`25`访问`hudzilla.org`上的 MTA。在`hudzilla.org`确认连接后，`hudson.org`上的 MTA 发送了邮件信息。在`hudzilla.org`接受并确认收到邮件后，连接关闭。
- 4. `hudzilla.org`上的 MTA 将邮件放入 paul 的收件箱；如果 paul 在登录时有新邮件，系统将通知他。

当然，在此过程中可能会出现一些问题。以下是几个例子：

如果`hudzilla.org`上并不存在 paul 这个用户，这会怎样？在这种情况下，`hudzilla.org`上的 MTA 会拒绝该邮件并通知`hudson.org`上的 MTA 问题所在。`hudson.org`上的 MTA 会生成一封邮件发送给`andrew@hudson.org`，告知他`hudzilla.org`上不存在 paul（或者可能取决于服务器配置，直接丢弃邮件且不向发送者提供任何问题指示）。

如果`hudson.org`不响应`hudson.org`的连接请求，会怎样？（也许服务器正在维护而关机）。`hudson.org`上的 MTA 会通知发送者初始投递尝试失败。将根据服务器管理员决定的间隔进行后续尝试，直到达到期限，并通知发送者邮件无法投递。

# 邮件传输代理 (Mail Transport Agent)

Fedora 提供了多种 MTA 可供，每种都有其优缺点。通常情况下，它们隐藏在 Fedora 的底层，在世界各地的服务器之间静默运行，几乎或完全不需要维护。某些 MTA 极其强大，每天能够处理数十万封邮件，而另一些则是为规模较小的安装环境而设计的。其他 MTA 也许没有那么强大，但功能非常完备。在下一节中，我们将查看 Fedora 上可用的一些较流行的 MTA。

## Sendmail

今天通过互联网传输的绝大多数邮件都由 Sendmail 处理，而它恰好是 Fedora 的默认 MTA。它在 Linux/UNIX/BSD 世界中非常流行，并得到了良好的支持。它还有一个商业版本，为每个配置项都提供了图形界面（GUI）。

除了流行之外，Sendmail 与其他某些 MTA 相比也特别强大。然而，它并非没有缺点，在大型环境中，其他 MTA 每秒可以处理更多的邮件。Sendmail 的问题在于，要完全按照你想要的方式设置可能极其复杂。幸运的是，有几千页的文档反映了 Sendmail 配置的复杂性；其中最流行的一份就有一千多页。

Sendmail 的默认配置对于大多数基础安装来说开箱即用，运行良好，无需进一步配置。即使你想将其作为基础邮件服务器使用，也必须进行一些微调。与 Sendmail 相关的复杂度往往导致系统管理员将其替换为其他更容易配置的替代方案之一。我们将在在本章稍后的“基础 Sendmail 配置与操作”章节中查看基础 Sendmail 配置。

## Postfix

Postfix 起源于 IBM Secure Mail，但由 IBM 向社区发布。与 Sendmail 相比，它更容易管理，并且在速度上具有许多优势。Postfix 为 Sendmail 提供了一个无痛的替代方案，你可以在不影响系统的情况下将 Sendmail 替换为 Postfix。事实上，依赖 Sendmail 的应用程序将自动改用 Postfix 并继续正常工作。这是由于 Postfix 使用了 Sendmail 封装器（wrapper），它欺骗其他程序认为 Postfix 就是 Sendmail。这个封装接口使得切换到 Postfix 变得极其简单。

> 注意
>
> Fedora 提供了 2.2 `Postfix`，其配置与早期版本略有不同。如果你是从早版本的 Fedora 或 Red Hat 版本升级 Postfix，请检查你的配置文件。

Fedora 还针对版本 2 的 Cyrus SASL 库（一种身份验证库）编译了 Postfix 和 Sendmail。发布说明（Release Notes）包含了如果你使用这些库时会影响你的文件位置和选项更改的详细信息。

为了增强安全性，许多 Postfix 进程使用 `chroot` 来提高安全性，且 Postfix 中没有固定的组件。在 Fedora 目前的发行版中，`chroot` 配置不再被使用，且 Postfix 作者也不建议使用它。你可以手动重新配置 Postfix 为 `chroot` 配置，但 Fedora 不再支持这种操作。

如果你是从零开始，Postfix 被认为是比 Sendmail 更好的选择。

## Qmail 和 Exim

Qmail 是 Postfix 的直接竞争对手，但 Fedora 并不提供它。Postfix 设计得比 Sendmail 更易使用，因为它更快、更安全。然而，Qmail 不是 Sendmail 的直接替代品，因此将现有的 Sendmail 安装迁移到 Qmail 并不像 Sendmail 迁移到 Postfix 那么简单。Qmail 相对容易管理，并与许多软件插件集成，包括网页邮箱系统和 POP3 服务器。可以通过 `http://www.qmail.org` 获取 Qmail。

![](img/c4a0ea5ab3561ff33a8da88)

## MDIR 对比 MAILBOX

Qmail 还引入了 `maildir`，这是存储邮件的标准方法的替代方案。`maildir` 是一个更灵活的邮件处理系统，但它要求你的邮件客户端识别 `maildir` 格式。（现代程序都支持。）

传统的 `mbox` 格式将所有邮件保存在单个文件中，并维护每封邮件的索引。而使用 `maildir`，每封邮件都保存在一个独立的、唯一的文件。如果你为大量用户运行邮件服务器，你应该选择一个能够高效处理小文件的文件系统。

`mbox` 有一个主要的缺点。当你访问包含所有邮件的单体 `mbox` 文件时，假设文件或索引发生了某种类型的损坏。从该问题恢复可能非常困难。如果文件通过网络访问，文件可能会出现问题并导致损坏；你应该避免通过 `NFS`（网络文件系统）访问 `mbox`。

取决于你访问邮件的方式，`maildir` 允许多个应用程序同时访问 `maildir` 文件；而 `mbox` 则不允许。

用户代理（或客户端）的选择也会影响你对邮件目录格式的选择。例如，`pine` 程序不缓存任何目录信息，并且在每次访问邮件目录时都必须读取该目录。如果你正在使用 `pine`，`maildir` 将是一个糟糕的选择。更高级的客户端会执行缓存，因此 `maildir` 可能是一个很好的选择，尽管邮件客户端缓存可能会不同步。

似乎没有完美的选择。Fedora 为你提供了具有优缺点的邮件替代方案。请注意这些替代方案之间的差异，并频繁重新评估你的选择，以确保它是最适合你情况的。

## 选择 MTA

Fedora 提供了其他 MTA 可供使用，但本节讨论的那些是最流行的。你应该选择哪一个？这取决于你需要做什么。Sendmail 的主要优势是它被认为是标准，并且它可以完成许多其他 MTA 无法完成的任务。然而，如果易用性速度对你是一个考虑因素，你可能考虑将 Sendmail 替换为 Postfix、Exim 或 Qmail。由于 Sendmail 是 Fedora 包含的默认 MTA，它将在后续章节中有更详细的介绍。

## 邮件投递代理

`SMTP` 是一种服务器到服务器的协议，旨在将邮件递送到始终连接到 Internet 的系统。拨号系统仅在用户命令下进行连接；它们为了特定操作而连接，并经常断开。为了适应这种差异，许多邮件系统还包含一个邮件投递代理，简称 `MDA`。`MDA` 将邮件传输到没有永久 Internet 连接的系统。`MDA` 类似于 `MTA`（参见下文注释），但它不处理系统之间的投递，也不向用户提供接口。

> 注意
>
> `Procmail` 和 `Spamassassin` 是 `MTA` 的示例；它们都为 `MTA` 提供过滤服务，同时它们在本地存储消息，然后将它们提供给 `MUA` 或电子邮件客户端供用户阅读。
