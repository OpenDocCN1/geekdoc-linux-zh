
`/home/christine/factorial.sh`

We are outside the if statement

$

```

然而，如果你将 `testuser` 变量设置为系统上不存在的用户，则 `then` 代码中的任何内容都不会执行：

```bash
$ cat test3.sh

!/bin/bash

# testing multiple commands in the then block

#

tester=NoSuchUser

#

if grep $testuser /etc/passwd

then

    echo "This is my first command in the then block."

    echo "This is my second command in the then block."

    echo "I can even put in other commands besides echo:"

    ls /home/$testuser*/.sh

fi

echo "We are outside the if statement"

$
$ ./test3.sh
```

这并不完全有趣。如果我们可以显示一条小消息，说明系统上没有找到该用户名，就太好了。

## 探索 if-else 语句

在 if-then 语句中，你可以添加一个 `else` 部分来指定当条件为假时发生的情况。if-then-else 语句具有以下格式：

```bash
if command

then

    commands

else

    commands
```

if-then-else 语句运行 if 行定义的命令。如果命令的退出状态为零，则执行 `then` 部分的命令。如果命令的退出状态为任何其他值，则执行 `else` 部分的命令。`fi` 语句设置 if-then-else 语句的结束。

这里有一个简单的示例来演示这个概念：

```bash
if pwd

then

    echo "We are in the directory"

else

    echo "Something went wrong"

fi
```

如果我们将命令改为一个不存在的内容：

```bash
$ ls /nonexistent
ls: cannot access 'nonexistent': No such file or directory
```

这就是 if-else 语句提供的功能：

```bash
if ls /nonexistent

then

    echo "The directory exists"

else

    echo "The directory does not exist"

fi
```

if-else 语句允许你处理命令的所有可能结果。

另一个例子：

```bash
$ cat test4.sh

#!/bin/bash

# testing multiple commands in the then block and adding an else block

#

tester=NoSuchUser

#

if grep $testuser /etc/passwd

then

    echo "This is my first command in the then block."

    echo "This is my second command in the then block."

    echo "I can even put in other commands besides echo:"

    ls /home/$testuser*/.sh

else

    echo "The user $tester does not exist."

fi

echo "We are outside the if statement"
```

```bash
$ ./test4.sh

The user NoSuchUser does not exist.

We are outside the if statement

$
```

if-else 语句是控制脚本逻辑的强大工具。

## 嵌套 ifs

有时，你需要在脚本中检查多个条件。在这些情况下，你可以嵌套 if-then 语句。嵌套的 if 语句是另一个 if 语句内部的 if 语句。

```bash
if command1

then

    if command2

    then

        commands

    fi

fi
```

这里有一个简单的示例来演示这个概念：

```bash
$ cat test5.sh

#!/bin/bash

# testing nested ifs

#

tester=christine

#

if grep $tester /etc/passwd

then

    echo "The user $tester exists on the system."

    if [ -d /home/$tester

    then

        echo "The user $tester has a home directory."

    else

        echo "The user $tester does not have a home directory."

    fi

else

    echo "The user $tester does not exist on the system."

fi
```

```bash
$ ./test5.sh

The user christine exists on the system.

The user christine has a home directory.

$
```

如果我们将 `tester` 改为一个不存在的用户：

```bash
$ ./test5.sh
tester=NoSuchUser
The user NoSuchUser does not exist on the system.

$
```

嵌套的 if 语句允许你创建复杂的逻辑。然而，过多的嵌套 if 语句可能会导致代码难以阅读。在某些情况下，使用其他方法简化逻辑可能更好。

## 第 12 章：使用结构化命令

在第二个 `then` 部分的命令。使用这种嵌套方法可以提供更整洁的代码和更易追踪的逻辑流：

```bash
$ cat test5.sh

#!/bin/bash

# testing nested ifs - using elif

#

tester=NoSuchUser

#

if grep $tester /etc/passwd

then

    echo "The user $tester account exists on this system."

    echo

elif ls -d /home/$tester/

then

    echo "The user $tester has a directory,"

    echo "even though $tester doesn't have an account."

fi

echo "We are outside the nested statements."
```

```bash
$ ./test5.sh

/home/NoSuchUser/
```

用户 NoSuchUser 有一个目录，
尽管 NoSuchUser 并没有账户。
我们已经在嵌套的 if 语句之外了。

这个脚本的问题在于，如果账户和目录都消失了，你将无法收到这些事实的通知。你可以修复这个问题，并进一步改进脚本，让它同时检查“拥有目录的不存在的用户”和“没有目录的不存在的用户”。通过在嵌套的 `elif` 中添加 `else` 语句可以实现这一点：

```bash
$ cat test5.sh

#!/bin/bash

# testing nested ifs - using elif and else

#

tester=NoSuchUser

#

if grep $tester /etc/passwd

then

    echo "The user $tester account exists on this system."

    echo

elif ls -d /home/$tester/

then

    echo "The user $tester has a directory,"

    echo "even though $tester doesn't have an account."

else

    echo "The user $tester does not exist on this system,"

    echo "and no directory exists for the $tester."

fi
```
