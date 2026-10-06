
### 配置 DNS 以实现直接投递

为了使直接投递生效，SMTP 服务（TCP 端口 25）必须通过 DNS 中的一个固定名称被外部世界访问。该名称将采用 A（地址）记录的形式。A 记录允许 DNS 解析器进程根据特定名称确定 IP 地址，并被 Internet 上大多数常用协议使用。一个典型的 A 记录如下：

```
bigserver.example.org IN A 10.0.12.16
```

第一个参数 `bigserver.example.org.` 是标签（label），第二个参数是类（IN 代表 Internet，即大多数 DNS 记录所在之处）。A 表示类型，最后一个参数是与标签关联的 IP 地址。

在你拥有一个 A 记录后，可以使用 MX（邮件邮件交换者）记录将邮件指向你的服务器。A 记录和 MX 记录不需要属于同一个域名，这提供了更大的灵活性。以下是一个 MX 记录示例：

```
widgets.test. IN MX 0 bigserver.example.org.
```

此 MX 记录表示，任何 `any@widgets.test` 都应该通过服务器 `bigserver.example.org` 发送。0 表示此 MX 记录的数字优先级。当一个标签存在多个 MX 记录时，会先尝试优先级最低的。如果遇到临时错误，将尝试下一个优先级的邮件服务器，依此类推，直到列表耗尽。此时，发送服务器将定期重试，直到消息超时（通常为五天）。如果存在多个优先级相同的 MX 记录，将按随机顺序尝试。

**注意**

在没有 MX 记录的情况下，大多数邮件服务器也将回退到标签的 A 记录中列出的 IP 地址。然而，依赖此功能被认为是不良做法。

在某些情况下，由于你的 IP 地址经常变化，建立 A 记录可能会变得复杂。某些服务可以接收邮件，这显然是可能的。以下是一些受欢迎的服务之一：

- [ZoneEdit](www.zoneedit.com/) — 支持 ez-update 
- [No-IP](www.no-ip.com/) — 支持 no-update 

**注意**

邮件服务器通常也会回退到 A 记录中列出的 IP 地址。然而，依赖此功能被认为是不良做法。

### 从邮件主机获取邮件

从邮件主机获取邮件的配置是有限的。你必须能够接收邮件。软件安装分为两个部分。第一部分涵盖 Exim。

### 安装并配置邮件服务器

安装和配置 Exim 非常简单，得益于 Ubuntu 自带的软件包。以下是安装步骤：

1. 首先安装 Exim：

```
$ sudo apt-get install ex4-daemon
```

2. 你需要更改一些配置选项。运行以下命令：

```
$ dpkg-reconfigure --priority=medium exim4-config
```

你被问了几个问题。以下是回答方式：

- 通用类型：如果你需要通过服务器发送所有邮件，选择“通过 smarthost 发送；通过 SMTP 接收”。否则，选择“站点；通过 SMTP 发和接收”。
- 邮件名称：在此处输入你的邮件服务器名称。
- IP 地址：清除此框（如果它已经是空的），以便 Exim 监听所有 IP 地址。
- 接收邮件的域名：输入你的服务器将接收的任何域名。请确保使用冒号分隔，而不是逗号。
- 转发域名：输入你的服务器将转发的任何域名名称，这意味着它可以从那里接收邮件并转发。在大多数情况下，你不需要在这里输入任何内容。
- 转发机器：输入你希望服务器接收的客户端机器的 IP 地址。另一种（安全的）选项是留空并要求客户端使用 SMTP 进行身份验证。
- 重写头：如果你想通过在输出邮件中重写 From、Reply-To、Sender 和 Return-Path 值来保留本地邮件名称，请选择 Yes。如果是，你必须为本地用户设置可见的域名。
- 将配置拆分为小文件：选择 Yes 让 Exim 将配置文件分成 50 个小文件（而不是一个大文件），放在 `/etc/exim4/conf.d` 目录。否则，将使用 `/etc/exim4/exim4.template` 文件作为单体文件。

3. 此配置使用 Maildrop 进行本地邮件投递。Maildrop 可以将消息投递到 Courier 预期的 Maildir 目录，还可以处理基础排序。

## 第 16 章：运行邮件服务器

过滤（如“配置邮件客户端”章节中所述）。此包默认未安装，请按照以下方式安装：

```
$ sudo apt get install maildrop
```

- 4. 为系统中的每个用户根目录创建 Maildir 目录。此步骤必须以用户身份运行，因为运行此命令会导致 Maildrop 无法写入文件夹：

```
$ mailirdrop.maildrop $HOME/Maildir
$ mailirdrop.maildrop -f Trash $HOME/Maildir
```

- 5. 在 `/etc/skel` 下创建邮件目录。`/etc/skel` 的内容将复制到设置完成后你创建的任何新账户的家目录下：

```
$ sudo mailirdrop.maildrop /etc/skel/Maildir
$ sudo mailirdrop.maildrop -f Trash /etc/skel/Maildir
```

- 6. 配置 Maildrop 将邮件投递到 Maildir 文件夹，而不是存储在 `/var/spool/mail` 中的 mbox 文件。使用你喜欢的文本编辑器编辑 `/etc/maildroprc`，并取消文件末尾此行的注释：

