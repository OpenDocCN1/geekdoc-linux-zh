

## type：显示命令相关信息

`type` 内建命令提供关于命令的信息：

```
$ type cat echo who if lt
cat is hashed (/bin/cat)
echo is a shell builtin
who is /usr/bin/who
if is a shell keyword
lt is aliased to 'ls -ltrh | tail'
```

上述输出显示了如果将 `cat` 或 `who` 作为命令输入时将执行的文件。由于当前 shell 已经调用过 `cat`，它存在于哈希表（第 376 页）中，因此 `type` 报告 `cat` 已被哈希。输出还表明，调用 `echo` 会执行 `echo` 内建命令，`if` 是一个关键字，而 `lt` 是一个别名。

## read：接受用户输入

用户创建变量的一个常见用途是存储在响应提示时用户输入的信息。使用 `read`，脚本可以从用户那里接受输入并将该输入存储到变量中。`read` 内建命令从标准输入读取一行，并将该行上的单词分配给一个或多个变量：

```
$ cat read1
echo -n "Go ahead: "
read firstline
echo "You entered: $firstline"

$ ./read1
Go ahead: This is a line.
You entered: This is a line.
```

`read1` 脚本的第一行使用 `echo` 提示输入一行文本。`-n` 选项抑制了随后的 NEWLINE（换行符），允许你在与提示相同的行上输入一行文本。第二行将文本读取到变量 `firstline` 中。第三行通过显示 `firstline` 的值来验证 `read` 的操作。

`-p`（prompt，提示）选项使 `read` 将其后的参数发送到标准错误。`read` 不会用 NEWLINE 结束此提示。此功能允许你在同一行上既提示用户输入又读取输入：

```
$ cat read1a
read -p "Go ahead: " firstline
echo "You entered: $firstline"

$ ./read1a
Go ahead: My line.
You entered: My line.
```

前例中的变量被加引号（连同文本字符串一起），因为作为脚本编写者，你无法预料用户在响应提示时可能输入哪些字符。考虑一下如果变量没有加引号，而用户在响应提示时输入了 `*` 会发生什么：

```
$ cat read1_no_quote
read -p "Go ahead: " firstline
echo You entered: $firstline

$ ./read1_no_quote
Go ahead: *
You entered: read1 read1_no_quote script.1
$ ls
read1 read1_no_quote script.1
```

`ls` 命令列出了与脚本相同的单词，表明 shell 将星号扩展为工作目录中的文件列表。当变量 `$firstline` 被双引号包围时，shell 不会扩展星号。因此 `read1` 脚本的行为是正确的：

```
$ ./read1
Go ahead: *
You entered: *
```

当你没有指定接收 `read` 输入的变量时，`bash` 将输入放入名为 `REPLY` 的变量中。以下 `read1b` 脚本执行与 `read1` 相同的任务：

```
$ cat read1b
read -p "Go ahead: "
echo "You entered: $REPLY"
```

`read2` 脚本提示输入命令行，读取用户的响应，并将其分配给变量 `cmd`。然后，脚本尝试执行由 `cmd` 变量扩展结果产生的命令行：

```
$ cat read2
read -p "Enter a command: " cmd
$cmd
echo "Thanks"
```

在下面的示例中，`read2` 读取一个调用 `echo` 内建命令的命令行。shell 执行该命令，然后显示 **Thanks**。接下来，`read2` 读取一个执行 `who` 实用工具的命令行：

```
$ ./read2
Enter a command: echo Please display this message.
Please display this message.
Thanks
$ ./read2
Enter a command: who
max    pts/4    2013-06-17 07:50 (:0.0)
sam    pts/12   2013-06-17 11:54 (guava)
Thanks
```

如果 `cmd` 没有扩展为有效的命令行，shell 会发出错误消息：

```
$ ./read2
Enter a command: xxx
./read2: line 2: xxx: command not found
Thanks
```

**read3** 脚本将值读取到三个变量中。**read** 内建命令为每个变量分配一个单词（非空白字符序列）：

