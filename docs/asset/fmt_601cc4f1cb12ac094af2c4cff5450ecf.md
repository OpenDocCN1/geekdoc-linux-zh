
| FTP VII 第 3 章 | 设置 FTP 服务器 |

## 576 配置 FTP 服务器

- `ascii_upload_enable=YES` 启用 ASCII 模式下的文件上传（用于文本文件）。

- `async_abor_enable=YES` 使 `vsftpd` 识别随时到达的 `ABOR`（中止）请求。你可能需要启用它，以允许较旧的 FTP 客户端与 `vsftpd` 工作。

- `banned_email_file=/etc/vsftpd.banned_emails` 指定包含黑名单电子邮件地址列表的文件（仅在 `deny_email_enable` 设置为 `YES` 时使用）。

- `chown_uploads=YES` 使上传的匿名文件所有者变为由 `chown username` 指定的用户。除非绝对必要，否则不要启用此选项——并且不要将 `root` 指定为 `chown_username`（这将导致一场不可避免的灾难）。如果运行在特定用户名下的进程使用了上传的文件，你可能需要启用此选项，这意味着无论谁上传文件，所有者都必须更改为进程预期的用户名。

- `chown_username_name` 指定由匿名 FTP 用户上传文件的所有者用户名。

- `chroot_list_enable=YES` 使 `vsftpd` 在用户登录 FTP 服务时，将 `chroot_list_file` 列表之外的所有用户都限制在他们的主目录中。此选项防止这些用户访问其主目录以外的任何其他文件。

- `chroot_list_file=/etc/vsftpd.chroot_list` 是被限制在主目录或不受的用户列表，取决于 `chroot_local_user` 的设置。

- `connect_from_port_20=YES` 使 `vsftpd` 确保数据传输通过 20 端口（FTP 数据端口）进行。

- `data_connection_timeout=120` 是在数据连接空闲后超时的时间（秒）。

- `deny_email_enable=YES` 使 `vsftpd` 检查黑名单电子邮件列表，并拒绝任何尝试使用黑名单电子邮件作为密码进行匿名登录的人。

- `dismissage_enable=YES` 使 `vsftpd` 在 FTP 用户切换到某些目录时显示消息。

- `ftpd_banner=Welcome to my FTP service` 设置用户登录时 `vsftpd` 显示的横幅。你可以将消息更改为任何内容。

- `idle_session_timeout=600` 是空闲会话（指有人连接后未进行任何操作）超时并由 `vsftpd` 注销用户的时间（秒）。

- `listen=YES` 使 `vsftpd` 监听连接请求，从而在独立模式下运行。如果你想在 `xinetd` 下运行 `vsftpd`，请将此选项设置为 `NO`。

# 安装邮件服务器

在 Debian 中，输入 `apt-get install sendmail` 来安装 `sendmail` 服务器。在 Fedora Core 中，以 root 身份登录，挂载 DVD，然后输入 `cd /mnt/cdrom/Fedora/RPM` 运行 `rpm -ivh sendmail*`。在 SUSE 中，从 YaST 控制中心的软件目录中点击“安装和移除软件”。使用 YaST 的搜索功能找到 `sendmail` 包并安装它们。

![](img/fb03f7f944c69a481f34f490e877a2b9_607_0.png)

# 使用 sendmail

要将你的系统配置为邮件服务器，你必须正确配置 `sendmail` 邮件传输代理。`sendmail` 被誉为一个复杂但完善的邮件投递系统。只需看一眼 `sendmail` 的配置文件——Fedora Core 中的 `/etc/mail/sendmail.cf` 和 SUSE 中的 `/etc/sendmail.cf`——就能让你相信 `sendmail` 确实很复杂。幸运的是，你不需要成为 `sendmail` 配置文件的专家。你只需要使用预定义的配置文件之一——例如安装在系统上的那个——即可使用 `sendmail`。

你的系统已经有一个可以工作的 `sendmail` 配置文件——`/etc/sendmail.cf`。默认文件假设你已经有了互联网连接和名称服务器。只要你有互联网连接且你的系统拥有官方域名，你就可以从你的 Linux PC 发送接收电子邮件。

