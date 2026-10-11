
## 第 10 章 常见管理任务

你可以使用 `systemd-cat` 命令或 `logger` 命令向 journal 数据库添加日志条目；例如，你可以在脚本中使用 `echo "Backup of $DIR completed successfully at \`date\` | systemd-cat` 或 `logger "Backup of $DIR completed successfully at \`date\`"` 来向 journal 数据库记录一条消息，表明 `$DIR` 变量中的目录备份已在特定时间完成。`logger` 命令也可以用于在运行系统日志守护进程的系统上添加日志条目；只需在 `logger` 命令旁边指定 `-p facility.priority` 选项来控制事件记录的方式。

## 管理日志文件和 journal 数据库

尽管日志文件和 journal 数据库包含了重要的系统信息，但它们可能会在文件系统中占用不必要的空间，因为 journal 默认配置为使用持久存储。然而，你可以取消注释并配置 `/etc/systemd/journal.conf` 中的 `Storage=volatile` 行，以确保事件只存储在内存中，而不是文件系统上。或者，你也可以通过取消注释并配置 `/etc/systemd/journal.conf` 中的 `SystemMaxUse` 行来限制 journal 在文件系统中存储事件的空间。例如，`SystemMaxUse=75M` 将数据库限制为 75MB，当新事件产生时，旧的事件将被删除。为了防止关键的旧事件被覆盖，你可以创建一个脚本，执行相应的 `journalctl` 命令并打印结果或将其保存到文本文件中。

然后，你可以按照第 9 章讨论的那样，配置 `cron` 守护进程定期执行此脚本。

对于 `/var/log` 目录下的日志文件，你可以定期清除其内容以释放文件系统空间。

不要删除日志文件，因为权限和所有权也会被删除。
在清除重要日志文件之前，良好的做法是将它们保存到不同的位置或打印内容以备后参考。

要清除日志文件，请记住你可以使用 `>` 重定向符号。以下命令显示了 `/var/log/boot.log` 文件在打印和清除之前的大小：

```
[root@server1 ~]# ls -l /var/log/boot.log

-rw---- 1 root root 21705 Aug 27 10:52 /var/log/
boot.log

[root@server1 ~]# lp -d printer1 /var/log/boot.log

[root@server1 ~]# ls -1 /var/log/boot.log

-rw---- 1 root root 0 Aug 27 10:52 /var/log/
boot.log
```

或者，你可以通过调度 `logrotate` 命令来备份和清除存储在 `/etc/logrotate.conf` 文件以及 `/etc/logrotate.d` 目录下的文件的日志条目。`logrotate` 命令通常循环地重命名日志文件；日志文件将被重命名为包含数字或日期的扩展名，并创建一个新的日志文件来接收系统信息。你可以指定扩展类型以及保留的日志文件数量。如果配置为只保留两份旧日志文件，那么在两次轮转之后，最旧的日志将被删除。

`/etc/logrotate.conf` 的示例输出如下：

```
[root@server1 ~]# cat /etc/logrotate.conf
# see "man logrotate" for details
# rotate log files weekly
weekly
# keep 4 weeks worth of backlogs
rotate 4
# create new (empty) log files after rotating old ones
create
# use date as a suffix of the rotated file
dateext
# uncomment this if you want your log files
#compress
# RPM packages drop log rotation information into this directory
include /etc/logrotate.d
```

```
# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
  monthly
  create 0664 root utmp
  minsize 1M
  rotate 1
}
/var/log/btmp {
  missingok
  monthly
  create 0600 root utmp
  rotate 1
}
```

在前面的输出中，任何 `#` 字符均表示注释并被忽略。其他行表示该文件中包含的日志文件，以及 `/etc/logrotate.d` 目录中的所有其他文件 `include /etc/logrotate.d` 除非指定 `weekly`，否则将使用日期扩展 `dateext` 每周轮转一次，并保留 4 周的日志文件 `rotate 4`。

`/logrotate.conf` 文件末尾有两个覆盖这些值的条目。对于 `/var/log/wtmp` 文件，这种轮转每月发生一次而非每周，仅当日志文件大小大于 1MB 时发生。只保留一份旧日志文件，新日志文件的权限为 0664(rw-rw-)，所有者为 root，组为 utmp。对于 `/var/log/btmp` 文件，轮转每月发生一次而非每周，如果日志文件缺失则不报告错误。只保留一份旧日志文件，新日志文件的权限为 0600 (rw-------)，所有者为 root，组为 utmp。

`/etc/logrotate.conf` 中的大部分轮转都被 `/etc/logrotate.d` 目录中的文件覆盖。以 `/var/log/psacct` 文件为例：

```
[root@server1 ~]# cat /etc/logrotate.d/psacct
# Logrotate file for psacct
/var/log/psacct {
  compress
  daily
  rotate 7
  create 0600 root root
  postrotate
    /usr/sbin/killall -HUP psacct
  endscript
}
```

## 显示 `/etc/passwd` 文件的示例

```
[root@server1 ~]# cat /etc/passwd
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/bin/sync
shutdown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
```
