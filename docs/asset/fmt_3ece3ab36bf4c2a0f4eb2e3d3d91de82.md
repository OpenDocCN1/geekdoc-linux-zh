
```bash
$ pg ifcounter
#!/bin/sh
# ifcounter
COUNTER=100
echo "Do you wish to change the counter value currently set at $COUNTER [y..n]:"
read ANS
if [ "$ANS" = "y" ] || [ "$ANS" = "Y" ]; then
  # 是，用户想要更改值
  echo "Enter a sensible value"
  read VALUE
  # 简单测试是否为数字，将任何数字加到 VALUE
  # 然后检查返回值
  # 代码
  expr $VALUE + 10 > /dev/null 2>&1
  STATUS=$?
  # 检查 expr 的返回码
  if [ "$VALUE" = "" ] || [ "$STATUS" != "0" ]; then
    # 将错误发送到标准错误
    echo "You either entered nothing or a non-numeric " >&2
    echo "Sorry now exiting.counter stays at $COUNTER" >&2
    exit 1
  fi
  # 如果我们运行到这里，说明是一个数字，所以将其加到 COUNTER
  COUNTER=`expr $COUNTER + $VALUE`
  echo "Counter now set to $COUNTER"
else
  # 如果我们运行到这里，说明只是按了回车而不是输入数字
  # 或者在更改值提示回答了 n
  echo "Counter stays at $COUNTER"
fi
```

以上脚本的运行方式如下。

```bash
$ ifcount
Do you wish to change the counter value currently set at 100 ? [y..n]:n
Counter stays at 100
```

```bash
$ ifcount
Do you wish to change the counter value currently set at 100 ? [y..n]:y
Enter a sensible value
abc
You either entered nothing or a non-numeric
Sorry now exiting.counter stays at 100
```

```bash
$ ifcount
Do you wish to change the counter value currently set at 100 ? [y..n]:y
Enter a sensible value 250
Counter now set to 350
```

## 254 控制流结构

### 18.3.21 添加登录脚本的简单安全性

这是一个在用户登录时启动应用程序之前添加额外安全性的框架。它会提示输入用户名和密码；如果用户名和密码与脚本中包含的字符串匹配，则用户进入。否则，用户将被退出。

该脚本的工作原理是先将变量设置为假值——始终确保用户输入是错误的。保存当前的 `stty` 设置，这样我们就可以隐藏输入密码时的字符。随后恢复 `stty` 设置。

如果用户输入正确的用户 ID 和密码（密码为 `mayday`），则 `INVALID_USER` 和 `INVALID_PASSWD` 将由于无效的用户或密码被设置为 'no'。然后将进行测试，如果任何一个变量被设置为 `yes`（默认值），脚本将退出用户。

然后允许具有有效 ID 和密码的用户进入。对于这类登录脚本来说，这是一个非常基本的框架。在这个示例中，有效的用户 ID 是 `dave` 和 `pauline`。

```bash
$ pg ifpass
#!/bin/sh
# ifpass
# 将变量设置为假
INVALID_USER=yes
INVALID_PASSWD=yes
# 保存当前的 stty 设置
SAVEDSTTY=`stty -g`
echo "You are logging into a sensitive area"
echo -n "Enter your ID name :"
read NAME
# 隐藏输入的字符
stty -echo
echo "Enter your password :"
read PASSWORD
# 恢复设置
stty $SAVEDSTTY
if [ "$NAME" = "dave" ] || [ "$NAME" = "pauline" ]; then
  # 检查密码
  if [ "$PASSWORD" = "mayday" ]; then
    # 无效的用户或密码
    INVALID_USER=no
    INVALID_PASSWD=no
  fi
fi
# 执行测试
if [ "$INVALID_USER" = "yes" ] || [ "$INVALID_PASSWD" = "yes" ]; then
  # 如果无效，退出
  echo "Access denied" >&2
  exit 1
fi
echo "Welcome $NAME"
```

## 18.4.1 简单的 case 语句

