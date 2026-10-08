
请注意，您可能需要启动 telnet 守护进程（telnetd）才能运行 telnet。

如果未运行 telnetd，请参阅 telnetd 的手册页了解启动说明。

telnetd 会向 telnet 会话的客户端发送选项，以便在 telnet 会话期间建立合适的通信交换。

## 第 10 章 UNIX 工具 - grep、awk、sed 及其他

### 并非所有 UNIX 变体都包含所有命令

本章涵盖了许多有用且令人愉悦的命令。然而，并非所有命令在所有 UNIX 变体上都可用。如果某个特定命令在您的系统上不可用，那么您可能有一个类似的命令，或者可以组合多个命令以达到预期结果。

在介绍更高级的命令之前，我会先介绍重定向和文件查看。在使用许多命令时，重定向非常重要，因此在讲解命令之前先介绍这个话题会有所帮助。

我还会介绍文件查看。重定向和文件查看在前文中已经出现；但是，既然你可能直接跳到了这一章，我就免得你翻回去查看如何浏览文件了。

### 重定向

在介绍文件查看之前，让我们花一分钟谈谈重定向，因为接下来的部分会用到一些重定向。我在 shell 编程部分详细介绍了重定向，但现在我想给你一个关于重定向的简单介绍，以便我们更有效地讲解本章的一些命令。

UNIX 系统的设置通常是命令从键盘获取输入，这通常被称为*标准输入*，并且通常将输出发送到屏幕，这通常被称为*标准输出*。命令还会将错误信息发送到屏幕。输入来自标准输入以及输出和错误发送到标准输出并不总是理想的。你被赋予了大量控制权来覆盖这些默认设置。这被称为重定向。表 10-1 展示了许多常见的重定向形式。

如表所示，要将命令的输出从标准输出重定向到文件，你可以使用“>”。这在几乎所有情况下都有效。如果设置了一个名为 **noclobber** 的环境变量，那么重定向到现有文件将不起作用（我们将很快介绍环境变量）。**noclobber** 不允许重定向覆盖现有文件。如果你试图覆盖现有文件，例如下面的 /tmp/processes，你会收到一条文件已存在的消息：

![](img/75f39fc91296b889c0653851accdfd46_609_0.png)

```
# ps -ef > /tmp/processes
/tmp/processes: File exists
```

然而，你可以使用“!”与重定向结合，强制覆盖文件。使用“>!”会强制覆盖文件，而“>>!”将强制输出追加到现有文件的末尾。表 10-1 展示了这些用法示例。

### 表 10-1 常用的重定向形式

| 命令或赋值 | 示例 | 描述 |
| :--- | :--- | :--- |
| `<` | `wc -l < .login` | 标准输入重定向：执行 **wc**（单词计数）并列出 **.login** 中的行数（-l） |
| `>` | `ps -ef > /tmp/processes` | 标准输出重定向：执行 **ps** 并将输出发送到文件 **/tmp/processes** |
| `>>` | `ps -ef >> /tmp/processes` | 追加标准输出：执行 **ps** 并将输出追加到文件 **/tmp/processes** 的末尾 |
| `>!` | `ps -ef >! /tmp/processes` | 追加输出重定向并覆盖 **noclobber**：即使 **/tmp/processes** 已存在也写入其上 |
| `>>!` | `ps -ef >>! /tmp/processes` | 追加标准输出并覆盖 **noclobber**：追加到 **/tmp/processes** 的末尾 |
| `\|` (管道) | `ps \| wc -l` | 运行 **ps** 并将其结果用作 **wc** 的输入 |
| `2` - 标准错误 | `cat program 2> errors` | 将文件 **program** **cat**（输出）到标准输出，并将 **errors** 重定向到文件 **errors** |
| | `cat program 2>> errors` | 将文件 **program** **cat**（输出）到标准输出，并将 **errors** 追加到文件 **errors** |
| | `find / -name '*.c' -print > cprograms 2> errors` | **find** 系统中所有以 **.c** 结尾的文件，将文件列表放入当前工作目录中的 **cprograms**，并将所有错误（文件描述符 2）发送到当前工作目录中的文件 **errors** |
| | `find / -name '*.c' -print > cprograms 2>&1` | **find** 系统中所有以 **.c** 结尾的文件，将文件列表放入当前工作目录中的 **cprograms**，并将所有错误（文件描述符 2）发送到与文件描述符 1（**cprograms**）相同的位置 |

使用表 10-1 中显示的符号，你可以从标准输入和标准输出进行重定向。例如，而不是在屏幕上显示输出，你可以将输出发送到文件。我们将在接下来的示例中使用其中一些重定向形式。

