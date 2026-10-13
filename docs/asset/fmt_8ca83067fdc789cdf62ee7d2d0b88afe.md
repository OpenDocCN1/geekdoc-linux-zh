
互联网上绝大多数的电子邮件流量都由一个名为 `Sendmail` 的 `MTA` 处理，这是 `Fedora`（以及许多其他 Unix 发行版）随附的默认 `MTA`。`Sendmail` 的优势在于它已在您的 `Fedora` 系统中安装并得到良好的支持。商业版本（不包括在 `Fedora` 中）还提供了 GUI 配置实用工具。

`Sendmail` 是现存最古老且功能最强大的 `MTA` 之一，但它也有一些缺点。它的速度有点慢；在高负载环境中，其他 `MTA`（包括 `Postfix` 和 `Qmail`）通常每秒可以处理更多的消息。`Sendmail` 也以错综复杂著称；配置文件极其晦涩难懂。（关于 `Sendmail` 的畅销书长度超过 1,000 页。）

幸运的是，`Fedora Core` 提供的 `Sendmail` 默认配置在大多数基本安装中工作良好，只需进行少量更改即可将其配置为基本电子邮件服务器的安装。然而，由于高级 `Sendmail` 配置的复杂性，许多管理员选择用另一种替代 `MTA`（邮件传输代理）来替换它。（本章稍后的“`Sendmail` 基本配置与操作”部分将介绍配置和使用 `Sendmail` 的基础知识）。

## Postfix

`Postfix`（最初于 1998 年以 `IBM Secure Mailer` 的名字发布）是一个流行的 `Sendmail` 替代品；它速度快、安全性高且易于管理。`Postfix` 是 `Sendmail` 的直接替换品（这意味着期望使用 `Sendmail` 的其他应用程序不会注意到 `Postfix` 已将其替换，并且会继续正确工作），将 `Sendmail` 安装迁移到 `Postfix` 相对简单。为了让所有这些神奇操作得以实现，`Postfix` 使用了一个 `Sendmail` 包装器（一种让其他程序误以为它是 `Sendmail` 的接口），以便 `MUA`（邮件用户代理）等可以像与 `Sendmail` 通信一样与其通信。

![](img/774d40fd20903495c5cd00e2efad3f33_696_0.png)

`Fedora` 提供 `Postfix` 版本 2，它使用的是与早期版本略有不同的配置。如果你正在从早期 Red Hat 版本的 `Postfix` 进行升级，请检查你的配置文件。

`Fedora` 现在还将 `Postfix` 和 `Sendmail` 编译为针对 `Cyrus SASL` 库版本 2（一种身份验证库）。发行说明中包含关于文件位置和功能变化的详细信息，如果你使用这些库，这些信息将对你产生影响。

为了增强安全性，许多 `Postfix` 进程过去使用 `chroot` 机制（该机制限制只能访问文件系统的特定部分）来提高安全性，并且 `Postfix` 中没有任何 `setuid` 组件。在当前版本的 `Fedora` 中，不再使用 `chroot` 配置，实际上 `Postfix` 作者也不建议这样做。你可以手动重新配置 `Postfix` 以使用 `chroot` 配置，但 `Fedora` 不再支持这一配置。

如果你是从头开始安装，`Postfix` 被认为比 `Sendmail` 是更好的选择。

## Qmail 和 Exim

`Qmail` 是 `Postfix` 的直接竞争对手，但未随 `Fedora` 提供。`Postfix` 被设计得比 `Sendmail` 更易用，同时更快且更安全。然而，`Qmail` 并不是 `Sendmail` 的直接替换品，因此将现有的 `Sendmail` 安装迁移到 `Qmail` 并不像从 `Sendmail` 迁移到 `Postfix` 那么简单。`Qmail` 管理相对容易，并且可以与多种软件插件集成，包括 Web 邮件系统和 `POP3` 服务器。`Qmail` 可从 `http://www.qmail.org/` 获取。

`Exim` 是另一种 `MTA`，可从 `http://www.exim.org/` 获取。`Exim` 被认为比 `Sendmail` 或 `Postfix` 更快且更安全，但其配置方式与两者差异较大。`Exim` 和 `Qmail` 使用 `maildir` 格式而非 `mbox`，因此两者都被认为是“`NFS` 安全”的（参见以下侧边栏）。

## MDIR 与 Mailbox

`Qmail` 还引入了 `maildir`，这是标准 Unix 存储 incoming 邮件方法的替代方案。`maildir` 是一种处理 incoming 电子邮件更灵活的系统，但它要求重新配置你的邮件客户端，并且与传统 Unix 存储 incoming 邮件的方式不兼容。你需要使用能够识别 `maildir` 格式的邮件程序。（现代程序都能做到。）

传统的 `mbox` 格式将分配给文件夹的所有邮件作为单个文件连接保存，并维护单个电子邮件的索引。在 `maildir` 中，每个邮件文件夹有三个子文件夹：`/cur`、`/new` 和 `/tmp`。每封电子邮件都保存在单独的、唯一的文件中。如果你正在为大量用户运行邮件服务器，你应该选择能够有效处理大量小文件的文件系统。

