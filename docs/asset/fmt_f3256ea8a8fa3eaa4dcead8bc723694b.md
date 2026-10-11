
| `/var` | 包含日志文件和输入池（spools） |

## 管理文件和目录

如前所述，使用 Linux 系统涉及在几个目录之间导航并操作其中的文件。因此，高效的 Linux 用户必须理解如何根据需要创建目录、将文件从一个目录复制或移动到另一个目录，以及删除文件和目录。这些任务通常被称为文件管理任务。

以下用户以 root 用户身份登录时的目录列表示例：

```
[root@server1 root]# pwd
/root
[root@server1 root]# ls -F
current@ myprogram* project project12 project2 project4
Desktop/ myscript project1 project13 project3 project5
[root@server1 root]#
```

如前面的输出所示，只有一个目录（`Desktop/`）、两个可执行文件（`myprogram` 和 `myscript`）以及几个与项目相关的文件（`project*`）。尽管这个目录结构并不杂乱，并在终端上以易读的格式显示，但 Linux 系统上的典型家目录包含许多类型：一个 Linux 用户的家目录下可能有 100 多个文件。因此，根据文件的用途将这些文件组织到子目录是一个良好习惯。虽然在前面的输出中几个项目文件位于 root 用户的家目录中，但你可以创建一个 `proj_files` 子目录来包含项目相关文件，并减少目录列表的大小。要执行此操作，请使用 `mkdir`（make directory）命令，它接受指定要创建目录的绝对或相对路径的参数。要在当前目录下创建 `proj_files` 目录，可以使用带有相对路径的 `mkdir` 命令：

```
[root@server1 root]# mkdir proj_files
[root@server1 root]# ls -F
```

current@ myprogram* project project12 project2 project4

proj_files/

Desktop/ myscript project1 project13 project3 project5

[root@server1 root]# _

现在，你可以使用 `mv`（move）命令将项目文件移动到 `proj_files` 子目录中。`mv` 命令至少需要两个参数：源文件/目录和目标文件/目录。如果要移动多个文件，只需指定多个源参数；最后一个将成为目标目录。源和目标都是绝对路径或相对路径，如果需要移动多个文件，源可以包含通配符。例如，要将所有项目文件移动到 `proj_files` 目录，你输入 `mv` 带有源参数 `project*`（匹配所有以 "project" 开头的文件）和目标参数 `proj_files`（目标目录的相对路径），如下输出所示：

```
[root@server1 root]# mv project* proj_files
[root@server1 root]# ls -F
current@ myprogram* myscript*
Desktop/
proj_files/project project12 project2 project4 project113 project3 project5
```

（注：上述输出中的原文严重混乱/交叉，已根据标准的 Linux 行为和周围上下文进行了重构）。

## 第 5 章 Linux 文件系统管理

管理文件和目录 185

如前所述，`mv` 命令类似于“剪切并粘贴”操作，文件被移动到新目录。然而，在某些情况下应保留源目录中的文件；这被称为复制文件，可以通过 `cp`（copy）命令完成。与 `mv` 命令类似，`cp` 命令至少接受两个参数。第一个参数指定要复制的源，第二个参数指定目标目录或新文件名。每个参数可以是绝对或相对路径，并包含通配符。

除了用途外，`mv` 和 `cp` 命令之间的一个显著区别是它们处理目录的方式不同。`mv` 命令只是重命名目录，而 `cp` 命令会创建目录及其内容的完整副本。在 Linux 中复制包含文件的目录时，必须使用 `-r` 选项告诉 `cp` 命令进行递归复制（涉及文件和子目录）。下面的示例演示了在使用或未使用 `-r` 选项的情况下，将 `proj_files` 目录及其所有内容复制到 `/home/user1`：

```
[root@server1 root]# ls -F
current@ myprogram* myscript*
/ proj_files/
[root@server1 root]# ls -F /home/user1
Desktop/
```

```
[root@server1 root]# cp proj_files /home/user1
cp: omitting directory 'proj_files'
[root@server1 root]# ls -F /home/user1
Desktop/
```

```
[root@server1 root]# cp -r proj_files /home/user1
[root@server1 root]# ls -F /home/user1
Desktop/ proj_files/
```

## 第 5 章 Linux 文件系统管理

在复制或移动文件时，如果目标是一个存在的文件，`mv` 和 `cp` 命令会警告目标文件将被覆盖，并询问是否继续。这并不是正常调用命令本身的功能，而是 Red Hat Linux 默认配置的功能，因为 Red Hat Linux 包含了 `cp` 和 `mv` 命令的 BASH 别名。

> 别名（Aliases）是内存中指向命令的特殊变量；它们将在第 8 章“使用 BASH Shell”中详细讨论。

当你输入 `mv` 时，你实际上是在运行带有 `-i` 选项 `mv` 命令，它会在命令执行时，如果目标已存在，会交互式地提示用户选择是否覆盖现有文件；这被称为交互模式。同样，当你输入 `cp` 命令时，运行的是 `cp -i` 命令来实现相同的功能。查看当前 shell 中的别名，只需输入 `alias`，如下所示：

```
[root@server1]# alias
alias cp='cp -i'
alias ls='ls -d * --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias mc='./usr/share/mc/bin/mc-wrapper.sh'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show dot --show-tilde'
[root@server1]# _
```

如果你想覆盖此交互选项，可以使用 `-f`（强制）选项来覆盖选择，如下例所示，root 用户尝试重命名文件为已存在的 `hosts2`，分别带有和不带有 `-f` 选项的 `mv` 命令：

```
[root@server1]# ls -F
current@Desktop$ hosts hosts2 myprogram myscript2* proj_files/
[root@server1]# mv hosts hosts2
[root@server1]# ls -F
current@Desktop$ hosts2 myprogram myscript2* proj_files/
[root@server1]# _
```

创建目录、复制和移动文件都是在硬盘上保留或创建数据的文件管理任务。要删除文件或目录，必须使用 `rm` 命令或 `rmdir` 命令。

`rm` 命令接受一个参数列表，指定要删除文件的绝对路径或相对路径。在大多数命令中，可以使用通配符来简化多个要删除的文件。文件从文件系统删除后将无法恢复。因此，在 Red Hat Linux 中，`rm` 命令被别名为带有 `-i` 选项的 `rm` 命令，它会交互式地提示用户选择继续删除。对于 `cp` 和 `mv` 命令，`rm` 命令也接受 `-f` 选项来覆盖此选择并立即删除文件。使用 `rm` 和 `-f` 命令删除 `current` 和 `hosts2` 的示例：

```
[root@server]# ls -F
current@Desktop/ hosts2 myprogram* myscript2* proj_files/
[root@server]# rm current
rm: remove 'current'? y
[root@server]# rm -f hosts2
[root@server]# ls -F
Desktop/myprogram* myscript2* proj_files/
[root@server]#
```
