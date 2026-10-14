
```
set daemon 600
set postmaster foobar
set logfile ~/.fetchmail.log
```

```
poll mail.samenet.org
proto pop3
no dns
```

```
user foobar
pass secretword
fetchall
flush
```

此文件告诉 Fetchmail 执行以下操作：

- 每 600 秒检查 POP3 服务器 `mail.samenet.org` 的新邮件。
- 使用用户名 `foobar` 和密码 `secret` 登录。
- 从服务器下载所有消息。
- 下载后从服务器上删除消息。
- 将收到的任何无法投送到本地用户的邮件发送到账户 `foobar`。

![](img/3d6f0094eea43cca43a26f4e063dddf0_597_0.png)

你根据对邮件的处理方式选择 MDA（邮件投递代理）。在你的特定情况下，如果你有简单的需求（例如组织规则），那么提供过滤功能的 MUA（邮件用户代理）之一可能更适合你的情况。Ubuntu 提供了 Evolution MUA

## 选择邮件投递代理

作为默认选择（它包含了之前提到的某些 MDA 功能），因此请先尝试它，看看是否能满足你的需求。如果不满足，请研究 Ubuntu 提供的以下 MDA 之一。

除非另有说明，这里讨论的所有 MDA 都由 Ubuntu 存储库提供。第 9 章“管理软件”详细介绍了任何软件的通用安装方法。

### Procmail

作为一个面向高级用户的工具，Procmail 程序在邮件从邮件服务器获取时充当过滤器。它使用规则（称为配方）来读取每条消息。它不提供默认配置；你必须为每个用户手动创建一个 `~/.procmail` 文件，或者用户可以创建自己的。

系统没有系统级的默认配置。规则集的创建非常简单，但需要对正则表达式的使用有一定理解，这已经超出了本章的范围。Ubuntu 在 `/usr/share/doc/procmail/examples` 中提供了三个文件示例，并在 `/usr/share/doc/procmail` 目录下提供了一个带完整注释的示例。

### Spamassassin

如果你使用邮件已经很久，你可能受到过垃圾邮件的骚扰。Spassassin 是一个可以与 Sendmail 集成的工具。README 文件 `/usr/share/doc/spamassassin` 包含了关于规则集的说明。启用Spassassin 的操作非常简单。

### Squirrelmail

你可能通过 Web 界面读取邮件。Squirrelmail 支持 IMAP 和 SMTP。Squirrelmail 支持附件和地址录。

### 病毒扫描器

虽然目前认为 Linux 对针对微软用户的病毒具有免疫，但让 UNIX 邮件服务器允许感染邮件通过其发送是没有意义的。Ubuntu 默认不提供病毒扫描器，但在存储库中提供了一些流行的扫描器。可以查看 ClamAV。

### 自动回复

自动回复会对收到的消息生成回复；通常用于通知他人收件人不在。Ubuntu 默认不包含，但你可以从存储库找到并安装像 `vacation` 这样的自动回复。如果你订阅了邮件列表，请注意账户的自动回复可能会骚扰他人。在开启自动回复离开办公室之前，请取消订阅。

## 参考文献

