
如果一个符号依赖于另一个符号，必须按照从左到右的顺序指定重定向。在上面的命令中，首先将标准错误更改为 `cat.output.errors` 文件，然后将标准输出也指向同一个文件 `cat.output.errors`。`cat lab1 lab2 lab3 1> cat.output.errors 2&1` 命令执行了相同的任务。

因此，下面的命令并没有达到上述两个命令的效果，因为在该命令中，标准错误在重定向之前就已经变成了标准输出的副本。因此，stderr 首先成为 stdout（此时为显示器）的副本，然后标准输出被更改为 `cat-output.errors` 文件。因此，命令的输出进入了 `cat-output.errors` 文件，而错误则显示在屏幕上。

```
$ cat lab1 lab2 lab3 1> cat.output.errors
```

```
$
```

在 TC shell 中，你可以使用 `>&` 操作符将命令的 stdout 和 stderr 重定向到同一个文件，如下所示。`%` 符号用作 TC shell 的提示符。

```
$ cat lab1 lab2 lab3 >< cat.output.errors
```

```
$
```

## 82 第3章 输入输出重定向

TC shell 没有重定向 stderr 操作符。你可以通过在子shell 中执行命令（通过括号包裹命令）将命令的 stdout 和 stderr 附加到不同的文件。在下面的命令中，`find` 命令的输出进入 `out` 文件，错误消息进入 `error.log` 文件。

```bash
# (find -name foo -print foo.paths) >& error.log
```

默认情况下，输出和错误重定向会覆盖目标文件的内容。Bash 的 `noclobber` 变量可以防止意外覆盖文件。你可以通过如下所示的 `set -C` 命令设置此变量。如果你想永久设置此变量，请将 `set -C` 命令放在 `~/.profile` 等启动文件中。

```bash
# $ set -C
```

你可以使用如下所示的 `set` 和 `unset` 命令在 TC shell 中设置和重置（取消）`noclobber` 变量。

- `% set noclobber`
[ 交互会话 ]
- `% unset noclobber`

当 `noclobber` 变量被设置时，你可以使用 `>|` 操作符强制覆盖文件。

## 3.5 向文件追加数据

你可以使用 `>>` 操作符代替 `>` 操作符，将命令生成的输出或错误追加到文件末尾。与 `>` 操作符类似，`1>>`（追加到 stdout）和 `2>>`（追加到 stderr）可以分别重定向输出和错误并追加。在下面的命令中，`cat` 的输出被追加到 `stuff` 文件，错误消息追加到 `error.log` 文件。

```
$ cat memo letter >> stuff 2>> error.log
```

在接下来的章节内练习中，你将在命令行练习 LINUX/UNIX shell 的输入、输出和错误重定向功能。

## 章节内练习

- 3.1 写一个 shell 命令，显示当前工作目录下名为 `memo` 的文件的行数、单词数和字符数。使用输入重定向。
- 3.2 重复练习 3.1，但将输出重定向到名为 `counts.memo` 的文件。使用 IOO 重定向。
- 3.3 写一个 shell 命令，将 `lab3,lab4,lab5` 文件追加到 `labs` 文件的末尾。任何错误消息都追加到 `error.log` 文件。
- 3.4 写一个 TC 命令在你的家目录下定位 `lab1` 文件。将输出和错误消息重定向到 `lab1.all` 文件。
- 3.5 重复练习 3.4，但命令输出应进入 `find.lab1` 文件，任何错误消息进入 `error.log` 文件。
- 3.6 写一个 shell 命令，使用 `mail` 命令将 `greetings` 文件的内容发送到 `doe1@domain.net`。如果 `mail` 命令失败，输出应进入 `mail`。使用输入重定向。
- 3.7 写一个 shell 命令，在根目录 `/` 下搜索名为 `sort` 的文件。确保错误消息不显示在屏幕上。

## 3.4 LINUX/UX 过滤器与管道

LINUX 和 UNIX 命令被称为过滤器（filters），它们从 stdin 读取输入，进行某种处理，并将结果发送到 stdout。管道和过滤器常用于 LINUX/UX 执行单个命令无法完成的任务。常用的过滤器有 `cat`, `grep`, `gzip`, `ip`, `pr`, `sort`, `tr`, `uniq`, `wc` 和 `zip`。管道和重定向操作符可以在命令行结合使用。

有时你需要连接多个命令。下面的命令行演示了多个管道的使用，形成了一个命令管道。在该命令行中，我们使用了 `sort`、`uniq` 和 `grep` 过滤器。

| command1 | command2 | command3 | ... | commandN |
|---|---|---|---|---|
| 语法: | command1 的 stdout 连接到 command2 的 stdin | command2 的 stdout 连接到 command3 的 stdin | | |

通常，只要其中一个命令输出到另一个命令，任何两个命令都可以通过管道连接。例如，在下面的命令中，`more` 命令接收 `ls -1` 的输出作为其输入。

```
$ ls -1 | more
[ -1 命令的输出一次显示一次 ]
```

任何可以使用管道完成的任务也可以仅使用重定向操作符完成，但这样做需要许多命令、临时文件和昂贵的磁盘操作。例如，创建一个包含 `ls -l` 输出的临时文件。然后一次一页地显示临时文件的内容。最后，删除临时文件。

```
$ ls -l > temp
$ more temp
[ -l 命令的输出一次显示一页 ]
$ rm temp
```

图 3.2 `ls -1 | more` 命令的语义

```
$ ls -1 | more
[ -1 命令的输出一次显示一次 ]
```

## 重定向与管道的结合 85

在 TC shell 中，你可以使用 `| &` 操作符将一个命令的标准输出（stdout）和标准错误（stderr）附加到另一个命令的标准输入（stdin）。以下是该操作语法。

```
command1 | & command2
```

用途：`command1` 的 stdout 和 stderr 被附加到 `command2` 的 stdin。

在以下命令中，`cat` 命令的 stdout 和 stderr 被附加到 `grep` 命令，`grep` 命令的 stdout 被附加到 `sort` 命令的 stdin，而 `sort` 命令的 stdout 则被重定向到 `JohnDoe` 文件中。

```
$ cat filele2 | grep "John Doe" | sort JohnDoe
```

## 3.5 重定向与管道的结合

单凭重定向操作符和管道无法在单行命令行中将命令的 stdout 重定向到文件，同时将其连接到另一个命令的 stdin。`tee` 工具可以完成此任务。你可以使用 `tee` 工具告诉 shell 将命令的 stdout 发送到一个或多个文件，同时作为另一个命令的 stdin。以下是 `tee` 命令的语法。

```
tee [options] file-list
```

`tee` 工具通常用于通过管道读取另一个命令的输出，而不是读取键盘输入。此外，命令输出会被保存到 file-list 中的文件中，并重定向到另一个命令，而不是显示在屏幕上。以下是该工具的常用语法。

```
command1 | tee [options] file-list | command2
```

用途：该命令语法的语义是：执行 `command1`，将其输出存储在文件 file1 到 fileN 中，同时作为输入发送给 `command2`

## 86 第3章 输入/输出重定向

![](img/62803a90ad1a923bf070a7b5e2ffbb05_103_0.png)

图 3.3 命令 `cat tempfile | grep "John Doe" | tee file 1 file 2 | wc -l` 的语义。

以下命令给出了 `tee` 工具的一个示例。

```
$ cat names students | grep "John Doe" | tee file1file2 | wc -l$
```
