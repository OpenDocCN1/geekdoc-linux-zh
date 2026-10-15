
shell 执行了 `if` 行上列出的 `pwd` 命令。因为退出状态为 0，它还执行了 `then` 部分列出的 `echo` 语句。

这是另一个示例：

```bash
$ cat test2.sh

#!/bin/bash

# testing a bad command

if IamNotaCommand

then

  echo "It worked"

fi

echo "We are outside the if statement"

$
$ ./test2.sh
```

```
./test2.sh: line 3: IamNotaCommand: command not found
We are outside the if statement
$
```

在这个例中，我们刻意在 `if` 语句中使用了一个无法运行的命令 `IamNotaCommand`。由于这是一个错误的命令，它产生了一个非零的退出状态，`bash` shell 跳过了 `then` 部分的 `echo` 语句。同样注意，在 `if` 语句中运行命令时生成的错误信息仍然出现在脚本的输出中。有时你可能不希望错误语句出现。第 15 章讨论了如何避免。

## 注意

你可能会在某些脚本中使用 `if-then` 语句的另一种形式：

```
if command; then
  commands
fi
```

通过在要评估的命令末尾加上一个分号，你可以将 `then` 语句包含在同一行，这看起来更接近其他某些编程语言处理 `if-then` 语句的方式。

`then` 部分不仅限于包含一个命令。你可以像 shell 脚本的其他部分一样列出多个命令。`bash` shell 将这些命令视为一个块，当 `if` 语句中的命令返回 0 退出状态时，执行所有命令；或者当命令返回非零退出状态时，跳过所有命令：

```bash
$ cat test3.sh

#!/bin/bash

# testing multiple commands in the then section
#
testuser=Christine
#
if grep $testuser /etc/passwd
then
  echo "This is my first command"
  echo "This is my second command"
  echo "I can even put in other commands besides echo:"
  ls -a /home/$testuser/.
fi
$
```

`if` 语句使用 `grep` 命令搜索 `/etc/passwd`，以检查特定用户名当前是否被系统使用。如果存在该登录用户，脚本将显示一些文本，然后显示用户 HOME 目录下的 bash 文件：

```bash
$ ./test3.sh
x:501:501:ChristineB:/home/Christine:/bin/bash
This is my first command
This is my second command
I can even put in other commands besides echo:
/home/Christine/.bash_profile
/home/Christine/.bash_logout
/home/Christine/.bashrc
$
```

然而，如果你将 `testuser` 变量设置为系统上不存在的用户，则什么什么都不会发生：

```bash
$ cat test3.sh

#!/bin/bash

# testing multiple commands in the then section
#
testuser=NoSuchUser
#
# if grep $testuser /etc/passwd
then
    echo "This is my first command"
    echo "This is my second command"
    echo "I can even put in other commands besides echo:"
    ls -a /home/$testuser/.
fi
$
  ./test3.sh
$
```

这并不完全有趣。如果我们能显示一条小消息，说明系统中未找到该用户名，那就好了。嗯，我们可以利用 `if-then` 语句的另一个功能来实现。

## 探索 if-then-else 语句

在 `if-then` 语句中，对于命令是否成功你只有一个选择。如果命令返回非零退出状态码，`bash` shell 只是移动到脚本中的下一条命令。在这种情况下，如果能够执行另一组备用命令将是好。这正是 `if-then-else` 语句的作用。

`if-then-else` 语句在 `else` 中提供了另一组命令：

```
if command
then
  commands
else
  commands
fi
```

当 `if` 语句中的命令返回 0 退出状态时，`bash` 执行 `then` 部分的命令。如果命令返回非零退出状态，则 `bash` 执行 `else` 部分的命令。

```bash
$ ./test5.sh
ls: cannot access /home/NoSuchUser: No such file or directory
The user NoSuchUser does not exist on this system.
And, NoSuchUser does not have a directory.
$
```

在 `/home/NoSuchUser` 目录被删除并在执行 `elif` 语句之前，返回了零退出状态。因此，`elif` 的 `then` 代码块中的语句被执行了。在删除 `/home/NoSuchUser` 目录后，`elif` 语句返回了非零退出状态。这导致 `elif` 块中的 `else` 块语句被执行。

## 提示

请记住，对于 `elif` 语句，紧随其后的任何 `else` 语句都是针对该 `elif` 代码块的。它们不是之前的 `if-then` 语句代码块的一部分。

你可以将多个 `elif` 语句连接在一起，创建一个庞大的 `if-then-elif` 组合体：

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

每个命令块的执行取决于哪个命令返回了零退出状态码。记住，`bash` shell 会按顺序执行 `if` 语句，只有第一个返回零退出状态的语句会导致该部分被执行。

尽管使用 `elif` 语句让代码看起来更整洁，但要遵循脚本的逻辑仍然可能很令人困惑。在稍后的“考虑 `case` 情况”章节中，你将看到如何使用 `case` 命令，而不是嵌套大量的 `if-then` 语句。

# 尝试 test 命令

到目前为止，你看到的所有 `if` 语句行都是普通的 shell 命令。你可能会怀疑 `bash` 的 `if-then` 语句是否有能力评估除命令退出状态码以外的任何条件。

答案是否定的，它不能不能。但是，`bash` shell 中有一个非常实用的工具，可以帮助你使用 `if-then` 语句来评估其他内容。

`test` 命令提供了一种在 `if-then` 语句中测试不同条件的方法。如果 `test` 命令中列出的条件评估为真（TRUE），则 `test` 命令以零退出状态码退出。这使得 `if-then` 语句的行为与其他编程语言中的 `if-then` 语句工作方式相同。如果条件为假（FALSE），`test` 命令以非零退出状态码退出，导致 `if-then` 语句退出。

`test` 命令的格式非常简单：

```
test condition
```

条件是一系列由 `test` 命令评估的参数和值。在 `if-then` 语句中使用时，`test` 命令看起来如下所示：

```
if test condition
  commands
fi
```

如果你漏掉了 `test` 命令语句中的条件部分，它将以非零退出状态码退出，并触发任何 `else` 块语句：

```bash
$ cat test6.sh
!/bin/bash
# Testing the test command
#
if test
  echo "No expression returns a True"
else
  echo "No expression returns a False"
fi
$ ./test6.sh
No expression returns a False
$
```
