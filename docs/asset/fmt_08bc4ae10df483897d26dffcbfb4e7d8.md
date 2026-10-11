
```bash
count=10
```

要使用变量，使用带有 `$` 的变量名。以下是示例：

```bash
echo $count
```

## 调用函数

你可以将一组命令组合成函数并在稍后调用它。这是一个接受两个参数并打印它们的简单示例：

```bash
#!/bin/sh
hello() {
  echo -n "Hello, "
  echo $1
  echo $2
}
```

当你运行此脚本时，它显示如下输出：

```
Hello, Jane

```

## 控制流程

在脚本中，你可以使用 `if`、`for`、`while` 等特殊命令控制执行流——即命令执行的顺序。这些控制语句使用命令的退出状态决定下一步。任何命令执行时都会返回一个退出状态——一个指示命令是否成功的数值值。按照惯例，退出状态为零表示命令成功。非零退出状态表示命令出现问题。

例如，假设你想在使用 `vi` 编辑器编辑文件之前对其创建一个备份。更重要的是，如果无法创建备份，你想避免编辑该文件。这里有一个处理此任务的 Bash 脚本：

```bash
#!/bin/sh
if cp "$1" "$1"
then
    vi "$1"
else
    echo "Failed to create backup copy"
fi
```

此脚本说明了 `if-then-else` 结构的语法，并展示了如何使用 `cp` 命令的退出状态由 `if` 命令决定下一步。如果 `cp` 返回零，脚本使用 `vi` 编辑文件；否则，脚本显示错误信息并退出。顺带提一下，脚本将备份保存在与原始相同的文件中，但在文件名开头添加了一个哈号 (#)。

不要忘记最后结束 `if` 命令的 `fi`。忘记它是 Bash 脚本中常见的错误源。

# 探索 Shell 脚本基础

你可以使用 `test` 命令来评估任何表达式，并使用该命令的退出状态。假设你希望脚本只在文件存在时对其进行编辑。使用 `test`，你可以编写如下的脚本：

```sh
#!/bin/sh
if test -f "$1"
then
    vi "$1"
else
    echo "No such file"
fi
```

`test` 命令的更短形式是将表达式放在方括号 `([..])` 中。使用这种简写符号，你可以这样重写之前的脚本：

```sh
#!/bin/sh
if [ -f "$1" ]
then
    vi "$1"
else
    echo "No such file"
fi
```

注意：你必须在两个方括号之间留空格。

```sh
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
    sum=expr $sum + $i
echo "Sum = $sum"
fi
```

这个示例还说明了如何使用 `expr` 命令来评估表达式。

`case` 语句用于根据变量的值执行一组命令。例如，考虑以下脚本：

```sh
#!/bin/sh
echo -n "What should I do -- (Y)es/(N)o/(C)ontinue? [Y] "
read answer
case $answer in
    y|Y|)
        echo "YES"
        ;;
    c|C)
        echo "CONTINUE"
        ;;
    n|N)
        echo "NO"
        ;;
    *)
        echo "UNKNOWN"
        ;;
esac
```

将此代码保存到名为 `confirm` 的文件中，并输入 `chmod +x confirm` 使其变为可执行文件。然后这样尝试运行：

```
./confirm
```

当脚本提示你时，输入 y、n 或 c 字符之一并按回车。脚本会显示 YES、NO 或 CONTINUE。例如，当我输入 c（然后按回车）时发生了的情况：

What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c

CONTINUE

脚本显示提示符并读取你输入的内容。你的输入存储在名为 `answer` 的变量中。然后 `case` 语句根据 `answer` 变量的值执行一个代码块。例如，当我输入 c 时，执行了以下命令块：

```sh
    c|C)
        echo "CONTINUE"
        ;;
```

`echo` 命令导致脚本显示 CONTINUE。

从这个示例中，你可以看到 `case` 命令的通用语法如下：

```sh
case $variable in
  value1 | value2)
    command1
    command2
    ...other commands...
    ;;
  value3)
    command3
    command4
    ...other commands...
    ;;
esac
```

本质上，`case` 命令以单词 `case` 开始以 `esac` 结束。独立的代码块包含在变量的值之间，后面跟着右括号，并以一对分号（`;`）结束。

## 探索 Bash 的内置命令

Bash 拥有 50 多个内置命令，包括 `cd` 和 `pwd` 等常用命令，以及许多其他不常用的命令。你可以在任何 Bash 脚本或命令行提示符中使用这些内置命令。表 3-1 描述了大多数 Bash 命令及其参数。浏览这些信息后，可以通过 `help` 命令来读取更多关于特定内置命令的信息。例如，要获取更多关于内置命令 `test` 的信息，请输入以下：

```
help test
```

执行后会显示以下信息：

```
test: [expr]
根据 EXPR 的评估结果返回状态 0（真）或 1（假）。表达式可以是一元或二元的。一元表达式通常用于检查文件的状态。提供了字符串操作符和数字比较操作符。
```

文件操作符：

- -a FILE 如果文件存在则为真。
- -b FILE 如果文件是块设备文件则为真。
- -c FILE 如果文件是字符设备文件则为真。
- -d FILE 如果文件是目录则为真。
- -e FILE 如果文件存在则为真。
- -f FILE 如果文件存在且是普通文件则为真。
- -g FILE 如果设置了组 ID 则为真。
- -H FILE 如果文件是符号链接则为真。
- -L FILE 如果文件是符号链接则为真。
- -k FILE 如果文件设置了粘滞位则为真。
- -p FILE 如果文件是命名管道则为真。
- -r FILE 如果你可读则为真。
- -s FILE 如果文件存在且为空则为真。
- -S FILE 如果文件是套接字则为真。
- -t FD 如果文件在终端打开则为真。
- -u FILE 如果设置了 UID 则为真。
- -w FILE 如果你可写则为真。
- -x FILE 如果你可执行则为真。
- -o FILE 如果文件所有权属于你则为真。
- -G FILE 如果文件所有权属于你的组则为真。

(...) 已删除行 ...

在需要时，`help` 命令提供的在线帮助包含了大量的细节。

## 探索 Shell 脚本基础

某些外部程序的名称可能与内置命令同名。如果你想运行外部程序，必须指定完整路径。

表 3-1 Bash 内置命令总结

| 命令 | 功能 |
| :--- | :--- |
| alias | 定义别名。 |
| bg | 将作业后台运行。 |
| bind | 将键序列绑定到宏。 |
| break | 跳出 for 或循环。 |
| cd | 切换目录。 |
| continue | 继续 for 或循环的下次迭代。 |
| declare | 声明变量并可选地赋值。 |
| dirs | 显示当前目录列表。 |
| echo | 在标准输出显示参数。 |
| enable | 启用或禁用内置命令。 |
| eval | 连接参数并作为命令执行。 |
| exec | 用运行命令的进程替换 shell 实例。 |
| exit | 用状态码退出 shell。 |
| export | 定义指定的环境变量并导出到后续进程。 |
| fc | 在替换 pat 后重新执行命令。 |
| fg | 将指定的作业前台运行。如果没有指定作业，则将最近的作业前台运行。 |
| getopts | 获取可选参数（在脚本中用于从命令行提取参数）。 |
| hash | 记住命令的完整路径。 |
| help | 显示内置命令的帮助信息。 |
| history | 显示历史或 n 命令（如果你指定了数字）。 |
| jobs | 列出活动作业。 |
| kill | 向进程发送信号。 |
| local | 创建具有指定名称和值的局部变量（用于 shell 函数）。 |
| logout | 退出 shell。 |
| popd | 从目录栈中移除项。 |
| pushd | 将指定的目录添加到目录栈顶部。 |
| pwd | 打印当前工作目录的完整路径。 |