以下脚本提示输入 1 到 5 之间的数字。该数字被传递给 `case` 语句，变量 `ANS` 被赋值为 `case` 值 `ANS`，并将 `ANS` 与每个模式进行比较。

如果找到匹配项，将执行模式部分内部的命令直到遇到 `;`。在这种情况下，它将仅 `echo` 一个命令来告知用户选择了什么。由于找到了匹配项，`case` 的执行将终止。

在 `case` 语句之后可以继续继续处理。如果没有找到匹配项，它将使用 `*` 模式进行捕获，该模式可以捕获任何内容。然后执行错误消息。

```
$ caseselect
!/bin/sh
caseselect
echo -n"enter a number from 1 to 5 :"
read ANS
case $ANS in
1) echo "select 1"
  ;
2) echo "select 2"
  ;
3) echo "select 3"
  ;
4) echo "select 4"
  ;
5) echo "select 5"
  ;
*) echo "`basename $0`: This is not between 1 and 5" >&2
  exit 1
  ;
esac
```

当我们用不同的输入运行此脚本时，得到：

```
$ caseselect
enter a number from 1 to 5 : 4
you select 4
```

使用模式 `*` 可以捕获其他任何不匹配的内容：

```
$ caseselect
enter a number from 1 to 5 :pen
caseselect: This is not between 1 and 5
```

## 18.4.2 与模式匹配结合

在使用 `case` 时，你也可以指定 `|` 符号作为“或”逻辑命令。例如，`vt100|vt102)` 将匹配模式 `vt100` 或 `vt102`。

在此示例中，用户被要求输入其模式，并将与模式 'vt100|vt102)` 匹配。要执行的命令是将 `TERM` 变量设置为 `vt100`。如果用户输入的终端类型与模式不匹配，`*` 将捕获它并强制将其设置为 `vt100`。最后，在 `case` 语句之外，导出了 `TERM`。无论用户输入什么，`TERM` 都将持有一个有效的终端类型，因为我们使用了 `*` 模式匹配。

```
$ caseterm
!/bin/sh
$ caseterm
echo choices are.. vt100, vt102, vt220
echo -n"enter your terminal type :"
read TERMINAL
case $TERMINAL in
vt100|vt102) TERM=vt100
  ;
vt220) TERM=vt220
  ;
*) echo `basename $0`: Unknown response >&2
echo "setting it to vt100 anyway, so there"
TERM=vt100
  ;
esac
export TERM
echo Your terminal is set to $TERM
```

当脚本运行且我们输入无效终端类型时，得到：

```
$ caseterm
choices are.. vt100, vt102, vt220
enter your terminal type :vt900
caseterm : Unknown response
setting it to vt100 anyway, so there
Your terminal is set to vt100
```

对于正确的终端类型，我们得到：

```
$ case2
choices are.. vt100, vt102, vt220
enter your terminal type :vt220
Your terminal is set to vt220
```

无论何种，用户都设置了一个终端类型。

## 18.4.3 提示输入 y 或 n

`case` 的一个良好用法是提示用户是否继续处理。在这里，用户被提示回答 `y` 继续处理或回答 `n` 退出。如果用户输入 `y`、`Y` 或 `Yes`，处理将继续，因为脚本的执行会在 `case` 语句之后继续。如果用户输入 `n`、`N` 或其他任何响应，则用户将退出脚本。

```
$ caseans
#!/bin/sh
# caseans
echo -n "Do you wish to proceed [y..n] "
read ANS
case $ANS in
y|Y|yes|Yes) echo "yes is selected"
  
n|N) echo "no is selected"
  exit 0 # 无错误，所以只退出 0 以终止
  
*) echo "`basename $0`: Unknown response" >&2
  exit 1
esac
# 如果我们只选了 y|Y|yes|Yes。
```

如果用无效的响应运行脚本，输出如下：

```
$ caseans
Do you wish to proceed [y..n] :df
caseans : Unknown response
```

