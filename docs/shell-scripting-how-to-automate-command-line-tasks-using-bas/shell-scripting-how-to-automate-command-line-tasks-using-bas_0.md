

# Shell 脚本：如何使用 Bash 脚本和 Shell 编程自动化命令行任务

![](img/rsrc2J2.jpg)

## 作者其他书籍

- 命令行武功夫：Bash 脚本技巧、Linux Shell 编程技巧以及 Bash 单行命令 [`www.linuxtrainingacademy.com/command-line-kung-fu-book`](http://www.linuxtrainingacademy.com/command-line-kung-fu-book)
- LAMP 堆栈的高可用性：消除单点故障并增加基于 Linux、Apache、MySQL 和 PHP 的 Web 应用程序运行时间 [`www.linuxtrainingacademy.com/ha-lamp-book`](http://www.linuxtrainingacademy.com/ha-lamp-book)
- 初学者 Linux：Linux 操作系统和命令行介绍 [`www.linuxtrainingacademy.com/linux`](http://www.linuxtrainingacademy.com/linux)
- 初学者 Python 编程 [`www.linuxtrainingacademy.com/python-programming-for-beginners`](http://www.linuxtrainingacademy.com/python-programming-for-beginners)

## 引言

我很懒。我承认这一点。我深信懒惰的好处，以至于我会做任何事情来促进未来更加懒惰。例如，如果我认为以后极小可能需要再次执行同一组命令，我就会创建一个 Shell 脚本。当我再次需要执行该任务时，我就会懒惰地执行我的脚本。如果需要在凌晨 2 点对系统进行维护，我会编写一个执行所需工作的脚本，并安排一个作业来运行它。懒人喜欢睡觉。

我也相信帮助人们发现他们内心的懒惰。为什么？因为懒人解决问题。他们消除了不必要的。他们简化了复杂的。这就是我写这本书的原因。我想与你们分享我最喜欢的技巧和方法，我用这些技巧来自动化重复、单调、枯燥和复杂的任务。希望它们能激励你们变懒。

在我们开始之前，我建议您访问以下网址下载书中使用的 Shell 脚本：[`www.linuxtrainingacademy.com/shell-scripts`](http://www.linuxtrainingacademy.com/shell-scripts)

## 简明 Shell 脚本编程

脚本是一个包含一系列命令的命令行程序。脚本中的命令由解释器执行。在 Shell 脚本的情况下，Shell 充当解释器，并逐个执行脚本中的命令。任何你可以在命令行中执行的内容，都可以放入 Shell 脚本中。Shell 脚本非常擅长自动化任务。如果你发现自己正在通过运行一系列命令来完成给定的任务，并且将来还需要执行该任务，那么你可以——而且可能应该——为此创建一个 Shell 脚本。

让我们来看一个简单的 Shell 脚本。这个脚本的名称是 `script.sh`。

```bash
#!/bin/bash
echo "Scripting is fun!"
```

在尝试执行脚本之前，请确保它是可执行的。

```bash
chmod 755 script.sh
./script.sh
Scripting is fun!
```

### Shebang（解释器）

你会注意到脚本的第一行以 `#!` 开头，后面跟着 `bash` shell 的路径 `/bin/bash`。`#!` 符号与音乐中使用的井号非常相似。此外，有些人也将感叹号称为 "bang"。因此，`#!` 可以读作 "sharp bang"。"Shebang" 这个词是 "sharp bang" 的不准确写法。当脚本的第一行以 shebang 开头时，其后的内容被用作脚本命令的解释器。这里有三个 Shell 脚本示例，每个示例使用不同的 shell 程序作为解释器。

```bash
#!/bin/csh
echo "This script uses csh as the interpreter."
```

```bash
#!/bin/ksh
echo "This script uses ksh as the interpreter."
```

```bash
#!/bin/zsh
echo "This script uses zsh as the interpreter."
```

当你执行包含 shebang 的脚本时，实际发生的情况是执行解释器，并将调用脚本的路径作为参数传递给解释器。你可以通过检查进程表来证明这一点。让我们在后台启动这个脚本 `sleepy.sh` 并查看进程表。

```bash
./sleepy.sh &
[1] 16796
ps -fp 16796
UID PID PPID STIME TTY CMD
jason 16796 1725 0 pts/0 /bin/bash sleepy.sh
```

你可以看到实际运行的是 `/bin/bash ./sleepy.sh`。让我们使用全路径运行脚本。

```bash
/tmp/sleepy.sh &
[1] 16804
ps -fp 16804
UID PID PPID STIME TTY CMD
jason 16804 1725 0 pts/0 /bin/bash /tmp/sleepy.sh
```

确确实，`/bin/bash /tmp/sleepy.sh` 正在执行。你可以看到 `/bin/bash` 正在执行 `sleep` 命令，这是脚本中的第一个也是唯一的命令。

```bash
ps -ef | grep 16796
jason 16796 1725 0 10:00 pts/0 /bin/bash sleepy.sh
jason 16797 16796 0 10:00 pts/0 sleep 1000
jason 16798 16797 0 10:00 pts/0 grep 16796
```

如果你没有提供 shebang 且在脚本的第一行指定解释器，脚本中的命令将使用你当前的 shell 执行。尽管在许多情况下这可以正常工作，但最好明确指定用于脚本的解释器。例如，在 `bash` shell 中有效的特性在 `csh` shell 中可能无效。此外，你不必使用 shell 作为脚本的解释器。这里有一个名为 `hi.py` 的 Python 脚本示例。

```python
#!/usr/bin/python
print "This is a Python script."
```

让它可执行并运行它。

```bash
chmod 755 hi.py
./hi.py
This is a Python script.
```

关于 Python 编程和脚本的更多信息，请参阅我的书籍《Python for Beginners》。

变量是具有命名的存储位置。要给变量赋值，使用 `VARIABLE_NAME="Value"`。不要在等号前后使用空格。此外，按照习惯，变量名使用大写。

```bash
#!/bin/bash
MY_SHELL="bash"
```

使用变量时，在变量名前加上美元符号。

```bash
#!/bin/bash
MY_SHELL="bash"
echo "I like $MY_SHELL shell."
```

你也可以将变量名放在大括号中，并在左括号前加上美元符号。语法：`${VARIABLE_NAME}`。

```bash
#!/bin/bash
MY_SHELL="bash"
echo "I like ${MY_SHELL} shell."
```

除非你需要紧跟变量的额外数据，否则大括号语法是可选的。

```bash
#!/bin/bash
MY_SHELL="bash"
echo "I am ${MY_SHELL} on my keyboard."
```

如果你不将变量名封装在大括号中，shell 将额外的文本视为变量名的一部分。由于不存在该变量，因此没有内容被放入其中。

```bash
#!/bin/bash
MY_SHELL="bash"
echo "I am $MY_SHELL on my keyboard."
```

你还可以将命令的输出赋值给变量。为此，将命令放在括号中并在其前面加上美元符号。

```bash
#!/bin/bash
SERVER_NAME=$(hostname)
echo "You are running this script on ${SERVER_NAME}."
```

`hostname` 命令的输出存储在变量 `SERVER_NAME` 中。在本示例中，服务器名为 `svr`。你正在 `svr` 上运行此脚本。你也可以将命令放在反引号中。这是一种正在被 `$()` 替换的旧语法。然而，你可能在旧脚本中看到它。

```bash
#!/bin/bash
SERVER_NAME=`hostname`
echo "You are running this script on ${SERVER_NAME}."
```

### 变量

变量名可以包含字母、数字和下划线。它们可以是字母或下划线开头，但不能以数字开头。以下是有效变量名的示例。

```bash
FIRSTLETTERS="ABC"
FIRST_THREE_LETTERS="ABC"
```

是一些无效变量名的示例。

```bash
3="ABC"
first-three-letters="ABC"
Three@Letters="ABC"
```

### 测试

脚本的设计是为了取代人们亲自坐在键盘前输入一系列命令。如果你有一个想要自动化的任务，但需要根据不同情况采取不同的操作该怎么办？由于在脚本运行时人可能不在场做决定，我们需要测试条件并让脚本据此行动。要创建一个测试，在括号之间放置一个条件表达式。语法是 `[ condition-to-test ]`。你可以测试几种情况。例如，你可以比较字符串是否相等、一个数字是否大于另一个数字，或者文件是否存在。此测试检查 `/etc/passwd` 是否存在。如果存在，它返回真（退出状态为 0）。如果不存在，它返回假（退出状态为 1）。

```bash
[ -e /etc/passwd ]
```

如果你使用的是 `bash` shell，可以运行 `help test` 查看你可以执行的各种测试类型。你也可以阅读 `test` 的 man 页。这里是一些常用的测试文件运算符：

- `-d FILE`：目录是否存在
- `-e FILE`：文件是否存在
- `-f FILE`：普通文件是否存在
- `-r FILE`：是否可读
- `-s FILE`：是否不为空
- `-w FILE`：是否可写
- `-x FILE`：是否可执行

字符串运算符：

- `-z STRING`：字符串是否为空
- `-n STRING`：字符串是否不为空

算术运算符：

- `eq arg2`：arg1 等于 arg2
- `ne arg2`：arg1 不等于 arg2
- `lt arg2`：arg1 小于 arg2
- `le arg2`：arg1 小于或等于 arg2
- `gt arg2`：arg1 大于 arg2
- `ge arg2`：arg1 大于或等于 arg2

## `if` 语句

现在你已经知道了如何判断某个条件是否成立，你可以将其与 `if` 语句结合，在脚本中做出决策。`if` 语句以 `if` 为开头，后面跟着测试。接下来的行包含 `then`。如果测试条件真，将执行一系列命令。最后，`if` 语句以 `fi` 结束，它是 `if` 的倒写。这是语法：

```bash
if [ condition-true ]
then
  command 1
  command 2
fi
```

这是一个示例：

```bash
#!/bin/bash
MY_SHELL="bash"
if [ "$MY_SHELL" = "bash" ]
then
  echo "You seem to like the shell."
fi
```

执行条件测试时，将变量放在引号中是最佳实践，以防止某些副作用。你还可以使用 `if/else` 语句在条件不成立时执行操作。这是一个 `if/else` 语句：

```bash
if [ condition-true ]
then
  command 1
  command 2
else
  command 3
  command 4
fi
```

让我们更新脚本，在语句不成立时执行操作。

```bash
#!/bin/bash
MY_SHELL="csh"
if [ "$MY_SHELL" = "bash" ]
then
  echo "You seem to like the shell."
else
  echo "You don't seem to like the shell."
fi
```

因为 `[ "$MY_SHELL" = "bash" ]` 为假，所以执行了 `else` 后面的语句。你还可以使用 `elif` 测试多个条件。`elif` 是 "else if" 的缩写。像 `if` 一样，在 `elif` 后面跟着一个要测试的条件。在下一行使用 `then`。最后，提供条件为真时执行的一系列命令。

```bash
if [ condition-true ]
then
  command 1
  command 2
elif [ condition-true ]
then
  command 3
  command 4
else
  command 5
  command 6
fi
```

这是一个使用 `elif` 的更新脚本：

```bash
#!/bin/bash
MY_SHELL="csh"
if [ "$MY_SHELL" = "bash" ]
then
  echo "You seem to like the bash shell."
elif [ "$MY_SHELL" = "ksh" ]
then
  echo "You seem to like the csh shell."
else
  echo "You don't seem to like the bash or csh shells."
fi
```

输出：You seem to like the csh shell.

## `for` 循环

如果你想对项目列表执行操作，使用 `for` 循环。`for` 循环的第一行以 `for` 单词开头，后面跟着变量名，然后是 `in` 和项目列表。下一行包含 `do`。最后，用单行的单词 `done` 结束 `for` 循环。

```bash
for VARIABLE_NAME in ITEM_1 ITEM_2 ITEM_N
do
  command 1
  command 2
done
```

本质上发生的是列表中的第一个项目被赋值给变量并执行代码块。然后列表中的下一个项目被赋值给变量并执行命令。这对于列表中的每个项目都会发生。这里有一个显示 `for` 循环如何工作的简单脚本。

```bash
#!/bin/bash
for COLOR in red green blue
do
  echo "COLOR: $COLOR"
done
```

输出：

```text
COLOR: red
COLOR: green
COLOR: blue
```

将项目列表存储在变量中的常见做法如示例所示：

```bash
#!/bin/bash
COLORS="red green blue"
for COLOR in $COLORS
do
  echo "COLOR: $COLOR"
done
```

输出：

```text
COLOR: red
COLOR: green
COLOR: blue
```

此脚本 `rename-pics.sh` 将所有以 `.jpg` 结尾的文件重命名，加上今天的日期。

```bash
#!/bin/bash
PICTURES=$(ls *.jpg)
DATE=$(date +%F)
for PICTURE in $PICTURES
do
  echo "Renaming $PICTURE to ${DATE}-${PICTURE}"
  mv $PICTURE ${DATE}-${PICTURE}
done
```

### 位置参数

位置参数是包含命令行内容的变量。这些变量为 `$0` 到 `$9`。脚本本身存储在 `$0`，第一个参数在 `$1`，第二个在 `$2`，以此类推。以此命令行作为示例：

```bash
script.sh parameter1 parameter2 parameter3
```

内容如下：`$0` 是 `script.sh`，`$1` 是 `parameter1`，`$2` 是 `parameter2`，而 `$3` 是 `parameter3`。此脚本 `archive_user.sh` 接受用户名。

```bash
#!/bin/bash

echo "Executing script: $0"

echo "Archiving user: $1"

## 锁定账户

passwd -l $1

## 创建目录存档

tar cf /archives/${1}.tar.gz /home/${1}
```

`#` 后的任何内容都是注释。唯一的例外是第一行的 shebang。脚本中其他地方遇到井号都会被忽略。如果井号出现在行开头，整行会被忽略。如果在行中间遇到井号，只有右侧的信息会被忽略。这是我们执行 `archive_user.sh` 的输出。

与其在整个脚本中引用 `$1`，不如将其值赋值给更有意义的变量名。

```bash
#!/bin/bash

USER=$1

## 第一个参数是用户。

echo "Executing script: $0"

echo "Archiving user: $USER"

## 锁定账户

passwd -l $USER

## 创建目录存档

tar cf /archives/${USER}.tar.gz /home/${USER}
```

输出保持相同。

```text
./archive_user.sh elvis

Executing script: ./archive_user.sh

Archiving user: elvis

passwd locking elvis...

tar creating '/archives/elvis.tar.gz'
```




你可以使用特殊变量`$@`访问从`$1`到命令行最后一个的所有参数。下面是更新`archive_user.sh`脚本以接受一个或多个参数的方法：

```bash
#!/bin/bash

echo "Executing script: $0"

for USER in $@
do
  echo "Archiving user: $USER"

  # 锁定账户
  passwd -l $USER

  # 创建目录存档
  tar cf /archives/${USER}.tar.gz /home/${USER}
done
```

让我们向脚本传递多个用户。

## 获取用户输入

如果你想接受标准输入，请使用`read`命令。记住，标准输入通常来自在键盘上打字的人，但也可以来自其他源，例如命令行管道中命令的输出。`read`命令的格式为`read -p "PROMPT" VARIABLE_NAME`。这个版本的`archive_user.sh`脚本请求用户账户。

```bash
#!/bin/bash

read -p "Enter a user name: " USER
echo "Archiving user: $USER"

# 锁定账户
passwd -l $USER

# 创建目录存档
tar cf /archives/${USER}.tar.gz /home/${USER}
```

让我们运行此脚本并存档`mitch`账户。

```text
./archive_user.sh
Enter a user name: mitch
Archiving user: mitch
passwd locking mitch...
tar creating '/archives/mitch.tar.gz'
```

## 复习

脚本的第一行应该以 shebang 开头，后面跟着用于执行脚本的解释器路径。要给变量赋值，在变量名后跟着等号和值。不要在等号前后使用空格。

你可以通过`$VARIABLE_NAME`或`${VARIABLE_NAME}`访问存储在变量中的值。如果你需要在变量之前或紧跟额外数据，后者的形式是必要的。要将命令的输出赋值给变量，将命令放在括号中并在其前面加上美元符号。

通过在括号内放置表达式来执行测试，通常与`if`语句结合。使用`if`、`if/else`或`if/elif/else`语句在脚本中做出决策。使用`for`循环对多个项执行操作。

要访问命令行上的项，使用位置参数。程序名由`$0`表示，第一个参数由`$1`表示，以此类推。你可以使用特殊变量`$@`访问所有参数。最后，你可以使用`exit`命令控制脚本的退出状态。

## 练习题

**练习 1：** 编写一个显示“This script will exit with a 0 status.”的 Shell 脚本。确保脚本确实以 0 状态退出。

**练习 2：** 编写一个接受文件或目录名作为参数的 Shell 脚本。让脚本报告它是普通文件、目录还是其他类型。如果是普通文件，退出 0；如果是目录，退出 1；如果是其他类型，退出 2。

**练习 3：** 编写一个脚本将当前目录下所有以`.jpg`结尾的文件重命名为以今天的日期开头，格式为`YYYY-MM-DD`。例如，如果当前目录下有`mycat.jpg`且今天是 2016 年 10 月 31 日，它将更改为`2016-10-31-mycat.jpg`。作为额外加分，确保处理当前目录下没有`.jpg`文件的情况（提示：查看`bash`的`nullglob`选项）。

**练习 2：** 编写一个根据文件扩展名重命名文件的脚本。脚本应提示用户输入扩展名。然后询问用户前缀。默认情况下，前缀应该是`YYYY-MM-DD`格式的当前日期。如果用户直接按回车，将使用当前日期。否则，用户输入的内容将作为前缀。接下来，应显示原始文件名和新文件名。最后，应重命名文件。

## 练习题答案

### 练习 1

```bash
#!/bin/bash

# 可选：取消注释以避免未找到 jpg 文件时出现错误
# shopt -s nullglob

# YYYY-MM-DD
DATE=$(date +%F)

for FILE in *.jpg
do
  mv $FILE $DATE-$FILE
done
```

### 练习 2

```bash
#!/bin/bash

DATE=$(date +%F)

read -p "Enter a file extension: " EXTENSION
read -p "Enter a file prefix: " PREFIX

if [ -z "$PREFIX" ]; then
  PREFIX="$DATE"
fi

for FILE in *.*
do
  NEW_FILE="${PREFIX}-${FILE##*}.${EXTENSION}"

  # 等，示例文本中的逻辑略有问题
  echo "Renaming $FILE to $NEW_FILE"
  mv $FILE "$NEW_FILE"
done
```

# 退出状态与返回码

在本章，你将学习如何确定给定命令的退出状态。你将学习根据各种命令的退出状态在脚本中做出决策。最后，你将学习如何在自己的脚本中使用退出状态。

每执行一次命令都会返回一个退出状态。退出状态（有时被称为返回码或退出代码）是一个 0 到 255 的整数。按照惯例，成功执行的命令返回退出状态 0。如果遇到某种错误，则返回非零退出状态。

这些返回码可以在脚本中用于错误检查。它可以是简单的测试，例如检查零返回码，也可以是复杂的，例如检查特定的错误码。如果你想知道各种退出状态意味着什么，必须咨询给定命令的文档或查看其源代码。

你可以使用`man`和`info`命令来阅读系统中大多数命令的文档。例如，在`grep`的 man 页中，解释了如果找到了搜索模式，`grep`以状态 0 退出；如果没有找到，则以状态 1 退出。

特殊变量`$?`包含上一个执行命令的返回码。在这个 Shell 脚本片段中，调用`ls`命令时使用了不存在的文件路径：

```bash
ls /not/here
echo "$?"
```

输出：

```text
ls: /not/here: No such file or directory
2
```

在`ls`命令执行后，立即使用`echo $?`在屏幕上显示该命令的返回码。将在屏幕上显示 2。记住，非零退出代码意味着某种错误。如果`/not/here`文件存在且`ls`能够显示该文件的信息，退出状态将是 0。

你可以使用命令的退出状态来决策。在示例脚本中：

```bash
HOST="google.com"

ping -c 1 $HOST

if [ "$?" -eq "0" ]
then
  echo "HOST reachable."
else
  echo "HOST unreachable."
fi
```

执行`ping`命令后，我们检查退出状态。如果退出状态等于 0，则在屏幕上显示`google.com`是可达的。如果退出状态不等于 0，则显示`google.com`是不可达的。你可以使用命令的退出状态来决策。

## `exit`命令

不仅普通命令返回退出状态，Shell 脚本也是如此。你可以使用`exit`命令控制你的脚本的退出状态。只需在脚本中使用`exit`命令并在后面跟一个 0 到 255 之间的数字。

如果没有为`exit`命令指定返回码，则上一个执行命令的退出状态将被用作退出状态。这在脚本中没有`exit`命令时也是成立的。在这种情况下，脚本执行的最后一个命令将决定整个脚本的返回码。

```bash
exit 0
```

在脚本任何地方遇到`exit`命令，脚本都会停止运行。

```bash
echo "HOST unreachable."

exit 1

fi

exit 0
```

在示例脚本中：

```bash
#!/bin/bash

HOST="google.com"

ping -c 1 $HOST

if [ "$?" -eq "0" ]
then
  echo "HOST reachable."
else
  echo "HOST unreachable."
fi
```

在执行`ping`命令后，我们检查退出状态。如果退出状态等于 0，则在屏幕上显示`google.com`是可达的。如果退出状态不等于 0，则在屏幕上显示`google.com`是不可达的。你可以使用命令的退出状态来决策。

在示例脚本片段中，我们使用`ping`命令来测试到`google.com`的连通性。

```bash
HOST="google.com"

ping -c 1 $HOST

if [ "$?" -eq "0" ]
then
  echo "HOST reachable."
else
  echo "HOST unreachable."
fi
```

## 复习

在本章中，你学习了所有命令都返回退出状态。有效的退出状态是 0 到 255 之间的数字，0 代表命令执行成功，非零代表错误。

你学习了特殊变量`$?`以及它如何包含上一个执行命令的值。你使用`if`语句、`&&`和`||`做出决策。最后，你学习了如何使用`exit`命令控制自己脚本的退出状态。

## 练习题

**练习 1：** 编写一个显示“This script will exit with a 0 status.”的 Shell 脚本。确保脚本确实以 0 状态退出。

**练习 2：** 编写一个接受文件或目录名作为参数的 Shell 脚本。让脚本报告它是普通文件、目录还是其他类型。如果是普通文件，退出 0；如果是目录，退出 1；如果是其他类型，退出 2。

**练习 3：** 编写一个脚本执行`cat /etc/shadow`命令。如果命令返回状态 0，报告“Command succeeded”并退出 0。如果命令返回非零状态，报告“Command failed”并退出 1。

## 练习题答案

### 练习 1

```bash
#!/bin/bash

echo "This script will exit with a 0 status."

exit 0
```

### 练习 2

```bash
#!/bin/bash

echo "This script will exit with a 0 status."

exit 0
```

### 练习 3

```bash
#!/bin/bash

cat /etc/shadow

if [ "$?" -eq "0" ]
then
  echo "Command succeeded"
  exit 0
else
  echo "Command failed"
  exit 1
fi
```

# 函数

在本章中，你将学习为什么以及何时想要使用函数。你将学习如何创建函数，以及如何使用它们。我们将讨论变量及其作用域。你将学习如何使用参数来访问传递给函数的参数。最后，你将学习如何在函数中处理退出状态和返回码。

计算机编程和应用开发中有一个概念被称为 DRY。DRY 代表“Don't Repeat Yourself”（不要重复自己）。函数允许你编写一次代码并多次使用。这有助于缩短脚本的长度，并提供了一个进行更改、测试和文档化的统一位置。每当你需要在脚本中多次执行相同的操作时，可能应该写一个函数。

在脚本中，命令和组件是从上到下读取的。函数是一个执行特定操作的代码块并返回退出状态或返回码。函数必须在调用它之前定义。

## 创建函数

创建函数有两种方法。第一种是显式使用`function`关键字，后面跟着函数名，然后是括号。紧接着是大括号`{`。在函数内部的代码或命令将在函数调用时执行。要结束函数，使用右大括号`}`。

```bash
function function-name() {
  # 代码在这里
}
```

第二种声明函数的方法与第一种完全相同，除了不用`function`关键字。其他部分保持不变。

```bash
function-name() {
  # 代码在这里
}
```

## 调用函数

要调用函数，只需在脚本中列出它的名称。在调用函数时，不要使用括号。你可能在其他编程语言中见过这种语法，但在 Shell 脚本中不起作用。只需将函数名放在一行，它就会执行该函数。

```bash
#!/bin/bash

function hello() {
  echo "Hello!"
}

hello
```

输出：Hello

注意，函数可以调用其他函数。在本脚本中，`hello`函数被声明了。接下来`now`函数被声明了。最后，调用了`hello`函数。

```bash
#!/bin/bash

function hello() {
  echo "Hello!"
  now
}

function now() {
  echo $(date +%F)
}

hello
```

输出：

```text
Hello!
2023-10-27
```

你可能注意到`now`函数是在`hello`函数之后定义的。我说过函数必须在调用之前定义。在执行顺序中，它是在调用之前定义的。

```bash
#!/bin/bash

function now() {
  echo $(date +%F)
}

function hello() {
  echo "Hello!"
  now
}

hello
```

## 位置参数

和 Shell 脚本一样，函数可以接受参数。和 Shell 脚本一样，你可以使用`$1`、`$2`等访问这些传递参数的值。你甚至可以使用`$@`访问传递给函数的所有参数。

唯一的区别是`$0`仍然是脚本的名字。你不能通过`$0`访问函数名，但好消息是你永远不想这样做。要向函数传递数据，在函数名后提供数据。

在本示例中，调用`hello`函数时传递了一个参数`Jason`。这意味着函数内部`$1`的内容是“Jason”。

```bash
#!/bin/bash

function hello() {
  echo "Hello $1"
}

hello Jason
```

输出：Hello Jason

此脚本将循环传递给函数的每个参数，并打印“Hello”后跟该参数。此脚本的输出将是三行。第一行是“Hello Jason”，第二行是“Hello Dan”，第三行是“Hello Ryan”。

```bash
#!/bin/bash

function hello() {
  for NAME in $@
  do
    echo "Hello $NAME"
  done
}

hello Jason Dan Ryan
```

输出：

```text
Hello Jason
Hello Dan
Hello Ryan
```

## 作用域

默认情况下，所有变量都是全局的。这意味着变量可以在脚本的任何地方访问，包括任何函数内部。唯一的陷阱是变量在使用之前必须定义。你不能在脚本的末尾给变量赋值，然后在顶部通过变量访问它。

```bash
#!/bin/bash

GLOBAL_VAR=1

function my_function() {
  echo $GLOBAL_VAR
}

my_function
```

局部变量只能在声明它的函数内部访问。在变量名之前使用`local`关键字。

```bash
#!/bin/bash

function my_function() {
  local LOCAL_VAR=1
  echo $LOCAL_VAR
}

my_function

# 尝试访问 $LOCAL_VAR 将导致错误
echo $LOCAL_VAR
```

## 退出状态与返回码

函数实际上就像 Shell 脚本。和 Shell 脚本一样，函数有一个退出状态，有时被称为返回码。此退出状态可以通过`return`语句明确设置，并在后面跟上你想要返回的状态。

如果没有使用`return`语句，函数的退出状态是函数中执行的最后一个命令的状态。

```bash
function my_function() {
  echo "Task"
  return 0
}

my_function

echo $?
```

输出：

```text
Task
0
```

# 编辑器

- `vi` / `vim`
- `emacs`
- `nano`
- `gedit`
- `kate`
- `geany`
- 许多其他

# 环境变量与 Shell 调试

你可能熟悉`PS1`环境变量。它控制命令提示符显示的内容。还有其他与其类似的变量。对于 Shell 脚本调试非常有价值的变量是`PS4`。

在执行跟踪过程中，`PS4`会在每个命令执行之前展开并显示。这意味着当你对 bash 脚本使用`set -x`或`-x`选项时，`PS4`的内容会被打印到屏幕上。默认情况下，这是一个加号。不过，我们可以显式地设置`PS4`变量。

Bash 包含了几个内置变量，例如`$BASH_SOURCE`（脚本本身的名称）和`$LINENO`（脚本中的行号）。要查看更多变量，请访问：[Bash Variables](http://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html)。

这里是一个使用`PS4`变量的示例。该脚本将`PS4`设置为`"+ $BASH_SOURCE : $LINENO : "`。

```bash
#!/bin/bash -x

PS4='+ $BASH_SOURCE : $LINENO : '

TEST_VAR="test"

echo "$TEST_VAR"
```

输出：

```text
+ PS4='+ $BASH_SOURCE : $LINENO : '+ ./test.sh : 3 : TEST_VAR=test
+ ./test.sh : 4 : echo test
```

你可以看到当脚本执行时，在设置`PS4`变量后输出发生了变化。这可以使输出更清晰。例如，如果`echo`命令有问题，我们知道可以直接编辑脚本并直达第 4 行。

这是一个更高级的示例。它包含了更多信息，例如函数名。

```bash
#!/bin/bash -x



```bash
PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}() '

debug() {
  echo "Executing: $@"
  $@
}

debug ls
```

输出：

```text
+ PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}() '+ /tmp/j:7:() debug ls
+ /tmp/j:4:debug() echo 'Executing: ls'
Executing: ls
+ /tmp/j:5:debug() ls
```

你可以看到 `PS4` 变量如何允许我们使用内置变量 `FUNCNAME` 输出函数名。

## 文件类型与行结束符

文本文件（如我们处理 Shell 脚本时使用的文件）包含一个表示行结束的控制字符。对于 Unix 和 Linux 系统，表示新行的控制字符是`换行符`（Line Feed）。DOS 或 Windows 系统实际上使用两个字符来表示换行：`回车符`（carriage return）和`换行符`（line feed）。

如果你曾在 Linux 系统上创建了一个文本文件并发送给使用 Windows 系统的人，那么该文件在他们的电脑上很可能显示为长长的一行。这是由于缺少`回车符`。如果你相反操作，在 Windows 系统上创建文本文件并在 Linux 系统上打开它，该文件中会有额外的字符，特别是`回车符`。

（注：原文中剩余的关于回车符和 shebang 的重复/乱码句子已压缩，以保持关于 `dosunix` 和 `^M` 字符表示的核心技术信息。）

## 练习题

### 练习 1

编写一个 Shell 脚本，使其在出错时退出并在执行时显示命令，包括所有的展开和替换。在脚本中使用 3 个 `ls` 命令。让第一个成功，第二个失败，第三个成功。如果你使用了正确的选项，第三个 `ls` 命令将不会执行。

### 练习 2

修改上一个练习，使脚本在发生错误时继续运行。这一次，三个 `ls` 命令都将执行。

## 练习题答案

### 练习 1

```bash
#!/bin/bash -ex

ls /etc/passwd

ls /move/along/nothing/to/see/

ls /etc/passwd
```

### 练习 2

```bash
#!/bin/bash -xls

ls /etc/passwd

ls /move/along/nothing/to/see/

ls /etc/passwd
```

## Shell 脚本清单

1. 你的脚本是以 shebang 开头的吗？例如：`#!/bin/bash`
2. 你的脚本是否包含描述脚本用途的注释？例如：`# This script creates a backup of every MySQL database on the system.`
3. 全局变量是否声明在脚本顶部、紧随初始注释之后？例如：`DEBUG=true`，`HTML_DIR=/var/www`
4. 你是否将所有函数都集中写在全局变量之后？
5. 你的函数是否使用了局部变量？例如：`local GREETING="Hello!"`
6. 你的 Shell 脚本主体是否在函数之后？
7. 你的脚本是否带有显式的退出状态退出？例如：`exit 0`
8. 在各个退出点处，是否显式地使用了退出状态？例如：

```bash
if [ ! -d "$HTML_DIR" ]; then
  echo "$HTML_DIR does not exist. Exiting."
fi
```

## Shell 脚本模板

```bash
#!/bin/bash

### <替换为此 shell 脚本的描述和/或目的>

GLOBAL_VAR1="one"

GLOBAL_VAR2="two"

function function_one() {
  local LOCAL_VAR1="one"

  # <替换为函数代码>
}

### 脚本正文在此开始。

### <替换为你的 shell 脚本的主要命令>

### 以显式的退出状态退出。

exit 0
```

上述模板由一系列简短的最佳实践组成。首先，所有脚本都应该以 shebang 开头。这是脚本的第一行，它显式地声明了使用哪种解释器来执行脚本。

接下来，你应该至少包含一行注释，来总结脚本的作用和存在的原因。如果你愿意，也可以包含更多信息。有些人喜欢包含诸如其类的信息，例如脚本的原始作者、脚本版本以及其他细节。

如果你打算使用全局变量，它们应该紧随其后，除非它们的值在脚本的后续部分才能确定。函数应该紧随其之后。将你所有的函数在全局变量之后分组在一起。

在函数内部，定义局部函数的变量时，务必使用 `local` 关键字。在函数部分之后，你的 shell 脚本的主部分开始。

最后，记住显式地使用退出状态。如果你不提供退出状态（一个 `0` 到 `255` 之间的数字），则上一个执行命令的退出状态将作为你脚本的退出状态。最好由你控制这一点，而不是听由概率。至少用 `exit 0` 行结束你的脚本。如果你的脚本能够运行到最后一行，那么在大多数情况下，它已经成功完成。还要记住你的 shell 脚本可能终止的其他地方。你需要在那些地方也使用 `exit` 语句。例如，如果你的脚本执行了某种检查并因为检查失败而停止，你将希望以非零退出状态退出。

## 我个人收藏的脚本

如果你想查看我个人收藏的一些 shell 脚本，请访问：[`github.com/jasonc/scripts`](https://github.com/jasonc/scripts)

## 恭喜与感谢！

恭喜你完成了这本书！为了感谢你阅读这本书并读到最后，我想为我的 shell 脚本课程提供一个巨大的折扣。

仅需 15 美元（原价 99 美元的 85 折）即可报名——请访问：[`www.linuxtrainingacademy.com/shell-course`](http://www.linuxtrainingacademy.com/shell-course)

我期待在课程中见到你！

感谢，Jason

## 作者的其他书籍

- **命令行武术：Bash 脚本技巧、Linux Shell 编程贴士与 Bash 单行命令** [`www.linuxtrainingacademy.com/command-line-kung-fu-book`](http://www.linuxtrainingacademy.com/command-line-kung-fu-book)
- **LAMP 栈的高可用性：为你的基于 Linux、Apache、MySQL 和 PHP 的 Web 应用程序消除单点故障并增加运行时间** [`www.linuxtrainingacademy.com/ha-lamp-book`](http://www.linuxtrainingacademy.com/ha-lamp-book)
- **初学者 Linux：Linux 操作系统和命令行介绍** [`www.linuxtrainingacademy.com/linux`](http://www.linuxtrainingacademy.com/linux)
- **面向初学者的 Python 编程** [`www.linuxtrainingacademy.com/python-programming-for-beginners`](http://www.linuxtrainingacademy.com/python-programming-for-beginners)

## 包含你的专属折扣的额外资源

如需更多资源，请访问：[`www.linuxtrainingacademy.com/resources`](http://www.linuxtrainingacademy.com/resources)

## 书籍

### 命令行武术

你认为你必须把自己锁在地下室里连续阅读几个月晦涩的 man 手页，才能拥有像忍者一样的命令行技能吗？实际上，如果有人和你分享他们最强大的命令行技巧、技巧和模式，你将节省大量的时间和挫败感。这本书正是要做这些。

### LAMP 栈的高可用性

为你的基于 Linux、Apache、MySQL 和 PHP 的 Web 消除单点故障并增加运行时间。

### 初学者 Linux

如果你对学习编程感兴趣，或者特别是学习使用 Python，那么这本书适合你。在书中，你将学习如何安装 Python、选择哪个版本、如何为你的电脑准备以获得良好的体验，以及开始编写完整功能程序所需的所有计算机编程基础。

### 面向初学者的 Python 编程

## 课程

### LAMP 栈的高可用性

学习如何设置高可用 LAMP 栈（Linux、Apache、MySQL、PHP）。你将学习负载均衡、数据库集群、创建分布式文件系统等。

### 5 天学会 Linux

接下来的 5 天里，每天花 45 分钟，我将教你关于 Linux 操作系统所需的全部知识。你将学习到最重要的概念和命令，我甚至会引导你逐步完成几个实用且真实的示例。

### Shell 脚本编写

### 云托管和 VPS（虚拟专用服务器）

#### Digital Ocean

为开发者构建的简单云托管。仅需 55 秒即可部署 SSD 云服务器。每月低至 5 美元即可拥有自己的服务器。

### 使用 SSH 和 Shell 访问 Web 托管

#### Bluehost

我 99% 的网站都托管在 Bluehost 上。为什么？因为它非常易用，具有一键自动安装 WordPress 的功能以及卓越的客户服务——通过电话和聊天。我强烈建议你的第一个网站使用 Bluehost。此外，如果你计划创建更多网站，可以使用同一个托管账户管理多个域名。访问 http://www.linuxtrainingacademy.com/bluehost 获取比原价更低的折扣！

## 附录：商标

- BSD/OS 是 Berkeley Software Design, Inc. 在美国及其他国家的商标。
- Facebook 是 Facebook, Inc. 的注册商标。
- Firefox 是 Mozilla Foundation 的注册商标。
- HP 和 HEWLETT-PACKARD 是属于 Hewlett-Packard Development Company, L.P. 的注册商标。
- `IBM®` 是 International Business Machines Corp. 的注册商标，已在全球许多司法辖区注册。
- `Linux®` 是 Linus Torvalds 在美国及其他国家的注册商标。
- `Mac` 和 `OS X` 是 Apple Inc. 的商标，在美国及其他国家注册。
- `Open Source` 是 Open Source Initiative 的注册认证标记。
- `Sun` 和 `Oracle Solaris` 是 Oracle Corporation 关联公司在美国及其他国家的商标或注册商标。
- `UNIX` 是 The Open Group 的注册商标。
- `Windows` 是 Microsoft Corporation 在美国及其他国家的商标。
- 这里提到的所有其他产品名称均为其所有者的商标。
