

# v.4.33 Linux 作为数字取证平台的全方位入门指南

我们可以讨论的三种流：stdin 是标准输入（通常是键盘）；stdout 是标准输出（通常是显示器）；而 stderr 是标准错误（通常是显示器）。

我们使用特定的符号来重定向这些流：

- stdin: <n
  - cmd < infile
  - cmd 从 infile 获取输入，而不是键盘。

- stdout: >
  - cmd > outfile
  - cmd 将输出发送到 outfile 而不是显示器。

- stderr: 2>
  - cmd 2> errlog
  - cmd 将任何错误消息发送到文件 errlog。

操作流对于某些任务非常有用，例如创建一个包含挂载卷（volume）或目录中文件列表的输出文件。例如：

```
barry@forensic1:-$ ls -al filelist.txt
```

上述命令将输出当前目录中所有文件的长列表。它不是将列表输出到控制台，而是创建一个名为 filelist.txt 的新文件，其中包含该列表。如果 filelist.txt 已经存在，则它将被覆盖。使用以下命令将命令的输出追加到现有文件，而不是覆盖它：

```
barry@forensic1:-$ ls -al >> filelist.txt
```

另一个有用的工具是命令管道，它使用 `|` 符号。命令管道接收一个命令的输出并将其直接“管道”到另一个命令的输入。

在这种情况下，我们将输出重定向到另一个命令而不是文件。你可以看到下方的区别。我可以使用 `>` 将字符串回显到文件，也可以使用 `|` 将其回显到命令。下面显示的 `wc` 命令提供了行、字和字节的计数。在第一次重定向中，我正在使用 echo 的输出创建一个名为 wc 的文件。在第二次中，我使用了管道，因此 echo 的输出被发送到命令 wc。在第三次中，我正将 echo 的输出管道到 wc，并将 wc 的输出重定向到一个文件：请遵循下文，并进行实验。不要这样做。

```
bar@forensic1:~$ echo hello
hello
bar@forensic1:~$ echo hello > wc
bar@forensic1:~$ echo hello | wc
1 1 6
bar@forensic1:~$ echo hello | wc > outfile.txt
bar@forensic1:~$ cat outfile.txt
1 1 6
```

这是命令行中极其强大的工具。查看以下进程列表（显示部分输出）：

```
bar@forensic1:~$ ps ax
PID TTY STAT TIME COMMAND
1 ? S 0:00 init [4]
2 ? S 0:00 [kthread]
3 ? S 0:00 [ksoftirqd/0H]
5 ? S< 0:00 [kworker/0:0H]
6 ? S 0:00 [kworker/u4:0]
7 ? S 0:00 [rcu_sched]
<continues>
```

如果你只想看到那些表示 bash 的进程 ID 呢？你可以将 `ps` 的输出 `pipe` 到 `grep` 的输入，并指定 bash 为 `grep` 搜索的模式。结果将只给你提供 `ps` 输出中包含 bash 模式的行。

```
bar@forensic1:~$ ps ax | grep bash
1522 pts/0 S 0:00 bash
1714 pts/1 S 0:00 -bash
1729 pts/1 S+ 0:00 grep bash
```

有时你可能想既在屏幕上显示命令的输出，又同时将其重定向到文件中。你可以使用 `tee` 命令来实现此点。

```
bar@forensic1:~$ ls | tee filelist.txt
```

# v.4.33 Linux 作为数字取证平台的全方位入门指南

Desktop/Documents/Evidence/winlog.txt

```
barry@forensic1:-$ cat filelist.txt
```

Desktop/Documents/Evidence/winlog.txt

在上面的会话中，我们使用 `tee` 命令将 `ls` 命令的输出显示在屏幕上，并发送到名为 filelist.txt 的文件中。在取证检查的范围内，这对于在文件中捕工具的输出非常有用（记得使用 `>>` 追加）。

将多个强大的命令组合在一起是 Linux 为取证分析提供的最有用且最强大的技术之一。如果你打算将 Linux 作为一种取证工具，这是你想要学习的最重要的概念之一。通过由多个命令和管道构建的单个命令行，你可以使用多个实用程序和程序快速构建一个分析。

# 文件属性

