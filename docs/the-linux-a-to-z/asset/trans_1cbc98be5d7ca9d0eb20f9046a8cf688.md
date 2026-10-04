
本质上只是一个在登录时执行的 shell 脚本。如果您有一个个人登录脚本，它必须存储在您的主目录中。当您登录时，bash 会在您的主目录中查找其中一个特定的文件名。这些是：
- `~/.bash_profile`
- `~/.bash_login`
- `~/.profile`

bash 按此顺序查找这三个文件名，并仅执行找到的第一个。

当您注销时，bash 也可以执行个人注销脚本。同样，它必须存储在您的主目录中，名称为：

```
~/.bash_logout
```

除了 bash 可以执行的个人脚本外，系统管理员还可以创建一个名为的全局登录脚本：

```
/etc/profile
```

bash 会在每个用户登录时执行它。这允许系统管理员为整个系统设置本地配置。如果存在，全局登录脚本将在您的个人脚本之前执行，以便您的个人脚本可以进一步自定义您的环境。例如，常出现在此全局文件中的内容是设置 shell 忽略文件结束符（Ctrl-d）以便注销的那一行。如果文件中包含带有单词 ignoreeof 的行，则删除该行将允许您使用 Ctrl-d 注销。

下一个示例展示了设置个人登录脚本以自定义 shell 提示符并将您自己的 bin 目录添加到 PATH 列表中是多么容易：

```
$ cat > ~/.profile
PS1='What Now!  '
PATH=~/bin:$PATH
Ctrl-d
```

## 6.5 更多变量赋值方法

之前的示例已展示如何将一个简单的字符串赋给指定的变量。在两种其他情况下，您可能希望将值赋给变量：首先，您可能希望 shell 脚本从键盘交互式地获取一个值，然后将其存储在变量中，其次，您可能希望执行一个命令并将命令的标准输出重定向到变量中而不是显示到屏幕上。正如您可能猜到的，这两种类型的变量赋值都是可用的。

### 6.5.1 交互式输入

shell 脚本可以使用 read 命令从标准输入获取字符行并将其分配给一个或多个变量。在最简单的形式中，read 命令单独使用，不指定变量。在这种情况下，从标准输入读取的字符串被赋给变量 REPLY。如果您根据以下文本创建一个名为 readtest1 的可执行 shell 脚本：

```
echo -n "Enter some text: "
read
echo The text was: $REPLY
```

然后运行它，您将得到如下结果：

```
$ readtest1
Enter some text: THIS IS THE TEXT I ENTERED!!
The text was: THIS IS THE TEXT I ENTERED!!
```

通常，使用 echo 时，它会自动在行尾添加一个换行符，以便后续输出从下一行开始。正如示例所示，使用 echo 的 -n 开关会导致 echo 抑制换行输出，以便随后发送到显示器的任何字符都跟在同一行上。在这种情况下，后续的文本是您响应 read 命令输入的文本。正如您所见，这允许您在 shell 脚本内部给出提示，并在同一行立即获取响应。

如果您在 read 命令后指定变量名，则输入行将被赋给该变量而不是变量 REPLY。

更有趣的情况是当您在 read 命令后指定多个变量时会发生什么。考虑 shell 脚本 readtest2：

```
echo -n "Enter some text: "
read one two restofline
echo The first word was: $one
echo The second word was: $two
echo The rest of the line was: $restofline
```

执行时，此脚本将像之前一样读取一行输入。不过这次，该行将被拆分为单独的单词。第一个单词将被赋给列出的第一个变量，第二个单词赋给第二个变量，第三个单词赋给第三个变量，以此类推，直到用完单词或变量（或两者）。

如果单词和变量同时用完，那也没问题，因为每个变量都会有一个单词赋给它：

```
$ readtest2
Enter some text: 1 2 3
```

```
The first word was: 1
The second word was: 2
The rest of the line was: 3
```

如果先用完单词，这只意味着后面的变量不会从输入中赋值为值，而是被设为空（或 NULL） instead：

```
$ readtest2
Enter some text: 1 2
The first word was: 1
The second word was: 2
The rest of the line was:
```

如果单词比变量多，则每个变量都赋予其预期的单词，但随后，而不是丢弃多余的单词，它们会被附加到列表中最后一个变量的值中：

```
$ readtest2
Enter some text: 1 2 3 4
The first word was: 1
The second word was: 2
The rest of the line was: 3 4
```

read 命令对它所认为的单词有一个相当宽泛的定义——任何由空格、制表符或换行符分隔的字符字符串。事实上，这个分隔符列表只是默认值，并且这些字符存储在名为 IFS 的 shell 变量中。因此，如果需要，可以将分隔符集更改为其他值。

### 6.5.2 命令替换

命令替换允许将管道的标准输出用作管道本身的替代。一个简单的示例可能有助于阐明这一点：

```
$ date
Wed Jun 14 22:50:52 BST 1995
$ datestore=`date`
$ echo $datestore
Wed Jun 14 22:51:11 BST 1995
```

在此示例中，date 命令用于显示其输出的格式。然后，相同的命令再次执行，这次在成对的反引号 (`) 之间，这使得 date 的标准输出可用，在这里被赋给变量 datestore。

一种实现相同效果的替代记法是将命令或管道用括号括起来，并在前面加上美元符号：

```
$ datestore=$(date)
$ echo $datestore
Wed Jun 14 22:53:21 BST 1995
```

在命令替换中经常使用的另一个命令称为 basename。此命令的作用是以完整的文件路径名作为参数并返回去掉路径后的基本文件名。例如：

```
$ basefile=`basename /usr/bin/man`
$ echo $basefile
man
```

## 6.6 自动状态变量

当您执行 Linux 命令时，它要么可以无错误地运行完成，要么会遇到一些问题从而阻止它完成任务。如果您在 shell 脚本中使用命令，了解发生了哪种事件会非常有用，以便在出现错误时可以采取某种补救措施。所有 Linux 命令都安排在终止时返回一个值。该值称为退出状态。退出状态为零表示命令成功，而任何非零值表示命令不成功。在管道的情况下，返回的退出状态只是管道中最后一个（最右侧）命令的退出状态。

每当您运行命令或管道时，shell 都有一个名为 $? 的特殊变量，它被赋值为返回的退出状态：

```
$ cd /zz
bash: /zz: No such file or directory
$ echo $?
1
$ echo $?
0
```

在此示例中，尝试更改目录到 /zz 失败，因为该目录不存在。因此，显示 $? 的值表明 cd 的退出状态为非零。请注意，第二次显示 $? 的内容会得到不同的结果。这是因为在每个命令或管道完成后变量的值都会更新，而第二次显示实际上表明第一个 echo 命令执行成功。

shell 脚本本身可以通过使用 exit 命令返回退出状态。您应该养成指定明确且适当的退出状态值的习惯，以便由您的 shell 脚本返回：

```
$ cat >tryexit
```
