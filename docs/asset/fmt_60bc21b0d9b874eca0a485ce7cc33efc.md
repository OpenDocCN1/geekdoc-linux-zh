
```
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/wu-ftpd.2.6.1-18.i386.rpm a _ o a testing.test.com ftp 0 * c
```

## 相关的 FEDORA 和 LINUX 命令

你将使用这些命令在 Fedora Core 中安装、配置和管理 FTP 服务：

- `epiphany`—一个支持 FTP 的 GNOME 图形浏览器
- `ftp`—一个基于文本的交互式 FTP 命令
- `ftpcopy`—从 FTP 服务器复制目录和文件
- `ftpcp`—从远程 FTP 服务器检索数据，但不覆盖现有的本地文件
- `gftp`—一个用于 GNOME 的图形 FTP 客户端
- `konqueror`—KDE 的图形 Web 浏览器
- `lftp`—一个高级的基于文本的 FTP 程序
- `nautilus`—红帽的图形文件管理器和浏览器
- `ncftp`—一个复杂的基于文本的 FTP 程序
- `sftp`—安全文件传输程序
- `smclient`—Samba FTP 客户端，用于访问资源上的 SMB/CIFS 资源
- `system-config-services`—红帽的系统服务 GUI 管理工具
- `vsftpd`—非常安全的 FTP 守护进程
- `webcam`—包含在 xawtw 中的面向网络摄像头的 FTP 客户端

## 引用资料

- `http://www.wu-ftpd.org`—WU-FTP 官方网站
- `http://fedora.redhat.com/`—红帽 Fedora Core 官方网站
- `http://www.cert.org/`—计算机应急响应小组
- `http://www.openssh.com/`—OpenSSH 主页，以及最新版本 OpenSSH 及其组件客户端（如 `sftp`）的源码
- `http://www.cert.org/tech_tips/anonymous_ftp_config.html`—CERT 匿名 FTP 配置指南
- `http://vsftpd.beasts.org/`—vsftpd 服务器主页
- `ft://ferret.lmh.ox.ac.uk/pub/linux/vsftp`—vsftpd 服务器最新发布版本的下载站点

# 第 19 章 处理电子邮件

通过电子邮件进行通信（通常称为 email）无疑是互联网和局域网上最流行的活动之一。电子邮件快速、免费（显然如此）且易于使用。然而，在看似易用的背后，隐藏着一个复杂的架构，可以通过 Fedora Linux 的功能进行访问和控制。

在本章中，你将学习如何配置 Fedora Core 作为电子邮件服务器运行。你还将查看 Fedora Core 为你提供的各种电子邮件客户端，并学习一些使用这些客户端的技术。尽管你可能永远不需要管理邮件服务器，但理解它们的工作原理可以让你成为一个更出色的邮件用户。

## 本章内容

- 电子邮件如何发送和接收
- 选择邮件客户端 `MUA`
- 附件——将二进制文件作为文本发送
- 基础 Sendmail 配置与操作
- 使用 Fetchmail 检索邮件
- 选择邮件投递代理 `MDA`
- 邮件守护进程
- 微软 Exchange 服务器的困境
- 引用资料

## 电子邮件术语简介绍

世界上充斥着缩写和技术术语。这里介绍的第一部分术语描述了电子邮件系统的组件。某些应用程序结合了这三组组件的功能。

邮件用户代理 `MUA`、邮件客户端或邮件阅读器，允许用户读取和编写他们的电子邮件。这是大多数用户最熟悉的应用程序；它向用户呈现文本或图形界面。例如 `Evolution`、`Balsa`、`mutt`、`Mozilla Mail` 或 `KMail`。所有这些都由 Fedora Core 提供。

邮件传输代理 `MTA` 在后台工作，在计算机之间发送和接收电子邮件。例如 `Sendmail`、`Postfix`、`Fetchmail`、`Exim` 或 `Qmail`。但后两个都由 Fedora Core 提供。邮件投递代理 `MDA` 与 `MTA` 类似，但不处理系统之间的投递，也不像 `MUA` 那样为用户提供界面。例如 `Procmail` 或 `Spamassassin`；两者都为 `MTA` 提供过滤服务，其中后者由 Fedora Core 提供。

