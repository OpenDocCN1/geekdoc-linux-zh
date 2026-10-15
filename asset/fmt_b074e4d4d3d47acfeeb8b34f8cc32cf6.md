
# 第二部分：Shell 脚本基础

```bash
$ ./test.sh

/home/NoNoSuchUser/

The user NoNoSuchUser has a directory, even though NoSuchUser doesn't have an account.

We are outside the nested if statements.

$ sudo rmd /home/NoNoSuchUser/

[sudo] password for christine:

$ ./test.sh

ls: cannot access '/home/NoNoSuchUser': No such file or directory

The user NoNoSuchUser does not exist on this system, and no directory exists for the NoSuchUser.

We are outside the nested if statements.

$ 
```

在 `/home/NoSuchUser` 目录被删除且测试脚本执行 `elif` 语句之前，返回了零退出状态。因此，`elif` 代码块中的语句被执行了。在删除 `/home/NoSuchUser` 目录后，`elif` 语句返回了非零退出状态。这导致 `elif` 块中 `else` 块的被执行。

> 请记住，使用 `elif` 语句时，紧随其后的任何 `else` 语句仅适用于该 `elif` 代码块。它们不是前面的 `if-then` 语句块的一部分。

你可以继续将 `elif` 语句连接在一起，创建一个巨大的 `if-then-elif` 组合体：

```bash
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

# 第 12 章：使用结构化命令

每个命令块的执行取决于哪个命令返回了零退出状态码。记住，Bash Shell 会按顺序执行 `if` 语句，只有第一个返回零退出状态的语句会导致 `then` 部分被执行。

尽管使用 `elif` 语句后代码看起来更整洁，但遵循脚本的逻辑仍然可能令人困惑。在“考虑 case 命令”一节中，你将看到如何使用 `case` 命令，而不是嵌套大量的 `if` 语句。

## 尝试 test 命令

到目前为止，你在 `if` 语句中看到的所有都是普通的 Shell 命令。你可能在想，Bash `if` 语句是否具有评估命令退出状态以外的任何条件的能力。

答案是否定的，不能。但是，Bash 中可用的一个简洁工具可以帮你使用 `if-then` 语句评估其他事情。

`test` 命令提供了一种在 `if-then` 语句中测试不同条件的方法。如果 `test` 命令列出的条件评估为 **真**，它返回零退出状态。这使得 `if-then` 语句的行为与其他编程语言中的 `if-then` 语句相同。如果条件为 **假**，`test` 命令返回非零退出状态，导致 `if-then` 语句退出。

`test` 命令的格式非常简单：

```bash
test condition
```

条件是 `test` 命令评估的一系列参数和值。在 `if-then` 语句中，`test` 命令如下：

```bash
if test
then
  commands
fi
```

如果你漏掉了 `test` 命令的条件部分，它会返回非零退出状态（假）并触发 `else` 块：

```bash
$ cat test6.sh

#!/bin/bash

# testing the test command
#
if test
then
  echo "No expression returns a True"
else
  echo "No expression returns a False"
fi
```

# 第二部分：Shell 脚本基础

*(注：源文本中部分 OCR 存在冗余和乱码，此处已处理为连贯的叙述流。）*

# 第 12 章：使用结构化命令

# 表 12-2 字符串比较测试

| 比较 | 说明 |
|---|---|
| str1 = str2 | 检查 str1 是否与字符串 str2相同 |
| str1 != str2 | 检查 str1 是否不等于 str2。 |
| str1 < str2 | 检查 str1 是否小于 str2。 |
| str1 > str2 | 检查 str1 是否大于 str2。 |
| -n str1 | 检查 str1 的长度是否大于零。 |
| -z str1 | 检查 str1 的长度是否为零。 |

以下章节介绍了各种各种字符串比较方法。

## 查看字符串相等性

对于字符串，相等和不等于条件是非常自而易见的。判断两个字符串是否相同很容易。

```bash
$ cat string_test.sh

#!/bin/bash

# 使用字符串测试评估
#
tester=christine
#
if [ $tester = christine ]
then
  echo "The tester variable contains: christine"
else
  echo "The tester variable contains: $tester"
fi
$
./string_test.sh
The tester variable contains: christine
$
```

此外，使用不等于字符串比较允许你确定两个字符串是否具有相同的值：

```bash
$ cat string_not_test.sh

#!/bin/bash

# 使用字符串测试不相等评估
#
tester=rich
#
if [ $tester != christine ]
then
  echo "The tester variable does NOT contain: christine"
```

```bash
else
  echo "The tester variable contains: christine"
  fi
  $ ./string_not_test.sh
  The tester variable does NOT contain: christine
  $
```

请记住，在比较字符串相等性时，测试比较会考虑所有的标点符号和大小写。

## 查看字符串顺序

尝试确定一个字符串小于或大于另一个字符串时开始变得复杂。程序员在尝试使用测试条件中的大于或小于功能时，经常有两个问题困扰他们：

- 大于和小于号必须转义，否则 shell 将它们用作重定向符号，并将字符串值视为文件名。
- 大于和小于的顺序与 `sort` 命令使用的顺序不同。

第一项可能会在编写字符串时导致巨大的问题，且往往无法被察觉。以下是初学者脚本程序员有时发生的情况示例：

```bash
$ cat bad_string_comparison.sh

#!/bin/bash

# 错误使用字符串比较
#
string1=soccer
string2=zorbfootball
#
if [ $string1 > $string2 ]
then
  echo "$string1 is greater than $string2"
else
  echo "$string1 is less than $string2"
fi
$ ./bad_string_comparison.sh
soccer is greater than zorbfootball
$
$ ls z*
```

通过在脚本中使用大于号本身，不会产生错误，但结果是错误的。脚本将大于号解释为输出重定向（详见第 15 章）。因此，它创建了一个名为 `zorbfootball` 的文件。由于重定向成功完成，测试条件返回零退出状态码，`if` 语句将其评估为执行成功！

要修复这个问题，你需要使用反斜杠 (`\`) 正确地转义大于号：

```bash
$ cat good_string_comparison.sh

#!/bin/bash

# 正确使用字符串比较
#
string1=soccer
string2=zorbfootball
#
if [ $string1 \> $string2 ]
then
    echo "$string1 is greater than $string2"
else
    echo "$string1 is less than $string2"
fi
$
rm -i zorbfootball
```
