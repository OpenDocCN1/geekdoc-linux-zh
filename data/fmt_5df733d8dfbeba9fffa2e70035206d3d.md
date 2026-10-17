
Connected to localhost.localdomain (127.0.0.1).

Escape character is '^'.

220 mail.example.com ESMTP Postfix

```
此时，你已经连接上了。你现在可以与服务器进行对话了。下面展示了此类对话的示例。**粗体行**是你输入的内容，正字体行是 Postfix 回给你的内容。（不要忘记：将 mail.example.com 替换为你的用户名和电子邮件地址）。
```

```
telnet 127.0.0.1 25

Trying 127.0.0.1...

Connected to localhost.localdomain (127.0.0.1).

Escape character is '^'.

220 mail.example.com ESMTP Postfix

helo me

250 mail.example.com

mail from: user@example.com

250 Ok

rcpt to: user@example.com

250 Ok

data

354 End data with <CR><LF><CR><LF>

This is a test of the Postfix mail server.

250 Ok: queued as 67DB75F7
```

## 388 PC Magazine — Linux Solutions

```
quit

221 8bye

Connection closed by foreign host.
```

此时，你应该已经收到一封包含句子“This is a test of the Postfix server.”的邮件了。在（非超级用户）提示符下，输入 `mail` 命令，你应该就能看到它。在此时你还没有配置 POP 或 IMAP 服务器，可以使用普通的电子邮件程序。通过输入 `q` 退出邮件程序。

关于发出的邮件，最简单的方法是向远程地址发送邮件。如果你有一个电子邮件地址，例如 Google Mail、Yahoo! Mail或其他类型的账户，或者一个与你用于此服务器的网络不同的家庭或业务账户，请向它发送一条消息。例如，如果你有地址 user@gmail.com，使用文本编辑器创建此文件：

```
From: user@example.com

To: user@gmail.com
```

This is a test of outgoing mail.

保存文件并将其命名为 `mailtest.txt`。现在输入命令

```
cat mailtest.txt | mail@gmail.com
```

当你检查 Google Mail 账户时，你应该能看到这条消息。（注意，消息可能需要一些时间才会显示。）

如果你可以使用 Postfix 发收邮件（或者如果你的 ISP 限制了发送邮件，则仅测试发送），则说明 Postfix 配置完成，你现在可以继续设置你的 POP/IMAP 服务器了。

# Dovecot 邮件投递代理

有很多邮件投递代理 (`MDA`)，它们的作用大同小异：它们允许邮件客户端连接到服务器并下载邮件。它们中的任何一个设置和运行都不算困难，因此选择哪一个完全取决于你。本章重点介绍 Dovecot 服务器，因为它相对简单且直观。

## 注意事项

如果你在运行 MTA 的那台机器上读取邮件，则不需要使用 MDA。MTA 会将入站邮件放入邮件箱目录，大多数 Linux 客户端可以直接从这些目录中读取。然而，如果你想从另一台机器读取邮件，你绝对需要一个 MDA。既然它们反正很容易设置，你不妨这样做。这样一来，当你的邮件服务器超出实验范围时，你就做好了准备。

# 第 22 章：邮件服务器解决方案

## 第 1 步：安装 Dovecot

Dovecot 包含在 Fedora Core 发发行中；因此，在执行任何其他操作之前，检查它是否已经安装。运行命令

```
rpm -qiv dovecot
```

如果 Dovecot 已经安装，你应该看到这些：

| Name | dovecot | Relocations: (not relocatable) |
| :--- | :--- | :--- |
| Version | 0.99.11 | Vendor: Red Hat, Inc. |
| Release | 1.FC3.4 | Build Date: Thu 21 Oct 2004 12:34:42 |
| PM EDT | Install Date: Mon 09 May 2005 01:04:33 PM EDT | Build Host: |
| Group | System Environment/Daemons | Source RPM: dovecot-0.99-11- |
| 1.FC3.4.src.rpm | License: LGPL |
| Size | 1344685 |
| Signature | DSA/SHA1, Thu 21 Oct 2004 01:09:33 PM EDT, Key ID b44269d04f26fd2 |
| Packager | Red Hat, Inc. | <http://bugzilla.redhat.com/bugzilla> |
| URL | http://dovecot.procontrol.fi/ |
| Summary | Dovecot Secure imap server |

Dovecot 是一个为 Linux/UNIX 类系统设计的 IMAP 服务器，主要为了安全性而编写。它还包含一个小型 POP3 服务器。它支持 maildir 或 mbox 格式的邮件。

如果 Dovecot 未安装，你需要安装该软件包。你应该可以在你的安装 CD 中找到它，或者如果你倾向于下载它，你应该可以在下载 Postfix 的相同网站找到它。

如果你没有使用 Fedora Core，你可以在 `www.dovecot.org/download.html` 找到软件包链接。

### 第 2 步：配置 Dovecot

作为超级用户，用你喜欢的文本编辑器器打开 `/etc/dovecot.conf` 文件，如图 22-3 所示。

你只需要检查几个参数。向下滚动直到找到类似这样的部分：

```
# Protocols we want to be serving:
# imap imaps pop3 pop3
protocols = imap imaps pop3
```

## 390 PC Magazine — Linux Solutions

![](img/65ef2f6e9fc73ddc3051990377c4f5b_414_0.png)

```
/etc/dovecot.conf - edit

Dovecot 1.0 configuration file

# Default values are shown after each value, it's not required to uncomment
# any of the lines. Exception to these paths, they're just examples
# with defaults on configuration options.
# are for configure --prefix=/usr --sysconfdir=/etc --localstatedir=/
```

## 第 22 章：邮件服务器解决方案

## 注意事项

`/etc/dovecot.conf` 文件有更多参数。这些大部分是面向安全的；如果你打算运行一个人们可以连接到互联网的服务器，我强烈建议你花时间学习如何配置它，因为本章描述的配置将使你的服务器完全不安全。你可以在 http://wiki.dovecot.org 找到所有 Dovecot 参数的完整文档。

### 第 3 步：启动并测试服务器

与其他服务器一样，你需要在连接之前启动它。对于这一点，你可以使用 `system-config-services` 或直接输入命令

```
/etc/rc.d/init.d/dovecot start
```

如果没有问题，你现在应该连接到服务器并下载邮件。你可以通过 Telnet 程序测试 Dovecot 是否接受连接，就像你对 Postfix 服务器做的那样。首先，退出超级用户账户——你需要以普通用户的身份执行此操作。其次，输入以下命令：

```
telnet 127.0.0.1 110
```

你应该得到以下响应：

```
Trying 127.0.0.1...

Connected to localhost.localdomain (127.0.0.1).

Escape character is '^'.

+OK dovecot ready.
```
