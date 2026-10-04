
## 第 9 章

使用 `echo` 命令显示文本和 shell 变量的值：

- `$ age=32` [Return] ... 将值 32 赋值给 age。
- `$ echo Hi, nice day` [Return] ... 显示参数字符串。
  Hi, nice day
- `$ echo $age` [Return] ... 显示参数，单词 age。
  32
- `$ echo Sage` [Return] ... 现在参数是 Sage，即 age 中存储的值。
  32
- `$ echo "You are $age years old."` [Return] ... 添加文本以获得更具意义的输出。
  You are 32 years old.
- `$ ...` 准备执行下一条命令，
  shell 变量经常被用作命令行上的命令参数，如下所示：

- `$ all=-laF` [Return] ... 创建一个名为 all 的变量，并将值（字符串）-laF（大写、小写字母 l、大写字母 F、小写字母 a）赋值给它。
- `$ ls $all myfirst` [Return] ... 将变量作为命令行输出的一部分使用
- `$ ...` 显示提示符。
  变量名前面有 `$`。shell 将值 -laF 替换为变量 all。替换后，命令变为 `-laF myfirst`。

- 观察以下命令的输出。它们展示了变量在引号之间时解释方式的微妙区别。

- `$ age=32` [Return] ... 将 32 赋值给变量 age。
- `$ echo $age "$age" '$age'` [Return] ... 显示 age。
  32 Sage Sage
- `$ ...` 提示符。

### 9.2.4 理解标准 shell 变量

标准 shell 变量的赋值通常由系统管理员设置。当你登录时，shell 会引用这些变量来跟踪你的环境。然而，这些更改是临时的，仅对当前会话有效。下次登录时，你必须重新设置它们。如果你希望更改永久生效，请将它们放在一个名为 `.profile` 的文件中。`.profile` 文件将在本章稍后的部分进行解释。

#### HOME

当你登录时，shell 将你的 HOME 目录的全路径分配给变量 `HOME`。多个 UNIX 命令使用 `HOME` 变量来定位 HOME 目录。例如，不带参数的 `cd` 命令会检查此变量，以确定 HOME 目录的路径，然后将系统切换到你的 HOME 目录。

要对 `HOME` 变量进行实验，尝试以下命令序列：

```
$ echo $HOME [Return] ... 显示你的 HOME 目录路径。

/usr/david

$ pwd [Return] ... 显示当前目录路径。

/usr/david/source

$ cd [Return] ... 未指定参数。默认是你的 HOME 目录。

$ pwd [Return] ... 检查你的当前目录。你在 david，即你的 HOME 目录。

/usr/david

$ HOME=/usr/david/memos/important [Return] ... 修改你的 HOME 目录路径。

现在你的 HOME 目录是 important。

$ cd [Return] ... 回到你的 HOME 目录。

$ pwd [Return] ... 显示当前目录；你的当前目录是 important。

/usr/david/memos/important

$_ ... 提示符出现。
```

#### IFS

内部字段分隔符 (`IFS`) 变量设置为一组字符，shell 将这些字符作为命令元素的分割符。例如，要获取目录下文件的长列表，输入 `ls -l` 并按 [Return]。命令中的空格字符将命令 (`ls`) 与其选项 (`-`) 隔开。

赋值给 `IFS` 变量的其他分隔符是制表符 [Tab] 和换行符 [Return]。

`IFS` 字符是不可见的（非打印）字符，因此你不在等号右侧看到它们。但它们确实在那里！

```
$ echo $IFS [Return] ... 显示赋值给 IFS 的字符。

$_ .

```

空行和提示符返回。赋值给 `IFS` 的字符是不可打印的。

将 `IFS` 字段分隔符改为（冒号）。原始 `IFS` 设置在更改之前会被保存，随后恢复为原始字符。

```
$ cd $HOME [Return] ... 注意字段分隔符在 cd 和 HOME 之间是一个空格。

$ old_IFS=$IFS [Return] ... 保存 IFS 字符。

$ IFS=":" [Return] ... 将字段分隔符改为 :

$ cd:$HOME [Return] ... 注意冒号被用作字段分隔符而不是空格。

$ IFS=$old_IFS [Return] ... 将字段分隔符还原。

$_ ... 提示符返回。
```

不建议更改字段分隔符。你通常是为了适应特殊情况而这样做。我们将在第 13 章的示例程序中使用此功能。

#### MAIL

`MAIL` 变量被设置为接收你邮件的文件名。发送给你的邮件存储在该文件中，shell 会定期检查该文件的内容，如果有你的邮件会通知你。例如，如果你将邮箱箱设置为 `/usr/david/mbox`，则需要输入 `MAIL=/usr/david/mbox` 并按 [Return]。

#### MAILCHECK

