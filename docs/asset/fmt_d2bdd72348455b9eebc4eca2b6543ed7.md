
由于此命令发生在 `if` 语句（第 3 到 6 行）之前，在执行 `if` 语句时 shell 跟踪将处于激活状态。除非脚本后面显式禁用，否则 shell 跟踪将一直生效直到脚本退出。你将在本章的“Shell 跟踪”部分学习 shell 跟踪对脚本输出的影响。

# 使用 set 禁用调试

除了启用调试模式外，你还可以使用 `set` 命令禁用调试模式，如下：

```
set +option
```

此处的 `option` 是对应表 20.1 中给出的选项的字母。例如，命令

```
$ set +x
```

会禁用 shell 跟踪调试模式。

脚本中启用的所有调试模式都可以以下命令去激活：

```
$ set -
```

# 为单个函数启用调试

`set` 命令最常用的用途之一是在函数执行之前启用特定的调试模式，然后在函数结束时禁用调试。

例如，如果你有一个名为 `BuggyFunction()` 的函数，并且只想在该 particular 函数执行时启用 shell 跟踪调试模式，请使用以下命令：

```
set -x ; BuggyFunction(); set +x ;
```

在这里，调试模式在调用函数之前启用，并在函数完成时禁用。这种方法比在函数内部显式使用 `set` 命令启用调试更受青睐，因为它可以保持函数的实现不变。

© Copyright Macmillan Computer Publishing. 保留所有权利。

# 语法检查

## 为什么你应该使用语法检查

使用详细模式

在处理任何 shell 脚本时，在尝试执行它之前检查脚本的语法。这让你能够修复大多数问题。

要启用语法检查，如下使用 `-n` 选项：

```
/bin/sh -n script arg1 arg2 ... argN
```

此处的 `script` 是脚本名称，`arg1` 到 `argN` 是该脚本的参数。此命令仅在指定的 `script` 发生错误时生成输出。

检查以下脚本的语法（包含行号供你参考）：

```
1 #!/bin/sh

2

3 YN=y

4 if [ $YN = "yes" ]

5     echo "yes"

6 fi
```

你能发现这个错误吗？

如果此脚本存储在文件 `buggy1.sh` 中，按如下方式检查其语法：

```
/bin/sh -n ./buggy1.sh
```

输出看起来如下：

```
./buggy1.sh: syntax error at line 7; 'fi' unexpected
```

这告诉你 shell 尝试读取第 7 行，发现第 6 行的 `fi` 语句是意外的。你可能已经意识到，shell 读取第 7 行的原因是第 4 行的 `if` 语句

```
if [ $YN = "y" ]
```

没有以 `then` 语句终止。此行应该读如下：

```
if [ $YN = "y" ]; ; then
```

做出此更改后，你发现脚本的语法没有问题，因为命令

```
/bin/sh -n ./buggy1.sh
```

没有输出。

## 为什么你应该使用语法检查

在查看了前面的脚本后，你可能会疑惑为什么不直接执行脚本来确定问题。毕竟，命令

```
/bin/sh -n buggy1.sh
```

输出了：

```
buggy1.sh: syntax error at line 7; 'fi' unexpected
```

这告诉你 shell 尝试读取第 7 行，发现第 6 行的 `fi` 语句是意外的。

对于这个脚本，使用语法检查并不总是如此。例如，考虑以下脚本（包含行号）：

```
1 #!/bin/sh
2 Failed() {
3   if [ $1 -ne 0 ]; then
4   echo "Failed. Exiting."; exit 1
5   fi
6   echo "Done."
7 }

9 echo "Deleting old backups, please wait..."
10 rm -r backup > /dev/null 2>&1
11 Failed?
12

13 echo "Make backup (y/n)?"
14 read RESPONSE
15 case $RESPONSE in
16   y)
17     echo "Making backup, please wait..."
18     cp -r docs backup
19     Failed
20     echo "Backup created."
21     ;;
22   n)
23     echo "Backup Skipped."
24     ;;
25 esac
26 echo "."
```

这个脚本至少有三个错误。看看你能找到几个。

如果此脚本在文件 `buggy2.sh` 中，执行它会产生输出：

```
Deleting old backups, please wait...
Done.
Make backup (y/n)?
```

在提示符输入 y 会产生以下错误：

```
buggy2.sh: syntax error at line 21: ') unexpected
```

由于脚本中的错误，你无法进行备份，而且你已经丢失了之前的备份。

由于命令

```
/bin/sh -n buggy1.sh
```

输出了：

```
buggy1.sh: syntax error at line 7; 'fi' unexpected
```

对于这个脚本，使用语法检查并不总是如此。

脚本在检测到错误之前执行那么远，是因为 shell 逐行读取并执行每一行，就像在命令行中执行一样。在这里，shell 读取并执行直到遇到问题。

通过使用 `-n` 选项，脚本不执行。相反，检查每一行是否具有正确的语法。这有助于你避免运行 `buggy2.sh` 时遇到的情况，只报告了：

```
buggy2.sh: syntax error at line 21: ') unexpected
```

# 使用详细模式

现在你知道了为什么应该采用语法检查，你可以追踪问题的根源。

查看 `buggy2.sh` 的第 21 行

```
21 )
```

很难看出 shell 为什么认为括号 `)` 是意外的。有时知道语法错误发生的位置是不够——你必须知道错误发生的上下文。

shell 提供了 `-v`（v 代表 verbose）调试顺序来检查语法错误发生的上下文。当指定此选项时，shell 会打印它正在读取的每一行。

如果你单独发布 `-v` 选项，脚本中的每一行都会执行。因为你想检查语法，所以将 `-n` 和 `-v` 选项组合如下：

```
/bin/sh -nv script arg1 arg2 ... argN
```

如果你使用调试选项执行 `buggy2.sh`

```
/bin/sh -nv ./buggy2.sh
```

输出如下所示（行号供你参考）：

```
1 #!/bin/sh

3 Failed() {

4     if [ $1 -ne 0 ]; then

5         echo "Failed. Exiting." exit 1

6     fi

7     echo "Done."

8 }

10 echo "Deleting old backups, please wait... \c"

11 rm -r backup > /dev/null 2>&1

12

13 Failed ?

14 echo "Make backup (y/n)? \c"

15 read RESPONSE

16 case $RESPONSE in

17 [yY]|[Ee][Ss])

18 echo "Making backup, please wait... \c"

19     cp -r docs backup

20 Failed

21 [nN]|[Nn][Oo])) .buggy2.sh: syntax error at line 21: ' '
```

从这个输出可以看出，shell 错误是显而易见的。问题出现在第 20 行；case 语句的第一个模式没有以 `;;` 终止。为了修复此脚本，请进行更改：

`Failed ;;`

或者

`Failed ;;`

进行此更改后，执行命令

```
/bin/sh -n buggy2.sh
```
