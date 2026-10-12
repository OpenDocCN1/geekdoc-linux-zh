
```
# Run the command
$LOGRESOLVER -s $STATFILE < $LOGFILE > $OUTFILE
```

```
exit 0;
```

当此脚本从命令行或作为 cron 作业运行时，它会创建一个名为 /usr/local/apache/logs/access_log.resolved 的文件，其中将包含解析为各自主机名的所有 IP 地址。此外，脚本还会生成一个名为 /tmp/log_stats.txt 的统计文件，其中显示缓存使用信息、总解析 IP 地址以及解析器实用程序报告的其他信息。以下是此类统计文件的示例：

```
logresolve Statistics:
Entries: 3
    With name  : 0
    Resolves   : 3
Cache hits  : 0
Cache size  : 3
Cache buckets  :     IP number * hostname
130   207.183.233.19 - nano.evoknow.com
131   207.183.233.20 - rhat.evoknow.com
132   207.183.233.21 - r2d2.evoknow.com
```

请注意，由于它解析的三个 IP 地址（对于上面显示的示例日志条目）都是唯一的，因此该实用程序无法利用缓存。但是，如果日志文件中有来自同一主机的 IP 地址，则缓存将被用于解析它们，而不是盲目地进行 DNS 请求。

如果你认为可以使用此脚本，我建议将其作为 cron 作业运行。例如，在我的 Linux 上的 Apache Web 服务器上，我只需将脚本添加到 /etc/cron.daily 以便每天创建日志的解析版本。

## 第13章
## 配置电子邮件服务
### 本章内容
- 为电子邮件服务配置 DNS 记录
- 使用 `sendmail` 创建 SMTP 邮件服务
- 测试 `sendmail` 配置
- 保护 `sendmail`
- 创建 POP 邮件服务
- 设置 SMTP 和 POP 邮件客户端

电子邮件是现代通信的先决条件。每天有数百万封电子邮件在数百万人之间发送。在本章中，我将讨论如何使用 SMTP 和 POP 邮件服务器设置电子邮件服务。

## 为邮件服务设置 DNS

在 Red Hat Linux 服务器上运行自己的 SMTP 服务器之前，你需要为电子邮件传递创建适当的 DNS 配置。方法如下。你可以使用邮件交换（MX）记录在域的 DNS 配置中标识 SMTP 邮件服务器资源。

![](img/9eb7e89292d2f85707b4d49102c865b7_382_0.png)

请参阅第 15 章了解有关 MX 记录的详细信息。

假设你想将名为 mail.yourdomain.com 的主机指定为 yourdomain.com 域的 SMTP 邮件服务器。yourdomain.com 的起始授权（SOA）记录必须包含如下一行：

```
IN MX preference_value mail_server_hostname.
```

上述中，preference_value 是一个正整数，仅在你拥有多个 SMTP 邮件服务器时才有用。如果只有一个 SMTP 邮件服务器，此数字可以是任意值。例如：

```
IN MX 5 mail.yourdomain.com.
```

这里单个 SMTP 邮件服务器 mail.yourdomain.com 已设置为优先级 5。以下是多服务器场景的示例：

```
IN MX 10 fast-mail-server.ad-engine.com.
IN MX 20 slow-mail-server.ad-engine.com.
```

在此示例中，偏好号码起着至关重要的作用。当互联网上的任何人使用 SMTP 邮件服务器希望向 someone@ad-engine.com 发送邮件时，它首先执行 DNS 查询以查找 ad-engine.com 的 MX 记录。返回给 SMTP 邮件服务器的 MX 记录将类似于前面代码中显示的内容。然后 SMTP 邮件服务器选择 fast-mail-server.ad-engine.com 作为首选邮件服务器进行投递，因为它在两个可用服务器中具有更高的优先级（即更低的偏好号码）。然后 SMTP 邮件服务器尝试使用端口 25 与 fast-mail-server.ad-engine.com 计算机建立 SMTP 连接。如果 fast-mail-server.ad-engine.com 服务器因任何原因不可用，则会选择 slow-mail-server.ad-engine.com 服务器进行投递。拥有多个 MX 记录可为你的邮件投递系统提供冗余，这对于电子邮件是组织关键部分的情况非常重要。

![](img/9eb7e89292d2f85707b4d49102c865b7_383_0.png)

> 在 MX 记录中始终使用具有自己的 A 记录的主机名。换句话说，不要在 MX 记录中使用主机别名。有关详细信息，请参阅 RFC 1123。

在使用适当的 MX 记录设置 DNS 后，通过 nslookup -q=mx yourdomain 命令测试配置。如果正确配置了 DNS，你将看到刚刚创建的 MX 记录。完成此操作后，你就可以设置 SMTP 邮件服务了。

## 设置 SMTP 邮件服务

