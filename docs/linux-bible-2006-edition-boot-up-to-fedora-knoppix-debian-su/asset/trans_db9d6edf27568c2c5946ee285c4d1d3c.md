

## 第五部分 ♦ 运行服务器

- 7. 接下来，需要配置 Exim 使用 Maildrop 投递邮件。使用你偏好的文本编辑器打开 /etc/exim4/update-exim4.conf，并在文件末尾添加以下行：
  `dc_localdelivery='maildrop_pipe'`

- 8. 告诉 Exim 加载最新的配置更改：

```bash
# invoke-rc -d exim4 reload
```

- 9. 最后，安装 Courier IMAP 和 Courier POP：
```bash
# apt-get install courier-imap courier-pop
```

当安装程序询问是否应该为基于 Web 的管理创建目录时，请选择 "no"。

你的系统现在应该能够接收邮件了。你还应该能够使用 Thunderbird 或 Evolution 等邮件客户端连接到你的服务器。现在是测试邮件投递的好时机，即使你计划按照下一节的说明启用病毒和垃圾邮件过滤器。关于配置邮件客户端连接到你的服务器的更多信息，可以参考本章的“配置邮件客户端”部分。

## 安装 ClamAV 和 SpamAssassin

安装和配置病毒及垃圾邮件过滤机制比安装 Exim 和 Courier 要复杂，但只要你仔细按照步骤操作，应该仍然会顺利。然而，请记住，这将增加系统的复杂性，最好的做法是先确保 Exim 邮件服务器运行正常，这样如果系统没有按预期工作，你就不会有太多需要检查的地方。

> Debian 3.1（又名 "Sarge"）包含的 ClamAV 版本使用了旧的病毒扫描引擎。由于 Debian 的升级策略，更新后的引擎可能在几年内无法进入更新，因此，一组开发者创建了一组特殊的 ClamAV 软件包，设计用于在 Sarge 上进行轻松安装。关于如何使用这些包而不是标准版本的更多信息，请参阅 http://volatile.debian.net/。你可以选择从开始就这样做，或者将相应的 URI 添加到你的 APT 配置并进行升级。无论哪种情况，本节详细介绍的配置过程都是

以下是安装 ClamAV 和 SpamAssassin，然后配置 Exim 使用它们扫描邮件的方法：

- 1. 安装 ClamAV 和 SpamAssassin 软件包：
```bash
# apt-get install clamav-daemon clamav-testfiles \ spamassassin spamc
```

你会被问及许多关于如何配置 ClamAV 的问题。以下是回答方式：

- **Virus update method（病毒更新方法）** —— 这是 freshclam（ClamAV 的一部分）用于下载更新数据库的方法。推荐选项是作为守护进程（daemon）运行 freshclam。

- **Local database mirror site（本地数据库镜像站点）** —— 这是 freshclam 获取病毒信息更新的站点。站点第二部分是两个字母的国家代码。选择你的国家代码，如果你的不可用，则选择附近国家的代码。

- **HTTP proxy information（HTTP 代理信息）** —— 除非你需要通过代理服务器访问 Web 服务器，否则不要在此处输入任何内容。如果你的连接适合运行邮件服务器，你可能不需要使用代理服务器。

- **Notify clam after updates（更新后通知 clam）** 选择 "yes"

2. 将 clamav 加入 Debian-exim 组并重启 ClamAV 守护进程。这允许 ClamAV 读取 Exim 邮件队列中的文件：

```bash
# gpasswd -a clamav Debian-exim
# invoke rc-d clamav-daemon restart
```

3. 将 SpamAssassin 使用的报告模板替换为更适合邮件头的模板。使用文本编辑器在 /etc/spassassin/local.cf 的末尾添加这些行：

```
clear_report_template
YES_NO, score=SCORE_, required=REQD, summary=
report_SUMMARY_
```

4. 配置 SpamAssassin 后台守护进程自动运行且不尝试为用户创建偏好。更改 /etc/default/spamassin 中的以下选项：

```bash
ENABLED=1
OPTIONS="--max-children 5*"
```

5. 启动 SpamAssassin 守护进程：

```bash
# invoke rc-d spamassin-start
```

