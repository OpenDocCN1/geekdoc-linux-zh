
```
#
# Filter definitions
#
f_iptables { facility(kern) and match("IN=") and match("OUT="); }
f_console { level(warn) and facility(kern) and not filter(f_iptables) or level(err) and not facility(authpriv); };
f_newsnotice { level(notice) and facility(news); };
f_newcrit { level(crit) and facility(news); };
f_newerr { level(err) and facility(news); };
f_news { facility(news); };
...
f_messages { not facility(news, mail) and not filter(f_iptables); };
...
```

如你所见，设施和优先级（`level`）可以在过滤器中使用。然而，也可以根据被记录的行内容进行过滤，如上面的 `f_iptables` 过滤器所示。

使用 `"and"`, `"or"` 和 `"not"` 组合表达式允许你创建非常特定的过滤器。

## 目的地 (Destinations)

目的地定义了可以记录到何处。通用语法如下：

```
destination <identifier> {
destination-driver(params);
destination-driver(params); ... };
```

可能的目的地是文件、fifos、套接字、特定用户的 tty、程序或其他主机。

`/etc/syslog-ng/syslog-ng.conf` 的示例如下所示：

```
destination console {
file("/var/log/messages");
};
```

## 日志路径 (Log Paths)

日志路径是消息写入点，取决于源、过滤器和目的地。通用语法如下：

```
log { source(); filter(); destination(); };
```

`/etc/syslog-ng/syslog-ng.conf` 中的以下条目定义了日志路径：

```
log {
    source src;
    filter f_messages;
    destination d1;
};
```

| 表 6-4 (续) | 日志文件 | 描述 |

| --- | --- | --- |

| | `/var/log/lastlog` | 该文件包含关于用户最后登录的信息，包括从何处登录以及持续多久。你只能使用 `lastlog` (`/usr/bin/lastlog`) 命令查看其内容。 |

## 归档日志文件 (logrotate)

确保日志文件不会过大且占用系统过多的空间是非常关重要的。因此，`logrotate` (`/usr/sbin/logrotate`) 程序会自动监控日志文件的大小和时长。

该程序由 cron 守护进程 `/etc/cron.daily/logrotate` 每天运行一次。程序会检查其配置文件中列出的所有日志文件，并根据配置对相应文件执行任何所需的操作。

你可以在文件中配置设置，以指示文件是否应该在定期间隔内或在达到特定大小时被压缩或删除。

你还可以配置在指定时间段内保留多少个日志文件的压缩版本。日志文件还可以通过电子邮件转发。

`logrotate` 的配置文件为 `/etc/logrotate.conf`，它包含了通用配置设置。以下是 `logrotate.conf` 的示例：

```
# 详情请参见 "man logrotate"
# 每周轮转日志文件
weekly

# 保留 4 周的备份
rotate 4

# 在轮转旧文件后创建新的（空）日志文件
create

# 如果你想压缩日志文件，请取消此行的注释
#compress

# 取消这些行的注释将压缩方式切换为 bzip2
#compresscmd /usr/bin/bzip2
#uncompresscmd /usr/bin/bzip2

# RPM 包会将日志轮转信息放入此目录
include /etc/logrotate.d
```

下表描述了文件中的选项：

### 表 6-5

| 选项 | 描述 |

|---|---|

| weekly | 日志文件每周创建或替换一次。 |

| rotate 4 | 除非指定了 rotate 选项，否则旧文件将被删除。在本示例中，保留日志文件的最后 4 个版本 (`rotate 4`)。 |

| create | 将旧文件以新名称保存，并创建一个新的空日志文件。 |

| compress | 如果激活了 compress 选项，副本将以压缩形式存储。 |

许多 RPM 包包含供 `logrotate` 评估的预配置文件，它们存储在 `/etc/logrotate.d/` 中。`logrotate` 通过 `/etc/logrotate.conf` 中的 `include /etc/logrotate.d` 条目读取该目录下的文件。

`logrotate.d` 文件中的任何设置都将覆盖 `logrotate.conf` 中的通用设置。

所有必须监控的文件都必须列出。这是通过 `/etc/logrotate.conf` 中的项目（如 `/var/log/wtmp [options]`）或单独的配置文件来实现。

以下是 `/etc/logrotate.d/` 中 syslog 文件的示例：

```
#
# 注意，如果使用 syslog-ng 作为日志守护进程，
# 仅在此文件中更改日志文件权限是不够的。
# 还需要在 syslog-ng 配置
# /etc/syslog-ng/syslog-ng.conf 中指定权限。
#
/var/log/warn /var/log/messages /var/log/allmessages
/var/log/localmessages /var/log/firewall {
compress
dateext
maxage 365
rotate 99
missingok
notifyempty
size +4096k
create 640 root root
sharedscripts
postrotate
    /etc/init.d/syslog reload
endscript
..
```

`/etc/logrotate.d/` 中的 syslog 和 syslog-ng 文件包含了配置如何处理由 syslog (`syslog-ng`) 写入文件的设置。

以下描述了文件中的选项：

| 选项 | 描述 |

| --- | --- |

| size +4096k | 文件将不会每周轮转，而是在当它们的大小达到 4096 KB 时立即轮转。 |

| rotate 99 | 将保留每个文件的 99 个版本。 |

| compress | 旧的日志文件将被压缩。 |

| maxage 365 | 一只要压缩文件超过 365 天，就会被删除。 |

| nonempty | 如果日志文件为空，则不进行轮转。 |

| create 640 root | 轮转后创建新的日志文件，并指定所有者、组和权限。 |

| postrotate ... endscript | 轮转后可以调用脚本。例如，某些服务在日志文件更改后必须重启。 |

在本示例中，syslog 守护进程将在轮转后重新读取其配置文件 (`/etc/init.d/syslog reload`)。对于 `logrotate` 来说，由于脚本对 syslogd 和 syslog-ng 是相同的，因此使用哪一个并不重要。

大多数需要监控日志文件的服务带有预配置文件，因此通常只需要进行微调。

要获取所有可能选项的完整列表，请输入 `man logrotate`。

![](img/84d12236ddfe17cc29fd21173b9904ac_303_0.png)

## 练习 6-2 管理系统日志

在此练习中，你将练习配置 `syslog-ng` 和 `logrotate`。

你将在练习集中找到此练习。

（练习结束）

## 目标 3 监控登录活动

作为管理员，你最关键的任务之一是确保日志文件不会过大且占用系统过多的空间。你最关键的任务之一是监控系统中的登录活动，这可能意味着安全风险。通过 `syslog/messages` 等文件可以提供关于登录活动（logins）的详细信息。你可以使用以下命令来监控登录活动：

- `who` 命令显示当前登录的用户。你可以使用以下命令来监控登录活动：

- `w` 命令显示当前登录的用户以及正在做什么。它提供了更详细的信息。

- `last` 命令显示最后登录的信息。你可以使用以下命令来监控登录活动：

- `lastlog` 命令格式化并显示最后登录日志文件 (`/var/log/lastlog`) 的内容。显示登录名、端口和最后登录时间。

# 监控 SUSE Linux Enterprise Server 10

不带选项输入命令将按数字 ID 排序显示条目。