## 第 19 章 处理电子邮件

用于电子邮件的协议是缩写词的温床；接下来将介绍这些。

`RFC`—“意见请求”`Request For Comments` 是最接近互联网规则的内容。请参阅本章末尾的“资源”部分获取特定 RFC 的链接。通过更改链接中的数字，你可以查询任何 RFC。如果你安装了 `Fetchmail`，Eric S. Raymond 在 `/usr/share/doc/fetchmail/NOTES` 文件中列了一份与电子邮件相关的 RFC 列表（带有描述）。

`POP`—由 `RFC-1939` 定义，邮局协议 `Post Office Protocol` 是一种用于向客户端投递邮件的邮件服务器。`它不用于发送邮件；发送邮件使用的是 SMTP。` 当你在一台计算机上只有一个邮件客户端时（例如家庭用户），`POP` 非常好用。`POP` 设计为本地访问而设计；它从中央服务器下载所有邮件到本地客户端，并删除服务器上的文件。`MSP` 通常是更好的 POP 邮件访问方式。

`IMAP`—互联网邮件访问协议 `Internet Mail Access Protocol` 允许用户访问存储在远程服务器上的电子邮件，而不是本地磁盘。只要用户在使用支持 `IMAP` 的邮件客户端，就可以随地访问这些电子邮件。`IMAP` 是为局域网提供邮件的良好解决方案。Fedora Core 版本是华盛顿大学的 `IMAP` 服务器，位于 `http://www.washington.edu/imap`。

`SMTP`—由 `RFC-821` 定义，简单邮件传输协议 `Simple Mail Transport Protocol`，用于从一个地方发送邮件到另一个。

`MIME`—由 `RFC-2045` 定义，多用途互联网邮件扩展 `Multipurpose Internet Mail Extensions` 允许电子邮件包含非 ASCII 文本、二进制文件和附件。`MIME` 用于协议识别消息的部分类型。

## 电子邮件如何发送和接收

电子邮件通过网络以纯文本发送，使用 `SMTP` 用于从一个地方发送到另一个。邮件传输代理 `MTA` 在后台工作，在计算机之间发送和接收电子邮件。`MTAs` 是 `Sendmail`、`Postfix`、`Fetchmail` 或 `Qmail`。

## 邮件传输代理

`SMTP` 帮助沿线的计算机确定如何将邮件投递到目的地。

这是一个电子邮件成功处理的简化示例：

1. `user1@lion.org` 编写并发送电子邮件给 `user2@cheetah.org`。
2. `lion.org` 的 `MTA` 接收 `user1` 的邮件消息，并将其排队与其他其它等待发送的消息一起投递。
3. `lion.org` 的 `MTA` 连接 `cheetah.org` 的 25 端口。在 `cheetah.org` 确认连接后，`lion.org` 的 `MTA` 发送邮件。在 `cheetah.org` 接受并确认接收后，连接关闭。
4. `cheetah.org` 的 `MTA` 将邮件消息放入 `user2` 的邮箱中；`user2` 在登录时会收到新邮件通知。

当然，在这个过程中可能会发生几种故障：

如果 `user2` 不存在于 `cheetah.org` 在这种情况下，`cheetah.org` 将拒绝邮件并通知 `lion.org` 的 `MTA` 问题所在。`lion.org` 的 `MTA` 将生成一条邮件并发送给 `user1@lion.org`，告知她 `cheetah.org` 上不存在 `user2`。`或者取决于邮件配置，直接丢弃消息而不给发送者任何指示`。

如果 `cheetah.org` 对 `lion.org` 的连接尝试没有响应？`也许服务器正在进行维护。` `lion.org` 的 `MTA` 通知发送者初始投递尝试失败。将根据服务器管理员决定的间隔再次尝试，直到达到截止日期，然后通知发送者邮件无法投递。

