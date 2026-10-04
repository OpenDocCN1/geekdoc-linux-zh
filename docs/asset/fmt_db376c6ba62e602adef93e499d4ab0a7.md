
# sort

`sort` 命令将排序后的输入输出到标准输出。它执行 ASCII 排序（参见 ascii 的 man 页面）。如果没有提供输入文件，它将从标准输入（stdin）查找待排序的数据。默认情况下，该命令使用空白分隔的键字段进行排序，从最左侧的字段开始。使用 `sort` 的旧版职员可能会使用 `+field_num` 语法指定不同的排序字段。该语法现在已经过时了。`sort` 命令，例如 `sort +5 -k +2 -3 file_to_be_sorted`，请求在第五字段之后查找第一个键并在第六个字段处停止，在第二个字段之后查找决胜键并在第三个字段处停止。该语法应替换为以下内容：

```
sort -k 6 -k 3,4 file_to_be_sorted
```

## 注意

第二个键可以显示为 `-k 3`。如果排序包含多个字段，所示语法将非常有用。此外，`-k` 选项将第一个字段表示为字段数 1。（过时的语法将第一个字段表示为字段数 0。）显然，UNIX 的神们对与此命令保持任何形式的一致性完全不感兴趣！

`sort` 命令的一些选项如下：

- `-b` 忽略排序字段或键开头的空格
- `-c` 检查给定文件是否已经排序；不进行排序
- `-d` 在键中仅考虑 [a-z, A-Z, 和 0-9] 字符
- `-f` 在键中将小写转为大写
- `-g` 根据通用数值值进行比较（可能在在所有的 UNIX 变体上均可用）
- `-k POS1,POS2` 从 POS1 开始并在 POS2 结束键的范围
- `-m` 合并已排序的文件；不进行排序
- `-n` 根据字符串数值进行比较
- `-o FILE` 将结果写入 FILE 而不是标准输出
- `-r` 反转比较结果
- `-u` 仅输出相等序列中的第一个（唯一）

以下示例展示了将简单的 `sort` 字段 4（CMD 列）作为键字段。它使用新语法和过时语法执行相同的排序任务：

![](img/de6a3b5a3b516159c825f1c10314d877_248_0.png)

```
$ cat newfile2

PID TTY TIME CMD

614 pts/1 00:00:00 ksh

727 pts/1 00:00:00 ps

728 pts/1 00:00:00 tee
```

```
$ sort -rk 4 newfile2 # Reverse sort based on key field number 4

728 pts/1 00:00:00 tee

727 pts/1 00:00:00 ps

614 pts/1 00:00:00 ksh

PID TTY TIME CMD
```

```
$ sort -r +3 newfile2 # Same but using old syntax

728 pts/1 00:00:00 tee

727 pts/1 00:00:00 ps

614 pts/1 00:00:00 ksh

PID TTY TIME CMD
```

# grep

`grep` 命令使用正则表达式来搜索字符模式。字母 g 代表全局。`grep` 命令在文件内容搜索请求的模式；它不搜索文件名。如果你需要搜索文件名，请使用 `find` 命令。

`grep` 命令的一些选项如下（查看你的 man 页面确认是否支持）：

- `-A` 打印匹配行之后的 NUM 行上下文
- `-B` 打印匹配行之前的 NUM 行上下文
- `-b` 在输出的每行前打印字节偏移
- `-c` 打印每个输入文件的匹配行数
- `-f` 从 FILE 获取模式，每个一个
- `-h` 在搜索多个文件时抑制文件名前缀
- `-i` 忽略模式和输入文件的大小写区分
- `-n` 在输出的每行前加上行号
- `-r` 递归读取目录下的所有文件
- `-v` 反转匹配意义，选择非匹配行

以下示例展示了使用 `grep` 命令定位文件内的字符串。示例使用了多个正则表达式来表示字符串聚合信息：

![](img/de6a3b5a3b516159c825f1c10314d877_249_0.png)

```
$ cat sortfile2

pears

oranges

apples

beer

$ grep app sortfile2 # Search for app in sortfile2

apples

$ grep s sortfile2 # Search for lines ending with the letter 's'

pears

oranges/apples

$ grep ^b sortfile2 # Search for lines beginning with the letter 'b'

beer

$ ls -1 | grep "^d' # Search the output of ls -1 for directories

drwx-rx-x 2 obrien 1024 Oct 12:30 Mail

drwx-rwxr-x 3 obrien 1024 Nov 4:39 scripts

drwx-rwxr-x 2 obrien 1024 Oct 16:22 temp
```

# sed

`sed` 命令是一个非交互式编辑器。你可以在命令行或 sed 文件中提供编辑。该命令对从输入文件读取的数据应用编辑，并将修改后的数据写入标准输出。语法源于 ed 编辑器（参见 man）。注意 `sed` 不会更改输入文件中的数据。查看 sed 示例末尾关于如何让 sed 在多个文件中进行更改的想法。

