
## 注意

当你说一个程序“退出”时，你是指它已经运行完毕，并且你回到了 Linux 命令提示符。从你作为用户的角度来看，似乎是“你”退出了程序，这样说起来可能有点奇怪。这种说法源于 UNIX 的早期，是由编写该系统的程序员们创造的。他们是从程序的角度来看待事情的，而不是从用户的角度！

那么，如何使用 **cat** 来创建一个文件呢？很简单！你只需将 **cat** 的输出从屏幕重定向到一个文件：

```
darkstar:~$ cat > newfile
Hello world
Here's some text
```

你可以输入任意多的内容。完成后，单独在一行按下 ^D；你就回到了 Linux 提示符。相反于在屏幕上逐行显示你输入的内容，**cat** 将它们重定向到了名为 **newfile** 的文件中。

现在你想查看 **newfile** 的内容。你可以使用 **more** 或 **less** 命令，但在这里，让我们使用 **cat**。是的，你可以通过提供一个文件名来使用 **cat** 查看文件：

```
darkstar:~$ cat newfile
Hello world
Here's some text
darkstar:~$
```

酷！你还可以使用 `>>` 在文件末尾追加内容。无论使用 **cat** 还是其他任何命令，只要使用 `>>`，输出总是*追加*到指定的文件中。（请注意，^D 字符不会在屏幕上显示。在示例中显示它只是为了清晰起见。）

```
darkstar:~$ cat >> newfile
Some more lines
^D
darkstar:~$ cat newfile
Hello world
Here's some text
Some more lines
darkstar:~$
```

要弄清楚 **cat** 究竟代表什么，让我们创建另一个文件。

```
darkstar:~$ cat > anotherfile
Different text
^D
darkstar:~$
```

现在，尝试一下这个：

```
darkstar:~$ cat newfile anotherfile > thirdfile
darkstar:~$ cat thirdfile
Hello world
Here's some text
Some more lines
Different text
darkstar:~$
```

**cat** 代表 concatenate（连接）：**cat** 接收所有指定的输入，并将它们作为一个整体重新输出。我们将 **newfile** 和 **anotherfile** 连接在一起形成了 **thirdfile**。单凭这一点可能没什么有趣的，但结合 Linux 中可用的各种输入和输出重定向形式，你就拥有了一个强大且实用的工具。

有时你想只修改文件中的一行，或者你正在创建一个庞大而复杂的文件，并不想依赖 **cat**（它不允许你更正错误）。为此，你应该使用 Linux 中可用的编辑程序之一。这些工具在第 16 章《文本编辑器：vi 和 emacs》中有所讨论。

## 创建目录

要创建新目录，请使用 **mkdir** 命令。语法为 `mkdir <name>`，其中 `<name>` 替换为你希望目录的名称。这会在当前目录下创建一个指定名称的子目录：

```
darkstar:~$ ls
anotherfile    newfile    thirdfile
darkstar:~$ mkdir newdir
darkstar:~$ ls
anotherfile    newdir     newfile    thirdfile
```

> **提示**
>
> 如果你使用过 MS-DOS 系统，那么**mkdir**命令对你来说已经很熟悉了。在 MS-DOS 中，你可以将**mkdir**简写为**md**。你可能会认为**md**在 Linux 中也能用，因为毕竟，我们见过的大多数命令名称都非常简洁。然而，Linux 并不识别**md**；它坚持使用完整的**mkdir**。
>
> 如果你经常在 Linux 和 MS-DOS 之间切换，你可能希望在两个系统中都使用**mkdir**。但请注意，你可能会开始将其他 Linux 命令输入到 MS-DOS 中——例如，输入**ls**而不是**dir**！

**mkdir** 命令会在 Linux 的所有文件和目录表（称为 I-node 表）中为该子目录创建一个条目。当 Linux 创建目录名称时，实际上并没有向磁盘驱动器写入任何内容，因为直到你向其中保存文件之前，目录名称没有物理内容。目录被 Linux 用作方便用户的一种机制。

你可以使用相对路径名和绝对路径名与 **mkdir** 一起使用，例如：

```
$ pwd
/usr/tparker/temp
$ ls
$ mkdir book1
$ ls
book1
$ mkdir /usr/tparker/temp/book2
$ ls
book1
book2
```

在第一种情况下，我们使用相对名称在当前目录下创建了一个名为 **book1** 的目录。在第二个示例中，我们使用绝对寻址在同一位置创建 **book2**。我们可以使用更方便的格式。两种方法都达到相同的结果。

## 移动和复制文件

你经常需要移动或复制文件。**mv** 命令用于移动文件（这与重命名相同），而 **cp** 命令用于复制文件。这两个命令的语法相似：

```
mv <source> <destination>
cp <source> <destination>
```

你可以看到，**mv** 和 **cp** 是非常简单的命令。这里有一个示例：