等等——每个工具都有自己的优缺点。有些非常强大，但配置非常困难且速度较慢；另一些快速且易于配置，但不包含许多功能。以下章节将提供有关 Fedora Core 可用的一些常用 `MTA` 的更多信息。

# Sendmail

互联网上绝大多数电子邮件流量都由名为 `Sendmail` 的 `MTA` 处理，它是 Fedora Core Linux（以及许多其他 UNIX 发行版）的默认 `MTA`。`Sendmail` 的优势在于它是预装的并良好支持的

核心 Linux 系统。商业版本（不包含在 Fedora Core 中）还带有 GUI 配置工具。

`Sendmail` 是现有最古老且最强大的邮件传输代理 `MTA` 之一，但它也有一些缺点。它的速度较慢；在高负载环境下，包括 `Postfix` 和 `Qmail` 在内的其他 `MTA` 通常每秒可以处理多多的邮件。`Sendmail` 还以复杂而闻名；配置文件极其晦涩懂。`那本关于 Sendmail 的畅销书籍长度超过了 1000 页。`

幸运的是，Fedora Core 提供的 `Sendmail` 默认配置适用于大多数基础安装，只需将其配置为基础邮件服务器安装仅需进行微小的更改。然而，由于高级 `Sendmail` 配置的复杂性，许多管理员选择用其他 `MTA` 之一替换它。`你将在本章后部分的“基础 Sendmail 配置与操作” Basic Sendmail Configuration and Operation 中学习配置和使用 Sendmail 的基础知识`。

## Postfix

`Postfix`（最初于 1998 年作为 IBM Secure Mailer 发布）是一个流行的 `Sendmail` 替代方案；它快速、安全且易于管理。`Postfix` 是 `Sendmail` 的无缝替换方案（这意味着期望使用 `Sendmail` 的其他应用程序不会注意到 `Postfix` 替换了它，并会继续正常工作），而且将 `Sendmail` 安装迁移到 `Postfix` 相对简单。为了让这一切魔法般运行，`Postfix` 使用了 `Sendmail` 包装器（一个让其他程序认为它是 `Sendmail` 的接口），以便 `MUA`（邮件用户代理）等可以像与 `Sendmail` 通信一样与它通信。

> 注意
> Fedora Core 提供了版本 2 的 Post，它使用的配置与早期版本略有不同。如果你是从早期的 Red Hat 版本升级 `Postfix`，请检查你的配置文件。

Fedora 还针对第 2 版本的 Cyrus SASL 库（一个身份验证库）编译了 `Postfix` 和 `Sendmail`。发布说明 `Release Notes` 包含了文件位置和选项变化的详细信息，如果你使用这些库，这些更改将影响你。

为了增强安全性，许多 `Postfix` 进程使用 `chrootset`（限制仅访问文件系统的特定部分）来提高安全性，并且 `Postfix` 中没有 `setuid` 组件。在 Fedora 的当前版本中，某种配置已不再使用，而且实际上被 `Postfix` 作者建议不要使用。你可以手动将 `Postfix` 重新配置为 `chroot` 配置，但 Fedora 不再支持该配置。

如果你是从零开始，`Postfix` 被认为是比 `Sendmail` 更好的选择。

## Qmail 和 Exim

`Qmail` 是 `Postfix` 的直接竞争对手，但 Fedora Core 未提供它。`Postfix` 设计得比 `Sendmail` 更易用，同时也更快、更安全。然而，

`Qmail` 不是 `Sendmail` 的无缝替换方案，因此迁移现有的 `Sendmail` 安装并不像 `Sendmail` 迁移到 `Postfix` 那样简单。`Qmail` 相对容易管理，并与许多软件插件集成，包括 Web 邮件系统和 `POP3` 服务器。你可以从 `http://www.qmail.org/` 获取 `Qmail`。

`Exim` 是另一个 `MTA`，可以在 `http://www.exim.org/` 获取。`Exim` 被认为比 `Sendmail` 或 `Postfix` 更快、更安全，但其配置与后两者任何一个都不同。`Exim` 和 `Qmail` 使用 `maildir` 格式而不是 `mbox`，因此两者都被认为是“NFS 安全的”`见下文侧边栏`。

