
此文件的一个示例见清单 24.6。

## **清单 24.6** 包含传入和传出日志记录的 /var/log/xferlog 文件示例

```
Mon Sep 3 07:13:05 2001 1 localhost.localdomain 100
/var/ftp/pub/README b o a testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/configuration a
_ o a testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/temp.txt a o a
testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/ftp-server-
0.17-14.i386.rpm a o a testing@test.com ftp 0 * c
Mon Sep 3 02:35:35 2001 1 helios 8 /var/ftp/pub/wu-ftpd-2.6.1-
22.i386.rpm a o a testing@test.com ftp 0 * c
```

## 相关的 Fedora 和 Linux 命令

- 你使用以下命令在 Fedora Core 中安装、配置和管理 FTP 服务：
  - **epiphany**——支持 FTP 的图形化 GNOME 浏览器
  - **ftp**——基于文本的交互式 FTP 命令
  - **ftpcopy**——从 FTP 服务器复制目录和文件
  - **ftpp**——从远程 FTP 服务器检索数据，但不覆盖现有的本地文件
  - **gftp**——GNOME 的图形化 FTP 客户端
  - **konqueror**——KDE 的图形化 Web 浏览器
  - **lftp**——高级基于文本的 FTP 程序
  - **nautilus**——Red Hat 的图形化文件资源管理器和浏览器
  - **ncftp**——功能强大、基于文本的 FTP 程序
  - **sftp**——安全文件传输程序
  - **smbclient**——用于访问服务器上的 SMB/CIFS 资源的 Samba FTP 客户端
  - **system-config-services**——Red Hat 的系统服务 GUI 管理实用程序
  - **vsftpd**——非常安全的 FTP 守护进程
  - **webcam**——随 xawtv 包含的面向网络摄像头的 FTP 客户端

## 参考

- http://www.wu-ftpd.org/——wu-ftp 官方网站。
- http://www.cert.org/——计算机应急响应小组。
- http://www.openssh.com/——OpenSSH 主页以及最新版本 OpenSSH 及其组件客户端（如 sftp）的源码。
- http://www.cert.org/tech_tips/anonymous_ftp_config.html——CERT 匿名 FTP 配置指南。
- http://vsftpd.beasts.org/——vsftpd FTP 服务器的主页。
- ftp://vsftpd.beasts.org/users/sevans/——vsftpd 服务器最新版本的下载站点。

## 第 25 章
## 处理电子邮件

### 本章内容

- 电子邮件的发送与接收方式
- 基本的 Sendmail 配置与操作
- 介绍 Postfix
- 使用 Fetchmail 获取邮件
- 选择邮件交付代理
- 邮件守护进程
- Microsoft Exchange 服务器的替代方案
- 参考资源

电子邮件仍然是互联网上主导的通信形式。它速度快、免费且非常容易使用。然而，幕后发生的许多事情极其复杂，对于不太了解电子邮件处理方式的人来说可能会显得令人望而生畏。Fedora 配备了多种功能强大的应用程序，帮助你构建从小型邮件服务器到处理数千封消息的大型服务器等各类系统。

本章将向你展示如何配置 Fedora 作为邮件服务器。我们将探讨 Fedora 中可用的选项，并逐一分析每个选项的优缺点。你还将了解电子邮件在 Linux 中的处理机制，以及在较小程度上了解 UNIX 的处理方式。

### 电子邮件的发送与接收

电子邮件通过全球各地的网络使用 SMTP 协议（*简单邮件传输协议*）以纯文本形式传输。顾名思义，该协议本身相当基础，并已被扩展以增加进一步的认证和错误报告/消息功能，以满足现代电子邮件不断增长的需求。邮件传输代理（或 MTA）在后台运行，在服务器之间传输电子邮件，使邮件能够发送到世界各地。你可能接触过诸如 Sendmail、Postfix、Fetchmail、Exim 或 Qmail 等 MTA 软件。

SMTP 允许电子邮件经过的每台计算机将其转发到通往最终目的地的正确方向。当你考虑到世界上有数百万个邮件服务器时，不得不惊叹这一切看起来是多么简单。

以下是电子邮件成功处理并发送到目的地的简化示例：

1. `andrew@hudson.org` 撰写并发送一封电子邮件消息给 `paul@nuzzlella.org`。
2. `hudson.org` 的 MTA 接收 andrew 的电子邮件消息，并将其排入队列，等待在其他等待发出的消息之后进行投递。
3. `hudson.org` 的 MTA 联系 `nuzzlella.org` 的 MTA（端口 25）。在 `nuzzlella.org` 确认连接后，`hudson.org` 的 MTA 发送邮件消息。在 `nuzzlella.org` 接受并确认收到消息后，连接关闭。
4. `nuzzlella.org` 的 MTA 将邮件消息放入 paul 的收件箱；paul 下次登录时会被通知他收到了新邮件。

