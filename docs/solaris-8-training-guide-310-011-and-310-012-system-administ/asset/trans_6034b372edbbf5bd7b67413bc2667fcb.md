
## 重复操作命令

Bourne shell 提供了三种重复操作命令，每种都对应于你在其他编程语言中可能见过的结构：

- `for`
- `while`
- `until`

这些命令使程序循环或重复执行。接下来将对其进行描述。

### The for Loop

一个有用的 shell 命令是 for 循环，它是在 shell 脚本中设置重复的最简单方法。for 循环的语法如下：

```
for name [ in wordlist . . . ]
do list
done
```

每次执行 for 命令时，name 会被设置为从 in 单词列表中取出的下一个单词。如果省略 in word ...，则 for 命令对每个已设置的定位参数执行一次 do 列表。执行在列表中没有更多单词时结束。下面的示例说明了一个简单的 for 循环：

```
for i in eat run jump play
do
    echo See spot $i
done
```

当程序执行时，系统会响应如下：

```
See spot eat
See spot run
See spot jump
See spot play
```

如果你想交互式地输入数据，可以添加 shell 特殊命令 read：

```
echo Hello- What\'s your name\?
read name
for i in $name
do
    echo $i
done
```

执行程序时，会提示用户输入单词列表。请注意反斜杠 (\ ) 的使用，这样 ' 和 ? 就会被原样处理，而不会被用作特殊字符。

### The while Loop

while 循环会持续重复执行一组命令，直到满足条件为止。while 循环的语法如下：

```
while condition-list
do commands
done
```

首先，执行 condition-list。如果它返回 true 的退出状态，则执行 do 列表，并且操作从头开始重启。如果 condition-list 返回 false 的退出状态，则条件结构完成。

下文说明了 while 循环。该程序检查文件 /tmp/errlog 是否存在。如果文件不存在，程序将退出循环。如果文件存在，程序将打印一条消息并每五秒重新运行一次，直到文件被删除。

```
while [ -f /tmp/errlog ]
do echo The file is still there ; sleep 5
done
```

NOTE
特殊命令 sleep 5 指示系统在再次运行前等待五秒钟。

### The until Loop

until 循环是 while 语句的变体。就像 while 语句只要 condition-list 返回 true 值就重复执行一样，until 语句会重复执行直到 condition-list 返回 false 值。以下示例会每五秒显示一条消息，直到文件被创建为止：

```
until [ -f /tmp/errlog ]
  do echo the file is missing; sleep 5
  done
```

while 和 until 等条件结构由 shell 执行，就像它们是单个命令一样。shell 会在执行其任何部分之前扫描整个结构。

## SHELL FUNCTIONS

任何好的编程语言都提供对函数的支持。函数是一组语句的集合，作为一个整体执行。这些集合的执行方式就像“常规”命令一样，用于执行经常需要的任务。函数的一个优点是它存储在计算机的主内存中，因此执行速度比必须从磁盘检索的脚本快得多。当前版本的 Bourne shell 支持 shell 函数；旧版本的 Bourne shell 不支持。shell 函数的语法如下：

```
name()
{
command-list
}
```

此命令语法定义了一个名为 name 的函数。函数体是 { 和 } 之间的 command-list。每当 name 被指定为命令的名称时，就会执行此列表。作为示例，在命令提示符下，输入以下内容：

```
hello()
{
echo hello there
}
```

该函数名为 hello，可以通过输入 hello 来执行。函数的输出是 hello there。函数的退出状态是主体中执行的最后一个命令的退出状态。

## CHAPTER SUMMARY

### KEY TERMS

- Shell script
- Execution bit
- Restricted shell
- J-shell
- C-shell
- Korn shell
- Bourne shell
- Shell variable
- Quoting
- Shell built-ins
- Shell conditional
- Exit status
- Loop
- Shell function

使用脚本和 shell 程序构建自己的命令是协助系统管理的一种强大而灵活的工具。首先，你需要选择最适合你使用的 shell。可以从 Bourne shell、bash、C-shell、tcsh 或 Korn shell 中选择。然而需要注意的是，大多数系统管理员选择 Bourne shell，因为它使用广泛且可用性高。

本章描述了 Shell 变量。作为系统管理员，你会定期设置和使用变量。你大多数的 Solaris 和第三方程序都依赖于这些变量。如果设置不正确，程序将出错，系统可能无法正常运行。

最后，描述了 shell 内建命令和条件。你将在脚本中使用这些内建命令来设置变量、获取输入，并执行重复任务以及自动化常规任务所需的其他操作。

使用所有这些工具，可以简化并自动化常规任务，节省你的时间，让你能够处理更 demanding 的任务。Shell 编程是所有 UNIX 系统管理员必须具备的技能，也是成为熟练 UNIX 用户的关键之一。

