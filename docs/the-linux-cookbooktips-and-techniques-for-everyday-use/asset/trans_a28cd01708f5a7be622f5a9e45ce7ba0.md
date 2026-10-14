

[1]+  Stopped                  info -f cookbook.info

在此示例中，作业编号为 1，停止的命令是 `info -f cookbook.info`。作业编号旁边的 `+` 字符表示这是最近的作业。

如果在注销时有任何停止的作业，shell 将不会注销你，而是这样告诉你：

```
$ logout RET
There are stopped jobs.
$
```

此时你可以列出你的作业（参见章节 [Listing Your Jobs]），停止正在运行的任何作业（参见章节 [Stopping a Job]），然后注销。

## 4.3.2 Putting a Job in the Background

新作业默认在前台运行，除非另有指定。要在后台运行作业，请在输入行末尾加上一个和号（`&`）。这对于运行执行大量计算的非交互式程序很有用。

- 要将命令 **apropos shell > shell-commands** 作为后台作业运行，请输入：

```
$ apropos shell > shell-commands &
[1] 6575
$
```

shell 会输出作业编号（本例中为 1）和进程 ID（本例中为 6575），然后返回到 shell 提示符。当后台作业完成时，shell 会列出作业编号、命令，然后是文本 `Done`，表示作业已成功完成：

```
[1]+  Done                  apropos shell > shell-commands
```

要将作业从前台移动到后台，首先挂起它（参见章节 [Suspending a Job]），然后输入 **bg**（意为“background”）。

- 例如，要在前台启动命令 **apropos shell > shell-commands**，挂起它，然后指定它在后台完成，你需要输入：

```
$ apropos shell > shell-commands RET
C-z
```
```
[1]+  Stopped
apropos shell > shell-commands
$ bg RET
[1]+ apropos shell > shell-commands &
$
```

如果已挂起多个作业，请通过提供其作业编号作为参数来指定要放入后台的作业。

- 要将作业 4 置于后台，请输入：

```
$ bg %4 RET
```

> NOTE: 将作业置于后台有时被称为“backgrounding”或“amping off”一个作业。

## 4.3.3 Putting a Job in the Foreground

输入 fg 可将后台作业移动到前台。默认情况下，fg 作用于最近的后台作业。

- 要将最近的后台作业带到前台，请输入：

```
$ fg RET
```

当有多个后台作业时，要移动特定作业到前台，请将作业编号作为选项指定给 fg。

- 要将作业 3 带到前台，请输入：

```
$ fg %3 RET
```

## 4.3.4 Listing Your Jobs

要列出当前 shell 中正在运行的作业，请输入 jobs。

- 要列出你的作业，请输入：

```
$ jobs RET
[1]- Stopped          apropos shell > shell-commands
[2]+ Stopped          apropos bash > bash-commands
$
```

此示例显示了两个作业——apropos shell > shell-commands 和 apropos bash > bash-commands。作业编号旁边的 `+` 字符表示它是最近的作业，而 `-` 字符表示它是最近作业之前的作业。如果没有当前作业，jobs 不会返回任何内容。

要列出你在系统上运行的所有进程，请使用 ps 而不是 jobs——参见 Listing System Activity。

## 4.3.5 Stopping a Job

输入 C-C 会在作业完成前中断前台作业，从而退出程序。

- 要中断正在前台运行的 cat，请输入：

```
$ cat RET
C-c RET
$
```

使用 kill 中断（“kill”）后台作业，并指定作业编号作为参数。

- 要杀死作业编号 2，请输入：

```
$ kill %2 RET
```

## 4.4 Command History

你的命令历史是你在当前或之前的 shell 会话中输入的命令的顺序列表。这些历史列表中的命令称为事件。

## The Linux Cookbook: Tips and Techniques for Everyday Use:

默认情况下，`bash` 会记住最后 500 个事件，但这个数字是可配置的（参见章节 [Customizing Future Shells](#)）。

你的命令历史存储在你主目录中的一个名为 `.bash_history` 的文本文件中；你可以像查看或编辑任何其他文本文件一样查看或编辑此文件。

拥有命令历史记录让你可以做两件非常有用的事情：重复你上次输入的命令，以及（正如本章前面所解释的那样）对历史进行增量反向搜索。

以下各节解释了如何查看你的历史记录并在命令行中指定其中的事件。有关命令历史的更多信息，请参阅 Info 文件 `bashref.info`，节点 `Bash History Facilities`。

- [4.4.1 Viewing Your Command History](#) — 查看你输入的历史记录。
- [4.4.2 Specifying a Command from Your History](#) — 从你的历史记录中替换命令。

[<](#) [>](#) [<<](#) [Up](#) [>>](#) [Top](#) [Contents](#) [Index](#) [?](#)

### 4.4.1 Viewing Your Command History

使用 `history` 查看你的命令历史。

- 要查看你的命令历史，请输入：

```
$ history RET
1 who
2 apropos shell > shell-commands
3 apropos bash > bash-commands
4 history
$
```

此命令显示你的命令历史文件的内容，每行列出一个命令，并在前面加上其 *event number*。使用事件编号来指定历史记录中的该事件（参见章节 [Specifying a Command from Your History](#)）。

如果你的历史记录很长，这个列表会滚动出屏幕，在这种情况下，你可能希望将输出通过管道传递给 `less` 以便浏览。它也很常见通过将输出通过管道传递给 `grep` 来搜索过去的命令（参见章节 [Redirecting Output to Another Command's Input](#) 和 [Searching for a Word or Phrase](#)）。

- 要在历史记录中搜索文本 `apropos`，请输入：

```
$ history | grep apropos RET
```

