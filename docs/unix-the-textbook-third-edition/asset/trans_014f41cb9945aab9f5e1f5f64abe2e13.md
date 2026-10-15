

![](img/02e070097d401d3bf7de4bf1c470b267_360_0.png)

## FIGURE 9.15 Semantics of the ssh server cat ~/research/pvm/datafile.server | diff datafile - command.

以及发送给另一个命令。下面是对 tee 实用程序通常用法的简要描述。

```
SYNTAX
command1 | tee file1 file2 ... fileN | command2

Purpose: Standard output of command1 is connected to the stdin of tee, and tee sends its input to files file1 through fileN as well as the stdin of command2
```

此命令语法的语义是 command1 被执行，其输出存储在 file1 到 fileN 文件中，同时作为输入发送给 command2。tee 实用程序的使用示例在以下命令中给出。

```
$ cat names students | grep "John Doe" | tee file1 file2 | wc -l
$
```

此命令从 names 和 students 文件中提取包含字符串 "John Doe" 的行，将这些行通过管道传递给 tee 实用程序，tee 将这些行的副本写入 file1 和 file2，同时将它们发送给 wc -l，后者将输出发送到显示屏。因此，names 和 students 文件中包含字符串 "John Doe" 的行被保存到 file1 和 file2 中，并且此类行的行数显示在监视器屏幕上。图 9.16 说明了此命令行的语义。此类命令在 shell 脚本中很有用，其中需要在脚本后面对 file1 和 file2 执行不同的操作。

## 9.13 OUTPUT AND ERROR REDIRECTION IN THE C SHELL

执行输入、输出和追加操作 (<, >, >>) 的运算符在 C shell 中与在其他 shell 中一样工作，如前所述。然而，在 C shell 中，这些运算符不能使用文件描述符。此外，错误重定向在 C shell 中的工作方式与其他 shell 不同。在 C shell 中，输出和错误重定向的运算符是 >&。

![](img/02e070097d401d3bf7de4bf1c470b267_361_0.png)

FIGURE 9.16 Semantics of the cat names students | grep "John Doe" | tee file1 file2 | wc -l command.

### SYNTAX

```
command >& file
```

Purpose: Redirect stdout and stderr of command to file

例如，以下命令将 ls -l foo 命令的输出和错误重定向到 error.log 文件。命令的标准输入仍连接到键盘。请注意，我们使用 % 符号作为 shell 提示符，这是 C shell 的默认值。

```
% ls -l foo >& error.log
%
```

C shell 没有单独重定向 stderr 的运算符。然而，如果命令在子 shell 中执行，则可以通过将命令用括号括起来，使命令的 stdout 和 stderr 连接到不同的文件。以下会话说明了这一点。

```
% find ~ -name foo -print >& output.error.log
% (find ~ -name foo -print > foo.paths) >& error.log
%
```

你的当前 shell 进程的子进程，也称为子 shell，执行所有外部 shell 命令。执行第一个命令时，find 命令的输出和错误会进入 output.error.log 文件。因为子 shell 进程要等到整行命令被处理完才创建，所以由于 >& 运算符，父 shell 进程的 stdout 和 stderr 被重定向到 error.log 文件。因此，子 shell 的 stdout 和 stderr 也被重定向到 error.log 文件。

在第二个命令中，find 命令在子 shell 下执行并继承父 shell 的标准文件。当括号中的 find 命令执行时，它将命令的 stdout 重定向到 foo.paths 文件；命令的 stderr 仍连接到 error.log。因此，find 命令的输出进入 foo.paths 文件，而命令产生的错误进入 error.log 文件。图 9.17 说明了第二个 find 命令的语义。

你可以使用 >& & 运算符将 stdout 和 stderr 重定向并追加到文件中。例如，ls -l foo >& & output.error.log 将 ls 命令的 stdout 和 stderr 重定向并追加到 error.log 文件。

C shell 还允许使用 |& 运算符将命令的 stdout 和 stderr 连接到另一个命令的 stdin。下面是对该运算符的简要描述。

### SYNTAX

```
Command1 |& command2
```

Purpose: Redirect stdout and stderr of command1 to command2, that is, pipe stdout and stderr of command1 to command2

在以下命令中，cat 命令的 stdout 和 stderr 连接到 grep 命令的 stdin。因此，cat 命令的输出或其产生的任何错误，例如由于 file1 或 file2 缺少读权限而产生的错误，都作为输入提供给 grep 命令。

```
% cat file1 file2 |& grep "John Doe"
%
```

I/O 重定向和管道运算符（ | 和 |& ）可以在单个命令中使用，如以下会话所示。此命令是前一个命令的扩展，