```
$ cat read3
read -p "Enter something: " word1 word2 word3
echo "Word 1 is: $word1"
echo "Word 2 is: $word2"
echo "Word 3 is: $word3"
$ ./read3
Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

当你输入的单词数量多于 **read** 拥有的变量数时，**read** 为每个变量分配一个单词，并将所有剩余的单词分配给最后一个变量。**read1** 和 **read2** 都将第一个单词和所有剩余单词分配给脚本各自拥有的那一个变量。在以下示例中，**read** 将五个单词分配给三个变量：它将第一个单词分配给第一个变量，第二个单词分配给第二个变量，第三到第五个单词分配给第三个变量。

```
$ ./read3
Enter something: this is something else, really.
Word 1 is: this
Word 2 is: is
Word 3 is: something else, really.
```

表 27-4 列出了 **read** 内建命令支持的一些选项。

### 表 27-4 read 选项

| 选项 | 功能 |
| :--- | :--- |
| **-a _aname_** | （数组）将输入的每个单词分配给数组 _aname_ 的一个元素。 |
| **-d _delim_** | （分隔符）使用 _delim_ 终止输入，而不是 **NEWLINE**。 |
| **-e** | （Readline）如果输入来自键盘，则使用 Readline 库（第 386 页）获取输入。 |
| **-n _num_** | （字符数）读取 _num_ 个字符并返回。一旦用户输入 _num_ 个字符，**read** 就返回；无需按 **RETURN**。 |
| **-p _prompt_** | （提示）在读取输入之前，在标准错误上显示不带终止 **NEWLINE** 的 _prompt_。仅当输入来自键盘时显示 _prompt_。 |
| **-s** | （静默）不回显字符。 |
| **-u _n_** | （文件描述符）使用整数 _n_ 作为 **read** 从中获取输入的文件描述符。因此 `read -u4 arg1 arg2` 等同于 `read arg1 arg2 <&4`。有关重定向和文件描述符的讨论，参见“File Descriptors”（第 1016 页）。 |

如果 `read` 内建命令成功读取任何数据，它返回退出状态 0。当它到达 EOF（文件末尾）时，它具有非零退出状态。

以下示例从命令行运行 `while` 循环。它从 `names` 文件获取输入，并在读取 `names` 中的最后一行后终止。

```
$ cat names
Alice Jones
Robert Smith
Alice Paulson
John Q. Public
$ while read first rest
> do
> echo $rest, $first
> done < names
Jones, Alice
Smith, Robert
Paulson, Alice
Q. Public, John
$
```

重定向符号（`<`）在 `while` 结构中的位置至关重要。重要的是将重定向符号放在 `done` 语句处，而不是 `read` 调用处。

**optional** 每次重定向输入时，shell 都会打开输入文件并将读取指针重新定位到文件的开头：

```
$ read line1 < names; echo $line1; read line2 < names; echo $line2
Alice Jones
Alice Jones
```

在这里，每个 `read` 都打开 `names` 并从 `names` 文件的开头开始。在以下示例中，`names` 只打开一次，作为由括号创建的子 shell 的标准输入。然后，每个 `read` 读取标准输入的连续行：

```
$ (read line1; echo $line1; read line2; echo $line2) < names
Alice Jones
Robert Smith
```

获取相同效果的另一种方法是使用 `exec` 打开输入文件并保持其打开状态（参见第 1016 页的“File Descriptors”）：

```
$ exec 3< names
$ read -u3 line1; echo $line1; read -u3 line2; echo $line2
Alice Jones
Robert Smith
$ exec 3<&-
```

**whiptail** 在图形环境中运行时，`whiptail` 可以从 shell 脚本中显示对话框。以下命令在对话框中显示 **What is your name?**。当用户输入答案并按 RETURN 时，`whiptail` 将响应发送到标准错误，命令行将其重定向到文件 `named`。有关更多信息，请参见 `whiptail` 手册页。

```
$ whiptail --inputbox "What is your name?" 10 30 2> answer
$ cat answer
Sam the Great$
```

