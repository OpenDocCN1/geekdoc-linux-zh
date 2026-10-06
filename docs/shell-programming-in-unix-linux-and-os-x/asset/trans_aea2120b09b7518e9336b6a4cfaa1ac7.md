

# trap 命令 259

作为 trap 命令的一个示例，下面的内容展示了当有人尝试从终端中断程序时，如何删除某些文件并退出：

```
trap 'rm $WORKDIR/work1$$ $WORKDIR/data$$; exit' INT
```

一旦执行了这个 trap，如果程序接收到 SIGINT（信号数 2），`work1$$` 和 `data$$` 这两个文件将被自动删除。如果用户在此 trap 执行后中断了程序的运行，你可以确保这两个临时文件会被删除，而不会留在文件系统中。`rm` 之后的 `exit` 是必要的，因为如果不执行退出，程序将在接收到信号所在的位置继续执行。

信号 1-SIGHUP 或 HUP 用于挂断（hangup）：最初与拨号连接有关，但更广泛地指的是意料之外的断开，例如互联网连接掉落。你可以通过在信号列表中添加 SIGINT 来修改 trap，以便在这种情况下也删除这两个指定的两个文件：

```
trap 'rm $WORKDIR/work1$$ $WORKDIR/data$$; exit' INT HUP
```

现在，如果行挂断，或者用户使用 DELETE 键或 Ctrl+c 中断处理，这些文件将被删除。

如果要 trap 的序列（也称为 trap 处理程序）包含多个命令，则必须包含在引号中。还要注意，shell 会在 trap 执行时以及接收到信号列表中的任一信号时扫描该命令。

在前面的示例中，`WORKDIR` 和 `$$` 的值将在 trap 命令执行时时被替换。如果你想让这种替换在定义 trap 的时候发生：

```
trap 'rm $WORKDIR/work1$$ $WORKDIR/data$$; exit' INT HUP
```

trap 也可以用于让你的程序更加友好。在下一章对 rolo 程序的进一步修订中，Ctrl+c 中断信号将由程序捕获，并将用户带回主菜单，而不是让程序完全退出。

# 不带参数的 trap

不带参数执行 `trap` 将显示你已定义或修改的任何 trap 处理程序：

```
$ trap 'echo logged off at $(date) >>$HOME/logoffs' EXIT
$ trap                             List changed traps
trap - 'echo logged off at $(date) >>$HOME/logoffs' EXIT Log off
$ Ctrl+c
login: steve Log back in
Password:
$ cat $HOME/logoffs See what happened
logged off at Wed 2 15:11:58 EDT 2002
$
```

设置了一个 trap，每当 shell 接收到退出信号（信号 0，EXIT）时执行。由于是在登录 shell 中设置的，因此当你注销时，trap 处理程序会将你的注销时间写入文件 $HOME/logoffs。该命令被包含在单引号中，以防止 shell 在定义 trap 时执行 `date`。

执行不带参数的 `trap` 命令将列出针对信号 0 (EXIT) 要采取的新操作。当 steve 注销并重新登录时，文件 $HOME/logoffs 证实了 `echo` 命令已执行且 trap 正常工作。

# 忽略信号

如果为 trap 列出的命令为空，则在接收到指定信号时将忽略它。例如，命令：

```
trap " SIGINT"
```

这指定要忽略中断信号。在执行某些你不希望发生的操作时，你可能想要忽略某些信号。

注意，`trap` 允许你通过名称、简称名称（INT）或全信号名称（SIGINT）指定信号。我们鼓励你使用记忆名称来帮助生成可读性代码，但当然取决于你的喜好。

在示例中，第一个参数必须指定为空值以忽略信号，这不等同于编写以下内容，后者有其独立的含义：

```
trap 2
```

如果你忽略了一个信号，所有子 shell 也会忽略该信号。然而，如果你指定了信号处理操作，则所有子 shell 在接收到信号时将自动采取默认操作，而不是新的代码序列。

假设你执行了命令：

```
trap " 2"
```

然后启动一个子 shell，该子 shell 随后执行其他程序作为子 shell。如果生成了中断信号，它对正在执行的 shell 或子 shell 将没有影响，因为它们默认会忽略该信号。

相反，如果你不是执行上一个 trap 而是执行了：

```
trap : 2
```

然后执行你的子 shell，当前 shell 在接收到中断时将什么都不做（它将执行空命令），而子 shell 将被终止（默认操作）。

# 重置 trap

在你更改了接收到信号时采取的默认操作后，你可以简单地省略第一个参数来再次使用 `trap` 将其改回；因此

```
trap HUP INT
```

将接收到 SIGHUP 或 SIGINT 信号时采取的操作重置为 shell 的默认行为。

许多 shell 程序还会使用这样的结构：

```
trap /bin/rm -f $tmpfile; exit INT QUIT EXIT
```

以确保如果临时文件未创建，`rm` 命令不会产生错误信息。trap 处理会在临时文件存在时删除它，如果不存在则什么都不做。

# 更多 I/O

你已经知道了用于输入重定向、输出重定向、追加输出重定向的标准结构 `<`、 `>`, `>>`。你还知道通过写入 `2>` 而不是 `>` 可以从任何命令重定向标准错误。

```
command 2> file
```

有时你可能想在程序中重定向标准错误。通过对上述内容的稍微修改，你可以通过写入后续的文件符将标准输出重定向到标准错误。描述符 0 是标准输入，描述符 1 是标准输出，描述符 2 是错误。记住 `>` 和 `&` 之间不允许有空格。

向标准错误写入消息：

```
echo "Invalid number of arguments" >2
```

你可能想将程序的标准输出（通常称为 "stdout"）和标准错误（"stderr"）都重定向到同一个文件。如果你知道文件名，这是简单的：

```
command > foo 2>> foo
```

在这里，stdout 和 stderr 都将被写入 foo。你也可以写：

```
command > foo 2>&1
```

达到相同的效果；标准输出被重定向到 foo，标准错误被重定向到标准输出（标准输出已重定向到 foo）。因为 shell 在命令行上从左到右评估重定向，如果 stderr 序列出现在命令行首部，则最后一个示例将无法正常工作：

```
command 2>&> foo
```

因为你将首先将标准错误重定向到标准输出，然后将标准输出重定向到 foo。

你还可以使用 `exec` 命令在程序中动态重定向标准输入或输出：

```
exec < datafile
```

从 datafile 重定向标准输入。后续执行的命令将从 datafile 而不是标准输入读取。命令

```
exec > /tmp/output
```

对标准输出执行相同的操作：后续写入标准输出的所有命令都将写入 /tmp，除非显式重定向到别处。自然地，标准错误也可以重新分配：

```
exec 2> /tmp/errors
```

所有后续到标准错误的输出将去 /tmp/errors。

# <&- &&

序列 `&-` 的作用是关闭标准输出。如果前面是一个文件符，则关闭关联的文件。因此，写入

```
ls <&
```

会导致 ls 的输出无处可去，因为在 ls 执行时 shell 会关闭标准输出。我们承认，这并不大用！

# 内联输入重定向

如果 `<<` 字符遵循以下格式的命令

```
command <<word
```

shell 使用随后的行作为命令的输入，直到找到只包含 `>` 的行。这里有一个简单的示例：

```
$ wc -l << ENDOFDATA
```

使用直到 ENDOFDATA 的行作为标准输入

```
> here's a line
> and another
> and yet another
> ENDOFDATA
3
```

```
$
```

