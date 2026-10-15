
如果你想将 `var` 的值赋给变量 `lcount`，可以按如下方式操作：

| Command | Environment |
|---|---|
| `lcount=$var` | `pdksh` and `bash` |
| `set lcount=$var` | `tcsh` |

### 位置参数

可以从命令行或另一个 shell 脚本向你的 shell 程序传递选项。

这些选项由 Linux 作为位置参数提供给 shell 程序，这些参数具有系统规定的特殊名称。第一个参数存储在名为 `1`（数字 `1`）的变量中，可以在程序中使用 `$1` 访问。第二个参数存储在名为 `2` 的变量中，可以在程序中使用 `$2` 访问，以此类推。在调用 shell 程序时，可以省略一个或多个编号较高的位置参数。

了解如何使用这些位置参数以及如何访问和从命令行检索变量对于开发更高级的 shell 程序是必要的。

### 位置参数的一个简单示例

例如，如果 shell 程序 `mypgm` 预期两个参数——例如名字和姓氏——你可以仅使用一个参数，即名字来调用 shell 程序。但是，你不能仅使用第二个参数，即姓氏来调用它。

这里有一个名为 `mypgm1` 的 shell 程序，它只接受一个参数（一个名字）并将其显示在屏幕上：

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

如果你按如下方式执行 `mypgm1`：

```
$ bash mypgm1
```

你将得到以下输出：

未提供姓名

然而，如果你按如下方式执行 `mypgm1`：

```
$ bash mypgm1 Sanjiv
```

你将得到以下输出：

你的名字是 Sanjiv

shell 程序 `mypgm1` 还展示了 shell 编程的另一个方面：Linux 内核提供给 shell 的内置变量。在 `mypgm1` 中，内置变量 `$#` 提供了传递给 shell 程序的位置参数的数量。你将在本章下一主要部分中进一步了解如何使用内置变量。

### 使用位置参数从命令行访问和检索变量

在脚本中使用位置参数，当你需要使用带有管道命令且要求复杂参数的命令行时，会很有帮助。如果这些命令不常用，包含位置参数的 shell 程序甚至会更加方便。例如，如果你将带有外接语音调制解调器的 Ubuntu 系统用作应答机，你可以编写一个脚本，发出命令来检索并播放语音消息。下面的命令行将已保存的声音文件（`.rmd` 或语音电话格式）转换，并将结果通过管道发送到系统音频设备：

```
#!/bin/sh
#### play voice message in /var/spool/voice/incoming
rmdtopvf /var/spool/voice/incoming/$1 | pvfspeed -s 8000 | \
pvftobasic >/dev/audio
```

然后，你可以使用这个脚本（可能名为 `pmm`）轻松地回放语音消息：

```
$ pmm name_of_message
```

包含位置参数的 shell 脚本通常用于自动化日常事务性工作，例如系统日志报告生成、文件系统检查、用户资源统计、打印机使用统计，以及其他系统、网络或安全管理任务。

### 使用简单脚本自动化任务

例如，你可以使用一个简单脚本来检查系统日志中的特定关键字。如果该脚本通过系统的调度表 `/etc/crontab` 运行，它可以帮助自动化安全监控。通过将现有 Linux 命令的输出能力与 shell 的语言功能相结合，你可以快速构建一个有用的脚本，来执行通常需要许多命令行才能完成的任务。例如，你可以创建一个名为 `greplog` 的简短脚本，如下所示：

```
#!/bin/sh
#
#### name: greplog
#### use: mail grep of designated log using keyword
#### version: v.01 08aug02
#
#### author: bb
#
#### usage: greplog [keyword] [logpathname]
#
#### bugs: does not check for correct number of arguments
#
#### build report name using keyword search and date
log_report="/tmp/$1.logreport.`date '+%m%d%y'`"
#### build report header with system type, hostname, date and time
echo "==================================================================" \
> $log_report
echo "   S Y S T E M   M O N I T O R   L O G" >>$log_report
echo uname -a >>$log_report
echo "Log report for" `hostname -f` "on" `date '+%c'` >>$log_report
echo "==================================================================" \
>>$log_report ; echo "" >>$log_report
#### record log search start
echo "Search for-->" $1 "starting" `date '+%r'` >>$log_report
echo "" >>$log_report
#### get and save grep results of keyword ($1) from logfile ($2)
grep -i $1 $2 >>$log_report
#### build report footer with time
echo "" >>$log_report
echo "End of" $log_report "at" `date '+%r'` >>$log_report
```

```
#### mail report to root
mail -s "Log Analysis for $1" root <$log_report
```

```
#### clean up and remove report
rm $log_report
exit 0
```

在这个示例中，脚本创建变量 `$log_report`，它将作为临时报告的文件名。关键字（`$1`）即命令行上的第一个参数，与当前日期一起用作文件名的一部分（也许更好的做法是使用 `$$` 而不是日期，这样会将脚本的 PID 作为文件扩展名追加）。接下来，将包含一些格式化文本的报告头、`uname` 命令的输出以及主机名和日期添加到报告中。然后记录搜索的开始时间，并将日志中与关键字匹配的所有内容添加到报告中。随后添加包含报告名称和时间的报告尾。报告以搜索词作为邮件主题发送给 `root`，并删除临时文件。

你可以手动运行该脚本，给它提供一个关键字和系统日志的路径名 `/var/log/messages`，来测试它，如下所示：

```
#### greplog FAILED /var/log/messages
```

请注意，你的系统应该正在运行 `syslogd` 守护进程。如果系统上发生了任何登录失败，`root` 操作员可能会收到一封类似下面这样的电子邮件：
