

```bash
$ cat read1
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"
$ read1
Go ahead: This is a line.
You entered: This is a line.
```

`read1` 脚本的第一行使用 `echo` 来提示用户输入一行文本。`-n` 选项会抑制随后的换行符（NEWLINE），允许你在提示符所在的同一行输入文本。`read1` 的第二行将文本读入变量 `firstline` 中。第三行通过显示 `firstline` 的值来验证该操作。在这个示例中，变量被加上了引号（连同文本字符串一起），因为你（作为脚本）无法预测用户在响应提示时可能会输入什么字符。考虑一下如果变量没有引号，且用户在响应提示时输入了 `*`，会发生什么：

```bash
$ cat read1_no_quote
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"
$ read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1 read1_no_quote script.1
```

`ls` 命令列出了作为脚本的单词，这表明 shell 将星号 `*` 扩展为了工作目录下所有文件的列表。当变量 `$firstline` 被双引号包围时，shell 不会扩展星号。因此，`read1` 脚本的行为是正确的：

```bash
$ read1
Go ahead: *
You entered: *
```

如果你想让 shell 解释特殊字符的特殊含义，请不要使用引号。

`read2` 脚本提示一个命令行并将其读入变量 `command` 中。然后，脚本通过将 `$command` 单独放在一行来执行该命令行。当你执行该脚本时，shell 会将变量替换为它的值，并将该命令行作为脚本的一部分进行执行：

```bash
$ cat read2
echo -n "Enter a command: "
read command
$command
echo Thanks
```

在接下来的示例中，`read2` 读取了一个调用内置命令 `echo` 的命令行。shell 执行该命令，然后显示 Thanks。接下来，`read2` 读取了一个执行该实用程序的命令行：

# $ read2

Enter a command: echo display this message.
Please display this message.
Thanks

# $ read2

Enter a command: who
alex pts/4      Jun 17 07:50 (:0.0)
scott pts/12   Jun 17 11:54 (bravo.tcorp.com)
Thanks

接下来的 `read3` 脚本将值读入三个变量。`read` 内置命令将一个单词（一个非空字符序列）分配给每个变量：

```bash
$ cat read3
echo -n "Enter something:"
word1 1 is: word2 word3
echo "Word 1: $word1"
echo "Word 2: $word2"
echo "Word 3: $word3"
$ read3
```

Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something

当你进入的单词比 `read` 拥有的变量多时，`read` 会为每个变量分配一个单词。

# $ read3

Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something

当你进入的单词比 `read` 拥有的变量多时，`read` 会为每个变量分配一个单词。

# 命令替换

命令替换允许你将命令的输出作为另一个命令的参数。有两种方法可以：使用反引号 `` ` `` 或使用 `$( )` 语法。反引号语法较旧，而 `$( )` 语法更受青，因为它更容易嵌套。

```bash
$ echo "The today is $(date)"
The today is May 22 10:00:00 UTC 2024
```

括号内命令的输出会在执行前被替换到命令中。这对于获取命令的结果非常有用。

