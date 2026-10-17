
在默认的 Fedora/RHEL 配置中，`sendmail` MTA 使用 `procmail` 作为本地 MDA。反过来，`procmail` 将电子邮件写入收件人邮箱文件的末尾。你还可以使用 `procmail` 根据一组规则对电子邮件进行排序，无论是按用户还是全局。全局过滤功能对于系统范围内的垃圾邮件检测和其他任务很有用，但在现代系统中，按用户过滤的功能在很大程度上是多余的。传统的 UNIX MUA 是简单的程序，无法过滤邮件，因此将此功能委托给 `procmail` 等 MDA。相比之下，现代 MUA 集成了此功能。

### 你不需要设置 sendmail 来发送和接收电子邮件

大多数 MUA 可以使用 POP 或 IMAP 接收电子邮件。这些协议不需要 `sendmail` 等 MTA。因此，你不需要安装或配置 `sendmail`（或其他 MTA）来接收电子邮件。你仍然需要 SMTP 来发送电子邮件。但是，SMTP 服务器可以位于远程位置，例如你的 ISP，因此你不需要担心它。

### 引言

当最终演变成互联网的网络最初建立时，它连接了几台计算机，每台计算机为大量用户服务并运行多项服务。每台计算机都具备发送和接收电子邮件的能力，并拥有唯一的域名，用作电子邮件的目标。

如今，互联网上有大量的瞬态客户端。由于这些客户端没有固定的 IP 地址或域名，因此无法直接接收电子邮件。这些系统上的用户通常在他们雇主或 ISP 运行的电子邮件服务器上维护一个帐户，并使用 POP 或 IMAP 从该帐户收集电子邮件。除非你拥有一个想要接收电子邮件的域名，否则你不需要将 `sendmail` 设置为传入的 SMTP 服务器。

你可以在客户端系统上设置 `sendmail`，使其简单地将来站邮件中继到 SMTP 服务器。这种配置是那些使用防火墙防止从除公司官方邮件服务器以外的任何系统向互联网发送电子邮件的组织所必需的。作为防止病毒传播的部分防御措施，一些 ISP 阻止出站端口 25，以防止其客户直接向远程计算机发送电子邮件。这些 ISP 需要这种配置。

你还可以将 `sendmail` 设置为不使用 ISP 作为中继的出站服务器。在这种配置中，`sendmail` 直接连接到接收电子邮件的域名的 SMTP 服务器。设置为中继的 ISP 就是这种配置。

你可以设置 `sendmail` 以接受注册域名指定的电子邮件，如域名 DNS MX 记录中指定的（第 780 页）。但是，大多数邮件客户端（MUA）不直接与 `sendmail` 交互以接收电子邮件。相反，它们使用 POP 或 IMAP——这些协议包含管理邮件文件夹、将消息保留在服务器上以及仅读取电子邮件主题而不下载整个消息的功能。如果你想从除运行传入邮件服务器以外的系统收集电子邮件，你可能需要设置 POP 或 IMAP 服务器，如第 689 页所述。

### 前提条件

安装以下软件包：

- `sendmail`（必需）
- `sendmail-cf`（配置 `sendmail` 时必需）
- `squirrelmail`（可选；提供 Webmail，见第 686 页）
- `spamassassin`（可选；提供垃圾邮件过滤功能，见第 682 页）
- `mailman`（可选；提供邮件列表支持，见第 688 页）
- `dovecot`（可选；提供 IMAP 和 POP 入站邮件服务器守护进程）

运行 `chkconfig` 以便在系统进入多用户模式时启动 `sendmail`（默认情况下，`sendmail` 不会在单用户模式下运行）：

```bash
# /sbin/chkconfig sendmail on
```

启动 `sendmail`。由于 `sendmail` 通常正在运行，您需要重启它以使 `sendmail` 重新读取其配置文件。即使 `sendmail` 未运行，以下重启命令也能正常工作——它只是无法关闭 `sendmail`：

```bash
# /sbin/service sendmail restart
Shutting down sm-Client: [ OK ]
Shutting down sendmail: [ OK ]
Starting sendmail: [ OK ]
Starting sm-Client: [ OK ]
```

