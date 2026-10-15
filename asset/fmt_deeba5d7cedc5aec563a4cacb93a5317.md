
```
clear_report_template
report_YES_NO, score_=SCORE_, required=_REQD_, summary=
report_SUMMARY_
```

- 4. 配置 SpamAssassin 后守护进程自动运行，并更改 OPTIONS 行以防尝试为用户创建偏好。更改 `/etc/default/spamassassin` 文件中的以下选项：

```bash
ENABLED=1
OPTIONS="--max-children 5"
```

- 5. 启动 SpamAssassin 守护进程：

```
$ sudo invoke-rc.cd spamassassin start
```

- 6. 创建包含在 Exim ACL（访问控制列表）中用于扫描消息数据的条目。使用文本编辑器创建一个名为 `/etc/etc/exim4/acl_check_data_local` 的文件，包含以下内容：

```
deny message = $malware_name detected in message
demime = *
malware = *
```

```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${if <$message_size>(80k){1}{0}}
body:true/defer_ok
```

```
warn message = X-Spam-Status: $spam_report
condition = ${if <$message_size>(80k){1}{0}}
body:true/defer_ok
```

```
deny message = Spam score too high ($spam_score)
condition = ${if <$message_size>(80k){1}{0}}
body:true/defer_ok
```

- 7. 启动 SpamAssassin 守护进程：（此处存在上下文错误，已合并）

- 8. 告诉 Exim 加载最新的配置更改：

```
$ sudo invoke-rc.4 reload
```

现在通过你的服务器传输的所有消息都应该使用 ClamAV 进行病毒检查。此外，小于 80KB 的消息将由 SpamAssassin 检查。这是再次测试配置的好时机。你可能遇到的问题解决方法可以在下一节中找到。

# 测试与故障排除

本节包含一些通用故障排除技巧，以及关于常见错误及其修复方法的特定信息。

# 检查日志

Exim 的所有日志信息都写入三个文件，位于 `/var/log/exim4/mainlog`, `rejectlog`, `paniclog`。第一个文件 `mainlog` 包含所有事件的日志。第二个 `rejectlog` 包含被拒绝的消息。第三个 `paniclog` 包含配置或其他错误，通常在发生严重问题时出现。这些文件中的每个条目通常以时间戳开头。

`mainlog` 中的条目通常会包含一个 15 个字符的字符串，例如 `1E9PTu-003JN-Q`。这是记录该日志记录的消息标识符。标识符后面紧跟着双字符字符串。表 14-1 详细说明了这些字符串的含义。

### Exim 日志消息

| 符号 | 描述 | 解释 |

| --- | --- | --- |

| <= | 消息到达 | 这些条目显示消息进入 Exim，通常通过 SMTP 或本地 IPC。 |

| => | 消息投递 | 这些条目显示消息投递，无论是投递到本地邮箱还是通过 SMTP 或其他传输到远程主机。 |

| -> | 消息投递的额外地址 | 这些条目显示对于已投递给其他接收者的消息（由 `=>` 条目记录）的额外地址。 |

| ** | 投递失败 | 这些条目显示投递错误。此类错误表示消息已从邮件队列中删除，在大多数情况下已生成并发送了 DSN（传递状态通知）。 |

| -- | 投递延迟 | 这些条目显示临时投递问题。系统将继续尝试发送这些消息，直到投递成功，或由于重试超时导致永久性失败。 |

与未被接受队列的消息相关的条目将没有消息标识符或双字符标志。本节包含了此类类型条目的某些示例。

Courier IMAP 和 POP 守护进程的日志信息被写入到 `/var/log/mail.log`。正常条目包括 `LOGIN` 和 `LOGOUT` 消息。`DISCONNECTED` 消息通常表示在执行正常退出之前连接已中断。

`tail` 工具对于监控日志中的新条目非常有用。使用 `-f` 选项可以指示 `tail` 监控新条目并显示在屏幕上。

## 常见错误（以及修复方法）

