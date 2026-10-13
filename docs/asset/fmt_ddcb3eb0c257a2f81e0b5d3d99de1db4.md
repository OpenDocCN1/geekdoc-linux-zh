
```
# tree temp5
```

```
temp5
`-- parent
    `-- child

2 directories, 0 files
```

如你所见，`mkdir` 不仅创建了 `temp5` 目录，还创建了名为 `parent` 的子目录，以及 `parent` 下名为 `child` 的子目录。

现在你知道了如何创建目录，让我们看看如何删除它们。

## 使用 rmdir 命令删除目录

`rmdir` 命令用于删除目录。要删除目录，只需输入以下内容：

```
# rmdir tempdirectory
```

但有一个前提：目录必须先为空！如果你尝试删除包含任何文件的目录，会收到如下错误信息：

```
# rmdir temp5
```

```
rmdir: temp5: Directory not empty
```

`rmdir` 命令与 `mkdir` 一样也有 `-p` 选项。你可以使用此选项删除目录层次结构，如下所示：

```
# rmdir -p temp5
rmdir: temp5: Directory not empty
```

嗯……这不起作用！那试试下面的：

```
# rmdir -p temp5/parent
rmdir: temp5/parent: Directory not empty
```

嘿！这也不起作用。现在试试这个：

```
# rmdir -p temp5/*
rmdir: temp5/parent: Directory not empty
```

这越来越令人沮丧了！再试一次：

```
# rmdir -p temp5/parent/child
```

最后！如你所见，必须指定完整的目录树才能删除它。如果使用不带 `-p` 选项的相同命令行，只会删除 `child` 目录。但如果有两个或多个子目录怎么办，如以下示例所示：

```
# mkdir -p temp5/parent/child
# mkdir temp5/parent/child2
# tree temp5
temp5
|-- parent
|   |-- child
|   `-- child2
3 directories, 0 files
```

为了删除 `temp5` 的整个目录系统，你需要使用以下命令：

```
# rmdir temp5/parent/*
```

现在你知道了如何创建和删除目录。接下来，你将学习 `mv` 命令，可用于移动或重命名文件和目录。

## 使用 mv 命令重命名文件

`mv` 命令被称为重命名命令，确实可以重命名文件或目录——但对许多人来说，它也是一种移动命令，可在文件系统中移动文件或目录。

实际上，从技术角度来说，文件或目录并没有真正被移动。如果你坚持要了解所有细节，请阅读 Linux 系统管理员指南，或 SAG，可通过以下网站获取：

http://metalab.unc.edu/LDP/LDP/sag/index.html

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_120_0.png)

不想在线阅读 SAG？你可能在 OpenLinux 系统上已安装了副本。尝试使用以下方式使用 `lynx` 纯文本网页浏览器：

`lynx /usr/doc/LDP/system-admin-guide/sag-0.6-html/sag.html`

有关使用 `lynx` 浏览器的更多信息，请参阅第 13 小时，“Internet 下载和浏览”。

在最简单的形式中，`mv` 可以重命名文件，例如：

```
# touch file1
# mv file1 file2
```

该命令将 `file1` 重命名为 `file2`。除重命名文件外，`mv` 还可以重命名目录，无论它们是否为空。例如，即使你使用 `mkdir` 命令创建了目录结构，也可以使用 `mv` 命令重命名新的顶级目录，如下所示：

```
# mkdir -p temp/temp2/temp3
# mv temp newtemp
```

虽然 `mv` 有九个不同的选项，本节重点介绍其中最常用的两个：`-b`（备份）和 `-i`（交互）。这些选项使你能够以相对安全的方式使用 `mv`——`mv` 不仅重命名，还会快速且静默地覆盖（不会询问！）第一个选项 `-b` 会为重命名为已存在名称的任何文件或目录创建备份，例如：

```
# touch uno deux tres
# ls uno deux tres
deux tres uno
# mv uno deux
# ls uno deux tres
ls: uno: No such file or directory
deux tres
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_120_1.png)

