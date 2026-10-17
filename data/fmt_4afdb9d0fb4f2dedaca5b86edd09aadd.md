
类似的想法，可以尝试 `sort` 程序。正如其名字，它是一个排序程序。如果你输入几行，然后按 `Ctrl-d`，它将按排序顺序输出这些行。这些类型的程序被称为过滤器（`filters`），因为它们接收文本，对其进行过滤，并以稍不同的方式输出文本。`cat` 和 `sort` 都是不寻过滤器，因为它们对文本没有进行任何更改。`sort` 是不寻，因为它按行读取，在看到 EOF 字符之前不输出任何内容。许多过滤器是按行运行的：它们读取一行，执行某些计算，并输出另一行。

## 4.2 自力更生

`man` 命令显示你指定的命令^4 的参考页。例如：

```
/home/larry# man cat
```

```
cat(1) cat(1)
NAME
cat - 合并或显示文件
SYNOPSIS
cat [--benstuvAET] [--number] [--nonblank] [--squeeze-blank]
[--show-newprinting] [--show-ends] [--show-tabs] [--show-all]
[help] [--version] [file...]
```

^2 `_` 表示用户使用了空格。

3 按住标记为 'Ctrl' 和 'd' 的键，然后松开两个。

4 `man` 还会显示系统调用、子程序、文件格式等信息。在 Unix 的原始版本中，它显示的是与打印文档完全一致的信息。现在，你可能只对获取命令的帮助感兴趣。

## 4.3 存储信息

描述

此手册页包含关于 `cat` 的完整信息。现在尝试运行 `man`。不要期望能理解 `man` 手页。页面通常假设你具备相当的 Unix 知识——你可能还没有这些知识。当你读完该页面后，屏幕底部可能会有一个小黑块，类似于 "--more--" 或 "Line 1"。这是 `more` 提示符，你会学会爱它的。

`man` 并没有让文本滚动消失，而是在每页结束处停止，等待你决定现在要做什么。如果你想继续，按空格键将翻到一页。如果你想退出 `quit` 手册页，只需按 `q`。你将回到 `shell` 提示符。

`man` 还有关键词功能。例如，如果你对处理 Postscript（Adobe 的打印控制语言）的任何命令感兴趣。输入 `-k ps` 或 `man -k Postscript`，你将获得包含 "Postscript" 字样的命令、系统调用和其他 Unix 文档部分的列表。

过滤器在你成为经验用户后非常有用，但它们有一个小问题。你如何存储信息？你并不被要求输入所有内容！Unix 提供了文件和目录。

每个文件和目录都有一个名字。它有一个短名，可以与其他文件或目录同名。一个文件的全名可能是 `joe`，而它的路径是 `home/larry/joe`。全名被称为路径（`path`）。路径可以解码为目录序列。例如，这里是 `/home/larry/joe`：

```
/home/larry/joe
```

初始斜杠表示根目录。

这表示名为 `home` 的目录。它在根目录内。

`joe` 在 `larry` 内。所以 `joe` 可能是两者。短名之前的所有项必须是目录。

最好的可视化方法是树。要查看典型的 Linux 系统，请看图 4.1。请注意，此图并不是完整的——完整的 Linux 系统有 8000 多个文件！而且只显示了标准目录。那里有很多你系统中不存在的目录，而你的系统肯定有未列出的目录。

### 4.3.1 使用 ls 查看目录

现在你知道文件和目录了，一定有一些操作它们的方法。确实有。`ls` 命令是最重要的命令之一。它列出文件。如果你尝试 `ls` 命令，你会看到：

```bash
/home/larry# ls
/home/larry#
```

目录的深度可能没有限制——人们可以轻松进入 10 层目录。

# 196

# 第 4 章. Unix Shell

没错，你什么也看不见。Unix 的设计刻意非常简洁：它什么都不给你，即使在没有文件时，它连“没有文件”都不会提示。因此，没有输出是 `ls` 表达它没有找到任何文件的方式。