你会遇到两类问题：Exim 拒绝消息，或者在连接时出现失败。

## 被 Exim 拒绝的消息

Exim 拒绝消息时，通常需要检查日志文件。以下是常见的错误以及修复方法：

- 拒绝转发（Relaying Denied）——以下错误表示 Exim 不允许该客户端转发邮件，除非它是信任的 relay 用户。例如：

```
if (condVar > someVal) {console.log("xxx")}
messages are rejected by Exim
```

如果客户端 IP 地址发生变化，或者它不在信任的 relay 范围内，你可能会看到类似下面的错误：

```bash
tail -f /var/log/mail.log
```

如果客户端 IP 地址经常变化，或者它不在信任的 relay 范围内，你可以通过 `/var/log/mail.log` 看到以下错误：

```bash
tail -f /var/log/mail.log
```

当 Exim 拒绝消息时，首先要检查的地方是日志文件 `/var/log/exim4/main.log`。

## ClAV 失败

这些错误表示 ClAV 守护进程未以 Exim 连接：

- ClAV 配置错误（ClAVMisconfiguration）——以下错误表示 ClAV 守护进程无法读取文件：

```
/var/log/exim4/----------------------------------------------------------------------
Exim 拒绝
```

请确保你已将用户添加到 `clamav` 组并重启了 ClAV。

- ClAV 不可用（ClAV Unavailable）——这通常表示 ClAV 守护进程未运行：

```
connect to UNIX socket /var/run/clamav/clamd.ctl (No such file or directory)
```

使用 `invoke-rc.d clam-daemon start` 启动。你也可以使用以下命令测试 clamAV：

```bash
$ sudo clamscan /usr/share/clamav-testfiles/clam.exe
```

## 无法投递的消息

在某些情况下，消息会被服务器接收但无法投递。这些错误中的某些是暂时的，在计时器之前不会产生退回邮件。你最可能看到的错误看起来像这样：

```
user@example.org R=local_user T-maildrop pipe defer (0):
Child process of maildrop transport returned 75 (could mean temporary
error) from command: /usr/bin/maildrop
```

此错误表示 Exim 尝试将消息传递给 Maildrop，但 Maildrop 返回了错误。最可能的原因缺少 Maildrop 目录，或者 Maildrop 目录的所有者不正确。接下来的章节将介绍如何检测并修复这些问题。

## 连接 Courier 时登录失败

除了真实的密码错误（可以通过在邮件客户端中输入正确的密码来解决）之外，还有其他几种导致登录失败的情况。这些情况中的某些也会导致暂时的投递问题。正常的登录失败会导致如下日志条目：

```
courierpoplogin: LOGIN FAILED, ip=[:ffff:1.2.3.4]
```

在这种情况下，IP 1.2.3.4 输入了正确的用户名或密码。还有其他几种可能导致登录失败的错误。

如果你以前没有配置过 crontab 文件，设置它就像输入以下三条命令一样简单：

```
$ cat mycron
@reboot /usr/bin/fetchmail -daemon 300
<Ctrl+D>
$ crontab mycron
```

## 配置基于 Web 的邮件

如果你正在运行 IMAP 服务器，可以通过安装 SquirrelMail（http://squirrelmail.org/）来提供基于 Web 的访问，该软件也可以在 squirrelmail 软件包中找到。首先将你的系统配置为 LAMP 服务器（参见第 13 节），然后安装并配置相应的软件包。

## 使用 SSL/TLS 保护通信

由于邮件客户端与服务器之间的通信通常包含密码等敏感信息，因此启用 SSL/TLS 加密是非常理想的。以下是在 Exim 和 Courier 中启用 SSL/TLS 的方法：

- 1. 安装带有 SSL/TLS 支持的 Courier 守护进程：

```bash
$ sudo apt-get install courier-imap-ssl courier-pop-ssl
```

- 2. 第三方 CA 证书在 ca-certificates 软件包中提供。配置将引用这些证书，因此请安装它：

