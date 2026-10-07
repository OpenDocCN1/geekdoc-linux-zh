
在这里，`/etc/shells` 的文本被包含在命令行中，因此如果读取它，就是 `ls -1 /bin/bash /bin/sh /bin/tcsh /bin/csh /bin/ash /bin/bsh /bin/bash2 /bin/ksh`。（记住，每个换行符只是将命令行周围的单词分隔开。）

我们可以使用反引号来转义几个 PS 提示符部分的转义序列；`whoami` 可以被替换为 `whoami -d -f 1`，`h` 可以被替换为 `hostname`。因此，使用该命令设置我的默认 bash 提示符：`PS1={\u\h \W}`。`$` 可以被替换为 `PS1=\whoami \hostname -d -f 1\$$`。我无法转义的一个字符是 `$`，它为 root 用户以外的所有用户打印美元符号，而在那种情况下，它打印井号（#）。¹

在大多数方面，反引号类似于 `xargs`，但有两个显著的差异点。首先，`xargs` 只能将信息附加到命令行的末尾。其次，`xargs` 避免了命令行长度的限制，而反引号没有。当反引号中的表达式返回大量数据时（例如很长的文件列表），可能会导致生成的命令行过长而无法处理。

如果你不完全确定何时使用单引号何时使用双引号，我的建议是使用单引号，除非你需要将变量作为字符串的一部分进行解释。像是对提示词字符串（prompt strings）进行适当解释的情况相对少见，许多用户忽略它们也不会产生太大危险。对于那些真正喜欢了解系统的用户——也包括你——获得详细的解释会有帮助，即使这些解释可能没有即时的用处。

## 练习题

- 8. 创建名为 `THIRDARM` 的变量，包含数字 4。显示字符串 `My third arm is number XYZ of 1000`，其中 XYZ 被替换为变量 `THIRDARM` 变量的内容。
- 9. 显示字符串 `The serial number of my third arm is stored in the variable $THIRDARM`，其中 `$THIRDARM` 不会被该变量的内容替换。
- 10. 显示字符串 `Today's date is:`，随后显示今天的日期。
- 11. 设置名为 `DATELINE` 的变量，内容为 `Today's date is: `。
- 12. 将 `DATELINE` 设置为一个值，使得每当运行 `eval echo '$DATELINE'` 命令时，都会显示短语 `Today's date is:` 后接当前日期。（该命令会以显示的方式解释字符串。）

硬链接 * 软链接 * 重定向与重定向标准错误 * 名称查找 * 通过 POP3 路由 * 文件名通配与正则表达式 * 交互式命令行编辑 * 历史替换 * 作业控制 * 变量与引用 * 控制 * 条件执行 * WHILE 和 UNTIL 循环 函数 * 窗口客户端/服务器 小部件与工具包 配置 X 权限所有权 * 用户与组 * HARE 软链接 * 重定向与管道 * 重定向标准错误 名称查找 * 路由 读修改 (MA) 和正则表达式 * 文件名通配与正则表达式 * 交互式命令行编辑

## 条件执行与循环

计算机的另一个基本属性是条件执行。简单来说，这意味着计算机可以根据情况改变它们的行为。这听起来完全是显而易见的，但请考虑一下它的影响：如果没有改变并根据输入采取行动的能力，计算机只是一台昂贵的计算器。没有条件执行，用户输入没有任何意义，因为没有办法说“如果用户选择保存，则将文件存储在磁盘上；但如果用户选择加载，则询问从磁盘读取哪个文件。”广义地说，条件执行是程序员说“如果是这样，就执行此；否则执行那件事”的能力。

条件执行也让循环成为可能。循环正如其字面意思是一组重复的指令。它可能会对列表中的每个项目执行某些操作。它可能会重复固定次数，也可能等待特定条件的满足，从用户那里接收特定的响应。在本章中，我们将讨论如何同时使用条件执行和循环在 shell 中更高效地工作。一如既往，`bash` 是参考平台，尽管本章中的所有内容在 `ksh` 上也应该同样运行，而 `tc` 和 `C Shell` 是不同的，本章中的任何内容在这些 shell 中都不应该运行。（它们有具有等功能的语法，但我没有介绍。如果你对这些 shell 感兴趣，互联网或书店会有足够的资源。）

## 顺序执行

要理解条件执行，我们必须首先理解它的替代方案：顺序执行正如其字面意思：一个命令接一个命令地运行，无论情况如何。这不等同于一次只输入一个命令，你可能会根据已经发生的情况而输入不同的命令。例如：

```
[jon@frog ~]$ cd new_directory

bash: new_directory: No such file or directory

[jon@frog ~]$ mkdir new_directory

[jon@frog ~]$ cd new_directory

bash: new: No such file or directory

[jon@frog ~]$ cd new_directory

[jon@frog new_directory~]$
```

我在那段命令序列中犯了几个错误。因为我是在交互式地使用这个 shell，所以我能够纠正这些错误。这是一种特殊的条件执行。

Unix 使用分号 (`;`) 来分隔用于顺序执行的命令。从左到右顺序执行每个命令，而不考虑上一个命令的成功或失败：