但我刚刚说过可能有 8000 个或更多文件散落在各处；它们在哪里呢？你会遇到“当前”目录的概念。你可以在你的当前目录看到它，即 `/home/larry`，那里你没有任何文件。如果你想查看一个更活跃目录的文件列表，可以尝试根目录：

```
/home/larry# ls -
 install root user var
dev etc mint tmp
home lib proc usr vmlinux
/home/larry#
```

在上面的命令中，“`ls`”是命令，目录（“`./`”）是一个参数。命令的第一个词是命令（`command`），后面是参数（`parameter`）。参数通常修改程序的操作对象——`ls` 的参数指定了你想查看哪个目录的列表。某些命令具有特殊的参数，称为选项（`options`）或开关（`switches`）。查看如下：

```
/home/larry# ls -F /
root user var*
bin/ etc/ mint usr/
dev/ lib proc tmp/ vmlinux
home/#
```

`-F` 是一个选项。选项是一种特殊的参数，带有一个连字符，它修改的是程序运行的方式，而不是程序运行的对象。对于 `ls -F` 来说，这个选项让你看到哪些是目录、哪些是特殊文件、哪些是程序，以及哪些是普通文件。任何带有斜杠的都是目录。我们稍后会详细讨论 `ls` 的功能。它是一个惊地完整的程序！

现在，还有两点需要学习。首先，你应该学习 `ls` 的作用。尝试图 4.1 所示的目录以及它们包含的内容。自然地，有些是空的，有些会有很多文件。我建议你分别执行带 `-F` 和不带 `-F` 的 `ls`。例如，`ls /usr/local` Looks：

```
/home/larry# ls /usr/local
archives bin emacs etc ka9q lib tcl
/home/larry#
```

第二个是通用的。许多 Unix 命令都像 `ls` 一样。它们有选项（通常是连字符后跟一个字符），并且有参数。与 `ls` 不同，某些命令需要特定的参数和/或选项。要显示命令的通用格式，请使用以下：

## `ls [-aRF] [directory]`

我通常会使用 `ls2)` 遵循我从现在起介绍的任何命令的这种模板。第一个词是命令（在此处的 `ls2` 中）。后面是所有参数。可选参数包含在括号 `[ ]` 中。元变量是斜体的——它们是用来替换实际参数的单词。（例如，上面你看到了 `directory`，它应该被替换为目录的名字。）

选项是一个特殊情况。它们被括在括号中，但你可以选取其中任何一个，而不需要使用全部。例如，当 `ls` 提供了三个选项时，你有八种不同的运行命令方式：带上或不带这些选项。（对比 `ls -R` 和 `ls -F`。）

## 4.3.2 当前目录和 cd

```
pwd
```

如果你每次想访问目录都必须输入完整路径，那么使用目录将非常繁琐。相反，Unix 有一个叫做“当前”或“工作”目录的功能。你的设置可能在提示符中显示你的目录：`/home/larry`。如果没有显示，尝试命令 `pwd`，用于显示当前

## 4.3. 存储信息

目录.。（有时提示符会显示机器名称。这只在有许多不同机器的网络环境中才真正有用。）

```
mousehouse>pwd
/home/larry
mousehouse>
```

## `cd [directory]`

如你所见，`pwd` 告诉你你所在的目录——这是一个非常简单的命令。大多数命令默认在当前目录中执行。例如，不带任何参数的 `ls` 会显示当前目录的内容。我们可以使用 `cd` 改变当前目录。例如，尝试：

```
/home/larry# cd /home
/home# ls -F
larry/ sam/    shutdown/ steve/    user/
/home#
```

如果你省略了可选参数 `directory`，你将返回你的家目录（`home`）或原始目录。否则，`cd` 将切换到你指定的目录。例如：

```
/home# cd
/home/larry# cd /
# cd home
/home# cd /usr
/usr# cd local/bin
```

如你所见，`cd` 允许你提供绝对或相对路径。绝对路径以 `/` 开头，并指定目标目录之前的所有目录。相对路径存在于你的当前目录。在上面的示例中，当我在 `/usr` 时，我相对移动到了 `/local/bin`——`local` 是 `usr` 下的一个目录，而 `bin` 是目标目录之前的目录。（`cd home` 是一个相对目录切换。）