`sed` 命令的一些选项是：

- `-n` 除非被 p 命令请求否则产生输出行
- `-e` 提供为数据提供多次编辑的机制
- `-f` 向命令提供完整的 sed 编辑文件

以下示例使用 `sed` 命令替换任何字符串 `appl` 为 `snapple`。注意输出显示文件中的所有行，包括未更改的行。记住 sed 是一个编辑器，而不是像 grep 那样的字符串搜索命令：

![](img/de6a3b5a3b516159c825f1c10314d877_250_0.png)

```
$ sortfile2

pears

oranges

apples

beer

$ sed 's/appl/snappl/' sortfile2 # Replace appl with snapple

pears

oranges

snapple

beer
```

以下示例展示了如何限制 sed 显示的行：

```
$ sed '2q' sortfile2  # Display two lines and then quit

pears

oranges

$ sed '2d' sortfile2  # Delete line 2 from the display

pears

apples

beer

$ sed '1,2d' sortfile2  # Delete first two lines from the display

apples

beer
```

以下示例结合 sed 命令与 Korn Shell 循环来更改文件内容：

```
$ cat test1  # Contents of first test file

Welcome to the world of Donald Davis.

$ cat sedtest2  # Contents of second test file

Donald Davis Knows讲笑话。

$ cat sedtest3 # Contents of third test file

goodbye to the world of Donald Davis.
```

```
$ for f in sedtest3? # Use a loop to make global changes

> do

> mv $f old$f # Rename files

> sed 's/Davis/Duck/' old$f > $f # Recreate original files applying edits

> done
```

```
$ cat sedtest1

Welcome to the world of Donald Duck.

$ cat sedtest2

Donald Duck knows how to quack jokes.

$ cat sedtest3

goodbye to the world of Donald Duck.
```

# xargs

`xargs` 命令构建由你提供的参数和给定的标准输入组成的命令行。它通常在管道中使用。关于 `xargs` 需要记住的关键点是，如果有必要，它将形成多个命令来处理从管道呈现输入数据的大小。

- `-0` 输入文件名以空字符而不是空白符结束。
- `-i[replace-str]` 用从标准输入读取的名称替换初始参数中的 replace-str 出现。
- `-l[max-lines]` 每行命令行最多使用 max-lines 非空输入行。
- `-n max-args` 每行命令行最多使用 max-args 个参数。
- `-p` 提示用户是否运行每个命令行并从终端读取一行。
- `-t` 在执行命令之前在标准错误输出上打印命令行。
- `-P max-procs` 一次运行最多 max-procs 个进程。

以下示例使用 `while` 创建了 19,000 个文件。通过 Ctrl+C 停止循环。然后通过将 `find` 命令的输出管道到 `xargs` 并使用 `rm` 来删除文件。使用 `find` 命令是因为在大多数 UNIX 变体，尝试在命令行使用 `rm *` 会导致“行过长”的错误。

另一种选项是使用 `find` 命令的 `-exec` 选项。然而，它为每个文件创建一个进程。此外，它没有 `xargs` 效率高，`xargs` 让每个进程尽可能在一个命令行中执行多个 `rm` 命令。因此，在删除操作期间创建的进程较少：

```
$ count=1

$ while $file$count # 使用重定向操作创建文件

> do

> count=$count+1

> done # 使用 Ctrl+C 终止循环

$ ls -l | wc -l # 计算我们创建了多少文件

19168

$ pwd

/home/obrien/lotsofiles

$ find . -name "file*" | xargs rm # 使用 find 和 xargs 移除

$ ls -l | wc -l

2
```

# awk

`awk` 命令是一种模式扫描和处理语言。它是一个可编程的过滤器。“awk”这个名字来源于该程序三位创建者的首字母：Aho, Weiner 和 Kernighan。它搜索模式并在匹配模式时执行动作。执行的动作被包含在花括号 `{ }` 围起来。`awk` 可以用于扩展 `sed` 命令的功能。

`awk` 命令的一些选项如下：

- `-F fs` 字段分隔符 指示使用非默认字段分隔符。默认字段分隔符是空白字符（一个或多个空格、制表符）。
- `-v var=val` 在程序执行之前，将值 `val` 赋值给变量 `var`。
- `-f file` 从文件读取 `awk` 程序源码，而不是从第一个命令行参数。

以下示例使用 `awk` 过滤器处理 `stats` 文件中的数据：

| PID | TTY | S | TIME | CMD |
| :--- | :--- | :--- | :--- | :--- |
| 200691 | pts/6 | S | 0:01.11 | dtksh |
| 200731 | pts/6 | I | 0:00.19 | -ksh (ksh) |
| 200774 | pts/6 | I | 0:00.17 | dtksh |

