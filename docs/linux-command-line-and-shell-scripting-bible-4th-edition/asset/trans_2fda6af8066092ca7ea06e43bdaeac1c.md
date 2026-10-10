
- 将包含我们的 shell 脚本文件的目录添加到 PATH 环境变量中。
- 在 prompt 中使用绝对路径或相对文件路径来引用我们的 shell 脚本文件。

## 提示

一些 Linux 发行版会将 `$HOME/bin` 目录添加到 PATH 环境变量中。这会在每个用户的 `$HOME` 目录下创建一个位置，用于放置文件，以便 shell 能够找到并执行它们。

在这个例子中，我们将使用第二种方法，明确告知 shell 脚本文件的确切位置。请记住，要在 shell 中引用当前目录中的文件，可以使用单点运算符：

```bash
$ ./test1
bash: ./test1: Permission denied
$
```

现在 shell 成功找到了 shell 脚本文件，但还有另一个问题。Shell 显示你没有权限执行该文件。快速查看文件权限应该会揭示这里发生了什么：

```bash
$ ls -l test1
-rw-r--r--     1 user     user        73 Jun 02 15:36 test1
$
```

当创建新的 test1 文件时，umask 值决定了新文件的默认权限设置。由于 umask 变量设置为 022（参见第 7 章，“理解 Linux 文件权限”），系统创建的文件仅具有文件所有者的读/写权限。

下一步是使用 chmod 命令（参见第 7 章）授予文件所有者执行文件的权限：

```bash
$ chmod u+x test1
$ ./test1
Mon Jun 01 15:38:19 EST 2020
Christine tty2          2020-06-01 15:26
Samantha  tty3          2020-06-01 15:26
Timothy   tty1          2020-06-01 15:26
user      tty7          2020-06-01 14:03 (:0.0)
user      pts/0         2020-06-01 15:21 (:0.0)
$
```

成功！现在所有部件都已到位，可以执行新的 shell 脚本文件了。

## 显示消息

大多数 shell 命令都会产生自己的输出，这些输出显示在运行脚本的控制台监视器上。然而，很多时候，你会希望添加自己的文本消息，以帮助脚本用户了解脚本内部正在发生什么。你可以使用 echo 命令来实现这一点。如果添加字符串跟随在命令之后，echo 命令可以显示一个简单的文本字符串：

```bash
$ echo This is a test
This is a test
$
```

请注意，默认情况下，你不需要使用引号来界定你要显示的字符串。但是，如果你在字符串内部使用引号，这有时会变得棘手：

```bash
$ echo Let's see if this'll work
Lets see if this'll work
$
```

echo 命令使用双引号或单引号来界定文本字符串。如果你在字符串内部使用它们，你需要在文本中使用一种类型的引号，并使用另一种类型的引号来界定字符串：

```bash
$ echo "This is a test to see if you're paying attention"
This is a test to see if you're paying attention
$ echo 'Rich says "scripting is easy".'
Rich says "scripting is easy".
$
```

现在所有的引号都正确地出现在输出中。

你可以在 shell 脚本中任何需要显示额外信息的地方添加 echo 语句：

```bash
$ cat test1
#!/bin/bash
# This script displays the date and who's logged on
echo The time and date are:
date
echo "Let's see who's logged into the system:"
who
$ 
```

当你运行这个脚本时，它会生成以下输出：

```bash
$ ./test1
The time and date are:
Mon Jun 01 15:41:13 EST 2020
Let's see who's logged into the system:
Christine tty2	2020-06-01 15:26
Samantha tty3	2020-06-01 15:26
Timothy tty1	2020-06-01 15:26
user	tty7	2020-06-01 14:03 (:0)
user	pts/0	2020-06-01 15:21 (:0.0)
$ 
```

这很不错，但如果你希望在同一行上显示文本字符串和命令输出怎么办？你可以使用 echo 语句的 -n 参数来实现。只需将第一个 echo 语句行更改为以下内容：

```bash
echo -n "The time and date are: "
```

你需要在字符串周围使用引号，以确保在回显字符串的末尾有一个空格。命令输出从字符串输出停止的确切位置开始。输出现在看起来像这样：

```bash
$ ./test1
The time and date are: Mon Jun 01 15:42:23 EST 2020
Let's see who's logged into the system:
Christine tty2	2020-06-01 15:26
Samantha tty3	2020-06-01 15:26
Timothy tty1	2020-06-01 15:26
user	tty7	2020-06-01 14:03 (:0)
user	pts/0	2020-06-01 15:21 (:0.0)
$ 
```

