

一个团队，很难理解和维护，通常被称为遗留代码。你可能会在文献中找到遗留代码的不同定义。

一个好的程序头必须至少包含以下项目。此外，你可以根据认为重要或在组织或团队的编码规范中常用的内容插入其他项目。

- 1. 包含脚本的文件名
- 2. 作者姓名
- 3. 编写日期
- 4. 最后修改日期
- 5. 脚本的用途（一到两行）
- 6. 用于实现手头问题解决方案的算法的简要描述

注释行，包括程序头中的每一行，必须以井号（#）开头，如

```
# This is a comment line.
```

然而，注释不必从新行开始；它可以跟随命令，如：

```
set -- `ls -l lab1`  # Assign new values to positional parameters
and
# if the first argument starts with a -, do
not
# consider it an option for the set command.
# This is to handle the output of the ls -l
# command if lab1 is an ordinary file.
```

以下是 set_demo 脚本的示例头。

```
# File Name:        ~/Bourne/examples/set_demo
# Author:           Syed Mansoor Sarwar
# Date Written:     August 10, 1999
# Modified:         May 21, 2004 (by the original author)
# Date Last Modified: July 27, 2014 (by the original author)
# Purpose:          To illustrate how the set command works
# Brief Description: The script runs with a filename as the only command
#                    line argument, saves the filename, runs
#                    the set command
```

# to assign output of ls -il command to positional
# arguments ($1-$9), and displays file name, its
# inode number, file permissions, and its size in bytes.

为了简洁起见，我们在此教材中没有展示所有示例脚本的程序头。

## 12.6 程序控制流命令

程序控制流命令/语句用于确定 shell 脚本中语句执行的顺序。控制脚本流程的语句有三种基本类型：双向分支、多向分支以及一个或多个命令的重复执行。Bourne shell 中用于双向分支的语句是 if，用于多向分支的语句是 if 和 case，用于重复执行某些代码的语句是 for、while 和 until。

### 12.6.1 if-then-elif-else-fi 语句

if 语句最基本的形式用于单向分支，但该语句也可以用于双向和多向分支。以下是多向 if 语句的语法和简要描述。等宽字体中的单词是关键字，必须按语法中所示使用。中括号中的所有内容都是可选的。所有命令列表都旨在帮助你完成手头的任务。

```
SYNTAX
if expression
    then
    [elif expression
        then
            then-command-list]
    ...
    [else
        else-command-list]
fi

Purpose: To implement two-way or multiway branching
```

这里，expression 是一个命令列表。expression 中命令的执行会返回 true（成功）或 false（失败）的状态。我们讨论 if 语句的三个版本，它们共同构成了语句的完整语法和语义。if 语句的第一个版本不带任何可选功能，这就产生了该语句通常用于单向分支的语法。

```
SYNTAX
if expression
    then
        then-commands
fi

Purpose: To implement two-way branching
```

如果 expression 为 true，则执行 then-commands；否则，执行 fi 之后的命令。语句的语义如图 12.1 所示。

expression 可以使用 test 命令进行求值。它评估一个表达式并返回 true 或 false。该命令有两种语法：一种使用关键字 test，另一种使用括号。以下是该命令的简要描述。

```
SYNTAX
test [ expression ]

Or.

[[expression]]

Purpose: To evaluate expression and return true or false status
```

关于这种第二种语法的一个重要点是，普通（内部）括号表示可选的 expression，而等宽（外部）括号是必需的，因为

![](img/02e070097d401d3bf7de4bf1c470b267_511_0.png)

图 12.1 if-then-fi 语句的语义。