6. 创建将包含在 Exim ACL（访问控制列表）中的条目，用于扫描邮件数据。使用文本编辑器创建一个名为 /etc/exim4/acl_check_data_local 的文件，内容如下：

```
deny message = $malware_name detected in message
demime = *
malware = *
```

```
warn message = X-Spam-Score: $spam_score ($spam_bar)
condition = ${$if <($message_size)(80k)[1](0)}
spam = nobody:true/defer_ok
warn message = X-Spam-Status: $spam_report
condition = ${$if <($message_size)(80k)[1](0)}
spam = nobody:true/defer_ok
```

第一个块拒绝包含病毒或恶意软件的邮件，第二和第三个头部处理 SpamAssassin 是否认为它们是垃圾邮件的邮件。最后一个块拒绝垃圾邮件评分高于 12 的邮件。
最后三个块中的 `defer_ok` 告诉 Exim，如果无法连接 SpamAssassin 守护进程，则继续处理。如果你希望在在这种情况下服务器返回临时性故障，可以将其删除。如果你希望在邮件无法被 ClamAV 扫描时继续处理，可以在 `message = ""` 行末尾添加 `/defer_ok`。

- 7. 告诉 Exim 病毒扫描器使用以及如何连接 SpamAssassin。使用编辑器创建一个名为 /etc/exim4/conf.d/main/10_exim4-exiscan_acl_options 的文件，内容如下：
```
av_scanner = clamd:var/run/clamav/clamd.ctl
spam_address = 127.0.0.1:783

CHECK_DATA_LOCAL_ACL_FILE = CONFDIR/acl_check_data_local
```

- 8. 告诉 Exim 加载新配置：
```bash
# invoke-rc.d exim4 reload
```

现在，通过你的服务器传输的所有邮件都应该使用 ClamAV 进行病毒检查。此外，小于 80 字节的邮件也将使用 SpamAssassin 进行检查。现在是再次测试配置的好时机。你可能遇到的问题的解决方法可以在下一节中找到。

## 测试与故障排除

本节包含通用的故障排除提示、关于某些常见错误的特定信息以及修复方法。

## 检查日志

Exim 的所有日志信息都写入三个文件：mainlog、rejectlog 和 paniclog。第一个文件 mainlog 包含所有事件。第二个 rejectlog 包含被拒绝邮件的条目。第三个 paniclog 除非发生严重问题，否则通常是空的。这些文件中的每个条目都时间戳开头。

### Exim 日志消息

| 符号 | 描述 | 解析 |
| :--- | :--- | :--- |
| <= | 邮件到达 | 这些条目显示进入 Exim 的邮件。 |
| => | 邮件投递 | 这些条目显示投递到本地或远程主机。 |
| -> | 附加地址 | 这些条目显示投递到另一个收件者。 |
| ** | 投递失败 | 这些条目显示永久投递错误。邮件从队列移除。 |
| == | 投递延迟 | 这些条目显示临时投递错误。系统将继续重试直到成功。 |

## 常见错误（如何修复）

有两种与服务器冲突的常见问题：被 Exim 拒绝的邮件以及连接 Courier 失败。

## 被 Exim 拒绝的邮件

当邮件被 Exim 拒绝时，首先应检查 mainlog 和 reject 文件。以下是常见错误示例及其修复建议：

以下错误表示发送邮件的客户端未被 Exim 识别为客户端，且接收者域名不在本地或中继域名列表中：

```
H=sample.client [1.2.3.4] f=<sender@example.org> rejected RCPT <rcpt@remotes.example.org>: relay not permitted
```

如果 IP 地址经常变化或属于信任范围，可以通过运行以下命令进行添加：

```bash
$ dpkg-reconfigure --priority=medium exim4-config
```

相同的命令也可用于将接收者域名作为本地中继域名添加。

不要添加 IP 范围，除非你信任从这些地址连接的所有用户。同样，除非你了解域所有者并已为他们中继邮件做好了安排，否则不要将域名作为中继域名。任何错误操作都可能导致你的服务器变成垃圾邮件发送者攻击其他站点的中继。

如果 IP 地址经常变化且不属于信任范围，理想情况下你应该配置客户端使用其本地邮件服务器，或在 Exim 中配置 SMTP 身份验证。

