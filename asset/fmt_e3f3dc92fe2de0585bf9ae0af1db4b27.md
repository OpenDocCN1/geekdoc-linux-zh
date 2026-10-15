
# Authorization Required

此服务器无法验证您有权访问请求的文档。您提供的凭据错误（例如，密码错误），或者您的浏览器不理解如何提供凭据。

```
Apache/2.2.20 (Ubuntu) Server at admin.megacorp.com Port 81
```

```
08:51:25.444 172.16.40.101 /208.68.24.99.333: E.s@m.@U....HTTP/1.1 301 Moved Permanently
Date: Mon, 22 Apr 2013 12:51:25 GMT
PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 103
基于 Kali Linux 的渗透测试 2.0
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_130_0.png)

```
Server: Apache/2.2.20 (Ubuntu)
Location: http://admin.megacorp.com:81/admin
Vary: Accept-Encoding
Content-Length: 333
Content-Type: text/html; charset=iso-8859-1
```

```
<!DOCTYPE HTML PUBLIC "//RFC//DTD HTML//EN">
<head>
<title>301 Moved Permanently</title>
</head>
<body>
<h1>Moved Permanently</h1>
<p>文档已移动到 <a href="http://admin.megacorp.com:81/admin">这里</a>。</p>
<br>
<address>Apache/2.2.20 (Ubuntu) Server at admin.megacorp.com Port 81</address>
</body>
```

## 列表 133 - 使用高级过滤器 tcpdump

从这里开始，我们的故事变得清晰了。我们看到大量尝试验证 `/admin` 目录导致了 HTTP 401 回复，而最后一次尝试似乎成功，因为服务器回复了 301。似乎有人访问了 megacorp 的一个服务器！

## 4.5.3 练习

1. 使用 `tcpdump` 重现对端口 80 捕捉流量。
2. 使用 `-X` 标志查看数据包内容。如果被截断，调查 `-s` 长度是否有帮助。
3. 在 `password_cracking_filtered.pcap` 文件查找所有 'SYN'、'ACK' 和 'RST' 数据包。
4. 另一种语法是使用 `tcpdump`，可以使用用户友好的过滤器仅显示 ACK 和 PSH 数据包。在 `tcpdump` 手册中搜索 "tcpflags"。使用该语法编写相应的显示过滤器来过滤 ACK 和 PSH 数据包。

## 4.6 总结

在本模块中，我们演示了每个渗透测试工具箱中常用的实用工具，包括 `Netcat`、`Socat`、`PowerShell`、`Wireshark` 和 `Tcpdump`。这些工具在渗透测试期间非常有帮助，特别是当我们缺少专用工具或需要传输小工具来扩大我们在目标网络上的 foothold 时。

# 5. Bash 脚本

GNU Bourne-Again Shell (`Bash`) 是一个强大的工作环境和脚本引擎。专业的安全人员利用 Bash 脚本来简化和自动化许多 Linux 任务和程序。在本模块中我们将介绍 Bash 脚本并探索几种实际场景。

## 5.1 Bash 脚本简介

Bash 脚本是一个纯文本文件，包含一系列命令，这些命令执行就像在终端提示符处输入的一样。通常情况下，Bash 脚本具有可选的扩展名 `.sh`（便于识别），以 `#!/bin/bash` 开头，并在执行之前必须具有执行权限。让我们从简单的 'Hello World' Bash 脚本开始：

### 列表 134 - 创建简单的 'Hello World' Bash 脚本

此脚本包含几个组件：

- 第 1 行：`#!/bin/bash` 通常称为 shebang（解释器路径），用于告诉解释器应该使用哪一个。这是 Bash 解释器的路径。
- 第 2 行：`# echo` 添加注释，因此之后的所有文本都会被忽略。
- 第 3 行：`# echo "Hello World!"` 使用 `echo` 命令向终端打印字符串，在这种情况下是 "Hello World!"。

接下来，让脚本变为可执行，并使用 `./hello-world.sh` 实际运行它。该符号可能确认这仅仅是一个路径表示，表示该脚本位于当前目录。每当我们使用命令时，`Bash` 都会尝试在存储在变量 `PATH` 中的目录中查找它。由于我们的家目录...

### 列表 135 - 运行简单的 'Hello World' Bash 脚本

