
# Ubuntu 中 FTP 服务与邮件传输

你使用以下命令在 Ubuntu 中安装、配置和管理 FTP 服务：

- `epiphany`—支持 FTP 的图形 GNOME 浏览器
- `ftp`—基于文本的交互式 FTP 命令
- `ftpcopy`—从 FTP 服务器复制目录和文件
- `ftpcp`—从远程 FTP 服务器检索数据，但不覆盖现有本地文件
- `gftp`—GNOME 的图形 FTP 客户端
- `konqueror`—KDE 的图形网页浏览器
- `lftp`—高级基于文本的 FTP 程序
- `nautilus`—Gnome 的图形文件资源管理器和浏览器
- `ncftp`—功能强大的基于文本的 FTP 程序
- `sftp`—安全文件传输程序
- `smbclient`—访问服务器上 SMB/CIFS 资源 的 Samba FTP 客户端
- `vsftpd`—非常安全的 FTP 守护进程
- `webcam`—随 `xawtv` 包含的面向网络摄像头的 FTP 客户端

## 参考

- http://www.wu-ftpd.org/—官方 Wu-FTP 网站。
- http://www.cert.org/—计算机应急响应团队。
- http://www.openssh.com/—OpenSSH 主页以及 OpenSSH 最新版本及其组件客户端（如 `sftp`）的源。
- http://www.cert.org/tech_tips/anonymous_ftp_config.html—CERT 匿名 FTP 配置指南。
- http://vsftpd.beasts.org/—`vsftpd` FTP 服务器的主页。
- ftp://vsftpd.beasts.org/users/cevans/—`vsftpd` 服务器最新版本的下载站点。

### 邮件投递流程示例

1. `andrew@hudson.org` 编写并发送一封电子邮件给 `paul@hudzilla.org`。
2. `hudson.org` 的 MTA 收到 Andrew 的电子邮件，并将其排在所有其他等待发送的邮件后面，等待发送。
3. `hudson.org` 的 MTA 通过 `25` 端口联系 `hudzilla.org` 的 MTA。在 `hudzilla.org` 确认连接后，`hudson.org` 的 MTA 发送邮件。`hudzilla.org` 接受并确认收到消息后，连接关闭。
4. `hudzilla.org` 的 MTA 将邮件放入 Paul 的收件箱；Paul 下次登录时会收到有新邮件的通知。

当然，这个过程中可能会有很多事情出错。以下是一些例子：

如果 `hudzilla.org` 上不存在 Paul 怎么办？在这种情况下，`hudzilla.org` 的 MTA 会拒绝该邮件，并通知 `hudson.org` 的 MTA 问题所在。然后 `hudson.org` 的 MTA 会生成一封电子邮件发送给 `andrew@hudson.org`，告知他 `hudzilla.org` 上不存在 Paul（或者，根据邮件服务器的配置，只是静默丢弃该邮件，不给发件人任何问题指示）。

如果 `hudzilla.org` 不响应 `hudson.org` 的连接尝试怎么办？（也许服务器因维护而停机。）`hudson.org` 的 MTA 会通知发件人初次投递尝试失败。随后，会按照服务器管理员决定的时间间隔进行进一步尝试，直到到达截止时间，届时发件人会收到邮件无法投递的通知。

## 邮件传输代理

Ubuntu 提供了多种 MTA，各有其优缺点。它们通常隐藏在 Ubuntu 系统内部，默默地在世界各地的服务器之间传递邮件，几乎不需要维护。有些 MTA 极其强大，每天能够处理数十万条消息，而有些则更适用于小型安装环境。另外一些 MTA 可能没有那么强大，但功能丰富。在下一节中，我们将介绍 Ubuntu 可用的一些较流行的 MTA。

### Postfix

`Postfix` 起源于 IBM Secure Mailer，但由 IBM 发布给社区。与 `Sendmail` 相比，它更易于管理，并且具有许多速度优势。`Postfix` 可以无痛替代 `Sendmail`，你完全可以不费吹灰之力就用 `Postfix` 替换掉 `Sendmail`。事实上，依赖 `Sendmail` 的应用程序会自动改用 `Postfix` 并继续正常工作（因为 `Postfix` 使用了 `Sendmail` 包装器，让其他程序误以为 `Postfix` 就是 `Sendmail`）。这个包装器，或者更准确地说是一个接口，使得如果你已经在运行 `Sendmail`，切换到 `Postfix` 变得非常容易。`Postfix` 也恰好是 Ubuntu 的首选 MTA，因此本章后面我们会花更多时间介绍它。

为了增强安全性，许多 `Postfix` 进程过去使用 `chroot` 功能（将访问限制在文件系统的特定部分）来提高安全性，并且 `Postfix` 中没有 `setuid` 组件。在当前的 Ubuntu 版本中，不再使用 `chroot` 配置，事实上 `Postfix` 作者也不鼓励这样做。你可以手动将 `Postfix` 重新配置为 `chroot` 配置，但 Ubuntu 已不再支持这种配置。

