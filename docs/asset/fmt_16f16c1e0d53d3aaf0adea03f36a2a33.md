
虽然选择器中允许多个设施和级别，但没有提供多个操作的规定。要将消息发送到两个地方（例如本地文件和中央日志主机），你可以在配置文件中包含两行具有相同选择器的内容。由于 syslog 消息可以用于拒绝服务攻击，可以配置 `syslogd` 限制其接受的消息速率。这在暴露于网络的系统上特别为重要。

# 第 11 章 Syslog 与日志文件

Syslog 配置在不同发行版之间差异很大。我们将查看一些常见示例。

syslog 配置在名为 `syslog.conf` 的文件中完成。该文件通常位于 `/etc/`。

## 独立主机

一个独立主机的配置配置所示：

```
# 小网络
*emerg
*info /var/log/messages
*auth.* /var/log/auth.log
*cron /var/log/cron.log
*user /var/log/user.log
```

第一行将紧急消息写入所有用户的屏幕。紧急级别消息是系统关闭时由 `shutdown` 产生的。第二行将重要消息写入 `/var/log/messages`。`*auth.*` 写入 `/var/log/auth.log`。`*cron` 写入 `/var/log/cron.log`。`*user` 写入 `/var/log/user.log`。

## Linux 系统管理手册

全范围日志主机，boulder。最后两个项目保留了打印机错误和 sudo 日志消息本地副本。

### 集中日志主机

此示例适用于 netloghost，它是一个约 7,000 台主机中型网络的中央安全日志主机。

+ # CS 部门 syslog.conf 配置文件，主日志主机

* 紧急到控制台和日志文件，带有时间标记

* emerg /dev/console

* err,kern.mark.debug:auth.notice /dev/console

* err,kern.mark.debug:user.none /var/log/console.log

* auth.notice /var/log/console.log

* 将非紧急消息发送到常规日志文件

* err,user.none:kern.debug /var/log/messages

* daemon,auth.notice:mail.crit /var/log/lpd-errs

* lpr.debug /var/log/mail

* mail /var/log/mail.log

### 本地授权内容，如 sudo 和 npasswd

* local2.debug /var/log/sudo.log

* local2.alert /var/log/sudo-errs.log

* auth.info /var/log/auth.log

### 其他本地内容

* local4.notice /var/log/da.log

* local7.debug /var/log/tcp.log

* 用户内容（未指定 facility 默认值）

* user.info /var/log/user.log

来自本地程序和网络上 syslog 的日志数据被写入文件。在某些情况下，每个项的输出被存放在它自己的文件中。

日志主机在写入消息时为每个消息生成时间戳。时间戳并不反映源主机。如果你的机器位于多个时区，或者你的系统时钟未同步，时间戳可能会产生误导性。

### 示例 syslog 输出

以下是科罗拉多大学计算机科学系主 syslog 主机上的文件片段。约有 200 台主机向该机器记录日志。

```
Dec 18 15:42 av18.cs.colorado.edu sbatchd[295]:main: ls_info()
failed: LIM is down; try later, trying ...nDec 18 15:28 proxy-1.cs.colorado.edu pop-proxy[27283]: Connection from
128.138.198.84
Dec 18 15:40 mroe.cs.colorado.edu pingem[271]: maltese-
office.cs.colorado.edu has not answered 42 times
```

## 第 11 章 syslog 和日志文件 213

Dec 14 15:14:51 coyote.cs.colorado.edu PAM_unix[17405]: (sshd) session closed

user trent

Dec 18 15:15:48 proxy-1.cs.colorado.edu pop-proxy(27285): Connection from

12.2.209:183

Dec 18 15:15:50 av18.cs.colorado.edu last message repeated 100 times

此示例包含了来自多个主机（av18, proxy-1, coyote, 和 imroe）以及来自多个程序的条目：batchd, pop-proxy, pingem 和可插身份模块（Pluggable Authentication Modules）库。

注意片段的最后一行，它抱怨消息被重复了 100 次。为了帮助保持日志简短，syslog 通常尝试合并重复消息并将其替换为此类消息。然而，提取此示例的机器接受来自许多其他主机的日志条目，因此特定的消息有点误导性。它实际上指的是 av18 的上一个日志条目，而不是复合日志中紧接其后的条目。

定期检查日志是一个好主意。确定什么是正常情况，这样当异常发生时你可以识别出来。更好的是设置一个像 `swatch` 这样的日志处理器来自动捕获这些情况；参见第 216 页“配置日志文件以有用信息”。

## 为你的系统设计日志方案

在小型站点，配置日志以便将重要的系统错误和警告保留在每台机器的文件中足够了，就像我们在使用 syslog 之前做的那样。`syslog.conf` 文件可以为每个主机进行定制。

在大型网络中，集中日志是关重要的。它能让海量信息变得可管理，而且运气好的话，可以防止违反网络机器安全的人员获取审计数据。黑客经常编辑系统日志来掩盖踪迹；如果日志信息一旦生成就被立即移走，就很难破坏。但要注意，任何人都可以调用 syslog 并从任何守护进程伪造日志记录。syslog 还使用 UDP 协议，其可靠性无法保证；消息可能会丢失。你的防火墙不应允许外部实体向你的 syslog 提交消息。

为你的日志服务器选择一个方案，最好是安全的且登录良好的。其他机器可以使用在中央维护的通用配置文件。因此，只需要维护两个 `syslog.conf` 文件。这种方法允许日志是完整的，同时又不会成为管理的噩梦。

某些大型站点可能想向日志层次结构添加更多级别。遗憾的是，syslog 只保留一次跳转源主机名称。如果“客户端将日志条目发送到主机 'server'，server 将其发送到主机 'master'”，那么 master 将看到数据来自 server 而不是客户端。

有关在网络上分发文件的更多信息请参阅第 18 章。

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_250_0.png)

## 软件使用 syslog

表 11.7 列出了一些使用 syslog 的程序、它们记录的 facility 和级别，以及每个程序的简要描述。某些行进行了阴处理以提高可读性。

| 程序 | facility | 级别 | 描述 |
| --- | --- | --- | --- |
| cron | cron | info | 任务调度进程 |
| ftpd | ftp | debug | FTP 守护进程 (ftpd) |
| imapd | mail | info | IMAP 邮件服务器 |
| inet | daemon | warning | 网络守护进程 |
| login | authpriv | err | 登录程序 |
| lpd | auth | err | 打印守护进程 |
| named | daemon | notice | 名称服务器 (DNS) |
| passwd | local0 | alert | 密码设置 |
| popper | mail | notice | POP 服务器 |
| sendmail | mail | notice | 邮件传输系统 |
| shutdown | auth | notice | 机 |
| sudo | local2 | err | UID 切换 |
| syslog | syslog | notice | syslog 系统 |
| tcpd | local7 | debug | TCP 接收器 |
| vmlinuz | kern | all | 内内核 |
| xinetd | inet | info | inet 变体 (Red Hat) |

## 调试 syslog