> (GNU, 2017), http://www.gnu.org/software/bash/
> (Wikipedia, 2019), https://en.wikipedia.org/wiki/Bash_(Unix)
> (The Linux Information Project, 2005), http://www.linux.org/absolute_pathname.html
> (O'Reilly Media, 1998), https://www.oreilly.com/

## 5.2 变量

变量是用于临时存储数据的命名位置。我们可以设置（或“声明”）变量，为其分配一个值，或者读取变量，它将“展开”或“解析”为其值。

我们可以通过许多方式声明变量值。最简单的方法是使用简单的 `name=value` 声明直接设置。注意 `=` 前后没有空格：

### 列表 136 - 声明简单的变量

```bash
kali@~$ first_name=Good
```

如果不引用它，声明变量是没有意义的。为了这样做，我们在变量名之前加上 `$` 字符。每当 `Bash` 在命令中遇到这种语法时，它会在执行之前将变量名替换为其值（展开变量）。

变量名可以是大写、小写或两者的混合。然而，`Bash` 是区分大小写敏感的，因此在声明和展开变量时必须保持一致。此外，使用描述性变量名是一个良好的做法，这使得我们的脚本更容易易读和维护。

请注意 `Bash` 以特定方式解释某些字符。例如，此声明演示了不当的多值变量赋值：

### 列表 138 - 尝试给变量赋值复杂值

一个简单的示例将有助于这一点：

```bash
kali@kali:~ $ first_name=Good
kali@kali:~ $ last_name=Hacker
```

```bash
kali@kali:~ $ echo $first_name $last_name
Good Hacker
```

```bash
kali@kali:~ $ greeting=Hello World
bash: World: command not found
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_133_0.png)

（通常会打印到屏幕上）并将其保存为变量的值，这允许我们获取命令或程序的输出（即什么）

### 列表 140 - 演示命令替换和变量的使用

在列表 140 中，我们将 `whoami` 命令的输出赋值给 `user` 变量。然后我们显示了它的值。使用反引号（`` ` ``）进行命令替换的另一种语法如下所示：

### 列表 141 - 命令替换的另一种语法

反引号方法较旧，通常不建议使用，因为两种命令替换方法的行为存在差异。

> 《Kali Linux 渗透测试 2.0》

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_134_0.png)

```bash
kali@kali:~ $ echo $greeting
Hello World
kali@kali:~ $ greeting2="New $greeting"
kali@kali:~ $ echo $greeting2
Hello World
```

### 列表 139 - 使用单引号和双引号包裹 `greeting` 来使用字符串进行复杂的变量赋值

在这个示例中，单引号包裹的 `greeting` 声明完整地保留了文本的值，并且没有将空格解释为命令分隔符。然而，在双引号包裹的 `greeting2` 声明中，`Bash` 将 `$greeting` 扩展为它的值（"Hello World"），尊重了 `$` 字符的特殊含义。

我们还可以将变量的值设置为命令或程序的结果。这被称为**命令替换**。

命令替换发生在子 shell 中，子 shell 中变量的更改不会改变主进程中的变量。以下示例演示了这一点：

```bash
kali@kali:~ $ user=$(whoami)
kali@kali:~ $ echo $user
kali
kali@kali:~ $ user2=`whoami`
kali@kali:~ $ echo $user2
kali
```

需要注意的是，命令

### 列表 142 - 子 shell 中的命令替换

```bash
kali@kali:~ $ cat ./subshell.sh
#!/bin/bash -x

var1=value
echo $var1
var2=value
echo $var2
```

> 115 (GNU, 2019), https://www.gnu.org/software/bash/manual/html_node/Command-Substitution.html
> 116 (BashFAQ, 2016), http://mywiki.wooledge.org/BashFAQ/08

`Bash` 脚本也无异；我们可以提供命令行参数并在脚本中使用它们：

> 117 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Parameter_(computer_programming)

并不是所有脚本都需要参数。它们由 `Bash` 解释，取决于如何使用它们。我们已经执行过带有参数的 Linux 命令。例如，当我们运行命令 `ls -l /var/log` 时，`-l` 和 `/var/log` 都是 `ls` 命令的参数。

> 《Kali Linux 渗透测试 2.0》

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_135_0.png)

在示例中，首先注意我们更改了 shebang，添加了 `-x` 标志。这指示 `Bash` 打印额外的调试输出，以便我们能够轻松地看到执行的命令及其结果。当我们查看此输出时，注意以单加 `+` 前缀的命令是在当前 shell 中执行的，而以双加 `++` 前缀的命令是在子 shell 中执行的。

这让我们清楚地看到 `var1` 和 `var2` 的第二次声明发生在子 shell 中，并没有像初始声明那样更改当前 shell 中的值。

## 5.2.1 参数

然而，理解如何操作至关重要

```bash
kali@kali:~ $ cat ./arg.sh
#!/bin/bash

echo The first two arguments are $1 and $2
kali@kali:~ $ chmod +x ./arg.sh
kali@kali:~ $ ./arg.sh hello here
The first two arguments are hello and here
```