这结束了第一部分以及第一部分考试所涵盖的材料。下一部分涵盖你为第二次考试需要了解的主题。在许多情况下，第二部分提供了本节中介绍但不是第一次考试目标的主题的更多细节。

## Apply Your Knowledge

### Exercises

### 12.1 Using Bourne Shell Variables

在本练习中，你将显示和设置 Bourne shell 变量。

Estimated Time: 10 minutes

- 1. 通过输入 `/sbin/sh` 确保你处于 Bourne shell。通过显示 `$SHELL` 变量的值来验证你是否处于 Bourne shell：
```
echo $SHELL
```
- 2. 打印环境中环境变量的值：
```
env
```
- 3. 打印环境中本地变量的值：
```
set
```
- 4. 更改到你的主目录：
```
cd $HOME
```
- 5. 创建一个名为 ME 的环境变量。分配给该变量的值应为你的姓名。
```
ME='Bill Calkins'
export ME
echo $ME
```
- 6. 删除该变量：
```
unset ME
```

### 12.2 Creating a Bourne Shell Script

编写一个名为 search1 的 Bourne shell 脚本，提示用户输入要在其目录中所有文件中搜索的字符串。显示包含该字符串的所有文件的文件名。

Estimated Time: 15 minutes

- 1. 在你的主目录中，使用 vi 创建一个名为 search1 的文本文件，包含以下条目：
```
#!/bin/sh
echo "Please enter a string to search for: "
read string
echo The following files contain the string \
$string:
grep -l $string *
```
- 2. 设置文件可执行权限：
```
chmod 744 search1
```
- 3. 按如下方式执行文件：
```
./search1
```

确保你的主目录中有一个包含你计划搜索的字符串的文本文件。如果需要，使用 vi 创建几个临时文件。

使用 vi 编辑器编写以下名为 reverse 的 shell 脚本，该脚本将接收最多 10 个参数并按相反顺序列出参数。

- 4. 在你的主目录中，使用 vi 编辑器创建以下名为 mylist 的脚本：
```
#!/sbin/sh
echo $10 $9 $8 $7 $6 $5 $4 $3 $2 $1
```
- 5. 设置文件可执行权限：
```
chmod 744 mylist
```
- 6. 按如下方式执行脚本，并查看结果：
```
./mylist 1 2 3 4 5 6 7
```

## APPLY YOUR KNOWLEDGE

### 12.3 Using the case Conditional in a Script

本练习演示了在脚本中使用 case 条件语句。脚本将为用户显示一个选项列表。会根据所选选项运行特定命令。

Estimated Time: 15 minutes

- 1. 在你的主目录中，使用 vi 编辑器创建一个名为 *options* 的文件，包含以下条目：
- 2. 设置名为 *options* 的文件可执行权限：
- 3. 执行脚本并输入 a、b 或 c 并观察结果：

```
#!/bin/sh
echo Please enter the letter next to the \
command that you want to select:
echo 'a  date'
echo 'b  ls'
echo 'c  who'
read choice
case $choice in
  a) date;;
  b) ls;;
  c) who;;
  *)  echo Invalid choice - Bye.
esac
```

```
chmod 744 options
```

```
./options
```

### 12.4 Creating an Interactive for Loop

本练习将演示如何使用 for 循环在脚本中设置重复。此脚本将提示用户输入姓名，并为每个输入的姓名生成问候语。

Estimated Time: 15 minutes

- 1. 在你的主目录中，使用 vi 编辑器创建一个名为 *users* 的文件，包含以下条目：

```
#!/bin/sh
echo "Hello- Please enter a list of names \
(ie. Bill Tom Mike)"
read LIST
for file in $LIST
do
echo Greetings $LIST
done
```
- 2. 设置名为 *users* 的文件可执行权限：
- 3. 执行脚本：

```
chmod 744 users
```

```
./users
```

### 12.5 Using the while Conditional

本练习将演示如何在脚本中使用 while 循环。你将创建一个名为 *msg* 的程序，该程序每五秒向活动窗口显示一条消息，持续一分钟。

Estimated Time: 15 minutes

- 1. 在你的主目录中，使用 vi 编辑器创建一个名为 *msg* 的文件，内容如下：
- 2. 设置名为 *msg* 的文件可执行权限：
- 3. 执行脚本：

```
#!/bin/sh
count=1
while
  [ count -lt 12 ]
do
  echo "Hello, I'm glad you're here"
  sleep 5
  let count=count+1
done
```

```
chmod 744 msg
```

```
./msg
```

```
#!/bin/sh
echo "Hello- Please enter a list of names \
```
