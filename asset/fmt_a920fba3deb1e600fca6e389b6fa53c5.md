
是的。把它们放在你的`.profile`文件中（C shell 用`.login`），它们将在整个会话中可用，并在所有子 shell 或脚本中可用。

## 我应该删除变量吗？

不需要。它们通常不会造成任何伤害，但如果你对这类事情难以忍受地挑剔，那就去做吧，尽情发挥吧！删除变量的命令是`unset variable`。

## 我如何查看变量的值？

使用`print`命令。你可以通过使用`print "$variable"`来查看变量被设置为什么。`echo`命令也可以用于此，但最好使用`print`，因为`echo`在不同系统上的行为可能不同。另请注意，我们将变量名用双引号括起来。`shell`仍会在双引号内看到`$`并将变量扩展为其值。

## UNIX 中的 DOS 命令

我们这些必须在 UNIX 和 DOS 或 Windows 机器之间不断切换的人，总是会因为差异而遇到问题。两个操作系统中的命令足够相似以至于我们的手指不断感到困惑。解决方法是创建一个与 DOS 等效命令类似工作的 UNIX 命令集，然后在 DOS（或 Windows 95/NT）中做同样的事情，这样当我们在那里时，我们的手指也不会感到困惑。以下是一组有用的别名。你可能会发现其他想要别名的情况。只需将它们添加到列表中，然后将它们放入你的`.kshrc`文件中。

```
### DOS aliases, only available from an interactive shell so we
### don't slow down scripts.
case $- in
'*i' # if $ - matches '*i', this is a shell, not a script
alias copy='cp'
alias move='mv'
alias rd='rmdir'
alias deltree='rm -r'
alias cls='clear'
alias dir='ls -l'
alias type='cat'

esac
!!
```

我们有一个类似的集合，我在 Windows NT 和 Windows 95 中使用来处理问题的另一面。创建一个名为`unix.bat`的文件并将其放在你的路径中的某个位置。然后从`autoexec.bat`文件中调用该文件。以下是我在 DOS 中的 UNIX 命令集

```
REM Only need to load DOSKEY inside here if you aren't using
REM it already. To load it from within here, UNREM the next
REM line. Note the fairly large buffer size. You may need it.
REM doskey /bufsize=2048
doskey mv=move $*
doskey cp=copy $*
doskey ll=dir $* /p
doskey pwd=cd
doskey more=type $1 $b more
doskey cat=type $*
doskey man=help $1
doskey rm=del $*
doskey env=set | more
doskey grep=find $*
```

最后，你可能会发现两个环境之间最令人恼火的差异是文本编辑器的差异。

Tip: 如果你必须在 DOS 或 Windows 中工作很多，你会怀念你的`vi`。不过在 DOS 世界中也有不错的替代品。其中之一是 Oak Hill Software, Inc. 在亚利桑那州斯科茨代尔提供的 Oak Hill Vi。MKS Toolkit 拥有出色的`vi`以及适用于 Windows 的图形化`vi`，同时还提供了一个完整的 DOS（以及 Windows 95 的）`COMMAND.COM`（或 Windows NT 的`CMD.EXE`）shell 的替代品，其外观与 UNIX 非常相似。正如我们在第 11 章中讨论的那样，对于需要在 UNIX 和 NT 环境中同时工作的人来说，一份 MKS Toolkit 的拷贝会带来很大不同。

## Shell 脚本快捷方式

你使用 UNIX 越多，就会发现自己写 shell 脚本的次数越多。大多数脚本会是服务于简单目的的短小脚本。有些可能是冗长复杂的脚本，其中包含各种错误检查。但无论你写什么脚本，它们都应该有一些共同点。最容易忘记但最重要的，是始终为你的脚本编写文档。是的，没错。每个人总是这么说。但我们是认真的。事实上，让我们为了强调而重复一遍。

- 始终为你的 shell 脚本编写文档。无论它们多么简单，在其中插入一个包含关键信息的小标题几乎没有成本，例如文件名、创建日期以及它本应执行的任务。当然，你现在知道它做什么。但你不会记得两周后，更不用说两年后了。
- 为每个脚本制作一个标准头文件。每个脚本都应该有一个头文件，你会自动将其包含在每个将足够长久以至于离开你的`~/tmp`目录的 shell 脚本中。你可以在其中包含任何你想要的内容，但我们强烈建议你在脚本中也添加注释。你以后会感谢自己的。
- 让系统为你创建唯一的文件名。如果你每天运行一个脚本——例如，将一组重要文件备份到不同的文件系统——就让 UNIX 做一些工作吧。如果你每天需要生成一个文件名，就让`date`命令为你工作。下面的示例展示了一个每天运行以导出关键数据库的脚本。我们使用`date`命令生成文件名。这使得很容易跟踪哪个文件是最新的，同时让我们可以将整个命令粘贴到`crontab`中以使其自动执行。有关`crontabs`和在指定时间自动运行作业的更多信息，请参阅第 7 章。

```
### Filename: db_exp.ksh
### Author: Charlie Russel
### Description: Script to create an automatic export of the database.
### Last Modification: 8/15/97-Modified to compress file on creation - cpr
### Prev. Modification: Added absolute path to exp - 7/14/97

//scripts/oracle_setup DUMMY
### Run Script
print "\n"
print "Executing script db_exp.ksh"
ORACLE_SID=... export ORACLE_SID
file="/safety/`date +%Y%m%d`.dmp" # Create unique filename with today's date
### Put command into variable
oracmd="/oracle/bin/exp system/ricpw file=$file grants=y indexes=y full=y"
print "Executing command..."
print "$oracmd"
oracmd
### Execute the compression on the created file to reduce space.
### This could simply be piped from the export, but is separate for historical reasons.
compress $file
exit
```

如果你只需要一个文件作为临时存储位置，就让系统来做这项工作。让 UNIX 担心清理工作并跟踪文件名。某些命令需要一个文件作为中间存储位置，因此使用 UNIX 的内置功能来创建和删除临时文件名。`mktemp`命令存在于许多 UNIX 实现中，但如果你的系统上不存在，你可以让 shell 生成一个名称。如果`mktemp`存在，尝试这样做：

`filename=`mktemp``

然后，当脚本结束时，只需添加一行来清理自己：

`rm $filename`

如果你的 UNIX 版本不支持`mktemp`，就使用 shell 的内置功能来完成工作：

`filename= "/tmp/$LOGNAME.$SECONDS"`

这将基于你的登录名和自启动此 shell 以来的秒数生成一个文件名。只要记住在使用完后删除该文件。否则，你的系统管理员很可能会因为清理你的残留物而变得不高兴。

## 第 6 章

## 打印

## 答案主题！

### 立即打印 87

- 标准 UNIX 打印命令
- 更改默认打印机目标
- 覆盖默认打印机目标
- 消除横幅页
- 控制打印的份数
- UNIX 打印的特殊性
- 让 UNIX 在打印作业完成后通知你
- 控制打印文档的外观
- 现在打印 vs 稍后打印

### 稍后打印 91

- 暂存打印作业以便稍后打印
- 检查打印作业的状态
- 安排稍后打印作业

### 格式设置 93

- 基本格式选项
- 使用 UNIX 进行格式设置
- 双倍行距文件
- 为文件添加左边界
- 删除硬制表符并重新对齐制表位
- 用制表符替换空格
- 将列表转换为多列

### 其他有用的打印技巧 97

- 取消打印作业