## MDIR 对比 MAILBOX

`Qmail` 还引入了 `maildir`，这是存储入站邮件的标准 UNIX 方法的替代方案。`maildir` 是一个更通用的电子邮件处理系统，但它要求你重新配置邮件客户端，而且它与传统的 UNIX 存储入站邮件的方式兼容。你需要使用识别 `maildir` 格式的邮件程序。`现代程序都是支持的。`

传统的 `mbox` 格式将分配到一个文件夹的所有邮件合并为一个单独的文件，并维护单封邮件的索引。使用 `maildir` 时，每个邮件文件夹都有子目录：`/cur`、`/new` 和 `/tmp`。每封邮件都保存在一个独特的文件。如果你在为大量人员运行邮件服务器，你应该选择一个能够高效处理大量小文件的文件系统。

`mbox` 有一个主要缺点。虽然单体 `mbox` 文件包含了你所有的电子邮件，但会发生某种损坏，要么损坏文件本身，要么损坏索引。从该问题中恢复可能是困难的。如果通过网络访问文件，`mbox` 文件特别容易出现问题并可能导致文件损坏；应该避免访问挂载在 `NFS`（网络文件系统）上的 `mbox` 文件，因为可能会发生文件损坏。

取决于你如何访问邮件，`maildirir` 允许多个应用程序同时访问 `maildir` 文件；而 `maildir` 不允许。

`MUA` 的选择影响你对邮件目录格式的选择。例如，`pine` 不缓存任何目录信息，并且每次访问邮件目录时必须读取它。如果你正在使用 `pine`，`maildir` 将是一个糟糕的选择。更高级的 `MUA` 执行缓存，因此 `maildir` 可能是一个不错的选择，尽管 `mua` 缓存可能会不同步。似乎没有完美的选择。

Fedora Linux 为你提供了既有优点也有缺点的邮件替代方案。请注意这些替代方案之间的差异，并频繁重新评估你的选择，以确保它是最适合你情况的选择。

## 选择 MTA

Fedora Core 还有其他 `MTA` 可用，但如前几节所述，上述这些是比较流行的。你应该选择哪一个？这取决于你需要做什么。`Sendmail` 的主要优势是它被视为标准，并且它可以完成许多其他 `MTA` 不能做的事情。然而，如果易用性或速度对你来说，你可能想考虑将 `Sendmail` 替换为 `Postfix`、`Exim` 或 `Qmail`。由于 `Sendmail` 是 Fedora Core 包含的默认 `MTA`，将在下一节中详细介绍。

## 邮件投递代理 MDA

`SMTP` 是一种服务器之间的协议，设计用于向始终连接的系统传递邮件。拨号系统仅根据用户命令连接；它们经常断开连接。为了适应这种差异，许多邮件系统还包含一个邮件投递代理，即 `MDA`。`MDA` 将邮件传输到没有永久连接的系统。`MDA` 类似于 `MTA`（见下文注释），但不处理系统之间的传递，并为用户提供界面。

> `Procmail` 或 `Spamassin` 是 `MTA` 的示例；它们在本地存储消息时为 `MTA` 提供过滤服务，然后将其供 `MUA` 读取

`MDA` 使用 `POP3` 和 `IMAP` 协议来实现此。类似于类似于邮局的方式，`POP3` 和 `IMAP` 实现了“存储并转发”的过程，如果你只是读邮件，这样就不需要维护本地邮件服务器。例如，拨号上网用户可以定期连接到他们的 ISP 邮件服务器，使用 `Fetchmail` 获取邮件——这是 Fedora Core 提供的 `MDA`（见本章后部分的“使用 Fetchmail 获取邮件”章节）。

## 邮件用户代理 MUA

