
安装服务器后，只需要修改 `/etc/inetd.conf` 文件。当 POP 客户端尝试访问你的服务器时，它将与端口 `110` 通信。`inetd` 超守护进程将检测到通信并启动 `pop3`。

修改文件如下：确保注释掉引用 `pop-2` 的行。重启 `inetd` 守护进程。

```
/etc/rc.d/inetd restart
```

当 POP 请求到达系统时，`inetd` 将启动 `popd` 守护进程来处理请求。你的 POP 服务器现在准备好处理请求。

![](img/1d90939eac39ca76d12e353542e54751_316_0.png)

> 如果你想增强系统安全性，可能希望使用 TCP wrapper (`tcpd`) 使用的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件来限制对 POP 服务器的访问。详情请见第 17 章“安全 101”。

### 使用 IMAP

IMAP 协议与 POP 类似，IMAP 客户端（如 Netscape Communicator 或 `pipe`）与 IMAP 服务器交互以发送或检索消息。IMAP 服务器反过来向 SMTP 服务器发送或从其发送/检索消息。然而，IMAP 比 POP 更高效，因为它从服务器读取邮件标头信息，但保持消息内容不变。因此，一个或多个 IMAP 客户端可以同时访问 IMAP 服务器而不会触动消息。可以将信息从服务器传输到本地机器，但必须手动完成。

IMAP 服务器包含在 `pop.rpm` 包中，该包未作为最小 SuSE 安装的一部分安装。幸运的是，它不需要很多配置即可使用。要安装软件包，以 `root` 登录，挂载光盘，并运行：

```
rpm -ivh /cdrom/suse/n/pop.rpm
```

进一步的文档和源代码头可以从 `imap.rpm` 包获取：

```
rpm -ivh /cdrom/suse/n/imap.rpm
```

> 阅读 RFC 2060 以了解更多关于 IMAP 的信息。你也可以咨询 `/usr/doc/packages/pop` 和 `/usr/doc/packages/imap` 目录下的文档。

修改 `/etc/inetd.conf` 文件使 `imapd` 按需启动。

#### Imap - 交互式邮件访问服务器

#### 注意：此服务非常不安全

`imap stream tcp nowait root /usr/sbin/tcpd imapd`

你可以按照之前描述 POP 的方式与 IMAP 服务器通信。由于相似性，我们不再重复该过程。

## 配置 SMTP/POP/IMAP 邮件客户端

一旦配置了 SMTP 以及 POP 或 IMAP 服务器，你就需要为用户设置邮件客户端软件。如果用户将通过 Telnet 访问邮件服务器访问，你需要安装一个或多个邮件客户端包，如 `mail`、`pine` 和 `procmail`。使用 Telnet 访问邮件的用户很容易使用邮件转发功能。

但在大多数情况下，用户将通过运行 POP 客户端的 Windows 访问邮件。为了让用户配置典型的 Windows IMAP/POP/SMTP 邮件客户端，你只需要向每个用户提供以下信息：

- 用户名
- 密码
- 入站 POP/IMAP 邮件服务器 IP 地址或主机
- 出站 SMTP 邮件服务器 IP 地址或主机

注意，你必须允许此类客户端使用你的 `sendmail` 服务器作为中继，否则客户端将无法发送邮件。例如，如果你的邮件

## 第 10 章：电子邮件服务

如果通过 SouthWest Cyberport 访问服务器，你将不得不将 `swcp.com` 添加到你的 `/etc/mail/relay-domains` `sendmail` 配置文件中。

Netscape Communicator 是世界上最流行的电子邮件客户端之一，本文将对其进行介绍。由于我们没有配置 SuSE Linux 服务器使用 X 窗口系统，以下指令假设你将在另一台客户端机器上配置 Netscape Communicator。该客户端机器可以是 Linux、UNIX、Windows 或 Mac 机器，配置方法是相同的。然而，描述将针对一台通过 IMAP 访问 `sendmail` 服务器 `veracruz` 的 Linux 机器。

