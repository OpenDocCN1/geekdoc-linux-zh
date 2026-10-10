
# 日志文件管理 439

举例来说，如果你希望搜索系统中来自特定命令的日志信息，你可以输入 `journalctl _COMM=` 并按 Tab 键，以查看系统中通过 journald 执行日志记录的所有可用命令，如下所示：

```
[root@server1 ~]# journalctl _COMM=
abrtd        dnsmasq     mtp-probe   sh        tgtd
anaconda     gnome-keyring-d network   smarthd   udisksd
avahi-daemon hd-idle-temp polkit-agent-he sssmd   umount
bash         journal2gelf  polkitd     sshd      userhelper
blueman-mechani journalctl pulseaudio ssadd be yunm
chronyd      krb5_child   qemu-system-x86 su
colord       libvirtd    sealert   sudo
crond        logger      sendmail  systemd
dbus-daemon  mcelog      troubleeshoo systemct- journal
```

要查看 cron 守护进程（crond）的日志，你可以运行命令 `journalctl _COMM=crond | less`，因为输出行数可能很多。然而，在排查与 cron 守护进程相关的问题时，缩小时间范围会更实用。以下命令显示当天 1:00 p.m.（13:00）到 2:00 p.m.（14:00）之间的 crond 日志条目：

```
[root@server1 ~]# journalctl _COMM=crond --since "13:00" --until "14:00"
-- Logs begin at Tue 2015-09-16 21:56:29 EDT, end at Tue 2015-10-14 20:43:32 EDT
Oct 14 13:50:58 server1 crond[457] : (CRON) INFO (RANDOM_DELAY will be scaled with factor 30% if used.)
Oct 14 13:50:59 server1 crond[457] : (CRON) INFO (running with inotify support)
[root@server1 ~]# _
```

`journalctl` 命令中使用的 时间格式遵循标准的 `YYYY-MM-DD HH:MM:SS`。因此，若要获取 2015 年 8 月 22 日 5:30 p.m.（17:30）之后的 crond 事件，你可以改为运行 `journalctl _COMM=crond --since "2015-08-22 17:30:00"` 命令。

如果你指定可执行文件的路径名或 PID，也可以查询与特定进程或守护进程相关的事件。例如，由于 Systemd 初始化守护进程的路径为 /usr/lib/systemd/systemd，且 PID 为 1，你可以运行 `journalctl /usr/lib/systemd/systemd` 命令或 `journalctl _PID=1` 命令来查看与 Systemd 初始化守护进程相关的事件。

### 管理日志文件和 Journald 数据库

虽然日志文件和 journald 数据库包含重要的系统信息，但随时间推移，它们可能会占用文件系统中不必要的空间。在使用 Systemd 的系统上，你可以通过取消注释并配置 /etc/systemd/journald.conf 中的 SystemMaxUse 行来限制 journald 数据库的大小。例如，SystemMaxUse=75M 将把数据库限制在 75MB，并且随着新事件记录，最旧的事件会被删除。为了防止重要的旧事件被覆盖，你可以创建一个执行相应 `journalctl` 命令的 shell 脚本，并将结果打印出来或保存到文本文件中。然后，你可以按照第 9 章中讨论的方法，配置 cron 守护进程定期执行此 shell 脚本。

对于 /var/log 目录内的日志文件，你可以定期清除其内容以回收文件系统中的空间。

![](img/c27875544958897d817484d558c208c8_469_0.png)

不要删除日志文件，因为其权限和所有者也会被移除。

在清除重要的日志文件之前，最好将它们保存到另一个位置或打印其内容以供将来参考。

要清除日志文件，请记住你可以使用 > 重定向符号。以下命令显示 /var/log/wtmp 日志文件在打印并清除前后的文件大小：

```
[root@server1 ~]# ls -l /var/log/wtmp
-rw-r-----  1 root  wtmp  21705 Aug 27 10:52 /var/log/wtmp
[root@server1 ~]# lp -d printer1 /var/log/wtmp
[root@server1 ~]# > /var/log/wtmp
[root@server1 ~]# ls -l /var/log/wtmp
-rw-m-----  1 root  wtmp  0 Aug 27 10:52 /var/log/wtmp
[root@server1 ~]# _
```

