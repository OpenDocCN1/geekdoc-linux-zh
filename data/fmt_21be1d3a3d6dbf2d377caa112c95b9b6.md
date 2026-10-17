
你可能会好奇如何成为一个文件的所有者。事实上，你创建的任何文件自动成为所有者，这是合理的。作为所有者，你可以更改默认权限以及所有权。如果你更改了文件所有权，就会失去所有权权限。

要更改文件或目录的所有权，请使用 `chown` 命令。（懂了吗？`chown` — change ownership，更改所有权。）假设你决定安定下来，过上更沉静的生活，更符合俳句写作这一新职业。其他人将不得不负责周末的狂欢和通宵派对。因此，你放弃了 `partytime` 文件的所有权：

```
maddog@shamet:~ > chown root parttime
```

这把 `parttime` 的所有者更改为了 `root`。如果你想改回来，可以使用 `chown` 命令，但必须以 `root` 身份执行。

![](img/96a9ce6a13d8d15ed05f867f41574278_173_0.png)

在某些 Linux 安装中，你无法使用 `chown` 命令将文件送给别人。你会收到一条错误消息，提示操作不允许（Operation is not permitted）。一些系统管理员认为 `chown` 命令存在安全风险。因此，只有超级用户才能执行 `chown` 命令。如果你拥有发行版之一（《SuSE Linux For Dummies》光盘就是其中之一）并想把文件给别人，我们建议让对方复制文件，创建一个由他们自己拥有的文件。

文件和用户属于不同的组。在 `parttime` 示例中，组是 `users`。设置组允许让你赋予大量用户（而非所有用户）访问权限。组权限和所有权对于确保特殊项目或工作组的成员能够访问整个组所需的文件非常有用。

要查看系统中可用的哪些组，请查看 `/etc/group` 文件。操作时使用 `more` 命令。你会看到一个类似这样的文件：

```
root::0:root
bin::1:1:root,daemon
nobody::99:
users::100:your-user-name, maddog
floppy:x:19:
...
your-user-name:500:your-user-name
```

## 第 8 章：文件与命令的操作

### 随心所欲

Linux 系统中的大多数命令都是灵活的，并且可以通过修改来执行特殊任务。你可以使用两种设备来更改命令：命令选项（options）以及标准输入和输出重定向。首先，你需要了解命令。

你可以使用命令选项来精细调整 Linux 命令的操作行为。在本章的早些部分中，我们引入了 `ls` 命令，以便你可以看到对文件系统执行操作的结果，但我们没有在章节中解释它是如何工作的，或者它执行了哪些更改。要查看选项是如何工作的，在下一个示例中，你将使用不同的选项多次尝试 `ls` 命令。

使用 `mkdir` 命令创建一个名为 `gregger` 的新目录；然后，使用 `cd` 命令将你的工作目录更改到该新目录：

```
maddog@localhost:~/emptirectory> mkdir gregger
maddog@localhost:~/emptirectory> cd gregger
```

在 Linux 提示符下，如下所示输入 `ls`：

```
maddog@localhost:~/emptirectory/gregger> ls
maddog@localhost:~/emptirectory/ 
```

这并没有起到什么作用，对吧？看起来该账户似乎没有文件。你可能需要一个选项。尝试 `-a` 选项看看发生了什么：

```
maddog@localhost:~/emptirectory/gregger> ls -a
maddog@localhost:~/emptirectory/ 
```

记得按照所示的内容精确输入命令和选项。例如，`ls -a` 命令在命令和选项之间有一个空格，而连字符和字母 `a` 之间没有空格。

注意 `ls` 命令显示的两个文件（它们实际上是目录，但在 Linux 中所有目录都是文件）。什么？你只看到了点？嗯，单点 `.` 代表你所在的目录；双点 `..` 代表父目录，通常是你所在目录的上一级目录。（Linux 会为你创建这些文件名并将它们放入目录中。如果你刚刚创建了目录，你拥有的只有以句开头的文件。）

现在我们使用 `touch` 命令在 `gregger` 目录中创建几个额外的文件：

```
maddog@localhost:~/emptirectory/gregger> touch file1
maddog@localhost:~/emptirectory/gregger> touch .dotfile
```

