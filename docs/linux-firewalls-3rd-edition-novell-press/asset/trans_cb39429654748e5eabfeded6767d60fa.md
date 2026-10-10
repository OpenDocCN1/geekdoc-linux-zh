

消息按照产生它们的子系统进行分类。在 man 手册页中，这些类别被称为 *设施*（参见表 8.1）。

### 表 8.1 SYS 日志设施类别

| 设施 | 消息类别 |
| :--- | :--- |
| auth 或 security | 安全/授权 |
| authpriv | 私有安全/授权 |
| cron | cron 守护进程消息 |
| daemon | 系统守护进程生成的消息 |
| ftp | FTP 服务器消息 |
| kern | 内核消息 |
| lpr | 打印机子系统 |
| mail | 邮件子系统 |
| news | 网络新闻子系统 |
| syslog | syslogd 生成的消息 |
| user | 用户程序生成的消息 |
| uucp | UUCP 子系统 |

在任何给定的设施类别中，日志消息被划分为 *优先级* 类型。优先级按重要性递增的顺序列于表 8.2 中。

### 表 8.2 SYS 日志消息优先级

| 优先级 | 消息类型 |
| :--- | :--- |
| debug | 调试消息 |
| info | 信息性状态消息 |
| notice | 正常但重要的状况 |
| warning 或 warn | 警告消息 |
| err 或 error | 错误消息 |
| crit | 严重状况 |
| alert | 需要立即关注 |
| emerg 或 panic | 系统不可用 |

*syslog.conf* 中的条目指定了日志设施、优先级以及消息写入的位置。并不明显的是，优先级具有包含性。它意味着包含该优先级及所有更高优先级的消息。例如，如果你指定错误优先级的消息，则包含错误及更高优先级（即 crit、alert 和 emerg）的所有消息。

日志可以写入设备（如控制台），也可以写入文件和远程机器。

## /var/log 中日志文件的提示

syslogd 不会创建文件。它只写入已存在的文件。如果日志文件不存在，你可以使用 touch 命令创建它，然后确保它由 root 拥有。出于安全目的，日志文件通常不可被普通用户读取。特别是安全日志文件 /var/log/secure，仅由 root 可读。

以下两个条目将所有内核消息写入控制台和 /var/log/messages。消息可以复制到多个目的地：

```
kern.*	/dev/console
kern.*	/var/log/messages
```

此条目将 panic 消息写入所有默认位置，包括 /var/log/messages、控制台以及所有用户终端会话：

```
*.emerg
```

接下来两个条目将与 root 权限和连接相关的身份验证信息写入 /var/log/secure，并将用户授权信息写入 /var/log/auth。由于优先级定义为 info 级别，debug 消息不会被写入：

```
authpriv.info	/var/log/secure
auth.info	/var/log/auth
```

接下来两个条目将一般守护进程信息写入 /var/log/daemon，并将邮件流量信息写入 /var/log/maillog：

```
daemon.notice	/var/log/daemon
mail.info	/var/log/maillog
```

debug 和 info 优先级的守护进程消息以及 debug 优先级的邮件消息不会被记录（这是作者的个人偏好）。named、crond 和定期系统邮件检查会定期产生无趣的信息性消息。

最后一个条目将 info 或更高优先级的所有消息类别记录到 /var/log/messages，但排除了 auth、authpriv、daemon 和 mail。在这种情况下，后四种消息设施被设置为 none，因为它们的消息被重定向到它们自己的专用日志文件：

```
*.info;auth,authpriv,daemon,mail.none	/var/log/messages
```

## 关于 syslog 配置的更多信息

> 有关 *syslog* 配置选项和示例配置的更完整描述，请参阅 *syslog.conf(5)* 和 *syslogd(8)* 的 man 手册页。

*syslogd* 可以配置为将系统日志写入远程机器。使用类似于第 6 章“数据包转发”中示例的网络服务器配置，并从 DMZ 中的内部机器提供服务的站点，可能会希望保留系统日志的远程副本。维护远程副本有两个优点：首先，日志文件集中在一台机器上，使系统管理员更容易监控日志。其次，如果某台服务器机器被入侵，信息将得到保护。

第 9 章“入侵检测与响应”讨论了系统日志在系统被入侵后恢复过程中的重要性。攻击者在成功获得被入侵机器的 *root* 访问权限后，最先做的事情之一，就是要么擦除系统日志，要么安装特洛伊木马程序以不记录其活动。在你最需要系统日志文件时，它们要么消失，要么变得不可信。维护日志的远程副本有助于保护这些信息，至少可以在黑客替换写入日志文件信息的守护进程之前提供保护。

要远程记录系统信息，本地日志配置和远程日志配置都需要进行 slight modifications（轻微修改）。

在收集系统日志的远程机器上，在调用 *syslogd* 时添加 *-r* 选项。*-r* 选项告诉 *syslogd* 监听 UDP *syslog* 端口 *514*，以接收来自远程系统的传入日志信息。