`MAILCHECK` 变量指定了 shell 检查 `MAIL` 变量设置的文件是否有邮件到达的频率。`MAILCHECK` 的默认值为 600（秒）。

#### PATH

`PATH` 变量被设置为 shell 搜索命令（程序）位置的目录名称。path 字符串中的目录由冒号分隔。path 字符串中的第一个字符如果解释为 `:`，意味着首先搜索当前目录。UNIX 通常将可执行文件存储在名为 `bin` 的目录中。你可以创建自己的目录并将可执行文件存储在其中。如果你将你的目录（或其它路径）添加到路径中，shell 将在这些目录中查找命令。

#### PS1

提示符字符串 1 (`PS1`) 变量设置为作为提示符的字符串。shell 提示符被设置为美元符号 (`$`)。如果你厌了看到美元符号，可以通过为 `PS1` 赋值新值来轻松更改。

```
$ PS1=Here ... 更改提示符为

Here:-

$ PS1="Here " [Return] ... 在末尾添加一个空格。

Here:- 看起来好多了！
```

如果你的提示符字符串包含空格，必须用引号括起来。

```
$ PS1="Next Command:" [Return] ... 更改提示符。

Next Command:- 更改成功。

$ PS1="$" [Return] ... 改回美元符号。

$ ... 提示。
```

#### PS2

提示符字符串 2 (`PS2`) 变量设置为当你按下 [Return] 但未完成命令时显示的提示符。你可以以更改 `PS1` 相同的方法更改 `PS2`。二级提示符默认为大于号 (`>`)。

以下命令序列展示了二级提示符的示例：

- `$ echo "Good news, UNIX [Return].` . 命令未完成；因此显示二级提示符。现在命令完成。
> `is CDs."` [Return] ... 现在命令完成。
Good news, UNIX is CDs.... 命令未完成；这由反斜杠表示。
- `$ ls \` [Return] ... shell 显示二级提示符并等待命令的剩余部分。
> `...` 现在命令完成。shell 将其组合为 `ls -l` 并执行它。提示符返回。
> `-l` [Return] ...
$_ ...

#### CDPATH

`CDPATH` 被设置为一组绝对路径列表，类似于 `PATH` 变量。`CDPATH` 影响 `cd`（切换目录）的操作。如果此变量未定义，`cd` 会在你的工作目录中查找匹配的文件。如果子目录不在工作目录中，`cd` 会搜索指定的目录并在 Unix 显示错误消息。如果此变量已定义，`cd` 将根据赋值给 `CDPATH` 变量的路径进行搜索。如果找到了，它将成为你的工作目录。

例如，如果你输入 `CDPATH=$HOME:$HOME/memos` 并按 [Return]，下次使用 `cd` 命令时，它将从当前目录开始搜索，然后是 `HOME` 目录，最后是 `memos` 以匹配指定的文件。

#### SHELL

`SHELL` 变量设置为登录 shell 的全路径：

```
SHELL=/bin/sh
```

#### TERM

`TERM` 变量设置你的终端类型：

```
TERM=ansi
```

#### TZ

`TZ` 变量设置你所在的时区：

```
TZ=EST
```

它通常由系统管理员设置。

# 更多元字符

如你在第 8 章中所记忆的，元字符（或特殊字符）由 shell 以一种特殊的方式进行解释和处理。到目前为止，我们已经讨论了文件替换和重定向的元字符。本节将探索更多的元字符。

## 9.3.1 执行命令：使用反引号

在命令前后使用反引号（`` ` ``）会告诉 shell 执行该命令，并将命令的输出插入到命令行的相同位置。这也被称为*命令替换*。其格式如下：

其中 *command* 是要执行的命令名称。

反引号字符位于键盘最左侧的按键上，紧挨着 [`Esc`] 键的的下方。

以下命令序列展示了命令替换的示例：

```
$ echo The date and time is: `date` [Return] . Command date is executed.

    The date and time is: Mon Nov 28 14:14:14 EDT 2005

    $_ . . . . . . The prompt is back.
```

shell 扫描命令行，找到反引号并执行命令 `date`。它将命令行上的‘date’替换为 `date` 命令的输出并执行该命令。

```
$ echo "List of filenames in your current directory:\" ' 'ls -C' > LIST [Return]

    $ cat LIST [Return] . . . . . . . . . . Check what you have stored in LIST.
```

```
List of filenames in your current directory:

    memos myfirst REPORT

    $_ . . . . . . . . . . . . . . . Ready for the next command.
```

## 9.3.2 命令序列化：使用分号

你可以在命令行上输入一系列命令，并用分号隔开。shell 从左到右顺序执行它们。

要尝试分号元字符，请尝试以下操作：

```
$ date ; pwd ; ls -C [Return] . . . . . . . . . . Three commands in sequence.

    Mon Nov 28 14:14:14 EST 2005

    /usr/david

    memos myfirst REPORT
```