![](img/96a9ce6a13d8d15ed05f867f41574278_176_0.png)

现在如果你执行相同的 `ls` 命令（不带 `a` 选项），你会看到以下内容：

```
maddog@localhost:~/emptydirectory/gregger> ls
file1
maddog@localhost:~/emptydirectory/gregger>
```

如果你使用 `-a` 选项重做 `ls` 命令，你会得到这个：

```
maddog@localhost:~/emptydirectory/gregger> ls -a
..dotfile file1
maddog@localhost:~/emptydirectory/gregger>
```

`ls` 命令默认不列出以点开头的文件。通过添加 `-a` 选项，你修改了 `ls` 的操作，使其打印文件名无论是否以点开头。

`ls` 命令有许多选项，你可以同时使用多个。想看怎么做吗？通过在 `-a` 选项上添加 `-l` 来修改它。命令行变为：

```
maddog@localhost:~/emptirectory/gregger>ls -al
total 5
drwxr-xr-x 3 (username)(group)(filesize) Jan 10 14:33 ../
drwxr-xr-x 6 root (filesize) Jan 04 22:15 ../
-rw-r--r-- 1(username)(group)(filesize) Jun 18 11:30 .dotfile
-rw-r--r-- 1(username)(group)(filesize) Apr 13 17:40 file1
```

如你所示，不仅仅是文件名，`l` 选项显示了更详细的文件列表。如果长列表无法在单行显示，Linux 将其换换到下一行。

大多数情况下，Linux 并不在意你输入选项的顺序，因此认为 `ls -a` 和 `ls -la` 是相同的。然而，并不是所有命令都提供多个选项选择，并且仅适用于使用单字母来指定其选项的命令。

`ls` 命令默认按字母顺序列出文件，但你可以定制输出。例如，`ls -alt` 按日期顺序显示文件，最近的在前；`ls -ltr` 则反转该顺序。

![](img/96a9ce6a13d8d15ed05f867f41574278_177_0.png)

### 噢，管道管道……

Linux 命令会产生大量的输出，如果没有某种控制让它们全部进入屏幕，它们就会飞过。例如，输入以下内容：

```
ls -al /etc
```

此命令列出了你 `/etc` 目录中的所有文件。由于此目录包含许多文件，信息向下滚动的速度比你阅读的速度快。不过，你可以使用称为管道（piping）的进程。Linux 将一个命令的输出作为另一个命令的输入。这听起来可能没那么复杂。在上一个例子中，你有太多信息无法在一个屏幕显示。你可以获取这些信息并放入程序中，该程序将信息分成屏幕大小的部分并显示它们。要这样做，请使用 `more` 命令，这个工具的名字很合适。如何管道？你使用键盘上的空格键。你可能在想那个键是做什么的。如下所示输入命令：

```
ls -al /etc | more
```

Linux 不在乎管道周围的空格，但你可能想使用它们来保持清晰，并养成包含空格的习惯，因为它们有时是重要的。当你按下回车键时，信息一个屏幕一个屏幕地出现，每个屏幕底部都会出现 `more` 字样。

# 154 第三部分：使用 Linux

Linux 附带了一个或两个文本编辑器：`ed` 和 `vi`。`ed` 是一个行导向的文本编辑器。它是 UNIX 系统最早的编辑器之一，传统上包含在每个 UNIX 和 Linux 系统中。它也是一个很小的编辑器，可以包含在较小的 UNIX 和 Linux 发行版中。你可以随时信任 `ed` 的。Linux 附带的第二个编辑器是 `vi`。这个全屏编辑器还支持名为 `ex` 的行导向编辑器的命令集。Linux 的第三种文本编辑器是 `emacs`；有些人倾向于用它来处理大部分工作。

![](img/96a9ce6a13d8d15ed05f867f41574278_181_0.png)

在 Linux 中，`ed` 和 `vi` 是由另一个名为 `vim` 的编辑器模拟的。`vi` 的命令在 `vim` 中运行良好良好。此外，`vim` 的功能比 `vi` 更强大。因此，Linux 系统没有提供一个独立的程序。当你输入 `vi` 时，你实际上在使用 `vim`，但这一点对你来说是不可见的。
