
Connected to localhost (127.0.0.1).

(vsFTPD 1.1.3)

(localhost:naba): anonymous

331 Please specify the password.

Password: <-- 我可以任何内容作为密码

230 Login successful. Have fun.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> -1

227 Entering Passive Mode (127,0,0.1,169,190)

150 Here comes the directory listing.

drwx-xr-x 2 0 4096 Jun 06 04:36 pub

226 Directory send OK.

ftp> bye

221 Goodbye.

```
当你成功登录匿名 FTP 时，你访问的是名为 `ftp` 的用户的主目录 (`/var/ftp`)。将公开访问的文件——你希望让其他人从你的系统下载的文件放在 `/var/ftp/pub` 目录下。之后，你必须向世界宣布（可能通过在 comp.os.announce 中发帖）你那里有一个新程序可用。

# 设置安全匿名 FTP

## 匿名 FTP 的主要特性

匿名 FTP 设置的关键特性如下：

- 有一个名为 `ftp` 的用户，其主目录为 `/var/ftp`。该用户没有分配 shell。当你在 `/etc/passwd` 文件中搜索 "ftp" 时，你会得到以下内容：
```bash
grep ftp /etc/passwd
```
输出应该类似于此：
```
ftp:x:14:50:User:/var/ftp:/sbin/nologin own
```
（注意：原文此处有拼写错误 \ftp，已修正为 /ftp）

- 以下是 `/var/ftp` 目录的完整权限设置和所有者信息：
```
dwxr-xr-x 3 root root 4096 Jun 22 12:10 ftp
```

- 正如此行代码所示：

- 你可以使用 `ls -la` 命令查看 `/var/ftp` 目录的内容。结果如下：
```
total 12
dr-xr-x 3 root root 4096 Jun 22 12:10 *
dr-xr-x 21 root root 4096 Jun 22 12:10 ..
dr-xr-x 2 root root 4096 Jun 6 00:36 pub
```

- `pub` 目录用于存放任何你想让他人通过匿名 FTP 从你的系统中下载的文件。

## 第 4 章：提供邮件和新闻服务

**本章内容**

- 安装和使用 sendmail
- 手动测试邮件投递
- 配置 sendmail
- 安装 InternetNews (INN) 服务端
- 配置并启动 INN
- 设置本地新闻组

电子邮件（e-mail）是 Internet 主机上的可用服务之一。电子邮件软件由两部分组成：邮件传输代理 (MTA)，它在物理上发送和接收邮件消息；以及邮件用户代理 (MUA)，它负责读取消息并准备新消息。在本章中，我将描述该电子邮件服务，并展示如何在 Red Hat Linux PC 上配置 sendmail 服务器。

除了电子邮件之外，Internet 新闻组提供了讨论各种话题和与他人分享知识的另一种方便方式。Red Hat Linux 自带了读取新闻组以及将系统配置为新闻服务器所需的软件。在本章中，我将描述如何配置和运行流行的新闻服务器 InternetNews 服务器。我还将展示如何为你的企业局域网（甚至是你的家庭网络）设置本地新闻组。

## 安装邮件服务器

如果你在 Red Hat Linux 安装期间安装了邮件服务器软件，就不需要做更多操作即可开始使用邮件服务。要检查邮件服务器是否已安装，输入以下命令：
```bash
rpm -q sendmail
```
如果响应如下所示，说明你已经准备就绪：
```
sendmail-8.12.9-7
```
此输出表示系统上安装了版本为 8.12.9 的 sendmail。

如果输出提示未安装 sendmail，可以使用 Red Hat 软件包管理器 (RPM) 安装运行和配置 sendmail 所需的各个包。要安装 sendmail 的 RPM 文件，请以 root 身份登录并在 CD-ROM 驱动器中插入第二张光。如果你使用 GNOME 或 KDE，CD-ROM 会自动挂载。否则，请输入以下命令挂载 CD-ROM：
```bash
mount /mnt/cdrom
```
然后输入以下命令安装 sendmail 文件：
```bash
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh sendmail*
```
这应该安装两个包：

- `sendmail` — 一个复杂的邮件传输代理 (MTA)
- `sendmail-cf` — sendmail 的配置文件

## 使用 sendmail

要将你的系统配置为邮件服务器，你必须正确配置 sendmail 传输代理。sendmail 以复杂但强大的邮件投递系统而闻名。光看 sendmail 的配置文件 `/etc/mail/sendmail.cf` 就应该让你确信 sendmail 确实很复杂。幸运的是，你不需要成为 sendmail 配置文件的专家。你只需要预定义的配置文件之一——即安装在你的系统上的那一个——即可使用 sendmail。

你的系统应该有一个可以工作的 sendmail 配置文件——`/etc/mail/sendmail.cf`。默认文件假设你拥有 Internet 连接和名称服务器。只要你有 Internet 连接，就应该能够从你的 Red Hat Linux PC 发送和电子邮件。

为了确保邮件投递正常工作，你的系统名称必须与 ISP 分配给你的系统名称匹配。尽管你可以给系统起任何名称，但只有当系统名称在 ISP 服务器上时，其他系统才能成功地向你的系统投递邮件。

## 邮件投递测试

要尝试 sendmail 邮件传输代理，你可以使用 `mail` 命令编写并向另一个地址给自己发送邮件消息。例如，以下是我如何使用 `mail` 命令给自己发送消息的：
```text
mail naba@comcast.net
Subject: Testing e-mail
This is from Red Hat Linux system.
Cc: Press Ctrl+D.
```
`mail` 命令是一个简单的邮件用户代理。在前面的示例中，我在命令行中指定了地址——`naba@comcast.net`。mail 程序提示输入主题（Subject）。在主题之后，我输入了消息，并以仅包含一个句点的行结束。在提示 Cc 时，我按了 Ctrl+D。在消息结束后，邮件用户代理将消息传递给 sendmail——投递到指定地址的邮件传输代理。由于我的系统已经连接到 Internet，sendmail 会立即投递邮件。

为了验证邮件投递，我检查了来自 ISP 的邮件，发现邮件已经到达。只要我的系统拥有官方 DNS 主机名并在 ISP 的 数据库中，我也可以发送回复。因此，只要你的 Red Hat 系统拥有 Internet 连接和注册域名，Red Hat Linux 自带的 sendmail 配置文件就足够收发电子邮件了。

## 邮件投递机制

在 Internet 主机上，sendmail 邮件传输代理使用简单邮件传输协议 (SMTP) 递递。基于 SMTP 的邮件传输代理监听 TCP 端口 25。
```text
telnet localhost
220 2.0.0 localhost.localdomain
HELO localhost
250 2.0.0 Hello you
MAIL FROM: naba@localhost
250 2.1.0 Sender ok
RCPT TO: naba@comcast.net
250 2.1.5 Recipient ok
DATA
354 Enter mail, end with "*"
This is from Red Hat Linux system.
.
250 2.0.0 Message accepted for delivery
QUIT
221 2.0.0 localhost.localdomain closing connection
```

## 安装邮件服务器 645
```
mail
Mail version 8.1 6/6/93. Type ? for help.
/var/spool/mail/naba*: 1 message 1 new
>N1 naba@localhost.local Tue Jul 15 19:25 12/479
& 1
Message:
From naba@localhost.localdomain Tue Jul 15 19:25:20 2003
Date: Tue, 15 Jul 2003 19:22:24 -0400
```
