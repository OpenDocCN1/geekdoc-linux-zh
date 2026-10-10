
它返回假的 oops，因为 `100 – 50` 不等于 `40`。

## unless 语句

`if` 的反面是 `unless` 语句。它允许你根据条件假而非真来执行一系列操作。它的调用方法与 `if` 语句类似：

```scheme
(unless (= 100 50)
  (display '100 is not equal to 50')(newline)
  (display 'There's not much we can do about it')(newline))
```

这段代码段显示：

100 is not equal to 50

There's not much we can do about it

`unless` 语句除非表达式返回真，否则就会执行其命令。在这种情况下，它是假的。请注意 `unless` 语句不包含 `else` 表达式，

![](img/f36419c0b225d12fa66de83fa271829b_948_0.png)

因此你可以在其中放置多个命令——而 `if` 语句中只有一个命令。

## when 语句

`when` 语句的作用与 `unless` 语句完全相同，但在条件为真时执行其例程。

现在你已经理解了组成 Scheme 的条件语句，下一步是查看文件操作。

## 文件输入与输出

在 Scheme 中，文件被指定为输入文件或输出文件。输出文件允许你写入文件，而输入文件是从中读取。`read` 命令从文件中读取，而 `display` 和 `write` 命令则用于写入文件。在本节中，我们将涵盖从文件读取和向文件写入。

### 从文件读取

要从文件中读取，你需要将其作为输入文件打开并读取一行或一个字符。随后的 `read` 调用将读取下一行或字符，直到读取到文件结束符 (`eof`)。此示例假设一个名为 `test.dat` 的文件包含文本 "This is a test":

- `(define a (open-input-file "test.dat"))`

- `(read-char a)` - 返回字符 `'T'`

- `(define b(read a))`

- `(close a)`

### 创建文件

创建文件与读取类似。首先，打开一个输出文件，然后向其中写入：

```scheme
(define a (open-output-file "test.dat"))
(write "This is a test" a)
(close a)
```

# 使用 Scheme 和 Expect 编程

第 28 章 919

此时，你应该通过输入命令

`expect -v`

来验证一切是否运行顺利。

如果一切顺利，你会在屏幕上看到 Expect 的版本。如果出现问题，你可能需要重新执行步骤，或者阅读 Expect 随附的 INSTALL 文件以寻求可能的解决方案。

## 命令行开关

Expect 带有许多命令行开关。如果你对提高自己的技能感兴趣，建议你阅读 Expect 随附的 man 手页（帮助文档），以了解各个开关的细节。

`-f` 开关告诉 Expect 从文件中读取命令。在编写脚本时，我倾向于使用这种写法，因为这和你从命令行运行脚本时使用的命令相同。

可以使用 `-d` 选项启用诊断输出。如果你在脚本方面遇到困难，我建议使用 `-d` 选项。这是一个交互式调试器，有助于诊断某些区域。

如果你在上一节中安装了 Expect，你会记得可以使用 `-v` 开关获取版本信息。在显示这些信息后，Expect 会立即退出，让你继续操作。

![](img/f36419c0b225d12fa66de83fa271829b_952_0.png)

## send

Expect 允许你自动化交互过程。你可以自动化机器上几乎任何通常需要你亲自操作的程序。例如，如果我想知道网络上另一台机器的服务器负载，我会 Telnet 到那台机器并查看 `/proc/loadavg` 文件的内容。

Expect 具有快速任务的能力。因为它使用 tcl 作为基础，所以当服务器负载高于某个数字时，向你发送电子邮件或让你的控制台发出蜂响非常容易。它也可以记录这些信息。

可以理解，可以在另一台机器上写一个服务器来提供负载平均值，然后在你当前的计算机上通过轮询该服务器，每几分钟查看一次负载。使用 Expect，我只需要八行代码就能获取信息。

首先，让我们在交互模式下运行 Expect。要进入此模式，输入命令

`expect`

你会看到 Expect 提示符旁边有一个闪烁的光标，你可以输入命令了。输入命令

`send "Hello World\n"`

