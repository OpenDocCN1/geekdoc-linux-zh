
第一行是提示符和我们输入的 `history` 命令。随后的行是历史列表的内容。下面的对话显示了历史列表中的最后三个条目（最新的在最后）：

```
$ history 3
9 slickedit fill.java
10 java fill.java
11 history
```

你可能已经注意到命令行显示的条目与历史列表输出之间存在细微差异。历史列表中的每个条目都有一个关联的行号。你可以使用关联的行号来回溯命令：下面的对话演示了如何执行 `make package` 命令：

```
$ 16
16 $ make package
```

与其他 shell 不同，`bash` 提供了对命令行字符串强大的编辑功能。你可以使用 `vi` 和 `Emacs` 的许多编辑功能。详情请参阅 `bash` 文档。

你还可以使用 `history` 命令一次查看完整的历史记录。如果历史条目的数量超过屏幕行数，历史列表将会滚动，你将无法看到某些条目。`history` 命令的语法如下：

```
history [#]
```

要验证变量是否存在，请使用 `set` 命令查看结果：

```
stimppy $ set
SHELL=/bin/bash
HOME=/home/stobler
LOGNAME=stobler
MAIL=/usr/mail/stobler
MAILCHECK=300
TZ=$ENVCDT
IFS=
PS2=
OPTIND=1
PS1=
REN=cat
```

那么，这个变量是环境局部的，还是全局的？我们没有导出该变量，所以它一定是局部的。我们可以使用 `env` 命令来验证，如下所示：

```
stimppy $ env
SHELL=/bin/bash
HOME=/home/stobler
LOGNAME=stobler
MAIL=/usr/mail/stobler
TZ=$ENVCDT
PS1=$
```

果然，`REN` 在这个 shell 中不存在，所以它必须是局部的。我们可以更改 `REN` 的值吗？当然！我们只需再次输入 `REN` 并设置新值，如下所示：

```
stimppy $ REN="a happy cat"
stimppy $
```

然后，让我们看看 `REN` 是否发生了变化。记住，我们必须使用 `set` 命令：

```
stimppy $ set
SHELL=/bin/bash
HOME=/home/stobler
LOGNAME=stobler
MAIL=/usr/mail/stobler
MAILCHECK=300
TZ=$ENVCDT
IFS=
PS2=
OPTIND=1
PS1=
RENa= happy cat
```

你也可以将环境变量的值设置为空字符串（无值）。该变量将继续存在，但没有关联任何值。下面的对话演示了这一点：

```
stimppy $ REN
stimppy $ set
SHELL=/bin/bash
HOME=/home/stobler
LOGNAME=stobler
MAIL=/usr/mail/stobler
MAILCHECK=300
TZ=$ENVCDT
IFS=
PS2=
OPTIND=1
PS1=
REN=
```

更改上列表中 `MAILCHECK` 的值允许你更改程序的行为。这个变量用于指定如何检查新邮件。这里显示的值是 own。如果我们想将邮件检查的值从 5 分钟增加到 10 分钟，可以如下操作：

```
stimppy $ MAILCHECK=600
stimppy $ set
SHELL=/bin/bash
HOME=/home/stobler
LOGNAME=stobler
MAIL=/usr/mail/stobler
MAILCHECK=600
TZ=$ENVCDT
IFS=
PS2=
OPTIND=1
PS1=
REN=$
```

我们可以从 `set` 的输出中看到该变量现在已设置为新值。

# Linux 内部

另一种打印环境变量内容的方法是使用 `echo` 命令。`echo` 命令用于将提供的参数打印到标准输出，并紧跟一个换行。如果你不提供参数，将输出一个换行。下面的对话显示了如何显示变量的值：

```
$ stimpy $ echo RENa happy cat
stimppy $ echo REN
REN
$ stimpy $
```

发生了什么？`echo` 命令按照我们指示的那样使用了：打印参数 `REN`。我们该如何打印 `REN` 的值呢？我们在变量名前面加上 `$` 字符。让我们试一次看看会发生什么：

```
$ stimpy $ echo REN
a happy cat
$ stimpy $
```

这里有一个问题需要回答：它们是如何使用的？我们见过一个例子，那是 `MAILCHECK` 环境。另一个例子是 `PAGER` 环境。这个变量由 `man` 命令使用。某些页面可能非常长，通常超过屏幕可以显示的的行数。`PAGER` 变量包含了 `man` 将显示页面的命令。你可以指定 `less` 命令作为参数。该命令允许你向上或向下滚动文本——不仅仅是显示到末尾。

我们讨论过环境变量可以是局部的也可以是导出的。要使用 `export` 命令，如面的对话所示：

```
$ stimpy RENa friend of Stimpy
stimppy $ export REN
SHELL=/bin/bash
HOME=/home/stober
LOGNAME=stober
MAIL=/usr/mail/stober
TZ=UTC-CDST
PS=8
RENA friend of Stimpy
```

如你所见，`REN` 现在是导出环境的一部分。该变量现在对会话下的所有进程都可用。或者，我们可以使用命令分隔符将两个独立的命令合并为一个。接下来的显示：

```
$ stimpya happy cat; export REN
stimppy $ env
SHELL=/bin/bash
HOME=/home/stober
LOGNAME=stober
MAIL=/usr/mail/stober
TZ=UTC-CDST
PS=8
RENA happy cat
```

使用命令分隔符时，务必仔细输入你的命令，否则可能会得到未定义的结果。

最重要的环境变量是 `PATH` 变量。当系统需要查找命令文件时就会使用 `PATH` 变量。该变量是一个由冒号分隔的目录路径列表。你的 `PATH` 变量可能设置如下：

```
$ stimpy $ echo PATH
/usr/bin:/usr/local/bin
$ stimpy $
```

如果你输入以下命令，Linux 会搜索 `PATH` 中的每个目录。如果第一项中没有找到命令，它将继续查找下一项，以此此类推。如果未找到命令，将显示错误消息。

# 使用文件和目录

在本节中，我们将定义 Linux 文件和目录。理解 Linux 系统是非常重要的，因为你所在的 Linux 涉及到文件系统。如果你来自 DOS 或 Windows，你看到的内容会很熟悉。这是因为 DOS、Windows 和文件系统诞生于 UNIX。Linux 使用文件系统来存储程序文件、用户邮件、系统文件和库文件等。它还使用文件系统处理专门的编程任务。

在安装过程中，目录结构被创建，所有所需的文件都被放置在正确的位置。安装完成后，由你来维护文件系统。

关于文件系统的一个重要点是在操作它之前要考虑两次。

## 理解文件和目录

在文件被存储之前，Linux 系统必须存在一个或多个目录。如果没有目录，文件将无法存在。

执行位是文件访问权限的一部分。每个文件都与多个权限位相关。权限分类分为用户、组和其他。对于每个类别，都必须设置权限位，包括读、写和执行。Linux 为每个文件维护了这些权限位，例如，如果你想执行一个文件，你必须拥有该文件的执行权限和读取权限。读标志位表示你可以以只读模式打开它。文件的写位表示你可以以写模式打开该文件。要创建一个文件，你必须对该目录具有写和执行权限。要删除一个文件，你必须对该目录具有写和执行权限。

特殊文件分为两个子类。第一类是块特殊设备，第二类是字符特殊设备。更准确地说，如果不是这样的话，所有的物理设备都与文件系统相关。你使用的键盘、你查看的控制台以及你使用的打印机都与 Linux 文件系统相关。这些特殊文件大多位于 `/dev` 中。