### 使用 cat、more、pg、head 和 tail 查看文件

![](img/75f39fc91296b889c0653851accdfd46_611_0.png)

首先，让我们看一下一个长文件。事实上，让我们看一个长到如果将其内容打印到屏幕上，将无法在一屏内显示的文件。

**cat** 命令（concatenate 的缩写）正好可以做这件事，将文件打印到屏幕上。然而，如果文件很长，你只能在屏幕上看到文件的末尾。还记得本书前面提到的用户 **denise** 吗？她的目录中有许多文件。让我们列出她目录中的文件，并使用以下命令将输出重定向到名为 **listing** 的文件中：

```
$ ls -a /home/denise > listing
```

当我们**cat listing** 到屏幕上时，我们只看到了它的末尾，如 figure 10-1 所示。我们知道这是文件的末尾，因为我使用了带有 **-n** 选项的 **cat**，该选项包含行号。行号表明这不是文件的开头。

![](img/75f39fc91296b889c0653851accdfd46_612_0.png)

图 10-1 cat -n 命令

只看到这个文件的末尾并不是我们想要的结果。使用 **pg**（page 的缩写），我们一次看到一个屏幕，如 figure 10-2 所示。

![](img/75f39fc91296b889c0653851accdfd46_613_0.png)

图 10-2 pg 命令

![](img/75f39fc91296b889c0653851accdfd46_613_1.png)

**more** 命令产生的输出与 **pg** 相同，如 figure 10-3 所示。

![](img/75f39fc91296b889c0653851accdfd46_614_0.png)

这就更像回事了；现在我们可以使用 **pg** 和 **more** 按屏幕逐屏滚动。然而，有时你只想查看文件的开头或结尾。你可以使用 **head** 命令查看文件的开头，使用 **tail** 命令查看文件的底部。以下两个 **head** 和 **tail** 的示例（见图 10-4 和 10-5）分别展示了查看 **listing** 的前 20 行和最后 20 行。

![](img/75f39fc91296b889c0653851accdfd46_614_1.png)

![](img/75f39fc91296b889c0653851accdfd46_614_2.png)

![](img/75f39fc91296b889c0653851accdfd46_614_3.png)

```
head example
$ head -20 listing
..
..
.CbtOptSet
.Xauthority
.cshrc
.cshrc.orig
.elm
.exrc
.fmrc
.fmrc.orig
.glanCerc
.gpmh
.history
.login
.lrom
.mailrc
.netscape-bookmarks.html
.netscape-cache
.netscape-history
.netscape-newsgroups=news.spry.com
$
```

![](img/75f39fc91296b889c0653851accdfd46_615_0.png)

```
tail example
$ tail -20 listing
shellup.exe
smsup2.exe
softinit.remotesoftcm
srvpr.exe
tabnd1.exe
target.exe
tcp41a.exe
tnds2.exe
trace.TRC1
trace.TRC1.Z.uae
upgrade.exe
uae.syntax
v103.txt
who on
win95app.exe
wsdrv1.exe
wsos21.exe
wsos22.exe
wsos23.exe
xferp110.zip
$
```

![](img/75f39fc91296b889c0653851accdfd46_615_1.png)

你使用的命令取决于你希望显示的信息。就个人偏好而言，无论是查看大文件的内容还是长文件列表，我都倾向于使用 **more**。我没有很好的理由，只能说是因为我们是习惯的产物，而且我一直都使用 **more**。以下是 **cat**、**pg**、**more**、**head** 和 **tail** 的命令摘要。我列出了这些命令中最常用的一些选项。由于这些命令都不难使用，我建议尝试每个命令，看看哪个更适合你的需求。

![](img/75f39fc91296b889c0653851accdfd46_616_0.png)

![](img/75f39fc91296b889c0653851accdfd46_616_1.png)

以下是 **cat**、**pg**、**more**、**head** 和 **tail** 命令的摘要。

![](img/75f39fc91296b889c0653851accdfd46_616_2.png)

**cat** - 显示、合并、追加、复制或创建文件。

![](img/75f39fc91296b889c0653851accdfd46_616_3.png)

选项

- **-** 当你想用键盘作为标准输入时，作为指定文件名的替代。
- **-n** 显示行号与输出行一起显示。
- **-P** 将多个连续的空白行替换为一行空白。
- **-s** 这是静默模式，会抑制关于不存在文件的信息。
- **-u** 输出是非缓冲的，这意味着它是逐字符处理的。
- **-v** 可见地打印大部分不可打印字符。

**pg** - 显示文件或文件的部分。

选项

- **-number** 你希望显示的行数。
- **-p string** 使用字符串指定提示符。
- **-c** 在显示文件的下一页之前清除屏幕。

