
`test` 命令的更短形式是将表达式放在方括号（`[...]`）中。使用这种简写形式，你可以这样重写前面的脚本：

```bash
#!/bin/sh
if [ -f "$1" ]
then
  vi "$1"
else
  echo "No such file"
fi
```

注意：必须在两个方括号之间留空格。

另一个常见的控制结构是 `for` 循环。以下脚本会将数字 1 到 10 相加：

```bash
#!/bin/sh
sum=0
for i in 1 2 3 4 5 6 7 8 9 10
do
  sum=expr $sum + $i
done
```

这个示例还说明了如何使用 `expr` 命令评估表达式。

`case` 语句用于根据变量的值执行一组命令。例如，考虑以下脚本，它基于你的 Red Hat Linux 系统中 `/etc/init.d/functions` 文件中的 `confirm()` 函数：

```bash
#!/bin/sh
echo -n "What should I do -- (Y)es/(n)o/(C)ontinue? [Y]"
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

将此内容保存为名为 `confirm` 的文件，并输入 `chmod +x confirm` 变为可执行。然后这样尝试运行：

```bash
./confirm
```

当脚本提示你时，输入 y、n 或 c 字符之一，然后按回车。脚本应该显示 YES、NO 或 CONTINUE。例如，当你输入 c（然后按回车）时，会发生以下情况：

```bash
What should I do -- (Y)es/(N)o/(C)ontinue? [Y] c
CONTINUE
```

脚本显示提示符并读取你输入的输入。你的输入被存储在一个名为 `answer` 的变量中。然后 `case` 语句根据 `answer` 变量的值执行一个代码块。例如，当我输入 `c` 时，会执行以下命令块：

```bash
c|C)
echo "CONTINUE"
;;
```

`echo` 命令导致脚本显示 CONTINUE。

通过这个示例，你可以看到 `case` 命令的通用语法如下：

```bash
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

本质上，`case` 命令以单词 `case` 开头，以 `esac` 结尾。不同的代码块位于变量的值之间，后面跟着右括号，并用一对分号（`;`）结束。

## 探索 Bash 的内置命令

Bash 拥有超过 50 多个内置命令，包括 `cd` 和 `pwd` 等常用命令，以及其他频繁使用的命令。如果你想运行任何外部程序，必须指定该程序的完整路径。否则，Bash 将执行同名的内置命令。要了解更多关于内置命令的信息，请输入 `help`：

```bash
test [expr]
```

其中 `expr` 是一元或二元表达式。`test` 根据表达式返回零（真）或 1（假）。

以下是 `test` 运算符：

-a: 如果表达式真

- -b: 如果是二进制文件

- -c: 如果是字符文件

- -d: 如果是目录

- -e: 如果文件存在

- -f: 如果是普通文件

- -g: 如果是组

- -h: 如果是符号链接

- -l: 如果是命名管道

- -p: 如果是套接

- -r: 如果可读

- -s: 如果文件为空

- -t: 如果是终端

- -u: 如果是用户

- -w: 如果可写

- -x: 如果可执行文件

## 775 学习 Shell 脚本基础

表 3-1 Bash 内置命令摘要 | 该功能的作用 |

| :--- | :--- |

| . filename [arguments] | 从文件读取并执行命令（带有可选参数，与 source 命令相同）。 |

| : [arguments] | 展开参数但不处理它们。 |

| exp expr | 评估表达式，如果真则返回零。 |

| alias [name=value ...] | 定义别名。 |

| bg [job] | 将指定的作业放入后台。如果没有指定作业，则将正在执行的命令放入后台。 |

| bind [-m keymap] [-l q] | 将键序列绑定到宏。 |

| break [n] | 退出 for、while 或 until 循环。如果指定了 n，则退出第 n 层循环。 |

| builtin builtin_command [arguments] | 执行内置命令。 |

| cd [dir] | 将当前目录更改为 dir。 |

| command [-pVv] cmd [arg ...] | 使用指定的参数运行 cmd（忽略同名的 shell 函数）。 |

| continue [n] | 开始 for、while 或 until 循环的下一次迭代。如果指定了 n，则启动第 n 层循环的下次迭代。 |

| declare [-frxi] [name=value] | 声明指定名称变量并可选赋值。 |

| dirs [-l] [+/-n] | 显示当前记忆的目录列表。 |

| echo [-neE] [arg ...] | 在标准输出显示参数。 |

| enable [-n] [-all] [name ...] | 启用或禁用内置命令。 |

| eval [arg ...] | 合并参数并作为命令执行。 |

| exec [command [arguments]] | 用运行指定命令的新进程替换当前的 shell 实例。 |

| exit [n] | 以状态 n 退出 shell。 |

| export [-nf] [name=word ...] | 定义指定的环境变量并将其导出到未来的进程。 |

# 学习 Shell 脚本基础 779

| 此函数 | 功能 | 第九章 |

|---|---|---|

| fc -s [pat-rep] [cmd] | 在将模式替换为替换字符串后重新执行命令。 | | |

| fg [jobspec] | 将指定的作业置于前台。如果没有指定作业，则将最近的作业置于前台。 | | |

| getopts optstring name [args] | 获取可选参数（在 shell 脚本中调用，用于从命令行提取参数）。 | 编写 |

| hash -r [name] | 记住指定命令的完整路径。 | Shell |

| help [cmd ... ] | 显示指定的内置命令的帮助信息。 | | |

| history n | 显示过去的命令，或者如果你指定了数字 n，则显示 n 条命令。 | | |

| jobs [-lnp] [jobspec ... kill [-sig] -sigspec] [pid | jobspec] -let arg ... ] | 列出当前激活的作业。评估每个参数，如果最后一个参数为 0，则返回 1。 | | |

| local [name=value] ...] | 在（shell 中）创建一个具有指定名称和值的局部变量。 | | | |

| logout | 退出登录 shell。 | | | |

| popd [+/-] | 从目录栈中移除项。 | | | |

| pushd [dir] | 将指定的目录添加到目录栈顶端。 | | | |

| pwd | 打印当前工作目录的完整路径。 | | | |

| read [-r] [name ... ] | 从标准输入读取一行并进行解析。 | | | |

| readonly [-f] [name ... ] | 将指定的变量标记为只读，以便变量无法更改。 | | | |

| return [n] | 以返回值 n 退出 shell。 | | | |

| set [-abefhkmntuvxldChP] [-o option ...] | 设置变量。 | | | |

| shift [n] | 使第 n+1 个参数变为 $1，第 n+2 个参数变为 $2，依此类推。 | | | |

| source filename [arguments] | 从文件中读取并执行命令。 | | | |

| suspend [-f] | 停止直到接收到 SIGINT 信号。 | | | | |

| test expr | 评估表达式 expr，如果 expr 为真，则返回零。 | | | | |

| times | 打印从 shell 运行的进程的累计用户时间和系统时间。 | | | | |

| 表 3-1（续） |
