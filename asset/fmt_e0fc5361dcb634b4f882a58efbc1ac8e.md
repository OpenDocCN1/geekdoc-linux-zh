
你创建了一个名为 `emptyfiles` 的目录（`ls` 将其显示为蓝色，表示这是一个目录），你可以将 `empty.txt` 移动到其中。Linux 文件可以使用 `mv` 命令进行移动，该命令接受要移动的文件名并将目标路径作为最后一个参数。完成后，你可以使用以下命令验证 `mv` 的效果：

```
[@workstation20 you]$ mv empty.txt emptyfiles
[@workstation20 you]$ ls
emptyfiles notfull.txt
[@workstation20 you]$ ls emptyfiles
empty.txt
[@workstation20 you]$ 
```

注意，你刚刚输入的命令中的路径没有以斜杠字符开头。这是因为这些命令给出的是相对路径，我们将在下一节中讨论。

## 使用相对路径

在你刚刚输入的一系列命令中，你只给 `ls` 传递了一个目录名 `emptyfiles` 作为参数，而不是带有斜杠的完整路径。一个没有返回根目录“路线地图”的目录就是相对路径，因此它不以根目录 `/` 开头，而是该参数相对于你当前的工作目录。Linux 足够聪明，注意到你提供给 `ls` 的路径不是从根目录开始的；因此，它会将你提供的路径添加到你的当前工作目录 `/home/you`（当前工作目录）加上 `emptyfiles`（提供给 `ls` 的参数），导致 `/home/you/emptyfiles` 的内容出现在控制台上，从而省去了你手动输入长路径的麻烦。

为了更多练习相对路径，请尝试再创建一个目录。这次将其命名为 `deeperfiles`。通过在之前创建的目录 `emptyfiles` 内部创建它，从而将其放置在主目录下“更深”的位置。记住，你当前的工作目录仍然是主目录；你可以使用 `pwd` 来验证这一点：

## 在控制台导航 Linux

```
[you@workstation20]$ pwd
/home/you
[you@workstation20]$ mkdir emptyfiles/deeperfiles
[you@workstation20]$ ls
emptyfiles notfull.txt
[you@workstation20]$ ls emptyfiles
deeperfiles empty.txt
[you@workstation20]$
```

现在，为了练习，将文件 `notfull.txt` 移动到 `deeperfiles` 目录：

```
[you@workstation20]$ mv notfull.txt emptyfiles/deeperfiles
[you@workstation20]$ ls
emptyfiles
[you@workstation20]$ ls emptyfiles
deeperfiles empty.txt
[you@workstation20]$ ls emptyfiles/deeperfiles
notfull.txt
[you@workstation20]$
```

> 如果你想查看最后几个命令的输出，可以通过按住 Shift 键并按下 Page Up 或 Page Down 在虚拟控制台中向上或向下滚动。

如果这些相对路径让你感到有些困惑，请学习图 4.4。该图显示了 Linux 文件系统树的图，包含了你的主目录以及你在主目录内创建的所有文件和目录。

图 4.4

文件系统树的一部分，显示了主目录的当前状态以及到目前为止的所有文件和目录。

![](img/92a94ba94656919835b7a50a27c9d9ba_111_0.png)

在结束相对路径之前，你应该熟悉两个特殊的相对路径。它们是单点 `.` 和双点 `..`，它们都可以用于任何你通常使用目录名的地方。

单点 `.` 始终指向当前工作目录。因此，假设你的工作目录是 `/home/you`，以下三个命令将产生相同的结果：

```
[you@workstation20]$ ls
emptyfiles
[you@workstation20]$ ls /home/you
emptyfiles
[you@workstation20]$ ls .
emptyfiles
```

双点 `..` 指向相对于当前工作目录的文件树中较低的目录分支。因此，假设你的当前目录是 `/home/you`，以下两个命令将产生相同的结果：

```
[you@workstation20]$ ls /home
you
[you@workstation20]$ ls ..
you
[you@workstation20]$
```

你也可以使用相对路径通过 `cd` 修改你的当前工作目录：

```
[you@workstation20]$ cd .
[you@workstation20]$ pwd home]
/
[you@workstation20]$ home]
```

由于根目录位于文件系统树的最底部，且 Linux 文件系统中没有“更低”的目录，在根目录下，单点和双点是等效的：

```
[you@workstation20 home]$ cd ..
[you@workstation20]$ pwd ..
/
```

```
@workstation20 $ ls lib
bin/ dev home lib misc opt root tmp var
bot etc initrd lost+found mnt proc sbin usr
[you@workstation20]$ ls opt
dev dev home lib misc opt root tmp var
etc initrd lost+found mnt proc sbin usr
[you@workstation20]$ ls ..
dev dev home lib misc opt root tmp var
initrd lost+found mnt proc sbin usr
[you@workstation20]$
```

在控制台导航

记住你可以通过不带参数的 `cd` 命令快速返回主目录：

```
[you@workstation20 |]$ cd
[you@workstation20 |]$ pwd
/home/you
[you@workstation20 |]$
```

> 你经常会看到双点 (...) 被称为父目录。在 Linux 文件系统中，一个文件的父目录是包含它的目录。例如，`/home` 是 `/home/you` 的父目录。你还会看到子目录这个术语。在这个例子中，`/home/you` 是 `/home` 的子目录。

尽管你不总是理解特殊的相对路径如何有用，例如你可以将 `empty.txt`、`notfull.txt` 和 `deeperfiles` 移回：

```
[you@workstation20 |]$ mv emptyfiles/empty.txt emptyfiles/notfull.txt emptyfiles/deeperfiles
[you@workstation20 |]$ ls
deeperfiles notfull.txt
[you@workstation20]$
```

> 如果这些相对路径让你感到有些困惑，请学习图 4.4。该图显示了 Linux 文件系统树的图，包含了你的主目录以及你在主目录内创建的所有文件和目录。

图 4.4

文件系统树的一部分，显示了主目录的当前状态以及到目前为止的所有文件和目录。

![](img/92a94ba94656919835b7a50a27c9d9ba_0.png)

在结束相对路径之前，你应该熟悉两个特殊的相对路径。它们是单点 `.` 和双点 `..`，两者都可以用于任何你通常使用目录名的地方。

单点 `.` 始终指向当前工作目录。因此，假设你的工作目录是 `/home/you`，以下三个命令将产生相同的结果：

```
[you@workstation20]$ ls
emptyfiles
[you@workstation20]$ ls /home/you
emptyfiles
[you@workstation20]$ ls .
emptyfiles
```

双点 `..` 指向相对于当前工作目录的文件树中较低的目录分支。因此，假设你的当前目录是 `/home/you`，以下两个命令将产生相同的结果：

```
[you@workstation20]$ ls /home
you
[you@workstation20]$ ls ..
you
[you@workstation20]$
```

你也可以使用相对路径通过 `cd` 修改你的当前工作目录：

```
[you@workstation20]$ cd .
[you@workstation20]$ pwd home]
/
[you@workstation20]$ home]
```

由于根目录位于文件系统树的最底部，且 Linux 文件系统中没有“更低”的目录，在根目录下，单点和双点是等效的：

```
[you@workstation20 home]$ cd ..
[you@workstation20]$ pwd ..
/
```
