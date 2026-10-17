
`user.emerg`				*

# log what the authentication system is doing

`auth.info`					`/var/log/authlog`

# local facilities

# local1 is used for the baseline skripts

`local1.info`				`/var/log/baselinelog`

# local2 - local7 unused at the moment

# if used, document usage here and in system docs

清单 5.11 中的示例包含一些需要解释的特殊情况。指令 `mark.debug /var/adm/messages` 的意思是将内容为 -- MARK -- 的消息写入 `/var/adm/messages`。间隔 `[20 分钟]` 通常编译到 `syslog` 二进制文件中。有两个原因导致这种配置。第一，无论系统负载如何，每 20 分钟都会有一条消息。负载非常低的机器通常只会在偶尔时写入 syslog；此设置允许你查看 syslog 进程是否仍在运行。第二，命令 `grep MARK /var/adm/messages` 应该显示标记条目的连续列表，从而让你确定 syslog 是否一直处于运行状态。如果入侵者试图通过禁用 syslog 或修改日志文件来隐藏其存在，那么其中一个标记可能丢失的可能性很小。这不是真正的监控，但每个细节都很重要。条目 `user.emerg` 看起来有点过分，但如果用户空间中的程序开始异常行为甚至崩溃，那么系统的所有用户都应该知道并决定是否需要该程序的存在。设施 `local1` 用于基线脚本的消息。记住：清单 3.19 使用了 `user.crit`，但只有一个原因；此设施通常会将带有 crit 的消息写入系统范围的日志文件，从而确保命令在示例中有效。因为你现在知道如何自定义 syslog 的行为，所以你应该使用 `local0-7` 设施。

以下是 syslog 配置的一些提示。你应该始终确保使用 `touch` 命令创建要写入的文件（如果它们不存在）；syslog 不会创建文件。测试对 `syslog.conf` 的更改以避免丢失重要消息。程序将在重新启动时或向进程发送 `HUP` 信号时重新读取配置。你应该始终通过 `logger` 程序向已更改或添加的设施发送消息来测试新配置。如果此测试失败，你应该尝试纠正错误并再次测试。如果找不到错误，你应该启用旧的工作配置，并在具有相同 OS 版本的测试系统上测试不工作的配置。寻找此配置中错误的一个提示：当你重新输入配置时，拼写错误就会显现出来，复制配置来查找错误通常没有帮助。

你需要确保监控日志文件的增长，尤其是在更改配置之后。`/var` 目录必须有足够的空间来存储数据，并且应留出一些剩余空间。文件应根据文件的重要性复制到系统上的另一个位置或不同的系统。另一个选择是将文件存储在磁带上或写入 CD/DVD。你应始终使用提供的机制来轮转日志；这意味着使用 `logrotate` 的变体（几乎所有 *NIX 系统都可用）或 Solaris 上的自带软件如 `logadm`。由于 `logrotate` 可在 Solaris、HP-UX、GNU-Linux 和 AIX 上使用（参见附录 B），作者提供了关于其配置的示例（参见清单 5.12）。需要轮转的日志文件是 `/var/log/localmessages`。配置通常存储在 `/etc/logrotate.d` 中，这是 `logrotate` 的默认设置。

### LISTING 5.12 Configuration for logrotate to Rotate /var/log/localmessages

```
# rotates the logfiles created by local facility

/var/log/localmessages {

    compress

    daily

    dateext

    rotate 31

    create 640 root root

    postrotate

        kill -HUP `cat /etc/syslog.pid`

    endscript

}
```

配置的含义如下：`compress`——旧日志文件将被压缩；`daily`——配置应每日执行；`dateext`——轮转后日志文件的名称将附加日期；`rotate 31`——如果文件被轮转 31 次，则将被删除；`create 640 root root`——将创建具有指定所有者和权限的新文件；`postrotate` 与 `endscript` 之间的命令将在轮转后执行。你必须确保弄清楚如何让相应的 syslog 守护进程重新读取配置。所示命令应在所有将 `syslog.pid` 文件存储在 `/etc` 中的系统上工作。某些程序变体可以用命令 `/etc/init.d/syslog reload` 或类似命令重新启动（手册页通常包含详细信息）。

```
LOGPATH=/var/log
LOGFILES="local1log local1log local2log"

if test -d $LOGPATH
then
    cd $LOGPATH
    for LOG in $LOGFILES; do
        test -f $LOG.6 && mv $LOG.6 $LOG.7
        test -f $LOG.5 && mv $LOG.5 $LOG.6
        test -f $LOG.4 && mv $LOG.4 $LOG.5
        test -f $LOG.3 && mv $LOG.3 $LOG.4
        test -f $LOG.2 && mv $LOG.2 $LOG.3
        test -f $LOG.1 && mv $LOG.1 $LOG.2
        test -f $LOG.0 && mv $LOG.0 $LOG.1
        test -f $LOG && mv $LOG $LOG.0
    done
    sleep 30
    kill -HUP `cat /etc/syslog.pid`
fi

# EOF
```

你可以用此脚本作为基础并根据需要对其进行自定义。如果日志文件需要保存更长时间，则可以扩展 `for` 循环或使用清单 3.23 中的脚本作为模板。

如前所述，你应始终监控日志文件。问题在于检查所有文件以查找特定内容所需的时间。有商业和开源产品可以使此任务变得稍微容易一些，但这些产品也需要进行管理和配置，这同样需要时间。解决这一困境的一种可能方案是使用一个小型脚本来监控被认为足够重要的日志文件。一个简单的脚本本身就可以基于轮转频率产生大量数据。例如，如果包含失败登录的日志文件每周仅轮转一次，那么这些失败登录的输出在周内会不断增长，从而变得越来越难以阅读。清单 5.15 包含了一个此类监控脚本的示例。

### LISTING 5.15 A Script to Monitor the File authlog

```
#!/usr/bin/perl

# $Id: chkauth.pl,v 1.1 2004/09/03 09:00:36 erikk Exp erikk $

########################################

#

#    file:      chkauth.pl

#

#   purpose:      scan the contents of authlog

#                 for failed attempts

#

#   author:        Erik Keller

#

#   parameters:    none

#

########################################
# Variables
$WORKDIR = "/var/log";
$LOGFILE = "authlog";

# open the file
open(MY_LOG, "$WORKDIR/$LOGFILE")
    or die "$0: couldn't open log file: $!";

while(<MY_LOG>)
{
    chop;
    if(/failed/)
    {
        print "$\n";
    }
}

close(MY_LOG);
# EOF
```
