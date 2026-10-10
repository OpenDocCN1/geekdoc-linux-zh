

## 相关的 Fedora 和 Linux 命令

在 Fedora 中，使用以下命令来安装、配置和管理 FTP 服务：

- **epiphany**—支持 FTP 的图形化 GNOME 浏览器
- **ftp**—基于文本的交互式 FTP 命令
- **ftpcopy**—从 FTP 服务器复制目录和文件
- **ftpcur**—从远程 FTP 服务器获取数据，但不会覆盖现有的本地文件
- **gftp**—GNOME 的图形化 FTP 客户端
- **konqueror**—KDE 的图形化网络浏览器
- **lftp**—一个高级的基于文本的 FTP 程序
- **nautilus**—Red Hat 的图形化文件资源管理器及浏览器
- **ncftp**—一个复杂的基于文本的 FTP 程序
- **sftp**—安全文件传输程序
- **smbclient**—用于访问服务器上 SMB/CIFS 资源的 Samba FTP 客户端
- **system-config-services**—Red Hat 的系统服务 GUI 管理工具
- **vsftpd**—非常安全的 FTP 守护进程
- **webcam**—xawtv 中附带的一个面向摄像头的 FTP 客户端

## 参考资料

- **http://www.wu-ftpd.org/**—wu-ftpd 官方网站。
- **http://www.cert.org/**—计算机应急响应团队。
- **http://www.openssh.com**—OpenSSH 主页以及最新版本的 OpenSSH 及其组件客户端（如 **sftp**）的源代码。
- **http://www.cert.org/tech\_tips/anomymous\_ftp\_config.html**—CERT 匿名 FTP 配置指南。
- **http://vsftpd.beasts.org/****—**vsftpd** FTP 服务器的主页。
- **ftp://vsftpd.beasts.org/users/cevasan/**—最新发布的 **vsftpd** 服务器下载站点。

# 第 21 章
## 处理电子邮件

电子邮件仍然是互联网上占主导地位的通信形式。它速度快、免费且极易使用。然而，幕后发生的大量事务极其复杂，对于不了解电子邮件处理机制的人来说可能会显得令人望而生畏。Fedora 配备了一系列强大的应用程序，可帮助您构建从小型电子邮件服务器到处理数千条消息的大型服务器的任何东西。

本章将展示如何配置 Fedora 以充当电子邮件服务器。我们将探讨 Fedora 中可用的选项，以及每个选项的优缺点。您还将了解电子邮件在 Linux 中是如何被处理的，以及在较小程度上，在 UNIX 中是如何被处理的。

## 电子邮件如何发送和接收

电子邮件通过 *SMTP*（*简单邮件传输协议*）以纯文本形式在全球各地的网络中传输。顾名思义，该协议本身相当基础，并经过扩展以增加更多的认证和错误报告/消息功能，以满足现代电子邮件日益增长的需求。*邮件传输代理*（*MTA*）在后台工作，将电子邮件从一台服务器传输到另一台服务器，使电子邮件可以发送到世界各地。您可能已经接触过此类 *MIA* 软件，如 Sendmail、Postfix、Fetchmail、Exim 或 Qmail。

SMTP 使邮件经过的每一台计算机都能将其转发到通往最终目的地的正确方向。当您考虑到世界上有数百万台电子邮件服务器时，就会惊叹于这一切看似多么简单。

### 本章内容

- 电子邮件如何发送和接收
- Sendmail 基本配置和操作
- 介绍 Postfix
- 使用 Fetchmail 获取邮件
- 选择邮件投递代理
- 邮件守护进程
- Microsoft Exchange Server 的替代方案
- 参考资料

这是一个关于电子邮件如何被成功处理并发送到目的地的简化示例：

1. andrew@hudson.org 编写并发送一封电子邮件消息给 paul@hudzilla.org。
2. hudson.org 上的 MTA 接收 andrew 的电子邮件消息，并将其排队等待投递，排在该时段内其他等待发出的消息之后。
3. hudson.org 上的 MTA 通过 25 端口联系 hudz11a.org 上的 MTA。在 hudz11a.org 确认连接后，hudson.org 上的 MTA 发送邮件消息。在 hudz11a.org 接受并确认收到该消息后，连接关闭。
4. hudz11a.org 上的 MTA 将邮件消息放入 paul 的收件箱；paul 在下次登录时会被通知他有新邮件。

