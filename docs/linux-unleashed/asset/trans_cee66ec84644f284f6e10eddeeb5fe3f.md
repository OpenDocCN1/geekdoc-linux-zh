

正如你一开始所见，**mv** 和 **cp** 是非常简单的命令。真正复杂的部分是指定文件！如果这些事情看起来仍然令人困惑，别担心。即使是专家有时也会搞砸“简单”的移动和复制操作。跟随示例，尝试任何你能想到的不同方法。关于如何指定要移动和复制的文件，有着明确的逻辑。熟悉这种逻辑需要一段时间，你可能需要练习一段时间，这些东西才会变得直观。

## 移动目录

要移动目录，请使用 **mv** 命令。语法是 **mv** _<directory>_<destination>_。在下面的示例中，让我们将当前目录中找到的 **newdir** 子目录移动到 _/tmp_ 目录：

```bash
darkstar:~$ mv newdir /tmp
darkstar:~$ cd /tmp
darkstar:/tmp$ ls
newdir
```

目录 **newdir** 现在是 _/tmp_ 的子目录。

当你移动目录时，它所有的文件和子目录都会随之移动。

你可以使用 **mv** 命令在不移动目录的情况下重命名目录。例如，如果你想将目录 **newdir** 重命名为 **olddir** 而不复制它，命令

```bash
mv newdir olddir
```

即可完成该任务。现在 **newdir** 中的所有文件都在 **olddir** 之下。

## 删除文件和目录

现在你已经知道如何创建文件和目录，是时候学习如何撤销你的操作了。

要删除（或移除）一个文件，请使用 **rm** 命令（**rm** 是 _remove_ 的非常简洁的拼写）。语法是 **rm** _<filename>_。例如，命令：

```bash
darkstar:~$ rm dead_duck
```

会从你的当前目录中删除文件 **dead_duck**。

```bash
darkstar:~$ rm /tmp/dead_duck
```

会从 _/tmp_ 目录中删除文件 **dead_duck**。

你可以使用通配符配合 **rm** 命令，就像在所有其他 Linux 命令中一样。如果你在不正确的位置输入该命令，这可能会给你带来很多麻烦。

例如，命令
`darkstar:~$ rm *`
会从你的当前目录中删除所有文件。没有撤销删除文件的方法，因此如果你意外输入了此命令，那就倒霉了。故事的寓意是，在使用 `rm` 命令配合通配符时要非常小心！

你可以将通配符和目录路径组合使用。例如，命令
`darkstar:~$ rm /tmp/*duck`
会从 /tmp 目录中删除所有以 **duck** 结尾的文件。

一旦文件被删除，它就*消失了！*在删除文件之前，务必考虑清楚你要做什么。你可以使用以下选项之一，以避免在使用通配符时遇到麻烦：

-   使用与 `rm` 命令相同的文件规范运行 `ls`。例如：
    ```text
    darkstar:~$ ls *duck
    dead_duck    guiduck    lame-duck
    :~$ rm *duck
    ```
    在这种情况下，*你* *认为*你想删除所有匹配 `*duck` 的文件。为了验证情况确实如此，列出了所有 `*duck` 文件（通配符在所有命令中工作方式相同）。列表看起来没问题，所以你继续删除了这些文件。

-   使用 `i`（交互）选项配合 `rm`：
    ```text
    darkstar:~$ rm -i *duck
    rm: remove 'dead_duck'? y
    rm: remove 'guiduck'? n
    rm: remove 'lame-duck'? y
    darkstar:~$
    ```
    当你使用 `rm -i` 时，命令会逐一遍历要删除的文件列表，提示你确认是否删除该文件。如果你输入 `y` 或 `Y`，`rm` 会删除该文件。如果你输入任何其他字符，`rm` 则不会删除它。使用这种交互模式的唯一缺点是，当要删除的文件列表很长时，它会非常繁琐。

## 删除目录

rm 命令主要作用于文件。如果你尝试用 rm 删除目录，会显示一条错误信息。通常用于删除（移除）目录的命令是 rmdir。语法是 rmdir <directory>。

在删除目录之前，它必须是空的（目录中不能包含任何文件或子目录）。否则，你会看到

```text
rmdir: <directory>: Directory not empty
```

这是你在 Linux 中能看到的接近安全特性的功能！

下面这个例子可能会让你困惑：

