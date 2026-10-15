
| daily, weekly, monthly | 按指定的计划轮转日志文件 |
| delaycompress | 压缩除当前和上一次最近脚本以外的所有版本 |
| endscript | 标记轮转前或轮转后脚本的结束 |
| errors emailaddr | 向指定的 emailaddr 发送错误通知邮件 |
| missingok | 如果日志文件不存在则不报错 |
| notemify | 如果日志为空则不进行轮转 |
| olddir dir | 指定将日志文件的旧版本放置在 |
| postrotate | 引入一个在日志轮转后运行的脚本 |
| prerorate | 引入一个在轮转前运行的脚本 |
| rotate n | 包括 n 个版本 |
| sharedscripts | 运行脚本 |
| size=logsize | 如果大小达到 logsize |

`logrotate` 通常配合运行。

# 1.4 Syslog：系统事件

`Syslog` 最初由 Eric Allman 编写，是一个全面的。它有两个重要的功能：将程序员从繁琐的机制中解放出来。`Syslog` 非常灵活。它允许根据来源对消息并路由到各种目的地：日志文件、终端或其他机器。`Syslog` 集中日志的能力是其最有价值的功能之一。`Syslog` 由三部分组成：

- `syslog`，守护进程（以及其配置文件）
- `openlog`，提交消息的库程序
- `logger`，从 shell 提交消息的用户命令

## 配置 syslog

在下面的讨论中，我们首先介绍 `syslog` 的配置，并要演示如何从

`syslogd` 在启动时启动并持续运行；无法通过 `inetd` 管理。感知 `syslog` 的程序使用 `syslog` 库将日志记录写入特殊文件 `/dev/log`，Unix 域接字。`syslogd` 从 `/dev/log` 读取消息，查询其配置文件并将每条消息分发到相应的目的地。

内核日志守护进程 `klogd` 负责从内核缓冲区检索消息并将其传递给 `syslog`。挂起信号（HUP，信号 1）会导致 `syslog` 关闭日志文件，重新读取配置文件并重新开始记录日志。如果你修改了 `/etc/syslog.conf`，必须向 `syslog` 发送挂起信号使更改生效。`TERM` 信号会导致 `syslog` 退出。

`syslog` 将进程 ID 写入文件 `/var/run/syslog.pid`。这种惯使得脚本向 `syslog` 发送信号变得简单。例如，以下命令发送挂起信号：

```
# kill HUP /bin/cat /var/run/syslog.pid
```

尝试修改 `syslog` 已打开的日志文件是不健康的，会导致不可预测的结果。正确的做法是将旧日志移开，以相同的所有权权限重建日志，然后向 `syslog` 发送 HUP 信号。此过程可以通过 `logrotate` 轻松实现，见第 205 页。

配置文件 `/etc/syslog.conf` 控制 `syslog` 的行为。它是一个格式简单的文本文件。空行和第一列带有井号 (`#`) 的行会被忽略。基本格式为：

```
- selector <Tab> action
```

例如，行

```
mail info /var/log/maillog
```

会将系统消息发送到 `/var/log/maillog` 文件。

选择器可以包含特殊关键字 `"*"` 和 `none`，分别表示所有或无。一个选择器可以包含多个由逗号分隔的设施。多个选择器还可以用分号组合。

## Linux 管理手册

通常情况下，选择器之间是逻辑或（OR）关系组合的；匹配任何选择器的消息都将执行该行的操作。然而，级别为 `none` 的选择器将排除列出的设施，无论同一行上的其他选择器如何规定。

以下是几种格式化和组合选择器的方法示例：

```
*level                   action
*facility1,facility2     action
*facility1 & facility2  action
*level                   action
*level,badfacility none  action
```

### 表 11.3 Syslog 设施名称

