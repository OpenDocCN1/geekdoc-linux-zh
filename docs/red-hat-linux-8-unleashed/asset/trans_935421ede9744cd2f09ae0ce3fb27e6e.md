

## 在 Shell 脚本中使用变量

```bash
$ env
...
HOSTTYPE=1386
HOSTNAME=thinkpad.home.org
```

虽然内置命令的行为并没有由 POSIX 定义，但在编写 shell 脚本时，其使用方式的变体可能会帮助。例如，如 `wish` 的 man 页面所述的，你可以使用 shell 来帮助执行 shell 脚本内部调用的程序，而无需硬编码程序的模式。`wish` 命令是一个窗口控制语言（tcl）解释器，可用于编写图形化客户端。避免使用特定程序可以增加 shell 脚本的可移植性，因为并不是每个 UNIX 系统都将在相同的位置拥有这些程序。

例如，如果你想使用 `wish` 命令，你的第一直可能是编写：
`!/usr/local/bin/wish`

尽管这在许多其他操作系统上可以运行，但脚本会在 Linux 下执行失败，因为 `wish` 位于 `/usr/bin` 目录下。然而，如果你想这样编写命令行：

```bash
#!/bin/sh
exec wish "$$"
```

你就可以使用 `wish` 命令（作为二进制文件或 shell 脚本本身）。

## 在 Shell 脚本中使用变量

本书的这一部分继续讨论 shell 变量的使用。这些信息将帮助你在 shell 脚本中定义、分配和使用变量。“位置参数（Positional Parameters）”章节将展示如何访问和使用存储命令行参数的变量。Linux shell 支持完整的编程语言以及此类变量。

在为 Red Hat Linux 编写 shell 脚本时，你会处理三种类型的变量：

-   **环境变量**是系统环境的一部分，你可以在 shell 程序中使用它们。可以定义新变量，并且某些变量（如 `PATH`）也可以在 shell 程序中修改。
-   **内置变量**（例如命令行选项，被 shell 解释为位置参数）由 Linux 提供。与环境变量不同，你无法修改它们。
-   **用户变量**是在你编写 shell 脚本时定义的。你可以在 shell 程序中随任意地使用和修改它们。

shell 编程与其他编程语言的主要区别在于，在 shell 编程中，变量是无类型的——也就是说，你不需要指定变量是数字还是字符串等。

## 给变量赋值

假设你想使用变量 `lcount` 来统计 shell 程序中循环循环的迭代次数。你可以按照以下方式声明并初始化该变量：

| 命令 | 环境 |
| :--- | :--- |
| lcount=0 | csh |
| set lcount=0 | tcsh |

注意：在 csh 和 bash 中，你必须确保等号 (=) 前没有空格。

要向变量中存储字符串，可以使用以下方法：

| 命令 | 环境 |
| :--- | :--- |
| myname=John | csh |
| set myname=John | tcsh |

如果字符串不包含嵌入空格，则上述变量形式有效。如果字符串包含嵌入空格，你可以按照以下方式赋值：

| 命令 | 环境 |
| :--- | :--- |
| myname="John Doe" | csh |
| set myname="John Doe" | tcsh |

## 访问变量值

可以通过在变量名前面加上 `$`（美元符号）来访问变量的值。也就是说，如果变量名为 `var`，你可以使用 `$var` 来访问该变量。

如果你想将 `var` 的值赋值给变量 `lcount`，可以这样操作：

| 命令 | 环境 |
| :--- | :--- |
| lcount=$var | csh |
| set lcount=$var | tcsh |

## 位置参数

你可以从命令行或另一个 shell 脚本向你的 shell 程序传递选项。这些选项由 Linux 作为位置参数提供给 shell 程序，具有系统提供的特殊名称。第一个参数存储在名为 `$1`（数字）的变量中，可以在程序中使用 `$1` 进行访问。第二个参数存储在名为 `$2` 的变量中，可以在程序中使用 `$2` 进行访问。可以省略一个或多个编号靠后的参数。在开发高级 shell 程序时，理解如何使用这些位置参数以及如何访问从命令行获取的变量是必要的。

## 位置参数的简单示例

例如，如果你执行一个期望两个参数（例如名和姓）的 shell 程序，但你只带了一个参数（名）来调用该 shell 程序。然而，你不能只带第二个参数（姓）来调用它。这里有一个名为 `name1` 的 shell 程序，它只接受一个参数（名称）并将其显示在屏幕上：

```bash
#!/bin/sh
# display program
if [ $# -eq 0 ]; then
    echo "Name not provided"
else
    echo "Your name is $1"
fi
```

如果你如下执行 `name1`：

```bash
$ name1
```
你得到以下输出：
Name not provided

然而，如果你如下执行 `name1`：

```bash
$ name1 John
```
你得到以下输出：
Your name is John

shell 程序 `name1` 阐了 shell 编程的另一个方面：shell 内核提供的内置变量。在 `name1` 中，内置变量 `$$` 提供了传递给 shell 程序的参数数量。你将在本章下一节学习更多关于处理内置变量的知识。

## 使用位置参数从命令行访问和检索变量

如果你需要使用带有复杂参数的管道命令的命令行，那么在脚本中使用位置参数将非常有用。包含位置参数的 shell 程序在命令频繁使用时会变得更加方便。例如，如果你使用带有连接调制解调器的 Red Hat Linux 系统，你可以编写一个脚本来命令检索并播放语音消息（`.wav` 格式），并将结果管道到你的系统音频设备：

```bash
#!/bin/sh
# play voice message /var/spool/incoming
cat /var/spool/incoming/$1 | play -s 8000 >/dev/audio
```

消息可以通过此脚本轻松地回放（可能命名为 `play`）：

```bash
$ play name_of_message
```

包含位置参数的 shell 脚本通常用于自动化例行任务，例如系统日志生成、文件系统检查、用户资源统计、打印机使用统计以及其他系统、网络或安全管理任务。你可以使用简单的脚本检查某些关键词检查系统日志。如果脚本通过调度表 `/etc/crontab` 运行，它可以帮助监控安全。通过将现有 Linux 命令的输出能力与 shell 的语言功能相结合，你可以快速构建一个脚本来执行通常需要多行命令行的任务。例如，你可以创建一个名为 `greplog` 的短脚本：

```bash
#!/bin/sh
# name: greplog
# use: mail grep of designated log using keyword
# version: v.01 08aug02
#
# author: author

# usage greplog [keyword] [logpathname]
#
# bugs: does not check for correct number of arguments

# 使用关键字搜索和日期构建报告名
log_report=/tmp/$1.logreport.$(date '+%m%d%y')

# 构建系统类型、主机名、日期和时间的报告头
echo "==================================" > $log_report
echo " SYSTEM LOG" >> $log_report
uname -a >> $log_report
echo "Log report for $(hostname) on $(date '+%c')" >> $log_report
echo "==================================" >> $log_report
echo "" >> $log_report

# 记录日志搜索开始
echo "Search for $1 starting $(date '+%r')" >> $log_report
echo "" >> $log_report

# 从日志文件 ($2) 获取并保存关键字 ($1) 的 grep 结果
grep -i "$1" "$2" >> $log_report

# 构建时间的页脚
echo "" >> $log_report
echo "End of $log_report at $(date '+%r')" >> $log_report

# 将报告邮件给 root
mail -s "Log Analysis for $1" root < $log_report

# 清理并移除报告
rm $log_report
exit 0
```

