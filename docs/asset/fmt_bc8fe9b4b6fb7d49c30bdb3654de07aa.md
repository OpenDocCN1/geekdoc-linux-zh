
当你使用输出重定向运算符将输出重定向到文件时，shell 会用你指定的命令的输出覆盖该文件中的数据。例如，命令 `$ date > now` 会用 `date` 命令的输出覆盖文件 `now` 中的所有数据。因此，你应格外小心，确保指定的文件不包含重要信息。

## Appending to a File

简单地通过重定向输出来覆盖文件通常是不期望的。幸运的是，shell 提供了使用 `>>` 运算符的第二种输出重定向形式，它将输出追加到文件。基本语法如下：

```
cmd >> file
list >> file
```

在此形式中，输出会被追加到 `file` 的末尾。如果文件不存在，则会创建它。例如，你可以使用以下命令防止每次添加日期时文件 `mylog` 的数据丢失：

```
{ date; uptime; who ; } >> mylog
```

如果你查看 `mylog` 的内容，你会发现它包含两个列表的输出：

```
11:15am up 79 days, 14:48, 5 users, load average: 0.00, 0.00, 0.00
ranga tty1 Aug 28 14:12
ranga tty2 Aug 28 14:13
ranga tty0 Oct 27 19:42 (:0.0)
amma tty3 Oct 30 08:29 (localhost)
ranga tty4 Nov 14 11:13 (rishi.bosland.u)
Sat Nov 14 11:15:54 PST 1988
11:15am up 79 days, 14:48, 5 users, load average: 0.00, 0.00, 0.00
ranga tty1 Aug 28 14:12
ranga tty2 Aug 28 14:13
ranga tty0 Oct 27 19:42 (:0.0)
amma tty3 Oct 30 08:29 (localhost)
ranga tty4 Nov 14 11:13 (rishi.bosland.u)
```

## Redirecting Output to a File and the Screen

在某些情况下，你需要将脚本的输出同时定向到文件和终端。一个例子是需要生成其活动日志文件的 shell 脚本。对于交互式脚本，日志文件不能仅包含重定向到文件的脚本输出。

将输出重定向到文件和屏幕，可以使用 `tee` 命令。基本语法如下：

```
cmd | tee file
```

这里 `cmd` 是命令的名称，例如 `ls`，而 `file` 是要写入输出的文件名。例如，命令

```
$ date | tee now
```

在终端上产生以下输出：

```
Sat Nov 14 19:50:16 PST 2001
```

相同的输出也被写入文件 `now`。

## 输入

许多 UNIX 程序是交互式的并从用户读取输入。要在 shell 脚本中使用此类程序，需要以非交互方式为其提供输入。此外，脚本通常需要向用户询问输入以便正确执行命令。

要向交互式程序提供输入或从用户读取输入，需要使用输入重定向。在本节中，您将详细了解以下方法：

- 从文件重定向输入
- 从用户读取输入
- 将一个命令的输出重定向到另一个命令的输入

### 输入重定向

当您需要在脚本中使用交互式命令，例如 `mail` 时，需要为命令提供输入。一种方法是將命令的输入存储在文件中，然后告诉命令从该文件读取输入。您可以使用输入重定向来实现这一点。输入可以以与输出重定向类似的方式重定向。一般而言，输入重定向为

```
cmd < file
```

这里 `file` 的内容成为 `cmd` 的输入。作为示例，以下命令是重定向的绝佳用法：

```
Mail ranga@soda.berkeley.edu < Final_Exam_Answers
```

这里 `Mail` 命令的输入，即成为邮件消息正文的部分，是文件 `Final_Exam_Answers`。在这个特定示例中，教授可能会执行此功能，而该文件可能包含当前期末考试的答案。

### Here 文档

输入重定向的额外用途是在创建 here 文档中。假设您需要将电话号码或 URL 列表发送到打印机。您可以将要发送到打印机​​的信息输入到 here 文档中，然后将该 here 文档发送到打印机。这比使用临时文件要简单得多，临时文件需要创建然后应删除。

Here 文档的一般形式如下：

```
cmd << delimiter
document
delimiter
```

