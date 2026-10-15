
在接下来的示例中，`read2` 读取了一个调用内置命令 `echo` 的命令行。shell 执行该命令，然后显示 Thanks。接下来，`read2` 读取了一个执行该实用程序的命令行：

```
# $ read2

Enter a command: echo display this message.
Please display this message.
Thanks

# $ read2

Enter a command: who
alex pts/4      Jun 17 07:50 (:0.0)
scott pts/12   Jun 17 11:54 (bravo.tcorp.com)
Thanks
```

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

```
# $ read3

Enter something: this is something
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

当你进入的单词比 `read` 拥有的变量多时，`read` 会为每个变量分配一个单词。

### 命令替换

命令替换允许你将命令的输出作为另一个命令的参数。有两种方法可以：使用反引号 `` ` `` 或使用 `$( )` 语法。反引号语法较旧，而 `$( )` 语法更受青睐，因为它更容易嵌套。

```bash
$ echo "The today is $(date)"

The today is May 22 10:00:00 UTC 2024
```

括号内命令的输出会在执行前被替换到命令中。这对于获取命令的结果非常有用。

并位于工作目录列表中。字符串中的空值表示工作目录。字符串的最后一个元素有一个空值（冒号与行尾之间没有任何内容）。工作目录由开头的冒号表示（不建议；请参见下文的安全框）、末尾的冒号表示（如示例所示），或字符串中任何位置的两个相邻的冒号表示。你也可以用一个 `(.)` 显式地表示工作目录。以下命令为 `PATH` 赋值并将其导出。导出 `PATH` 使其新值对登录会话期间可能调用的子 shell 可用：

```
$ export PATH=/usr/local/bin:$bin:/usr/bin:/home/alex/bin
```

请参见第 708 页列表中的“PATH”以获取技术示例。由于 GNU/Linux 将许多可执行文件存储在名为 `bin`（二进制文件）的目录中，因此用户通常也会将自己的可执行文件放在自己的 `~/bin` 目录中。如果你像 Alex 那样将 `bin` 目录放在 `PATH` 的末尾，shell 将在 `PATH` 中列出的目录目录查找它找不到的命令。

## PATH 与安全

当考虑安全问题时，不要将工作目录放在 `PATH` 的最前面。例如，大多数人在进入目录时会将 `ls` 作为第一个命令。如果目录的所有者在该目录下有一个同名的可执行文件，则会执行该文件而不是系统命令，可能会导致意外的结果。如果你以超级用户（Superuser）身份运行，绝不应该将工作目录放在 `PATH` 的最前面。事实上，超级用户的 `PATH` 完全省略工作目录是非常普遍的。你始终可以通过在名称前加一个 `/` 来执行工作目录中的文件，例如 `/.`。

如果你想将目录添加到 `PATH` 中，可以在设置 `PATH` 的新值时引用 `PATH` 变量的旧值。以下命令将 `/usr/X11R6/bin` 添加到当前 `PATH` 的前端，并将 `/usr/bin` 添加到末尾：

```
$ PATH=/usr/X11R6/bin:$PATH:/usr/bin
```

### MAIL: 你的邮件已妥收

`MAIL` 变量包含存储邮件的文件的路径（你的邮箱，否则为 `/var/spool/mail/name`，其中 `name` 是你的登录名）。

`PATH` 变量包含一个由冒号分隔的文件名列表。当列表中的某个文件名被修改时（例如当邮件到达时），shell 会通过此变量通知你。你可以在列表中的任何文件名后加上百分号（%），后跟一条消息。该消息将替换你在登录时收到邮件时的“you have mail”提示。

`MAILCHECK` 变量指定了 shell 检查新邮件的频率。默认值是 60 秒。如果你将此变量设置为 0，shell 会在每次提示符出现前进行检查。如果你按如下方式取消设置 `MAILCHECK`，shell 将完全不检查邮件：

```
$ unset MAILCHECK
```

### PS1: 用户提示符（主）

`PS1` 或 `prompt` 变量持有 shell 用于告知你它正在等待命令的提示符。本章示例中使用的 bash 提示符是 `$ `（空格）；你的提示符可能有所不同。当你更改 `PS1` 或 `prompt` 的值时，你就更改了提示符的外观。

如果你在多台机器上工作，将机器名称纳入提示符中会有帮助。以下示例显示了如何将提示符更改为你正在使用的机器名称，后面跟着冒号和空格（提示符末尾的空格会让你在提示符后输入的命令更易读）：

```
$ PS1='hostname': 

bravo.tcorp.com: echo test

bravo.tcorp.com:
```

前面的命令在 bash 和 tsh 下均有效。bash 下的优选结构是：

```
$ PS1="$(hostname)":
```

### PS2: 用户提示符（次）

提示符字符串2（Prompt String 2）是 shell 存储在 `PS2` 中的次级提示符。在以下示例的第一行，有一个未闭合的引号字符串。shell 假设命令尚未结束，并在第二行给出提示符（`>`）。此提示符表示 shell 正在等待输入：

```
$ PS2="echo 'line1

> line2'"
line1
line2
```

之前的命令会影响你的提示符：

```
$ PS1="hostname": 

bravo.tcorp.com: echo "

line'
```

### IFS: 输入字段分隔符

`IFS` 变量持有内部字段分隔符。请参见第 612 页的“单词拆分”。

### CDPATH: 扩展范围

`CDPATH` 和 `path` 变量允许你在使用 `cd` 切换工作目录时引用同名目录。当你调用 shell 脚本时，命令名和参数是位置参数。虽然你可以引用它们，但只有 `set` bash 内置命令允许更改位置参数的值（第 584 页）。

### $0: 调用程序名称

shell 将你调用程序时使用的命令名称存储在参数 `$` 中。它是 0 号参数，因为它出现在命令行第一个参数之前：

- 8. 虽然它是 shell 内置命令，`set` 无法更改位置参数的值。

```bash
$ cat abc

echo The name of the command used

echo to execute this shell script was $0

$ abc

The name of the command used

execute this shell script was abc
```

此 shell 脚本使用 `echo` 来验证你正在执行的脚本名称。

### $1-$Sn: 命令行参数

命令行上的第一个参数由参数 `$1` 表示，第二个参数由参数 `$2` 表示，以此类推直到 `$x`。以下脚本显示了持有命令行参数的位置参数：

```bash
$ cat display_sargs

echo The first five command line

echo arguments are $1 $2 $3 $4 $5

$ display_sargs jenny alex helen

The first five command line

arguments are jenny alex helen
```

`display_sargs` 脚本显示了前五个位置参数。shell 会为每个代表命令行中不存在的参数分配一个空值（null value）。`$4` 和 `$5` 变量具有空值。

`@` 变量代表所有的命令行参数，如 `display_all` 程序所示：

```bash
$ cat display_all

echo All the command line arguments are:

echo $$

$ display_all a b c d e f g h i j k l m n o p

All the command line arguments are:

a b c d e f g h i j k l m n o p
```