```
darkstar:~$ ls
anotherfile      newdir     newfile    thirdfile
darkstar:~$ mv anotherfile movedfile
darkstar:~$ ls
movedfile      newdir     newfile    thirdfile
darkstar:~$ cp thirdfile xyz
darkstar:~$ ls
movedfile      newdir     newfile    thirdfile    xyz
```

你可以随时使用 **cat**（或 **more** 或 **less**）来验证 **anotherfile** 是否变成了 **movedfile**，以及文件 **xyz** 的内容是否与 **thirdfile** 的内容相同。

如果你从一个目录移动或复制文件到另一个目录，情况可能会变得更令人困惑。这是因为文件的实际名称包括其绝对路径——例如，/home/fido/newfile。然而，Linux 允许你省略文件名称的一部分，因为引用 **newfile** 比 /home/fido/newfile 更方便。

例如，假设你想将 **newfile** 从当前目录移动到 **newdir** 子目录中。如果你希望文件保持相同的名称，你可以输入：

```
darkstar:~$ mv newfile newdir/newfile
```

然而，更常见的是输入：

```
darkstar:~$ mv newfile newdir
```

主要是因为这样更短一些。在这种情况下，由于你输入了目录名称作为目标，Linux 假设你想将文件放置到指定的目录中，并保持与现有文件相同的名称。

你还可以使用 **cd** 更改到你要移动文件的目录：

```
darkstar:~$ cd newdir
darkstar:~newdir$ cp ../newfile .
```

这个示例比前两个稍微不那么直观。你指定源为 `../newfile`，这意味着“当前目录的父目录中的文件 **newfile**”。目标简单地指定为 `.`，这是“当前目录”的简写。换句话说，你正在告诉 **mv** “向上提升一级，抓取 **newfile**，并将其移动到此处”。由于这不太直观，你可能会发现自己自动地将文件从当前目录推送到另一个目录，而不是将另一个目录中的文件拉取到当前目录。

你还可以通过指定所需的新名称，在移动或复制文件到另一个目录时更改文件的名称。以下只是可能的方法之一：

```
darkstar:~$ cp newfile newdir/anothername
```

这会在目录 **newdir** 中创建 **newfile** 的副本，并将复制的文件命名为 **anothername**。

![](img/e8e6b47ac20475e23d48b4c476f5d891_200_0.png)

## 警告

在目录之间移动或复制文件时，应始终仔细检查文件的目标目录是否存在，并验证目录的名称。否则，你的命令结果可能会出乎意料，如下面的两个例子所示。

在刚才展示的示例中，假设你将 `newdir` 错误输入为 `newdir`。那么，由于 `newdir` 是一个目录，`mv` 命令会将文件 `newfile` 移动到 `newdir` 中。然而，如果你输入了 `mv newfile m`，如果存在名为 `m` 的目录，它会将 `newfile` 移动到该目录中；如果不存在，它会创建一个名为 `m` 的文件，其中包含 `newfile` 的数据。

另一种获得意外结果的情况是，如果你没有意识到目录 `newdir` 已经存在，却输入了 `cp newfile newdir`。在这种情况下，你期望在当前目录中创建一个名为 `newdir` 的相同文件。但实际上，你正在子目录 `newdir` 中创建一个名为 `newfile` 的 `newfile` 副本。

`mv` 命令比 `cp` 命令效率高得多。当你使用 `mv` 时，文件的内容完全不会移动；相反，Linux 会做一个笔记，表明该文件现在位于文件系统目录结构中的其他位置。

当你使用 `cp` 时，你实际上是在制作文件的第二个物理副本并将其放置在磁盘上。这可能更慢（尽管对于小文件，你不会注意到任何差异），并且会对你的电脑造成更多的磨损。当你真正只想移动文件时，不要制作文件的副本！

## 使用通配符进行移动和复制

如果一个目录中有 20 个文件，并且你想将它们复制到另一个目录，逐个使用 `cp` 命令将非常繁琐。幸运的是，你可以使用通配符 `*` 和 `?` 一次复制多个文件。

如果你想移动或复制目录中的所有文件，请使用通配符 `*`：

```
darkstar:~$ cp * /tmp
```

此命令将当前目录中的每个文件复制到目录 `/tmp`。

你可以将 `*` 与其他字符一起使用，以仅匹配某些文件。例如，假设你有一个目录，其中包含文件 `book1`、`book_idea`、`book-chapter-1` 和 `poem.book`。要仅复制前三个文件，你可以输入 `cp book* /tmp`。当你输入 `book*` 时，你是在要求 Linux 匹配所有以 `book` 开头的文件。在这种情况下，`poem.book` 不以 `book` 开头，因此 `book*` 无法匹配它。（请注意，如果你的文件名是 `book.poem`，则 `book*` 会匹配它。）