如果你是从零开始，`Postfix` 被认为是比 `Sendmail` 更好的选择。

### Sendmail

`Sendmail` 处理着当今互联网上传输的绝大多数电子邮件。它在 Linux/UNIX/BSD 世界中非常流行，并且得到了良好的支持。还有一个商业版本，提供 GUI 界面，便于配置。

`Sendmail` 不仅广受欢迎，而且与其他一些 MTA 相比特别强大。然而，它并非没有缺点，你会发现其他 MTA 在更大的环境中每秒可以处理更多邮件。`Sendmail` 的另一个问题是，要完全按照你想要的方式进行配置可能极其复杂。有几本书专门介绍 `Sendmail`，但最流行的一本超过一千页，这反映了 `Sendmail` 配置的复杂性。

但值得庆幸的是，`Sendmail` 的默认配置对大多数基本安装开箱即用，因此无需进一步配置。即使你想将它用作基本邮件服务器，也只需要做一些小调整。`Sendmail` 的复杂性常常导致系统管理员用其他更易于配置的替代品替换它。

### Qmail 和 Exim

`Qmail` 是 `Postfix` 的直接竞争对手，但并不随 Ubuntu 提供。`Qmail` 的设计目标是比 `Sendmail` 更易用、更快、更安全。然而，`Qmail` 不是 `Sendmail` 的直接替代品，因此将现有的 `Sendmail` 安装迁移到 `Qmail` 并不像从 `Sendmail` 迁移到 `Postfix` 那么简单。`Qmail` 相对易于管理，并且与许多软件附加组件集成，包括 Web 邮件系统和 POP3 服务器。`Qmail` 可从 http://www.qmail.org/ 获取。

`Exim` 是另一种 MTA，可从 http://www.exim.org/ 获取。`Exim` 被认为比 `Sendmail` 或 `Postfix` 更快、更安全，但配置起来与这两者有很大不同。`Exim` 和 `Qmail` 使用 `maildir` 格式而不是 `mbox`，因此两者都被认为是“NFS 安全”的（参见下面的侧边栏）。

## MDIR 与 Mailbox 的对比

`Qmail` 还引入了 `maildir`，这是标准 UNIX 存储传入邮件方式之外的另一种选择。`maildir` 是一种更通用的处理传入电子邮件的系统，但它要求重新配置你的电子邮件客户端，并且与传统的 UNIX 存储传入邮件方式不兼容。你需要使用能够识别 `maildir` 格式的邮件程序。（现代程序都能识别。）

传统的 `mbox` 格式将指派给某个文件夹的所有邮件合并保存为单个文件，并维护各封邮件的索引。而使用 `maildir` 时，每个邮件文件夹都包含三个子文件夹：`/cur`、`/new` 和 `/tmp`。每封电子邮件都保存在一个独立且唯一的文件中。如果你为大量用户运行邮件服务器，则应选择能够高效处理大量小文件的文件系统。

`mbox` 确实有一个重大缺点。当你在访问包含所有邮件的单一 `mbox` 文件时，假设文件本身或索引发生了某种损坏，要从此问题中恢复可能很困难。如果通过网络访问这些 `mbox` 文件，则它们尤其容易出现问题并可能导致文件损坏；应该避免访问通过 `NFS`（网络文件系统）挂载的 `mbox` 邮件，因为可能发生文件损坏。

根据你访问邮件的方式，`maildir` 确实允许多个应用程序同时访问 `maildir` 文件；`mbox` 则不允许。

邮件用户代理（MUA，即电子邮件客户端）的选择也会影响你对邮件目录格式的选择。例如，`pine` 程序不缓存任何目录信息，每次访问邮件目录时都必须重新读取。如果你使用 `pine`，那么 `maildir` 并不是一个好的选择。更先进的电子邮件客户端会执行缓存，因此 `maildir` 可能是好的选择，尽管电子邮件客户端的缓存可能会失去同步。似乎不存在完美的选择。

Ubuntu 为你提供了各有利弊的邮件替代方案。请注意各方案之间的差异，并经常重新评估你的选择，以确保它最适合你的情况。

## 选择 MTA

还有其他 MTA 可用于 Ubuntu，但前面几节讨论的是最流行的。你应该选择哪一个？这取决于你需要做什么。`Postfix` 的主要优势在于扩展性好，并且能够高速处理大量电子邮件，更不用说它比更晦涩难懂的 `Sendmail` 容易配置得多。然而，你可能会发现，有些特定需求只有 `Sendmail` 才能提供。需要时，在不同 MTA 之间切换很容易。

## 邮件投递代理