# 探索 Shell

```
$ ls -C > list ; date > today; pwd [Return]. . Three commands in sequence, with the output of two commands redirected to the files.

/usr/david
$ cat list [Return] . . . . Check content of list.

memos myfirst REPORT . . . . . . . Check contents of today.

$ cat today [Return] .
Mon Nov 28 14:14:14 EST 2001
$_ . . . . . . . . . . . Your favorite prompt sign appears.
```

## 9.3.3 命令分组：使用括号

你可以通过将命令放在一对括号之间将它们组合在一起。如果这组命令是一个单一命令，则可以对该组进行重定向。

要尝试将括号作为元字符，请尝试以下操作：

![](img/3847727709b8de371ecce9ca47ff3f66_303_0.png)

```
$ (ls -C ; date ; pwd) > outfile [Return]. . . Three commands in sequence, grouped with the output, redirected to a file.

$ cat outfile [Return] . . . . . Check contents of outfile.

memos myfirst REPORT

Mon Nov 28 14:14:14 EST 2001

/usr/david$_
```

提示符出现。

## 9.3.4 后台处理：使用安符

UNIX 是多任务系统；它允许你并发执行多个程序。通常，你运行一个命令，几秒钟后输出就会显示在终端上。如果你运行一个需要几分钟才能执行的命令怎么办？在这种情况下，你必须等待命令完成才能继续下一个任务。然而，你不需要在所有无意义的分钟里等待。shell 元字符安符（`&`）为你提供了在后台运行程序的手段，只要后台程序不需要从键盘输入。如果你输入一个命令后跟着 `&`，那么该命令将被发送到后台执行，你的终端就可以释放出来执行下一个命令。

以下示例展示了安符元字符的应用：

![](img/3847727709b8de371ecce9ca47ff3f66_303_1.png)

```
$ sort data > sorted & [Return]. . . . Sort data and the results are sorted.

1348

$ date [Return] . . . . . . . Process ID is displayed.

The prompt is immediately displayed, for the next command.
```

`sort` 命令的输出被重定向到另一个文件，以防止在你执行其他任务时 `sort` 将输出发送到终端。

- 1. 后台进程 ID (PID) 标识后台进程，并用于终止它或获取其状态。
- 2. 你可以在单条命令行上指定多个后台命令。

![](img/3847727709b8de371ecce9ca47ff3f66_303_2.png)

# 第 9 章

```
$ date & pwd & ls -C & [Return] . . . . Create three background processes; tree PID numbers are displayed.

2215
2217
2216
$ echo "the foreground process" [Return] . . . Run the echo command in foreground.
Mon Nov 28 14:14:14 EST 2005 . . . . Output from the background process date is displayed.
the foreground process . . . . . . Output from the foreground process echo is displayed.
/usr/david . . . . . . . . . . . Output from the background process pwd is displayed.
$_ . . . . . . . . . . . The prompt appears and then output from the background process ls -C displayed.
memos myfirst REPORT . . . . . . . Ready for the next command.
```

![](img/3847727709b8de371ecce9ca47ff3f66_304_0.png)

默认情况下，后台命令的输出显示在你的终端上。因此，前景程序的输出与后台程序的输出交织，会导致非常混乱的显示。你可以通过将后台命令的输出重定向到文件来防止这种混乱。

## 9.3.5 命令链：使用管道符

shell 允许将一个进程的标准输出作为另一个进程的标准输入。在命令之间使用管道元字符 `|`。通用格式如下：

```
command A | command B
```

其中 `command A` 的输出被作为 `command B` 的输入。你可以将命令序列链接在一起，创建所谓的流水线（pipeline）。让我们来看一些示例，让你体会这种实用且灵活的 shell 能力。

![](img/3847727709b8de371ecce9ca47ff3f66_304_1.png) 输入 `ls -l` 并按 [Return] 将 `ls -l` 命令的输出发送到打印机。要统计你当前目录下的文件数量，请执行以下操作：

- `$ ls -l` [Return] . . . . . . . 看看你目录中的文件。
memos myfirst REPORT
- `$ ls -l > count` [Return] . . . . . . 现在将文件列表保存到 count 中。
- `$ wc -w count` [Return] . . . . . . 统计单词数。你当前目录下有三个文件。

![](img/3847727709b8de371ecce9ca47ff3f66_304_2.png)

- `ls -l | wc -w` [Return] . . . . . 使用管道符获取你当前目录下的文件数量。

命令 `ls -l`（你当前目录下的文件列表）的输出作为 `wc -w` 命令的输入。

# 探索 Shell

要将系统中的登录用户数量保存到文件中，请执行以下操作：

```
$ echo "Number of logged-in users:" who | wc -l > outfile [Return]

$ cat outfile [Return] . . . Check what is stored in outfile.
```