有两个目录专门用于相对路径：`.` 和 `..`。`.` 指当前目录，而 `..` 指父目录。这些存在于每个目录中的“快捷目录”，但并不填充“文件夹中的文件夹”的概念。根目录没有父目录——它自己自己的父目录。

文件 `./chapter-1` 就是当前目录下的 `chapter-1` 文件。偶尔，你需要加上 `./` 才能让某些命令工作，尽管这很少见。在大多数情况下，`./chapter-1` 和 `chapter-1` 是等价的。目录 `.` 在“备份”时最有用：

```
/usr/local/bin# cd ..
/usr/local# ls -F
archives/ bin/emacs@    etc/        ka9q/    lib/    tcl@
/usr/local# ls -F ../src
web/    linux/
/usr/
```

在这个示例中，我使用 `..` 切换了父目录，并在 `/usr/local` 使用 `..` 列出了 `usr/src`。注意，如果我在 `/home/larry`，输入 `ls -F ../src` 就没用了！目录 `~` 是你家目录的别名：

```
/usr/local# ls -F
```

> 你将使用书中所有的术语：工作目录、当前目录或家目录。我更倾向于使用“当前目录”，尽管为了风格目的会使用其他形式。

# 198

# 4. The Unix Shell

你可以一眼看出你的家目录里什么都没有！随着我们学习更多如何操作文件，`~/` 将变得越来越有用。

## 4.3.3 创建和删除目录

## `mkdir [directory...]`

在 Unix 下创建自己的目录极其简单，并且是一个非常有用的工具。创建一个新目录，使用 `mkdir` 命令。自然地，有些是空的，有些会有很多文件。我建议你分别执行带 `-F` 和不带 `-F` 的 `ls`。例如，`ls /usr/local` 如下：

```
/home/larry# ls /usr/local
archives bin emacs etc ka9q lib tcl
/home/larry#
```

`mkdir` 可以接受多个参数，其中每一个都是目录路径。你可以一次性用 `mkdir` 创建多个目录。尝试一下：

```
/home/larry# mkdir dir1 dir2 dir3
/home/larry# ls -F
dir1/ dir2/ dir3/
```

`mkdir` 还可以创建嵌套的目录。例如：

```
/home/larry# mkdir -p a/b/c
/home/larry# ls -F a
a/
```

我们稍后会详细讨论 `ls` 的功能。它是一个惊地完整的程序！

现在，还有两点需要学习。首先，你应该学习 `ls` 的作用。尝试图 4.1 所示的目录以及它们包含的内容。自然地，有些是空的，有些会有很多文件。我建议你分别执行带 `-F` 和不带 `-F` 的 `ls`。例如，`ls /usr/local` 如下：

```
/home/larry# ls /usr/local
archives bin emacs etc ka9q lib tcl
/home/larry#
```

`mkdir` 还可以接受多个参数，其中每一个都是目录路径。你可以一次性用 `mkdir` 创建多个目录。尝试一下：

```
/home/larry# mkdir dir1 dir2 dir3
/home/larry# ls -F
dir1/ dir2/ dir3/
```

`mkdir` 还可以创建嵌套的目录。例如：

```
/home/larry# mkdir -p a/b/c
/home/larry# ls -F a
a/
```

## 4.3.3 创建和删除目录

## 创建目录

在 Unix 下创建自己的目录极其简单，并且是一个非常有用的工具。创建一个新目录，使用 `mkdir` 命令。自然地，有些是空的，有些会有很多文件。我建议你分别执行带 `-F` 和不带 `-F` 的 `ls`。例如，`ls /usr/local` 如下：

```
/home/larry# ls /usr/local
archives bin emacs etc ka9q lib tcl
/home/larry#
```

`mkdir` 还可以接受多个参数，其中每一个都是目录路径。你可以一次性用 `mkdir` 创建多个目录。尝试一下：

```
/home/larry# mkdir dir1 dir2 dir3
/home/larry# ls -F
dir1/ dir2/ dir3/
```

`mkdir` 还可以创建嵌套的目录。例如：