```
DEFAULT="$HOME/Maildir/"
```

- 7. Exim 需要配置为使用 Maildrop 投递消息。使用你喜欢的文本编辑器打开 `/etc/exim4/update-exim4.conf`，将文件末尾的 `dc_local_delivery` 行修改如下：

```
dc_local_delivery='maildrop_pipe'
```

- 8. 告诉 Exim 加载最新的配置更改：

```
$ sudo invoke rc.d exim4 reload
```

- 9. 安装 Courier IMAP 和 Courier POP：

```
$ sudo apt-get install courier-imap courier-pop
```

当询问安装程序是否应该为 Web 端管理创建目录时，选择 No。

你的系统现在应该能够接收消息了。你还应该能够使用 Thunderbird 或 Evolution 等邮件客户端连接到你的服务器。如果你计划按照下一节说明启用病毒和垃圾邮件过滤器，现在是测试邮件投递的好时机。你可以在本章稍后的“配置邮件客户端”章节找到有关如何配置邮件客户端连接到服务器的更多信息。

## 安装 ClamAV 和 SpamAssassin

安装和配置病毒及垃圾邮件过滤机制比安装 Exim 和 Courier 更复杂，但只要你仔细按照步骤操作，应该会进展顺利。然而，请记住，这种过滤为系统增加了许多复杂性，请确保 Exim 邮件服务器先运行，这样当系统运行不如预期时，你不需要检查这么多内容。

## 注意

Ubuntu 自带的 ClamAV 版本使用了较旧的病毒扫描引擎，与其基于的 Debian 系统也是如此。由于 Debian 的升级策略，更新后的引擎可能不会很快进入更新，一组 Debian 开发人员创建了特殊的 ClamAV 包，旨在易于安装。有关如何使用这些包代替标准版本的更多信息，请参阅 http://volatile.debian.net/。你可以从一开始就使用这些包，也可以之后向 APT 配置中添加相应的 URI 并进行升级。无论哪种情况，本节详细介绍的配置都是都是。你还可以使用 `freshclam` 和 `clamget` 定期更新数据库，以生成新的 clamav 数据包。

以下是安装 ClamAV 和 SpamAssassin，然后配置 Exim 使用它们来扫描消息的方法：

- 1. 安装 ClamAV 和 SpamAssassin 包：

```
$ sudo apt get install clamav-daemon clamav-testfiles \
spamassassin spamc
```

- 2. 将 clamav 加入 Debian-exim 组并重启 ClamAV 守护进程。此步骤允许 ClamAV 守护进程读取 Exim 邮件队列中的文件。

```
$ sudo gpasswd -a clamav Debian-exim
$ sudo invoke -rc.d clamav daemon restart
```

- 3. 将 SpamAssassin 使用的报告模板替换为更适合邮件头的模板。使用文本编辑器在 `/etc/spamassassin/local.cf` 文件末尾添加这些行：

```
clear_report_template
report_YES_, score=SCORE_, required=_REQD_, summary=
report_SUMMARY_
```

- 4. 配置 SpamAssassin 后守护进程自动运行，并更改 OPTIONS 行以尝试为用户创建配置文件。在 `/etc/default/spamassassin` 文件中更改以下选项：

```
ENABLED=1
OPTIONS="--max-children 5"
```

- 5. 启动 SpamAssassin 守护进程：

```
$ sudo invoke-rc.d spamassassin start
```

- 6. 创建将包含在 Exim ACL（访问控制列表）中用于扫描消息数据的条目。使用文本编辑器创建一个名为 `/etc/exim4/acl_check_data_local` 的文件，包含以下内容：

```
deny message = $malware_name detected in message
demime = *
malware = *
```

```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${if <$message_size>(80k)|1|{0}}
spam = nobody:true/defer_ok
```

```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${if <$message_size>(80k)|1|{0}}
spam = nobody:true/defer_ok
```

- 7. 告诉 Exim 使用哪种扫描器以及如何连接 SpamAssassin。使用文本编辑器创建 `/etc/exim4/conf.d/main_acl_options` 文件，包含以下内容：

```
av_scanner = clamd:/var/run/clamav/clamd.ctl
spamd_address = 127.0.0.1
CHECK_DATA_LOCAL_ACL_FILE = CONFDIR/acl_check_data
```

- 8. 告诉 Exim 加载新配置：

```
$ sudo invoke.d exim4 reload
```

## 第四部分：设置 Linux 服务器

现在通过服务器传输的消息都应该使用 ClamAV 检查病毒。此外，小于 80KB 的消息也将由 SpamAssassin 检查。现在是再次测试配置的好时机。你可以在下一节找到你可能遇到的问题的解决方法。

## 测试与故障排除

本节包含通用的故障排除提示，以及关于某些常见错误的特定信息解决方法。

## 查看日志

Exim 的所有日志信息都写入三个文件，位于 `/var/log/exim4:mainlog`。

`mainlog` 中的条目通常包含一组字符，例如 `n7MJ123W00243`。这是相关日志条目的消息标识符。在消息标识符之后有两个字符字符串。表 16-1 显示了这些字符串的含义。