登录到任何可以使用 Netscape 的网络上，你可以。启动 Netscape 并选择 Edit（编辑）-> Preferences（首选项）。当 Netscape: Preferences 窗口弹出时，选择 Mail & Newgroups（邮件与新闻组）-> Mail Servers（邮件服务器）-> Add（添加）。添加你的 IMAP 服务器名称和用户名。默认设置是每十分钟检查一次电子邮件。你也可以选择保存你的 IMAP 密码（这与你在服务器上的用户名密码相同），或者在每次读取邮件时手动输入。按照图 10-4 所示输入信息，该图显示了完成后的 IMAP “add”窗口。

![](img/1d90939eac39ca76d12e353542e54751_318_0.png)

点击 OK 回到 Mail Servers 窗口。接下来，为发送邮件添加你的 SMTP 服务器名称，如图 10-5 所示。

![](img/1d90939eac39ca76d12e353542e54751_319_0.png)

点击 Identity（标识）选项并输入你的姓名和全限定电子邮件地址。你可以可选地输入组织名称和签名文件名，如图 10-6 所示。

![](img/1d90939eac39ca76d12e353542e54751_319_1.png)

点击 OK，你的信息就会被保存。打开 Netscape Communicator 并点击 Get（获取）按钮。Netscape 将从 IMAP 服务器读取你的电子邮件邮件头。你可以打开尽可能多的 IMAP 邮件客户端而不会占用你的电子邮件地址，因为只有邮件头被下载到客户端。实际消息（包括附件）将留在服务器上，直到你通过 File（文件）菜单选项显式地传输它们。

## sendmail 的商业替代方案

尽管我们认为开源 `sendmail` 服务器适用于几乎所有情况，但你的组织可能有某些需求，这些不允许使用 `sendmail` 作为主邮件服务器软件。例如，如果你组织的软件策略要求组织内的所有软件都必须由供应商提供商业支持，那么你可能需要使用 `sendmail` 的商业版本，因为它由 Sendmail, Inc. 直接支持。你可能还想购买一套系统，因为维护 `sendmail` 的复杂性不值得投入成本。在这种情况下，商业供应商可以为你的目的提供从头到尾（全生命周期）的支持。

以下是开源 `sendmail` 服务器的一些备替代方案。

### Sendmail Pro

Sendmail Pro 是开源 `sendmail` 服务器的商业版本。它带有增强功能，并提供了你从可靠供应商处期望的商业级支持。你可以在以下 URL 找到该产品的更多信息：http://www.sendmail.com/

> 不要将 http://www.sendmail.org/ 与 http://www.sendmail.com/ 混淆。第一个网站由 Sendmail 组织维护，第二个网站是 Sendmail, Inc. 的网站。

### qmail

这个 q 包声称是开源 `sendmail` 的现代替代品。根据我们从其他系统管理员那里听到的，它的设置非常简单，而且与邮件列表软件提供了良好的集成。你可以从以下 URL 下载该软件的 RPM 包版本：http://www.qmail.org/

> 如果你对在 `sendmail` 中使用邮件列表软件包感兴趣，你应该考虑 Majordomdo，它可以在 http://www.greatcircle.com/majordomo/ 找到。

## 总结

在本章中，你学习了如何使用 `sendmail` 系统将你的 SuSE Linux 服务器配置为 SMTP。`sendmail` 系统对于本地电子邮件可以“开箱即用”。稍微修改 `sendmail` 配置即可创建一个简单的、支持网络的 SMTP 电子邮件服务器。你还可以通过 IMAP 和/或 POP，允许如 Netscape Communicator 等邮件客户端从 SuSE Linux 服务器读取/写入/查看电子邮件。

# 第 11 章

## Web 服务

本章内容

- 启动 Apache Web 服务器
- 配置 Apache 以支持 CGI
- 配置 Apache 以支持服务器端包含
- 使用 Apache 支持虚拟 Web 服务
- 使用 Apache 使用 HTTP 身份验证
- 监控 Apache 服务器
- 使用 Apache 记录访问次数和错误
- 增强你的网站安全性
- 使用安全套接层（SSL）进行安全交易