在产生系统日志的本地机器上，编辑 *syslogd* 的配置文件 */etc/syslog.conf*，并添加指定哪些日志设施和优先级要写入远程主机的行。例如，以下内容将所有日志信息复制到 *hostname*：

```
*.*			@hostname
```

*syslogd* 的输出通过 UDP 发送。源端口和目标端口都是 *514*。客户端防火墙规则如下：

```
iptables -A OUTPUT -o <out-interface> -p udp \
-S <this host> --sport 514 \
-d <log host> --dport 514 -j ACCEPT
```

## 防火墙日志消息：它们意味着什么？

为了生成防火墙日志，内核必须启用防火墙日志记录进行编译。默认情况下，单独匹配的数据包作为 **kern.warn**（优先级 4）消息被记录。可以使用 `-j LOG` 的 `--log-level` 选项更改日志优先级。当数据包匹配具有 LOG 目标的规则时，会报告大多数 IP 数据包头部字段。默认情况下，防火墙日志消息被写入 `/var/log/messages`。

你可以通过创建新的日志文件并添加一行到 `/etc/syslog.conf` 来将防火墙日志消息复制到不同的文件：

```
kern.warn	/var/log/fwlog
```

作为一个 TCP 示例，拒绝访问 portmap/sunrpc TCP 端口 111 的此规则将在 `/var/log/messages` 中产生以下消息：

```
iptables -A INPUT -i $EXTERNAL_INTERFACE -p tcp \
     --dport 111 -j LOG --log-prefix "DROP portmap: "

iptables -A INPUT -i $EXTERNAL_INTERFACE -p tcp \
     --dport 111 -j DROP
```

```
(1)    (2)     (3)    (4)     (5)      (6)   (7)
Jun 19 15:24:16 firewall kernel: DROP portmap: IN=eth0 OUT=
                  (8)
                  MAC=00:a0:cc:40:9b:a8::00:a0:cc:d4:a7:81:08:00

                  (9)         (10)        (11)
                  SRC=192.168.1.4 DST=192.168.1.2 LEN=60
                  (12)       (13)     (14)    (15)    (16)
                  TOS=0x00 PREC=0x00 TTL=64 ID=57743 DF
                  (17)      (18)        (19)      (20)
                  PROTO=TCP SPT=33926 DPT=111 WINDOW=5840
                  (21)     (22)      (23)
                  RES=0x00 SYN URG=0
```

为了讨论的目的，日志消息字段被编号：

- 字段 1 是日期，**Jun 19**。
- 字段 2 是写入日志的时间，**15:24:16**。
- 字段 3 是计算机的主机名，**firewall**。
- 字段 4 是生成消息的日志设施，**kernel**。
- 字段 5 是 LOG 规则中定义的 `log-prefix` 字符串。
- 字段 6 是输入规则所附加的传入网络接口，`eth0`。
- 字段 7 是传出接口，在 `INPUT` 链的规则上没有值。
- 字段 8 是数据包到达的接口的 MAC 地址，后面跟着八对无用的十六进制数字。
- 字段 9 是数据包的源地址，`192.168.1.4`。
- 字段 10 是数据包的目标地址，`192.168.1.2`。
- 字段 11 是 IP 数据包的总长度（以字节为单位），`LEN=60`，包括数据包头部及其数据。
- 字段 12 是服务类型（TOS）字段的 3 个服务位，加上一个保留的尾部位，`TOS=0x00`。
- 字段 13 是 TOS 字段的顶部 3 个优先级位，`PREC=0x00`。
- 字段 14 是数据包的时间剩余（TTL）字段，`TTL=64`。时间剩余是数据包过期前剩余的最大跳数（即访问的路由器数量）。
- 字段 15 是数据包的数据报 ID，`ID=57743`。数据报 ID 是数据包 ID 或此 TCP 片段所属的段。
- 字段 16 是片段标志字段，指示“不分片”（DF）位已设置。
- 字段 17 是数据包中包含的消息协议类型，`PROTO=TCP`。字段值包括 6 (TCP)、17 (UDP)、1 (ICMP)，以及用于其他协议类型的 `PROTO=<number>`。
- 字段 18 是数据包的源端口，`33926`。
- 字段 19 是数据包的目标端口，`111`。
- 字段 20 是发送方的窗口大小，`WINDOW=5840`，表示此时它愿意从该主机接受和缓冲的数据量。
- 字段 21 报告 TCP 头部的保留字段。所有 4 个位必须为 0。
- 字段 22 是 TCP 状态字段。在这种情况下，`SYN` 标志已设置。
- 字段 23 是紧急指针，指示被认为紧急的数据量。由于 `URG` 标志未设置，该字段为 0。

在解释日志消息时，最有趣的字段是这些：

```
Jun 19 15:24:16 DROP portmap: IN=eth0 SRC=192.168.1.4 DST=192.168.1.2 PROTO=TCP SPT=33926 DPT=111 SYN
```