```
[jon@frog ~]$ mkdir the_flintstones; cd the_flintstones; touch barney

bash: the flintstones: no such file or directory

[jon@frog ~]$ pwd
```

```
/home/jon
[jon@frog ~]$ ls the_flintstones barney
barney
```

`the_flintstones:` 

在这种情况下，第一个命令执行成功了，创建了 `the_flintstones` 目录，但第二个命令由于拼写错误失败了。尽管如此，第三个命令仍然在当前目录下创建了 `barney`。这当然不是我们想要做的。

尽管顺序执行存在很多问题，但这样做既方便又简单。很多时候，我也会偶尔使用它。它是在单行上输入多个命令的快捷方式，但出于显而见的原因应该谨慎使用。永远不要用顺序执行 `rm` 文件，因为……

## 条件执行

为了让这个想法生效，shell 必须知道上一个命令是否成功完成。退出状态（exit status）是程序返回的数字。零通常表示成功，而任何非零表示错误。不同的程序可能返回不同的值，但在 `$` 总是成功之外。

关于退出状态的另一种说法是，shell 返回的是“是，这成功了”或“否，这没有成功”。如果你将这些响应简短为 `yes` 和 `no`，你会发现它们等同于布尔值 `true` 和 `false`，即我们的老朋友 1 和 `$0`。但在这种情况下，`true` 等于 `$0` 而 `false` 等于 1，这颠转了传统的含义。你可以通过系统中存在的两个可执行文件来验证这一点：Unix 实际上有输出 `true` 和 `false` 的程序。

```
[jon@frog tmp]$ true
[jon@frog tmp]$ echo $?
0
```

```
[jon@frog tmp]$ false
[jon@frog tmp]$ echo $?
1
```

`grep` 找到正则后返回 0。

```
[jon@frog tmp]$ grep jon /etc/passwd
jon:x:500:500:jon:/home:/bin/bash
[jon@frog tmp]$ echo $?
0
```

`grep` 未找到正则后返回 1……

```
[jon@frog tmp]$ grep papasurf /etc/passwd
[jon@frog tmp]$ echo $?
1
```

……但 `grep` 找不到文件返回 2。

```
[jon@frog tmp]$ grep papasurf smurf-village
grep: smurf-village: No file or directory
[jon@frog tmp]$ echo $?
2
```

## 退出状态

退出状态是程序返回的数字。零通常表示成功，而任何非零表示错误。不同的程序可能返回不同的值，但在 `$` 总是成功之外。（有时非零也表示成功，但这很罕见。）

`grep` 在找不到文件时总是返回 2，但不能保证其他单个程序也会返回相同的值。某些程序（包括 GNU 版本的 `grep`）实际上会在主页上记录不同退出状态值的含义。如果退出状态值没有记录，请假设它们在程序的不同版本之间是一致的，但在 `$` 总是成功之外。

## 条件执行与循环

最后，请注意错误代码并不总是较小的数字。`bash` 中“未找到命令”的错误代码是 127：

### &&, || 和 !

Unix 提供了一种机制根据上一个命令的退出状态来执行后续命令的机制。这两者的工作原理类似于顺序执行，但将分号替换为了不同的符号。如果上一个命令执行成功，则执行另一个命令，用双 ampersand（`&&`）分隔两个命令；如果上一个命令失败，则使用双管道符（`||`）。这些符号与布尔运算符 AND（与）和 OR（或）相关：

`&&` 和 `||` 的一个重要用途是组合一串顺序执行的命令，当其中任何一个命令失败时执行将停止。让我们重新尝试之前的例子：

由于 `cd` 命令执行失败，`bash` 没有执行 `touch` 命令，文件 `barney` 从未被创建。这使得执行长命令字符串时变得更安全。`||` 的主要用途是提供错误检测和有用的错误信息，或者纠正错误：

```bash
$jon@frogbog jon$ cd _jetsons | mkdir _jetsons && cd _jetsons
bash: no such file or directory
$jon@frogbog the_jetsons$ cat george || echo "George isn't home right now."
cat: No such file or directory
George isn't home right now.
$jon@frogbog the_jetsons$
```

在第一个示例中，我尝试进入 `_jetsons` 目录，如果它不存在，则创建目录并切换进去。它报告了错误，但命令其余部分因为第一个命令失败而失败，且目录并没有被创建。（这样做有更好的方法，我们将在章节稍后的部分讨论，但现在它是一个很好的例子。）

在第二个示例中，我 `cat` 了 `george` 文件的内容，但如果它不存在，我会打印一条相应的错误信息。（如果文件存在但我没有权限读取它，结果也是相同的）。这两个例子都存在一个问题，尽管 shell 对某些命令的失败发出了抱怨。更好的做法是将 STDERR 重定向到 `/dev/null` 并保持屏幕整洁：

```bash
[jonfrog] the_jetsons$ cd && rm -rf the_jetsons
[jonfrog] jonj$ cd jetsons 2>/dev/null || mkdir the_jetsons && cd \the_jetsons
```

