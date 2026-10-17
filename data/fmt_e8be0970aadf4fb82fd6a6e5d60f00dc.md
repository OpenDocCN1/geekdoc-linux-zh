
Chaining two or more commands together is what gives the shell its real power. Hundreds of commands are available and, by combining them in different ways, you get hundreds of new commands. Some of the shell commands are available through the GUI, but these commands usually have only a small subset of their parameters available, which limits what you are able to do with them.

Working from a text-only system encapsulates both working locally with a broken GUI and also connecting to a remote, text-only system. If your Linux server is experiencing problems, the last thing you want to do is load it down with a GUI connection—working in text mode is faster and more efficient.

The last use is the most common: People use the shell just because it is familiar to them, with many people even using the shell to start GUI applications just because it saves them taking their hands off the keyboard for a moment! This is not a bad thing; it provides fluency and ease with the system and is a perfectly valid way of working.

## Basic Commands

It is impossible to know how many commands the average shell citizen uses, but if we had to guess, we would place it at about 25:

- `cat`—Prints the contents of a file
- `cd`—Changes directories
- `chmod`—Changes file access permissions
- `cp`—Copies files
- `du`—Prints disk usage
- `emacs`—Text editor
- `find`—Finds files by searching
- `gcc`—The C/C++/Fortran compiler
- `grep`—Searches for a string in input
- `less`—Filter for paging through output
- `ln`—Creates links between files
- `locate`—Finds files from an index
- `ls`—Lists files in the current directory
- `make`—Compiles and installs programs
- `man`—The manual page reader
- `mkdir`—Makes directories
- `mv`—Moves files
- `ps`—Lists processes
- `rm`—Deletes files and directories
- `ssh`—Connects to other machines
- `tail`—Prints the last lines of a file
- `top`—Prints resource usage
- `vim`—A text editor
- `which`—Prints the location of a command

## `xargs`—从输入执行命令

当然，还有许多其他命令可供你使用，且使用频率相当高——`diff`、`nmap`、`ping`、`su`、`uptime`、`who` 等等——但如果你能理解下面列出的 25 个命令，你将具备足够的技能来组合自己的命令。

请注意，我们说的是理解这些命令——而不是知道它们所有可能的參數和用法。这是因为其中一些命令虽然常用，但只有有特定需求的人才会以复杂的方式使用它们。`gcc` 和 `make` 就是很好的例子：除非你打算成为一名程序员，否则你无需担心它们，只需偶尔输入 `make` 和 `make install` 即可。如果你想了解更多关于这两种工具的信息，请参阅第 26 章，“Ubuntu 的 C/C++ 编程工具”。

同样，`Emacs` 和 `Vim` 都是具有各自文本界面的文本编辑器，而 `SSH` 已在第 15 章“使用 SSH 和 Telnet 进行远程访问”中详细介绍过。

剩下的就是 20 个命令，每个命令都有许多参数来自定义其实际功能。同样，我们可以排除其中大部分，因为许多参数晦涩且很少使用，而在你 Linux 使用生涯中需要它们的少数几次，你只需阅读手册页即可！

我们将逐一介绍这些命令，解释最常用的使用方式。这里有一个例外：`xargs` 命令要求你理解如何将命令连接起来。

## 使用 `cat` 打印文件内容

Ubuntu 的许多 shell 命令都会操作文本字符串，因此如果你想将文件内容提供给它们，就需要能够将文件作为文本输出。此时 `cat` 命令就派上用场了，它会打印你传递给它的任何文件的内容。

其最基本的使用方式如下：

```
cat myfile.txt
```

这会打印 `myfile.txt` 的内容。对于这种用法，经常使用的两个额外参数是：`-n` 对输出进行行号编号，`-s`（“squeeze”）每次最多打印一行空白行。也就是说，如果你的文件有 1 行文本、10 行空白、1 行文本、10 行空白，依此类推，`-s` 会显示第一行文本、一个空白行、下一行文本、一个空白行，等等。当你同时使用 `-s` 和 `-n` 时，`cat` 只对打印的行进行编号——显示为一行的 10 个空白行在编号时计为 1 行。

此命令会打印有关 CPU 的信息，同时去除多余的空白行并对输出进行编号：

```
cat -sn /proc/cpuinfo
```

你也可以一次打印多个文件的内容，如下所示：

```
cat -s myfile.txt myotherfile.txt
```

在此命令中，`cat` 将 `myfile.txt` 和 `myotherfile.txt` 合并到输出中，并去除多余的空白行。重要的是，`cat` 在输出中不会区分文件——不会打印文件名，也不会在两者之间添加额外的分隔。 这允许你将 2 个文件视为 1 个，或通过在命令行中添加更多文件，将 20 个文件视为 1 个。

## 使用 `cd` 更改目录

更改目录肯定是没有选项的，对吧？并非如此。`cd` 实际上比大多数人想象的更灵活。与大多数其他命令动词不同，`cd` 本身并不是一个命令——它内置于 `bash`（或你使用的任何 shell 解释器）中，但仍像命令一样使用。

`cd` 最基本的使用方式如下：

```
cd somedir
```

这会在当前目录中查找 `somedir` 子目录，然后进入其中。你也可以指定目录的确切位置，如下所示：

```
cd /home/paul/stuff/somedir
```

`cd` 的第一个魔力在于字符（`-` 和 `~`，即连字符和波浪号）。前者表示“切换到我的上一个目录”，后者表示“切换到我的主目录”。下面与 `cd` 的对话展示了这一点：

```
[paul@caitlin ~]$ cd /usr/local
[paul@caitlin local]$ cd bin
[paul@caitlin bin]$ cd -
/usr/local
[paul@caitlin local]$ cd ~
[paul@caitlin ~]$
```

在第一行，我们切换到 `/usr/local`，命令没有输出。在第二行，我们切换到 `bin`，它是 `/usr/local` 的子目录。接下来，使用 `cd -` 切换回上一个目录。这次 Bash 会打印上一个目录的名称，以便我们知道自己在哪里。最后，使用 `cd -` 切换回主目录，虽然如果你想节省几个按键，只需单独输入 `cd` 就等同于 `cd ~`。
