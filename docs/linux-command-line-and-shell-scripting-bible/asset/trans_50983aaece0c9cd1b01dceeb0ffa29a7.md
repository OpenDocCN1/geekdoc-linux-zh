

## 表 9-4

## 双括号命令符号

| 符号 | 说明 |
| --- | --- |
| val++ | 后置自增 |
| val-- | 后置减 |
| ++val | 前置自增 |
| --val | 前置减 |
| ! | 逻辑取反 |
| ~ | 位运算取反 |
| ** | 幂 |
| << | 左移 |
| >> | 右移 |
| & | 位运算布尔与 |
| | | 位运算布尔或 |
| && | 逻辑与 |
| || | 逻辑或 |

注意，在双括号内的表达式中，你不需要转义大于符号。这是双括号命令提供的另一个高级功能。

## 使用双括号

双括号命令为字符串比较提供了高级功能。双括号命令的格式为：

```
[[ expression ]]]
```

双括号表达式使用 `test` 命令中标准的字符串比较。然而，它提供了一个 `test` 命令不具备的额外功能：模式匹配。

在模式匹配中，你可以定义一个正则表达式（在第 17 章详细讨论），并将其与字符串值进行匹配：

```
$ cat test24
#!/bin/bash
# using pattern matching
```

```
if [[ $USER == r* ]]
then
    echo "Hello $USER"
else
    echo "Sorry, I don't know you"
fi
$ ./test24
Hello rich
$
```

双括号匹配 `$USER` 环境变量以检查它是否以字母 `r` 开头。如果是，则比较成功，shell 将执行 `then` 部分的命令。

## case 命令

你经常会发现自己正试图评估一个变量的值，在一组可能的值中寻找特定的值。在这种情况下，你最终不得不写一个长长的 `if-then-else` 语句，如下所示：

```
$ cat test25
#!/bin/bash
# looking for a possible value

if [ $USER = "rich" ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit"
elif [ $USER = barbara ]
then
    echo "Welcome $USER"
    echo "Please enjoy your visit"
elif [ $USER = testing ]
then
    echo "Special testing account"
elif [ $USER = jessica ]
then
    echo "Don't forget to logout when you're done"
else
    echo "Sorry, you're not allowed here"
fi
$ ./test25
Welcome rich
nPlease enjoy your visit
$
```

`elif` 语句继续进行 `if-then` 检查，为单变量比较变量寻找特定的值。

与其被迫编写所有的 `elif` 语句来继续检查同一个变量值，你可以使用 `case` 命令。`case` 命令以列表形式的形式检查单个变量的多个值：

```
* case variable in
* pattern1 | pattern2) commands1;
* pattern3) commands2;
*) default commands;
esac
```

`case` 命令将指定的变量与不同的模式进行比较。如果变量匹配模式，shell 将执行为该模式指定的命令。你可以在同一行中列出多个模式，并使用管道符 `|` 分隔每个模式。星号符号 `*` 是用于匹配不符合任何列出模式的值的兜符。这里是将 `if-then-else` 程序转换为使用 `case` 命令的示例：

```
$ test26
#!/bin/bash
# using the case command
```

```
case USER in
rich | barbara)
echo "Welcome, $USER"
echo "Please enjoy your visit";
testing)
echo "Special testing account";
jessica)
echo "Don't forget to log off when you're done";
*)
echo "Sorry, you're not allowed here";
$ ./test26
Welcome, rich
nPlease enjoy your visit
$
```

`case` 命令提供了一种为每个可能的变量值指定各种选项的清晰方法。

## 总结

结构化命令允许你更改 shell 脚本的正常执行流。最基本的结构化命令是 `if-then` 语句。该语句允许你评估一个命令，并根据该命令的结果执行其他命令。

你可以扩展 `if-then` 语句，包含一组 bash 在指定命令失败时也执行的命令。`if-then-else` 语句允许你仅在被评估的命令返回非零退出状态码时执行命令。

## 第二部分 Shell 脚本基础

你可以使用 `elif` 语句将多个 `if-then-else` 语句连接起来。`elif` 等同于使用 `else` 语句，当被评估的原始命令失败时提供额外的检查。

在脚本中，你将不再评估一个命令，而是想要评估一个条件，例如数值、字符串的内容或文件或目录的状态。`test` 命令为你提供了一种简单的方法来评估所有这些条件。如果条件评估为真，`test` 命令为 `if-then` 语句产生零退出状态码。如果条件评估为假，`test` 命令为 `if-then` 语句产生非零退出状态码。

方括号 `[` 是一个特殊的 bash 命令，是 `test` 命令的同义词。你可以在 `if-then` 语句中将测试条件包含在方括号内，以测试数值、字符串。

## 第 10 章

### 更多结构化命令

双括号表达式提供了一个 `test` 命令不具备的额外功能：模式匹配。在模式匹配中，你可以定义一个正则表达式（在第 17 章详细讨论），并将其与字符串值进行匹配。

方括号 `[` 是一个特殊的 bash 命令，是 `test` 命令的同义词。你可以在 `if-then` 语句中将测试条件包含在方括号内，以测试数值、字符串。

### for 命令

`for` 命令最基本的用法是遍历在 `for` 命令内部定义的值列表。`for` 命令的基本格式为：

```
for var in list
  commands
```

你需要在列表中提供迭代中使用的系列值。有若干种不同的方法可以指定列表中的值。

### 读取列表中的值

`for` 命令最基本的用法是遍历在 `for` 命令内部定义的值列表：

```
$ test1
#!/bin/bash
# basic for command
```

```
for test in Alabama Arkansas California Colorado
do
  echo The next state is $test
done
$ ./test1
The next state is Alabama
The next state is Alaska
The next state is Arizona
The next state is Arkansas
The next state is California
The next state is Colorado
$
```

当 `for` 命令每次遍历提供的值列表时，它会将列表中的下一个值赋值给 `test` 变量。`$test` 变量像任何其他脚本变量一样在 `for` 命令语句中使用。在最后一次迭代之后，`test` 变量在 shell 脚本的剩余部分中仍然有效。它保留了最后迭代的值（除非你更改了它的值）。