在列表 143 中，我们创建了一个简单的 Bash 脚本，对其设置了可执行权限，然后用两个参数运行了它。`$1` 和 `$2` 变量代表传递给脚本第一个和第二个参数。让我们探索一些特殊的 Bash 变量：

### 表 4 - 特殊 Bash 变量

| 变量名 | 说明 |
| --- | --- |
| `$0` | 脚本名称 |
| `$1` | 传递给脚本的第一个参数 |
| `$2` | 传递给脚本的第二个参数 |
| `$#` | 传递给脚本的参数数量 |
| `$@` | 传递的所有参数 |
| `$$` | 当前 shell 的进程 ID |
| `$USER` | 当前用户名 |
| `$HOSTNAME` | 主机名 |
| `$RANDOM` | 随机数（0-32767 之间） |
| `$SHELL` | 运行脚本的 shell |
| `$LINENO` | 脚本中的行号 |

这些特殊变量在调试脚本时可能非常有用。例如，我们可能获取命令的退出状态，以判断它是否成功执行。

## 5.2.2 读取输入

命令行参数是用户输入的一种，但我们也可以在脚本运行时通过 `read` 命令捕捉用户输入。在这个示例中，我们将使用 `read` 来捕捉用户输入并将其赋值给变量。

### 列表 144 - 提示用户输入并静默读取

```bash
read -p "Username: " username
read -s -p "Password: " password
```

`read` 命令可以通过各种选项更改行为：`-p` 允许提示，`-s` 静默读取（不显示输入）。

### 列表 145 - 提示用户输入并静默读取

```bash
read -p "Username: " username
echo -s = password
```

## 5.3 If, Else, Elif 语句

**条件语句允许我们根据不同的条件执行不同的操作。** 最常用的 Bash 语句包括 `if`、`else` 和 `elif`。

`if` 语句相对简单——检查条件是否为真，但它需要特定的语法。注意这种语法，特别是空格的使用：

### 列表 146 - if 语句的通用语法

```bash
if [ <test> ]; then
    <perform an action>
fi
```

在列表中，如果 “test” 结果为真，脚本将“执行操作”，即 `then` 和 `fi` 之间的任何命令。让我们看一个真实的示例：

### 列表 147 - 在 Bash 中使用 if 语句

```bash
kali:~$ cat ./if.sh
#!/bin/bash
# if statement example

read -p "What is your age: " age

if [ $age -lt 16 ]; then
    echo "You might need parental permission to take this course!"
fi

kali:~$ chmod +x ./if.sh
kali:~$ ./if.sh
What is your age: 15
You might need parental permission to take this course!
```

在这个示例中，我们使用 `if` 语句来检查用户输入的年龄。如果输入的年龄小于 (`-lt`) 16，脚本将输出警告信息。

### 表 5 - 常用测试命令运算符

| 运算符 | 描述：表达式为真，如果... |
| --- | --- |
| `! EXPRESSION` | EXPRESSION 为假 |
| `-n STRING` | STRING 长度大于 0 |
| `-z STRING` | STRING 长度为 0（空） |
| `STRING1 != STRING2` | STRING1 不等于 STRING2 |
| `STRING1 = STRING2` | STRING1 等于 STRING2 |
| `INTEGER1 -eq INTEGER2` | INTEGER1 等于 INTEGER2 |
| `INTEGER1 -ne INTEGER2` | INTEGER1 不等于 INTEGER2 |
| `INTEGER1 -gt INTEGER2` | INTEGER1 大于 INTEGER2 |
| `INTEGER1 -lt INTEGER2` | INTEGER1 小于 INTEGER2 |
| `INTEGER1 -ge INTEGER2` | INTEGER1 大于等于 INTEGER2 |
| `INTEGER1 -le INTEGER2` | INTEGER1 小于等于 INTEGER2 |
| `-d FILE` | FILE 存在且是一个目录 |
| `-e FILE` | FILE 存在 |
| `-r FILE` | FILE 存在且具有读取权限 |
| `-s FILE` | FILE 存在且不为空 |
| `-w FILE` | FILE 存在且具有写入权限 |
| `-x FILE` | FILE 存在且具有执行权限 |

根据上述思路，我们之前的 `if` 示例可以在不使用方括号的情况下重写如下：

### 列表 148 - 在 if 语句中使用 test 命令

```bash
kali@kali:~$ cat ./if2.sh
#!/bin/bash
# if statement 2

read -p "What is your age: " age

if test $age -lt 16; then
    echo "You might need parental permission to take this course!"
fi

kali@kali:~$ chmod +x ./if2.sh
kali@kali:~$ ./if2.sh
What is your age: 15
You might need parental permission to take this course!
```