```
$ awk '{print $4}' stats  # 打印 stats 文件中的第四字段

TIME

0:01.11

0:00.19

0:00.17

$
```

以下示例使用 `awk` 处理来自 `/etc/passwd` 的的数据。它还使用了 `-F` 选项，该选项识别一个非默认字段指定符：冒号 (`:`)。

```
$ sed 3q /etc/passwd | awk -F: '{print $1}'  # 显示 /etc/passwd 前 3 条记录的第 1 字段

root

bin

daemon

$

$ awk -F: '{print $1}' /etc/passwd  # 显示 /etc/passwd 中的所有用户名

root

bin

daemon

adm

(...)

obrien

$
```

## 使用临时文件

以下示例将 `awk` 作为格式化工具：

```
$ cat firstlastamount

Dennis O'Brien 234.56

Cheryl Dyment 12345.67

Al Smith 66.33

Juana D'Ance 22.11

# 未格式化的数据

$ awk 'printf "%-4d %10s %10s %10.2f\n", NR, $1, $2, $3' firstlastamount

1 Dennis O'Brien 234.56

2 Cheryl Dyment 12345.67

3 Al Smith 66.33

4 Juana D'Ance 22.11

# Awk 被用格式化工具
```

以下示例使用 `awk` 脚本搜索密码文件，查找密码字段为空（第二个字段）的记录。这是一个重大的安全漏洞，因为它允许任何人无需提供密码即可登录：

```
$ cat breakers

BEGIN # 一个 awk 脚本

{ # 先执行 BEGIN 部分

print "Investigate these accounts:"

}

{ # 模式搜索和动作部分

if ($2 == "*") { print "Account name is ",\nUser is", $5 };

}

END

{print "Done."} # END 部分

$ awk -F -f breakers /tmp/passwd
```

```
Investigate these accounts:
Account name is hacker
User is Bertha D. Blooze
Done.
```

```
$ grep hacker /tmp/passwd

hacker::13:30:Bertha D. Blooze:/bin/ksh
```

## 使用临时文件

如前所述，在文件名方面存在许多选项。脚本可能需要在不可预测的目录或 `/tmp` 目录创建临时文件。脚本的设计应使其不会无意中覆盖另一个用户的文件。如何在不使用繁琐代码的情况下实现？如果你在末尾使用 shell 变量命名你的临时文件，你将创建一个带有进程标识 (PID) 后缀的文件。因此在删除操作期间创建的进程较少：

```
$ $$ # 显示当前 PID

2466

$ touch $$ # 使用 PID 创建文件

-rw-r-- 1 obrien obrien 0 Jan 1 00:00 $$
```

## 接下来

现在你已经增强了文件和目录的知识，接下来的工作是在输出方面尝试更高级的技巧。第 10 章“输出控制”介绍了 `echo`、`print` 和 `printf` 命令。

# 输出控制

你在此阶段所掌握的词汇与之前不同。从书的开始，输出方式就不再一样了。同样，你对脚本的输出方式也发生了变化。你已经开始使用 `echo` 命令。由于你已经开始使用更高级的语句，你还需要进一步改进？本章检查了 Korn Shell 的 `printf` 命令作为 `print` 命令的逻辑扩展，包括输出重定向的不同形式。本章通过查看经常被误解的 here documents 能力结束，该能力允许输入重定向指向当前执行的脚本行。本章将教你：

- `echo` 和 `print` 命令的区别
- 如何使用 `printf` 命令
- 循环和子壳的输出重定向
- 管道与重定向的区别
- 如何重定向 stderr
- 如何使用 here documents

## Echo 输出

Unix 新学习的第一个命令之一是 `echo` 命令。它是一个简单的程序，将命令行参数放置在标准输出 (stdout) 上。任何人都可以轻松理解。`echo` 命令可以在管道中向工具提供输入（如下一个示例所示）。在脚本中，`echo` 可用于提示显示以及产生标准输出。

以下示例使用 `echo` 命令为 `ex` 编辑器产生输入。后续脚本使用 `ex` 搜索文件中包含 `?` 的任何行。找到此类行时将其删除。这消除了与终端关联的进程（TTY 列包含 `?`）。剩余行的计数使用 `wc -l` 创建，并使用子字符串移除最大模式显示。模式移除消除了从第一个 `/` 到行尾的所有字符。如果不使用字符串移除语法，计数变量将包含一个数字后跟着 `/tmp/newstats$`。

```
$ ps aux # 生成日志输出

F UID PID PPID PRI NI VSZ RRS STAT TTY TIME COMMAND

100 0 1 0 0 1104 368 do_sel S ? 0:04 init [5]

040 0 2 1 0 0 0 bdlush SW ? 0:00 [kflush]

(..)

000 500 614 613 12 2084 1284 wait4 S pts/ 4:28 -ksh

000 500 15954 614 19 0 2496 828 - R pts/ 0:00 ps aux
```