```bash
[jonfrog] the_jetsons$ cat gecho 2>/dev/null || echo "gecho isn't home\
right now."
George isn't home right now.
[jonfrog] the_jetsons$
```

搞定！没有多余的消息干扰我们漂亮整洁的屏幕。将 `&&` 运算符理解为“如果是，那么……”将 `||` 运算符理解为“如果不是，那么……””，会让它们的用法更加清晰。

`!` 不要与历史记录回溯命令混淆，它等同于布尔 NOT（非）；它否定其后命令的退出状态。你必须在感叹号后面加一个空格，以便系统区分感叹号是用于历史回溯还是用于 NOT。

```bash
[jonfrog] jonj$ echo "Test"
Test
[jonfrog]jonj$ echo $0
[jonfrog]jonj$ echo "Test"
Test
[jonfrog]jonj$ echo $1
[jonfrog]jonj$ ! cd nothing-to-see-here
bash: nothing-to-see-here: No file or directory
[jonfrog]jonj$ echo $0
[jonfrog]jonj$ ! cd tmp
```

在实践中，大多数用户会反转 `&&` 和 `||` 的用法，而不是放在命令行前面，尽管后者方法更符合用户的意图。在编写他人最终可能需要维护的 shell 脚本时这很重要，尽管在实践中几乎没有区别。此外，任何由 `;`、`&&` 或 `||` 连接的命令组都被称为列表。

## If/Then/Else

`if`、`then` 和 `else` 命令可能是 Bourne Shell 家族中最常用的控制结构。`if` 后面跟着一个命令或一个命令列表，该命令列表返回真 (0) 或假 (1)。后面紧跟着 `then`，它是当 `if` 表达式被求值为真时要执行的命令列表。在最简单的情况下，由于这个命令列表由 `fi` 结束，标记该结构的结束：

```bash
[jon@frogbog jen$] if cd tmp
> then
> echo 'Fer, dude!'
> echo 'I've changed your directory.'
> fi
Fer sure, dude!
I've changed your directory.
[jon@frogbog tmp$]$
```

在这种情况下，命令 `cd tmp` 执行成功，因此也运行了 `echo 'Fer, dude!'` 和 `echo 'I've changed your directory.'`。让我们在 `tmp` 内部尝试，让 `cd` 命令失败：

```bash
[jon@frogbog jen$] if cd tmp
> then
> echo 'Fer, dude!'
> echo 'I've changed your directory.'
> fi
bash: np: No such file or directory
[jon@frogbog tmp$] pwd
/home/jon/tmp
```

现在再来一次，将 `cd` 命令的 STDERR 重定向到 `/dev/null` 以免它弄乱屏幕，并添加一个 `else` 子句以提供风格一致的错误信息：

```bash
[jon@frogbog tmp$] cd ..
[jon@frogbog jen$] if cd tmp 2>/dev/null
> then
> echo 'Fer, dude!'
> echo 'I've changed your directory.'
> else
> echo 'Directory not found.'
> fi
Directory not found.
```

搞定！没有多余的消息干扰我们漂亮整洁的屏幕。将 `&&` 运算符理解为“如果是，那么……”将 `||` 运算符理解为“如果不是，那么……””，会让它们的用法更加清晰。

## 176

# 第二部分 Shell 概念

```
> then
  echo "The file is empty"
else
  echo "No file"
fi
else
  echo "File not empty"
```

对于文件不存在，原始问题并没有要求我们区分不存在的文件和为空的文件。虽然我们可以在上一个问题中简单地对这两种情况给出相同的响应，但不会这样做。相反，我们想要测试两个条件的逻辑与。`test` 命令的 `-a` 选项允许你在 `-a` 的两侧对两个测试条件进行 AND 操作：

```bash
[jon@frog tmp]$ test -e testfile -a ! -s testfile
> then
  echo "The file is empty"
else
  echo "No file or file not empty"
fi
No file is not empty
[jon@frog tmp]$ touch testfile
[jon@frog tmp]$ if test -e testfile -a ! -s testfile
> then
  echo "The file is empty"
else
  echo "No file or file not empty"
fi
```

```bash
The file is empty
[jon@frog tmp]$ echo "stuff" > testfile
[jon@frog tmp]$ if test -e testfile -a ! -s testfile
> then
  echo "The file is empty"
else
  echo "No file or file not empty"
fi
No file is not empty
```

最后，一个解决该问题的优雅方案！与 `-a` 选项互补的是 `-o` 选项，它是对该选项两侧条件的逻辑 OR 操作。例如，假设我想知道一个文件是目录还是符号链接。我可以使用条件 `-i testfile -o -d testfile` 来测试这些条件中是否有一个为真。

`test` 命令有一个快捷方式。不需要写出整个 `test` 单词，可以将测试条件包含在方括号中。这不仅减少了两个字符，还能让被测试的条件更加一目易然。

# 条件执行与循环 第 8 章

（当然，这假设你已经熟悉 `test` 命令使用的短选项。详细信息请参阅 `man test`。）

```bash
[jon@frogbog jon$ if [ ! -d tmp -a ! -e tmp ]
> then
    mkdir tmp
> else
    echo "Directory or file tmp exists"
```
