
`/home/rich/.bash_history` `/home/rich/.bash.profile`

`/home/rich/.bash_logout` `/home/rich/.bashrc`

```
```

然而，如果你将 `tester` 变量设置为系统中不存在的用户，会发生什么：

```bash
$ .test3
$
```

这并不完全令人兴奋。如果我们能显示一条小消息，说明在系统中没有找到该用户名就太好了。好吧，我们可以做到，使用 `if-then` 语句的另一个功能：

> 你可能会在某些脚本中看到 `if-then` 语句的另一种形式：

```bash
if command; then
commands
fi
```

通过在要求值的命令末尾加上一个分号，你可以将 `then` 语句包含在同一行，这看起来更像某些其他编程语言处理 `if-then` 语句的方式。

# if-then-else 语句

在 `if-then-else` 语句中，你对于命令是否成功只有一种选择之外。如果命令返回非零退出状态码，`bash` shell 将移动到脚本中的下一个命令。在这种情况下，如果能够执行另一组命令就太好了。这正是 `if-then-else` 语句的用途。

`if-then-else` 语句在语句中提供了另一组命令：

```bash
if command
    commands
else
    commands
fi
```

如果语句行中的命令返回退出状态码为 `0`，则执行 `then` 部分列出的命令，就像普通的 `if-then` 语句一样。如果语句行中的命令返回非零退出状态码，`bash` shell 将执行 `else` 部分的命令。

现在你可以将测试脚本修改如下：

```bash
$ cat test4
#!/bin/bash
# testing the else section
testeruser=badtest
if grep $testuser /etc/passwd
then
    echo The files for user $testuser:
    ls -a /home/$testuser/.b*
else
    echo "The user name $testuser doesn't exist on this system"
fi
$ .test4
nThe user name badtest doesn't exist on this system
$
```

这更符合用户习惯。就像 `then` 部分一样，`else` 部分也可以包含多个命令。`fi` 语句划分了 `else` 部分的结束。

# 嵌套 if

有时你必须在脚本代码中检查几种情况。与其编写多个独立的 `if-then` 语句，你可以使用 `else` 部分的替代版本，称为 `elif`。

`elif` 使用另一个 `if-then` 语句继续 `else` 部分：

```bash
if command1
then
  commands
elif command2
then
  more commands
fi
```

`elif` 语句提供了另一个待求值的命令，类似于原始的 `if` 语句行。如果 `elif` 命令的退出状态码为零，`bash` 执行第二个 `then` 语句部分。你可以继续将 `elif` 语句连接在一起，创建一个巨大的 `if-then-elif` 组合：

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

每个命令块的执行取决于哪个命令返回零状态。记住，`bash` shell 会按顺序执行 `if` 语句，只有第一个返回零状态的会导致部分被执行。在后面的“Case 命令”部分，你将看到如何使用 `case` 命令代替嵌套大量的 `if-then` 语句。

# test 命令

你在 `if` 语句行中看到的所有都是普通的 shell 命令。你可能在想 `if-then` 语句是否具有评估命令退出状态码以外的任何条件的能力。

答案是，不能。然而，`bash` shell 中有一个非常实用的工具可以帮助我们评估其他事物，并配合 `if-then` 语句。

`test` 命令为 `if-then` 语句提供了一种测试不同条件方法。如果 `test` 命令列出的条件为真，则 `test` 命令以零退出状态码退出，这使得 `if-then` 语句的行为与其相似。

## 第二部分 Shell 脚本基础

语句在其他编程语言中也同样工作。如果条件为假，`test` 命令将以状态 `1` 退出，这会导致 `if-then` 语句失败。

`test` 命令的格式非常简单：

```
test condition
```

条件是一系列供 `test` 命令评估的参数和值。当用于 `if-then` 语句时，`test` 命令看起来如下：

```
if test condition
then
commands
fi
```

`bash` shell 提供了另一种方式在 `if-then` 语句中声明 `test` 命令：

```bash
if [ condition ]
then
commands
fi
```

方括号 `[]` 定义了在 `test` 命令中使用的条件。请注意：在第一个括号之后必须有一个空格，在最后一个括号之前也有一个空格，否则你将收到错误信息。

`test` 命令可以评估的比较有三类：

- 数字比较
- 字符串比较
- 文件比较

接下来的章节将描述如何在 `if-then` 语句中使用这些类别的测试。

## 数字比较

使用 `test` 命令最常用的方法是对两个数值进行比较。表 9-1 显示了用于测试两个值的条件参数列表。

数字测试条件可用于评估数字和评估变量。这里有一个示例：

```bash
$ cat test5
#!/bin/bash
# using numeric test comparisons
val=10
```

```bash
val2=11
if [ $val1 -gt 5 ]
then
  echo "The test value $val1 is greater than 5"
fi
if [ $val1 -eq $val2 ]
then
  echo "The values are equal"
else
  echo "The values are different"
fi
```

### 表 9-1 test 数字比较

| 比较符 | 描述 |
|---|---|
| n1 -eq n2 | 检查 n1 是否等于 n2 |
| n1 -ge n2 | 检查 n1 是否大于或等于 n2 |
| n1 -gt n2 | 检查 n1 是否大于 n2 |
| n1 -le n2 | 检查 n1 是否小于或等于 n2 |
| n1 -lt n2 | 检查 n1 是否小于 n2 |
| n1 -ne n2 | 检查 n1 是否不等于 n2 |

第一个测试条件：
`if [ $val1 -gt 5 ]`
测试变量 `val1` 的值是否大于 `5`。第二个测试条件：
`if [ $val1 -eq $val2 ]`
测试变量 `val1` 的值是否等于变量 `val2` 的值。运行脚本并观察结果：

```
$ ./test5
The test value 10 is greater than 5
The values are different
$
```

两个数字测试条件都按预期进行了评估。

## Shell 脚本基础

尽管，数字测试条件存在局限性。尝试这个脚本：

```bash
$ cat test6
#!/bin/bash
# testing floating point numbers
vall=`echo "scale=4; 10 / 3 " | bc
echo The test value is $vall
if [ $vall -gt 3 ]
then
echo The result is larger than 3
fi
$ ./test6
The test value is 3.3333
./test6 line 5: [ : 3.3333: integer expression expected
$
```