完美！echo 命令是与用户交互的 shell 脚本中至关重要的部分。你会发现自己在许多情况下都会使用它，尤其是当你想要显示脚本变量的值时。接下来让我们看看这一点。

## 使用变量

仅仅从 shell 脚本中运行单独的命令是有用的，但这样做有其局限性。通常，你希望在 shell 命令中整合其他数据以处理信息。你可以通过使用变量来实现这一点。变量允许你在 shell 脚本中临时存储信息，以便在脚本中的其他命令中使用。本节展示了如何在 shell 脚本中使用变量。

### 环境变量

你已经见过一种 Linux 变量在发挥作用。第 6 章描述了 Linux 系统中可用的环境变量。你也可以从你的 shell 脚本中访问这些值。

Shell 维护跟踪特定系统信息的环境变量，例如系统名称、登录系统的用户名、用户的系统 ID（称为 UID）、用户的默认主目录以及 shell 用于查找程序的搜索路径。你可以使用 set 命令显示所有活动的可用环境变量列表：

```bash
$ set
BASH=/bin/bash
...
HOME=/home/Samantha
HOSTNAME=localhost.localdomain
HOSTTYPE=i386
IFS=$' \t\n'
IMSETTINGS_INTEGRATE_DESKTOP=yes
IMSETTINGS_MODULE=none
LANG=en_US.utf8
LESSOPEN= '|/usr/bin/lesspipe.sh %s'
LINES=24
LOGNAME=Samantha
...
```

你可以通过使用环境变量名称，并在其前面加一个美元符号，来在脚本内部利用这些环境变量。

以下脚本演示了这一点：

```bash
$ cat test2
#!/bin/bash
# display user information from the system.
echo "User info for userid: $USER"
echo UID: $UID
echo HOME: $HOME
$  
```

环境变量 `$USER`、`$UID` 和 `$HOME` 被用来显示关于登录用户的相关信息。输出应该类似于以下内容：

```bash
$ chmod u+x test2
$ ./test2
User info for userid: Samantha
UID: 1001
HOME: /home/Samantha
$ 
```

请注意，在脚本运行时，`echo` 命令中的环境变量会被其当前值替换。还要注意，我们能够将 `$USER` 系统变量放在第一个字符串的双引号内，而 shell 脚本仍然能够理解我们的意思。然而，使用这种方法有一个缺点。看看在这个例子中发生了什么：

```bash
$ echo "The cost of the item is $15"
The cost of the item is 5  
```

显然这不是预期的结果。每当脚本在引号内看到美元符号时，它就假定你正在引用一个变量。在这个例子中，脚本试图显示变量 $1（该变量未定义），然后是数字 5。要显示实际的美元符号，你必须在其前面加上反斜杠字符：

```bash
$ echo "The cost of the item is \$15"
The cost of the item is $15  
```

这样就更好了。反斜杠使 shell 脚本将美元符号解释为实际的美元符号，而不是变量。下一节展示了如何在你的脚本中创建自己的变量。

> **注意**
> 
> **你也可能看到使用格式 `$[variable]` 引用的变量。变量名称周围的额外括号通常用于帮助将变量名称与美元符号区分开来。**

### 用户变量

除了环境变量，shell 脚本还允许你在脚本内设置和使用自己的变量。设置变量允许你临时存储数据并在整个脚本中使用它们，使 shell 脚本更像真正的计算机程序。

用户变量可以是任意长度的文本字符串，最长可达 20 个字母、数字或下划线字符。用户变量对大小写敏感，因此变量 *var1* 与变量 *VAR1* 不同。这条小规则常常让初学者脚本程序员陷入困境。

使用等号将值分配给用户变量。变量、等号和值之间不能有空格（这是另一个让初学者容易出错的地方）。以下是向用户变量分配值的几个例子：

```bash
var1=10
var2=-57
var3=testing
var4="still more testing"
```

Shell 脚本将所有变量值存储为文本字符串；至于用于变量值的数据类型，则由 shell 中的各个命令决定。在 shell 脚本内定义的变量在整个 shell 脚本的生命周期中保持其值，但当 shell 脚本完成时会被删除。

与系统变量一样，可以使用美元符号引用用户变量：

```bash
$ cat test3
```
