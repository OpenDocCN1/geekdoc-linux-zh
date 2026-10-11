
### 结论

这就是你可以使用简单的 bash 脚本生成随机密码的方法。

⚠️ 正如前面提到的，请务必使用强密码以确保你的账户受到保护。此外，在可能的情况下，请使用双重身份验证，因为这将为你的账户提供额外的安全保障。

虽然该脚本运行正常，但它假设用户会提供请求的输入。为了防止任何问题，你可能需要对用户输入进行更高级的检查，以确保即使提供的输入不符合我们的需求，脚本也能继续正常工作。

### 贡献者

`Alex Georgiev`

## Bash 中的重定向

Linux 超级用户必须对 Bash 中的管道（pipes）和重定向（redirection）有良好的了解。这是系统的核心组成部分，在 Linux 系统管理领域通常非常有帮助。

当你运行像 `ls`、`cat` 等命令时，你会在终端上看到一些输出。如果你写了错误的命令、传递了错误的标记或错误的命令行参数，你会在终端上得到错误输出。在这两种情况下，你都会得到一些文本。对你来说这似乎仅仅是“文本”，但系统处理这些文本的方式是不同的。这个标识符被称为文件描述符（File Descriptor， `fd`）。

在 Linux 中，有 3 个文件描述符：`STDIN` (`0`)、`STDOUT` (`1`) 和 `STDERR` (`2`)。

- `STDIN` (`fd: 0`): 管理终端的输入。
- `STDOUT` (`fd: 1`): 管理终端的输出文本。
- `STDERR` (`fd: 2`): 管理终端的错误文本。

### 管道与重定向的区别

*管道*和*重定向*都会重定向执行进程的流（文件描述符）。主要的区别在于，*重定向*处理的是*文件流*，将输出流发送到文件，或将给定文件的内容发送到进程的输入流。

另一方面，管道通过将第一个命令的输出流发送到第二个命令的输入流来连接两个命令，而无需指定任何重定向。

## Bash 中的重定向

### STDIN（标准输入）

当你为要求要求输入的命令输入一些输入文本时，你实际上是在向 `STDIN` 文件描述符输入这些文本。运行不带任何命令行参数的 `cat` 命令。看起来进程似乎暂停了，但实际上是 `cat` 在请求 `STDIN`。`cat` 是一个简单的程序，它会打印传递给 `STDIN` 的文本。然而，你可以通过重定向输入到接收 `STDIN` 的命令来扩展其用法。

使用 `cat` 的示例：

```
cat << EOF

Hello World!

How are you?

EOF
```

这将简单地在终端屏幕上打印提供的文本：

```
Hello World!

How are you?
```

其他通过 `STDIN` 接收输入的命令也可以进行相同的操作。例如，`wc`：

```
wc -l << EOF

Hello World!

How are you?

EOF
```

`wc` 的 `-l` 标记统计行数。这段 bash 代码将向终端屏幕上打印行数：

```
2
```

### STDOUT（标准输出）

你终端屏幕上的正常非错误文本是通过 `STDOUT` 文件描述符打印的。命令的 `STDOUT` 可以重定向到文件，使得命令的输出被写入文件而不是打印在终端屏幕上。这简单地通过 `>` 和 `>>` 运算符来实现。

示例：

```
echo "Hello World!" > file.txt
```

接下来的命令不会在终端屏幕上打印 "Hello World"，它会创建一个名为 `file.txt` 的文件并将字符串 "Hello World" 写入其中。可以通过在 `file.txt` 文件上运行 `cat` 命令来验证。

```
cat file.txt
```

然而，当你多次将任何命令的 `STDOUT` 重定向到同一个文件时，它会移除文件的现有内容并写入新内容。

示例：

```
echo "Hello World!" > file.txt

echo "How are you?" > file.txt
```

在 `file.txt` 文件上运行 `cat` 时：

```
cat file.txt
```

你只会得到打印出的 "How are you?" 字符串。

```
How are you?
```

这是因为 "Hello World" 字符串被覆盖了。可以使用 `>>` 运算符避免这种行为。

上面的示例可以写成：

```
echo "Hello World!" > file.txt

echo "How are you?" >> file.txt
```

在 `file.txt` 文件上运行 `cat`，你将得到预期的结果：

```
Hello World!

How are you?
```

或者，`STDOUT` 的重定向运算符也可以写为 `1>`。例如，

```
echo "Hello World!" 1> file.txt
```

### STDERR（标准错误）

终端屏幕上的错误文本是通过命令的 `STDERR` 打印的。
例如：

```
ls --hello
```

会给出错误消息。此错误消息就是命令的 `STDERR`。

可以使用 `2>` 重定向 `STDERR`：

```
ls --hello 2> error.txt
```

然后你可以通过查看 `error.txt` 看到错误：

```
cat error.txt
```

你也可以使用 `2>>` 来追加错误信息：

```
ls --hello 2>> error.txt
```

此外，还可以将 `STDOUT` 和 `STDERR` 同时重定向到同一个文件：

```
ls --hello > output.txt 2> output.txt
```

或者使用 `2>&1` 将 `STDERR` 重定向到 `STDOUT`：

```
ls --hello > output.txt 2>&1
```

### 管道

到为止，我们已经了解了如何通过重定向 `STDOUT`、`STDIN` 和文件。为了将程序（命令）的输出作为另一个程序（命令）的输入，可以使用管道符 `|`。

示例：

```
ls | grep ".txt"
```

语法：

```
command1 | command2
```

你也可以通过将它们组合成任意链来实现强大的结果。这个示例创建了目录下拥有文件的用户列表，以及他们有多少文件和目录：

```bash
ls -l /projects/bash_scripts | tail -n +2 | sed 's/\s*/ /g' | cut -d ' ' -f 3 | sort | uniq -c
```

输出：

- 8 anne
- 34 harry
- 37 tina
- 18 ryan

### Here

可以使用 `<<` 创建临时 heredoc 并在命令行处重定向。

```
COMMAND << EOF

ContentOfDocument

...

...

EOF
```

注意这里的 `EOF` 代表 heredoc 的结束符（文件结束）。实际上，我们可以在此处使用任何字母数字单词来表示文件的开始和结束。例如，这是一个有效的 heredoc：

```
cat << randomword1

This script will print these lines on the terminal.

Note that cat can read from standard input. Using this heredoc, we can

create a temporary file with these lines as it's

content and pipe that

to cat.

randomword1
```

实际上，这看起来就像是 heredoc 的内容被管道传输到了命令。如果需要将多行管道到程序，这可以让脚本变得非常整洁。

此外，我们可以如所示附加更多管道：

```
cat << randomword1 | wc

This script will print these lines on the terminal.

Note that cat can read from standard input. Using this

heroc, we can

create a temporary file with these lines as it's

content and pipe that

into cat.

randomword1
```

此外，可以在 heredoc 中使用预定义的变量。

```
cat << EOF

$VAR

EOF
```

它们都可以重定向到文件：

```
cat << EOF > file.txt
```

还有另一种更短的方法来这样做：

```
./install_package.sh > file.txt 2>&1
```

### HereString

Herestring 与 heredoc 非常相似，但使用的是 `<<<`。这些用于必须管道到某些程序的单行字符串。这看起来比 heredoc 更整洁，因为我们不需要指定分隔符。
