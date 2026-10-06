

# 处理用户输入

```
echo "Checking data for $last, $first..."
$ ./test23
Enter your name: Rich Blum
Checking data for Blum, Rich...
$
```

你也可以在 `read` 命令中不指定变量。如果你这样做，`read` 命令会将接收到的任何数据存放在特殊环境变量 `REPLY` 中：

```bash
$ cat test24
#!/bin/bash
# testing the REPLY environment variable

read -p "Enter a number: " 
factorial=1
for (( count=1; count <= $REPLY; count++ ))
do
    factorial=$[ factorial * $count ]
done
echo "The factorial of $REPLY is $factorial"
$ ./test24
Enter a number: 5
The factorial of 5 is 120
```

`REPLY` 变量将包含输入输入的所有数据，并像其他其他变量一样在 shell 脚本中使用。

# 超时

使用 `read` 命令时存在风险。你的脚本可能会卡在等待用户输入数据的地方。如果脚本无论是否有输入都必须继续运行，你可以使用 `-t` 选项来指定计时器。`-t` 选项指定 `read` 命令等待输入的秒数。当计时过期时，`read` 命令将返回非零退出状态：

```bash
$ cat test25
#!/bin/bash
# timing the data input
```

```bash
if read -t 5 -p "Please enter your name: " name
then
    echo "Hello $name, welcome to my script"
else
    echo "Sorry, too slow!"
fi
$ ./test25
```

# 第二部分：Shell 脚本基础

```
Please enter your name: Rich
Hello Rich, welcome to my script
$ ./test25
Please enter your name:
Sorry, too slow!
$
```

由于 `read` 命令在计时过期后以非零退出状态退出，因此使用标准的结构化语句（如 `if-then` 或 `while` 循环）来跟踪发生了什么。在这个示例中，当计时过期时，`if` 语句执行失败，shell 将执行 `else` 部分的命令。

你不仅可以输入进行计时，还可以设置 `read` 命令来计算输入的字符。当输入了预设数量的字符后，它会自动退出，并将输入的数据赋值给变量：

```bash
cat test26
#!/bin/bash
# getting just one character of input

read -n1 -p "Do you want to continue [Y/N]? " answer
case answer in
Y) echo
	echo "fine, continue on..."
N) echo
	echo "OK, goodbye"
		exit
esac
echo "This is the end of the script"
$ ./test26
Do you want to continue [Y/N]? Y
fine, continue...
This is the end of the script
$ ./test26
Do you want to continue [Y/N]? n
OK, goodbye
$
```

这个示例使用了值为 `1` 的 `-n` 选项，指示 `read` 命令在退出前仅接受单个字符。一旦你按下单个字符进行回答，`read` 命令就会接受输入并将其传递给变量。不需要按 Enter 键。

# 静默读取

有时你需要来自脚本用户的输入，但你不希望这些输入显示在显示器上。最经典的例子是输入密码，但还有许多其他类型的数据你需要隐藏。

`-s` 选项防止 `read` 命令中输入的数据显示在显示器上（实际上，数据被显示了，但 `read` 命令将文本颜色设置为与背景颜色相同）。这里是在脚本中使用 `-s` 选项的示例：

```bash
$ cat test27
#!/bin/bash
# hiding input data from the monitor

read -s p "Enter your password: " pass
echo
echo "Is your password really $pass?"
$ ./test27
Enter your password:
Is your password really Tstling?
$
```

在输入提示符处输入的数据不会显示在显示器上，但会被赋值给变量供脚本使用。

# 从文件读取

最后，你还可以使用 `read` 命令读取存储在 Linux 系统文件中。每次调用 `read` 命令都会从文件中读取一行文本。当文件中没有更多行时，$read$ 命令将以非零退出状态退出。

这部分的困难之处是将数据从文件传递给 `read` 命令。最常用的方法是将文件的 `cat` 命令结果直接管道到包含 `read` 命令的 `while` 命令中。以下是这样做的示例：

```bash
$ cat test28
#!/bin/bash
# reading data from a file

count=1
cat test | while read line
do
	echo "Line $count: $line"
	count=$[$count + 1]
done
	echo "Finished processing the file"
$ cat test
The quick brown dog jumps over the lazy dog.
This is a test, this is only a test.
0 Romeo Romeo, Romeo! wherefore art thou Romeo?
$ ./test28
Line 1: The quick brown dog jumps over the lazy dog.
Line 2: This is a test, this is only a test.
Line 3: Romeo, Romeo! wherefore art thou Romeo?
Finished processing the file
$
```

`while` 命令循环继续使用 `read` 命令处理文件的行，直到 `read` 命令以非零退出状态退出。

# 总结

本章展示了从脚本用户处获取数据的不同方法。命令行参数允许用户在运行脚本时直接在命令行输入数据。脚本使用位置参数来获取命令行参数并将其赋值给变量。

`shift` 命令允许你通过在位置参数中旋转来操作命令行参数。该命令允许你在知道可用参数数量的情况下轻松遍历参数。

在处理命令行参数时，可以使用三个特殊变量。shell 将 `$` 赋值为命令行上输入的参数数量。`$*` 包含所有参数并作为一个单个字符串，而 `$@` 包含所有参数并作为独立的单词。这些变量在尝试处理参数列表时非常有用。