![](img/fb03f7f944c69a481f34f490e877a2b9_607_1.png)

为了确保邮件投递正确，你的系统名称必须与 ISP 分配给你的系统名称匹配。尽管你可以给系统命名任何主机名，但如果你的系统名称在 ISP 的名称服务器中，其他系统才能成功向你的系统投递邮件。

# 邮件传输测试

为了尝试 `sendmail` 邮件传输代理，你可以使用 `mail` 命令向 Linux 系统上的任何用户账户编写并发送邮件。例如，以下是我如何使用 `mail` 命令给自己发送消息的：

```
mail naba
Subject: Testing e-mail
This is from your Linux system.
```

`mail` 命令是一个简单的邮件用户代理。在前面的示例中，我在命令行中指定了收件者——`naba`。`mail` 程序提示输入主题。在主题之后，我输入消息并以一行只包含一个句点的行结束消息。消息消息后，邮件代理会将消息传递给 `sendmail`——即邮件传输代理——以投递到指定的地址。`sendmail` 会立即投递邮件。为了验证邮件是否投递，我输入 `mail` 来运行 `mail` 命令。

# 邮件服务器配置说明

因此，初始的配置配置文件对于发送和接收电子邮件是足够的，至少在你的 Linux 系统内部如此。只要你的 Linux 系统有互联网连接并注册了域名，外部邮件投递也可以正常工作。

如果你有一个为你的 Linux 系统提供动态 IP 地址的 ISP 账户，你必须使用像 Evolution 或 Mozilla Mail 这样的邮件客户端，通过它们连接你 ISP 的邮件服务器来投递出站邮件。

![](img/fb03f7f944c69a481f34f490e877a2b9_608_0.png)

# 邮件投递机制

在互联网上，`sendmail` 邮件传输代理使用简单邮件传输协议 (`SMTP`) 投递邮件。基于 `SMTP` 的邮件传输代理监听 TCP 25 端口，并使用一小组文本命令与其他邮件传输代理交换信息。事实上，`SMTP` 命令非常简单，你可以手动从终端使用它们来发送邮件。接下来的示例显示了我如何通过运行在同一系统上的 `telnet` 会话，使用 `SMTP` 命令向我在 Linux PC 上的账户发送邮件：

```
telnet localhost 127.0.0.1.
Trying 127.0.0.1.
Connected to localhost.
Escape character 'j'.
220 linux.site SMTP Sendmail 8.12.10/8.12.10/SuSE Linux 0.7; Sun, 26 Sep 2004 10:40:02 -0400
HELO localhost
250 linux.site Hello localhost [127.0.0.1], pleased to meet you
MAIL: FROM:naba
250 localhost... Domain name registered for sender address naba
RCPT: TO:naba
250 localhost... Recipient ok
DATA
354 Mail entry, end with "." on a line by itself
Testing... 1 2 3
Sending mail by telnet to port 25
250 localhost.localdomain Message accepted for delivery
QUIT
quit
```

`telnet` 命令打开到 25 端口的 TELNET 会话——这是 `sendmail` 接收 `SMTP` 命令的端口。Linux 系统上的 `sendmail` 进程立即回复公告。我输入 `HELP` 来查看 `SMTP` 命令列表。要获取特定命令的帮助，我可以输入 `HELP` 命令。列表显示了当我输入 `DATA` 时打印的帮助信息。

我输入 `HELP localhost` 与主机建立会话。`sendmail` 进程回复问候。要发送邮件，我从 `MAIL FROM:` 命令开始，指定消息的发送者。我输入正在发送消息的系统用户名。

接下来，我使用 `RCPT TO:` 命令指定消息的收件者。如果我想向多个收件者发送消息，只需通过 `RCPT TO:` 命令提供地址。

要输入消息，我使用 `DATA` 命令。在 `DATA` 命令响应后，`sendmail` 显示我需要以句点来结束消息。我输入消息并以单独的一行句点结束。消息结束后，`sendmail` 显示消息已接受投递。最后，我通过 `QUIT` 命令退出 `sendmail` 会话。
