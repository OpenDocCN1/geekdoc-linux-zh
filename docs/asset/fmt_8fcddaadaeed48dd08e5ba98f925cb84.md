
`% set noclobber`

your interactive session

...

`% unset noclobber`

`%`

```
```

如果设置了 `noclobber` 变量，命令 `cat file1 > file2` 会在 `file2` 已存在时生成错误消息。如果 `file2` 不存在，则会创建它并将 `file1` 的数据复制到其中。命令 `cat file1 >> file2` 在 `file2` 存在且 `noclobber` 设置时有效，但在 `file2` 不存在时会生成错误消息。你可以使用 `>`, `>>!` 和 `>>&!` 运算符来覆盖 `noclobber` 变量设置时的效果。因此，即使 `noclobber` 变量已设置且 `file2` 存在，命令 `cat file1 >! file2` 也会将 `file1` 的数据复制到 `file2`。对于 `cat file1 >>! file2` 命令，如果 `noclobber` 变量已设置且 `file2` 不存在，则会创建 `file2` 并将 `file1` 的数据复制到其中。`>>&!` 运算符的工作方式与 `>>!` 运算符类似。

## 9.14 I/O 和错误重定向回顾

表 9.1 总结了 Bourne、Korn 和 C shell 中的输入、输出和错误重定向运算符。我们在本章中没有讨论其中一些运算符；我们将在第 12 章至第 15 章的 shell 编程中详细讨论它们。我们将这些运算符包含在此表中，因为这似乎是将它们全部一起展示的最合适位置。请注意，所有适用于 Bourne 和 Korn shell 的运算符也适用于 Bash shell。

## 9.15 FIFOs

FIFO，也称为命名管道，也可用于系统上两个进程之间的通信。虽然通过管道通信的进程必须通过你执行的共同祖先进程相互关联，但进程

## 表 9.1 Bourne、Korn 和 C shell 中重定向运算符及其含义

| Operator | Bourne Shell | Korn Shell | C Shell |
|---|---|---|---|
| < file | Input redirection | Input redirection | Input redirection |
| > file | Output redirection | Output redirection | Output redirection |
| >> file | Append standard output | Append standard output | Append output |
| 0< file | Input redirection | Input redirection |  |
| 1> file | Output redirection | Output redirection |  |
| 2> file | Error redirection | Error redirection |  |
| 1>> file | Append standard output to file | Append standard output to file |  |
| 2>> file | Append standard error to file | Append standard error to file |  |
| <&m | Attach standard input to file descriptor m | Attach standard input to file descriptor m |  |
| >&m | Attach standard output to file with descriptor m | Attach standard output to file with descriptor m |  |
| m>&n | Attach file descriptor m to file descriptor n | Attach file descriptor m to file descriptor n |  |
| <&- | Close standard input | Close standard input |  |
| >&- | Close standard output | Close standard output |  |
| m<&- or m>&- | Close file descriptor m | Close file descriptor m |  |
| >& file |  |  | Output and error redirection |
| >| file |  | Ignore noclobber and assign standard output to file |  |
| >>| file |  | Ignore noclobber and append standard output to file |  |
| >! file |  |  | Ignore noclobber and assign standard output to file |
| >>! file |  |  | Ignore noclobber and append standard output to file; if file does not exist, create it |
| >>&! file |  |  | Ignore noclobber and append standard output and standard error to file |
| cmd1 | cmd2 | Connect standard output of command cmd1 to standard input of command cmd2 | Connect standard output of command cmd1 to standard input of command cmd2 | Connect standard output of command cmd1 to standard input of command cmd2 |

(Continued)

# 表 9.1（续）Bourne、Korn 和 C Shell 中的重定向运算符及其含义

| 运算符 | Bourne Shell | Korn Shell | C Shell |
|---|---|---|---|
| cmd1 | &cmd2 |  | 将命令 `cmd1` 的标准输出和标准错误连接到命令 `cmd2` 的标准输入 |
| (cmd>/dev/tty)>&file | | | 将 `cmd` 命令的标准错误重定向到文件。 |
| | & | | 允许命令的 stdout 和 stderr 连接到另一命令的 stdin |

使用 FIFO 进行通信不必具有这种关系——它们可以是在一个系统上独立执行的程序。对于管道和 FIFO 的命令行使用，这意味着管道只能用于通过管道连接的命令之间的通信，而 FIFO 可用于单独运行的命令之间的通信。管道和 FIFO 之间的另一个区别是，管道是 UNIX 内核维护的主内存缓冲区且没有名称，而 FIFO 是在磁盘上创建并具有像文件名一样的名称。这意味着与文件一样，FIFO 在用于进程间通信之前必须先创建并打开。因此，访问 FIFO 需要访问其所在的二级存储设备。

管道是进程持久的，这意味着它们只要创建它们的进程存在就存在。大多数 UNIX 系统上的 FIFO 是文件系统持久的，这意味着它们会一直存在于系统上，直到被显式删除/移除或相关文件系统被卸载（即从系统中移除）为止。

你可以使用 `mk nod()` 系统调用或 `mkfifo()` 库调用在程序中创建 FIFO，也可以使用 `mkfifo` 命令在 shell 会话中创建文件。我们在本节讨论 FIFO 的命令行使用。我们将在系统编程章节（第 18 章至第 21 章）中讨论 FIFO、管道以及相关的系统调用和库调用。下面是对 `mkfifo` 命令的简要描述。

#### 语法

```
mkfifo [option] file-list
```

+   **用途：** 创建 `file-list` 中给出的路径名的 FIFO
+   **输出：** 为 `file-list` 中给出的路径名在相关目录中创建 FIFO
+   **常用选项/功能：**
+   - `-m mode` 将新创建的 FIFO 的访问权限设置为“mode”，访问权限的指定方式与 `chmod` 命令相同，例如 `666`，表示每个人都有读和写权限，无人有执行权限

在下面的会话中，我们使用第一个命令创建名为 `myfifo1` 的 FIFO，其默认权限基于 `umask` 的当前值（参见第 5 章中的讨论）。我们

使用第二个命令创建名为 `myfifo2` 的 FIFO，其所有者具有读和写权限，所有其他用户无权限。我们使用 `ls -al myfifo1 myfifo2` 命令来显示两个 FIFO 的访问权限。请注意，两个 FIFO 的长列表中的第一个字符是 "p"，表示 `myfifo1` 和 `myfifo2` 是 FIFO（命名管道）类型。

```
$ mkfifo myfifo1

$ mkfifo -m 600 myfifo2
```