设置 SMTP 服务的第一步是决定要为 Red Hat Linux 系统使用哪个 SMTP 邮件服务器。有许多 SMTP 邮件服务器产品可用。然而，由于其悠久的全球部署历史，sendmail 在众多产品中脱颖而出。sendmail 也是 Red Hat Linux 的默认 SMTP 邮件服务器，因此在本章中我使用 sendmail 作为 SMTP 服务器。

你可以从 Linux 系统运行 `telnet localhost 25` 命令来查看端口 25 上是否已安装 `sendmail` 服务器。如果可以使用上一个命令连接到邮件服务器，你可以按 Ctrl+C 断开连接，然后跳过以下各节中讨论的安装部分。

### 安装 sendmail

与你在 Red Hat 系统上安装的任何其他服务器软件一样，sendmail 也以 RPM 包的形式提供。然而，你需要安装多个 RPM 包；它们是：

- `sendmail-version.architecture.rpm` — 主要发行版
- `sendmail-cf-version.architecture.rpm` — sendmail 邮件配置文件发行版
- `sendmail-config-version.architecture.rpm` — 辅助配置文件发行版
- `sendmail-doc-version.architecture.rpm` — 文档发行版

前三个 RPM 包可以在官方 Red Hat CD-ROM 1 和 2 上找到。最后一个文档包可以从 www.rpmfind.net 下载。

安装这些包非常简单；只需运行 `rpm -ivh package_name` 来安装每个包即可。

![](img/9eb7e89292d2f85707b4d49102c865b7_385_0.png)

如果你在 Red Hat Linux 安装期间安装了旧版本的 sendmail，请在安装新版本之前删除 sendmail 包；它们可能不完全兼容。要卸载 RPM 包，请使用 rpm -e package_name 命令。你还可以使用 rpm -q partial_package_name 命令查找 RPM 包的确切包名。

安装包后，你就可以配置 sendmail 了。sendmail 的主要配置文件是 /etc/sendmail.cf。

### 配置 sendmail 监听网络接口

默认情况下 sendmail 仅监听 127.0.0.1 接口，即回环接口，这意味着你无法在本地邮件服务器系统之外发送或接收邮件。对于大多数场景来说这并不理想，因为你希望与其他机器之间发送和接收邮件——这正是电子邮件的全部意义所在。在这种情况下，请按照以下步骤启用 sendmail 接受所有主机的连接：

1. 以 root 身份，从 /etc/mail/sendmail.mc 文件中删除以下行：
2. 将你的 /etc/sendmail.cf 文件备份到 /etc/sendmail.cf.good。
3. 运行 m4 /etc/mail/sendmail.mc > /etc/sendmail.cf 以创建新的 /etc/sendmail.cf 文件，其中已删除或注释掉网络接口限制。

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```

![](img/9eb7e89292d2f85707b4d49102c865b7_385_1.png)

如果你希望将该行保留为注释，只需在行前添加 dnl，使其如下所示：

```
dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')
```

4. 使用 `/etc/rc.d/init.d/sendmail restart` 命令重启 sendmail。

现在 sendmail 将监听你的非回环网络接口以及回环接口。

### 启动和停止 sendmail

虽然你尚未配置 sendmail 服务器，但仍可以运行它。要手动启动 sendmail，可以运行以下命令：

```
/usr/sbin/sendmail -qqueue_processing_interval
```

你必须用时间替换 queue_processing_interval。通常，时间以分钟或小时为单位指定。例如，要使 sendmail 每 15 分钟处理一次邮件队列，可以使用 -q15m；或者，另一个例子，要每小时处理一次队列，可以使用 -q1h。你还可以指定秒（s）、天（d）或周（w）。例如，你可以指定 -q1h30m，以便 sendmail 每一个半小时处理一次查询。

![](img/9eb7e89292d2f85707b4d49102c865b7_386_0.png)

> 如果你没有全天候的互联网连接，你可以使用 /usr/sbin/sendmail -bd -o DeliveryMode=d 以延迟模式启动 sendmail，这会避免在下次通过 /usr/sbin/sendmail -q 再次运行之前使用 DNS。如果定期连接，你可以将 /usr/sbin/sendmail -q 放入 cron 作业中，这样当你的连接建立时，队列会自动处理。

如果你希望 sendmail 在每次启动后自动启动，请确保从默认运行级别目录到 /etc/rc.d/init.d/sendmail 脚本创建一个符号链接（以 Sxx 开头，其中 xx 为数字）。例如，要在多用户系统（运行级别 3）每次启动后运行 sendmail，我可以创建以下符号链接：

```
ln -s /etc/rc.d/init.d/sendmail /etc/rc.d/rc3.d/S85sendmail
```

此符号链接确保 sendmail 在每次启动后自动启动。如果你查看此脚本，你会看到 sendmail 是使用 -bd 选项启动的，这会将其作为守护进程、后台进程启动。你可能希望修改 /etc/rc.d/init.d/sendmail 脚本来反映你站点对队列间隔的要求。你可能