```
/home/larry# mkdir -p a/b/c
/home/larry# ls -F a
a/
```

## 删除目录

## `rmdir [directory]`

删除一个空目录，使用 `rmdir` 命令。它只能删除空目录。如果目录不为空，它会报错。

```
/home/larry# mkdir test
/home/larry# rdir test
/home/larry#
```

如果要删除非空目录，需要使用 `rm` 命令配合 `-r` 参数。

```
/home/larry# mkdir test
/home/larry# touch test/file
/home/larry# rdir test
/home/larry# rdir: Directory not empty
/home/larry# rm -r test
/home/larry# ls -F
```

## 删除文件

## `rm [file...]`

删除文件，使用 `rm` 命令。它也可以删除一个或多个文件。

```
/home/larry# touch file1 file2
/home/larry# rm file1 file2
/home/larry# ls
```

注意：`rm` 命令是不可逆的，删除的文件将无法轻易恢复。请务必谨慎使用。

# 200

第 4 章. Unix Shell

```
/home/larry# ls -F
frog passwd passwd_version/
/home/larry# ls -F passwd_version
frog passwd
/home/larry#
```

我是如何使用 `cp` 的？显然，`cp` 可以接受两个以上的参数。（这是命令模板中的第二行。）上述命令的作用是复制了列出的所有文件（`frog` 和 `passwd`），并将它们放在 `passwd_version` 目录中。事实上，`cp` 可以接受任意数量的参数，并将前 $n-1$ 个参数解释为要复制的文件，将第 $n^{th}$ 个参数解释为复制的目标位置。

当你一次复制多个文件时，你无法重命名它们——它们始终保留原始的短名称。这引发了一个有趣的问题：如果我输入 `cp frog passwd toad`，而 `frog` 和 `passwd` 存在且 `toad` 不是一个目录呢？试试看。

## 4.4.2 使用 rm 剪枝

```
rm [-i] file1...fileN
```

现在我们已经学习了如何使用 `cp` 创建文件（相信我，你很快就会发现创建更多文件的新方法），实际上，这非常简单：你寻找的命令是 `rm`，它的工作方式正如你预期的那样：任何作为 `rm` 参数的文件都会被删除。

例如：

```
/home/larry# ls -F
frog passwd passwd_version/
/home/larry# rm frog toad passwd
rm: toad: No such file or directory
/home/larry# ls -F
passwd_version/
/home/larry#
```

如你所见，`rm` 非常不友好。它不仅会向你请求确认，而且即使命令行不正确，它也会删除东西。这实际上可能是危险的。考虑以下这两个命令之间的区别：

```
/home/larry# ls -F
toad frog/
/home/larry# ls -F frog
toad
/home/larry# rm frog toad
/home/larry#
```

以及这个

```
/home/larry# rm frog toad
rm: frog is a directory
/home/larry# ls -F
frog/
/home/larry#
```

如你所见，一个字符的差异导致了命令结果的巨大变化。在按下回车键之前，检查你的命令行至关重要！

![](img/e0ed64e774a11b944fd2651b5a09cd8c_202_0.png)

图 4.1 一个典型的（简化的）Unix 目录树。

![](img/e0ed64e774a11b944fd2651b5a09cd8c_203_0.png)

# 第 5 章

# X窗口系统

标准的良好之处在于有很多供你选择。

Andrew S. Tanenbaum

本章仅适用于那些使用 X窗口系统的人。如果你看到一个带有多个窗口、颜色或只能用鼠标移动的光标的屏幕，你正在使用 X。（如果你的屏幕是黑色背景上的白色字符，说明你目前没有使用 X。如果你想启动它，请查看第 5.1 节。）

## 5.1 启动和停止 X窗口系统

### 5.1.1 启动 X

即使 X 在你登录时没有自动启动，也可以从普通的文本模式 `shell` 提示符启动它。有两个可能的命令可以启动 X：`startx` 或 `xinit`。先尝试 `startx`。如果 `shell` 报错找不到该命令，请尝试 `xinit` 并查看 X 是否启动。如果两个命令都不起作用，说明你的系统中可能没有安装 X；请咨询你所在发行版的本地文档。