- [www.sendmail.org](https://www.sendmail.org) Sendmail 首页，可以在此处找到邮件 MTA 的配置信息和常见问题。
- [www.postfix.org](https://www.postfix.org) Postfix 首页，可以在此处找到文档和示例配置。
- [help.ubuntu.com/community/Postfix](https://help.ubuntu.com/community/Postfix) 关于 Postfix 的 Ubuntu 社区文档。
- [www.qmail.org](https://www.qmail.org) Qmail MTA 首页，包含了文档以及关于 Qmail 的其他资源。
- [help.ubuntu.com/community/ClamAV](https://help.ubuntu.com/community/ClamAV) 关于 ClamAV 的 Ubuntu 社区文档。
- [rfc-editor.org](https://rfc-editor.org) 征求意见（RFC）存储库，定义了现代计算机使用的“规则”。
- [www.procmail.org](https://www.procmail.org) Procmail 首页。
- **Sendmail by Brian Costales, Claus Assmann, George Jansen, and Gregory Shapiro** 安全 Sendmail 的事实标准指南，超过 1000 页，让你知道 Sendmail 到底有多复杂。
- **Postfix by Richard Blum** 一本涵盖 Postfix MTA 的优秀书籍。
- **Postfix: The Definitive Guide by Kyle D. Dent** 另一个 Postfix 的另一个优秀资源。

# 第 35 章

## 本章内容

# 代理、反向代理与虚拟专用网络 (VPN)

- 什么是代理服务器？
- 安装 Squid
- 配置客户端
- 访问列表
- 指定客户端 IP 地址
- 示例配置
- 虚拟专用网络 (VPN)
- 参考文献

在这个世界上，两样东西你越拥有越好：时间和与带宽。Ubuntu 自带了一个名为 Squid 的代理服务器，它可以让你在服务器上缓存流量，从而使网站加载更快，用户消耗的带宽更少。某些代理服务器是为了安全和隐私的，但如果安全和隐私是你的主要考虑，虚拟专用网络（VPN）是更好的选择。本章的最后一节关于 VPN。代理服务器和 VPN 都有一个有趣的特性：你的计算机连接的所有内容（例如某个网站）都认为代理或 VPN 服务器的 IP 地址就是你的 IP 地址。

## 什么是代理服务器？

代理服务器位于客户端（例如你公司的桌面电脑）和互联网之间。当客户端请求网站时，它们不会直接连接 Web 并发送 HTTP 请求，而是连接到本地代理服务器。然后，代理将它们的请求转发到互联网，获取结果并将其发送回客户端。简单来说，代理服务器实际上只是客户端和服务器之间的额外层，那么为什么要多费此呢？

部署代理服务器的三个主要原因如下：

- 内容控制——你想防止访问某些类型的内容。
- 速度——你想缓存常用网站以最大限度地利用带宽。
- 安全——你想监控人们在做什么。

Squid 可以实现这些功能以及更多。

## 安装 Squid

你可以轻松从 Ubuntu 软件仓库中安装 Squid，它在其中被称为 `squid`。安装 Squid 后，它会在每次启动时自动启用。你可以在机器启动时运行 `ps aux | grep squid` 来检查它。如果没有看到输出，请运行 `sudo systemctl start squid`。

## 配置客户端

在配置新的 Squid 服务器之前，先设置好用于访问的本地 浏览器。这可以让你在处理配置文件时测试规则。

要配置 Firefox，当 Firefox 在前台运行时，从 Ubuntu 桌面顶部面板的“编辑”菜单中选择“选项 (Preferences)”。在出现的对话框中，使用第一行的图标选择“高级设置 (Advanced)”，并在高级中选择“网络 (Network)”选项卡。然后点击“设置”按钮来配置 Firefox 如何连接互联网，并选择“手动代理配置 (Manual Proxy Configuration)”。勾选下方的“所有协议均使用相同代理”。在 HTTP 代理框中输入 `127.0.0.1`，端口输入 `3128`。外观见图 35.1。如果你使用的是远程客户端，请选择 Squid 服务器的 IP 地址而不是 `127.0.0.1`。

![](img/3d6f0094eea43cca43a26f4e063dddf0_602_0.png)

图 35.1 设置 Firefox 使用 127.0.0.1 使其所有 Web 请求都通过 Squid 进行。

## 访问列表

你同样可以配置其他网络浏览器，如 Google Chrome、Opera 等。区别在于使用的标签和选项的菜单位置，你可能需要稍微挖掘一下才能发现调整特定浏览器的设置。

## 访问列表

Squid 主配置文件是 `/etc/squid/squid.conf`，默认的 Ubuntu 配置文件包含了许多引导你使用的注释。默认配置允许完全访问本地机器，但拒绝你的网络其他部分。这是一个安全的起点；我们建议你在向他人发布规则之前，先在自己（localhost）上尝试所有规则。

打开两个终端窗口。在第一个窗口中，切换到目录 `/var/log/squid` 并运行此命令：

```bash
mathew@sem:~ sudo tail -f access.log
```