Linux 文件系统（如 ext2, ext3, ext4）支持所谓的的文件属性。有几种属性，我们不会涵盖所有属性。其中有两种属性对于保护取证数据免受随意的删除和篡改非常有用。它们是只允许追加 (a) 和不可变 (i)。

属性是控制允许在文件目录上发生哪些文件操作的标志位。其中某些属性可以更改，而另一些则不能。我们可以使用 `lsattr` 列出当前目录下文件和目录的属性。

```
root@forensic1:/MyDirectory# lsattr
------e /data
------e /textfile.txt
------e /file1.txt
------e /log.txt
```

我有一个目录，在 /home/$USER 目录下（由提示符中的 `~/DIRNAME` 指定）。此输出显示所有可用属性、文件和单个目录（data 是一个目录）都只有 extents 属性 (e)。我们不会涵盖

> “区段（Extents）是一种以连续方式映射物理数据块的方法。”

# Linux 作为数字取证平台的全方位入门指南

我们使用 `chattr` 命令添加属性，只需在文件名后使用 `+` 添加我们想要的属性。例如，如果我想让 `data/` 变为不可变，我可以这样添加 `i` 属性：

```
root@forensic1:/~/Directory# chattr +i data/
root@forensic1:/~/Directory# lsattr
------ /data
------ /textfile.txt
------ /file1.txt
------ /log.txt
root@forensic1:/~/Directory# rm -rf data
rm: cannot remove 'data': Operation not permitted
```

我们为 data 目录添加了不可变 (i) 属性，你可以在随后的 `chattr` 属性显示中看到 ./data。当我们尝试用 `rm-rf` 删除目录时，我们发现即使我们是 root，操作也是不允许的。这非常强大。我们无法删除该目录，无法向目录中添加或更改文件。

现在我们将为 log.txt 添加只允许追加 (a) 的属性。该属性意味着文件只能以追加模式打开。我们无法更改或删除当前内容，也不能向其添加内容。当我们把输出重定向到日志文件以记录工作时，会发现这一点。

```
root@forensic1:/~/Directory# chattr +a log.txt
root@forensic1:/~/Directory# lsattr
------ /data
------ /textfile.txt
------ /file1.txt
------ /log.txt
root@forensic1:/~/Directory# echo "text" > log.txt
: log.txt: Operation not permitted
root@forensic1:/~/Directory# echo "text" >> log.txt
```

我们使用 `chattr` 修改属性，使用 `lsattr` 查看 log.txt 中的更改，然后尝试重定向输出覆盖文件（使用单重定向 `>`），这失败了。然而追加是成功的（追加通过 `>>` 完成，我们将在指南后续部分介绍更多关于重定向的内容）。关于 extents 可以在网上找到。https://en.wikipedia.org/wiki/Chattr

# v.4.33 Linux 作为数字取证平台的全方位入门指南

某些属性（例如 a 和 i）只能由 root 设置。你可以拥有用户文件的属性，但必须由 root 设置。

# 元字符

Linux 命令行（在本例中实际上是 bash）也支持通配符（元字符）：

- `*` 用于多个字符（包括空）
- `?` 用于单个字符。
- `]` 用于字符组或字符或数字范围。

这是一个复杂且非常强大的主题，需要进一步阅读……请参考你喜爱的 Linux 文本中的“正则表达式”，以及“通配符（globbing）”或“shell 扩展”。这些差异可能会让学者感到困惑，所以不要对不同情况下的 "*" 感到沮丧。

# 命令提示

- 1. Linux 有命令历史（存储在主目录下的 .bash_history 文件中）。使用键盘方向键滚动已输入的命令。
- 2. Linux 支持命令行编辑。你可以使用光标移动之前的命令并修正错误。
- 3. Linux 命令和文件名区分大小写。
- 4. 学习输出重定向到 stdout 和 stderr（“1”和“2”）。稍后介绍。
- 5. Linux 使用 / 表示目录，MS Windows 使用 $。
- 6. Linux 使用 - 表示命令选项，DOS 使用 /。
- 7. 在 less 或 man 会话中使用 q 退出。
- 8. 要执行当前目录中的命令（如果当前目录不在 PATH 中），请使用 `./command` 语法。这告诉 Linux 在当前目录中查找命令。除非明确指定，否则当前目录不是正常路径的一部分。

