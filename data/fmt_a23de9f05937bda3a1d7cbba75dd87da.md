
# 第 11 章

```
20 uucp                               /var/spool
21 # 所有人接收紧急消息
22 #                                     
```

以井号 (`#`) 开头的行是注释。

项目 (`items`) 的一些有效条目包括：

- `*Everything` (全部)
- `uucp`
- `news` (新闻)
- `mail` (邮件)
- `kern` (内核)
- `authpriv` (隐私认证)
- `auth` (认证)
- `lpr`
- `cron`
- `user` (用户)

许多系统上的内核守护进程——`klogd`——可以仅为了记录内核消息而运行。

优先级字段的 10 个有效值按优先级从高到低的顺序排列为：

- `*emergency` (紧急)
- `*alert` (警报)
- `*crit` (严重)
- `*err` (错误)
- `*warning` (警告)
- `*notice` (通知)
- `*info` (信息)
- `*debug` (调试)
- `*Everything` (全部)
- `*none` (无)

记住，当你指定一个优先级时，该优先级代表最小值。消息会在该优先级以及任何更高的优先级处生成。如果你只想记录该优先级，可以使用等号 (`=`)。例如，你可以使用 `*=err /var/log/errors`。

如果你想排除一种特定类型的优先级但获取所有其他优先级，可以使用感叹号 (`!`)。例如，要记录除关键消息以外的所有新闻消息，可以使用：

```
news.*;;news.-crit
```

位置 (`location`) 字段可以是任何内容。一些有效条目包括：

- `*where` (何处)
- `/dev/console`—通知当前控制台用户
- `/var/log/{日志文件名称}`

因为 `/etc/syslog.conf` 文件是在 `syslogd` 启动时读取的，如果你对文件进行了更改，则必须重启守护进程使更改生效。守护进程在死亡后会自动重启，然后你可以通过将其杀死来强制它读取更改：

```
kill -HUP
```

```
kill -1
```

对 `syslogd` 进程的 `PID`（进程 ID）执行（这两个值相同，但一个是数字表示，另一个是符号）。你可以

通过运行 `ps -ef` 或查看文件 `/var/run/syslogd.pid` 中的值来查找 `syslogd` 的 `PID` 号。你也可以使用以下命令：

```
pidof syslogd
```

来获取进程的 `PID` 号。

## 需要了解的文件

你应该识别默认存在的若干日志文件。表 11.1 汇总了 `/var/log` 下的主要文件。

你应该了解一些与日志相关的可执行程序。第一个是 `logger`。使用该工具必须紧跟要写入的文件名和一条消息；它会将该消息插入日志文件中。例如，系统默认的消息为：

```
$pwd
/var/log
$ tail messages
Oct 16 14:40:00 noname CRON[3823]: (root) CMD (/sbin/rmmod -a)
Oct 16 14:42:01 noname CRON[3825]: (root) CMD
(( -x /usr/sbin/cronloop ) && /usr/sbin/cronloop Hourly)
Oct 16 14:45:00 noname CRON[3829]: (root) CMD (/sbin/rmmod -a)
Oct 16 14:50:00 noname CRON[3832]: (root) CMD (/sbin/rmmod -a)
Oct 16 14:55:00 noname CRON[3833]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:00:00 noname CRON[3853]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:05:01 noname CRON[3896]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:10:00 noname CRON[3921]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:15:00 noname CRON[3925]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:20:00 noname CRON[3934]: (root) CMD (/sbin/rmmod -a)
$ logger hey
$ tail messages
Oct 16 14:42:01 noname CRON[3825]: (root) CMD
(( -x /usr/sbin/cronloop ) && /usr/sbin/cronloop Hourly)
Oct 16 14:45:00 noname CRON[3829]: (root) CMD (/sbin/rmmod -a)
Oct 16 14:50:00 noname CRON[3832]: (root) CMD (/sbin/rmmod -a)
Oct 16 14:55:00 noname CRON[3833]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:00:00 noname CRON[3853]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:05:01 noname CRON[3896]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:10:00 noname CRON[3921]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:15:00 noname CRON[3925]: (root) CMD (/sbin/rmmod -a)
Oct 16 15:20:00 noname CRON[3934]: (root) CMD (/sbin/rmmod -a)
$
```

注意，每个条目都以日期和时间开头，随后是系统名称、调用者、冒号（`:`）和消息。

## 表 11.1 常见日志文件。

| 文件 | 用途 |
| :--- | :--- |
| `cron` | `cron` 守护进程生成的事件日志。 |
| `lastlog` | 显示每个用户最后的时间（由 `last` 命令读取）。 |
| `mail` or `maillog` | 邮件消息。 |
| `messages` | 大文件：默认情况下大多数事件都记录在此处。 |
| `news` or `news.all` | 显示新闻消息。 |
| `secure` | 提供安全信息。 |
| `spooler` | 缓存消息。 |
| `uucp` | 显示 `uucp` 事件。 |
| `wtmp` | 跟踪登录和注销；被 `last` 命令使用；是 `/var/run/utmp` 的对应文件。 |

你应该了解的下一个可执行程序是 `logrotate`。该工具读取配置文件并按指定压缩或删除日志文件。你使用 `gzip` 进行压缩，操作可以在每天、每周、每月或达到特定大小时进行。管理员随时可以手动归档、删除和压缩日志文件。`logrotate` 的唯一目的就是自动化这一过程。你可以配合该工具使用的命令有：

- `compress`
- `copytruncate`
- `create`
- `daily`
- `errors`
- `extension`
- `empty`
- `include`
- `mail`
- `mailfirst`
- `missingok`
- `monthly`
- `nocopytruncate`
- `nocreate`
- `delay`
- `nomail`
- `missingok`
- `olddir`
- `notempty`
- `postrotate`
- `rotate`
- `size`
- `weekly`

文本文件 `/var/log/logrotate` 显示该工具与其交互的文件状态。该文件的一个示例为：