`mbox` 确实存在一个主要缺点。当你正在访问包含你所有电子邮件的单一 `mbox` 文件时，假设发生了某种损坏，无论是文件本身还是索引。从这个问题中恢复可能很困难。如果文件是通过网络访问的，`mbox` 文件特别容易出现问题，并可能导致文件损坏；应避免通过 `NFS`（网络文件系统）访问挂载的 `mbox` 邮件，因为可能会发生文件损坏。

取决于你如何访问邮件，`maildir` 允许多个应用程序同时访问 `maildir` 文件；而 `mbox` 不允许。

`MUA` 的选择也会影响你对邮件目录格式的选择。例如，`pine` 程序不缓存任何目录信息，每次访问时必须重新读取邮件目录。如果你正在使用 `pine`，`maildir` 将是一个糟糕的选择。更高级的 `MUA` 执行缓存，因此 `maildir` 可能是一个不错的选择，尽管 `MUA` 缓存可能会失去同步。似乎没有完美的选择。

`Fedora` 为你提供了具有优缺点的邮件替代方案。请了解这些替代方案之间的差异，并经常重新评估你的选择，以确保它最适合你的情况。

## 选择 MTA

还有其他 `MTA` 可用于 `Fedora Core`，但前几节讨论的是其中最流行的。你应该选择哪一个？这取决于你需要做什么。`Sendmail` 的主要优势在于它被视为标准，并且它可以完成许多其他 `MTA` 无法完成的任务。然而，如果易用性或速度是你关心的问题，你可能需要考虑用 `Postfix`、`Exim` 或 `Qmail` 替换 `Sendmail`。由于 `Sendmail` 是随 `Fedora Core` 一起提供的默认 `MTA`，将在下一节中更详细地介绍。

## 邮件投递代理

`SMTP` 是一种服务器到服务器的协议，旨在将邮件投递到始终连接到 Internet 的系统。拨号系统仅在用户命令下连接；它们针对特定操作进行连接，并且经常断开连接。为了适应这种差异，许多邮件系统还包含一个邮件投递代理，或 `MDA`。`MDA` 将邮件传输到没有永久 Internet 连接的系统。`MDA` 类似于 `MTA`（参见以下注意事项），但不处理系统之间的投递，也不提供用户界面。

> > **注意**
> >
> > `Procmail` 或 `Spamassassin` 是 `MTA` 的示例；它们都为 `MTA` 提供过滤服务，同时将消息存储在本地，然后将其提供给 `MUA` 或邮件客户端供用户阅读。

`MDA` 使用 `POP3` 或 `IMAP` 协议来完成此过程。类似于邮局的邮箱，`POP3` 和 `IMAP` 实现了“存储和转发”过程，如果你只是想阅读邮件，这就免除了维护本地邮件服务器的需要。例如，拨号 Internet 用户可以间歇性地连接到他们的 ISP 邮件服务器，使用 `Fedora` 提供的 `MDA` `Fetchmail` 检索邮件（参见本章稍后的“使用 `Fetchmail` 检索邮件”部分）。

### 邮件用户代理

邮件用户代理，或 `MUA`，是电子邮件系统的另一个必要部分。`MUA` 是邮件客户端或邮件阅读器，允许用户阅读和撰写电子邮件，并提供用户界面。（这是大多数用户熟悉的“电子邮件”应用程序本身。）一些流行的 Unix 命令行 `MUA` 有 `elm`、`pine` 和 `mutt`。`Fedora` 还提供现代 GUI `MUA`：`Evolution`、`Thunderbird`、`Mozilla Mail`、`Balsa`、`Sylpheed` 和 `KMail`。作为对比，常见的非 Unix `MUA` 有 `Microsoft Outlook`、`Outlook Express`、`Pegasus`、`Eudora` 或 `Netscape Messenger`。

`Microsoft Windows` 和 `Macintosh` 的 `MUA` 通常包含一些 `MTA` 功能；Unix 则没有。例如，`Microsoft Outlook` 可以连接到你的 Internet 服务提供商的邮件服务器来发送消息。另一方面，Unix `MUA` 通常依赖外部 `MTA`，如 `Sendmail`。这看起来可能是一种不必要的复杂方式，如果用于将单个用户连接到她的 ISP，确实如此。然而，对于其他任何情况，使用外部 `MTA` 可以提供更大的灵活性，因为你可以使用任意数量的外部程序来处理和处理你的电子邮件功能并自定义服务。由不同应用程序处理流程使你对如何在网络上为用户提供电子邮件服务以及对个人和 SOHO 用户具有非常大的控制力。

例如，你可以：

- 使用 `Evolution` 阅读和撰写邮件。
- 使用 `Sendmail` 发送你的邮件。
- 使用 `xbiff` 在你有新邮件时通知你。
- 使用 `Fetchmail` 从远程邮件服务器检索你的邮件。