邮件用户代理，或 `MUA`，是邮件系统的另一个必要部分。`MUA` 是一个邮件客户端或邮件阅读器，允许用户读取和编写电子邮件，并提供用户界面（大多数用户熟悉的“电子邮件”是指应用程序本身。）某些 UNIX 命令行 `MUA` 有 `email`、`pine` 和 `mutt`。Fedora Core 提供了现代的 GUI `MUA`：`Mozilla Mail`、`Balsa`、`Evolution`、`Thunderbird` 和 `KMail`。作为对比，常见的非 UNIX `MUA` 有 Microsoft Outlook、Outlook Express、Pegasus、Eudora 和 Messenger。

Microsoft Windows 和 Macintosh `MUA` 通常包含某些 `MTA` 功能；UNIX 不包含。例如，Microsoft Outlook 可以连接到你的 Internet 提供商邮件服务器以发送消息。相反，UNIX `MUA` 通常依赖于外部 `MTA`，如 `Sendmail`。这似乎是一个不必要的复杂的方法，而且它用于将单个用户连接到 ISP。对于任何其他情况，使用外部 `MTA` 允许你获得更大的灵活性，因为可以使用任何外部程序来处理和处理你的电子邮件功能和

自定义服务。通过由不同的应用程序处理进程，你可以非常灵活地控制如何为网络上的用户以及个人和 SOHO（家庭办公）用户提供电子邮件服务。

例如，你可以：

- 使用 `Evolution` 读取和编写邮件。
- 使用 `Sendmail` 发送邮件。
- 使用 `xbill` 在你有新邮件时通知你。
- 使用 `Fetchmail` 从远程邮件服务器检索邮件。
- 使用 `Procmail` 根据发件者、主题以及许多其他变量对收到的邮件进行自动排序。
- 使用 `Spammassin` 在你阅读邮件之前消除不需要的邮件。

## 选择邮件客户端 MUA

你需要一个客户端来读取邮件。Fedora Core 提供了一个名为 `mutt` 的控制台邮件客户端；其他如 `elm` 或 `pine` 的客户端可以从常规来源（如存储为 Freshmart 或 RPMind 的仓库）或从我的网站或应用程序页面获取。在选择 `MUA` 时，你可以从许多高度可配置的命令行客户端和易于使用的菜单驱动客户端中进行选择。以下章节将讨论其中一些客户端，以及 GUI 邮件客户端程序。GUI 是新用户最常选择的 `MUA`。然而，许多人在尝试后发现基于控制台的文本 `MUA` 非常有用，因此不要自误而忽略了它们。

你选择的图形化 `MUA` 可能与 Microsoft Outlook 或 Outlook Express 客户端有些相似。这些应用程序被广泛使用，许多用户都很熟悉。现代 Linux 邮件客户端在保持熟悉性的同时，提供了增强功能、功能和可配置性，这些都是 UNIX 环境的标志。`Evolution` 客户端已成为 Fedora Core 的默认 `MUA`，它与 MS Outlook 非常相似。

## 邮件应用程序

所有 UNIX 和 Linux 发行版都包含一个名为 `mail` 的 UNIX 实用程序。由于它的界面非常简单，通常不用于交互操作。然而，`mail` 在 shell 脚本中仍然极其有用，因为它可以从命令行获取发送邮件所需的所有信息。不需要用户交互。`mail` 也适用于发送快速备注的菜单，因为它启动速度快，不需要通过菜单即可发送消息。

## 第 19 章处理电子邮件

### 使用 mail

要开始使用 `mail` 发送消息，只需在 shell 提示符下输入 `mail`，后跟着要发送的邮件地址：

```
$ mail john@cheetah.org
```

`mail` 将提示你输入消息主题。输入主题并按回车。光标将会移动到下一个空行。现在你可以开始输入消息正文了。完成后，在空行上按 `Ctrl+D` 退出 `mail` 程序并发送消息。`可能会提示你输入 Cc:。如果你不想向任何人发送抄送，直接按回车即可。` 消息将移交给 `MTA`，你的提示符将返回。如果想放弃正在编写的消息，请按 `Ctrl+C`。

如果你想使用 `mail` 程序检索邮件，只需在 shell 提示符下输入 `mail`。系统将返回类似以下的内容：