```bash
$ sudo apt-get install ca-certificates
```

Defconf 会询问你是否默认信任这些 CA 证书。在大多数情况下，你应该选择 Yes。

- 3. 如果你将使用来自尚未被识别的 CA 的证书（如果你运行自己的 CA，通常如此），请将 CA 公钥证书放在你的文件 `/etc/ssl/certs/` 中并更新证书数据库：

```bash
$ sudo update-ca-certificates
```

- 4. 按照第 13 节所述生成私钥和证书签名请求（CSR）。你的文件的最佳位置是 `/etc/ssl/private/`。这里是一个示例：

```bash
$ sudo su
# cd /etc/exim4
# openssl genrsa -out mail.key 1024
# chmod 640 mail.key
# openssl req -new -key mail.key -out mail.csr
# chown root:Debian-exim mail.key
```

## 设置 Linux 服务器

- 5. 获取你的 CSR（证书签名请求）的签名，并将证书放置在 `/etc/mail/private/mail.crt`。或者，使用自签名证书执行以下操作：

```bash
# /etc/exim4
# openssl req -new -x509 -nodes - -days 365 -key mail.key -out mail.crt
# chmod 640 mail.crt
# chown root:Debian-exim mail.crt
```

如果你的证书不是由它们识别的 CA 签名，某些服务器将拒绝向你的服务器发送消息。此外，确保证书上的通用名称（cn）属性与 DNS 中的服务器名称匹配。

- 6. 将你的密钥和证书合并为一个文件供 Courier 使用：

```bash
# /etc/courier
# cat /etc/exim4/mail.key /etc/exim4/mail.crt > mail.pem
# chmod 600 mail.pem
```

- 7. 通过启用 `/etc/courier/imapd-ssl` 和 `/etc/courier/pop3d-ssl` 中的 TLS，在 Courier IMAP 和 POP 守护进程中启用 SSL/TLS，并将 `TLS_CERTFILE` 和 `TLS_TRUSTCERT` 的值替换为以下内容：

```
TLS_CERTFILE=/etc/courier/mail.pem
TLS_TRUSTCERT=/etc/ssl/certs/ca-certificates.pem
```

- 8. 告诉 Exim 在哪里找到证书并启用 TLS。创建一个名为 `/etc/exim4/conf.d/main/12_exim4-config_local_tlsoptions` 的文件，包含以下内容：

```
MAIN_TLS_CERTIFICATE = CONFDIR/mail.crt
MAIN_TLS_PRIVATEKEY = CONFDIR/mail.key
MAIN_TLS_ENABLE = 1
```

- 9. 重启 Exim：

```bash
$ sudo invoke-rc exim4 restart
```

你的服务器现在与 SMTP、POP 和 IMAP 客户端通信时应该支持 SSL/TLS。

## 总结

使用 Linux 和良好的互联网连接，你可以建立并维护自己的邮件服务器。准备你的计算机成为邮件服务器包括配置网络连接、设置投递和检索方法以及添加所需的软件包。

本章描述了如何安装、配置和排排除 Exim MTA。Exim 可以与垃圾邮件过滤软件（如 SpamAssassin）和病毒扫描软件（如 ClamAV）配合使用。保护邮件服务器的方法包括配置对 SSL/TLS 加密的支持。

## 第 15 章

## 运行打印服务器

共享打印机是节省资金和提高打印效率的好方法。很少有人需要一直打印，但当他们想要打印某些东西时，通常需要快速获得。设置打印服务器可以通过消除工作站对打印机的需求来节省费用。节省的资金可以用于购买每分钟打印页更多或输出质量更高的打印机。