| 表 16-1 | Exim 日志文件消息 |
| 符号 | 描述 | 解释 |
| --- | --- | --- |
| < | 消息到达 | 这些条目显示进入 Exim 的消息，通常通过 SMTP 或本地 IPC。 |
| --> | 消息投递 | 这些条目显示消息投递，无论是投递到本地邮箱还是使用 SMTP 或其他传输方式到远程主机。 |
| > | 消息投递中的额外地址 | 这些条目显示已投递给另一个收接收者的额外地址（并以 -- 条目记录）。 |
| ** | 投递失败 | 这些条目显示永久性投递错误。错误表明消息已从邮件队列中删除，在大多数情况下已生成 DSN（投递状态通知）并发送给原始消息发送者。 |

## 第 16 章：运行邮件服务器

Courier IMAP 和 POP 守护进程的日志信息保存到 `/var/log/mail.log`。正常条目包括 LOGIN（登录）和 LOGOUT（注销）。DISCONNECTED（断开）消息通常表示在执行正常注销之前连接已中断。

## 注意

`tail` 工具对于观察日志的新条目非常有用。使用 `-f` 切换到 tail 可以监控新条目，并在它们写入日志时将其显示在屏幕上——例如，`tail -f /var/log/exim4/mainlog`。

## 常见错误（以及解决方法）

你会在服务器上遇到两种常见类型的问题：消息被 Exim 拒绝或未送达，以及连接到 Courier 时登录失败。

## 被 Exim 拒绝的消息

当消息被 Exim 拒绝时，首先检查的地方是 `maillog` 和 `rejectlog` 文件。以下是常见错误示例及其修复建议：

- **Relaying Denied（拒绝转发）** —— 下列错误表示发送消息的客户端未被 Exim 识别为客户端，且收件者不在本地或中继域列表中：

```
H=sample.client [10.0.12.16] F=<sender@example.org> rejected RCPT <rcpt@remotesite.org>: relay not permitted
```

如果客户端 IP 地址经常变化或属于信任的 IP 地址范围，你可以通过运行以下命令将其添加：

```
sudo dpkg-reconfigure --priority=medium exim4-config
```

同一命令也可用于将收件者域添加本地域或中继域。

## 注意事项

除非所有能从这些地址连接的用户都是你的，否则不要添加客户端 IP。同样，除非你了解该域的所有者并已为其转发邮件做出了安排，否则不要将某个域作为中继域。对其中任何一种错误的操作都可能导致你的服务器变成垃圾邮件发送者的中继站，被用来攻击其他站点。

如果客户端 IP 地址可能频繁变化且不属于信任范围，你应该配置客户端使用本地邮件服务器，或者在 Exim 中配置 SMTP 认证。你可以在 `/usr/share/doc/exim4-base/README.Debian.html` 和 `/etc/exim4/conf.d/auth/30_exim4_config_examples` 中找到关于在服务器上启用 SMTP 认证的更多信息。

## 第部分：设置 Linux 服务器

## 注意

你可以在 `30_exim4_config_examples` 中启用 Courier 认证示例，允许 Exim 使用该功能进行认证，从而消除设置不同机制的需求。但是，为了使其工作，你需要将 `debian-exim` 用户添加到守护进程组（`sudo gpasswd -a debim daemon`）并重启 Exim。

- **ClamAV 配置错误** —— 下列错误表示 ClamAV 守护进程无法读取临时文件：

```
acl condition: clamd: Access denied /var/spool/exim4/scan/tmp
```

确保你已将 `clamd` 添加到守护进程组并重启了 ClamAV。

- **ClamAV Unavailable（不可用）** —— 这通常表示 ClamAV 守护进程未运行：

```
acl condition: clamd: unable to connect to UNIX socket /var/run/clamav/clamd.ctl (No such file or directory)
```

使用 `invoke-rc.d clamav start` 启动守护进程。你也可以使用 `clamscan` 程序来测试守护进程，如下：

```
$ clamscan /usr/share/clamav/testfiles/clam.exe:
-----------------------
SCAN SUMMARY
-----------------------
Infected files: 0
Time: 0 sec
```

## Exim 未未送达的消息

在某些情况下，消息会被服务器接收但不会被送达。这些错误中的某些被视为临时故障，在重试计时器耗尽之前不会生成退信邮件。你最可能在 `maillog` 文件中看到的错误如下所示：

```
transport=local_pipe deliver=7 (could mean temporary error) from command: /usr/bin/maildrop
```

这表示 Exim 尝试将消息传递给 Maildrop，但 Maildrop 返回了错误。最可能的原因是缺少 Maildrop 目录，或者 Maildrop 目录的所有者不正确。下一节将显示如何检测并修复这些问题。

## 连接到 Courier 时的登录失败

除非真正的密码错误（可以通过在邮件客户端中输入正确的密码来解决），其他一些情况也可能导致登录失败。其中某些情况还可能导致送达问题。正常的登录失败会产生类似下面的日志条目：

```
courierpop3login: LOGIN FAILED, ip=::ffff:127.0.0.1 entered the username or password
```