| 设施 (Facility) | 使用它的程序 |
| :--- | :--- |
| * | 除“mark”之外的所有设施 |
| auth | 安全和授权相关的命令 |
| authpriv | 敏感/隐私授权消息 |
| cron | cron 守护进程 |
| daemon | 系统守护进程 |
| ftp | FTP 守护进程，fptpd |
| kern | 内核 |
| local0-7 | 八种类型的本地消息 |
| lpr | 行打印机池化系统 |
| mail | sendmail 及其他邮件相关软件 |
| mark | 定期生成的时间戳 |
| news | Usenet 新闻系统 |
| syslog | syslog 内部消息 |
| user | 用户进程（若未指定则默认值） |
| uucp | 留给 UUCP，它不使用 |

> a. 授权消息是敏感的。`authpriv` 消息和 `auth` 消息都不应该是全局可读的。

`syslog` 本身产生时间消息，如果 `syslog.conf` 中出现了“mark”设施来指定它们的目的地，这些消息就会被记录。时间戳可以帮助你确定机器是在凌晨 3:00 到 3:20 之间崩溃的，而不仅仅是“过去的某个时候”。当你调试似乎定期发生的问题时，这些信息会有很大帮助。例如，许多站点在深夜清洁人员插上吸尘器导致断路器跳闸时经历过神秘的崩溃。

如果你的系统非常繁忙，其他日志消息通常提供足够的时间戳信息。但在凌晨，情况并不总是如此。

### 表 11.4 Syslog 严重级别（按严重程度降序）

| 级别 (Level) | 大致含义 |
| :--- | :--- |
| emerg | 恐慌状况 |
| alert | 紧急情况 |
| crit | 关键条件 |
| err | 其他错误情况 |
| warning | 警告消息 |
| notice | 值得调查的事 |
| info | 信息消息 |
| debug | 仅用于调试 |

消息的严重级别指定了其重要性。在 `syslog.conf` 文件中，级别表示消息必须具有的最低重要性才能记录。例如，来自主系统的级别为 `warning` 的消息将匹配选择器 `mail.warning *`，以及选择器 `notice`、`mail.info`、`mail.debug`、`* notice`、`*`、`debug`。如果 `syslog.conf` 指定将 mail info 消息记录到文件中，那么 `mail.warning` 消息将发送那里。

作为语法的改进，Linux 版本的 `syslog` 还允许在优先级级别前加上 `=` 和 `!` 字符，表示“仅限此优先级”和“此优先级及以上级别”。表 11.5 显示了示例。

### 表 11.5 syslog.conf 中优先级限定符的示例

| 选择器 (Selector) | 含义 |
| :--- | :--- |
| mail.info | 选择 info 优先级及以上的邮件相关消息 |
| mail=info | 仅选择 info 优先级的消息 |
| mail.info,mail.err | 仅选择 info、notice 和 warning 优先级 |
| mail:debug,mail!=warning | 选择除 warning 外的所有优先级 |

`action` 字段告诉要如何处理消息。表 11.6 列出了这些选项。

### 表 11.6 Syslog 操作

| 操作 (Action) | 含义 |
| :--- | :--- |
| filename | 将消息写入本地机器上的文件 |
| @hostname | 将消息写入 hostname 上的 syslogd |
| @ipaddress | 将消息写入 IP 地址为 ipaddress 的主机 |
| |fifo | 将消息写入命名管道 fifo |
| user1,user2,... | 如果用户已登录，则将消息写入用户屏幕 |
| * | 将消息写入所有当前登录的用户 |

a. 更多信息请参阅 info fifo。

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_246_0.png)

有关如何将主机名转换为 IP 地址的更多信息，请参见第 498 页。

如果使用了 filename（或 fifename）操作，名称应为绝对路径。如果你指定了一个不存在的文件，`syslogd` 将在第一次消息重定向到它时创建该文件。你可以在 filename 操作前加一个连字符 `-`，表示在写入每条日志条目后不对文件系统进行**同步 (synced)**。同步有助于在崩溃时准备尽可能多的日志信息，或者在磁盘吞吐量方面它是昂贵的的。

如果使用主机名而不是 IP 地址，则它必须通过 DNS 或 NIS 等转换机制进行解析。
