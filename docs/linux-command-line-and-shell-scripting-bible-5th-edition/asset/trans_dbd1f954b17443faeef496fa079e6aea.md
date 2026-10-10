

## 第二部分

### Shell 脚本基础

本部分包含

- 第 11 章
  构建基础脚本
- 第 12 章
  使用结构化命令
- 第 13 章
  更多结构化命令
- 第 14 章
  处理用户输入
- 第 15 章
  呈现数据
- 第 16 章
  脚本控制

![](img/0798d50a0e5dbf1265fbda3832b3e015_264_0.png)

### 构建基础脚本

本章包含

- 使用多个命令
- 创建脚本文件
- 显示消息
- 使用变量
- 重定向输入和输出
- 使用管道
- 执行数学运算
- 扩展脚本

现在你已了解 Linux 系统和命令行的基础知识，是时候开始编写代码了。本章讨论编写 Shell 脚本的基础知识。在你开始编写自己的 Shell 脚本杰作之前，你需要了解这些基本概念。

## 使用多个命令

到目前为止，你已经看到了如何使用 Shell 的命令行界面 (CLI) 提示符输入命令并查看命令结果。Shell 脚本的关键在于能够输入多个命令并处理每个命令的结果，甚至可能将一个命令的结果传递给另一个命令。Shell 允许你将命令串联起来作为一个步骤执行。

如果你想同时运行两个命令，你可以在同一个提示行中输入它们，用分号分隔：

```
$ date ; who
Sun Jun 01 15:36:09 BST 2025
Christine tty2    2025-06-01 15:26
Gamantha  tty3    2025-06-01 15:26
Timothy   tty1    2025-06-01 15:26
user      tty7    2025-06-01 14:03 (:0)
user      pts/0   2025-06-01 15:21 (:0.0)
$
```

如果你输入了这段代码，恭喜你，你刚刚编写了一个 Shell 脚本！这个简单的脚本只使用了两个 Bash Shell 命令。`date` 命令首先运行，显示当前日期和时间，接着是 `who` 命令的输出，显示当前谁登录在系统中。使用这种技术，你可以按意愿串联任意数量的命令，上限为 255 个字符的命令行最大字符计数。

虽然对于小型脚本来说，使用这种技术没问题，但它有一个主要缺点：每次想要运行命令时，你都必须手动输入整个命令。而不是在命令行上手动输入命令，你可以将它们组合到一个简单的文本文件中。当你需要运行命令时，只需简单地运行该文本文件即可。

## 创建脚本文件

要在文本文件中放置 Shell 命令，首先你需要使用文本编辑器（参见第 10 章，“使用编辑器”）创建一个文件，然后将命令输入到文件中。

在创建 Shell 脚本文件时，你应该在文件的第一行指定你正在使用的 Shell。其格式为：

```
#!/bin/bash
```

在普通的 Shell 脚本行中，井号 (#) 用作注释行。Shell 脚本中的注释行不会被 Shell 处理。（但是，Shell 脚本文件的第一行是一个特殊情况，井号后跟感叹号告诉 Shell 使用哪个 Shell 来运行脚本（是的，你可以使用 Bash Shell 运行，但使用另一个 Shell 来执行脚本））。

指定 Shell 后，命令输入到文件的每一行中，后跟回车。如前所述，可以使用井号添加注释。示例如下：

```
#!/bin/bash
# This script displays the date and who's logged on
date
who
```

这就全部了。如果你愿意，可以使用分号并将两个命令放在同一行上，但在 Shell 脚本中，你可以将命令列在单独的行上。Shell 将按照命令在文件中出现的顺序处理它们。

注意还包含了一行以井号符号开头并添加注释的行。以井号符号开头的行（除第一行 `#!` 外）不会被 Shell 解释。这是一种很好的方式，可以为你（和其他人）留下关于脚本中正在发生什么事件的注释，这样当你两年后回来查看时，就能轻松记住你做了什么。

将此脚本保存在名为 test1 的文件中，你就几乎准备好了。在运行新的 Shell 脚本文件之前，仍有几件事需要做。

如果你现在尝试运行该文件，你会稍微失望地看到以下内容：

```
$ test1
bash: test1: command not found
$
```

要克服的第一个障碍是让 Bash Shell 找到你的脚本文件。如果你记得第 6 章“使用 Linux 环境变量”中的内容，Shell 使用一个名为 `PATH` 的环境变量来查找命令。快速查看 `PATH` 环境变量可以说明这个问题：

```
$ echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin
:/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/user/bin $
```

`PATH` 环境变量被设置为仅在少数目录中查找命令。要让 Shell 找到 test1 脚本，你需要做以下两件事之一：

- 将 Shell 脚本文件所在的目录添加到 `PATH` 环境变量。
- 使用绝对或相对文件路径在提示符中引用 Shell 脚本文件。

> 提示
> 某些 Linux 发行版将 `$HOME/bin` 目录添加到 `PATH` 环境变量中。这为每个用户的 `$HOME` 目录创建了一个位置，用于放置 Shell 可以查找并执行的文件。

此示例使用第二种方法告知 Shell 脚本文件的确切位置。请记住，要引用当前目录中的文件，你可以在 Shell 中使用单点运算符：

```
$ ./test1
bash: ./test1: Permission denied
$
```

现在 Shell 成功找到了 Shell 脚本文件，但还有另一个问题。Shell 指示你没有权限执行该文件。快速查看文件权限应该能让你明白这里发生了什么：

```
$ ls -l test1
-rw-r-r-- 1 user user 73 Jun 02 15:36 test1
$
```

当创建新的 test1 文件时，`umask` 值决定了新文件的默认权限设置。由于 `umask` 变量设置为 022（参见第 7 章，“理解 Linux 文件权限”），系统仅创建了对文件所有者具有读/写权限的文件。

下一步是使用 `chmod` 命令（参见第 7 章）授予文件所有者执行该文件的权限：

```
$ chmod u+x test1
$ ./test1
```

```
Sun Jun 01 15:38:19 EST 2025
Christine tty2    2025-06-01 15:26
Samantha tty3     2025-06-01 15:26
Timothy tty1      2025-06-01 15:26
user tty7         2025-06-01 14:03 (:0.0)
user pts/0        2025-06-01 15:21 (:0.0)
$
```

成功！现在所有组件都已就位，可以执行新的 Shell 脚本文件了。

## 显示消息

大多数 Shell 命令会产生自己的输出，并在脚本运行的控制台监视器上显示。然而，很多时候，你会希望添加自己的文本消息，以帮助脚本用户了解脚本内部正在发生的事情。你可以使用 `echo` 命令来实现这一点。如果你将字符串放在命令之后，`echo` 命令可以显示简单的文本字符串：

```
$ echo This is a test
This is a test
$
```

请注意，默认情况下，你不需要使用引号来界定你要显示的字符串。但是，如果你在我的字符串中使用引号，这可能会变得棘手：

```
$ echo Let's see if this'll work
Let's see if this'll work
$
```

`echo` 命令使用双引号或单引号来界定文本字符串。如果你在字符串内使用它们，你需要在文本内使用一种引号，并使用另一种引号来界定字符串：

```
$ echo "This is a test to see if you're paying attention"
This is a test to see if you're paying attention
$ echo 'Rich says "scripting is easy".'
Rich says "scripting is easy".
$
```

现在所有引号都正确显示在输出中。

你可以在 Shell 脚本中任何需要显示额外信息的地方添加 `echo` 语句：

```
$ cat test1
#!/bin/bash
# This script displays the date and who's logged on
echo  The time and date are:
date
echo "Let's see who's logged into the system:"
who
$
```