当然，在这个过程中可能会出现许多问题。请考虑以下示例：

- 如果 paul 在 hudz11a.org 上不存在怎么办？在这种情况下，hudz11a.org 上的 MTA 将拒绝该电子邮件，并通知 hudson.org 上的 MTA 问题所在。随后，hudson.org 上的 MTA 会生成一封电子邮件消息并发送给 andrew@hudson.org，告知他 hudz11a.org 上不存在 paul（或者根据电子邮件服务器的配置，可能只是静默丢弃该消息，不给发送者任何问题的迹象）。
- 如果 hudz11a.org 没有响应 hudson.org 的连接尝试会发生什么？（也许服务器正在停机维护中。）hudson.org 上的 MTA 会通知发送者初始投递尝试失败。服务器管理员决定的间隔时间内会进行进一步的尝试，直到达到截止日期，然后发送者将收到通知，表明该邮件无法投递。

## 邮件传输代理

Fedora 提供几种 MTA，每种都有各自的优缺点。通常它们隐藏在 Fedora 的底层，默默地在全球各地服务器之间传输邮件，几乎不需要维护。一些 MTA 功能极其强大，每天能够处理数十万条消息，而另一些则面向较小的安装环境。其他 MTA 可能功能稍弱，但功能丰富。下一节将介绍 Fedora 上一些更受欢迎的 MTA。

### Sendmail

当今互联网上传输的电子邮件的绝大多数都是由 Sendmail 处理的，而它恰好也是 Fedora 提供的默认 MTA。它在 Linux/UNIX/BSD 世界中非常流行，并得到良好的支持。有一个商业版本可用，提供了用于简化的 GUI 配置界面。

除了流行之外，与其他一些 MTA 相比，Sendmail 特别强大。然而，它并非没有缺点，其他 MTA 在大型环境中每秒可以处理更多的电子邮件。Sendmail 的另一个问题是，要将其设置得完全符合您的意愿可能极其复杂。事实上，与 Sendmail 相关的复杂程度通常会导致系统管理员将其替换为更容易配置的其他替代方案。市面上有几本专门针对 Sendmail 的书，但最受欢迎的那本有超过一千页，反映了 Sendmail 配置的复杂性质。

然而，好消息是，Sendmail 的默认配置对于大多数基本安装来说开箱即用，不需要进一步配置。即使您想将其用作基本的电子邮件服务器，也只需进行一些微小的调整。我们将在本章稍后标题为“Sendmail 基本配置和操作”的章节中查看一些基本的 Sendmail 配置。

### Postfix

Postfix 起源于 IBM Secure Mailer，但由 IBM 发布给开发社区。与 Sendmail 相比，它更容易管理，并且具有许多速度优势。Postfix 提供了 Sendmail 的无痛替代方案，您可以将 Sendmail 替换为 Postfix，而系统不会出任何问题。事实上，当您安装 Postfix 替代 Sendmail 时，依赖 Sendmail 的应用程序会自动使用 Postfix 并继续正常工作。Postfix 使用 Sendmail 包装器，使其他程序误以为 Postfix 就是 Sendmail。这个包装器，或者更准确地说是接口，使得切换到 Postfix 变得极其简单。

> **注意**
> Fedora 提供 Postfix 版本 2.4，其配置与早期版本略有不同。如果您正在从早期版本的 Fedora 或 Red Hat 升级 Postfix，请检查您的配置文件。
> Fedora 现在针对版本 2.1 的 Cyrus SASL 库（一个认证库）编译 Postfix 和 Sendmail。发行说明中包含关于文件位置和选项更改的详细信息，如果您使用这些库，这些信息将对您产生影响。

为了增强安全性，许多 Postfix 进程过去使用 chroot 机制（该机制限制访问仅限于文件系统的特定部分）来提高安全性，并且 Postfix 中没有 setuid 组件。在当前的 Fedora 版本中，不再使用 chroot 配置，实际上 Postfix 作者也不推荐这样做。您可以手动将 Postfix 重新配置为 chroot 配置，但 Fedora 不再支持此配置。

如果您是从零开始，Postfix 被认为是比 Sendmail 更好的选择。

### Qmail 和 Exim

Qmail 是 Postfix 的直接竞争者，但未随 Fedora 提供。Postfix 的设计目标是比 Sendmail 更易用，同时更快、更安全。然而，Qmail 并不是

