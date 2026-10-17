
由于使用了 `syslog` 设施，日志会定期轮转，并保留之前的五个日志文件。旧日志命名为 `maillog.X`，其中 `X` 是数字。数字越大，日志越旧。

日志级别可以在 `sendmail.mc` 中设置，默认认为 `9`。`11–64` 级为详细模式，有关常用级别的进一步解释可以在 `/usr/share/log/sendmail/doc/op/ps` 中找到。如果你修改了日志，请通过服务 `sendmail reload` 启用更改。

Sendmail 的基础统计也记录在 `/var/log/maillog/statistics` 文件。必须使用 `mailstats` 工具读取。以 `root` 身份执行 `mailstats` 命令以显示 Sendmail 统计数据。默认情况下，它返回来自 `/var/log/maillog/statistics` 文件的统计数据（或 `sendmail.mc` 中为 `StatusFile` 指定的文件）。要指定不同的文件，请使用 `mailstats -f <filename>` 命令，其中 `<filename>` 是替代文件名和位置。列表 18.2 显示了示例输出。

## 列表 18.2 示例统计

Statistics from Sat Mar 25 16:04:28 2006

| M msgsfr bytes_from msgsto bytes_to msgsrej msgsdis msgsquir Mailer |
| 4 1054 5467K 1004 6030K 0 0 0 esmtp |

# 列表 18.2 续

| 9 | 2079 | 7248K | 8230K | 0 | 0 | local |
|---|---|---|---|---|---|--|
| T | 3133 | 12716K | 3079 | 14260K | 0 | 0 | 0 |
| C | 3133 | | 3079 | | 0 | |

如列表 18.2 所示，`mailstats` 的输出以统计开始的日期作为开头。在等号（`=`）所在行之前的几行包含了每个邮件发送器的统计数据，列的描述见表 18.1。

# 表格 18.1 mailstats 列

| 列 | 描述 |
|---|---|
| M | 邮件发送器数量 |
| msgsfr | 从邮件发送器收到的消息数 |
| bytes_from | 从邮件发送器接收的千字节数 |
| msgsto | 发往邮件发送器的消息数 |
| bytes_to | 发送到被拒绝消息的千字节数 |
| msgsrej | 被拒绝的消息数 |
| msgsdis | 丢弃的消息数 |
| msgsqur | 隔离的消息数（标记为隔离的特定消息，不会被投递或显示） |
| Mailer | 邮件发送器名称 |

以 `T` 开头的行列出了所有邮件发送器的总计，最后一行以 `C` 开头的行显示 TCP 连接数。

默认情况下，Dovecot 也会记录到 `/var/log/mailog` 文件，并包含如下登录尝试条目：

```
Jun 12 13:52:26 hostname doovec: imap-login: Login: user=<tfox>, method=PLAIN, rip=:ffff:127.0.0.1, lip=:ffff:127.0.0.1, TLS
```

要将 Dovecot 文件写入单独的文件，请在 `/etc/dovec.conf` 中使用 `log_path` 变量，如下所示：

```
log_path = /var/log/dovec
```

# 允许邮件连接

默认情况下，Sendmail 使用 TCP 和 UDP 端口 `25` 进行非加密传输。如果邮件服务器配置为使用 SSL 加密发送和接收邮件，则使用端口 `465`。如果你还启用了 POP 协议来检索邮件，请允许端口 `110` 用于不安全的 POP 连接，或端口 `995` 用于基于 SSL 的安全 POP 连接。如果你允许 IMAP，请允许端口 `143` 用于不安全的 IMAP 连接，或端口 `993` 用于基于 SSL 的安全 IMAP。请验证邮件服务器上的防火墙设置允许在相应端口上进行入站和出站请求。

如果使用了自定义 IPTables 规则，请参考第 24 章“配置防火墙”，允许这些端口的详情。

如果在 Red Hat Enterprise Linux 中使用默认安全级别，请使用安全级别配置工具（Security Level Configuration）。首先从桌面顶部的系统菜单中选择“管理”、“安全级别和防火墙”，或者通过执行 `system-config-securitylevel` 命令。在提示以用户身份运行时输入 `root` 密码。点击“其他端口”表格旁边的“添加”以添加相应的端口。

> 提示 如果设置内部邮件服务器，请确保配置其接受来自私有网络内 IP 地址的连接。如果邮件服务器可以通过互联网访问并接受来自任何计算机的邮件，可能会被未经授权的用户发送垃圾邮件给他人。

## 总结

在许多公司，邮件对于内部通信至关重要。在许多公司，它取代了纸质备忘录和公告。本章描述了邮件发送后的路径。然后在 Red Hat Enterprise Linux 上设置邮件 服务器。如果配合 Dovecot 使用，用于发送邮件的服务器还可以支持检索邮件的 IMAP 和 POP 协议。Sendmail、POP 和 IMAP 都可以配置 SSL 证书，使得发送和接收的邮件即使被拦截也难以读取。

# 第 19 章

# 本章

- `xinetd` 服务器
- 使用 FTP 传输文件
- 使用 NTP 保持同步
- 使用 CUPS 创建网络打印机

## 解释其他网络服务

本章描述了 `xinetd`、`FTP`、`NTP` 和 `CUPS` 网络服务，包括如何配置它们、如何连接它们以及它们使用的端口，以便管理员配置防火墙设置。

这四个服务有一个共同点——配置后，它们通常不需要通过 Red Hat 网络检查安全更新进行维护。

## xinetd 服务器

并不是所有服务都有自己的启动、停止和检查守护进程状态的脚本。某些网络服务由 `xinetd` 控制，也称为超级服务器。通过 `xinetd` 运行服务允许管理员利用 `xinetd` 的功能，如访问控制、自定义日志和连接速率。

`xinetd` 服务监听它所控制的所有端口。当请求连接时，`xinetd` 决定是否允许访问。如果允许客户端，`xinetd` 会启动所需的服务并将连接传递给它。使用此超级服务必须安装 `xinetd` RPM 软件包。如果没有，请按照第 3 章“操作系统更新”所述通过 Red Hat 网络安装。

## 配置 xinetd 服务器

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

# 385

# 19 解释其他网络服务

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

`xinetd` 超守护进程使用 `/etc/xinetd.conf` 文件。

# 386

## 列表 19.1 续

```
v6only           = no
```

```
# 设置环境变量属性
#
# passenv         =
 groups           = yes
 umask            = 002
```

```
# 通常不使用横幅。这设置了全局默认值
#
# banner          =
# banner_fail     =
# banner_success  =
}
```

```
included /xinetd.d
```
