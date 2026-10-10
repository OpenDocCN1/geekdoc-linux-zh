
## 第二部分：Shell 脚本基础

$ ls -d /home/NoSuchUser/
/home/NoSuchUser/
$
$ ./test5.sh
用户 NoSuchUser 在此系统上不存在。
/home/NoSuchUser/
然而，NoSuchUser 拥有一个目录。
我们已离开了嵌套的 if 语句。
$

该脚本正确地发现，尽管登录名已从 /etc/passwd 文件中移除，但用户的目录仍保留在系统上。在脚本中使用这种嵌套的 if-then 语句的问题在于，代码可能会变得难以阅读，并且逻辑流程也变得难以跟踪。

> **注意**
>
> 本章中使用了 `ls` 命令的一些其他有用命令选项（及选项组合）：
>
> - -d 仅显示目录信息，不显示目录内容。
> - -sh 以人类可读的格式显示文件大小。
> - -g 显示文件的长列表，但不显示所有者的名称。
> - -o 显示文件的长列表，但不显示组的名称。
>
> `ls` 命令在第 3 章“基本 Bash Shell 命令”中首次介绍。

无需编写单独的 `if-then` 语句，你可以使用 `else` 部分的另一种版本，称为 `elif`。`elif` 通过另一个 `if-then` 语句继续 `else` 部分：

```
if command1
then
commands
elif command2
then
more commands
fi
```

`elif` 语句行提供另一个要评估的命令，类似于原始的 `if` 语句行。如果 `elif` 命令的退出状态码为 0，Bash 将执行第二个 `then` 语句部分中的命令。使用这种嵌套方法可以提供更干净的代码，并且逻辑流程更容易跟踪：

```
$ cat test5.sh
#!/bin/bash
# 测试嵌套 if - 使用 elif
#
testuser=NoSuchUser
#
if grep $testuser /etc/passwd
then
echo "用户 $testuser 的账户在此系统上存在。"
echo
elif ls -d /home/$testuser/
    echo "用户 $testuser 拥有一个目录，"
    echo "尽管 $testuser 没有账户。"
fi
echo "我们已离开了嵌套的 if 语句。"

$ ./test5.sh
/home/NoSuchUser/
用户 NoSuchUser 拥有一个目录，
尽管 NoSuchUser 没有账户。
我们已离开了嵌套的 if 语句。
$
```

该脚本的问题在于，如果账户和目录都不存在了，你得不到关于这些事实的通知。你可以通过让脚本同时检查没有目录的无用户和没有目录的无用户来解决这个问题，并进一步将脚本提升一个层次。你通过在嵌套的 *elif* 中添加 *else* 语句来实现这一点：

```
$ cat test5.sh
#!/bin/bash
# 测试嵌套 if - 使用 elif 和 else
#
testuser=NoSuchUser

if grep $testuser /etc/passwd
then
echo "用户 $testuser 的账户在此系统上存在。"
echo
elif ls -d /home/$testuser/
    echo "用户 $testuser 拥有一个目录，"
    echo "尽管 $testuser 没有账户。"
else
echo "用户 $testuser 在此系统上不存在，"
echo "并且没有为 $testuser 创建目录。"
fi
echo "我们已离开了嵌套的 if 语句。"

$ ./test5.sh
/home/NoSuchUser/
用户 NoSuchUser 拥有一个目录，
尽管 NoSuchUser 没有账户。
我们已离开了嵌套的 if 语句。
$
```

```
$ sudo mkdir /home/NoSuchUser/
[sudo] christine 的密码：
$
$ ./test5.sh
ls: 无法访问 '/home/NoSuchUser/'：没有那个文件或目录
用户 NoSuchUser 在此系统上不存在，
并且没有为 NoSuchUser 创建目录。
我们已离开了嵌套的 if 语句。
$
```

在 /home/NoSuchUser 目录被移除且测试脚本执行 elif 语句之前，返回了 0 退出状态。因此，elif 的 then 代码块内的语句被执行。在 /home/NoSuchUser 目录被移除后，elif 语句返回了非 0 退出状态。这导致在 elif 块内的 else 块中的语句被执行。