这里 shell 将 `<<` 运算符解释为读取输入直到找到包含指定 `delimiter` 的行的指令。直到包含 `delimiter` 的行之前的所有输入行然后被馈送到 `cmd` 的标准输入。`delimiter` 告诉 shell here 文档已完成。没有它，shell 将永远继续读取输入。`delimiter` 必须是一个不包含空格或制表符的单个词。例如，要打印快速的 URL 列表，您可以使用以下 here 文档：

```
lpr << MYURLS
http://www.csua.berkeley.edu/~ranga/
http://www.cisco.com/
http://www.marathon.org/story/
http://www.gnu.org/
MYURLS
```

要在此示例中删除制表符，您可以为 `<<` 运算符提供 `-` 选项。

您还可以将 here 文档与输出重定向结合使用如下：

```
cmd > file << delimiter
document
delimiter
```

如果以此形式使用，`cmd` 的输出将被重定向到指定的文件，而 `cmd` 的输入成为 here 文档。例如，您可以使用以下命令创建包含前面给出的简短 URL 列表的文件：

```
cat > urls << MYURLS
http://www.csua.berkeley.edu/~ranga/
http://www.cisco.com/
http://www.marathon.org/story/
http://www.gnu.org/
MYURLS
```

### 读取用户输入

在 shell 脚本中常见的任务是提示用户输入然后读取其响应。您可以使用 `read` 命令读取用户的响应并将其存储在变量中。变量在第 8 章“变量”中详细解释。`read` 命令的语法如下：

```
read name
```

它读取用户在按下 Enter 之前输入的整行，并将输入字符串分配给 `name` 指定的变量。以下示例说明了 `read` 的用法：

```
echo "What is your name? \c"
read NAME
```

用户的响应存储在变量 `NAME` 中。

![](img/3def70414996f811615f713b2077a154_96_0.png)

> 在某些版本的 `echo` 中，前一个示例中的 `\c` 将按字面意思出现在输出中如下：
> 
> What is your name? \c
> 
> 如果您遇到此行为，您应该改用以下 `echo` 命令，而不是前一个示例中给出的命令：
> 
> `echo -n "What is your name?"`

## 管道

大多数在 UNIX 中设计用于处理文件的命令也可以从 STDIN 读取输入。这使您能够使用一个程序过滤另一个程序的输出。使用一个程序操作另一个程序的输出是在 shell 编程中最常见的任务之一。本节提供了该技术的简短描述；第 15、16 和 17 章包含更详细的示例。

您可以使用管道将一个命令的输出重定向到另一个命令的输入，管道将多个命令用管道连接如下：

```
cmd1 | cmd2 | ... | cmdN
```

管道字符 `|` 将 `cmd1` 的标准输出连接到 `cmd2` 的标准输入，以此类推。命令可以简单也可以复杂，具体取决于需要。以下命令说明了管道的用法：

```
tail -f /var/adm/messages | more
ps -ael | grep "UID" | more
```

在第一个示例中，`tail` 命令的标准输出被管道传输到 `more` 命令的标准输入，这使得输出可以一次一屏地查看。在第二个示例中，`ps` 的标准输出连接到 `grep` 的标准输入，而 `grep` 的标准输出连接到 `more` 的标准输入，以便可以一次一屏地查看 `grep` 的输出。`tail` 和 `grep` 命令在第 15 章“文本过滤器”中详细解释。

![](img/3def70414996f811615f713b2077a154_97_0.png)

> 关于管道的重要一点是每个命令都作为单独的进程执行，并且管道的退出状态是最后一个命令的退出状态。
> 
> 在编写必须进行错误处理的脚本时，牢记这一事实至关重要。

## 文件描述符

当您发出任何命令时，会打开三个文件并与该命令关联。在 shell 中，每个文件都由一个称为文件描述符的小整数表示。文件描述符是一种机制，您可以通过它将一个数字与文件名关联，然后使用该数字从文件中读取和写入。文件描述符通常称为文件句柄。

- 标准输入 `STDIN`，`0`
- 标准输出 `STDOUT`，`1`
- 标准错误 `STDERR`，`2`
