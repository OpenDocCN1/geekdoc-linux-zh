

function 按原样编写的话，只有在以超级用户权限运行脚本时才会工作。更好的解决方案是让脚本根据用户的权限调整其行为。我们将在下一章讨论这个问题。

## .BASHRC 文件中的 SHELL 函数

Shell 函数是别名的优秀替代品，也是创建个人使用的小型命令的首选方法。别名在支持的命令和 shell 功能方面有限，而 shell 函数允许任何可以脚本化的内容。例如，如果我们喜欢为脚本开发的 report_disk_space shell 函数，我们可以在 .bashrc 文件中创建一个名为 ds 的类似函数：

```
ds () {
    echo "Disk Space Utilization For $HOSTNAME"
    df -h
}
```

## 小结

在本章中，我们介绍了一种称为自顶向下设计的常见程序设计方法，并看到了 shell 函数如何用于构建其所需的逐步细化。我们还看到了如何使用局部变量使 shell 函数彼此独立以及与它们所在的程序独立。这使得 shell 函数能够以可移植的方式编写，并可通过将其放置在多个程序中而被重用；这是一种节省大量时间的方法。

## 27

## 流程控制：使用 IF 进行分支

![](img/314a0280bc10c5c0de172677_464_0.png)

在上一章中，我们遇到了一个问题。如何使我们的报告生成脚本适应运行脚本的用户权限？解决这个问题需要我们找到一种根据测试结果在脚本内部“改变方向”的方法。在编程术语中，我们需要程序进行分支。

让我们考虑用伪代码表达的一个简单逻辑示例，伪代码是一种面向人类的计算机语言模拟。

- X = 5
- 如果 X = 5，则：
- 说“X 等于 5。”
- 否则：
- 说“X 不等于 5。”

这是一个分支的例子。根据条件“X = 5 吗？”做一件事，“说 X 等于 5”，否则做另一件事，“说 X 不等于 5。”

## if 语句

使用 shell，我们可以按如下方式编写之前的逻辑：

```sh
x=5

if [ "$x" -eq 5 ]; then
    echo "x equals 5."
else
    echo "x does not equal 5."
fi
```

或者我们可以直接在命令行中输入它（稍微缩短）。

```text
[me@linuxbox ~]$ x=5
[me@linuxbox ~]$ if [ "$x" -eq 5 ]; then echo "equals 5"; else echo
"does not equal 5";
fi
equals 5
[me@linuxbox ~]$ x=0
[me@linuxbox ~]$ if [ "$x" -eq 5 ]; then echo "equals 5"; else echo
"does not equal 5";
fi
does not equal 5
```

在这个例子中，我们执行命令两次：第一次将 x 的值设置为 5，结果输出字符串“equals 5”，第二次将 x 的值设置为 0，结果输出字符串“does not equal 5”。

if 语句的语法如下：

```sh
if commands; then
    commands
[elif commands; then
    commands...]
[else
    commands]
fi
```

其中 *commands* 是命令列表。乍一看这有点令人困惑。但在澄清之前，我们必须先看看 shell 如何评估命令的成功或失败。

## 退出状态

命令（包括我们编写的脚本和 shell 函数）在终止时会向系统发出一个值，称为退出状态。该值是一个介于 0 到 255 之间的整数，表示命令执行成功或失败。根据惯例，值为零表示成功，任何其他值表示失败。shell 提供了一个参数供我们检查退出状态。这里我们看到它的实际应用：

```
[me@linuxbox ~]$ ls -d /usr/bin
/usr/bin
[me@linuxbox ~]$ echo $?
0
[me@linuxbox ~]$ ls -d /bin/usr
ls: cannot access /bin/usr: No such file or directory
[me@linuxbox ~]$ echo $?
2
```

在这个例子中，我们执行 ls 命令两次。第一次，命令执行成功。如果我们显示参数 $? 的值，我们会看到它为零。我们第二次执行 ls 命令（指定一个不存在的目录），产生错误，并再次检查参数 $?。这次它包含 2，表示命令遇到错误。一些命令使用不同的退出状态值来提供错误诊断，而许多命令在失败时简单地以 1 退出。手册页通常包含一个名为“Exit Status”的部分，描述了使用的代码。然而，零始终表示成功。

shell 提供了两个极其简单的内置命令，它们除了以 0 或 1 的退出状态终止外什么都不做。true 命令总是执行成功，而 false 命令总是执行不成功。

```
[me@linuxbox ~]$ true
[me@linuxbox ~]$ echo $?
0
[me@linuxbox ~]$ false
[me@linuxbox ~]$ echo $?
1
```

