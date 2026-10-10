
数据以创建任何类型的输出报告。

## 从命令行读取程序脚本

一个 awk 程序脚本由开括号和闭括号定义。您必须将脚本命令放在两个括号（{}）之间。如果您错误地使用括号代替花括号来包裹您的 awk 脚本，将会产生类似以下所示的错误消息：

```
$ awk '(print "Hello World!")'
awk: cmd. line:1: (print "Hello World!")
awk: cmd. line:1: ^ syntax error
awk: cmd. line:2: (print "Hello World!")
awk: cmd. line:2: ^ unexpected newline
or
end of string
$
```

由于 awk 命令行假定脚本是一个单一的文本字符串，因此您还必须用单引号将脚本包裹起来。以下是一个在命令行上指定的简单 awk 程序脚本的示例：

```
$ awk '{print "Hello World!"}'
```

该程序脚本定义了一个单一命令，即 `print` 命令。`print` 命令的作用如其所言：它将文本打印到 STDOUT。如果您尝试运行此命令，您会略显失望，因为当下不会发生任何事情。由于命令行中未定义文件名，awk 程序将从 STDIN 获取数据。当您运行程序时，它只是等待通过 STDIN 输入文本。

如果您输入一行文本并按下 Enter 键，awk 就会将该文本通过程序脚本进行处理。就像 `sed` 编辑器一样，awk 程序会针对数据流中可用的每一行文本执行该程序脚本。由于程序脚本被设置为显示一个固定的文本字符串，无论您在数据流中输入什么文本，您得到的文本输出都是相同的：

```
$ awk '{print "Hello World!"}'
This is a test
Hello World!
hello
Hello World!
Goodbye
Hello World!
This is another test
Hello World!
```

为了终止 gawk 程序，您必须发出信号表明数据流已结束。Bash shell 提供了一个键位组合来生成文件结束（EOF）字符。在 Bash 中，`Ctrl+D` 键位组合会生成一个 EOF 字符。使用该键位组合将终止 gawk 程序，并返回到命令行界面提示符。

## 使用数据字段变量

gawk 的主要功能之一是它能够操纵文本文件中的数据。它通过自动为每行中的每个数据元素分配变量来实现这一点。默认情况下，gawk 为它在文本行中检测到的每个数据字段分配以下变量：

- `$0` 代表整行文本。
- `$1` 代表文本行中的第一个数据字段。
- `$2` 代表文本行中的第二个数据字段。
- `$n` 代表文本行中的第 n 个数据字段。

文本行中的每个数据字段由字段分隔符确定。当 gawk 读取一行文本时，它会使用定义的字段分隔符来区分每个数据字段。gawk 中的默认字段分隔符是任何空白字符（例如制表符或空格字符）。

以下是一个示例 gawk 程序，它读取一个文本文件并仅显示第一个数据字段的值：

```
$ cat data2.txt
One line of test text.
Two lines of test text.
Three lines of test text.
$
$ gawk '{print $1}' data2.txt
One
Two
Three
```

此程序使用 `$1` 字段变量来显示每行文本的仅第一个数据字段。

对于读取使用不同字段分隔符的文件，请使用 `-F` 选项指定该字符：

```
$ gawk -F: '{print $1}' /etc/passwd
root
daemon
bin
[…]
christine
sshd
$
```

这个简短的程序显示了系统中密码文件的第一个数据字段。由于 `/etc/passwd` 文件使用冒号 (:) 来分隔数据字段，为了分隔每个数据元素，我们在 gawk 选项中使用了字段分隔符（`-F:`）。

## 在程序脚本中使用多个命令

如果您只能执行一条命令，那么编程语言就没太大用处了。gawk 编程语言允许将命令组合成一个正常的程序。要在命令行指定的程序脚本中使用多个命令，只需在每个命令之间放置一个分号：

```
$ echo "My name is Rich" | gawk '{$4="Christine"; print $0}'
My name is Christine
$
```

第一个命令将值分配给 $4 字段变量。第二个命令然后打印整个数据字段。从输出中可以看到，gawk 程序将原始文本中的第四个数据字段替换为新值。