如果是良好的响应，输出如下：

```
$ caseans
Do you wish to proceed [y..n] :y
yes is selected
```

## 18.4.4 Case 与传递命令参数

你也可以使用 `case` 来处理传递给脚本的参数。

在下一个脚本中，对特殊变量 `#$` 进行了测试，该变量持有传递的参数个数。如果它不等于 1，则将带有一个用法消息退出。

`case` 语句可以捕获以下参数：`passwd`、`start`、`stop` 或 `help`。可以对这些匹配的每个模式进行进一步的编码。如果传递了未知值，则向标准错误回显用法消息。

```
$ caseparam
!/bin/sh
# caseparam
if [ $# != 1 ]; then
  echo "Usage: `basename $0 [start|stop|help]`" >&2
  exit 1
fi
# 将参数赋值给变量 OPT
OPT=$1
case $OPT in
  start) echo "starting..`basename $0`
    # 在处启动进程的代码
    ;
  stop) echo "stopping..`basename $0`
    # 在处停止进程的代码
    ;
  help)
    # 在处显示帮助页
    ;
  *) echo "Usage: `basename $0 [start|stop|help]`"
    ;
esac
```

当用无效参数运行脚本时，我们得到：

```
$ caseparam what
Usage:caseparam [start|stop|help]
```

当传递有效参数时：

```
$ caseparam stop
stopping..caseparam
```

## 18.4.5 无模式命令的输入捕获

你可以在模式匹配部分之后放置命令，尽管这并不总是如此。

## 18.4.6 默认变量值

如果用户只是在 `read` 变量上按了回车，脚本并不总是必须退出。一个测试可以确定变量是否已设置，如果没有设置，则一个值……

## 264 控制流结构

对于正确的输入，我们得到：

```
$ caserep
Weekly Report
你想在星期几运行报告 [Saturday]
validating..Saturday
即在周六运行的报告
```

对于错误的输入，我们可能会得到：

```
$ caserep
Weekly Report
你想在星期几运行报告 [Saturday]:Tuesday
validatng..Tuesday
你疯了吗！此报告只能在周六、周日或周一运行
```

你可能已经得出结论，`case` 语句可以完成与几个 `if then else` 语句相同的任务。你的假设是正确的。

## 18.5 for 循环

`for` 循环的一般格式为：

```bash
for variable_name in list
do
  command1
  command...
done
```

`for` 循环会对 `list` 中包含的每个值处理一次信息。要访问 `list` 中的每个值，请使用 `variable_name`。命令可以是任何有效的 shell 命令或语句。`variable_name` 可以是你想要的任何单词。

`list` 使用是可选的；如果你不包含它，`for` 循环将使用命令行中的位置参数。

`in list` 可以包含替换、字符串和文件名。让我们来看一些示例。

### 18.5.1 简单 for 循环

此循环简单地输出列表，即 `1 2 3 4 5`。为了访问每个变量 `variable_name`，使用了 `loop` 循环。

```bash
$ pg for_i
#!/bin/sh
# for_i

for loop in 1 2 3 4 5
do
  echo $loop
done
```

运行上述脚本输出：

```
$ for_i
1
2
3
4
5
```

### 18.5.2 打印字符串列表

这是一个 `for` 循环，其中列表包含持有 "orange red blue grey" 值的字符串。每个变量的命令是 `echo`，变量 `variable_name` 是 `loop`。`echo` 命令使用 `$loop` 输出列表中的每个值，直到列表为空。

```bash
$ pg forlist
#!/bin/sh
# forlist
for loop in "orange red blue grey"
do
  echo $loop
done
```

```
$ forlist
orange red blue grey
```

你也可以将字符串与 `variable_name` 结合，在我们案例中变量名是 `loop`。

`echo " this is the fruit $loop`

这将得到

This is the fruit orange red blue grey

### 18.5.3 在 for 循环中使用 ls

此循环评估 shell 的 `ls` 命令并打印出当前目录下的每个文件。