如你所见，如果不使用 `-b`，`mv` 不仅将文件 `uno` 重命名为 `deux`，而且在过程中删除了文件 `deux`。这危险吗？当然危险！现在，试试 `-b` 选项：

```
# touch uno
# ls uno deux tres
deux tres uno
# mv -b uno deux
# ls deux* tres
deux deux~ tres
```

此示例显示，虽然文件 `uno` 被重命名并替换了文件 `deux`，但会创建 `deux` 的备份，默认扩展名为波浪号（~）。

`mv` 命令可以静默工作，或者像 `rm` 一样，你可以使用 `-i` 选项，例如：

```
# touch file2 file3
# mv file2 file3
# touch file2
# mv -i file2 file3
mv: replace `file3'? y
```

这里，我创建了两个文件，然后将文件 `file2` 重命名为 `file3`，从而删除了原始的 `file3`。然而，我随后使用了 `-i` 选项，`mv` 命令会询问是否要覆盖文件。如果没有发生覆盖，即使使用 `-i`，`mv` 命令也不会请求许可。你也可以按如下方式组合 `-b` 和 `-i` 选项：

```
# mv -bi file2 file3
```

现在你知道了如何删除、重命名或移动文件，那么如何复制文件呢？

## 使用 cp 命令复制

`cp`，或复制，命令用于复制文件或目录。该命令近有 40 个命令行选项。这里并未全部介绍，但你将学习一些最常用的选项，可节省时间和麻烦。

你最有可能首先以最简单的形式使用 `cp`，例如：

```
# cp file1 file2
```

这会复制 `file1` 以创建 `file2`，并且与 `mv` 不同，`file1` 会保留原地。但使用 `cp` 时必须小心，因为你可以将文件复制到第二个文件上，从而有效地替换它！在这方面，`cp` 的行为可能像 `mv`。为了展示这种情况如何发生，请尝试使用 `cat` 命令创建三个文件，每个文件包含一行文本：

```
# cat > file1
this is file1
# cat > file2
this is file2
# cat > file3
this is the third file
# ls -l file*
-rw-r--r-- 1 bball users 14 Jan 5 13:29 file1
-rw-r--r-- 1 bball users 15 Jan 5 13:29 file2
-rw-r--r-- 1 bball users 23 Jan 5 13:29 file3
```

现在，将一个文件复制到另一个文件上，然后检查文件大小和新文件的内容，如下所示：

```
# cp file1 file2
# ls -l file*
-rw-r--r-- 1 bball users 14 Jan 5 13:29 file1
-rw-r--r-- 1 bball users 14 Jan 5 13:31 file2
-rw-r--r-- 1 bball users 23 Jan 5 13:29 file3
# cat file2
this is file1
```

显而易见，`file1` 会替换 `file2`。为了避免这个问题（除非你真的想覆盖文件），你可以使用 `-b` 或 `-i` 选项，其作用类似于 `mv`。下面是一个示例：

```
# cp -i file1 file2
cp: overwrite 'file2'? n
# cp -bi file1 file2
cp: overwrite 'file2'? y
# ls file*
file1 file2 file2- file3
```

请注意，被覆盖的 `file2` 已被备份。

`cp` 命令也可以一次复制多个文件。以下示例展示了如何将 `tempdir1` 目录中的所有文件复制到 `tempdir2` 目录：

```
# cp tempdir1/* tempdir2
# tree tempdir2
tempdir2
|-- tempfile1
|-- tempfile2
|-- tempfile3

0 directories, 3 files
```

与 `rm` 命令类似，`cp` 也有 `-r` 或递归选项。你可以使用此选项将一个目录复制到另一个目录中。例如，要将 `tempdir1` 目录及其文件复制到 `tempdir2` 中，使用以下语法：