```bash
darkstar:/home$ ls
zippy/
darkstar:~/home$ ls zippy
core kazoo stuff
darkstar:~/home$ rm zippy/*
darkstar:~/home$ ls zippy
darkstar:~/home$ rmdir zippy
rmdir: zippy: Directory not empty
darkstar:~/home$
```

出现“Directory not empty”（目录非空）信息的原因是，以 . 开头的文件通常是特殊的系统文件，通常对用户隐藏。要列出以 . 开头的文件，你必须使用 `ls -a`。要删除这些文件，请使用 `rm .*`：

```bash
darkstar:~/home$ ls -a zippy
/ ... .bashrc .profile
darkstar:~/home$ rm zippy/*
rm: cannot remove '...' or '...'
darkstar:~/home$ ls -a zippy
/ ...
darkstar:~/home$ rmdir zippy
darkstar:~/home$ ls
darkstar:~/home$
```

在系统管理员角色中，你最常遇到这种情况。

有时你想要删除一个包含多层子目录的目录。逐一清空并删除所有子目录非常繁琐。Linux 提供了一种方法，可以轻而易举地一步删除目录及其包含的所有文件和子目录。这就是 rm 命令的 r（递归）选项。语法是 rm -r <directory>。目录及其所有内容将被移除。

> **警告**
>
> 只有在绝对必要时才使用 `rm -r`。借用一句老话：“这只是一个捷径，直到你犯错误为止。”例如，如果你以 root 身份登录，以下命令会删除硬盘上的所有文件，然后就是“你好，安装程序”的时候了（不要输入以下命令！）：
> `rm -r /`
>
> 相信与否，人们经常这样做。别加入这个俱乐部！

# 对压缩的恐惧：无压缩文件

大多数 Linux 文件都以压缩形式存储在安装 CD-ROM 上。这允许存储更多信息。如果你使用 DOS 或 Windows，你可能已经看到过将文件压缩到较大库中的实用工具。诸如 PKZIP 和 WINZIP 之类的实用工具在这些操作系统中非常流行。UNIX 几十年来一直使用相同类型的技术，只是使用了不同的名称和压缩技术。

安装 Linux 时，安装程序会解压缩许多传输到硬盘上的文件。但是，如果你仔细查看，你会发现压缩文件！

任何以 .gz 结尾的文件——例如，squashed.gz——都是压缩文件。要解压缩这种类型的文件，输入 `gunzip <file>`。对于这个示例，输入 `gunzip squashed.gz`。gunzip 程序会创建一个未压缩的文件，并移除 .gz 扩展名。因此，你最终会得到一个名为 squashed 的普通文件。要压缩文件，请使用 `gzip` 命令。输入 `gzip squashed` 会压缩 squashed 并将其重命名为 squashed.gz。

你可能看到的另一种压缩文件以扩展名 .zip 结尾。使用 `unzip` 来解压缩这些文件。要创建此类型的文件，请使用 `zip`。

Linux 还有另外两种压缩系统。这些系统提供以 .Z 或 .z 结尾的压缩文件（这两者不是由同一个压缩工具产生的）。

# Linux 文件系统中的重要目录

存放 Linux 系统文件的大多数目录都是“标准的”。其他 UNIX 系统会有相同的目录，内容相似。本节总结了你的 Linux 系统中一些更重要的目录。

## /

这是根目录。它包含实际的 Linux 程序，以及子目录。不要用你的文件弄乱这个目录！

## /home

这个目录存放用户的家庭目录。在其他 UNIX 系统中，这可能是 /usr 或 /u 目录。

## /bin

这个目录存放许多基本的 Linux 程序。bin 代表二进制文件（binaries），这些是可执行的、仅计算机能理解的文件，而不包含文本。

## /usr

这个目录存放许多面向用户的其他目录。下面几节描述了其中一些最重要的目录。/usr 中找到的其他目录包括：

-   **docs**：各种文档，包括有用的 Linux 信息
-   **man**：通过输入 `man <command>` 访问的手册页
-   **games**：有趣的东西！

## /usr/bin

这个目录存放面向用户的 Linux 程序。

## /usr/spool

这个目录有几个子目录。mail 存放邮件文件，spool 存放待打印的文件，uucp 存放 Linux 机器之间复制的文件。

![](img/e8e6b47ac20475e23d48b4c476f5d891_206_0.png)