您也可以使用次要提示符逐行输入您的程序脚本命令：

```
$ gawk '{
> $4="Christine";
> print $0}'
My name is Rich
My name is Christine
$
```

当我们用单引号打开后，Bash shell 提供了次要提示符，提示我们输入更多数据。我们在每一行上逐条添加命令，直到输入闭合的单引号为止。由于命令行中未定义文件名，`gawk` 程序从 `STDIN` 获取数据。当我们运行程序时，它等待通过 STDIN 输入文本。为了退出程序，我们按下了 `Ctrl+D` 键位组合以表明数据结束并回到 shell 提示符。

## 从文件中读取程序

与 `sed` 编辑器一样，`gawk` 编辑器允许您将程序存储在文件中，并在命令行中引用它们：

```
$ cat script2.gawk
{print $1 "'s home directory is " $6}
$
$ gawk -F: -f script2.gawk /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
bin's home directory is /bin
[...]
christine's home directory is /home/christine
sshd's home directory is /run/sshd
$
```

`script2.gawk` 程序脚本再次使用 `print` 命令来打印 `/etc/passwd` 文件的主目录数据字段（字段变量 `$6`）和用户名数据字段（字段变量 `$1`）。

您可以在程序文件中指定多个命令。为此，只需将每个命令放在单独的一行上即可。您不需要使用分号：

```
$ cat script3.gawk
{
 text = "'s home directory is "
 print $1 text $6
}
$
```

```
$ gawk -F: -f script3.gawk /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
bin's home directory is /bin
[...]
christine's home directory is /home/christine
sshd's home directory is /run/sshd
$
```

`script3.gawk` 程序脚本定义了一个变量 `text`，用于存储 `print` 命令中使用的文本字符串。请注意，`gawk` 程序在引用变量值时不使用美元符号，这与 shell 脚本不同。

## 在处理数据之前运行脚本

`gawk` 程序还允许您指定程序脚本的运行时间。默认情况下，`gawk` 从输入中读取一行文本，然后在该行文本的数据上执行程序脚本。有时，您可能需要在处理数据之前运行脚本，例如创建报告的文件头部分。`BEGIN` 关键字用于实现此目的。它强制 `gawk` 在读取数据之前执行 `BEGIN` 关键字后指定的程序脚本：

```
$ gawk 'BEGIN {print "Hello World!"}'
Hello World!
$
```

这次，`print` 命令在读取任何数据之前显示了文本。然而，显示文本后，它很快就退出，而不等待任何数据。

原因是 `BEGIN` 关键字仅在处理任何数据之前应用指定的脚本。如果您希望使用普通程序脚本处理数据，必须使用另一个脚本部分定义程序：

```
$ cat data3.txt
Line 1
Line 2
Line 3
$
$ gawk 'BEGIN {print "The data3 File Contents:"}
> {print $0}' data3.txt
The data3 File Contents:
Line 1
Line 2
Line 3
$
```

现在，在 gawk 执行完 BEGIN 脚本后，它使用第二个脚本来处理任何文件数据。这样做时请小心 —— gawk 命令行上的这两个脚本仍然被视为一个文本字符串。您需要相应地放置单引号。

## 在处理数据之后运行脚本

与 `BEGIN` 关键字类似，`END` 关键字允许您指定 gawk 在读取数据之后执行的程序脚本：

```
$ gawk 'BEGIN {print "The data3 File Contents:"}
> {print $0}
> END {print "End of File"}' data3.txt
The data3 File Contents:
Line 1
Line 2
Line 3
End of File
$
```

当 gawk 程序打印完文件内容后，它会执行 `END` 脚本中的命令。这是一种很好的技术，用于在所有常规数据处理完成后为报告添加页脚数据。

您可以将所有这些元素组合到一个小的程序脚本文件中，以从简单的数据文件创建完整的报告：

```
$ cat script4.gawk
BEGIN {
print "The latest list of users and shells"
print "UserID \t Shell"
print "------- \t -------"
FS=";"
}

{
print $1 "          \t "  $7
}
```