在这里，你只用了 20 个字符就写了一个整个 "Hello World" 程序。

`\n` 代表换行。当屏幕显示时，换行会移动到下一行。使用换行符开发程序是很常见的，但 Expect 让你从另一个角度来看待编程。

Expect 程序的动作就像是你（用户）在输入命令一样。输出换行使用键位 `\n`，但输入该键位时使用 `\r`。关于为什么这样做存在争论，但只需说：向另一个程序发送信息时，使用 `\r`；而向屏幕发送信息时，使用 `\n` 符号——你就没问题。

在这种情况下，它运行正常，因为 "Hello World" 字符串被发送回了屏幕。

每次想运行某些东西时都在 Expect 提示符下输入程序并不好用，所以让我们从创建一个简单的脚本开始。

首先，你需要退出 Expect 提示符。退出的命令是

`exit`

这会将你回到提示符。

接下来，你需要使用你的编辑器（我们推荐 `vi` 或 `emacs`，书中都有关于这两者的章节）并创建一个名为 `hello` 的新文件。然后，向文件中添加以下行：

```
#!/usr/bin/expect -f
```

`send "Hello World\n"`

现在，在继续之前，确保脚本是可执行的，使用命令

```
chmod +x hello
```

并使用命令运行你的“Hello World”程序

```
./hello
```

在大多数情况下，`send` 用于向另一个程序发送信息。在这种情况下，我们使用了它的默认模式，它会将信息发送到你运行命令的终端（STDOUT）。

## expect

为了看到此命令的示例，我们需要编辑你用 `send` 命令创建的 `hello` 文件。它现在应该是：

```
#!/usr/bin/expect -f

send "Hello World\n"
send "What's the best OS in the world?"
expect "linux"
send "Exactly!"
```

当你运行这个程序时，发生的情况是 Expect 正在等待你输入 `linux` 这个单词。在你这样做之前，程序会一直等待。这在负载密集的服务器上执行工作或程序交互时非常有用，因为在不同的流量水平或服务器负载下时间可能会不同。你可以输入任何想要的内容，Expect 都会耐心地等待——大约 10 秒。之后，它觉得你永远不会与它交互了，它就会继续执行。

如果你想更改超时的时间，可以重置 `timeout` 变量。例如，如果你想让程序在仅五秒后超时，只需在文件的第二行添加以下行：

```
set timeout 5
```

在不输入任何内容的情况下运行程序。

如果你不想让程序超时，再次更改 `timeout` 变量，但这次将其设置为 -1：

```
set timeout -1
```

这会导致超时无限等待。

## spawn

`spawn` 是用于启动新进程的命令。它的运行方式就像你从 shell 中运行程序一样。如果我想运行一个 Telnet 会话来登录 `expect.nist.gov`，我需要用以下命令启动会话

```
spawn telnet expect.nist.gov
```

在下一节中，我们将查看 `spawn` 的完整示例。

## interact

`interact` 允许你停止脚本并接管控制。这在你想完成自动化任务后手动进行最后操作时非常有用。

## 脚本——下载

Expect 允许你自动化交互过程。你可以自动化机器上几乎任何通常需要你亲自操作的程序。例如，如果我想知道网络上另一台机器的服务器负载，我会 Telnet 到那台机器并查看 `/proc/loadavg` 文件的内容。

```
expect "ftp>"
send "ls\r"
expect "ftp>"
send "cd /pub/communicator/$version/english/unix/\r"
expect "ftp>"
send "get communicator-v$fv-expect.x86-unknown| linux2.0.tar.gz\r"
interact
```

## 开发环境

## 第四部分

下载完成后，我们退出 FTP 程序，并来到 Expect 程序的最后一行：

```
expect "ftp"
send "exit\r"
```

要使用此程序下载 Communicator 4.7，我将文件保存为 `getnetscape` 并如下如下调用它：

```bash
./getnetscape 4.7
```

几分钟后（或几小时，取决于你的连接速度），Netscape Communicator 4.7 就会出现在同一个目录中。