或者，你可以调度 logrotate 命令来备份和清除存储在 /etc/logrotate.conf 文件以及 /etc/logrotate.d 目录中的文件里的日志文件条目。`logrotate` 命令通常按循环方式重命名（或轮转）日志文件；日志文件将被重命名为包含数字或日期扩展名的形式，并且会创建一个新的日志文件来接收系统信息。你可以指定扩展名的类型以及 logrotate 保留的日志文件数量。如果 logrotate 配置为仅保留两份旧日志文件，那么经过两次日志轮转后，最旧的日志文件将被自动删除。

/etc/logrotate.conf 文件的一个示例如下面的输出所示：

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
# uncomment this if you want your log files compressed
#compress
# RPM packages drop log rotation information into this directory
include /etc/logrotate.d
# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
    monthly
    create 0664 root wtmp
    minsize 1M
    rotate 1
}
/var/log/btmp {
    missingok
    monthly
    create 0600 root btmp
    rotate 1
}
[root@server1 ~]# _
```

在上面的输出中，任何 # 字符表示注释，将被忽略。其他行表明，此文件中包含的日志文件以及 /etc/logrotate.d 目录中的所有其他文件（include /etc/logrotate.d）中的日志文件每周轮转一次，除非另有指定（weekly），使用日期扩展名（dateext），并且最多保留 4 周的日志文件（rotate 4）。

/etc/logrotate.conf 文件底部有两条条目覆盖这些值。对于文件 /var/log/wtmp，此轮转每月发生一次，而不是每周，且仅当日志文件大小大于 1MB 时才进行。仅保留一份旧日志文件，新创建的日志文件具有 0664（rw-rw-r--）权限，所有者为 root，组为 wtmp。对于文件 /var/log/btmp，此轮转每月发生一次，而不是每周，如果日志文件缺失则不报告错误。仅保留一份旧日志文件，新创建的日志文件具有 0600（rw-------）权限，所有者为 root，组为 utmp。

/etc/logrotate.conf 中的大多数轮转信息被存储在 /etc/logrotate.d 目录中的文件覆盖。以文件 /etc/logrotate.d/psacct 为例：

```
[root@server1 ~]# cat /etc/logrotate.d/psacct
# Logrotate file for psacct RPM

/var/account/psacct {
    compress
    delaycompress
    notifempty
    daily
    rotate 31
    create 0600 root root
    postrotate
        if /etc/init.d/psacct status >/dev/null 2>&1; then
        /usr/sbin/accton /var/account/psacct
        fi
    endscript
}
[root@server1 ~]# _
```

此文件表明，/var/account/psacct 文件每天轮转一次，但前提是它不为空，并且新日志文件的所有者为 root 用户/组，权限为 0600（rw-------）。最多保留 31 个旧日志文件并对其进行压缩，但仅在下次轮转时进行（delaycompress）。此外，如果 /etc/init.d/psacct status 命令返回 true，则每次轮转后都会运行 /usr/sbin/accton /var/account/psacct 命令。

在大多数 Linux 系统上，logrotate 实用程序通过文件 /etc/cron.daily/logrotate 自动调度每天运行；然而，你可以选择在命令提示符下输入命令 logrotate /etc/logrotate.conf 手动运行它。

随着时间推移，logrotate 命令会为每个日志文件生成多个副本，如下面的 /var/log 目录列表所示：

```
[root@server1 ~]# ls /var/log
anaconda.log      dmesg             ppp
anaconda.program.log    dmesg.old     prelink
anaconda.storage.log    gdm             sa
anaconda.syslog         httpd           samba
anaconda.xlog           jetty           sa-update.log
anaconda.yum.log        lastlog         secure
audit                 mail            secure-20150808
BackupPC            maillog           secure-20150818
bittorrent          maillog-20150808  secure-20150823
boot.log          maillog-20150818  setroubleshoot
```