当然，在此过程中可能会出现多种问题。以下是几个示例：

> 如果 `paul` 在 `nuzzlella.org` 上不存在怎么办？在这种情况下，`nuzzlella.org` 的 MTA 会拒绝该电子邮件，并通知 `hudson.org` 的 MTA 问题所在。随后，`hudson.org` 的 MTA 会生成一封电子邮件消息并发送给 `andrew@hudson.org`，告知他 `nuzzlella.org` 上不存在 paul（或者，根据邮件服务器的配置，它可能只是默默地丢弃该消息，而不向发件人提示任何问题）。

> 如果 `nuzzlella.org` 没有响应 `hudson.org` 的连接尝试会怎样？（也许服务器正在维护中。）`hudson.org` 的 MTA 会通知发件人初始投递尝试失败。服务器管理员决定的时间间隔内会进行进一步的尝试，直到达到截止日期，届时发件人将收到通知，得知邮件无法投递。

### 邮件传输代理

Fedora 有几种可用的 MTA，每种都有其优缺点。通常它们隐藏在 Fedora 的外衣之下，悄无声息地在世界各地的服务器之间传输邮件，几乎无需维护。一些 MTA 功能极其强大，能够每天处理数十万条消息，而另一些则更适合较小的安装环境。还有一些 MTA 也许功能不那么强大，但功能丰富。在下一节中，我们将介绍 Fedora 中一些更流行的 MTA。

### Sendmail

目前通过互联网传输的绝大多数电子邮件都由 Sendmail 处理，它恰好是 Fedora 提供的默认 MTA。它在 Linux/UNIX/BSD 世界中非常流行，并且支持度很高。有一个商业版本提供图形用户界面（GUI）以便于配置。

除了流行之外，与其他一些 MTA 相比，Sendmail 特别强大。然而，它并非没有缺点，且在更大的环境中，其他 MTA 每秒能处理的邮件量更多。Sendmail 的另一个问题是，要完全按照你的意愿进行配置可能极其复杂。幸运的是，有几本专门针对 Sendmail 的书可供参考，其中最受欢迎的一本有超过一千页，反映了 Sendmail 配置的复杂性。

幸运的是，Sendmail 的默认配置对于大多数基本安装来说开箱即用，无需进一步配置。即使你想将其用作基本的邮件服务器，你也只需要进行一些小的调整。Sendmail 相关的复杂程度通常导致系统管理员将其替换为更容易配置的其他替代方案。我们将在本章稍后的“基本 Sendmail 配置与操作”一节中查看一些基本的 Sendmail 配置。

### Postfix

Postfix 起源于 IBM Secure Mailer，但由 IBM 发布给社区。与 Sendmail 相比，它更易于管理，并且在速度上具有许多优势。Postfix 提供了 Sendmail 的无痛替代方案，你可以直接将 Sendmail 替换为 Postfix，而系统不会受到影响。实际上，依赖 Sendmail 的应用程序会自动使用 Postfix 代替，并继续正常工作。这是因为 Postfix 使用了一个 Sendmail 包装器（wrapper），它欺骗其他程序使其认为 Postfix 就是 Sendmail。这个包装器，或者更准确地说，接口，使得切换到 Postfix 极其简单。

> **注意**
> Fedora 提供的是 Postfix 2.2 版本，其配置方式与早期版本略有不同。如果你是从早期版本的 Fedora 或 Red Hat 升级 Postfix，请检查你的配置文件。
> Fedora 现在还将 Postfix 和 Sendmail 针对 Cyrus SASL 库（一种认证库）的第 2 版进行编译。发行说明包含关于文件位置和选项变化的详细信息，如果你使用这些库，这些变化将对你产生影响。

为了增强安全性，许多 Postfix 进程过去使用 chroot 功能（该功能限制只能访问文件系统的特定部分）以提高安全性，并且 Postfix 中没有 setuid 组件。在当前 Fedora 发行版中，不再使用 chroot 配置，事实上，Postfix 作者也不建议使用它。你可以手动将 Postfix 重新配置为 chroot 配置，但这不再受 Fedora 支持。

如果你是从零开始，Postfix 被认为比 Sendmail 是更好的选择。

### Qmail 和 Exim

Qmail 是 Postfix 的直接竞争者，但不随 Fedora 提供。Postfix 的设计旨在比 Sendmail 更易于使用，同时更快、更安全。然而，Qmail 并不是 Sendmail 的直接替代品，因此将现有的 Sendmail 安装迁移到 Qmail 并不像从 Sendmail 迁移到 Postfix 那么简单。Qmail 管理相对容易，并且可与多种软件附加组件集成，包括 Web 邮件系统和 POP3 服务器。Qmail 可从 http://www.qmail.org/ 获取。

