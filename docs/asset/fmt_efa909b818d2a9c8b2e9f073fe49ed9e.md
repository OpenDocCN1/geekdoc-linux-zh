
在这里我将向你展示如何通过 Telnet 模拟邮件客户端并向某人发送邮件消息。由于我已经在一个名为 `blackhole.nitec.com` 的 Red Hat Linux 服务器上运行了 SMTP 服务器，我只需运行 `telnet picaso.nitec.com 25` 即可连接到本地 SMTP 服务器。这是一个交互式的 SMTP 会话。

# 第 11 章：邮件服务

当我尝试连接名为 `picaso.nitec.com` 的 SMTP 服务器的 25 端口时，它显示了以下消息：

```
220 picaso.nitec.com SMTP Sendmail 8.9.3/8.9.3/Rb1-Orbs-Dul; Sun,
21 Feb 1999 10:08:00 -0800
```

这是来自 `picaso.nitec.com` 上 SMTP 服务器的欢迎消息。一旦发送了欢迎消息，服务器就会等待我的命令。我输入的第一个 SMTP 命令是：

```
helo nite.com
```

这生成了服务器的以下响应：

```
250 picaso.nitec.com Hello IDENTENT:kabir@picaso.nitec.com
[206.171.50.50], pleased to meet you
```

为了获取有关可用 SMTP 命令的帮助，我输入了：

```
help
```

服务器回复了帮助消息：

```
214-This is Sendmail version 8.9.3
214-Topics:
214- HELLO EHLO MAIL RCPT DATA
214- RSET NOOP QUIT HELP VFRFY
214- EXPN VERB ETRN DSN
214-For info use "HELP <topic>"
214-To report bugs in the implementation send email to
214- sendmail-bugs@sendmail.org.
214-For local information send email to Postmaster at your site.
214- End of HELP info
```

现在我可以使用这些命令来创建邮件消息。首先，我使用 `MAIL` 命令告诉服务器我的发件人地址，如下：

```
MAIL From: someone@out-there.com
```

服务器回复了以下确认消息：

```
250 someone@out-there.com... Sender ok
```

然后我使用 `RCPT` 命令提供了收件人的邮件地址：

```
RCPT To: kabir@nitec.com
```

服务器再次回复了以下确认消息：

```
250 kabir@nitec.com... Recipient ok
```

一旦我向服务器给了发件人和收件人的邮件地址，就是时候输入邮件消息的内容了。我如下使用了 `DATA` 命令：

服务器回复了以下内容：

```
354 Enter mail
```

我输入了以下邮件：

```
Date: 21 Feb 1999 10:08:00 -0800
From: someone@out-there.com
To: kabir@nitec.com
Subject: Ping
```

我用一个点结束了消息：

```
.
```

服务器回复了：

```
250 OK: queued as 123
```

最后，我输入了 `quit` 命令完成事务：

```
quit
```

服务器回复了以下：

```
221 picaso.nitec.com closing connection
```

# 第四部分：设置内网/互联网服务

如你所见，一旦运行了 SMTP 服务器，整个过程就非常简单。在你的 Red Hat Linux 服务器上运行自己的 SMTP 服务器之前，你需要为电子邮件创建适当的 DNS 配置。方法如下。

## 设置 DNS 邮件服务

你可能在上一章（DNS 服务）中记得邮件交换（MX）记录用于标识域名 DNS 配置中的邮件服务器资源。假设你想将主机 `mail.yourdomain.com` 指定为域名 `yourdomain.com` 的 SMTP 服务器。`yourdomain.com` 的起始授权记录（SOA）记录必须包含如下行：

- MX preference-value mail-server-hostname

在这里，`preference-value` 是一个正整数，仅在你有多个 SMTP 服务器时才有用用。如果你只有一个 SMTP 服务器，它可以是任何数字。例如：

- MX 5 mail.yourdomain.com

- MX 10 fast-mail-server.ad-engine.com

- MX 20 slow-mail-server.ad-engine.com

在这里，优先级数字起着至关重要的作用。当互联网上的任何 SMTP 服务器想要向 `someone@ad-engine.com` 发送邮件时，它首先会对 `ad-engine.com` 的 MX 记录进行 DNS 查询。返回给 SMTP 服务器的 MX 记录将所示。SMTP 服务器将选择 `fast-mail-server.ad-engine.com` 作为交付的首选邮件服务器，因为它在两个可用服务器中优先级更高（即优先级数字较小）。然后它将尝试与 `fast-mail-server.ad-engine.com` 建立 SMTP 连接（使用端口 25）。如果 `mailserver.ad-engine.com` 服务器由于任何原因不可用，则将选择 `slowmailserver.ad-engine.com` 服务器进行交付。

## 第 11 章：邮件服务 289

在 MX 记录中，始终使用具有对应 A 记录的主机名。换句话说，不要在 MX 记录中使用主机别名。详情请参阅 RFC 1123。

![](img/cbfef09f620ba4100baa62876f6f02b1_318_0.png)

一旦你设置了带有适当 MX 记录的 DNS，就可以通过 `nslookup -qmx yourdomain` 命令测试配置。如果你正确配置了 DNS，你应该能看到刚刚创建的 MX 记录。这项工作已经完成，你准备好设置 SMTP 邮件服务了。

## 设置 SMTP 邮件服务

设置 SMTP 服务的第一步是决定你想为你的 Red Linux 系统使用哪种 SMTP 邮件服务器。目前有很多 SMTP 邮件服务器产品可用。然而，`sendmail` 因其在全球范围内部署的历史悠而脱颖而出。它也是 Red Hat Linux 的默认 SMTP 邮件服务器。因此，在本章中我将使用 `sendmail` 作为 SMTP 服务器。查看如何在你的系统上安装 `sendmail`。

## 安装 sendmail

与你在 Red Hat 系统上安装的任何服务器软件一样，`sendmail` 也以 RPM 包的形式提供。然而，你需要安装多个 RPM 包；它们是：

- `sendmail-<version>.<architecture>.rpm` – 主分发包

- `sendmail-cf-<version>.<architecture>.rpm` – 邮件发送配置文件包

- `sendmail-config-<version>.<architecture>.rpm` – 辅助配置文件包

- `sendmail-doc-<version>.<architecture>.rpm` – 文档包

安装这些包非常简单；只需运行 `rpm -ivh package name` 来安装每个包即可。

## 第四部分：设置局域网/互联网服务

> 如果你在安装 Red Hat Linux 期间安装了旧版本的 `sendmail`，那么你应该在安装新版本之前删除 `sendmail` 包，因为它们可能并不完全兼容。要卸载 RPM 包，请使用 `rpm -e package name` 命令。你也可以使用 `rpm -q partial package name` 命令找到 RPM 包的确切包名。

一旦安装了这些包，你就可以配置 `sendmail` 了。`sendmail` 的主配置文件是 `/etc/sendmail.cf`。

## 启动和停止 sendmail

尽管你还没有配置 `sendmail` 服务器，但仍然可以运行它。要手动启动 `sendmail`，你可以运行以下命令：

```bash
/usr/sbin/sendmail -qprocessing interval>
```

通常，你需要将 `processing interval` 替换为时间。时间以分钟或小时为单位。例如，若要让 `sendmail` 每 15 分钟处理一次邮件，可以使用 `-q15m`；或者每小时处理一次查询，可以使用 `-q1h`。你也可以指定秒 (`s`)、`天` (`d`) 或周 (`w`)。例如，你可以指定 `-q1h30m`，让 `sendmail` 每一个小时半处理一次查询。