你可以将打印机连接到你的 Linux 系统，供该系统的用户使用（独立打印机），或作为共享打印机供网络上的其他计算机使用。你还可以将 Linux 打印机配置为远程 CUPS 或 Samba 打印机。通过 Samba，你可以模拟 Windows 打印服务，考虑到大量的 Windows 客户端这非常有用。本章描述了在使用各种桌面环境的 Linux 系统上配置和使用打印机。某些细节在不同发行版之间可能有所不同，但这里包含的信息对于更常用的发行版非常有效。本章重点介绍了 Linux 上的通用打印系统 CUPS，它是大多数发行版的打印服务。一旦配置了本地打印机，可以使用 GNOME 等桌面环境中的配置选项。

# 本章内容

- 理解 Linux 上的打印

- 设置打印机

- 使用打印命令

- 管理打印

- 共享打印机

## 通用打印系统

CUPS 是 Linux 和类 Unix 操作系统的打印标准。它的设计是为了满足当今对标准化打印定义和共享的需求。几乎每个 Linux 发行版都带有 CUPS 作为其打印服务。以下是一些功能：

- IPP：CUPS 基于 打印协议（www.pwg.org/ipp/），这是一种为了简化打印机共享而创建的标准。在 IPP 模型中，打印服务器和想要打印的客户端可以使用 HTTP 交换有关打印机的型号和功能的信息。服务器还可以广播打印机的可用性。

- 驱动程序：CUPS 还标准化了驱动程序的创建。想法是创建一个可以适用于所有类型 Unix 系统的通用格式。这样，制造商只需为 Linux 创建驱动程序。

- 打印机类：你可以使用打印机类创建多个指向同一打印机的服务器条目，或者指向多个打印机的单个服务器条目。在前的情况下，每个条目可以使用不同的选项（例如指向特定的纸盒或使用特定的字体大小或页边距打印）。在后的情况下，你可以拥有打印机池来分配任务，从而减少由于打印机故障或处理大文档导致的队列拥塞。CUPS 还支持隐式类，这是通过自动识别网络打印机形成的打印机类。

- 打印机浏览：通过打印机浏览，客户端可以看到局域网内开启浏览功能的 CUPS 打印机。结果是客户端可以从局域网广播的打印机名称中选择想要使用的打印机，而无需预先知道它们的名称和位置。如果你不想让其他人看到你的打印机，可以关闭此功能。

- Unix 打印命令：为了集成到 Linux 和其他 Unix 环境中，CUPS 提供了 Unix 系统提供的打印和管理打印的标准命令版本。

许多发行版提供了配置 CUPS 打印机的简化方法。这里是一些示例：

- 在 Fedora、CentOS 和 Red Hat Enterprise Linux 系统中，打印配置（`system-config-printer` 命令）允许你配置使用该设施的打印机。

# 运行打印机服务器

- 在 Ubuntu 中，相同的打印机配置窗口（选择系统 ⟒ 管理 ⟒ 打印来打开）允许您添加、删除和管理打印机。

- 在 SUSE 中，YaST 工具包含一个打印机配置模块。从 YaST 控制中心，选择硬件 ⟒ 打印机。

对于没有自带打印机配置工具的发行版，有几种方法可以使用并非特定于 Linux 发行版的工具来配置 CUPS。以下是其中方法：

- 从浏览器配置 CUPS —— CUPS 提供了一个基于 Web 的界面用于访问和管理打印机。您可以在运行 CUPS 服务的计算机上，通过 Web 浏览器定位到 `localhost:631` 来访问此服务。（参见本章节后的“基于 Web 的 CUPS 管理”章节）。KDE 桌面带有一个用于管理 CUPS 服务器功能的工具。在终端中运行 `/usr/bin/cupsconf` 即可启动 CUPS 服务器配置窗口。

- 手动配置 CUPS —— 您也可以通过编辑配置文件并手动启动 cups 守护进程来手动配置 CUPS。CUPS 的配置文件包含在 `/etc/cups` 目录中。特别是，您可能对 `cupsd.conf` 文件感兴趣，它标识了打印机守护进程的权限、认证和其他信息；以及 `printers.conf`，它标识了已配置打印机的地址和选项。使用 `classes.conf` 文件定义本地类。