> 注意
> 请记住，在使用 elif 语句时，紧随其后的任何 else 语句仅适用于该 elif 代码块。它们不是前面 if-then 语句代码块的一部分。

你可以继续将 elif 语句串联起来，创建一个巨大的 if-then-elif 集合：

```
if command1
then
command set 1
elif command2
then
command set 2
elif command3
then
command set 3
elif command4
then
command set 4
fi
```

每一组命令的执行取决于哪个命令返回 0 退出状态码。请记住，Bash shell 按顺序执行 if 语句，并且只有第一个返回 0 退出状态的命令才会导致 then 部分被执行。

尽管使用 elif 语句后代码看起来更干净，但跟踪脚本的逻辑仍然可能令人困惑。在后文的“考虑 case 命令”部分，你将看到如何使用 case 命令来替代嵌套大量的 if-then 语句。

## 尝试 test 命令

到目前为止，你在 if 语句行中看到的都是普通的 shell 命令。你可能会想知道 Bash 的 if-then 语句是否可以评估除命令退出状态码以外的任何其他条件。

答案是否定的，它不能。然而，Bash shell 中可用的一个实用工具可以帮助你使用 `if-then` 语句评估其他事物。

`test` 命令提供了一种在 `if-then` 语句中测试不同条件的方法。如果 `test` 命令中列出的条件评估为 `TRUE`，`test` 命令将以 0 退出状态码退出。这使得 `if-then` 语句的行为与其他编程语言中的 `if-then` 语句非常相似。如果条件为假，`test` 命令将以非 0 退出状态码退出，这会导致 `if-then` 语句退出。

`test` 命令的格式非常简单：

```bash
test condition
```

*condition*（条件）是一系列参数和值，`test` 命令会对它们进行评估。当在 `if-then` 语句中使用时，`test` 命令看起来像这样：

```bash
if test condition
then
    commands
fi
```

如果你省略 `test` 命令语句中的 *condition*（条件）部分，它将以非 0 退出状态码退出（*False*）并触发任何 `else` 块语句：

```bash
$ cat test6.sh
#!/bin/bash
# 测试 test 命令
#
if test
then
    echo "没有表达式返回 True"
else
    echo "没有表达式返回 False"
fi
$
$ ./test6.sh
没有表达式返回 False
$
```

当你添加一个条件时，它会由 `test` 命令进行测试。例如，使用 `test` 命令，你可以确定变量是否包含内容。确定变量是否包含内容需要一个简单的条件表达式：

```bash
$ cat test6.sh
#!/bin/bash
# 测试变量是否包含内容
# my_variable="Pull"
#
if test $my_variable
then
    echo "my_variable 变量包含内容并返回 True。"
    echo "my_variable 变量的内容是：$my_variable"
else
    echo "my_variable 变量不包含内容，"
    echo "并返回 False。"
fi
$
$ ./test6.sh
my_variable 变量包含内容并返回 True。
my_variable 变量的内容是：Pull
$
```

my_variable 变量包含内容（Pull），因此当 test 命令检查条件时，退出状态返回 0。这触发了 then 代码块中的语句。

正如你所料，当变量不包含内容时，会发生相反的情况：

```
$ cat test6.sh
#!/bin/bash
# 测试变量是否包含内容
#
my_variable=""
#
if test $my_variable
then
    echo "my_variable 变量包含内容并返回 True。"
    echo "my_variable 变量的内容是：$my_variable"
else
    echo "my_variable 变量不包含内容，"
    echo "并返回 False。"
fi
$
$ ./test6.sh
my_variable 变量不包含内容，
并返回 False。
$
```

Bash shell 提供了一种在 if-then 语句中不使用 test 命令来测试条件的替代方法：

```
if [ condition ]
then
    commands
fi
```

方括号定义了测试条件。请注意：第一个括号后面必须有一个空格，最后一个括号前面必须有一个空格，否则你将收到错误消息。

test 命令和测试条件可以评估三类条件：

- 数值比较
- 字符串比较
- 文件比较

