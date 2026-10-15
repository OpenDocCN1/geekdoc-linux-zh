

一个 shell 命令可以是内部/内置的，也可以是外部的。执行内部命令的代码是 shell 进程的一部分，但处理外部命令的代码则驻留在文件系统中，以二进制可执行程序文件或 shell 脚本的形式存在。（我们在第 10 章详细描述了 shell 如何执行命令。）由于 shell 执行从键盘输入的命令，当它发现无法再从键盘读取任何内容时就会终止。你可以通过在新行的开头按下 <Ctrl+D> 来通知你的 shell。shell 一旦接收到 <Ctrl+D>，就会终止并将你注销系统。系统随后会再次显示 login: 提示符，告知你需要重新登录才能使用它。

shell 会解释符合第 2.2 节结构的单个 UNIX 命令——即假设命令行中的第一个词是你想要执行的命令的名称。它假设其余以连字符 (-) 开头的词是选项（可能后跟选项参数），其余的则是命令参数。

在读取你的命令行后，它会确定该命令是内部命令还是外部命令。它通过使用自身代码中的相应代码段来处理所有内部命令。要执行外部命令，它会在文件系统结构中搜索多个目录（参见第 4 章），查找具有该命令名称的文件。然后它假设该文件包含要执行的代码并运行该代码。

shell 搜索以查找对应外部命令的文件的目录名称存储在名为 PATH（或在 C shell 中为 path）的 shell 变量中。在 Bourne、Korn 和 Bash shell 中，目录名称由冒号分隔，而在 C shell 中则由空格分隔。存储在 PATH 变量中的目录名称构成了 shell 的搜索路径。你可以通过在 Bourne、Korn、Bash 和 C shell 中使用 echo $PATH 命令来查看你的变量的搜索路径。

以下是使用该命令在登录 shell 中运行的两个示例会话，首先是 Bourne shell，然后是 C shell。请注意，在 Bourne shell 中，搜索路径包含由冒号分隔的目录名称，而在 C shell 中，目录名称由空格分隔。

```
$ echo $PATH
/usr/sbin:/usr/X11/include/X11:../users/faculty/sarwar/bin:/usr/ucb
:/bin:/usr/bin:/usr/include:/usr/X11/lib:/usr/lib:/etc:/usr/etc:/usr
/local/bin:/usr/local/lib:/usr/local/games:/usr/X11/bin
$
```

```
% echo $path
/usr/sbin /usr/X11/include/X11 . /users/faculty/sarwar/bin /usr/ucb /bin
/usr/bin /usr/include /usr/X11/lib /usr/lib /etc /usr/etc /usr/local/bin /usr/local/lib /usr/local/games /usr/X11/bin
%
```

PATH（或 path）变量定义在名为 .profile（Solaris）或 .login（PC-BSD）的隐藏文件（也称为点文件）中。如果你在这些文件中找不到该变量，它就在你所使用的 shell 特有的启动文件（也是一个点文件）中。你可以通过更改该变量的值来更改 shell 的搜索路径。要仅临时更改当前会话的搜索路径，你可以在命令行更改 PATH 的值。要永久更改，你需要在相应的点文件中更改该变量的值。

在下面的 Bash shell 示例中，搜索路径通过两个目录 ~/bin 和 .（当前目录）进行了扩充。而且，搜索从 ~/bin 开始，以当前目录结束。

在编辑或更改 PATH 变量时要小心，以免丢失系统管理员为系统所有用户设置的默认搜索路径的任何组件。

```
$ PATH=~/bin:$PATH:.
$
```

你可以通过使用 echo $SHELL 命令来确定你的登录 shell，如第 2.8.3 节所述。每个 shell 在与其关联的隐藏文件中设置了多个其他环境变量。我们在第 2.8.4 节中描述了这些文件，并在第 4 章中对 UNIX 文件进行了详细讨论。

## 2.8 各种 UNIX Shell

每个 UNIX 系统都附带多种 shell，其中 Bash 和 C shell（我们基础系统 Solaris 和 PC-BSD 中的默认 shell）是最常见的。Bourne、Korn、TC 和 Z shell 较少流行，但在某些应用和与 UNIX 系统交互的方式中提供了优势。当你登录时，一种特定的 shell 类型开始执行。该 shell 被称为你的登录 shell，由你的 UNIX 系统的系统管理员确定。如果你想使用不同的 shell，你可以通过运行系统上可用的相应命令来实现。例如，如果你的登录 shell 是 Bash，但你想使用 C shell，你可以通过使用 csh 命令来实现。

### 2.8.1 Shell 程序

本质上，shell 程序本身是用 C 编程语言实现的，允许你进行解释性编程（与编译型编程相对）。它在两个意义上实现了这一点：首先，你可以使用简单的单个或复杂的多个 UNIX 命令，通过重定向运算符和/或 sed、awk 或 grep 等实用程序连接起来，来完成常见任务；其次，通过用户编写的脚本文件，这些文件以 shell 解释语言编写，可自动化并简化那些常见、也许高度重复的任务。这种解释语言具有 Perl、Tcl 或 Python 等任何其他结构化、高级编程语言的所有特性。shell 语言只是没有其他常见脚本语言那么复杂。这一事实应该告诉你为什么有这么多不同的 shell，就像有许多不同的高级编程和脚本语言一样。

