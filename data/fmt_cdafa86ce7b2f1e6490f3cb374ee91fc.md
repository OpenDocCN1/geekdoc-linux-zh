
```bash
#!/bin/bash

# Clean nonexistent log entries from status file
/var/log/logrotate.status | ...
# Clean nonexistent log entries from status file
cat /var/log/logrotate.status | ...
status | touch status | head -1 status > status.cleansed
'sed' status | while read logfile date; do
[ -e "$logfile" ] && echo "$logfile $date"
done > status.clean
mv test -x /usr/sbin/logrotate || exit
/usr/sbin/logrotate /etc/logrotate.conf
```

如果你现在还不理解脚本中的所有内容，不用担心。你不需要理解`logrotate`就可以做你想做的事情。你可以在第 14 章“自动化任务和 Shell 脚本”中了解更多关于`bash`和 shell 脚本的信息。

现在重要的行是最后一行，它列出了`logrotate`配置文件的位置。以下是`/etc/logrotate.conf`的默认内容：

```
# see "logrotate" for details

# rotate log files weekly
# use the syslog group by default, since this is the owning group
# of /var/log/syslog.
su root syslog
# keep 4 weeks' worth of logs
rotate 4
# create new (empty) log files after rotating old ones
create
```

```
# uncomment if you want your log files compressed
# compress
# packages drop log rotation information into this directory
/etc/logrotate.d
# no packages drop log rotation or btmp - we'll rotate them here
/var/log/wtmp {
    syslog
    monthly
    create 0664 utmp
    rotate 1
}
/var/log/btmp {
    missing
    monthly
    create 0660 utmp
    rotate 1
}
# system-specific logs may be configured here
```

该文件包含有用的注释，其可配置的内容也很直接。如果你阅读该文件，你已经对变体细节有相当准确的猜测。正如文件中的第一条注释所说，`logrotate`的主页面对你可以咨询的一切都有解释，如果它尚不清楚。

一个有趣的条目显示，软件包会将日志轮转信息放入`/etc/logrotate.d`。这值得更仔细地查看。该目录包含一个配置文件，用于使用软件包管理器安装的应用程序，并且日志信息文件以它们控制的日志文件的应用程序命名。让我们看两个例子。第一个是`apt`，即软件包管理器：

```
/var/log/apt/term.log {
    rotate 12
    monthly
    compress
    missingok
    notempty
}
/var/log/apt/history.log {
    rotate 12
    monthly
    compress
    missingok
    notempty
}
```

有两个条目，每个条目对应`apt`创建和使用的不同日志文件。条目定义了要保留多少旧日志文件，`logrotate`会多频繁地轮转日志，是否压缩日志文件，日志文件丢失是否可以，以及文件为空时是否轮转。同样很直接。以下是更复杂的示例，针对`rsyslog`，即系统日志记录：

```
/var/log/syslog
{
    rotate 7
    daily
    missingok
    notempty
    delaycompress
    compress
    postrotate
        reload syslog >/dev/null 2>&1 || true
    endscript
}
```

```
/var/log/mail.info
/var/log/mail.warn
/var/log/mail.err
/var/log/mail.log
/var/log/daemon.log
/var/log/kern.log
/var/log/auth.log
/var/log/user.log
/var/log/lpr.log
/var/log/cron.log
/var/log/debug
/var/log/messages
{
    rotate 4
    weekly
    missingok
    notifempty
    compress
    delaycompress
    sharedscripts
    postrotate
        reload syslog >/dev/null 2>&1 || true
    endscript
}
```

`logrotate`的 man 手册定义了这些配置文件中使用的所有命令，但其中许多你可能已经很清楚了。以下是其中最重要的一些：

- `rotate` — 定义任何时候保留多少个日志
- `interval` — 定义轮转日志的频率；实际设置将是`daily`、`weekly`、`monthly`或`yearly`
- `size` — 定义日志文件在被轮转前可以变得多大；这会覆盖上面的时间设置，其格式为数字和单位，例如`size 512k`或`size 128M`或`size 100G`
- `compress` — 配置日志文件将被压缩
- `nocompress` — 配置日志文件不会被压缩

比所有单独的选项更重要的是要涵盖的内容，你可以在`man`手册中查找，这些特定应用程序的单独配置文件将覆盖`/etc/logrotate.conf`中的默认设置。如果在该文件中为设置分配了一个值，它将被所有受`logrotate`影响的应用程序使用，除非`/etc/logrotate.d`中的应用程序特定文件包含相同的设置。

## 图形化进程和系统管理工具

GNOME 和 KDE 桌面环境提供了一套丰富的网络和系统监控工具。图形界面元素，例如菜单和按钮，以及图形输出，包括计量和实时负载图表，使这些工具易于使用。这些客户端需要 X 会话，在某些情况下需要`root`权限，已包含在 Ubuntu 中。

如果你在服务器上运行时在本地查看工具，你必须在本地机器上正确安装和配置 X。虽然一些工具可用于远程监控系统或本地挂载的文件系统，但你必须正确配置 X11 环境变量，例如`$DISPLAY`，以使用软件或在连接到远程时使用`ssh`客户端的`-x`选项。

### 系统监视器

系统监视器是一个信息丰富、易于使用和理解且非常有用的图形监控工具。它具有关于正在运行的进程、可用资源和本地文件系统的信息标签。

### Conky

Conky 是一个高度可配置、相当复杂的系统监视器，对系统资源占用很低，可以提供几乎任何信息。缺点是你需要学习如何配置它。仅从软件仓库安装 Conky 只是开始。然而，对于那些希望在桌面上显示特定信息的人来说，它是无价的，值得花时间弄清楚。我们在这里给出一个示例，要真正欣赏 Conky 的强大功能、灵活性和可能性，请访问 https://github.com/brdmndthmw/conky。

Conky 使用文本文件进行配置，并使用简短脚本启动。图 16.1 中的示例来自 Matthew 在其工作站上的个人配置，旨在作为入门的简单示例。

![](img/cc25c1772b156472bdf9ab1775163582_351_0.png)

图 16.1 你可以使用 conky 来实时提供有关系统当前的信息。这在很小的空间内包含了大量信息。此设置不如你在之前链接中看到的一些设置漂亮，几乎所有这些设置都由编写配置的人免费公开了其设置细节。

在此示例中，Matthew 使用两个文件运行 Conky。第一个名为`conkyrc`的文本文件包含了图 16.1 中显示内容的配置细节：
