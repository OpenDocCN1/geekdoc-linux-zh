
**脚本 15.17 分析：** 当我们运行脚本时，首先按了 `ctrl+z`。它并没有停止脚本。接着我们立即按了 `ctrl+c`，它在打印完 `94` 后停止了脚本。然而，你必须足够快，因为完成所有 `1000` 个数字的显示并不需要长时间。

## 15.7 内置命令

Shell 脚本可以使用 UNIX 中的任何命令或工具。这包括用户创建的工具（脚本）。许多标准命令和工具是如此常见，以至于它们内置在 Shell 本中。这意味着它们是立即可用的；Shell 不需要搜索库来查找并执行命令。这些命令总结在表 15.5 中。

### 表 15.5 内置命令

| 命令 | 描述 |
| --- | --- |
| `:` | 空语句。什么都不做（占位符）。 |
| `.` | 作为命令时，导致其后的命令或工具在当前 shell 中执行，而不是子 shell。 |
| `break` | 强制终止循环或 case 语句。 |
| `case` | 指定为匹配的值要执行的命令。 |
| `cd` | 更改当前目录。 |
| `continue` | 继续循环的下一次迭代。 |
| `eval` | 读取其参数并执行生成的命令。 |
| `exec` | 在另一个 shell 中执行命令。 |
| `exit` | 设置退出状态并退出 shell。 |
| `export` | 将变量标记为可导出。 |
| `expr` | 评估数学表达式。 |
| `for` | 处理列表中的数据。 |
| `if` | 标准条件命令。 |
| `print` | 显示到标准输出上。 |
| `pwd` | 显示当前目录。 |
| `read` | 从标准输入读取一行。 |
| `readonly` | 使参数变为只读。 |
| `return` | 回到调用的 shell。 |
| `select` | 菜单循环。 |
| `set` | 设置变量。 |
| `shift` | 将位置参数向左移动。 |
| `test` | 评估关系、逻辑表达式。 |
| `trap` | 当接收到信号时运行命令。 |
| `type` | 解释 shell 如何使用某个命令。 |
| `ulimit` | 显示或设置资源。 |
| `umask` | 显示或设置文件创建模式。 |
| `unset` | 取消变量设置。 |
| `until` | 循环直到变量为真。 |
| `wait` | 等待子进程完成。 |
| `while` | 当变量为真时循环。 |

### sleep 命令

`sleep` 命令需要一个参数：暂停的秒数。当执行时，它会挂起执行指定的持续时间。它通常在后台执行。例如，如果我们需要联系另一个当前登录的用户，可以创建一个脚本来监控谁在线。当它发现用户已登录时，它会发送消息。这一概念在 15.18 中演示。

脚本 15.18 演示 `sleep` 命令

```
#!/bin/ksh

# 脚本:sleep.scr

# 监控在线并发送消息

# 每分钟检查一次 $1 是否登录

until who | grep "$1" >/dev/null

do

    sleep 60

done

# 在后台运行

# 用户现在登录了

write $1 << MSG

Urgent we talk.

Please call me A.S.A.P!

MSG

$ ./sleep.scr &
```

### 点 命令

脚本技术

在本节中，我们展示了一些用于 Shell 脚本的技巧。许多技巧要求我们处理字符串而不是单词或值。因此，在演示脚本之前，让我们讨论一下当作为参数传递字符串或在脚本中读取字符串会发生什么。

#### 读取字符串

当字符串作为参数传递时，其格式决定了如何将其解析为脚本参数。如果它包含在引号中，会被放在一个参数中。如果没有引号，则每个单词都是一个独立的参数。

脚本 15.19 演示了这一概念。我们首先打印完整参数 (`$*`)，然后单独打印四个位置参数。

### 642 • 第 15 章 • KORN SHELL高级编程

#### 脚本 15.19 演示字符串参数

```
1 #!/bin/ksh -f
2 # 脚本: strArguments.scr
3 # 演示参数格式如何影响 read

5 print All Arguments: $*
6 print Parm1 is: $1
7 print Parm2 is: $2
8 print Parm3 is: $3
9 print Parm4 is: $4
```

执行结果：
```
$strArguments.str Now is the time
All Arguments: Now is the time
Parm1 is: Now
Parm2 is: is
Parm3 is: the
Parm4 is: time
```

```
$strArguments.str "Now is the time"

All Arguments: Now is the time

Parm1 is: Now is the time

Parm2 is: is

Parm3 is: is

Parm4 is: 
```

## 用户交互

虽然许多脚本可以独立运行，但另一些脚本需要交互式输入。这意味着用户必须接收到提示（prompt），而 shell 必须接收回答。在本节中，我们将演示如何让一个 shell 脚本具有交互性。其中许多技术已经在之前的脚本中演示过。

### 创建提示

提示是一种不以换行符结束的输出行，并且需要用户的响应。通常我们在提示的末尾加上一个冒号和一个空格。用户的回答在提示末尾冒号之后输入。脚本 15.20 演示了一个请求文件名的提示。我们打印了提示以进行验证。通常，提示不会在响应中重复出现。在学习该脚本时，请注意提示包含在引号中。之所以需要引号是因为字符串末尾有取消换行的命令。我们本可以只在取消命令周围加引号。

#### 脚本 15.20 提示脚本

```
1 #!/bin/ksh
2 # 脚本: prompt.scr
3 # 演示典型的用户提示

5 print "Enter file name: \c"
6 read fileName
7 print You entered $fileName
```

`$prompt.scr`
输出：
```
Enter file name: payroll.dat
You entered payroll.dat
```

### 问题提示

交互式脚本处理通常必须向用户提问。最常见的问题是：你想继续吗？接下来的脚本会提该问题并根据答案设置标记（flag）。取决于脚本的性质，可能会设置标记，或者脚本可能会带有 `exit` 命令结束。脚本 15.21 展示了我们如何使用提示来提问。

#### 脚本 15.21 问题脚本

```
1 #!/bin/ksh
2 # 脚本 question.scr
3 # 演示问题提示
4 contFlag=2
5 while (( contFlag == 2 ))
6 do
7 print "Do you want to continue [y/n]: \c"
8 read answer
9 case $answer in
10 y|Y) contFlag=1);
11 n|N) contFlag=0);
12 *) print Invalid response.
13 print Usage: 'y' or 'n'.
14 esac
15 done

17 if (( contFlag == 1 ))
18 then
19 print script Continues
20 else
21 print script will stop; exit 1
22 fi
23 # 脚本其余部分
```

执行结果：
```
$ question.scr
Do you want to continue [y/n]: z
Invalid response.
Usage: 'y' or 'n'.
Do you want to continue [y/n]: y
script Continues
```

```
$ question.scr

Do you want to continue [y/n]: N

script will stop
```

**脚本 15.21 分析：** 这个脚本中有一个非常重要的点需要学习。许多脚本编写者犯了一个错误，即只测试一个答案（例如 yes），并设置默认答案。这是一种容错率很低的技术。

## 第 15.8 节 脚本技术 • 647

#### 脚本 15.24 带有值的选项

```
Output:

Processing x option here

Value of the x option is XXX

Processing y option here

Value of the y option is YYY

Processing in body: Parameters contain -x XXX -y YYY
```
