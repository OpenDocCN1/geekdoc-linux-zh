
# 在 Shell 脚本中使用变量

本书的这一部分节将继续讨论 shell 变量的使用。这些信息将帮助你在 shell 脚本中定义、赋值和使用变量。`位置参数`部分将展示如何访问和使用持有来自命令行参数的变量。Linux shell 支持功能完整的编程语言，因此可以处理三种类型的变量：

- `环境变量`是系统环境的一部分，你可以在 shell 程序中使用它们。可以定义新变量，某些变量（如 `PATH`）也可以在 shell 程序中修改。
- `内置变量`（例如命令行中使用的选项，被 shell 解释为位置参数）由 Linux 提供。与环境变量不同，你无法修改它们。
- `用户变量`是在你编写 shell 脚本时定义的。你可以在 shell 程序中使用并修改它们。

shell 编程与其他编程语言的一个主要区别在于，在 shell 编程中，变量并不是典型的——也就是说，你不需要指定一个变量是数字还是字符串等。

## 给变量赋值

假设你想使用一个名为 `lcount` 的变量来统计 shell 程序中循环的迭代次数。你可以如下方式声明并初始化该变量：

| 命令 | 环境 |
|---|---|
| lcount=0 | pdksh and bash |
| set lcount=0 | tcsh |

> 在 `pdksh` 和 `bash` 下，你必须确保等号（`=`）的前后没有空格。

要向变量中存储字符串，可以使用以下方法：

| 命令 | 环境 |
|---|---|
| myname=Sanjay | pdksh and bash |
| set myname=Sanjay | tcsh |

上述的变量形式适用于字符串中不包含空格的情况。如果字符串包含空格，你可以如下方式进行赋值：

| 命令 | 环境 |
|---|---|
| myname="Sanjiv Guha" | pdksh and bash |
| set myname="Sanjiv Guha" | tcsh |

## 访问变量值

你可以通过在变量名前前加上 `$`（美元符号）来访问变量的值。也就是说，如果变量名为 `var`，你可以使用 `$var` 访问该变量。

如果你想将 `var` 的值赋值给变量 `lcount`，可以如下操作：

| 命令 | 环境 |
|---|---|
| lcount=var | pdksh and bash |
| set lcount=$var | tcsh |

## 位置参数

从命令行或另一个 shell 脚本向 shell 程序传递选项。

这些选项作为位置参数提供给 shell，它们具有特殊的名称。第一个参数存储在变量 `$1` 中，第二个参数存储在 `$2` 中，以此此类推。在编写脚本时，可以省略编号较高的参数。

### 位置参数的简单示例

例如，如果一个 shell 程序期望两个参数——例如名和姓——你用第一个参数（名）调用该 shell 程序。然而，你无法只用第二个参数（姓）调用它。

这是一个名为 `myprog1` 的 shell 程序，它接收一个参数（名称）并显示在屏幕上：

```bash

#!/bin/sh

#Name program

if [ $#-eq 0 ]; then

  echo "Name not provided"

else

  echo "Your name is $1"

fi

```

如果你如下执行 `myprog1`：

```bash

$ bash myprog1

```

你将得到输出：

Name not provided

然而，如果你如下执行 `myprog1`：

```bash

$ bash myprog1 Sanjiv

```

你将得到输出：

Your name is Sanjiv

shell 程序 `myprog1` 还说明了 shell 编程的另一个方面：Linux 内核提供的内置变量。在 `myprog1` 中，内置变量 `#` 提供传递给 shell 程序的参数数量。你将在本章下一节学习更多关于内置变量的内容。

## 使用位置参数从命令行访问和检索变量

如果你需要使用带有复杂参数的命令行，在脚本中使用位置参数非常有帮助。包含位置参数的 shell 程序如果频繁使用则会更加方便。例如，如果你使用 Fedora 脚本编写一个带有连接调制解调器的脚本，用于发布检索和播放语音消息的命令。以下行转换保存的音频文件（`.cmd` 或 `voice-phone` 格式）并将其结果管道到你的音频设备：

```bash

#!/bin/sh

# play voice message in /var/spool/voice/incoming

rmdtopvf /var/spool/voice/incoming/$1 \

pvfspeed 8000 \ \

>/dev/audio

```

然后可以使用此脚本（可能命名为 `pmm`）轻松地回放语音消息：

```bash

$ pmm name_of_message

```

### 位置参数

包含位置参数的 Shell 脚本通常用于自动化例行且繁琐的工作，例如系统日志报告生成、文件系统检查、用户资源统计、打印机使用统计以及其他系统、网络或安全管理任务。

### 使用简单脚本自动化任务

你可以使用简单的脚本（例如）来检查系统日志中的某些关键词。如果该脚本通过系统的调度表 `/etc/crontab` 运行，它可以帮助实现安全监控。通过将 Linux 命令的输出能力与 Shell 的语言功能相结合，你可以快速构建一个实用的脚本来执行通常需要多行命令行完成的任务。例如，你可以创建一个名为 `greplog` 的短脚本，如下：

```bash

#!/bin/sh

# name: greplog

# use: 使用关键字对指定日志进行 grep 邮件

# version: v.0108aug02

#

# author: bb

#

# usage: greplog [keyword] [logfile]

#

# bugs: 未检查参数数量是否正确

# 使用关键字搜索和日期构建报告名称

log_report=/tmp/$1.logreport.$(date '+%m%d%y')

# 使用系统类型、主机名、日期和时间构建报告头

echo "====================================================" \

    >>$log_report

echo " SYSTEM MONITOR LOG " >>$log_report

echo uname -a $(hostname -f) "$(date '+%c')" >>$log_report

echo " Log report for" >>$log_report

echo "====================================================" \

    >>$log_report ; echo "" >>$log_report

# 记录日志搜索开始

echo "Search for->" "starting" $(date '+%r') >>$log_report

echo "*" >>$log_report

# 从日志 ($2) 获取并保存关键词 ($1) 的 grep 结果

grep -i $1 $2 >>$log_report

```

```bash

# 使用时间构建页脚

echo "" >>$log_report

echo "End of $log_report at $(date +%r)" >>$log_report

# 将报告邮件给 root

mail -s "Log Analysis for $1" root <$log_report

# 清理删除报告

rm $log_report

exit 0

```

在这个示例中，脚本创建了变量 `$log_report` 参数，它将是临时报告的文件名。关键词（$1）和命令行上的第一个参数被用作文件名的一部分，以及当前日期（更好的方法是使用 `$$` 代替日期，这会将 PID 作为文件扩展名）。接下来，将包含格式化文本、`uname` 命令的输出以及主机名和日期的报告头添加到报告中。记录搜索开始，日志中关键词的任何匹配项都会添加到报告中。然后添加一个包含报告名称和时间的页脚。报告以邮件形式发送给 root，并以搜索词作为邮件主题，最后删除临时文件。

> 默认情况下，Fedora 使用系统 `/etc/cron.daily` 目录中的 watchdog 日志监控命令（实际上是一个 Perl 脚本）在每天的 0402（凌晨 4:02）生成各种报告。通过编辑文件 `/etc/log.d.d/logwatch.conf` 来配置日志记录。还包括其他系统监控工具，例如 tripwire。可以通过编辑 `/etc/syslog.conf` 来配置系统日志。

可以通过手动运行脚本并向系统日志 `/var/log/messages` 提供关键词和路径来测试脚本，如下：

```bash

# greplog FAILED /var/log/messages
```