运行 `chkconfig` 以便在系统进入多用户模式时启动 SpamAssassin 守护进程 `spamd`（在此配置中通常会安装 SpamAssassin）：

```bash
# /sbin/chkconfig spamassassin on
```

与 `sendmail` 类似，SpamAssassin 通常也在运行。重启它以便 `spamd` 重新读取其配置文件：

```bash
# /sbin/service spamassassin restart
Stopping spamd: [ OK ]
Starting spamd: [ OK ]
```

IMAP 和 POP 协议由多个守护进程实现。有关这些守护进程及其启动方法的信息，请参见第 689 页。

## 注意事项

- **防火墙**

  SMTP 服务器通常使用 TCP 端口 25。如果运行 SMTP 服务器的系统启用了防火墙，您需要打开此端口。使用防火墙配置窗口中的“信任服务”选项卡（见第 824 页），勾选标有 `Mail (SMTP)` 的复选框以打开此端口。有关更通用的信息，请参见详细介绍 `iptables` 的第 25 章。

- **cyrus**

  本章涵盖 `dovecot` 软件包中包含的 IMAP 和 POP3 服务器。Fedora/RHEL 还在 `cyrus-imapd` 软件包中提供了 IMAP 和 POP3 服务器。

## 更多信息

- `sendmail`: www.sendmail.org
- IMAP: www.imap.org
- IMAP 和 POP3: www.dovecot.org
- IMAP 和 POP3: cyrusimap.web.cmu.edu
- SquirrelMail: www.squirrelmail.org
- Postfix: www.postfix.org/docs.html（替代 MTA，见第 691 页）
- Qmail: qmail.area.com
- Mailman: www.list.org
- `procmal`: www.procmal.org
- SpamAssassin: spamassassin.org
- 垃圾邮件数据库: razor.sourceforge.net

## 快速上手 1：配置客户端上的 sendmail

**您可能不需要配置 sendmail 来发送电子邮件**

在 `sendmail` 正在运行的情况下，执行第 673 页“测试”部分中描述的命令。只要 `sendmail` 能够向外连接到端口 25，您就不需要按照本节所述设置 `sendmail` 使用 SMTP 中继。如果您收到了测试发送的邮件，可以跳过本节。

此快速上手配置了一个出站 `sendmail` 服务器。该服务器

- 使用远程 SMTP 服务器（通常是 ISP）将出站电子邮件中继到其目的地（SMTP 中继）。
- 仅向 SMTP 服务器发送源自本地系统的电子邮件。它不转发源自其他系统的电子邮件。
- 不处理入站电子邮件。正如常见的情况一样，您需要使用 POP 或 IMAP 来接收电子邮件。

要设置此服务器，您必须编辑 `/etc/mail/sendmail.mc` 并重启 `sendmail`。

`sendmail.mc` 中下一行开头的 `dnl` 表示该行是注释：

```
dnl define(`SMART_HOST', `smtp.your.provider')dnl
```

您可以忽略行尾的 `dnl`。要指定远程 SMTP 服务器，您必须在编辑器中打开 `sendmail.mc` 并修改上述行，删除行首的 `dnl`，并将 `smtp.your.provider` 替换为您 ISP 的 SMTP 服务器的 FQDN（请向您的 ISP 获取此名称）。请小心不要更改行中的反引号 (` ` `) 和单引号 (` ' `)。如果您的 ISP 的 SMTP 服务器位于 `smtp.myisp.com`，您将把该行更改为

```
define(`SMART_HOST', `smtp.myisp.com')
```

## 不要更改反引号 (`) 或单引号 (')

请小心不要更改 `sendmail.mc` 任何行中的反引号 (`) 或单引号 (')。这些符号控制 `m4` 预处理器如何将 `sendmail.mc` 转换为 `sendmail.cf`。如果您未保留这些符号，`sendmail` 将无法正常工作。

当您重启它时，`sendmail` 会由您编辑的 `sendmail.mc` 文件重新生成 `sendmail.cf` 文件：

```bash
# /sbin/service sendmail restart
```

使用以下命令测试 `sendmail`：
