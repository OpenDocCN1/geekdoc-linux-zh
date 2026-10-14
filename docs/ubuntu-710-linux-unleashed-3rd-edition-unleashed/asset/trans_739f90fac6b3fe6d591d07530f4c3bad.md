

这是一个名为 mypgm1 的 shell 程序，它只接受一个参数（姓名）并将其显示在屏幕上：

```
#!/bin/sh
#Name display program
if [ $# -eq 0 ]
then
    echo "Name not provided"
else
    echo "Your name is $1"
fi
```

如果按如下方式执行 mypgm1，

```
$ bash mypgm1
```

你会得到以下输出：

```
Name not provided
```

然而，如果按如下方式执行 mypgm1，

```
$ bash mypgm1 Sanjiv
```

你会得到以下输出：

```
Your name is Sanjiv
```

shell 程序 mypgm1 还说明了 shell 编程的另一个方面：由 Linux 内核提供给 shell 的内置变量。在 mypgm1 中，内置变量 $# 提供传递给 shell 程序的位置参数数量。你将在本章的下一个主要部分了解更多关于使用内置变量的信息。

## 使用位置参数从命令行访问和检索变量

如果需要在使用管道命令且需要复杂参数的命令行中使用，脚本中使用位置参数会很有帮助。如果命令很少使用，包含位置参数的 shell 程序会更方便。

例如，如果你使用附带语音调制解调器的 Ubuntu 系统作为应答机，你可以编写一个脚本来发出检索并播放语音消息的命令。以下行将保存的音频文件（.rmd 或语音电话格式）转换为并将结果传输到系统的音频设备：

```
#!/bin/sh
# play voice message in /var/spool/voice/incoming
rmdtopvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 | \
pvftobasic >/dev/audio
```

然后就可以使用此脚本（也许命名为 pmn）轻松播放语音消息：

```
$ pmn name_of_message
```

包含位置参数的 shell 脚本通常用于自动化例行和琐碎的工作，例如系统日志报告生成、文件系统检查、用户资源核算、打印机使用核算以及其他系统、网络或安全管理任务。

## 使用简单脚本自动化任务

你可以使用一个简单的脚本，例如检查系统日志中的某些关键字。如果脚本通过系统的调度表 /etc/crontab 运行，它可以帮助自动化安全监控。通过将现有 Linux 命令的输出功能与 shell 的语言功能结合起来，你可以快速构建一个有用的脚本来执行通常需要多条命令行的任务。例如，你可以创建一个名为 greplog 的简短脚本，如下所示：

```
#!/bin/sh
#
# name: greplog
# use: mail grep of designated log using keyword
# version: v.01 08aug02
#
# author: bb
#
# usage: greplog [keyword] [logpathname]
#
# bugs: does not check for correct number of arguments
#
# build report name using keyword search and date
log_report="/tmp/$1.logreport.`date '+%m%d%y'`"

# build report header with system type, hostname, date and time
echo "============================================================" \
>>$log_report
echo "          S Y S T E M   M O N I T O R   L O G" >>$log_report
echo `uname -a` >>$log_report
echo "Log report for: `hostname -f` on `date '+%c'`" >>$log_report
echo "============================================================" \
>>$log_report ; echo "" >>$log_report

# record log search start
echo "Search for->" $1 "starting" `date '+%r'` >>$log_report
echo "" >>$log_report
```

```
# get and save grep results of keyword ($1) from logfile ($2)
grep -i $1 $2 >>$log_report

# build report footer with time
echo "" >>$log_report
echo "End of $log_report at `date +%i`" >>$log_report

# mail report to root
mail -s "Log Analysis for $1" root <$log_report

# clean up and remove report
rm $log_report
exit 0
```

在此示例中，脚本创建了变量 `$log_report`，它将是临时报告的文件名。命令行上的第一个参数和关键字 `$1` 与当前日期一起用作文件名的一部分（也许更好的做法是使用 `$$` 而不是日期，这将把脚本的 PID 作为文件扩展名附加）。接下来，包含一些格式化的文本、uname 命令的输出以及主机名和日期的报告头被添加到报告中。然后记录搜索的开始，并将日志中关键字的任何匹配项添加到报告中。然后添加包含报告名称和时间的页脚。报告将以搜索词作为邮件主题发送给 root，并删除临时文件。

你可以通过手动运行脚本并向其提供关键字和系统日志的路径名 `/var/log/messages` 来测试脚本，如下所示：

```
# grep log FAILED /var/log/messages
```

请注意，你的系统应正在运行 syslog 守护进程。如果你的系统发生了任何登录失败，root 操作员可能会收到类似这样的电子邮件：

```
Date: Thu, 23 Oct 2003 16:23:24 -0400
From: root <root@stinkpad.home.org>
To: root@stinkpad.home.org
Subject: FAILED

============================================================
                 S Y S T E M   M O N I T O R   L O G
Linux stinkyp 2.4.22-1.2088.1pl #1 Thu Oct 9 20:21:24 EDT 2003 i686 i686 i386
+GNU/Linux
Log report for stinkpad.home.org on Thu 23 Oct 2003 04:23:24 PM EDT
============================================================

Search for-> FAILED starting 04:23:24 PM
```

